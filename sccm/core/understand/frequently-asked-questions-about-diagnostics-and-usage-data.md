---
title: "Dados de diagnóstico FAQ | Documentos do Microsoft"
description: "Localize as perguntas mais frequentes sobre os dados de diagnóstico e a utilização do System Center Configuration Manager."
ms.custom: na
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3fe32aa2-d594-4ad0-a291-b8f5395ac50b
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 6cf291d79c1c5d9540f809fcb00e7ab48e0c3d3b
ms.openlocfilehash: 177a30a30f6b8579fa1956d28581d4f9d3a11838
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="frequently-asked-questions-about-diagnostics-and-usage-data-for-system-center-configuration-manager"></a>Perguntas frequentes sobre diagnósticos e dados de utilização para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O seguinte é perguntas mais frequentes sobre dados de utilização e de diagnóstico para o System Center Configuration Manager:  

###  <a name="bkmk_off"></a> como desligo a telemetria?  
Telemetria não pode ser desligada. No entanto, pode escolher o nível de dados de telemetria que são recolhidos. Também pode utilizar um ponto de ligação de serviço no modo offline para ajudar a gerir quando for submetidos dados telemétricos.

O ramo atual do Configuration Manager tem de ser atualizada regularmente para suportar novas versões do Windows 10 e o Microsoft Intune. Microsoft necessita pelo menos o nível básico de diagnóstico e dados de utilização para manter o produto atualizado, melhorar a experiência de atualização e melhorar a qualidade e segurança do produto.

###  <a name="bkmk_retention"></a> O que é o período de retenção de dados?  
 Os dados de diagnóstico e de utilização são conservados durante um ano.  

###  <a name="bkmk_update"></a> Os diagnósticos e dados de utilização são enviados ao instalar ou atualizar o produto?  
 Não. Os diagnósticos e dados de utilização são apenas enviados depois do site ser instalado e estar operacional.  

###  <a name="bkmk_frequency"></a> Os dados são enviados com que frequência?  
 O SQL Server armazenada procedimentos executar cada sete dias (a partir da data em que a instalação do site). No modo online, o ponto de ligação de serviço está configurado para carregar os dados após a execução de consultas. No modo offline, o administrador utiliza a ferramenta de ligação de serviço para carregar os dados. (Tenha em atenção de que os dados não são inicialmente disponíveis para utilização offline até sete dias após a instalação do site.)  

###  <a name="bkmk_network"></a> Os dados podem ser utilizados para formar um mapa de rede?  
 Como é apresentado na descrição dos níveis de recolha de dados de diagnóstico de utilização para o System Center Configuration Manager, detalhes do site incluem informações de fuso horário de cada site. Estas informações podem fornecer informações aprofundadas de geolocalização abrangente e dispersion global dos sites numa hierarquia. No entanto, não existem detalhes de rede são recolhidos, (como endereços IP ou informações geográficas mais detalhadas).
 - [Dados de diagnóstico para 1511](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1511)
 - [Dados de diagnóstico para 1602](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1602)
 - [Dados de diagnóstico para 1606](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1606)
 - [Dados de diagnóstico para 1610](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1610)


###  <a name="bkmk_tables"></a> Consegue ver os dados nas tabelas personalizadas?  
 Não. Os dados de diagnóstico e de utilização são recolhidos através de procedimentos armazenados de SQL relativamente a tabelas de produto de predefinição na base de dados (que é adicionado como prefixo com **TEL_** ). Como parte da consulta de deteção do esquema SQL, todos os nomes de tabela estão têm um hash para comparação contra as predefinições conhecidas. Isto pode determine que tabelas personalizadas existem na base de dados (que o esquema de base de dados é expandido a predefinição), mas não a qualquer um dos dados contidos nessas tabelas.  

###  <a name="bkmk_databases"></a>Consegue ver os nomes de outras bases de dados ou, pode ver dados noutras bases de dados?  
 Não. Os procedimentos armazenados para recolher dados estão limitados à base de dados do site.  

## <a name="see-also"></a>Consulte também  
 [Diagnóstico e dados de utilização para o System Center Configuration Manager](../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)

