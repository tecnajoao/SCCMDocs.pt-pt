---
title: "Создание коллекции MDM с помощью System Center Configuration Manager | Документация Майкрософт"
description: "Создание коллекции MDM с помощью System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d1b4337f-85e8-45e6-8bbe-9f18b49041c7
caps.latest.revision: "18"
caps.handback.revision: "0"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: fabbcfd2d5656d4fa8cb87feffe87e17998df145
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="create-an-mdm-collection-with-system-center-configuration-manager-and-microsoft-intune"></a>Создание коллекции MDM с помощью System Center Configuration Manager и Microsoft Intune

*Применимо к: System Center Configuration Manager (Current Branch)*

Коллекция пользователей Configuration Manager необходима для указания пользователей, которые могут регистрировать устройства для управления. Можно использовать только коллекции пользователей (но не коллекции устройств), так как лицензии Intune назначаются пользователям.

> [!NOTE]
> Для регистрации устройств в Intune не нужно назначать лицензии пользователям на портале Office 365 или портале Azure Active Directory. Нужно всего лишь включить пользователей в коллекцию, связанную с подпиской Intune (при выполнении [следующего шага](configure-intune-subscription.md)).

В целях тестирования можно настроить **прямое правило** и добавить конкретных пользователей, которые могут регистрировать устройства. В консоли Configuration Manager выберите **Активы и соответствие** > **Коллекции пользователей**, откройте вкладку **Главная**, в группе **Создать** щелкните **Создать коллекцию пользователей**. Для более широкого распространения следует использовать **правила запросов**, позволяющие определять пользователей. Дополнительные сведения о коллекциях см. в статье [Создание коллекций](https://technet.microsoft.com/library/mt629371.aspx).

![Создание коллекции пользователей для MDM](../media/mdm-create-user-collection.png)

> [!div class="button"]
[Следующий этап >](confirm-dns.md)
