---
title: "Планирование Endpoint Protection | Документы Майкрософт"
ms.custom: na
ms.date: 03/07/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 7610bbd3-a67f-4a09-8115-e35d40d43b42
caps.latest.revision: "16"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 6c4273dae99ec8db2cf827f463b973e876d0d35b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="planning-for-endpoint-protection-in-system-center-configuration-manager"></a>Планирование для Endpoint Protection в System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*


Endpoint Protection в System Center Configuration Manager позволяет управлять политиками защиты от вредоносных программ и параметрами безопасности брандмауэра Windows для клиентских компьютеров в иерархии Configuration Manager.  

> [!IMPORTANT]  
>  Чтобы использовать Endpoint Protection для управления клиентами в иерархии Configuration Manager, необходима лицензия.  

Совместное использование Endpoint Protection и Configuration Manager обеспечивает следующие преимущества:  

-   Настройка политик защиты от вредоносных программ, параметров брандмауэра Windows и управление Advanced Threat Protection в Защитнике Windows для выбранных групп компьютеров.  

-   Использование обновлений программного обеспечения Configuration Manager для загрузки актуальных файлов определений вредоносных программ на клиентские компьютеры.  

-   Отправка уведомлений по электронной почте, использование средств мониторинга в консоли и просмотр отчетов, чтобы информировать пользователей с правами администратора об обнаружении вредоносных программ на клиентских компьютерах  

Компьютеры с Windows 10 не требуют дополнительного клиента для управления Endpoint Protection. На компьютерах с Windows 8.1 и более ранними версиями Endpoint Protection устанавливает собственный клиент в дополнение к клиенту Configuration Manager. Возможности клиента Endpoint Protection:  

-   обнаружение и исправление вредоносных программ и шпионского программного обеспечения;  

-   обнаружение и исправление пакетов программ rootkit;  

-   оценка критических уязвимостей и автоматическое обновление определений и антивирусного модуля;  

-   обнаружение уязвимости сети с помощью системы проверки сети;  

-   интеграция со службой Cloud Protection Service для передачи сведений о вредоносных программах в Майкрософт. При подключении этой службы клиент Endpoint Protection или Защитник Windows, обнаружив на компьютере неопознанную вредоносную программу, может скачивать новейшие определения из Центра по защите от вредоносных программ.  

> [!NOTE]  
>  Клиент Endpoint Protection можно установить на сервере под управлением Hyper-V и на гостевых виртуальных машинах с поддерживаемыми операционными системами. Во избежание чрезмерного использования ресурсов ЦП действия Endpoint Protection имеют встроенную случайную задержку, чтобы службы не запускались одновременно.  

  Кроме того, Endpoint Protection в Configuration Manager позволяет управлять параметрами брандмауэра Windows в консоли Configuration Manager.  

 В разделе [Пример сценария: использование System Center Endpoint Protection для защиты компьютеров от вредоносных программ в System Center Configuration Manager](../deploy-use/scenarios-endpoint-protection.md) показано, как можно настроить Endpoint Protection и брандмауэр Windows, а также управлять ими.  

## <a name="managing-malware-with-endpoint-protection"></a>Защита от вредоносных программ с помощью Endpoint Protection  

Endpoint Protection в Configuration Manager позволяет создавать политики защиты от вредоносных программ, содержащие параметры для конфигураций клиента Endpoint Protection. Созданные политики защиты от вредоносных программ можно развертывать на клиентских компьютерах и отслеживать их применение в узле **Состояние Endpoint Protection** рабочей области **Наблюдение** (или с помощью отчетов Configuration Manager).  

 Дополнительные сведения:  

-   [Создание и развертывание политик защиты от вредоносных программ для Endpoint Protection в System Center Configuration Manager](../deploy-use/endpoint-antimalware-policies.md) — сведения о создании, развертывании и мониторинге политик защиты от вредоносных программ со списком параметров, которые можно настраивать.  

-   [Мониторинг Endpoint Protection в System Center Configuration Manager](../deploy-use/monitor-endpoint-protection.md) — отчеты о действиях мониторинга, сведения о зараженных клиентских компьютерах и другие возможности.   

-   [Управление политиками защиты от вредоносных программ и параметрами брандмауэра для Endpoint Protection в System Center Configuration Manager](../deploy-use/endpoint-antimalware-firewall.md) — сведения об изменении приоритета политики для задач [защиты от вредоносных программ](../deploy-use/endpoint-antimalware-firewall.md#manage-antimalware-policies), [брандмауэра](../deploy-use/endpoint-antimalware-firewall.md#manage-windows-firewall-policies), [устранения вредоносных программ, найденных на клиентских компьютерах](../deploy-use/endpoint-antimalware-firewall.md#remediate-detected-malware), и других задач.

## <a name="managing-windows-firewall-with-endpoint-protection"></a>Управление брандмауэром Windows с помощью Endpoint Protection  
 Endpoint Protection в Configuration Manager позволяет управлять основными параметрами брандмауэра Windows на клиентских компьютерах. Для каждого сетевого профиля можно настроить следующие параметры:  

-   включение и отключение брандмауэра Windows;  

-   блокирование входящих подключений, включая указанные в списке разрешенных программ;  

-   уведомление пользователя о блокировании брандмауэром Windows новой программы.  

> [!NOTE]  
>  Endpoint Protection поддерживает управление только брандмауэром Windows.  

  Дополнительные сведения о создании и развертывании политик брандмауэра Windows для Endpoint Protection см. в разделе [Создание и развертывание политик брандмауэра Windows для Endpoint Protection в System Center Configuration Manager](../deploy-use/create-windows-firewall-policies.md).  

## <a name="windows-defender-advanced-threat-protection"></a>Advanced Threat Protection в Защитнике Windows

Начиная с Configuration Manager версии 1606 (Current Branch) Endpoint Protection помогает отслеживать службу Advanced Threat Protection (ATP) в Защитнике Windows и управлять ею. ATP в Защитнике Windows представляет собой новую службу, с помощью которой предприятия могут обнаруживать, исследовать атаки повышенной сложности и реагировать на них в своих сетях. См. раздел [Advanced Threat Protection в Защитнике Windows](../deploy-use/windows-defender-advanced-threat-protection.md).

## <a name="endpoint-protection-workflow"></a>Рабочий процесс Endpoint Protection  
 Приведенная ниже схема поможет вам понять рабочий процесс для внедрения Endpoint Protection в вашей иерархии Configuration Manager.  

 ![Рабочий процесс Endpoint Protection](../media/Endpoint-Protection-Workflow.gif)

## <a name="endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Клиент Endpoint Protection для компьютеров Mac и серверов Linux  
 System Center включает в себя клиент Endpoint Protection для Linux и компьютеров Mac. Эти клиенты не поставляются с Configuration Manager; вместо этого необходимо скачать следующие продукты с сайта [Microsoft Volume Licensing Service Center](https://www.microsoft.com/licensing/servicecenter/default.aspx).  

> [!IMPORTANT]  
>  Для загрузки файлов установки Endpoint Protection для Linux и Mac вы должны быть клиентом корпоративного лицензирования Майкрософт.  

 Этими продуктами нельзя управлять из консоли Configuration Manager. Тем не менее пакет управления System Center Operations Manager поставляется с файлами установки, что позволяет управлять клиентом для Linux с помощью Operations Manager.  

 Дополнительные сведения о том, как устанавливать и управлять клиентами Endpoint Protection для компьютеров Linux и Mac, см. в документации, поставляемой с этими продуктами, которая находится в папке **Документация** .

## <a name="best-practices-for-endpoint-protection-in-configuration-manager"></a>Рекомендации по использованию Endpoint Protection in Configuration Manager  
 Следуйте данным рекомендациям, связанным с компонентом Endpoint Protection в System Center 2012 Configuration Manager.  

### <a name="configure-custom-client-settings-for-endpoint-protection"></a>Задание значений настраиваемых параметров клиентов для Endpoint Protection.  
 При настройке параметров клиента для Endpoint Protection не следует использовать параметры по умолчанию, так как они будут применены ко всем компьютерам в иерархии. Вместо этого необходимо указать настраиваемые параметры клиента и назначить их коллекциям компьютеров в иерархии.  

 Настройка собственных параметров клиента позволяет решать следующие задачи:  

-   настраивать параметры безопасности и защиты от вредоносных программ для разных групп компьютеров организации;  
-   тестировать влияние использования Endpoint Protection в небольших группах компьютеров перед развертыванием для всей иерархии;  
-   со временем добавлять другие клиенты в коллекцию для поэтапного развертывания клиента Endpoint Protection.  

### <a name="distributing-definition-updates-by-using-software-updates"></a>Распространения обновлений определений с помощью обновления программного обеспечения  
 Если вы используете обновления программного обеспечения Configuration Manager для распространения обновлений определений, рассмотрите возможность размещения обновлений определений в пакете, который не содержит других обновлений ПО. Это означает, что размер пакета для обновления определения меньше позволит реплицировать на точки распространения быстрее.
