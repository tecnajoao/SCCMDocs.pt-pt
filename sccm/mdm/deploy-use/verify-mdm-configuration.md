---
title: "Проверка конфигурации управления мобильными устройствами с помощью System Center Configuration Manager | Документация Майкрософт"
description: "Проверка конфигурации управления мобильными устройствами с помощью System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 94ecfada-97d9-4d5f-bb04-63550dda5f47
caps.latest.revision: "18"
caps.handback.revision: "0"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: ad4b923bd6d3e8acfe799a4ebe2adec737939d75
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="verify-mdm-configuration-with-system-center-configuration-manager"></a>Проверка конфигурации управления мобильными устройствами с помощью System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

Можно проверить определенные компоненты управления устройствами, просмотрев следующие файлы журнала.

-   Проверьте журнал Cloudusersync.log, чтобы убедиться, что учетные записи пользователей успешно синхронизируются.

-   Проверьте журнал Sitecomp.log, чтобы убедиться, что точка подключения службы была успешно создана.

Дополнительные сведения об этих файлах журналов и о том, как их просмотреть, см. в разделе [Файлы журналов функций Configuration Manager](../../core/plan-design/hierarchy/log-files.md#a-namebkmkfunctionlogsa-log-files-for-configuration-manager-functionality).

> [!div class="button"]
[< Назад](set-up-additional-management.md)
