---
title: "Versões do Technical Preview"
titleSuffix: Configuration Manager
description: "Saiba mais sobre a versão de pré-visualização técnica que permite-lhe test-drive novas funcionalidades e capacidades no System Center Configuration Manager."
ms.custom: na
ms.date: 12/22/2017
ms.prod: configuration-manager
ms.reviewer: nab
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
caps.latest.revision: "157"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 692cf74cbae3f176bab254aeec0e63c10929cfcc
ms.sourcegitcommit: ca9d15dfb1c9eb47ee27ea9b5b39c9f8cdcc0748
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/04/2018
---
# <a name="technical-preview-for-system-center-configuration-manager"></a>Technical Preview do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (Technical Preview)*

**Bem-vindo ao do System Center Configuration Manager Technical Preview**. Este artigo fornece detalhes sobre a versão de pré-visualização em desenvolvimento que introduz novas funcionalidades e capacidades que estamos a trabalhar. Cada versão do technical preview introduz novas funcionalidades que não estejam incluídas no ramo atual do Configuration Manager no momento que da versão de pré-visualização técnica é disponibilizada. Estas funcionalidades poderão eventualmente ser incluídas numa atualização à versão do ramo atual, mas antes de finalizarmos as funcionalidades e de as adicionarmos, queremos que tenha a oportunidade de experimentá-las e de nos enviar os seus comentários.  

 Como se trata de uma versão de pré-visualização técnica, os detalhes e a funcionalidade estão sujeitos a alterações.  

 Este artigo contém informações que se aplicam a todas as versões do Technical Preview. Lista também cada nova capacidade (ou funcionalidade), juntamente com a versão de pré-visualização técnica em que a capacidade aparece pela primeira vez, como a versão 1712 para Dezembro de 2017. Estas capacidades estão descritas nos tópicos separados dedicados para cada versão de pré-visualização.  

 Para obter informações sobre quais são as novidades no ramo atual do Configuration Manager, consulte [que há de novo no System Center Configuration Manager](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012).



##  <a name="bkmk_reqs"></a> Requisitos e limitações do Technical Preview  

> [!IMPORTANT]     
>  A Technical Preview está licenciada para ser utilizada apenas num ambiente de laboratório.  A Microsoft poderá não fornecer serviços de suporte e determinadas funcionalidades poderão não estar disponíveis no software da Preview. Além disso, o software de pré-visualização, poderá ter reduzida ou padrões diferentes de segurança, privacidade, acessibilidade, disponibilidade e fiabilidade relativa comercialmente fornecidos software.  

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

-   Não existe suporte para atualizar para uma compilação de produção (ramo atual) a partir desta preview build. No entanto, quando as atualizações estiverem disponíveis para uma versão de pré-visualização, pode encontrar e instalá-los a partir de **atualizações e manutenção** nós da consola do Configuration Manager. Para ver um vídeo do processo de atualização na consola, veja [Installing ConfigMgr Update Packages](https://www.youtube.com/embed/KBd_EGFbUT8) (Instalar Pacotes de Atualização do ConfigMgr) em youtube.com.  
-   Apenas é suportado um site primário autónomo. Não existe suporte para um site de administração central, múltiplos sites primários ou sites secundários.  

Os produtos e tecnologias que se seguem são suportadas por este ramo do Configuration Manager. No entanto, a sua inclusão neste conteúdo não implica uma extensão de suporte para um produto ou a versão que está fora individual do produto vida de suporte. Os produtos que estejam fora do respetivo ciclo de vida de suporte não são suportados para utilização com o Configuration Manager. Para mais informações sobre os Ciclos de Vida do Suporte da Microsoft, aceda ao site [Ciclo de Vida do Suporte da Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=208270) .  

-   Apenas são suportadas as seguintes versões do SQL Server:  

    -   SQL Server 2016 (sem Service Pack e posterior)
    -   SQL Server 2014 (com Service Pack 1 e posterior)
    -   SQL Server 2012 (com Service Pack 3, ou posterior)


-   O site suporta até 10 clientes, tem de executar uma das seguintes versões do Windows:  

      -   Windows 10  
      -   Windows 8,1  
      -   Windows 8  
      -   Windows 7  

##  <a name="bkmk_install"></a> Instalar e atualizar o Technical Preview  
 O System Center Configuration Manager Technical Preview é distinto da versão atual do System Center Configuration Manager.  

 Para utilizar a pré-visualização técnica, primeiro tem de instalar um **versão de linha** da versão de pré-visualização técnica. Depois de instalar uma versão de linha de base, pode então utilizar as **atualizações na consola** para atualizar a sua instalação com a versão de pré-visualização mais recente. Normalmente, existem novas versões mensais da Technical Preview.

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




##  <a name="bkmk_tpCaps"></a>Capacidades fornecidas no technical preview mais recente  
Seguem-se as capacidades fornecidas com a versão de pré-visualização técnica mais recente do Configuration Manager.  Capacidades que estavam disponíveis numa versão anterior do technical preview permanecem disponíveis nas versões posteriores. Da mesma forma, as capacidades que foram adicionadas para o ramo atual do Configuration Manager permanecerem disponíveis em versões de pré-visualização técnica.  Clique nas hiperligações para o conteúdo de cada versão de pré-visualização para saber mais sobre uma capacidade específica.  

<!-- This is the full list of new features in the latest TP release -->

### <a name="technical-preview-version-1712"></a>Pré-visualização técnica versão 1712
- [Não atualizar automaticamente as aplicações substituídas](capabilities-in-technical-preview-1712.md#do-not-automatically-upgrade-superseded-applications)<!-- 1351266 --> 
- [Instalar várias aplicações no Centro de Software](capabilities-in-technical-preview-1712.md#install-multiple-applications-in-software-center)<!-- 1357126 --> 
- [Alteração no cliente do Configuration Manager instalar](capabilities-in-technical-preview-1712.md#change-in-the-configuration-manager-client-install)<!-- 1356195 --> 
- [Mude para o dashboard de dispositivo superfície](capabilities-in-technical-preview-1712.md#change-to-the-surface-device-dashboard)<!-- 1355788 --> 
- [Melhoramentos ao dashboard de gestão de clientes do Office 365](capabilities-in-technical-preview-1712.md#improvements-to-office-365-client-management-dashboard)<!-- 1357281 --> 
- [Melhorias à consola do Configuration Manager](capabilities-in-technical-preview-1712.md#improvements-to-the-configuration-manager-console)<!-- 1357280,1357282 --> 
- [Melhorias para implementação do sistema operativo](capabilities-in-technical-preview-1712.md#improvements-to-operating-system-deployment)<!-- SMS 500897 --> 
- [Integração de aplicações do Hub de comentários do Windows 10](capabilities-in-technical-preview-1712.md#windows-10-feedback-hub-app-integration)<!-- NA -->




## <a name="capabilities-delivered-in-recent-supported-technical-previews"></a>Capacidades fornecidas em pré-visualizações técnicas de suportados recentes
Seguem-se as capacidades fornecidas em versões anteriores da versão de pré-visualização técnica do Configuration Manager que ainda são suportadas. 

<!-- This is the full list of new features in the past three TP releases. Each month, add features from the list above to the top of this table. Then remove the bottom of this list (and/or move individual items not in CB to the third table below). -->

 |Funcionalidade |Versão de pré-visualização técnica |Versão do ramo atual|  
 |----------------|---------------------|--------------------|
 |Executar o passo de sequência de tarefas<!-- 1261338 --> | [Pré-visualização do técnico 1711](capabilities-in-technical-preview-1711.md) |[Versão 1710](/sccm/osd/understand/task-sequence-steps#child-task-sequence)    |
 |Permitir interação do utilizador quando instalar uma aplicação<!-- 1356976 --> | [Pré-visualização do técnico 1711](capabilities-in-technical-preview-1711.md) |![Não foi adicionada](media/Red_X.gif)    |
 |Windows 10 telemetria para o estado de funcionamento de dispositivo de análise de Windows<!--1356148 --> | [Pré-visualização do técnico 1710](capabilities-in-technical-preview-1710.md#limit-windows-10-enhanced-telemetry-to-only-send-data-relevant-to-windows-analytics-device-health) |[Versão 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710#reporting)    |
 |Melhoramentos para os ícones de centro de Software<!-- 1356194 --> | [Pré-visualização do técnico 1710](capabilities-in-technical-preview-1710.md#software-center-no-longer-distorts-icons-larger-than-250x250) |[Versão 1710](/sccm/apps/plan-design/plan-for-and-configure-application-management#supplemental-procedures-to-install-and-configure-the-application-catalog-and-software-center)    |
 |Verificação de conformidade do Centro de Software para dispositivos geridos conjuntamente<!-- 1356374 -->|[Pré-visualização do técnico 1710](capabilities-in-technical-preview-1710.md#check-compliance-from-software-center-for-co-managed-devices)|[Versão 1710](/sccm/core/clients/manage/co-management-overview)    |
 |Suporte limitado para certificados CNG<!-- 1356191 -->| [Pré-visualização do técnico 1710](capabilities-in-technical-preview-1710.md#limited-support-for-cng-certificates)|[Versão 1710](/sccm/core/plan-design/network/cng-certificates-overview)    |
 |Suporte para proteção de exploração<!--1355468 --> | [Pré-visualização do técnico 1710](capabilities-in-technical-preview-1710.md#support-for-exploit-guard) |[Versão 1710](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy)    |
 |Descrições melhoradas para pendentes reinícios de computador<!-- 1356283  -->| [Pré-visualização do técnico 1710](capabilities-in-technical-preview-1710.md)|[Versão 1710](/sccm/core/clients/manage/manage-clients)    |
 |Alterações de política de proteção de dispositivos<!-- 1355092  -->| [Pré-visualização do técnico 1710](capabilities-in-technical-preview-1710.md)|[Versão 1710](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)    |
 |Configurar e implementar políticas de proteção de aplicações do Windows Defender<!-- 1351960  -->| [Pré-visualização do técnico 1710](capabilities-in-technical-preview-1710.md)|[Versão 1710](/sccm/protect/deploy-use/create-deploy-application-guard-policy)    |
 |Melhoramentos para a implementação de scripts do PowerShell do Configuration Manager<!-- 1236459 -->| [Pré-visualização do técnico 1710](capabilities-in-technical-preview-1710.md#improvements-for-deploying-powershell-scripts-from-configuration-manager) | [Versão 1710](/sccm/apps/deploy-use/create-deploy-scripts)
 |Experiência de perfil VPN melhorada na consola do Configuration Manager<!-- 1313282 --> | [Pré-visualização do técnico 1709](capabilities-in-technical-preview-1709.md) |[Versão 1710](/sccm/protect/deploy-use/create-vpn-profiles)    |
 |Gestão conjunta para dispositivos Windows 10|[Pré-visualização do técnico 1709](capabilities-in-technical-preview-1709.md#co-management-for-windows-10-devices)|[Versão 1710](/sccm/core/clients/manage/co-management-overview.md)|
 

## <a name="capabilities-delivered-in-previous-technical-previews"></a>Capacidades fornecidas em pré-visualizações técnicas anteriores
Seguem-se as capacidades específicas fornecidas com versões anteriores da versão de pré-visualização técnica do Configuration Manager. Estas capacidades permanecem disponíveis nas versões posteriores, mas ainda não estão disponíveis na versão atual do ramo. 

<!-- This is the list of individual features that are still in TP (not in CB). Note there is no third column in this table! Each month review and remove from this list for anything that's now available in CB. Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column) -->

 |Funcionalidade |Versão de pré-visualização técnica |  
 |----------------|---------------------|
 |Informações de gestão<!-- 1353967 --> |[Pré-visualização do técnico 1708](capabilities-in-technical-preview-1708.md#management-insights)|
 |Dashboard de dispositivo superfície<!-- 1355788 --> |[Pré-visualização do técnico 1707](capabilities-in-technical-preview-1707.md#surface-device-dashboard)|
 |Disponibilidade elevada de função do servidor de site<!-- 1128774 --> |[Pré-visualização do técnico 1706](capabilities-in-technical-preview-1706.md#site-server-role-high-availability) |
 |Suporte de arranque de rede do PXE para IPv6<!-- 1269793 --> |[Pré-visualização do técnico 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
 |Avaliação de atestado de estado de funcionamento do dispositivo para as políticas de conformidade de acesso condicional<!-- 1235616 -->|[Pré-visualização do técnico 1706](capabilities-in-technical-preview-1706.md#device-health-attestation-assessment-for-compliance-policies-for-conditional-access)|
 |Utilizar o Azure Active Directory<!-- 1322145? --> | [Pré-visualização do técnico 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
 |Avaliação de compatibilidade para o Windows Update para atualizações de negócio<!-- 1235390 --> | [Pré-visualização do técnico 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |
 |Acesso de dados de ponto final de OData<!-- 1321523 --> |[Pré-visualização do técnico 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|
 |Melhoramentos ao Asset Intelligence<!-- 1307390 --> |[Pré-visualização do técnico 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|
 |Os utilizadores finais podem instalar aplicações a partir do Portal da empresa<!-- 1037233? --> |[Pré-visualização do técnico 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|





## <a name="see-also"></a>Consulte Também  
[Quais são as novidades no System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
 [Introdução ao System Center Configuration Manager](../../core/understand/introduction.md)
