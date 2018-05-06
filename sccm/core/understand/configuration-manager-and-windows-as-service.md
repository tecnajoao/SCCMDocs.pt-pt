---
title: Noções básicas do Windows como um serviço
titleSuffix: Configuration Manager
description: Obter informações básicas sobre a adotar o ramo atual do Configuration Manager para suportar o Windows como um serviço.
ms.date: 04/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c8534a1e-57b8-4688-b6e6-299d82cfcec9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6ca2b72cb3533c3b857b3edbb4e37ca846d4cfa4
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="keep-windows-10-up-to-date-in-the-enterprise-using-configuration-manager"></a>Par Windows 10 na empresa com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager fornece controlo abrangente sobre atualizações de funcionalidade para o Windows 10. Totalmente adotar o Windows como um modelo de serviço, pode também tem adotar o modelo de ramo atual do Configuration Manager. Para se manter atual com o Windows 10, requer que, mantenha-se atualizado com o Configuration Manager para uma experiência otimizada. São necessárias novas versões do Configuration Manager para tirar partido das novas funcionalidades de enterprise e extraordinária para Windows 10. Este conteúdo se destina a ser uma página de destino para os artigos de chaves necessário adotar o ramo atual do Configuration Manager. O ramo atual do Configuration Manager obtém o seu caminho para o Windows como um serviço.

## <a name="key-topics-about-adopting-configuration-manager-current-branch"></a>Principais tópicos sobre adotar o ramo atual do Configuration Manager

| Tópico        | Descrição          | 
| ------------- |-------------|
|[Descrição geral do ramo atual do Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)|Fornece um breve resumo dos pontos de chaves para o novo modelo de manutenção para o Configuration Manager (ramo atual)|
|[Ciclo de vida de suporte](/sccm/core/servers/manage/current-branch-versions-supported)|Explica o novo suporte e manutenção de modelo.|
|[Itens removidos e preteridos](/sccm//core/plan-design/changes/deprecated/removed-and-deprecated)|Fornece o aviso antecipado sobre futuras alterações que podem afetar a utilização do Configuration Manager.|
|[Atualizações para o ramo atual do Configuration Manager](/sccm/core/servers/manage/updates)|Explica o método fácil de na consola de aplicação de atualizações de funcionalidade do Configuration Manager.|
|[Obter as atualizações disponíveis](/sccm/core/servers/manage/install-in-console-updates#get-available-updates)|Explica os dois modos de disponíveis para obter o novo Gestor de configuração de atualizações de funcionalidade.|
|[Lista de verificação de atualização](/sccm/core/servers/manage/install-in-console-updates#bkmk_beforeinstall)|Fornece listas de verificação de atualização específico da versão, se aplicável.| 
|[Instalar novas atualizações de funcionalidade do Configuration Manager](/sccm/core/servers/manage/install-in-console-updates#bkmk_install)|Explica os passos de instalação simples para atualizações de funcionalidade.|
|[Suporte para Windows 10](/sccm/core/plan-design/configs/support-for-windows-10)|Fornece um suporte de versões de matriz para o Windows 10 (e ADK).|
|[Pré-visualizações técnicas para o Configuration Manager](/sccm/core/get-started/technical-preview)|Fornece informações sobre o programa de pré-visualização técnica do ConfigMgr.|


## <a name="key-topics-about-adopting-windows-as-a-service"></a>Principais tópicos sobre adotar o Windows como um serviço
| Tópico        | Descrição          | 
| ------------- |-------------|
|[Gerir o Windows como um serviço](/sccm/osd/deploy-use/manage-windows-as-a-service)|Explica como utilizar planos de manutenção para implementar atualizações de funcionalidade do Windows 10.|
|[Atualizar o Windows 10 através de sequência de tarefas](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system)|Os detalhes de criação de uma sequência de tarefas para atualizar o Windows 10 com recomendações adicionais.|
|[Implementações faseadas](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)|Implementações faseadas automatizam uma coordenada, sequenciada implementação da sequência de tarefas em várias coleções.|  
|[Integrar com a preparação de atualização](/sccm/core/clients/manage/upgrade/upgrade-analytics)|Preparação de atualização permite-lhe avaliar e analisar a preparação de dispositivos no seu ambiente para uma atualização para o Windows 10.| 
|[Atualização do Windows para integração de negócios (opcional)](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10)|Explica como definir e implementar o Windows Update para políticas de Business (WUfB) com o Configuration Manager.|
|[Utilize a gestão conjunta com o Microsoft Intune e o Windows Update para empresas (opcional)](/sccm/core/clients/manage/co-management-overview)|Fornece uma descrição geral da gestão conjunta| 


## <a name="related-articles"></a>Artigos relacionados

- [Atualização no local para o System Center Configuration Manager (ramo atual) do ConfigMgr 2012](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)
- [Planear a migração para o System Center Configuration Manager (ramo atual) do ConfigMgr 2007](/sccm/core/migration/planning-for-migration)