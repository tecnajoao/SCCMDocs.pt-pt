---
title: "Необходимые условия для ведения отчетов | Документы Майкрософт"
description: "Сведения о различных зависимостях, которые влияют на использование отчетов в System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9cc508a5-5023-4833-b776-ae9a6971138f
caps.latest.revision: "5"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 2e624eb2ea061a4eb7d92365410fada335640224
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="prerequisites-for-reporting-in-system-center-configuration-manager"></a>Необходимые условия для ведения отчетов в System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

Функция отчетов в System Center Configuration Manager имеет внешние зависимости и зависимости в пределах продукта.  

## <a name="dependencies-external-to-configuration-manager"></a>Внешние зависимости Configuration Manager  
 В следующей таблице перечислены внешние зависимости для отчетов.  

|Необходимое условие|Дополнительные сведения|  
|------------------|----------------------|  
|SQL Server Reporting Services|Перед использованием отчетов в Configuration Manager необходимо установить и настроить службы SQL Server Reporting Services.<br /><br /> Сведения о планировании и развертывании Reporting Services в вашей среде см. в разделе [Службы отчетов](http://go.microsoft.com/fwlink/p/?LinkId=212032) в документации к SQL Server 2008 в Интернете.|  
|Зависимости ролей систем сайта для компьютеров, на которых находится точка служб отчетов.|[Поддерживаемые конфигурации для System Center Configuration Manager](../../../core/plan-design/configs/supported-configurations.md)|  

## <a name="dependencies-internal-to-configuration-manager"></a>Внутренние зависимости Configuration Manager  
 В приведенной ниже таблице перечислены зависимости для отчетов в Configuration Manager.  

|Необходимое условие|Дополнительные сведения|  
|------------------|----------------------|  
|Точка служб отчетов|Чтобы создавать отчеты в Configuration Manager, необходимо настроить роль системы сайта "Точка служб отчетов". Дополнительные сведения об установке и настройке точки служб отчетов см. в разделе [Настройка отчетов в System Center Configuration Manager](../../../core/servers/manage/configuring-reporting.md).|  

## <a name="supported-sql-server-versions-for-the-reporting-services-point"></a>Поддерживаемые версии SQL Server для точки служб отчетов  
 Базу данных служб отчетов можно установить на экземпляре по умолчанию или на именованном экземпляре 64-разрядной версии SQL Server. Экземпляр SQL Server может размещаться на одном компьютере с сервером системы сайта или на удаленном компьютере.  

 В следующей таблице приведены версии SQL Server, поддерживаемые точками служб отчетов.  

|Версия SQL Server|Точка служб отчетов|  
|------------------------|------------------------------|  
|SQL Server 2008 с пакетом обновления 2 (SP2) и минимальным накопительным пакетом обновления 9<br /><br /> — Standard<br />— Enterprise<br />— Datacenter|Да|  
|SQL Server 2008 с пакетом обновления 3 (SP3) и минимальным накопительным пакетом обновления 4<br /><br /> — Standard<br />— Enterprise<br />— Datacenter|Да|  
|SQL Server 2008 R2 с пакетом обновления 1 (SP1) и минимальным накопительным пакетом обновления 6<br /><br /> — Standard<br />— Enterprise<br />— Datacenter|Да|  
|SQL Server 2008 R2 с пакетом обновления 2 (SP2)<br /><br /> — Standard<br />— Enterprise<br />— Datacenter|Да|  
|SQL Server Express 2008 R2 с пакетом обновления 1 (SP1) и минимальным накопительным пакетом обновления 4|Не поддерживается|  
|SQL Server Express 2008 R2 с пакетом обновления 2 (SP2)|Не поддерживается|  
|SQL Server 2012 с минимальным накопительным пакетом обновления 2<br /><br /> — Standard<br />— Enterprise|Да|  
|SQL Server 2012 с пакетом обновления 1 (SP1) и без минимального накопительного пакета обновления<br /><br /> — Standard<br />— Enterprise|Да|  
|SQL Server 2014<br /><br /> — Standard<br />— Enterprise|Да|
|SQL Server 2016<br /><br /> — Standard<br />— Enterprise|Да|
|SQL Server 2016 с пакетом обновления 1 (SP1)<br /><br /> — Standard<br />— Enterprise|Да|
## <a name="next-steps"></a>Дальнейшие действия
[Использование и обслуживание отчетов](operations-and-maintenance-for-reporting.md)
