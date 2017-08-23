---
title: "Команды и службы компонентов клиента UNIX и Linux | Документы Майкрософт"
description: "Узнайте о службах компонентов и командах для клиентов Linux и UNIX в System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e5a8c79f-5791-49c5-8055-086d742e5559
caps.latest.revision: "6"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 89668f3e2e0a3e2e0178e5b2c91b2508f583649f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="linux-and-unix-clients-component-services-and-commands-for-system-center-configuration-manager"></a>Команды и службы компонентов клиента UNIX и Linux в System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*


 В следующей таблице приведены службы компонентов клиента Configuration Manager для Linux и UNIX.  

|Имя файла|Дополнительные сведения|  
|---------------|----------------------|  
|ccmexec.bin|Эта служба эквивалентна службе ccmexc на клиентском компьютере под управлением Windows. Он отвечает за все связи с ролями системы сайта Configuration Manager, а также взаимодействует со службой omiserver.bin для сбора данных инвентаризации оборудования с локального компьютера.<br /><br /> Чтобы получить список поддерживаемых аргументов командной строки, выполните **ccmexec -h**.|  
|omiserver.bin|Эта служба является CIM-сервером. CIM-сервер предоставляет платформу для подключаемых программных модулей, которые называются поставщиками. Поставщики взаимодействуют с ресурсами компьютеров Linux и UNIX и собирают данные инвентаризации оборудования. Например **процесс поставщика** для Linux компьютер собирает данные, связанные с процессами операционной системы Linux.|  

 Следующие команды список таблиц, которые можно использовать для запуска, остановить или перезапустить службы клиента (ccmexec.bin и omiserver.bin) на каждой версии Linux или UNIX. При запуске или остановке службы ccmexec также происходит запуск или остановка службы omiserver.  

|Операционная система|Команды|  
|----------------------|--------------|  
|Universal Agent<br /><br /> RHEL 4 и SLES 9|Запуск: **/etc/init d/ccmexecd start**<br /><br /> Остановка: **/etc/init d/ccmexecd stop**<br /><br /> Перезапуск: **/etc/init d/ccmexecd restart**|  
|Solaris 9|Запуск: **/etc/init d/ccmexecd start**<br /><br /> Остановка: **/etc/init d/ccmexecd stop**<br /><br /> Перезапуск: **/etc/init d/ccmexecd restart**|  
|Solaris 10|Запуск:<br /><br /> **svcadm enable -s svc:/application/management/omiserver**<br /><br /> **svcadm enable -s svc:/application/management/ccmexecd**<br /><br /> Остановка:<br /><br /> **svcadm disable -s svc:/application/management/ccmexecd**<br /><br /> **svcadm disable -s svc:/application/management/omiserver**|  
|Solaris 11|Запуск:<br /><br /> **svcadm enable -s svc:/application/management/omiserver**<br /><br /> **svcadm enable -s svc:/application/management/ccmexecd**<br /><br /> Остановка:<br /><br /> **svcadm disable -s svc:/application/management/ccmexecd**<br /><br /> **svcadm disable -s svc:/application/management/omiserver**|  
|AIX|Запуск:<br /><br /> **startsrc -s omiserver**<br /><br /> **startsrc -s ccmexec**<br /><br /> Остановка:<br /><br /> **stopsrc -s ccmexec**<br /><br /> **stopsrc -s omiserver**|  
|HP-UX|Запуск: **/sbin/init.d/ccmexecd start**<br /><br /> Остановка: **/sbin/init.d/ccmexecd stop**<br /><br /> Перезапуск: **/sbin/init.d/ccmexecd restart**|  
