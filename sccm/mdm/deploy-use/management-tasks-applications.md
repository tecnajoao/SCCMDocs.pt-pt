---
title: "Управление приложениями в System Center Configuration Manager | Документация Майкрософт"
description: "Управление приложениями в System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8adbe2e2-de26-4a80-8bbd-a5f34b8bac79
caps.latest.revision: "18"
caps.handback.revision: "0"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: bc7bb99bc526ed0bbaaad15fc9af39fa8b7c3893
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="manage-applications-in-system-center-configuration-manager"></a>Управление приложениями в System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

При управлении устройствами с помощью Microsoft Intune или локального управления устройствами Configuration Manager вы можете управлять следующими типами приложений:
- Пакет приложения Windows Phone (XAP-файл)
- Пакет приложения для iOS (IPA-файл)
- Пакет приложения для Android (APK-файл)
- Пакет приложения для ОС Android в Google Play
- Пакет приложения для ОС Windows Phone (в Магазине Windows)
- Установщик Windows через MDM (MSI)
- Веб-приложение

В этом разделе приведены подробные сведения о создании приложений и управлении ими с помощью гибридного или локального управления мобильными устройствами.

Общие сведения об управлении приложениями и типами развертывания System Center Configuration Manager см. в статье [Задачи управления для приложений System Center Configuration Manager](../../apps/deploy-use/management-tasks-applications.md).

## <a name="deploying-and-monitoring-apps"></a>Развертывание и мониторинг приложений

Процедуры развертывания и мониторинга приложений в System Center Configuration Manager на мобильных устройствах и на таких устройствах, как ноутбуки и настольные компьютеры, ничем не отличаются. Общие сведения о развертывании и мониторинге приложений см. в следующих статьях:

- [Развертывание приложений в System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md)
- [Мониторинг приложений из консоли System Center Configuration Manager](../../apps/deploy-use/monitor-applications-from-the-console.md)

Ниже приведены некоторые рекомендации, касающиеся управления мобильными устройствами, которые следует учитывать при развертывании и мониторинге приложений.

- Устройства, зарегистрированные в системе управления мобильными устройствами, не поддерживают имитацию развертывания, взаимодействие с пользователем и параметры планирования.

- Развертывание можно связать с политикой конфигурации приложения iOS, если таковая настроена. Дополнительные сведения см. в статье [Применение параметров к приложениям iOS с помощью политик конфигурации приложений в System Center Configuration Manager](configure-ios-apps-with-app-configuration-policies.md).

### <a name="next-steps"></a>Дальнейшие шаги

Со временем вам может потребоваться изменить приложение, удалить его или заменить уже развернутое приложение новым. Как это сделать см. в статье [Обновление и прекращение использования приложений с помощью System Center Configuration Manager](../../apps/deploy-use/update-and-retire-applications.md).
