---
title: Cluster do SQL Server | Documentos do Microsoft
description: "Utilize um cluster do SQL Server para alojar a base de dados do site do System Center Configuration Manager. Inclui informações sobre as opções suportadas."
ms.custom: na
ms.date: 2/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d09a82c6-bbd1-49ca-8ffe-e3ce87b85d33
caps.latest.revision: 10
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: ce0d7fc5f3d1812c4d62e551661c0ef89707567b
ms.openlocfilehash: 53f119bbb1f8827a9c23c8b747840350bbb92790
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="use-a-sql-server-cluster-for-the-system-center-configuration-manager-site-database"></a>Utilizar um cluster do SQL Server para a base de dados do site do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


 Pode utilizar um cluster do SQL Server para alojar a base de dados do site do System Center Configuration Manager. A base de dados do site é a única função do sistema de sites suportada num cluster de Servidores.  

> [!IMPORTANT]  
>  Configurar com êxito o de clusters do SQL Server baseia-se na documentação e procedimentos fornecidos na biblioteca de documentação do SQL Server.  

 Um cluster pode fornecer suporte de ativação pós-falha e melhorar a fiabilidade da base de dados do site. No entanto, este não forneça processamento adicional ou vantagens do balanceamento de carga. Na verdade, degradação do desempenho pode ocorrer, porque o servidor do site tem de localizar o nó ativo do cluster do SQL Server antes de ligar à base de dados do site.  

 Antes de instalar o Configuration Manager, tem de preparar o cluster do SQL Server para suportar o Configuration Manager. (Consulte as pré-requisitos posteriormente nesta secção.)  

 Durante a configuração do Configuration Manager, o escritor do serviço de cópia sombra de volumes do Windows Volume instala em cada nó de computador físico do cluster do Microsoft Windows Server. Isto suporta a **cópia de segurança do servidor do Site** tarefa de manutenção.  

 Após a instalação do site, do Configuration Manager verifica a existência de alterações no nó de cluster cada hora. O Configuration Manager gere automaticamente quaisquer alterações que encontram-se que afetam as instalações de componente do Configuration Manager (como uma ativação pós-falha de nó, ou a adição de um novo nó ao cluster do SQL Server).  

## <a name="supported-options-for-using-a-sql-server-failover-cluster"></a>Suportado opções para utilizar um cluster de ativação pós-falha do SQL Server

As opções seguintes são suportadas para clusters de ativação pós-falha do SQL Server utilizados como a base de dados do site:

-   Um cluster de instância única  

-   Configuração de várias instâncias  

-   Vários nós ativos  

-   Com um nome ou uma instância predefinida  

Tenha em atenção os seguintes pré-requisitos:  

-   A base de dados do site tem de ser remota em relação ao servidor do site. (O cluster não pode incluir o servidor do sistema de sites.)  

-   Tem de adicionar a conta de computador do servidor do site para o grupo Local de administradores de cada dos servidores no cluster.  

-   Para suportar a autenticação Kerberos, o **TCP/IP** protocolo de comunicação de rede tem de ser ativado para a ligação de rede de cada nó de cluster do SQL Server. O protocolo**Pipes nomeados** não é necessário, mas pode ser utilizado para resolver problemas de autenticação Kerberos. As definições do protocolo de rede são configuradas no **SQL Server Configuration Manager**, em **configuração de rede do SQL Server**.  

-   Se utilizar uma PKI, consulte os requisitos de certificados PKI para o Configuration Manager para obter os requisitos específicos do certificado quando utiliza um cluster do SQL Server para a base de dados do site.  

Considere as seguintes limitações:  

-   **Instalação e configuração:**  

    -   Os sites secundários não podem utilizar um cluster do SQL Server.  

    -   A opção para especificar localizações de ficheiros não predefinidas para a base de dados do site não se encontra disponível quando especificar um cluster do SQL Server.  

-   **Fornecedor de SMS:**  

    -   Não é suportada para instalar uma instância do fornecedor de SMS num cluster do SQL Server ou num computador que é executado como um nó em cluster do SQL Server.  

-   **Opções de replicação de dados:**  

    -   Se pretender utilizar **vistas distribuídas**, não é possível utilizar um cluster do SQL Server para alojar a base de dados do site.  

-   **Cópia de segurança e recuperação:**  

    -   O Configuration Manager não suporta a cópia de segurança do Data Protection Manager (DPM) para um cluster do SQL Server que utilize uma instância nomeada. No entanto,-, suporta a cópia de segurança do DPM num cluster do SQL Server que utilize a instância predefinida do SQL Server.  

## <a name="prepare-a-clustered-sql-server-instance-for-the-site-database"></a>Preparar uma instância do SQL Server em cluster para a base de dados do site  

Seguem-se as tarefas a concluir para preparar a base de dados do site principais:

-   Crie o cluster virtual do SQL Server para alojar a base de dados do site num ambiente de cluster do Windows Server existente. Para obter passos específicos instalar e configurar um cluster do SQL Server, consulte a documentação específica da sua versão do SQL Server. Por exemplo, se estiver a utilizar o SQL Server 2008 R2, consulte o artigo [instalar um Cluster de ativação pós-falha do SQL Server 2008 R2](http://go.microsoft.com/fwlink/p/?LinkId=240231).  

-   Em cada computador do cluster do SQL Server, pode colocar um ficheiro na pasta raiz de cada unidade em que não pretenda do Configuration Manager para instalar componentes do site. O ficheiro deve ser chamado **no_sms_on_drive**. Por predefinição, o Configuration Manager instala alguns componentes em cada nó físico para suportar operações, tais como a cópia de segurança.  

-   Adicione a conta de computador do servidor do site ao grupo **Administradores Locais** do computador de cada nó do cluster do Windows Server.  

-   Na instância virtual do SQL Server, atribua o **sysadmin** função do SQL Server para a conta de utilizador que vai ser executado a configuração do Configuration Manager.  

### <a name="to-install-a-new-site-using-a-clustered-sql-server"></a>Para instalar um novo site utilizando um SQL Server em cluster  
 Para instalar um site que utiliza uma base de dados do site em cluster, execute a configuração do Configuration Manager seguir o processo normal para a instalação de um site, com a seguinte alteração:  

-   Na página **Informações da Base de Dados** , especifique o nome da instância virtual do cluster do SQL Server que irá alojar a base de dados do site. A instância virtual substitui o nome do computador que executa o SQL Server.  

    > [!IMPORTANT]  
    >  Quando introduzir o nome da instância virtual do cluster do SQL Server, não introduza o nome do Windows Server virtual criado pelo cluster do Windows Server. Se utilizar o nome virtual do Windows Server, a base de dados do site instala no disco rígido local do nó do cluster do Windows Server Active Directory. Isto impede a ativação pós-falha bem sucedida se esse nó falhar.  

