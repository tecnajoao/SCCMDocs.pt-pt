---
title: "Развертывание приложения Lookout for Work | Документация Майкрософт"
description: "Сведения о настройке и развертывании приложений Lookout for Work."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3f62b763-4347-453d-b0a7-1f4a0d1d4105
caps.latest.revision: 
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 59f43c922d1d3bc64625733014b0def1e42c4d2d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="configure-and-deploy-lookout-for-work-apps"></a>Настройка и развертывание приложений Lookout for Work

*Применимо к: System Center Configuration Manager (Current Branch)*

В этой статье описывается настройка и развертывание приложения Lookout for Work для устройств Android и iOS.

## <a name="android-google-play-store-app"></a>Android (приложение магазина Google Play)
1.  В консоли Configuration Manager последовательно выберите **Библиотека программного обеспечения** > **Управление приложениями** > **Приложения**.

2.  На странице **Общие** мастера развертывания программного обеспечения укажите следующие сведения.
  * Тип: выберите **Пакет приложения для ОС Android в Google Play**.
  * Расположение: скопируйте ссылку на приложение Lookout for Work из магазина Google Play и вставьте ее здесь
  * Издатель: Lookout Mobile Security
  * Имя: Lookout for Work
  * Описание: Lookout предлагает лучшую защиту от мобильных угроз, чтобы обеспечить безопасность устройства. При установке приложения Lookout на устройстве оно защищает устройство от угроз и при обнаружении оповещает вас и администратора компании.
  * Административная категория: управление компьютерами

  После успешного завершения вы увидите приложение Lookout for Work в списке приложений.

3.  На вкладке **Главная** в группе **Развертывание** выберите **Развернуть**, чтобы развернуть приложение Lookout for Work для пользователей.
>[!IMPORTANT]
>Необходимо выбрать тех же пользователей, которые добавлены в параметр "Управление регистрацией" в консоли Lookout MTP.

  Выберите параметр **Обязательная установка**, чтобы установка приложения Lookout требовалась на устройстве пользователя.

## <a name="ios-enterprise-signed-version-of-lookout-app"></a>iOS (подписанная предприятием версия приложения Lookout)

* **Шаг 1.** Убедитесь в том, что **управление iOS** настроено на устройстве. Инструкцию по настройке устройства для управления iOS см. в разделе [Настройка управления устройствами в iOS и Mac]().

* **Шаг 2.** **Повторно подпишите** приложение Lookout for Work для iOS. Компания Lookout распространяет приложение Lookout for Work для iOS вне магазина iOS App Store. **Перед распространением приложения** необходимо повторно подписать приложение с помощью сертификата iOS Enterprise Developer Certificate. Подробные инструкции по повторному подписанию приложений Lookout for Work для iOS см. в статье [Lookout for Work iOS app re-signing process](https://personal.support.lookout.com/hc/en-us/articles/114094038714) ("Процесс повторного подписания приложения Lookout for Work для iOS") на сайте Lookout.


* **Шаг 3.** Включите проверку подлинности Azure Active Directory для пользователей iOS, выполнив указанные ниже действия.
  1.  Войдите на [портал управления Azure Active Directory](https://manage.windowsazure.com) и перейдите на страницу приложения.
  2.  Добавьте **приложение Lookout for Work для iOS** в качестве **собственного клиентского приложения**.
  ![снимок экрана: диалоговое окно добавления приложений с вариантом добавления собственного клиентского приложения](media/aad-add-app.png)

  3. Замените **com.lookout.enterprise.yourcompanyname** на идентификатор пакета клиента, выбранный при подписании IPA.
  4.  Добавьте дополнительный код URI перенаправления: **&lt;корпоративный_портал://код/>**, после которого укажите версию исходного кода URI перенаправления в кодировке URL.
  5.  Добавьте **делегированные разрешения** к приложению.

  Подробные сведения см. в разделе [Настройка собственного клиентского приложения](https://azure.microsoft.com/en-us/documentation/articles/app-service-mobile-how-to-configure-active-directory-authentication/#optional-configure-a-native-client-application).


* **Шаг 4.** Отправьте повторно подписанный IPA-файл, как описано в разделе [Создание приложений iOS в System Center Configuration Manager](https://docs.microsoft.com/en-us/sccm/apps/get-started/creating-ios-applications). В качестве минимальной версии ОС укажите iOS 8.0 или более позднюю.


* **Шаг 5.** Создайте политику конфигурации мобильных приложений, как описано в разделе [Настройка приложений iOS с помощью политик конфигурации мобильных приложений в System Center Configuration Manager](https://docs.microsoft.com/en-us/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies).


* **Шаг 6.** **Чтобы развернуть приложение для пользователей**, выберите приложение Lookout for Work на странице **Приложения**, а затем на вкладке **Главная** в группе **Развертывание** нажмите кнопку **Развернуть**.

  Необходимо выбрать тех же пользователей, которые были добавлены в параметр "Управление регистрацией" в консоли Lookout.  
Выберите параметр **Обязательная установка**, чтобы установка приложения Lookout требовалась на устройстве пользователя.

## <a name="what-happens-when-the-deployed-app-is-opened-on-the-device"></a>Что происходит, когда развернутое приложение открывается на устройстве




Когда пользователь открывает Lookout for Work на устройстве, ему предлагается активировать приложение и выполнить вход с помощью Azure Active Directory. Подробное пошаговое руководство с описанием процесса для конечных пользователей можно найти в следующих разделах:

* [Вам предложено установить Lookout for Work на устройстве Android](http://docs.microsoft.com/intune/enduser/you-are-prompted-to-install-lookout-for-work-android)

* [Вам необходимо устранить угрозу, которую приложение Lookout for Work обнаружило на устройстве Android](http://docs.microsoft.com/intune/enduser/you-need-to-resolve-a-threat-found-by-lookout-for-work-android)

## <a name="next-steps"></a>Дальнейшие действия
* [Включение правила защиты устройств от угроз в политике соответствия требованиям](enable-device-threat-protection-rule-compliance-policy.md)
