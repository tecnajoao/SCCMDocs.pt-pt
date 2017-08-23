---
title: Endpoint Protection | Microsoft Docs
description: "Узнайте, как управлять политиками защиты от вредоносных программ и параметрами безопасности брандмауэра Windows для клиентских компьютеров в иерархии Configuration Manager."
ms.custom: na
ms.date: 02/6/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 76c90f64-d729-456b-8304-01852cd66fb6
caps.latest.revision: "11"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 3c31271f3e3ae7aa45da03b3d75fd78242330646
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="endpoint-protection"></a>Endpoint Protection

*Применимо к: System Center Configuration Manager (Current Branch)*

Endpoint Protection в System Center Configuration Manager позволяет управлять политиками защиты от вредоносных программ и параметрами безопасности брандмауэра Windows для клиентских компьютеров в иерархии Configuration Manager.  

> [!IMPORTANT]  
>  Чтобы использовать Endpoint Protection для управления клиентами в иерархии Configuration Manager, необходима лицензия.  

 Совместное использование Endpoint Protection и Configuration Manager обеспечивает следующие преимущества:  

-   Настройка политик защиты от вредоносных программ, параметров брандмауэра Windows и управление Advanced Threat Protection в Защитнике Windows для выбранных групп компьютеров.  
-   Использование обновлений программного обеспечения Configuration Manager для загрузки актуальных файлов определений вредоносных программ на клиентские компьютеры.  
-   Отправка уведомлений по электронной почте, использование средств мониторинга в консоли и просмотр отчетов, чтобы информировать пользователей с правами администратора об обнаружении вредоносных программ на клиентских компьютерах  

На компьютерах под управлением ОС начиная с Windows 10 и Windows Server 2016 Защитник Windows уже установлен. В этих операционных системах клиент управления для Защитника Windows устанавливается при установке клиента Configuration Manager. На компьютерах под управлением Windows 8.1 и более ранних версий вместе с клиентом Configuration Manager также устанавливается клиент Endpoint Protection. Возможности клиентов Защитника Windows и Endpoint Protection:  

-   обнаружение и исправление вредоносных программ и шпионского программного обеспечения;  
-   обнаружение и исправление пакетов программ rootkit;  
-   оценка критических уязвимостей и автоматическое обновление определений и антивирусного модуля;  
-   обнаружение уязвимости сети с помощью системы проверки сети;  
-   интеграция со службой Cloud Protection Service для передачи сведений о вредоносных программах в Майкрософт. При подключении этой службы клиент Endpoint Protection или Защитник Windows, обнаружив на компьютере неопознанную вредоносную программу, может скачивать новейшие определения из Центра по защите от вредоносных программ.  

> [!NOTE]  
>  Клиент Endpoint Protection можно установить на сервере под управлением Hyper-V и на гостевых виртуальных машинах с поддерживаемыми операционными системами. Во избежание чрезмерного использования ресурсов ЦП действия Endpoint Protection имеют встроенную случайную задержку, чтобы службы защиты не запускались одновременно.  

 Кроме того, Endpoint Protection в Configuration Manager позволяет управлять параметрами брандмауэра Windows в консоли Configuration Manager.  

 См. раздел [Пример сценария: использование System Center Endpoint Protection для защиты компьютеров от вредоносных программ в System Center Configuration Manager](scenarios-endpoint-protection.md).  


## <a name="managing-malware-with-endpoint-protection"></a>Защита от вредоносных программ с помощью Endpoint Protection  
 Endpoint Protection в Configuration Manager позволяет создавать политики защиты от вредоносных программ, содержащие параметры для конфигураций клиента Endpoint Protection. Созданные политики защиты от вредоносных программ можно развертывать на клиентских компьютерах и отслеживать их применение в узле **Состояние Endpoint Protection** раздела **Безопасность** рабочей области **Мониторинг** (или через отчеты Configuration Manager).  

 Дополнительные сведения:  

-   [Создание и развертывание политик защиты от вредоносных программ для Endpoint Protection в System Center Configuration Manager](endpoint-antimalware-policies.md) — сведения о создании, развертывании и мониторинге политик защиты от вредоносных программ со списком параметров, которые можно настраивать.  

-   [Мониторинг Endpoint Protection в System Center Configuration Manager](monitor-endpoint-protection.md) — отчеты о действиях мониторинга, сведения о зараженных клиентских компьютерах и другие возможности.  

-   [Управление политиками защиты от вредоносных программ и параметрами брандмауэра для Endpoint Protection в System Center Configuration Manager](endpoint-antimalware-firewall.md) — сведения об устранении вредоносных программ, найденных на клиентских компьютерах.  


## <a name="managing-windows-firewall-with-endpoint-protection"></a>Управление брандмауэром Windows с помощью Endpoint Protection  
 Endpoint Protection в Configuration Manager позволяет управлять основными параметрами брандмауэра Windows на клиентских компьютерах. Для каждого сетевого профиля можно настроить следующие параметры:  

-   включение и отключение брандмауэра Windows;  

-   блокирование входящих подключений, включая указанные в списке разрешенных программ;  

-   уведомление пользователя о блокировании брандмауэром Windows новой программы.  

> [!NOTE]  
>  Endpoint Protection поддерживает управление только брандмауэром Windows.  


 Дополнительные сведения о создании и развертывании политик брандмауэра Windows для Endpoint Protection см. в разделе [Создание и развертывание политик брандмауэра Windows для Endpoint Protection в System Center Configuration Manager](create-windows-firewall-policies.md).  


## <a name="windows-defender-advanced-threat-protection"></a>Advanced Threat Protection в Защитнике Windows

Начиная с Configuration Manager версии 1606 (Current Branch) Endpoint Protection помогает отслеживать службу Advanced Threat Protection (ATP) в Защитнике Windows и управлять ею. ATP в Защитнике Windows представляет собой новую службу, с помощью которой предприятия могут обнаруживать, исследовать атаки повышенной сложности и реагировать на них в своих сетях. См. раздел [Advanced Threat Protection в Защитнике Windows](windows-defender-advanced-threat-protection.md).

## <a name="endpoint-protection-workflow"></a>Рабочий процесс Endpoint Protection  
 Приведенная ниже схема поможет вам понять рабочий процесс для внедрения Endpoint Protection в вашей иерархии Configuration Manager.  

 ![Рабочий процесс Endpoint Protection](../media/Endpoint-Protection-Workflow.gif)  

## <a name="endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Клиент Endpoint Protection для компьютеров Mac и серверов Linux  
 System Center Endpoint Protection включает в себя клиент Endpoint Protection для компьютеров Linux и Mac. Эти клиенты не поставляются с Configuration Manager; вместо этого необходимо скачать следующие продукты с сайта [Microsoft Volume Licensing Service Center](https://www.microsoft.com/licensing/servicecenter/default.aspx).  

-   System Center 2012 Endpoint Protection для Mac  

-   System Center 2012 Endpoint Protection для Linux  


> [!IMPORTANT]  
>  Для загрузки файлов установки Endpoint Protection для Linux и Mac вы должны быть клиентом корпоративного лицензирования Майкрософт.  

 Этими продуктами нельзя управлять из консоли Configuration Manager. Тем не менее пакет управления System Center Operations Manager поставляется с файлами установки, что позволяет управлять клиентом для Linux с помощью Operations Manager.  

### <a name="how-to-get-the-endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Как получить клиент Endpoint Protection для компьютеров Mac и серверов Linux

Используйте следующие действия, чтобы скачать файл образа, содержащий клиентское программное обеспечение Endpoint Protection и документацию для компьютеров Mac и серверов Linux.
1. Войдите на веб-сайт [Microsoft Volume Licensing Service Center](https://www.microsoft.com/licensing/servicecenter/default.aspx).
2. В верхней части веб-сайта перейдите на вкладку **Downloads and Keys** (Загрузки и ключи).
3. Используйте фильтр по продукту **System Center Endpoint Protection (текущая ветвь)**.
4. Щелкните ссылку **Download** (Скачать).
5. Нажмите кнопку **Continue**(Продолжить). Вы увидите несколько файлов, включая один с именем **System Center Endpoint Protection (current branch - version 1606) for Linux OS and Macintosh OS Multilanguage   32/64 bit   1507 MB ISO**.
6. Щелкните значок стрелки, чтобы скачать файл. Имя файла — **SW_DVD5_Sys_Ctr_Endpnt_Prtctn_1606_MultiLang_EptProt_Lin_Mac_MLF_X21 30777. ISO**.

 Дополнительные сведения о том, как устанавливать и управлять клиентами Endpoint Protection для компьютеров Linux и Mac, см. в документации, поставляемой с этими продуктами, которая находится в папке **Документация** .
