---
title: Arquivos de log para o Configuration Manager | Microsoft Docs
description: Use arquivos de log para solucionar problemas em uma hierarquia do System Center Configuration Manager.
ms.custom: na
ms.date: 7/03/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c1ff371e-b0ad-4048-aeda-02a9ff08889e
caps.latest.revision: 9
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 5e1bc0063ab3d34410f7dbc773a5eacdd5eb6d2f
ms.openlocfilehash: 28597cf1cb269fff0872c7f79ef961496aea32ab
ms.contentlocale: pt-pt
ms.lasthandoff: 07/05/2017


---
# <a name="log-files-in-system-center-configuration-manager"></a>Ficheiros de registo no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

No System Center Configuration Manager, os componentes de servidor cliente e o site registram as informações de processo nos arquivos de log individuais. Você pode usar as informações nos arquivos de log para ajudá-lo a solucionar problemas que podem ocorrer em sua hierarquia do Configuration Manager. Por padrão, o log de componente de cliente e servidor está habilitado no Configuration Manager.   

 As seções a seguir fornecem detalhes sobre os arquivos de log diferentes disponíveis para você. Você pode usar essas informações para exibir e monitorar o cliente do Configuration Manager e os logs do servidor para obter detalhes de operação e para identificar o erro informações que podem ajudá-lo a solucionar quaisquer problemas.  

-   [Sobre arquivos de log do Configuration Manager](#BKMK_AboutLogs)  

    -   [Configurar opções de log usando o Configuration Manager Service Manager](#BKMK_LogOptions)  

    -   [Localizando logs do Configuration Manager](#BKMK_LogLocation)  

-   [Logs de cliente do Configuration Manager](#BKMK_ClientLogs)  

    -   [Operações do cliente](#BKMK_ClientOpLogs)  

    -   [Arquivos de log de instalação do cliente](#BKMK_ClientInstallLog)  

    -   [Cliente para Linux e UNIX](#BKMK_LogFilesforLnU)  

    -   [Cliente para computadores Mac](#BKMK_LogfilesforMac)  

-   [Arquivos de log de servidor de site do Configuration Manager](#BKMK_ServerLogs)  

    -   [Logs de servidor de sistema de site e servidor de site](#BKMK_SiteSiteServerLog)  

    -   [Arquivos de log de instalação de servidor do site](#BKMK_SiteInstallLog)  

    -   [Arquivos de log do ponto de status de fallback](#BKMK_FSPLog)  

    -   [Arquivos de log do ponto de gerenciamento](#BKMK_MPLog)  

    -   [Arquivos de log do ponto de atualização de software](#BKMK_SUPLog)  

-   [Arquivos de log para a funcionalidade do Configuration Manager](#BKMK_FunctionLogs)  

    -   [Gerenciamento de aplicativos](#BKMK_AppManageLog)  

    -   [Inteligência de ativos](#BKMK_AILog)  

    -   [Cópia de segurança e recuperação](#BKMK_BnRLog)  

    -   [Registro de certificado](#BKMK_CertificateEnrollment)

    -   [Notificação do cliente](#BKMK_BGB)

    -   [Gateway de gerenciamento de nuvem](#cloud-management-gateway)

    -   [Configurações de conformidade e acesso a recursos da empresa](#BKMK_CompSettingsLog)  

    -   [Console do Configuration Manager](#BKMK_ConsoleLog)  

    -   [Gerenciamento de conteúdo](#BKMK_ContentLog)  

    -   [Deteção](#BKMK_DiscoveryLog)  

    -   [Endpoint Protection](#BKMK_EPLog)  

    -   [Extensões](#BKMK_Extensions)  

    -   [Inventário](#BKMK_InventoryLog)  

    -   [Medição](#BKMK_MeteringLog)  

    -   [Migração](#BKMK_MigrationLog)  

    -   [Dispositivos móveis](#BKMK_MDMLog)  

    -   [Implantação de sistema operacional](#BKMK_OSDLog)  

    -   [Gerenciamento de energia](#BKMK_PowerMgmtLog)  

    -   [Controle remoto](#BKMK_RCLog)  

    -   [Relatórios](#BKMK_ReportLog)  

    -   [Administração baseada em função](#BKMK_RBALog)  

    -   [Ponto de conexão de serviço](#BKMK_WITLog)  

    -   [Atualizações de software](#BKMK_SU_NAPLog)  

    -   [Wake On LAN](#BKMK_WOLLog)  

    -   [Serviço do Windows 10](#BKMK_WindowsServicingLog)

    -   [O Windows Update Agent](#BKMK_WULog)  

    -   [Servidor do WSUS](#BKMK_WSUSLog)  

##  <a name="BKMK_AboutLogs"></a>Sobre arquivos de log do Configuration Manager  
 A maioria dos processos no Configuration Manager grava as informações operacionais em um arquivo de log que é dedicado a esse processo. Os arquivos de log são identificados por **. log** ou **. lo _** extensões de arquivo. Configuration Manager grava um arquivo. log até que o log atinja seu tamanho máximo. Quando o log está cheio, o arquivo. log é copiado para um arquivo com o mesmo nome mas com a extensão. lo _ e o processo ou componente continua a gravar o arquivo. log. Quando o arquivo. log atinge novamente seu tamanho máximo, o arquivo. lo _ é substituído e o processo se repete. Alguns componentes criam um histórico de arquivos de log acrescentando um carimbo de data e hora para o nome do arquivo de log e mantendo a extensão. log. Uma exceção ao tamanho máximo e uso do arquivo. lo _ é o cliente para Linux e UNIX. Para obter informações sobre como o cliente para Linux e UNIX usa arquivos de log, consulte [gerenciar arquivos de log no cliente para Linux e UNIX](#BKMK_ManageLinuxLogs) neste tópico.  

 Para exibir os logs, use a ferramenta de Visualizador de log do Configuration Manager CMTrace, localizada no \\SMSSetup\\pasta de ferramentas da mídia de origem do Configuration Manager. A ferramenta CMTrace é adicionada a todas as imagens de inicialização que são adicionadas à biblioteca de Software.  

###  <a name="BKMK_LogOptions"></a>Configurar opções de log usando o Configuration Manager Service Manager  
 No Configuration Manager, você pode alterar onde os arquivos de log são armazenados, e você pode alterar o tamanho do arquivo de log.  

 Para modificar o tamanho dos arquivos de log, altere o nome e o local do arquivo de log, ou para forçar os vários componentes a gravar em um único arquivo de log, siga as etapas a seguir.  

#### <a name="to-modify-logging-for-a-component"></a>Para modificar o log para um componente  

1.  No console do Configuration Manager, selecione **monitoramento**, selecione **Status do sistema**e, em seguida, selecione **Status do Site** ou **Status do componente**.  
2.  No **início** guia o **componente** grupo, selecione **iniciar**e, em seguida, selecione **Configuration Manager Service Manager**.  
3.  Quando o Configuration Manager Service Manager abrir, conecte-se ao site que você deseja gerenciar. Se o site que você deseja gerenciar não for exibido, selecione **Site**, selecione **conectar**e, em seguida, insira o nome do servidor do site para o site correto.  
4.  Expanda o site e vá para **componentes** ou **servidores**, dependendo de onde estejam localizados os componentes que você deseja gerenciar.  
5.  No painel direito, selecione um ou mais componentes.  
6.  Sobre o **componente** menu, selecione **log**.  
7.  Na caixa de diálogo **Registo de Componente do Configuration Manager**, preencha as opções de configuração disponíveis para a sua seleção.  
8.  Selecione **Okey** para salvar a configuração.  

###  <a name="BKMK_LogLocation"></a>Localizar os logs do Configuration Manager  
Arquivos de log do Configuration Manager são armazenados em vários locais que dependem do processo que cria o arquivo de log e a configuração de seus sistemas de site. Como o local do log em um computador pode variar, use a função de pesquisa para localizar os arquivos de log relevantes nos computadores do Configuration Manager, se você precisar solucionar um cenário específico.  

##  <a name="BKMK_ClientLogs"></a>Logs de cliente do Configuration Manager  
As seções a seguir listam os arquivos de log relacionados a operações do cliente e instalação de cliente.  

###  <a name="BKMK_ClientOpLogs"></a>Operações do cliente  
A tabela a seguir lista os arquivos de log localizados no cliente do Configuration Manager.  

|Nome do registo|Descrição|  
|--------------|-----------------|  
|CAS.log|O serviço de acesso ao conteúdo. Mantém a cache do pacote local no cliente.|  
|Ccm32BitLauncher.log|Registra as ações para iniciar aplicativos no cliente marcado como "Executar como 32 bits".|  
|CcmEval.log|Registra atividades de avaliação do Configuration Manager cliente status e detalhes para os componentes que são exigidos pelo cliente do Configuration Manager.|  
|CcmEvalTask.log|Registra as atividades de avaliação de status de cliente do Configuration Manager que são iniciadas pela tarefa agendada de avaliação.|  
|CcmExec.log|Regista atividades do cliente e do serviço Anfitrião de Agente do SMS. Este ficheiro de registo também inclui informações sobre como ativar e desativar o proxy de reativação.|  
|CcmMessaging.log|Registra as atividades relacionadas a comunicação entre o cliente e o gerenciamento de pontos.|  
|CCMNotificationAgent.log|Regista atividades relacionadas com as operações de notificação de cliente.|  
|Ccmperf.log|Regista atividades relacionadas com a manutenção e a captura de dados relacionados com os contadores de desempenho do cliente.|  
|CcmRestart.log|Regista a atividade de reinício do serviço de cliente.|  
|CCMSDKProvider.log|Regista atividades das interfaces SDK do cliente.|  
|CertificateMaintenance.log|Mantém certificados para os Serviços de Domínio do Active Directory e os pontos de gestão.|  
|CIDownloader.log|Regista detalhes sobre transferências de definições de itens de configuração.|  
|CITaskMgr.log|Registra as tarefas que são iniciadas para cada aplicativo e o tipo de implantação, como conteúdo baixarem e instalar ou desinstalar ações.|  
|ClientAuth.log|Registros de assinatura e a atividade de autenticação para o cliente.|  
|ClientIDManagerStartup.log|Cria e mantém o GUID do cliente e identifica as tarefas executadas durante o registo e atribuição do cliente.|  
|ClientLocation.log|Regista tarefas relacionadas com a atribuição do site do cliente.|  
|CMHttpsReadiness.log|Registra os resultados de executar a ferramenta de avaliação de prontidão do Configuration Manager HTTPS. Essa ferramenta verifica se os computadores têm um certificado de autenticação de cliente da infraestrutura de chave pública (PKI) que pode ser usado com o Configuration Manager.|  
|CmRcService.log|Regista informações para o serviço de controlo remoto.|  
|ContentTransferManager.log|Agenda o serviço de transferência inteligente em segundo plano (BITS) ou o bloco de SMB (Server Message) para baixar ou acessar os pacotes.|  
|DataTransferService.log|Regista todas as comunicações BITS para acesso a políticas ou pacotes.|  
|EndpointProtectionAgent|Registra as informações sobre a instalação do cliente do System Center Endpoint Protection e a aplicação de política de antimalware para esse cliente.|  
|execmgr.log|Regista detalhes dos pacotes e sequências de tarefas que são executados no cliente.|  
|ExpressionSolver.log|Registra os detalhes sobre os métodos de detecção aprimorados que são usados quando detalhado ou o log de depuração está ativado.|  
|ExternalEventAgent.log|Regista o histórico de deteção de malware do Endpoint Protection e eventos relacionados com o estado do cliente.|  
|FileBITS.log|Regista todas as tarefas de acesso do pacote SMB.|  
|FileSystemFile.log|Regista a atividade do fornecedor do Windows Management Instrumentation (WMI) para recolha de ficheiros e inventário de software.|  
|FSPStateMessage.log|Regista a atividade de mensagens de estado que são enviadas pelo cliente para o ponto de estado de contingência.|  
|InternetProxy.log|Registra a atividade configuração e o uso do proxy de rede para o cliente.|  
|InventoryAgent.log|Regista atividades de inventário de hardware, inventário de software e ações de deteção de heartbeat no cliente.|  
|LocationCache.log|Registra a atividade de uso do cache local e manutenção para o cliente.|  
|LocationServices.log|Regista a atividade do cliente para localizar pontos de gestão, pontos de atualização de software e pontos de distribuição.|  
|MaintenanceCoordinator.log|Registra a atividade das tarefas de manutenção geral do cliente.|  
|Mifprovider.log|Registra a atividade do provedor WMI para arquivos de formato MIF (Management Information).|  
|mtrmgr.log|Monitoriza todos os processos de medição de software.|  
|PolicyAgent.log|Registra as solicitações de políticas feitas usando o serviço de transferência de dados.|  
|PolicyAgentProvider.log|Regista alterações de política.|  
|PolicyEvaluator.log|Regista detalhes sobre a avaliação das políticas em computadores cliente, incluindo políticas de atualizações de software.|  
|PolicyPlatformClient.log|Registra o processo de correção e conformidade para todos os provedores localizados em \Program Files\Microsoft Policy Platform, exceto o provedor de arquivo.|  
|PolicySdk.log|Regista atividades das interfaces SDK do sistema de políticas.|  
|Pwrmgmt.log|Regista informações sobre a ativação ou desativação e a configuração de definições de cliente do proxy de reativação.|  
|PwrProvider.log|Registra as atividades do provedor de gerenciamento de energia (PWRInvProvider) hospedado no serviço do WMI. Em todas as versões suportadas do Windows, o fornecedor enumera as definições atuais nos computadores durante o inventário de hardware e aplica as definições do plano de energia.|  
|SCClient_&lt;*domain*\>@&lt;*username*\>_1.log|Regista a atividade no Centro de Software para o utilizador especificado no computador cliente.|  
|SCClient_&lt;*domain*\>@&lt;*username*\>_2.log|Regista a atividade do histórico no Centro de Software para o utilizador especificado no computador cliente.|  
|Scheduler.log|Regista atividades de tarefas agendadas para todas as operações de cliente.|  
|SCNotify_&lt;*domain*\>@&lt;*username*\>_1.log|Regista a atividade para notificar os utilizadores sobre software para o utilizador especificado.|  
|SCNotify_&lt;*domain*\>@&lt;*username*\>_1-&lt;*date_time*>.log|Regista a informação do histórico para notificar os utilizadores sobre software para o utilizador especificado.|  
|setuppolicyevaluator.log|Regista a configuração e a criação da política de inventário no WMI.|  
|SleepAgent_&lt;*domínio*\>@SYSTEM_0.log|O arquivo de log principal para o proxy de ativação.|  
|smscliui.log|Registra o uso do cliente do Configuration Manager no painel de controle.|  
|SrcUpdateMgr.log|Regista a atividade das aplicações do Windows Installer instaladas que são atualizadas com as localizações de origem do ponto de distribuição atual.|  
|StatusAgent.log|Regista mensagens de estado que são criadas pelos componentes de cliente.|  
|SWMTRReportGen.log|Gera um relatório de dados de uso é coletado pelo agente de medição. Estes dados são registados no ficheiro Mtrmgr.log.|  
|UserAffinity.log|Regista detalhes sobre a afinidade de dispositivo do utilizador.|  
|VirtualApp.log|Registra as informações específicas para a avaliação dos tipos de implantação do Application Virtualization (App-V).|  
|Wedmtrace.log|Regista operações relacionadas com filtros de escrita nos clientes do Windows Embedded.|  
|wakeprxy-install.log|Registra informações de instalação quando os clientes recebem a opção de configuração do cliente para ativar o proxy de ativação.|  
|wakeprxy-uninstall.log|Registra as informações sobre a desinstalação do proxy de ativação quando os clientes recebem a configuração de opção para desativar o proxy de ativação, se o proxy de ativação foi ativado anteriormente do cliente.|  

###  <a name="BKMK_ClientInstallLog"></a>Arquivos de log de instalação do cliente  
 A tabela a seguir lista os arquivos de log que contêm informações relacionadas à instalação do cliente do Configuration Manager.  

|Nome do registo|Descrição|  
|--------------|-----------------|  
|ccmsetup.log|Ccmsetup.exe registra as tarefas de configuração do cliente, atualização e remoção do cliente. Pode ser utilizado para resolver problemas de instalação de cliente.|  
|ccmsetup-ccmeval.log|Registra as tarefas de ccmsetup.exe status e correção do cliente.|  
|CcmRepair.log|Regista as atividades de reparação do agente de cliente.|  
|Client.msi.log|Os registos configuram tarefas executadas por client.msi. Pode ser utilizado para resolver problemas de instalação ou remoção de clientes.|  

###  <a name="BKMK_LogFilesforLnU"></a>Cliente para Linux e UNIX  
 O cliente do Configuration Manager para Linux e UNIX registra as informações nos seguintes arquivos de log.  

> [!TIP]  
>  Começando com os clientes do Linux e UNIX da atualização cumulativa 1, você pode usar o CMTrace para exibir os arquivos de log para o cliente para Linux e UNIX.  

> [!NOTE]  
>  Quando utilizar a edição inicial do cliente para Linux e UNIX e consultar a documentação desta secção, substitua as seguintes referências para cada ficheiro ou processo:  
>   
>  -   Substitua **omiserver.bin** por **nwserver.bin**  
> -   Substitua **omi** por **nanowbem**  

|Nome do registo|Detalhes|  
|--------------|-------------|  
|Scxcm.log|O arquivo de log do serviço principal do cliente do Configuration Manager para Linux e UNIX (ccmexec.bin). Este ficheiro de registo contém informações sobre a instalação e as operações do ccmexec.bin. em curso<br /><br /> Por padrão, esse arquivo de log está localizado em **/var/opt/microsoft/scxcm.log**<br /><br /> Para alterar a localização do ficheiro de registo, edite **/opt/microsoft/configmgr/etc/scxcm.conf** e altere o campo **PATH**. Não é necessário reiniciar o serviço ou o computador cliente para que a alteração produza efeito.<br /><br /> Você pode definir o nível de log para uma das quatro diferentes configurações.|  
|Scxcmprovider.log|O arquivo de log do serviço CIM de cliente do Configuration Manager para Linux e UNIX (omiserver.bin). Este ficheiro de registo contém informações sobre as operações do nwserver.bin em curso.<br /><br /> Esse log está localizado em**/var/opt/microsoft/configmgr/scxcmprovider.log**<br /><br /> Para alterar a localização do ficheiro de registo, edite **/opt/microsoft/omi/etc/scxcmprovider.conf** e altere o campo **PATH**. Não é necessário reiniciar o serviço ou o computador cliente para que a alteração produza efeito.<br /><br /> Você pode definir o nível de log para uma das três configurações.|  

 Ambos os ficheiros de registo suportam vários níveis de registo:  

-   **scxcm.log**. Para alterar o nível de log, edite **/opt/microsoft/configmgr/etc/scxcm.conf** e altere cada instância do **módulo** marca para o nível de log desejado:  

    -   ERRO: Indica problemas que exigem atenção  

    -   AVISO: Indica possíveis problemas de operações do cliente  

    -   INFO: Log mais detalhado que indica o status de vários eventos no cliente  

    -   RASTREAMENTO: Log detalhado que normalmente é usado para diagnosticar problemas  

-   **scxcmprovider.log**. Para alterar o nível de log, edite **/opt/microsoft/omi/etc/scxcmprovider.conf** e altere cada instância do **módulo** marca para o nível de log desejado:  

    -   ERRO: Indica problemas que exigem atenção  

    -   AVISO: Indica possíveis problemas de operações do cliente

    -   INFO: Log mais detalhado que indica o status de vários eventos no cliente  

Em condições normais de operação, use o nível de log de erro. Esse nível de log cria o menor arquivo de log. Como o nível de log vai aumentando de erro, aviso, informações e, em seguida, para rastreamento, um arquivo de log maior será criado conforme mais dados são gravados no arquivo.  

####  <a name="BKMK_ManageLinuxLogs"></a>Gerenciar arquivos de log para o cliente Linux e UNIX  
O cliente para Linux e UNIX não limita o tamanho máximo dos arquivos de log do cliente nem copia automaticamente o conteúdo de seus arquivos. log para outro arquivo, como em um arquivo. lo _. Se você quiser controlar o tamanho máximo de arquivos de log, implemente um processo para gerenciar os arquivos de log independente do cliente do Configuration Manager para Linux e UNIX.  

Por exemplo, você pode usar o comando do Linux e UNIX **logrotate** para gerenciar o tamanho e a rotação dos arquivos de log do cliente. O cliente do Configuration Manager para Linux e UNIX tem uma interface que permite **logrotate** para avisar o cliente quando a rotação de log estiver concluída, então o cliente pode retomar o log para o arquivo de log.  

Para obter informações sobre o comando **logrotate**, veja a documentação das distribuições de Linux e UNIX que utiliza.  

###  <a name="BKMK_LogfilesforMac"></a>Cliente para computadores Mac  
O cliente do Configuration Manager para computadores Mac registra as informações nos seguintes arquivos de log.  

|Nome do registo|Detalhes|  
|--------------|-------------|  
|CCMClient -&lt;*data_hora*>. log|Registra as atividades relacionadas a operações de cliente Mac, incluindo o gerenciamento de aplicativos, inventário e log de erros.<br /><br /> Esse arquivo de log está localizado na pasta /Library/Application Support/Microsoft/CCM/Logs no computador Mac.|  
|CCMAgent -&lt;*data_hora*>. log|Registra as informações relacionadas a operações do cliente, incluindo a atividade do computador Mac e operações de logoff e logon do usuário.<br /><br /> Esse arquivo de log está na pasta ~/Library/Logs no computador Mac.|  
|CCMNotifications -&lt;*data_hora*>. log|Registra as atividades relacionadas a notificações do Gerenciador de configuração exibidas no computador Mac.<br /><br /> Esse arquivo de log está localizado na pasta ~/Library/Logs no computador Mac.|  
|CCMPrefPane -&lt;*data_hora*>. log|Registra as atividades relacionadas à caixa de diálogo de preferências do Configuration Manager no computador Mac, que inclui status geral e log de erros.<br /><br /> Esse arquivo de log está localizado na pasta ~/Library/Logs no computador Mac.|  

O arquivo de log SMS_DM.log no servidor do sistema de site também registra a comunicação entre computadores Mac e o ponto de gerenciamento que está configurado para dispositivos móveis e computadores Mac.  

##  <a name="BKMK_ServerLogs"></a>Arquivos de log de servidor de site do Configuration Manager  
 As seções a seguir listam os arquivos de log que estão no servidor do site ou que estão relacionados às funções de sistema de site específico.  

###  <a name="BKMK_SiteSiteServerLog"></a>Logs de servidor de sistema de site e servidor de site  
 A tabela a seguir lista os arquivos de log que estão no servidor de site do Configuration Manager e servidores do sistema de site.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|adctrl.log|Regista a atividade de processamento de registo.|Servidor do site|  
|ADForestDisc.log|Regista ações da Deteção de Florestas do Active Directory.|Servidor do site|  
|ADService.log|Regista detalhes sobre grupos de segurança e a criação de contas no Active Directory.|Servidor do site|  
|adsgdis.log|Regista ações da Deteção de Grupos do Active Directory.|Servidor do site|  
|adsysdis.log|Regista ações da Deteção de Sistemas do Active Directory.|Servidor do site|  
|adusrdis.log|Regista ações da Deteção de Utilizadores do Active Directory.|Servidor do site|  
|ccm.log|Regista atividades de instalação push de cliente.|Servidor do site|  
|CertMgr.log|Registros de atividades para a comunicação do certificado.|Servidor do sistema de sites|  
|chmgr.log|Regista atividades do gestor de estado de funcionamento de cliente.|Servidor do site|  
|Cidm.log|Regista alterações das definições de cliente efetuadas pelo CIDM (Client Install Data Manager).|Servidor do site|  
|colleval.log|Regista detalhes sobre o momento de criação, alteração e eliminação das coleções pelo Avaliador de Coleção.|Servidor do site|  
|compmon.log|Regista o estado de threads de componentes monitorizados para o servidor do site.|Servidor do sistema de sites|  
|compsumm.log|Regista tarefas do Summarizer de Estado do Componente.|Servidor do site|  
|ComRegSetup.log|Regista a instalação inicial de resultados de registo COM para um servidor do site.|Servidor do sistema de sites|  
|dataldr.log|Registra as informações sobre o processamento de arquivos MIF e inventário de hardware no banco de dados do Configuration Manager.|Servidor do site|  
|ddm.log|Regista atividades do gestor de dados de deteção.|Servidor do site|  
|despool.log|Regista transferências de comunicação site a site recebidas.|Servidor do site|  
|distmgr.log|Regista detalhes sobre a criação de pacotes, compressão, replicação de diferenças e atualizações de informações.|Servidor do site|  
|EPCtrlMgr.log|Registra informações sobre a sincronização de informações de ameaça de malware do servidor de função de sistema do Endpoint Protection site com o banco de dados do Configuration Manager.|Servidor do site|  
|EPMgr.log|Regista o estado da função de sistema de sites do Endpoint Protection.|Servidor do sistema de sites|  
|EPSetup.log|Fornece informações sobre a instalação da função de sistema de sites do Endpoint Protection.|Servidor do sistema de sites|  
|EnrollSrv.log|Regista atividades do processo do serviço de registo.|Servidor do sistema de sites|  
|EnrollWeb.log|Regista atividades do processo do Web site de registo.|Servidor do sistema de sites|  
|fspmgr.log|Regista atividades da função de sistema de sites do ponto de estado de contingência.|Servidor do sistema de sites|  
|hman.log|Registra as informações sobre as alterações de configuração do site e a publicação de informações do site nos serviços de domínio do Active Directory.|Servidor do site|  
|Inboxast.log|Regista os ficheiros que são movidos do ponto de gestão para a pasta A RECEBER correspondente no servidor do site.|Servidor do site|  
|inboxmgr.log|Regista atividades de transferência de ficheiros entre pastas A Receber.|Servidor do site|  
|inboxmon.log|Regista o processamento de ficheiros a receber e atualizações de contadores de desempenho.|Servidor do site|  
|invproc.log|Regista o reencaminhamento de ficheiros MIF de um site secundário para o seu site principal.|Servidor do site|  
|migmctrl.log|Registra as informações para ações de migração que envolvem trabalhos de migração, pontos de distribuição compartilhados e atualizações do ponto de distribuição.|Site de nível superior na hierarquia do Configuration Manager e cada site primário filho.<br /><br /> Em uma hierarquia de vários sites primários, use o arquivo de log é criado no site de administração central.|  
|mpcontrol.log|Grava o registro do ponto de gerenciamento com o nome do serviço WINS (Windows Internet). Regista a disponibilidade do ponto de gestão a cada 10 minutos.|Servidor do sistema de sites|  
|mpfdm.log|Regista as ações do componente do ponto de gestão que move ficheiros de cliente para a pasta A RECEBER correspondente no servidor do site.|Servidor do sistema de sites|  
|mpMSI.log|Registra os detalhes sobre o gerenciamento de instalação do ponto.|Servidor do site|  
|MPSetup.log|Regista o processo do wrapper de instalação do ponto de gestão.|Servidor do site|  
|netdisc.log|Regista ações da Deteção de Rede.|Servidor do site|  
|ntsvrdis.log|Regista a atividade de deteção de servidores de sistema de sites.|Servidor do site|  
|Objreplmgr|Regista o processamento de notificações de alteração de objetos para replicação.|Servidor do site|  
|offermgr.log|Regista atualizações de anúncios.|Servidor do site|  
|offersum.log|Regista o resumo das mensagens de estado de implementação.|Servidor do site|  
|OfflineServicingMgr.log|Regista as atividades de aplicação de atualizações a ficheiros de imagem de sistema operativo.|Servidor do site|  
|outboxmon.log|Regista o processamento de ficheiros a enviar e atualizações de contadores de desempenho.|Servidor do site|  
|PerfSetup.log|Regista os resultados da instalação de contadores de desempenho.|Servidor do sistema de sites|  
|PkgXferMgr.log|Registra as ações do componente SMS_Executive que é responsável por enviar conteúdo de um site primário para um ponto de distribuição remoto.|Servidor do site|  
|policypv.log|Regista as atualizações das políticas de cliente para refletir as alterações das implementações ou definições de cliente.|Servidor do site principal|  
|rcmctrl.log|Regista as atividades de replicação de base de dados entre sites na hierarquia.|Servidor do site|  
|replmgr.log|Regista a replicação de ficheiros entre os componentes do servidor do site e o componente do Programador.|Servidor do site|  
|ResourceExplorer.log|Registra erros, avisos e informações sobre como executar o Gerenciador de recursos.|Computador que executa o console do Configuration Manager|  
|ruleengine.log|Regista detalhes sobre regras de implementação automática para a identificação, transferência de conteúdo e criação de implementação e de grupos de atualização de software.|Servidor do site|  
|Schedule.log|Regista detalhes sobre replicação de ficheiros e tarefas site a site.|Servidor do site|  
|Sender.log|Regista os ficheiros que são transferidos entre sites através de replicação baseada em ficheiros.|Servidor do site|  
|sinvproc.log|Regista informações sobre o processamento de dados de inventário de software para a base de dados do site.|Servidor do site|  
|sitecomp.log|Regista detalhes sobre a manutenção dos componentes instalados do site em todos os servidores de sistema de sites do site.|Servidor do site|  
|sitectrl.log|Regista as alterações de definições do site efetuadas nos objetos de controlo do site na base de dados.|Servidor do site|  
|sitestat.log|Regista a disponibilidade e o processo de monitorização do espaço em disco de todos os sistemas.|Servidor do site|  
|SmsAdminUI.log|Registra a atividade de console do Configuration Manager.|Computador que executa o console do Configuration Manager|  
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

###  <a name="BKMK_SiteInstallLog"></a>Arquivos de log de instalação de servidor do site  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com a instalação do site.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|ConfigMgrPrereq.log|Registros componente de pré-requisito avaliação e atividades de instalação.|Servidor do site|  
|ConfigMgrSetup.log|Saída detalhada de registros da instalação do servidor do site.|Servidor do Site|  
|ConfigMgrSetupWizard.log|Registra as informações relacionadas à atividade no Assistente de instalação.|Servidor do Site|  
|SMS_BOOTSTRAP.log|Regista informações sobre o progresso do início do processo de instalação do site secundário. Os detalhes do processo de configuração estão contidos no ficheiro ConfigMgrSetup.log.|Servidor do Site|  
|smstsvc.log|Registra informações sobre a instalação, o uso e a remoção de um serviço do Windows que é usado para testar a conectividade de rede e permissões entre servidores, usando a conta de computador do servidor que inicia a conexão.|Servidor do site e o servidor do sistema de site|  

###  <a name="BKMK_FSPLog"></a>Arquivos de log do ponto de status de fallback  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com o ponto de estado de contingência.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|FspIsapi|Regista detalhes sobre comunicações com o ponto de estado de contingência a partir de clientes legados de dispositivos móveis e de computadores cliente.|Servidor do sistema de sites|  
|fspMSI.log|Regista mensagens geradas pela instalação de um ponto de estado de contingência.|Servidor do sistema de sites|  
|fspmgr.log|Regista atividades da função de sistema de sites do ponto de estado de contingência.|Servidor do sistema de sites|  

###  <a name="BKMK_MPLog"></a>Arquivos de log do ponto de gerenciamento  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com o ponto de gestão.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|CcmIsapi.log|Regista atividades de mensagens de cliente no ponto final.|Servidor do sistema de sites|  
|MP_CliReg.log|Regista a atividade de registo de cliente processada pelo ponto de gestão.|Servidor do sistema de sites|  
|MP_Ddr.log|Registra a conversão de XML.ddr registros de clientes e, em seguida, copia para o servidor do site.|Servidor do sistema de sites|  
|MP_Framework.log|Regista as atividades do ponto de gestão central e dos componentes da estrutura de cliente.|Servidor do sistema de sites|  
|MP_GetAuth.log|Regista a atividade de autorização de cliente.|Servidor do sistema de sites|  
|MP_GetPolicy.log|Regista a atividade de pedidos de política de computadores cliente.|Servidor do sistema de sites|  
|MP_Hinv.log|Regista detalhes sobre a conversão de registos de inventário de hardware XML a partir de clientes e a cópia desses ficheiros para o servidor do site.|Servidor do sistema de sites|  
|MP_Location.log|Regista a atividade de pedido e resposta de localização a partir de clientes.|Servidor do sistema de sites|  
|MP_OOBMgr.log|Registra as atividades do ponto de gerenciamento relacionadas ao recebimento de uma OTP de um cliente.|Servidor do sistema de sites|  
|MP_Policy.log|Regista a comunicação de políticas.|Servidor do sistema de sites|  
|MP_Relay.log|Regista a transferência de ficheiros que são recolhidos do cliente.|Servidor do sistema de sites|  
|MP_Retry.log|Processos de repetição de inventário de hardware de registros.|Servidor do sistema de sites|  
|MP_Sinv.log|Regista detalhes sobre a conversão de registos de inventário de software XML a partir de clientes e a cópia desses ficheiros para o servidor do site.|Servidor do sistema de sites|  
|MP_SinvCollFile.log|Regista detalhes sobre a recolha de ficheiros.|Servidor do sistema de sites|  
|MP_Status.log|Regista detalhes sobre a conversão de ficheiros de mensagens de estado XML.svf a partir de clientes e a cópia desses ficheiros para o servidor do site.|Servidor do sistema de sites|  
|mpcontrol.log|Regista o registo do ponto de gestão com o WINS. Regista a disponibilidade do ponto de gestão a cada 10 minutos.|Servidor do site|  
|mpfdm.log|Regista as ações do componente do ponto de gestão que move ficheiros de cliente para a pasta A RECEBER correspondente no servidor do site.|Servidor do sistema de sites|  
|mpMSI.log|Registra os detalhes sobre o gerenciamento de instalação do ponto.|Servidor do site|  
|MPSetup.log|Regista o processo do wrapper de instalação do ponto de gestão.|Servidor do site|  

###  <a name="BKMK_SUPLog"></a>Arquivos de log do ponto de atualização de software  
 A tabela a seguir lista os arquivos de log que contêm informações relacionadas ao ponto de atualização de software.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|objreplmgr.log|Registra os detalhes sobre a replicação de software atualiza os arquivos de notificação de um site pai para sites filho.|Servidor do site|  
|PatchDownloader.log|Regista detalhes sobre o processo de transferência de atualizações de software da origem da atualização para o destino da transferência no servidor do site.|Computador que hospeda o console do Configuration Manager a partir do qual os downloads são iniciados|  
|ruleengine.log|Regista detalhes sobre regras de implementação automática para a identificação, transferência de conteúdo e criação de implementação e de grupos de atualização de software.|Servidor do site|  
|SUPSetup.log|Regista detalhes sobre a instalação do ponto de atualização de software. Quando a instalação de ponto de atualização de software estiver concluída, é escrito **Instalação bem-sucedida** neste ficheiro de registo.|Servidor do sistema de sites|  
|WCM.log|Registra os detalhes sobre a atualização de software do ponto de configuração e as conexões ao servidor do WSUS para categorias de atualização assinadas, classificações e idiomas.|Servidor do site que se conecta ao servidor do WSUS|  
|WSUSCtrl.log|Regista detalhes sobre a configuração, a conectividade de base de dados e o estado de funcionamento do servidor WSUS do site.|Servidor do sistema de sites|  
|wsyncmgr.log|Registra os detalhes sobre o processo de sincronização de atualizações de software.|Servidor do sistema de sites|  
|WUSSyncXML.log|Registra os detalhes sobre a Inventory Tool for Microsoft Updates o processo de sincronização.|Computador cliente configurado como o host de sincronização para a ferramenta de inventário para o Microsoft Updates|  

##  <a name="BKMK_FunctionLogs"></a>Arquivos de log para a funcionalidade do Configuration Manager  
 A lista de seções a seguir arquivos relacionados às funções do Gerenciador de configuração de log.  

###  <a name="BKMK_AppManageLog"></a>Gerenciamento de aplicativos  
 A tabela a seguir lista os arquivos de log que contêm informações relacionadas ao gerenciamento de aplicativos.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|AppIntentEval.log|Regista os detalhes sobre o estado atual e previsto das aplicações, a sua aplicabilidade, se os requisitos foram satisfeitos, os tipos de implementação e as dependências.|Cliente|  
|AppDiscovery.log|Regista os detalhes sobre a descoberta ou deteção de aplicações em computadores cliente.|Cliente|  
|AppEnforce.log|Regista os detalhes sobre medidas de imposição (instalar e desinstalar) tomadas para aplicações do cliente.|Cliente|  
|awebsctl.log|Função de sistema de site do ponto de registros de monitoramento de atividades para o serviço web de catálogo de aplicativos.|Servidor do sistema de sites|  
|awebsvcMSI.log|Regista informações detalhadas de instalação da função do sistema de sites do ponto de serviço Web do Catálogo de Aplicações.|Servidor do sistema de sites|  
|Ccmsdkprovider.log|Regista as atividades do SDK de gestão de aplicações.|Cliente|  
|colleval.log|Regista detalhes sobre o momento de criação, alteração e eliminação das coleções pelo Avaliador de Coleção.|Servidor do sistema de sites|  
|ConfigMgrSoftwareCatalog.log|Regista a atividade do Catálogo de Aplicações, que inclui a sua utilização do Silverlight.|Cliente|  
|portlctl.log|Regista as atividades de monitorização da função do sistema de sites do ponto do Web site do Catálogo de Aplicações.|Servidor do sistema de sites|  
|portlwebMSI.log|Regista a atividade de instalação do MSI para a função de Web site do Catálogo de Aplicações.|Servidor do sistema de sites|  
|PrestageContent.log|Registra os detalhes sobre o uso da ferramenta ExtractContent.exe em um ponto de distribuição remoto e pré-configurado. Esta ferramenta extrai o conteúdo exportado para um ficheiro.|Servidor do sistema de sites|  
|ServicePortalWebService.log|Regista a atividade do serviço Web do Catálogo de Aplicações.|Servidor do sistema de sites|  
|ServicePortalWebSite.log|Regista a atividade do Web site do Catálogo de Aplicações.|Servidor do sistema de sites|  
|SMSdpmon.log|Regista os detalhes sobre a tarefa agendada de monitorização do estado de funcionamento do ponto de distribuição configurada num ponto de distribuição.|Servidor do site|  
|SoftwareCatalogUpdateEndpoint.log|Registra as atividades de gerenciamento de URL para o catálogo de aplicativos mostrado no Centro de Software.|Cliente|  
|SoftwareCenterSystemTasks.log|Registra as atividades relacionadas à validação de componente de pré-requisito do Centro de Software.|Cliente|  

 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com a implementação de pacotes e programas.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|colleval.log|Regista detalhes sobre o momento de criação, alteração e eliminação das coleções pelo Avaliador de Coleção.|Servidor do site|  
|execmgr.log|Regista os detalhes sobre pacotes e sequências de tarefas que são executados.|Cliente|  

###  <a name="BKMK_AILog"></a>Inteligência de ativos  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com o Asset Intelligence.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|AssetAdvisor.log|Regista as atividades das ações de inventário do Asset Intelligence.|Cliente|  
|aikbmgr.log|Regista os detalhes sobre o processamento de ficheiros XML a partir da caixa de entrada para atualização do catálogo do Asset Intelligence.|Servidor do site|  
|AIUpdateSvc.log|Registra a interação da sincronização do Asset Intelligence ponto com o System Center Online (SCO), o serviço da web online.|Servidor do sistema de sites|  
|AIUSMSI.log|Registra os detalhes sobre a instalação da sincronização do Asset Intelligence ponto de função do sistema de site.|Servidor do sistema de sites|  
|AIUSSetup.log|Registra os detalhes sobre a instalação da sincronização do Asset Intelligence ponto de função do sistema de site.|Servidor do sistema de sites|  
|ManagedProvider.log|Regista os detalhes sobre a deteção de software com uma etiqueta de identificação de software associada. Também registra as atividades relacionadas ao inventário de hardware.|Servidor do sistema de sites|  
|MVLSImport.log|Regista os detalhes sobre o processamento de ficheiros de licenciamento importados.|Servidor do sistema de sites|  

###  <a name="BKMK_BnRLog"></a>Backup e recuperação  
 A tabela a seguir lista os arquivos de log que contêm informações relacionadas às ações de backup e recuperação, inclusive redefinições de site e alterações no provedor de SMS.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|ConfigMgrSetup.log|Registra informações sobre tarefas de configuração e recuperação quando o Configuration Manager recupera um site de backup.|Servidor do site|  
|Smsbkup.log|Regista os detalhes sobre a atividade de cópia de segurança do site.|Servidor do site|  
|smssqlbkup.log|Registra a saída do processo de backup de banco de dados do site quando o SQL Server está instalado em um servidor que não seja o servidor do site.|Servidor da base de dados do site|  
|Smswriter.log|Registra informações sobre o estado do gravador VSS do Configuration Manager que é usado pelo processo de backup.|Servidor do site|  

###  <a name="BKMK_CertificateEnrollment"></a>Registro de certificado  
 A tabela a seguir lista os arquivos de log do Configuration Manager que contêm informações relacionadas ao registro de certificado. Registro de certificado usa o ponto de registro de certificado e o módulo de política do Configuration Manager no servidor que está executando o serviço de registro de dispositivo de rede.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|Crp.log|Registra as atividades de registro.|Ponto de registo de certificados|  
|Crpctrl.log|Regista o estado de funcionamento operacional do ponto de registo de certificados.|Ponto de registo de certificados|  
|Crpsetup.log|Regista os detalhes sobre a instalação e a configuração do ponto de registo de certificados.|Ponto de registo de certificados|  
|Crpmsi.log|Regista os detalhes sobre a instalação e a configuração do ponto de registo de certificados.|Ponto de registo de certificados|  
|NDESPlugin.log|Registros de desafiam de verificação e as atividades de registro de certificado.|Módulo de política do Configuration Manager e o serviço de registro de dispositivo de rede|  

 Além dos arquivos de log do Configuration Manager, examine os logs de aplicativo do Windows no Visualizador de eventos no servidor que executa o serviço de registro de dispositivo de rede e o servidor que hospeda o ponto de registro de certificado. Por exemplo, procure mensagens da origem **NetworkDeviceEnrollmentService**. Também pode utilizar os seguintes ficheiros de registo:  

-   Arquivos de log do IIS para o serviço de registro do dispositivo de rede:  **&lt;caminho\>\inetpub\logs\LogFiles\W3SVC1**  

-   IIS arquivos de log para o ponto de registro de certificado:  **&lt;caminho\>\inetpub\logs\LogFiles\W3SVC1**  

-   Ficheiro de registo da Política de Inscrição de Dispositivos de Rede: **mscep.log**  

    > [!NOTE]  
    >  Este ficheiro está localizado na pasta do perfil da conta do Serviço de Inscrição de Dispositivos de Rede, por exemplo, em C:\Users\SCEPSvc. Para obter mais informações sobre como ativar o registo do Serviço de Inscrição de Dispositivos de Rede, veja a secção [Ativar Registo](http://go.microsoft.com/fwlink/?LinkId=320576) no Serviço de Inscrição de Dispositivos de Rede (NDES) do artigo dos Serviços de Certificados do Active Directory (AD CS) da Wiki da TechNet.  

###  <a name="BKMK_BGB"></a>Notificação do cliente  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com a notificação do cliente.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|bgbmgr.log|Registra os detalhes sobre as atividades de servidor de site relacionadas a tarefas de notificação do cliente e de processamento on-line e arquivos de status da tarefa.|Servidor do site|  
|BGBServer.log|Registra as atividades do servidor de notificação, como a comunicação cliente-servidor e enviar tarefas aos clientes. Também registra informações sobre a geração do on-line e os arquivos de status de tarefa a ser enviado ao servidor do site.|Ponto de gestão|  
|BgbSetup.log|Registra as atividades do processo de wrapper de instalação de servidor de notificação durante a instalação e desinstalação.|Ponto de gestão|  
|bgbisapiMSI.log|Registra os detalhes sobre a instalação do servidor de notificação e a desinstalação.|Ponto de gestão|  
|BgbHttpProxy.log|Regista as atividades do proxy de HTTP de notificação enquanto reencaminha as mensagens de clientes utilizando o HTTP de e para o servidor de notificação.|Cliente|  
|CcmNotificationAgent.log|Registra as atividades do agente de notificação, como a comunicação cliente-servidor e informações sobre tarefas recebidas e enviadas para outros agentes cliente.|Cliente|  

### <a name="cloud-management-gateway"></a>Gateway de gerenciamento de nuvem

A tabela a seguir lista os arquivos de log que contêm informações relacionadas para o gateway de gerenciamento de nuvem.

||||
|-|-|-|
|Nome do registo|Descrição|Computador com o ficheiro de registo|
|CloudMgr.log|Registra os detalhes sobre como implantar o serviço de gateway de gerenciamento de nuvem, o status do serviço em andamento e o uso de dados associado ao serviço.<br>Você pode configurar o nível de log ser a edição do registro **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_CLOUD_SERVICES_MANAGER\Logging nível**|O *installdir* pasta no servidor do site primário ou autoridades de certificação.|
|CMGSetup.log ou CMG -*RoleInstanceID*-CMGSetup.log<sup>1</sup>|Registra os detalhes sobre a fase 2 da implantação de gateway de gerenciamento de nuvem (implantação local no Azure)<br>Você pode configurar o nível de log usando a configuração **o nível de rastreamento** (**informações** (padrão), **detalhado**, **erro**) sobre o **configuração de serviços do Azure portal\Cloud** guia.|O **%approot%\logs** no seu servidor do Azure, ou a pasta de Logs do SMS no servidor do sistema de site|
|CMGHttpHandler.log ou CMG -*RoleInstanceID*-CMGHttpHandler.log<sup>1</sup>|Registra os detalhes sobre a associação de manipulador http do nuvem management gateway com serviços de informações da Internet no Azure<br>Você pode configurar o nível de log usando a configuração **o nível de rastreamento** (**informações** (padrão), **detalhado**, **erro**) sobre o **configuração de serviços do Azure portal\Cloud** guia.|O **%approot%\logs** no seu servidor do Azure, ou a pasta de Logs do SMS no servidor do sistema de site|
|CMGService.log ou CMG -*RoleInstanceID*-CMGService.log<sup>1</sup>|Registra os detalhes sobre o componente nuvem gerenciamento gateway service principal no Azure<br>Você pode configurar o nível de log usando a configuração **o nível de rastreamento** (**informações** (padrão), **detalhado**, **erro**) sobre o **configuração de serviços do Azure portal\Cloud** guia.|O **%approot%\logs** no seu servidor do Azure, ou a pasta de Logs do SMS no servidor do sistema de site|
|SMS_Cloud_ProxyConnector.log|Registra detalhes sobre como configurar conexões entre o serviço de gateway de gerenciamento da nuvem e a conexão de gateway de gerenciamento de nuvem ponto.|Servidor do sistema de sites|

<sup>1</sup> esses são arquivos de log do Configuration Manager local que a sincronização do Gerenciador de serviço do armazenamento do Azure em nuvem a cada 5 minutos. O gateway de gerenciamento de nuvem enviará por push logs no armazenamento do Azure a cada 5 minutos. Portanto, o atraso máximo será de 10 minutos. Comutadores detalhados afetará os logs de locais e remotos.

- Para implantações de solução de problemas, use **CloudMgr.log** e **CMGSetup.log**
- Para solucionar problemas de integridade do serviço, use **CMGService.log** e **SMS_Cloud_ProxyConnector.log**.
- Para solucionar problemas de tráfego do cliente, use **CMGHttpHandler.log**, **CMGService.log**, e **SMS_Cloud_ProxyConnector.log**.

###  <a name="BKMK_CompSettingsLog"></a>Configurações de conformidade e acesso a recursos da empresa  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com as definições de compatibilidade e o acesso a recursos da empresa.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|CIAgent.log|Regista os detalhes sobre o processo de remediação e compatibilidade das definições de compatibilidade, atualizações de software e gestão de aplicações.|Cliente|  
|CITaskManager.log|Regista informações sobre o agendamento da tarefa de itens de configuração.|Cliente|  
|DCMAgent.log|Regista informações de alto nível sobre a avaliação, a comunicação de conflitos e a remediação de itens de configuração e aplicações.|Cliente|  
|DCMReporting.log|Regista informações sobre os relatórios de resultados da plataforma de política em mensagens de estado para itens de configuração.|Cliente|  
|DcmWmiProvider.log|Registra as informações sobre a leitura de synclets de item de configuração por meio do WMI.|Cliente|  

###  <a name="BKMK_ConsoleLog"></a>Console do Configuration Manager  
 A tabela a seguir lista os arquivos de log que contêm informações relacionadas ao console do Configuration Manager.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|ConfigMgrAdminUISetup.log|Registra a instalação do console do Configuration Manager.|Computador que executa o console do Configuration Manager|  
|SmsAdminUI.log|Registra as informações sobre a operação do console do Configuration Manager.|Computador que executa o console do Configuration Manager|  
|Smsprov.log|Regista atividades executadas pelo fornecedor de SMS. As atividades do console do Configuration Manager usam o provedor de SMS.|Servidor do site ou servidor de sistema de sites|  

###  <a name="BKMK_ContentLog"></a>Gerenciamento de conteúdo  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com a gestão de conteúdos.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|Clouddp-<ServiceName>.log&lt;guid\>. log|Regista os detalhes de um ponto de distribuição baseado na nuvem específico, incluindo informações sobre armazenamento e acesso ao conteúdo.|Servidor do sistema de sites|  
|CloudMgr.log|Registra os detalhes sobre o provisionamento de conteúdo, coletando armazenamento e estatísticas de largura de banda e as ações iniciadas pelo administrador para interromper ou iniciar o serviço de nuvem que executa um ponto de distribuição baseado em nuvem.|Servidor do sistema de sites|  
|DataTransferService.log|Regista todas as comunicações BITS para acesso a políticas ou pacotes. Esse log também é usado para gerenciamento de conteúdo por pontos de distribuição de recepção.|Computador que está configurado como um ponto de distribuição de recepção|  
|PullDP.log|Regista os detalhes sobre o conteúdo que o ponto de distribuição de extração transfere dos pontos de distribuição de origem.|Computador que está configurado como um ponto de distribuição de recepção|  
|PrestageContent.log|Registra os detalhes sobre o uso de ExtractContent.exe ferramenta em um ponto de distribuição remoto e pré-configurado. Esta ferramenta extrai o conteúdo exportado para um ficheiro.|Função do sistema de sites|  
|SMSdpmon.log|Registra os detalhes sobre as tarefas agendadas que estão configuradas em um ponto de distribuição de monitoramento de integridade de ponto de distribuição.|Função do sistema de sites|  
|smsdpprov.log|Regista os detalhes sobre a extração de ficheiros comprimidos recebidos de um site primário. Esse log é gerado pelo provedor WMI do ponto de distribuição remoto.|Computador do ponto de distribuição que não seja colocada com o servidor do site|  


###  <a name="BKMK_DiscoveryLog"></a>Descoberta  
A tabela a seguir lista os arquivos de log que contêm informações relacionadas à descoberta.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|adsgdis.log|Regista ações da Deteção de Grupos de Segurança do Active Directory.|Servidor do site|  
|adsysdis.log|Regista ações da Deteção de Sistemas do Active Directory.|Servidor do site|  
|adusrdis.log|Regista ações da Deteção de Utilizadores do Active Directory.|Servidor do site|  
|ADForestDisc.Log|Regista ações da Deteção de Florestas do Active Directory.|Servidor do site|  
|ddm.log|Regista atividades do gestor de dados de deteção.|Servidor do site|  
|InventoryAgent.log|Regista atividades de inventário de hardware, inventário de software e ações de deteção de heartbeat no cliente.|Cliente|  
|netdisc.log|Regista ações da Deteção de Rede.|Servidor do site|  

###  <a name="BKMK_EPLog"></a>Proteção de ponto de extremidade  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com o Endpoint Protection.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|EndpointProtectionAgent.log|Regista os detalhes sobre a instalação do cliente do Endpoint Protection e a aplicação da política antimalware a esse cliente.|Cliente|  
|EPCtrlMgr.log|Registra os detalhes sobre a sincronização de informações de ameaça de malware do servidor de função de proteção de ponto de extremidade com o banco de dados do Configuration Manager.|Servidor do sistema de sites|  
|EPMgr.log|Monitoriza o estado da função do sistema de sites do Endpoint Protection.|Servidor do sistema de sites|  
|EPSetup.log|Fornece informações sobre a instalação da função de sistema de sites do Endpoint Protection.|Servidor do sistema de sites|  

###  <a name="BKMK_Extensions"></a>Extensões  
 A tabela a seguir lista os arquivos de log que contêm informações relacionadas às extensões.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|AdminUI.ExtensionInstaller.log|Regista informações sobre a transferência de extensões da Microsoft e sobre a instalação e desinstalação de todas as extensões.|Computador que executa o console do Configuration Manager|  
|FeatureExtensionInstaller.log|Registra informações sobre a instalação e remoção das extensões individuais quando elas são habilitadas ou desabilitadas no console do Configuration Manager.|Computador que executa o console do Configuration Manager|  
|SmsAdminUI.log|Registra a atividade de console do Configuration Manager.|Computador que executa o console do Configuration Manager|  

###  <a name="BKMK_InventoryLog"></a>Inventário  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com o processamento de dados de inventário.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|dataldr.log|Registra as informações sobre o processamento de arquivos MIF e inventário de hardware no banco de dados do Configuration Manager.|Servidor do site|  
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
|migmctrl.log|Regista informações sobre ações de migração que envolvam tarefas de migração, pontos de distribuição partilhados e atualizações de pontos de distribuição.|Site de nível superior na hierarquia do Configuration Manager e cada site primário filho.<br /><br /> Numa hierarquia com vários sites primários, utilize o ficheiro de registo criado no site de administração central.|  

###  <a name="BKMK_MDMLog"></a>Dispositivos móveis  
 As seções a seguir listam os arquivos de log que contêm informações relacionadas ao gerenciamento de dispositivos móveis.  

####  <a name="BKMK_EnrollmentLog"></a>Registro  
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
|SMS_DM.log|Registra a comunicação entre o ponto de gerenciamento habilitado para dispositivos móveis e computadores Mac, dispositivos móveis e computadores Mac.|Servidor do sistema de sites|  

####  <a name="BKMK_ExchSrvLog"></a>Conector do Exchange Server  
 Os logs a seguir contêm informações relacionadas ao conector do Exchange Server.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|easdisc.log|Regista as atividades e o estado do conector do Exchange Server.|Servidor do site|  

####  <a name="BKMK_MDLegLog"></a>Herdado de dispositivo móvel  
 A tabela seguinte lista registos que contêm informações relacionadas com o cliente legado do dispositivo móvel.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|DmCertEnroll.log|Regista os detalhes sobre os dados de inscrição do certificado em clientes legados de dispositivos móveis.|Cliente|  
|DMCertResp.htm|Regista a resposta HTML a partir do servidor de certificado quando o programa de inscrição do cliente legado do dispositivo móvel solicita um certificado PKI.|Cliente|  
|DmClientHealth.log|Registra os GUIDs dos clientes herdados de todos os dispositivos móveis que se comunicam com o ponto de gerenciamento habilitado para dispositivos móveis.|Servidor do sistema de sites|  
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

###  <a name="BKMK_OSDLog"></a>Implantação de sistema operacional  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com a implementação do sistema operativo.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|CAS.log|Regista detalhes quando são encontrados pontos de distribuição para conteúdo referenciado.|Cliente|  
|ccmsetup.log|Registra tarefas do ccmsetup para a instalação do cliente, atualização e remoção do cliente. Pode ser utilizado para resolver problemas de instalação de cliente.|Cliente|  
|CreateTSMedia.log|Regista detalhes para a criação de suportes de dados de sequências de tarefas.|Computador que executa o console do Configuration Manager|  
|DeployToVhd.log|Registra os detalhes sobre o processo de criação e modificação de disco rígido Virtual (VHD).|Computador que executa o console do Configuration Manager|  
|Dism.log|Registra ações de instalação do driver ou ações de atualização do aplicativo para a instalação offline.|Servidor do sistema de sites|  
|Distmgr.log|Registra os detalhes sobre a configuração de habilitação de um ponto de distribuição para o Preboot Execution Environment (PXE).|Servidor do sistema de sites|  
|DriverCatalog.log|Regista detalhes sobre controladores de dispositivo importados para o catálogo de controladores.|Servidor do sistema de sites|  
|mcsisapi.log|Regista informações de transferência de pacotes multicast e respostas de pedidos de cliente.|Servidor do sistema de sites|  
|mcsexec.log|Verificação de integridade de registros, namespace, criação de sessão e certificado verificar ações.|Servidor do sistema de sites|  
|mcsmgr.log|Registra as alterações na configuração, o modo de segurança e disponibilidade.|Servidor do sistema de sites|  
|mcsprv.log|Regista a interação do fornecedor de multicast com os Serviços de Implementação do Windows (WDS).|Servidor do sistema de sites|  
|MCSSetup.log|Regista detalhes sobre a instalação da função de servidor multicast.|Servidor do sistema de sites|  
|MCSMSI.log|Regista detalhes sobre a instalação da função de servidor multicast.|Servidor do sistema de sites|  
|Mcsperf.log|Regista detalhes sobre as atualizações do contador de desempenho multicast.|Servidor do sistema de sites|  
|MP_ClientIDManager.log|Regista as respostas do ponto de gestão a sequências de tarefas de pedidos de ID de cliente iniciadas a partir de PXE ou de suportes de dados de arranque.|Servidor do sistema de sites|  
|MP_DriverManager.log|Regista as respostas do ponto de gestão a pedidos de ação da sequência de tarefas Aplicar Controlador Automaticamente.|Servidor do sistema de sites|  
|OfflineServicingMgr.log|Registra os detalhes da atualização e agendas de manutenção offline aplicam ações em arquivos de formato WIM (Windows Imaging) do sistema operacional.|Servidor do sistema de sites|  
|Setupact.log|Regista detalhes sobre os registos do Windows Sysprep e do programa de configuração.|Cliente|  
|Setupapi.log|Regista detalhes sobre os registos do Windows Sysprep e do programa de configuração.|Cliente|  
|Setuperr.log|Regista detalhes sobre os registos do Windows Sysprep e do programa de configuração.|Cliente|  
|smpisapi.log|Regista detalhes sobre as ações de captura e restauro do estado de cliente e informações de limiares.|Cliente|  
|Smpmgr.log|Regista detalhes sobre os resultados de verificações do estado de funcionamento do ponto de migração de estado e de alterações de configuração.|Servidor do sistema de sites|  
|smpmsi.log|Regista detalhes da instalação e configuração do ponto de migração de estado.|Servidor do sistema de sites|  
|smpperf.log|Regista as atualizações do contador de desempenho do ponto de migração de estado.|Servidor do sistema de sites|  
|smspxe.log|Registra os detalhes sobre as respostas a clientes que usam o PXE inicializa e detalhes sobre a expansão de imagens de inicialização e arquivos de inicialização.|Servidor do sistema de sites|  
|smssmpsetup.log|Regista detalhes da instalação e configuração do ponto de migração de estado.|Servidor do sistema de sites|  
|Smsts.log|Regista atividades de sequência de tarefas.|Cliente|  
|TSAgent.log|Regista o resultado de dependências de sequência de tarefas antes de iniciar uma sequência de tarefas.|Cliente|  
|TaskSequenceProvider.log|Regista detalhes sobre sequências de tarefas quando estas são importadas, exportadas ou editadas.|Servidor do sistema de sites|  
|loadstate.log|Regista detalhes sobre a Ferramenta de Migração de Estado de Utilizador (USMT) e o restauro de dados de estado do utilizador.|Cliente|  
|scanstate.log|Regista detalhes sobre a Ferramenta de Migração de Estado de Utilizador (USMT) e a captura de dados de estado do utilizador.|Cliente|  

###  <a name="BKMK_PowerMgmtLog"></a>Gerenciamento de energia  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com a gestão de energia.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|pwrmgmt.log|Registra os detalhes sobre as atividades de gerenciamento de energia no computador cliente, incluindo o monitoramento e a imposição de configurações pelo agente de cliente de gerenciamento de energia.|Cliente|  

###  <a name="BKMK_RCLog"></a>Controle remoto  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com controlo remoto.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|CMRcViewer.log|Regista detalhes sobre a atividade do visualizador de controlo remoto.|Na pasta % temp % no computador que executa o Visualizador de controle remoto|  

###  <a name="BKMK_ReportLog"></a>Emissão de relatórios  
 A tabela a seguir lista os arquivos de log do Configuration Manager que contêm informações relacionadas a relatórios.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|srsrp.log|Regista informações sobre a atividade e o estado do ponto do Reporting Services.|Servidor do sistema de sites|  
|srsrpMSI.log|Regista resultados detalhados do processo de instalação do ponto do Reporting Services a partir da saída MSI.|Servidor do sistema de sites|  
|srsrpsetup.log|Regista resultados do processo de instalação do ponto do Reporting Services.|Servidor do sistema de sites|  

###  <a name="BKMK_RBALog"></a>Administração baseada em função  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com a gestão da administração baseada em funções.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|hman.log|Registra informações sobre as alterações de configuração do site e a publicação de informações do site nos serviços de domínio do Active Directory.|Servidor do site|  
|SMSProv.log|Regista o acesso do fornecedor WMI à base de dados do site.|Computador com o Fornecedor de SMS|  

###  <a name="BKMK_WITLog"></a>Ponto de conexão de serviço  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com o ponto de ligação de serviço.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|CertMgr.log|Regista informações de certificados e de contas proxy.|Servidor do site|  
|CollEval.log|Regista detalhes sobre o momento de criação, alteração e eliminação das coleções pelo Avaliador de Coleção.|Site primário e site de administração central|  
|Cloudusersync.log|Regista a ativação de licenças para os utilizadores.|Computador com o ponto de ligação de serviço|  
|Dataldr.log|Regista informações sobre o processamento de ficheiros MIF.|Servidor do site|  
|ddm.log|Regista atividades do gestor de dados de deteção.|Servidor do site|  
|Distmgr.log|Regista detalhes sobre pedidos de distribuição de conteúdo.|Servidor de site de nível superior|  
|Dmpdownloader.log|Registra os detalhes sobre downloads do Microsoft Intune.|Computador com o ponto de ligação de serviço|  
|Dmpuploader.log|Registra os detalhes relacionados ao carregar alterações do banco de dados para o Microsoft Intune.|Computador com o ponto de ligação de serviço|  
|hman.log|Regista informações sobre o reencaminhamento de mensagens.|Servidor do site|  
|objreplmgr.log|Regista o processamento de política e de atribuição.|Servidor do site principal|  
|PolicyPV.log|Regista a criação de política de todas as políticas.|Servidor do site|  
|outgoingcontentmanager.log|Registra o conteúdo carregado para o Microsoft Intune.|Computador com o ponto de ligação de serviço|  
|Sitecomp.log|Regista os detalhes da instalação do ponto de ligação de serviço.|Servidor do site|  
|SmsAdminUI.log|Registra a atividade de console do Configuration Manager.|Computador que executa o console do Configuration Manager|  
|Smsprov.log|Regista atividades executadas pelo fornecedor de SMS. As atividades do console do Configuration Manager usam o provedor de SMS.|Computador com o Fornecedor de SMS|  
|SrvBoot.log|Regista os detalhes sobre o serviço do instalador do ponto de ligação de serviço.|Computador com o ponto de ligação de serviço|  
|Statesys.log|Regista o processamento de mensagens de gestão de dispositivos móveis.|Site primário e site de administração central|  

###  <a name="BKMK_SU_NAPLog"></a>Atualizações de software  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com as atualizações de software.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|ccmperf.log|Regista atividades relacionadas com a manutenção e a captura de dados relacionados com os contadores de desempenho do cliente.|Cliente|  
|PatchDownloader.log|Regista detalhes sobre o processo de transferência de atualizações de software da origem da atualização para o destino da transferência no servidor do site.|Computador que hospeda o console do Configuration Manager a partir do qual os downloads são iniciados|  
|PolicyEvaluator.log|Regista detalhes sobre a avaliação das políticas em computadores cliente, incluindo políticas de atualizações de software.|Cliente|  
|RebootCoordinator.log|Regista detalhes sobre a coordenação de reinícios do sistema em computadores cliente após instalações de atualizações de software.|Cliente|  
|ScanAgent.log|Regista detalhes sobre pedidos de análise de atualizações de software, a localização do WSUS e ações relacionadas.|Cliente|  
|SdmAgent.log|Registra os detalhes sobre o controle de correção e conformidade. No entanto, o arquivo de log de atualizações de software, o Updateshandler.log, fornece detalhes mais informativos sobre como instalar as atualizações de software que são necessárias para conformidade.<br /><br /> Este ficheiro de registo é partilhado com definições de compatibilidade.|Cliente|  
|ServiceWindowManager.log|Regista detalhes sobre a avaliação de janelas de manutenção.|Cliente|  
|SmsWusHandler.log|Regista detalhes sobre o processo de análise da Ferramenta de Inventário das Atualizações da Microsoft.|Cliente|  
|StateMessage.log|Registra os detalhes sobre o software atualizar mensagens de estado que são criadas e enviadas ao ponto de gerenciamento.|Cliente|  
|SUPSetup.log|Regista detalhes sobre a instalação do ponto de atualização de software. Quando a instalação de ponto de atualização de software estiver concluída, é escrito **Instalação bem-sucedida** neste ficheiro de registo.|Servidor do sistema de sites|  
|UpdatesDeployment.log|Regista detalhes sobre implementações no cliente, incluindo a ativação, avaliação e imposição de atualizações de software. O registo verboso mostra informações adicionais sobre a interação com a interface de utilizador do cliente.|Cliente|  
|UpdatesHandler.log|Regista detalhes sobre a análise de compatibilidade de atualizações de software e sobre a transferência e instalação de atualizações de software no cliente.|Cliente|  
|UpdatesStore.log|Regista detalhes sobre o estado de compatibilidade das atualizações de software que foram analisadas durante o ciclo de análise de compatibilidade.|Cliente|  
|WCM.log|Registra os detalhes sobre o software atualizar configurações de ponto e conexões ao servidor do WSUS para categorias de atualização assinadas, classificações e idiomas.|Servidor do site|  
|WSUSCtrl.log|Regista detalhes sobre a configuração, a conectividade de base de dados e o estado de funcionamento do servidor WSUS do site.|Servidor do sistema de sites|  
|wsyncmgr.log|Registra os detalhes sobre o software atualizar o processo de sincronização.|Servidor do site|  
|WUAHandler.log|Regista detalhes sobre o Windows Update Agent no cliente quando este procura atualizações de software.|Cliente|  

###  <a name="BKMK_WOLLog"></a>Wake On LAN  
 A tabela a seguir lista os arquivos de log que contêm informações relacionadas ao uso de Wake On LAN.  

> [!NOTE]  
>  Quando você suplementa o Wake On LAN usando proxy de ativação, essa atividade será registrada no cliente. Por exemplo, consulte CcmExec.log e SleepAgent_ <*domínio* \> @SYSTEM_0.log no [operações do cliente](#BKMK_ClientOpLogs) seção deste tópico.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|wolcmgr.log|Regista detalhes sobre quais os clientes que devem receber pacotes de reativação, o número de pacotes de reativação enviados e o número de pacotes de reativação repetidos.|Servidor do site|  
|wolmgr.log|Regista detalhes sobre procedimentos de reativação automática, tais como a reativação de implementações que estão configuradas para Reativação por LAN.|Servidor do site|  

###  <a name="BKMK_WindowsServicingLog"></a>Serviço do Windows 10  
 A tabela a seguir lista os arquivos de log que contêm informações relacionadas ao serviço do Windows 10.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|ccmperf.log|Regista atividades relacionadas com a manutenção e a captura de dados relacionados com os contadores de desempenho do cliente.|Cliente|  
|CcmRepair.log|Regista as atividades de reparação do agente de cliente.|Cliente|
|PatchDownloader.log|Regista detalhes sobre o processo de transferência de atualizações de software da origem da atualização para o destino da transferência no servidor do site.|Computador que hospeda o console do Configuration Manager a partir do qual os downloads são iniciados|  
|PolicyEvaluator.log|Regista detalhes sobre a avaliação das políticas em computadores cliente, incluindo políticas de atualizações de software.|Cliente|  
|RebootCoordinator.log|Regista detalhes sobre a coordenação de reinícios do sistema em computadores cliente após instalações de atualizações de software.|Cliente|  
|ScanAgent.log|Regista detalhes sobre pedidos de análise de atualizações de software, a localização do WSUS e ações relacionadas.|Cliente|  
|SdmAgent.log|Registra os detalhes sobre o controle de correção e conformidade. No entanto, o arquivo de log de atualizações de software, o UpdatesHandler.log, fornece detalhes mais informativos sobre como instalar as atualizações de software que são necessárias para conformidade.<br /><br /> Este ficheiro de registo é partilhado com definições de compatibilidade.|Cliente|  
|ServiceWindowManager.log|Regista detalhes sobre a avaliação de janelas de manutenção.|Cliente|  
|Setupact.log|Arquivo de log primário para a maioria dos erros que ocorrem durante o processo de instalação do Windows. O arquivo de log está localizado na pasta % windir %\$Windows.~BT\sources\panther pasta.|Cliente|
|SmsWusHandler.log|Regista detalhes sobre o processo de análise da Ferramenta de Inventário das Atualizações da Microsoft.|Cliente|  
|StateMessage.log|Regista detalhes sobre as mensagens de estado de atualizações de software que são criadas e enviadas para o ponto de gestão.|Cliente|  
|SUPSetup.log|Regista detalhes sobre a instalação do ponto de atualização de software. Quando a instalação de ponto de atualização de software estiver concluída, é escrito **Instalação bem-sucedida** neste ficheiro de registo.|Servidor do sistema de sites|  
|UpdatesDeployment.log|Regista detalhes sobre implementações no cliente, incluindo a ativação, avaliação e imposição de atualizações de software. O registo verboso mostra informações adicionais sobre a interação com a interface de utilizador do cliente.|Cliente|  
|Updateshandler.log|Regista detalhes sobre a análise de compatibilidade de atualizações de software e sobre a transferência e instalação de atualizações de software no cliente.|Cliente|  
|UpdatesStore.log|Regista detalhes sobre o estado de compatibilidade das atualizações de software que foram analisadas durante o ciclo de análise de compatibilidade.|Cliente|  
|WCM.log|Registra os detalhes sobre o software atualizar configurações de ponto e conexões ao servidor do WSUS para categorias de atualização assinadas, classificações e idiomas.|Servidor do site|  
|WSUSCtrl.log|Regista detalhes sobre a configuração, a conectividade de base de dados e o estado de funcionamento do servidor WSUS do site.|Servidor do sistema de sites|  
|wsyncmgr.log|Registra os detalhes sobre o software atualizar o processo de sincronização.|Servidor do site|  
|WUAHandler.log|Regista detalhes sobre o Windows Update Agent no cliente quando este procura atualizações de software.|Cliente|  

###  <a name="BKMK_WULog"></a>O Windows Update Agent  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com o Windows Update Agent.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|WindowsUpdate.log|Registra os detalhes sobre quando o Windows Update Agent se conecta ao servidor do WSUS e recupera as atualizações de software para avaliação de conformidade, e se há atualizações para os componentes do agente.|Cliente|  

###  <a name="BKMK_WSUSLog"></a>Servidor do WSUS  
 A tabela seguinte lista os ficheiros de registo que contêm informações relacionadas com o servidor WSUS.  

|Nome do registo|Descrição|Computador com o ficheiro de registo|  
|--------------|-----------------|----------------------------|  
|Change.log|Registra os detalhes sobre informações de banco de dados do servidor do WSUS foi alterada.|Servidor WSUS|  
|SoftwareDistribution.log|Registra os detalhes sobre as atualizações de software que foram sincronizados de origem de atualização configurada para o banco de dados do servidor do WSUS.|Servidor WSUS|  

