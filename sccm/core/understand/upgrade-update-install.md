---
title: "Сведения об обновлении и установке | Документы Майкрософт"
description: "Узнайте о различиях между терминами \"установка\" и \"обновление\" в контексте управления инфраструктурой Configuration Manager."
ms.custom: na
ms.date: 1/11/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 17fab17f-304d-4f6a-87c7-30ab4f5521ed
caps.latest.revision: "0"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 6bd6cd7ea3c41fa1d70e17a1290c9f1f74cc9e37
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="about-upgrade-update-and-install-for-site-and-hierarchy-infrastructure"></a>Сведения об обновлении и установке для инфраструктуры сайтов и иерархий

*Применимо к: System Center Configuration Manager (Current Branch)*


При управлении инфраструктурой иерархий и сайтов System Center Configuration Manager термины *модернизация*, *обновление* и *установка* обозначают три разных понятия.

## <a name="upgrade"></a>Upgrade
*Обновление* или *обновление на месте* означает преобразование сайта или иерархии Configuration Manager 2012 в сайт или иерархию System Center Configuration Manager.
При обновлении System Center 2012 Configuration Manager до System Center Configuration Manager вы продолжаете использовать те же серверы для размещения сайтов и серверов сайтов. Кроме того, сохраняются существующие данные и конфигурации Configuration Manager.  В отличие от этого при [миграции](/sccm/core/migration/migrate-data-between-hierarchies) сохраняются конфигурации и данные управляемых устройств, но используются новые сайты System Center Configuration Manager, установленные на новом оборудовании.

Дополнительные сведения см. в разделе [Обновление до System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager).



## <a name="update"></a>Обновление
Термин *обновление* также используется в отношении установки обновлений в консоли для System Center Configuration Manager и в отношении внештатных обновлений, то есть обновлений, которые не могут быть предоставлены из консоли Configuration Manager. Обновления в консоли могут изменять версию сайта Current Branch (или Technical Preview), то есть производится переход на более позднюю версию. Например, если у вас есть сайт версии 1606, вы можете установить обновление для версии 1610. С помощью обновлений также могут устанавливаться исправления для известных проблем без изменения версии сайта.      

Как правило, обновления служат для применения исправлений для системы безопасности, повышения качества и добавления новых функций в существующую среду. Если вы используете ветвь Technical Preview, обновление может установить более позднюю версию Technical Preview.
-   Вы выбираете время установки обновления в консоли начиная с сайта верхнего уровня в иерархии.
- Из консоли можно установить любое доступное обновление. Например, если сайт работает под управлением версии 1602 и предлагаются версии 1606 и 1610, рекомендуется установить версию 1610, так как каждая версия включает в себя функции, которые были реализованы в ранее выпущенных версиях.
- После завершения установки обновления на сайте верхнего уровня автоматически начинается обновление дочерних первичных сайтов. Однако вы можете настроить [периоды обслуживания](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkservicewindowa-service-windows-for-site-servers), чтобы контролировать время выполнения обновления.
- На вторичных сайтах обновления автоматически не устанавливаются. Вместо этого обновление следует запустить вручную с помощью консоли Configuration Manager.

Дополнительные сведения см. в разделах [Обновления для System Center Configuration Manager](/sccm/core/servers/manage/updates) и [Technical Preview для System Center Configuration Manager](/sccm/core/get-started/technical-preview).



## <a name="install"></a>Установка
*Установка* используется при создании иерархии Configuration Manager с нуля или добавлении новых сайтов в существующую иерархию.  

При установке нового первичного сайта или сайта центра администрирования расположение файла setup.exe и связанных исходных файлов зависит от сценария установки.

Дополнительные сведения см. в разделе [Подготовка к установке сайтов](/sccm/core/servers/deploy/install/prepare-to-install-sites).
