---
title: "Создание профилей сертификатов PFX с помощью импорта сведений о сертификате | Документация Майкрософт"
description: "Узнайте, как использовать PFX-файлы в System Center Configuration Manager для создания пользовательских сертификатов, которые поддерживают обмен зашифрованными данными."
ms.custom: na
ms.date: 04/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e3bb3e13-3037-4122-93bc-504bfd080a4d
caps.latest.revision: "5"
caps.handback.revision: "0"
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.openlocfilehash: c8346d04c7cd9761291824f5d30f09fab9acbcf9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-create-pfx-certificate-profiles-by-importing-certificate-details"></a>Как создать профили сертификатов PFX с помощью импорта сведений о сертификате

*Применимо к: System Center Configuration Manager (Current Branch)*


Вы узнаете, как создать профиль сертификата с помощью импорта учетных данных из внешних сертификатов.  

См. дополнительные сведения о создании и настройке [профилей сертификатов](../../protect/deploy-use/introduction-to-certificate-profiles.md). В этой статье представлены некоторые сведения о профилях сертификатов, связанные с сертификатами PFX.

-  Configuration Manager предлагает широкий набор хранилищ сертификатов, применимых с разными устройствами и операционными системами.  Сюда входит следующее.

 -   iOS и MacOS/OSX;
 -   Android и Android for Work;
 -   Windows 10, включая Windows 10 Mobile.

См. дополнительные сведения о [необходимых компонентах для профилей сертификатов](../../protect/plan-design/prerequisites-for-certificate-profiles.md).

## <a name="pfx-certificate-profiles"></a>Профили сертификатов PFX
System Center Configuration Manager позволяет импортировать учетные данные сертификата, а затем подготавливать файлы обмена личной информацией (PFX) для устройств пользователей. PFX-файлы можно использовать для создания пользовательских сертификатов с целью поддержки обмена зашифрованными данными.

> [!TIP]  
>  Пошаговое руководство, в котором описан этот процесс, доступно в разделе [Создание и развертывание профилей сертификатов PFX в Configuration Manager](http://blogs.technet.com/b/karanrustagi/archive/2015/09/01/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager.aspx).  

## <a name="create-import-and-deploy-a-personal-information-exchange-pfx-certificate-profile"></a>Создание, импорт и развертывание профиля сертификата обмена личной информацией (PFX)  

### <a name="get-started"></a>Начало работы

1.  В консоли System Center Configuration Manager щелкните элемент **Активы и соответствие**.  
2.  В рабочей области **Активы и соответствие** разверните узлы **Параметры соответствия**и **Доступ к ресурсам компании**, а затем выберите пункт **Профили сертификатов**.  

3.  На вкладке **Главная** в группе **Создать** щелкните пункт **Создать профиль сертификата**.

4.  На странице **Общие** мастера **Создание профилей сертификатов** введите перечисленные ниже сведения.  

    -   **Имя**: введите уникальное имя для профиля сертификата. Можно использовать не более 256 символов.  

    -   **Описание**: введите описание, которое позволяет получить представление о профиле сертификата и содержит другие важные сведения для его идентификации в консоли System Center Configuration Manager. Можно использовать не более 256 символов.  

    -   **Укажите тип профиля сертификата, который вы хотите создать**. Для сертификатов PFX выберите один из следующих вариантов:  

        -   **Файл обмена личной информацией — параметры PKCS 12 (PFX) — импорт**. Создание профиля сертификата с помощью программного импорта информации из существующих сертификатов.  

        -   **Файл обмена личной информацией — параметры PKCS 12 (PFX) — создание**. Создание профиля сертификата PFX с использованием учетных данных, предоставленных центром сертификации.  Дополнительные сведения см. в статье [Создание профилей сертификатов PFX с помощью центра сертификации](../../mdm/deploy-use/create-pfx-certificate-profiles.md).


### <a name="create-a-pfx-certificate-profile-for-the-imported-credentials"></a>Создание профиля сертификата PFX для импортированных учетных данных

Чтобы импортировать сертификат PFX, нужно развернуть скрипт создания PFX с помощью пакета SDK для Configuration Manager. 

Импортированные сертификаты впоследствии будут развертываться на зарегистрированных устройствах.

1. На странице **Сертификат PFX** **мастера создания профиля сертификата** укажите, где должен размещаться провайдер хранилища для ключей устройства.
    -   **Установить в доверенный платформенный модуль (TPM) при его наличии**  
    -   **Установить в доверенный платформенный модуль (TPM), в противном случае выдать отказ** 
    -   **Установить в Windows Hello для бизнеса, в ином случае— сбой** 
    -   **Установить в поставщик хранилища ключей программного обеспечения** 
2. Нажмите кнопку **Далее**. 
3. На странице **Поддерживаемые платформы** в мастере выберите платформы устройств, а затем щелкните **Далее**.

### <a name="finish-the-profile"></a>Завершение создания профиля

1.  Щелкните **Далее**, просмотрите страницу **Сводка** , а затем закройте мастер.  
2.  Профиль сертификата, содержащий PFX-файл, теперь доступен в рабочей области **Профили сертификатов** . 
3.  Чтобы развернуть этот профиль, в консоли **Активы и соответствие** откройте **Параметры соответствия** > **Доступ к ресурсам компании** > **Профили сертификатов**, затем щелкните правой кнопкой мыши нужный сертификат и выберите **Развернуть**. 

### <a name="deploy-a-create-pfx-script"></a>Развертывание скрипта создания PFX

Чтобы развернуть скрипт создания PFX, используйте [пакет SDK для Configuration Manager](http://go.microsoft.com/fwlink/?LinkId=613525). 

Сценарий создания PFX, добавленный в Configuration Manager 2012 с пакетом обновления 2 (SP2), добавляет класс SMS_ClientPfxCertificate в пакет SDK. Этот класс содержит следующие методы.  

    -   `ImportForUser`  

    -   `DeleteForUser`  

Следующий пример кода импортирует учетные данные в профиль сертификата PFX.

``` powershell
    $EncryptedPfxBlob = "<blob>"  
    $Password = "abc"  
    $ProfileName = "PFX_Profile_Name"  
    $UserName = "ComputerName\Administrator"  

    #New pfx  
    $WMIConnection = ([WMIClass]"\\nksccm\root\SMS\Site_MDM:SMS_ClientPfxCertificate")  
        $NewEntry = $WMIConnection.psbase.GetMethodParameters("ImportForUser")  
        $NewEntry.EncryptedPfxBlob = $EncryptedPfxBlob  
        $NewEntry.Password = $Password  
        $NewEntry.ProfileName = $ProfileName  
        $NewEntry.UserName = $UserName  
    $Resource = $WMIConnection.psbase.InvokeMethod("ImportForUser",$NewEntry,$null)  
```  

Чтобы использовать этот пример, измените в скрипте следующие переменные:  

   -   **blob**\ — зашифрованный с помощью base64 BLOB-объект PFX;  
   -   **$Password** — пароль для PFX-файла;  
   -   **$ProfileName** — имя профиля PFX;  
   -   **ComputerName** — имя главного компьютера.   

## <a name="see-also"></a>См. также
В разделе [Создание профиля сертификата](../../protect/deploy-use/create-certificate-profiles.md) рассматривается выполнение этой процедуры с помощью мастера создания профилей сертификатов.

[Как создать профили сертификатов PFX с помощью импорта сведений о сертификате](../../mdm/deploy-use/create-pfx-certificate-profiles.md)

В статье [Развертывание профилей в System Center Configuration Manager](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md) описано, как развертывать профили сертификатов.