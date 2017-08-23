---
title: "Общие сведения о ветви Long-Term Servicing Branch | Документы Майкрософт"
description: "Основные сведения о ветви System Center Configuration Manager (Long-Term Servicing Branch)."
ms.custom: na
ms.date: 05/01/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 694bc29f-a7fd-4e06-815a-1a9c5e9ac563
caps.latest.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 91c1ca860069c6ebe0d20230c4620bf3f68735a2
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="introduction-to-the-long-term-servicing-branch-of-system-center-configuration-manager"></a>Общие сведения о версии System Center Configuration Manager (Long-Term Servicing Branch)

*Применимо к: System Center Configuration Manager (Long-Term Servicing Branch)*

System Center Configuration Manager (Long-Term Servicing Branch) является отдельной ветвью Configuration Manager, которая разработана в качестве параметра установки, доступного для всех клиентов. Однако этот параметр предназначен только для клиентов, у которых истек срок действия соглашения Software Assurance или аналогичных прав по подписке Configuration Manager.


С учетом Configuration Manager версии 1606 возможности LTSB ограничены по сравнению с Configuration Manager (Current Branch).

 > [!TIP]   
 > Дополнительные сведения о ветвях **Windows Server** см. в статье [Windows Server 2016 new Current Branch for Business servicing option]( https://blogs.technet.microsoft.com/windowsserver/2016/07/12/windows-server-2016-new-current-branch-for-business-servicing-option/) (Новая ветвь обслуживания Current Branch for Business для Windows Server 2016).

## <a name="features-that-are-not-available-in-the-ltsb-of-configuration-manager"></a>Функции, которые недоступны в Configuration Manager (LTSB).
Configuration Manager (Current Branch) поддерживает следующие возможности, недоступные в LTSB:

-   Обновления в консоли, добавляющие новые функции и улучшения.
-   Поддержка недавно выпущенных операционных систем, которые будут использоваться в качестве серверов сайта и клиентов.
-   Использование подписки Microsoft Intune для поддержки:
    -   Intune в конфигурации гибридного управления мобильными устройствами (MDM);
    -   локальное управление мобильными устройствами (MDM).
-   Панель мониторинга обслуживания и планы обслуживания Windows 10, включая поддержку ранних версий Windows 10 Current Branch (CB) и Current Branch for Business (CBB).  
-   Поддержка будущих выпусков Windows Server и Windows 10 LTSB.
-   Аналитика активов
-   Облачные точки распространения
-   Использование Exchange Online как соединителя Exchange.    

Хотя поддержка для этих функций не включена в LTSB, некоторые функции остаются видимыми в консоли Configuration Manager, однако они неактивны.


## <a name="find-documentation-for-the-ltsb"></a>Поиск документации по LTSB
Ветвь LTSB основана на версии Current Branch 1606. Для документации по продукту используйте [документацию по Current Branch](https://docs.microsoft.com/sccm/) с учетом предупреждений и ограничений, относящихся к LTSB. Эти предупреждения и ограничения указаны в следующих статьях:

-     [Общие сведения о версии System Center Configuration Manager (Long-Term Servicing Branch)](introduction-to-the-ltsb.md) (эта статья);
-     [Установка и обновление с помощью базового носителя версии 1606 для System Center Configuration Manager](install-the-ltsb.md);
-     [Обновление Long-Term Servicing Branch до Current Branch](convert-to-current-branch.md);
-     [Поддерживаемые конфигурации для Long-Term Servicing Branch](supported-configurations-for-ltsb.md)
-   [Управление Long-Term Servicing Branch в Configuration Manager](manage-the-ltsb.md).

Ссылаясь на документацию по Current Branch для LTSB, сведения о версии 1606 также применяются к LTSB. Функции или сведения, внесенные в версию 1610 или более позднюю, не поддерживаются LTSB.


## <a name="licensing-overview-for-the-ltsb"></a>Общие сведения о лицензировании LTSB   
Клиенты с действующим соглашением Software Assurance (SA) для лицензий System Center Configuration Manager или с эквивалентными правами по подписке с 1 октября 2016 г. имеют право на использование выпуска System Center Configuration Manager версии 1606 за октябрь 2016 г. Клиенты с правами на System Center Configuration Manager, действительными на 1 октября 2016 г. или после этой даты, могут выбрать один из двух вариантов лицензирования после установки: Current Branch и Long-Term Servicing Branch (LTSB).

Клиенты, имеющие бессрочные права на System Center Configuration Manager или срок действия SA или подписки которых истекает после 1 октября, могут установить версию System Center Configuration Manager LTSB, которая является текущей на момент истечения срока действия соглашения.

[Полные условия в отношении продуктов, приобретаемых в рамках программ корпоративного лицензирования Майкрософт, можно найти здесь](http://go.microsoft.com/fwlink/?LinkId=800052).

Дополнительные сведения о лицензировании ветвей Configuration Manager см. в статье [Лицензирование и ветви в System Center Configuration Manager](learn-more-editions.md).

## <a name="next-steps"></a>Дальнейшие шаги

Если вы решили, что Configuration Manager LTSB — это нужная ветвь для вашей среды, [установите новый сайт LTSB](/sccm/core/understand/install-the-ltsb#install-a-new-site) как часть новой иерархи или [обновите сайт System Center 2012 Configuration Manager](/sccm/core/understand/install-the-ltsb#upgrade-from-system-center-2012-configuration-manager) и иерархию.

Если у вас нет установочного носителя, ознакомьтесь с [документацией по System Center 2016](https://technet.microsoft.com/system-center-docs/system-center) для получения сведений о System Center 2016, включая данные о носителях, которые можно использовать для установки LTSB System Center Configuration Manager.  
