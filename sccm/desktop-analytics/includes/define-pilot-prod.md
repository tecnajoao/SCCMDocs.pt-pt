---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/30/2018
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8305102657a5973c19ca161f65204587954b0232
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56142728"
---
Utilize as seguintes definições para diferenciar entre o piloto e de produção:  

- **Piloto**: Um subconjunto dos seus dispositivos que pretende validar antes de implementar um conjunto maior. Utilize a análise de ambiente de trabalho para marcar dispositivos como exclusivo para o conjunto de piloto. Dispositivos no projeto piloto estão prontos para atualização quando não existem recursos estão a bloquear. Um recurso de bloqueio está marcado como *críticas* e *não é possível* para atualizar.  

- **Produção**: Todos os outros dispositivos inscritos para análise de ambiente de trabalho que não estão no projeto piloto. Dispositivos de produção estão prontos para atualização quando todos os recursos são assinados-off. Análise de área de trabalho iniciar sessão automaticamente desativar qualquer ativos não críticas.  

