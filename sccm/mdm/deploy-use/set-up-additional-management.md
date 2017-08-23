---
title: "Настройка дополнительного управления с помощью System Center Configuration Manager | Документация Майкрософт"
description: "Настройте дополнительное управление с помощью System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4877d674-6bbc-4e16-810c-daad70c74daa
caps.latest.revision: "18"
caps.handback.revision: "0"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 947d2a85f2ac68c7ccaf9a1237fd60e89e7d1d10
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="set-up-additional-management-with-system-center-configuration-manager"></a>Настройка дополнительного управления с помощью System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

Дополнительное управление можно настроить до регистрации устройств (необязательно). Решения по управлению можно создать и развернуть после регистрации устройств, несмотря на то, что многие организации предпочитают развертывать их после ввода устройств в режим управления.

**Элементы конфигурации** позволяют управлять параметрами, такими как требование ПИН-кода или требование шифрования на зарегистрированных устройствах на основе платформы устройства:
- [Устройства Windows 10 и Windows 8.1](create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)
- [Устройства Windows Phone](create-configuration-items-for-windows-phone-devices-managed-without-the-client.md)
- [Устройства iOS и Mac](create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client.md)
- [Устройства Android и Samsung KNOX Standard](create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md)

На управляемых устройствах можно развернуть следующие **приложения**:
- [Приложения для iOS](creating-ios-applications.md)
- [Приложения для Mac](../../apps/get-started/creating-mac-computer-applications.md)
- [Приложения для ПК Windows](../../apps/get-started/creating-windows-applications.md)
- [Приложения для Windows Phone](creating-windows-phone-applications.md)
- [Приложения для Android](creating-android-applications.md)

**Условный доступ** позволяет управлять доступом к ресурсам компании, включая:  
- [Доступ к электронной почте](manage-email-access.md)
- [Доступ к SharePoint](manage-sharepoint-online-access.md)
- [Доступ к Skype для бизнеса](manage-skype-for-business-online-access.md)
- [Dynamic CRM Online](manage-dynamics-crm-online-access.md)

**Многофакторная идентификация (MFA)** позволяет реализовать несколько методов проверки, которые добавляют критически важный второй уровень безопасности при операциях входа и транзакциях пользователей.
Чтобы настроить MFA для регистраций в Intune, ранее необходимо было перейти в консоль Intune или консоль Configuration Manager. Теперь можно войти на [портал Microsoft Azure](https://manage.windowsazure.com), используя свои учетные данные Intune, и настроить параметры MFA с помощью Azure AD. Дополнительные сведения см. в статье [Многофакторная идентификация для регистрации устройств в Intune](https://aka.ms/mfa_ad).

> [!div class="button"]
[< Назад](enable-platform-enrollment.md) [Вперед >](verify-mdm-configuration.md)
