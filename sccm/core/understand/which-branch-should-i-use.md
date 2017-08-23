---
title: "Какую ветвь следует использовать | Документация Майкрософт"
description: "В этой статье описаны различия между доступными ветвями System Center Configuration Manager."
ms.custom: na
ms.date: 05/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a3be4f8f-3d44-4e3c-9fa1-e85f30a36e72
caps.latest.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 26356a80bd8c78d4517253bae73e53d8d8f3a73a
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="which-branch-of-configuration-manager-should-i-use"></a>Какую ветвь Configuration Manager следует использовать?

*Применяется к: System Center Configuration Manager (Current Branch, Long-Term Servicing Branch, Technical Preview)*


С октября 2016 г. доступны три ветви System Center Configuration Manager. Сведения в этом разделе помогут вам выбрать наиболее подходящую ветвь.

> [!TIP]  
> На всех сайтах в иерархии должна использоваться одна ветвь. Иерархия с различными ветвями на разных сайтах не поддерживается.

## <a name="current-branch-of-system-center-configuration-manager"></a>System Center Configuration Manager (Current Branch)
Это лицензированная ветвь для использования в рабочей среде, для тех клиентов, которым требуется возможность получать доступ к новейшим компонентам и функциям. Эту ветвь следует использовать при наличии одного из следующих выпусков: System Center Datacenter, System Center Standard, System Center Configuration Manager или эквивалентных прав по подписке. Дополнительные сведения о вариантах лицензирования и программе Software Assurance см. в статье [Лицензирование и ветви в System Center Configuration Manager](learn-more-editions.md).


>  [!TIP]
> Ветвь Current Branch можно установить как ознакомительный выпуск, не требующий лицензии. Ознакомительную версию можно использовать в течение 180 дней; она поддерживает обновление до лицензионной версии Current Branch.

Ветвь Current Branch обновляется несколько раз в год с добавлением новых функций и компонентов. Каждая версия обновления поддерживается в течение одного года после ее выпуска. Вам потребуется обновить ветвь Current Branch до новой версии до истечения срока действия этого периода или на момент его истечения. Обновления до новых версий доступны как обновления в консоли.

Для установки ветви Current Branch в качестве нового сайта или обновления System Center 2012 Configuration Manager с пакетом обновления 2 (SP2) или System Center 2012 R2 Configuration Manager с пакетом обновления 1 (SP1) используется [базовый носитель](/sccm/core/servers/manage/updates#baseline-and-update-versions) для System Center Configuration Manager, который поставляется как DVD-диск с System Center 2016 или доступен в рамках автономного выпуска System Center Configuration Manager. Доступ к носителю зависит от способа лицензирования System Center Configuration Manager. Более поздние базовые версии, например 1702, не поддерживают установку LTSB.

Базовый носитель также можно использовать для установки нового сайта ознакомительной версии Current Branch. Если вы хотите установить только ознакомительную версию, можно получить программное обеспечение на веб-сайте [Центра оценки TechNet](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection).

>  [!NOTE]
> Базовый носитель используется только для установки сайтов для новой иерархии Configuration Manager. Если вы ранее установили базовую версию, такую как 1511, для обновления сайтов до новой версии, например до 1606, используются обновления в консоли.
>
> При обновлении сайтов с помощью обновлений в консоли создаются сайты, эквивалентные новому сайту, установленному с помощью базового носителя.
>
> Дополнительные сведения см. в статье [Обновления для System Center Configuration Manager](/sccm/core/servers/manage/updates).

**Возможности Current Branch**
- Принимает [обновления в консоли](/sccm/core/servers/manage/install-in-console-updates), предоставляющие доступ к новым функциям.
- Принимает обновления в консоли, обеспечивающие исправления безопасности и качества для существующих компонентов.
- Поддерживает обновление по внештатному каналу при необходимости. См. разделы [Использование инструмента регистрации обновлений](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes) и [Использование установщика исправлений](/sccm/core/servers/manage/use-the-hotfix-installer-to-install-updates).
- Может взаимодействовать с Microsoft Intune и другими облачными службами и инфраструктурой.
- Поддерживает [миграцию данных](/sccm/core/migration/migrate-data-between-hierarchies) в другие установки Configuration Manager и из них.
- Поддерживает обновление с предыдущих версий Configuration Manager.
- Поддерживает установку в качестве ознакомительного выпуска с последующим обновлением до полностью лицензированной версии.

Первоначальным выпуском ветви Current Branch была версия 1511. Последующие обновления включают версии 1602, 1606 и так далее. Каждая версия поддерживается в течение одного года, и специалисты Майкрософт рекомендуют выполнять обновление до последней версии вскоре после ее выпуска. Тем не менее можно работать с текущей версией в течение одного года до обновления до новой версии, а также пропустить обновление для установки самой последней доступной версии. Поскольку каждая версия является накопительной, даже если вы пропустите одно обновление и установите последнюю версию, вы по-прежнему получите доступ ко всем функциям и усовершенствованиям предыдущих версий.

Дополнительные сведения см. в разделе [Поддержка версий Current Branch](/sccm/core/servers/manage/current-branch-versions-supported).

**Варианты обновления**
- При наличии действующего соглашения Software Assurance можно установить обновления в консоли для версий Current Branch.  
- Преобразовать Current Branch в Technical Preview нельзя. Выпуски Technical Preview — это отдельные установки, которые не требуют лицензии.
- Кроме того, нет возможности преобразовать Current Branch в ветвь Long-Term Servicing Branch (LTSB). Необходимо удалить Current Branch, а затем установить LTSB в рамках новой установки.

##  <a name="long-term-servicing-branch-of-system-center-configuration"></a>System Center Configuration Manager (Long-Term Servicing Branch)
Это лицензированная ветвь для использования в рабочей среде Configuration Manager для клиентов, использующих Current Branch, участие в программе Configuration Manager Software Assurance (SA) или аналогичные права по подписке, истекающие после 1 октября 2016 г. Дополнительные сведения о вариантах лицензирования и программе Software Assurance см. в статье [Лицензирование и ветви в System Center Configuration Manager](learn-more-editions.md).

В основе ветви LTSB лежит версия 1606. Эта ветвь не получает обновления в консоли, предоставляющие новые возможности или обновляющие существующие компоненты. Тем не менее важные исправления безопасности предоставляются. Чтобы установить LTSB, необходимо использовать [базовый носитель](/sccm/core/servers/manage/updates#baseline-and-update-versions) с версией 1606, который поставляется на DVD-диске вместе с System Center 2016 или System Center Configuration Manager.

Чтобы установить ветвь LTSB как новый сайт или обновление поддерживаемого сайта Configuration Manager 2012, используйте [базовый носитель](/sccm/core/servers/manage/updates#baseline-and-update-versions) версии 1606, полученный как DVD-диск с выпуском System Center 2016 или System Center Configuration Manager (Current Branch и Long-Term Servicing Branch 1606). Базовый носитель можно использовать для установки нового сайта под управлением версии 1606 ветви Current Branch или нового сайта под управлением ветви Long-Term Servicing Branch.

> [!TIP]  
> Дополнительные сведения о System Center 2016 см. в [документации по System Center 2016](https://technet.microsoft.com/system-center-docs/system-center). Эта документация также определяет способ получения System Center 2016, для чего требуется лицензионное соглашение с Майкрософт или аналогичные права.

> Чтобы найти System Center Configuration Manager версии 1606 в Volume Licensing Service Center (VLSC), перейдите на вкладку **Downloads and Keys** (Файлы для загрузки и ключи) сайта [VLSC](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx), выполните поиск по запросу "system center config", а затем выберите **System Center Config Mgr** (Current Branch и LTSB).

> Ознакомительную версию System Center 2016 также можно скачать в [Центре оценки TechNet](https://www.microsoft.com/evalcenter/evaluate-system-center-technical-preview).

**Возможности LTSB**
-   Принимает обновления в консоли, обеспечивающие важные исправления безопасности.
- Предоставляет возможность установки, если истек срок действия соглашения SA или эквивалентных прав на Configuration Manager.
- Поддерживает обновление (преобразование) в Current Branch после получения действующего соглашения SA или эквивалентных прав на Configuration Manager.

**Ограничения**  
Ветвь LTSB основана на версии Current Branch 1606 и имеет следующие ограничения.
- Ветвь LTSB поддерживается в течение 10 лет после выпуска общедоступной версии (октябрь 2016 г.). В течение этого срока предоставляются важные обновления безопасности, но после 10 лет срок поддержки для этой версии истекает. Дополнительные сведения о жизненном цикле поддержки см. в разделе [Политика жизненного цикла поддержки Майкрософт](https://support.microsoft.com/en-us/lifecycle).
- Поддерживает ограниченный набор серверных и клиентских операционных систем и связанных технологий, таких как версии SQL Server. Дополнительные сведения о том, что поддерживается в этой ветви, см. в разделе [Поддерживаемые конфигурации для LTSB](supported-configurations-for-ltsb.md).
- Не принимает обновления, предоставляющие новые функции.
- Не поддерживает добавление подписки Microsoft Intune, что не позволяет использовать:
  - Intune в гибридной конфигурации MDM;
 - локальное управление мобильными устройствами (MDM).
-   Не поддерживает использование панели мониторинга обслуживания Windows 10, планов обслуживания и ветвей Windows 10 Current Branch (CB) и Current Branch for Business (CBB).
- Не поддерживает будущие выпуски Windows 10 LTSB и Windows Server.
-   Не поддерживает аналитику активов.
-   Не поддерживает облачные точки распространения.
-   Не поддерживает использование Exchange Online как соединителя Exchange.
-   Не поддерживает функции предварительного выпуска.



**Варианты обновления**
- Установку LTSB можно преобразовать в установку Current Branch. Преобразование в ветвь Current Branch поддерживается до или после истечения срока действия поддержки для LTSB.

  Для преобразования необходимо действующее соглашение Software Assurance с Майкрософт. Дополнительные сведения см. в следующих разделах.
  - [Обновление Long-Term Servicing Branch до Current Branch](convert-to-current-branch.md)
  - [Лицензирование и ветви в System Center Configuration Manager](learn-more-editions.md)
  - Раздел [Базовые и обновленные версии](/sccm/core/servers/manage/updates#baseline-and-update-versions) статьи [Обновления для Configuration Manager](/sccm/core/servers/manage/updates)
- Преобразовать LTSB в Technical Preview нельзя. Выпуски Technical Preview — это отдельные установки, которые не требуют лицензии.
-   Ознакомительную версию Current Branch нельзя обновить до установки LTSB.


## <a name="technical-preview-for-system-center-configuration-manager"></a>Technical Preview для System Center Configuration Manager
Ветвь Technical Preview предназначена для использования в лабораторной среде, где предполагается изучать и апробировать новейшие возможности, разрабатываемые для Configuration Manager. Technical Preview не поддерживается в рабочей среде и не требует наличия лицензионного соглашения Software Assurance.

Чтобы установить новый сайт под управлением Technical Preview, используйте последнюю версию [базового носителя для System Center Configuration Manager Technical Preview](/sccm/core/get-started/technical-preview#install-and-update-the-technical-preview). После установки Technical Preview новые версии доступны как ежемесячные обновления в консоли.

**Возможности Technical Preview**
-  Ветвь основана на последних базовых версиях Current Branch.
-  Принимает обновления в консоли для обновления до последней версии Technical Preview.
-  Включает новые разрабатываемые компоненты, по которым требуется получить ваши отзывы.
-  Принимает обновления, которые применяются только к ветви Technical Preview.

**Ограничения**
-  [Поддержка ограничена](/sccm/core/get-started/technical-preview#requirements-and-limitatins-for-the-techincal-preview), включая только один первичный сайт и до 10 клиентов.  
-  Нельзя обновить до Current Branch или LTSB.
-  Не поддерживает использование миграции для импорта или экспорта данных в другую установку Configuration Manager.
-  Не поддерживает обновление с предыдущих версий Configuration Manager.
-  Не поддерживает установку в качестве ознакомительного выпуска.

Функции, которые впервые были представлены в Technical Preview, часто добавляются в Current Branch при последующем обновлении. Каждая новая версия Technical Preview включает функции из предыдущих выпусков Technical Preview даже после того, как эти функции были добавлены в выпуск Current Branch.

Дополнительные сведения см. в разделе [Technical Preview для System Center Configuration Manager](/sccm/core/get-started/technical-preview).

**Варианты обновления**
-   Можно установить любые обновления в консоли для новой версии Technical Preview.
-   Преобразовать Technical Preview в Current Branch или LTSB нельзя.


## <a name="identify-your-branch-and-version"></a>Определение ветви и версии
При просмотре сведений о версии для сайта Configuration Manager также необходимо проверить сведения о ветви.

**Версия**   
Чтобы проверить версию сайта, в левом верхнем углу консоли перейдите к элементу **О System Center Configuration Manager**, где должна отображаться **версия сайта**. Список версий сайта см. в статье []().

**Ветвь**  
Чтобы узнать ветвь сайта (LTSB или Current Branch), в консоли перейдите в раздел **Администрирование** > **Конфигурация сайта** > **Сайты** и откройте **Параметры иерархии**. Если имеется возможность преобразования в Current Branch и она активна, на сайте выполняется версия LTSB. Если на сайте выполняется Current Branch, эта возможность неактивна.
Сведения о различных версиях Configuration Manager см. в разделе "Базовые и обновленные версии" статьи [Обновления для System Center Configuration Manager](/sccm/core/servers/manage/updates).
