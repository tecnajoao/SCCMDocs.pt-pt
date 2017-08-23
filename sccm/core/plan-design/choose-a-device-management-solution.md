---
title: "Выбор решения для управления устройствами в Configuration Manager | Документы Майкрософт"
description: "Сведения о решениях, предлагаемых System Center Configuration Manager для управления ПК, серверами и устройствами."
ms.custom: na
ms.date: 12/08/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 24633725-791a-4df7-8dce-2c24c1a19a03
caps.latest.revision: "14"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 9989ea1bf4cb74a6286ebae9de7614ed622de5b6
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="choose-a-device-management-solution-for-system-center-configuration-manager"></a>Выбор решения для управления устройствами в System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager (SCCM) включает в себя различные решения для управления компьютерами, серверами и устройствами. Вы можете выбрать подходящее решение в зависимости от платформ устройств, которыми необходимо управлять, и от требуемых функций управления.  


##  <a name="overview-of-device-management-solutions"></a>Общие сведения о решениях для управления устройствами  
 В этой статье описаны четыре решения для управления устройствами: клиентское приложение Configuration Manager, локальная инфраструктура Configuration Manager, Microsoft Intune и Exchange. В конце этой статьи приведены две сравнительных таблицы решений. В одной таблице производится сравнение [по поддерживаемым платформам мобильных устройств](#compare-device-management-solutions-based-on-supported-mobile-device-platforms), в другой — [по функциям управления](#compare-mobile-device-management-solutions-based-on-management-functionality).


###  <a name="manage-devices-with-the-configuration-manager-client"></a>Управление устройствами с помощью клиента Configuration Manager  

Этот вариант, при котором требуется установка клиента Configuration Manager на каждом устройстве, предоставляет больше всего функций для управления компьютерами, серверами и другими устройствами в вашей среде. Дополнительные сведения см. в разделе [Методы установки клиента в System Center Configuration Manager](/sccm/core/clients/deploy/plan/client-installation-methods).  

###  <a name="manage-devices-with-on-premises-configuration-manager-infrastructure"></a>Управление устройствами с помощью локальной инфраструктуры Configuration Manager  

В этом варианте используются возможности управления устройствами, встроенные в операционные системы для некоторых платформ устройств. Хотя при локальном управлении мобильными устройствами вы не получаете такой же обширный набор функций, как при управлении с помощью клиента, этот подход будет более простым за счет использования локальных ресурсов Configuration Manager для охвата устройств и управления ими. Обратите внимание, что сейчас этот вариант поддерживается только для компьютеров с Windows 10 и устройств с Windows 10 Mobile.  

Дополнительные сведения см. в разделе [Управление мобильными устройствами с помощью локальной инфраструктуры в System Center Configuration Manager](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

###  <a name="manage-devices-with-microsoft-intune-hybrid"></a>Управление устройствами с помощью Microsoft Intune (гибридное управление)  

В этом варианте для регистрации устройств и управления ими используется служба Microsoft Intune, а не локальные ресурсы Configuration Manager. Несмотря на то что Intune управляет устройствами, доступ к задачам управления осуществляется из консоли Configuration Manager. Этот вариант поддерживает все основные операционные системы мобильных устройств, включая Windows 10 Mobile, Windows Phone, iOS, Mac OS X и Android. Он также обеспечивает управление компьютерами с Windows 8.1 и Windows 10 в вашей организации.  

Дополнительные сведения см. в статье [Гибридное управление мобильными устройствами (MDM) с помощью System Center Configuration Manager и Microsoft Intune](../../mdm/understand/hybrid-mobile-device-management.md).  

###  <a name="manage-devices-with-microsoft-exchange"></a>Управление устройствами с помощью Microsoft Exchange  

В этом варианте используется соединитель Exchange Server, который подключает несколько серверов Exchange к Configuration Manager. Это позволяет централизованно управлять устройствами, которые могут подключаться к Exchange ActiveSync. В консоли Configuration Manager можно настроить такие функции управления мобильными устройствами Exchange, как удаленная очистка устройств и управление параметрами для нескольких серверов Exchange.  

Дополнительные сведения см. в разделе [Управление мобильными устройствами с помощью System Center Configuration Manager и Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

Вы можете использовать эти решения для управления устройствами как по отдельности, так и в сочетании друг с другом. Например, можно использовать подход к управлению на основе клиентов для управления компьютерами и серверами в вашей организации и использовать Intune для управления мобильными устройствами. Объединив эти подходы таким образом, вы сможете выполнять все необходимые задачи, связанные с управлением устройствами, в консоли Configuration Manager.  

## <a name="compare-device-management-solutions-based-on-supported-mobile-device-platforms"></a>Сравнение решений для управления мобильными устройствами на основе поддерживаемых платформ мобильных устройств  

|Платформа|С клиентом Configuration Manager|Configuration Manager с Microsoft Intune (гибридная)|Локальное управление мобильными устройствами|Configuration Manager с Exchange|  
|--------------|-------------------------------------------|-------------------------------------------------------------------|-------------------------------|-----------------------------------------|  
|Android||Да||Да|  
|iOS||Да||Да|  
|Mac OS X|Да|||Да|  
|UNIX/Linux|Да|||Да|  
|Windows 10|Да|Да|Да|Да|  
|Windows 10 Mobile||Да|Да|Да|  
|Windows (предыдущие версии)|Да|Да||Да|  
|Windows CE|Да (с устаревшим клиентом мобильных устройств)|||Да|  
|Windows Embedded|Да||||  
|Windows Phone||Да||Да|  
|Windows Server|Да|||Да|  

 Полный список поддерживаемых платформ см. в статье [Поддерживаемые операционные системы для клиентов и устройств в System Center Configuration Manager](configs\supported-operating-systems-for-clients-and-devices.md).

##  <a name="bkmk_comp2"></a> Сравнение решений для управления мобильными устройствами на основе функциональности управления  

|Функция управления|С клиентом Configuration Manager|Configuration Manager с Microsoft Intune (гибридная)|Локальное управление мобильными устройствами|Configuration Manager с Exchange|  
|------------------------------|-------------------------------------------|-------------------------------------------------------------------|-------------------------------|-----------------------------------------|  
|Безопасность инфраструктуры открытых ключей (PKI) между мобильным устройством и Configuration Manager (использование взаимной проверки подлинности и протокола SSL для шифрования передаваемых данных)|Да|Да|Да||  
|Установка клиента|Да||||  
|Поддержка через Интернет|Да||||  
|Обнаружение|Да|||Да|  
|Инвентаризация оборудования|Да|Да|Да|Да|  
|Инвентаризация программного обеспечения|Да|||Да|  
|Параметры|Да|Да|Да|Да|  
|Развертывание программного обеспечения|Да|Да|Да||  
|Мониторинг с помощью резервной точки состояния|Да||||  
|Подключения к точкам управления|Да||Да||  
|Подключения к точкам распространения|Да||Да||  
|Блокировка из Configuration Manager|Да|Да|Да||  
|Карантин и блокировка из Exchange Server (и Configuration Manager)||||Да|  
|Удаленная очистка| |Да|Да|Да|  
