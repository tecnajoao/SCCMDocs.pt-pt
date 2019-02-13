---
title: Cluster do SQL Server
titleSuffix: Configuration Manager
description: Utilize um cluster do SQL Server para alojar a base de dados do site do System Center Configuration Manager. Inclui informações sobre as opções suportadas.
ms.date: 2/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d09a82c6-bbd1-49ca-8ffe-e3ce87b85d33
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f01367c76383454ded14390fc0583c874d32d60e
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56141743"
---
# <a name="use-a-sql-server-cluster-for-the-system-center-configuration-manager-site-database"></a>Utilizar um cluster do SQL Server para a base de dados do site do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


 Pode utilizar um cluster do SQL Server para alojar a base de dados do site do System Center Configuration Manager. A base de dados do site é a única função do sistema de sites suportada num cluster de Servidores.  

> [!IMPORTANT]  
>  Configuração concluída com êxito de clusters do SQL Server se baseia em documentação e procedimentos fornecidos na biblioteca de documentação do SQL Server.  

 Um cluster pode fornecer suporte de ativação pós-falha e melhorar a fiabilidade da base de dados do site. No entanto, não fornece processamento adicional nem benefícios de balanceamento de carga. Na verdade, degradação do desempenho pode ocorrer, porque o servidor do site tem de localizar o nó ativo do cluster do SQL Server antes de ligar à base de dados do site.  

 Antes de instalar o Configuration Manager, tem de preparar o cluster do SQL Server para suportar o Configuration Manager. (Consulte os pré-requisitos mais à frente nesta secção).  

 Durante a configuração do Configuration Manager, o escritor do serviço de cópia de sombra de volumes do Windows é instalado em cada nó de computador físico do cluster do Microsoft Windows Server. Isto suporta o **servidor do Site de cópia de segurança** tarefa de manutenção.  

 Após a instalação do site, o Configuration Manager verifica a existência de alterações para o nó de cluster por hora. O Configuration Manager gerencia automaticamente quaisquer alterações encontradas que afetem as instalações de componentes do Configuration Manager (como uma ativação pós-falha de nó ou a adição de um novo nó ao cluster do SQL Server).  

## <a name="supported-options-for-using-a-sql-server-failover-cluster"></a>Opções suportadas para utilizar um cluster de ativação pós-falha do SQL Server

As opções seguintes são suportadas para clusters de ativação pós-falha do SQL Server utilizados como a base de dados do site:

-   Um cluster de instância única  

-   Configuração de várias instâncias  

-   Vários nós ativos  

-   Uma determinada ou uma instância predefinida  

Tenha em atenção os seguintes pré-requisitos:  

-   A base de dados do site tem de ser remota em relação ao servidor do site. (O cluster não pode incluir o servidor do sistema de sites.)  

-   Tem de adicionar a conta de computador do servidor do site para o grupo de administradores locais de cada servidor no cluster.  

-   Para suportar a autenticação Kerberos, o **TCP/IP** protocolo de comunicação de rede tem de estar ativado para a ligação de rede de cada nó de cluster do SQL Server. O protocolo**Pipes nomeados** não é necessário, mas pode ser utilizado para resolver problemas de autenticação Kerberos. As definições de protocolo de rede são configuradas no **Gestor de configuração do SQL Server**, em **configuração de rede do SQL Server**.  

-   Se utilizar uma PKI, consulte requisitos de certificado PKI para o Configuration Manager para requisitos de certificado específicos quando utilizar um cluster do SQL Server para a base de dados do site.  

Considere as seguintes limitações:  

-   **Instalação e configuração:**  

    -   Os sites secundários não podem utilizar um cluster do SQL Server.  

    -   A opção para especificar localizações de ficheiros não predefinidas para a base de dados do site não se encontra disponível quando especificar um cluster do SQL Server.  

-   **Fornecedor de SMS:**  

    -   Não é suportada para instalar uma instância do fornecedor de SMS num cluster do SQL Server ou num computador que é executado como um nó em cluster do SQL Server.  

-   **Opções de replicação de dados:**  

    -   Se pretender utilizar **vistas distribuídas**, não é possível utilizar um cluster do SQL Server para alojar a base de dados do site.  

-   **Cópia de segurança e recuperação:**  

    -   O Configuration Manager não suporta a cópia de segurança do Data Protection Manager (DPM) para um cluster do SQL Server que utilize uma instância nomeada. No entanto, ele, suportam a cópia de segurança do DPM num cluster do SQL Server que utiliza a instância predefinida do SQL Server.  

## <a name="prepare-a-clustered-sql-server-instance-for-the-site-database"></a>Preparar uma instância do SQL Server em cluster para a base de dados do site  

Seguem-se as tarefas principais para concluir a fim de preparar a sua base de dados do site:

-   Crie o cluster virtual do SQL Server para alojar a base de dados do site num ambiente de cluster do Windows Server existente. Para obter passos específicos para instalar e configurar um cluster do SQL Server, consulte a documentação específica da sua versão do SQL Server. Por exemplo, se estiver a utilizar o SQL Server 2008 R2, consulte [instalando um Cluster de ativação pós-falha do SQL Server 2008 R2](http://go.microsoft.com/fwlink/p/?LinkId=240231).  

-   Em cada computador no cluster do SQL Server, pode colocar um ficheiro na pasta raiz de cada unidade onde não pretenda do Configuration Manager para instalar componentes do site. O arquivo deve ser nomeado **no_sms_on_drive**. Por predefinição, o Configuration Manager instala alguns componentes em cada nó físico, para suportar operações, tais como cópia de segurança.  

-   Adicione a conta de computador do servidor do site ao grupo **Administradores Locais** do computador de cada nó do cluster do Windows Server.  

-   Na instância virtual do SQL Server, atribua a **sysadmin** função do SQL Server para a conta de utilizador que irá executar a configuração do Configuration Manager.  

### <a name="to-install-a-new-site-using-a-clustered-sql-server"></a>Para instalar um novo site utilizando um SQL Server em cluster  
 Para instalar um site que utiliza uma base de dados do site em cluster, execute a configuração do Configuration Manager seguindo o processo normal para instalar um site, com a seguinte alteração:  

-   Na página **Informações da Base de Dados** , especifique o nome da instância virtual do cluster do SQL Server que irá alojar a base de dados do site. A instância virtual substitui o nome do computador que executa o SQL Server.  

    > [!IMPORTANT]  
    >  Quando introduzir o nome da instância virtual do cluster do SQL Server, não introduza o nome do Windows Server virtual criado pelo cluster do Windows Server. Se utilizar o nome virtual do Windows Server, a base de dados do site é instalado no disco rígido local do nó de cluster do Windows Server Active Directory. Isto impede a ativação pós-falha bem sucedida se esse nó falhar.  
