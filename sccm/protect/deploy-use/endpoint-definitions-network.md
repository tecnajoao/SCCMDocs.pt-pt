---
title: "Скачивание определений Endpoint Protection из сетевой папки | Документы Майкрософт"
description: "Узнайте, как вручную загрузить последние обновления определений с сайта корпорации Майкрософт и затем настроить клиенты для скачивания этих определений."
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: ddef4d2a-f481-4020-9ddd-9cca5f9795cb
caps.latest.revision: "21"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 110bd9a9d04b27ef6794145fae66dbd910308bdc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-a-network-share-for-configuration-manager"></a>Включение скачивания определений вредоносных программ Endpoint Protection из сетевой папки для Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

 Вы можете вручную загрузить последние обновления определений из корпорации Майкрософт и затем настроить клиенты для загрузки этих определений из общей папки в сети. Когда вы используете этот источник обновления, пользователи также могут инициировать обновления.

> [!NOTE]
>  Чтобы загружать обновления определений, клиенты должны иметь доступ на чтение общей папки.

 Дополнительные сведения о скачивании обновлений определений и антивирусного модуля для сохранения в общей папке см. в разделе [Установка последнего антивредоносного и антишпионского ПО Майкрософт](http://www.microsoft.com/security/portal/Definitions/HowToForeFront.aspx).

## <a name="to-configure-definition-downloads-from-a-file-share"></a>Настройка загрузки определений из общей папки

1.  В консоли Configuration Manager щелкните элемент **Активы и соответствие**.

2.  В рабочей области **Активы и соответствие** разверните узел **Endpoint Protection**и щелкните **Политики защиты от вредоносных программ**.

3.  Откройте страницу свойств **политики защиты от вредоносных программ по умолчанию** или создайте новую политику защиты от вредоносных программ. Дополнительные сведения о создании политик защиты от вредоносных программ см. в разделе [Создание и развертывание политик защиты от вредоносных программ для Endpoint Protection в System Center Configuration Manager](endpoint-antimalware-policies.md).

4.  В разделе **Обновления определений** диалогового окна свойств защиты от вредоносных программ щелкните **Задать источник**.

5.  В диалоговом окне **Настройка источников обновления определений** выберите **Обновления из общих папок в формате UNC**.

6.  Нажмите кнопку **ОК** , чтобы закрыть диалоговое окно **Настройка источников обновления определений** .

7.  Нажмите кнопку **Задать пути**. Затем в диалоговом окне **Настройка UNC-путей обновления определений** добавьте UNC-пути к расположению файлов обновлений определений на общем сетевом ресурсе.

8.  Нажмите кнопку **ОК** , чтобы закрыть диалоговое окно **Настройка UNC-путей обновления определений** .


> [!div class="button"]
[Следующий этап >](endpoint-antimalware-policies.md)

> [!div class="button"]
[Назад >](endpoint-configure-alerts.md)
