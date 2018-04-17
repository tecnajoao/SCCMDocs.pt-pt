---
title: Dados de diagnóstico e utilização FAQ
titleSuffix: Configuration Manager
description: Localize perguntas mais frequentes sobre os dados de diagnóstico e utilização para o System Center Configuration Manager.
ms.custom: na
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3fe32aa2-d594-4ad0-a291-b8f5395ac50b
caps.latest.revision: 6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5a8a34e14d0e4f187e520faf9b2e520945087097
ms.sourcegitcommit: fb84bcb31d825f454785e3d9d8be669e00fe2b27
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/16/2018
---
# <a name="frequently-asked-questions-about-diagnostics-and-usage-data-for-system-center-configuration-manager"></a>Perguntas frequentes sobre diagnósticos e dados de utilização para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo fornece respostas às perguntas mais frequentes sobre os dados de diagnóstico e utilização no Configuration Manager.

## <a name="faqs"></a>FAQs

###  <a name="bkmk_off"></a> como desligo a telemetria?  
Telemetria não pode ser desativada. No entanto, pode escolher o nível de dados de telemetria que são recolhidos. Para ajudar a gerir quando os dados telemétricos for submetidos, utilize o ponto de ligação de serviço no modo offline.

O ramo atual do Configuration Manager tem de ser atualizado regularmente para suportar novas versões do Windows 10 e o Microsoft Intune. Microsoft necessita, pelo menos, o nível básico dos dados de diagnóstico e de utilização. Estes dados são utilizados para manter o produto atualizado, melhorar a experiência de atualização e melhorar a qualidade e segurança do produto.

###  <a name="bkmk_retention"></a> O que é o período de retenção de dados?  
 Dados de diagnóstico e utilização são armazenados durante um ano.  

###  <a name="bkmk_update"></a> Os diagnósticos e dados de utilização são enviados ao instalar ou atualizar o produto?  
 Não. Os diagnósticos e dados de utilização são apenas enviados depois do site ser instalado e estar operacional.  

###  <a name="bkmk_frequency"></a> Os dados são enviados com que frequência?  
 O SQL Server armazenada procedimentos executados a cada sete dias a contar da data a instalação do site. No modo online, o ponto de ligação de serviço está configurado para carregar os dados após a execução de consultas. No modo offline, o administrador utiliza a ferramenta de ligação de serviço para carregar os dados. (Os dados não estão disponíveis inicialmente para utilização offline sete dias após a instalação do site.)  

###  <a name="bkmk_network"></a> Os dados podem ser utilizados para formar um mapa de rede?  
 Como é mostrado na descrição dos níveis de dados de diagnóstico e utilização, detalhes de site incluem informações de fuso horário de cada site. Esta informação pode fornecem informações aprofundadas de geolocalização abrangente e dispersão global dos sites numa hierarquia. Estes dados não incluem quaisquer detalhes da rede, tais como endereços IP ou informações geográficas mais detalhadas. Para obter mais informações, consulte a lista de [artigos de dados de utilização e diagnóstico](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data#articles)e localize os níveis de recolha de dados de diagnóstico e utilização para a versão que está a utilizar.


###  <a name="bkmk_tables"></a> Consegue ver os dados nas tabelas personalizadas?  
 Não. O Configuration Manager recolhe diagnóstico e procedimentos armazenados de dados de utilização através do SQL Server. Estes procedimentos executados em relação a tabelas de produtos predefinidas na base de dados de armazenados. Todas estas tabelas SQL são adicionado o prefixo **Tel _**. Como parte da consulta de deteção do esquema SQL, todos os nomes de tabela estão têm um hash para comparação contra as predefinições conhecidas. Este comportamento determina que tabelas personalizadas existem na base de dados. A presença de tabelas personalizadas informa que o esquema de base de dados é expandido do predefinido. Não inclui quaisquer dados armazenados nessas tabelas.  

###  <a name="bkmk_databases"></a> Pode ver os nomes de outras bases de dados ou, pode ver os dados nas outras bases de dados? 
 Não. Os procedimentos armazenados para recolher dados estão limitados à base de dados do site.  

### <a name="bkmk_gdpr"></a> É o Configuration Manager sujeitos regulamento gerais de proteção de dados (GDPR)?
 Não. O Configuration Manager não está sujeita a supervisão GDPR. É um produto no local que diretamente implementar, gerir e operar. Os dados de diagnóstico e de utilização que a Microsoft recolhe melhora a experiência de instalação, qualidade e segurança de versões futuras. Estes dados estão sujeita a supervisão GDPR. Não existem informações de identificação do utilizador final (EUII) ou identificadores pseudonymous do utilizador final (EUPI) são recolhidos e transmitidos à Microsoft. Para mais informações sobre GDPR, consulte o [Microsoft Trust Center no GDPR](https://microsoft.com/gdpr). Para mais informações sobre dados do Configuration Manager, consulte [diagnósticos e dados de utilização](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).


## <a name="see-also"></a>Consulte também  
 [Dados de diagnóstico e de utilização](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data)
