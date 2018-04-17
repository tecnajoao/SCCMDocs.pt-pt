---
title: Nova versão 1802
titleSuffix: Configuration Manager
description: Obter informações sobre as alterações e novas funcionalidades introduzidas na versão 1802 do Configuration Manager.
ms.custom: na
ms.date: 04/11/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5bd637b1-d7a1-411b-877a-c7aae9741173
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a667c34dc39ef0578ff840e5603080b09c67c63c
ms.sourcegitcommit: fb84bcb31d825f454785e3d9d8be669e00fe2b27
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/16/2018
---
# <a name="whats-new-in-version-1802-of-system-center-configuration-manager"></a>Novidades na versão 1802 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Atualize 1802 para o ramo atual do Configuration Manager está disponível como uma atualização na consola. Aplicar esta atualização em sites que executam a versão 1702, 1706 ou 1710. <!-- baseline only statement: -->Ao instalar um novo site, também está disponível como uma versão de linha de base.

Para além de novas funcionalidades, esta versão inclui também alterações adicionais, tais como correções de erros. Para obter mais informações, consulte [resumo das alterações no ramo atual do System Center Configuration Manager, versão 1802](https://support.microsoft.com/help/4101375).

<!--
The following additional updates to this release are also now available:
- [Update rollup for System Center Configuration Manager current branch, version 1710](https://support.microsoft.com/help/4057517)
-->

> [!TIP]  
> Para instalar um novo site, tem de utilizar uma versão de linha de base do Configuration Manager.  
>
>  Saiba mais sobre:    
>   - [Instalar novos sites](/sccm/core/servers/deploy/install/installing-sites)  
>   - [Instalar atualizações em sites](/sccm/core/servers/manage/updates)  
>   - [Versões de linha de base e atualização](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

As secções seguintes fornecem detalhes sobre as alterações e novas capacidades do versão 1802 do Configuration Manager.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).

Version 1802 drops support for the following products:
-->


## <a name="site-infrastructure"></a>Infraestrutura de sites

### <a name="reassign-distribution-point"></a>Reatribuir o ponto de distribuição
<!-- 1306937 -->
Muitos clientes têm infraestruturas de grandes dimensões do Configuration Manager e reduzindo a sites primários ou secundários para simplificar o respetivo ambiente. Tem de manter pontos de distribuição em localizações de sucursais para servir conteúdo para clientes geridos. Estes pontos de distribuição, muitas vezes, contenham vários terabytes ou mais dos conteúdos. Este conteúdo é dispendioso em termos de largura de banda de hora e a rede para distribuir a estes servidores remotos. Esta funcionalidade permite-lhe reatribuir um ponto de distribuição para outro site primário sem redistribuir o conteúdo. Esta ação atualiza a atribuição de sistema de site enquanto a persistência de todo o conteúdo no servidor. Para obter mais informações, consulte [reatribuir um ponto de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_reassign).

### <a name="configure-windows-delivery-optimization-to-use-configuration-manager-boundary-groups"></a>Configurar a otimização de entrega do Windows para utilizar grupos de limites do Configuration Manager
<!-- 1324696 -->
Utilize grupos de limites do Configuration Manager para definir e regular a distribuição de conteúdo através da rede empresarial em escritórios remotos. [Otimização de entrega de Windows](/windows/deployment/update/waas-delivery-optimization) é uma tecnologia de baseado na nuvem, ponto a ponto para partilhar conteúdo entre dispositivos Windows 10. A partir desta versão, configure a otimização de entrega a utilizar os grupos de limites, quando a partilha de conteúdo entre elementos. Uma nova definição de cliente aplica-se o identificador do grupo de limites como o identificador do grupo de otimização de entrega no cliente. Quando o cliente comunica com o serviço de nuvem de otimização de entrega, utiliza este identificador para localizar os elementos de rede com os conteúdos pretendidos. Para obter mais informações, consulte [conceitos fundamentais da gestão de conteúdos](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#delivery-optimization).

### <a name="support-for-windows-10-arm64-devices"></a>Suporte para dispositivos Windows 10 ARM64
<!-- 1353704 -->
A partir desta versão que cliente do Configuration Manager é suportado em dispositivos Windows 10 ARM64. As funcionalidades de gestão existentes do cliente deverá trabalhar com estes novos dispositivos. Por exemplo, hardware e inventário de software, atualizações de software e gestão de aplicações. Implementação do sistema operativo não é atualmente suportada. 

### <a name="improved-support-for-cng-certificates"></a>Suporte melhorado para certificados CNG
<!-- 1357314 -->
Suporta a versão do Configuration Manager (ramo atual) 1710 [criptografia: Certificados do próximos geração (CNG)](/sccm/core/plan-design/network/cng-certificates-overview). Suportam 1710 limites de versão para certificados de cliente em vários cenários. 

A partir desta versão, utilize certificados CNG para as seguintes funções de servidor ativado para HTTPS:
- Ponto de gestão
- Ponto de distribuição
- Ponto de atualização de software
- Ponto de Migração de Estado  


### <a name="boundary-group-fallback-for-management-points"></a>Grupo de limites contingência para pontos de gestão
<!-- 1324594 -->
Configurar as relações de contingência para pontos de gestão entre [grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups). Este comportamento proporciona maior controlo para os pontos de gestão que os clientes utilizam. Para obter mais informações, consulte [configurar grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups#management-points).


### <a name="cloud-distribution-point-site-affinity"></a>Afinidade de site do ponto de distribuição de nuvem
<!--503719-->
Esta funcionalidade beneficia os clientes com uma hierarquia de vários site, geograficamente com pontos de distribuição de nuvem. Quando um cliente baseado na internet procura de conteúdo, anteriormente não ocorreu nenhuma ordem à lista de pontos de distribuição de nuvem recebida pelo cliente. Este comportamento pode resultar em clientes baseados na internet receber conteúdos dos pontos de distribuição de nuvem, geograficamente distante. Transferir o conteúdo de um servidor distantes tal é, normalmente, mais lenta do que um servidor mais próximo dos.
 
Com a afinidade de sites de ponto de distribuição de nuvem, um cliente baseado na internet recebe uma lista ordenada. Esta lista dá prioridade aos pontos de distribuição em nuvem do site atribuído do cliente. Este comportamento permite ao administrador preservar a sua intenção de design para transferências de conteúdo a partir dos recursos de site.
 

## <a name="management-insights"></a>Informações de gestão
<!-- 1353967 -->
Informações de gestão no System Center Configuration Manager fornecem informações sobre o estado atual do seu ambiente. As informações é com base na análise de dados a partir da base de dados do site. Insights ajudam-para melhor compreender o seu ambiente e atue com base nas informações. Para obter detalhes, veja [Insights de gestão](/sccm/core/servers/manage/management-insights)

No Configuration Manager 1802, estão disponíveis as seguintes informações:
- Aplicações:
    - Aplicações sem implementações
- Serviços de cloud: <!--1356412-->
    - Avaliar a preparação de gestão conjunta 
    - Ativar os dispositivos para ser híbrida associados ao Azure Active Directory
    - Modernize a infraestrutura de identidade e acesso
    -  Atualizar os clientes para o Windows 10, versão 1709 ou superior 
- Coleções:
    - Coleções vazias
- Gestão simplificada:  <!--1355148-->
    - Versões de cliente Desatualizadas  
- Centro de Software: 
    - Utilizadores diretos ao centro de Software em vez do catálogo de aplicações  
    - Utilize a versão nova do Centro de Software 
- Windows 10: <!--1357421-->
    - Configurar a telemetria do Windows e a chave de ID comercial 
    - Ligar a preparação para a atualização do Configuration Manager 
   
<!-- ## Migration  -->



## <a name="client-management"></a>Gestão de clientes

### <a name="cloud-management-gateway-support-for-azure-resource-manager"></a>Suporte de gateway de gestão de nuvem do Azure Resource Manager
<!-- 1324735 -->
Quando criar uma instância do [gateway de gestão de nuvem](/sccm/core/clients/manage/plan-cloud-management-gateway) (CMG), o assistente fornece agora a opção para criar um **implementação Azure Resource Manager**. [O Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) é uma plataforma moderna para gerir todos os recursos de solução como uma única entidade, chamada um [grupo de recursos](/azure/azure-resource-manager/resource-group-overview#resource-groups). Quando implementar CMG com o Azure Resource Manager, o site utiliza o Azure Active Directory (Azure AD) para autenticar e criar os recursos de nuvem necessário. Esta implementação modernized não requer o certificado de gestão do Azure clássico. Para obter mais informações, consulte [design de topologia CMG](/sccm/core/clients/manage/plan-cloud-management-gateway#azure-resource-manager).

> [!IMPORTANT]
> Esta capacidade não ative o suporte para fornecedores de serviços de nuvem do Azure (CSP). A implementação de CMG com o Azure Resource Manager continua a utilizar o serviço de nuvem clássico, que não suporta o CSP. Para obter mais informações, consulte [serviços do Azure disponíveis no Azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services).  

### <a name="improvements-to-cloud-management-gateway"></a>Melhoramentos ao gateway de gestão de nuvem  

- A partir desta versão, o **gateway de gestão de nuvem** já não é uma funcionalidade de pré-lançamento.  

- A documentação de funcionalidade é revista e avançada. Para obter mais informações, consulte os artigos seguintes:
    - [Planear para o gateway de gestão de nuvem](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)
    - [Tamanho da gestão do gateway de nuvem e números de escala](/sccm/core/plan-design/configs/size-and-scale-numbers#bkmk_cmg)
    - [Segurança e privacidade para o gateway de gestão na cloud ](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)
    - [Perguntas mais frequentes sobre o gateway de gestão de nuvem](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)
    - [Certificados para o gateway de gestão na cloud](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)
    - [Configurar o gateway de gestão na cloud](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)  


### <a name="configure-hardware-inventory-to-collect-strings-larger-than-255-characters"></a>Configurar o inventário de hardware para recolher cadeias maiores do que 255 carateres
<!-- 1357389 -->
Pode configurar o comprimento das cadeias de ser maior que 255 carateres para propriedades de inventário de hardware. Esta alteração aplica-se apenas às classes adicionadas recentemente e as propriedades de inventário de hardware que não existem chaves. Para obter mais informações, consulte o [inventário de hardware expanda](/sccm/core/clients/manage/inventory/extend-hardware-inventory#BKMK_GreaterThan255) artigo. 

 ### <a name="deprecation-announcement-for-linux-and-unix-client-support"></a>Anúncio de depreciação de suporte de clientes Linux e Unix
 <!--510139-->
Microsoft pretende despromover aproximadamente de um ano a partir de agora o suporte de clientes Linux e UNIX no System Center Configuration Manager, como é que os clientes não serão incluídos em 1902 o SCCM versão calendário antecipado 2019.  A versão do Configuration Manager 1810, num calendário de enlace tardio 2018, estará a última versão para incluir os clientes Linux e UNIX e serão suportados para o ciclo de vida completo de 1810 do Gestor de configuração.  Depois de 1810 do Gestor de configuração, os clientes devem considerar Operations Management Suite do Microsoft para gerir servidores Linux.  OMS tem um vasto conjunto Linux que suportam que, na maioria dos casos, excedem a funcionalidade do Configuration Manager, incluindo gestão de patch de ponto a ponto para Linux.

### <a name="surface-device-dashboard"></a>Dashboard de dispositivo superfície
<!--1355788-->
O dashboard de dispositivo superfície fornece informações sobre os dispositivos superfície encontrado no seu ambiente. Na consola, aceda a **monitorização** > **dispositivos Surface**. Pode ver os itens:
- percentagem de analisa
- percentagem dos modelos superfície
- Principais cinco versões de firmware

Para obter mais informações, consulte o [dashboard superfície](/sccm/core/clients/manage/surface-device-dashboard) artigo.

### <a name="change-in-the-configuration-manager-client-install"></a>Instalar a alteração no cliente do Configuration Manager
<!--1356195-->
A partir desta versão, Silverlight está já não está instalado nos dispositivos cliente automaticamente. Para obter mais informações, consulte [pré-requisitos para implementar clientes em computadores Windows](/sccm/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers#bkmk_ExternalDependencies)

## <a name="co-management"></a>Gestão conjunta

### <a name="transition-endpoint-protection-workload-to-intune-using-co-management"></a>Carga de trabalho de proteção de ponto final de transição para o Intune utilizando a gestão de conjunta
<!-- 1357365 -->
 A carga de trabalho do Endpoint Protection pode ser transitada para o Intune depois de ativar a gestão conjunta. A transição a carga de trabalho do Endpoint Protection, vá para a página de propriedades de gestão conjunta e desloque o cursor de controlo do Configuration Manager para **piloto** ou **todos os**. Para obter detalhes sobre as cargas de trabalho, consulte [cargas de trabalho podem ser transitado para o Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune). Para obter mais informações sobre a gestão de conjunta, consulte [conjunta management para Windows 10 dispositivos](/sccm/core/clients/manage/co-management-overview).
 
### <a name="co-management-dashboard-in-system-center-configuration-manager"></a>Dashboard de gestão conjunta no System Center Configuration Manager
<!--1356648-->
A partir desta versão, pode ver um dashboard com informações sobre a gestão conjunta. O dashboard ajuda a rever máquinas que estejam conjuntamente geridas no seu ambiente. Os gráficos podem ajudar a identificar dispositivos que necessitem de atenção. Para obter mais informações, consulte o [dashboard de gestão conjunta](\sccm\core\clients\manage\client-management-dashboard) artigo. 


## <a name="compliance-settings"></a>Definições de compatibilidade

### <a name="microsoft-edge-browser-policies"></a>Políticas de browser Microsoft Edge
<!-- 1357310 -->
Para os clientes que utilizam o [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) web browser em clientes Windows 10, crie uma política de definições de compatibilidade do Configuration Manager para configurar várias definições do Microsoft Edge. Para obter mais informações, consulte [perfil de browser Microsoft Edge criar](/sccm/compliance/deploy-use/browser-profiles). 



## <a name="application-management"></a>Gestão de Aplicações

### <a name="allow-user-interaction-when-installing-an-application"></a>Permitir interação do utilizador quando instalar uma aplicação
<!-- 1356976 -->
Permitir que um utilizador final interagir com a instalação de uma aplicação durante a execução da sequência de tarefas. Por exemplo, execute um processo de configuração que pede ao utilizador final para várias opções. Alguns programas de instalação da aplicação não é possível silence avisos do utilizador ou o processo de instalação pode necessitar de valores de configuração específicas conhecidos apenas ao utilizador. Esta funcionalidade permite-lhe lidar com estes cenários de instalação. Para obter mais informações, consulte [especificar opções de experiência de utilizador para o tipo de implementação](/sccm/apps/deploy-use/create-applications#specify-user-experience-options-for-the-deployment-type).

### <a name="do-not-automatically-upgrade-superseded-applications"></a>Não atualizar automaticamente as aplicações substituídas
<!-- 1351266 -->
Configure uma implementação de aplicações para atualizar automaticamente qualquer versão de substituição. Agora ao criar a implementação no **definições de implementação** página do **Assistente de implementação de Software**, para um **disponível** ou **necessário**instalar fim, pode ativar ou desativar a opção para **atualizar automaticamente qualquer substituídas versões desta aplicação**. Para obter mais informações, consulte [especificar definições de implementação](/sccm/apps/deploy-use/deploy-applications#specify-deployment-settings).

### <a name="approve-application-requests-for-users-per-device"></a>Aprovar pedidos de aplicações para os utilizadores por dispositivo
<!-- 1357015 -->
A partir desta versão, quando um utilizador solicita uma aplicação que necessita de aprovação, o nome de dispositivo específico faz agora parte do pedido. Se o administrador aprova o pedido, o utilizador só é possível instalar a aplicação nesse dispositivo. O utilizador tem de submeter outro pedido para instalar a aplicação noutro dispositivo. Para obter mais informações, consulte [especificar definições de implementação](/sccm/apps/deploy-use/deploy-applications#specify-deployment-settings).

 > [!Note]  
 > Esta é uma funcionalidade opcional. Para obter mais informações, consulte [ativar funcionalidades opcionais de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  


### <a name="run-scripts-improvements"></a>Execute os melhoramentos de scripts 
<!-- 1236459 -->
 A partir desta versão, **executar Scripts** já não é uma funcionalidade de pré-lançamento. O resultado do script devolve agora com a formatação JSON. Para obter mais informações, consulte [criar e executadas scripts do PowerShell da consola do Configuration Manager](/sccm/apps/deploy-use/create-deploy-scripts).


## <a name="operating-system-deployment"></a>Implementação do sistema operativo

### <a name="windows-10-in-place-upgrade-task-sequence-via-cloud-management-gateway"></a>Sequência de tarefas de atualização no local do Windows 10 através do gateway de gestão de nuvem
<!-- 1357149 -->
O Windows 10 [sequência de tarefas de atualização no local](/sccm/osd/deploy-use/upgrade-windows-to-the-latest-version) suporta agora a implementação de clientes baseados na internet geridos através de [gateway de gestão de nuvem](/sccm/core/clients/manage/plan-cloud-management-gateway). Esta capacidade permite aos utilizadores remotos mais facilmente atualizar para o Windows 10, sem necessitar de ligar à rede empresarial. Para obter mais informações, veja [Implementar uma sequência de tarefas](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#deploy-windows-10-in-place-upgrade-via-cmg).

### <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Melhoramentos à sequência de tarefas de atualização no local do Windows 10
<!-- 1357425 -->
O modelo de sequência de tarefas predefinido para a atualização no local do Windows 10 inclui agora grupos adicionais com as ações recomendadas para adicionar antes e depois do processo de atualização. Estas ações são comuns entre muitos clientes que com êxito estiver a atualizar dispositivos para Windows 10. Para obter mais informações, consulte [criar uma sequência de tarefas para atualizar o sistema operativo](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#recommended-task-sequence-steps-to-prepare-for-upgrade).

### <a name="improvements-to-operating-system-deployment"></a>Melhorias para implementação do sistema operativo
Esta versão inclui as seguintes melhorias para implementação do sistema operativo:
 - No Windows PE, quando iniciar cmtrace.exe, já não for pedido para escolher se pretende que este programa o Visualizador de predefinidos para ficheiros de registo. <!-- SMS 500897 -->
 - Adicionar imagens de arranque para o [transferir conteúdo do pacote](/sccm/osd/understand/task-sequence-steps#BKMK_DownloadPackageContent) passo de sequência de tarefas.
 - Melhoramentos para o [executar a sequência de tarefas](/sccm/osd/understand/task-sequence-steps#child-task-sequence) passo: <!-- 1261338 -->   
     - Suporte para todos os cenários de implementação de sistema operativo no Centro de Software, PXE e suporte de dados.
     - Melhorias na consola ações como copiar, importar, exportar e aviso durante a eliminação de objetos.
     - Suporte para o [criar pré-configurado ficheiro de conteúdo](/sccm/core/plan-design/hierarchy/manage-network-bandwidth#BKMK_PrestagingContent) assistente.
     - Integração com verificação de implementação. Para obter mais informações, consulte [implementações de sequência de tarefas de alto risco](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS). 
     - O passo de sequência de tarefas executar pode agora ser utilizado em vários níveis de sequências de tarefas, não apenas uma relação de único principal-subordinado. Relações de múltiplos níveis aumente a complexidade, por isso, utilize com cuidado. Estas relações ainda são verificados relativamente à referências circulares.
    
### <a name="deployment-templates-for-task-sequences"></a>Modelos de implementação para sequências de tarefas
<!-- 1357391 -->
O [Assistente de implementação para sequências de tarefas](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS) agora pode criar um modelo de implementação. O modelo de implementação pode ser guardado e aplicado a uma sequência de tarefas existente ou novo para criar uma implementação. 

### <a name="phased-deployments-for-task-sequences"></a>Faseada implementações de sequências de tarefas
<!--1356837-->
 Implementações faseadas é um [funcionalidade de pré-lançamento](/sccm/core/servers/manage/pre-release-features). Implementações faseadas automatizam uma coordenada, sequenciada implementação da sequência de tarefas em várias coleções. Pode [criar implementações faseadas](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence) com a predefinição de duas fases, ou configurar manualmente várias fases. Implementação faseada de sequências de tarefas não suporta a instalação de PXE ou suportes de dados.




## <a name="software-center"></a>Centro de software

### <a name="install-multiple-applications-in-software-center"></a>Instalar várias aplicações no Centro de Software
<!-- 1357126 -->
Se um utilizador final ou o técnico de ambiente de trabalho tem de instalar várias aplicações num dispositivo, o Centro de Software suporta agora a instalar várias aplicações selecionadas. Este comportamento permite ao utilizador ser mais eficiente ao não espera uma instalação concluir antes de iniciar a próxima. Para obter mais informações, consulte [instalar várias aplicações](/sccm/core/understand/software-center#install-multiple-applications) no guia de utilizador do Centro de Software novo.

### <a name="use-software-center-to-browse-and-install-user-available-applications-on-azure-ad-joined-devices"></a>Utilizar o Centro de Software para procurar e instalar aplicações disponíveis ao utilizador no Azure AD-dispositivos associados a um
<!-- 1322613 -->
Se implementar aplicações como disponíveis para os utilizadores, pode agora navegar e instalá-los através do Centro de Software nos dispositivos do Azure Active Directory (Azure AD). Para obter mais informações, consulte [implementar aplicações disponíveis ao utilizador no Azure AD-dispositivos associados a um](/sccm/apps/deploy-use/deploy-applications#deploy-user-available-applications-on-azure-ad-joined-devices).

### <a name="hide-installed-applications-in-software-center"></a>Ocultar as aplicações instaladas no Centro de Software
<!--1357592-->
Agora podem ser ocultadas aplicações instaladas no Centro de Software. As aplicações que já se encontram instaladas deixarão de aparecer no separador de aplicações quando esta opção está ativada nas definições de cliente. Esta opção estiver definida como predefinição, ao instalar ou atualizar para o Configuration Manager 1802.  As aplicações instaladas ainda estão disponíveis para revisão no separador de estado de instalação. [Aplicações de ocultar instalada no Centro de Software](/sccm/core/clients/deploy/about-client-settings#BKMK_HideInstalled) tem detalhes adicionais.   

### <a name="hide-unapproved-applications-in-software-center"></a>Ocultar aplicações não aprovadas no Centro de Software
 <!--1355146-->
Quando esta opção de definição de cliente estiver ativada, as aplicações disponíveis de utilizador que necessitem de aprovação estão ocultas no Centro de Software.  [Ocultar aplicações não aprovadas no Centro de Software](/sccm/core/clients/deploy/about-client-settings#BKMK_HideUnapproved) tem detalhes adicionais.  

### <a name="software-center-shows-user-additional-compliance-information"></a>Centro de software mostra informação de compatibilidade adicional do utilizador
<!-- 1235616 -->
 Ao utilizar o estado do atestado de estado de funcionamento do dispositivo como uma regra de política de conformidade de acesso condicional aos recursos da empresa, o Centro de Software mostra agora o utilizador a definição de atestado de estado de funcionamento de dispositivos que não está em conformidade.


 ## <a name="software-updates"></a>Atualizações de software 

### <a name="schedule-automatic-deployment-rule-evaluation-to-be-offset-from-a-base-day"></a>Agendar avaliação da regra de implementação automática para o deslocamento de um dia base. 
<!--1357133-->
Regras de implementação automática podem ser agendadas para avaliar o desvio de um dia base. Ou seja, se patch Terça-feira, na verdade, em que recai o quarta-feira por si, pode ser definido o agendamento de avaliação para a segunda Terça-feira da desvio mês por um dia. Para obter mais informações, consulte [implementar automaticamente atualizações de software](/sccm/sum/deploy-use/automatically-deploy-software-updates#BKMK_CreateAutomaticDeploymentRule). 



## <a name="reporting"></a>Relatórios

### <a name="report-for-default-browser-counts"></a>Relatório de contagens de browser predefinido
<!-- 1357830 -->
Agora é um relatório novo para mostrar a contagem de clientes com um browser específico, como a predefinição do Windows. Consulte o **contagens de Browser predefinido** comunicar no **Software - empresas e produtos** grupo de relatórios. Para obter mais informações, consulte o [lista de relatórios](/sccm/core/servers/manage/list-of-reports#software---companies-and-products).

### <a name="report-on-windows-autopilot-device-information"></a>Relatório sobre as informações do dispositivo Windows AutoPilot
<!-- 1351442 -->
Windows AutoPilot é uma solução de integração e a configuração de novos dispositivos Windows 10 de forma moderna. Para obter mais informações, consulte um [descrição geral do Windows AutoPilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-10-autopilot). É um método de registo de dispositivos existentes com Windows AutoPilot carregar as informações do dispositivo para a Microsoft Store para empresas e Education. Estas informações incluem o número de série do dispositivo, identificador de produto do Windows e um identificador de hardware. Utilize o Gestor de configuração para recolher e comunicar estas informações de dispositivo com o novo relatório, **informações de dispositivo do Windows AutoPilot**, no **Hardware - geral** o nó de relatórios. Para obter mais informações, consulte [dispositivos Windows 10 novo](/sccm/core/clients/manage/co-management-prepare#new-windows-10-devices) na preparação para gestão conjunta.

### <a name="report-on-windows-10-servicing-details-for-a-specific-collection"></a>Relatório sobre os detalhes de manutenção do Windows 10 para uma coleção específica
<!--1357653-->
O **detalhes de manutenção do Windows 10 para uma coleção específica** relatório mostra informações gerais sobre a manutenção do Windows 10 para uma coleção específica. Este relatório mostra o ID de recurso, nome NetBIOS, nome do SO, nome da versão de SO, compilação, SO ramo e estado para dispositivos Windows 10 de manutenção. Para obter mais informações, consulte o [lista de relatórios](/sccm/core/servers/manage/list-of-reports#operating-system)



<!-- ## Inventory  -->



<!-- ## Mobile device management -->



 ## <a name="protect-devices"></a>Proteger dispositivos

### <a name="improvements-to-configuration-manager-policies-for-windows-defender-exploit-guard"></a>Melhoramentos às políticas do Configuration Manager para o Windows Defender exploram proteção
<!-- 1356220 -->
Definições de política adicionais para o [redução da superfície de ataque](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy#BKMK_ASR) e [pasta acesso controlado](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy#BKMK_CFA) foram adicionados os componentes do Configuration Manager para [Windows Defender exploram proteção ](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-exploit-guard/windows-defender-exploit-guard).

### <a name="new-host-interaction-settings-for-windows-defender-application-guard"></a>Novas definições de interação de anfitrião para proteção de aplicações do Windows Defender
<!-- 1356256 -->
Para Windows 10 versão 1709 e dispositivos posteriores, existem duas novas anfitrião interação definições para [Guard de aplicação do Windows Defender](/sccm/protect/deploy-use/create-deploy-application-guard-policy#BKMK_HIS): 
- Web sites podem ser dado acesso ao processador de gráficos virtuais do anfitrião. 
- Podem ser persistente ficheiros transferidos no interior do contentor no anfitrião. 




## <a name="configuration-manager-console"></a>Consola do Configuration Manager

### <a name="improvements-to-the-configuration-manager-console"></a>Melhorias à consola do Configuration Manager 
Esta versão inclui as seguintes melhorias à consola do Configuration Manager.
- Apresenta uma lista de dispositivos em ativos e compatibilidade, dispositivos, agora apresenta o utilizador primário por predefinição. Esta coluna apresenta apenas o nó de dispositivos. Também pode ser adicionado o último utilizador com sessão iniciado como uma coluna opcional.<!-- 1357280 --> Ativar [afinidade dispositivo / utilizador](/sccm/core/clients/deploy/about-client-settings#user-and-device-affinity) definições de cliente para o site para associar um utilizador principal de um dispositivo.
- Se uma coleção é um membro de outra coleção e nome é alterado, o novo nome é atualizado nas regras de associação.<!--1357282--> 
- Ao utilizar o controlo remoto num cliente com vários monitores em dimensionamento de DPI diferentes, o cursor do rato agora corretamente mapeia entre eles. <!--433170-->
- O [dashboard de gestão de clientes do Office 365](/sccm/sum/deploy-use/manage-office-365-proplus-updates#office-365-client-management-dashboard) apresenta uma lista de dispositivos relevantes quando estão selecionadas secções de gráfico. <!--1357281 --> 



## <a name="next-steps"></a>Passos Seguintes
Quando estiver pronto para instalar esta versão, consulte [atualizações do Configuration Manager](/sccm/core/servers/manage/updates).
