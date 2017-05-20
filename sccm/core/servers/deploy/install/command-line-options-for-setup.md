---
title: "Configurar opções da linha de comandos | Documentos do Microsoft"
description: "Utilize informações neste artigo para configurar scripts ou para instalar o System Center Configuration Manager a partir de uma linha de comandos."
ms.custom: na
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0da167f1-52cf-4dfd-8f73-833ca3eb8478
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 04fe7b3e674287c4255563ab4a308e54d0b6c3aa
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="command-line-options-for-setup-in-system-center-configuration-manager"></a>Opções da linha de comandos para a configuração no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


 Utilize as seguintes informações para configurar scripts ou para instalar o System Center Configuration Manager a partir de uma linha de comandos.  

##  <a name="bkmk_setup"></a>Opções da linha de comandos para a configuração  
 **/ DESINSTALAR**  
 Desinstala o site. Tem de executar o programa de configuração a partir do computador do servidor do site.  

 **/ DONTSTARTSITECOMP**  
 Instala um site, mas impede que o serviço Gestor de componentes do Site iniciar. Até que o serviço Gestor de componentes do Site é iniciado, o site não está ativo. O Gestor de componentes do Site é responsável pela instalação e a paragem do serviço de início e de processos adicionais no site. Após a instalação do site estiver concluída, quando iniciar o serviço do Gestor de componentes do Site, instala o serviço SMS_Executive e os processos adicionais necessários para o site operar.  

 **/ OCULTO**  
 Oculta a interface de utilizador durante a configuração. Utilize esta opção apenas em conjunto com o **/SCRIPT** opção. O ficheiro de script automático tem de fornecer todas as opções necessárias ou a configuração falha.  

 **/ NOUSERINPUT**  
 Desativa a intervenção do utilizador durante a configuração, mas apresenta o Assistente de configuração. Utilize esta opção apenas em conjunto com o **/SCRIPT** opção. O ficheiro de script automático tem de fornecer todas as opções necessárias ou a configuração falha.  

 **/RESETSITE**  
 Efetua um site de reposição que repõe as contas de serviço e da base de dados para o site. Tem de executar a configuração a partir  **<* caminho de instalação do Configuration Manager*> \BIN\X64** no servidor do site. Para mais informações sobre a reposição do site, consulte o [executar uma reposição do site](../../../../core/servers/manage/modify-your-infrastructure.md#bkmk_reset) secção [modificar a infraestrutura do System Center Configuration Manager](../../../../core/servers/manage/modify-your-infrastructure.md).  

 **/ TESTDBUPGRADE <*nome da instância*>\\<*nome de base de dados*>**  
 Efetua um teste numa cópia de segurança da base de dados do site para garantir que a base de dados é capaz de uma atualização. Tem de fornecer o nome da instância e o nome de base de dados para a base de dados do site. Se especificar apenas o nome da base de dados, a configuração utiliza o nome da instância predefinido.  

> [!IMPORTANT]  
>  Não execute esta opção da linha de comandos na sua base de dados do site de produção. Com esta opção da linha de comandos na sua base de dados do site de produção atualiza a base de dados do site e foi inoperacional seu site.  

 **/ ATUALIZAR**  
 Executa uma atualização automática de um site. Quando utiliza **/ATUALIZAR**, tem de especificar a chave de produto, incluindo os traços (-). Além disso, tem de especificar o caminho para os ficheiros de pré-requisitos do programa de configuração anteriormente transferidos.  

 Exemplo: `setupwpf.exe /UPGRADE xxxxx-xxxxx-xxxxx-xxxxx-xxxxx <path to external component files>`  

 Para obter mais informações sobre os ficheiros de pré-requisitos de configuração, consulte o artigo [dispositivo de transferência da configuração](setup-downloader.md).  

 **/ SCRIPT <*caminho do script de configuração*>**  
 Efetua instalações automáticas. Um ficheiro de inicialização da configuração é necessário quando utiliza o **/SCRIPT** opção. Para obter mais informações sobre como executar a configuração automática, consulte o artigo [instalar sites que utilizem uma linha de comandos](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md).  

 **/ SDKINST <*FQDN do fornecedor de SMS*>**  
 Instala o fornecedor de SMS no computador especificado. Tem de fornecer o nome de domínio completamente qualificado (FQDN) para o computador do fornecedor de SMS. Para mais informações sobre o fornecedor de SMS, consulte o artigo [planear o fornecedor de SMS para o System Center Configuration Manager](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

 **/ SDKDEINST <*FQDN do fornecedor de SMS*>**  
 Desinstala o fornecedor de SMS no computador especificado. Tem de fornecer o FQDN para o computador do fornecedor de SMS.  

 **/ /MANAGELANGS <*caminho do script de idioma*>**  
 Gere os idiomas que estão instalados num site anteriormente instalado. Para utilizar esta opção, tem de executar a configuração a partir  **<* caminho de instalação do Configuration Manager*> \BIN\X64** no servidor do site e fornecer a localização para o ficheiro de script de idioma que contém as definições de idioma. Para obter mais informações sobre as opções de idioma disponíveis no ficheiro de script de configuração de idiomas, consulte o artigo [opções da linha de comandos para gerir idiomas](#bkmk_Lang) neste tópico.  

##  <a name="bkmk_Lang"></a>Opções da linha de comandos para gerir idiomas  
 **Identificação**  

-   **Nome da chave:** Ação  

    -   **Necessário:** Sim  

    -   **Valores:** ManageLanguages  

    -   **Detalhes:** Gere o servidor, o cliente e o suporte de idiomas de cliente móvel num site.  

**Opções**  

-   **Nome da chave:** AddServerLanguages  

    -   **Necessário:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Detalhes:** Especifica os idiomas do servidor que estarão disponíveis para a consola do Configuration Manager, relatórios e objetos do Configuration Manager. O inglês está disponível por predefinição.  

-   **Nome da chave:** AddClientLanguages  

    -   **Necessário:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Detalhes:** Especifica os idiomas que estarão disponíveis para os computadores cliente. O inglês está disponível por predefinição.  

-   **Nome da chave:** DeleteServerLanguages  

    -   **Necessário:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Detalhes:** Especifica os idiomas a remover e que já não estará disponível para a consola do Configuration Manager, relatórios e objetos do Configuration Manager. O inglês está disponível por predefinição e não pode ser removido.  

-   **Nome da chave:** DeleteClientLanguages  

    -   **Necessário:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Detalhes:** Especifica os idiomas a remover e que já não estará disponível para computadores cliente. O inglês está disponível por predefinição e não pode ser removido.  

-   **Nome da chave:** MobileDeviceLanguage  

    -   **Necessário:** Sim  

    -   **Valores:** 0 ou 1  

         0 = efetue não instalar  

         1 = instalação  

    -   **Detalhes:** Especifica se os idiomas de cliente do dispositivo móvel são instalados.  

-   **Nome da chave:** PrerequisiteComp  

    -   **Necessário:** Sim  

    -   **Valores:** 0 ou 1  

         0 = transferência  

         1 = Already transferido  

    -   **Detalhes:** Especifica se os ficheiros de pré-requisitos de configuração já foram transferidos. Por exemplo, se utilizar um valor de **0**, a configuração transfere os ficheiros.  

-   **Nome da chave:** PrerequisitePath  

    -   **Necessário:** Sim  

    -   **Valores:** <*caminho para ficheiros de pré-requisitos do programa de configuração*>  

    -   **Detalhes:** Especifica o caminho para os ficheiros de pré-requisitos do programa de configuração. Conforme o valor de **PrerequisiteComp** , a Configuração utiliza este caminho para armazenar os ficheiros transferidos ou localizar os ficheiros transferidos anteriormente.  

##  <a name="bkmk_Unattended"></a>Chaves de ficheiro de script de configuração automáticas  
 Utilize as secções seguintes para o ajudar a criar o script para a configuração automática. As listas de mostram as chaves de script de configuração disponíveis, os valores correspondentes, se são necessárias, que tipo de instalação são utilizadas e uma descrição breve da chave.  

### <a name="unattended-install-for-a-central-administration-site"></a>Instalação autónoma do site de administração central  
 Utilize as seguintes informações para instalar um site de administração central utilizando um ficheiro de script de configuração automática.  

**Identificação**  

-   **Nome da chave:** Ação  

    -   **Necessário:** Sim  

    -   **Valores:** InstallCAS  

    -   **Detalhes:** Instala um site de administração central.  

-   **Nome da chave:** CDLatest  

    -   **Necessário:** Sim – apenas quando utilizar suportes de dados a partir do CD. Pasta mais recente.    

    -   **Valores:** 1. qualquer valor diferente de 1 é considerada como não estar a utilizar o CD. Mais recente.

    -   **Detalhes:** O script tem de incluir este valor e chave quando executa a configuração a partir do suporte no CD. Pasta mais recente para efeitos de instalação de um site primário ou de administração central ou a recuperar um site primário ou de administração central. Este valor informa o programa de configuração que o suporte de dados de formulário CD. Está a ser utilizada a versão mais recente.

**Opções**  

-   **Nome da chave:** Iddoproduto  

    -   **Necessário:** Sim  

    -   **Valores:** <*xxxxx-xxxxx-xxxxx-xxxxx-xxxxx*> *ou* aval  

    -   **Detalhes:** Especifica a chave de produto de instalação do Configuration Manager, incluindo os traços. Introduza **Eval** para instalar a versão de avaliação do Configuration Manager.  

-   **Nome da chave:** Código do site  

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

         0 = transferência  

         1 = Already transferido  

    -   **Detalhes:** Especifica se os ficheiros de pré-requisitos de configuração já foram transferidos. Por exemplo, se utilizar um valor de **0**, configuração irá transferir os ficheiros.  

-   **Nome da chave:** PrerequisitePath  

    -   **Necessário:** Sim  

    -   **Valores:** <*caminho para ficheiros de pré-requisitos do programa de configuração*>  

    -   **Detalhes:** Especifica o caminho para os ficheiros de pré-requisitos do programa de configuração. Conforme o valor de **PrerequisiteComp** , a Configuração utiliza este caminho para armazenar os ficheiros transferidos ou localizar os ficheiros transferidos anteriormente.  

-   **Nome da chave:** AdminConsole  

    -   **Necessário:** Sim  

    -   **Valores:** 0 ou 1  

         0 = efetue não instalar  

         1 = instalação  

    -   **Detalhes:** Especifica se pretende instalar a consola do Configuration Manager.  

-   **Nome da chave:** JoinCEIP  

    -   **Necessário:** Sim  

    -   **Valores:** 0 ou 1  

         0 = efetue não aderir  

         1 = associação  

    -   **Detalhes:** Especifica se pretende aderir o programa de melhoramento da experiência do cliente (PMEC).  

-   **Nome da chave:** AddServerLanguages  

    -   **Necessário:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Detalhes:** Especifica os idiomas do servidor que estarão disponíveis para a consola do Configuration Manager, relatórios e objetos do Configuration Manager. O inglês está disponível por predefinição.  

-   **Nome da chave:** AddClientLanguages  

    -   **Necessário:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Detalhes:** Especifica os idiomas que estarão disponíveis para os computadores cliente. O inglês está disponível por predefinição.  

-   **Nome da chave:** DeleteServerLanguages  

    -   **Necessário:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Detalhes:** Modifica um site após a respetiva instalação. Especifica os idiomas a remover e que já não estará disponível para a consola do Configuration Manager, relatórios e objetos do Configuration Manager. O inglês está disponível por predefinição e não pode ser removido.  

-   **Nome da chave:** DeleteClientLanguages  

    -   **Necessário:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Detalhes:** Modifica um site após a respetiva instalação. Especifica os idiomas a remover e que já não estará disponível para computadores cliente. O inglês está disponível por predefinição e não pode ser removido.  

-   **Nome da chave:** MobileDeviceLanguage  

    -   **Necessário:** Sim  

    -   **Valores:** 0 ou 1  

         0 = efetue não instalar  

         1 = instalação  

    -   **Detalhes:** Especifica se os idiomas de cliente do dispositivo móvel são instalados.  

**SQLConfigOptions**  

-   **Nome da chave:** SQLServerName  

    -   **Necessário:** Sim  

    -   **Valores:** <*nome do SQL Server*>  

    -   **Detalhes:** Especifica o nome do servidor ou instância em cluster que está a executar o SQL Server e que irá alojar a base de dados do site.  

-   **Nome da chave:** DatabaseName  

    -   **Necessário:** Sim  

    -   **Valores:** <*nome de base de dados do Site*> ou <*nome da instância*>\\<*nome de base de dados do Site*>  

    -   **Detalhes:** Especifica o nome da base de dados do SQL Server para criar ou a base de dados do SQL Server a utilizar para instalar a base de dados do site de administração central.  

        > [!IMPORTANT]  
        >  Se não utilizar a instância predefinida, terá de especificar o nome da instância e o nome da base de dados do site.  

-   **Nome da chave:** SQLSSBPort  

    -   **Necessário:** Não  

    -   **Valores:** <*número de porta do SSB*>  

    -   **Detalhes:** Especifica a porta do SQL Server Service Broker (SSB) que utiliza o SQL Server. SSB normalmente está configurado para utilizar a porta TCP 4022, mas pode utilizar uma porta diferente.  

-   **Nome da chave:** SQLDataFilePath  

    -   **Necessário:** Não  

    -   **Valores:** <*caminho do ficheiro. mdb de base de dados*>  

    -   **Detalhes:** Especifica uma localização alternativa para criar o ficheiro. mdb de base de dados.  

-   **Nome da chave:** SQLLogFilePath  

    -   **Necessário:** Não  

    -   **Valores:** <*caminho do ficheiro. ldf da base de dados*>  

    -   **Detalhes:** Especifica uma localização alternativa para criar o ficheiro. ldf da base de dados.  

**CloudConnectorOptions**  

-   **Nome da chave:** CloudConnector  

    -   **Necessário:** Sim  

    -   **Valores:** 0 ou 1  

         0 = efetue não instalar  

         1 = instalação  

    -   **Detalhes:** Especifica se deve instalar um ponto de ligação de serviço neste site. Uma vez que o ponto de ligação de serviço só pode ser instalado no site de nível superior de uma hierarquia, este valor tem de ser **0** para um site primário subordinado.  

-   **Nome da chave:** CloudConnectorServer  

    -   **Necessário:** Obrigatório quando **CloudConnector** é igual a 1  

    -   **Valores:** <*o servidor de ponto de ligação de serviço FQDN*>  

    -   **Detalhes:** Especifica o FQDN do servidor que irá alojar a função de sistema de sites de ponto de ligação de serviço.  

-   **Nome da chave:** UseProxy  

    -   **Necessário:** Obrigatório quando **CloudConnector** é igual a 1  

    -   **Valores:** 0 ou 1  

         0 = efetue não instalar  

         1 = instalação  

    -   **Detalhes:** Especifica se o ponto de ligação de serviço irá utilizar um servidor proxy.  

-   **Nome da chave:** ProxyName  

    -   **Necessário:** Obrigatório quando **UseProxy** é igual a 1  

    -   **Valores:** <*FQDN do servidor de Proxy*>  

    -   **Detalhes:** Especifica o FQDN do servidor proxy que será utilizado pela função de sistema de sites de ponto de ligação de serviço.  

-   **Nome da chave:** /Proxyport  

    -   **Necessário:** Obrigatório quando **UseProxy** é igual a 1  

    -   **Valores:** <*número da porta*>  

    -   **Detalhes:** Especifica o número de porta a utilizar para a porta de proxy.  

### <a name="unattended-install-for-a-primary-site"></a>Instalação autónoma para um site primário  
Utilize as seguintes informações para instalar um site primário utilizando um ficheiro de script de configuração automática.  

**Identificação**  

-   **Nome da chave:** Ação  

    -   **Necessário:** Sim  

    -   **Valores:** InstallPrimarySite  

    -   **Detalhes:** Instala um site primário.  

-   **Nome da chave:** CDLatest  

    -   **Necessário:** Sim – apenas quando utilizar suportes de dados a partir do CD. Pasta mais recente.    

    -   **Valores:** 1. qualquer valor diferente de 1 é considerada como não estar a utilizar o CD. Mais recente.

    -   **Detalhes:** O script tem de incluir este valor e chave quando executa a configuração a partir do suporte no CD. Pasta mais recente para efeitos de instalação de um site primário ou de administração central ou a recuperar um site primário ou de administração central. Este valor informa o programa de configuração que o suporte de dados de formulário CD. Está a ser utilizada a versão mais recente.

**Opções**  

-   **Nome da chave:** Iddoproduto  

    -   **Necessário:** Sim  

    -   **Valores:** <*xxxxx-xxxxx-xxxxx-xxxxx-xxxxx*> *ou* aval  

    -   **Detalhes:** Especifica a chave de produto de instalação do Configuration Manager, incluindo os traços. Introduza **Eval** para instalar a versão de avaliação do Configuration Manager.  

-   **Nome da chave:** Código do site  

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

         0 = transferência  

         1 = Already transferido  

    -   **Detalhes:** Especifica se os ficheiros de pré-requisitos de configuração já foram transferidos. Por exemplo, se utilizar um valor de **0**, configuração irá transferir os ficheiros.  

-   **Nome da chave:** PrerequisitePath  

    -   **Necessário:** Sim  

    -   **Valores:** <*caminho para ficheiros de pré-requisitos do programa de configuração*>  

    -   **Detalhes:** Especifica o caminho para os ficheiros de pré-requisitos do programa de configuração. Conforme o valor de **PrerequisiteComp** , a Configuração utiliza este caminho para armazenar os ficheiros transferidos ou localizar os ficheiros transferidos anteriormente.  

-   **Nome da chave:** AdminConsole  

    -   **Necessário:** Sim  

    -   **Valores:** 0 ou 1  

         0 = efetue não instalar  

         1 = instalação  

    -   **Detalhes:** Especifica se pretende instalar a consola do Configuration Manager.  

-   **Nome da chave:** JoinCEIP  

    -   **Necessário:** Sim  

    -   **Valores:** 0 ou 1  

         0 = efetue não aderir  

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

-   **Nome da chave:** Ponto dedistribuição  

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

    -   **Detalhes:** Especifica se pretende configurar todos os sistemas de sites para aceitar apenas comunicações HTTPS de clientes ou o método de comunicação seja configurado para cada função do sistema de sites. Quando seleciona **EnforceHTTPS**, computador cliente tem de ter um certificado de infraestrutura de chaves públicas (PKI) válido para autenticação de cliente.  

-   **Nome da chave:** ClientsUsePKICertificate  

    -   **Necessário:** Sim  

    -   **Valores:** 0 ou 1  

         0 = efetue não utilizar  

         1 = utilizar  

    -   **Detalhes:** Especifica se os clientes utilizam um certificado PKI de cliente para comunicar com funções de sistema de sites.  

-   **Nome da chave:** AddServerLanguages  

    -   **Necessário:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Detalhes:** Especifica os idiomas do servidor que estarão disponíveis para a consola do Configuration Manager, relatórios e objetos do Configuration Manager. O inglês está disponível por predefinição.  

-   **Nome da chave:** AddClientLanguages  

    -   **Necessário:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Detalhes:** Especifica os idiomas que estarão disponíveis para os computadores cliente. O inglês está disponível por predefinição.  

-   **Nome da chave:** DeleteServerLanguages  

    -   **Necessário:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Detalhes:** Modifica um site após a respetiva instalação. Especifica os idiomas a remover e que já não estará disponível para a consola do Configuration Manager, relatórios e objetos do Configuration Manager. O inglês está disponível por predefinição e não pode ser removido.  

-   **Nome da chave:** DeleteClientLanguages  

    -   **Necessário:** Não  

    -   **Valores:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Detalhes:** Modifica um site após a respetiva instalação. Especifica os idiomas a remover e que já não estará disponível para computadores cliente. O inglês está disponível por predefinição e não pode ser removido.  

-   **Nome da chave:** MobileDeviceLanguage  

    -   **Necessário:** Sim  

    -   **Valores:** 0 ou 1  

         0 = efetue não instalar  

         1 = instalação  

    -   **Detalhes:** Especifica se os idiomas de cliente do dispositivo móvel são instalados.  

**SQLConfigOptions**  

-   **Nome da chave:** SQLServerName  

    -   **Necessário:** Sim  

    -   **Valores:** <*nome do SQL Server*>  

    -   **Detalhes:** Especifica o nome do servidor ou instância em cluster que está a executar o SQL Server e que irá alojar a base de dados do site.  

-   **Nome da chave:** DatabaseName  

    -   **Necessário:** Sim  

    -   **Valores:** <*nome de base de dados do Site*> ou <*nome da instância*>\\<*nome de base de dados do Site*>  

    -   **Detalhes:** Especifica o nome da base de dados do SQL Server para criar ou a base de dados do SQL Server a utilizar para instalar a base de dados do site primário.  

        > [!IMPORTANT]  
        >  Se não utilizar a instância predefinida, terá de especificar o nome da instância e o nome da base de dados do site.  

-   **Nome da chave:** SQLSSBPort  

    -   **Necessário:** Não  

    -   **Valores:** <*número de porta do SSB*>  

    -   **Detalhes:** Especifica a porta SSB que utiliza o SQL Server. SSB normalmente está configurado para utilizar a porta TCP 4022, mas pode utilizar uma porta diferente.  

-   **Nome da chave:** SQLDataFilePath  

    -   **Necessário:** Não  

    -   **Valores:** <*caminho do ficheiro. mdb de base de dados*>  

    -   **Detalhes:** Especifica uma localização alternativa para criar o ficheiro. mdb de base de dados.  

-   **Nome da chave:** SQLLogFilePath  

    -   **Necessário:** Não  

    -   **Valores:** <*caminho do ficheiro. ldf da base de dados*>  

    -   **Detalhes:** Especifica uma localização alternativa para criar o ficheiro. ldf da base de dados.  

**HierarchyExpansionOption**  

-   **Nome da chave:** CCARSiteServer  

    -   **Necessário:** Não  

    -   **Valores:** <*FQDN de site de Administração Central*>  

    -   **Detalhes:** Especifica o site de administração central que um site primário se ligará quando aderir hierarquia do Configuration Manager. Tem de especificar o site de administração central durante a configuração.  

-   **Nome da chave:** CASRetryInterval  

    -   **Necessário:** Não  

    -   **Valores:** <*Interval*>  

    -   **Detalhes:** Especifica o intervalo entre tentativas (em minutos) para estabelecer uma ligação para o site de administração central após a ligação falha. Por exemplo, se a ligação ao site de administração central falhar, o site primário aguarda o número de minutos que especificar para a **CASRetryInterval** valor e, em seguida, tenta restabelecer a ligação.  

-   **Nome da chave:** WaitForCASTimeout  

    -   **Necessário:** Não  

    -   **Valores:** <*Timeout*>  

         Um valor de **0** para **100**  

    -   **Detalhes:** Especifica o valor de tempo limite máximo (em minutos) para um site primário ligar ao site de administração central. Por exemplo, se um site primário não conseguir ligar a um site de administração central, o site primário repetirá a ligação ao site de administração central com base no **CASRetryInterval** valor até que o **WaitForCASTimeout** período for atingido. Pode especificar um valor de **0** para **100**.  

**CloudConnectorOptions**  

-   **Nome da chave:** CloudConnector  

    -   **Necessário:** Sim  

    -   **Valores:** 0 ou 1  

         0 = efetue não instalar  

         1 = instalação  

    -   **Detalhes:** Especifica se deve instalar um ponto de ligação de serviço neste site. Uma vez que o ponto de ligação de serviço só pode ser instalado no site de nível superior de uma hierarquia, este valor tem de ser **0** para um site primário subordinado.  

-   **Nome da chave:** CloudConnectorServer  

    -   **Necessário:** Obrigatório quando **CloudConnector** é igual a 1  

    -   **Valores:** <*o servidor de ponto de ligação de serviço FQDN*\>  

    -   **Detalhes:** Especifica o FQDN do servidor que irá alojar a função de sistema de sites de ponto de ligação de serviço.  

-   **Nome da chave:** UseProxy  

    -   **Necessário:** Obrigatório quando **CloudConnector** é igual a 1  

    -   **Valores:** 0 ou 1  

         0 = efetue não instalar  

         1 = instalação  

    -   **Detalhes:** Especifica se o ponto de ligação de serviço irá utilizar um servidor proxy.  

-   **Nome da chave:** ProxyName  

    -   **Necessário:** Obrigatório quando **UseProxy** é igual a 1  

    -   **Valores:** <*FQDN do servidor de Proxy*>  

    -   **Detalhes:** Especifica o FQDN do servidor proxy que será utilizado pela função de sistema de sites de ponto de ligação de serviço.  

-   **Nome da chave:** /Proxyport  

    -   **Necessário:** Obrigatório quando **UseProxy** é igual a 1  

    -   **Valores:** <*número da porta*>  

    -   **Detalhes:** Especifica o número de porta a utilizar para a porta de proxy.  

### <a name="unattended-recovery-for-a-central-administration-site"></a>Recuperação automática de um site de administração central  
 Utilize os seguintes detalhes para recuperar um site de administração central utilizando um ficheiro de script de configuração automática.  

**Identificação**  

-   **Nome da chave:** Ação  

    -   **Necessário:** Sim  

    -   **Valores:** RecoverCCAR  

    -   **Detalhes:** Recupera um site de administração central.  

-   **Nome da chave:** CDLatest  

    -   **Necessário:** Sim – apenas quando utilizar suportes de dados a partir do CD. Pasta mais recente.    

    -   **Valores:** 1. qualquer valor diferente de 1 é considerada como não estar a utilizar o CD. Mais recente.

    -   **Detalhes:** O script tem de incluir este valor e chave quando executa a configuração a partir do suporte no CD. Pasta mais recente para efeitos de instalação de um site primário ou de administração central ou a recuperar um site primário ou de administração central. Este valor informa o programa de configuração que o suporte de dados de formulário CD. Está a ser utilizada a versão mais recente.

**RecoveryOptions**  

-   **Nome da chave:** ServerRecoveryOptions  

    -   **Necessário:** Sim  

    -   **Valores:** 1, 2 ou 4  

         1 = servidor de site de recuperação e SQL Server.  

         2 = Recuperar apenas servidor de site.  

         4 = Recuperar apenas SQL Server.  

    -   **Detalhes:** Especifica se o programa de configuração irá recuperar o servidor do site, do SQL Server ou ambos. As chaves associadas são necessárias quando define o seguinte valor para o **ServerRecoveryOptions** definição:  

        -   Valor = 1: Tem a opção para especificar um valor para o **SiteServerBackupLocation** chave para recuperar o site utilizando uma cópia de segurança do site. Se não especificar um valor, o site será reinstalado sem ser restaurado a partir de um conjunto de cópias de segurança.  

        -   Valor = 2: Tem a opção para especificar um valor para o **SiteServerBackupLocation** chave para recuperar o site utilizando uma cópia de segurança do site. Se não especificar um valor, o site será reinstalado sem ser restaurado a partir de um conjunto de cópias de segurança.  

        -   Valor = 4: A chave **BackupLocation** é obrigatória se configurar o valor **10** para a chave **DatabaseRecoveryOptions** , para restaurar a base de dados do site a partir de uma cópia de segurança.  

-   **Nome da chave:** DatabaseRecoveryOptions  

    -   **Necessário:** Esta chave é necessária quando a definição **ServerRecoveryOptions** tem o valor **1** ou **4**  

    -   **Valores:** 10, 20, 40 ou 80  

         10 = Restaurar a base de dados do site a partir de cópia de segurança.  

         20 = Utilizar uma base de dados do site que tenha sido recuperada manualmente utilizando outro método.  

         40 = Criar uma nova base de dados para o site. Utilize esta opção quando não estiver disponível nenhuma cópia de segurança da base de dados do site. Os dados globais e de site são recuperados através da replicação a partir de outros sites.  

         80 = ignorar recuperação da base de dados.  

    -   **Detalhes:** Especifica a forma como a configuração recupera a base de dados do site no SQL Server.  

-   **Nome da chave:** ReferenceSite  

    -   **Necessário:** Esta chave é obrigatória se a definição **DatabaseRecoveryOptions** tiver o valor **40**.  

    -   **Valores:** <*FQDN de site de referência*>  

    -   **Detalhes:** Especifica o site primário de referência que utiliza o site de administração central para recuperar dados globais se a cópia de segurança da base de dados for anterior ao período de retenção de registo de alterações ou quando a recuperação de site sem uma cópia de segurança.  

         Quando não especificar um site de referência e a cópia de segurança é anterior ao período de retenção de registo de alterações, todos os sites primários serão reinicializados com os dados restaurados a partir do site de administração central.  

         Quando não especificar um site de referência e a cópia de segurança estiver dentro do período de retenção de registo de alterações, apenas as alterações efetuadas após a cópia de segurança são replicadas a partir de sites primários. Quando existirem alterações de diferentes sites primários em conflito, o site de administração central utilizará a primeira que receber.  

-   **Nome da chave:** SiteServerBackupLocation  

    -   **Necessário:** Não  

    -   **Valores:** <*caminho para o conjunto de cópia de segurança do servidor de site*>  

    -   **Detalhes:** Especifica o caminho para o conjunto de cópia de segurança de servidor de site. Esta chave é opcional se a definição **ServerRecoveryOptions** tiver o valor **1** ou **2**. Especifique um valor para a chave **SiteServerBackupLocation** para recuperar o site com uma cópia de segurança do mesmo. Se não especificar um valor, o site será reinstalado sem ser restaurado a partir de um conjunto de cópias de segurança.  

-   **Nome da chave:** BackupLocation  

    -   **Necessário:** Esta chave é necessária quando configura um valor de **1** ou **4** para o **ServerRecoveryOptions** chave e configura o valor **10** para o **DatabaseRecoveryOptions** chave.  

    -   **Valores:** <*caminho para o conjunto de cópia de segurança de base de dados do site*>  

    -   **Detalhes:** Especifica o caminho para o conjunto de cópia de segurança de base de dados de site.  

**Opções**  

-   **Nome da chave:** Iddoproduto  

    -   **Necessário:** Sim  

    -   **Valores:** <*xxxxx-xxxxx-xxxxx-xxxxx-xxxxx*> *ou* aval  

    -   **Detalhes:** Especifica a chave de produto de instalação do Configuration Manager, incluindo os traços. Introduza **Eval** para instalar a versão de avaliação do Configuration Manager.  

-   **Nome da chave:** Código do site  

    -   **Necessário:** Sim  

    -   **Valores:** <*código do Site*>  

    -   **Detalhes:** Especifica três carateres alfanuméricos que identificam o site na sua hierarquia. Tem de especificar o código do site que o site utilizava antes da falha.

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

    -   **Detalhes:** Especifica o FQDN do servidor que alojará o fornecedor de SMS. Terá de especificar o servidor que hospedava o Fornecedor de SMS antes da falha.  

         Pode configurar Fornecedores de SMS adicionais para o site após a instalação inicial. Para mais informações sobre o fornecedor de SMS, consulte o artigo [planear o fornecedor de SMS para o System Center Configuration Manager](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

-   **Nome da chave:** PrerequisiteComp  

    -   **Necessário:** Sim  

    -   **Valores:** 0 ou 1  

         0 = transferência  

         1 = Already transferido  

    -   **Detalhes:** Especifica se os ficheiros de pré-requisitos de configuração já foram transferidos. Por exemplo, se utilizar um valor de **0**, a configuração transfere os ficheiros.  

-   **Nome da chave:** PrerequisitePath  

    -   **Necessário:** Sim  

    -   **Valores:** <*caminho para ficheiros de pré-requisitos do programa de configuração*>  

    -   **Detalhes:** Especifica o caminho para os ficheiros de pré-requisitos do programa de configuração. Conforme o valor de **PrerequisiteComp** , a Configuração utiliza este caminho para armazenar os ficheiros transferidos ou localizar os ficheiros transferidos anteriormente.  

-   **Nome da chave:** AdminConsole  

    -   **Necessário:** Esta chave é necessária, exceto se a definição **ServerRecoveryOptions** tiver o valor **4**.  

    -   **Valores:** 0 ou 1  

         0 = efetue não instalar  

         1 = instalação  

    -   **Detalhes:** Especifica se pretende instalar a consola do Configuration Manager.  

-   **Nome da chave:** JoinCEIP  

    -   **Necessário:** Sim  

    -   **Valores:** 0 ou 1  

         0 = efetue não aderir  

         1 = associação  

    -   **Detalhes:** Especifica se pretende aderir ao CEIP.  

**SQLConfigOptions**  

-   **Nome da chave:** SQLServerName  

    -   **Necessário:** Sim  

    -   **Valores:** <*nome do SQL Server*>  

    -   **Detalhes:** Especifica o nome do servidor ou instância em cluster que está a executar o SQL Server e que irá alojar a base de dados do site. Terá de especificar o mesmo servidor que alojava a base de dados do site antes da falha.  

-   **Nome da chave:** DatabaseName  

    -   **Necessário:** Sim  

    -   **Valores:** <*nome de base de dados do Site*> ou <*nome da instância*>\\<*nome de base de dados do Site*>  

    -   **Detalhes:** Especifica o nome da base de dados do SQL Server para criar ou a base de dados do SQL Server a utilizar para instalar a base de dados do site de administração central. Terá de especificar o nome da mesma base de dados que foi utilizada antes da falha.  

        > [!IMPORTANT]  
        >  Se não utilizar a instância predefinida, terá de especificar o nome da instância e o nome da base de dados do site.  

-   **Nome da chave:** SQLSSBPort  

    -   **Necessário:** Sim  

    -   **Valores:** <*número de porta do SSB*>  

    -   **Detalhes:** Especifica a porta SSB que utiliza o SQL Server. Normalmente, o SSB está configurado para utilizar a porta TCP 4022. Tem de especificar a mesma porta do SSB que foi utilizada antes da falha.  

-   **Nome da chave:** SQLDataFilePath  

    -   **Necessário:** Não  

    -   **Valores:** <*caminho do ficheiro. mdb de base de dados*>  

    -   **Detalhes:** Especifica uma localização alternativa para criar o ficheiro. mdb de base de dados.  

-   **Nome da chave:** SQLLogFilePath  

    -   **Necessário:** Não  

    -   **Valores:** <*caminho do ficheiro. ldf da base de dados*>  

    -   **Detalhes:** Especifica uma localização alternativa para criar o ficheiro. ldf da base de dados.  

**CloudConnectorOptions**  

-   **Nome da chave:** CloudConnector  

    -   **Necessário:** Sim  

    -   **Valores:** 0 ou 1  

         0 = efetue não instalar  

         1 = instalação  

    -   **Detalhes:** Especifica se deve instalar um ponto de ligação de serviço neste site. Uma vez que o ponto de ligação de serviço só pode ser instalado no site de nível superior de uma hierarquia, este valor tem de ser **0** para um site primário subordinado.  

-   **Nome da chave:** CloudConnectorServer  

    -   **Necessário:** Obrigatório quando **CloudConnector** é igual a 1  

    -   **Valores:** <*o servidor de ponto de ligação de serviço FQDN*>  

    -   **Detalhes:** Especifica o FQDN do servidor que irá alojar a função de sistema de sites de ponto de ligação de serviço.  

-   **Nome da chave:** UseProxy  

    -   **Necessário:** Obrigatório quando **CloudConnector** é igual a 1  

    -   **Valores:** 0 ou 1  

         0 = efetue não instalar  

         1 = instalação  

    -   **Detalhes:** Especifica se o ponto de ligação de serviço irá utilizar um servidor proxy.  

-   **Nome da chave:** ProxyName  

    -   **Necessário:** Obrigatório quando **CloudConnector** é igual a 1  

    -   **Valores:** <*FQDN do servidor de Proxy*>  

    -   **Detalhes:** Especifica o FQDN do servidor proxy que será utilizado pela função de sistema de sites de ponto de ligação de serviço.  

-   **Nome da chave:** /Proxyport  

    -   **Necessário:** Obrigatório quando **CloudConnector** é igual a 1  

    -   **Valores:** <*número da porta*>  

    -   **Detalhes:** Especifica o número de porta a utilizar para a porta de proxy.  

### <a name="unattended-recovery-for-a-primary-site"></a>Recuperação automática para um site primário  
 Utilize os seguintes detalhes para recuperar um site primário utilizando um ficheiro de script de configuração automática.  

**Identificação**  

-   **Nome da chave:** Ação  

    -   **Necessário:** Sim  

    -   **Valores:** <*RecoverPrimarySite*>  

    -   **Detalhes:** Recupera um site primário.  

-   **Nome da chave:** CDLatest  

    -   **Necessário:** Sim – apenas quando utilizar suportes de dados a partir do CD. Pasta mais recente.    

    -   **Valores:** 1. qualquer valor diferente de 1 é considerada como não estar a utilizar o CD. Mais recente.

    -   **Detalhes:** O script tem de incluir este valor e chave quando executa a configuração a partir do suporte no CD. Pasta mais recente para efeitos de instalação de um site primário ou de administração central ou a recuperar um site primário ou de administração central. Este valor informa o programa de configuração que o suporte de dados de formulário CD. Está a ser utilizada a versão mais recente.    

**RecoveryOptions**  

-   **Nome da chave:** ServerRecoveryOptions  

    -   **Necessário:** Sim  

    -   **Valores:** 1, 2 ou 4  

         1 = servidor de site de recuperação e SQL Server.  

         2 = Recuperar apenas servidor de site.  

         4 = Recuperar apenas SQL Server.  

    -   **Detalhes:** Especifica se o programa de configuração irá recuperar o servidor do site, do SQL Server ou ambos. As chaves associadas são necessárias quando define o seguinte valor para o **ServerRecoveryOptions** definição:  

        -   Valor = 1: Tem a opção para especificar um valor para o **SiteServerBackupLocation** chave para recuperar o site utilizando uma cópia de segurança do site. Se não especificar um valor, o site será reinstalado sem ser restaurado a partir de um conjunto de cópias de segurança.  

        -   Valor = 2: Tem a opção para especificar um valor para o **SiteServerBackupLocation** chave para recuperar o site utilizando uma cópia de segurança do site. Se não especificar um valor, o site será reinstalado sem ser restaurado a partir de um conjunto de cópias de segurança.  

        -   Valor = 4: A chave **BackupLocation** é obrigatória se configurar o valor **10** para a chave **DatabaseRecoveryOptions** , para restaurar a base de dados do site a partir de uma cópia de segurança.  

-   **Nome da chave:** DatabaseRecoveryOptions  

    -   **Necessário:** Esta chave é necessária quando a definição **ServerRecoveryOptions** tem o valor **1** ou **4**  

    -   **Valores:** 10, 20, 40 ou 80  

         10 = Restaurar a base de dados do site a partir de cópia de segurança.  

         20 = Utilizar uma base de dados do site que tenha sido recuperada manualmente utilizando outro método.  

         40 = Criar uma nova base de dados para o site. Utilize esta opção quando não estiver disponível nenhuma cópia de segurança da base de dados do site. Os dados globais e de site são recuperados através da replicação a partir de outros sites.  

         80 = ignorar recuperação da base de dados.  

    -   **Detalhes:** Especifica a forma como a configuração recupera a base de dados do site no SQL Server.  

-   **Nome da chave:** SiteServerBackupLocation  

    -   **Necessário:** Não  

    -   **Valores:** <*caminho para o conjunto de cópia de segurança do servidor de site*>  

    -   **Detalhes:**  

         Especifica o caminho para o conjunto de cópia de segurança de servidor de site. Esta chave é opcional se a definição **ServerRecoveryOptions** tiver o valor **1** ou **2**. Especifique um valor para a chave **SiteServerBackupLocation** para recuperar o site com uma cópia de segurança do mesmo. Se não especificar um valor, o site será reinstalado sem ser restaurado a partir de um conjunto de cópias de segurança.  

-   **Nome da chave:** BackupLocation  

    -   **Necessário:** Esta chave é necessária quando configura um valor de **1** ou **4** para o **ServerRecoveryOptions** chave e configura o valor **10** para o **DatabaseRecoveryOptions** chave.  

    -   **Valores:** <*caminho para o conjunto de cópia de segurança de base de dados do site*>  

    -   **Detalhes:** Especifica o caminho para o conjunto de cópia de segurança de base de dados de site.  

**Opções**  

-   **Nome da chave:** Iddoproduto  

    -   **Necessário:** Sim  

    -   **Valores:** *xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* ou *aval*  

    -   **Detalhes:** Especifica a chave de produto de instalação do Configuration Manager, incluindo os traços. Introduza **Eval** para instalar a versão de avaliação do Configuration Manager.  

-   **Nome da chave:** Código do site  

    -   **Necessário:** Sim  

    -   **Valores:** <*código do Site*>  

    -   **Detalhes:** Especifica três carateres alfanuméricos que identificam o site na sua hierarquia. Tem de especificar o código do site que o site utilizava antes da falha.

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

    -   **Detalhes:** Especifica o FQDN do servidor que alojará o fornecedor de SMS. Terá de especificar o servidor que hospedava o Fornecedor de SMS antes da falha. Pode configurar Fornecedores de SMS adicionais para o site após a instalação inicial. Para mais informações sobre o fornecedor de SMS, consulte o artigo [planear o fornecedor de SMS para o System Center Configuration Manager](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

-   **Nome da chave:** PrerequisiteComp  

    -   **Necessário:** Sim  

    -   **Valores:** 0 ou 1  

         0 = transferência  

         1 = Already transferido  

    -   **Detalhes:** Especifica se os ficheiros de pré-requisitos de configuração já foram transferidos. Por exemplo, se utilizar um valor de **0**, a configuração transfere os ficheiros.  

-   **Nome da chave:** PrerequisitePath  

    -   **Necessário:** Sim  

    -   **Valores:** <*caminho para ficheiros de pré-requisitos do programa de configuração*>  

    -   **Detalhes:** Especifica o caminho para os ficheiros de pré-requisitos do programa de configuração. Conforme o valor de **PrerequisiteComp** , a Configuração utiliza este caminho para armazenar os ficheiros transferidos ou localizar os ficheiros transferidos anteriormente.  

-   **Nome da chave:** AdminConsole  

    -   **Necessário:** Esta chave é necessária, exceto se a definição **ServerRecoveryOptions** tiver o valor **4**.  

    -   **Valores:** 0 ou 1  

         0 = efetue não instalar  

         1 = instalação  

    -   **Detalhes:** Especifica se pretende instalar a consola do Configuration Manager.  

-   **Nome da chave:** JoinCEIP  

    -   **Necessário:** Sim  

    -   **Valores:** 0 ou 1  

         0 = efetue não aderir  

         1 = associação  

    -   **Detalhes:** Especifica se pretende aderir ao CEIP.  

**SQLConfigOptions**  

-   **Nome da chave:** SQLServerName  

    -   **Necessário:** Sim  

    -   **Valores:** <*nome do SQL Server*>  

    -   **Detalhes:** Especifica o nome do servidor ou instância em cluster que está a executar o SQL Server e que irá alojar a base de dados do site. Terá de especificar o mesmo servidor que alojava a base de dados do site antes da falha.  

-   **Nome da chave:** DatabaseName  

    -   **Necessário:** Sim  

    -   **Valores:**  <*nome de base de dados do Site*> ou <*nome da instância*>\\<*nome de base de dados do Site*>

    -   **Detalhes:**  

         Especifica o nome da base de dados do SQL Server para criar ou a base de dados do SQL Server a utilizar para instalar a base de dados do site de administração central. Terá de especificar o nome da mesma base de dados que foi utilizada antes da falha.  

        > [!IMPORTANT]  
        >  Se não utilizar a instância predefinida, terá de especificar o nome da instância e o nome da base de dados do site.  

-   **Nome da chave:** SQLSSBPort  

    -   **Necessário:** Sim  

    -   **Valores:** <*número de porta do SSB*>  

    -   **Detalhes:** Especifica a porta SSB que utiliza o SQL Server. Normalmente, o SSB está configurado para utilizar a porta TCP 4022. Tem de especificar a mesma porta do SSB que foi utilizada antes da falha.  

-   **Nome da chave:** SQLDataFilePath  

    -   **Necessário:** Não  

    -   **Valores:** <*caminho do ficheiro. mdb de base de dados*>  

    -   **Detalhes:** Especifica uma localização alternativa para criar o ficheiro. mdb de base de dados.  

-   **Nome da chave:** SQLLogFilePath  

    -   **Necessário:** Não  

    -   **Valores:** <*caminho do ficheiro. ldf da base de dados*>  

    -   **Detalhes:** Especifica uma localização alternativa para criar o ficheiro. ldf da base de dados.  

**HierarchyExpansionOptions**  

-   **Nome da chave:** CCARSiteServer  

    -   **Necessário:** Consulte os detalhes.  

    -   **Valores:** <*código do site de administração central do Site*>  

    -   **Detalhes:** Especifica o site de administração central ao qual o site primário liga quando é associado a hierarquia do Configuration Manager. Esta definição é necessária se o site primário estava ligado a um site de administração central antes da falha. Tem de especificar o código do site que era utilizado para o site de administração central antes da falha.  

-   **Nome da chave:** CASRetryInterval  

    -   **Necessário:** Não  

    -   **Valores:** <*Interval*>  

    -   **Detalhes:** Especifica o intervalo entre tentativas (em minutos) para estabelecer uma ligação para o site de administração central após a ligação falha. Por exemplo, se a ligação ao site de administração central falhar, o site primário aguarda o número de minutos que especificar para a **CASRetryInterval** valor e, em seguida, tenta restabelecer a ligação.  

-   **Nome da chave:** WaitForCASTimeout  

    -   **Necessário:** Não  

    -   **Valores:** <*Timeout*>  

    -   **Detalhes:** Especifica o valor de tempo limite máximo (em minutos) para um site primário ligar ao site de administração central. Por exemplo, se um site primário não conseguir ligar a um site de administração central, o site primário repetirá a ligação ao site de administração central com base no **CASRetryInterval** valor até que o **WaitForCASTimeout** período for atingido. Pode especificar um valor de **0** para **100**.  

**CloudConnectorOptions**  

-   **Nome da chave:** CloudConnector  

    -   **Necessário:** Sim  

    -   **Valores:** 0 ou 1  

         0 = efetue não instalar  

         1 = instalação  

    -   **Detalhes:** Especifica se deve instalar um ponto de ligação de serviço neste site. Uma vez que o ponto de ligação de serviço só pode ser instalado no site de nível superior de uma hierarquia, este valor tem de ser **0** para um site primário subordinado.  

-   **Nome da chave:** CloudConnectorServer  

    -   **Necessário:** Obrigatório quando **CloudConnector** é igual a 1  

    -   **Valores:** <*o servidor de ponto de ligação de serviço FQDN*>  

    -   **Detalhes:** Especifica o FQDN do servidor que irá alojar a função de sistema de sites de ponto de ligação de serviço.  

-   **Nome da chave:** UseProxy  

    -   **Necessário:** Obrigatório quando **CloudConnector** é igual a 1  

    -   **Valores:** 0 ou 1  

         0 = efetue não instalar  

         1 = instalação  

    -   **Detalhes:** Especifica se o ponto de ligação de serviço irá utilizar um servidor proxy.  

-   **Nome da chave:** ProxyName  

    -   **Necessário:** Obrigatório quando **CloudConnector** é igual a 1  

    -   **Valores:** <*FQDN do servidor de Proxy*>  

    -   **Detalhes:** Especifica o FQDN do servidor proxy que será utilizado pela função de sistema de sites de ponto de ligação de serviço.  

-   **Nome da chave:** /Proxyport  

    -   **Necessário:** Obrigatório quando **CloudConnector** é igual a 1  

    -   **Valores:** <*número da porta*>  

    -   **Detalhes:** Especifica o número de porta a utilizar para a porta de proxy.  

