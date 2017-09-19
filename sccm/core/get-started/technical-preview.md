---
title: "Pré-visualização técnica para o Configuration Manager | Microsoft Docs"
description: "Saiba mais sobre a versão de pré-visualização técnica que permite-lhe test-drive novas funcionalidades e capacidades no System Center Configuration Manager."
ms.custom: na
ms.date: 08/25/2017
ms.prod: configuration-manager
ms.reviewer: nab
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
caps.latest.revision: "157"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: e471e11b3c61172b4e9fcae74944d39aa0ab702f
ms.sourcegitcommit: 31c670a4bce74fd64a7d46ebf7702f65b80d4147
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/13/2017
---
# <a name="technical-preview-for-system-center-configuration-manager"></a>Technical Preview do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (Technical Preview)*

**Bem-vindo ao do System Center Configuration Manager Technical Preview**. Este tópico fornece detalhes sobre a versão de pré-visualização em desenvolvimento, que apresenta novas funcionalidades e capacidades nas quais estamos a trabalhar. Com cada versão do technical preview, foram introduzidas novas funcionalidades que não estejam incluídas no ramo atual do System Center Configuration Manager no momento que da versão de pré-visualização técnica é disponibilizada. Estas funcionalidades poderão eventualmente ser incluídas numa atualização à versão do ramo atual, mas antes de finalizarmos as funcionalidades e de as adicionarmos, queremos que tenha a oportunidade de experimentá-las e de nos enviar os seus comentários.  

 Como se trata de uma versão de pré-visualização técnica, os detalhes e a funcionalidade estão sujeitos a alterações.  

 Este tópico contém informações que se aplica a todas as versões do Technical Preview e também apresenta uma lista de cada nova capacidade (ou funcionalidade), juntamente com a versão de pré-visualização técnica em que a capacidade aparece pela primeira vez, como a versão 1701 de Janeiro de 2017. Os detalhes destas capacidades estão descritos em tópicos separados dedicados a cada versão de pré-visualização.  

 Para obter informações sobre quais são as novidades no ramo atual do Configuration Manager, consulte [que há de novo no System Center Configuration Manager](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012).



##  <a name="bkmk_reqs"></a> Requisitos e limitações do Technical Preview  

> [!IMPORTANT]     
>  A Technical Preview está licenciada para ser utilizada apenas num ambiente de laboratório.  A Microsoft poderá não fornecer serviços de suporte e determinadas funcionalidades poderão não estar disponíveis no software da Preview. Além disso, o software da Preview poderá ter um nível reduzido ou diferente de padrões de segurança, privacidade, acessibilidade, disponibilidade e fiabilidade em relação ao software disponibilizado comercialmente.  

 Para a maioria dos pré-requisitos de produto, utilize as informações de [configurações suportadas para o System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md). As seguintes exceções são aplicáveis apenas às versões do Technical Preview:  

-   Cada instalação permanece ativa durante 90 dias até se tornar inativa.  

-   O inglês é o único idioma suportado.


-   Apenas os seguintes sinalizadores de instalação (comutadores) são suportados:  

    -   **/silent**  
    -   **/testdbupgrade**    


-   Por predefinição, quando utiliza o technical preview, o ponto de ligação de serviço está definido para o modo online quando é instalada e não suporta uma alteração para o modo offline.

-   Quando aplicável, são incluídos requisitos ou limitações adicionais com detalhes para cada versão específica do Technical Preview  

-   Não existe suporte para migração para ou a partir desta versão de pré-visualização.  

-   Não existe suporte para atualizar para esta versão de pré-visualização.  

-   Não existe suporte para atualizar para uma compilação de produção (ramo atual) a partir desta preview build. No entanto, quando as atualizações estiverem disponíveis para uma versão de pré-visualização, pode encontrar e instalá-los a partir de **atualizações e manutenção** nós da consola do Configuration Manager. Para ver um vídeo do processo de atualização na consola, veja [Installing ConfigMgr Update Packages](https://www.youtube.com/embed/KBd_EGFbUT8) (Instalar Pacotes de Atualização do ConfigMgr) em youtube.com.  
-   Apenas é suportado um site primário autónomo. Não existe suporte para um site de administração central, múltiplos sites primários ou sites secundários.  

Os produtos e tecnologias que se seguem são suportadas por este ramo do Configuration Manager. No entanto, a sua inclusão neste conteúdo não implica uma extensão de suporte para um produto ou a versão que está fora individual do produto vida de suporte. Os produtos que estejam fora do respetivo ciclo de vida de suporte não são suportados para utilização com o Configuration Manager. Para mais informações sobre os Ciclos de Vida do Suporte da Microsoft, aceda ao site [Ciclo de Vida do Suporte da Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=208270) .  

-   Apenas são suportadas as seguintes versões do SQL Server:  

    -   SQL Server 2016 (sem Service Pack e posterior)
    -   SQL Server 2014 (com Service Pack 1 e posterior)
    -   SQL Server 2012 (com Service Pack 3, ou posterior)


-   O site suporta até 10 clientes, que têm de estar a executar um dos seguintes sistemas operativos:  

      -   Windows 10  
      -   Windows 8,1  
      -   Windows 8  
      -   Windows 7  

##  <a name="bkmk_install"></a> Instalar e atualizar o Technical Preview  
 O System Center Configuration Manager Technical Preview é distinto da versão atual do System Center Configuration Manager.  

 Para utilizar a versão de pré-visualização técnica, primeiro tem de instalar uma **versão de linha de base** da compilação da versão de pré-visualização técnica. Depois de instalar uma versão de linha de base, pode então utilizar as **atualizações na consola** para atualizar a sua instalação com a versão de pré-visualização mais recente.     Normalmente, existem novas versões mensais da Technical Preview.

Cada versão de pré-visualização é suportado até três versões sucessivas estão disponíveis. Ou seja, quando versão 1708 versões, versão 1704 já não seria suporte, mas versões 1705, 1706 e 1707 permanecerá suporte. Quando uma linha de base está fora de suporte (como a versão 1703), ainda é suportada para instalar um novo site de pré-visualização técnica até que uma nova versão de linha de base está disponível, desde que, em seguida, atualizar essa instalação para uma versão suportada. Quando a atualização, se não vir a versão mais recente disponível na consola do seu, atualize para a versão mais recente oferecidos e, em seguida, repita esse processo até que pode instalar a versão mais recente do technical preview.

> [!TIP]  
>  Quando instala uma atualização da versão de pré-visualização técnica, atualiza a instalação de pré-visualização para essa nova versão de pré-visualização técnica.    Uma instalação de pré-visualização técnica nunca inclui a opção de atualizar para uma instalação do ramo atual, nem de receber atualizações da versão do ramo atual.  

**Versões de linha de base ativas da Technical Preview:**  
Pode instalar uma versão de linha de até 1 ano após a respetiva versão. No entanto, quando instala um novo site de pré-visualização técnica, recomendamos que utilize a versão de linha de base mais recente que está disponível.
-  **Technical Preview 1703** -o Configuration Manager Technical Preview 1703 está disponível como ambos os uma atualização na consola do Configuration Manager Technical Preview e como uma nova versão de linha de base é [disponível a partir do Web site do Centro de avaliação TechNet](http://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).

<!-- out of support. Use baseline 1703
-  **Technical Preview 1610** - The Configuration Manager Technical Preview 1610 was available as both an in-console update for the Configuration Manager Technical Preview, and as a baseline version. If you have media for installing 1610, we recommend you download version 1703 and install that version instead.
-->



##  <a name="BKMK_TPFeedback"></a> Fornecer comentários  
 Gostaríamos de receber o seu feedback sobre as nossas versões de pré-visualização técnica. Para submeter comentários sobre as funcionalidades de cada versão de pré-visualização, siga a hiperligação para o nosso formulário de resposta na página do [programa de comentários do Configuration Manager](https://connect.microsoft.com/ConfigurationManagervnext/Feedback) no site do Microsoft Connect.  

 Se tiver ideias sobre novas funcionalidades que gostaria de ver, estamos interessados. Para submeter novas ideias e votar nas ideias submetidas por outras pessoas, [visite a nossa página do UserVoice](http://configurationmanager.uservoice.com).  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->




##  <a name="bkmk_tpCaps"></a>Capacidades fornecidas no technical preview mais recente  
 Seguem-se as capacidades fornecidas em cada versão de pré-visualização técnica do Configuration Manager.  As capacidades que estão disponíveis a partir de uma versão da Technical Preview permanecem disponíveis em versões posteriores. Da mesma forma, as capacidades que foram adicionadas para a versão do System Center Configuration Manager (ramo atual) permanecem disponíveis nas pré-visualizações técnicas subsequentes.  Clique nas hiperligações para o conteúdo de cada versão de pré-visualização para saber mais sobre uma capacidade específica.  

 |Funcionalidade |Versão de pré-visualização técnica |Versão do ramo atual|  
 |----------------|---------------------|--------------------|
 |Melhoramentos para especificar os parâmetros do script ao implementar scripts do PowerShell do Configuration Manager<!-- 1236459 -->|[Pré-visualização do técnico 1708](capabilities-in-technical-preview-1708.md#improvements-for-specifying-script-parameters-when-you-deploy-powershell-scripts-from-configuration-manager)|![Não foi adicionada](media/Red_X.gif)|
 |Informações de gestão<!-- 1353967 --> |[Pré-visualização do técnico 1708](capabilities-in-technical-preview-1708.md#management-insights)|![Não foi adicionada](media/Red_X.gif)|
 |Reinicie os computadores a partir da consola do Configuration Manager<!-- 1356283 --> |[Pré-visualização do técnico 1708](capabilities-in-technical-preview-1708.md#restart-computers-from-the-configuration-manager-console)|![Não foi adicionada](media/Red_X.gif)|
 |Personalização de centro de software<!-- 1351224 --> |[Pré-visualização do técnico 1708](capabilities-in-technical-preview-1708.md#software-center-customization)|![Não foi adicionada](media/Red_X.gif)|


## <a name="capabilities-delivered-in-previous-technical-previews"></a>Capacidades fornecidas em pré-visualizações técnicas anteriores
 Quando todas as funcionalidades de uma versão de pré-visualização técnica estão disponíveis na versão mínima suportada do ramo atual, os detalhes para essa versão de pré-visualização são removidos da tabela seguinte.  

 |Funcionalidade |Versão de pré-visualização técnica |Versão do ramo atual|  
 |----------------|---------------------|--------------------|
 |Suporte de Cache ponto a ponto do cliente para ficheiros de instalação rápida para Windows 10 e o Office 365|[Pré-visualização do técnico 1707](capabilities-in-technical-preview-1707.md#client-peer-cache-support-for-express-installation-files-for-windows-10-and-office-365)|![Não foi adicionada](media/Red_X.gif)|
 |Dashboard de dispositivo superfície|[Pré-visualização do técnico 1707](capabilities-in-technical-preview-1707.md#surface-device-dashboard)|![Não foi adicionada](media/Red_X.gif)|
 |Configurar e implementar políticas de proteção de aplicações do Windows Defender|[Pré-visualização do técnico 1707](capabilities-in-technical-preview-1707.md#configure-and-deploy-windows-defender-application-guard-policies)|![Não foi adicionada](media/Red_X.gif)|
 |Adicionar parâmetros ao implementar scripts do PowerShell do Configuration Manager|[Pré-visualização do técnico 1707](capabilities-in-technical-preview-1707.md#add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager)|![Não foi adicionada](media/Red_X.gif)|
 |Novas definições de política de gestão de aplicações móveis|[Pré-visualização do técnico 1706](capabilities-in-technical-preview-1706.md#new-mobile-application-management-policy-settings)|![Não foi adicionada](media/Red_X.gif)|
 |Grupos de limites melhorada para pontos de atualização de software|[Pré-visualização do técnico 1706](capabilities-in-technical-preview-1706.md#improved-boundary-groups-for-software-update-points)|[Versão 1706](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points)|
 |Disponibilidade elevada de função do servidor de site|[Pré-visualização do técnico 1706](capabilities-in-technical-preview-1706.md#site-server-role-high-availability) |![Não foi adicionada](media/Red_X.gif)|
 |Incluir confiança para pastas e ficheiros específicos numa política de proteção de dispositivos|[Pré-visualização do técnico 1706](capabilities-in-technical-preview-1706.md#include-trust-for-specific-files-and-folders-in-a-device-guard-policy)|[Versão 1706](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)|
 |Ocultar o progresso da sequência de tarefas|[Pré-visualização do técnico 1706](capabilities-in-technical-preview-1706.md#hide-task-sequence-progress)|![Não foi adicionada](media/Red_X.gif)|
 |Especificar uma localização de conteúdo diferente para o conteúdo de instalação e desinstalação de conteúdo|[Pré-visualização do técnico 1706](capabilities-in-technical-preview-1706.md#specify-a-different-content-location-for-install-content-and-uninstall-content)|[Versão 1706](/sccm/core/get-started/capabilities-in-technical-preview-1706#hide-task-sequence-progress)|
 |Melhoramentos de acessibilidade |[Pré-visualização do técnico 1706](capabilities-in-technical-preview-1706.md#accessibility-improvements)|[Versão 1706](/sccm/core/understand/accessibility-features)|
 |Suporte de Assistente de serviços do Azure para a preparação da atualização |[Pré-visualização do técnico 1706](capabilities-in-technical-preview-1706.md#changes-to-the-azure-services-wizard-to-support-upgrade-readiness)|[Versão 1706](/sccm/core/servers/deploy/configure/azure-services-wizard)|
 |Novas definições de cliente para serviços em nuvem|[Pré-visualização do técnico 1706](capabilities-in-technical-preview-1706.md#new-client-settings-for-cloud-services)|[Versão 1706](/sccm/core/clients/deploy/deploy-clients-cmg-azure)|
 |Criar e executar scripts do PowerShell a partir da consola do Configuration Manager|[Pré-visualização do técnico 1706](capabilities-in-technical-preview-1706.md#create-and-run-powershell-scripts-from-the-configuration-manager-console)|[Versão 1706](/sccm/apps/deploy-use/create-deploy-scripts)|
 |Suporte de arranque de rede do PXE para IPv6 |[Pré-visualização do técnico 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|![Não foi adicionada](media/Red_X.gif)|
 |Gerir atualizações de controladores Microsoft Surface |[Pré-visualização do técnico 1706](capabilities-in-technical-preview-1706.md#manage-microsoft-surface-driver-updates)|[Versão 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706#manage-microsoft-surface-driver-updates)|
 |Configurar o Windows Update para as políticas de diferimento por de negócio |[Pré-visualização do técnico 1706](capabilities-in-technical-preview-1706.md#configure-windows-update-for-business-deferral-policies)|[Versão 1706](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10#configure-windows-update-for-business-deferral-policies)|
 |Restrições de inscrição de iOS|[Pré-visualização do técnico 1706](capabilities-in-technical-preview-1706.md#android-and-ios-enrollment-restrictions)|[Versão 1706](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac#configure-enrollment-restrictions)|
 |Restrições de inscrição de dispositivos Android|[Pré-visualização do técnico 1706](capabilities-in-technical-preview-1706.md#android-and-ios-enrollment-restrictions)|[Versão 1706](/sccm/mdm/deploy-use/enroll-hybrid-android#enable-android-enrollment)|
 |Android para a política de gestão de aplicações de trabalho para copiar-colar|[Pré-visualização do técnico 1706](capabilities-in-technical-preview-1706.md#android-for-work-application-management-policy-for-copy-paste)|[Versão 1706](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client#android-for-work-configuration-item-settings-reference)|
 |Novas definições de item de configuração do Windows|[Pré-visualização do técnico 1706](capabilities-in-technical-preview-1706.md#new-windows-configuration-item-settings)|[Versão 1706](/sccm/mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client)|
 |Novas regras de política de conformidade de dispositivo|[Pré-visualização do técnico 1706](capabilities-in-technical-preview-1706.md#new-device-compliance-policy-rules)|[Versão 1706](/sccm/mdm/deploy-use/create-compliance-policy)|
 |Avaliação de atestado de estado de funcionamento do dispositivo para as políticas de conformidade de acesso condicional|[Pré-visualização do técnico 1706](capabilities-in-technical-preview-1706.md#device-health-attestation-assessment-for-compliance-policies-for-conditional-access)|![Não foi adicionada](media/Red_X.gif)|
 |Suporte Entrust autoridades de certificação|[Pré-visualização do técnico 1706](capabilities-in-technical-preview-1706.md#support-for-entrust-certification-authorities)|[Versão 1706](/sccm/mdm/deploy-use/create-pfx-certificate-profiles)|
 |Suporte para perfis VPN macOS Cisco (IPSec)|[Pré-visualização do técnico 1706](capabilities-in-technical-preview-1706.md#cisco-ipsec-support-for-macos-vpn-profiles)|[Versão 1706](/sccm/protect/deploy-use/vpn-profiles)|
 |Novas funcionalidades para o Azure AD e gestão de nuvem|[Pré-visualização do técnico 1705](capabilities-in-technical-preview-1705.md#new-capabilities-for-azure-ad-and-cloud-management)|[Versão 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706#azure-ad-integration-with-configuration-manager)|
 |Configurar e implementar políticas de proteção de aplicações do Windows Defender|[Pré-visualização do técnico 1705](capabilities-in-technical-preview-1705.md#configure-and-deploy-windows-defender-application-guard-policies)|![Não foi adicionada](media/Red_X.gif)|
 |Ferramenta de reposição de atualização  |[Pré-visualização do técnico 1705](capabilities-in-technical-preview-1705.md#update-reset-tool)|[Versão 1706](/sccm/core/servers/manage/update-reset-tool)|
 |Suporte da consola PPP elevado  |[Pré-visualização do técnico 1705](capabilities-in-technical-preview-1705.md#high-dpi-console-support)|[Versão 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706#high-dpi-console-support)|
 |Melhorias da Cache ponto a ponto  |[Pré-visualização do técnico 1705](capabilities-in-technical-preview-1705.md#peer-cache-improvements) |[Versão 1706](/sccm/core/plan-design/hierarchy/client-peer-cache#requirements-and-considerations-for-peer-cache)|
 |Melhoramentos para o SQL Server Always On nos grupos de disponibilidade |[Pré-visualização do técnico 1705](capabilities-in-technical-preview-1705.md#improvements-for-sql-server-always-on-availability-groups) |[Versão 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706#improvements-for-sql-server-always-on-availability-groups)|
 |Melhorado notificações de utilizador para atualizações do Office 365|[Pré-visualização do técnico 1705](capabilities-in-technical-preview-1705.md#improved-user-notifications-for-office-365-updates) |[Versão 1706](/sccm/sum/deploy-use/manage-office-365-proplus-updates#restart-behavior-and-client-notifications-for-office-365-updates)|
 |Utilize o Assistente de serviços do Azure para configurar uma ligação à OMS|[Pré-visualização do técnico 1705](capabilities-in-technical-preview-1705.md#use-azure-services-wizard-to-configure-a-connection-to-oms) |[Versão 1706](/sccm/core/servers/deploy/configure/azure-services-wizard)|
 |Configurar as aplicações Android com políticas de configuração de aplicação  |[Pré-visualização do técnico 1704](capabilities-in-technical-preview-1704.md#configure-android-apps-with-app-configuration-policies)|![Não foi adicionada](media/Red_X.gif)|
 |Inventário de hardware recolhe informações de arranque seguro |[Pré-visualização do técnico 1704](capabilities-in-technical-preview-1704.md#hardware-inventory-collects-secure-boot-information)|[Versão 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706#hardware-inventory-collects-secure-boot-information)|
 |Adicionar sequências de tarefas de subordinados a uma sequência de tarefas|[Pré-visualização do técnico 1704](capabilities-in-technical-preview-1704.md#add-child-task-sequences-to-a-task-sequence)|![Não foi adicionada](media/Red_X.gif)|
 |Volte a carregar as imagens de arranque com a versão atual do Windows PE |[Pré-visualização do técnico 1704](capabilities-in-technical-preview-1704.md#reload-boot-images-with-current-windows-pe-version)|[Versão 1706](/sccm/osd/get-started/manage-boot-images#update-distribution-points-with-the-boot-image)|
 |Melhorias para implementação do sistema operativo<!-- This item does not track to be added to the Current Branch. It is covered by various other incremental work. --> |[Pré-visualização do técnico 1704](capabilities-in-technical-preview-1704.md#improvements-to-operating-system-deployment)|![Não foi adicionada](media/Red_X.gif)|
 |Implementar aplicações iOS compradas em volume para coleções de dispositivos|[Pré-visualização do técnico 1703](capabilities-in-technical-preview-1703.md#deploy-volume-purchased-ios-apps-to-device-collections)|[Versão 1702](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps)|
 |Ligações diretas para aplicações no Centro de Software|[Pré-visualização do técnico 1703](capabilities-in-technical-preview-1703.md#direct-links-to-applications-in-software-center)|[Versão 1706](/sccm/apps/deploy-use/share-applications)
 |Certificados PFX para computadores de cliente do Windows do Configuration Manager|[Pré-visualização do técnico 1703](capabilities-in-technical-preview-1703.md#pfx-certificates-for-configuration-manager-windows-client-computers)|[Versão 1706](/sccm/protect/deploy-use/create-certificate-profiles)|
 |Configurar o Assistente de serviços do Azure|[Pré-visualização do técnico 1703](capabilities-in-technical-preview-1703.md#configure-azure-services-wizard)|[Versão 1706](/sccm/core/servers/deploy/configure/azure-services-wizard)|
 |A conversão de BIOS em UEFI numa sequência de tarefas de atualização do sistema operativo| [Pré-visualização do técnico 1703](capabilities-in-technical-preview-1703.md#convert-from-bios-to-uefi-during-an-in-place-upgrade) |[Versão 1702](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade)|
 |Grupos de sequências de tarefas expansível| [Pré-visualização do técnico 1703](capabilities-in-technical-preview-1703.md#collapsible-task-sequence-groups) |[Versão 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706#collapsible-task-sequence-groups)|
 |Definições de cliente para configurar a análise do Windows para a preparação da atualização | [Pré-visualização do técnico 1703](capabilities-in-technical-preview-1703.md#client-settings-to-configure-windows-analytics-for-upgrade-readiness) |[Versão 1706](/sccm/core/clients/manage/monitor-windows-analytics#configure-clients-to-report-data-to-windows-analytics)|
 |Novas definições de conformidade para dispositivos iOS|[Pré-visualização do técnico 1702](capabilities-in-technical-preview-1702.md#new-compliance-settings-for-ios-devices)|[Versão 1702](/sccm/mdm/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client)|
 |Criar os certificados PFX com suporte de S/MIME|[Pré-visualização do técnico 1702](capabilities-in-technical-preview-1702.md#create-pfx-certificates-with-s-mime-support)|[Versão 1706](/sccm/mdm/deploy-use/create-pfx-certificate-profiles)|
 |Verifique a existência de executar ficheiros executáveis antes de instalar uma aplicação|[Pré-visualização do técnico 1702](capabilities-in-technical-preview-1702.md#check-for-running-executable-files-before-installing-an-application)|[Versão 1702](/sccm/apps/deploy-use/deploy-applications)|
 |Enviar comentários a partir da consola do Configuration Manager | [Pré-visualização do técnico 1702](capabilities-in-technical-preview-1702.md#send-feedback-from-the-configuration-manager-console)    |[Versão 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#send-feedback-from-the-configuration-managercconsole)  |
 |Alterações para atualizações e manutenção  | [Pré-visualização do técnico 1702](capabilities-in-technical-preview-1702.md#changes-for-updates-and-servicing)  |[Versão 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#changes-for-updates-and-servicing) |
 |Melhorias da Cache ponto a ponto  | [Pré-visualização do técnico 1702](capabilities-in-technical-preview-1702.md#peer-cache-improvements) |[Versão 1702](/sccm/core/plan-design/hierarchy/client-peer-cache)|
 |Utilizar o Azure Active Directory<!-- This item does not track to be added to the Current Branch. It is covered by various other incremental work. --> | [Pré-visualização do técnico 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |![Não foi adicionada](media/Red_X.gif)|
 |Melhoramentos de política de conformidade de dispositivos de acesso condicional | [Pré-visualização do técnico 1702](capabilities-in-technical-preview-1702.md#conditional-access-device-compliance-policy-improvements) |[Versão 1702](/sccm/mdm/deploy-use/create-compliance-policy)|
 |Alerta de versão de cliente Antimalware | [Pré-visualização do técnico 1702](capabilities-in-technical-preview-1702.md#antimalware-client-version-alert) |[Versão 1702](/sccm/protect/deploy-use/endpoint-configure-alerts?branch=live#alert-for-outdated-malware-client)|
 |Avaliação de compatibilidade para o Windows Update para atualizações de negócio | [Pré-visualização do técnico 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |![Não foi adicionada](media/Red_X.gif)|
 |Melhoramentos às definições do Centro de Software e mensagens de notificação para sequências de tarefas de elevado impacto|[Pré-visualização do técnico 1702](capabilities-in-technical-preview-1702.md#antimalware-client-version-alert)|[Versão 1702](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#set-a-task-sequence-as-a-high-impact-task-sequence)|
 |Android para o suporte de trabalho| [Pré-visualização do técnico 1702](capabilities-in-technical-preview-1702.md#android-for-work-support) |[Versão 1702](/sccm/mdm/deploy-use/enroll-hybrid-android#enable-android-for-work-enrollment)|
 |Melhoramentos de grupos de limites para o software de pontos de atualização | [Pré-visualização do técnico 1701](capabilities-in-technical-preview-1701.md#boundary-groups-improvements-for-software-update-points)    |[Versão 1702](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points)  |
 |Inventário de hardware recolhe informações de UEFI | [Pré-visualização do técnico 1701](capabilities-in-technical-preview-1701.md#hardware-inventory-collects-uefi-information)|[Versão 1702](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#hardware-inventory-collects-uefi-information) |
 |Melhorias para implementação do sistema operativo| [Pré-visualização do técnico 1701](capabilities-in-technical-preview-1701.md#improvements-to-operating-system-deployment)|[Versão 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#operating-system-deployment) |
 |Atualizações de software de anfitrião em pontos de distribuição baseado na nuvem| [Pré-visualização do técnico 1701](capabilities-in-technical-preview-1701.md#host-software-updates-on-cloud-based-distribution-points)|[Versão 1702](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#plan-to-use-a-cloud-based-distribution-point) |
 |Validar os dados de atestado de estado de funcionamento de dispositivos através de pontos de gestão| [Pré-visualização do técnico 1701](capabilities-in-technical-preview-1701.md#validate-device-health-attestation-data-via-management-points)| [Versão 1702](/sccm/core/servers/manage/health-attestation) |
 |Conector do OMS para a nuvem do Microsoft Azure Government |[Pré-visualização do técnico 1701](capabilities-in-technical-preview-1701.md#use-the-oms-connector-for-microsoft-azure-government-cloud) |[Versão 1702](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#fairfaxconfig) |
 |Android e iOS versões deixam de ser targetable em assistentes de criação |[Pré-visualização do técnico 1701](capabilities-in-technical-preview-1701.md#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm) |[Versão 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm) |
 |Acesso de dados de ponto final de OData |[Pré-visualização do técnico 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|![Não foi adicionada](media/Red_X.gif)|
 |Ponto de serviço do armazém de dados |[Pré-visualização do técnico 1612](capabilities-in-technical-preview-1612.md#the-data-warehouse-service-point)|[Versão 1702](/sccm/core/servers/manage/data-warehouse)|
 |Ferramenta de limpeza da biblioteca de conteúdos |[Pré-visualização do técnico 1612](capabilities-in-technical-preview-1612.md#content-library-cleanup-tool)|[Versão 1702](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool) |
 |Melhoramentos para pesquisa na consola |[Pré-visualização do técnico 1612](capabilities-in-technical-preview-1612.md#improvements-for-in-console-search)|[Versão 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#improvements-for-in-console-search)|
 |Impedir a instalação de uma aplicação, se estiver a executar um programa especificado|[Pré-visualização do técnico 1612](capabilities-in-technical-preview-1612.md#prevent-installation-of-an-application-if-a-specified-program-is-running)|[Versão 1702](/sccm/apps/deploy-use/deploy-applications)|
 |Novo do Windows Hello para notificação de negócio para os utilizadores finais|[Pré-visualização do técnico 1612](capabilities-in-technical-preview-1612.md#new-windows-hello-for-business-notification-for-end-users)|[Versão 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#new-windows-hello-for-business-notification-for-end-users)|
 |Loja Windows para o suporte de negócio no Configuration Manager|[Pré-visualização do técnico 1612](capabilities-in-technical-preview-1612.md#windows-store-for-business-support-in-configuration-manager)|[Versão 1702](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|
 |Regressar à página anterior, quando ocorre uma falha de uma sequência de tarefas|[Pré-visualização do técnico 1612](capabilities-in-technical-preview-1612.md#return-to-previous-page-when-a-task-sequence-fails)|[Versão 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#operating-system-deployment)|
 |Suporte para atualizações do Windows 10 de ficheiros de instalação rápida|[Pré-visualização do técnico 1612](capabilities-in-technical-preview-1612.md#express-installation-files-support-for-windows-10-updates)|[Versão 1702](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates)|
 |Integração do Active Directory do Azure|[Pré-visualização do técnico 1612](capabilities-in-technical-preview-1612.md#azure-active-directory-onboarding)|[Versão 1706](/sccm/core/servers/deploy/configure/azure-services-wizard)|
 |Alterar para configurar a autenticação multifator para inscrição de dispositivos|[Pré-visualização do técnico 1612](capabilities-in-technical-preview-1612.md#change-to-configuring-multi-factor-authentication-for-device-enrollment)|![Não foi adicionada](media/Red_X.gif)|
 |Pré-armazenar conteúdo em cache para implementações e sequências de tarefas |[Pré-visualização do técnico 1611](capabilities-in-technical-preview-1611.md#pre-cache-content-for-available-deployments-and-task-sequences)|[Versão 1702](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content)|
 |Definições de configuração do Windows Defender|[Pré-visualização do técnico 1610](capabilities-in-technical-preview-1610.md#windows-defender-configuration-settings)|[Versão 1610](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client)|
 |Política de pedido de sincronização da consola do administrador|[Pré-visualização do técnico 1610](capabilities-in-technical-preview-1610.md#request-policy-sync-from-administrator-console)|[Versão 1610](/sccm/mdm/deploy-use/sync-intune-device)|
 |Suporte de função de segurança adicional para o nó de todos os dispositivos de empresa|[Pré-visualização do técnico 1610](capabilities-in-technical-preview-1610.md#additional-security-role-support)|[Versão 1610](/sccm/mdm/understand/whats-new-in-hybrid-mobile-device-management#new-hybrid-features-in-november-2016)|
 |Acesso condicional para perfis de VPN do Windows 10|[Pré-visualização do técnico 1610](capabilities-in-technical-preview-1610.md#conditional-access-for-windows-10-vpn-profiles)|[Versão 1610](/sccm/protect/deploy-use/create-vpn-profiles#configure-the-authentication-method-for-the-vpn-profile)|
 |Filtrar pelo tamanho do conteúdo nas regras de implementação automática|[Pré-visualização do técnico 1610](capabilities-in-technical-preview-1610.md#filter-by-content-size-in-automatic-deployment-rules)|[Versão 1610](/sccm/core/plan-design/changes/whats-new-in-version-1610#filter-by-content-size-in-automatic-deployment-rules) |
 |Funcionalidade melhorada para caixas de diálogo de software necessárias|[Pré-visualização do técnico 1610](capabilities-in-technical-preview-1610.md#improved-functionality-for-required-software-dialogs)|[Versão 1610](/sccm/apps/deploy-use/deploy-applications)|
 |Negar pedidos de aplicação anteriormente aprovados|[Pré-visualização do técnico 1610](capabilities-in-technical-preview-1610.md#deny-previously-approved-application-requests)|[Versão 1610](/sccm/apps/deploy-use/deploy-applications)|
 |Excluir os clientes da atualização automática|[Pré-visualização do técnico 1610](capabilities-in-technical-preview-1610.md#exclude-clients-from-automatic-upgrade)|[Versão 1610](/sccm/core/clients/manage/upgrade/exclude-clients-windows)|
 |Melhoramentos ao Endpoint Protection|[Pré-visualização do técnico 1609](capabilities-in-technical-preview-1609.md#improvements-to-endpoint-protection)|[Versão 1610](/sccm/protect/deploy-use/endpoint-antimalware-policies#cloud-protection-service)|
 |Aumento do número de dispositivos inscritos|[Pré-visualização do técnico 1609](/sccm/mdm/deploy-use/enable-platform-enrollment)|[Versão 1610](/sccm/mdm/deploy-use/enable-platform-enrollment)|
 |Definições adicionais do DEP da Apple|[Pré-visualização do técnico 1609](capabilities-in-technical-preview-1609.md#additional-apple-dep-settings)|[Versão 1610](/sccm/mdm/deploy-use/ios-device-enrollment-program-for-hybrid)|
 |Melhoramentos à loja Windows para integração de negócios com o Configuration Manager|[Pré-visualização do técnico 1609](capabilities-in-technical-preview-1609.md)|[Versão 1610](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|
 |Novas definições de conformidade para itens de configuração|[Pré-visualização do técnico 1609](capabilities-in-technical-preview-1609.md#new-compliance-settings-for-configuration-items)|[Versão 1610](/sccm/compliance/deploy-use/create-configuration-items)|
 |Integração com a análise de atualização|[Pré-visualização do técnico 1609](capabilities-in-technical-preview-1609.md#integration-with-upgrade-analytics)|[Versão 1610](/sccm/core/clients/manage/upgrade/upgrade-analytics)|
 |Perfis de VPN híbrida de tipos de ligação de nativo para Windows 10|[Pré-visualização do técnico 1609](capabilities-in-technical-preview-1609.md#native-connection-types-for-windows-10-vpn-hybrid-profiles)|![Não foi adicionada](media/Red_X.gif)|
 |Melhoramentos para os grupos de limites|[Pré-visualização do técnico 1609](capabilities-in-technical-preview-1609.md#improvements-for-boundary-groups)|[Versão 1610](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#BKMK_BoundaryGroups)|
 |Dashboard de gestão de clientes do Office 365|[Pré-visualização do técnico 1609](capabilities-in-technical-preview-1609.md#office-365-client-management-dashboard)|[Versão 1610](/sccm/sum/deploy-use/manage-office-365-proplus-updates#office-365-client-management-dashboard)|
 |Implementar aplicações do Office 365 nos clientes|[Pré-visualização do técnico 1609](capabilities-in-technical-preview-1609.md#deploy-office-365-apps-to-clients)|[Versão 1702](/sccm/sum/deploy-use/manage-office-365-proplus-updates#deploy-office-365-apps)|
 |Melhorias na BIOS para conversão de UEFI|[Pré-visualização do técnico 1609](capabilities-in-technical-preview-1609.md#BKMK_UEFIConversion)|[Versão 1610](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion)|
 |Gráficos de conformidade do Intune|[Pré-visualização do técnico 1609](capabilities-in-technical-preview-1609.md#intune-compliance-charts)|[Versão 1610](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy)|
 |Melhoramentos ao passo Preparar ConfigMgr Client para Captura de sequência de tarefas|[Pré-visualização do técnico 1608](capabilities-in-technical-preview-1608.md#improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step)|[Versão 1610](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture)|
 |Melhoramentos ao centro de Software|[Pré-visualização do técnico 1608](capabilities-in-technical-preview-1608.md#improvements-to-software-center)|[Versão 1610](/sccm/core/plan-design/changes/whats-new-in-version-1610#general-improvements-to-software-center)|
 |Melhoramentos ao Asset Intelligence<!-- Listed as TBD. No planned addition to Current Branch -->|[Pré-visualização do técnico 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|![Não foi adicionada](media/Red_X.gif)|
 |Tradução de teclado do controlo remoto|[Pré-visualização do técnico 1608](capabilities-in-technical-preview-1608.md#remote-control-keyboard-translation)| [Versão 1610](/sccm/core/clients/manage/remote-control/configuring-remote-control#enable-keyboard-translation)|
 |Melhoramentos à Política de Atualização de Edição do Windows 10|[Pré-visualização do técnico 1607](capabilities-in-technical-preview-1607.md#dmp_edition)|[Versão 1610](/sccm/compliance/deploy-use/upgrade-windows-version)|
 |Imagem Corporativa Personalizável para Caixas de Diálogo do Centro de Software|[Pré-visualização do técnico 1607](capabilities-in-technical-preview-1607.md#customizable-branding-for-software-center-dialogs)|[Versão 1610](/sccm/core/plan-design/changes/whats-new-in-version-1610#customizable-branding-for-software-center-dialogs)|  
 |Vários pontos de gestão de dispositivos para Gestão de Dispositivos Móveis no Local|[Pré-visualização do técnico 1606](capabilities-in-technical-preview-1606.md#dmp_onprem)|[Versão 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#on-premises-mobile-device-management)|
 |Categorizar automaticamente os dispositivos em coleções|[Pré-visualização do técnico 1606](capabilities-in-technical-preview-1606.md#dmp_category)|[Versão 1606](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections) |
 |Período de tolerância de imposição para implementações de atualizações de aplicações e de software|[Pré-visualização do técnico 1606](capabilities-in-technical-preview-1606.md#dmp_grace)|[Versão 1610](/sccm/apps/deploy-use/deploy-applications)|
 |Utilizar o Configuration Manager como um Instalador Gerido com Device Guard|[Pré-visualização do técnico 1606](capabilities-in-technical-preview-1606.md#dmp_devg)|[Versão 1702](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager )|
 |Gateway de gestão de nuvem (anteriormente denominado serviço de Proxy de nuvem)|[Pré-visualização do técnico 1606](capabilities-in-technical-preview-1606.md#cloud_proxy) | [Versão 1610](/sccm/core/clients/manage/plan-cloud-management-gateway)|  
 |Gerir o agente de cliente do Office 365 no Configuration Manager|[Pré-visualização do técnico 1606](capabilities-in-technical-preview-1606.md#manage_o365) |[Versão 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#software-updates)|  
 |A variável da sequência de tarefas OSDPreserveDriveLetter foi preterida|[Pré-visualização do técnico 1606](capabilities-in-technical-preview-1606.md#osdpreservedriveletter) |[Versão 1606](/sccm/osd/understand/task-sequence-built-in-variables) |
 |Alterações do Nó Atualizações e Manutenção|[Pré-visualização do técnico 1606](capabilities-in-technical-preview-1606.md#updatesandservicing)|[Versão 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#updates-and-servicing) |
 |VPN por Aplicação para dispositivos Windows 10|[Pré-visualização do técnico 1605](capabilities-in-technical-preview-1605.md#BKMK_PerAppVPN)|[Versão 1606](/sccm/protect/deploy-use/create-vpn-profiles)|  
 |Melhoramentos à sequência de tarefas Instalar atualizações de software|[Pré-visualização do técnico 1605](capabilities-in-technical-preview-1605.md#BKMK_InstallSU)|[Versão 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#operating-system-deployment)|  
 |Melhoramentos ao passo Preparar ConfigMgr Client para Captura de sequência de tarefas |[Pré-visualização do técnico 1605](capabilities-in-technical-preview-1605.md#BKMK_PrepareConfigMgrClient)|[Versão 1610](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture) |
 |Período de tolerância para implementações de aplicações necessárias |[Pré-visualização do técnico 1605](capabilities-in-technical-preview-1605.md#BKMK_Grace)|![Não foi adicionada](media/Red_X.gif)|  
 |Nova experiência para ações de dispositivos remotos |[Pré-visualização do técnico 1605](capabilities-in-technical-preview-1605.md#BKMK_Remote)|[Versão 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#device-configuration-and-protection)|  
 |Aplicações da Loja Windows para Empresas |[Pré-visualização do técnico 1605](capabilities-in-technical-preview-1605.md#BKMK_WSFB)|[Versão 1606](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|  
 |Melhoramentos gerais para aplicações compradas em volume|[Pré-visualização do técnico 1605](capabilities-in-technical-preview-1605.md#BKMK_VPP2)|[Versão 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)|  
 |Proteção de Dados Empresariais (EDP)|[Pré-visualização do técnico 1605](capabilities-in-technical-preview-1605.md#BKMK_VPP)|[Versão 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)|  
 |Os utilizadores finais podem instalar aplicações a partir do Portal da Empresa |[Pré-visualização do técnico 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|![Não foi adicionada](media/Red_X.gif)|  
 |Novos separadores para Atualizações e Sistemas Operativos no Centro de Software|[Pré-visualização do técnico 1605](capabilities-in-technical-preview-1605.md#BKMK_SW1)|[Versão 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#application-management)|  
 |Fazer manutenção a um grupo de servidores |[Pré-visualização do técnico 1605](capabilities-in-technical-preview-1605.md#BKMK_ServerGroups)|[Versão 1606](/sccm/sum/deploy-use/service-a-server-group)|   
 |Suporte do serviço Proteção Avançada Contra Ameaças do Windows Defender |[Pré-visualização do técnico 1605](capabilities-in-technical-preview-1605.md#BKMK_ATP)|[Versão 1606](/sccm/protect/deploy-use/windows-defender-advanced-threat-protection)|  
 |Novas opções de reinício para clientes do Windows 10 após a instalação de atualizações de software|[Pré-visualização do técnico 1605](capabilities-in-technical-preview-1605.md#BKMK_RestartOptions)|[Versão 1606](/sccm/sum/plan-design/plan-for-software-updates#restart-options-for-Windows-10-clients-after-software-update-installation)|  
 |Atestado de Estado de Funcionamento no Local |[Pré-visualização do técnico 1605](capabilities-in-technical-preview-1605.md#BKMK_DHA)|[Versão 1606](/sccm/core/servers/manage/health-attestation)|  
 |Pré-declarar dispositivos pertencentes à empresa com o número de série IMEI ou iOS|[Pré-visualização do técnico 1605](capabilities-in-technical-preview-1605.md#BKMK_IMEI)|[Versão 1606](/sccm/mdm/deploy-use/predeclare-devices-with-hardware-id)|  

 <!--  TP 1604 and earlier has aged out of support and all features are in Current Branch builds:
 |Manage volume-purchased apps from the Windows Store for Business| [Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_WindowsVPP)|[Version 1606](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|  
 |Improvements to Microsoft Passport for Work management|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_PFW)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#device-configuration-and-protection)|  
 |Option for clients to switch to a new software update point|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_switchsup)|[Version 1606](/sccm/sum/plan-design/plan-for-software-updates#BKMK_ManuallySwitchSUPs)|  
 |Client settings to manage Client Cache Settings and client Peer Cache |[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_peercache)|Client Settings: [Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#administration)<br/>Peer Cache: [Version 1610](/sccm/core/plan-design/hierarchy/client-peer-cache)|  
 |Support for Passport for Work as a KSP |[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_passport)|[Version 1606](/sccm/protect/deploy-use/create-certificate-profiles)|  
 |On-premises Device Health Attestation|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_onpremdha)|[Version 1606](/sccm/core/servers/manage/health-attestation)|  
 |SmartLock setting for Android devices|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_Smart)|[Version 1606](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client#android-and-samsung-knox-configuration-item-settings-reference)|  
 |Improvements to Software Center|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_SC1603)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#application-management)|  
 |Improvements to remote control|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_RC1603)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#remote-control)|  
 |Customize the RamDisk TFTP block size and window size on PXE-enabled distribution points|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_RamDiskTFTP)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#operating-system-deployment)|  
-->



## <a name="see-also"></a>Consulte Também  
[Quais são as novidades no System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
 [Introdução ao System Center Configuration Manager](../../core/understand/introduction.md)
