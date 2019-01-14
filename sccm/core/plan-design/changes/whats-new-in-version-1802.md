---
title: Nova versão 1802
titleSuffix: Configuration Manager
description: Obtenha detalhes sobre alterações e novas funcionalidades introduzidas na versão 1802 do Configuration Manager.
ms.date: 06/12/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5bd637b1-d7a1-411b-877a-c7aae9741173
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 763826a1a308130415fb972f7f3dc3e577b8e573
ms.sourcegitcommit: a3cec96a771eed69e58a29917d1a3fe1a5fb2e73
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/14/2019
ms.locfileid: "54250736"
---
# <a name="whats-new-in-version-1802-of-system-center-configuration-manager"></a>O que há de novo na versão 1802 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Atualização 1802 para o ramo atual do Configuration Manager está disponível como uma atualização na consola. Aplica esta atualização de sites que executam a versão 1702, 1706 ou 1710. <!-- baseline only statement: -->Ao instalar um novo site, também está disponível como uma versão de linha de base.

Além das novas funcionalidades, esta versão também inclui alterações adicionais, como correções de erros. Para obter mais informações, consulte [resumo das alterações no ramo atual do System Center Configuration Manager, versão 1802](https://support.microsoft.com/help/4101375).

As seguintes atualizações adicionais para esta versão também estão agora disponíveis:
- [Update rollup para o ramo atual do System Center Configuration Manager, versão 1802](https://support.microsoft.com/help/4163547)

> [!TIP]  
> Para instalar um novo site, tem de utilizar uma versão de linha de base do Configuration Manager.  
>
>  Saiba mais sobre:    
>   - [Instalar novos sites](/sccm/core/servers/deploy/install/installing-sites)  
>   - [Instalar atualizações em sites](/sccm/core/servers/manage/updates)  
>   - [Versões de linha de base e de atualização](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

As secções seguintes fornecem detalhes sobre as alterações e novas capacidades na versão 1802 do Configuration Manager.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).

Version 1802 drops support for the following products:
-->


## <a name="site-infrastructure"></a>Infraestrutura do site

### <a name="reassign-distribution-point"></a>Reatribuir o ponto de distribuição
<!-- 1306937 --> Muitos clientes têm de grandes infra-estruturas de Configuration Manager e reduzindo os sites primários ou secundários para simplificar o seu ambiente. Eles ainda precisam manter os pontos de distribuição nas localizações das sucursais para servir de conteúdo para clientes gerenciados. Esses pontos de distribuição geralmente contêm vários terabytes, ou mais dos conteúdos. Este conteúdo é dispendioso em termos de largura de banda de rede e de tempo para distribuir a estes servidores remotos. Esta funcionalidade permite-lhe reatribuir um ponto de distribuição para outro site principal sem redistribuir o conteúdo. Esta ação atualiza a atribuição de sistema do site e a persistência de todo o conteúdo no servidor. Para obter mais informações, consulte [reatribuir um ponto de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_reassign).

### <a name="configure-windows-delivery-optimization-to-use-configuration-manager-boundary-groups"></a>Configurar a Otimização da entrega do Windows para utilizar grupos de limites do Configuration Manager
<!-- 1324696 --> Utilizar grupos de limites do Configuration Manager para definir e regular a distribuição de conteúdo em sua rede empresarial e em escritórios remotos. [Otimização da entrega do Windows](/windows/deployment/update/waas-delivery-optimization) é uma tecnologia baseada na cloud, o ponto-a-ponto para partilhar conteúdo entre os dispositivos Windows 10. A partir desta versão, configure a otimização de entrega a utilizar os grupos de limites, quando partilha de conteúdo entre elementos de rede. Um nova definição de cliente aplica-se o identificador de grupo de limites como o identificador de grupo de Otimização da entrega no cliente. Quando o cliente comunica com o serviço de cloud de otimização de entrega, ele usa esse identificador para localizar os colegas com os conteúdos pretendidos. Para obter mais informações, consulte [conceitos fundamentais da gestão de conteúdos](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#delivery-optimization).

### <a name="support-for-windows-10-arm64-devices"></a>Suporte para dispositivos Windows 10 ARM64
<!-- 1353704 --> A partir desta versão que cliente do Configuration Manager é suportado em dispositivos Windows 10 ARM64. Funcionalidades de gestão de cliente existentes devem trabalhar com esses novos dispositivos. Por exemplo, hardware e inventário de software, atualizações de software e gerenciamento de aplicativos. Implementação do sistema operativo não é atualmente suportada. 

### <a name="improved-support-for-cng-certificates"></a>Suporte aprimorado para certificados CNG
<!-- 1357314 --> Configuration Manager (ramo atual) versão 1710 suporta [Cryptography: Certificados de próxima geração (CNG)](/sccm/core/plan-design/network/cng-certificates-overview). Limites de versão 1710 suportam para certificados de cliente em vários cenários. 

A partir desta versão, utilize certificados CNG para as seguintes funções de servidor com capacidade para HTTPS:
- Ponto de gestão
- Ponto de distribuição
- Ponto de atualização de software
- Ponto de Migração de Estado  


### <a name="boundary-group-fallback-for-management-points"></a>Contingência para pontos de gestão do grupo de limites
<!-- 1324594 --> Configurar as relações de contingência para pontos de gestão entre [grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups). Esse comportamento fornece maior controle para os pontos de gestão que os clientes utilizam. Para obter mais informações, consulte [configurar grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups#management-points).


### <a name="cloud-distribution-point-site-affinity"></a>Afinidade de site do ponto de distribuição de nuvem
<!--503719--> Esta funcionalidade beneficia os clientes com uma hierarquia de múltiplos site, geograficamente dispersa com pontos de distribuição de nuvem. Quando um cliente baseado na internet procura de conteúdo, anteriormente não havia nenhuma ordem à lista de pontos de distribuição de nuvem recebida pelo cliente. Esse comportamento pode resultar em clientes baseados na internet que recebem o conteúdo de pontos de distribuição de nuvem, geograficamente distante. Transferir o conteúdo de um servidor distante desse tipo é normalmente mais lento do que um servidor com mais detalhes.
 
Com a afinidade de site de ponto de distribuição de nuvem, um cliente baseado na internet recebe uma lista ordenada. Esta lista dá prioridade aos pontos de distribuição de nuvem de site atribuído do cliente. Este comportamento permite ao administrador preservar a sua intenção de design para transferência de conteúdo a partir dos recursos de site.
 

## <a name="management-insights"></a>Informações de gestão
<!-- 1353967 --> Informações de gestão no System Center Configuration Manager fornecem informações sobre o estado atual do seu ambiente. As informações baseia-se na análise de dados da base de dados do site. Insights ajudá-lo para melhor compreender o seu ambiente e tome medidas com base nas informações. Para obter detalhes, veja [informações de gestão](/sccm/core/servers/manage/management-insights)

Na versão 1802 do Gestor de configuração, as informações seguintes estão disponíveis:
- Aplicações:
    - Aplicações sem implementações
- Serviços cloud: <!--1356412-->
    - Avaliar a preparação de cogestão 
    - Ativar os seus dispositivos para serem híbridos associados ao Azure Active Directory
    - Modernize a sua infraestrutura de identidade e acesso
    -  Atualizar os clientes para o Windows 10, versão 1709 ou superior 
- Coleções:
    - Coleções vazias
- Gestão simplificada:  <!--1355148-->
    - Versões de cliente Desatualizadas  
- Centro de Software: 
    - Direcionar os utilizadores ao centro de Software em vez do catálogo de aplicações  
    - Utilizar a nova versão do Centro de Software 
- Windows 10: <!--1357421-->
    - Configurar telemetria do Windows e a chave do ID comercial 
    - Ligar o Configuration Manager à preparação de atualizações 
   
<!-- ## Migration  -->



## <a name="client-management"></a>Gestão de clientes

### <a name="cloud-management-gateway-support-for-azure-resource-manager"></a>Suporte do gateway de gestão da cloud para o Azure Resource Manager
<!-- 1324735 --> Ao criar uma instância do [gateway de gestão na cloud](/sccm/core/clients/manage/plan-cloud-management-gateway) (CMG), o assistente agora fornece a opção para criar um **implementação Azure Resource Manager**. [O Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) é uma plataforma moderna para o gerenciamento de todos os recursos de solução como uma única entidade, chamada um [grupo de recursos](/azure/azure-resource-manager/resource-group-overview#resource-groups). Quando implementa o CMG com o Azure Resource Manager, o site utiliza o Azure Active Directory (Azure AD) para autenticar e criar os recursos da cloud necessários. Esta implementação reestruturação não exige o certificado de gestão clássico do Azure. Para obter mais informações, consulte [design da topologia CMG](/sccm/core/clients/manage/plan-cloud-management-gateway#azure-resource-manager).

> [!IMPORTANT]
> Esta capacidade não ative o suporte para fornecedores de serviços de Cloud do Azure (CSP). A implementação do CMG com o Azure Resource Manager continua a utilizar o serviço de cloud clássica, o que não suporta o CSP. Para obter mais informações, consulte [serviços do Azure disponíveis no Azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services).  

### <a name="improvements-to-cloud-management-gateway"></a>Melhorias para a cloud do gateway de gestão  

- A partir desta versão, o **gateway de gestão da nuvem** já não é uma funcionalidade de pré-lançamento.  

- A documentação de funcionalidade é revista e avançada. Para obter mais informações, veja os artigos seguintes:
    - [Plano para o gateway de gestão da cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)
    - [Tamanho do gateway de gestão da cloud e dimensione números](/sccm/core/plan-design/configs/size-and-scale-numbers#bkmk_cmg)
    - [Segurança e privacidade para o gateway de gestão na cloud ](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)
    - [Perguntas mais frequentes sobre o gateway de gestão da cloud](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)
    - [Certificados para o gateway de gestão na cloud](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)
    - [Configurar o gateway de gestão na cloud](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)  


### <a name="configure-hardware-inventory-to-collect-strings-larger-than-255-characters"></a>Configurar o inventário de hardware para recolher as cadeias de caracteres superiores a 255 carateres
<!-- 1357389 --> Pode configurar o comprimento de cadeias de caracteres para ter mais de 255 carateres para propriedades de inventário de hardware. Esta alteração aplica-se apenas a classes adicionadas recentemente e para as propriedades de inventário de hardware que não são as chaves. Para obter detalhes, consulte a [expandir o inventário de hardware](/sccm/core/clients/manage/inventory/extend-hardware-inventory#BKMK_GreaterThan255) artigo. 

 ### <a name="deprecation-announcement-for-linux-and-unix-client-support"></a>Anúncio de preterição para o suporte de cliente de Linux e Unix
 <!--510139--> A Microsoft pretende Preterir o suporte de cliente Linux e UNIX no System Center Configuration Manager aproximadamente um ano de agora, por exemplo, que os clientes não serão incluídos no 1902 SCCM versão num calendário de início de 2019. A versão do Configuration Manager 1810, num calendário de final de 2018, será a última versão para incluir os clientes Linux e UNIX, e eles serão suportados para o ciclo de vida completo de 1810 do Gestor de configuração. Depois de 1810 do Gestor de configuração, os clientes devem considerar o Microsoft Azure Management para o gerenciamento de servidores Linux. Soluções do Azure tem amplo suporte de Linux que, na maioria dos casos, ter mais de funcionalidade do Configuration Manager, incluindo o gerenciamento de patches de ponto-a-ponto para Linux.

### <a name="surface-device-dashboard"></a>Dashboard de dispositivos Surface
<!--1355788--> O dashboard de dispositivos Surface fornece informações sobre os dispositivos Surface encontrado no seu ambiente. Na consola, aceda a **monitorização** > **dispositivos Surface**. Pode ver os itens:
- Número de Surfaces
- Percentagem de modelos de surfaces
- Principais cinco versões de firmware

Para obter detalhes, consulte a [painel do Surface](/sccm/core/clients/manage/surface-device-dashboard) artigo.

### <a name="change-in-the-configuration-manager-client-install"></a>Instalar a alteração no cliente do Configuration Manager
<!--1356195--> A partir desta versão, o Silverlight é já não está instalado nos dispositivos cliente automaticamente. Para obter mais informações, consulte [pré-requisitos para implementar clientes em computadores Windows](/sccm/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers#bkmk_ExternalDependencies)

## <a name="co-management"></a>Cogestão

### <a name="transition-endpoint-protection-workload-to-intune-using-co-management"></a>Carga de trabalho de proteção de ponto final de transição para o Intune através de cogestão
<!-- 1357365 --> A carga de trabalho do Endpoint Protection pode ser transferida para o Intune depois de ativar a cogestão. Para fazer a transição da carga de trabalho do Endpoint Protection, vá para a página de propriedades de cogestão e mova a barra de controlo de deslize do Configuration Manager para **piloto** ou **todos os**. Para obter detalhes sobre as cargas de trabalho, consulte [cargas de trabalho de cogestão](/sccm/comanage/workloads). Para obter mais informações sobre a cogestão, consulte [cogestão para dispositivos Windows 10](/sccm/comanage/overview).
 
### <a name="co-management-dashboard-in-system-center-configuration-manager"></a>Dashboard de cogestão no System Center Configuration Manager
<!--1356648--> A partir desta versão, pode ver um dashboard com informações sobre a cogestão. O dashboard ajuda-o a rever as máquinas que fazem cogeridas no seu ambiente. Os gráficos podem ajudar a identificar os dispositivos que possam necessitar de atenção. Para obter detalhes, consulte a [dashboard de cogestão](/sccm/core/clients/manage/client-management-dashboard) artigo. 


## <a name="compliance-settings"></a>Definições de compatibilidade

### <a name="microsoft-edge-browser-policies"></a>Políticas de browser Microsoft Edge
<!-- 1357310 --> Para os clientes que utilizam o [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) web browser em clientes Windows 10, criar uma política de definições de compatibilidade do Configuration Manager para configurar várias definições do Microsoft Edge. Para obter mais informações, consulte [perfil do browser Microsoft Edge criar](/sccm/compliance/deploy-use/browser-profiles). 



## <a name="application-management"></a>Gestão de Aplicações

### <a name="allow-user-interaction-when-installing-an-application"></a>Permitir a interação do usuário ao instalar um aplicativo
<!-- 1356976 --> Permitir que um utilizador final interagir com uma instalação da aplicação durante a execução da sequência de tarefas. Por exemplo, execute um processo de configuração que solicita ao usuário final para várias opções. Alguns instaladores de aplicativo não é possível silence avisos do utilizador ou o processo de instalação pode exigir valores de configuração específicas apenas conhecidas do usuário. Esta funcionalidade permite-lhe lidar com esses cenários de instalação. Para obter mais informações, consulte [especificar as opções de experiência de utilizador para o tipo de implementação](/sccm/apps/deploy-use/create-applications#specify-user-experience-options-for-the-deployment-type).

### <a name="do-not-automatically-upgrade-superseded-applications"></a>Não atualizar automaticamente aplicações substituídas
<!-- 1351266 --> Configure uma implementação de aplicações para atualizar automaticamente todas as versões substituídas. Agora quando criar a implementação, na **definições de implementação** página do **Assistente de implementação de Software**, para **disponível** instalar fim, pode ativar ou desativar o a opção de **atualizar automaticamente qualquer substituídas versões desta aplicação**. Para obter mais informações, consulte [especificar definições de implementação](/sccm/apps/deploy-use/deploy-applications#specify-deployment-settings).

### <a name="approve-application-requests-for-users-per-device"></a>Aprovar pedidos de aplicações para utilizadores por dispositivo
<!-- 1357015 --> A partir desta versão, quando um utilizador solicita um aplicativo que necessite de aprovação, o nome de dispositivo específico é agora uma parte do pedido. Se o administrador aprova o pedido, o utilizador só é possível instalar o aplicativo nesse dispositivo. O utilizador tem de submeter outro pedido para instalar a aplicação noutro dispositivo. Para obter mais informações, consulte [especificar definições de implementação](/sccm/apps/deploy-use/deploy-applications#specify-deployment-settings).

 > [!Note]  
 > Esta é uma funcionalidade opcional. Para mais informações, consulte [Enable optional features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  


### <a name="run-scripts-improvements"></a>Execute as melhorias de scripts 
<!-- 1236459 --> Nesta versão, a partir **executar Scripts** já não é uma funcionalidade de pré-lançamento. Agora, a saída do script retorna usando a formatação do JSON. Para obter mais informações, consulte [criar e executar scripts do PowerShell da consola do Configuration Manager](/sccm/apps/deploy-use/create-deploy-scripts).


## <a name="operating-system-deployment"></a>Implementação do sistema operativo

### <a name="windows-10-in-place-upgrade-task-sequence-via-cloud-management-gateway"></a>Sequência de tarefas de atualização in-loco do Windows 10 através do gateway de gestão da cloud
<!-- 1357149 --> O Windows 10 [sequência de tarefas atualização in-loco](/sccm/osd/deploy-use/upgrade-windows-to-the-latest-version) agora oferece suporte à implantação para os clientes baseados na internet geridos através do [gateway de gestão da nuvem](/sccm/core/clients/manage/plan-cloud-management-gateway). Esta capacidade permite aos usuários remotos mais facilmente atualizar para o Windows 10, sem terem de se ligar à rede empresarial. Para obter mais informações, veja [Deploy a task sequence (Implementar uma sequência de tarefas)](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#deploy-windows-10-in-place-upgrade-via-cmg).

### <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Melhoramentos à sequência de tarefas de atualização in-loco do Windows 10
<!-- 1357425 --> O modelo de sequência de tarefas padrão para a atualização in-loco do Windows 10 inclui agora grupos adicionais com as ações recomendadas para adicionar antes e depois do processo de atualização. Estas ações são comuns entre muitos clientes que estão com êxito a atualizar dispositivos Windows 10. Para obter mais informações, consulte [criar uma sequência de tarefas para atualizar um sistema operacional](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#recommended-task-sequence-steps-to-prepare-for-upgrade).

### <a name="improvements-to-operating-system-deployment"></a>Melhorias para implementação do sistema operativo
Esta versão inclui as seguintes melhorias para implementação do sistema operativo:
 - No Windows PE, ao iniciar cmtrace.exe, já não for pedido para escolher se pretende tornar este Visualizador padrão para ficheiros de registo do programa. <!-- SMS 500897 -->
 - Adicionar imagens de arranque para o [transferir conteúdo do pacote](/sccm/osd/understand/task-sequence-steps#BKMK_DownloadPackageContent) passo de sequência de tarefas.
 - Melhorias para o [executar a sequência de tarefas](/sccm/osd/understand/task-sequence-steps#child-task-sequence) passo: <!-- 1261338 -->   
     - Suporte para todos os cenários de implementação do sistema operativo do Centro de Software, PXE e suporte de dados.
     - Melhorias para ações como copiar, importar, exportar e aviso durante a eliminação de objetos da consola.
     - Suporte para o [criar pré-configuradas de ficheiro de conteúdo](/sccm/core/plan-design/hierarchy/manage-network-bandwidth#BKMK_PrestagingContent) assistente.
     - Integração com verificação de implementação. Para obter mais informações, consulte [implementações de sequência de tarefas de alto risco](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS). 
     - O passo de sequência de tarefas executar agora pode ser utilizado em vários níveis de sequências de tarefas, não apenas uma relação de único principal-subordinado. Relações de múltiplos níveis aumentar a complexidade, use com cautela. Esses relacionamentos ainda estão marcados para referências circulares.
    
### <a name="deployment-templates-for-task-sequences"></a>Modelos de implementação para sequências de tarefas
<!-- 1357391 --> O [Assistente de implementação para sequências de tarefas](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS) agora pode criar um modelo de implementação. O modelo de implementação pode ser salvo e aplicado a uma sequência de tarefas nova ou existente para criar uma implementação. 

### <a name="phased-deployments-for-task-sequences"></a>Implementações faseadas para sequências de tarefas
<!--1356837--> As implementações faseadas é um [funcionalidade de pré-lançamento](/sccm/core/servers/manage/pre-release-features). As implementações faseadas automatizam uma implementação coordenada e sequenciada de uma sequência de tarefas em vários conjuntos. Pode [criar implementações faseadas](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence) com a predefinição de duas fases, ou configurar manualmente as várias fases. Implementação faseada de sequências de tarefas não suporta a instalação de PXE ou suportes de dados.




## <a name="software-center"></a>Centro de software

### <a name="install-multiple-applications-in-software-center"></a>Instalar várias aplicações no Centro de Software
<!-- 1357126 --> Se um usuário final ou técnico de área de trabalho tem de instalar várias aplicações num dispositivo, o Centro de Software suporta agora a instalar diversas aplicações selecionadas. Este comportamento permite que o usuário a ser mais eficiente enquanto não aguarda uma instalação seja concluída antes de iniciar a próxima. Para obter mais informações, consulte [instalar várias aplicações](/sccm/core/understand/software-center#install-multiple-applications) no guia de utilizador nova do Centro de Software.

### <a name="use-software-center-to-browse-and-install-user-available-applications-on-azure-ad-joined-devices"></a>Utilizar o Centro de Software para procurar e instalar aplicações disponíveis para o utilizador em dispositivos associados ao AD Azure
<!-- 1322613 --> Se implementar aplicações como disponíveis para os utilizadores, agora pode procurar e instalá-los através do Centro de Software em dispositivos do Azure Active Directory (Azure AD). Para obter mais informações, consulte [implementar aplicações disponíveis para o utilizador em dispositivos associados ao AD Azure](/sccm/apps/deploy-use/deploy-applications#deploy-user-available-applications-on-azure-ad-joined-devices).

### <a name="hide-installed-applications-in-software-center"></a>Ocultar aplicações instaladas no Centro de Software
<!--1357592--> Agora é possível ocultar aplicações instaladas no Centro de Software. Aplicativos que já estejam instalados já não aparecerá no separador aplicações quando esta opção está ativada nas definições de cliente. Esta opção estiver definida como predefinição ao instalar ou atualizar para o Configuration Manager 1802.  Aplicações instaladas ainda estão disponíveis para revisão no separador de estado de instalação. [Aplicações de ocultar instalado no Centro de Software](/sccm/core/clients/deploy/about-client-settings#BKMK_HideInstalled) tem detalhes adicionais.   

### <a name="hide-unapproved-applications-in-software-center"></a>Ocultar aplicações não aprovadas no Centro de Software
 <!--1355146--> Quando esta opção de definição de cliente está ativada, os aplicativos disponíveis de usuário que exigem a aprovação estão ocultos no Centro de Software.  [Ocultar aplicações não aprovadas no Centro de Software](/sccm/core/clients/deploy/about-client-settings#BKMK_HideUnapproved) tem detalhes adicionais.  

### <a name="software-center-shows-user-additional-compliance-information"></a>Centro de software mostra informações de conformidade adicionais do utilizador
<!-- 1235616 --> Quando utiliza o estado de atestado de estado de funcionamento do dispositivo como uma regra de política de conformidade para o acesso condicional aos recursos da empresa, o Centro de Software mostra agora o utilizador a definição de atestado de estado de funcionamento do dispositivo que não está em conformidade.


 ## <a name="software-updates"></a>Atualizações de software 

### <a name="schedule-automatic-deployment-rule-evaluation-to-be-offset-from-a-base-day"></a>Agendar avaliação de regra de implementação automática desfasamento de um dia base. 
<!--1357133--> Regras de implementação automática podem ser agendadas para avaliar o desvio de um dia base. Ou seja, se patch Terça-feira, na verdade, se na quarta-feira para, o agendamento de avaliação pode ser definido para a segunda Terça-feira do deslocamento de mês por um dia. Para obter detalhes, consulte [implementar automaticamente atualizações de software](/sccm/sum/deploy-use/automatically-deploy-software-updates#BKMK_CreateAutomaticDeploymentRule). 



## <a name="reporting"></a>Relatórios

### <a name="report-for-default-browser-counts"></a>Relatório de contagens de browser predefinido
<!-- 1357830 --> Agora há um novo relatório para mostrar a contagem de clientes com um navegador da web específicas como sendo o padrão do Windows. Consulte a **contagens de Browser predefinido** relatório no **Software - empresas e produtos** grupo de relatórios. Para obter mais informações, consulte a [lista de relatórios](/sccm/core/servers/manage/list-of-reports#software---companies-and-products).

### <a name="report-on-windows-autopilot-device-information"></a>Relatório sobre as informações de dispositivo do Windows Autopilot
<!-- 1351442 --> Windows Autopilot é uma solução de integração e a configuração de novos dispositivos Windows 10 de uma maneira moderna. Para obter mais informações, consulte um [descrição geral do Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-10-autopilot). É um método de registo de dispositivos existentes no Windows Autopilot carregar as informações de dispositivo para a Microsoft Store para empresas e Education. Estas informações incluem o número de série do dispositivo, o identificador do produto Windows e um identificador de hardware. Utilize o Gestor de configuração para recolher e comunicar estas informações de dispositivo com o novo relatório **informações de dispositivo do Windows Autopilot**, na **Hardware - geral** nó de relatórios. Para obter mais informações, consulte [como preparar os dispositivos baseados na internet para a cogestão](/sccm/comanage/how-to-prepare-win10#windows-autopilot) na preparação para a cogestão.

### <a name="report-on-windows-10-servicing-details-for-a-specific-collection"></a>Relatório sobre os detalhes de manutenção do Windows 10 para uma coleção específica
<!--1357653--> O **detalhes de manutenção do Windows 10 para uma coleção específica** relatório apresenta informações gerais sobre a manutenção do Windows 10 para uma coleção específica. Este relatório mostra o ID de recurso, nome NetBIOS, nome do SO, o nome de versão do SO, compilação, ramo de SO e manutenção de estado para dispositivos Windows 10. Para obter mais informações, consulte o [lista de relatórios](/sccm/core/servers/manage/list-of-reports#operating-system)



<!-- ## Inventory  -->



<!-- ## Mobile device management -->



 ## <a name="protect-devices"></a>Proteger dispositivos

### <a name="improvements-to-configuration-manager-policies-for-windows-defender-exploit-guard"></a>Melhorias às políticas do Configuration Manager para o Windows Defender exploram Guard
<!-- 1356220 --> Definições de política adicionais para o [redução da superfície de ataque](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy#BKMK_ASR) e [acesso a pastas controladas](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy#BKMK_CFA) componentes foram adicionados no Configuration Manager para [Windows Defender Exploit Guard ](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-exploit-guard/windows-defender-exploit-guard).

### <a name="new-host-interaction-settings-for-windows-defender-application-guard"></a>Novas definições de interação de anfitrião para o Windows Defender Application Guard
<!-- 1356256 --> Para Windows 10 versão 1709 ou dispositivos posteriores, existem duas configurações de interação anfitrião novo para [Windows Defender Application Guard](/sccm/protect/deploy-use/create-deploy-application-guard-policy#BKMK_HIS): 
- Web sites podem ser dado acesso ao processador de gráficos virtual do anfitrião. 
- Os ficheiros transferidos dentro do contentor podem ser mantidos no anfitrião. 




## <a name="configuration-manager-console"></a>Consola do Configuration Manager

### <a name="improvements-to-the-configuration-manager-console"></a>Melhorias à consola do Configuration Manager 
Esta versão inclui as seguintes melhorias à consola do Configuration Manager.
- Listas de dispositivos em ativos e compatibilidade, dispositivos, agora apresentam o utilizador primário por predefinição. Esta coluna apresenta apenas no nó dispositivos. O último utilizador com sessão iniciado também pode ser adicionado como uma coluna opcional.<!-- 1357280 --> Ativar [afinidade dispositivo / utilizador](/sccm/core/clients/deploy/about-client-settings#user-and-device-affinity) definições de cliente para o site para associar um utilizador primário com um dispositivo.
- Se uma coleção é um membro de outra coleção e o nome é mudado, em seguida, o novo nome é atualizado nas regras de associação.<!--1357282--> 
- Ao utilizar o controlo remoto num cliente com vários monitores, o dimensionamento PPP de diferentes, o cursor do rato agora corretamente mapeia entre eles. <!--433170-->
- O [dashboard de gestão de clientes do Office 365](/sccm/sum/deploy-use/manage-office-365-proplus-updates#office-365-client-management-dashboard) apresenta uma lista de dispositivos relevantes quando as secções do gráfico estão selecionadas. <!--1357281 --> 



## <a name="next-steps"></a>Passos Seguintes
Quando estiver pronto para instalar esta versão, consulte [atualizações do Configuration Manager](/sccm/core/servers/manage/updates).
