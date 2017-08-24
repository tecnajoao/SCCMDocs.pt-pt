---
title: "Configurar o inventário de hardware | Microsoft Docs | dispositivos móveis"
description: "Configure o inventário de hardware para dispositivos móveis inscritos pelo Microsoft Intune e o System Center Configuration Manager."
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
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-configure-hardware-inventory-for-mobile-devices-enrolled-by-microsoft-intune-and-system-center-configuration-manager"></a>Como configurar inventário de hardware para dispositivos móveis inscritos pelo Microsoft Intune e o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

No Configuration Manager, é possível recolher o inventário de hardware em dispositivos iOS, Android e Windows dispositivos utilizando o conector do Microsoft Intune. Para obter informações sobre como configurar inventário de hardware, consulte [como expandir o inventário de hardware no System Center Configuration Manager](../../core/clients/manage/inventory/extend-hardware-inventory.md).  

 Para obter informações sobre como inscrever dispositivos no Microsoft Intune, consulte [gerir dispositivos móveis com o Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx).  

## <a name="hardware-inventory-for-mobile-devices"></a>Inventário de hardware para dispositivos móveis  
 As tabelas seguintes listam as classes de inventário disponíveis para o inventário de hardware entre plataformas móveis comummente utilizadas.  

 **iOS**  

|Classe de Inventário de Hardware|iOS|  
|------------------------------|---------|  
|Nome|Device_ComputerSystem.DeviceName|  
|ID de Dispositivo Exclusivo|Device_ComputerSystem.UDID|  
|Número de Série|Device_ComputerSystem.SerialNumber|  
|Endereço de E-mail|Device_Email.OwnerEmailAddress|  
|Tipo de Sistema Operativo|Não aplicável|  
|Versão do Sistema Operativo|Device_OSInformation.OSVersion|  
|Versão de Compilação|Não aplicável|  
|Versão Principal de Service Pack|Não aplicável|  
|Versão Secundária de Service Pack|Não aplicável|  
|Idioma do Sistema Operativo|Não aplicável|  
|Espaço de Armazenamento Total|Device_Memory.DeviceCapacity|  
|Espaço de Armazenamento Livre|Device_Memory.AvailableDeviceCapacity|  
|Identidade Internacional do Equipamento Móvel ou IMEI (IMEI)|Device_ComputerSystem.IMEI|  
|Identificador de Equipamento Móvel (MEID)|Device_ComputerSystem.MEID|  
|Fabricante|Não aplicável|  
|Modelo|ModelName|  
|Número de Telefone<sup>1</sup>|Device_ComputerSystem.PhoneNumber|  
|Operadora Subscritora|Device_ComputerSystem.SubscriberCarrierNetwork|  
|Tecnologia de Rede Móvel|Device_ComputerSystem.CellularTechnology|  
|MAC Wi-Fi|Device_WLAN.WiFiMAC|  

 **Android**  

> [!NOTE]  
>  **NOTA:** Classes de inventário Android estão disponíveis ao utilizar a aplicação Portal da empresa Android.  

|Classe de Inventário de Hardware|Android|  
|------------------------------|-------------|  
|Nome|Não aplicável|  
|ID de Dispositivo Exclusivo|Não aplicável|  
|Número de Série|Device_ComputerSystem.SerialNumber|  
|Endereço de E-mail|Não aplicável|  
|Tipo de Sistema Operativo|Device_OSInformation.Platform|  
|Versão do Sistema Operativo|Device_OSInformation.Version|  
|Versão de Compilação|Não aplicável|  
|Versão Principal de Service Pack|Não aplicável|  
|Versão Secundária de Service Pack|Não aplicável|  
|Idioma do Sistema Operativo|Não aplicável|  
|Espaço de Armazenamento Total|Device_Memory.StorageTotal|  
|Espaço de Armazenamento Livre|Device_Memory.StorageFree|  
|Identidade Internacional do Equipamento Móvel ou IMEI (IMEI)|Device_ComputerSystem.IMEI|  
|Identificador de Equipamento Móvel (MEID)|Não aplicável|  
|Fabricante|Device_Info.Manufacturer|  
|Modelo|Device_Info.Model|  
|Número de Telefone<sup>1</sup>|Device_ComputerSystem.PhoneNumber|  
|Operadora Subscritora|Device_ComputerSystem.SubscriberCarrierNetwork|  
|Tecnologia de Rede Móvel|Device_ComputerSystem.CellularTechnology|  
|MAC Wi-Fi|Device_WLAN.WiFiMAC|  

 **Windows Phone 8/8.1**  

|Classe de Inventário de Hardware|Windows Phone 8 e Windows Phone 8.1|  
|------------------------------|-------------------------------------------|  
|Nome|Device_ComputerSystem.DeviceName|  
|ID de Dispositivo Exclusivo|Device_ComputerSystem.DeviceClientID|  
|Número de Série|Não aplicável|  
|Endereço de E-mail|Device_Email.OwnerEmailAddress|  
|Tipo de Sistema Operativo|Device_OSInformation.Platform|  
|Versão do Sistema Operativo|Device_ComputerSystem.SoftwareVersion|  
|Versão de Compilação|Não aplicável|  
|Versão Principal de Service Pack|Não aplicável|  
|Versão Secundária de Service Pack|Não aplicável|  
|Idioma do Sistema Operativo|Device_OSInformation.Language|  
|Espaço de Armazenamento Total|Não aplicável|  
|Espaço de Armazenamento Livre|Não aplicável|  
|Identidade Internacional do Equipamento Móvel ou IMEI (IMEI)|Não aplicável|  
|Identificador de Equipamento Móvel (MEID)|Não aplicável|  
|Fabricante|Device_ComputerSystem.DeviceManufacturer|  
|Modelo|Device_ComputerSystem.DeviceModel|  
|Número de Telefone<sup>1</sup>|Não aplicável|  
|Operadora Subscritora|Não aplicável|  
|Tecnologia de Rede Móvel|Não aplicável|  
|MAC Wi-Fi|Não aplicável|  

 **Windows RT**  

|Classe de Inventário de Hardware|Windows RT|  
|------------------------------|----------------|  
|Nome|Device_ComputerSystem.DeviceName|  
|ID de Dispositivo Exclusivo|Device_ComputerSystem.DeviceName|  
|Número de Série|Não aplicável|  
|Endereço de E-mail|Device_Email.OwnerEmailAddress|  
|Tipo de Sistema Operativo|CCM_OperatingSystem.SystemType|  
|Versão do Sistema Operativo|Win32_OperatingSystem.Version|  
|Versão de Compilação|Win32_OperatingSystem.BuildNumber|  
|Versão Principal de Service Pack|Win32_OperatingSystem.ServicePackMajorVersion|  
|Versão Secundária de Service Pack|Win32_OperatingSystem.ServicePackMinorVersion|  
|Idioma do Sistema Operativo|Não aplicável|  
|Espaço de Armazenamento Total|Win32_PhysicalMemory.Capacity|  
|Espaço de Armazenamento Livre|Win32_OperatingSystem.FreePhysicalMemory|  
|Identidade Internacional do Equipamento Móvel ou IMEI (IMEI)|Não aplicável|  
|Identificador de Equipamento Móvel (MEID)|Não aplicável|  
|Fabricante|Win32_ComputerSystem.Manufacturer|  
|Modelo|Win32_ComputerSystem.Model|  
|Número de Telefone<sup>1</sup>|Não aplicável|  
|Operadora Subscritora|Não aplicável|  
|Tecnologia de Rede Móvel|Não aplicável|  
|MAC Wi-Fi|Win32_NetworkAdapter.MACAddress|  

 <sup>1</sup> O número de telefone está oculto com * exceto os últimos 4 dígitos.  

 Para o inventário recolher o número de telefone, o dispositivo tem de ter um cartão SIM inserido e um número de telefone aprovisionado pela operadora a esse SIM.  
