---
title: "Dados de diagnóstico e de utilização"
titleSuffix: Configuration Manager
description: "Saiba mais sobre os diagnósticos e dados de utilização que o System Center Configuration Manager recolhe sobre si próprio."
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
author: aaroncz
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: c70f7bc6e0b69685a8446a6d599b0b10f7508ac1
ms.sourcegitcommit: 7fe45ff75f05f7cc03ad021db8119791abe18049
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/01/2017
---
# <a name="diagnostics-and-usage-data-for-system-center-configuration-manager"></a>Dados de diagnóstico e de utilização para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager recolhe os diagnósticos e dados de utilização sobre si próprio, que são utilizados pela Microsoft para melhorar a experiência de instalação, qualidade e segurança de versões futuras.  

 Os diagnósticos e dados de utilização está ativada para cada hierarquia do System Center Configuration Manager. Consiste em consultas do SQL Server que são executadas semanalmente em cada site primário e no site de administração central. Quando a hierarquia utiliza um site de administração central, os dados de sites primários são replicados para esse site. No site de nível superior da hierarquia, o ponto de ligação de serviço envia estas informações quando verifica a existência de atualizações. Se o ponto de ligação de serviço estiver no modo offline, as informações são transferidas ao utilizar a ferramenta de ligação de serviço.  

> [!NOTE]  
>  O Configuration Manager recolhe os dados apenas a partir SQL server da base de dados do site e não recolhe dados diretamente a partir de clientes ou servidores de site.  

 Para obter mais informações, consulte o [declaração de privacidade do System Center Configuration Manager](http://go.microsoft.com/fwlink/?LinkID=626527).  

 Saiba mais sobre os dados de diagnóstico e utilização para o System Center Configuration Manager nos seguintes artigos:  

-   [Como os dados de diagnóstico e utilização são utilizados para o System Center Configuration Manager](../../../core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-used.md)  

-   Níveis de recolha de dados de diagnóstico de utilização:
    - [Dados de diagnóstico da versão 1702](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1702)      
    - [Dados de diagnóstico da versão 1610](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1610)  
    - [Dados de diagnóstico para 1606](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1606)    

<!--
    - [Diagnostic data for 1602](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1602)
    - [Diagnostic data for  1511](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1511)
-->

-   [Como os diagnósticos e dados de utilização são recolhidos pelo System Center Configuration Manager](../../../core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-collected.md)  

-   [Como visualizar diagnósticos e dados de utilização para o System Center Configuration Manager](../../../core/plan-design/diagnostics/view-diagnostics-and-usage-data.md)  

-   [Programa de melhoramento da experiência do cliente (PMEC) do System Center Configuration Manager](../../../core/plan-design/diagnostics/customer-experience-improvement-program-ceip.md)  

-   [Perguntas mais frequentes sobre diagnósticos e dados de utilização para o System Center Configuration Manager](../../../core/understand/frequently-asked-questions-about-diagnostics-and-usage-data.md)  

## <a name="see-also"></a>Consulte Também  
 [Acerca do ponto de ligação de serviço no System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md)
