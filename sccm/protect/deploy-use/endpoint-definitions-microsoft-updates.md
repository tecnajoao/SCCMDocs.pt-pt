---
title: "Скачивание определений Endpoint Protection из сетевой папки | Документы Майкрософт"
description: "Узнайте, как обеспечить скачивание определений вредоносных программ Endpoint Protection из Центра обновления Майкрософт для Configuration Manager."
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: ab7626ae-d4bf-4ca6-ab25-c61f96800a02
caps.latest.revision: "21"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 58c468fc3d4427cc1f2a8f197ab784a767151203
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-microsoft-updates-for-configuration-manager"></a>Включение скачивания определений вредоносных программ Endpoint Protection из Центра обновлений Майкрософт для Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*


 При загрузке обновлений определений из Центра обновления Майкрософт клиенты будут проверять сайт Центра обновления Майкрософт через интервал, указанный в разделе **Обновления определений** диалогового окна политики защиты от вредоносных программ.

 Этот метод может быть полезен, когда у клиента отсутствует подключение к сайту Configuration Manager или если требуется, чтобы пользователи могли инициировать обновления определений.

> [!IMPORTANT]
>  Чтобы использовать этот метод для загрузки обновлений определений, клиенты должны иметь доступ к Центру обновления Майкрософт через Интернет.

## <a name="using-the-microsoft-malware-protection-center-to-download-definitions"></a>Использование Центра Майкрософт по защите от вредоносных программ для загрузки определений
 Вы можете настроить клиенты для загрузки обновлений из Центра Майкрософт по защите от вредоносных программ. Клиенты Endpoint Protection применяют эту возможность для скачивания обновлений определений, если они не смогли загрузить обновления из другого источника. Этот метод обновления может быть полезен, если в вашей инфраструктуре Configuration Manager существует проблема, препятствующая доставке обновлений.

> [!IMPORTANT]
>  Чтобы использовать этот метод для загрузки обновлений определений, клиенты должны иметь доступ к Центру обновления Майкрософт через Интернет.


> [!div class="button"]
[Следующий этап >](endpoint-antimalware-policies.md)

> [!div class="button"]
[Назад >](endpoint-configure-alerts.md)
