---
title: "Diagnóstico e dados de utilização | Documentos do Microsoft"
description: "Saiba mais acerca do diagnostics e dados de utilização do Configuration Manager do System Center recolhe sobre si próprio."
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 88ac4e55-d47b-4c94-b9c3-704c6a48b845
caps.latest.revision: 9
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 4a4b7c9c0d40b6bd3ea2f318e37d744f1a0cc084
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="diagnostics-and-usage-data-for-system-center-configuration-manager"></a>Dados de diagnóstico e de utilização para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager recolhe diagnostics e dados de utilização sobre si, que são utilizados pela Microsoft para melhorar a experiência de instalação, qualidade e segurança dos lançamentos futuros.  

 Dados de utilização de diagnóstico e está ativada para cada hierarquia do System Center Configuration Manager. Ele consiste em consultas de SQL Server que são executadas semanalmente em cada site primário e para o site de administração central. Quando a hierarquia utiliza um site de administração central, os dados de sites primários são replicados para esse site. No site de nível superior da hierarquia, o ponto de ligação de serviço envia as informações quando verifica a existência de atualizações. Se o ponto de ligação de serviço estiver no modo offline, as informações são transferidas ao utilizar a ferramenta de ligação de serviço.  

> [!NOTE]  
>  O Configuration Manager recolhe dados apenas a partir da base de dados de servidor do site SQL, e não recolhe dados diretamente a partir de clientes ou servidores de sites.  

 Para obter mais informações, consulte o [declaração de privacidade para o System Center Configuration Manager](http://go.microsoft.com/fwlink/?LinkID=626527).  

 Saiba mais sobre dados de utilização e de diagnóstico para o System Center Configuration Manager nos seguintes artigos:  

-   [Como os dados de utilização e de diagnóstico são utilizados para o System Center Configuration Manager](../../../core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-used.md)  

-   Níveis de recolha de dados de diagnóstico de utilização:
    - [Dados de diagnóstico para 1702](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1702)      
    - [Dados de diagnóstico para 1610](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1610)  
    - [Dados de diagnóstico para 1606](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1606)    

<!--
    - [Diagnostic data for 1602](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1602)
    - [Diagnostic data for  1511](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1511)
-->

-   [Como os dados de diagnóstico e de utilização são recolhidos pelo System Center Configuration Manager](../../../core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-collected.md)  

-   [Como ver diagnósticos e dados de utilização para o System Center Configuration Manager](../../../core/plan-design/diagnostics/view-diagnostics-and-usage-data.md)  

-   [Programa de melhoramento da experiência do cliente (PMEC) para o System Center Configuration Manager](../../../core/plan-design/diagnostics/customer-experience-improvement-program-ceip.md)  

-   [Perguntas mais frequentes sobre diagnósticos e dados de utilização para o System Center Configuration Manager](../../../core/understand/frequently-asked-questions-about-diagnostics-and-usage-data.md)  

## <a name="see-also"></a>Consulte Também  
 [Sobre o ponto de ligação de serviço no System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md)

