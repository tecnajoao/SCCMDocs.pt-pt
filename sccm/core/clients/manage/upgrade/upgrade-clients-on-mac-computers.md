---
title: "Обновление клиентов для macOS в Configuration Manager | Документы Майкрософт"
description: "Вы можете обновить клиенты на компьютерах Mac в System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 74c60941-5eae-4905-9e58-252bdb39df96
caps.latest.revision: "10"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 502116b66fc14914ca0606ae416e82202824de7a
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-upgrade-clients-on-mac-computers-in-system-center-configuration-manager"></a>Обновление клиентов на компьютерах Mac в System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

Ниже приведены общие инструкции по обновлению клиента для компьютеров Mac с помощью приложения System Center Configuration Manager. Помимо этого,  можно загрузить файл установки клиента Mac, скопировать его в общую сетевую или локальную папку на компьютере Mac, а затем поручить пользователям выполнить установку вручную.  

> [!NOTE]  
>  Прежде чем приступить к выполнению этих действий, убедитесь, что компьютер Mac соответствует необходимым условиям. См. раздел [Поддерживаемые операционные системы для серверов системы сайта](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers).  

## <a name="step-1-download-the-latest-mac-client-installation-file-from-the-microsoft-download-center"></a>Шаг 1. Скачивание файла для установки последней версии клиента Mac из Центра загрузки Майкрософт  
 Клиент Mac для Configuration Manager не поставляется на установочном носителе Configuration Manager, и его необходимо скачать из центра загрузки Майкрософт. Установочные файлы клиента Mac содержатся в файле установщика Windows с именем ConfigmgrMacClient.msi.  

 Его можно загрузить в [Центре загрузки Майкрософт](http://go.microsoft.com/fwlink/p/?LinkId=525184).  

## <a name="step-2-run-the-downloaded-installation-file-to-create-the-mac-client-installation-file"></a>Шаг 2. Запуск скачанного файла установки для создания файла установки клиента Mac  
 На компьютере, работающем под управлением ОС Windows, запустите загруженный ранее файл **ConfigmgrMacClient.msi** , чтобы распаковать файл установки клиента Mac с именем **Macclient.dmg**. По умолчанию после распаковки этот файл размещается в папке **C:\Program Files (x86)\Microsoft\System Center 2012 Configuration Manager Mac Client** на компьютере Windows.  

## <a name="step-3-extract-the-client-installation-files"></a>Шаг 3. Извлечение файлов установки клиента  
 Скопируйте файл Macclient.dmg в сетевую или локальную папку на компьютере Mac. Затем на компьютере Mac подключите и откройте файл Macclient.dmg, после чего скопируйте файлы в папку на этом компьютере.  

## <a name="step-4-create-a-cmmac-file-that-can-be-used-to-create-an-application"></a>Шаг 4. Создание CMMAC-файла, который можно использовать для создания приложения  

1.  Используйте средство **CMAppUtil** (находится в папке **Tools** установочных файлов клиента Mac), чтобы создать CMMAC-файл из пакета установки клиента. Этот файл будет использоваться для создания приложения Configuration Manager.  

2.  Скопируйте новый файл **CMClient.pkg.cmmac** в папку, которая доступна для компьютера с работающей консолью Configuration Manager.  

 Дополнительные сведения см. в разделе [Дополнительные процедуры для создания и развертывания приложений для компьютеров Mac](/sccm/apps/get-started/creating-mac-computer-applications#supplemental-procedures-to-create-and-deploy-applications-for-mac-computers).  

## <a name="step-5-create-and-deploy-an-application-containing-the-mac-client-files"></a>**Шаг 5**. Создание и развертывание приложения, содержащего файлы клиента Mac  

1.  В консоли Configuration Manager создайте приложение из файла **CMClient.pkg.cmmac**, который содержит файлы установки клиента  

2.  Разверните это приложение на компьютерах Mac в своей иерархии.  

 Дополнительные сведения см.в разделе [Создание приложений для компьютеров Mac с помощью System Center Configuration Manager](../../../../apps/get-started/creating-mac-computer-applications.md).  

## <a name="step-6-users-install-the-latest-client"></a>Шаг 6. Установка пользователями последней версии клиента  
 Пользователи клиентов Mac получат сообщение о том, что клиент Configuration Manager доступен и его необходимо установить. После установки клиента пользователям необходимо перезапустить свои компьютеры Mac.  

 После перезапуска компьютера автоматически запустится мастер регистрации компьютеров, чтобы запросить новый сертификат пользователя.  

 Если вы не используете регистрацию в Configuration Manager и устанавливаете сертификат клиента независимо от Configuration Manager, см. раздел [Настройка обновленного клиента для использования существующего сертификата](#BKMK_UpgradingClient_MachineEnrollment).  

##  <a name="BKMK_UpgradingClient_MachineEnrollment"></a> Configure the upgraded client to use an existing certificate  
 Запустите следующую процедуру для предотвращения запуска мастера регистрации компьютеров и настройки обновленного клиента на использование существующего сертификата клиента.  

-   В консоли Configuration Manager создайте элемент конфигурации с типом **Mac OS X**.  

-   Добавьте к этому элементу конфигурации параметр с типом **Сценарий**.  

-   Добавьте следующий сценарий настройки:  

    ```  
    #!/bin/sh  
    echo "Starting script\n"  
    echo "Changing directory to MAC Client\n"  
    cd /Users/Administrator/Desktop/'MAC Client'/  
    echo "Import root cert\n"  
    /usr/bin/sudo /usr/bin/security import /Users/Administrator/Desktop/'MAC Client'/Root.pfx -A -k /Library/Keychains/System.Keychain -P ROOT  
    echo "Using openssl to convert pfx to a crt\n"  
    /usr/bin/sudo openssl pkcs12 -in /Users/Administrator/Desktop/'MAC Client'/Root.pfx -out Root1.crt -nokeys -clcerts -passin pass:ROOT  
    echo "Adding trust to root cert\n"  
    /usr/bin/sudo /usr/bin/security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.Keychain Root1.crt  
    echo "Import client cert\n"  
    /usr/bin/sudo /usr/bin/security import /Users/Administrator/Desktop/'MAC Client'/MacClient.pfx -A -k /Library/Keychains/System.Keychain -P MAC  
    echo "Executing ccmclient with MP\n"  
    sudo ./ccmsetup -MP https://SCCM34387.SCCM34387DOM.NET/omadm/cimhandler.ashx  
    echo "Editing Plist file\n"  
    sudo /usr/libexec/Plistbuddy -c 'Add:SubjectName string CMMAC003L' /Library/'Application Support'/Microsoft/CCM/ccmclient.plist  
    echo "Changing directory to CCM\n"  
    cd /Library/'Application Support'/Microsoft/CCM/  
    echo "Making connection to the server\n"  
    sudo open ./CCMClient  
    echo "Ending Script\n"  
    exit  

    ```  

-   Добавьте элемент конфигурации в конфигурационную базу, а затем разверните ее на всех компьютерах Mac, на которых установлен сертификат, независимо от Configuration Manager.  

 Дополнительные сведения о создании и развертывании элементов конфигурации для компьютеров Mac см. в разделах [Создание элементов конфигурации для устройств Mac OS X, управляемых с помощью клиента System Center Configuration Manager](../../../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md) и [Развертывание конфигурационных баз в System Center Configuration Manager](../../../../compliance/deploy-use/deploy-configuration-baselines.md).  
