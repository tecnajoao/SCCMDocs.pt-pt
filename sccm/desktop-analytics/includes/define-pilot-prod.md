---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/30/2018
ms.openlocfilehash: 5769a9de754bb13f9a00025b2c78dd3d334fc5e0
ms.sourcegitcommit: ad25a7bdd983c5a0e4c95bffdc61c9a1ebcbb765
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/26/2019
ms.locfileid: "55073369"
---
Utilize as seguintes definições para diferenciar entre o piloto e de produção:  

- **Piloto**: Um subconjunto dos seus dispositivos que pretende validar antes de implementar um conjunto maior. Utilize a análise de ambiente de trabalho para marcar dispositivos como exclusivo para o conjunto de piloto. Dispositivos no projeto piloto estão prontos para atualização quando não existem recursos estão a bloquear. Um recurso de bloqueio está marcado como *críticas* e *não é possível* para atualizar.  

- **Produção**: Todos os outros dispositivos inscritos para análise de ambiente de trabalho que não estão no projeto piloto. Dispositivos de produção estão prontos para atualização quando todos os recursos são assinados-off. Análise de área de trabalho iniciar sessão automaticamente desativar qualquer ativos não críticas.  

