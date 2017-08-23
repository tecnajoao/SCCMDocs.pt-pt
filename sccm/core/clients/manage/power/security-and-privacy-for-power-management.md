---
title: "Безопасность и конфиденциальность управления питанием | Документы Майкрософт"
description: "Сведения о безопасности и конфиденциальности управления питанием в System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 469ff35f-59a1-484d-902b-107dd6070baf
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 94d5418c364c318dba92dc9f9066f54d1130aa34
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-power-management-in-system-center-configuration-manager"></a>Безопасность и конфиденциальность управления питанием в System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

В этом разделе приводятся сведения о безопасности и конфиденциальности управления питанием в System Center Configuration Manager.  

## <a name="security-best-practices-for-power-management"></a>Рекомендации по обеспечению безопасности для управления питанием  
 Для функции управления питанием нет каких-то специальных рекомендаций по обеспечению безопасности.  

## <a name="privacy-information-for-power-management"></a>Сведения о конфиденциальности управления питанием  
 Функция управления питанием использует встроенные компоненты Windows для отслеживания энергопотребления и применения параметров питания к компьютерам в рабочее и нерабочее время. Configuration Manager собирает с компьютеров данные по энергопотреблению, включая сведения о периодах использования компьютера пользователем. Хотя Configuration Manager отслеживает энергопотребление для коллекции, а не для отдельных компьютеров, можно создать коллекцию, содержащую только один компьютер. Управление питанием не включено по умолчанию и должно быть настроено администратором.  

 Сведения об энергопотреблении сохраняются в базе данных Configuration Manager и не отправляются в Майкрософт. Подробные сведения хранятся в базе данных 31 день, сводные данные — 13 месяцев. Интервал удаления изменить нельзя.  

 Перед настройкой параметров управления питанием учтите требования к конфиденциальности.  
