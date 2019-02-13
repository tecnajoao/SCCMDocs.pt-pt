---
title: Recolha de dados de diagnóstico
titleSuffix: Configuration Manager
description: Saiba mais sobre como o System Center Configuration Manager recolhe os diagnósticos e dados de utilização sobre ele próprio.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: becfa825-b19f-448c-ab82-bb929255e4ae
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 704c64d314f2eaf4fe2678f316ea729584752d2e
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56125583"
---
# <a name="how-diagnostics-and-usage-data-is-collected-by-system-center-configuration-manager"></a>Como os diagnósticos e dados de utilização são recolhidos para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Para recolher dados de utilização e diagnóstico para o System Center Configuration Manager, cada site primário executa consultas de SQL Server semanalmente. Numa hierarquia multilocal, os dados são replicados para o site de administração central.  

No site de nível superior de uma hierarquia, a função do sistema do site do ponto de ligação de serviço envia estas informações quando verifica a existência de atualizações. O modo do detemines de ponto de ligação de serviço como os dados são transferidos:  

-   **No modo online:** Dados de diagnóstico e utilização são enviados automaticamente uma vez por semana a partir da ligação de serviço ponto para o serviço em nuvem.  

-   **No modo offline:** Dados de diagnóstico e utilização são transferidos manualmente utilizando a ferramenta de ligação de serviço. Para obter mais informações,ver [Utilize a Ferramenta de Ligação de Serviço para o System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md).  

Para obter mais informações, veja [Acerca do ponto de ligação de serviço no System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  
