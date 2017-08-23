---
title: "Обновление клиентов для Linux и UNIX в Configuration Manager | Документы Майкрософт"
description: "Наблюдайте за клиентами для серверов Linux и UNIX в System Center Configuration Manager."
ms.custom: na
ms.date: 08/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d827cf91-b18f-4ee7-b538-24ba6f003ab9
caps.latest.revision: "6"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 62843bd544217734c4566d656a7c3a35bd5613cb
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-monitor-clients-for-linux-and-unix-servers-in-system-center-configuration-manager"></a>Мониторинг клиентов для серверов Linux и UNIX в System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

Для просмотра сведений с серверов Linux и UNIX в консоли System Center Configuration Manager используются те же методы, что и для просмотра сведений с клиентских компьютеров под управлением Windows.  

 Для просмотра доступны следующие данные.  

-   Сведения о состоянии клиентов на панелях мониторинга консоли Configuration Manager  

-   Сведения о клиентах в отчетах Configuration Manager по умолчанию  

-   Сведения об инвентаризации в обозревателе ресурсов  

 В следующих разделах описывается, как получить эти сведения из обозревателя ресурсов и отчетов.  

##  <a name="BKMK_UseResourceExpforLnU"></a> Использование обозревателя ресурсов для просмотра данных инвентаризации для серверов Linux и UNIX  

 После того как клиент Configuration Manager отправит данные инвентаризации оборудования на сайт Configuration Manager, эти сведения вы можете просмотреть с помощью обозревателя ресурсов. Клиент Configuration Manager для Linux и UNIX не добавляет в обозреватель ресурсов новые классы или представления для инвентаризации. Данные инвентаризации Linux и UNIX сопоставляются с существующими WMI-классами. С помощью обозревателя ресурсов вы можете просмотреть сведения об инвентаризации для серверов Linux и UNIX в классификациях на основе Windows.  

 Например, вы можете составить список всех изначально установленных программ, обнаруженных на серверах Linux и UNIX. Примерами изначально установленных программ являются **.rpms** в Linux или **.pkgs** в Solaris. После того как клиент Linux или UNIX отправит данные инвентаризации, в обозревателе ресурсов в консоли Configuration Manager вы можете просмотреть список всех изначально установленных программ UNIX или Linux.  

 Сведения о том, как использовать обозреватель ресурсов, см. в разделе [Использование обозревателя ресурсов для просмотра данных инвентаризации оборудования в System Center Configuration Manager](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).  

##  <a name="BKMK_UseReportsforLnU"></a> Использование отчетов для просмотра сведений для серверов Linux и UNIX  
 Отчеты для Configuration Manager содержат сведения с серверов Linux и UNIX, а также сведения с компьютеров под управлением Windows. Для интеграции данных в отчетах Linux и UNIX выполнять дополнительные настройки не требуется.  

 Например, при выполнении отчета с именем «Количество версий операционной системы» в нем отображается список других операционных систем и количество клиентов, работающих под управлением каждой операционной системы. Отчет основан на данных инвентаризации оборудования, которые были отправлены различными клиентами Configuration Manager, работающими в разных операционных системах.  

 Кроме того, вы можете создать настраиваемые отчеты, связанные с данными серверов Linux и UNIX. Свойство **Caption** класса инвентаризации оборудования **Operating System** является полезным атрибутом, который вы можете использовать для идентификации конкретных операционных систем в запросе отчета.  

 Сведения об отчетах в Configuration Manager см. в разделе [Ведение отчетов в System Center Configuration Manager](../../../core/servers/manage/reporting.md).  
