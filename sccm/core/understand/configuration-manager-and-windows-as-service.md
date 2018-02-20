---
title: "Noções básicas do Configuration Manager como um serviço e o Windows como um serviço"
titleSuffix: Configuration Manager
description: "Obter informações básicas na adoção do Configuration Manager como um serviço para suportar o Windows como um serviço."
ms.custom: na
ms.date: 01/04/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c8534a1e-57b8-4688-b6e6-299d82cfcec9
caps.latest.revision: 
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 6d93be3ec04396c9980b039617c673985090cdc6
ms.sourcegitcommit: fbd4a9d2fa8ed4ddd3a0fecc4a2ec4fc0ccc3d0c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/19/2018
---
# <a name="keep-windows-10-up-to-date-in-the-enterprise-using-configuration-manager"></a>Par Windows 10 na empresa com o Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramo atual), Windows 10 (canal de ponto e anual)*

System Center Configuration Manager fornece controlo abrangente sobre atualizações de funcionalidade para o Windows 10. Totalmente adotar o Windows como um modelo de serviço, também tem de adotar o Gestor de configuração como um modelo de serviço. Para se manter atual com o Windows 10, requer que, mantenha-se atualizado com o Configuration Manager para uma experiência otimizada. São necessárias novas versões do Configuration Manager para tirar partido das novas funcionalidades de enterprise e extraordinária para Windows 10. Este conteúdo se destina a ser uma página de destino para os artigos de chaves necessário adotar o Configuration Manager como um serviço. Gestor de configuração como um serviço obtém o seu caminho para o Windows como um serviço.

## <a name="key-topics-about-adopting-configuration-manager-as-a-service"></a>Principais tópicos sobre adotar o Configuration Manager como um serviço

| Tópico        | Descrição          | 
| ------------- |-------------|
|[Descrição geral do Configuration Manager como um serviço](/sccm/core/plan-design/changes/whats-new-incremental-versions)|Fornece um breve resumo dos pontos de chaves para o novo modelo de manutenção para o Configuration Manager (ramo atual)|
|[Ciclo de vida de suporte](/sccm/core/servers/manage/current-branch-versions-supported)|Explica o novo suporte e manutenção de modelo.|
|[Itens removidos e preteridos](/sccm//core/plan-design/changes/deprecated/removed-and-deprecated)|Fornece o aviso antecipado sobre futuras alterações que podem afetar a utilização do Configuration Manager.|
|[Configuration Manager como um serviço](/sccm/core/servers/manage/updates)|Explica o método fácil de na consola de aplicação de atualizações de funcionalidade do Configuration Manager.|
|[Obter as atualizações disponíveis](/sccm/core/servers/manage/install-in-console-updates.md#get-available-updates)|Explica os dois modos de disponíveis para obter o novo Gestor de configuração de atualizações de funcionalidade.|
|[Lista de verificação de atualização](/sccm/core/servers/manage/install-in-console-updates#bkmk_beforeinstall)|Fornece listas de verificação de atualização específico da versão, se aplicável.| 
|[Instalar novas atualizações de funcionalidade do Configuration Manager](/sccm/core/servers/manage/install-in-console-updates#bkmk_install)|Explica os passos de instalação simples para atualizações de funcionalidade.|
|[Suporte para Windows 10](/sccm/core/plan-design/configs/support-for-windows-10)|Fornece um suporte de versões de matriz para o Windows 10 (e ADK).|
|[Pré-visualizações técnicas para o Configuration Manager](/sccm/core/get-started/technical-preview)|Fornece informações sobre o programa de pré-visualização técnica do ConfigMgr.|


## <a name="key-topics-about-adopting-windows-as-a-service"></a>Principais tópicos sobre adotar o Windows como um serviço
| Tópico        | Descrição          | 
| ------------- |-------------|
|[Gerir o Windows como um serviço](/sccm/osd/deploy-use/manage-windows-as-a-service)|Explica como utilizar planos de manutenção para implementar atualizações de funcionalidade do Windows 10.|
|[Atualização do Windows para integração de negócios (opcional)](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10)|Explica como definir e implementar o Windows Update para políticas de Business (WUfB) com o Configuration Manager.|
|[Utilize a gestão conjunta com o Microsoft Intune e o Windows Update para empresas (opcional)](/sccm/core/clients/manage/co-management-overview)|Fornece uma descrição geral da gestão conjunta| 


## <a name="related-articles"></a>Artigos relacionados

- [Atualização no local para o System Center Configuration Manager (ramo atual) do ConfigMgr 2012](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)
- [Planear a migração para o System Center Configuration Manager (ramo atual) do ConfigMgr 2007](/sccm/core/migration/planning-for-migration)