---
title: "Настройка инвентаризации оборудования | Документы Майкрософт"
description: "Настройка инвентаризации оборудования для всех клиентов или для коллекции в System Center Configuration Manager."
ms.custom: na
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0e45290e-f8f7-4335-801e-570225d12c2b
caps.latest.revision: "5"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 0baadb95ec8dbb945f1a611ebb95a03cec3199bd
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-configure-hardware-inventory-in-system-center-configuration-manager"></a>How to configure hardware inventory in System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

В ходе этой процедуры выполняется настройка параметров клиента по умолчанию для инвентаризации оборудования и их применение ко всем клиентам в иерархии. Если эти параметры требуется применить только к некоторым клиентам, создайте настраиваемые параметры клиентского устройства и назначьте их коллекции, которая содержит необходимые клиенты. См. раздел [Настройка параметров клиента в System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

> [!NOTE]  
>  Если клиентское устройство получает параметры инвентаризации из нескольких наборов клиентских параметров, классы инвентаризации оборудования из каждого набора параметров будут объединены при передаче клиентом данных инвентаризации оборудования.  

### <a name="to-configure-hardware-inventory"></a>Настройка инвентаризации оборудования  

1.  В консоли Configuration Manager последовательно выберите **Администрирование** > **Параметры клиента** > **Параметры клиента по умолчанию**.  

4.  На вкладке **Главная** в группе **Свойства** нажмите кнопку **Свойства**.  

5.  В диалоговом окне **Параметры по умолчанию** выберите пункт **Инвентаризация оборудования**.  

6.  В списке **Параметры устройства** настройте следующие параметры.  

    -   **Включить инвентаризацию оборудования для клиентов** — выберите значение **True**.  

    -   **Расписание инвентаризации оборудования** — щелкните **Расписание**, чтобы указать интервал сбора клиентами данных инвентаризации оборудования.  

7.  Настройте другие необходимые [параметры клиента, относящиеся к инвентаризации оборудования](../../../../core/clients/deploy/about-client-settings.md#hardware-inventory).  

Клиентские устройства будут настроены с использованием данных параметров при следующем скачивании ими клиентской политики. Чтобы инициировать получение политики для отдельного клиента, см. сведения в статье [Управление клиентами в System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  
