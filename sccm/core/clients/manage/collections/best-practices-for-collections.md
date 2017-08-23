---
title: "Рекомендации для коллекций | Документы Майкрософт"
description: "Воспользуйтесь приведенными далее рекомендациями по работе с коллекциями в System Center Configuration Manager."
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7a2abb79-9ae5-4a25-9e18-5dcf528de3bf
caps.latest.revision: "4"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: fd62af3910c0745e0f1105417701b894e10cbbac
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="best-practices-for-collections-in-system-center-configuration-manager"></a>Рекомендации для коллекций в System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

Воспользуйтесь приведенными далее рекомендациям по работе с коллекциями в System Center Configuration Manager.  

## <a name="do-not-use-incremental-updates-for-a-large-number-of-collections"></a>Не используйте добавочные обновления для большого числа коллекций.  
 Установка флажка **Использовать добавочные обновления для этой коллекции** может привести к задержке оценки, если эта конфигурация задана для многих коллекций. Пороговое значение — около 200 коллекций в иерархии. Точное число зависит от следующих факторов:  

-   общее число коллекций,  

-   частота добавления и изменения ресурсов в иерархии,  

-   число клиентских устройств в иерархии,  

-   сложность правил членства в коллекции в иерархии.  

## <a name="make-sure-that-maintenance-windows-are-large-enough-to-deploy-critical-software-updates"></a>Убедитесь, что периоды обслуживания обладают достаточной длительностью для развертывания критических обновлений программного обеспечения.  
 Можно настроить периоды обслуживания для коллекций устройств, чтобы ограничить интервалы времени, в течение которых Configuration Manager может устанавливать программное обеспечение на устройства. Если установить слишком маленький период обслуживания, клиент может не успеть установить важные обновления программного обеспечения и останется уязвимым для атак, для защиты от которых и предназначены обновления.  
