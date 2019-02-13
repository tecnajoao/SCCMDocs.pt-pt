---
title: Dados de diagnóstico e utilização FAQ
titleSuffix: Configuration Manager
description: Encontre as perguntas mais frequentes sobre os dados de diagnóstico e utilização para o System Center Configuration Manager.
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3fe32aa2-d594-4ad0-a291-b8f5395ac50b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 17e9ee2b969a9cc6e9258fa698be91fa15f4c2e3
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56127104"
---
# <a name="frequently-asked-questions-about-diagnostics-and-usage-data-for-system-center-configuration-manager"></a>Perguntas frequentes sobre diagnósticos e dados de utilização para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo fornece respostas às perguntas mais frequentes sobre os dados de diagnóstico e utilização no Configuration Manager.

## <a name="faqs"></a>FAQs

###  <a name="bkmk_off"></a> como desligo a telemetria?  
Telemetria não pode ser desativada. No entanto, pode escolher o nível de dados de telemetria que são recolhidos. Para ajudar a gerenciar de quando os dados de telemetria são submetidos, utilize o ponto de ligação de serviço no modo offline.

O current branch do Configuration Manager tem de ser atualizado regularmente para suportar as novas versões do Windows 10 e o Microsoft Intune. A Microsoft requer, pelo menos, o nível básico de dados de diagnóstico e utilização. Estes dados são utilizados para manter o produto atualizado, melhorar a experiência de atualização e melhorar a qualidade e segurança do produto.

###  <a name="bkmk_retention"></a> O que é o período de retenção de dados?  
 Dados de diagnóstico e utilização são armazenados durante um ano.  

###  <a name="bkmk_update"></a> Os diagnósticos e dados de utilização são enviados ao instalar ou atualizar o produto?  
 Não. Os diagnósticos e dados de utilização são apenas enviados depois do site ser instalado e estar operacional.  

###  <a name="bkmk_frequency"></a> Os dados são enviados com que frequência?  
 O SQL procedimentos armazenados são executados a cada sete dias a contar da data, a instalação do site. No modo online, o ponto de ligação de serviço está configurado para carregar os dados após a execução de consultas. No modo offline, o administrador utiliza a ferramenta de ligação de serviço para carregar os dados. (Os dados não estão disponíveis inicialmente para utilização offline sete dias após a instalação do site).  

###  <a name="bkmk_network"></a> Os dados podem ser utilizados para formar um mapa de rede?  
 Como mostra a descrição dos níveis de dados de diagnóstico e utilização, detalhes do site incluem informações de fuso horário de cada site. Estas informações podem fornecer informações detalhadas sobre a geolocalização abrangente e dispersão global dos sites numa hierarquia. Estes dados não incluem quaisquer detalhes da rede, como endereços IP ou informações geográficas mais detalhadas. Para obter mais informações, consulte a lista de [artigos de dados de utilização e diagnóstico](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data#articles)e encontrar os níveis de recolha de dados de diagnóstico e utilização para a versão que está a utilizar.


###  <a name="bkmk_tables"></a> Consegue ver os dados nas tabelas personalizadas?  
 Não. Do Configuration Manager recolhe os diagnósticos e dados de utilização através do SQL de procedimentos armazenados. Estes procedimentos armazenados são executados em relação a tabelas de produtos predefinidas na base de dados. Todas essas tabelas SQL têm o prefixo **Tel _**. Como parte da consulta de deteção do esquema SQL, todos os nomes de tabela estão têm um hash para comparação contra as predefinições conhecidas. Este comportamento determina que tabelas personalizadas existem na base de dados. A presença de tabelas personalizadas informa que o esquema de banco de dados é expandido a partir da predefinição. Não inclui nenhum dos dados armazenados contidos nessas tabelas.  

###  <a name="bkmk_databases"></a> Pode ver os nomes de outras bases de dados ou, pode ver os dados nas outras bases de dados? 
 Não. Os procedimentos armazenados para recolher dados estão limitados à base de dados do site.  

### <a name="bkmk_gdpr"></a> É o Configuration Manager sujeitos a Regulamento geral de proteção de dados (GDPR)?
 Não. O Configuration Manager não está sujeito a supervisão do GDPR. É um produto no local que diretamente implementa, gerir e opera. Os dados de diagnóstico e utilização que a Microsoft recolhe melhora a experiência de instalação, qualidade e segurança de versões futuras. Estes dados de diagnóstico e utilização estão sujeita a supervisão do GDPR. No entanto, sem informações de identificação do utilizador final (EUII) ou identificadores de utilizador final pseudonymous (EUPI) são recolhidos e transmitidas à Microsoft. Para obter mais informações sobre o GDPR, consulte a [Microsoft Trust Center no GDPR](https://microsoft.com/gdpr). Para obter mais informações sobre dados do Configuration Manager, consulte [diagnósticos e dados de utilização](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).


## <a name="see-also"></a>Consulte também  
 [Dados de diagnóstico e de utilização](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data)
