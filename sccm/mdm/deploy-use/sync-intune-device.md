---
title: "Удаленная синхронизация политики на устройствах, зарегистрированных в Intune | Документы Майкрософт"
description: "Узнайте, как синхронизировать политику на зарегистрированных в Intune устройствах из консоли Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b3731ad0-2a24-4042-994e-5e4c1230e3fe
caps.latest.revision: "18"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 337814fd5ba49ed17fc97aba49f79f02df817f4e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="remotely-synchronize-policy-on-intune-enrolled-devices-from-the-configuration-manager-console"></a>Удаленная синхронизация политики на зарегистрированных в Intune устройствах из консоли Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*


Вы можете запросить синхронизацию политики для зарегистрированного в Intune устройства из консоли Configuration Manager вместо того, чтобы запрашивать синхронизацию в приложении корпоративного портала на самом устройстве. 

Для этого выполните следующие действия.

1.  Выберите устройство в узле **Активы и соответствие** > **Обзор** > **Устройства**.
2.  В меню **Действия удаленного устройства** выберите команду **Отправить запрос синхронизации**.


Через 5–10 минут все изменения политики будут синхронизированы с устройством. Сведения о состоянии запроса синхронизации можно просмотреть в новом столбце **Состояние удаленной синхронизации** в представлениях устройств, а также в разделе данных обнаружения в диалоговом окне **Свойства** для каждого отдельного устройства.
