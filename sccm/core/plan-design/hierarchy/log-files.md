---
title: "Ficheiros de registo para resolução de problemas"
titleSuffix: Configuration Manager
description: Utilize ficheiros de registo para resolver problemas de uma hierarquia do System Center Configuration Manager.
ms.custom: na
ms.date: 7/03/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c1ff371e-b0ad-4048-aeda-02a9ff08889e
caps.latest.revision: "9"
caps.handback.revision: "0"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: c310e23b543e8767a393ca5bf87a224a9269e359
ms.sourcegitcommit: ca9d15dfb1c9eb47ee27ea9b5b39c9f8cdcc0748
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/04/2018
---
# <a name="log-files-in-system-center-configuration-manager"></a>Ficheiros de registo no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

No System Center Configuration Manager, os componentes de servidor do site e cliente registam informações de processo nos ficheiros de registo individuais. Pode utilizar as informações nos ficheiros de registo para o ajudar a resolver problemas que possam ocorrer na hierarquia do Configuration Manager. Por predefinição, o registo de componente de cliente e o servidor está ativado no Configuration Manager.   

 As secções seguintes fornecem detalhes sobre os ficheiros de registo diferentes disponíveis para si. Pode utilizar esta informação para ver e monitorizar o cliente do Configuration Manager e os registos do servidor para detalhes de operação e, para identificar o erro de informações que podem ajudar a resolver quaisquer problemas.  

-   [Sobre os ficheiros de registo do Configuration Manager](#BKMK_AboutLogs)  

    -   [Configurar opções de registo utilizando o Gestor de serviço do Configuration Manager](#BKMK_LogOptions)  

    -   [Localizar registos do Configuration Manager](#BKMK_LogLocation)  

-   [Registos de cliente do Configuration Manager](#BKMK_ClientLogs)  

    -   [Operações de cliente](#BKMK_ClientOpLogs)  

    -   [Ficheiros de registo de instalação do cliente](#BKMK_ClientInstallLog)  

    -   [Cliente para Linux e UNIX](#BKMK_LogFilesforLnU)  

    -   [Cliente para computadores Mac](#BKMK_LogfilesforMac)  

-   [Ficheiros de registo do servidor de site do Configuration Manager](#BKMK_ServerLogs)  

    -   [Servidor e o local registos sistema de sites servidor](#BKMK_SiteSiteServerLog)  

    -   [Ficheiros de registo de instalação de servidor do site](#BKMK_SiteInstallLog)  

    -   [Ficheiros de registo do ponto de estado de contingência](#BKMK_FSPLog)  

    -   [Ficheiros de registo do ponto de gestão](#BKMK_MPLog)  

    -   [Ficheiros de registo do ponto de atualização de software](#BKMK_SUPLog)  

-   [Ficheiros de registo para funcionalidade do Configuration Manager](#BKMK_FunctionLogs)  

    -   [Gestão de aplicações](#BKMK_AppManageLog)  

    -   [Do Asset intelligence](#BKMK_AILog)  

    -   [Cópia de segurança e recuperação](#BKMK_BnRLog)  

    -   [Inscrição de certificados](#BKMK_CertificateEnrollment)

    -   [Notificação do cliente](#BKMK_BGB)

    -   [Gateway de gestão de nuvem](#cloud-management-gateway)

    -   [Definições de compatibilidade e acesso a recursos da empresa](#BKMK_CompSettingsLog)  

    -   [Consola do Configuration Manager](#BKMK_ConsoleLog)  

    -   [Gestão de conteúdo](#BKMK_ContentLog)  

    -   [Deteção](#BKMK_DiscoveryLog)  

    -   [Endpoint Protection](#BKMK_EPLog)  

    -   [Extensões](#BKMK_Extensions)  

    -   [Inventário](#BKMK_InventoryLog)  

    -   [Medição](#BKMK_MeteringLog)  

    -   [Migração](#BKMK_MigrationLog)  

    -   [Dispositivos móveis](#BKMK_MDMLog)  

    -   [Implementação do sistema operativo](#BKMK_OSDLog)  

    -   [Gestão de energia](#BKMK_PowerMgmtLog)  

    -   [Controlo remoto](#BKMK_RCLog)  

    -   [Relatórios](#BKMK_ReportLog)  

    -   [Administração baseada em funções](#BKMK_RBALog)  

    -   [Ponto de ligação de serviço](#BKMK_WITLog)  

    -   [Atualizações de software](#BKMK_SU_NAPLog)  

    -   [Reativação por LAN](#BKMK_WOLLog)  

    -   [Manutenção do Windows 10](#BKMK_WindowsServicingLog)

    -   [Agente do Windows Update](#BKMK_WULog)  

    -   [Servidor WSUS](#BKMK_WSUSLog)  

##  <a name="BKMK_AboutLogs"></a>Sobre os ficheiros de registo do Configuration Manager  
 A maioria dos processos no Configuration Manager escrevem informações operacionais num ficheiro de registo que está dedicado a esse processo. Os ficheiros de registo são identificados pelo **. log** ou **. lo _** extensões de ficheiros. O Configuration Manager escreve num ficheiro. log até esse registo chegar ao tamanho máximo. Quando o registo está cheio, o ficheiro. log é copiado para um ficheiro com o mesmo nome mas com a extensão. lo _ e o processo ou componente continua a escrever no ficheiro. log. Quando o ficheiro. log atinge novamente o tamanho máximo, o ficheiro. lo _ é substituído e o processo é repetido. Alguns componentes criam um histórico de ficheiros de registo, acrescentando um carimbo de data e hora ao nome do ficheiro de registo e mantendo a extensão. log. Uma exceção ao tamanho máximo e a utilização do ficheiro. lo _ é o cliente para Linux e UNIX. Para obter informações sobre como o cliente para Linux e UNIX utiliza ficheiros de registo, consulte [gerir os ficheiros de registo do cliente para Linux e UNIX](#BKMK_ManageLinuxLogs) neste tópico.  

 Para ver os registos, utilize a ferramenta Gestor de configuração registo Visualizador CMTrace, localizada no \\SMSSetup\\pasta Ferramentas de suporte de dados de origem do Configuration Manager. A ferramenta CMTrace é adicionada a todas as imagens de arranque que são adicionadas à biblioteca de Software.  

###  <a name="BKMK_LogOptions"></a>Configurar opções de registo utilizando o Gestor de serviço do Configuration Manager  
 No Configuration Manager, pode alterar onde estão armazenados os ficheiros de registo e pode alterar o tamanho do ficheiro de registo.  

 Para modificar o tamanho dos ficheiros de registo, mudar o nome e localização do ficheiro de registo ou para forçar vários componentes a escreverem num ficheiro de registo único, efetue os seguintes passos.  

#### <a name="to-modify-logging-for-a-component"></a>Para modificar o registo para um componente  

1.  Na consola do Configuration Manager, selecione **monitorização**, selecione **estado do sistema**e, em seguida, selecione **estado do Site** ou **estado do componente**.  
2.  No **home page** separador o **componente** grupo, selecione **iniciar**e, em seguida, selecione **do serviço do Configuration Manager**.  
3.  Quando do Configuration Manager Service Manager for aberto, estabeleça a ligação ao site que pretende gerir. Se o site que pretende gerir não for apresentado, selecione **Site**, selecione **Connect**e, em seguida, introduza o nome do servidor do site do site correto.  
4.  Expandir o site e aceda a **componentes** ou **servidores**, consoante o local onde os componentes que pretende gerir estiverem localizados.  
5.  No painel direito, selecione um ou mais componentes.  
6.  No **componente** menu, selecione **registo**.  
7.  Na caixa de diálogo **Registo de Componente do Configuration Manager**, preencha as opções de configuração disponíveis para a sua seleção.  
8.  Selecione **OK** para guardar a configuração.  

###  <a name="BKMK_LogLocation"></a>Localizar registos do Configuration Manager  
Ficheiros de registo do Configuration Manager são armazenados em várias localizações que dependem do processo que cria o ficheiro de registo e a configuração dos sistemas de sites. Uma vez que a localização do registo num computador pode variar, utilize a função de pesquisa para encontrar os ficheiros de registo relevantes nos computadores do Configuration Manager se precisar de resolver problemas com um cenário específico.  

##  <a name="BKMK_ClientLogs"></a>Registos de cliente do Configuration Manager  
As secções seguintes listam os ficheiros de registo relacionados com operações de cliente e a instalação de cliente.  

###  <a name="BKMK_ClientOpLogs"></a>Operações de cliente  
A tabela seguinte lista os ficheiros de registo localizados no cliente do Configuration Manager.  

|Nome do registo|Descrição|  
|--------------|-----------------|  
|CAS.log|O serviço de acesso ao conteúdo. Mantém a cache do pacote local no cliente.|  
|Ccm32BitLauncher.log|Regista ações de início de aplicações no cliente marcadas como "Executar como 32 bits".|  
|CcmEval.log|Atividades de avaliação de estado do cliente do Configuration Manager de registos e detalhes dos componentes que são necessários para o cliente do Configuration Manager.|  
|CcmEvalTask.log|Regista as atividades de avaliação de estado de cliente de Configuration Manager que são iniciadas pela tarefa de avaliação agendada.|  
|CcmExec.log|Regista atividades do cliente e do serviço Anfitrião de Agente do SMS. Este ficheiro de registo também inclui informações sobre como ativar e desativar o proxy de reativação.|  
|CcmMessaging.log|Regista atividades relacionadas com a comunicação entre o cliente e gestão pontos.|  
|CCMNotificationAgent.log|Regista atividades relacionadas com as operações de notificação de cliente.|  
|Ccmperf.log|Regista atividades relacionadas com a manutenção e a captura de dados relacionados com os contadores de desempenho do cliente.|  
|CcmRestart.log|Regista a atividade de reinício do serviço de cliente.|  
|CCMSDKProvider.log|Regista atividades das interfaces SDK do cliente.|  
|CertificateMaintenance.log|Mantém certificados para os Serviços de Domínio do Active Directory e os pontos de gestão.|  
|CIDownloader.log|Regista detalhes sobre transferências de definições de itens de configuração.|  
|CITaskMgr.log|Regista tarefas que são iniciadas para cada aplicação e o tipo de implementação, tais como conteúdo transferiram e instalarem ou as ações de desinstalação.|  
|ClientAuth.log|Registos de assinatura e actividade de autenticação para o cliente.|  
|ClientIDManagerStartup.log|Cria e mantém o GUID do cliente e identifica as tarefas executadas durante o registo e atribuição do cliente.|  
|ClientLocation.log|Regista tarefas relacionadas com a atribuição do site do cliente.|  
|CMHttpsReadiness.log|Regista os resultados de executar a ferramenta de avaliação de preparação do HTTPS do Configuration Manager. Esta ferramenta verifica se os computadores têm um certificado de autenticação de cliente de infraestrutura de chaves públicas (PKI) que pode ser utilizado com o Configuration Manager.|  
|CmRcService.log|Regista informações para o serviço de controlo remoto.|  
|ContentTransferManager.log|Agenda o serviço de transferência inteligente em segundo plano (BITS) ou bloco de mensagem de servidor (SMB) para transferir ou aceder a pacotes.|  
|DataTransferService.log|Regista todas as comunicações BITS para acesso a políticas ou pacotes.|  
|EndpointProtectionAgent|Regista informações sobre a instalação do cliente do System Center Endpoint Protection e a aplicação da política antimalware a esse cliente.|  
|execmgr.log|Regista detalhes dos pacotes e sequências de tarefas que são executados no cliente.|  
|ExpressionSolver.log|Regista detalhes sobre os métodos de deteção melhorados que são utilizados quando verboso ou o registo de depuração está ativado.|  
|ExternalEventAgent.log|Regista o histórico de deteção de malware do Endpoint Protection e eventos relacionados com o estado do cliente.|  
|FileBITS.log|Regista todas as tarefas de acesso do pacote SMB.|  
|FileSystemFile.log|Regista a atividade do fornecedor do Windows Management Instrumentation (WMI) para recolha de ficheiros e inventário de software.|  
|FSPStateMessage.log|Regista a atividade de mensagens de estado que são enviadas pelo cliente para o ponto de estado de contingência.|  
|InternetProxy.log|Regista a atividade de configuração e utilização da proxy de rede para o cliente.|  
|InventoryAgent.log|Regista atividades de inventário de hardware, inventário de software e ações de deteção de heartbeat no cliente.|  
|LocationCache.log|Regista a atividade de utilização de cache de localização e manutenção para o cliente.|  
|LocationServices.log|Regista a atividade do cliente para localizar pontos de gestão, pontos de atualização de software e pontos de distribuição.|  
|MaintenanceCoordinator.log|Regista a atividade para tarefas de manutenção geral para o cliente.|  
|Mifprovider.log|Regista a atividade do fornecedor WMI para ficheiros de formato MIF (Management Information).|  
|mtrmgr.log|Monitoriza todos os processos de medição de software.|  
|PolicyAgent.log|Regista pedidos de políticas efetuados através do serviço de transferência de dados.|  
|PolicyAgentProvider.log|Regista alterações de política.|  
|PolicyEvaluator.log|Regista detalhes sobre a avaliação das políticas em computadores cliente, incluindo políticas de atualizações de software.|  
|PolicyPlatformClient.log|Regista o processo de remediação e compatibilidade para todos os fornecedores localizados em \Programas\Microsoft Policy Platform, exceto o fornecedor de ficheiros.|  
|PolicySdk.log|Regista atividades das interfaces SDK do sistema de políticas.|  
|Pwrmgmt.log|Regista informações sobre a ativação ou desativação e a configuração de definições de cliente do proxy de reativação.|  
|PwrProvider.log|Regista as atividades do fornecedor de gestão de energia (PWRInvProvider) alojado no serviço WMI. Em todas as versões suportadas do Windows, o fornecedor enumera as definições atuais nos computadores durante o inventário de hardware e aplica as definições do plano de energia.|  
|SCClient_&lt;*domínio*\>@&lt;*username*\>_1.log|Regista a atividade no Centro de Software para o utilizador especificado no computador cliente.|  
|SCClient_&lt;*domínio*\>@&lt;*username*\>_2.log|Regista a atividade do histórico no Centro de Software para o utilizador especificado no computador cliente.|  
|Scheduler.log|Regista atividades de tarefas agendadas para todas as operações de cliente.|  
|SCNotify_&lt;*domínio*\>@&lt;*username*\>_1.log|Regista a atividade para notificar os utilizadores sobre software para o utilizador especificado.|  
|SCNotify_&lt;*domínio*\>@&lt;*username*\>_1 -&lt;*Data_Hora*>. log|Regista a informação do histórico para notificar os utilizadores sobre software para o utilizador especificado.|  
|setuppolicyevaluator.log|Regista a configuração e a criação da política de inventário no WMI.|  
|SleepAgent_&lt;*domínio*\>@SYSTEM_0.log|O ficheiro de registo principal do proxy de reativação.|  
|smscliui.log|Utilizam registos de cliente do Configuration Manager no painel de controlo.|  
|SrcUpdateMgr.log|Regista a atividade das aplicações do Windows Installer instaladas que são atualizadas com as localizações de origem do ponto de distribuição atual.|  
|StatusAgent.log|Regista mensagens de estado que são criadas pelos componentes de cliente.|  
|SWMTRReportGen.log|Gera um relatório de dados de utilização é recolhido pelo agente de medição. Estes dados são registados no ficheiro Mtrmgr.log.|  
|UserAffinity.log|Regista detalhes sobre a afinidade de dispositivo do utilizador.|  
|VirtualApp.log|Regista informações específicas da avaliação dos tipos de implementação de Application Virtualization (App-V).|  
|Wedmtrace.log|Regista operações relacionadas com filtros de escrita nos clientes do Windows Embedded.|  
|wakeprxy-install.log|Regista informações de instalação quando os clientes recebem a opção de definição de cliente para ativar o proxy de reativação.|  
|wakeprxy-uninstall.log|Regista informações sobre a desinstalação do proxy de reativação quando os clientes recebem o definição de cliente a opção para desativar o proxy de reativação, se um proxy de reativação foi anteriormente ligado.|  

###  <a name="BKMK_ClientInstallLog"></a>Ficheiros de registo de instalação do cliente  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com a instalação do cliente do Configuration Manager.  

|Nome do registo|Descrição|  
|--------------|-----------------|  
|ccmsetup.log|Regista tarefas do ccmsetup.exe para a configuração de cliente, atualização de cliente e remoção de cliente. Pode ser utilizado para resolver problemas de instalação de cliente.|  
|ccmsetup-ccmeval.log|Regista tarefas do ccmsetup.exe para o estado do cliente e remediação.|  
|CcmRepair.log|Regista as atividades de reparação do agente de cliente.|  
|Client.msi.log|Os registos configuram tarefas executadas por client.msi. Pode ser utilizado para resolver problemas de instalação ou remoção de clientes.|  

###  <a name="BKMK_LogFilesforLnU"></a>Cliente para Linux e UNIX  
 O cliente do Configuration Manager para Linux e UNIX regista informações nos seguintes ficheiros de registo.  

> [!TIP]  
>  Começando com os clientes para Linux e UNIX da atualização cumulativa 1, pode utilizar CMTrace para ver os ficheiros de registo de cliente para Linux e UNIX.  

> [!NOTE]  
>  Quando utilizar a edição inicial do cliente para Linux e UNIX e consultar a documentação desta secção, substitua as seguintes referências para cada ficheiro ou processo:  
>   
>  -   Substitua **omiserver.bin** por **nwserver.bin**  
> -   Substitua **omi** por **nanowbem**  

|Nome do registo|Detalhes|  
|--------------|-------------|  
|Scxcm.log|O ficheiro de registo do serviço de núcleo do cliente do Configuration Manager para Linux e UNIX (ccmexec.bin). Este ficheiro de registo contém informações sobre a instalação e as operações do ccmexec.bin. em curso<br /><br /> Por predefinição, este ficheiro de registo está localizado em **/var/opt/microsoft/scxcm.log**<br /><br /> Para alterar a localização do ficheiro de registo, edite **/opt/microsoft/configmgr/etc/scxcm.conf** e altere o campo **PATH**. Não é necessário reiniciar o serviço ou o computador cliente para que a alteração produza efeito.<br /><br /> Pode definir o nível de registo para uma de quatro definições diferentes.|  
|Scxcmprovider.log|O ficheiro de registo do serviço CIM do cliente do Configuration Manager para Linux e UNIX (omiserver.bin). Este ficheiro de registo contém informações sobre as operações do nwserver.bin em curso.<br /><br /> Este registo está localizado em**/var/opt/microsoft/configmgr/scxcmprovider.log**<br /><br /> Para alterar a localização do ficheiro de registo, edite **/opt/microsoft/omi/etc/scxcmprovider.conf** e altere o campo **PATH**. Não é necessário reiniciar o serviço ou o computador cliente para que a alteração produza efeito.<br /><br /> Pode definir o nível de registo para uma de três definições.|  

 Ambos os ficheiros de registo suportam vários níveis de registo:  

-   **scxcm.log**. Para alterar o nível de registo, edite **/opt/microsoft/configmgr/etc/scxcm.conf** e altere cada instância do **módulo** etiqueta para o nível de registo que pretende:  

    -   ERRO: Indica problemas que necessitam da atenção  

    -   AVISO: Indica possíveis problemas para operações de cliente  

    -   INFO: Registo mais detalhado que indica o estado de vários eventos no cliente  

    -   RASTREIO: Que, normalmente, o registo verboso é utilizado para diagnosticar problemas  

-   **scxcmprovider.log**. Para alterar o nível de registo, edite **/opt/microsoft/omi/etc/scxcmprovider.conf** e altere cada instância do **módulo** etiqueta para o nível de registo que pretende:  

    -   ERRO: Indica problemas que necessitam da atenção  

    -   AVISO: Indica possíveis problemas para operações de cliente

    -   INFO: Registo mais detalhado que indica o estado de vários eventos no cliente  

Em condições de operação normais, utilize o nível de registo de erro. Este nível de registo cria o ficheiro de registo mais pequeno. Como o nível de registo aumenta de ERROR para aviso, informações e, em seguida, para o rastreio, é criado um ficheiro de registo maior que são escritos mais dados no ficheiro.  

####  <a name="BKMK_ManageLinuxLogs"></a>Gerir ficheiros de registo para o cliente Linux e UNIX  
O cliente para Linux e UNIX não limita o tamanho máximo dos ficheiros de registo de cliente, nem o cliente automaticamente copia os conteúdos dos respetivos ficheiros. log para outro ficheiro, tal como para um ficheiro. lo _. Se pretender controlar o tamanho máximo dos ficheiros de registo, implemente um processo para gerir os ficheiros de registo independentes do cliente do Configuration Manager para Linux e UNIX.  

Por exemplo, pode utilizar o comando padrão Linux e UNIX **logrotate** para gerir o tamanho e a rotação dos ficheiros de registo de cliente. O cliente do Configuration Manager para Linux e UNIX tem uma interface que permite **logrotate** sinalizar o cliente quando a rotação do registo é concluída, por isso, o cliente pode retomar o registo para o ficheiro de registo.  

Para obter informações sobre o comando **logrotate**, veja a documentação das distribuições de Linux e UNIX que utiliza.  

###  <a name="BKMK_LogfilesforMac"></a>Cliente para computadores Mac  
O cliente do Configuration Manager para computadores Mac regista as informações nos seguintes ficheiros de registo.  

|Nome do registo|Detalhes|  
|--------------|-------------|  
|CCMClient -&lt;*Data_Hora*>. log|Regista atividades relacionadas com as operações de cliente Mac, incluindo gestão de aplicações, inventário e registo de erros.<br /><br /> Este ficheiro de registo está localizado na pasta /Library/Application Support/Microsoft/CCM/Logs no computador Mac.|  
|CCMAgent -&lt;*Data_Hora*>. log|Regista informações relacionadas com operações de cliente, incluindo o início de sessão do utilizador e as operações de terminar sessão e atividade do computador Mac.<br /><br /> Este ficheiro de registo é na pasta ~/Library/Logs no computador Mac.|  
|CCMNotifications -&lt;*Data_Hora*>. log|Regista atividades relacionadas com as notificações do Configuration Manager apresentadas no computador Mac.<br /><br /> Este ficheiro de registo está localizado na pasta ~/Library/Logs no computador Mac.|  
|CCMPrefPane -&lt;*Data_Hora*>. log|Regista atividades relacionadas com a caixa de diálogo de preferências do Configuration Manager no computador Mac, que inclui o estado geral e o registo de erros.<br /><br /> Este ficheiro de registo está localizado na pasta ~/Library/Logs no computador Mac.|  

O ficheiro de registo SMS_DM.log no servidor do sistema de site também regista a comunicação entre computadores Mac e o ponto de gestão que esteja configurado para dispositivos móveis e computadores Mac.  

##  <a name="BKMK_ServerLogs"></a>Ficheiros de registo do servidor de site do Configuration Manager  
 As secções seguintes listam os ficheiros de registo que estão no servidor do site ou que estão relacionados com funções de sistema de sites específicas.  

###  <a name="BKMK_SiteSiteServerLog"></a>Servidor e o local registos sistema de sites servidor  
 A tabela seguinte lista os ficheiros de registo que se encontrem no servidor de site do Configuration Manager e servidores de sistema de sites.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|adctrl.log|Regista a atividade de processamento de registo.|Servidor do site|  
|ADForestDisc.log|Regista ações da Deteção de Florestas do Active Directory.|Servidor do site|  
|ADService.log|Regista detalhes sobre grupos de segurança e a criação de contas no Active Directory.|Servidor do site|  
|adsgdis.log|Regista ações da Deteção de Grupos do Active Directory.|Servidor do site|  
|adsysdis.log|Regista ações da Deteção de Sistemas do Active Directory.|Servidor do site|  
|adusrdis.log|Regista ações da Deteção de Utilizadores do Active Directory.|Servidor do site|  
|ccm.log|Regista atividades de instalação push de cliente.|Servidor do site|  
|CertMgr.log|Regista as atividades para comunicações intra-site de certificados.|Servidor do sistema de sites|  
|chmgr.log|Regista atividades do gestor de estado de funcionamento de cliente.|Servidor do site|  
|Cidm.log|Regista alterações das definições de cliente efetuadas pelo CIDM (Client Install Data Manager).|Servidor do site|  
|colleval.log|Regista detalhes sobre o momento de criação, alteração e eliminação das coleções pelo Avaliador de Coleção.|Servidor do site|  
|compmon.log|Regista o estado de threads de componentes monitorizados para o servidor do site.|Servidor do sistema de sites|  
|compsumm.log|Regista tarefas do Summarizer de Estado do Componente.|Servidor do site|  
|ComRegSetup.log|Regista a instalação inicial de resultados de registo COM para um servidor do site.|Servidor do sistema de sites|  
|dataldr.log|Regista informações sobre o processamento de ficheiros MIF e inventário de hardware na base de dados do Configuration Manager.|Servidor do site|  
|ddm.log|Regista atividades do gestor de dados de deteção.|Servidor do site|  
|despool.log|Regista transferências de comunicação site a site recebidas.|Servidor do site|  
|distmgr.log|Regista detalhes sobre a criação de pacotes, compressão, replicação de diferenças e atualizações de informações.|Servidor do site|  
|EPCtrlMgr.log|Regista informações sobre a sincronização de informações de ameaças de software maligno entre o servidor de função do sistema do site do Endpoint Protection com a base de dados do Configuration Manager.|Servidor do site|  
|EPMgr.log|Regista o estado da função de sistema de sites do Endpoint Protection.|Servidor do sistema de sites|  
|EPSetup.log|Fornece informações sobre a instalação da função de sistema de sites do Endpoint Protection.|Servidor do sistema de sites|  
|EnrollSrv.log|Regista atividades do processo do serviço de registo.|Servidor do sistema de sites|  
|EnrollWeb.log|Regista atividades do processo do Web site de registo.|Servidor do sistema de sites|  
|fspmgr.log|Regista atividades da função de sistema de sites do ponto de estado de contingência.|Servidor do sistema de sites|  
|hman.log|Regista informações sobre as alterações de configuração do site e sobre a publicação de informações do site nos serviços de domínio do Active Directory.|Servidor do site|  
|Inboxast.log|Regista os ficheiros que são movidos do ponto de gestão para a pasta A RECEBER correspondente no servidor do site.|Servidor do site|  
|inboxmgr.log|Regista atividades de transferência de ficheiros entre pastas A Receber.|Servidor do site|  
|inboxmon.log|Regista o processamento de ficheiros a receber e atualizações de contadores de desempenho.|Servidor do site|  
|invproc.log|Regista o reencaminhamento de ficheiros MIF de um site secundário para o seu site principal.|Servidor do site|  
|migmctrl.log|Regista informações de ações de migração que envolvam tarefas de migração, pontos de distribuição partilhados e atualizações de pontos de distribuição.|Site de nível superior na hierarquia do Configuration Manager e cada site primário subordinado.<br /><br /> Numa hierarquia com múltiplos sites primários, utilize o ficheiro de registo é criado no site de administração central.|  
|mpcontrol.log|Regista o registo do ponto de gestão com o Windows Internet Name Service (WINS). Regista a disponibilidade do ponto de gestão a cada 10 minutos.|Servidor do sistema de sites|  
|mpfdm.log|Regista as ações do componente do ponto de gestão que move ficheiros de cliente para a pasta A RECEBER correspondente no servidor do site.|Servidor do sistema de sites|  
|mpMSI.log|Regista detalhes sobre a gestão de instalação do ponto.|Servidor do site|  
|MPSetup.log|Regista o processo do wrapper de instalação do ponto de gestão.|Servidor do site|  
|netdisc.log|Regista ações da Deteção de Rede.|Servidor do site|  
|ntsvrdis.log|Regista a atividade de deteção de servidores de sistema de sites.|Servidor do site|  
|Objreplmgr|Regista o processamento de notificações de alteração de objetos para replicação.|Servidor do site|  
|offermgr.log|Regista atualizações de anúncios.|Servidor do site|  
|offersum.log|Regista o resumo das mensagens de estado de implementação.|Servidor do site|  
|OfflineServicingMgr.log|Regista as atividades de aplicação de atualizações a ficheiros de imagem de sistema operativo.|Servidor do site|  
|outboxmon.log|Regista o processamento de ficheiros a enviar e atualizações de contadores de desempenho.|Servidor do site|  
|PerfSetup.log|Regista os resultados da instalação de contadores de desempenho.|Servidor do sistema de sites|  
|PkgXferMgr.log|Regista as ações do componente do SMS_Executive que é responsável pelo envio de conteúdo de um site primário para um ponto de distribuição remoto.|Servidor do site|  
|policypv.log|Regista as atualizações das políticas de cliente para refletir as alterações das implementações ou definições de cliente.|Servidor do site principal|  
|rcmctrl.log|Regista as atividades de replicação de base de dados entre sites na hierarquia.|Servidor do site|  
|replmgr.log|Regista a replicação de ficheiros entre os componentes do servidor do site e o componente do Programador.|Servidor do site|  
|ResourceExplorer.log|Regista erros, avisos e informações sobre como executar o Explorador de recursos.|Computador que executa a consola do Configuration Manager|  
|ruleengine.log|Regista detalhes sobre regras de implementação automática para a identificação, transferência de conteúdo e criação de implementação e de grupos de atualização de software.|Servidor do site|  
|Schedule.log|Regista detalhes sobre replicação de ficheiros e tarefas site a site.|Servidor do site|  
|Sender.log|Regista os ficheiros que são transferidos entre sites através de replicação baseada em ficheiros.|Servidor do site|  
|sinvproc.log|Regista informações sobre o processamento de dados de inventário de software para a base de dados do site.|Servidor do site|  
|sitecomp.log|Regista detalhes sobre a manutenção dos componentes instalados do site em todos os servidores de sistema de sites do site.|Servidor do site|  
|sitectrl.log|Regista as alterações de definições do site efetuadas nos objetos de controlo do site na base de dados.|Servidor do site|  
|sitestat.log|Regista a disponibilidade e o processo de monitorização do espaço em disco de todos os sistemas.|Servidor do site|  
|SmsAdminUI.log|Regista a atividade de consola do Configuration Manager.|Computador que executa a consola do Configuration Manager|  
|SMSAWEBSVCSetup.log|Regista as atividades de instalação do serviço Web do Catálogo de Aplicações.|Servidor do sistema de sites|  
|smsbkup.log|Regista a saída do processo de cópia de segurança do site.|Servidor do site|  
|smsdbmon.log|Regista alterações de bases de dados.|Servidor do site|  
|SMSENROLLSRVSetup.log|Regista as atividades de instalação do serviço Web de registo.|Servidor do sistema de sites|  
|SMSENROLLWEBSetup.log|Regista as atividades de instalação do Web site de registo.|Servidor do sistema de sites|  
|smsexec.log|Regista o processamento de todos os threads de componentes de servidor do site.|Servidor do site ou servidor de sistema de sites|  
|SMSFSPSetup.log|Regista mensagens geradas pela instalação de um ponto de estado de contingência.|Servidor do sistema de sites|  
|SMSPORTALWEBSetup.log|Regista as atividades de instalação do Web site do Catálogo de Aplicações.|Servidor do sistema de sites|  
|SMSProv.log|Regista o acesso do fornecedor WMI à base de dados do site.|Computador com o Fornecedor de SMS|  
|srsrpMSI.log|Regista resultados detalhados do processo de instalação do ponto de relatório a partir da saída MSI.|Servidor do sistema de sites|  
|srsrpsetup.log|Regista resultados do processo de instalação do ponto de relatório.|Servidor do sistema de sites|  
|statesys.log|Regista o processamento de mensagens de sistema de estado.|Servidor do site|  
|statmgr.log|Regista a escrita de todas as mensagens de estado na base de dados.|Servidor do site|  
|swmproc.log|Regista o processamento de ficheiros e definições de medição.|Servidor do site|  

###  <a name="BKMK_SiteInstallLog"></a>Ficheiros de registo de instalação de servidor do site  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com a instalação do site.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|ConfigMgrPrereq.log|Regista componentes de pré-requisitos e instalação de avaliação atividades.|Servidor do site|  
|ConfigMgrSetup.log|Regista a saída do programa de configuração de servidor do site detalhada.|Servidor do Site|  
|ConfigMgrSetupWizard.log|Regista informações relacionadas com a atividade no Assistente de configuração.|Servidor do Site|  
|SMS_BOOTSTRAP.log|Regista informações sobre o progresso do início do processo de instalação do site secundário. Os detalhes do processo de configuração estão contidos no ficheiro ConfigMgrSetup.log.|Servidor do Site|  
|smstsvc.log|Regista informações sobre a instalação, utilização e remoção de um serviço do Windows que é utilizado para testar a conectividade de rede e as permissões entre servidores, utilizando a conta de computador do servidor que inicia a ligação.|Servidor do site e o servidor do sistema de sites|  

###  <a name="BKMK_FSPLog"></a>Ficheiros de registo do ponto de estado de contingência  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com o ponto de estado de contingência.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|FspIsapi|Regista detalhes sobre comunicações com o ponto de estado de contingência a partir de clientes legados de dispositivos móveis e de computadores cliente.|Servidor do sistema de sites|  
|fspMSI.log|Regista mensagens geradas pela instalação de um ponto de estado de contingência.|Servidor do sistema de sites|  
|fspmgr.log|Regista atividades da função de sistema de sites do ponto de estado de contingência.|Servidor do sistema de sites|  

###  <a name="BKMK_MPLog"></a>Ficheiros de registo do ponto de gestão  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com o ponto de gestão.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|CcmIsapi.log|Regista atividades de mensagens de cliente no ponto final.|Servidor do sistema de sites|  
|MP_CliReg.log|Regista a atividade de registo de cliente processada pelo ponto de gestão.|Servidor do sistema de sites|  
|MP_Ddr.log|Regista a conversão de XML.ddr registos de clientes e, em seguida, copia-os para o servidor do site.|Servidor do sistema de sites|  
|MP_Framework.log|Regista as atividades do ponto de gestão central e dos componentes da estrutura de cliente.|Servidor do sistema de sites|  
|MP_GetAuth.log|Regista a atividade de autorização de cliente.|Servidor do sistema de sites|  
|MP_GetPolicy.log|Regista a atividade de pedidos de política de computadores cliente.|Servidor do sistema de sites|  
|MP_Hinv.log|Regista detalhes sobre a conversão de registos de inventário de hardware XML a partir de clientes e a cópia desses ficheiros para o servidor do site.|Servidor do sistema de sites|  
|MP_Location.log|Regista a atividade de pedido e resposta de localização a partir de clientes.|Servidor do sistema de sites|  
|MP_OOBMgr.log|Regista as atividades do ponto de gestão relacionados com a receção de uma OTP de um cliente.|Servidor do sistema de sites|  
|MP_Policy.log|Regista a comunicação de políticas.|Servidor do sistema de sites|  
|MP_Relay.log|Regista a transferência de ficheiros que são recolhidos do cliente.|Servidor do sistema de sites|  
|MP_Retry.log|Processos de repetição de inventário de hardware de registos.|Servidor do sistema de sites|  
|MP_Sinv.log|Regista detalhes sobre a conversão de registos de inventário de software XML a partir de clientes e a cópia desses ficheiros para o servidor do site.|Servidor do sistema de sites|  
|MP_SinvCollFile.log|Regista detalhes sobre a recolha de ficheiros.|Servidor do sistema de sites|  
|MP_Status.log|Regista detalhes sobre a conversão de ficheiros de mensagens de estado XML.svf a partir de clientes e a cópia desses ficheiros para o servidor do site.|Servidor do sistema de sites|  
|mpcontrol.log|Regista o registo do ponto de gestão com o WINS. Regista a disponibilidade do ponto de gestão a cada 10 minutos.|Servidor do site|  
|mpfdm.log|Regista as ações do componente do ponto de gestão que move ficheiros de cliente para a pasta A RECEBER correspondente no servidor do site.|Servidor do sistema de sites|  
|mpMSI.log|Regista detalhes sobre a gestão de instalação do ponto.|Servidor do site|  
|MPSetup.log|Regista o processo do wrapper de instalação do ponto de gestão.|Servidor do site|  

###  <a name="BKMK_SUPLog"></a>Ficheiros de registo do ponto de atualização de software  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com o ponto de atualização de software.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|objreplmgr.log|Regista detalhes sobre a replicação de software atualiza ficheiros de notificação de um site principal para sites subordinados.|Servidor do site|  
|PatchDownloader.log|Regista detalhes sobre o processo de transferência de atualizações de software da origem da atualização para o destino da transferência no servidor do site.|Computador que aloja a consola do Configuration Manager a partir da qual as transferências são iniciadas|  
|ruleengine.log|Regista detalhes sobre regras de implementação automática para a identificação, transferência de conteúdo e criação de implementação e de grupos de atualização de software.|Servidor do site|  
|SUPSetup.log|Regista detalhes sobre a instalação do ponto de atualização de software. Quando a instalação de ponto de atualização de software estiver concluída, é escrito **Instalação bem-sucedida** neste ficheiro de registo.|Servidor do sistema de sites|  
|WCM.log|Regista detalhes sobre a atualização de software ponto a configuração e ligações para o servidor WSUS para idiomas, classificações e categorias de atualização subscritas.|Servidor do site que liga ao servidor WSUS|  
|WSUSCtrl.log|Regista detalhes sobre a configuração, a conectividade de base de dados e o estado de funcionamento do servidor WSUS do site.|Servidor do sistema de sites|  
|wsyncmgr.log|Regista detalhes sobre o processo de sincronização de atualizações de software.|Servidor do sistema de sites|  
|WUSSyncXML.log|Regista detalhes sobre a ferramenta de inventário para o Microsoft Updates processo de sincronização.|Computador cliente configurado como o anfitrião de sincronização da ferramenta de inventário Updates da Microsoft|  

##  <a name="BKMK_FunctionLogs"></a>Ficheiros de registo para funcionalidade do Configuration Manager  
 A lista de secções seguintes ficheiros relacionados com funções do Gestor de configuração de registo.  

###  <a name="BKMK_AppManageLog"></a>Gestão de aplicações  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com a gestão de aplicações.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|AppIntentEval.log|Regista os detalhes sobre o estado atual e previsto das aplicações, a sua aplicabilidade, se os requisitos foram satisfeitos, os tipos de implementação e as dependências.|Cliente|  
|AppDiscovery.log|Regista os detalhes sobre a descoberta ou deteção de aplicações em computadores cliente.|Cliente|  
|AppEnforce.log|Regista os detalhes sobre medidas de imposição (instalar e desinstalar) tomadas para aplicações do cliente.|Cliente|  
|awebsctl.log|Função de sistema de sites do ponto de registos de monitorização de atividades para o serviço web do catálogo de aplicações.|Servidor do sistema de sites|  
|awebsvcMSI.log|Regista informações detalhadas de instalação da função do sistema de sites do ponto de serviço Web do Catálogo de Aplicações.|Servidor do sistema de sites|  
|Ccmsdkprovider.log|Regista as atividades do SDK de gestão de aplicações.|Cliente|  
|colleval.log|Regista detalhes sobre o momento de criação, alteração e eliminação das coleções pelo Avaliador de Coleção.|Servidor do sistema de sites|  
|ConfigMgrSoftwareCatalog.log|Regista a atividade do Catálogo de Aplicações, que inclui a sua utilização do Silverlight.|Cliente|  
|portlctl.log|Regista as atividades de monitorização da função do sistema de sites do ponto do Web site do Catálogo de Aplicações.|Servidor do sistema de sites|  
|portlwebMSI.log|Regista a atividade de instalação do MSI para a função de Web site do Catálogo de Aplicações.|Servidor do sistema de sites|  
|PrestageContent.log|Regista detalhes sobre a utilização da ferramenta ExtractContent.exe num ponto de distribuição remoto, pré-configurado. Esta ferramenta extrai o conteúdo exportado para um ficheiro.|Servidor do sistema de sites|  
|ServicePortalWebService.log|Regista a atividade do serviço Web do Catálogo de Aplicações.|Servidor do sistema de sites|  
|ServicePortalWebSite.log|Regista a atividade do Web site do Catálogo de Aplicações.|Servidor do sistema de sites|  
|SMSdpmon.log|Regista os detalhes sobre a tarefa agendada de monitorização do estado de funcionamento do ponto de distribuição configurada num ponto de distribuição.|Servidor do site|  
|SoftwareCatalogUpdateEndpoint.log|Regista atividades de gestão do URL para o catálogo de aplicações mostrado no Centro de Software.|Cliente|  
|SoftwareCenterSystemTasks.log|Regista atividades relacionadas com a validação de componentes de pré-requisitos do Centro de Software.|Cliente|  

 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com a implementação de pacotes e programas.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|colleval.log|Regista detalhes sobre o momento de criação, alteração e eliminação das coleções pelo Avaliador de Coleção.|Servidor do site|  
|execmgr.log|Regista os detalhes sobre pacotes e sequências de tarefas que são executados.|Cliente|  

###  <a name="BKMK_AILog"></a>Do Asset intelligence  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com o Asset Intelligence.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|AssetAdvisor.log|Regista as atividades das ações de inventário do Asset Intelligence.|Cliente|  
|aikbmgr.log|Regista os detalhes sobre o processamento de ficheiros XML a partir da caixa de entrada para atualização do catálogo do Asset Intelligence.|Servidor do site|  
|AIUpdateSvc.log|Regista a interação de sincronização do Asset Intelligence ponto com o System Center Online (SCO), o serviço online web.|Servidor do sistema de sites|  
|AIUSMSI.log|Função de sistema de sites do ponto de regista os detalhes sobre a instalação da sincronização do Asset Intelligence.|Servidor do sistema de sites|  
|AIUSSetup.log|Função de sistema de sites do ponto de regista os detalhes sobre a instalação da sincronização do Asset Intelligence.|Servidor do sistema de sites|  
|ManagedProvider.log|Regista os detalhes sobre a deteção de software com uma etiqueta de identificação de software associada. Regista ainda as atividades relacionadas com o inventário de hardware.|Servidor do sistema de sites|  
|MVLSImport.log|Regista os detalhes sobre o processamento de ficheiros de licenciamento importados.|Servidor do sistema de sites|  

###  <a name="BKMK_BnRLog"></a>Cópia de segurança e recuperação  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com ações de cópia de segurança e recuperação incluindo reposições do site e alterações ao fornecedor de SMS.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|ConfigMgrSetup.log|Regista informações sobre as tarefas de configuração e recuperação quando o Configuration Manager recupera um site a partir da cópia de segurança.|Servidor do site|  
|Smsbkup.log|Regista os detalhes sobre a atividade de cópia de segurança do site.|Servidor do site|  
|smssqlbkup.log|Regista a saída do processo de cópia de segurança de base de dados de site quando o SQL Server é instalado num servidor que não seja o servidor do site.|Servidor da base de dados do site|  
|Smswriter.log|Regista informações sobre o estado do escritor de VSS do Configuration Manager que é utilizado pelo processo de cópia de segurança.|Servidor do site|  

###  <a name="BKMK_CertificateEnrollment"></a>Inscrição de certificados  
 A tabela seguinte lista os ficheiros de registo do Configuration Manager que contêm informações relacionadas com a inscrição de certificados. Inscrição de certificado utiliza o ponto de registo de certificados e o módulo de política do Configuration Manager no servidor que está a executar o serviço de inscrição de dispositivos de rede.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|Crp.log|Regista atividades de inscrição.|Ponto de registo de certificados|  
|Crpctrl.log|Regista o estado de funcionamento operacional do ponto de registo de certificados.|Ponto de registo de certificados|  
|Crpsetup.log|Regista os detalhes sobre a instalação e a configuração do ponto de registo de certificados.|Ponto de registo de certificados|  
|Crpmsi.log|Regista os detalhes sobre a instalação e a configuração do ponto de registo de certificados.|Ponto de registo de certificados|  
|NDESPlugin.log|Registos de desafio verificação e das atividades de inscrição de certificados.|Módulo de política do Configuration Manager e o serviço de inscrição de dispositivos de rede|  

 Para além dos ficheiros de registo do Configuration Manager, consulte os registos de aplicação do Windows no Visualizador de eventos do servidor que executa o serviço de inscrição de dispositivos de rede e o servidor que aloja o ponto de registo de certificados. Por exemplo, procure mensagens da origem **NetworkDeviceEnrollmentService**. Também pode utilizar os seguintes ficheiros de registo:  

-   Ficheiros de registo do IIS para o serviço de inscrição de dispositivos de rede:  **&lt;caminho\>\inetpub\logs\LogFiles\W3SVC1**  

-   Os ficheiros para o ponto de registo de certificados de registo do IIS:  **&lt;caminho\>\inetpub\logs\LogFiles\W3SVC1**  

-   Ficheiro de registo da Política de Inscrição de Dispositivos de Rede: **mscep.log**  

    > [!NOTE]  
    >  Este ficheiro está localizado na pasta do perfil da conta do Serviço de Inscrição de Dispositivos de Rede, por exemplo, em C:\Users\SCEPSvc. Para obter mais informações sobre como ativar o registo do Serviço de Inscrição de Dispositivos de Rede, veja a secção [Ativar Registo](http://go.microsoft.com/fwlink/?LinkId=320576) no Serviço de Inscrição de Dispositivos de Rede (NDES) do artigo dos Serviços de Certificados do Active Directory (AD CS) da Wiki da TechNet.  

###  <a name="BKMK_BGB"></a>Notificação do cliente  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com a notificação do cliente.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|bgbmgr.log|Regista detalhes sobre atividades de servidor do site relacionadas com as tarefas de notificação de cliente e de processamento online e de ficheiros de estado de tarefa.|Servidor do site|  
|BGBServer.log|Regista as atividades do servidor de notificação, como comunicações cliente-servidor e atribuição tarefas a clientes. Também regista informações sobre a geração de online e os ficheiros de estado de tarefa para serem enviados ao servidor do site.|Ponto de gestão|  
|BgbSetup.log|Regista as atividades do processo de wrapper de instalação de servidor de notificação durante a instalação e desinstalação.|Ponto de gestão|  
|bgbisapiMSI.log|Regista detalhes sobre a instalação de servidor de notificação e a desinstalação.|Ponto de gestão|  
|BgbHttpProxy.log|Regista as atividades do proxy de HTTP de notificação enquanto reencaminha as mensagens de clientes utilizando o HTTP de e para o servidor de notificação.|Cliente|  
|CcmNotificationAgent.log|Regista as atividades do agente de notificação, como comunicações cliente-servidor e informações sobre as tarefas de receberam e distribuídas por outros agentes de cliente.|Cliente|  

### <a name="cloud-management-gateway"></a>Gateway de gestão de nuvem

A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com o gateway de gestão de nuvem.

||||
|-|-|-|
|Nome do registo|Descrição|Computador com o ficheiro de registo|
|CloudMgr.log|Regista detalhes sobre como implementar o serviço de gateway de gestão de nuvem, o estado de interrupção contínua do serviço e a utilizar os dados associados ao serviço.<br>Pode configurar o nível de registo de editar o registo **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_CLOUD_SERVICES_MANAGER\Logging nível**|O *installdir* pasta no servidor de site primário ou ACs.|
|CMGSetup.log ou CMG -*RoleInstanceID*-CMGSetup.log<sup>1</sup>|Regista detalhes sobre a fase de 2nd da implementação de gateway de gestão da nuvem (implementação local no Azure)<br>Pode configurar o nível de registo utilizando a definição **nível de rastreio** (**informações** (predefinida), **verboso**, **erro**) no **configuração de serviços do Azure portal\Cloud** separador.|O **%approot%\logs** no seu servidor do Azure ou a pasta SMS/Logs no servidor do sistema de sites|
|CMGHttpHandler.log ou CMG -*RoleInstanceID*-CMGHttpHandler.log<sup>1</sup>|Regista detalhes sobre o enlace de processador de http de gateway de gestão do cloud com serviços de informação de Internet no Azure<br>Pode configurar o nível de registo utilizando a definição **nível de rastreio** (**informações** (predefinida), **verboso**, **erro**) no **configuração de serviços do Azure portal\Cloud** separador.|O **%approot%\logs** no seu servidor do Azure ou a pasta SMS/Logs no servidor do sistema de sites|
|CMGService.log ou CMG -*RoleInstanceID*-CMGService.log<sup>1</sup>|Regista detalhes sobre o componente de núcleo de serviço de gateway de gestão do cloud no Azure<br>Pode configurar o nível de registo utilizando a definição **nível de rastreio** (**informações** (predefinida), **verboso**, **erro**) no **configuração de serviços do Azure portal\Cloud** separador.|O **%approot%\logs** no seu servidor do Azure ou a pasta SMS/Logs no servidor do sistema de sites|
|SMS_Cloud_ProxyConnector.log|Regista detalhes sobre como configurar ligações entre o serviço de gateway de gestão de nuvem e a ligação de gateway de gestão de nuvem ponto.|Servidor do sistema de sites|

<sup>1</sup> estes são os ficheiros de registo do Configuration Manager local na nuvem a sincronização de Gestor do serviço de armazenamento do Azure a cada 5 minutos. O gateway de gestão de nuvem transmite os registos para o armazenamento do Azure a cada 5 minutos. por isso, o atraso máximo será de 10 minutos. Comutadores verbosos irão afetar os registos de locais e remotos.

- Para resolver problemas com implementações, utilize **CloudMgr.log** e **CMGSetup.log**
- Para resolver problemas com o estado de funcionamento do serviço, utilize **CMGService.log** e **SMS_Cloud_ProxyConnector.log**.
- Para resolver problemas com o tráfego de cliente, utilize **CMGHttpHandler.log**, **CMGService.log**, e **SMS_Cloud_ProxyConnector.log**.

###  <a name="BKMK_CompSettingsLog"></a>Definições de compatibilidade e acesso a recursos da empresa  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com as definições de compatibilidade e o acesso a recursos da empresa.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|CIAgent.log|Regista os detalhes sobre o processo de remediação e compatibilidade das definições de compatibilidade, atualizações de software e gestão de aplicações.|Cliente|  
|CITaskManager.log|Regista informações sobre o agendamento da tarefa de itens de configuração.|Cliente|  
|DCMAgent.log|Regista informações de alto nível sobre a avaliação, a comunicação de conflitos e a remediação de itens de configuração e aplicações.|Cliente|  
|DCMReporting.log|Regista informações sobre os relatórios de resultados da plataforma de política em mensagens de estado para itens de configuração.|Cliente|  
|DcmWmiProvider.log|Regista informações sobre a leitura de synclets de itens de configuração a partir da WMI.|Cliente|  

###  <a name="BKMK_ConsoleLog"></a>Consola do Configuration Manager  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com a consola do Configuration Manager.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|ConfigMgrAdminUISetup.log|Regista a instalação da consola do Configuration Manager.|Computador que executa a consola do Configuration Manager|  
|SmsAdminUI.log|Regista informações sobre o funcionamento da consola do Configuration Manager.|Computador que executa a consola do Configuration Manager|  
|Smsprov.log|Regista atividades executadas pelo fornecedor de SMS. As atividades da consola do Configuration Manager utilizam o fornecedor de SMS.|Servidor do site ou servidor de sistema de sites|  

###  <a name="BKMK_ContentLog"></a>Gestão de conteúdo  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com a gestão de conteúdos.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|Clouddp-<nomedoserviço>.log&lt;guid\>. log|Regista os detalhes de um ponto de distribuição baseado na nuvem específico, incluindo informações sobre armazenamento e acesso ao conteúdo.|Servidor do sistema de sites|  
|CloudMgr.log|Regista detalhes sobre o aprovisionamento de conteúdo, recolha as ações iniciadas pelo administrador para interromper ou iniciar o serviço em nuvem que executa um ponto de distribuição baseados na nuvem, armazenamento e estatísticas de largura de banda.|Servidor do sistema de sites|  
|DataTransferService.log|Regista todas as comunicações BITS para acesso a políticas ou pacotes. Este registo também é utilizado para gestão de conteúdos por pontos de distribuição de solicitação.|Computador que está configurado como um ponto de distribuição de solicitação|  
|PullDP.log|Regista os detalhes sobre o conteúdo que o ponto de distribuição de extração transfere dos pontos de distribuição de origem.|Computador que está configurado como um ponto de distribuição de solicitação|  
|PrestageContent.log|Ferramenta regista os detalhes sobre a utilização de ExtractContent.exe num ponto de distribuição remoto, pré-configurado. Esta ferramenta extrai o conteúdo exportado para um ficheiro.|Função do sistema de sites|  
|SMSdpmon.log|Regista detalhes sobre o estado de funcionamento do ponto de distribuição monitorização tarefas agendadas que estão configuradas num ponto de distribuição.|Função do sistema de sites|  
|smsdpprov.log|Regista os detalhes sobre a extração de ficheiros comprimidos recebidos de um site primário. Este registo é gerado pelo fornecedor WMI do ponto de distribuição remoto.|Computador de ponto de distribuição que não seja colocalizado com o servidor do site|  


###  <a name="BKMK_DiscoveryLog"></a>Deteção  
A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com a deteção.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|adsgdis.log|Regista ações da Deteção de Grupos de Segurança do Active Directory.|Servidor do site|  
|adsysdis.log|Regista ações da Deteção de Sistemas do Active Directory.|Servidor do site|  
|adusrdis.log|Regista ações da Deteção de Utilizadores do Active Directory.|Servidor do site|  
|ADForestDisc.Log|Regista ações da Deteção de Florestas do Active Directory.|Servidor do site|  
|ddm.log|Regista atividades do gestor de dados de deteção.|Servidor do site|  
|InventoryAgent.log|Regista atividades de inventário de hardware, inventário de software e ações de deteção de heartbeat no cliente.|Cliente|  
|netdisc.log|Regista ações da Deteção de Rede.|Servidor do site|  

###  <a name="BKMK_EPLog"></a>Endpoint Protection  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com o Endpoint Protection.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|EndpointProtectionAgent.log|Regista os detalhes sobre a instalação do cliente do Endpoint Protection e a aplicação da política antimalware a esse cliente.|Cliente|  
|EPCtrlMgr.log|Regista detalhes sobre a sincronização de informações de ameaças de software maligno entre o servidor da função Endpoint Protection com a base de dados do Configuration Manager.|Servidor do sistema de sites|  
|EPMgr.log|Monitoriza o estado da função do sistema de sites do Endpoint Protection.|Servidor do sistema de sites|  
|EPSetup.log|Fornece informações sobre a instalação da função de sistema de sites do Endpoint Protection.|Servidor do sistema de sites|  

###  <a name="BKMK_Extensions"></a>Extensões  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com extensões.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|AdminUI.ExtensionInstaller.log|Regista informações sobre a transferência de extensões da Microsoft e sobre a instalação e desinstalação de todas as extensões.|Computador que executa a consola do Configuration Manager|  
|FeatureExtensionInstaller.log|Regista informações sobre a instalação e remoção de extensões individuais quando estão ativadas ou desativadas na consola do Configuration Manager.|Computador que executa a consola do Configuration Manager|  
|SmsAdminUI.log|Regista a atividade de consola do Configuration Manager.|Computador que executa a consola do Configuration Manager|  

###  <a name="BKMK_InventoryLog"></a>Inventário  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com o processamento de dados de inventário.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|dataldr.log|Regista informações sobre o processamento de ficheiros MIF e inventário de hardware na base de dados do Configuration Manager.|Servidor do site|  
|invproc.log|Regista o reencaminhamento de ficheiros MIF de um site secundário para o seu site principal.|Servidor do Site Secundário|  
|sinvproc.log|Regista informações sobre o processamento de dados de inventário de software para a base de dados do site.|Servidor do site|  

###  <a name="BKMK_MeteringLog"></a>Medição  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com a medição.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|mtrmgr.log|Monitoriza todos os processos de medição de software.|Servidor do site|  

###  <a name="BKMK_MigrationLog"></a>Migração  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com a migração.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|migmctrl.log|Regista informações sobre ações de migração que envolvam tarefas de migração, pontos de distribuição partilhados e atualizações de pontos de distribuição.|Site de nível superior na hierarquia do Configuration Manager e cada site primário subordinado.<br /><br /> Numa hierarquia com vários sites primários, utilize o ficheiro de registo criado no site de administração central.|  

###  <a name="BKMK_MDMLog"></a>Dispositivos móveis  
 As secções seguintes listam os ficheiros de registo que contêm informações relacionadas com a gestão de dispositivos móveis.  

####  <a name="BKMK_EnrollmentLog"></a>Inscrição  
 A tabela seguinte lista registos que contêm informações relacionadas com a inscrição de dispositivos móveis.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|DMPRP.log|Regista a comunicação entre os pontos de gestão ativados para dispositivos móveis e os pontos finais do ponto de gestão.|Servidor do sistema de sites|  
|dmpmsi.log|Regista os dados do Windows Installer para a configuração de um ponto de gestão ativado para dispositivos móveis.|Servidor do sistema de sites|  
|DMPSetup.log|Regista a configuração do ponto de gestão quando este está ativado para dispositivos móveis.|Servidor do sistema de sites|  
|enrollsrvMSI.log|Regista os dados do Windows Installer para a configuração de um ponto de registo.|Servidor do sistema de sites|  
|enrollmentweb.log|Regista a comunicação entre dispositivos móveis e o ponto proxy de registo.|Servidor do sistema de sites|  
|enrollwebMSI.log|Regista os dados do Windows Installer para a configuração de um ponto proxy de registo.|Servidor do sistema de sites|  
|enrollmentservice.log|Regista a comunicação entre um ponto proxy de registo e um ponto de registo.|Servidor do sistema de sites|  
|SMS_DM.log|Regista a comunicação entre dispositivos móveis, computadores Mac e o ponto de gestão ativado para dispositivos móveis e computadores Mac.|Servidor do sistema de sites|  

####  <a name="BKMK_ExchSrvLog"></a>Conector do Exchange Server  
 Os seguintes registos contêm informações relacionadas com o conector do Exchange Server.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|easdisc.log|Regista as atividades e o estado do conector do Exchange Server.|Servidor do site|  

####  <a name="BKMK_MDLegLog"></a>Legado do dispositivo móvel  
 A tabela seguinte lista registos que contêm informações relacionadas com o cliente legado do dispositivo móvel.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|DmCertEnroll.log|Regista os detalhes sobre os dados de inscrição do certificado em clientes legados de dispositivos móveis.|Cliente|  
|DMCertResp.htm|Regista a resposta HTML a partir do servidor de certificado quando o programa de inscrição do cliente legado do dispositivo móvel solicita um certificado PKI.|Cliente|  
|DmClientHealth.log|Regista os GUIDs de todos os clientes legados de dispositivos móveis que comunicam com o ponto de gestão ativado para dispositivos móveis.|Servidor do sistema de sites|  
|DmClientRegistration.log|Regista os pedidos e respostas de registo de e para clientes legados de dispositivos móveis.|Servidor do sistema de sites|  
|DmClientSetup.log|Regista os dados da configuração do cliente para clientes legados de dispositivos móveis.|Cliente|  
|DmClientXfer.log|Regista os dados de transferência do cliente para clientes legados de dispositivos móveis e para implementações do ActiveSync.|Cliente|  
|DmCommonInstaller.log|Regista a instalação do ficheiro de transferência do cliente para a configuração de ficheiros de transferência de clientes legados de dispositivos móveis.|Cliente|  
|DmInstaller.log|Regista se o DMInstaller chama corretamente o DmClientSetup e se o DmClientSetup sai com sucesso ou falha em clientes legados de dispositivos móveis.|Cliente|  
|DmpDatastore.log|Regista todas as ligações de base de dados do site e consultas efetuadas pelo ponto de gestão ativado para dispositivos móveis.|Servidor do sistema de sites|  
|DmpDiscovery.log|Regista todos os dados de deteção dos clientes legados de dispositivos móveis no ponto de gestão ativado para dispositivos móveis.|Servidor do sistema de sites|  
|DmpHardware.log|Regista dados de inventário de hardware dos clientes legados de dispositivos móveis no ponto de gestão ativado para dispositivos móveis.|Servidor do sistema de sites|  
|DmpIsapi.log|Regista a comunicação do cliente legado de dispositivos móveis com um ponto de gestão ativado para dispositivos móveis.|Servidor do sistema de sites|  
|dmpmsi.log|Regista os dados do Windows Installer para a configuração de um ponto de gestão ativado para dispositivos móveis.|Servidor do sistema de sites|  
|DMPSetup.log|Regista a configuração do ponto de gestão quando este está ativado para dispositivos móveis.|Servidor do sistema de sites|  
|DmpSoftware.log|Regista dados de distribuição de software dos clientes legados de dispositivos móveis no ponto de gestão ativado para dispositivos móveis.|Servidor do sistema de sites|  
|DmpStatus.log|Regista dados de mensagens de estado de clientes de dispositivos móveis no ponto de gestão ativado para dispositivos móveis.|Servidor do sistema de sites|  
|DmSvc.log|Regista a comunicação de cliente dos clientes legados de dispositivos móveis com um ponto de gestão ativado para dispositivos móveis.|Cliente|  
|FspIsapi.log|Regista detalhes sobre comunicações com o ponto de estado de contingência a partir de clientes legados de dispositivos móveis e de computadores cliente.|Servidor do sistema de sites|  

###  <a name="BKMK_OSDLog"></a>Implementação do sistema operativo  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com a implementação do sistema operativo.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|CAS.log|Regista detalhes quando são encontrados pontos de distribuição para conteúdo referenciado.|Cliente|  
|ccmsetup.log|Regista tarefas do ccmsetup para a configuração de cliente, atualização de cliente e remoção de cliente. Pode ser utilizado para resolver problemas de instalação de cliente.|Cliente|  
|CreateTSMedia.log|Regista detalhes para a criação de suportes de dados de sequências de tarefas.|Computador que executa a consola do Configuration Manager|  
|DeployToVhd.log|Regista detalhes sobre o processo de criação e modificação do disco rígido Virtual (VHD).|Computador que executa a consola do Configuration Manager|  
|Dism.log|Regista ações de instalação de controladores ou ações de aplicação de atualizações para manutenção offline.|Servidor do sistema de sites|  
|Distmgr.log|Regista detalhes sobre a configuração de ativação de um ponto de distribuição para o ambiente de execução de Preboot (PXE).|Servidor do sistema de sites|  
|DriverCatalog.log|Regista detalhes sobre controladores de dispositivo importados para o catálogo de controladores.|Servidor do sistema de sites|  
|mcsisapi.log|Regista informações de transferência de pacotes multicast e respostas de pedidos de cliente.|Servidor do sistema de sites|  
|mcsexec.log|Verificação de estado de funcionamento de registos, espaço de nomes, criação de sessões e certificado de verificação ações.|Servidor do sistema de sites|  
|mcsmgr.log|Regista alterações da configuração, o modo de segurança e disponibilidade.|Servidor do sistema de sites|  
|mcsprv.log|Regista a interação do fornecedor de multicast com os Serviços de Implementação do Windows (WDS).|Servidor do sistema de sites|  
|MCSSetup.log|Regista detalhes sobre a instalação da função de servidor multicast.|Servidor do sistema de sites|  
|MCSMSI.log|Regista detalhes sobre a instalação da função de servidor multicast.|Servidor do sistema de sites|  
|Mcsperf.log|Regista detalhes sobre as atualizações do contador de desempenho multicast.|Servidor do sistema de sites|  
|MP_ClientIDManager.log|Regista as respostas do ponto de gestão a sequências de tarefas de pedidos de ID de cliente iniciadas a partir de PXE ou de suportes de dados de arranque.|Servidor do sistema de sites|  
|MP_DriverManager.log|Regista as respostas do ponto de gestão a pedidos de ação da sequência de tarefas Aplicar Controlador Automaticamente.|Servidor do sistema de sites|  
|OfflineServicingMgr.log|Regista detalhes de agendas de manutenção offline e atualização aplicam ações em ficheiros de formato Windows Imaging (WIM) do sistema operativo.|Servidor do sistema de sites|  
|Setupact.log|Regista detalhes sobre os registos do Windows Sysprep e do programa de configuração.|Cliente|  
|Setupapi.log|Regista detalhes sobre os registos do Windows Sysprep e do programa de configuração.|Cliente|  
|Setuperr.log|Regista detalhes sobre os registos do Windows Sysprep e do programa de configuração.|Cliente|  
|smpisapi.log|Regista detalhes sobre as ações de captura e restauro do estado de cliente e informações de limiares.|Cliente|  
|Smpmgr.log|Regista detalhes sobre os resultados de verificações do estado de funcionamento do ponto de migração de estado e de alterações de configuração.|Servidor do sistema de sites|  
|smpmsi.log|Regista detalhes da instalação e configuração do ponto de migração de estado.|Servidor do sistema de sites|  
|smpperf.log|Regista as atualizações do contador de desempenho do ponto de migração de estado.|Servidor do sistema de sites|  
|smspxe.log|Regista detalhes sobre as respostas aos clientes que utilizem o arranque PXE e detalhes sobre a expansão de imagens de arranque e ficheiros do arranque.|Servidor do sistema de sites|  
|smssmpsetup.log|Regista detalhes da instalação e configuração do ponto de migração de estado.|Servidor do sistema de sites|  
|Smsts.log|Regista atividades de sequência de tarefas.|Cliente|  
|TSAgent.log|Regista o resultado de dependências de sequência de tarefas antes de iniciar uma sequência de tarefas.|Cliente|  
|TaskSequenceProvider.log|Regista detalhes sobre sequências de tarefas quando estas são importadas, exportadas ou editadas.|Servidor do sistema de sites|  
|loadstate.log|Regista detalhes sobre a Ferramenta de Migração de Estado de Utilizador (USMT) e o restauro de dados de estado do utilizador.|Cliente|  
|scanstate.log|Regista detalhes sobre a Ferramenta de Migração de Estado de Utilizador (USMT) e a captura de dados de estado do utilizador.|Cliente|  

###  <a name="BKMK_PowerMgmtLog"></a>Gestão de energia  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com a gestão de energia.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|pwrmgmt.log|Regista detalhes sobre atividades de gestão de energia no computador cliente, incluindo a monitorização e a imposição de definições pelo agente de cliente de gestão de energia.|Cliente|  

###  <a name="BKMK_RCLog"></a>Controlo remoto  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com controlo remoto.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|CMRcViewer.log|Regista detalhes sobre a atividade do visualizador de controlo remoto.|Na pasta % temp % no computador que executa o Visualizador de controlo remoto|  

###  <a name="BKMK_ReportLog"></a>Relatórios  
 A tabela seguinte lista os ficheiros de registo do Configuration Manager que contêm informações relacionadas com relatórios.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|srsrp.log|Regista informações sobre a atividade e o estado do ponto do Reporting Services.|Servidor do sistema de sites|  
|srsrpMSI.log|Regista resultados detalhados do processo de instalação do ponto do Reporting Services a partir da saída MSI.|Servidor do sistema de sites|  
|srsrpsetup.log|Regista resultados do processo de instalação do ponto do Reporting Services.|Servidor do sistema de sites|  

###  <a name="BKMK_RBALog"></a>Administração baseada em funções  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com a gestão da administração baseada em funções.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|hman.log|Regista informações sobre as alterações de configuração do site e a publicação de informações do site para serviços de domínio do Active Directory.|Servidor do site|  
|SMSProv.log|Regista o acesso do fornecedor WMI à base de dados do site.|Computador com o Fornecedor de SMS|  

###  <a name="BKMK_WITLog"></a>Ponto de ligação de serviço  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com o ponto de ligação de serviço.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|CertMgr.log|Regista informações de certificados e de contas proxy.|Servidor do site|  
|CollEval.log|Regista detalhes sobre o momento de criação, alteração e eliminação das coleções pelo Avaliador de Coleção.|Site primário e site de administração central|  
|Cloudusersync.log|Regista a ativação de licenças para os utilizadores.|Computador com o ponto de ligação de serviço|  
|Dataldr.log|Regista informações sobre o processamento de ficheiros MIF.|Servidor do site|  
|ddm.log|Regista atividades do gestor de dados de deteção.|Servidor do site|  
|Distmgr.log|Regista detalhes sobre pedidos de distribuição de conteúdo.|Servidor de site de nível superior|  
|Dmpdownloader.log|Regista detalhes sobre transferências do Microsoft Intune.|Computador com o ponto de ligação de serviço|  
|Dmpuploader.log|Regista detalhes relacionados para carregamento de alterações de base de dados para o Microsoft Intune.|Computador com o ponto de ligação de serviço|  
|hman.log|Regista informações sobre o reencaminhamento de mensagens.|Servidor do site|  
|objreplmgr.log|Regista o processamento de política e de atribuição.|Servidor do site principal|  
|PolicyPV.log|Regista a criação de política de todas as políticas.|Servidor do site|  
|outgoingcontentmanager.log|Transferência de conteúdo de registos para o Microsoft Intune.|Computador com o ponto de ligação de serviço|  
|Sitecomp.log|Regista os detalhes da instalação do ponto de ligação de serviço.|Servidor do site|  
|SmsAdminUI.log|Regista a atividade de consola do Configuration Manager.|Computador que executa a consola do Configuration Manager|  
|Smsprov.log|Regista atividades executadas pelo fornecedor de SMS. As atividades da consola do Configuration Manager utilizam o fornecedor de SMS.|Computador com o Fornecedor de SMS|  
|SrvBoot.log|Regista os detalhes sobre o serviço do instalador do ponto de ligação de serviço.|Computador com o ponto de ligação de serviço|  
|Statesys.log|Regista o processamento de mensagens de gestão de dispositivos móveis.|Site primário e site de administração central|  

###  <a name="BKMK_SU_NAPLog"></a>Atualizações de software  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com as atualizações de software.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|ccmperf.log|Regista atividades relacionadas com a manutenção e a captura de dados relacionados com os contadores de desempenho do cliente.|Cliente|  
|PatchDownloader.log|Regista detalhes sobre o processo de transferência de atualizações de software da origem da atualização para o destino da transferência no servidor do site.|Computador que aloja a consola do Configuration Manager a partir da qual as transferências são iniciadas|  
|PolicyEvaluator.log|Regista detalhes sobre a avaliação das políticas em computadores cliente, incluindo políticas de atualizações de software.|Cliente|  
|RebootCoordinator.log|Regista detalhes sobre a coordenação de reinícios do sistema em computadores cliente após instalações de atualizações de software.|Cliente|  
|ScanAgent.log|Regista detalhes sobre pedidos de análise de atualizações de software, a localização do WSUS e ações relacionadas.|Cliente|  
|SdmAgent.log|Regista detalhes sobre o controlo da remediação e conformidade. No entanto, o ficheiro de registo de atualizações de software, Updateshandler.log, fornece mais detalhes informativos sobre a instalação de atualizações de software que são necessárias para compatibilidade.<br /><br /> Este ficheiro de registo é partilhado com definições de compatibilidade.|Cliente|  
|ServiceWindowManager.log|Regista detalhes sobre a avaliação de janelas de manutenção.|Cliente|  
|SmsWusHandler.log|Regista detalhes sobre o processo de análise da Ferramenta de Inventário das Atualizações da Microsoft.|Cliente|  
|StateMessage.log|Regista detalhes sobre o software de atualização mensagens de estado que são criadas e enviadas para o ponto de gestão.|Cliente|  
|SUPSetup.log|Regista detalhes sobre a instalação do ponto de atualização de software. Quando a instalação de ponto de atualização de software estiver concluída, é escrito **Instalação bem-sucedida** neste ficheiro de registo.|Servidor do sistema de sites|  
|UpdatesDeployment.log|Regista detalhes sobre implementações no cliente, incluindo a ativação, avaliação e imposição de atualizações de software. O registo verboso mostra informações adicionais sobre a interação com a interface de utilizador do cliente.|Cliente|  
|UpdatesHandler.log|Regista detalhes sobre a análise de compatibilidade de atualizações de software e sobre a transferência e instalação de atualizações de software no cliente.|Cliente|  
|UpdatesStore.log|Regista detalhes sobre o estado de compatibilidade das atualizações de software que foram analisadas durante o ciclo de análise de compatibilidade.|Cliente|  
|WCM.log|Regista detalhes sobre o software de ligações e as configurações do ponto de atualização para o servidor WSUS para idiomas, classificações e categorias de atualização subscritas.|Servidor do site|  
|WSUSCtrl.log|Regista detalhes sobre a configuração, a conectividade de base de dados e o estado de funcionamento do servidor WSUS do site.|Servidor do sistema de sites|  
|wsyncmgr.log|Regista detalhes sobre o software de atualização do processo de sincronização.|Servidor do site|  
|WUAHandler.log|Regista detalhes sobre o Windows Update Agent no cliente quando este procura atualizações de software.|Cliente|  

###  <a name="BKMK_WOLLog"></a>Reativação por LAN  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com a utilização de reativação por LAN.  

> [!NOTE]  
>  Quando completar Wake On LAN utilizando um proxy de reativação, esta atividade é registada no cliente. Por exemplo, veja CcmExec.log and SleepAgent_ <*domínio* \> @SYSTEM_0.log no [operações de cliente](#BKMK_ClientOpLogs) secção deste tópico.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|wolcmgr.log|Regista detalhes sobre quais os clientes que devem receber pacotes de reativação, o número de pacotes de reativação enviados e o número de pacotes de reativação repetidos.|Servidor do site|  
|wolmgr.log|Regista detalhes sobre procedimentos de reativação automática, tais como a reativação de implementações que estão configuradas para Reativação por LAN.|Servidor do site|  

###  <a name="BKMK_WindowsServicingLog"></a>Manutenção do Windows 10  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com a manutenção do Windows 10.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|ccmperf.log|Regista atividades relacionadas com a manutenção e a captura de dados relacionados com os contadores de desempenho do cliente.|Cliente|  
|CcmRepair.log|Regista as atividades de reparação do agente de cliente.|Cliente|
|PatchDownloader.log|Regista detalhes sobre o processo de transferência de atualizações de software da origem da atualização para o destino da transferência no servidor do site.|Computador que aloja a consola do Configuration Manager a partir da qual as transferências são iniciadas|  
|PolicyEvaluator.log|Regista detalhes sobre a avaliação das políticas em computadores cliente, incluindo políticas de atualizações de software.|Cliente|  
|RebootCoordinator.log|Regista detalhes sobre a coordenação de reinícios do sistema em computadores cliente após instalações de atualizações de software.|Cliente|  
|ScanAgent.log|Regista detalhes sobre pedidos de análise de atualizações de software, a localização do WSUS e ações relacionadas.|Cliente|  
|SdmAgent.log|Regista detalhes sobre o controlo da remediação e conformidade. No entanto, o ficheiro de registo de atualizações de software, UpdatesHandler.log, fornece mais detalhes informativos sobre a instalação de atualizações de software que são necessárias para compatibilidade.<br /><br /> Este ficheiro de registo é partilhado com definições de compatibilidade.|Cliente|  
|ServiceWindowManager.log|Regista detalhes sobre a avaliação de janelas de manutenção.|Cliente|  
|Setupact.log|Ficheiro de registo primário para a maioria dos erros ocorridos durante o processo de instalação do Windows. O ficheiro de registo está localizado em % windir %\$Windows.~BT\sources\panther pasta.|Cliente|
|SmsWusHandler.log|Regista detalhes sobre o processo de análise da Ferramenta de Inventário das Atualizações da Microsoft.|Cliente|  
|StateMessage.log|Regista detalhes sobre as mensagens de estado de atualizações de software que são criadas e enviadas para o ponto de gestão.|Cliente|  
|SUPSetup.log|Regista detalhes sobre a instalação do ponto de atualização de software. Quando a instalação de ponto de atualização de software estiver concluída, é escrito **Instalação bem-sucedida** neste ficheiro de registo.|Servidor do sistema de sites|  
|UpdatesDeployment.log|Regista detalhes sobre implementações no cliente, incluindo a ativação, avaliação e imposição de atualizações de software. O registo verboso mostra informações adicionais sobre a interação com a interface de utilizador do cliente.|Cliente|  
|Updateshandler.log|Regista detalhes sobre a análise de compatibilidade de atualizações de software e sobre a transferência e instalação de atualizações de software no cliente.|Cliente|  
|UpdatesStore.log|Regista detalhes sobre o estado de compatibilidade das atualizações de software que foram analisadas durante o ciclo de análise de compatibilidade.|Cliente|  
|WCM.log|Regista detalhes sobre o software de ligações e as configurações do ponto de atualização para o servidor WSUS para idiomas, classificações e categorias de atualização subscritas.|Servidor do site|  
|WSUSCtrl.log|Regista detalhes sobre a configuração, a conectividade de base de dados e o estado de funcionamento do servidor WSUS do site.|Servidor do sistema de sites|  
|wsyncmgr.log|Regista detalhes sobre o software de atualização do processo de sincronização.|Servidor do site|  
|WUAHandler.log|Regista detalhes sobre o Windows Update Agent no cliente quando este procura atualizações de software.|Cliente|  

###  <a name="BKMK_WULog"></a>Agente do Windows Update  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com o Windows Update Agent.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|WindowsUpdate.log|Regista detalhes sobre quando o Windows Update Agent liga ao servidor WSUS e obtém as atualizações de software para avaliação de compatibilidade, e se existem atualizações para os componentes do agente.|Cliente|  

###  <a name="BKMK_WSUSLog"></a>Servidor WSUS  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com o servidor WSUS.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|Change.log|Regista detalhes sobre informações de base de dados de servidor WSUS foi alterada.|Servidor WSUS|  
|SoftwareDistribution.log|Regista detalhes sobre as atualizações de software que são sincronizados a partir da origem de atualização configurada para a base de dados do servidor WSUS.|Servidor WSUS|  
