---
title: "Включение Lookout MTP в Intune | Документация Майкрософт"
description: "Вы можете включить Lookout Mobile Threat Protection в консоли администрирования Intune."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7e4ada34-63bf-4b9f-8246-31816aa44196
caps.latest.revision: 
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: f9ddbcc981fa1274a41ae16a6a939c0cdf739c3e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="enable-lookout-mtp-connection-in-the-intune-admin-console"></a>Включение подключения к Lookout MTP в консоли администрирования Intune

*Применимо к: System Center Configuration Manager (Current Branch)*

В этом разделе показано, как включить подключение к Lookout MTP в Intune. Перед выполнением этого действия соединитель Intune Connector уже должен быть настроен в консоли Lookout.  Если вы этого еще не сделали, выполните инструкции в разделе [Настройка службы защиты от угроз на устройствах Lookout в подписке](set-up-your-subscription-with-lookout.md).

Чтобы включить подключение к Lookout MTP в Intune, на странице **Администрирование** в [консоли администрирования Microsoft Intune](https://manage.microsoft.com) выберите **Интеграция со сторонней службой**. Выберите пункт **Состояние Lookout** и включите параметр **Синхронизация с MTP** с помощью переключателя.

![снимок экрана страницы синхронизации Lookout с выделенным переключателем](media/lookout-intune-synchronization.png)

Интеграция Lookout и Intune в консоли администратора Intune на этом завершена.  Для реализации решения потребуется выполнить еще ряд действия, в частности развернуть [приложения Lookout for Work](configure-and-deploy-lookout-for-work-apps.md) и настроить политику [соответствия требованиям](enable-device-threat-protection-rule-compliance-policy.md).

>[!IMPORTANT]
> Приложение Lookout for Work **необходимо** настроить перед созданием правил политики соответствия требованиям и настройкой условного доступа. Это позволит гарантировать, что приложение будет готово к работе и доступно для установки конечными пользователями, когда им потребуется доступ к электронной почте и другим корпоративным ресурсам.

## <a name="next-steps"></a>Дальнейшие действия
[Настройка приложения Lookout for Work ](configure-and-deploy-lookout-for-work-apps.md)
