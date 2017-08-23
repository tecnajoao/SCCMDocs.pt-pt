---
title: "Изменения с момента выпуска Configuration Manager 2012 | Документация Майкрософт "
description: "Узнайте об изменениях и новых возможностях System Center Configuration Manger и System Center 2012 Configuration Manager."
ms.custom: na
ms.date: 05/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3ae68fa6-8b30-45dd-9d12-50bb67cb4a9d
caps.latest.revision: "51"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 0a3eb93a99533a1569d8f72ca01d6dfcdc75da20
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="what39s-changed-in-system-center-configuration-manager-from-system-center-2012-configuration-manager"></a>Изменения в System Center Configuration Manager с момента выпуска версии System Center 2012 Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*


 В текущей ветви System Center Configuration Manager представлены важные изменения по сравнению с System Center 2012 Configuration Manager. В этом разделе указаны наиболее значительные изменения и новые возможности в базовой версии 1511 System Center Configuration Manager. Сведения об изменениях, которые представлены в последующих обновлениях для System Center Configuration Manager, см. в разделе [Новые возможности в добавочных версиях System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions).



 Выпуск System Center Configuration Manager за декабрь 2015 г. (версия 1511) был первым выпуском текущей версии Configuration Manager от Майкрософт. Как правило, он называется текущей ветвью System Center Configuration Manager. *Текущая ветвь* указывает на то, что данная версия поддерживает добавочные обновления для продукта. Она также позволяет различать текущий и предыдущие выпуски Configuration Manager.  

 System Center Configuration Manager:  

-   Не использует год или идентификатор продукта в имени продукта, как это было в прошлых версиях, таких как Configuration Manager 2007 или System Center 2012 Configuration Manager.

-   Поддерживает добавочные обновления в продукте, которые также называются версиями обновления. Первой выпущенной версией была версия 1511. Последующие версии выпускаются несколько раз в год как консольные обновления (например, версия 1610).
-   Устанавливается с использованием базовой версии. Исходной базовой версией была версия 1511, но время от времени выпускаются новые базовые версии, например 1702. Базовые версии могут использоваться для установки нового сайта и иерархии System Center Configuration Manager, а также для обновления с поддерживаемой версии Configuration Manager 2012.




##  <a name="bkmk_updates"></a> Обновления в консоли для Configuration Manager  
 System Center Configuration Manager использует метод обслуживания в консоли под названием **Обновления и обслуживание**, который позволяет легко найти и установить рекомендуемые обновления.  

 Некоторые версии доступны только как обновления для существующих сайтов (в консоли Configuration Manager) и не могут использоваться для установки новых сайтов Configuration Manager.   
Например, обновление 1610 можно установить только в консоли Configuration Manager. Оно используется для обновления сайта, на котором уже установлена версия System Center Configuration Manager.

Периодически выпускаются обновленные версии, которые служат новыми базовыми версиями (например, обновление 1702). Такое обновление может использоваться для установки новой иерархии без необходимости запуска предыдущей базовой версии (например, 1511) и обновления продукта до последней версии.


Дополнительные сведения об использовании обновлений см. в статье [Обновления для System Center Configuration Manager](../../../core/servers/manage/updates.md).  
Дополнительные сведения о базовых версия см. в разделе [Базовые и обновленные версии](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions).

##  <a name="bkmk_servicepoint"></a> Новая роль системы сайта: точка подключения службы  
 **Соединитель Microsoft Intune** заменяется новой ролью системы сайта — **точкой подключения службы**, обладающей дополнительными функциональными возможностями. Точка подключения службы:  

-   заменяет соединитель Microsoft Intune, который используется для интеграции Intune с локальным управлением мобильными устройствами в System Center Configuration Manager;  

-   используется как точка контакта для управляемых устройств;  

-   отправляет данные об использовании для развертывания в облачную службу Майкрософт;  

-   выдает обновления, относящиеся к развертыванию и доступные в консоли Configuration Manager.  

Эта роль системы сайта поддерживает как сетевой, так и автономный режим работы. Дополнительные сведения см. в статье [About the service connection point in System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  

##  <a name="bkmk_usage"></a> Сбор данных об использовании  
 System Center Configuration Manager собирает данные об использовании для ваших сайтов и инфраструктуры. Эта информация компилируется и отправляется в облачную службу корпорации Майкрософт точкой подключения службы. Она является обязательным условием использования Configuration Manager для скачивания обновлений развертывания, относящихся к используемой вами версии Configuration Manager. При настройке точки подключения службы можно задать как уровень сбора данных, так и режим их отправки — автоматический (работа в сети) или ручной (автономная работа).  

 Дополнительные сведения см. в разделе [Уровни и параметры сбора данных об использовании](../../../core/servers/deploy/install/setup-reference.md#bkmk_usage).  

##  <a name="bkmk_AMT"></a> Поддержка технологии Intel AMT  
 Для System Center Configuration Manager была удалена собственная поддержка для компьютеров на базе AMT в консоли Configuration Manager. При использовании [надстройки Intel SCS для Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html) компьютеры на базе AMT остаются полностью управляемыми. Эта надстройка предоставляет доступ к новейшим функциям для управления AMT, а также снимает ограничения, существовавшие до внедрения этих изменений в Configuration Manager.  

При удалении интегрированной технологии AMT для System Center Configuration Manager также удаляется аппаратный контроллер управления. Роль системы сайта точки использования аппаратного контроллера управления больше не используется и недоступна.  

Обратите внимание на то, что это изменение не затрагивает использование аппаратного контроллера управления в System Center 2012 Configuration Manager.

##  <a name="bkmk_out"></a> Нерекомендуемые функции  
 Некоторые возможности, такие как компьютеры с [собственной поддержкой технологии Intel AMT](#bkmk_AMT), удаляются из консоли Configuration Manager. Использование других возможностей, таких как защита доступа к сети, полностью прекращается. Кроме того, некоторые более старые продукты корпорации Майкрософт, такие как Windows Vista, Windows Server 2008 и SQL Server 2008, больше не поддерживаются.  

 Список нерекомендуемых компонентов см. в статье [Удаленные и устаревшие компоненты в System Center Configuration Manager](../../../core/plan-design/changes/removed-and-deprecated-features.md).  

 Дополнительные сведения о поддерживаемых продуктах, операционных системах и конфигурациях см. в статье [Поддерживаемые конфигурации для System Center Configuration Manager](../../../core/plan-design/configs/supported-configurations.md).  

## <a name="client-deployment"></a>Развертывание клиента  
 System Center Configuration Manager предоставляет новую возможность для тестирования новых версий клиента Configuration Manager перед обновлением остальной части сайта. Вы можете настроить подготовительную коллекцию для пилотного развертывания нового клиента. Обеспечив удовлетворительную работу нового клиентского программного обеспечения в подготовительной среде, можно повысить клиент для автоматического обновления остальной части сайта.  

 Дополнительные сведения о тестировании клиентов см. в разделе [Проверка обновления клиента в предварительной коллекции в System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

## <a name="operating-system-deployment"></a>Развертывание операционной системы  

Необходимо учитывать указанные ниже изменения развертывания операционной системы.

-   В мастере создания последовательностей задач доступен новый тип последовательности — **Обновить операционную систему из пакета обновления**. Он создает шаги для обновления компьютеров с Windows 7, Windows 8 или Windows 8.1 до Windows 10. Дополнительные сведения см. в статье [Обновление Windows до последней версии с помощью System Center Configuration Manager](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md).  

-   Теперь одноранговый кэш Windows PE доступен при развертывании операционных систем. Компьютеры, на которых выполняется последовательность задач для развертывания операционной системы, могут использовать одноранговый кэш Windows PE для получения содержимого из локального однорангового узла (источник однорангового кэша) вместо скачивания содержимого из точки распространения. Это позволяет уменьшить объем трафика глобальной сети (WAN) в сценариях с филиалами, где локальные точки распространения отсутствуют. Дополнительные сведения см. в статье [Подготовка однорангового кэша Windows PE для снижения трафика глобальной сети в System Center Configuration Manager](/sccm/osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic).  

-   Теперь вы можете просматривать состояние Windows в качестве службы в среде. Вы также можете создавать планы обслуживания для формирования колец развертываний и проверять, находятся ли компьютеры Windows 10 текущей ветви в актуальном состоянии при выходе новых сборок. Кроме того, можно просматривать оповещения, информирующие о наступлении окончания поддержки сборки Current Branch (CB) или Current Branch for Business (CBB) для клиентов Windows 10. Дополнительные сведения см. в статье [Управление Windows как службой с помощью System Center Configuration Manager](../../../osd/deploy-use/manage-windows-as-a-service.md).  

## <a name="application-management"></a>Управление приложениями  

Необходимо учитывать указанные ниже изменения, касающиеся управления приложениями.

-   System Center Configuration Manager позволяет развертывать приложения универсальной платформы Windows (UWP) для устройств под управлением Windows 10 и более поздней версии. См. статью [Создание приложений Windows с помощью System Center Configuration Manager](../../../apps/get-started/creating-windows-applications.md).  

-   Центр программного обеспечения имеет новый современный вид. Приложения, которые ранее были доступны только в каталоге приложений (приложения, доступные для пользователя), теперь доступны в центре программного обеспечения на вкладке "Приложения". Так эти развертывания становятся более доступными для обнаружения, и пользователи избавляются от необходимости обращаться к каталогу приложений. Кроме того, больше не требуется браузер с включенным Silverlight. См. статью [Планирование и настройка управления приложениями в System Center Configuration Manager](../../../apps/plan-design/plan-for-and-configure-application-management.md).  

-   Новый тип приложения "Установщик Windows через MDM" позволяет создавать и развертывать приложения на основе установщика Windows на зарегистрированных ПК под управлением Windows 10. См. статью [Создание приложений Windows с помощью System Center Configuration Manager](../../../apps/get-started/creating-windows-applications.md).  

-   При создании приложения для собственного приложения iOS вам требуется лишь указать файл установщика (IPA) для приложения. Указывать соответствующий файл списка свойств (PLIST) больше не требуется. См. статью [Создание приложений iOS с помощью System Center Configuration Manager](../../../apps/get-started/creating-ios-applications.md).  

-   В Configuration Manager 2012 для указания ссылки на приложение из Магазина Windows можно было указать непосредственно ссылку или перейти на удаленный компьютер с установленным приложением. В System Center Configuration Manager вы по-прежнему можете ввести непосредственно ссылку, но вместо перехода на компьютер-образец теперь можно выполнить поиск приложения в магазине прямо из консоли Configuration Manager.  

## <a name="software-updates"></a>Обновления программного обеспечения  

Необходимо учитывать указанные ниже изменения, касающиеся обновлений программного обеспечения.

-   Система System Center Configuration Manager теперь может различать методы управления обновлениями программного обеспечения для компьютеров. В частности, она может отличить компьютер с Windows 10, который подключается к Центру обновления Windows для бизнеса (WUfB) для управления обновлениями программного обеспечения, от компьютера, подключенного с той же целью к службам WSUS. Новый атрибут **UseWUServer** указывает, управляется ли компьютер с помощью WUfB. Этот параметр можно использовать в коллекции для удаления компьютеров из управления обновлениями программного обеспечения. Дополнительные сведения см. в разделе [Integration with Windows Update for Business in Windows 10](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md).  

-   Теперь можно планировать и запускать задание очистки WSUS из консоли Configuration Manager. При выборе задания очистки WSUS для запуска в свойствах **компонента точки обновления программного обеспечения** оно будет выполнено при следующей синхронизации обновлений программного обеспечения. Просроченным обновлениям присваивается состояние "Отклонено" на сервере WSUS, и агент обновления Windows на компьютерах больше не будет проверять эти обновления. Дополнительные сведения см. в статье [Планирование и запуск задачи очистки WSUS](../../../sum/deploy-use/software-updates-maintenance.md).  

## <a name="compliance-settings"></a>Параметры соответствия  

Необходимо учитывать указанные ниже изменения, касающиеся параметров соответствия требованиям.

-   В System Center Configuration Manager улучшен рабочий процесс создания элементов конфигурации. Теперь, когда вы создаете элемент конфигурации и выбираете поддерживаемые платформы, отображаются только параметры, относящиеся к соответствующей платформе. См. статью [Приступая к работе с параметрами соответствия в System Center Configuration Manager](../../../compliance/get-started/get-started-with-compliance-settings.md).  

-   Мастер **создания элементов конфигурации** упрощает выбор создаваемого типа элемента конфигурации. Кроме того, новые и обновленные элементы конфигурации доступны для:  

    -   устройств Windows 10, управляемых с помощью клиента Configuration Manager;  

    -   устройств Mac OS X, управляемых с помощью клиента Configuration Manager;  

    -   настольных систем и серверов Windows, управляемых с помощью клиента Configuration Manager;  

    -   устройств Windows 8.1 и Windows 10, управляемых без использования клиента Configuration Manager;  

    -   устройств Windows Phone, управляемых без использования клиента Configuration Manager;  

    -   устройств iOS и Mac OS X, управляемых без использования клиента Configuration Manager;  

    -   устройств Android и Samsung KNOX Standard, управляемых без использования клиента Configuration Manager.  

 См. статью [Создание элементов конфигурации в System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-items.md).  

-   Поддержка параметров управления на компьютерах Mac OS X, которые зарегистрированы в Microsoft Intune или управляются с помощью клиента Configuration Manager. См. статью [Создание элементов конфигурации для устройств iOS и Mac OS X, управляемых без использования клиента System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client.md).  

## <a name="protect-data-and-site-infrastructure"></a>Защита данных и инфраструктуры сайтов  
System Center Configuration Manager можно интегрировать с Windows Hello для бизнеса (прежнее название — Microsoft Passport для Windows). Windows Hello для бизнеса — это альтернативный метод входа, использующий Active Directory или учетную запись Azure Active Directory для замены пароля, смарт-карты или виртуальной смарт-карты на устройствах с ОС Windows 10. См. статью [Параметры Windows Hello для бизнеса в System Center Configuration Manager](../../../protect/deploy-use/windows-hello-for-business-settings.md).

## <a name="mobile-device-management-with-microsoft-intune"></a>Управление устройствами Windows с помощью Microsoft Intune  
 System Center Configuration Manager содержит улучшения для управления мобильными устройствами, включая следующее:  

-   ограничение числа устройств, которые может зарегистрировать пользователь;  

-   указание условий, которые должны принять пользователи корпоративного портала перед регистрацией или использованием приложения;  

-   добавление роли диспетчера регистрации устройств для управления большим количеством устройств.  

Дополнительные сведения о возможностях управления мобильными устройствами с помощью Configuration Manager и Intune см. в статье [Гибридное управление мобильными устройствами (MDM) с помощью System Center Configuration Manager и Microsoft Intune](../../../mdm/understand/hybrid-mobile-device-management.md).  

## <a name="on-premises-mobile-device-management"></a>Локальное управление мобильными устройствами  
 Теперь вы можете управлять мобильными устройствами с помощью локальной инфраструктуры Configuration Manager. Все операции управления устройствами и данные управления обрабатываются локально и не являются частью Microsoft Intune или других облачных служб. Этот тип управления устройствами не требует клиентского программного обеспечения. Configuration Manager управляет устройствами с помощью возможностей, встроенных в операционные системы устройств.  

 Дополнительные сведения см. в статье [Управление мобильными устройствами с помощью локальной инфраструктуры в System Center Configuration Manager](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).
