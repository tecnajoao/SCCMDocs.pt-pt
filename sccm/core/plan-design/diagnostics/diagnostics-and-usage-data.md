---
title: Dados de diagnóstico e de utilização
titleSuffix: Configuration Manager
description: Saiba mais sobre os diagnósticos e dados de utilização que o System Center Configuration Manager recolhe sobre si próprio.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 88ac4e55-d47b-4c94-b9c3-704c6a48b845
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5a70f632c04d7202ed1c41e5e138ed63dfdba1c6
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="diagnostics-and-usage-data-for-system-center-configuration-manager"></a>Dados de diagnóstico e de utilização para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O Configuration Manager recolhe os diagnósticos e dados de utilização sobre si próprio, que são utilizados pela Microsoft para melhorar a experiência de instalação, qualidade e segurança de versões futuras.  

 Diagnóstico e dados de utilização estão ativados para cada hierarquia do Configuration Manager. Consiste em consultas do SQL Server que são executadas semanalmente em cada site primário e no site de administração central. Quando a hierarquia utiliza um site de administração central, os dados de sites primários são replicados para esse site. No site de nível superior da hierarquia, o ponto de ligação de serviço envia estas informações quando verifica a existência de atualizações. Se o ponto de ligação de serviço estiver no modo offline, as informações são transferidas ao utilizar a ferramenta de ligação de serviço.  

> [!NOTE]  
>  O Configuration Manager recolhe os dados apenas a partir SQL server da base de dados do site e não recolhe dados diretamente a partir de clientes ou servidores de site.  

 Para obter mais informações, consulte o [declaração de privacidade do Microsoft](https://go.microsoft.com/fwlink/?LinkID=626527).  

## <a name="articles"></a>Artigos
 Saiba mais sobre os dados de diagnóstico e utilização para o Configuration Manager nos seguintes artigos:  

-   [Como os diagnósticos e dados de utilização são utilizados](../../../core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-used.md)  

-   Níveis de recolha de dados de diagnóstico de utilização:
    - [Dados de diagnóstico da versão 1802](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1802)  
    - [Dados de diagnóstico da versão 1710](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1710)  
    - [Dados de diagnóstico da versão 1706](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1706)    

<!--
    - [Diagnostic data for 1702](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1702)      
    - [Diagnostic data for 1610](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1610)  
    - [Diagnostic data for  1606](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1606)    
    - [Diagnostic data for 1602](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1602)
    - [Diagnostic data for  1511](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1511)
-->

-   [Como os diagnósticos e os dados de utilização são recolhidos](../../../core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-collected.md)  

-   [Como visualizar diagnósticos e dados de utilização](../../../core/plan-design/diagnostics/view-diagnostics-and-usage-data.md)  

-   [Programa de Melhoramento da Experiência do Cliente (PMEC)](../../../core/plan-design/diagnostics/customer-experience-improvement-program-ceip.md)  

     > [!Note]  
     > A partir do Configuration Manager versão 1802 a funcionalidade CEIP é removida do produto.


-   [Perguntas mais frequentes sobre diagnósticos e dados de utilização](../../../core/understand/frequently-asked-questions-about-diagnostics-and-usage-data.md)  

## <a name="see-also"></a>Consulte Também  
 [Sobre o ponto de ligação de serviço](../../../core/servers/deploy/configure/about-the-service-connection-point.md)
