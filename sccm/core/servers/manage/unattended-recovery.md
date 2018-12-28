---
title: Recuperação automática
titleSuffix: Configuration Manager
description: Utilize um script para recuperar seus sites no Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 828c31d1-3d70-4412-b1a8-c92e7e504d39
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 637727356724085f019ac9ab336bc37e3635ea3a
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53415148"
---
# <a name="unattended-site-recovery-for-configuration-manager"></a>Recuperação de site automática para o Configuration Manager   

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

 Para efetuar uma [recuperação automática](/sccm/protect/understand/recover-sites#site-recovery-procedures) de um site de administração central do Configuration Manager ou o site primário, pode criar um script de instalação automática e, em seguida, utilizar a configuração com o **/script** comando opção. O script fornece o mesmo tipo de informações que o Assistente de configuração solicita, mas existem não existem predefinições. Tem de especificar todos os valores para as chaves de configuração que se aplicam ao tipo de recuperação que está a utilizar.

 Para utilizar a opção de linha de comandos de configuração /script, tem de criar um ficheiro de inicialização. Em seguida, especifique este nome de ficheiro depois da opção /script. O nome do ficheiro for importante, desde que ele tem o **. ini** extensão de nome de ficheiro. Quando referenciar o ficheiro de inicialização da configuração na linha de comandos, tem de fornecer o caminho completo do ficheiro. Por exemplo, se o ficheiro de inicialização do programa de configuração *Setup. ini*, e é armazenado na *pasta C:\setup*, seria sua linha de comandos:

 `setup /script c:\setup\setup.ini`

> [!IMPORTANT]  
>  Tem de ter direitos de administrador para executar a configuração. Se executar a configuração com o script automático, inicie a linha de comandos num contexto de administrador utilizando **executar como administrador**.

 O script contém nomes de secções, nomes de chaves e valores. Os nomes de chaves de secção necessários variam consoante o tipo de recuperação que pretende realizar com o script. A ordem das chaves dentro das secções e a ordem das secções no ficheiro não são importantes. As chaves não diferenciam maiúsculas de minúsculas. Quando fornece valores de chaves, o nome da chave tem de ser seguido de um sinal de igual (=) e do valor da chave.

 Utilize as secções seguintes para criar o script para a recuperação de site automática. As tabelas apresentam as chaves de script de configuração disponíveis, os valores correspondentes, se são necessárias, para que tipo de instalação são utilizadas e uma descrição breve da chave.

## <a name="recover-a-central-administration-site-unattended"></a>Recuperar um site de administração central automática
 Utilize as seguintes informações para configurar um ficheiro de script de instalação autônoma para recuperar um site de administração central.

 **Identificação**

-   **Nome da chave:** Action

    -   **Necessário:** Sim
    -   **Valores:** RecoverCCAR
    -   **Detalhes:** Recupera um site de administração central


-   **Nome da chave:** CDLatest

    -   **Necessário:** Sim – apenas quando utilizar suportes de dados do CD. Pasta mais recente.
    -   **Valores:** 1-qualquer valor diferente de 1 é considerado como não use o CD. Mais recente.
    -   **Detalhes:** O script tem de incluir esta chave e valor ao executar a configuração do suporte de dados num CD. Pasta mais recente com o objetivo de instalação de um site de administração central ou primário ou a recuperar um site de administração central ou primário. Este valor informa o programa de configuração que o suporte de dados de formulário CD. Está a ser utilizada a versão mais recente.

**RecoveryOptions**   
-   **Nome da chave:** ServerRecoveryOptions   

    -   **Necessário:** Sim
    -   **Valores:** 1, 2 ou 4  
         1 = Servidor de site de recuperação e SQL Server.   
         2 = Recuperar apenas servidor de site.  
         4 = Recuperar apenas SQL Server.
    -   **Detalhes:** Especifica se a configuração recupera o servidor do site, do SQL Server ou ambos. As chaves associadas são necessárias quando define o seguinte valor para a definição ServerRecoveryOptions:  
        -   **Valor = 1** : tem a opção de especificar um valor para a chave **SiteServerBackupLocation** para recuperar o site com uma cópia de segurança do site. Se não especificar um valor, o site será reinstalado sem ser restaurado a partir de um conjunto de cópias de segurança.

             A chave **BackupLocation** é obrigatória se configurar o valor **10** para a chave **DatabaseRecoveryOptions** , para restaurar a base de dados do site a partir de uma cópia de segurança.

        -   **Valor = 2** : tem a opção de especificar um valor para a chave **SiteServerBackupLocation** para recuperar o site com uma cópia de segurança do site. Se não especificar um valor, o site será reinstalado sem ser restaurado a partir de um conjunto de cópias de segurança.

        -   **Valor = 4** : a chave **BackupLocation** é obrigatória se configurar o valor **10** para a chave **DatabaseRecoveryOptions** , que serve para restaurar a base de dados do site a partir de uma cópia de segurança.

-   **Nome da chave:** DatabaseRecoveryOptions

    -   **Necessário:** Talvez
    -   **Valores:**   
         - **10** = restaurar a base de dados de cópia de segurança.  
         - **20** = utilizar uma base de dados do site que tenha sido recuperada manualmente utilizando outro método.   
         - **40** = criar uma nova base de dados para o site. Utilize esta opção quando não estiver disponível nenhuma cópia de segurança da base de dados do site. Os dados globais e de site são recuperados através da replicação a partir de outros sites.  
         - **80** = ignorar recuperação de base de dados.
    -   **Detalhes:** Especifica a forma como a configuração recupera a base de dados no SQL Server. Esta chave é necessária quando a definição **ServerRecoveryOptions** tem o valor **1** ou **4**


-   **Nome da chave:** ReferenceSite  

    -   **Necessário:** Talvez
    -   **Valores:** &lt;ReferenceSiteFQDN\>
    -   **Detalhes:** Especifica o site primário de referência. Se a cópia de segurança da base de dados for anterior ao período de retenção de registo de alterações ou recuperar o site sem uma cópia de segurança, o site de administração central utiliza o site de referência para recuperar dados globais.

         Quando não especificar um site de referência e a cópia de segurança é anterior ao período de retenção do registo de alterações, todos os sites primários serão reinicializados com os dados restaurados a partir do site de administração central.

         Quando não especificar um site de referência e a cópia de segurança estiver dentro do período de retenção do registo de alterações, apenas as alterações desde a cópia de segurança são replicadas a partir de sites primários. Quando existirem alterações de diferentes sites primários em conflito, o site de administração central utilizará a primeira que receber.

         Esta chave é obrigatória se a definição **DatabaseRecoveryOptions** tiver o valor **40**.

-   **Nome da chave:** SiteServerBackupLocation

    -   **Necessário:** Não
    -   **Valores:** &lt;PathToSiteServerBackupSet\>
    -   **Detalhes:** Especifica o caminho para o conjunto de cópia de segurança de servidor de site. Esta chave é opcional se a definição **ServerRecoveryOptions** tiver o valor **1** ou **2**. Especifique um valor para a chave **SiteServerBackupLocation** para recuperar o site com uma cópia de segurança do mesmo. Se não especificar um valor, o site será reinstalado sem ser restaurado a partir de um conjunto de cópias de segurança.


-   **Nome da chave:** BackupLocation

    -   **Necessário:** Talvez
    -   **Valores:** &lt;PathToSiteDatabaseBackupSet\>
    -   **Detalhes:** Especifica o caminho para o conjunto de cópia de segurança de base de dados de site. A chave **BackupLocation** é obrigatória se configurar o valor **1** ou **4** na chave **ServerRecoveryOptions** e configurar o valor **10** na chave **DatabaseRecoveryOptions** .


**Opções**

- **Nome da chave:** ProductID
  -   **Necessário:** Sim
  -   **Valores:**   
       - xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  
       - Eval
  -   **Detalhes:** O Configuration Manager instalação chave de produto, incluindo os traços. Introduza **Eval** pode instalar a versão de avaliação do Configuration Manager.  


- **Nome da chave:** SiteCode

  -   **Necessário:** Sim
  -   **Valores:** &lt;Código do site\>
  -   **Detalhes:** Três carateres de alfanuméricos que identificam o site na sua hierarquia. Especifique o código do site que foi utilizado pelo site antes da falha.


- **Nome da chave:** SiteName

  -   **Necessário:** Sim
  -   **Valores:** SiteName
  -   **Detalhes:** Descrição para este site.


- **Nome da chave:** SMSInstallDir

  - **Necessário:** Sim
  - **Valores:** &lt;*ConfigMgrInstallationPath*>
  - **Detalhes:** Especifica a pasta de instalação para os ficheiros de programa do Configuration Manager.
    > [!NOTE]   
    >  Pode especificar o caminho original ou um novo caminho a utilizar para a instalação do Configuration Manager.

- **Nome da chave:** SDKServer

  -   **Necessário:** Sim
  -   **Valores:** &lt;*FQDN do fornecedor de SMS*>
  -   **Detalhes:** Especifica o FQDN do servidor que aloja o fornecedor de SMS. Especifique o servidor que alojava o fornecedor de SMS antes da falha.

       Pode configurar Fornecedores de SMS adicionais para o site após a instalação inicial.

- **Nome da chave:** PrerequisiteComp

  -   **Necessário:** Sim
  -   **Valores:** 0 ou 1  
       0 = transferir   
       1 = já transferido
  -   **Detalhes:** Especifica se os ficheiros de pré-requisitos de configuração já foram transferidos. Por exemplo, se usar um valor de 0, a configuração transfere os ficheiros.  


- **Nome da chave:** PrerequisitePath

  -   **Necessário:** Sim
  -   **Valores:** &lt;*PathToSetupPrerequisiteFiles*>
  -   **Detalhes:** Especifica o caminho para os ficheiros de pré-requisitos de configuração. Consoante a **PrerequisiteComp** valor, a configuração utiliza este caminho para armazenar os ficheiros transferidos ou localizar anteriormente os ficheiros transferidos.

- **Nome da chave:** AdminConsole

  -   **Necessário:** Talvez
  -   **Valores:** 0 ou 1 0 = não instalar   
       1 = instalar
  -   **Detalhes:** Especifica se pretende instalar a consola do Configuration Manager. Esta chave é necessária, exceto se a definição **ServerRecoveryOptions** tiver o valor **4**.


- **Nome da chave:** JoinCEIP   
  > [!Note]  
  > A partir do Configuration Manager versão 1802 a funcionalidade CEIP é removida do produto.

  -   **Necessário:** Sim
  -   **Valores:** 0 ou 1  
       0 = não aderir  
       1 = aderir
  -   **Detalhes:** Especifica se pretende aderir o programa de melhoramento da experiência do cliente.

**SQLConfigOptions**

-   **Nome da chave:** SQLServerName

    -   **Necessário:** Sim
    -   **Valores:** *&lt;SQLServerName\>*
    -   **Detalhes:** O nome do servidor ou o nome de instância em cluster, executar o SQL Server que aloja a base de dados do site. Especifique o mesmo servidor que alojava a base de dados do site antes da falha.


-   **Nome da chave:** databaseName

    -   **Necessário:** Sim
    -   **Valores:** *&lt;SiteDatabaseName\>*  ou  *&lt;InstanceName\>*\\*&lt;SiteDatabaseName\>*
    -   **Detalhes:** O nome da base de dados do SQL Server para criar ou utilizar para instalar a base de dados do site de administração central. Especifique o mesmo nome de base de dados que foi utilizado antes da falha.

        > [!IMPORTANT]  
        >  Se não utilizar a instância predefinida, tem de especificar o nome da instância e o nome de base de dados do site.

-   **Nome da chave:** SQLSSBPort

    -   **Necessário:** Não
    -   **Valores:** &lt;*SSBPortNumber*>
    -   **Detalhes:** Especifique a porta do SQL Server Service Broker (SSB) utilizada pelo SQL Server. Normalmente, o SSB está configurado para utilizar a porta TCP 4022, mas são suportadas outras portas. Especifique a mesma porta SSB que era utilizada antes da falha.

## <a name="recover-a-primary-site-unattended"></a>Recuperar um Site Primário em Modo Automático
 Utilize as seguintes informações para configurar um ficheiro de script de instalação autônoma para recuperar um site de administração central.

 **Identificação**

-   **Nome da chave:** Action

    -   **Necessário:** Sim
    -   **Valores:** RecoverPrimarySite
    -   **Detalhes:** Recupera um site primário


-   **Nome da chave:** CDLatest

    -   **Necessário:** Sim – apenas quando utilizar suportes de dados do CD. Pasta mais recente.
    -   **Valores:** 1-qualquer valor diferente de 1 é considerado como não use o CD. Mais recente.
    -   **Detalhes:** O script tem de incluir esta chave e valor ao executar a configuração do suporte de dados num CD. Pasta mais recente com o objetivo de instalação de um site de administração central ou primário ou a recuperar um site de administração central ou primário. Este valor informa o programa de configuração que o suporte de dados de formulário CD. Está a ser utilizada a versão mais recente.

**RecoveryOptions**

-   **Nome da chave:** ServerRecoveryOptions

    -   **Necessário:** Sim
    -   **Valores:** 1, 2 ou 4    
         1 = Servidor de site de recuperação e SQL Server.   
         2 = Recuperar apenas servidor de site.  
         4 = Recuperar apenas SQL Server.
    -   **Detalhes:** Especifica se a configuração recupera o servidor do site, do SQL Server ou ambos. As chaves associadas são necessárias quando define o seguinte valor para a definição ServerRecoveryOptions:

        -   **Valor = 1** : tem a opção de especificar um valor para a chave **SiteServerBackupLocation** para recuperar o site com uma cópia de segurança do site. Se não especificar um valor, o site será reinstalado sem ser restaurado a partir de um conjunto de cópias de segurança.

             A chave **BackupLocation** é obrigatória se configurar o valor **10** para a chave **DatabaseRecoveryOptions** , para restaurar a base de dados do site a partir de uma cópia de segurança.

        -   **Valor = 2** : tem a opção de especificar um valor para a chave **SiteServerBackupLocation** para recuperar o site com uma cópia de segurança do site. Se não especificar um valor, o site será reinstalado sem ser restaurado a partir de um conjunto de cópias de segurança.

        -   **Valor = 4** : a chave **BackupLocation** é obrigatória se configurar o valor **10** para a chave **DatabaseRecoveryOptions** , que serve para restaurar a base de dados do site a partir de uma cópia de segurança.

-   **Nome da chave:** DatabaseRecoveryOptions

    -   **Necessário:** Talvez
    -   **Valores:**   
         - **10** = restaurar a base de dados de cópia de segurança.  
         - **20** = utilizar uma base de dados do site que tenha sido recuperada manualmente utilizando outro método.     
         - **40** = criar uma nova base de dados para o site. Utilize esta opção quando não estiver disponível nenhuma cópia de segurança da base de dados do site. Os dados globais e de site são recuperados através da replicação a partir de outros sites.  
         - **80** = ignorar recuperação de base de dados.
    -   **Detalhes:** Especifica a forma como a configuração recupera a base de dados no SQL Server. Esta chave é necessária quando a definição **ServerRecoveryOptions** tem o valor **1** ou **4**


-   **Nome da chave:** SiteServerBackupLocation

    -   **Necessário:** Não
    -   **Valores:** &lt;PathToSiteServerBackupSet\>
    -   **Detalhes:** Especifica o caminho para o conjunto de cópia de segurança de servidor de site. Esta chave é opcional se a definição **ServerRecoveryOptions** tiver o valor **1** ou **2**. Especifique um valor para a chave **SiteServerBackupLocation** para recuperar o site com uma cópia de segurança do mesmo. Se não especificar um valor, o site será reinstalado sem ser restaurado a partir de um conjunto de cópias de segurança.     


-   **Nome da chave:** BackupLocation

    -   **Necessário:** Talvez
    -   **Valores:** &lt;PathToSiteDatabaseBackupSet\>
    -   **Detalhes:** Especifica o caminho para o conjunto de cópia de segurança de base de dados de site. A chave **BackupLocation** é obrigatória se configurar o valor **1** ou **4** na chave **ServerRecoveryOptions** e configurar o valor **10** na chave **DatabaseRecoveryOptions** .

**Opções**

-   **Nome da chave:** ProductID

    -   **Necessário:** Sim
    -   **Valores:**     
         - xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  
         - Eval     
    -   **Detalhes:** O Configuration Manager instalação chave de produto, incluindo os traços. Introduza **Eval** pode instalar a versão de avaliação do Configuration Manager.  


-   **Nome da chave:** SiteCode

    -   **Necessário:** Sim
    -   **Valores:** &lt;Código do site\>
    -   **Detalhes:** Três carateres de alfanuméricos que identificam o site na sua hierarquia. Especifique o código do site que foi utilizado pelo site antes da falha.


-   **Nome da chave:** SiteName

    -   **Necessário:** Sim
    -   **Valores:** SiteName
    -   **Detalhes:** Descrição para este site.


-   **Nome da chave:** SMSInstallDir

    -   **Necessário:** Sim
    -   **Valores:** &lt;*ConfigMgrInstallationPath*>
    -   **Detalhes:** Especifica a pasta de instalação para os ficheiros de programa do Configuration Manager.

        > [!NOTE]   
        >  Pode especificar o caminho original ou um novo caminho a utilizar para a instalação do Configuration Manager.

-   **Nome da chave:** SDKServer

    -   **Necessário:** Sim
    -   **Valores:** &lt;*FQDN do fornecedor de SMS*>
    -   **Detalhes:** Especifica o FQDN do servidor que aloja o fornecedor de SMS. Especifique o servidor que alojava o fornecedor de SMS antes da falha.

         Pode configurar Fornecedores de SMS adicionais para o site após a instalação inicial.

-   **Nome da chave:** PrerequisiteComp

    -   **Necessário:** Sim
    -   **Valores:** 0 ou 1    
         0 = transferir   
         1 = já transferido   
    -   **Detalhes:** Especifica se os ficheiros de pré-requisitos de configuração já foram transferidos. Por exemplo, se usar um valor de 0, a configuração transfere os ficheiros.


-   **Nome da chave:** PrerequisitePath

    -   **Necessário:** Sim
    -   **Valores:** &lt;*PathToSetupPrerequisiteFiles*>
    -   **Detalhes:** Especifica o caminho para os ficheiros de pré-requisitos de configuração. Consoante a **PrerequisiteComp** valor, a configuração utiliza este caminho para armazenar os ficheiros transferidos ou localizar anteriormente os ficheiros transferidos.


-   **Nome da chave:** AdminConsole

    -   **Necessário:** Talvez
    -   **Valores:** 0 ou 1  
         0 = não instalar   
         1 = instalar  
    -   **Detalhes:** Especifica se pretende instalar a consola do Configuration Manager. Esta chave é necessária, exceto se a definição **ServerRecoveryOptions** tiver o valor **4**.

-   **Nome da chave:** JoinCEIP  
    > [!Note]  
    > A partir do Configuration Manager versão 1802 a funcionalidade CEIP é removida do produto.

    -   **Necessário:** Sim
    -   **Valores:** 0 ou 1    
         0 = não aderir  
         1 = aderir
    -   **Detalhes:** Especifica se pretende aderir o programa de melhoramento da experiência do cliente.


**SQLConfigOptions**

-   **Nome da chave:** SQLServerName

    -   **Necessário:** Sim
    -   **Valores:** *&lt;SQLServerName\>*
    -   **Detalhes:** O nome do servidor ou o nome de instância em cluster, executar o SQL Server que aloja a base de dados do site. Especifique o mesmo servidor que alojava a base de dados do site antes da falha.


-   **Nome da chave:** databaseName

    -   **Necessário:** Sim
    -   **Valores:** *&lt;SiteDatabaseName\>*  ou  *&lt;InstanceName\>*\\*&lt;SiteDatabaseName\>*
    -   **Detalhes:** O nome da base de dados do SQL Server para criar ou utilizar para instalar a base de dados do site de administração central. Especifique o mesmo nome de base de dados que foi utilizado antes da falha.

        > [!IMPORTANT]    
        >  Se não utilizar a instância predefinida, tem de especificar o nome da instância e o nome de base de dados do site.

-   **Nome da chave:** SQLSSBPort

    -   **Necessário:** Não
    -   **Valores:** &lt;*SSBPortNumber*>
    -   **Detalhes:** Especifique a porta do SQL Server Service Broker (SSB) utilizada pelo SQL Server. Normalmente, o SSB está configurado para utilizar a porta TCP 4022, mas são suportadas outras portas. Especifique a mesma porta SSB que era utilizada antes da falha.

**ExpansionOption de hierarquia**

-   **Nome da chave:** CCARSiteServer

    -   **Necessário:** Talvez
    -   **Valores:** &lt;*SiteCodeForCentralAdministrationSite*>
    -   **Detalhes:** Especifica o site de administração central que um site primário liga para quando se associa à hierarquia do Configuration Manager. Esta definição é necessária se o site primário estava ligado a um site de administração central antes da falha. Especifique o código do site que foi utilizado para o site de administração central antes da falha.

-   **Nome da chave:** CASRetryInterval

    -   **Necessário:** Não
    -   **Valores:** &lt;*intervalo*>
    -   **Detalhes:** Especifica o intervalo entre tentativas (em minutos) para estabelecer uma ligação ao site de administração central, após a ligação falha. Por exemplo, se a ligação ao site de administração central falhar, o site primário aguarda o número de minutos que especificar para CASRetryInterval e, em seguida, reattempts a ligação.


-   **Nome da chave:** WaitForCASTimeout

    -   **Necessário:** Não
    -   **Valores:** &lt;*Tempo limite*>
    -   **Detalhes:** Especifica o valor de tempo limite máximo (em minutos) para um site primário ligar ao site de administração central. Por exemplo, se um site primário não conseguir ligar a um site de administração central, tenta efetuar de novo a ligação com base no CASRetryInterval, até atingir o WaitForCASTimeout. Pode especificar um valor entre 0 e 100.
