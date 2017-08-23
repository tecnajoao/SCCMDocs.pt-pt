---
title: "Создание профилей VPN в System Center Configuration Manager | Документы Майкрософт"
description: "Узнайте, как создавать профили VPN в System Center Configuration Manager."
ms.custom: 
ms.date: 4/19/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f338e4db-73b5-45ff-92f4-1b89a8ded989
caps.latest.revision: "15"
author: lleonard-msft
caps.handback.revision: "0"
ms.author: alleonar
ms.manager: angrobe
ms.openlocfilehash: 359fcfd9754fb5c81763bc44cac45376ea3ab0b8
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-create-vpn-profiles-in-system-center-configuration-manager"></a>Создание профилей VPN в System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

Сведения о типах соединений, доступных для различных платформ устройств, см. в разделе [Профили VPN в System Center Configuration Manager](../../protect/deploy-use/vpn-profiles.md).  

Для сторонних подключений VPN распространите приложение VPN перед развертыванием профиля VPN. Если не развернуть приложение, пользователям будет предложено сделать это при попытке подключиться к VPN. Сведения о развертывании приложений см. в разделе [Развертывание приложений с помощью System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md).

### <a name="create-a-vpn-profile"></a>Создание профиля VPN   

1.  В консоли Configuration Manager последовательно выберите **Активы и соответствие** > **Параметры соответствия** > **Доступ к ресурсам компании** > **Профили VPN**.  

3.  На вкладке **Главная** в группе **Создать** щелкните **Создать профиль VPN**.  


1.  Укажите сведения на странице **Общие**. и обратите внимание на следующее:  

    - Не используйте в имени профиля VPN символы \\/:*?&lt;>&#124; или пробел. Они не поддерживаются профилем VPN Windows Server.  

     -   Выберите **Импорт элемента существующего профиля VPN из файла**, чтобы импортировать сведения о профиле VPN, которые ранее были экспортированы в XML-файл (только для операционных систем Windows 8.1 и Windows RT).  

1.  На странице **Подключение** укажите приведенные ниже сведения.  

    -   **Тип подключения**. Выберите тип подключения VPN. Можно выбрать один из типов подключения, приведенных в таблице ниже.  

    -   **Список серверов**. Добавьте новый сервер для VPN-подключения. В зависимости от типа подключения можно добавить один или несколько VPN-серверов, а также выбрать сервер по умолчанию.  

        > [!NOTE]  
        >  Устройства, работающие под управлением iOS, не поддерживают использование нескольких VPN-серверов. Если настроить несколько VPN-серверов, а затем развернуть профиль VPN на устройстве iOS, будет использоваться только сервер по умолчанию.  

     В этой таблице перечислены параметры для типов подключений. Дополнительные сведения см. в вашей документации сервера VPN.

| &nbsp;&nbsp;Параметр&nbsp;&nbsp; | Дополнительные сведения | &nbsp;&nbsp;Подключение&nbsp;типа&nbsp;&nbsp; |  
|----------------|----------------------|---------------------|  
|**Область**     |Область проверки подлинности, которую следует использовать. Область проверки подлинности — это группа ресурсов проверки подлинности, используется для типа подключения Pulse Secure.|Pulse Secure|    
|**Роль**        |Роль пользователя, имеющая доступ к этому подключению. |Pulse Secure|  
|**Группа или домен входа** |Имя группы входа или домена, к которому следует подключиться.|Dell SonicWALL Mobile Connect|  
|**Отпечаток**  |Строка, например "Код отпечатка Contoso", которая будет использоваться для проверки доверия VPN-сервера.<br /><br /> Отпечаток пальца можно:<br /><br /> Отправить клиенту, чтобы он доверял любому серверу, представившему этот же отпечаток при подключении.<br /><br /> Если на устройстве еще нет отпечатка, пользователь получит запрос на доверие к VPN-серверу, к которому осуществляется подключение, с отображением отпечатка (пользователь вручную проверит отпечаток и нажмет кнопку **Доверять** для подключения).|Check Point Mobile VPN|  
|**Отправлять весь сетевой трафик через VPN-подключение** |Если этот параметр не выбран, можно указать дополнительные маршруты для подключения (для типов подключения **Microsoft SSL (SSTP)**, **Microsoft Automatic**, **IKEv2**, **PPTP** и **L2TP** ), которое называется раздельным или VPN-туннелированием.<br /><br /> Только подключения к локальной сети отправляются через туннель VPN. VPN-туннелирование не используется при подключении к ресурсам в Интернете. |Все|  
|**DNS-суффикс этого подключения** |DNS-суффикс для подключения.|Microsoft SSL (SSTP)<br /><br /> Microsoft Automatic<br /><br /> IKEv2<br /><br /> PPTP<br /><br /> L2TP|  
|**Обход VPN при подключении к корпоративной сети Wi-Fi**  |VPN-подключение не будет использоваться, когда устройство подключено к сети Wi-Fi организации.|Cisco AnyConnect<br /><br /> Pulse Secure<br /><br /> F5 Edge Client<br /><br /> Dell SonicWALL Mobile Connect<br /><br /> Check Point Mobile VPN<br /><br /> Microsoft SSL (SSTP)<br /><br /> Microsoft Automatic<br /><br /> IKEv2<br /><br /> L2TP|  
|**Обход VPN при подключении к домашней сети Wi-Fi**  |VPN-подключение не будет использоваться, когда устройство подключено к домашней сети Wi-Fi.|Все|  
|**VPN на приложение (iOS 7 и более поздней версии, Mac OS X 10.9 и более поздней версии)** |Свяжите VPN-подключение с приложением iOS, чтобы устанавливать подключение при запуске приложения. Профиль VPN можно связать с приложением при развертывании последнего.|Cisco AnyConnect<br /><br /> Pulse Secure<br /><br /> F5 Edge Client<br /><br /> Dell SonicWALL Mobile Connect<br /><br /> Check Point Mobile VPN|  
|**Настраиваемые XML-данные (необязательно)** |Укажите пользовательские команды XML, настраивающие VPN-подключение.<br /><br /> Примеры:<br /><br /> Для **Pulse Secure**:<br /><br /> **&lt;pulse-schema><br /> &nbsp; &lt;isSingleSignOnCredential>true&lt;/isSingleSignOnCredential\><br />&lt;/pulse-schema>**<br /><br /> Для **CheckPoint Mobile VPN**:<br /><br /> **&lt;CheckPointVPN <br /> &nbsp; port="443" name="CheckPointSelfhost" <br /> &nbsp; sso="true" <br /> &nbsp; debug="3"<br />/>**<br /><br /> Для **Dell SonicWALL Mobile Connect**:<br /><br /> **&lt;MobileConnect\><br />&nbsp; &nbsp; &lt;Compression\>false&lt;/Compression\><br />&nbsp; &nbsp; &lt;debugLogging\>True&lt;/debugLogging\><br />&nbsp; &nbsp; &lt;packetCapture\>False&lt;/packetCapture\><br />&lt;/MobileConnect\>**<br /><br /> Для **клиента F5 Edge**:<br /><br /> **&lt;f5-vpn-conf>&lt;single-sign-on-credential>&lt;/f5-vpn-conf>**<br /><br /> Дополнительные сведения о создании пользовательских команд XML см. в документации VPN каждого производителя.|Cisco AnyConnect<br /><br /> Pulse Secure<br /><br /> F5 Edge Client<br /><br /> Dell SonicWALL Mobile Connect<br /><br /> Check Point Mobile VPN|  

> [!NOTE]  
>  Сведения, относящиеся к созданию профилей VPN для мобильных устройств в System Center Configuration Manager, см. в [этой статье](../../mdm/deploy-use/create-vpn-profiles.md).  

Завершите работу мастера. Новый профиль VPN отобразится в узле **Профили VPN** рабочей области **Активы и соответствие** .

### <a name="next-steps"></a>Дальнейшие действия

- Для сторонних подключений VPN распространите приложение VPN перед развертыванием профиля VPN. Если не развернуть приложение, пользователям будет предложено сделать это при попытке подключиться к VPN. Сведения о развертывании приложений см. в разделе [Развертывание приложений с помощью System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md).

- Разверните профили VPN, как описано в разделе [Развертывание профилей VPN в System Center Configuration Manager](deploy-wifi-vpn-email-cert-profiles.md).  
