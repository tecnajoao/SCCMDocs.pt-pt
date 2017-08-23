---
title: "Планирование миграции | Документы Майкрософт"
description: "Получите сведения о сайтах и иерархиях перед переносом данных в иерархию назначения System Center Configuration Manager."
ms.custom: na
ms.date: 1/12/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b2bf493e-1e10-496f-a139-2646522703ed
caps.latest.revision: "7"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: fffef1e95e1dfa03971f140a6e5a7fff9bfe5e27
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="plan-for-migration-to-system-center-configuration-manager"></a>Планирование миграции в System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

Прежде чем переносить данные в конечную иерархию System Center Configuration Manager, убедитесь в том, что вы знакомы с сайтами и иерархиями в Configuration Manager. Дополнительные сведения о сайтах и иерархиях см. в разделе [Основные сведения о Microsoft System Center Configuration Manager](../../core/understand/fundamentals.md).  

 Необходимо установить иерархию System Center Configuration Manager в качестве конечной иерархии, чтобы можно было перенести данные из поддерживаемой исходной иерархии.  

 После установки конечной иерархии нужно настроить компоненты и функции управления, которые требуется использовать в вашей конечной иерархии перед началом переноса данных.  

 Кроме того, может потребоваться спланировать перекрытие между исходной иерархией и конечной иерархией. Например, исходная иерархия может быть настроена для использования тех же сетевых расположений или границ, что и конечная иерархия, а затем в конечной иерархии устанавливаются новые клиенты и используется автоматическое назначение сайта. В этом сценарии, так как вновь установленный клиент Configuration Manager может выбрать сайт для присоединения из любой иерархии, клиент может быть неправильно назначен исходной иерархии. Поэтому следует назначать все новые клиенты в конечной иерархии в конкретные сайты в данной иерархии, а не использовать автоматическое назначение.  

 Дополнительные сведения о назначении сайта см. в подразделе [Рекомендации по назначению сайта клиента](../../core/plan-design/hierarchy/interoperability-between-different-versions.md#BKMK_SupConfigSiteAssignment) раздела [Взаимодействие различных версий System Center Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  

## <a name="plan-topics"></a>Разделы по планированию  
 Следующие разделы содержат справочные сведения о планировании миграции поддерживаемой исходной иерархии в конечную иерархию System Center Configuration Manager:

-   [Необходимые условия для миграции в System Center Configuration Manager](../../core/migration/prerequisites-for-migration.md)  

-   [Контрольные списки администратора по планированию миграции в System Center Configuration Manager](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [Определение необходимости миграции данных в System Center Configuration Manager](../../core/migration/determine-whether-to-migrate-data.md)  

-   [Планирование стратегии для исходных иерархий в System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md)  

-   [Контрольные списки администратора по планированию миграции в System Center Configuration Manager](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [Планирование стратегии миграции клиентов в System Center Configuration Manager](../../core/migration/planning-a-client-migration-strategy.md)  

-   [Планирование стратегии миграции для развертывания содержимого в System Center Configuration Manager](../../core/migration/planning-a-content-deployment-migration-strategy.md)  

-   [Планирование миграции объектов Configuration Manager в System Center Configuration Manager](../../core/migration/planning-for-the-migration-of-objects.md)  

-   [Планирование наблюдения за действиями миграции в System Center Configuration Manager](../../core/migration/planning-to-monitor-migration-activity.md)  

-   [Планирование завершения миграции в System Center Configuration Manager](../../core/migration/planning-to-complete-migration.md)  
