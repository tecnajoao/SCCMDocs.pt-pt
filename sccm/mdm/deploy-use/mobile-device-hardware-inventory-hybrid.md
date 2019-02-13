---
title: Configurar o inventário de hardware para dispositivos móveis
titleSuffix: Configuration Manager
description: Configure o inventário de hardware para dispositivos móveis inscritos pelo Microsoft Intune e o System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 78a0aecc-f775-451e-aa05-56377ec91b1f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d1a208b3bac5d0b12a9fd395506f02d283a0b55f
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56125090"
---
# <a name="how-to-configure-hardware-inventory-for-mobile-devices-enrolled-by-microsoft-intune-and-system-center-configuration-manager"></a>Como configurar inventário de hardware para dispositivos móveis inscritos pelo Microsoft Intune e o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

No Configuration Manager, é possível recolher o inventário de hardware em iOS, Android e Windows dispositivos ao utilizar o conector do Microsoft Intune. Para obter informações sobre como configurar inventário de hardware, consulte [como expandir o inventário de hardware no System Center Configuration Manager](../../core/clients/manage/inventory/extend-hardware-inventory.md).  

 Para obter informações sobre como inscrever dispositivos no Microsoft Intune, consulte [gerir dispositivos móveis com o Microsoft Intune](https://technet.microsoft.com/library/dn646962.aspx).  

## <a name="hardware-inventory-for-mobile-devices"></a>Inventário de hardware para dispositivos móveis  
 As tabelas seguintes listam as classes de inventário disponíveis para o inventário de hardware em plataformas móveis comumente utilizadas.  

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
>  **NOTA:** Classes de inventário Android estão disponíveis quando utilizar a aplicação Portal da empresa para Android.  

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
