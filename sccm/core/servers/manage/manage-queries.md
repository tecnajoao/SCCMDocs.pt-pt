---
title: "Управление запросами | Документы Майкрософт"
description: "Сведения об управлении запросами. Содержит подробную справочную таблицу."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e562e2a0-8df8-4952-952f-e8c38461c612
caps.latest.revision: "6"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 738dcf0b52f18b38b732bf8ca5d7a87369b1c468
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-manage-queries-in-system-center-configuration-manager"></a>Управление запросами в System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

Используйте сведения в это статье для управления запросами в System Center Configuration Manager.  

 Сведения о том, как создавать запросы, см. в статье [Создание запросов в System Center Configuration Manager](../../../core/servers/manage/create-queries.md).  

## <a name="how-to-manage-queries"></a>Управление запросами  
 В рабочей области **Мониторинг** последовательно выберите **Запросы**, запрос для управления и задачу управления.  

 Для получения дополнительных сведений о задачах управления, которые могут требовать указания некоторой информации перед их выбором, используйте следующую таблицу.  

|Задача управления|Подробные сведения|Дополнительные сведения|  
|---------------------|-------------|----------------------|  
|**Выполнить**|Выполнение выбранного запроса и отображение результатов на консоли Configuration Manager.|Дополнительные сведения отсутствуют.|  
|**Установить клиент**|Открытие компонента **Мастер установки клиента**, который позволяет установить клиент Configuration Manager на компьютерах, возвращенных при выполнении выбранного запроса.<br /><br /> Этот параметр недоступен для запросов, возвращающих мобильные устройства, пользователей или группы пользователей.|Дополнительные сведения об установке клиентов Configuration Manager с помощью принудительной установки см. в статье [Развертывание клиентов на компьютерах Windows](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).|  
|**Экспортировать**|Открытие компонента **Мастер экспорта объектов** , который позволяет экспортировать этот запрос в MOF-файл, затем импортируемый на другой сайт.|Дополнительные сведения отсутствуют.|  
|**Переместить**|Открытие диалогового окна **Переместить выбранные элементы** , в котором можно переместить выбранный запрос в папку, ранее созданную в узле **Запросы** .|Дополнительные сведения отсутствуют.|  

## <a name="see-also"></a>См. также  
 [Использование и обслуживание запросов в System Center Configuration Manager](../../../core/servers/manage/operations-and-maintenance-for-queries.md)
