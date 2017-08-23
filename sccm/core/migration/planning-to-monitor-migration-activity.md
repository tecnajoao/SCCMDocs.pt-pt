---
title: "Мониторинг миграции | Документы Майкрософт"
description: "Узнайте, как использовать консоль Configuration Manager для отслеживания хода выполнения и успешности заданий миграции."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fc731d3f-edd7-4049-b17b-653d6693a564
caps.latest.revision: "4"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 896807ec2c4be2835094a27add59d4cc09e93add
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="planning-to-monitor-migration-activity-in-system-center-configuration-manager"></a>Планирование наблюдения за действиями миграции в System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

В System Center Configuration Manager вы можете отслеживать миграцию в консоли Configuration Manager, которая подключена к конечной иерархии. В консоли Configuration Manager в рабочей области **Администрирование** можно использовать узел **Миграция** для наблюдения за ходом выполнения и успешностью заданий миграции. Вы можете просмотреть сводные данные по каждому заданию миграции, определяющему перенесенные объекты, объекты, которые еще не перенесены и число объектов, исключенных из задания миграции. Вы также увидите подробные сведения обо всех проблемах миграции.  

## <a name="view-migration-progress"></a>Просмотр процесса миграции  
 Чтобы просмотреть ход выполнения задания миграции, выполните одно из следующих действий.  

-   В рабочей области **Администрирование** консоли Configuration Manager разверните узел **Задания миграции**, выберите задание миграции, а затем откройте вкладку **Объекты в задании**.  

-   Используйте файлы журналов Configuration Manager для анализа процесса миграции или определения каких-либо проблем. Диспетчер миграции — это процесс Configuration Manager, отслеживающий действия миграции и регистрирующий их в файле migmctrl.log, сохраняемом в папке **\&lt;путь_установки\>\\LOGS** на сервере сайта.  

    > [!NOTE]  
    >  Если задание миграции не выполнено, как можно скорее просмотрите сведения в файле migmctrl.log. Записи журнала миграции непрерывно добавляются в файл и перезаписывают старую информацию. Если записи перезаписаны, возможно, вы не сможете определить, связаны ли с миграцией какие-либо проблемы, возникающие с перенесенными объектами. Действия миграции регистрируются на сайте верхнего уровня в иерархии независимо от сайта, к которому подключается консоль Configuration Manager при настройке миграции.  

-   Используйте отчеты Configuration Manager. В Configuration Manager есть несколько встроенных отчетов о миграции, которые можно использовать как есть или изменить в соответствии со своими требованиями. Дополнительные сведения об отчетах Configuration Manager см. в разделе [Ведение отчетов в System Center Configuration Manager](../../core/servers/manage/reporting.md).  
