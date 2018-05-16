---
title: Versões do Technical Preview
titleSuffix: Configuration Manager
description: Saiba mais sobre a versão de pré-visualização técnica test-drive novas funcionalidades e capacidades no Configuration Manager.
ms.date: 05/11/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a6a4faff728b14fae198f9709ca9ce9ca5d04455
ms.sourcegitcommit: 021272d5858e5dbb650b95644736d1de3dab7d8a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/15/2018
---
# <a name="technical-preview-for-system-center-configuration-manager"></a>Pré-visualização técnica do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (Technical Preview)*

**Bem-vindo ao do System Center Configuration Manager Technical Preview**. Este artigo fornece detalhes sobre a versão de pré-visualização em desenvolvimento que introduz novas funcionalidades e capacidades que estamos a trabalhar. Cada versão do technical preview introduz novas funcionalidades que não estejam incluídas no ramo atual do Configuration Manager no momento que da versão de pré-visualização técnica é disponibilizada. Estas funcionalidades poderão eventualmente ser incluídas numa atualização à versão do ramo atual, mas antes de finalizarmos as funcionalidades e de as adicionarmos, queremos que tenha a oportunidade de experimentá-las e de nos enviar os seus comentários.  

 Porque esta versão é uma versão de pré-visualização técnica, detalhes e a funcionalidade estão sujeitos a alterações.  

 Este artigo contém informações que se aplicam a todas as versões do Technical Preview. Lista também cada nova capacidade (ou funcionalidade), juntamente com a versão de pré-visualização técnica em que a capacidade aparece pela primeira vez, como a versão 1805 de Maio de 2018. Estas capacidades estão descritas nos tópicos separados dedicados para cada versão de pré-visualização.  

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
>  Quando instala uma atualização para o technical preview, atualizar a instalação de pré-visualização para essa nova versão de pré-visualização técnica. Uma instalação de pré-visualização técnica nunca inclui a opção para atualizar para uma instalação do ramo atual, nem de receber atualizações da versão atual do ramo.  

**Versões de linha de base ativas da Technical Preview:**
   
Pode instalar uma versão de linha de base para até um ano depois da versão. No entanto, quando instala um novo site de pré-visualização técnica, recomendamos que utilize a versão de linha de base mais recente que está disponível.
-  **Technical Preview 1804** -o Configuration Manager Technical Preview 1804 está disponível como uma atualização de na consola e como uma nova versão de linha de base. Transferir as versões de linha de base [do Centro de avaliação TechNet](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).


##  <a name="BKMK_TPFeedback"></a> Fornecer comentários  
 Iremos adoram ouvir os seus comentários sobre as funcionalidades no nosso pré-visualizações técnicas. Para obter mais informações, consulte [comentários sobre produtos](../understand/find-help.md#product-feedback).

Se tiver ideias sobre novas funcionalidades que gostaria de ver, queremos interessados. Para submeter novas ideias e votar nas ideias submetidas por outras pessoas, [visite a nossa página do UserVoice](http://configurationmanager.uservoice.com).  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->




##  <a name="bkmk_tpCaps"></a> Capacidades fornecidas no technical preview mais recente  
Seguem-se as capacidades fornecidas com a versão de pré-visualização técnica mais recente do Configuration Manager.  Capacidades que estavam disponíveis numa versão anterior do technical preview permanecem disponíveis nas versões posteriores. Da mesma forma, as capacidades que foram adicionadas para o ramo atual do Configuration Manager permanecerem disponíveis em versões de pré-visualização técnica.  Clique nas hiperligações para o conteúdo de cada versão de pré-visualização para saber mais sobre uma capacidade específica.  

<!-- This is the full list of new features in the latest TP release -->

### <a name="technical-preview-version-1805"></a>Pré-visualização técnica versão 1805
- [Criar uma implementação faseada fases configurados manual de uma sequência de tarefas](capabilities-in-technical-preview-1805.md#create-a-phased-deployment-with-manually-configured-phases-for-a-task-sequence) <!--1358148--> 
- [Suporte de ponto de distribuição de nuvem do Azure Resource Manager](capabilities-in-technical-preview-1805.md#cloud-distribution-point-support-for-azure-resource-manager) <!--1322209--> 
- [Executar ações com base nas informações de gestão](capabilities-in-technical-preview-1805.md#take-actions-based-on-management-insights) <!--1357930--> 
- [Transição dispositivo configuração carga de trabalho utilizando a gestão de coadministrador do Intune](capabilities-in-technical-preview-1805.md#transition-device-configuration-workload-to-intune-using-co-management) <!--1357903--> 
- [Ative pontos de distribuição para utilizar o controlo de congestionamento de rede](capabilities-in-technical-preview-1805.md#enable-distribution-points-to-use-network-congestion-control) <!--1358112--> 
- [Dashboard de gestão de nuvem](capabilities-in-technical-preview-1805.md#cloud-management-dashboard) <!--1358461--> 
- [CMPivot](capabilities-in-technical-preview-1805.md#cmpivot) <!--1358456--> 
- [Melhorado comunicações de cliente seguras](capabilities-in-technical-preview-1805.md#improved-secure-client-communications) <!--1356889,1358228,1358460--> 
- [Melhoramentos para ativar o suporte de atualização de software de terceiros](capabilities-in-technical-preview-1805.md#improvements-for-enabling-third-party-software-update-support) <!--1357605--> 
- [Melhoramentos à sequência de tarefas de atualização no local do Windows 10](capabilities-in-technical-preview-1805.md#improvements-to-windows-10-in-place-upgrade-task-sequence) <!--1358500--> 
- [CMTrace instalado com o cliente](capabilities-in-technical-preview-1805.md#cmtrace-installed-with-client) <!--1357971--> 
- [Melhoria da consola do Configuration Manager](capabilities-in-technical-preview-1805.md#improvement-to-the-configuration-manager-console) <!--1358202--> 
- [Melhoramentos a comentários de consola](capabilities-in-technical-preview-1805.md#improvements-to-console-feedback) <!--1357542--> 
- [Melhoramentos para pontos de distribuição com PXE ativado](capabilities-in-technical-preview-1805.md#improvements-to-pxe-enabled-distribution-points) <!--1357580--> 
- [Melhoria do inventário de hardware para os valores de número inteiro grande](capabilities-in-technical-preview-1805.md#improvement-to-hardware-inventory-for-large-integer-values) <!--1357880--> 
- [Melhoria da manutenção do WSUS](capabilities-in-technical-preview-1805.md#improvement-to-wsus-maintenance) <!--1357898--> 
- [Melhoria para suportar em certificados CNG](capabilities-in-technical-preview-1805.md#improvement-to-support-for-cng-certificates) <!--1357314--> 






## <a name="capabilities-delivered-in-recent-supported-technical-previews"></a>Capacidades fornecidas em pré-visualizações técnicas de suportados recentes
Seguem-se as capacidades fornecidas em versões anteriores da versão de pré-visualização técnica do Configuration Manager que ainda são suportadas. 

<!-- This is the full list of new features in the past THREE (3) TP releases. 
Each month, add features from the list above to the top of this table. 
Then remove the bottom of this list and/or move individual items not in CB to the third table below.
-->

 |Funcionalidade |Versão de pré-visualização técnica |Versão do ramo atual|  
 |----------------|---------------------|--------------------|
 | Configure uma biblioteca de conteúdos remota para o servidor do site <!--1357525--> | [Pré-visualização do técnico 1804](capabilities-in-technical-preview-1804.md#configure-a-remote-content-library-for-the-site-server)  | ![Não foi adicionada](media/Red_X.gif) | 
 | Submeter comentários sobre a partir da consola do Configuration Manager <!--1357542--> | [Pré-visualização do técnico 1804](capabilities-in-technical-preview-1804.md#bkmk_feedback)  | ![Não foi adicionada](media/Red_X.gif) | 
 | Centro de suporte <!--1357489--> | [Pré-visualização do técnico 1804](capabilities-in-technical-preview-1804.md#support-center)  | ![Não foi adicionada](media/Red_X.gif) | 
 | Toolkit do Configuration Manager <!--1357145--> | [Pré-visualização do técnico 1804](capabilities-in-technical-preview-1804.md#configuration-manager-toolkit)  | ![Não foi adicionada](media/Red_X.gif) | 
 | Desinstalar a aplicação na revogação de aprovação <!--1357891--> | [Pré-visualização do técnico 1804](capabilities-in-technical-preview-1804.md#uninstall-application-on-approval-revocation)  | ![Não foi adicionada](media/Red_X.gif) | 
 | Excluir os contentores do Active Directory da deteção <!--1358143--> | [Pré-visualização do técnico 1804](capabilities-in-technical-preview-1804.md#exclude-active-directory-containers-from-discovery)  | ![Não foi adicionada](media/Red_X.gif) | 
 | Especifique a visibilidade da ligação de Web site do catálogo de aplicações no Centro de Software <!--1358214--> | [Pré-visualização do técnico 1804](capabilities-in-technical-preview-1804.md#specify-the-visibility-of-the-application-catalog-website-link-in-software-center)  | ![Não foi adicionada](media/Red_X.gif) | 
 | Regras de implementação automática pela arquitetura de atualização de software de filtro <!--1322266--> | [Pré-visualização do técnico 1804](capabilities-in-technical-preview-1804.md#filter-automatic-deployment-rules-by-software-update-architecture)  | ![Não foi adicionada](media/Red_X.gif) | 
 | Melhorias para implementação do SO <!--1358330,1358493--> | [Pré-visualização do técnico 1804](capabilities-in-technical-preview-1804.md#improvements-to-os-deployment) | ![Não foi adicionada](media/Red_X.gif) | 
 | Distribuição de solicitação os pontos de distribuição da nuvem de suporte de pontos como origem <!--1321554--> | [Pré-visualização do técnico 1803](capabilities-in-technical-preview-1803.md#pull-distribution-points-support-cloud-distribution-points-as-source)  | ![Não foi adicionada](media/Red_X.gif) | 
 | Suporte de transferência parcial na cache ponto a ponto do cliente para reduzir a utilização de WAN <!--1357346--> | [Pré-visualização do técnico 1803](capabilities-in-technical-preview-1803.md#partial-download-support-in-client-peer-cache-to-reduce-wan-utilization)  | ![Não foi adicionada](media/Red_X.gif) | 
 | Janelas de manutenção no Centro de Software <!--1358131--> | [Pré-visualização do técnico 1803](capabilities-in-technical-preview-1803.md#maintenance-windows-in-software-center)  | ![Não foi adicionada](media/Red_X.gif) | 
 | Separador personalizado para a página Web no Centro de Software <!--1358132--> | [Pré-visualização do técnico 1803](capabilities-in-technical-preview-1803.md#custom-tab-for-webpage-in-software-center)  | ![Não foi adicionada](media/Red_X.gif) | 
 | Ativar o suporte de atualização de software de terceiros em clientes <!--1357605--> | [Pré-visualização do técnico 1803](capabilities-in-technical-preview-1803.md#enable-third-party-software-update-support-on-clients)  | ![Não foi adicionada](media/Red_X.gif) | 
 | Permitir copiar/colar de detalhes do ativo de vistas de monitorização <!--1357552--> | [Pré-visualização do técnico 1803](capabilities-in-technical-preview-1803.md#enable-copypaste-of-asset-details-from-monitoring-views)  | ![Não foi adicionada](media/Red_X.gif) | 
 | Extensões SCAP <!--1357552--> | [Pré-visualização do técnico 1803](capabilities-in-technical-preview-1803.md#scap-extensions)  | ![Não foi adicionada](media/Red_X.gif) | 
 | Carga de trabalho de proteção de ponto final de transição para o Intune utilizando a gestão de conjunta <!-- 1357365 --> | [Pré-visualização do técnico 1802](capabilities-in-technical-preview-1802.md#transition-endpoint-protection-workload-to-intune-using-co-management) | [Versão 1802](/sccm/core/clients/manage/co-management-switch-workloads#workloads-able-to-be-transitioned-to-intune) |  
 | Configurar a otimização de entrega do Windows para utilizar grupos de limites do Configuration Manager <!-- 1324696 --> | [Pré-visualização do técnico 1802](capabilities-in-technical-preview-1802.md#configure-windows-delivery-optimization-to-use-configuration-manager-boundary-groups) | [Versão 1802](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#delivery-optimization) |  
 | Sequência de tarefas de atualização no local do Windows 10 através do gateway de gestão de nuvem <!-- 1357149 --> | [Pré-visualização do técnico 1802](capabilities-in-technical-preview-1802.md#windows-10-in-place-upgrade-task-sequence-via-cloud-management-gateway) | [Versão 1802](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#deploy-windows-10-in-place-upgrade-via-cmg) |  
 | Melhoramentos à sequência de tarefas de atualização no local do Windows 10 <!-- 1357425 --> | [Pré-visualização do técnico 1802](capabilities-in-technical-preview-1802.md#improvements-to-windows-10-in-place-upgrade-task-sequence) | [Versão 1802](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system) |  
 | Melhoramentos para pontos de distribuição com PXE ativado <!-- 1357580 --> | [Pré-visualização do técnico 1802](capabilities-in-technical-preview-1802.md#improvements-to-pxe-enabled-distribution-points) | ![Não foi adicionada](media/Red_X.gif) | 
 | Modelos de implementação para sequências de tarefas <!-- 1357391 --> | [Pré-visualização do técnico 1802](capabilities-in-technical-preview-1802.md#deployment-templates-for-task-sequences) | [Versão 1802](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS) |  
 | Dashboard de ciclo de vida do produto <!--1319632 --> | [Pré-visualização do técnico 1802](capabilities-in-technical-preview-1802.md#product-lifecycle-dashboard) | ![Não foi adicionada](media/Red_X.gif) | 
 | Melhoramentos aos relatórios <!--1357653 --> | [Pré-visualização do técnico 1802](capabilities-in-technical-preview-1802.md#improvements-to-reporting) | [Versão 1802](/sccm/core/servers/manage/list-of-reports#operating-system) |  
 | Melhoramentos ao centro de Software <!--1357592 --> | [Pré-visualização do técnico 1802](capabilities-in-technical-preview-1802.md#improvements-to-software-center) | [Versão 1802](/sccm/core/clients/deploy/about-client-settings#BKMK_HideInstalled) |  
 | Grupo de limites contingência para pontos de gestão <!-- 1324594 --> | [Pré-visualização do técnico 1802](capabilities-in-technical-preview-1802.md#boundary-group-fallback-for-management-points) | [Versão 1802](/sccm/core/servers/deploy/configure/boundary-groups#management-points) |  
 | Suporte melhorado para certificados CNG <!-- 1357314 --> | [Pré-visualização do técnico 1802](capabilities-in-technical-preview-1802.md#improved-support-for-cng-certificates) | [Versão 1802](/sccm/core/plan-design/network/cng-certificates-overview) |  
 | Suporte de gateway de gestão de nuvem do Azure Resource Manager <!-- 1324735 --> | [Pré-visualização do técnico 1802](capabilities-in-technical-preview-1802.md#cloud-management-gateway-support-for-azure-resource-manager) | [Versão 1802](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager) |  
 | Aprovar pedidos de aplicações para os utilizadores por dispositivo <!-- 1357015 --> | [Pré-visualização do técnico 1802](capabilities-in-technical-preview-1802.md#approve-application-requests-for-users-per-device) | [Versão 1802](/sccm/apps/deploy-use/deploy-applications#specify-deployment-settings) |  
 | Utilizar o Centro de Software para procurar e instalar aplicações disponíveis ao utilizador no Azure AD-dispositivos associados a um <!-- 1322613 --> | [Pré-visualização do técnico 1802](capabilities-in-technical-preview-1802.md#use-software-center-to-browse-and-install-user-available-applications-on-azure-ad-joined-devices) | [Versão 1802](/sccm/apps/deploy-use/deploy-applications#deploy-user-available-applications-on-azure-ad-joined-devices) |  
 | Relatório sobre as informações do dispositivo Windows AutoPilot <!-- 1351442 --> | [Pré-visualização do técnico 1802](capabilities-in-technical-preview-1802.md#report-on-windows-autopilot-device-information) | [Versão 1802](/sccm/core/clients/manage/co-management-prepare#new-windows-10-devices) |  
 | Melhoramentos às políticas do Configuration Manager para o Windows Defender exploram proteção <!-- 1356220 --> | [Pré-visualização do técnico 1802](capabilities-in-technical-preview-1802.md#improvements-to-configuration-manager-policies-for-windows-defender-exploit-guard) | [Versão 1802](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) |  
 | Políticas de browser Microsoft Edge <!-- 1357310 --> | [Pré-visualização do técnico 1802](capabilities-in-technical-preview-1802.md#microsoft-edge-browser-policies) | [Versão 1802](/sccm/compliance/deploy-use/browser-profiles) | 
 | Relatório de contagens de browser predefinido <!-- 1357830 --> | [Pré-visualização do técnico 1802](capabilities-in-technical-preview-1802.md#report-for-default-browser-counts) | [Versão 1802](/sccm/core/servers/manage/list-of-reports#software---companies-and-products) | 
 | Suporte para dispositivos Windows 10 ARM64 <!-- 1353704 --> | [Pré-visualização do técnico 1802](capabilities-in-technical-preview-1802.md#support-for-windows-10-arm64-devices) | [Versão 1802](/sccm/core/plan-design/configs/support-for-windows-10) |  
 
  

## <a name="capabilities-delivered-in-previous-technical-previews"></a>Capacidades fornecidas em pré-visualizações técnicas anteriores
Seguem-se as capacidades específicas fornecidas com versões anteriores da versão de pré-visualização técnica do Configuration Manager. Estas capacidades permanecem disponíveis nas versões posteriores, mas ainda não estão disponíveis na versão atual do ramo. 

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

 |Funcionalidade |Versão de pré-visualização técnica |  
 |----------------|---------------------|
 | Serviço baseado em clientes de dispositivo de resposta PXE <!-- 1357148 --> | [Pré-visualização do técnico 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
 |Disponibilidade elevada de função do servidor de site <!-- 1128774 --> |[Pré-visualização do técnico 1706](capabilities-in-technical-preview-1706.md#site-server-role-high-availability) |
 |Suporte de arranque de rede do PXE para IPv6 <!-- 1269793 --> |[Pré-visualização do técnico 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
 |Utilizar o Azure Active Directory <!-- 1322145? --> | [Pré-visualização do técnico 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
 |Avaliação de compatibilidade para o Windows Update para atualizações de negócio <!-- 1235390 --> | [Pré-visualização do técnico 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |
 |Acesso de dados de ponto final de OData <!-- 1321523 --> |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|
 |Melhoramentos ao Asset Intelligence <!-- 1307390 --> |[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|
 |Os utilizadores finais podem instalar aplicações a partir do Portal da empresa <!-- 1037233? --> |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|



## <a name="see-also"></a>Consulte Também  
[Quais são as novidades no System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
 [Introdução ao System Center Configuration Manager](../../core/understand/introduction.md)

> [!Tip]  
> Para mais informações sobre as funcionalidades de sucursais atuais que necessitam de consentimento para ativar, consulte [funcionalidades de pré-lançamento](/sccm/core/servers/manage/pre-release-features).  
> Para obter mais informações sobre as funcionalidades de sucursais atuais que tem de ativar primeiro, consulte [ativar funcionalidades opcionais de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  

