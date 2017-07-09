---
title: "Recuperação autônoma | Microsoft Docs"
description: Use um script para recuperar os sites no System Center Configuration Manager.
ms.custom: na
ms.date: 6/5/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 828c31d1-3d70-4412-b1a8-c92e7e504d39
caps.latest.revision: 
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: f7cd9c71287d62c9f5d36e2f032bc2a6065572ae
ms.openlocfilehash: b5a1a1d165a6888bc26e809666d2331ff3c24d68
ms.contentlocale: pt-pt
ms.lasthandoff: 06/06/2017

---

# <a name="unattended-site-recovery-for-configuration-manager"></a>Recuperação autônoma do site do Configuration Manager   

*Aplica-se a: System Center Configuration Manager (ramificação atual)* 
 para executar um [recuperação autônoma](/sccm/protect/understand/recover-sites#site-recovery-procedures) de um site de administração central do Configuration Manager ou site primário, você pode criar um script de instalação autônoma e, em seguida, usar a instalação com o **/script** de comando. O script fornece o mesmo tipo de informações pedidas pelo Assistente de configuração, mas não existem predefinições. Tem de especificar todos os valores para as chaves de configuração que se aplicam ao tipo de recuperação que está a utilizar.

 Para utilizar a opção da linha de comandos /script de configuração, tem de criar um ficheiro de inicialização e especificar o respetivo nome após esta opção da linha de comandos. O nome do arquivo é importante, desde que ele tenha o **. ini** extensão de nome de arquivo. Quando referenciar o ficheiro de inicialização da configuração na linha de comandos, tem de fornecer o caminho completo do ficheiro. Por exemplo, se o arquivo de inicialização de instalação é nomeado *Setup*, e é armazenado no *pasta C:\setup*, sua linha de comando será:

 **setup /script c:\setup\setup.ini**.

> [!IMPORTANT]  
>  Tem de ter direitos de Administrador para executar a Configuração. Quando executar a Configuração com o script automático, inicie a Linha de Comandos num contexto de Administrador através de **Executar como administrador**.

 O script contém nomes de secções, nomes de chaves e valores. Os nomes de chaves de secção necessários variam consoante o tipo de recuperação que pretende realizar com o script. A ordem das chaves dentro das secções e a ordem das secções no ficheiro não são importantes. As chaves não são sensíveis a maiúsculas e minúsculas. Quando fornece valores de chaves, o nome da chave tem de ser seguido de um sinal de igual (=) e do valor da chave.

 Utilize as secções seguintes para criar o script para a recuperação de site automática. As tabelas apresentam as chaves de script de configuração disponíveis, os valores correspondentes, se são necessárias, para que tipo de instalação são utilizadas e uma descrição breve da chave.

## <a name="recover-a-central-administration-site-unattended"></a>Recuperar um site de administração central automática
 Use as informações a seguir para configurar um arquivo de script de instalação autônoma para recuperar um site de administração central.

 **Identificação**

-   **Nome da chave:** Ação

    -   **Necessário:** Sim
    -   **Valores:** RecoverCCAR
    -   **Detalhes:** Recupera um site de administração central


-   **Nome da chave:** CDLatest

    -   **Necessário:** Sim – somente quando usar a mídia de CD. Pasta mais recente.
    -   **Valores:** 1 qualquer valor diferente de 1 é considerada não esteja usando o CD. Mais recente.
    -   **Detalhes:** O script deve incluir essa chave e valor ao executar a instalação da mídia em um CD. Pasta mais recente com a finalidade de instalar um site de administração central ou primário, ou recuperar um site de administração central ou primário. Esse valor informa instalação mídia formam CD. Versão mais recente está sendo usado.

**RecoveryOptions**   
-   **Nome da chave:** ServerRecoveryOptions   

    -   **Necessário:** Sim
    -   **Valores:** 1, 2 ou 4  
         1 = Servidor de site de recuperação e SQL Server.   
         2 = Recuperar apenas servidor de site.  
         4 = Recuperar apenas SQL Server.
    -   **Detalhes:** Especifica se a instalação recuperará o servidor do site, do SQL Server ou ambos. As chaves associadas são necessárias quando define o seguinte valor para a definição ServerRecoveryOptions:  
        -   **Valor = 1** : tem a opção de especificar um valor para a chave **SiteServerBackupLocation** para recuperar o site com uma cópia de segurança do site. Se não especificar um valor, o site será reinstalado sem ser restaurado a partir de um conjunto de cópias de segurança.

             A chave **BackupLocation** é obrigatória se configurar o valor **10** para a chave **DatabaseRecoveryOptions** , para restaurar a base de dados do site a partir de uma cópia de segurança.

        -   **Valor = 2** : tem a opção de especificar um valor para a chave **SiteServerBackupLocation** para recuperar o site com uma cópia de segurança do site. Se não especificar um valor, o site será reinstalado sem ser restaurado a partir de um conjunto de cópias de segurança.

        -   **Valor = 4** : a chave **BackupLocation** é obrigatória se configurar o valor **10** para a chave **DatabaseRecoveryOptions** , que serve para restaurar a base de dados do site a partir de uma cópia de segurança.

-   **Nome da chave:** DatabaseRecoveryOptions

    -   **Necessário:** Talvez
    -   **Valores:** 10, 20, 40, 80  
         10 = Restaurar a base de dados do site a partir de cópia de segurança.  
         20 = Utilizar uma base de dados do site que tenha sido recuperada manualmente utilizando outro método.   
         40 = Criar uma nova base de dados para o site. Utilize esta opção quando não estiver disponível nenhuma cópia de segurança da base de dados do site. Os dados globais e de site são recuperados através da replicação a partir de outros sites.  
         80 = ignorar recuperação da base de dados.
    -   **Detalhes:** Especifica como a instalação recuperará o banco de dados do site no SQL Server. Esta chave é necessária quando a definição **ServerRecoveryOptions** tem o valor **1** ou **4**


-   **Nome da chave:** ReferenceSite  

    -   **Necessário:** Talvez
    -   **Valores:** &lt;ReferenceSiteFQDN\>
    -   **Detalhes:** Especifica o site primário de referência que o site de administração central usa para recuperar dados globais se o backup do banco de dados for mais antigo que o período de retenção do controle de alterações ou quando você recupera o site sem um backup.

         Quando você não especificar um site de referência, e o backup é mais antigo que o período de retenção do controle de alterações, todos os sites primários são reinicializados com os dados restaurados do site de administração central.

         Quando você não especificar um site de referência e o backup está dentro do período de retenção do controle de alterações, somente as alterações ocorridas desde o backup são replicadas dos sites primários. Quando existirem alterações de diferentes sites primários em conflito, o site de administração central utilizará a primeira que receber.

         Esta chave é obrigatória se a definição **DatabaseRecoveryOptions** tiver o valor **40**.

-   **Nome da chave:** SiteServerBackupLocation

    -   **Necessário:** Não
    -   **Valores:** &lt;PathToSiteServerBackupSet\>
    -   **Detalhes:** Especifica o caminho para o conjunto de backup de servidor do site. Esta chave é opcional se a definição **ServerRecoveryOptions** tiver o valor **1** ou **2**. Especifique um valor para a chave **SiteServerBackupLocation** para recuperar o site com uma cópia de segurança do mesmo. Se não especificar um valor, o site será reinstalado sem ser restaurado a partir de um conjunto de cópias de segurança.


-   **Nome da chave:** BackupLocation

    -   **Necessário:** Talvez
    -   **Valores:** &lt;PathToSiteDatabaseBackupSet\>
    -   **Detalhes:** Especifica o caminho para o conjunto de backup de banco de dados do site. A chave **BackupLocation** é obrigatória se configurar o valor **1** ou **4** na chave **ServerRecoveryOptions** e configurar o valor **10** na chave **DatabaseRecoveryOptions** .


**Opções**

-   **Nome da chave:** ProductID
    -   **Necessário:** Sim
    -   **Valores:**   
         xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  
          Eval
    -   **Detalhes:** O Configuration Manager instalação chave do produto, incluindo os traços. Digite **Eval** pode instalar a versão de avaliação do Configuration Manager.  


-   **Nome da chave:** Código do site

    -   **Necessário:** Sim
    -   **Valores:** &lt;Código do site\>
    -   **Detalhes:** Três caracteres alfanuméricos que identificam exclusivamente o site na sua hierarquia. Tem de especificar o código do site que era utilizado pelo site antes da falha.


-   **Nome da chave:** Nome do site

    -   **Necessário:** Sim
    -   **Valores:** Nome do site
    -   **Detalhes:** Descrição para este site.


-   **Nome da chave:** SMSInstallDir

    -   **Necessário:** Sim
    -   **Valores:** &lt;*ConfigMgrInstallationPath*>
    -   **Detalhes:** Especifica a pasta de instalação para os arquivos de programa do Configuration Manager.
        > [!NOTE]   
        >  Você pode especificar o caminho original ou um novo caminho a ser usado para a instalação do Configuration Manager.

-   **Nome da chave:** SDKServer

    -   **Necessário:** Sim
    -   **Valores:** &lt;*FQDN do provedor de SMS*>
    -   **Detalhes:** Especifica o FQDN para o servidor que hospedará o provedor de SMS. Terá de especificar o servidor que hospedava o Fornecedor de SMS antes da falha.

         Pode configurar Fornecedores de SMS adicionais para o site após a instalação inicial.

-   **Nome da chave:** PrerequisiteComp

    -   **Necessário:** Sim
    -   **Valores:** 0 ou 1  
         0 = transferir   
         1 = já transferido
    -   **Detalhes:** Especifica se os arquivos de pré-requisito de instalação já foram baixados. Por exemplo, se utilizar o valor 0, o Programa de Configuração transferirá os ficheiros.  


-   **Nome da chave:** PrerequisitePath

    -   **Necessário:** Sim
    -   **Valores:** &lt;*PathToSetupPrerequisiteFiles*>
    -   **Detalhes:** Especifica o caminho para os arquivos de pré-requisito de instalação. Conforme o valor de **PrerequisiteComp** , a Configuração utiliza este caminho para armazenar os ficheiros transferidos ou localizar os ficheiros transferidos anteriormente.

-   **Nome da chave:** AdminConsole

    -   **Necessário:** Talvez
    -   **Valores:** 0 ou 1 0 = não instalar   
         1 = instalar
    -   **Detalhes:** Especifica se deseja instalar o console do Configuration Manager. Esta chave é necessária, exceto se a definição **ServerRecoveryOptions** tiver o valor **4**.


-   **Nome da chave:** JoinCEIP

    -   **Necessário:** Sim
    -   **Valores:** 0 ou 1  
         0 = não aderir  
         1 = aderir
    -   **Detalhes:** Especifica se o programa de Aperfeiçoamento da experiência de ingresso.

**SQLConfigOptions**

-   **Nome da chave:** SQLServerName

    -   **Necessário:** Sim
    -   **Valores:** *&lt;SQLServerName\>*
    -   **Detalhes:** O nome do servidor ou o nome da instância clusterizada, executando o SQL Server que hospedará o banco de dados do site. Terá de especificar o mesmo servidor que alojava a base de dados do site antes da falha.


-   **Nome da chave:** DatabaseName

    -   **Necessário:** Sim
    -   **Valores:** *&lt;Nomedobancodedadosdosite\>*  ou  *&lt;InstanceName\>*\\*&lt;Nomedobancodedadosdosite\>*
    -   **Detalhes:** O nome do banco de dados do SQL Server para criar ou usar para instalar o banco de dados do site de administração central. Terá de especificar o nome da mesma base de dados que foi utilizada antes da falha.

        > [!IMPORTANT]  
        >  Se não utilizar a instância predefinida, terá de especificar o nome da instância e o nome da base de dados do site.

-   **Nome da chave:** SQLSSBPort

    -   **Necessário:** Não
    -   **Valores:** &lt;*SSBPortNumber*>
    -   **Detalhes:** Especifique a porta do SQL Server Service Broker (SSB) usada pelo SQL Server. Normalmente, o SSB está configurado para utilizar a porta TCP 4022, mas são suportadas outras portas. Tem de especificar a mesma porta do SSB que foi utilizada antes da falha.

## <a name="recover-a-primary-site-unattended"></a>Recuperar um Site Primário em Modo Automático
 Use as informações a seguir para configurar um arquivo de script de instalação autônoma para recuperar um site de administração central.

 **Identificação**

-   **Nome da chave:** Ação

    -   **Necessário:** Sim
    -   **Valores:** RecoverPrimarySite
    -   **Detalhes:** Recupera um site primário


-   **Nome da chave:** CDLatest

    -   **Necessário:** Sim – somente quando usar a mídia de CD. Pasta mais recente.
    -   **Valores:** 1 qualquer valor diferente de 1 é considerada não esteja usando o CD. Mais recente.
    -   **Detalhes:** O script deve incluir essa chave e valor ao executar a instalação da mídia em um CD. Pasta mais recente com a finalidade de instalar um site de administração central ou primário, ou recuperar um site de administração central ou primário. Esse valor informa instalação mídia formam CD. Versão mais recente está sendo usado.

**RecoveryOptions**

-   **Nome da chave:** ServerRecoveryOptions

    -   **Necessário:** Sim
    -   **Valores:** 1, 2 ou 4    
         1 = Servidor de site de recuperação e SQL Server.   
         2 = Recuperar apenas servidor de site.  
         4 = Recuperar apenas SQL Server.
    -   **Detalhes:** Especifica se a instalação recuperará o servidor do site, do SQL Server ou ambos. As chaves associadas são necessárias quando define o seguinte valor para a definição ServerRecoveryOptions:

        -   **Valor = 1** : tem a opção de especificar um valor para a chave **SiteServerBackupLocation** para recuperar o site com uma cópia de segurança do site. Se não especificar um valor, o site será reinstalado sem ser restaurado a partir de um conjunto de cópias de segurança.

             A chave **BackupLocation** é obrigatória se configurar o valor **10** para a chave **DatabaseRecoveryOptions** , para restaurar a base de dados do site a partir de uma cópia de segurança.

        -   **Valor = 2** : tem a opção de especificar um valor para a chave **SiteServerBackupLocation** para recuperar o site com uma cópia de segurança do site. Se não especificar um valor, o site será reinstalado sem ser restaurado a partir de um conjunto de cópias de segurança.

        -   **Valor = 4** : a chave **BackupLocation** é obrigatória se configurar o valor **10** para a chave **DatabaseRecoveryOptions** , que serve para restaurar a base de dados do site a partir de uma cópia de segurança.

-   **Nome da chave:** DatabaseRecoveryOptions

    -   **Necessário:** Talvez
    -   **Valores:** 10, 20, 40, 80  
         10 = Restaurar a base de dados do site a partir de cópia de segurança.  
         20 = Utilizar uma base de dados do site que tenha sido recuperada manualmente utilizando outro método.     
         40 = Criar uma nova base de dados para o site. Utilize esta opção quando não estiver disponível nenhuma cópia de segurança da base de dados do site. Os dados globais e de site são recuperados através da replicação a partir de outros sites.  
         80 = ignorar recuperação da base de dados.
    -   **Detalhes:** Especifica como a instalação recuperará o banco de dados do site no SQL Server. Esta chave é necessária quando a definição **ServerRecoveryOptions** tem o valor **1** ou **4**


-   **Nome da chave:** SiteServerBackupLocation

    -   **Necessário:** Não
    -   **Valores:** &lt;PathToSiteServerBackupSet\>
    -   **Detalhes:** Especifica o caminho para o conjunto de backup de servidor do site. Esta chave é opcional se a definição **ServerRecoveryOptions** tiver o valor **1** ou **2**. Especifique um valor para a chave **SiteServerBackupLocation** para recuperar o site com uma cópia de segurança do mesmo. Se não especificar um valor, o site será reinstalado sem ser restaurado a partir de um conjunto de cópias de segurança.     


-   **Nome da chave:** BackupLocation

    -   **Necessário:** Talvez
    -   **Valores:** &lt;PathToSiteDatabaseBackupSet\>
    -   **Detalhes:** Especifica o caminho para o conjunto de backup de banco de dados do site. A chave **BackupLocation** é obrigatória se configurar o valor **1** ou **4** na chave **ServerRecoveryOptions** e configurar o valor **10** na chave **DatabaseRecoveryOptions** .

**Opções**

-   **Nome da chave:** ProductID

    -   **Necessário:** Sim
    -   **Valores:**     
         xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  
         Eval     
    -   **Detalhes:** O Configuration Manager instalação chave do produto, incluindo os traços. Digite **Eval** pode instalar a versão de avaliação do Configuration Manager.  


-   **Nome da chave:** Código do site

    -   **Necessário:** Sim
    -   **Valores:** &lt;Código do site\>
    -   **Detalhes:** Três caracteres alfanuméricos que identificam exclusivamente o site na sua hierarquia. Tem de especificar o código do site que era utilizado pelo site antes da falha.


-   **Nome da chave:** Nome do site

    -   **Necessário:** Sim
    -   **Valores:** Nome do site
    -   **Detalhes:** Descrição para este site.


-   **Nome da chave:** SMSInstallDir

    -   **Necessário:** Sim
    -   **Valores:** &lt;*ConfigMgrInstallationPath*>
    -   **Detalhes:** Especifica a pasta de instalação para os arquivos de programa do Configuration Manager.

        > [!NOTE]   
        >  Você pode especificar o caminho original ou um novo caminho a ser usado para a instalação do Configuration Manager.

-   **Nome da chave:** SDKServer

    -   **Necessário:** Sim
    -   **Valores:** &lt;*FQDN do provedor de SMS*>
    -   **Detalhes:** Especifica o FQDN para o servidor que hospedará o provedor de SMS. Terá de especificar o servidor que hospedava o Fornecedor de SMS antes da falha.

         Pode configurar Fornecedores de SMS adicionais para o site após a instalação inicial.

-   **Nome da chave:** PrerequisiteComp

    -   **Necessário:** Sim
    -   **Valores:** 0 ou 1    
         0 = transferir   
         1 = já transferido   
    -   **Detalhes:** Especifica se os arquivos de pré-requisito de instalação já foram baixados. Por exemplo, se utilizar o valor 0, o Programa de Configuração transferirá os ficheiros.


-   **Nome da chave:** PrerequisitePath

    -   **Necessário:** Sim
    -   **Valores:** &lt;*PathToSetupPrerequisiteFiles*>
    -   **Detalhes:** Especifica o caminho para os arquivos de pré-requisito de instalação. Conforme o valor de **PrerequisiteComp** , a Configuração utiliza este caminho para armazenar os ficheiros transferidos ou localizar os ficheiros transferidos anteriormente.


-   **Nome da chave:** AdminConsole

    -   **Necessário:** Talvez
    -   **Valores:** 0 ou 1  
         0 = não instalar   
         1 = instalar  
    -   **Detalhes:** Especifica se deseja instalar o console do Configuration Manager. Esta chave é necessária, exceto se a definição **ServerRecoveryOptions** tiver o valor **4**.

-   **Nome da chave:** JoinCEIP

    -   **Necessário:** Sim
    -   **Valores:** 0 ou 1    
         0 = não aderir  
         1 = aderir
    -   **Detalhes:** Especifica se o programa de Aperfeiçoamento da experiência de ingresso.


**SQLConfigOptions**

-   **Nome da chave:** SQLServerName

    -   **Necessário:** Sim
    -   **Valores:** *&lt;SQLServerName\>*
    -   **Detalhes:** O nome do servidor ou o nome da instância clusterizada, executando o SQL Server que hospedará o banco de dados do site. Terá de especificar o mesmo servidor que alojava a base de dados do site antes da falha.


-   **Nome da chave:** DatabaseName

    -   **Necessário:** Sim
    -   **Valores:** *&lt;Nomedobancodedadosdosite\>*  ou  *&lt;InstanceName\>*\\*&lt;Nomedobancodedadosdosite\>*
    -   **Detalhes:** O nome do banco de dados do SQL Server para criar ou usar para instalar o banco de dados do site de administração central. Terá de especificar o nome da mesma base de dados que foi utilizada antes da falha.

        > [!IMPORTANT]    
        >  Se não utilizar a instância predefinida, terá de especificar o nome da instância e o nome da base de dados do site.

-   **Nome da chave:** SQLSSBPort

    -   **Necessário:** Não
    -   **Valores:** &lt;*SSBPortNumber*>
    -   **Detalhes:** Especifique a porta do SQL Server Service Broker (SSB) usada pelo SQL Server. Normalmente, o SSB está configurado para utilizar a porta TCP 4022, mas são suportadas outras portas. Tem de especificar a mesma porta do SSB que foi utilizada antes da falha.

**ExpansionOption de hierarquia**

-   **Nome da chave:** CCARSiteServer

    -   **Necessário:** Talvez
    -   **Valores:** &lt;*SiteCodeForCentralAdministrationSite*>
    -   **Detalhes:** Especifica o site de administração central que um site primário se anexará quando ele ingressar na hierarquia do Configuration Manager. Esta definição é necessária se o site primário estava ligado a um site de administração central antes da falha. Tem de especificar o código do site que era utilizado para o site de administração central antes da falha.

-   **Nome da chave:** CASRetryInterval

    -   **Necessário:** Não
    -   **Valores:** &lt;*Intervalo*>
    -   **Detalhes:** Especifica o intervalo de repetição (em minutos) para tentar uma conexão ao site de administração central depois da conexão falha. Por exemplo, se a ligação ao site de administração central falhar, o site primário aguarda o número de minutos que especificar para CASRetryInterval e, em seguida, tenta restabelecer a ligação.


-   **Nome da chave:** WaitForCASTimeout

    -   **Necessário:** Não
    -   **Valores:** &lt;*Tempo limite*>
    -   **Detalhes:** Especifica o valor de tempo limite máximo (em minutos) de um site primário para se conectar ao site de administração central. Por exemplo, se um site primário não conseguir ligar a um site de administração central, tenta efetuar de novo a ligação com base no CASRetryInterval, até atingir o WaitForCASTimeout. Pode especificar um valor entre 0 e 100.

