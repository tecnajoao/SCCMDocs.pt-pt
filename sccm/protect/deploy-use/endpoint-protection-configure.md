---
title: "Настройка Endpoint Protection | Документы Майкрософт"
description: "Узнайте, как настроить Configuration Manager для обновления и распространения определений вредоносных программ для Защитника Windows."
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
caps.latest.revision: "21"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 6917644d6719a1ca636713aa5aebf277927123c8
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="configure-endpoint-protection"></a>Настройка Endpoint Protection

*Применимо к: System Center Configuration Manager (Current Branch)*

Прежде чем приступить к использованию Endpoint Protection для управления системой безопасности и защиты от вредоносных программ на клиентских компьютерах Configuration Manager, необходимо выполнить этапы настройки, описанные в этом разделе.  

## <a name="how-to-configure-endpoint-protection-in-configuration-manager"></a>Настройка Endpoint Protection в Configuration Manager  
 Endpoint Protection в Configuration Manager имеет внешние зависимости и зависимости в пределах продукта.  

### <a name="steps-to-configure-endpoint-protection-in-configuration-manager"></a>Этапы настройки Endpoint Protection в Configuration Manager  
 Следующая таблица содержит этапы, подробности и дополнительные сведения о настройке Endpoint Protection.  

> [!IMPORTANT]  
>  Если управление Endpoint Protection осуществляется для компьютеров Windows 10, необходимо настроить Configuration Manager для обновления и распространения определений вредоносных программ для Защитника Windows. Защитник Windows входит в состав Windows 10, но по-прежнему требуется устанавливать SCEPInstall и задавать настраиваемые параметры клиентов для Endpoint Protection (**шаг 5**).  

|Шаги|Подробные сведения|  
|-----------|-------------|  
|**Шаг 1.** [Создание роли системы сайта для точки Endpoint Protection](endpoint-protection-site-role.md)|Прежде чем использовать Endpoint Protection, устанавливается роль системы сайта точки Endpoint Protection. Ее следует устанавливать только на одном сервере системы сайта (на верхнем уровне иерархии сайта центра администрирования или автономного первичного сайта). |  
|**Шаг 2.** [Настройка оповещений для Endpoint Protection](endpoint-configure-alerts.md)|Оповещения информируют администратора при возникновении определенных событий, например при заражении компьютера вредоносными программами. Оповещения отображаются в узле **Оповещения** рабочей области **Мониторинг** или дополнительно могут быть отправлены указанным пользователям по электронной почте. |  
|**Шаг 3.** [Настройка источников обновления определений для клиентов Endpoint Protection](endpoint-definition-updates.md)|Endpoint Protection можно настроить для использования различных источников для скачивания обновлений определений. |  
|**Шаг 4.** [Настройка политики защиты от вредоносных программ по умолчанию и создание настраиваемых политик защиты от вредоносных программ](endpoint-antimalware-policies.md)|Политика защиты от вредоносных программ, используемая по умолчанию, применяется при установке клиента Endpoint Protection. Любые развернутые настраиваемые политики применяются по умолчанию в течение 60 минут процесса развертывания клиента. Перед тем как развернуть клиент Endpoint Protection, убедитесь, что политики защиты от вредоносных программ настроены. |  
|**Шаг 5.** [Задание значений настраиваемых параметров клиентов для Endpoint Protection](endpoint-protection-configure-client.md)|Используйте настраиваемые параметры клиентов, чтобы задать значения параметров Endpoint Protection для коллекций компьютеров в иерархии.<br /><br /> Примечание. Не следует изменять значения параметров клиентов Endpoint Protection, используемые по умолчанию, кроме случаев, когда требуется с уверенностью применить их на всех компьютерах в иерархии. |  
