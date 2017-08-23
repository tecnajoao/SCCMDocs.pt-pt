---
title: "Основные сведения о System Center Configuration Manager | Документы Майкрософт"
description: "Основные понятия, связанные с System Center Configuration Manager."
ms.custom: na
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc4cdb35-f0b4-42b5-9cec-6431a8c30793
caps.latest.revision: "11"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 662ac092746f37c354e5accf288e3375c16b9c72
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="fundamentals-of-system-center-configuration-manager"></a>Основные сведения о Microsoft System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

Если вы еще не работали с System Center Configuration Manager, прежде чем запускать программу установки для установки своего первого сайта, прочитайте основополагающие разделы, чтобы узнать об основных понятиях Configuration Manager. Если вы уже знакомы с Configuration Manager, можете сразу приступить к работе. Мы рекомендуем начать с раздела [Новые возможности System Center Configuration Manager](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012).  

 Для получения сведений о поддерживаемых операционных системах и средах, требованиях к аппаратному обеспечению и возможностях см. раздел [Supported configurations for System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md).  

 При развертывании Configuration Manager развертывается один или несколько сайтов.  

-   **При развертывании нескольких сайтов**между ними формируются иерархические отношения. Иерархия позволяет централизованно управлять большим количеством сайтов и устройств.  Данные и информация передаются с верхних уровней в нижние и таким образом достигают управляемых устройств. Сведения об устройствах, результаты выполнения задач настройки и поток запросов поднимаются по иерархии вверх.  

-   Иерархия возникает, даже если **развертывается всего один сайт**.  

 Одни задачи настройки и параметры применяются ко всем сайтам в иерархии, в то время как другие относятся только к отдельным сайтам.  

## <a name="fundamental-concepts-for-system-center-configuration-manager"></a>Основные понятия System Center Configuration Manager
В следующих разделах описаны основные понятия System Center Configuration Manager:  

-   [Основные принципы работы сайтов и иерархий в System Center Configuration Manager](../../core/understand/fundamentals-of-sites-and-hierarchies.md)  

-   [Основные принципы управления устройствами с помощью System Center Configuration Manager](../../core/understand/fundamentals-of-managing-devices.md)  

-   [Основные принципы выполнения задач управления клиентами для System Center Configuration Manager](../../core/understand/fundamentals-of-client-management-tasks.md)  

-   [Основы безопасности для System Center Configuration Manager](../../core/understand/fundamentals-of-security.md)  
