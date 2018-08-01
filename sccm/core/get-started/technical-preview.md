---
title: Versões de pré-visualização técnicas
titleSuffix: Configuration Manager
description: Saiba mais sobre o ramo de pré-visualização técnica a testarem novas funcionalidades e capacidades no Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b60ebcf0ce94dfdc25466b31c9a64d0d556e1ac6
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385393"
---
# <a name="technical-preview-for-configuration-manager"></a>Pré-visualização técnica do Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo fornece detalhes sobre o ramo mensal de pré-visualização técnica do Configuration Manager. O technical preview introduz novas funcionalidades que a Microsoft está trabalhando. Ele introduz novas funcionalidades que ainda não estão incluídas no ramo atual do Configuration Manager. Estas funcionalidades poderão eventualmente ser incluídas numa atualização para o current branch. Antes de vamos finalizar os recursos, queremos a experimentá-las e envie-nos comentários.  

Uma vez que esta versão é uma pré-visualização técnica, detalhes e a funcionalidade estão sujeitos a alterações.  

Essas informações se aplicam a todas as versões do ramo de pré-visualização técnica do Configuration Manager. Este artigo apresenta uma lista de cada funcionalidade nova juntamente com a versão de pré-visualização técnica em que ele aparece pela primeira vez. Por exemplo, a versão **1806** para Junho (06) de 2018 (18). Artigos separados dedicados para cada detalhe da versão de pré-visualização, os recursos individuais.  

Para obter informações sobre o que há de novo no *ramo atual* do Configuration Manager, consulte [o que há de novo no Configuration Manager versões incrementais](/sccm/core/plan-design/changes/whats-new-incremental-versions).



##  <a name="bkmk_reqs"></a> Requisitos e limitações  

> [!IMPORTANT]     
>  O technical preview é licenciado apenas para utilização num ambiente de laboratório. A Microsoft não pode fornecer serviços de suporte e determinadas funcionalidades poderão não estar disponíveis no software de pré-visualização. Além disso, o software de pré-visualização, pode ter reduzido ou diferentes padrões de segurança, privacidade, acessibilidade, disponibilidade e fiabilidade relação ao software disponibilizado comercialmente.  

Para a maioria dos pré-requisitos de produto, utilize as informações no [configurações suportadas](/sccm/core/plan-design/configs/supported-configurations). As exceções seguintes aplicam-se para o ramo de pré-visualização técnica:  

-   Cada instalação está ativa por 90 dias antes de se tornar inativa.  

-   O inglês é o único idioma suportado.  

-   Ela oferece suporte apenas os seguintes parâmetros de linha de comandos de configuração:  
    -   `/silent`  
    -   `/testdbupgrade`    

-   Instala o ponto de ligação de serviço para o modo online. Ele não suporta o modo offline.  

-   Os artigos separados para cada versão específica do technical preview incluem requisitos, conforme aplicável ou limitações adicionais.

-   As seguintes funcionalidades não são suportadas com o ramo de pré-visualização técnica:  

    - [Migração](/sccm/core/migration/migrate-data-between-hierarchies) de ou para este ramo de pré-visualização.  

    - [Atualizar](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager) para este ramo de pré-visualização.  

    - [Recuperação de sites](/sccm/core/servers/manage/recover-sites) da pasta CD. Latest.  <!--507106-->

-   Não há suporte para a atualização para o ramo atual do ramo pré-visualização.  

    > [!Note]  
    > Quando as atualizações estiverem disponíveis para uma versão de pré-visualização, ainda encontrar e instalá-los a partir da **atualizações e manutenção** nó da consola do Configuration Manager. Para ver um vídeo do processo de atualização na consola, consulte [pacotes de atualização de instalar o Configuration Manager](https://www.youtube.com/embed/KBd_EGFbUT8) em youtube.com.  

-   Ela oferece suporte apenas um site primário autónomo. Não há suporte para um site de administração central, múltiplos sites primários ou sites secundários.  

O ramo de pré-visualização técnica do Configuration Manager suporta os seguintes produtos e tecnologias: 

-   Ele só suporta as seguintes versões do **SQL Server**:  

    -   SQL Server 2017 (com a atualização cumulativa 2 e posterior) que começa no Configuration Manager versão 1710
    -   SQL Server 2016 (sem Service Pack e posterior)
    -   SQL Server 2014 (com Service Pack 1 e posterior)
    -   SQL Server 2012 (com Service Pack 3, ou posterior)  


-   O site suporta até 10 clientes, que tem de executar uma das seguintes versões do Windows:  

      -   Windows 10  
      -   Windows 8,1  
      -   Windows 7  

> [!Note]  
> A inclusão desses produtos neste conteúdo não implica uma extensão de suporte para uma versão que está além do seu ciclo de vida de suporte. O Configuration Manager não suporta produtos que estejam fora do respetivo ciclo de vida de suporte. Para obter mais informações, consulte [Microsoft Lifecycle Policy](https://go.microsoft.com/fwlink/p/?LinkId=208270).  



##  <a name="bkmk_install"></a> Instalação e atualização  

O ramo de pré-visualização técnica do Configuration Manager para utilização do laboratório é diferente do Configuration Manager current branch para utilização em produção.  

Primeiro de instalar uma versão de linha de base do ramo de pré-visualização técnica. Depois de instalar uma versão de linha de base, em seguida, utilize atualizações na consola para atualizar sua instalação atualizada com a versão de pré-visualização mais recente. Normalmente, as novas versões do technical preview estão disponíveis mensalmente.

A Microsoft suporta a cada versão de pré-visualização técnica até que existem três versões sucessivas. Por exemplo, quando versão 1708 lançado, versão 1704 não era mais suporte. Versões 1705, 1706 e versão 1707 permaneceram em suporte. Quando uma linha de base sai do suporte, ainda é suportado para a instalação de um novo site de pré-visualização técnica, partindo do princípio de que atualizar imediatamente para uma versão suportada. A linha de base mais antiga é suportada até que uma nova versão de linha de base está disponível. Atualize para a versão mais recente disponível da linha de base e, em seguida, repita o processo de atualização até que instale a versão de pré-visualização técnica mais recente.

> [!TIP]  
>  Quando instala uma atualização para o technical preview, atualizar sua instalação de visualização para essa nova versão de pré-visualização técnica. Uma instalação de pré-visualização técnica nunca tem a opção de atualizar para uma instalação do ramo atual. Também nunca recebe atualizações da versão do ramo atual. 
> 
> Várias vezes ao longo do ano, existem pré-visualização técnica e as versões atuais do ramo com o mesmo número de versão. Por exemplo, existe uma versão de pré-visualização técnica 1802 e uma versão de ramificação 1802 atual. 


### <a name="active-baseline-versions"></a>Versões de linha de Active Directory
   
Instale uma versão de linha de base para até um ano após o seu lançamento. Quando instala um novo site de pré-visualização técnica, se mais de uma versão de linha de base está atualmente disponível, utilize a versão de linha de base mais recente.

-  **Versão de pré-visualização técnica 1806**: A versão de pré-visualização técnica do Configuration Manager 1806 está disponível como uma atualização na consola e como uma nova versão de linha de base. Baixe versões de linha de base [do Centro de avaliação TechNet](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).



##  <a name="BKMK_TPFeedback"></a> Fornecer comentários  

Adoramos ouvir os seus comentários sobre as novas funcionalidades no technical preview. Para obter mais informações, consulte [comentários sobre o produto](/sccm/core/understand/find-help#product-feedback).

Se tiver ideias sobre novas funcionalidades que gostariam de ver, o que queremos saber que também. Para submeter novas ideias e votar em ideias submetidas por outras pessoas, [visite a nossa página UserVoice](https://configurationmanager.uservoice.com).  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->



##  <a name="bkmk_tpCaps"></a> A versão mais recente  

As seguintes funcionalidades estão disponíveis com a versão de pré-visualização técnica mais recente do Configuration Manager: 

<!-- This is the full list of new features in the latest TP release -->

### <a name="technical-preview-version-1807"></a>Pré-visualização técnica versão 1807

- [Hub de Comunidade](capabilities-in-technical-preview-1807.md#bkmk_hub) <!--1357766-->
- [Especifique a unidade para a manutenção da imagem de SO offline](capabilities-in-technical-preview-1807.md#bkmk_osd) <!--1358924-->
- [Atividade de sincronização de dispositivos cogeridos com o Intune](capabilities-in-technical-preview-1807.md#bkmk_comgmt) <!--1358565-->
- [Aplicativos de reparação](capabilities-in-technical-preview-1807.md#bkmk_app-repair) <!--1357866-->
- [Aprovar pedidos de aplicações através de e-mail](capabilities-in-technical-preview-1807.md#bkmk_email-approve) <!--1321550-->
- [Melhoria à saída do script](capabilities-in-technical-preview-1807.md#bkmk_script) <!--1236459-->
- [Melhoria para atualizações de software de terceiros](capabilities-in-technical-preview-1807.md#bkmk_3pupdate) <!--1358714-->


> [!Note]  
> Recursos que estavam disponíveis numa versão anterior do technical preview permanecem disponíveis nas versões posteriores. Da mesma forma, os recursos que são adicionados para o Configuration Manager current branch permanecem disponíveis no ramo de pré-visualização técnica.   



## <a name="features-in-recent-supported-technical-previews"></a>Recursos em technical previews recentes suportadas

As seguintes funcionalidades foram lançadas com versões anteriores do ramo de pré-visualização técnica do Configuration Manager que ainda são suportadas: 

<!-- This is the full list of new features in the past THREE (3) TP releases. 
Each month, add features from the list above to the top of this table. 
Then remove the bottom of this list and/or move individual items not in CB to the third table below.
-->

 |Funcionalidade |Versão de pré-visualização técnica |Versão do ramo atual|  
 |----------------|---------------------|--------------------|
 | Melhorias para as implementações faseadas <!--1358577,1358147,1358578--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_pod)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Suporte para novos formatos de pacote de aplicação Windows <!--1357427--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_msix)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Melhoria de segurança de push de cliente <!--1358204--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_client-push)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Informações de gestão para a manutenção proativa <!--1352184,et al--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_insights)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Carga de trabalho de aplicações móveis de transição para dispositivos cogeridos <!--1357892--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_comgmt)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Opções de grupos de limites para configurar o peering downloads <!--1356193--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_bgoptions)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Suporte para catálogos personalizados de atualizações de software de terceiros <!--1358714--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_3pupdate)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Melhorias para a cloud de funcionalidades de gestão <!--511980,515854--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_cloud)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Novo relatório de conformidade de atualizações de software <!--1357775--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_report)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Atualizações de software de terceiros <!--1352101--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#bkmk-3pupdate)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Configurar as definições do Windows Defender SmartScreen para o Microsoft Edge <!--1353701--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#configure-windows-defender-smartscreen-settings-for-microsoft-edge)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Política MDM de sincronização do Microsoft Intune para um dispositivo cogerido <!--1357377--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#sync-mdm-policy-from-microsoft-intune-for-a-co-managed-device)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Carga de trabalho de transição do Office 365 para o Intune através de cogestão <!--1357841--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#transition-office-365-workload-to-intune-using-co-management)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Gestor de conversão de pacotes <!--1357861--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#package-conversion-manager)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Implementar atualizações de software sem conteúdo <!--1357933--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#deploy-software-updates-without-content)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Integração de ferramenta de personalização do Office com o instalador do Office 365 <!--1358149--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#office-customization-tool-integration-with-the-office-365-installer)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Melhorias para a cloud do gateway de gestão <!--1358215,1358651,503899--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#improvements-to-cloud-management-gateway)   | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Melhorias para proteger as comunicações de cliente <!--1358278,1358279--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#improvements-to-secure-client-communications)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Melhorias na infraestrutura de centro de software <!--1358309--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#software-center-infrastructure-improvements)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Aprovisionar os pacotes de aplicações do Windows para todos os utilizadores num dispositivo <!--1358310--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#provision-windows-app-packages-for-all-users-on-a-device)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Aprimoramentos no painel do Surface <!--1358654--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#improvements-to-the-surface-dashboard)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Revisão de unidade de padrão de inventário de hardware <!--514442--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#hardware-inventory-default-unit-revision)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Criar uma implementação faseada com fases configurados manualmente para uma sequência de tarefas <!--1358148--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#create-a-phased-deployment-with-manually-configured-phases-for-a-task-sequence)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Suporte de ponto de distribuição de nuvem para o Azure Resource Manager <!--1322209--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#cloud-distribution-point-support-for-azure-resource-manager)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Executar ações com base nas informações de gestão <!--1357930--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#take-actions-based-on-management-insights)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Carga de trabalho do transição dispositivo configuração Intune com a cogestão <!--1357903--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#transition-device-configuration-workload-to-intune-using-co-management)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Ativar pontos de distribuição para utilizar o controlo de congestionamento de rede <!--1358112--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#enable-distribution-points-to-use-network-congestion-control)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Dashboard de gestão da cloud <!--1358461--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#cloud-management-dashboard)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | CMPivot <!--1358456--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#cmpivot)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Melhorada a comunicações de cliente seguras <!--1356889,1358228,1358460--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improved-secure-client-communications)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Melhorias para ativar o suporte de atualização de software de terceiros <!--1357605--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvements-for-enabling-third-party-software-update-support)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Melhoramentos à sequência de tarefas de atualização in-loco do Windows 10 <!--1358500--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvements-to-windows-10-in-place-upgrade-task-sequence)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | CMTrace instalado com o cliente <!--1357971--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#cmtrace-installed-with-client)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Melhoria na consola do Configuration Manager <!--1358202--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvement-to-the-configuration-manager-console)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Melhorias aos comentários de consola <!--1357542--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvements-to-console-feedback)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Melhorias aos pontos de distribuição com PXE ativado <!--1357580--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvements-to-pxe-enabled-distribution-points)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Melhoria para o inventário de hardware para valores inteiros grandes <!--1357880--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvement-to-hardware-inventory-for-large-integer-values)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Melhoria para manutenção WSUS <!--1357898--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvement-to-wsus-maintenance)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Melhoria para o suporte para certificados CNG <!--1357314--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvement-to-support-for-cng-certificates)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Configurar uma biblioteca de conteúdos remota para o servidor do site <!--1357525--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#configure-a-remote-content-library-for-the-site-server)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 | Enviar comentários a partir da consola do Configuration Manager <!--1357542--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#bkmk_feedback)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 | Centro de suporte <!--1357489--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#support-center)  | ![Não adicionado](media/Red_X.gif) | 
 | Kit de ferramentas do Configuration Manager <!--1357145--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#configuration-manager-toolkit)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 | Desinstalar a aplicação mediante a revogação de aprovação <!--1357891--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#uninstall-application-on-approval-revocation)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 | Excluir contentores do Active Directory da deteção <!--1358143--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#exclude-active-directory-containers-from-discovery)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 | Especifique a visibilidade da ligação de site do catálogo de aplicações no Centro de Software <!--1358214--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#specify-the-visibility-of-the-application-catalog-website-link-in-software-center)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 | Filtrar regras de implementação automática pela arquitetura de atualização de software <!--1322266--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#filter-automatic-deployment-rules-by-software-update-architecture)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 | Melhorias para implementação do SO <!--1358330,1358493--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#improvements-to-os-deployment) | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 | Distribuição de extração os pontos de distribuição da nuvem de suporte de pontos como origem <!--1321554--> | [Tech Preview versão 1803](capabilities-in-technical-preview-1803.md#pull-distribution-points-support-cloud-distribution-points-as-source)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 | Suporte de transferência parcial na cache de elemento de rede de cliente para reduzir a utilização de WAN <!--1357346--> | [Tech Preview versão 1803](capabilities-in-technical-preview-1803.md#partial-download-support-in-client-peer-cache-to-reduce-wan-utilization)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 | Janelas de manutenção no Centro de Software <!--1358131--> | [Tech Preview versão 1803](capabilities-in-technical-preview-1803.md#maintenance-windows-in-software-center)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 | Separador personalizado para a página Web no Centro de Software <!--1358132--> | [Tech Preview versão 1803](capabilities-in-technical-preview-1803.md#custom-tab-for-webpage-in-software-center)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 | Ativar o suporte de atualização de software de terceiros nos clientes <!--1357605--> | [Tech Preview versão 1803](capabilities-in-technical-preview-1803.md#enable-third-party-software-update-support-on-clients)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 | Ativar copiar/colar dos detalhes do recurso de vistas de monitorização <!--1357552--> | [Tech Preview versão 1803](capabilities-in-technical-preview-1803.md#enable-copypaste-of-asset-details-from-monitoring-views)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 | Extensões SCAP <!--1357552--> | [Tech Preview versão 1803](capabilities-in-technical-preview-1803.md#scap-extensions)  | [Versão 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) | 
 
  

## <a name="features-in-previous-technical-previews"></a>Recursos do anteriores pré-visualizações técnicas

As seguintes funcionalidades foram lançadas com versões anteriores do ramo de pré-visualização técnica do Configuration Manager. Estas funcionalidades permanecem disponíveis nas versões posteriores, mas não ainda estão disponíveis no ramo atual. 

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

|Funcionalidade |Versão de pré-visualização técnica |  
|----------------|---------------------|
| Serviço de resposta PXE baseada no cliente <!-- 1357148 --> | [Tech Preview versão 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
|Suporte de arranque de rede PXE para IPv6 <!-- 1269793 --> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
|Utilizar o Azure Active Directory <!-- 1322145? --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
|Avaliação de compatibilidade para o Windows Update para atualizações de negócios <!-- 1235390 --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |
|Acesso de dados do ponto final de OData <!-- 1321523 --> |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|
|Melhorias ao Asset Intelligence <!-- 1307390 --> |[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|
|Os utilizadores finais podem instalar aplicações do Portal da empresa <!-- 1037233? --> |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|

<!--Removed for 1806 CB:
 |Site server role high availability <!-- 1128774  |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#site-server-role-high-availability) |
 | Product lifecycle dashboard <!--1319632  | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#product-lifecycle-dashboard) | 
 | Improvements to PXE-enabled distribution points <!-- 1357580  | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-pxe-enabled-distribution-points) | 
-->



## <a name="see-also"></a>Consulte também  

Para obter mais informações, consulte os artigos seguintes:  

- [Avaliar o Configuration Manager num laboratório](/sccm/core/get-started/evaluate-with-lab-environment)
- [Quais são as novidades nas versões incrementais do Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
- [Introdução ao Configuration Manager](/sccm/core/understand/introduction)

> [!Tip]  
> Para obter mais informações sobre as funcionalidades de ramo atual que requerem o consentimento para ativar, consulte [funcionalidades de pré-lançamento](/sccm/core/servers/manage/pre-release-features).  
> 
> Para obter mais informações sobre funcionalidades atuais do ramo que tem de ativar primeiro, consulte [ativar funcionalidades opcionais de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  
