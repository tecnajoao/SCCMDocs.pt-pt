---
title: "Advanced Threat Protection в Защитнике Windows | Документы Майкрософт"
description: "Сведения о мониторинге Advanced Threat Protection в Защитнике Windows и управлении этой новой службой, которая помогает предприятиям реагировать на атаки повышенной сложности."
ms.custom: na
ms.date: 03/07/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a5fc033e-828e-4e45-9097-bbbd0697ebdf
caps.latest.revision: "5"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 6c3b67278fa587c137a29e174e277fb0f15872c8
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="windows-defender-advanced-threat-protection"></a>Advanced Threat Protection в Защитнике Windows

*Применимо к: System Center Configuration Manager (Current Branch)*

Начиная с Configuration Manager версии 1606 (Current Branch) Endpoint Protection помогает отслеживать службу Advanced Threat Protection (ATP) в Защитнике Windows и управлять ею. ATP в Защитнике Windows представляет собой новую службу, с помощью которой предприятия могут обнаруживать, исследовать атаки повышенной сложности и реагировать на них в своих сетях.  Узнайте больше об [ATP в Защитнике Windows](http://aka.ms/technet-wdatp). Политики Configuration Manager помогут вам подключить управляемую ОС Windows 10 версии 1607 (сборка 14328) или более поздние версии и вести за ней наблюдение.

Служба ATP в Защитнике Windows доступна в [центре обеспечения безопасности](https://securitycenter.windows.com). После добавления и развертывания файла конфигурации подключения клиента Configuration Manager может отслеживать состояние развертывания и состояние работоспособности агента ATP в Защитнике Windows. Служба ATP в Защитнике Windows поддерживается только на компьютерах под управлением клиента Configuration Manager. Локальное управление мобильными устройствами и компьютеры с гибридным управлением MDM в Intune не поддерживаются.

 **Предварительные требования**  

-   Подписка на веб-службу Advanced Threat Protection в Защитнике Windows  
-   Клиентские компьютеры под управлением Windows 10 версии 1607 и выше  
-   Клиентские компьютеры под управлением Configuration Manager версии 1610 или более поздней версии агента клиента

## <a name="how-to-create-an-onboarding-configuration-file"></a>Создание файла конфигурации подключения  

 1.  Войдите в [веб-службу ATP в Защитнике Windows](https://securitycenter.windows.com/).   

 2.  Выберите пункт меню **Управление конечными точками**.  

 3.  Выберите **System Center Configuration Manager (Current Branch) версии 1606** и нажмите кнопку **Скачать пакет**.  

 4.  Скачайте сжатый файл архива (ZIP-файл) и извлеките его содержимое.

> [!IMPORTANT]
> Файл конфигурации ATP в Защитнике Windows содержит конфиденциальные сведения, которые должны быть защищены.

## <a name="onboard-devices-for-windows-defender-atp"></a>Подключение устройств для ATP в Защитнике Windows  

1.  В консоли Configuration Manager последовательно выберите **Активы и соответствие** > **Обзор** > **Endpoint Protection** > **Политики ATP в Защитнике Windows** и щелкните **Создать политику Windows Defender ATP**. Откроется мастер политики ATP в Защитнике Windows.  

2.  Укажите значения в полях **Имя** и **Описание** для политики ATP в Защитнике Windows и выберите **Подключение**. Нажмите кнопку **Далее**.  

3.  **Найдите** файл конфигурации, предоставленный клиентом облачной службы ATP в Защитнике Windows вашей организации. Нажмите кнопку **Далее**.  

4.  Укажите образцы файлов, которые собираются и совместно используются с управляемых устройств для анализа.  

    -   **Нет**   

    -   **Все типы файлов**  

     Нажмите кнопку **Далее**.  

5.  Просмотрите сводные данные и завершите работу мастера.  

6.  Теперь можно развернуть политику ATP в Защитнике Windows на клиентских компьютерах, щелкнув **Развернуть**.  

## <a name="monitor-windows-defender-atp"></a>Мониторинг ATP в Защитнике Windows  

1.  В консоли Configuration Manager последовательно выберите **Мониторинг** > **Обзор** > **Безопасность** и щелкните **ATP в Защитнике Windows**.  

2.  Просмотрите сведения на панели мониторинга Advanced Threat Protection в Защитнике Windows.  

    -   **Состояние развертывания агента Защитника Windows** — количество и процент соответствующих управляемых клиентских компьютеров с активной включенной политикой ATP в Защитнике Windows.  

    -   **Состояние работоспособности агента ATP в Защитнике Windows** — процент клиентских компьютеров, сообщающих о состоянии агента ATP в Защитнике Windows.  

        -   **Работоспособно** — работает должным образом.  

        -   **Неактивно** — в течение определенного периода времени данные в службу не отправляются.  

        -   **Состояние агента** — системная служба для агента в Windows не запущена.  

        -   **Не подключено** — политика была применена, но агент не сообщил о ее подключении.  


## <a name="how-to-create-and-deploy-an-offboarding-configuration-file"></a>Создание и развертывание файла конфигурации отключения  

1.  Войдите в [веб-службу ATP в Защитнике Windows](https://securitycenter.windows.com/).   

2.  Выберите пункт меню **Управление конечными точками**.  

3.  Выберите **System Center Configuration Manager (Current Branch) версии 1606** и нажмите кнопку **Отключение конечной точки**.  

4.  Скачайте сжатый файл архива (ZIP-файл) и извлеките его содержимое. Файлы отключения действуют в течение 30 дней.

5.  В консоли Configuration Manager последовательно выберите **Активы и соответствие** > **Обзор** > **Endpoint Protection** > **Политики ATP в Защитнике Windows** и щелкните **Создать политику Windows Defender ATP**. Откроется мастер политики ATP в Защитнике Windows.  

6.  Укажите значения в полях **Имя** и **Описание** для политики ATP в Защитнике Windows и выберите **Подключение**. Нажмите кнопку **Далее**.  

7.  **Найдите** файл конфигурации, предоставленный клиентом облачной службы ATP в Защитнике Windows вашей организации. Нажмите кнопку **Далее**.  

8.  Просмотрите сводные данные и завершите работу мастера.  

9.  Теперь можно развернуть политику ATP в Защитнике Windows на клиентских компьютерах, щелкнув **Развернуть**.  

> [!IMPORTANT]
> Файлы конфигурации ATP в Защитнике Windows содержат конфиденциальные сведения, которые должны быть защищены.

[Advanced Threat Protection в Защитнике Windows](https://technet.microsoft.com/itpro/windows/keep-secure/windows-defender-advanced-threat-protection)

[Устранение неполадок с переходом на Advanced Threat Protection в Защитнике Windows](https://technet.microsoft.com/itpro/windows/keep-secure/troubleshoot-onboarding-windows-defender-advanced-threat-protection)
