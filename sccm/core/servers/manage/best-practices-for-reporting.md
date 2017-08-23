---
title: "Рекомендации по ведению отчетов | Документы Майкрософт"
description: "Ознакомьтесь с полезными советами по использованию возможности создания отчетов в System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 64f9d931-33f1-456f-a4e4-0ec077465bd0
caps.latest.revision: "4"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 759258999f3eaa810803a6a7f856f00fe7771a9e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="best-practices-for-reporting-in-system-center-configuration-manager"></a>Рекомендации по ведению отчетов в System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

Следуйте приведенным далее рекомендациям по ведению отчетов в System Center Configuration Manager.  

## <a name="for-best-performance-install-the-reporting-services-point-on-a-remote-site-system-server"></a>Для обеспечения оптимальной производительности точку служб отчетов рекомендуется установить на сервере удаленной системы сайта  
 Несмотря на возможность установки точки служб отчетов на сервере сайта или в удаленной системе сайта, производительность будет выше, если точка служб отчетов будет установлена на сервере удаленной системы сайта.  

## <a name="optimize-sql-server-reporting-services-queries"></a>Оптимизация запросов служб SQL Server Reporting Services  
 Как правило, задержки при создании отчетов возникают из-за времени, которое требуется на выполнение запросов и получение результатов. При использовании Microsoft SQL Server оптимизировать работу с запросами помогут такие средства, как профилировщик и анализатор запросов.  

## <a name="schedule-report-subscription-processing-to-run-outside-standard-office-hours"></a>Планирование выполнения обработки подписок на отчеты в нерабочее время  
 По возможности запланируйте выполнение обработки подписок на отчеты на нерабочее время. Это позволит снизить нагрузку на ЦП на сервере базы данных сайта Configuration Manager. Кроме того, повысится доступность непредсказуемых запросов отчетов.  

## <a name="next-steps"></a>Дальнейшие действия
[Настройка отчетов](configuring-reporting.md)
