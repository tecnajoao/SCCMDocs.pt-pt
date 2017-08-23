---
title: "Брандмауэры и домены | Документы Майкрософт"
description: "Настройка брандмауэров, портов и доменов для подготовки к взаимодействию с System Center Configuration Manager."
ms.custom: na
ms.date: 2/6/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d6993bba-f6bd-4639-adbf-efc1c638b2f3
caps.latest.revision: "15"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 4a2a8f96a900a2c4959ae3ff59232771ece95991
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="set-up-firewalls-ports-and-domains-for-system-center-configuration-manager"></a>Настройка брандмауэров, портов и доменов для System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

Чтобы подготовить сеть к поддержке System Center Configuration Manager, спланируйте настройку инфраструктуры, например брандмауэров, для передачи данных, используемых Configuration Manager.  

|Соображения|Подробные сведения|  
|-------------------|-------------|  
|**Порты и протоколы**, используемые различными возможностями Configuration Manager. Некоторые порты являются обязательными, тогда как другие **домены и службы** можно настроить.|Большинство функций взаимодействия Configuration Manager использует общие порты, например порт 80 для HTTP и порт 443 для HTTPS. Однако [некоторые роли системы сайта поддерживают использование настраиваемых веб-сайтов](/sccm/core/plan-design/network/websites-for-site-system-servers) и портов.<br /><br /> **Перед развертыванием Configuration Manager** определите порты, которые планируется использовать, и соответствующим образом настройте брандмауэры.<br /><br /> **Если потребуется изменить порт** после установки Configuration Manager, не забудьте обновить брандмауэры на устройствах и в сети, а также изменить конфигурацию порта в Configuration Manager.<br /><br /> Дополнительные сведения см. в следующих статьях: </br>- [Настройка портов связи для клиентов](../../../core/clients/deploy/configure-client-communication-ports.md) </br>- [Порты, используемые программой Configuration Manager](../../../core/plan-design/hierarchy/ports.md) </br>- [Требования для доступа к Интернету для точки подключения службы](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_urls)|  
|**Домены и службы**, которые может потребоваться использовать серверам сайта и клиентам.|Для использования возможностей Configuration Manager может потребоваться доступ серверов сайта и клиентов к отдельным службам и доменам в Интернете, например Windowsudpate.microsoft.com или службе Microsoft Intune.<br /><br /> Если вы будете использовать Microsoft Intune для управления мобильными устройствами, необходимо, кроме того, настроить доступ к [портам и доменам, которые нужны Intune](https://docs.microsoft.com/en-us/intune/get-started/network-infrastructure-requirements-for-microsoft-intune).|  
|**Прокси-серверы** для взаимодействия серверов системы сайта и клиентов. Вы можете указать разные прокси-серверы для отдельных клиентов и серверов системы сайта.|Поскольку эти настройки выполняются во время установки роли системы сайта или клиента, необходимо предусмотреть только конфигурации прокси-сервера для дальнейшего использования при настройке ролей системы сайта и клиентов.<br /><br /> Если вы не знаете, потребуются ли вашему развертыванию прокси-серверы, просмотрите статью [Поддержка прокси-сервера в System Center Configuration Manager](../../../core/plan-design/network/proxy-server-support.md) для получения сведений о действиях ролей системы сайта и клиентов, которые могут использовать прокси-сервер.|   
|  
