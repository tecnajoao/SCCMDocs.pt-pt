---
title: "Dados de diagnóstico FAQ"
titleSuffix: Configuration Manager
description: "Localize perguntas mais frequentes sobre os dados de diagnóstico e utilização para o System Center Configuration Manager."
ms.custom: na
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3fe32aa2-d594-4ad0-a291-b8f5395ac50b
caps.latest.revision: "6"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 91be283558f051f90080ac2e2f7abc09317eac4a
ms.sourcegitcommit: ca9d15dfb1c9eb47ee27ea9b5b39c9f8cdcc0748
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/04/2018
---
# <a name="frequently-asked-questions-about-diagnostics-and-usage-data-for-system-center-configuration-manager"></a>Perguntas frequentes sobre diagnósticos e dados de utilização para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

As seguintes perguntas mais frequentes sobre os dados de diagnóstico e utilização para o System Center Configuration Manager:  

###  <a name="bkmk_off"></a> como desligo a telemetria?  
Telemetria não pode ser desativada. No entanto, pode escolher o nível de dados de telemetria que são recolhidos. Também pode utilizar um ponto de ligação de serviço no modo offline, para ajudar a gerir quando os dados de telemetria são submetidos.

O ramo atual do Configuration Manager tem de ser atualizado regularmente para suportar novas versões do Windows 10 e o Microsoft Intune. Microsoft necessita, pelo menos, o nível básico dos diagnósticos e dados de utilização para manter o produto atualizado, melhorar a experiência de atualização e melhorar a qualidade e segurança do produto.

###  <a name="bkmk_retention"></a> O que é o período de retenção de dados?  
 Os dados de diagnóstico e de utilização são conservados durante um ano.  

###  <a name="bkmk_update"></a> Os diagnósticos e dados de utilização são enviados ao instalar ou atualizar o produto?  
 Não. Os diagnósticos e dados de utilização são apenas enviados depois do site ser instalado e estar operacional.  

###  <a name="bkmk_frequency"></a> Os dados são enviados com que frequência?  
 O SQL Server armazenada procedimentos executados a cada sete dias (a contar da data em que a instalação do site). No modo online, o ponto de ligação de serviço está configurado para carregar os dados após a execução de consultas. No modo offline, o administrador utiliza a ferramenta de ligação de serviço para carregar os dados. (Tenha em atenção de que os dados não estão disponíveis inicialmente para utilização offline sete dias após a instalação do site.)  

###  <a name="bkmk_network"></a> Os dados podem ser utilizados para formar um mapa de rede?  
 Como é mostrado na descrição dos níveis de recolha de dados de diagnóstico de utilização para o System Center Configuration Manager, os detalhes de site incluem informações de fuso horário de cada site. Esta informação pode fornecem informações aprofundadas de geolocalização abrangente e dispersão global dos sites numa hierarquia. No entanto, são recolhidos sem detalhes da rede, (esses endereços IP ou informações geográficas mais detalhadas).
 - [Dados de diagnóstico para 1511](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1511)
 - [Dados de diagnóstico para 1602](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1602)
 - [Dados de diagnóstico da versão 1606](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1606)
 - [Dados de diagnóstico da versão 1610](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1610)


###  <a name="bkmk_tables"></a> Consegue ver os dados nas tabelas personalizadas?  
 Não. Dados de diagnóstico e utilização são recolhidos através de procedimentos armazenados de SQL relativamente a tabelas de produtos predefinidas na base de dados (todas as que têm o prefixo **Tel _** ). Como parte da consulta de deteção do esquema SQL, todos os nomes de tabela estão têm um hash para comparação contra as predefinições conhecidas. Isto pode determinar que tabelas personalizadas existem na base de dados (que é expandido o esquema de base de dados da predefinição), mas não quaisquer dados contidos nessas tabelas.  

###  <a name="bkmk_databases"></a>Pode ver os nomes de outras bases de dados ou, pode ver os dados nas outras bases de dados?  
 Não. Os procedimentos armazenados para recolher dados estão limitados à base de dados do site.  

## <a name="see-also"></a>Consulte também  
 [Os diagnósticos e dados de utilização para o System Center Configuration Manager](../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)
