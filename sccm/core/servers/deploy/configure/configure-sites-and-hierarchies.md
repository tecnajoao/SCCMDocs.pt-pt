---
title: "Настройка сайтов | Документы Майкрософт"
description: "Просмотр контрольного списка для принятия во внимание стандартных конфигураций, влияющих на сайты и иерархии."
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9efb4061-f642-48bd-8332-3357ff5b3118
caps.latest.revision: "15"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 862f420c063cb44c419d4904fbb4696efb739758
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="configure-sites-and-hierarchies-for-system-center-configuration-manager"></a>Настройка сайтов и иерархий для System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

После установки первого сайта System Center Configuration Manager или добавления дополнительных сайтов в иерархию используйте приведенный ниже контрольный список, чтобы учесть наиболее распространенные конфигурации, затрагивающие как сайты, так и иерархии.  

## <a name="checklist-of-common-configurations-for-new-and-additional-sites"></a>Контрольный список стандартных конфигураций для новых и дополнительных сайтов  
Учитывайте следующие замечания о настройке, которые относятся к большинству развертываний:

-   Некоторые параметры созданы на основе других, например обнаружение в лесах Active Directory, границы и группы границ.  

-   Ряд конфигураций имеет заданные по умолчанию значения, которые временно можно использовать без изменений.  

-   Другие конфигурации, например группы границ и группы точек распространения, перед использованием должны быть настроены.  

|Действие|Подробные сведения|  
|------------|-------------|  
|Настройка ролевого администрирования|Разделите административные назначения, чтобы контролировать то, какие пользователи с правами администратора могут просматривать различные объекты и данные в вашей среде Configuration Manager и управлять ими.<br /><br /> Конфигурации для ролевого администрирования являются общими для всех сайтов в иерархии.   <br/><br/>Дополнительные сведения см. в разделе [Настройка ролевого администрирования для System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-role-based-administration.md).|  
|Публикация данных сайта в доменных службах Active Directory (AD DS)|Упрощает поиск служб для клиентов и обеспечивает эффективное использование ресурсов сайта.<br /><br /> Сначала необходимо [расширить схему Active Directory для System Center Configuration Manager](../../../../core/plan-design/network/extend-the-active-directory-schema.md), а затем настроить каждый сайт для [публикации данных сайта для System Center Configuration Manager](../../../../core/servers/deploy/configure/publish-site-data.md) по отдельности.|  
|Настройка точки подключения службы|Запланируйте установку и настройку точки подключения службы на сайте верхнего уровня иерархии. Дополнительные сведения см. в статье [Сведения о точке подключения службы в System Center Configuration Manager](../../../../core/servers/deploy/configure/about-the-service-connection-point.md).|  
|Добавление ролей системы сайта|Установите одну или несколько дополнительных ролей системы сайта для отдельных сайтов.  Дополнительные сведения см. в разделе [Добавление ролей системы сайта для System Center Configuration Manager](../../../../core/servers/deploy/configure/add-site-system-roles.md).|  
|Настройка границ сайта и групп границ|Укажите границы, которые определяют сетевые расположения в интрасети, содержащие устройства, которыми вы хотите управлять. Затем настройте группы границ таким образом, чтобы клиенты в этих сетевых расположениях могли найти ресурсы Configuration Manager. Дополнительные сведения см. в разделе [Определение границ сайта и групп границ для System Center Configuration Manager](../../../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md).|  
|Настройка групп точек распространения|Настройте логические группы точек распространения, чтобы упростить управление развертываниями. Дополнительные сведения см. в подразделе [Управление группами точек распространения](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage) раздела [Установка и настройка точек распространения для System Center Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md).|  
|Выполнение обнаружения|Запустите обнаружение для поиска ресурсов в сети, включая сетевую инфраструктуру, устройства и пользователей.<br /><br /> Дополнительные сведения см. в разделе [Выполнение обнаружения в System Center Configuration Manager](../../../../core/servers/deploy/configure/run-discovery.md).|  
|Добавление избыточности и емкости для администраторов, которые управляют инфраструктурой|Установите дополнительные поставщики SMS и консоли Configuration Manager, чтобы расширить возможности администраторов по управлению инфраструктурой.<br /><br /> **Установите дополнительные поставщики SMS**, чтобы обеспечить избыточные точки доступа для администрирования сайта и иерархии. Дополнительные сведения см. в подразделе [Управление поставщиком SMS](../../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider) раздела [Изменение инфраструктуры System Center Configuration Manager](../../../../core/servers/manage/modify-your-infrastructure.md).<br /><br /> **Установите дополнительные консоли Configuration Manager**, чтобы предоставить доступ дополнительным пользователям с правами администратора. Дополнительные сведения см. в разделе [Установка консолей Configuration Manager](../../../../core/servers/deploy/install/install-consoles.md).|  
|Настройка компонентов сайта|Настройте компоненты сайта на каждом сайте, чтобы изменить поведение ролей системы сайта и ведение отчетов о состоянии сайта. Дополнительные сведения см. в статье [Компоненты сайта для System Center Configuration Manager](../../../../core/servers/deploy/configure/site-components.md).|  
|Создание настраиваемых коллекций|Используя обнаруженные сведения об устройствах и пользователях, создайте пользовательские коллекции объектов для упрощения задач управления в будущем. Дополнительные сведения см. в разделе [Создание коллекций в System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md).|  
|Настройка параметров для управления развертываниями с высоким риском|Настройте параметры на сайте таким образом, чтобы предупреждать пользователей с правами администратора о том, что они создают развертывание последовательности задач с высоким риском.  Дополнительные сведения см. в разделе [Параметры для управления развертываниями с высоким риском для System Center Configuration Manager](../../../../protect/understand/settings-to-manage-high-risk-deployments.md).|  
|Настройка реплик базы данных для точек управления|Настройте реплику базы данных, чтобы снизить нагрузку на ЦП сервера базы данных сайта, которую создают точки управления при обработке запросов от клиентов. Дополнительные сведения см. в разделе [Реплики базы данных для точек управления для System Center Configuration Manager](../../../../core/servers/deploy/configure/database-replicas-for-management-points.md).|  
|Настройка группы доступности SQL Server AlwaysOn для размещения базы данных сайта|Начиная с версии 1602 в качестве решения для обеспечения высокой доступности и аварийного восстановления можно настроить группы доступности, чтобы размещать базу данных сайта на первичных сайтах и сайте центра администрирования. Дополнительные сведения см. в разделе [SQL Server AlwaysOn для высокодоступной базы данных сайта в System Center Configuration Manager](../../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).|  
|Изменение репликации между сайтами|Сведения по следующим темам см. в статье [Передача данных между сайтами в System Center Configuration Manager](../../../../core/servers/manage/data-transfers-between-sites.md).<br /><br /> Настройка [файловой репликации](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_fileroute) между вторичными сайтами<br /><br /> Настройка [каналов репликации базы данных](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_Dblinks)<br /><br /> Настройка [распределенных представлений](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_distviews)|  
