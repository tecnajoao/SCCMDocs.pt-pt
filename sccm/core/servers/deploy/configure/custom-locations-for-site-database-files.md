---
title: "Настраиваемые расположения для файлов базы данных | Документы Майкрософт"
description: "Узнайте, как задать настраиваемые расположения для файлов базы данных SQL Server."
ms.custom: na
ms.date: 10/06/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 500a9aa6-68aa-44eb-bf49-350c1314a697
caps.latest.revision: "3"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: cfac2c03c1b71b40c68d8acd5fbd96c5e98caaa9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="custom-locations-for-system-center-configuration-manager-site-database-files"></a>Настраиваемые расположения для файлов базы данных сайта System Center Configuration Manager.

*Применимо к: System Center Configuration Manager (Current Branch)*

 System Center Configuration Manager поддерживает настраиваемые расположения для файлов базы данных SQL Server.  

> [!NOTE]  
>  При использовании кластера SQL Server возможность указания расположений файлов не по умолчанию недоступна.  

 **Во время установки** нового первичного сайта или сайта центра администрирования вы можете:  

-   **Указать нестандартные расположения файлов для базы данных сайта**: программа установки Configuration Manager создает базу данных сайта с использованием этих расположений.  

-   **Задать применение предварительно созданной базы данных SQL Server, которая использует настраиваемые расположения файлов**: программа установки Configuration Manager использует эту заранее созданную базу данных и ее предварительно настроенные расположения для файлов.  

**После установки** вы можете изменить расположение файлов базы данных сайта. Для этого необходимо остановить сайт и изменить расположение файлов в SQL Server.  

-   На сервер сайта Configuration Manager остановите службу **SMS_Executive**.  

-   Следуйте инструкциям по перемещению пользовательской базы данных, приведенным в документации для вашей версии SQL Server. Например, если вы используете SQL Server 2014, см. статью [Перемещение пользовательских баз данных](https://technet.microsoft.com/library/ms345483\(v=sql.120\).aspx) на сайте TechNet.  

-   После перемещения файлов базы данных перезапустите службу **SMS_Executive** на сервере сайта Configuration Manager.  
