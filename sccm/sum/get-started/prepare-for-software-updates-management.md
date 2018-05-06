---
title: Preparar a gestão de atualizações de software
titleSuffix: Configuration Manager
description: Para se preparar para gerir as atualizações, conclua estas tarefas para apresentar os dados da avaliação de compatibilidade na consola do System Center Configuration Manager.
author: aczechowski
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 01907900-e28b-4cd7-9479-42906416707b
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: f2608d8cd46572a0fbcbafc6bc8c0f5e013356a2
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="prepare-for-software-updates-management"></a>Preparar a gestão de atualizações de software

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Apresenta os dados da avaliação de compatibilidade da atualização de software na consola do System Center Configuration Manager e antes de poder implementar atualizações de software para computadores cliente, tem de concluir os passos nas secções seguintes.

## <a name="step-1-install-a-software-update-point"></a>Passo 1: Instalar um ponto de atualização de software  
É necessário o ponto de atualização de software no site de administração central ou site primário autónomo e em sites primários para ativar o software de avaliação de compatibilidade de atualizações e para implementar software atualizações aos clientes. O ponto de atualização de software é opcional em site secundários. Para obter mais informações, consulte [instalar um ponto de atualização de software](install-a-software-update-point.md)  

## <a name="step-2-synchronize-software-updates"></a>Passo 2: Sincronizar atualizações de Software
Sincronização de atualizações de software é o processo de obtenção de metadados de atualizações de software que cumprem os critérios que configurou. As atualizações de software não são apresentadas na consola do Configuration Manager até sincronizar as atualizações de software. Para obter mais informações, consulte [sincronizar atualizações de software](synchronize-software-updates.md).   

## <a name="step-3-configure-classifications-and-products-to-synchronize"></a>Passo 3: Configurar classificações e produtos a sincronizar
Realize esta configuração no site de administração central ou site primário autónomo. Depois de sincronizar as atualizações de software pela primeira vez, o Configuration Manager obtém uma lista atualizada de classificações e produtos. Agora, pode selecionar de entre as novas opções nas propriedades do componente de ponto de atualização de Software. Depois de configurar novas classificações e produtos, repita o passo 2 para iniciar a sincronização de atualizações de software para obter metadados de atualizações de software para os critérios de novo. Para obter mais informações, consulte [configurar classificações e produtos para sincronizar](configure-classifications-and-products.md).

## <a name="step-4-manage-settings-for-software-updates"></a>Passo 4: Gerir as definições das atualizações de software
Depois de sincronizar as atualizações de software, certifique-se as definições de cliente do Configuration Manager, as configurações da política de grupo e definições de atualizações de software antes de implementar atualizações de software. Para obter mais informações, consulte [gerir as definições das atualizações de software](manage-settings-for-software-updates.md).
