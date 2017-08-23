---
title: "Общие сведения о запросах | Документы Майкрософт"
description: "Создавать и отправлять запросы для поиска объектов в иерархии System Center Configuration Manager, соответствующей выбранным условиям."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 03d1b3a9-41db-4d3a-a70e-e05ab5dc8141
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: f84d518670c0ece3c08c890d2293335518f7f8e9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="introduction-to-queries-in-system-center-configuration-manager"></a>Общие сведения о запросах в System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

Можно создавать и отправлять запросы для поиска объектов в иерархии System Center Configuration Manager, соответствующей выбранным условиям. В число таких объектов входят определенные типы компьютеров или групп пользователей. Запросы позволяют возвращать большую часть типов объектов Configuration Manager, в том числе сайтов, коллекций, приложений и данных инвентаризации.  

 При создании запроса необходимо указать не менее двух параметров: область поиска и предмет поиска. Например, чтобы найти сведения об объеме пространства на жестком диске, доступного на всех компьютерах сайта Configuration Manager, можно создать запрос для поиска класса атрибута **Логический диск** и атрибута **Свободно (МБ)**, определяющего доступный объем места.  

 После создания первоначального запроса можно указать дополнительные условия. Например, можно указать, чтобы в результаты запроса входили только компьютеры, назначенные определенному сайту. Кроме того, можно изменить способ отображения результатов для их просмотра в удобном для вас порядке. Например, можно указать, чтобы результаты сортировались по объему свободного пространства на жестком диске в порядке возрастания или убывания.  

 При создании запроса он сохраняется Configuration Manager и отображается в узле **Запросы** рабочей области **Мониторинг**. В этом узле можно создать новый запрос, а затем выполнить, обновить или управлять существующим запросом.  

 Можно также импортировать запрос в правило запроса коллекции Configuration Manager. Дополнительные сведения см. в статье [Создание коллекций в System Center Configuration Manager](../../../core/clients/manage/collections/create-collections.md).  

## <a name="see-also"></a>См. также  
 [Технический справочник по запросам для System Center Configuration Manager](../../../core/servers/manage/queries-technical-reference.md)
