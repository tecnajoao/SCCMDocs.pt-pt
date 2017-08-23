---
title: "Данные о диагностике и использовании | Документация Майкрософт"
description: "Дополнительные сведения о данных о диагностике и использовании, собираемых System Center Configuration Manager для собственных компонентов."
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 88ac4e55-d47b-4c94-b9c3-704c6a48b845
caps.latest.revision: "9"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 4a4b7c9c0d40b6bd3ea2f318e37d744f1a0cc084
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2017
---
# <a name="diagnostics-and-usage-data-for-system-center-configuration-manager"></a>Данные о диагностике и использовании для System Center Configuration Manager

*Применимо к: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager собирает собственные данные о диагностике и использовании, которые применяются корпорацией Майкрософт для улучшения процесса установки, качества и безопасности будущих выпусков.  

 Сбор данных о диагностике и использовании включен для всех иерархий System Center Configuration Manager. Они составляются посредством запросов SQL Server, выполняемых еженедельно на каждом первичном сайте и сайте центра администрирования. Когда иерархия использует сайт центра администрирования, данные из первичных сайтов реплицируются на этот сайт. На верхнем сайте иерархии точка подключения службы отправляет эти сведения при выполнении проверки на наличие обновлений. Если точка подключения службы находится в автономном режиме, данные передаются с помощью средства подключения службы.  

> [!NOTE]  
>  Configuration Manager собирает данные только из базы данных SQL Server сайта, не получая их непосредственно с клиентов или серверов сайта.  

 Дополнительные сведения см. в статье [Заявление о конфиденциальности для System Center Configuration Manager](http://go.microsoft.com/fwlink/?LinkID=626527).  

 Дополнительные сведения о данных диагностики и использования для System Center Configuration Manager можно найти в следующих разделах:  

-   [Как используются данные о диагностике и использовании для System Center Configuration Manager](../../../core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-used.md)  

-   Уровни сбора данных о диагностике и использовании:
    - [Диагностические данные для версии 1702](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1702)      
    - [Диагностические данные для 1610](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1610)  
    - [Диагностические данные для 1606](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1606)    

<!--
    - [Diagnostic data for 1602](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1602)
    - [Diagnostic data for  1511](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1511)
-->

-   [Как System Center Configuration Manager собирает данные о диагностике и использовании](../../../core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-collected.md)  

-   [Как просмотреть данные о диагностике и использовании для System Center Configuration Manager](../../../core/plan-design/diagnostics/view-diagnostics-and-usage-data.md)  

-   [Программа улучшения качества программного обеспечения (CEIP) для System Center Configuration Manager](../../../core/plan-design/diagnostics/customer-experience-improvement-program-ceip.md)  

-   [Часто задаваемые вопросы о данных по диагностике и использовании для System Center Configuration Manager](../../../core/understand/frequently-asked-questions-about-diagnostics-and-usage-data.md)  

## <a name="see-also"></a>См. также  
 [Сведения о точке подключения службы в System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md)
