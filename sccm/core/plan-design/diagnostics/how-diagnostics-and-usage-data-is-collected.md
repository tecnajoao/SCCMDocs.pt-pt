---
title: "Recolha de dados de diagnóstico | Documentos do Microsoft"
description: "Saiba mais sobre como o System Center Configuration Manager recolhe diagnósticos e dados de utilização sobre si próprio."
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: becfa825-b19f-448c-ab82-bb929255e4ae
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 24a233516058e645df2a43623855665b97b041b0
ms.openlocfilehash: 9c0165212fe34f460be2ce870d0542b616f3bc4d
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="how-diagnostics-and-usage-data-is-collected-by-system-center-configuration-manager"></a>Como os diagnósticos e dados de utilização são recolhidos para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Para recolher dados de utilização e de diagnóstico para o System Center Configuration Manager, cada site primário executa consultas de SQL Server semanalmente. Numa hierarquia multilocal, os dados são replicados para o site de administração central.  

No site de nível superior de uma hierarquia, a função do sistema do site do ponto de ligação de serviço envia estas informações quando verifica a existência de atualizações. O modo do detemines de ponto de ligação do serviço como os dados são transferidos:  

-   **No modo online:** Dados de utilização e de diagnóstico são enviados automaticamente quando dentro de um semana a ligação de serviço do ponto de serviço em nuvem.  

-   **No modo offline:** Dados de utilização e de diagnóstico são transferidos manualmente utilizando a ferramenta de ligação de serviço. Para obter mais informações,ver [ Utilize a Ferramenta de Ligação de Serviço para o System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md).  

Para obter mais informações, veja [Sobre o ponto de ligação de serviço no System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  

