---
title: "Необходимые условия для управления питанием | Документы Майкрософт"
description: "Ознакомьтесь с необходимыми условиями для управления питанием в System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9c062f13-3c1f-4621-9cae-de0e322aa03f
caps.latest.revision: "4"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 711ef491899846b86bfed0355ac7fd0f9d509c4f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="prerequisites-for-power-management-in-system-center-configuration-manager"></a>Необходимые условия для управления питанием в System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

Функция управления питанием в System Center Configuration Manager имеет внешние зависимости и зависимости в пределах продукта.  

## <a name="dependencies-external-to-configuration-manager"></a>Внешние зависимости Configuration Manager  
 Приведенная ниже таблица содержит список внешних зависимостей Configuration Manager для использования функций управления питанием.  

|Зависимость|Дополнительные сведения|  
|----------------|----------------------|  
|Клиентские компьютеры должны поддерживать требуемые режимы питания.|Чтобы использовать все возможности функций управления питанием, клиентские компьютеры должны поддерживать спящий режим, режим гибернации, выход из спящего режима и выход из режима гибернации. Соответствующие сведения о поддержке содержатся в отчете **Возможности электропитания** . Дополнительные сведения см. в подразделе [Отчет "Возможности электропитания"](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Capabilites) раздела [Отслеживание и планирование управления питанием в System Center Configuration Manager](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).|  

## <a name="configuration-manager-dependencies"></a>Зависимости Configuration Manager  
 Приведенная ниже таблица содержит список зависимостей в Configuration Manager для использования функций управления питанием.  

|Зависимость|Дополнительные сведения|  
|----------------|----------------------|  
|Прежде чем можно будет создавать схемы управления питанием и отслеживать их выполнение, необходимо включить функцию управления питанием.|Сведения о включении и настройке управления питанием см. в разделе [Настройка функций управления питанием в System Center Configuration Manager](../../../../core/clients/manage/power/configuring-power-management.md).|  
|Точка служб отчетов|Прежде чем можно будет просматривать отчеты управления питанием, необходимо настроить точку служб отчетов. Дополнительные сведения см. в статье [Ведение отчетов в System Center Configuration Manager](../../../../core/servers/manage/reporting.md).|  
