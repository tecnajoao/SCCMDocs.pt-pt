---
title: Cluster do SQL Server
titleSuffix: Configuration Manager
description: Utilizar um cluster do SQL Server para alojar a base de dados do site do Configuration Manager
ms.date: 03/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d09a82c6-bbd1-49ca-8ffe-e3ce87b85d33
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: cdbe1d7c3fb28a16c6ba55d073adba3781b12f58
ms.sourcegitcommit: 544f335cfd1bfd0a1d4973439780e9f5e9ee8bed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/07/2019
ms.locfileid: "57562062"
---
# <a name="use-a-sql-server-cluster-for-the-site-database"></a>Utilizar um cluster do SQL Server para a base de dados do site

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode utilizar um cluster do SQL Server para alojar a base de dados do site do Configuration Manager. Um cluster fornece suporte de ativação pós-falha e melhora a fiabilidade da base de dados do site. No entanto, ela não fornece processamento adicional ou balanceamento de carga benefícios. Pode ocorrer degradação do desempenho, porque o servidor do site tem de localizar o nó ativo do cluster do SQL Server antes de ligar à base de dados do site.  

> [!IMPORTANT]  
> Configuração concluída com êxito de clusters do SQL Server se baseia em documentação e procedimentos fornecidos na biblioteca de documentação do SQL Server.  


Antes de instalar o Configuration Manager, prepare o cluster do SQL Server para suportar o Configuration Manager. Para obter mais informações, consulte [preparar uma instância do SQL Server em cluster](#bkmk_prepare).

Durante a configuração do Configuration Manager, o escritor do serviço de cópia de sombra de volumes do Windows é instalado em cada nó de computador físico do cluster do Microsoft Windows Server. Este serviço suporta o **servidor do Site de cópia de segurança** tarefa de manutenção.  

Após a instalação do site, o Configuration Manager verifica a existência de alterações para o nó de cluster por hora. O Configuration Manager gerencia automaticamente quaisquer alterações que encontram-se que afetam suas instalações de componentes. Por exemplo, uma ativação pós-falha de nó ou a adição de um novo nó ao cluster do SQL Server.  



## <a name="supported-options"></a>Opções suportadas

As opções seguintes são suportadas para clusters de ativação pós-falha do SQL Server utilizados como a base de dados do site:

- Um cluster de instância única  

- Configurações de várias instâncias  

- Vários nós ativos  

- Uma determinada ou uma instância predefinida  



## <a name="prerequisites"></a>Pré-requisitos

Tenha em atenção os seguintes pré-requisitos:  

- A base de dados do site tem de ser remota em relação ao servidor do site. O cluster não pode incluir o servidor de sistema de sites.  

    > [!Note]  
    > A partir da versão 1810, o processo de configuração do Configuration Manager já não bloqueia a instalação da função de servidor de site num computador com a função do Windows para o Clustering de ativação pós-falha. Anteriormente não foi possível colocar a base de dados no servidor do site. Com esta alteração, pode criar um site de elevada disponibilidade com menos servidores através de um cluster SQL e um servidor de site em modo passivo. Para obter mais informações, consulte [opções de elevada disponibilidade](/sccm/core/servers/deploy/configure/high-availability-options). <!--3607761, fka 1359132-->  

- Adicione a conta de computador do servidor do site local **administradores** grupo de cada servidor no cluster.  

- Para suportar a autenticação Kerberos, ative o **TCP/IP** protocolo de comunicação para a ligação de rede de cada nó de cluster do SQL Server de rede. O **pipes nomeados** protocolo não é necessário, mas pode ser utilizado para resolver problemas de autenticação Kerberos. As definições de protocolo de rede são configuradas no **Gestor de configuração do SQL Server**, em **configuração de rede do SQL Server**.  

- Se utilizar uma infraestrutura de chaves públicas (PKI), consulte [requisitos de certificado PKI](/sccm/core/plan-design/network/pki-certificate-requirements). Existem requisitos de certificado específicos quando utilizar um cluster do SQL Server para a base de dados do site.  



## <a name="limitations"></a>Limitações

Considere as seguintes limitações:  


### <a name="installation-and-configuration"></a>Instalação e configuração

- Os sites secundários não é possível utilizar um cluster do SQL Server.  

- Quando especificar um cluster do SQL Server, a opção para especificar localizações de ficheiros não predefinidas para a base de dados do site não está disponível.  


### <a name="sms-provider"></a>Fornecedor de SMS

Não é possível instalar uma instância do fornecedor de SMS num cluster do SQL Server. Também não é suportada num computador que é executado como um nó em cluster do SQL Server.  


### <a name="data-replication-options"></a>Opções de replicação de dados

Se usar **vistas distribuídas**, não é possível utilizar um cluster do SQL Server para alojar a base de dados do site.  


### <a name="backup-and-recovery"></a>Cópia de segurança e recuperação

O Configuration Manager não suporta a cópia de segurança do Data Protection Manager (DPM) para um cluster de SQL Server que utiliza uma instância nomeada. Ele oferece suporte a cópia de segurança do DPM num cluster do SQL Server que utiliza a instância predefinida do SQL Server.  



## <a name="bkmk_prepare"></a> Preparar uma instância do SQL Server em cluster  

Aqui estão as principais tarefas para preparar a sua base de dados do site:

- Crie o cluster virtual do SQL Server para alojar a base de dados do site num ambiente de cluster do Windows Server existente. Para obter passos específicos para instalar e configurar um cluster do SQL Server, consulte a documentação específica da sua versão do SQL Server. Para obter mais informações, consulte [criar um novo Cluster de ativação pós-falha do SQL Server](https://docs.microsoft.com/sql/sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup?view=sql-server-2017).  

- Em cada computador no cluster do SQL Server, coloca um ficheiro na pasta raiz de cada unidade onde não pretende que o Configuration Manager para instalar componentes do site. Dê o nome `NO_SMS_ON_DRIVE.SMS` ao ficheiro. Por predefinição, o Configuration Manager instala alguns componentes em cada nó físico, para suportar operações, tais como cópia de segurança.  

- Adicione a conta de computador do servidor do site local **administradores** grupo de cada computador de nó de cluster do Windows Server.  

- Na instância virtual do SQL Server, atribua a **sysadmin** função do SQL Server para a conta de utilizador que executa a configuração do Configuration Manager.  


### <a name="to-install-a-new-site-using-a-clustered-sql-server"></a>Para instalar um novo site utilizando um SQL Server em cluster  

Para instalar um site que utiliza uma base de dados do site em cluster, execute a configuração do Configuration Manager seguindo o processo normal para instalar um site, com a seguinte alteração:  

- Na página **Informações da Base de Dados** , especifique o nome da instância virtual do cluster do SQL Server que irá alojar a base de dados do site. A instância virtual substitui o nome do computador que executa o SQL Server.  

    > [!IMPORTANT]  
    > Ao introduzir o nome da instância virtual do cluster do SQL Server, não introduza o nome do Windows Server virtual criado pelo cluster do Windows Server. Se utilizar o nome virtual do Windows Server, a base de dados do site é instalado no disco rígido local do nó de cluster do Windows Server Active Directory. Isto impede a ativação pós-falha bem sucedida se esse nó falhar.  
