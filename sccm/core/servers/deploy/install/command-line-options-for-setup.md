---
title: Opções da linha de comandos de configuração
titleSuffix: Configuration Manager
description: Crie scripts de automação para instalar o System Center Configuration Manager numa linha de comandos.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0da167f1-52cf-4dfd-8f73-833ca3eb8478
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f5c85e3058a63868cfee28865c1be222919b29a8
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56141828"
---
# <a name="command-line-options-for-setup-in-system-center-configuration-manager"></a>Opções da linha de comandos para configuração no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


 Utilize as seguintes informações para configurar scripts ou para instalar o System Center Configuration Manager numa linha de comandos.  

##  <a name="bkmk_setup"></a> Opções da linha de comandos para configuração  
 **/DEINSTALL**  
 Desinstala o site. Execute a configuração do computador do servidor do site.  

 **/DONTSTARTSITECOMP**  
 Instala um site, mas impede que o serviço de Gestor de componentes do Site a partir de. Até que o serviço de Gestor de componentes do Site é iniciado, o site não está ativo. O Gestor de componentes do Site é responsável por instalar e iniciar o serviço SMS_Executive e de processos adicionais no site. Depois de concluída a instalação do site, quando iniciar o serviço de Gestor de componentes do Site, ele instala o serviço SMS_Executive e de processos adicionais necessários para o site operar.  

 **/HIDDEN**  
 Oculta a interface do usuário durante a configuração. Utilize esta opção apenas em conjunto com o **/script** opção. O ficheiro de script automático tem de fornecer todas as opções necessárias a configuração falha.  

 **/NOUSERINPUT**  
 Desativa a intervenção do utilizador durante a configuração, mas apresenta o Assistente de configuração. Utilize esta opção apenas em conjunto com o **/script** opção. O ficheiro de script automático tem de fornecer todas as opções necessárias a configuração falha.  

 **/RESETSITE**  
 Executa um site de reposição que repõe as contas de serviço e da base de dados para o site. Execute a configuração partir  **< *caminho de instalação do Configuration Manager*> \BIN\X64** no servidor do site. Para obter mais informações sobre a reposição do site, consulte a [executar uma reposição do site](../../../../core/servers/manage/modify-your-infrastructure.md#bkmk_reset) secção [modificar a infraestrutura do System Center Configuration Manager](../../../../core/servers/manage/modify-your-infrastructure.md).  

 **/TESTDBUPGRADE <*nome da instância*>\\<*nome de base de dados*>**  
 Efetua um teste uma cópia de segurança da base de dados do site para se certificar de que a base de dados é capaz de uma atualização. Forneça o nome da instância e o nome de base de dados para a base de dados do site. Se especificar apenas o nome da base de dados, a configuração utiliza o nome da instância predefinida.  

> [!IMPORTANT]  
>  Não execute esta opção da linha de comandos no seu banco de dados do site de produção. Executar esta opção da linha de comandos no seu banco de dados do site de produção, atualiza a base de dados do site e pode processar o seu site inoperável.  

 **/UPGRADE**  
 Executa uma atualização automática de um site. Quando utiliza **/ATUALIZAR**, tem de especificar a chave de produto, incluindo os traços (-). Além disso, tem de especificar o caminho para os ficheiros de pré-requisitos de configuração anteriormente transferidos.  

 Exemplo: `setupwpf.exe /UPGRADE xxxxx-xxxxx-xxxxx-xxxxx-xxxxx <path to external component files>`  

 Para obter mais informações sobre os ficheiros de pré-requisitos de configuração, consulte [programa de configuração](setup-downloader.md).  

 **/SCRIPT <*caminho do script de configuração*>**  
 Efetua instalações automáticas. Um ficheiro de inicialização do programa de configuração é necessário quando utiliza a **/script** opção. Para obter mais informações sobre como a configuração de execução automática, consulte [instalar sites utilizando uma linha de comando](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md).  

 **/ SDKINST <*FQDN do fornecedor de SMS*>**  
 Instala o fornecedor de SMS no computador especificado. Forneça o nome de domínio completamente qualificado (FQDN) para o computador do fornecedor de SMS. Para obter mais informações sobre o fornecedor de SMS, consulte [planear o fornecedor de SMS](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

 **/ SDKDEINST <*FQDN do fornecedor de SMS*>**  
 Desinstala o fornecedor de SMS no computador especificado. Fornece o FQDN para o computador do fornecedor de SMS.  

 **/MANAGELANGS <*caminho do script de idioma*>**  
 Gere os idiomas que estão instalados num site instalado anteriormente. Para utilizar esta opção, executar a configuração a partir  **< *caminho de instalação do Configuration Manager*> \BIN\X64** no servidor do site. Forneça o local para o ficheiro de script de idioma que contém as definições de idioma. Para obter mais informações sobre as opções de idioma disponíveis no ficheiro de script de configuração de idioma, consulte a [opções da linha de comandos para gerir idiomas](#bkmk_Lang) secção.  

##  <a name="bkmk_Lang"></a> Opções da linha de comandos para gerir idiomas  
 **Identificação**  

-   **Nome da chave:** Action  

    -   **Necessário:** Sim  

    -   **Valores:** ManageLanguages  

    -   **Detalhes:** Gere o servidor, o cliente e o suporte de idiomas de cliente móvel num site.  

**Opções**  

-   **Nome da chave:** AddServerLanguages  

    -   **Necessário:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK, or ZHH  

    -   **Detalhes:** Especifica os idiomas do servidor que estarão disponíveis para a consola do Configuration Manager, relatórios e objetos do Configuration Manager. O inglês está disponível por predefinição.  

-   **Nome da chave:** AddClientLanguages  

    -   **Necessário:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK, or ZHH  

    -   **Detalhes:** Especifica os idiomas que estarão disponíveis para os computadores cliente. O inglês está disponível por predefinição.  

-   **Nome da chave:** DeleteServerLanguages  

    -   **Necessário:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK, or ZHH  

    -   **Detalhes:** Especifica os idiomas a remover e que já não estará disponível para a consola do Configuration Manager, relatórios e objetos do Configuration Manager. O inglês está disponível por predefinição e não pode ser removido.  

-   **Nome da chave:** DeleteClientLanguages  

    -   **Necessário:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK, or ZHH  

    -   **Detalhes:** Especifica os idiomas a remover e que já não estarão disponível para computadores cliente. O inglês está disponível por predefinição e não pode ser removido.  

-   **Nome da chave:** MobileDeviceLanguage  

    -   **Necessário:** Sim  

    -   **Valores:** 0 ou 1  

         0 = fazer não instalar  

         1 = instalar  

    -   **Detalhes:** Especifica se estão instalados os idiomas de cliente do dispositivo móvel.  

-   **Nome da chave:** PrerequisiteComp  

    -   **Necessário:** Sim  

    -   **Valores:** 0 ou 1  

         0 = download  

         1 = já transferido  

    -   **Detalhes:** Especifica se os ficheiros de pré-requisitos de configuração já foram transferidos. Por exemplo, se utilizar o valor **0**, configuração transfere os ficheiros.  

-   **Nome da chave:** PrerequisitePath  

    -   **Necessário:** Sim  

    -   **Valores:** <*caminho para ficheiros de pré-requisitos de configuração*>  

    -   **Detalhes:** Especifica o caminho para os ficheiros de pré-requisitos de configuração. Consoante a **PrerequisiteComp** valor, a configuração utiliza este caminho para armazenar os ficheiros transferidos ou localizar anteriormente os ficheiros transferidos.  

##  <a name="bkmk_Unattended"></a> Chaves de ficheiro de script de instalação autônoma  
 Utilize as secções seguintes para o ajudar a criar o script para a configuração automática. As listas mostram as chaves de script de configuração disponíveis, os valores correspondentes, se são necessárias, que tipo de instalação são utilizadas e uma breve descrição da chave.  

### <a name="unattended-install-for-a-central-administration-site"></a>Instalação automática de um site de administração central  
 Utilize os detalhes seguintes para instalar um site de administração central utilizando um ficheiro de script de instalação autônoma.  

**Identificação**  

-   **Nome da chave:** Action  

    -   **Necessário:** Sim  

    -   **Valores:** InstallCAS  

    -   **Detalhes:** Instala um site de administração central.  

-   **Nome da chave:** CDLatest  

    -   **Necessário:** Sim – apenas quando utilizar suportes de dados do CD. Pasta mais recente.    

    -   **Valores:** 1-qualquer valor diferente de 1 é considerado como não use o CD. Mais recente.

    -   **Detalhes:** O script tem de incluir esta chave e valor ao executar a configuração do suporte de dados num CD. Pasta mais recente com o objetivo de instalação de um site de administração central ou primário ou a recuperar um site de administração central ou primário. Este valor informa o programa de configuração que o suporte de dados de formulário CD. Está a ser utilizada a versão mais recente.

**Opções**  

-   **Nome da chave:** ProductID  

    -   **Necessário:** Sim  

    -   **Valores:** <*xxxxx-xxxxx-xxxxx-xxxxx-xxxxx*> *ou* Eval  

    -   **Detalhes:** Especifica a chave de produto de instalação do Configuration Manager, incluindo os traços. Introduza **Eval** para instalar a versão de avaliação do Configuration Manager.  

-   **Nome da chave:** SiteCode  

    -   **Necessário:** Sim  

    -   **Valores:** <*código do Site*>  

    -   **Detalhes:** Especifica três carateres alfanuméricos que identificam o site na sua hierarquia.  

-   **Nome da chave:** Nome do site  

    -   **Necessário:** Sim  

    -   **Valores:** <*nome do Site*>  

    -   **Detalhes:** Especifica o nome para este site.  

-   **Nome da chave:** SMSInstallDir  

    -   **Necessário:** Sim  

    -   **Valores:** <*caminho de instalação do Configuration Manager*>  

    -   **Detalhes:** Especifica a pasta de instalação para os ficheiros de programa do Configuration Manager.  

-   **Nome da chave:** SDKServer  

    -   **Necessário:** Sim  

    -   **Valores:** <*FQDN do fornecedor de SMS*>  

    -   **Detalhes:** Especifica o FQDN do servidor que alojará o fornecedor de SMS. Pode configurar Fornecedores de SMS adicionais para o site após a instalação inicial.  

-   **Nome da chave:** PrerequisiteComp  

    -   **Necessário:** Sim  

    -   **Valores:** 0 ou 1  

         0 = download  

         1 = já transferido  

    -   **Detalhes:** Especifica se os ficheiros de pré-requisitos de configuração já foram transferidos. Por exemplo, se utilizar o valor **0**, configuração transfere os ficheiros.  

-   **Nome da chave:** PrerequisitePath  

    -   **Necessário:** Sim  

    -   **Valores:** <*caminho para ficheiros de pré-requisitos de configuração*>  

    -   **Detalhes:** Especifica o caminho para os ficheiros de pré-requisitos de configuração. Consoante a **PrerequisiteComp** valor, a configuração utiliza este caminho para armazenar os ficheiros transferidos ou localizar anteriormente os ficheiros transferidos.  

-   **Nome da chave:** AdminConsole  

    -   **Necessário:** Sim  

    -   **Valores:** 0 ou 1  

         0 = fazer não instalar  

         1 = instalar  

    -   **Detalhes:** Especifica se pretende instalar a consola do Configuration Manager.  

-   **Nome da chave:** JoinCEIP  
    > [!Note]  
    > A partir do Configuration Manager versão 1802 a funcionalidade CEIP é removida do produto.

    -   **Necessário:** Sim  

    -   **Valores:** 0 ou 1  

         0 = fazer não aderir  

         1 = associação  

    -   **Detalhes:** Especifica se pretende aderir o programa de melhoramento da experiência do cliente (PMEC).  

-   **Nome da chave:** AddServerLanguages  

    -   **Necessário:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK, or ZHH  

    -   **Detalhes:** Especifica os idiomas do servidor que estarão disponíveis para a consola do Configuration Manager, relatórios e objetos do Configuration Manager. O inglês está disponível por predefinição.  

-   **Nome da chave:** AddClientLanguages  

    -   **Necessário:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK, or ZHH  

    -   **Detalhes:** Especifica os idiomas que estarão disponíveis para os computadores cliente. O inglês está disponível por predefinição.  

-   **Nome da chave:** DeleteServerLanguages  

    -   **Necessário:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK, or ZHH  

    -   **Detalhes:** Modifica um site depois de ser instalado. Especifica os idiomas a remover e que já não estará disponível para a consola do Configuration Manager, relatórios e objetos do Configuration Manager. O inglês está disponível por predefinição e não pode ser removido.  

-   **Nome da chave:** DeleteClientLanguages  

    -   **Necessário:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK, or ZHH  

    -   **Detalhes:** Modifica um site depois de ser instalado. Especifica os idiomas a remover e que já não estarão disponível para computadores cliente. O inglês está disponível por predefinição e não pode ser removido.  

-   **Nome da chave:** MobileDeviceLanguage  

    -   **Necessário:** Sim  

    -   **Valores:** 0 ou 1  

         0 = fazer não instalar  

         1 = instalar  

    -   **Detalhes:** Especifica se estão instalados os idiomas de cliente do dispositivo móvel.  

**SQLConfigOptions**  

-   **Nome da chave:** SQLServerName  

    -   **Necessário:** Sim  

    -   **Valores:** <*nome do SQL server*>  

    -   **Detalhes:** Especifica o nome do servidor ou instância em cluster que está a executar o SQL Server e que irá alojar a base de dados do site.  

-   **Nome da chave:** databaseName  

    -   **Necessário:** Sim  

    -   **Valores:** <*nome de base de dados do Site*> ou <*nome da instância*>\\<*nome de base de dados do Site*>  

    -   **Detalhes:** Especifica o nome da base de dados do SQL Server para criar ou a base de dados do SQL Server para utilizar, quando o programa de configuração instala o banco de dados do site de administração central.  

        > [!IMPORTANT]  
        >  Se não utilizar a instância predefinida, tem de especificar o nome da instância e o nome de base de dados do site.  

-   **Nome da chave:** SQLSSBPort  

    -   **Necessário:** Não  

    -   **Valores:** <*número da porta SSB*>  

    -   **Detalhes:** Especifica a porta do SQL Server Service Broker (SSB) que utiliza o SQL Server. SSB normalmente é configurado para utilizar a porta TCP 4022, mas pode utilizar uma porta diferente.  

-   **Nome da chave:** SQLDataFilePath  

    -   **Necessário:** Não  

    -   **Valores:** <*caminho do ficheiro. mdb de base de dados*>  

    -   **Detalhes:** Especifica uma localização alternativa para criar o ficheiro. mdb de base de dados.  

-   **Nome da chave:** SQLLogFilePath  

    -   **Necessário:** Não  

    -   **Valores:** <*caminho do ficheiro. ldf de base de dados*>  

    -   **Detalhes:** Especifica uma localização alternativa para criar o ficheiro. ldf de base de dados.  

**CloudConnectorOptions**  

-   **Nome da chave:** CloudConnector  

    -   **Necessário:** Sim  

    -   **Valores:** 0 ou 1  

         0 = fazer não instalar  

         1 = instalar  

    -   **Detalhes:** Especifica se pretende instalar um ponto de ligação de serviço neste site. Porque o ponto de ligação de serviço só pode ser instalado no site de nível superior de uma hierarquia, este valor tem de ser **0** para um site primário subordinado.  

-   **Nome da chave:** CloudConnectorServer  

    -   **Necessário:** É necessário quando **CloudConnector** é igual a 1  

    -   **Valores:** <*o servidor de ponto de ligação de serviço FQDN*>  

    -   **Detalhes:** Especifica o FQDN do servidor que irá alojar a função de sistema de sites de ponto de ligação de serviço.  

-   **Nome da chave:** UseProxy  

    -   **Necessário:** É necessário quando **CloudConnector** é igual a 1  

    -   **Valores:** 0 ou 1  

         0 = fazer não instalar  

         1 = instalar  

    -   **Detalhes:** Especifica se o ponto de ligação utiliza um servidor proxy.  

-   **Nome da chave:** ProxyName  

    -   **Necessário:** É necessário quando **UseProxy** é igual a 1  

    -   **Valores:** <*FQDN do servidor Proxy*>  

    -   **Detalhes:** Especifica o FQDN do servidor proxy que utiliza o ponto de ligação de serviço.  

-   **Nome da chave:** ProxyPort  

    -   **Necessário:** É necessário quando **UseProxy** é igual a 1  

    -   **Valores:** <*número da porta*>  

    -   **Detalhes:** Especifica o número de porta a utilizar para a porta de proxy.  

### <a name="unattended-install-for-a-primary-site"></a>Instalação automática de um site primário  
Utilize os seguintes detalhes para instalar um site primário utilizando um ficheiro de script de instalação autônoma.  

**Identificação**  

-   **Nome da chave:** Action  

    -   **Necessário:** Sim  

    -   **Valores:** InstallPrimarySite  

    -   **Detalhes:** Instala um site primário.  

-   **Nome da chave:** CDLatest  

    -   **Necessário:** Sim – apenas quando utilizar suportes de dados do CD. Pasta mais recente.    

    -   **Valores:** 1-qualquer valor diferente de 1 é considerado como não use o CD. Mais recente.

    -   **Detalhes:** O script tem de incluir esta chave e valor ao executar a configuração do suporte de dados num CD. Pasta mais recente com o objetivo de instalação de um site de administração central ou primário ou a recuperar um site de administração central ou primário. Este valor informa o programa de configuração que o suporte de dados de formulário CD. Está a ser utilizada a versão mais recente.

**Opções**  

-   **Nome da chave:** ProductID  

    -   **Necessário:** Sim  

    -   **Valores:** <*xxxxx-xxxxx-xxxxx-xxxxx-xxxxx*> *ou* Eval  

    -   **Detalhes:** Especifica a chave de produto de instalação do Configuration Manager, incluindo os traços. Introduza **Eval** para instalar a versão de avaliação do Configuration Manager.  

-   **Nome da chave:** SiteCode  

    -   **Necessário:** Sim  

    -   **Valores:** <*código do Site*>  

    -   **Detalhes:** Especifica três carateres alfanuméricos que identificam o site na sua hierarquia.  

-   **Nome da chave:** SiteName  

    -   **Necessário:** Sim  

    -   **Valores:** <*nome do Site*>  

    -   **Detalhes:** Especifica o nome para este site.  

-   **Nome da chave:** SMSInstallDir  

    -   **Necessário:** Sim  

    -   **Valores:** <*caminho de instalação do Configuration Manager*>

    -   **Detalhes:** Especifica a pasta de instalação para os ficheiros de programa do Configuration Manager.  

-   **Nome da chave:** SDKServer  

    -   **Necessário:** Sim  

    -   **Valores:** <*FQDN do fornecedor de SMS*>  

    -   **Detalhes:** Especifica o FQDN do servidor que alojará o fornecedor de SMS. Pode configurar Fornecedores de SMS adicionais para o site após a instalação inicial.  

-   **Nome da chave:** PrerequisiteComp  

    -   **Necessário:** Sim  

    -   **Valores:** 0 ou 1  

         0 = download  

         1 = já transferido  

    -   **Detalhes:** Especifica se os ficheiros de pré-requisitos de configuração já foram transferidos. Por exemplo, se utilizar o valor **0**, configuração transfere os ficheiros.  

-   **Nome da chave:** PrerequisitePath  

    -   **Necessário:** Sim  

    -   **Valores:** <*caminho para ficheiros de pré-requisitos de configuração*>  

    -   **Detalhes:** Especifica o caminho para os ficheiros de pré-requisitos de configuração. Consoante a **PrerequisiteComp** valor, a configuração utiliza este caminho para armazenar os ficheiros transferidos ou localizar anteriormente os ficheiros transferidos.  

-   **Nome da chave:** AdminConsole  

    -   **Necessário:** Sim  

    -   **Valores:** 0 ou 1  

         0 = fazer não instalar  

         1 = instalar  

    -   **Detalhes:** Especifica se pretende instalar a consola do Configuration Manager.  

-   **Nome da chave:** JoinCEIP  
    > [!Note]  
    > A partir do Configuration Manager versão 1802 a funcionalidade CEIP é removida do produto.

    -   **Necessário:** Sim  

    -   **Valores:** 0 ou 1  

         0 = fazer não aderir  

         1 = associação  

    -   **Detalhes:** Especifica se pretende aderir ao CEIP.  

-   **Nome da chave:** ManagementPoint  

    -   **Necessário:** Não  

    -   **Valores:** <*FQDN do servidor do site do ponto de gestão*>  

    -   **Detalhes:** Especifica o FQDN do servidor que irá alojar a função de sistema de sites de ponto de gestão.  

-   **Nome da chave:** ManagementPointProtocol  

    -   **Necessário:** Não  

    -   **Valores:** HTTPS *ou* HTTP  

    -   **Detalhes:** Especifica o protocolo a utilizar para o ponto de gestão.  

-   **Nome da chave:** DistributionPoint  

    -   **Necessário:** Não  

    -   **Valores:** <*o servidor de site de ponto de distribuição FQDN*>  

    -   **Detalhes:** Especifica o protocolo a utilizar para o ponto de distribuição.  

-   **Nome da chave:** DistributionPointProtocol  

    -   **Necessário:** Não  

    -   **Valores:** HTTPS *ou* HTTP  

    -   **Detalhes:** Especifica o protocolo a utilizar para o ponto de distribuição.  

-   **Nome da chave:** RoleCommunicationProtocol  

    -   **Necessário:** Sim  

    -   **Valores:** EnforceHTTPS *ou* HTTPorHTTPS  

    -   **Detalhes:** Especifica se pretende configurar todos os sistemas de sites para aceitar apenas comunicações HTTPS de clientes ou para o método de comunicação para ser configurado para cada função de sistema de sites. Quando seleciona **EnforceHTTPS**, computador cliente tem de ter um certificado de infraestrutura de chaves públicas (PKI) válido para autenticação de cliente.  

-   **Nome da chave:** ClientsUsePKICertificate  

    -   **Necessário:** Sim  

    -   **Valores:** 0 ou 1  

         0 = fazer não utilizar  

         1 = utilizar  

    -   **Detalhes:** Especifica se os clientes utilizam um certificado PKI de cliente para comunicar com funções de sistema de sites.  

-   **Nome da chave:** AddServerLanguages  

    -   **Necessário:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK, or ZHH  

    -   **Detalhes:** Especifica os idiomas do servidor que estarão disponíveis para a consola do Configuration Manager, relatórios e objetos do Configuration Manager. O inglês está disponível por predefinição.  

-   **Nome da chave:** AddClientLanguages  

    -   **Necessário:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK, or ZHH  

    -   **Detalhes:** Especifica os idiomas que estarão disponíveis para os computadores cliente. O inglês está disponível por predefinição.  

-   **Nome da chave:** DeleteServerLanguages  

    -   **Necessário:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK, or ZHH  

    -   **Detalhes:** Modifica um site depois de ser instalado. Especifica os idiomas a remover e que já não estará disponível para a consola do Configuration Manager, relatórios e objetos do Configuration Manager. O inglês está disponível por predefinição e não pode ser removido.  

-   **Nome da chave:** DeleteClientLanguages  

    -   **Necessário:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK, or ZHH  

    -   **Detalhes:** Modifica um site depois de ser instalado. Especifica os idiomas a remover e que já não estarão disponível para computadores cliente. O inglês está disponível por predefinição e não pode ser removido.  

-   **Nome da chave:** MobileDeviceLanguage  

    -   **Necessário:** Sim  

    -   **Valores:** 0 ou 1  

         0 = fazer não instalar  

         1 = instalar  

    -   **Detalhes:** Especifica se estão instalados os idiomas de cliente do dispositivo móvel.  

**SQLConfigOptions**  

-   **Nome da chave:** SQLServerName  

    -   **Necessário:** Sim  

    -   **Valores:** <*nome do SQL server*>  

    -   **Detalhes:** Especifica o nome do servidor ou instância em cluster que está a executar o SQL Server e que irá alojar a base de dados do site.  

-   **Nome da chave:** databaseName  

    -   **Necessário:** Sim  

    -   **Valores:** <*nome de base de dados do Site*> ou <*nome da instância*>\\<*nome de base de dados do Site*>  

    -   **Detalhes:** Especifica o nome da base de dados do SQL Server para criar ou a base de dados do SQL Server a utilizar ao instalar a base de dados do site primário.  

        > [!IMPORTANT]  
        >  Se não utilizar a instância predefinida, tem de especificar o nome da instância e o nome de base de dados do site.  

-   **Nome da chave:** SQLSSBPort  

    -   **Necessário:** Não  

    -   **Valores:** <*número da porta SSB*>  

    -   **Detalhes:** Especifica a porta do SSB que utiliza o SQL Server. SSB normalmente é configurado para utilizar a porta TCP 4022, mas pode utilizar uma porta diferente.  

-   **Nome da chave:** SQLDataFilePath  

    -   **Necessário:** Não  

    -   **Valores:** <*caminho do ficheiro. mdb de base de dados*>  

    -   **Detalhes:** Especifica uma localização alternativa para criar o ficheiro. mdb de base de dados.  

-   **Nome da chave:** SQLLogFilePath  

    -   **Necessário:** Não  

    -   **Valores:** <*caminho do ficheiro. ldf de base de dados*>  

    -   **Detalhes:** Especifica uma localização alternativa para criar o ficheiro. ldf de base de dados.  

**HierarchyExpansionOption**  

-   **Nome da chave:** CCARSiteServer  

    -   **Necessário:** Não  

    -   **Valores:** <*FQDN do site de Administração Central*>  

    -   **Detalhes:** Especifica o site de administração central que um site primário liga para quando se associa à hierarquia do Configuration Manager. Especifica o site de administração central durante a configuração.  

-   **Nome da chave:** CASRetryInterval  

    -   **Necessário:** Não  

    -   **Valores:** <*Interval*>  

    -   **Detalhes:** Especifica o intervalo entre tentativas (em minutos) para estabelecer uma ligação ao site de administração central, após a ligação falha. Por exemplo, se a ligação ao site de administração central falhar, o site primário aguarda o número de minutos que especificar para o **CASRetryInterval** valor e, em seguida, reattempts a ligação.  

-   **Nome da chave:** WaitForCASTimeout  

    -   **Necessário:** Não  

    -   **Valores:** <*Timeout*>  

         Um valor de **0** para **100**  

    -   **Detalhes:** Especifica o valor de tempo limite máximo (em minutos) para um site primário ligar ao site de administração central. Por exemplo, se um site primário não conseguir ligar a um site de administração central, o site primário tentará novamente a ligação ao site de administração central com base na **CASRetryInterval** valor até a  **WaitForCASTimeout** período for atingido. Pode especificar um valor de **0** ao **100**.  

**CloudConnectorOptions**  

-   **Nome da chave:** CloudConnector  

    -   **Necessário:** Sim  

    -   **Valores:** 0 ou 1  

         0 = fazer não instalar  

         1 = instalar  

    -   **Detalhes:** Especifica se pretende instalar um ponto de ligação de serviço neste site. Porque o ponto de ligação de serviço só pode ser instalado no site de nível superior de uma hierarquia, este valor tem de ser **0** para um site primário subordinado.  

-   **Nome da chave:** CloudConnectorServer  

    -   **Necessário:** É necessário quando **CloudConnector** é igual a 1  

    -   **Valores:** <*o servidor de ponto de ligação de serviço FQDN*\>  

    -   **Detalhes:** Especifica o FQDN do servidor que irá alojar a função de sistema de sites de ponto de ligação de serviço.  

-   **Nome da chave:** UseProxy  

    -   **Necessário:** É necessário quando **CloudConnector** é igual a 1  

    -   **Valores:** 0 ou 1  

         0 = fazer não instalar  

         1 = instalar  

    -   **Detalhes:** Especifica se o ponto de ligação utiliza um servidor proxy.  

-   **Nome da chave:** ProxyName  

    -   **Necessário:** É necessário quando **UseProxy** é igual a 1  

    -   **Valores:** <*FQDN do servidor Proxy*>  

    -   **Detalhes:** Especifica o FQDN do servidor proxy que utiliza o ponto de ligação de serviço.  

-   **Nome da chave:** ProxyPort  

    -   **Necessário:** É necessário quando **UseProxy** é igual a 1  

    -   **Valores:** <*número da porta*>  

    -   **Detalhes:** Especifica o número de porta a utilizar para a porta de proxy.  

### <a name="unattended-recovery-for-a-central-administration-site"></a>Recuperação automática de um site de administração central  
 Utilize os seguintes detalhes para recuperar um site de administração central utilizando um ficheiro de script de instalação autônoma.  

**Identificação**  

-   **Nome da chave:** Action  

    -   **Necessário:** Sim  

    -   **Valores:** RecoverCCAR  

    -   **Detalhes:** Recupera um site de administração central.  

-   **Nome da chave:** CDLatest  

    -   **Necessário:** Sim – apenas quando utilizar suportes de dados do CD. Pasta mais recente.    

    -   **Valores:** 1-qualquer valor diferente de 1 é considerado como não use o CD. Mais recente.

    -   **Detalhes:** O script tem de incluir esta chave e valor ao executar a configuração do suporte de dados num CD. Pasta mais recente com o objetivo de instalação de um site de administração central ou primário ou a recuperar um site de administração central ou primário. Este valor informa o programa de configuração que o suporte de dados de formulário CD. Está a ser utilizada a versão mais recente.

**RecoveryOptions**  

-   **Nome da chave:** ServerRecoveryOptions  

    -   **Necessário:** Sim  

    -   **Valores:** 1, 2 ou 4  

         1 = servidor de site de recuperação e SQL Server.  

         2 = Recuperar apenas servidor de site.  

         4 = Recuperar apenas SQL Server.  

    -   **Detalhes:** Especifica se a configuração recupera o servidor do site, do SQL Server ou ambos. As chaves associadas são necessárias quando definir o seguinte valor para o **ServerRecoveryOptions** definição:  

        -   Value = 1: Tem a opção de especificar um valor para o **SiteServerBackupLocation** chave para recuperar o site utilizando uma cópia de segurança do site. Se não especificar um valor, o site será reinstalado sem ser restaurado a partir de um conjunto de cópias de segurança.  

        -   Valor = 2: Tem a opção de especificar um valor para o **SiteServerBackupLocation** chave para recuperar o site utilizando uma cópia de segurança do site. Se não especificar um valor, o site será reinstalado sem ser restaurado a partir de um conjunto de cópias de segurança.  

        -   Value = 4: A chave **BackupLocation** é obrigatória se configurar o valor **10** para a chave **DatabaseRecoveryOptions** , para restaurar a base de dados do site a partir de uma cópia de segurança.  

-   **Nome da chave:** DatabaseRecoveryOptions  

    -   **Necessário:** Esta chave é necessária quando a definição **ServerRecoveryOptions** tem o valor **1** ou **4**  

    -   **Valores:** 10, 20, 40 ou 80  

         10 = Restaurar a base de dados do site a partir de cópia de segurança.  

         20 = Utilizar uma base de dados do site que tenha sido recuperada manualmente utilizando outro método.  

         40 = Criar uma nova base de dados para o site. Utilize esta opção quando não estiver disponível nenhuma cópia de segurança da base de dados do site. Os dados globais e de site são recuperados através da replicação a partir de outros sites.  

         80 = a recuperação de base de dados de ignorar.  

    -   **Detalhes:** Especifica a forma como a configuração recupera a base de dados no SQL Server.  

-   **Nome da chave:** ReferenceSite  

    -   **Necessário:** Esta chave é obrigatória se a definição **DatabaseRecoveryOptions** tiver o valor **40**.  

    -   **Valores:** <*FQDN do site de referência*>  

    -   **Detalhes:** Especifica o site primário de referência utilizado pelo site de administração central para recuperar dados globais se a cópia de segurança da base de dados é mais antiga do que o período de retenção do registo de alterações ou quando recuperar o site sem uma cópia de segurança.  

         Quando não especificar um site de referência e a cópia de segurança é mais antiga do que o período de retenção do registo de alterações, todos os sites primários serão reinicializados com os dados restaurados a partir do site de administração central.  

         Quando não especificar um site de referência e a cópia de segurança estiver dentro do período de retenção do registo de alterações, apenas as alterações que são efetuadas após a cópia de segurança são replicadas a partir de sites primários. Quando existirem alterações de diferentes sites primários em conflito, o site de administração central utilizará a primeira que receber.  

-   **Nome da chave:** SiteServerBackupLocation  

    -   **Necessário:** Não  

    -   **Valores:** <*caminho para o conjunto de cópia de segurança de servidor do site*>  

    -   **Detalhes:** Especifica o caminho para o conjunto de cópia de segurança de servidor de site. Esta chave é opcional se a definição **ServerRecoveryOptions** tiver o valor **1** ou **2**. Especifique um valor para a chave **SiteServerBackupLocation** para recuperar o site com uma cópia de segurança do mesmo. Se não especificar um valor, o site será reinstalado sem ser restaurado a partir de um conjunto de cópias de segurança.  

-   **Nome da chave:** BackupLocation  

    -   **Necessário:** Esta chave é necessária quando configura o valor **1** ou **4** para o **ServerRecoveryOptions** chave e configura o valor **10** para o **DatabaseRecoveryOptions** chave.  

    -   **Valores:** <*caminho para o conjunto de cópia de segurança de base de dados do site*>  

    -   **Detalhes:** Especifica o caminho para o conjunto de cópia de segurança de base de dados de site.  

**Opções**  

-   **Nome da chave:** ProductID  

    -   **Necessário:** Sim  

    -   **Valores:** <*xxxxx-xxxxx-xxxxx-xxxxx-xxxxx*> *ou* Eval  

    -   **Detalhes:** Especifica a chave de produto de instalação do Configuration Manager, incluindo os traços. Introduza **Eval** para instalar a versão de avaliação do Configuration Manager.  

-   **Nome da chave:** SiteCode  

    -   **Necessário:** Sim  

    -   **Valores:** <*código do Site*>  

    -   **Detalhes:** Especifica três carateres alfanuméricos que identificam o site na sua hierarquia. Especifique o código do site que o site utilizava antes da falha.

-   **Nome da chave:** SiteName  

    -   **Necessário:** Não  

    -   **Valores:** <*nome do Site*>  

    -   **Detalhes:** Especifica o nome para este site.  

-   **Nome da chave:** SMSInstallDir  

    -   **Necessário:** Sim  

    -   **Valores:** <*caminho de instalação do Configuration Manager*>  

    -   **Detalhes:** Especifica a pasta de instalação para os ficheiros de programa do Configuration Manager.  

-   **Nome da chave:** SDKServer  

    -   **Necessário:** Sim  

    -   **Valores:** <*FQDN do fornecedor de SMS*>  

    -   **Detalhes:** Especifica o FQDN do servidor que aloja o fornecedor de SMS. Especifique o servidor que alojava o fornecedor de SMS antes da falha.  

         Pode configurar Fornecedores de SMS adicionais para o site após a instalação inicial. Para obter mais informações sobre o fornecedor de SMS, consulte [planear o fornecedor de SMS para o System Center Configuration Manager](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

-   **Nome da chave:** PrerequisiteComp  

    -   **Necessário:** Sim  

    -   **Valores:** 0 ou 1  

         0 = download  

         1 = já transferido  

    -   **Detalhes:** Especifica se os ficheiros de pré-requisitos de configuração já foram transferidos. Por exemplo, se utilizar o valor **0**, configuração transfere os ficheiros.  

-   **Nome da chave:** PrerequisitePath  

    -   **Necessário:** Sim  

    -   **Valores:** <*caminho para ficheiros de pré-requisitos de configuração*>  

    -   **Detalhes:** Especifica o caminho para os ficheiros de pré-requisitos de configuração. Consoante a **PrerequisiteComp** valor, a configuração utiliza este caminho para armazenar os ficheiros transferidos ou localizar anteriormente os ficheiros transferidos.  

-   **Nome da chave:** AdminConsole  

    -   **Necessário:** Esta chave é necessária, exceto se a definição **ServerRecoveryOptions** tiver o valor **4**.  

    -   **Valores:** 0 ou 1  

         0 = fazer não instalar  

         1 = instalar  

    -   **Detalhes:** Especifica se pretende instalar a consola do Configuration Manager.  

-   **Nome da chave:** JoinCEIP  
    > [!Note]  
    > A partir do Configuration Manager versão 1802 a funcionalidade CEIP é removida do produto.

    -   **Necessário:** Sim  

    -   **Valores:** 0 ou 1  

         0 = fazer não aderir  

         1 = associação  

    -   **Detalhes:** Especifica se pretende aderir ao CEIP.  

**SQLConfigOptions**  

-   **Nome da chave:** SQLServerName  

    -   **Necessário:** Sim  

    -   **Valores:** <*nome do SQL server*>  

    -   **Detalhes:** Especifica o nome do servidor ou instância em cluster que está a executar o SQL Server e que aloja a base de dados do site. Especifique o mesmo servidor que alojava a base de dados do site antes da falha.  

-   **Nome da chave:** databaseName  

    -   **Necessário:** Sim  

    -   **Valores:** <*nome de base de dados do Site*> ou <*nome da instância*>\\<*nome de base de dados do Site*>  

    -   **Detalhes:** Especifica o nome da base de dados do SQL Server para criar ou a base de dados do SQL Server a utilizar ao instalar a base de dados do site de administração central. Especifique o mesmo nome de base de dados que foi utilizado antes da falha.  

        > [!IMPORTANT]  
        >  Se não utilizar a instância predefinida, tem de especificar o nome da instância e o nome de base de dados do site.  

-   **Nome da chave:** SQLSSBPort  

    -   **Necessário:** Sim  

    -   **Valores:** <*número da porta SSB*>  

    -   **Detalhes:** Especifica a porta do SSB que utiliza o SQL Server. Normalmente, o SSB está configurado para utilizar a porta TCP 4022. Especifique a mesma porta SSB que era utilizada antes da falha.  

-   **Nome da chave:** SQLDataFilePath  

    -   **Necessário:** Não  

    -   **Valores:** <*caminho do ficheiro. mdb de base de dados*>  

    -   **Detalhes:** Especifica uma localização alternativa para criar o ficheiro. mdb de base de dados.  

-   **Nome da chave:** SQLLogFilePath  

    -   **Necessário:** Não  

    -   **Valores:** <*caminho do ficheiro. ldf de base de dados*>  

    -   **Detalhes:** Especifica uma localização alternativa para criar o ficheiro. ldf de base de dados.  

**CloudConnectorOptions**  

-   **Nome da chave:** CloudConnector  

    -   **Necessário:** Sim  

    -   **Valores:** 0 ou 1  

         0 = fazer não instalar  

         1 = instalar  

    -   **Detalhes:** Especifica se pretende instalar um ponto de ligação de serviço neste site. Porque o ponto de ligação de serviço só pode ser instalado no site de nível superior de uma hierarquia, este valor tem de ser **0** para um site primário subordinado.  

-   **Nome da chave:** CloudConnectorServer  

    -   **Necessário:** É necessário quando **CloudConnector** é igual a 1  

    -   **Valores:** <*o servidor de ponto de ligação de serviço FQDN*>  

    -   **Detalhes:** Especifica o FQDN do servidor que irá alojar a função de sistema de sites de ponto de ligação de serviço.  

-   **Nome da chave:** UseProxy  

    -   **Necessário:** É necessário quando **CloudConnector** é igual a 1  

    -   **Valores:** 0 ou 1  

         0 = fazer não instalar  

         1 = instalar  

    -   **Detalhes:** Especifica se o ponto de ligação utiliza um servidor proxy.  

-   **Nome da chave:** ProxyName  

    -   **Necessário:** É necessário quando **CloudConnector** é igual a 1  

    -   **Valores:** <*FQDN do servidor Proxy*>  

    -   **Detalhes:** Especifica o FQDN do servidor proxy que utiliza o ponto de ligação de serviço.  

-   **Nome da chave:** ProxyPort  

    -   **Necessário:** É necessário quando **CloudConnector** é igual a 1  

    -   **Valores:** <*número da porta*>  

    -   **Detalhes:** Especifica o número de porta a utilizar para a porta de proxy.  

### <a name="unattended-recovery-for-a-primary-site"></a>Recuperação automática de um site primário  
 Utilize os seguintes detalhes para recuperar um site primário utilizando um ficheiro de script de instalação autônoma.  

**Identificação**  

-   **Nome da chave:** Action  

    -   **Necessário:** Sim  

    -   **Valores:** <*RecoverPrimarySite*>  

    -   **Detalhes:** Recupera um site primário.  

-   **Nome da chave:** CDLatest  

    -   **Necessário:** Sim – apenas quando utilizar suportes de dados do CD. Pasta mais recente.    

    -   **Valores:** 1-qualquer valor diferente de 1 é considerado como não use o CD. Mais recente.

    -   **Detalhes:** O script tem de incluir esta chave e valor ao executar a configuração do suporte de dados num CD. Pasta mais recente com o objetivo de instalação de um site de administração central ou primário ou a recuperar um site de administração central ou primário. Este valor informa o programa de configuração que o suporte de dados de formulário CD. Está a ser utilizada a versão mais recente.    

**RecoveryOptions**  

-   **Nome da chave:** ServerRecoveryOptions  

    -   **Necessário:** Sim  

    -   **Valores:** 1, 2 ou 4  

         1 = servidor de site de recuperação e SQL Server.  

         2 = Recuperar apenas servidor de site.  

         4 = Recuperar apenas SQL Server.  

    -   **Detalhes:** Especifica se a configuração recupera o servidor do site, do SQL Server ou ambos. As chaves associadas são necessárias quando definir o seguinte valor para o **ServerRecoveryOptions** definição:  

        -   Value = 1: Tem a opção de especificar um valor para o **SiteServerBackupLocation** chave para recuperar o site utilizando uma cópia de segurança do site. Se não especificar um valor, o site será reinstalado sem ser restaurado a partir de um conjunto de cópias de segurança.  

        -   Valor = 2: Tem a opção de especificar um valor para o **SiteServerBackupLocation** chave para recuperar o site utilizando uma cópia de segurança do site. Se não especificar um valor, o site será reinstalado sem ser restaurado a partir de um conjunto de cópias de segurança.  

        -   Value = 4: A chave **BackupLocation** é obrigatória se configurar o valor **10** para a chave **DatabaseRecoveryOptions** , para restaurar a base de dados do site a partir de uma cópia de segurança.  

-   **Nome da chave:** DatabaseRecoveryOptions  

    -   **Necessário:** Esta chave é necessária quando a definição **ServerRecoveryOptions** tem o valor **1** ou **4**  

    -   **Valores:** 10, 20, 40 ou 80  

         10 = Restaurar a base de dados do site a partir de cópia de segurança.  

         20 = Utilizar uma base de dados do site que tenha sido recuperada manualmente utilizando outro método.  

         40 = Criar uma nova base de dados para o site. Utilize esta opção quando não estiver disponível nenhuma cópia de segurança da base de dados do site. Os dados globais e de site são recuperados através da replicação a partir de outros sites.  

         80 = a recuperação de base de dados de ignorar.  

    -   **Detalhes:** Especifica a forma como a configuração recupera a base de dados no SQL Server.  

-   **Nome da chave:** SiteServerBackupLocation  

    -   **Necessário:** Não  

    -   **Valores:** <*caminho para o conjunto de cópia de segurança de servidor do site*>  

    -   **Detalhes:**  

         Especifica o caminho para o conjunto de cópia de segurança de servidor de site. Esta chave é opcional se a definição **ServerRecoveryOptions** tiver o valor **1** ou **2**. Especifique um valor para a chave **SiteServerBackupLocation** para recuperar o site com uma cópia de segurança do mesmo. Se não especificar um valor, o site será reinstalado sem ser restaurado a partir de um conjunto de cópias de segurança.  

-   **Nome da chave:** BackupLocation  

    -   **Necessário:** Esta chave é necessária quando configura o valor **1** ou **4** para o **ServerRecoveryOptions** e configura um valor de **10** para o **DatabaseRecoveryOptions** chave.  

    -   **Valores:** <*caminho para o conjunto de cópia de segurança de base de dados do site*>  

    -   **Detalhes:** Especifica o caminho para o conjunto de cópia de segurança de base de dados de site.  

**Opções**  

-   **Nome da chave:** ProductID  

    -   **Necessário:** Sim  

    -   **Valores:** *xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* ou *Eval*  

    -   **Detalhes:** Especifica a chave de produto de instalação do Configuration Manager, incluindo os traços. Introduza **Eval** para instalar a versão de avaliação do Configuration Manager.  

-   **Nome da chave:** SiteCode  

    -   **Necessário:** Sim  

    -   **Valores:** <*código do Site*>  

    -   **Detalhes:** Especifica três carateres alfanuméricos que identificam o site na sua hierarquia. Especifique o código do site que o site utilizava antes da falha.

-   **Nome da chave:** SiteName  

    -   **Necessário:** Não  

    -   **Valores:** <*nome do Site*>  

    -   **Detalhes:** Especifica o nome para este site.  

-   **Nome da chave:** SMSInstallDir  

    -   **Necessário:** Sim  

    -   **Valores:** <*caminho de instalação do Configuration Manager*>  

    -   **Detalhes:** Especifica a pasta de instalação para os ficheiros de programa do Configuration Manager.  

-   **Nome da chave:** SDKServer  

    -   **Necessário:** Sim  

    -   **Valores:** <*FQDN do fornecedor de SMS*>  

    -   **Detalhes:** Especifica o FQDN do servidor que aloja o fornecedor de SMS. Especifique o servidor que alojava o fornecedor de SMS antes da falha. Configure fornecedores de SMS adicionais para o site após a instalação inicial. Para obter mais informações sobre o fornecedor de SMS, consulte [planear o fornecedor de SMS](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

-   **Nome da chave:** PrerequisiteComp  

    -   **Necessário:** Sim  

    -   **Valores:** 0 ou 1  

         0 = download  

         1 = já transferido  

    -   **Detalhes:** Especifica se os ficheiros de pré-requisitos de configuração já foram transferidos. Por exemplo, se utilizar o valor **0**, configuração transfere os ficheiros.  

-   **Nome da chave:** PrerequisitePath  

    -   **Necessário:** Sim  

    -   **Valores:** <*caminho para ficheiros de pré-requisitos de configuração*>  

    -   **Detalhes:** Especifica o caminho para os ficheiros de pré-requisitos de configuração. Consoante a **PrerequisiteComp** valor, a configuração utiliza este caminho para armazenar os ficheiros transferidos ou localizar anteriormente os ficheiros transferidos.  

-   **Nome da chave:** AdminConsole  

    -   **Necessário:** Esta chave é necessária, exceto se a definição **ServerRecoveryOptions** tiver o valor **4**.  

    -   **Valores:** 0 ou 1  

         0 = fazer não instalar  

         1 = instalar  

    -   **Detalhes:** Especifica se pretende instalar a consola do Configuration Manager.  

-   **Nome da chave:** JoinCEIP  
    > [!Note]  
    > A partir do Configuration Manager versão 1802 a funcionalidade CEIP é removida do produto.

    -   **Necessário:** Sim  

    -   **Valores:** 0 ou 1  

         0 = fazer não aderir  

         1 = associação  

    -   **Detalhes:** Especifica se pretende aderir ao CEIP.  

**SQLConfigOptions**  

-   **Nome da chave:** SQLServerName  

    -   **Necessário:** Sim  

    -   **Valores:** <*nome do SQL server*>  

    -   **Detalhes:** Especifica o nome do servidor ou instância em cluster que está a executar o SQL Server e que aloja a base de dados do site. Especifique o mesmo servidor que alojava a base de dados do site antes da falha.  

-   **Nome da chave:** databaseName  

    -   **Necessário:** Sim  

    -   **Valores:** <*nome de base de dados do Site*> ou <*nome da instância*>\\<*nome de base de dados do Site*>

    -   **Detalhes:**  

         Especifica o nome da base de dados do SQL Server para criar ou a base de dados do SQL Server a utilizar ao instalar a base de dados do site de administração central. Especifique o mesmo nome de base de dados que foi utilizado antes da falha.  

        > [!IMPORTANT]  
        >  Se não utilizar a instância predefinida, tem de especificar o nome da instância e o nome de base de dados do site.  

-   **Nome da chave:** SQLSSBPort  

    -   **Necessário:** Sim  

    -   **Valores:** <*número da porta SSB*>  

    -   **Detalhes:** Especifica a porta do SSB que utiliza o SQL Server. Normalmente, o SSB está configurado para utilizar a porta TCP 4022. Especifique a mesma porta SSB que era utilizada antes da falha.  

-   **Nome da chave:** SQLDataFilePath  

    -   **Necessário:** Não  

    -   **Valores:** <*caminho do ficheiro. mdb de base de dados*>  

    -   **Detalhes:** Especifica uma localização alternativa para criar o ficheiro. mdb de base de dados.  

-   **Nome da chave:** SQLLogFilePath  

    -   **Necessário:** Não  

    -   **Valores:** <*caminho do ficheiro. ldf de base de dados*>  

    -   **Detalhes:** Especifica uma localização alternativa para criar o ficheiro. ldf de base de dados.  

**HierarchyExpansionOptions**  

-   **Nome da chave:** CCARSiteServer  

    -   **Necessário:** Ver detalhes.  

    -   **Valores:** <*código para o site de administração central do Site*>  

    -   **Detalhes:** Especifica o site de administração central ao qual um site primário liga quando se associa à hierarquia do Configuration Manager. Esta definição é necessária se o site primário estava ligado a um site de administração central antes da falha. Especifique o código do site que foi utilizado para o site de administração central antes da falha.  

-   **Nome da chave:** CASRetryInterval  

    -   **Necessário:** Não  

    -   **Valores:** <*Interval*>  

    -   **Detalhes:** Especifica o intervalo entre tentativas (em minutos) para estabelecer uma ligação ao site de administração central, após a ligação falha. Por exemplo, se a ligação ao site de administração central falhar, o site primário aguarda o número de minutos que especificar para o **CASRetryInterval** valor e, em seguida, tenta restabelecer a ligação.  

-   **Nome da chave:** WaitForCASTimeout  

    -   **Necessário:** Não  

    -   **Valores:** <*Timeout*>  

    -   **Detalhes:** Especifica o valor de tempo limite máximo (em minutos) para um site primário ligar ao site de administração central. Por exemplo, se um site primário não conseguir ligar a um site de administração central, o site primário tentará novamente a ligação ao site de administração central com base na **CASRetryInterval** valor até a  **WaitForCASTimeout** período for atingido. Pode especificar um valor de **0** ao **100**.  

**CloudConnectorOptions**  

-   **Nome da chave:** CloudConnector  

    -   **Necessário:** Sim  

    -   **Valores:** 0 ou 1  

         0 = fazer não instalar  

         1 = instalar  

    -   **Detalhes:** Especifica se pretende instalar um ponto de ligação de serviço neste site. Porque o ponto de ligação de serviço só pode ser instalado no site de nível superior de uma hierarquia, este valor tem de ser **0** para um site primário subordinado.  

-   **Nome da chave:** CloudConnectorServer  

    -   **Necessário:** É necessário quando **CloudConnector** é igual a 1  

    -   **Valores:** <*o servidor de ponto de ligação de serviço FQDN*>  

    -   **Detalhes:** Especifica o FQDN do servidor que irá alojar a função de sistema de sites de ponto de ligação de serviço.  

-   **Nome da chave:** UseProxy  

    -   **Necessário:** É necessário quando **CloudConnector** é igual a 1  

    -   **Valores:** 0 ou 1  

         0 = fazer não instalar  

         1 = instalar  

    -   **Detalhes:** Especifica se o ponto de ligação utiliza um servidor proxy.  

-   **Nome da chave:** ProxyName  

    -   **Necessário:** É necessário quando **CloudConnector** é igual a 1  

    -   **Valores:** <*FQDN do servidor Proxy*>  

    -   **Detalhes:** Especifica o FQDN do servidor proxy que utiliza o ponto de ligação de serviço.  

-   **Nome da chave:** ProxyPort  

    -   **Necessário:** É necessário quando **CloudConnector** é igual a 1  

    -   **Valores:** <*número da porta*>  

    -   **Detalhes:** Especifica o número de porta a utilizar para a porta de proxy.  
