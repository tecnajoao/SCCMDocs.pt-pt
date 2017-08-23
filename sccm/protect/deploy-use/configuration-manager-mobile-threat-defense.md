---
title: Mobile Threat Defense | System Center Configuration Manager
description: "Ограничение доступа к ресурсам компании на основе риска для устройства, сети и приложения с помощью Configuration Manager и решений партнеров Intune Mobile Threat Defense"
ms.custom: na
ms.date: 03/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4c0e6824-2dfe-4700-b817-d5631e0eb872
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 298d879638a2d20d421b19752cb5f20f6725df14
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="intune-mobile-threat-defense-connectors-in-configuration-manager"></a>Соединители Intune Mobile Threat Defense в Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

[Гибридное развертывание системы управления мобильными устройствами (SCCM с Intune)](https://docs.microsoft.com/en-us/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management) и интеграция между Intune и партнерами Mobile Threat Defense дает возможность контролировать доступ к ресурсам компании и данным на основе оценки риска устройства.

Соединители Intune Mobile Threat Defense позволяют использовать выбранного поставщика Mobile Threat Defense как источник информации для политик соответствия и правил условного доступа. Это позволяет ИТ-администраторам добавить уровень защиты корпоративных ресурсов, например Exchange или Sharepoint, особенно если дело касается скомпрометированных мобильных устройств.

## <a name="what-problem-does-this-solve"></a>Какую проблему это решает?

Организациям требуется защищать конфиденциальные данные от новых угроз, включающих физические, основанные на приложениях и сетевые угрозы, а также уязвимости операционной системы.
Сложилось так, что организации действуют с упреждением, когда дело касается защиты компьютеров от атак, однако при этом не уделяют должного внимания мониторингу и защите мобильных устройств. Мобильные платформы имеют встроенную защиту, такую как изоляция приложений и проверка приложений для пользователей в магазинах, однако остаются уязвимыми для более сложных атак. Сейчас все больше сотрудников используют устройства для работы и нуждаются в доступе к конфиденциальной информации. Эти устройства нужно защитить от постоянно совершенствующихся атак.

## <a name="how-the-intune-mobile-threat-defense-connectors-work"></a>Принцип работы соединителей Intune Mobile Threat Defense

Соединитель защищает ресурсы компании, создавая канал связи между Intune и выбранным поставщиком Mobile Threat Defense. Партнеры Intune Mobile Threat Defense предлагают интуитивно понятные, простые в развертывании приложения для мобильных устройств, которые активно сканируют и анализируют сведения об угрозах и передают их в Intune для формирования отчетности либо в принудительных целях. Например, если подключенное приложение Mobile Threat Defense сообщает поставщику Mobile Threat Defense о том, что телефон в вашей сети в настоящее время подключен к сети, уязвимой для атак "злоумышленник в середине". Эти сведения передаются дальше и относятся к соответствующему уровню риска (низкий, средний или высокий), которые сравниваются с допусками, настроенными для уровня риска в Intune. Это позволяет определить, следует ли отозвать доступ к определенным ресурсам, если устройство скомпрометировано.

## <a name="sample-scenarios"></a>Примеры сценариев

Если решение Mobile Threat Defense определяет, что устройство заражено:

![](http://i.imgur.com/Li1WUOU.png)

Доступ предоставляется после того, как устройство исправлено:

![](http://i.imgur.com/VCIwpdz.png)

## <a name="mobile-threat-defense-partners"></a>Партнеры Mobile Threat Defense

Узнайте, как защитить доступ к ресурсам компании на основе рисков, связанных с устройствами, сетями и приложениями, с помощью:

- [Lookout](https://docs.microsoft.com/sccm/protect/deploy-use/lookout-mobile-threat-defense-in-configuration-manager)