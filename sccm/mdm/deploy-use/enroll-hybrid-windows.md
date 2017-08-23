---
title: "Настройка гибридного управления устройствами Windows с помощью System Center Configuration Manager и Microsoft Intune | Документы Майкрософт"
description: "Настройте управление устройствами Windows с помощью System Center Configuration Manager и Microsoft Intune."
ms.custom: na
ms.date: 03/17/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: dc1f70f5-64ab-42ab-aa91-d3858803e12f
caps.latest.revision: "9"
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 47348baeac26bfa2ad5016622fe4dbcb9f572483
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="set-up-windows-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Настройка гибридного управления устройствами Windows с помощью System Center Configuration Manager и Microsoft Intune

*Применимо к: System Center Configuration Manager (Current Branch)*

В этом разделе ИТ-администраторы узнают, как позволить пользователям управлять компьютерами c Windows и мобильными устройствами с помощью Configuration Manager и Windows Intune.

## <a name="enable-windows-device-management"></a>Включение управления устройствами с Windows
Чтобы включить управление устройствами с Windows для компьютеров и мобильных устройств, сделайте следующее:

1.  Перед настройкой регистрации для любой платформы выполните предварительные требования и процедуры в статье [Настройка гибридного управления мобильными устройствами (MDM) с помощью System Center Configuration Manager и Microsoft Intune](setup-hybrid-mdm.md).  
2.  В консоли Configuration Manager в рабочей области **Администрирование** перейдите к разделу **Обзор** > **Облачные службы** > **Подписки Microsoft Intune**.  
3.  На ленте щелкните **Настройка платформ** и выберите платформу Windows.
    - Для платформы **Windows** для компьютеров и ноутбуков с Windows сделайте следующее:
      1. На вкладке **Общие** щелкните **Включить регистрацию в ОС Windows**.
      2. Если вы используете сертификат для подписывания кода и развертывания приложения корпоративного портала, перейдите к пункту меню **Code-signing certificate** (Сертификат подписывания кода). Кроме того, пользователи устройств могут установить приложение корпоративного портала из Магазина Windows или же развернуть приложение из Магазина Windows для бизнеса без подписывания кода.
      3. Вы можете также настроить [параметры Windows Hello для бизнеса](windows-hello-for-business-settings.md).
    - Для платформы **Windows Phone** для телефонов и планшетов с Windows сделайте следующее:
      1. На вкладке **Общие** установите флажок **Windows Phone 8.1 и Windows 10 Mobile**. Windows Phone 8.0 больше не поддерживается.
      2. Если организации требуется загрузить неопубликованные корпоративные приложения, можно передать необходимый токен или файл. Дополнительные сведения о загрузке неопубликованных приложений см. в статье [Создание приложений для Windows](https://docs.microsoft.com/sccm/apps/get-started/creating-windows-applications).
        - **Токен регистрации приложений**
        - **PFX-файл**
        - **Нет.** При использовании сертификата Symantec можно указать, что нужно **отображать оповещение перед истечением срока действия сертификатов Symantec**.
4. Нажмите кнопку **ОК** , чтобы закрыть диалоговое окно.  Чтобы упростить процесс регистрации с помощью корпоративного портала, необходимо создать DNS-псевдоним для регистрации устройств. Затем необходимо проинструктировать пользователей о том, как регистрировать свои устройства.

## <a name="choose-how-to-enroll-windows-devices"></a>Выбор способа регистрации на устройствах с Windows

После назначения лицензий Intune для пользователей устройства Windows можно будет зарегистрировать без дополнительных действий, но вы можете также упростить регистрацию для пользователей.

Ниже приведены два фактора, которые определяют способ упрощения регистрации устройств Windows.
- **Вы используете Azure Active Directory Premium?** <br>[Azure AD Premium](https://docs.microsoft.com/azure/active-directory/active-directory-get-started-premium) входит в состав Enterprise Mobility + Security и других планов лицензирования.
- **Какие версии клиентов Windows будут регистрироваться?** <br>Устройства с Windows 10 можно зарегистрировать автоматически, добавив рабочую или учебную учетную запись. Более ранние версии необходимо регистрировать с помощью приложения корпоративного портала.

||**Azure AD Premium**|**AD других версий**|
|----------|---------------|---------------|  
|**Windows 10**|[Автоматическая регистрация](#enable-windows-10-automatic-enrollment) |[Регистрация пользователей](#enable-windows-enrollment-without-azure-ad-premium)|
|**Более ранние версии Windows**|[Регистрация пользователей](#enable-windows-enrollment-without-azure-ad-premium)|[Регистрация пользователей](#enable-windows-enrollment-without-azure-ad-premium)|

## <a name="enable-windows-10-automatic-enrollment"></a>Включение автоматической регистрации Windows 10

Автоматическая регистрация позволяет пользователям регистрировать корпоративные или личные компьютеры Windows 10 и устройства Windows 10 Mobile в Intune, добавляя рабочую или учебную учетную запись и соглашаясь на управление. Просто и удобно. Устройство пользователя регистрируется и присоединяется к Azure Active Directory в фоновом режиме. После регистрации управление устройством выполняется с помощью Intune.

**Предварительные требования**
- Подписка Azure Active Directory Premium ([пробная подписка](http://go.microsoft.com/fwlink/?LinkID=816845))
- Подписка на Microsoft Intune


### <a name="configure-automatic-mdm-enrollment"></a>Настройка автоматической регистрации для управления мобильными устройствами

1. Войдите на [портал управления Azure](https://portal.azure.com) (https://manage.windowsazure.com) и выберите **Active Directory**.

  ![Снимок экрана портала Azure](../media/auto-enroll-azure-main.png)

2. Выберите **Мобильность (MDM и MAM)**.

  ![Снимок экрана портала Azure](../media/auto-enroll-mdm.png)

3. Выберите **Microsoft Intune**.

  ![Снимок экрана портала Azure](../media/auto-enroll-intune.png)

4. Настройте **область пользователя MDM**. Укажите, каким устройствами пользователей следует управлять с помощью Microsoft Intune. Устройства Windows 10 этих пользователей будут автоматически регистрироваться для управления в Microsoft Intune.

    - **Нет**
    - **Некоторые**
    - **Все**

   ![Снимок экрана портала Azure](../media/auto-enroll-scope.png)

5. Используйте значения по умолчанию для следующих URL-адресов:
    - **URL-адрес условий использования MDM**;
    - **URL-адрес обнаружения MDM**;
    - **URL-адрес соответствия MDM**.

6. Нажмите кнопку **Сохранить**.


По умолчанию двухфакторная проверка подлинности для службы отключена. Тем не менее мы рекомендуем использовать ее при регистрации устройства. Прежде чем запрашивать двухфакторную проверку подлинности для этой службы, необходимо настроить ее поставщика в Azure Active Directory и настроить учетные записи пользователей для использования Многофакторной идентификации. Ознакомьтесь со статьей [Приступая к работе с Многофакторной аутентификацией Azure в облаке](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-cloud).

## <a name="enable-windows-enrollment-without-azure-ad-premium"></a>Разрешение регистрации Windows без Azure AD Premium
Можно разрешить пользователям регистрировать свои устройства без автоматической регистрации в Azure AD Premium. После назначения лицензий пользователи могут регистрироваться после добавления их рабочей учетной записи на личные устройства или после присоединения их корпоративных устройств к Azure AD. Создание DNS-псевдонима (типа записи CNAME) упрощает регистрацию устройств пользователями. Если вы создаете записи ресурсов CNAME DNS, пользователи подключаются к Intune и выполняют регистрацию без необходимости ввода имени сервера Intune.

### <a name="create-cnames-to-simplify-enrollment"></a>Создание записей CNAME для упрощения регистрации
Создайте запись ресурсов CNAME DNS для домена вашей организации. Например, если компания имеет веб-сайт contoso.com, необходимо создать запись CNAME в DNS, перенаправляющую EnterpriseEnrollment.contoso.com на enterpriseenrollment-s.manage.microsoft.com.

Несмотря на то, что создавать записи CNAME в DNS не обязательно, записи CNAME позволяют упростить регистрацию для пользователей. Если запись CNAME для регистрации не обнаружена, пользователям предлагается вручную ввести имя сервера MDM — enrollment.manage.microsoft.com.

|Тип|Имя узла|Указывает на|СРОК ЖИЗНИ|  
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.company_domain.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 час|

При наличии нескольких UPN-суффиксов необходимо создать по одной записи CNAME для каждого имени домена и указать для них EnterpriseEnrollment-s.manage.microsoft.com. Например, если в качестве электронной почты или UPN пользователи используют name@contoso.com, а также name@us.contoso.com и name@eu.constoso.com, администратору Contoso DNS необходимо создать следующие записи CNAME.

|Тип|Имя узла|Указывает на|СРОК ЖИЗНИ|  
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 час|
|CNAME|EnterpriseEnrollment.us.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 час|
|CNAME|EnterpriseEnrollment.eu.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 час|

`EnterpriseEnrollment-s.manage.microsoft.com` — поддерживает перенаправление в службу Intune с распознаванием домена по имени домена электронной почты.

Распространение изменений записей DNS может занимать до 72 часов. Вы не можете проверить смену DNS в Intune, пока запись DNS не будет распространена.

## <a name="tell-users-how-to-enroll-devices"></a>Предоставление пользователям указаний по регистрации их устройств  

 После выполнения настроек необходимо проинформировать пользователей о том, как регистрировать свои устройства. Рекомендации см. в статье [What to tell users about enrolling their devices](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune) (Что сообщать пользователям о регистрации устройств). Вы можете направить пользователей ознакомиться со статьей [Регистрация устройства Windows в Intune](https://docs.microsoft.com/intune/enduser/enroll-your-device-in-intune-windows). Эти сведения относятся к мобильным устройствам под управлением Microsoft Intune и Configuration Manager.

> [!div class="button"]
[< Назад](create-service-connection-point.md) [Вперед >](set-up-additional-management.md)
