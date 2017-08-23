---
title: "Настройка инвентаризации оборудования | Документы Майкрософт | Мобильные устройства"
description: "Настройте инвентаризацию оборудования для мобильных устройств, зарегистрированных в Microsoft Intune и System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 78a0aecc-f775-451e-aa05-56377ec91b1f
caps.latest.revision: "7"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 7ab9042a525e07b8e3107479cedeec6b99f7bc86
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-configure-hardware-inventory-for-mobile-devices-enrolled-by-microsoft-intune-and-system-center-configuration-manager"></a>Настройка инвентаризации оборудования для мобильных устройств, зарегистрированных в Microsoft Intune и System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

В Configuration Manager вы можете собирать данные инвентаризации оборудования для устройств iOS, Android и Windows с помощью соединителя Microsoft Intune. Сведения о настройке инвентаризации оборудования см. в разделе [Расширение инвентаризации оборудования в System Center Configuration Manager](../../core/clients/manage/inventory/extend-hardware-inventory.md).  

 Сведения о том, как зарегистрировать устройства в Microsoft Intune, см. в разделе [Управление мобильными устройствами с помощью Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx).  

## <a name="hardware-inventory-for-mobile-devices"></a>Инвентаризация оборудования для мобильных устройств  
 В приведенных ниже таблицах перечислены классы инвентаризации, доступные при инвентаризации оборудования для распространенных мобильных платформ.  

 **iOS**  

|Класс инвентаризации оборудования|iOS|  
|------------------------------|---------|  
|Имя|Device_ComputerSystem.DeviceName|  
|Уникальный идентификатор устройства|Device_ComputerSystem.UDID|  
|Серийный номер|Device_ComputerSystem.SerialNumber|  
|Адрес электронной почты|Device_Email.OwnerEmailAddress|  
|Тип операционной системы|Неприменимо|  
|Версия операционной системы|Device_OSInformation.OSVersion|  
|Версия сборки|Неприменимо|  
|Основная версия пакета обновления|Неприменимо|  
|Дополнительный номер версии пакета обновления|Неприменимо|  
|Язык операционной системы|Неприменимо|  
|Общая вместимость хранилища|Device_Memory.DeviceCapacity|  
|Свободное место для хранения данных|Device_Memory.AvailableDeviceCapacity|  
|IMEI|Device_ComputerSystem.IMEI|  
|MEID|Device_ComputerSystem.MEID|  
|Изготовитель|Неприменимо|  
|Модель|Модель|  
|Номер телефона<sup>1</sup>|Device_ComputerSystem.PhoneNumber|  
|Абонентская система связи|Device_ComputerSystem.SubscriberCarrierNetwork|  
|Сотовая технология|Device_ComputerSystem.CellularTechnology|  
|Wi-Fi MAC|Device_WLAN.WiFiMAC|  

 **Android**  

> [!NOTE]  
>  **ПРИМЕЧАНИЕ**. Классы инвентаризации Android доступны при использовании приложения корпоративного портала для Android.  

|Класс инвентаризации оборудования|Android|  
|------------------------------|-------------|  
|Имя|Неприменимо|  
|Уникальный идентификатор устройства|Неприменимо|  
|Серийный номер|Device_ComputerSystem.SerialNumber|  
|Адрес электронной почты|Неприменимо|  
|Тип операционной системы|Device_OSInformation.Platform|  
|Версия операционной системы|Device_OSInformation.Version|  
|Версия сборки|Неприменимо|  
|Основная версия пакета обновления|Неприменимо|  
|Дополнительный номер версии пакета обновления|Неприменимо|  
|Язык операционной системы|Неприменимо|  
|Общая вместимость хранилища|Device_Memory.StorageTotal|  
|Свободное место для хранения данных|Device_Memory.StorageFree|  
|IMEI|Device_ComputerSystem.IMEI|  
|MEID|Неприменимо|  
|Изготовитель|Device_Info.Manufacturer|  
|Модель|Device_Info.Model|  
|Номер телефона<sup>1</sup>|Device_ComputerSystem.PhoneNumber|  
|Абонентская система связи|Device_ComputerSystem.SubscriberCarrierNetwork|  
|Сотовая технология|Device_ComputerSystem.CellularTechnology|  
|Wi-Fi MAC|Device_WLAN.WiFiMAC|  

 **Windows Phone 8 и 8.1**  

|Класс инвентаризации оборудования|Windows Phone 8 и Windows Phone 8.1|  
|------------------------------|-------------------------------------------|  
|Имя|Device_ComputerSystem.DeviceName|  
|Уникальный идентификатор устройства|Device_ComputerSystem.DeviceClientID|  
|Серийный номер|Неприменимо|  
|Адрес электронной почты|Device_Email.OwnerEmailAddress|  
|Тип операционной системы|Device_OSInformation.Platform|  
|Версия операционной системы|Device_ComputerSystem.SoftwareVersion|  
|Версия сборки|Неприменимо|  
|Основная версия пакета обновления|Неприменимо|  
|Дополнительный номер версии пакета обновления|Неприменимо|  
|Язык операционной системы|Device_OSInformation.Language|  
|Общая вместимость хранилища|Неприменимо|  
|Свободное место для хранения данных|Неприменимо|  
|IMEI|Неприменимо|  
|MEID|Неприменимо|  
|Изготовитель|Device_ComputerSystem.DeviceManufacturer|  
|Модель|Device_ComputerSystem.DeviceModel|  
|Номер телефона<sup>1</sup>|Неприменимо|  
|Абонентская система связи|Неприменимо|  
|Сотовая технология|Неприменимо|  
|Wi-Fi MAC|Неприменимо|  

 **Windows RT**  

|Класс инвентаризации оборудования|Windows RT|  
|------------------------------|----------------|  
|Имя|Device_ComputerSystem.DeviceName|  
|Уникальный идентификатор устройства|Device_ComputerSystem.DeviceName|  
|Серийный номер|Неприменимо|  
|Адрес электронной почты|Device_Email.OwnerEmailAddress|  
|Тип операционной системы|CCM_OperatingSystem.SystemType|  
|Версия операционной системы|Win32_OperatingSystem.Version|  
|Версия сборки|Win32_OperatingSystem.BuildNumber|  
|Основная версия пакета обновления|Win32_OperatingSystem.ServicePackMajorVersion|  
|Дополнительный номер версии пакета обновления|Win32_OperatingSystem.ServicePackMinorVersion|  
|Язык операционной системы|Неприменимо|  
|Общая вместимость хранилища|Win32_PhysicalMemory.Capacity|  
|Свободное место для хранения данных|Win32_OperatingSystem.FreePhysicalMemory|  
|IMEI|Неприменимо|  
|MEID|Неприменимо|  
|Изготовитель|Win32_ComputerSystem.Manufacturer|  
|Модель|Win32_ComputerSystem.Model|  
|Номер телефона<sup>1</sup>|Неприменимо|  
|Абонентская система связи|Неприменимо|  
|Сотовая технология|Неприменимо|  
|Wi-Fi MAC|Win32_NetworkAdapter.MACAddress|  

 <sup>1</sup> Номер телефона скрыт символами *, за исключением 4 последних цифр.  

 Чтобы функция инвентаризации выполнила сбор номера телефона, необходимо, чтобы в устройство была вставлена SIM-карта и оператор подготовил для нее соответствующий номер телефона.  
