---
title: "Управление LTSB | Документация Майкрософт"
description: "Различия в управлении LTSB System Center Configuration Manager."
ms.custom: na
ms.date: 05/01/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8da2887a-fd8e-438c-b926-849c121f7fdf
caps.latest.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 9c6f349ead906532a7a58df74609de976769e251
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="manage-the-long-term-servicing-branch-of-configuration-manager"></a>Управление ветвью Configuration Manager (Long-Term Servicing Branch)

*Применимо к: System Center Configuration Manager (Long-Term Servicing Branch)*

Если вы работаете с ветвью System Center Configuration Manager Long-Term Servicing Branch (LTSB), используйте следующие сведения, чтобы ознакомиться с важными изменениями, влияющими на управление инфраструктурой.

Так как ветвь LTSB эквивалентна версии Current Branch 1606 (за некоторыми исключениями, такими как интеграция с Intune и облачными компонентами), большинство задач, используемых для планирования, развертывания, настройки и ежедневного управления, идентичны.

Например, LTSB поддерживает такое же число сайтов, типы сайтов, клиенты и общие инфраструктуры, как и Current Branch. Поэтому вы можете использовать рекомендации в разделах, посвященных планированию и проектированию сайтов и иерархии для Current Branch. Аналогичным образом для функций LTSB, поддерживаемых обеими ветвями, таких как обновления программного обеспечения или развертывание операционной системы, можно использовать рекомендации в соответствующих разделах документации по Current Branch с учетом отсутствия доступа к изменению функций, появившегося после версии Current Branch 1606.

В следующих разделах содержатся сведения об управлении задачами, которые отличаются друг от друга.

## <a name="updates-and-servicing"></a>Обновления и обслуживание
В качестве обновлений в консоли в LTSB доступны только критические обновления безопасности.  

В консоли отображаются сведения о регулярных обновлениях для последующих выпусков Current Branch, но данные об обновлениях LTSB отсутствуют. Они недоступны для загрузки и установки.

Для поддержки обновлений в консоли для установки критически важных исправлений на сайте LTSB требуется использовать [точку подключения службы](/sccm/core/servers/deploy/configure/about-the-service-connection-point). Эту роль системы сайта можно настроить в сетевом или автономном режиме, как и для Current Branch. LTSB собирает и отправляет те же данные телеметрии и использования, что и Current Branch.

LTSB поддерживает использование установщика исправлений и средства регистрации обновлений, как задокументировано для Current Branch.

Общие сведения об обновлениях и обслуживании см. в разделе [Обновления для Configuration Manager](/sccm/core/servers/manage/updates).


## <a name="changes-for-site-expansion-and-the-cdlatest-folder"></a>Изменения для расширения сайта и папки CD.Latest
Если при использовании LTSB выполняется расширение автономного первичного сайта путем установки нового сайта центра администрирования, необходимо использовать программу установки и исходные файлы с базового носителя версии 1606. Для Current Branch используется программа установки и исходные файлы из папки CD.Latest.

Хотя вы не запускаете программу установки для расширения сайта из папки CD.Latest, эту папку по-прежнему можно использовать для восстановления сайта, а также для установки нового дочернего первичного сайта, если первый сайт LTSB был сайтом центра администрирования.

Дополнительные сведения о расширении автономного первичного сайта см. в [этом разделе](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#expand-a-stand-alone-primary-site). Дополнительные сведения о папке CD.Latest см. в разделе [Папка CD.Latest](/sccm/core/servers/manage/the-cd.latest-folder).


## <a name="recovery"></a>Модель
При восстановлении сайта необходимо восстановить сайт или базу данных сайта до исходной ветви. Невозможно восстановить базу данных сайта Current Branch до установки LTSB и наоборот.
