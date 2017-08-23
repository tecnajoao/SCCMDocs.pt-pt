---
title: "Оценка Configuration Manager | Документы Майкрософт"
description: "Создайте лабораторную среду для оценки использования System Center Configuration Manager в вашей организации."
ms.custom: na
ms.date: 2/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 01b30260-f03a-4851-a549-d1b76e8cfc69
caps.latest.revision: "25"
caps.handback.revision: "0"
author: brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: d7ea785ab1beee09b9adda735a87f89bc9481620
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="evaluate-system-center-configuration-manager-by-building-your-own-lab-environment"></a>Оценка System Center Configuration Manager путем создания собственной лабораторной среды

*Применимо к: System Center Configuration Manager (Current Branch)*

 Узнайте, как создать лабораторную среду для оценки использования System Center Configuration Manager в вашей организации.  

 System Center Configuration Manager — это сложное и эффективное средство для управления пользователями, устройствами и программным обеспечением. Рекомендуется провести тщательную оценку System Center Configuration Manager до полного развертывания, чтобы закрепить полученные знания практическими упражнениями.  

 Это руководство предназначено в первую очередь для администраторов, оценивающих использование Configuration Manager в корпоративных средах.  

-   Администраторы, ищущие решение для полноценного управления компьютерами, серверами и мобильными устройствами.  

-   Администраторы из отраслей с повышенным уровнем безопасности, которым требуется защита, характерная для локального управления устройствами, и гибкость, характерная для управления устройствами в облаке.  

-   Администраторы, которые хотят управлять масштабированием своей локальной серверной архитектуры.  

## <a name="what-this-lab-does"></a>Что входит в эту лабораторную работу  
 Основная цель создания этой среды — получение общих знаний, достаточных для начала работы с Configuration Manager, а также более глубокое изучение Configuration Manager во время работы. Вы выполняете ускоренную сборку текущей версии Configuration Manager с использованием двух серверов.  

-   На одном размещается Active Directory, контроллер домена и DNS-сервер.  

-   На втором размещается Configuration Manager и все связанные компоненты SQL Server.  

Клиентские компьютеры устанавливаются в Hyper-V. Саму лабораторную работу также можно запустить в виде полностью виртуализированной системы на одном сервере.  

## <a name="what-this-lab-does-not-do"></a>Что выходит за рамки этой лабораторной работы  
 Эта лабораторная работа не охватывает все сценарии Configuration Manager. Она не предназначена для немедленной миграции в активную среду.  

 При выполнении этой лабораторной работы вы получите функционирующую среду. Но эта среда не оптимизирована для таких факторов, как производительность системы, управление местом на жестком диске, хранилище SQL Server и т. п.  

##  <a name="BKMK_EvalRec"></a> Материалы, с которыми рекомендуется ознакомиться до создания лабораторной среды  
 [Документация по System Center Configuration Manager](http://docs.microsoft.com/sccm/) содержит множество различных материалов. Ниже приведена подборка статей из этой библиотеки, которые рекомендуется изучить всем администраторам перед началом выполнения упражнений лабораторной работы.  

-   Основные понятия о консоли Configuration Manager, порталах пользователей и примерах сценариев см. в разделе [Общие сведения о System Center Configuration Manager](../../core/understand/introduction.md).  

-   Описание основных возможностей управления Configuration Manager см. в разделе [Функции и возможности в System Center Configuration Manager](../../core/plan-design/changes/features-and-capabilities.md).  

-   Более подробные сведения см. в разделе [Основные сведения о Microsoft System Center Configuration Manager](../../core/understand/fundamentals.md).  

-   Сведения о важности ролей безопасности см. в разделе [Основы ролевого администрирования для System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

-   Определенные понятия, относящиеся к управлению содержимым, см. в статье [Концепции управления содержимым](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

-   [Пояснения о том, как клиенты находят ресурсы и службы сайта для System Center Configuration Manager](../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md), помогут обеспечить поддержку ежедневных операций в развертывании.  
