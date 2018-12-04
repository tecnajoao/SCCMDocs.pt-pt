---
title: Dados de diagnóstico e de utilização
titleSuffix: Configuration Manager
description: Saiba mais sobre os diagnósticos e dados de utilização que o System Center Configuration Manager, recolhe sobre si próprio.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 88ac4e55-d47b-4c94-b9c3-704c6a48b845
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 132604418ce810fb78b397f3d5f322b10abe6bb3
ms.sourcegitcommit: 1439817f1309658b31008d7bafaab32fc5ef8789
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52820021"
---
# <a name="diagnostics-and-usage-data-for-system-center-configuration-manager"></a>Dados de diagnóstico e de utilização para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O Configuration Manager recolhe os diagnósticos e dados de utilização sobre ele próprio, que são utilizados pela Microsoft para melhorar a experiência de instalação, qualidade e segurança de versões futuras.  

 Dados de diagnóstico e utilização estão ativados para cada hierarquia do Configuration Manager. Ele consiste em consultas de SQL Server que são executadas semanalmente em cada site primário e para o site de administração central. Quando a hierarquia utiliza um site de administração central, os dados de sites primários são replicados para esse site. No site de nível superior da hierarquia, o ponto de ligação de serviço envia estas informações quando verifica a existência de atualizações. Se o ponto de ligação de serviço estiver no modo offline, as informações são transferidas ao utilizar a ferramenta de ligação de serviço.  

> [!NOTE]  
>  O Configuration Manager recolhe dados apenas a partir SQL server da base de dados do site, o, e não recolhe dados diretamente a partir de clientes ou servidores de site.  

 Para obter mais informações, consulte a [declaração de privacidade do Microsoft](https://go.microsoft.com/fwlink/?LinkID=626527).  

## <a name="articles"></a>Artigos
 Saiba mais sobre os dados de diagnóstico e utilização para o Configuration Manager nos seguintes artigos:  

-   [Como os diagnósticos e dados de utilização são utilizados](/sccm/core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-used)  

-   Níveis de recolha de dados de diagnóstico de utilização:
    - [Dados de diagnóstico para 1810](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1810)  

    - [Dados de diagnóstico da versão 1806](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1806)  

    - [Dados de diagnóstico da versão 1802](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1802)  
    
    - [Dados de diagnóstico da versão 1710](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1710)  

-   [Como os diagnósticos e os dados de utilização são recolhidos](/sccm/core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-collected)  

-   [Como visualizar diagnósticos e dados de utilização](/sccm/core/plan-design/diagnostics/view-diagnostics-and-usage-data)  

-   [Programa de Melhoramento da Experiência do Cliente (PMEC)](/sccm/core/plan-design/diagnostics/customer-experience-improvement-program-ceip)  

     > [!Note]  
     > A partir do Configuration Manager versão 1802 a funcionalidade CEIP é removida do produto.  


-   [Perguntas mais frequentes sobre diagnósticos e dados de utilização](/sccm/core/understand/frequently-asked-questions-about-diagnostics-and-usage-data)  



## <a name="see-also"></a>Consulte Também  
 [Sobre o ponto de ligação de serviço](/sccm/core/servers/deploy/configure/about-the-service-connection-point)
