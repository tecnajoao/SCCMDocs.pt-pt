---
title: "Условный доступ | Документы Майкрософт"
description: "Узнайте, как использовать условный доступ в System Center Configuration Manager для защиты электронной почты и других служб."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b04727b-d563-422f-8d59-4dd66215d0b3
caps.latest.revision: "26"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: d6933a331bb229f7e378e8f0bfa511f6b0553ae9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="manage-access-to-services-in-system-center-configuration-manager"></a>Управление доступом к службам в System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*


## <a name="conditional-access-in-system-center-configuration-manager"></a>Условный доступ в System Center Configuration Manager
Используйте **условный доступ** для защиты электронной почты и других служб на устройствах, зарегистрированных в Microsoft Intune, в зависимости от указанных вами условий.  

 Сведения об **условном доступе на компьютерах, управляемых System Center Configuration Manager** и проверенных на соответствие, см. в разделе [Управление доступом к службам Office 365 для компьютеров под управлением System Center Configuration Manager](../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md).  


 Типовой алгоритм настройки условного доступа может выглядеть следующим образом.  

 ![ConditionalAccess4](media/ConditionalAccess4.png)  

 Использование условного доступа для управления доступом к следующим службам:  

-   Microsoft Exchange (локально)  

-   Microsoft Exchange Online  

-   Выделенная среда Exchange Online  

-   SharePoint Online  

-   Skype для бизнеса Online

-   Dynamics CRM Online

 Для реализации условного доступа в Configuration Manager настраиваются два типа политики.  

-   **Политики соответствия требованиям** — это необязательные политики, которые можно развернуть для коллекций пользователей и использовать для оценки таких параметров, как:  

    -   Секретный код  

    -   Шифрование  

    -   Выполнено ли на устройстве рутирование или джейлбрейк  

    -   Осуществляется ли управление электронной почтой на устройстве с помощью Configuration Manager или политики Intune  

     **Если на устройстве не развернута политика соответствия требованиям, все применимые политики условного доступа будут расценивать устройство как совместимое**.  

-   **Политики условного доступа** настраиваются для конкретной службы и определяют правила, указывающие, например, целевые группы безопасности Azure Active Directory или коллекции пользователей Configuration Manager, которые будут целевыми или будут исключены.  

     Политика условного доступа к локальной службе Exchange настраивается в консоли Configuration Manager. Однако при настройке политики Exchange Online или SharePoint Online открывается консоль администрирования Configuration Manager, в которой выполняется настройка политики.  

     В отличие от других политик Intune или Configuration Manager, развертывание политик условного доступа не выполняется. Они настраиваются один раз и применяются ко всем целевым пользователям.  

 Если устройство не удовлетворяет настроенным вами условиям, запускается процесс регистрации устройства и исправления проблемы, из-за которой устройство не является соответствующим.  

**Перед** началом использования условного доступа убедитесь, что выполнены нужные **требования**:  

## <a name="requirements-for-exchange-online-using-the-shared-multi-tenant-environment"></a>Требования к Exchange Online (с использованием общей мультитенантной среды)
Условный доступ к Exchange Online поддерживает устройства под управлением:
-   Windows 8.1 и более поздней версии (при регистрации в Intune)
-   Windows 7.0 или Windows 8.1 (при присоединении к домену)
-   Windows Phone 8.1 и более поздней версии
-   iOS 7.1 и более поздние версии
-   Android 4.0 и более поздние версии, Samsung KNOX Standard 4.0 и более поздние версии

 **Дополнительно**:
-   Устройства должны быть присоединенных к рабочей области, в рамках этой процедуры устройство регистрируется в службе регистрации устройств Azure Active Directory (AAD DRS).<br />     
- Компьютеры, присоединенные к домену, должны быть автоматически зарегистрированы в Azure Active Directory с помощью групповой политики или MSI.

  В разделе **Условный доступ для ПК** этой статьи описываются все требования для включения условного доступа для ПК.<br />     
  Служба AAD DRS активируется автоматически для клиентов Intune и Office 365. Клиенты, которые уже развернули службу регистрации устройств ADFS, не будут видеть зарегистрированные устройства в своем локальном Active Directory.
-   Необходимо использовать подписку Office 365, включающую в себя Exchange Online (например, E3), а пользователи должны иметь лицензию на Exchange Online.
-   **Коннектор Exchange Server** является необязательным. Он подключает Configuration Manager к Microsoft Exchange Online и помогает отслеживать сведения об устройстве через консоль Configuration Manager (см. раздел [Управление мобильными устройствами с помощью System Center Configuration Manager и Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)).
Соединитель не требуется для использования политик соответствия требованиям или политик условного доступа, но необходим для выполнения отчетов, которые помогут оценить влияние условного доступа.

## <a name="requirements-for-exchange-online-dedicated"></a>Требования к выделенной среде Exchange Online
Условный доступ к выделенной среде Exchange Online поддерживает устройства под управлением:
-   Windows 8 и более поздней версии (при регистрации в Intune)
-   Windows 7.0 или Windows 8.1 (при присоединении к домену)

  Условный доступ к компьютерам, присоединенным к домену, только для клиентов в новой выделенной среде Exchange Online.
-   Windows Phone 8 и более поздней версии
-   Любое устройство iOS, использующее почтовый клиент Exchange ActiveSync (EAS).
-   Android 4 и более поздней версии.
-   Для клиентов в **выделенной среде Exchange Online прежних версий**    

  Необходимо использовать **коннектор Exchange Server**, который подключает Configuration Manager к локальной среде Microsoft Exchange. Это позволяет управлять мобильными устройствами и обеспечивает условный доступ (см. раздел [Управление мобильными устройствами с помощью System Center Configuration Manager и Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)).
-   Для клиентов в **новой выделенной среде Exchange Online**     
  Необязательный **коннектор Exchange Server** подключает Configuration Manager к Microsoft Exchange Online и помогает отслеживать сведения об устройстве (см. раздел [Управление мобильными устройствами с помощью System Center Configuration Manager и Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)). Соединитель не требуется для использования политик соответствия требованиям или политик условного доступа, но необходим для выполнения отчетов, которые помогут оценить влияние условного доступа.  

## <a name="requirements-for-exchange-on-premises"></a>Требования к локальной версии Exchange
Условный доступ к локальной системе Exchange поддерживается для следующих устройств.
-   Windows 8 и более поздней версии (при регистрации в Intune)
-   Windows Phone 8 и более поздней версии.
-   Собственное почтовое приложение в iOS
-   Собственное почтовое приложение в Android 4 или более поздней версии
-   Приложение Microsoft Outlook не поддерживается (в Android и iOS).

**Дополнительно**:

-  Следует использовать Exchange 2010 или более поздней версии. Массив сервера клиентского доступа (CAS) сервера Exchange Server поддерживается.

> [!TIP]
> Если ваша среда Exchange находится в конфигурации серверов клиентского доступа, необходимо настроить локальный соединитель Exchange таким образом, чтобы он указывал на один из серверов клиентского доступа.
- Необходимо использовать **коннектор Exchange Server**, который подключает Configuration Manager к локальной среде Microsoft Exchange. Это позволяет управлять мобильными устройствами и обеспечивает условный доступ (см. раздел [Управление мобильными устройствами с помощью System Center Configuration Manager и Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)).
  - Убедитесь, что используется последняя версия **локального соединителя Exchange**. Локальный соединитель Exchange следует настроить в консоли Configuration Manager. Подробное пошаговое руководство см. в разделе [Управление мобильными устройствами с помощью System Center Configuration Manager и Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).
  - Соединитель должен быть настроен только на основном сайте System Center Configuration Manager.</li><li>Этот соединитель поддерживает среду серверов клиентского доступа Exchange. <br />        Соединитель необходимо настроить так, чтобы он обменивался данными с одним из серверов клиентского доступа Exchange.

- Exchange ActiveSync можно настроить с помощью проверки подлинности на основе сертификатов или входа по учетным данным пользователя.


## <a name="requirements-for-skype-for-business-online"></a>Требования к Skype для бизнеса Online
Условный доступ к SharePoint Online поддерживает устройства под управлением:
 -   iOS 7.1 и более поздние версии
 -   Android 4.0 и более поздней версии
 -   Samsung KNOX Standard 4.0 или более поздней версии

**Кроме того**, необходимо включить современную проверку подлинности для Skype для бизнеса Online. Заполните эту [форму Connect](https://connect.microsoft.com/office/Survey/NominationSurvey.aspx?SurveyID=17299&ProgramID=8715) , чтобы зарегистрироваться в программе современной проверки подлинности.

Все пользователи должны использовать Skype для бизнеса Online. Если имеется развертывание со Skype для бизнеса Online и локальным экземпляром Skype для бизнеса, политика условного доступа не будет применяться к пользователям, находящимся в локальном развертывании.

## <a name="requirements-for-sharepoint-online"></a>Требования к SharePoint Online
Условный доступ к SharePoint Online поддерживает устройства под управлением:
 -   Windows 8.1 и более поздней версии (при регистрации в Intune)
 -   Windows 7.0 или Windows 8.1 (при присоединении к домену)
 -   Windows Phone 8.1 и более поздней версии
 -   iOS 7.1 и более поздние версии
 -   Android 4.0 и более поздние версии, Samsung KNOX Standard 4.0 и более поздние версии

 **Дополнительно**:
 -   Устройства должны быть присоединенных к рабочей области, в рамках этой процедуры устройство регистрируется в службе регистрации устройств Azure Active Directory (AAD DRS).

 Компьютеры, присоединенные к домену, должны быть автоматически зарегистрированы в Azure Active Directory с помощью групповой политики или MSI. В разделе **Условный доступ для ПК** этой статьи описываются все требования для включения условного доступа для ПК.

 Служба AAD DRS активируется автоматически для клиентов Intune и Office 365. Клиенты, которые уже развернули службу регистрации устройств ADFS, не будут видеть зарегистрированные устройства в своем локальном Active Directory.
 -   Требуется подписка SharePoint Online, а пользователи должны иметь лицензию на SharePoint Online.

 ### <a name="conditional-access-for-pcs"></a>Условный доступ для ПК

 Условный доступ к **Exchange Online** и **SharePoint Online** можно настроить для компьютеров с настольными приложениями Office, которые отвечают следующим требованиям.
 -   Компьютер должен работать под управлением Windows 7.0 или Windows 8.1.
 -   Компьютер должен быть присоединен к домену или соответствовать требованиям.

 Для соответствия требованиям компьютер должен быть зарегистрирован в Intune и соответствовать политикам.

 Для ПК, присоединенных к домену, необходимо задать [автоматическую регистрацию устройства](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/) в Azure Active Directory.
 -   [Должна быть включена современная проверка подлинности Office 365](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/), а также должны быть установлены все последние обновления Office.<br />     Современная проверка подлинности для клиентов Office 2013 под управлением Windows использует библиотеку проверки подлинности Active Directory (ADAL) и обеспечивает более высокий уровень безопасности, сравнимый с **многофакторной проверкой подлинности**и **проверкой подлинности на основе сертификатов**.
 -   Настройте правила утверждений ADFS для блокирования несовременных протоколов проверки подлинности.  

## <a name="next-steps"></a>Дальнейшие шаги  
 Ознакомьтесь со следующими разделами, чтобы узнать о настройке политик соответствия требованиям и политик условного доступа для нужного сценария:  

-   [Управление политиками соответствия устройств в System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md)  

-   [Управление доступом к электронной почте в System Center Configuration Manager](../../protect/deploy-use/manage-email-access.md)  

-   [Управление доступом к SharePoint Online в System Center Configuration Manager](../../protect/deploy-use/manage-sharepoint-online-access.md)  

-   [Управление доступом к Skype для бизнеса Online](../../protect/deploy-use/manage-skype-for-business-online-access.md)  

### <a name="see-also"></a>См. также  

 [Приступая к работе с параметрами соответствия в System Center Configuration Manager](../../compliance/get-started/get-started-with-compliance-settings.md)
