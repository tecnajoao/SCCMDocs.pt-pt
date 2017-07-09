---
title: "Visualização técnica do Configuration Manager | Microsoft Docs"
description: "Saiba mais sobre a versão de Technical Preview que vamos você testar novos recursos e capacidades no System Center Configuration Manager."
ms.custom: na
ms.date: 06/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
caps.latest.revision: 157
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 6f9e6e93fce95666503907010a5c253158c5de7c
ms.openlocfilehash: 736e5a04d3d5f2a3825ed4e801308fd5699ea86e
ms.contentlocale: pt-pt
ms.lasthandoff: 07/07/2017


---
# <a name="technical-preview-for-system-center-configuration-manager"></a>Technical Preview do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (Technical Preview)*

**Boas-vindas para o System Center Configuration Manager Technical Preview**. Este tópico fornece detalhes sobre a versão de pré-visualização em desenvolvimento, que apresenta novas funcionalidades e capacidades nas quais estamos a trabalhar. Com cada versão de technical preview, os novos recursos são apresentados que não estão incluídos na ramificação atual do System Center Configuration Manager no momento em que a versão technical preview é disponibilizada. Estas funcionalidades poderão eventualmente ser incluídas numa atualização à versão do ramo atual, mas antes de finalizarmos as funcionalidades e de as adicionarmos, queremos que tenha a oportunidade de experimentá-las e de nos enviar os seus comentários.  

 Como se trata de uma versão de pré-visualização técnica, os detalhes e a funcionalidade estão sujeitos a alterações.  

 Este tópico contém informações que se aplica a todas as versões do Technical Preview e também lista cada nova funcionalidade (ou recurso) junto com a versão de Technical Preview na qual o recurso aparece primeiro, como a versão 1701 para janeiro de 2017. Os detalhes destas capacidades estão descritos em tópicos separados dedicados a cada versão de pré-visualização.  

 Para obter informações sobre o que há de novo na ramificação atual do Configuration Manager, consulte [o que há de novo no System Center Configuration Manager](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012).



##  <a name="bkmk_reqs"></a> Requisitos e limitações do Technical Preview  

> [!IMPORTANT]     
>  A Technical Preview está licenciada para ser utilizada apenas num ambiente de laboratório.  A Microsoft poderá não fornecer serviços de suporte e determinadas funcionalidades poderão não estar disponíveis no software da Preview. Além disso, o software da Preview poderá ter um nível reduzido ou diferente de padrões de segurança, privacidade, acessibilidade, disponibilidade e fiabilidade em relação ao software disponibilizado comercialmente.  

 Para a maioria dos pré-requisitos do produto, use as informações de [configurações com suporte para o System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md). As seguintes exceções são aplicáveis apenas às versões do Technical Preview:  

-   Cada instalação permanece ativa durante 90 dias até se tornar inativa.  

-   O inglês é o único idioma suportado.


-   Apenas os seguintes sinalizadores de instalação (comutadores) são suportados:  

    -   **/silent**  
    -   **/testdbupgrade**    


-   Por padrão, quando você usar a technical preview, o ponto de conexão de serviço é definido para o modo online quando é instalado e não dá suporte a uma alteração para o modo offline.

-   Quando aplicável, são incluídos requisitos ou limitações adicionais com detalhes para cada versão específica do Technical Preview  

-   Não existe suporte para migração para ou a partir desta versão de pré-visualização.  

-   Não existe suporte para atualizar para esta versão de pré-visualização.  

-   Não existe suporte para atualizar para uma compilação de produção (ramo atual) a partir desta preview build. No entanto, quando as atualizações estiverem disponíveis para uma versão de visualização, você pode encontrar e instalá-los a partir de **atualizações e manutenção** nó do console do Configuration Manager. Para ver um vídeo do processo de atualização na consola, veja [Installing ConfigMgr Update Packages](https://www.youtube.com/embed/KBd_EGFbUT8) (Instalar Pacotes de Atualização do ConfigMgr) em youtube.com.  
-   Apenas é suportado um site primário autónomo. Não existe suporte para um site de administração central, múltiplos sites primários ou sites secundários.  

Os produtos e tecnologias a seguir têm suporte por esta ramificação do Configuration Manager. No entanto, sua inclusão nesse conteúdo não implica uma extensão de suporte para um produto ou a versão que está além do ciclo de vida de suporte individual do produto. Não há suporte para produtos que estão além de seu ciclo de vida de suporte para uso com o Configuration Manager. Para mais informações sobre os Ciclos de Vida do Suporte da Microsoft, aceda ao site [Ciclo de Vida do Suporte da Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=208270) .  

-   Apenas são suportadas as seguintes versões do SQL Server:  

    -   SQL Server 2016 (sem Service Pack e posterior)
    -   SQL Server 2014 (com Service Pack 1 e posterior)
    -   O SQL Server 2012 (com Service Pack 3 ou posterior)


-   O site suporta até 10 clientes, que têm de estar a executar um dos seguintes sistemas operativos:  

      -   Windows 10  
      -   Windows 8,1  
      -   Windows 8  
      -   Windows 7  

##  <a name="bkmk_install"></a> Instalar e atualizar o Technical Preview  
 O System Center Configuration Manager Technical Preview é diferente da versão atual do System Center Configuration Manager.  

 Para utilizar a versão de pré-visualização técnica, primeiro tem de instalar uma **versão de linha de base** da compilação da versão de pré-visualização técnica. Depois de instalar uma versão de linha de base, pode então utilizar as **atualizações na consola** para atualizar a sua instalação com a versão de pré-visualização mais recente.     Normalmente, existem novas versões mensais da Technical Preview.

Cada versão de visualização há suporte para até três versões sucessivas estão disponíveis. Ou seja, quando versões 1702, versão 1610 não seria mais suporte, mas versões 1611 1612 e 1701 permaneceria no suporte. Quando uma linha de base fica sem suporte (como a versão 1610), ainda há suporte para instalar um novo site de Technical Preview até que uma nova versão de linha de base está disponível, desde que você atualizar essa instalação para uma versão com suporte. Durante a atualização, se você não vir a versão mais recente disponível no console do, atualize para a versão mais recente oferecido e, em seguida, repita esse processo até que você pode instalar a versão mais atual da technical preview.

> [!TIP]  
>  Quando instala uma atualização da versão de pré-visualização técnica, atualiza a instalação de pré-visualização para essa nova versão de pré-visualização técnica.    Uma instalação de pré-visualização técnica nunca inclui a opção de atualizar para uma instalação do ramo atual, nem de receber atualizações da versão do ramo atual.  

**Versões de linha de base ativas da Technical Preview:**  
Você pode instalar uma versão de linha de base de até 1 ano após seu lançamento. No entanto, quando você instala um novo site do technical preview, é recomendável que usar a versão de linha de base mais recente disponível.
-  **1703 de visualização técnica** -o Configuration Manager Technical Preview 1703 está disponível como uma atualização no console do Configuration Manager Technical Preview e como uma nova versão de linha de base é [disponível no site do Centro de avaliação TechNet](http://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).

-  **1610 de visualização técnica** -o Configuration Manager Technical Preview 1610 estava disponível como uma atualização no console do Configuration Manager Technical Preview e como uma versão de linha de base. Se você tiver a mídia de instalação 1610, é recomendável baixar a versão 1703 e instalar a versão em vez disso.




##  <a name="BKMK_TPFeedback"></a> Fornecer comentários  
 Gostaríamos de receber o seu feedback sobre as nossas versões de pré-visualização técnica. Para submeter comentários sobre as funcionalidades de cada versão de pré-visualização, siga a hiperligação para o nosso formulário de resposta na página do [programa de comentários do Configuration Manager](https://connect.microsoft.com/ConfigurationManagervnext/Feedback) no site do Microsoft Connect.  

 Se tiver ideias sobre novas funcionalidades que gostaria de ver, estamos interessados. Para submeter novas ideias e votar nas ideias submetidas por outras pessoas, [visite a nossa página do UserVoice](http://configurationmanager.uservoice.com).  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->




##  <a name="bkmk_tpCaps"></a>Recursos fornecidos na visualização técnica mais recente  
 A seguir estão os recursos fornecidos com cada versão de visualização técnica do Configuration Manager.  As capacidades que estão disponíveis a partir de uma versão da Technical Preview permanecem disponíveis em versões posteriores. Da mesma forma, os recursos que foram adicionados à versão System Center Configuration Manager (ramificação atual) permanecem disponíveis nas visualizações técnica subsequentes.  Clique nas hiperligações para o conteúdo de cada versão de pré-visualização para saber mais sobre uma capacidade específica.  

 |Funcionalidade |Versão de visualização técnica |Versão da ramificação atual|  
 |----------------|---------------------|--------------------|
 |Novas configurações de política de gerenciamento de aplicativos móveis|[Visualização técnica 1706](capabilities-in-technical-preview-1706.md#new-mobile-application-management-policy-settings)|![Não foi adicionado](media/Red_X.gif)|
 |Grupos de limites aprimorada para pontos de atualização de software|[Visualização técnica 1706](capabilities-in-technical-preview-1706.md#improved-boundary-groups-for-software-update-points)|![Não foi adicionado](media/Red_X.gif)|
 |Disponibilidade alta da função de servidor de site|[Visualização técnica 1706](capabilities-in-technical-preview-1706.md#site-server-role-high-availability) |![Não foi adicionado](media/Red_X.gif)|
 |Incluir relação de confiança para arquivos e pastas específicos em uma política de proteção do dispositivo|[Visualização técnica 1706](capabilities-in-technical-preview-1706.md#include-trust-for-specific-files-and-folders-in-a-device-guard-policy)|![Não foi adicionado](media/Red_X.gif)|
 |Ocultar o andamento da sequência de tarefas|[Visualização técnica 1706](capabilities-in-technical-preview-1706.md#hide-task-sequence-progress)|![Não foi adicionado](media/Red_X.gif)|
 |Especificar um local de conteúdo diferente para o conteúdo de instalar e desinstalar o conteúdo|[Visualização técnica 1706](capabilities-in-technical-preview-1706.md#specify-a-different-content-location-for-install-content-and-uninstall-content)|![Não foi adicionado](media/Red_X.gif)|
 |Aprimoramentos de acessibilidade |[Visualização técnica 1706](capabilities-in-technical-preview-1706.md#accessibility-improvements)|![Não foi adicionado](media/Red_X.gif)|
 |Suporte do Assistente de serviços do Azure para preparação de atualização |[Visualização técnica 1706](capabilities-in-technical-preview-1706.md#changes-to-the-azure-services-wizard-to-support-upgrade-readiness)|![Não foi adicionado](media/Red_X.gif)|
 |Novas configurações de cliente para serviços de nuvem|[Visualização técnica 1706](capabilities-in-technical-preview-1706.md#new-client-settings-for-cloud-services)|![Não foi adicionado](media/Red_X.gif)|
 |Criar e executar scripts do PowerShell do console do Configuration Manager|[Visualização técnica 1706](capabilities-in-technical-preview-1706.md#create-and-run-powershell-scripts-from-the-configuration-manager-console)|![Não foi adicionado](media/Red_X.gif)|
 |Suporte de inicialização de rede do PXE para IPv6 |[Visualização técnica 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|![Não foi adicionado](media/Red_X.gif)|
 |Gerenciar atualizações de driver do Microsoft Surface |[Visualização técnica 1706](capabilities-in-technical-preview-1706.md#manage-microsoft-surface-driver-updates)|![Não foi adicionado](media/Red_X.gif)|
 |Configurar o Windows Update para políticas de adiamento de negócios |[Visualização técnica 1706](capabilities-in-technical-preview-1706.md#configure-windows-update-for-business-deferral-policies)|![Não foi adicionado](media/Red_X.gif)|
 |Restrições de registro do Android e iOS|[Visualização técnica 1706](capabilities-in-technical-preview-1706.md#android-and-ios-enrollment-restrictions)|![Não foi adicionado](media/Red_X.gif)|
 |Android para a política de gerenciamento de aplicativos de trabalho para copiar e colar|[Visualização técnica 1706](capabilities-in-technical-preview-1706.md#android-for-work-application-management-policy-for-copy-paste)|![Não foi adicionado](media/Red_X.gif)|
 |Novas definições de item de configuração do Windows|[Visualização técnica 1706](capabilities-in-technical-preview-1706.md#new-windows-configuration-item-settings)|![Não foi adicionado](media/Red_X.gif)|
 |Novas regras de política de conformidade do dispositivo|[Visualização técnica 1706](capabilities-in-technical-preview-1706.md#new-device-compliance-policy-rules)|![Não foi adicionado](media/Red_X.gif)|
 |Avaliação de atestado de integridade do dispositivo para políticas de conformidade para acesso condicional|[Visualização técnica 1706](capabilities-in-technical-preview-1706.md#device-health-attestation-assessment-for-compliance-policies-for-conditional-access)|![Não foi adicionado](media/Red_X.gif)|
 |Suporte para autoridades de certificação Entrust|[Visualização técnica 1706](capabilities-in-technical-preview-1706.md#support-for-entrust-certification-authorities)|![Não foi adicionado](media/Red_X.gif)|
 |Suporte para perfis VPN macOS Cisco (IPSec)|[Visualização técnica 1706](capabilities-in-technical-preview-1706.md#cisco-ipsec-support-for-macos-vpn-profiles)|![Não foi adicionado](media/Red_X.gif)|

## <a name="capabilities-delivered-in-previous-technical-previews"></a>Recursos fornecidos na visualização técnica anterior
 Quando todos os recursos de uma versão de visualização técnica estão disponíveis na versão mínima com suporte da ramificação atual, detalhes para essa versão de visualização são removidas da tabela a seguir.  

 |Funcionalidade |Versão de visualização técnica |Versão da ramificação atual|  
 |----------------|---------------------|--------------------|
  |Novos recursos do AD do Azure e gerenciamento de nuvem|[Visualização técnica 1705](capabilities-in-technical-preview-1705.md#new-capabilities-for-azure-ad-and-cloud-management)|![Não foi adicionado](media/Red_X.gif)|
 |Configurar e implantar políticas de proteção de aplicativos do Windows Defender|[Visualização técnica 1705](capabilities-in-technical-preview-1705.md#configure-and-deploy-windows-defender-application-guard-policies)|![Não foi adicionado](media/Red_X.gif)|
 |Ferramenta de redefinição de atualização  |[Visualização técnica 1705](capabilities-in-technical-preview-1705.md#update-reset-tool)|![Não foi adicionado](media/Red_X.gif)|
 |Suporte a alto DPI console  |[Visualização técnica 1705](capabilities-in-technical-preview-1705.md#high-dpi-console-support)|![Não foi adicionado](media/Red_X.gif)|
 |Aprimoramentos de Cache de mesmo nível  |[Visualização técnica 1705](capabilities-in-technical-preview-1705.md#peer-cache-improvements) |![Não foi adicionado](media/Red_X.gif)|
 |Melhorias para o SQL Server em grupos de disponibilidade AlwaysOn |[Visualização técnica 1705](capabilities-in-technical-preview-1705.md#improvements-for-sql-server-always-on-availability-groups) |![Não foi adicionado](media/Red_X.gif)|
 |Melhor notificações de usuário para atualizações do Office 365|[Visualização técnica 1705](capabilities-in-technical-preview-1705.md#improved-user-notifications-for-office-365-updates) |![Não foi adicionado](media/Red_X.gif)|
 |Use o Assistente para serviços do Azure para configurar uma conexão para OMS|[Visualização técnica 1705](capabilities-in-technical-preview-1705.md#use-azure-services-wizard-to-configure-a-connection-to-oms) |![Não foi adicionado](media/Red_X.gif)|
 |Configurar aplicativos Android com as políticas de configuração de aplicativo  |[Visualização técnica 1704](capabilities-in-technical-preview-1704.md#configure-android-apps-with-app-configuration-policies)|![Não foi adicionado](media/Red_X.gif)|
 |Inventário de hardware coleta informações de inicialização segura |[Visualização técnica 1704](capabilities-in-technical-preview-1704.md#hardware-inventory-collects-secure-boot-information)|![Não foi adicionado](media/Red_X.gif)|
 |Adicionar as sequências de tarefas filho para uma sequência de tarefas|[Visualização técnica 1704](capabilities-in-technical-preview-1704.md#add-child-task-sequences-to-a-task-sequence)|![Não foi adicionado](media/Red_X.gif)|
 |Recarregar imagens de inicialização com a versão atual do Windows PE |[Visualização técnica 1704](capabilities-in-technical-preview-1704.md#reload-boot-images-with-current-windows-pe-version)|![Não foi adicionado](media/Red_X.gif)|
 |Aprimoramentos de implantação de sistema operacional|[Visualização técnica 1704](capabilities-in-technical-preview-1704.md#improvements-to-operating-system-deployment)|![Não foi adicionado](media/Red_X.gif)|
 |Implantar aplicativos iOS adquiridos por volume em coleções de dispositivos|[Visualização técnica 1703](capabilities-in-technical-preview-1703.md#deploy-volume-purchased-ios-apps-to-device-collections)|[Versão 1702](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps)|
 |Links diretos para aplicativos no Centro de Software|[Visualização técnica 1703](capabilities-in-technical-preview-1703.md#direct-links-to-applications-in-software-center)|![Não foi adicionado](media/Red_X.gif)
 |Certificados PFX para computadores cliente do Windows do Configuration Manager|[Visualização técnica 1703](capabilities-in-technical-preview-1703.md#pfx-certificates-for-configuration-manager-windows-client-computers)|![Não foi adicionado](media/Red_X.gif)|
 |Configurar o Assistente de serviços do Azure|[Visualização técnica 1703](capabilities-in-technical-preview-1703.md#configure-azure-services-wizard)|![Não foi adicionado](media/Red_X.gif)|
 |Converter de BIOS em UEFI em uma sequência de tarefas de atualização do sistema operacional| [Visualização técnica 1703](capabilities-in-technical-preview-1703.md#convert-from-bios-to-uefi-during-an-in-place-upgrade) |[Versão 1702](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade)|
 |Grupos de sequências de tarefas recolhível| [Visualização técnica 1703](capabilities-in-technical-preview-1703.md#collapsible-task-sequence-groups) |![Não foi adicionado](media/Red_X.gif)|
 |Configurações do cliente para configurar a análise do Windows para preparação de atualização | [Visualização técnica 1703](capabilities-in-technical-preview-1703.md#client-settings-to-configure-windows-analytics-for-upgrade-readiness) |![Não foi adicionado](media/Red_X.gif)|
 |Novas configurações de conformidade para dispositivos iOS|[Visualização técnica 1702](capabilities-in-technical-preview-1702.md#new-compliance-settings-for-ios-devices)|[Versão 1702](/sccm/mdm/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client)|
 |Criar certificados PFX com suporte a S/MIME|[Visualização técnica 1702](capabilities-in-technical-preview-1702.md#create-pfx-certificates-with-s-mime-support)|[Versão 1702](/sccm/mdm/deploy-use/create-pfx-certificate-profiles)|
 |Verificar para executar arquivos executáveis antes de instalar um aplicativo|[Visualização técnica 1702](capabilities-in-technical-preview-1702.md#check-for-running-executable-files-before-installing-an-application)|[Versão 1702](/sccm/apps/deploy-use/deploy-applications)|
 |Enviar comentários no console do Configuration Manager | [Visualização técnica 1702](capabilities-in-technical-preview-1702.md#send-feedback-from-the-configuration-manager-console)    |[Versão 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#send-feedback-from-the-configuration-managercconsole)  |
 |Alterações para atualizações e manutenção  | [Visualização técnica 1702](capabilities-in-technical-preview-1702.md#changes-for-updates-and-servicing)  |[Versão 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#changes-for-updates-and-servicing) |
 |Aprimoramentos de Cache de mesmo nível  | [Visualização técnica 1702](capabilities-in-technical-preview-1702.md#peer-cache-improvements) |[Versão 1702](/sccm/core/plan-design/hierarchy/client-peer-cache)|
 |Usar o Active Directory do Azure  | [Visualização técnica 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |![Não foi adicionado](media/Red_X.gif)|
 |Aprimoramentos de política de conformidade de dispositivo de acesso condicional | [Visualização técnica 1702](capabilities-in-technical-preview-1702.md#conditional-access-device-compliance-policy-improvements) |[Versão 1702](/sccm/mdm/deploy-use/create-compliance-policy)|
 |Alerta de versão do cliente de antimalware | [Visualização técnica 1702](capabilities-in-technical-preview-1702.md#antimalware-client-version-alert) |[Versão 1702](/sccm/protect/deploy-use/endpoint-configure-alerts?branch=live#alert-for-outdated-malware-client)|
 |Avaliação de conformidade para o Windows Update para atualizações de negócios | [Visualização técnica 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |![Não foi adicionado](media/Red_X.gif)|
 |Aprimoramentos para configurações do Centro de Software e mensagens de notificação para sequências de tarefas de alto impacto|[Visualização técnica 1702](capabilities-in-technical-preview-1702.md#antimalware-client-version-alert)|[Versão 1702](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#set-a-task-sequence-as-a-high-impact-task-sequence)|
 |Android para suporte de trabalho| [Visualização técnica 1702](capabilities-in-technical-preview-1702.md#android-for-work-support) |[Versão 1702](/sccm/mdm/deploy-use/enroll-hybrid-android#enable-android-for-work-enrollment)|
 |Aprimoramentos de grupos de limites para o software de pontos de atualização | [Visualização técnica 1701](capabilities-in-technical-preview-1701.md#boundary-groups-improvements-for-software-update-points)    |[Versão 1702](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points)  |
 |Inventário de hardware coleta informações de UEFI | [Visualização técnica 1701](capabilities-in-technical-preview-1701.md#hardware-inventory-collects-uefi-information)|[Versão 1702](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#hardware-inventory-collects-uefi-information) |
 |Aprimoramentos de implantação de sistema operacional| [Visualização técnica 1701](capabilities-in-technical-preview-1701.md#improvements-to-operating-system-deployment)|[Versão 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#operating-system-deployment) |
 |Atualizações de software do host nos pontos de distribuição baseado em nuvem| [Visualização técnica 1701](capabilities-in-technical-preview-1701.md#host-software-updates-on-cloud-based-distribution-points)|![Não foi adicionado](media/Red_X.gif) |
 |Validar dados de atestado de integridade do dispositivo por meio de pontos de gerenciamento| [Visualização técnica 1701](capabilities-in-technical-preview-1701.md#validate-device-health-attestation-data-via-management-points)| [Versão 1702](/sccm/core/servers/manage/health-attestation) |
 |Conector do OMS para a nuvem do Microsoft Azure Government |[Visualização técnica 1701](capabilities-in-technical-preview-1701.md#use-the-oms-connector-for-microsoft-azure-government-cloud) |[Versão 1702](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#fairfaxconfig) |
 |Android e iOS versões não são mais targetable nos assistentes para criação |[Visualização técnica 1701](capabilities-in-technical-preview-1701.md#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm) |![Não foi adicionado](media/Red_X.gif) |
 |Acesso de dados do ponto de extremidade OData |[Visualização técnica 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|![Não foi adicionado](media/Red_X.gif)|
 |Ponto de serviço de depósito de dados |[Visualização técnica 1612](capabilities-in-technical-preview-1612.md#the-data-warehouse-service-point)|[Versão 1702](/sccm/core/servers/manage/data-warehouse)|
 |Ferramenta de limpeza de biblioteca de conteúdo |[Visualização técnica 1612](capabilities-in-technical-preview-1612.md#content-library-cleanup-tool)|[Versão 1702](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool) |
 |Melhorias para a pesquisa no console |[Visualização técnica 1612](capabilities-in-technical-preview-1612.md#improvements-for-in-console-search)|[Versão 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#improvements-for-in-console-search)|
 |Impedir a instalação de um aplicativo se estiver executando um programa especificado|[Visualização técnica 1612](capabilities-in-technical-preview-1612.md#prevent-installation-of-an-application-if-a-specified-program-is-running)|[Versão 1702](/sccm/apps/deploy-use/deploy-applications)|
 |Novo Windows Hello para notificação de negócios para usuários finais|[Visualização técnica 1612](capabilities-in-technical-preview-1612.md#new-windows-hello-for-business-notification-for-end-users)|![Não foi adicionado](media/Red_X.gif)|
 |Windows Store para suporte de negócios no Configuration Manager|[Visualização técnica 1612](capabilities-in-technical-preview-1612.md#windows-store-for-business-support-in-configuration-manager)|![Não foi adicionado](media/Red_X.gif)|
 |Retornar à página anterior, quando não é uma sequência de tarefas|[Visualização técnica 1612](capabilities-in-technical-preview-1612.md#return-to-previous-page-when-a-task-sequence-fails)|[Versão 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#operating-system-deployment)|
 |Suporte para atualizações do Windows 10 arquivos de instalação expressa|[Visualização técnica 1612](capabilities-in-technical-preview-1612.md#express-installation-files-support-for-windows-10-updates)|[Versão 1702](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates)|
 |Integração do Active Directory do Azure|[Visualização técnica 1612](capabilities-in-technical-preview-1612.md#azure-active-directory-onboarding)|![Não foi adicionado](media/Red_X.gif)|
 |Alterar a configuração de autenticação multifator para registro de dispositivo|[Visualização técnica 1612](capabilities-in-technical-preview-1612.md#change-to-configuring-multi-factor-authentication-for-device-enrollment)|![Não foi adicionado](media/Red_X.gif)|
 |Conteúdo do cache de pré-lançamento para implantações e sequências de tarefas |[Visualização técnica 1611](capabilities-in-technical-preview-1611.md#pre-cache-content-for-available-deployments-and-task-sequences)|[Versão 1702](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content)|
 |Definições de configuração do Windows Defender|[Visualização técnica 1610](capabilities-in-technical-preview-1610.md#windows-defender-configuration-settings)|[Versão 1610](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client)|
 |Sincronização de diretiva de solicitação do console do administrador|[Visualização técnica 1610](capabilities-in-technical-preview-1610.md#request-policy-sync-from-administrator-console)|[Versão 1610](/sccm/mdm/deploy-use/sync-intune-device)|
 |Suporte à função de segurança adicional para o nó de todos os dispositivos corporativos|[Visualização técnica 1610](capabilities-in-technical-preview-1610.md#additional-security-role-support)|[Versão 1610](/sccm/mdm/understand/whats-new-in-hybrid-mobile-device-management#new-hybrid-features-in-november-2016)|
 |Acesso condicional para perfis de VPN do Windows 10|[Visualização técnica 1610](capabilities-in-technical-preview-1610.md#conditional-access-for-windows-10-vpn-profiles)|[Versão 1610](/sccm/protect/deploy-use/create-vpn-profiles#configure-the-authentication-method-for-the-vpn-profile)|
 |Filtrar por tamanho do conteúdo nas regras de implantação automática|[Visualização técnica 1610](capabilities-in-technical-preview-1610.md#filter-by-content-size-in-automatic-deployment-rules)|[Versão 1610](/sccm/core/plan-design/changes/whats-new-in-version-1610#filter-by-content-size-in-automatic-deployment-rules) |
 |Funcionalidade aprimorada para caixas de diálogo do software necessário|[Visualização técnica 1610](capabilities-in-technical-preview-1610.md#improved-functionality-for-required-software-dialogs)|[Versão 1610](/sccm/apps/deploy-use/deploy-applications)|
 |Negar as solicitações de aplicativo anteriormente aprovado|[Visualização técnica 1610](capabilities-in-technical-preview-1610.md#deny-previously-approved-application-requests)|[Versão 1610](/sccm/apps/deploy-use/deploy-applications)|
 |Excluir os clientes da atualização automática|[Visualização técnica 1610](capabilities-in-technical-preview-1610.md#exclude-clients-from-automatic-upgrade)|[Versão 1610](/sccm/core/clients/manage/upgrade/exclude-clients-windows)|
 |Melhorias para a proteção de ponto de extremidade|[Visualização técnica 1609](capabilities-in-technical-preview-1609.md#improvements-to-endpoint-protection)|[Versão 1610](/sccm/protect/deploy-use/endpoint-antimalware-policies#cloud-protection-service)|
 |Aumento do número de dispositivos registrados|[Visualização técnica 1609](/sccm/mdm/deploy-use/enable-platform-enrollment)|[Versão 1610](/sccm/mdm/deploy-use/enable-platform-enrollment)|
 |Configurações adicionais de DEP da Apple|[Visualização técnica 1609](capabilities-in-technical-preview-1609.md#additional-apple-dep-settings)|[Versão 1610](/sccm/mdm/deploy-use/ios-device-enrollment-program-for-hybrid)|
 |Aprimoramentos da Windows Store para a integração de negócios com o Configuration Manager|[Visualização técnica 1609](capabilities-in-technical-preview-1609.md)|[Versão 1610](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|
 |Novas configurações de conformidade para itens de configuração|[Visualização técnica 1609](capabilities-in-technical-preview-1609.md#new-compliance-settings-for-configuration-items)|[Versão 1610](/sccm/compliance/deploy-use/create-configuration-items)|
 |Integração com a análise de atualização|[Visualização técnica 1609](capabilities-in-technical-preview-1609.md#integration-with-upgrade-analytics)|[Versão 1610](/sccm/core/clients/manage/upgrade/upgrade-analytics)|
 |Perfis de VPN híbrida de tipos de Conexão nativo para Windows 10|[Visualização técnica 1609](capabilities-in-technical-preview-1609.md#native-connection-types-for-windows-10-vpn-hybrid-profiles)|![Não foi adicionado](media/Red_X.gif)|
 |Aprimoramentos para grupos de limites|[Visualização técnica 1609](capabilities-in-technical-preview-1609.md#improvements-for-boundary-groups)|[Versão 1610](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#BKMK_BoundaryGroups)|
 |Painel de gerenciamento de clientes do Office 365|[Visualização técnica 1609](capabilities-in-technical-preview-1609.md#office-365-client-management-dashboard)|[Versão 1610](/sccm/sum/deploy-use/manage-office-365-proplus-updates#office-365-client-management-dashboard)|
 |Implantar aplicativos do Office 365 para clientes|[Visualização técnica 1609](capabilities-in-technical-preview-1609.md#deploy-office-365-apps-to-clients)|[Versão 1702](/sccm/sum/deploy-use/manage-office-365-proplus-updates#deploy-office-365-apps)|
 |Aprimoramentos do BIOS para conversão de UEFI|[Visualização técnica 1609](capabilities-in-technical-preview-1609.md#BKMK_UEFIConversion)|[Versão 1610](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion)|
 |Gráficos de conformidade do Intune|[Visualização técnica 1609](capabilities-in-technical-preview-1609.md#intune-compliance-charts)|[Versão 1610](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy)|
 |Melhoramentos ao passo Preparar ConfigMgr Client para Captura de sequência de tarefas|[Visualização técnica 1608](capabilities-in-technical-preview-1608.md#improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step)|[Versão 1610](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture)|
 |Melhorias no Centro de Software|[Visualização técnica 1608](capabilities-in-technical-preview-1608.md#improvements-to-software-center)|[Versão 1610](/sccm/core/plan-design/changes/whats-new-in-version-1610#general-improvements-to-software-center)|
 |Aprimoramentos de inteligência de ativos|[Visualização técnica 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|![Não foi adicionado](media/Red_X.gif)|
 |Conversão de teclado de controle remoto|[Visualização técnica 1608](capabilities-in-technical-preview-1608.md#remote-control-keyboard-translation)|![Não foi adicionado](media/Red_X.gif)|
 |Melhoramentos à Política de Atualização de Edição do Windows 10|[Visualização técnica 1607](capabilities-in-technical-preview-1607.md#dmp_edition)|[Versão 1610](/sccm/compliance/deploy-use/upgrade-windows-version)|
 |Imagem Corporativa Personalizável para Caixas de Diálogo do Centro de Software|[Visualização técnica 1607](capabilities-in-technical-preview-1607.md#customizable-branding-for-software-center-dialogs)|![Não foi adicionado](media/Red_X.gif)|  
 |Vários pontos de gestão de dispositivos para Gestão de Dispositivos Móveis no Local|[Visualização técnica do 1606](capabilities-in-technical-preview-1606.md#dmp_onprem)|[Versão 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#on-premises-mobile-device-management)|
 |Categorizar automaticamente os dispositivos em coleções|[Visualização técnica do 1606](capabilities-in-technical-preview-1606.md#dmp_category)|[Versão 1606](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections) |
 |Período de tolerância de imposição para implementações de atualizações de aplicações e de software|[Visualização técnica do 1606](capabilities-in-technical-preview-1606.md#dmp_grace)|[Versão 1610](/sccm/apps/deploy-use/deploy-applications)|
 |Utilizar o Configuration Manager como um Instalador Gerido com Device Guard|[Visualização técnica do 1606](capabilities-in-technical-preview-1606.md#dmp_devg)|![Não foi adicionado](media/Red_X.gif)|
 |Gateway de gerenciamento de nuvem (anteriormente conhecida como serviço de Proxy de nuvem)|[Visualização técnica do 1606](capabilities-in-technical-preview-1606.md#cloud_proxy) | [Versão 1610](/sccm/core/clients/manage/plan-cloud-management-gateway)|  
 |Gerir o agente de cliente do Office 365 no Configuration Manager|[Visualização técnica do 1606](capabilities-in-technical-preview-1606.md#manage_o365) |[Versão 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#software-updates)|  
 |A variável da sequência de tarefas OSDPreserveDriveLetter foi preterida|[Visualização técnica do 1606](capabilities-in-technical-preview-1606.md#osdpreservedriveletter) |[Versão 1606](/sccm/osd/understand/task-sequence-built-in-variables) |
 |Alterações do Nó Atualizações e Manutenção|[Visualização técnica do 1606](capabilities-in-technical-preview-1606.md#updatesandservicing)|[Versão 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#updates-and-servicing) |
 |VPN por Aplicação para dispositivos Windows 10|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_PerAppVPN)|[Versão 1606](/sccm/protect/deploy-use/create-vpn-profiles)|  
 |Melhoramentos à sequência de tarefas Instalar atualizações de software|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_InstallSU)|[Versão 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#operating-system-deployment)|  
 |Melhoramentos ao passo Preparar ConfigMgr Client para Captura de sequência de tarefas |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_PrepareConfigMgrClient)|[Versão 1610](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture) |
 |Período de tolerância para implementações de aplicações necessárias |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_Grace)|![Não foi adicionado](media/Red_X.gif)|  
 |Nova experiência para ações de dispositivos remotos |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_Remote)|[Versão 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#device-configuration-and-protection)|  
 |Aplicações da Loja Windows para Empresas |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_WSFB)|[Versão 1606](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|  
 |Melhoramentos gerais para aplicações compradas em volume|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_VPP2)|[Versão 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)|  
 |Proteção de Dados Empresariais (EDP)|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_VPP)|[Versão 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)|  
 |Os utilizadores finais podem instalar aplicações a partir do Portal da Empresa |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|![Não foi adicionado](media/Red_X.gif)|  
 |Novos separadores para Atualizações e Sistemas Operativos no Centro de Software|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_SW1)|[Versão 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#application-management)|  
 |Fazer manutenção a um grupo de servidores |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_ServerGroups)|[Versão 1606](/sccm/sum/deploy-use/service-a-server-group)|   
 |Suporte do serviço Proteção Avançada Contra Ameaças do Windows Defender |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_ATP)|[Versão 1606](/sccm/protect/deploy-use/windows-defender-advanced-threat-protection)|  
 |Novas opções de reinício para clientes do Windows 10 após a instalação de atualizações de software|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_RestartOptions)|[Versão 1606](/sccm/sum/plan-design/plan-for-software-updates#restart-options-for-Windows-10-clients-after-software-update-installation)|  
 |Atestado de Estado de Funcionamento no Local |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_DHA)|[Versão 1606](/sccm/core/servers/manage/health-attestation)|  
 |Pré-declarar dispositivos pertencentes à empresa com o número de série IMEI ou iOS|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_IMEI)|[Versão 1606](/sccm/mdm/deploy-use/predeclare-devices-with-hardware-id)|  

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
[O que há de novo no System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
 [Introdução ao System Center Configuration Manager](../../core/understand/introduction.md)

