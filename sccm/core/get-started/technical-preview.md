---
title: "Versões do Technical Preview"
titleSuffix: Configuration Manager
description: "Saiba mais sobre a versão de pré-visualização técnica que permite-lhe test-drive novas funcionalidades e capacidades no System Center Configuration Manager."
ms.custom: na
ms.date: 02/09/2018
ms.prod: configuration-manager
ms.reviewer: nab
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
caps.latest.revision: 
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 1cb4d775985839ea7c4fb1b48a04ab0be64f5d8c
ms.sourcegitcommit: 32bbc006a41868a6d9a708db5f7b372d9c71d985
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/08/2018
---
# <a name="technical-preview-for-system-center-configuration-manager"></a>Pré-visualização técnica do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (Technical Preview)*

**Bem-vindo ao do System Center Configuration Manager Technical Preview**. Este artigo fornece detalhes sobre a versão de pré-visualização em desenvolvimento que introduz novas funcionalidades e capacidades que estamos a trabalhar. Cada versão do technical preview introduz novas funcionalidades que não estejam incluídas no ramo atual do Configuration Manager no momento que da versão de pré-visualização técnica é disponibilizada. Estas funcionalidades poderão eventualmente ser incluídas numa atualização à versão do ramo atual, mas antes de finalizarmos as funcionalidades e de as adicionarmos, queremos que tenha a oportunidade de experimentá-las e de nos enviar os seus comentários.  

 Porque esta versão é uma versão de pré-visualização técnica, detalhes e a funcionalidade estão sujeitos a alterações.  

 Este artigo contém informações que se aplicam a todas as versões do Technical Preview. Lista também cada nova capacidade (ou funcionalidade), juntamente com a versão de pré-visualização técnica em que a capacidade aparece pela primeira vez, como a versão 1802 de Fevereiro de 2018. Estas capacidades estão descritas nos tópicos separados dedicados para cada versão de pré-visualização.  

 Para obter informações sobre quais são as novidades no ramo atual do Configuration Manager, consulte [que há de novo no System Center Configuration Manager](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012).



##  <a name="bkmk_reqs"></a> Requisitos e limitações do Technical Preview  

> [!IMPORTANT]     
>  A Technical Preview está licenciada para ser utilizada apenas num ambiente de laboratório.  A Microsoft poderá não fornecer serviços de suporte e algumas funcionalidades poderão não estar disponíveis no software de pré-visualização. Além disso, o software de pré-visualização, poderá ter reduzida ou padrões diferentes de segurança, privacidade, acessibilidade, disponibilidade e fiabilidade relativa comercialmente fornecidos software.  

 Para a maioria dos pré-requisitos de produto, utilize as informações de [configurações suportadas para o System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md). As seguintes exceções são aplicáveis apenas às versões do Technical Preview:  

-   Cada instalação permanece ativa durante 90 dias até se tornar inativa.  

-   O inglês é o único idioma suportado.


-   Apenas os seguintes sinalizadores de instalação (comutadores) são suportados:  

    -   **/silent**  
    -   **/testdbupgrade**    


-   Por predefinição, quando utiliza o technical preview, o ponto de ligação de serviço é instalado para o modo online. Não suporta a alteração para o modo offline.

-   Os artigos separados para cada versão específica do technical preview incluem limitações ou requisitos, conforme aplicável.

-   Não existe suporte para migração para ou a partir desta versão de pré-visualização.  

-   Não existe suporte para atualizar para esta versão de pré-visualização. 

-   Não são suportadas para a recuperação de sites a partir da pasta CD. Latest.  <!--507106-->

-   Não existe suporte para atualizar para uma compilação de produção (ramo atual) a partir desta preview build. No entanto, quando as atualizações estiverem disponíveis para uma versão de pré-visualização, pode encontrar e instalá-los a partir de **atualizações e manutenção** nós da consola do Configuration Manager. Para ver um vídeo do processo de atualização na consola, veja [Installing ConfigMgr Update Packages](https://www.youtube.com/embed/KBd_EGFbUT8) (Instalar Pacotes de Atualização do ConfigMgr) em youtube.com.  
-   Apenas é suportado um site primário autónomo. Não existe suporte para um site de administração central, múltiplos sites primários ou sites secundários.  

Os produtos e tecnologias que se seguem são suportadas por este ramo do Configuration Manager. No entanto, a sua inclusão neste conteúdo não implica uma extensão de suporte para um produto ou a versão que está fora individual do produto vida de suporte. Os produtos que estejam fora do respetivo ciclo de vida de suporte não são suportados para utilização com o Configuration Manager. Para mais informações sobre os Ciclos de Vida do Suporte da Microsoft, aceda ao site [Ciclo de Vida do Suporte da Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=208270) .  

-   Apenas são suportadas as seguintes versões do SQL Server:  

    -   SQL Server 2017 (com a atualização cumulativa 2 e posterior) que começa no Configuration Manager versão 1710
    -   SQL Server 2016 (sem Service Pack e posterior)
    -   SQL Server 2014 (com Service Pack 1 e posterior)
    -   SQL Server 2012 (com Service Pack 3, ou posterior)


-   O site suporta até 10 clientes, tem de executar uma das seguintes versões do Windows:  

      -   Windows 10  
      -   Windows 8,1  
      -   Windows 7  

##  <a name="bkmk_install"></a> Instalar e atualizar o Technical Preview  
 O System Center Configuration Manager Technical Preview é distinto da versão atual do System Center Configuration Manager.  

 Para utilizar a pré-visualização técnica, primeiro tem de instalar um **versão de linha** da versão de pré-visualização técnica. Depois de instalar uma versão de linha de base, em seguida, utilizar **atualizações na consola** para ter a sua instalação atualizada com a versão de pré-visualização mais recente. Normalmente, existem novas versões mensais da Technical Preview.

Cada versão de pré-visualização é suportado até três versões sucessivas estão disponíveis. Ou seja, quando 1708 lançada, versão 1704 foi versão já não suporte, mas versões 1705, 1706 e 1707 permanecer suporte. Quando uma linha de base está fora do suporte, ainda é suportada para instalar um novo site de pré-visualização técnica até que uma nova versão de linha de base está disponível, desde que, em seguida, atualizar essa instalação para uma versão suportada. Atualizar para a versão mais recente disponível e, em seguida, repita esse processo até que pode instalar a versão mais recente do technical preview.

> [!TIP]  
>  Quando instala uma atualização da versão de pré-visualização técnica, atualiza a instalação de pré-visualização para essa nova versão de pré-visualização técnica.    Uma instalação de pré-visualização técnica nunca inclui a opção de atualizar para uma instalação do ramo atual, nem de receber atualizações da versão do ramo atual.  

**Versões de linha de base ativas da Technical Preview:**
   
Pode instalar uma versão de linha de base para até um ano depois da versão. No entanto, quando instala um novo site de pré-visualização técnica, recomendamos que utilize a versão de linha de base mais recente que está disponível.
-  **Technical Preview 1711** -o Configuration Manager Technical Preview 1711 está disponível como uma atualização de na consola e como uma nova versão de linha de base. Transferir as versões de linha de base [do Centro de avaliação TechNet](http://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).


##  <a name="BKMK_TPFeedback"></a> Fornecer comentários  
 Iremos adoram ouvir os seus comentários sobre as funcionalidades no nosso pré-visualizações técnicas. Para obter mais informações, consulte [comentários sobre produtos](../understand/find-help.md#product-feedback).

Se tiver ideias sobre novas funcionalidades que gostaria de ver, queremos interessados. Para submeter novas ideias e votar nas ideias submetidas por outras pessoas, [visite a nossa página do UserVoice](http://configurationmanager.uservoice.com).  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->




##  <a name="bkmk_tpCaps"></a> Capacidades fornecidas no technical preview mais recente  
Seguem-se as capacidades fornecidas com a versão de pré-visualização técnica mais recente do Configuration Manager.  Capacidades que estavam disponíveis numa versão anterior do technical preview permanecem disponíveis nas versões posteriores. Da mesma forma, as capacidades que foram adicionadas para o ramo atual do Configuration Manager permanecerem disponíveis em versões de pré-visualização técnica.  Clique nas hiperligações para o conteúdo de cada versão de pré-visualização para saber mais sobre uma capacidade específica.  

<!-- This is the full list of new features in the latest TP release -->

### <a name="technical-preview-version-1802"></a>Pré-visualização técnica versão 1802
- [Carga de trabalho de proteção de ponto final de transição para o Intune utilizando a gestão de conjunta](capabilities-in-technical-preview-1802.md#transition-endpoint-protection-workload-to-intune-using-co-management) <!-- 1357365 -->
- [Configurar a otimização de entrega do Windows para utilizar grupos de limites do Configuration Manager](capabilities-in-technical-preview-1802.md#configure-windows-delivery-optimization-to-use-configuration-manager-boundary-groups) <!-- 1324696 --> 
- [Sequência de tarefas de atualização no local do Windows 10 através do gateway de gestão de nuvem](capabilities-in-technical-preview-1802.md#windows-10-in-place-upgrade-task-sequence-via-cloud-management-gateway) <!-- 1357149 -->
- [Melhoramentos à sequência de tarefas de atualização no local do Windows 10](capabilities-in-technical-preview-1802.md#improvements-to-windows-10-in-place-upgrade-task-sequence) <!-- 1357425 --> 
- [Melhoramentos para pontos de distribuição com PXE ativado](capabilities-in-technical-preview-1802.md#improvements-to-pxe-enabled-distribution-points) <!-- 1357580 --> 
- [Modelos de implementação para sequências de tarefas](capabilities-in-technical-preview-1802.md#deployment-templates-for-task-sequences) <!-- 1357391 --> 
- [Dashboard de ciclo de vida do produto](capabilities-in-technical-preview-1802.md#product-lifecycle-dashboard) <!--1319632 --> 
- [Melhoramentos aos relatórios](capabilities-in-technical-preview-1802.md#improvements-to-reporting) <!--1357653 --> 
- [Melhoramentos ao centro de Software](capabilities-in-technical-preview-1802.md#improvements-to-software-center) <!--1357592 --> 
- [Melhoramentos para executar Scripts](capabilities-in-technical-preview-1802.md#improvements-to-run-scripts) <!--1236459 --> 
- [Grupo de limites contingência para pontos de gestão](capabilities-in-technical-preview-1802.md#boundary-group-fallback-for-management-points) <!-- 1324594 --> 
- [Suporte melhorado para certificados CNG](capabilities-in-technical-preview-1802.md#improved-support-for-cng-certificates) <!-- 1357314 --> 
- [Suporte de gateway de gestão de nuvem do Azure Resource Manager](capabilities-in-technical-preview-1802.md#cloud-management-gateway-support-for-azure-resource-manager) <!-- 1324735 --> 
- [Aprovar pedidos de aplicações para os utilizadores por dispositivo](capabilities-in-technical-preview-1802.md#approve-application-requests-for-users-per-device) <!-- 1357015 --> 
- [Utilizar o Centro de Software para procurar e instalar aplicações disponíveis ao utilizador no Azure AD-dispositivos associados a um](capabilities-in-technical-preview-1802.md#use-software-center-to-browse-and-install-user-available-applications-on-azure-ad-joined-devices) <!-- 1322613 --> 
- [Relatório sobre as informações do dispositivo Windows AutoPilot](capabilities-in-technical-preview-1802.md#report-on-windows-autopilot-device-information) <!-- 1351442 --> 
- [Melhoramentos às políticas do Configuration Manager para o Windows Defender exploram proteção](capabilities-in-technical-preview-1802.md#improvements-to-configuration-manager-policies-for-windows-defender-exploit-guard) <!-- 1356220 -->
- [Políticas de browser Microsoft Edge](capabilities-in-technical-preview-1802.md#microsoft-edge-browser-policies) <!-- 1357310 -->
- [Relatório de contagens de browser predefinido](capabilities-in-technical-preview-1802.md#report-for-default-browser-counts) <!-- 1357830 --> 
- [Suporte para dispositivos Windows 10 ARM64](capabilities-in-technical-preview-1802.md#support-for-windows-10-arm64-devices) <!-- 1353704 --> 
- [Alterações das implementações faseada](capabilities-in-technical-preview-1802.md#changes-to-phased-deployments) <!-- 1357405 -->



## <a name="capabilities-delivered-in-recent-supported-technical-previews"></a>Capacidades fornecidas em pré-visualizações técnicas de suportados recentes
Seguem-se as capacidades fornecidas em versões anteriores da versão de pré-visualização técnica do Configuration Manager que ainda são suportadas. 

<!-- This is the full list of new features in the past three TP releases. 
Each month, add features from the list above to the top of this table. 
Then remove the bottom of this list and/or move individual items not in CB to the third table below.
-->

 |Funcionalidade |Versão de pré-visualização técnica |Versão do ramo atual|  
 |----------------|---------------------|--------------------|
 |Criar implementações faseadas <!-- 1357405 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#create-phased-deployments)  |![Não foi adicionada](media/Red_X.gif)    |
 |Relatórios de gestão conjunta <!-- 1356648 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#co-management-reporting)  |![Não foi adicionada](media/Red_X.gif)    |
 |Melhoramentos à agenda de avaliação da regra de implementação automática <!-- 1357133 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#improvements-to-automatic-deployment-rule-evaluation-schedule)  |![Não foi adicionada](media/Red_X.gif)    |
 |Reatribuir o ponto de distribuição <!-- 1306937 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#reassign-distribution-point)  |![Não foi adicionada](media/Red_X.gif)    |
 |Melhoramentos ao inventário de hardware <!-- 1357389 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#improvements-to-hardware-inventory)  |![Não foi adicionada](media/Red_X.gif)    |
 |Melhoramentos às definições de cliente no Centro de Software <!-- 1355146 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#improvements-to-client-settings-for-software-center)  |![Não foi adicionada](media/Red_X.gif)    |
 |Novas definições de proteção de aplicações do Windows Defender <!-- 1356256 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#new-settings-for-windows-defender-application-guard)  |![Não foi adicionada](media/Red_X.gif)    |
 |Melhoramentos para executar Scripts <!-- 1236459 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#improvements-to-run-scripts)  |![Não foi adicionada](media/Red_X.gif)    |
 |Não atualizar automaticamente as aplicações substituídas <!-- 1351266 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#do-not-automatically-upgrade-superseded-applications)  |![Não foi adicionada](media/Red_X.gif)    | 
 |Instalar várias aplicações no Centro de Software <!-- 1357126 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#install-multiple-applications-in-software-center)  |![Não foi adicionada](media/Red_X.gif)    |
 |Serviço baseado em clientes de dispositivo de resposta PXE <!-- 1357148 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service)  |![Não foi adicionada](media/Red_X.gif)    |
 |Instalar a alteração no cliente do Configuration Manager <!-- 1356195 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#change-in-the-configuration-manager-client-install)  |![Não foi adicionada](media/Red_X.gif)    | 
 |Mude para o dashboard de dispositivo superfície <!-- 1355788 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#change-to-the-surface-device-dashboard)  |![Não foi adicionada](media/Red_X.gif)    | 
 |Melhoramentos ao dashboard de gestão de clientes do Office 365 <!-- 1357281 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#improvements-to-office-365-client-management-dashboard)  |![Não foi adicionada](media/Red_X.gif)    | 
 |Melhorias à consola do Configuration Manager <!-- 1357280,1357282 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#improvements-to-the-configuration-manager-console)  |![Não foi adicionada](media/Red_X.gif)    | 
 |Melhorias para implementação do sistema operativo <!-- SMS 500897 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#improvements-to-operating-system-deployment)  |![Não foi adicionada](media/Red_X.gif)    | 
 |Executar o passo de sequência de tarefas <!-- 1261338 --> | [Tech Preview 1711](capabilities-in-technical-preview-1711.md) |[Versão 1710](/sccm/osd/understand/task-sequence-steps#child-task-sequence)    |
 |Permitir interação do utilizador quando instalar uma aplicação <!-- 1356976 --> | [Tech Preview 1711](capabilities-in-technical-preview-1711.md) |![Não foi adicionada](media/Red_X.gif)    |

 

## <a name="capabilities-delivered-in-previous-technical-previews"></a>Capacidades fornecidas em pré-visualizações técnicas anteriores
Seguem-se as capacidades específicas fornecidas com versões anteriores da versão de pré-visualização técnica do Configuration Manager. Estas capacidades permanecem disponíveis nas versões posteriores, mas ainda não estão disponíveis na versão atual do ramo. 

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

 |Funcionalidade |Versão de pré-visualização técnica |  
 |----------------|---------------------|
 |Experiência de perfil VPN melhorada na consola do Configuration Manager <!-- 1313282 --> | [Tech Preview 1709](capabilities-in-technical-preview-1709.md) |
 |Informações de gestão  <!-- 1353967 --> |[Tech Preview 1708](capabilities-in-technical-preview-1708.md#management-insights)|
 |Dashboard de dispositivo superfície <!-- 1355788 --> |[Tech Preview 1707](capabilities-in-technical-preview-1707.md#surface-device-dashboard)|
 |Disponibilidade elevada de função do servidor de site <!-- 1128774 --> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#site-server-role-high-availability) |
 |Suporte de arranque de rede do PXE para IPv6 <!-- 1269793 --> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
 |Avaliação de atestado de estado de funcionamento do dispositivo para as políticas de conformidade de acesso condicional <!-- 1235616 -->|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#device-health-attestation-assessment-for-compliance-policies-for-conditional-access)|
 |Utilizar o Azure Active Directory <!-- 1322145? --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
 |Avaliação de compatibilidade para o Windows Update para atualizações de negócio <!-- 1235390 --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |
 |Acesso de dados de ponto final de OData <!-- 1321523 --> |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|
 |Melhoramentos ao Asset Intelligence <!-- 1307390 --> |[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|
 |Os utilizadores finais podem instalar aplicações a partir do Portal da empresa <!-- 1037233? --> |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|



## <a name="see-also"></a>Consulte Também  
[Quais são as novidades no System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
 [Introdução ao System Center Configuration Manager](../../core/understand/introduction.md)
