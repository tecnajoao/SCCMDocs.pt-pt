---
title: O Configuration Manager e o Windows como um Serviço
titleSuffix: Configuration Manager
description: Obtenha informações básicas sobre a adoção de ramo atual do Configuration Manager para suportar o Windows como um serviço.
ms.date: 06/15/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c8534a1e-57b8-4688-b6e6-299d82cfcec9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 329f5c2f227cbd8a51b1c9ccc21810cda9f6a2cf
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53417144"
---
# <a name="configuration-manager-and-windows-as-a-service"></a>O Configuration Manager e o Windows como um Serviço

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager fornece controlo abrangente sobre as atualizações de funcionalidades para o Windows 10. Adotar totalmente o Windows como um modelo de serviço, também deve adotar o modelo de ramo atual do Configuration Manager. Manter-se atualizado com o Windows 10, requer que mantenha-se atualizado com o Configuration Manager para a melhor experiência. Novas versões do Configuration Manager são necessários para aproveitarem os novos recursos empresariais para Windows 10. Este artigo destina-se para ser uma página de destino para os artigos de chave necessários para adotar o ramo atual do Configuration Manager. Ramo atual do Configuration Manager permite-lhe no caminho certo para o Windows como um serviço.

## <a name="key-articles-about-adopting-configuration-manager-current-branch"></a>Principais artigos sobre como adotar o ramo atual do Configuration Manager

| Artigo        | Descrição          | 
| ------------- |-------------|
|[Descrição geral do Configuration Manager current branch](/sccm/core/plan-design/changes/whats-new-incremental-versions)|Fornece um breve resumo dos pontos chave para o novo modelo de manutenção para o Configuration Manager (ramo atual)|
|[Ciclo de vida de suporte](/sccm/core/servers/manage/current-branch-versions-supported)|Explica o novo suporte e o modelo de manutenção.|
|[Itens removidos e preteridos](/sccm//core/plan-design/changes/deprecated/removed-and-deprecated)|Fornece um aviso antecipado sobre futuras alterações que pode afetar a utilização do Configuration Manager.|
|[Atualizações para o Configuration Manager current branch](/sccm/core/servers/manage/updates)|Explica o método na consola fácil de aplicar as atualizações de funcionalidades para o Configuration Manager.|
|[Obter as atualizações disponíveis](/sccm/core/servers/manage/install-in-console-updates#get-available-updates)|Explica os dois modos disponíveis para obter o novo Gestor de configuração de atualizações de funcionalidades.|
|[Lista de verificação de atualização](/sccm/core/servers/manage/install-in-console-updates#bkmk_beforeinstall)|Fornece listas de verificação de atualização específico da versão, se aplicável.| 
|[Instalar novas atualizações de funcionalidade do Configuration Manager](/sccm/core/servers/manage/install-in-console-updates#bkmk_install)|Explica os passos de instalação simples para atualizações de funcionalidades.|
|[Suporte para Windows 10](/sccm/core/plan-design/configs/support-for-windows-10)|Fornece um suporte a versões de matriz para o Windows 10 (e ADK).|
|[Pré-visualizações técnicas para o Configuration Manager](/sccm/core/get-started/technical-preview)|Fornece informações sobre o programa de pré-visualização técnica do ConfigMgr.|


## <a name="key-articles-about-adopting-windows-as-a-service"></a>Principais artigos sobre como adotar o Windows como um serviço

| Artigo        | Descrição          | 
| ------------- |-------------|
|[Gerir o Windows como um serviço](/sccm/osd/deploy-use/manage-windows-as-a-service)|Explica como utilizar planos de manutenção para implementar atualizações de funcionalidades do Windows 10.|
|[Atualizar o Windows 10 através de sequência de tarefas](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system)|Os detalhes da criação de uma sequência de tarefas para atualizar o Windows 10 com recomendações adicionais.|
|[Implementações faseadas](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)|As implementações faseadas automatizam uma implementação coordenada e sequenciada de uma sequência de tarefas em vários conjuntos.|  
|[Optimize Windows 10 update delivery (Otimizar a entrega das atualizações do Windows 10)](/sccm/sum/deploy-use/optimize-windows-10-update-delivery)|Utilize o Configuration Manager para gerir o conteúdo da atualização para se manter atualizado com o Windows 10.|
|[Integrar com a preparação da atualização](/sccm/core/clients/manage/upgrade/upgrade-analytics)|Preparação de atualizações permite-lhe avaliar e analisar a preparação de dispositivos no seu ambiente para uma atualização para Windows 10.| 
|[Atualização do Windows para integração de negócios (opcional)](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10)|Explica como definir e implantar o Windows Update para políticas de Business (WUfB) com o Configuration Manager.|
|[Utilizar cogestão com Microsoft Intune e o Windows Update para empresas (opcional)](/sccm/core/clients/manage/co-management-overview)|Fornece uma descrição geral de cogestão| 


## <a name="related-articles"></a>Artigos relacionados

- [Atualização no local para o System Center Configuration Manager (ramo atual) a partir do ConfigMgr 2012](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)
- [Planear a migração para o System Center Configuration Manager (ramo atual) do ConfigMgr 2007](/sccm/core/migration/planning-for-migration)