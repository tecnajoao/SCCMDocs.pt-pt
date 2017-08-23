---
title: "Поддержка виртуализации | Документы Майкрософт"
description: "Требования для установки клиента и ролей системы сайта System Center Configuration Manager в среде виртуализации."
ms.custom: na
ms.date: 1/12/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1098e8c5-9676-4c2b-841b-ec88bd04e495
caps.latest.revision: "6"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: b49bd179da850cee35b2487a353bb1788df03d58
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="support-for-virtualization-environments-for-system-center-configuration-manager"></a>Поддержка сред виртуализации для System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

Configuration Manager поддерживает установку клиента и ролей системы сайта в поддерживаемых операционных системах, которые работают как виртуальные машины в средах виртуализации, перечисленных в этом разделе. Эта поддержка остается даже тогда, когда узел виртуальной машины (среда виртуализации) не поддерживается как клиент или сервер сайта.  

 Например, если вы используете Microsoft Hyper-V Server 2012 для размещения виртуальной машины, на которой работает Windows Server 2012, вы можете установить роли клиента или системы сайта на виртуальной машине (Windows Server 2012), но не в узле (Microsoft Hyper-V Server 2012).  

|Среда виртуализации|  
|--------------------------------|  
|Windows Server 2008 R2|  
|Microsoft Hyper-V Server 2008 R2|  
|Windows Server 2012|  
|Microsoft Hyper-V Server 2012|  
|Windows Server 2012 R2|
|Windows Server 2016 <sup>(см. *примечание 1*)</sup>|
|Microsoft Hyper-V Server 2016 <sup>(см. *примечание 1*)|
-  *Примечание 1*. Configuration Manager не поддерживает [вложенную виртуализацию](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/what-s-new-in-hyper-v-on-windows#a-namebkmknestedanested-virtualization-new), которая появилась в Windows Server 2016.


 Каждый используемый виртуальный компьютер должен соответствовать требованиям к оборудованию и программному обеспечению, которые применялись бы для физического компьютера Configuration Manager (или превосходить их).  

 Можно проверить поддержку среды виртуализации в Configuration Manager, используя программу проверки виртуализации серверов (SVVP) и связанный с ней мастер политики поддержки программы виртуализации (Virtualization Program Support Policy Wizard) в Интернете. Дополнительные сведения о программе проверки виртуализации серверов см. в разделе [Программа проверки виртуализации Windows Server](https://www.windowsservercatalog.com/svvp.aspx).  

> [!NOTE]  
>  Configuration Manager не поддерживает гостевые операционные системы Virtual PC и Virtual Server, работающие на компьютерах Mac.  

Configuration Manager не может управлять виртуальными машинами, если они недоступны в Интернете. Образ отключенной виртуальной машины нельзя обновить; также нельзя проводить сбор данных инвентаризации при помощи клиента Configuration Manager на основном компьютере.  

Виртуальные машины не обслуживаются особым образом. Например, Configuration Manager может не определить, необходимо ли повторно применить к образу виртуальной машины обновление, если виртуальная машина, к которой применялось обновление, была остановлена и перезапущена без сохранения состояния.  

##  <a name="bkmk_Azure"></a> Виртуальные машины Microsoft Azure  
 Configuration Manager может выполняться на виртуальных машинах в Azure точно так же, как и локально в физической корпоративной сети. Вы можете использовать Configuration Manager с виртуальными машинами Azure в описанных ниже сценариях.  

-   **Сценарий 1**. Вы можете запускать Configuration Manager на виртуальной машине Azure и использовать его для управления клиентами, установленными на других виртуальных машинах Azure.  

-   **Сценарий 2**. Вы можете запускать диспетчер Configuration Manager в виртуальной машине Azure и использовать его для управления клиентами, работающими за пределами Azure.  

-   **Сценарий 3**. Вы можете запускать различные роли системы сайта Configuration Manager в виртуальных машинах Azure и одновременно запускать другие роли в своей физической корпоративной сети (с соответствующим сетевым подключением).  

Те же требования System Center Configuration Manager для сетей, поддерживаемых конфигураций и требования к оборудованию, применяемые к установке Configuration Manager локально в физической корпоративной сети, применяются и к установке в виртуальных машинах Azure.  

Дополнительные сведения см. в разделе [Вопросы и ответы по использованию Configuration Manager в Azure](/sccm/core/understand/configuration-manager-on-azure).

> [!IMPORTANT]  
>  На сайты и клиенты Configuration Manager, работающие на виртуальных машинах Azure, распространяются те же требования к лицензиям, что и на локальные установки.  
