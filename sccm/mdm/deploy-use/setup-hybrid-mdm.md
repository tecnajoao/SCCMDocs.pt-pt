---
title: "Настройка гибридного управления мобильными устройствами | Документы Майкрософт"
description: "Настройка гибридной регистрации устройств с помощью Configuration Manager и Intune."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
caps.latest.revision: "34"
caps.handback.revision: "0"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: c494fcc38955571c06507278a1ae88e5777b5708
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="setup-hybrid-mobile-device-management-mdm-with-system-center-configuration-manager-and-microsoft-intune"></a>Настройка гибридного управления мобильными устройствами (MDM) с помощью System Center Configuration Manager и Microsoft Intune

*Применимо к: System Center Configuration Manager (Current Branch)*


Прежде чем начать управление устройствами iOS, Windows и Android с помощью Configuration Manager, их необходимо зарегистрировать в Intune. Выполните следующие действия, чтобы настроить гибридную регистрацию устройств гибридной установки в Configuration Manager с помощью Intune. После этого пользователи смогут регистрировать личные устройства (BYOD). Эти действия также являются обязательными для [регистрации устройств BYOD](enroll-hybrid-ios-mac.md) и [устройств, принадлежащих компании](enroll-company-owned-devices.md).

 |Шаги|Подробные сведения|  
 |-----------|-------------|  
 |**Шаг 1.** [Создание коллекции MDM](create-mdm-collection.md)|Создание коллекции пользователей Configuration Manager, включающую пользователей, устройства которых могут быть зарегистрированы.|  
 |**Шаг 2.** [Требования к имени домена](confirm-dns.md)|Проверка DNS-службы и управления пользователями Active Directory в организации на соответствие требованиям MDM.|
 |**Шаг 3.** [Настройка подписки Intune](configure-intune-subscription.md)|Служба Intune позволяет управлять устройствами через Интернет.|  
 |**Шаг 4.** [Добавление условий](terms-and-conditions.md)| Создание условий, которые должны принять пользователи, прежде чем они смогут использовать приложение портала компании.|
 |**Шаг 5.** [Создание точки подключения службы](create-service-connection-point.md)|Точка подключения службы отправляет параметры и сведения о развертывании ПО в Configuration Manager и получает сообщения о состоянии и инвентаризации от мобильных устройств. |  
 |**Шаг 6.** [Включение регистрации платформы](enable-platform-enrollment.md)|Для включения регистрации MDM для устройств iOS и Windows требуется выполнить дополнительные действия по обеспечению взаимодействия между службой и устройствами. Для устройств Android никаких дополнительных настроек не требуется.|  
 |**Шаг 7.** [Настройка дополнительного управления](set-up-additional-management.md)|Настройка элементов конфигурации и условного доступа для зарегистрированных устройств (необязательно)|
 |**Шаг 8.** [Проверка конфигурации MDM](verify-mdm-configuration.md)|Просмотр файлов журнала для проверки успешного создания точки подключения службы и синхронизации учетных записей пользователей.|

Требуется Intune без Configuration Manager?
> [!div class="button"]
[Просмотрите документы по Intune >](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune)


## <a name="enroll-devices"></a>регистрации устройств;
По завершении гибридной настройки устройства можно зарегистрировать в Configuration Manager несколькими способами.
- **Устройства, принадлежащие компании (COD):** [в этой статье](enroll-company-owned-devices.md) содержатся рекомендации по регистрации принадлежащих компании устройств на разных платформах.
- **Пользовательские устройства (BYOD):** [в этой статье](enroll-hybrid-ios-mac.md) содержатся рекомендации по регистрации пользовательских устройств.
