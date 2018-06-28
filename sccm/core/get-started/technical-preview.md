---
title: Versões do Technical Preview
titleSuffix: Configuration Manager
description: Saiba mais sobre a versão de pré-visualização técnica test-drive novas funcionalidades e capacidades no Configuration Manager.
ms.date: 06/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1fd848c3e0ed663e0731eb86d39c930db3af7819
ms.sourcegitcommit: d1bf26bcf0d78b37ac7598fab36eb58ca69b1dc5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 06/28/2018
ms.locfileid: "37066288"
---
# <a name="technical-preview-for-system-center-configuration-manager"></a>Pré-visualização técnica do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (Technical Preview)*

**Bem-vindo ao do System Center Configuration Manager Technical Preview**. Este artigo fornece detalhes sobre a versão de pré-visualização em desenvolvimento que introduz novas funcionalidades e capacidades que estamos a trabalhar. Cada versão do technical preview introduz novas funcionalidades que não estejam incluídas no ramo atual do Configuration Manager no momento que da versão de pré-visualização técnica é disponibilizada. Estas funcionalidades poderão eventualmente ser incluídas numa atualização à versão do ramo atual, mas antes de finalizarmos as funcionalidades e de as adicionarmos, queremos que tenha a oportunidade de experimentá-las e de nos enviar os seus comentários.  

 Porque esta versão é uma versão de pré-visualização técnica, detalhes e a funcionalidade estão sujeitos a alterações.  

 Este artigo contém informações que se aplicam a todas as versões do Technical Preview. Lista também cada nova capacidade (ou funcionalidade), juntamente com a versão de pré-visualização técnica em que a capacidade aparece pela primeira vez, como a versão 1806 para Junho de 2018. Estas capacidades estão descritas nos tópicos separados dedicados para cada versão de pré-visualização.  

 Para obter informações sobre quais são as novidades no ramo atual do Configuration Manager, consulte [que há de novo no System Center Configuration Manager](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012).



##  <a name="bkmk_reqs"></a> Requisitos e limitações do Technical Preview  

> [!IMPORTANT]     
>  A Technical Preview está licenciada para ser utilizada apenas num ambiente de laboratório. A Microsoft poderá não fornecer serviços de suporte e algumas funcionalidades poderão não estar disponíveis no software de pré-visualização. Além disso, o software de pré-visualização, poderá ter reduzida ou padrões diferentes de segurança, privacidade, acessibilidade, disponibilidade e fiabilidade relativa comercialmente fornecidos software.  

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

Os produtos e tecnologias que se seguem são suportadas por este ramo do Configuration Manager. No entanto, a sua inclusão neste conteúdo não implica uma extensão de suporte para um produto ou a versão que está fora individual do produto vida de suporte. Os produtos que estejam fora do respetivo ciclo de vida de suporte não são suportados para utilização com o Configuration Manager. Para obter mais informações sobre ciclos de vida de suporte de Microsoft, visite o [ciclo de vida de suporte de Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=208270) Web site.  

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
-  **Technical Preview 1806** -o Configuration Manager Technical Preview 1806 está disponível como uma atualização de na consola e como uma nova versão de linha de base. Transferir as versões de linha de base [do Centro de avaliação TechNet](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).


##  <a name="BKMK_TPFeedback"></a> Fornecer comentários  
 Iremos adoram ouvir os seus comentários sobre as funcionalidades no nosso pré-visualizações técnicas. Para obter mais informações, consulte [comentários sobre produtos](../understand/find-help.md#product-feedback).

Se tiver ideias sobre novas funcionalidades que gostaria de ver, queremos interessados. Para submeter novas ideias e votar nas ideias submetidas por outras pessoas, [visite a nossa página do UserVoice](https://configurationmanager.uservoice.com).  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->




##  <a name="bkmk_tpCaps"></a> Capacidades fornecidas no technical preview mais recente  
Seguem-se as capacidades fornecidas com a versão de pré-visualização técnica mais recente do Configuration Manager. Capacidades que estavam disponíveis numa versão anterior do technical preview permanecem disponíveis nas versões posteriores. Da mesma forma, as capacidades que foram adicionadas para o ramo atual do Configuration Manager permanecerem disponíveis em versões de pré-visualização técnica. Clique nas hiperligações para o conteúdo de cada versão de pré-visualização para saber mais sobre uma capacidade específica.  

<!-- This is the full list of new features in the latest TP release -->

### <a name="technical-preview-version-18062"></a>Pré-visualização técnica versão 1806.2
- [Melhoramentos às implementações faseadas](capabilities-in-technical-preview-1806-2.md#bkmk_pod) <!--1358577,1358147,1358578-->
- [Suporte para formatos de pacote de aplicação do novo Windows](capabilities-in-technical-preview-1806-2.md#bkmk_msix) <!--1357427-->
- [Melhoramento de segurança de push de cliente](capabilities-in-technical-preview-1806-2.md#bkmk_client-push) <!--1358204-->
- [Informações de gestão para uma manutenção pró-ativa](capabilities-in-technical-preview-1806-2.md#bkmk_insights) <!--1352184,et al-->
- [Carga de trabalho de aplicações móveis de transição para dispositivos geridos conjuntamente](capabilities-in-technical-preview-1806-2.md#bkmk_comgmt) <!--1357892-->
- [Opções do grupo de limites para transferências de elemento](capabilities-in-technical-preview-1806-2.md#bkmk_bgoptions) <!--1356193-->
- [Suporte para catálogos personalizados de atualizações de software de terceiros](capabilities-in-technical-preview-1806-2.md#bkmk_3pupdate) <!--1358714-->
- [Melhoramentos às funcionalidades de gestão de nuvem](capabilities-in-technical-preview-1806-2.md#bkmk_cloud) <!--511980,515854-->
- [Novo relatório de compatibilidade de atualizações de software](capabilities-in-technical-preview-1806-2.md#bkmk_report) <!--1357775-->



## <a name="capabilities-delivered-in-recent-supported-technical-previews"></a>Capacidades fornecidas em pré-visualizações técnicas de suportados recentes
Seguem-se as capacidades fornecidas em versões anteriores da versão de pré-visualização técnica do Configuration Manager que ainda são suportadas. 

<!-- This is the full list of new features in the past THREE (3) TP releases. 
Each month, add features from the list above to the top of this table. 
Then remove the bottom of this list and/or move individual items not in CB to the third table below.
-->

 |Funcionalidade |Versão de pré-visualização técnica |Versão do ramo atual|  
 |----------------|---------------------|--------------------|
 | Atualizações de software de terceiros <!--1352101--> | [Pré-visualização do técnico 1806](capabilities-in-technical-preview-1806.md#bkmk-3pupdate)  | ![Não foi adicionada](media/Red_X.gif) |  
 | Configurar as definições do Windows Defender SmartScreen para Microsoft Edge <!--1353701--> | [Pré-visualização do técnico 1806](capabilities-in-technical-preview-1806.md#configure-windows-defender-smartscreen-settings-for-microsoft-edge)  | ![Não foi adicionada](media/Red_X.gif) |  
 | Política MDM de sincronização do Microsoft Intune para um dispositivo gerido conjuntamente <!--1357377--> | [Pré-visualização do técnico 1806](capabilities-in-technical-preview-1806.md#sync-mdm-policy-from-microsoft-intune-for-a-co-managed-device)  | ![Não foi adicionada](media/Red_X.gif) |  
 | Transição do Office 365 carga de trabalho utilizando a gestão de coadministrador do Intune <!--1357841--> | [Pré-visualização do técnico 1806](capabilities-in-technical-preview-1806.md#transition-office-365-workload-to-intune-using-co-management)  | ![Não foi adicionada](media/Red_X.gif) |  
 | Gestor de conversão de pacotes <!--1357861--> | [Pré-visualização do técnico 1806](capabilities-in-technical-preview-1806.md#package-conversion-manager)  | ![Não foi adicionada](media/Red_X.gif) |  
 | Implementar atualizações de software sem conteúdo <!--1357933--> | [Pré-visualização do técnico 1806](capabilities-in-technical-preview-1806.md#deploy-software-updates-without-content)  | ![Não foi adicionada](media/Red_X.gif) |  
 | Integração de ferramenta de personalização do Office com o instalador do Office 365 <!--1358149--> | [Pré-visualização do técnico 1806](capabilities-in-technical-preview-1806.md#office-customization-tool-integration-with-the-office-365-installer)  | ![Não foi adicionada](media/Red_X.gif) |  
 | Melhoramentos ao gateway de gestão de nuvem <!--1358215,1358651,503899--> | [Pré-visualização do técnico 1806](capabilities-in-technical-preview-1806.md#improvements-to-cloud-management-gateway)   | ![Não foi adicionada](media/Red_X.gif) |  
 | Melhoramentos para proteger as comunicações de cliente <!--1358278,1358279--> | [Pré-visualização do técnico 1806](capabilities-in-technical-preview-1806.md#improvements-to-secure-client-communications)  | ![Não foi adicionada](media/Red_X.gif) |  
 | Melhorias na infraestrutura de centro de software <!--1358309--> | [Pré-visualização do técnico 1806](capabilities-in-technical-preview-1806.md#software-center-infrastructure-improvements)  | ![Não foi adicionada](media/Red_X.gif) |  
 | Aprovisionar pacotes de aplicações do Windows para todos os utilizadores num dispositivo <!--1358310--> | [Pré-visualização do técnico 1806](capabilities-in-technical-preview-1806.md#provision-windows-app-packages-for-all-users-on-a-device)  | ![Não foi adicionada](media/Red_X.gif) |  
 | Melhoramentos ao dashboard superfície <!--1358654--> | [Pré-visualização do técnico 1806](capabilities-in-technical-preview-1806.md#improvements-to-the-surface-dashboard)  | ![Não foi adicionada](media/Red_X.gif) |  
 | Revisão de unidade da predefinição de inventário de hardware <!--514442--> | [Pré-visualização do técnico 1806](capabilities-in-technical-preview-1806.md#hardware-inventory-default-unit-revision)  | ![Não foi adicionada](media/Red_X.gif) |  
 | Criar uma implementação faseada fases configurados manual de uma sequência de tarefas <!--1358148--> | [Pré-visualização do técnico 1805](capabilities-in-technical-preview-1805.md#create-a-phased-deployment-with-manually-configured-phases-for-a-task-sequence)  | ![Não foi adicionada](media/Red_X.gif) |  
 | Suporte de ponto de distribuição de nuvem do Azure Resource Manager <!--1322209--> | [Pré-visualização do técnico 1805](capabilities-in-technical-preview-1805.md#cloud-distribution-point-support-for-azure-resource-manager)  | ![Não foi adicionada](media/Red_X.gif) |  
 | Executar ações com base nas informações de gestão <!--1357930--> | [Pré-visualização do técnico 1805](capabilities-in-technical-preview-1805.md#take-actions-based-on-management-insights)  | ![Não foi adicionada](media/Red_X.gif) |  
 | Transição dispositivo configuração carga de trabalho utilizando a gestão de coadministrador do Intune <!--1357903--> | [Pré-visualização do técnico 1805](capabilities-in-technical-preview-1805.md#transition-device-configuration-workload-to-intune-using-co-management)  | ![Não foi adicionada](media/Red_X.gif) |  
 | Ative pontos de distribuição para utilizar o controlo de congestionamento de rede <!--1358112--> | [Pré-visualização do técnico 1805](capabilities-in-technical-preview-1805.md#enable-distribution-points-to-use-network-congestion-control)  | ![Não foi adicionada](media/Red_X.gif) |  
 | Dashboard de gestão de nuvem <!--1358461--> | [Pré-visualização do técnico 1805](capabilities-in-technical-preview-1805.md#cloud-management-dashboard)  | ![Não foi adicionada](media/Red_X.gif) |  
 | CMPivot <!--1358456--> | [Pré-visualização do técnico 1805](capabilities-in-technical-preview-1805.md#cmpivot)  | ![Não foi adicionada](media/Red_X.gif) |  
 | Melhorado comunicações de cliente seguras <!--1356889,1358228,1358460--> | [Pré-visualização do técnico 1805](capabilities-in-technical-preview-1805.md#improved-secure-client-communications)  | ![Não foi adicionada](media/Red_X.gif) |  
 | Melhoramentos para ativar o suporte de atualização de software de terceiros <!--1357605--> | [Pré-visualização do técnico 1805](capabilities-in-technical-preview-1805.md#improvements-for-enabling-third-party-software-update-support)  | ![Não foi adicionada](media/Red_X.gif) |  
 | Melhoramentos à sequência de tarefas de atualização no local do Windows 10 <!--1358500--> | [Pré-visualização do técnico 1805](capabilities-in-technical-preview-1805.md#improvements-to-windows-10-in-place-upgrade-task-sequence)  | ![Não foi adicionada](media/Red_X.gif) |  
 | CMTrace instalado com o cliente <!--1357971--> | [Pré-visualização do técnico 1805](capabilities-in-technical-preview-1805.md#cmtrace-installed-with-client)  | ![Não foi adicionada](media/Red_X.gif) |  
 | Melhoria da consola do Configuration Manager <!--1358202--> | [Pré-visualização do técnico 1805](capabilities-in-technical-preview-1805.md#improvement-to-the-configuration-manager-console)  | ![Não foi adicionada](media/Red_X.gif) |  
 | Melhoramentos a comentários de consola <!--1357542--> | [Pré-visualização do técnico 1805](capabilities-in-technical-preview-1805.md#improvements-to-console-feedback)  | ![Não foi adicionada](media/Red_X.gif) |  
 | Melhoramentos para pontos de distribuição com PXE ativado <!--1357580--> | [Pré-visualização do técnico 1805](capabilities-in-technical-preview-1805.md#improvements-to-pxe-enabled-distribution-points)  | ![Não foi adicionada](media/Red_X.gif) |  
 | Melhoria do inventário de hardware para os valores de número inteiro grande <!--1357880--> | [Pré-visualização do técnico 1805](capabilities-in-technical-preview-1805.md#improvement-to-hardware-inventory-for-large-integer-values)  | ![Não foi adicionada](media/Red_X.gif) |  
 | Melhoria da manutenção do WSUS <!--1357898--> | [Pré-visualização do técnico 1805](capabilities-in-technical-preview-1805.md#improvement-to-wsus-maintenance)  | ![Não foi adicionada](media/Red_X.gif) |  
 | Melhoria para suportar em certificados CNG <!--1357314--> | [Pré-visualização do técnico 1805](capabilities-in-technical-preview-1805.md#improvement-to-support-for-cng-certificates)  | ![Não foi adicionada](media/Red_X.gif) |  
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
 
  

## <a name="capabilities-delivered-in-previous-technical-previews"></a>Capacidades fornecidas em pré-visualizações técnicas anteriores
Seguem-se as capacidades específicas fornecidas com versões anteriores da versão de pré-visualização técnica do Configuration Manager. Estas capacidades permanecem disponíveis nas versões posteriores, mas ainda não estão disponíveis na versão atual do ramo. 

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

 |Funcionalidade |Versão de pré-visualização técnica |  
 |----------------|---------------------|
 | Melhoramentos para pontos de distribuição com PXE ativado <!-- 1357580 --> | [Pré-visualização do técnico 1802](capabilities-in-technical-preview-1802.md#improvements-to-pxe-enabled-distribution-points) | 
 | Dashboard de ciclo de vida do produto <!--1319632 --> | [Pré-visualização do técnico 1802](capabilities-in-technical-preview-1802.md#product-lifecycle-dashboard) | 
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

