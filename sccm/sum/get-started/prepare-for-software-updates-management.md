---

title: "Preparar para a gestão de atualizações de software | Documentos do Microsoft"
description: "Para se preparar para gerir atualizações, conclua estas tarefas para apresentar dados da avaliação de compatibilidade na consola do System Center Configuration Manager."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: 01907900-e28b-4cd7-9479-42906416707b
ms.translationtype: Machine Translation
ms.sourcegitcommit: e6cf8c799b5be2f7dbb6fadadddf702ec974ae45
ms.openlocfilehash: 5c34bd1ea108dffda10c30281fb9c97ba38ae1ae
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---

# <a name="prepare-for-software-updates-management"></a>Preparar para a gestão de atualizações de software

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Antes dos dados de avaliação de conformidade da atualização de software é apresentada na consola do System Center Configuration Manager e antes de poder implementar atualizações de software para computadores cliente, tem de concluir os passos nas secções seguintes.

## <a name="step-1-install-a-software-update-point"></a>Passo 1: Instalar um ponto de atualização de software  
O ponto de atualização de software é necessário no site de administração central ou site primário autónomo e em sites primários para ativar o software de avaliação de compatibilidade de atualizações e para implementar software atualizações para clientes. O ponto de atualização de software é opcional em site secundários. Para obter mais detalhes, consulte o artigo [instalar um ponto de atualização de software](install-a-software-update-point.md)  

## <a name="step-2-synchronize-software-updates"></a>Passo 2: Sincronizar atualizações de Software
Sincronização de atualizações de software é o processo de obtenção de metadados de atualizações de software que cumprem os critérios que configurou. As atualizações de software não são apresentadas na consola do Configuration Manager até que a sincronizar as atualizações de software. Para obter mais detalhes, consulte o artigo [sincronizar atualizações de software](synchronize-software-updates.md).   

## <a name="step-3-configure-classifications-and-products-to-synchronize"></a>Passo 3: Configurar classificações e produtos a sincronizar
Realize esta configuração no site de administração central ou site primário autónomo. Depois de sincronizar as atualizações de software pela primeira vez, o Configuration Manager obtém uma lista atualizada de classificações e produtos. Agora, pode selecionar a partir de novas opções nas propriedades do componente de ponto de atualização de Software. Depois de configurar os produtos e classificações de novo, repita o passo 2 para iniciar a sincronização de atualizações de software para obter metadados de atualizações de software para os critérios de novo. Para obter mais detalhes, consulte o artigo [configurar classificações e produtos a sincronizar](configure-classifications-and-products.md).

## <a name="step-4-manage-settings-for-software-updates"></a>Passo 4: Gerir definições das atualizações de software
Depois de sincronizar as atualizações de software, certifique-se de definições de cliente do Configuration Manager, as configurações da política de grupo e definições de atualizações de software antes de implementar atualizações de software. Para obter mais detalhes, consulte o artigo [gerir as definições das atualizações de software](manage-settings-for-software-updates.md).

