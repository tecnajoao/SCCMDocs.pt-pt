---
title: "Сбор данных диагностики | Документы Майкрософт"
description: "Узнайте, как System Center Configuration Manager собирает собственные данные диагностики и сведения об использовании."
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: becfa825-b19f-448c-ab82-bb929255e4ae
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 9c0165212fe34f460be2ce870d0542b616f3bc4d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="how-diagnostics-and-usage-data-is-collected-by-system-center-configuration-manager"></a>Как System Center Configuration Manager собирает данные о диагностике и использовании

*Применимо к: System Center Configuration Manager (Current Branch)*

Для сбора данных диагностики и сведений об использовании для System Center Configuration Manager каждый первичный сайт еженедельно выполняет запросы SQL Server. В иерархии с несколькими сайтами данные реплицируются на сайт центра администрирования.  

На верхнем сайте иерархии роль системы сайта точки подключения службы отправляет эти сведения при выполнении проверки на наличие обновлений. Режим точки подключения службы определяет способ передачи данных.  

-   **Режим "в сети"** . Каждую неделю данные о диагностике и использовании автоматически отправляются из точки подключения службы в облачную службу.  

-   **Режим "вне сети"** . Данные о диагностике и использовании передаются вручную с помощью инструмента подключения службы. Дополнительные сведения см. в разделе [Использование инструмента подключения службы для System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md).  

Дополнительные сведения см. в статье [Сведения о точке подключения службы в System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  
