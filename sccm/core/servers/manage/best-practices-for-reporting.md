---
title: "Melhores práticas de relatórios | Documentos do Microsoft"
description: "Leia algumas sugestões úteis sobre como utilizar a capacidade de criação de relatórios do System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 64f9d931-33f1-456f-a4e4-0ec077465bd0
caps.latest.revision: 4
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 759258999f3eaa810803a6a7f856f00fe7771a9e
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="best-practices-for-reporting-in-system-center-configuration-manager"></a>Melhores práticas para relatórios no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize as seguintes melhores práticas para criar relatórios no System Center Configuration Manager:  

## <a name="for-best-performance-install-the-reporting-services-point-on-a-remote-site-system-server"></a>Para obter o melhor desempenho, instalar o ponto do Reporting Services num servidor do sistema de sites remoto  
 Embora possa instalar o ponto do Reporting Services no servidor do site ou num sistema de sites remoto, o desempenho aumenta quando instala o ponto do Reporting Services num servidor do sistema de sites remoto.  

## <a name="optimize-sql-server-reporting-services-queries"></a>Otimizar as consultas do SQL Server Reporting Services  
 Normalmente, os atrasos na criação de relatórios devem-se ao tempo necessário para executar as consultas e obter os resultados. Se estiver a utilizar o Microsoft SQL Server, ferramentas como o Analisador de Consultas e o Gerador de Perfis podem ajudar a otimizar as consultas.  

## <a name="schedule-report-subscription-processing-to-run-outside-standard-office-hours"></a>Agendar o processamento de subscrição de relatório para ser executado fora do horário de expediente normal  
 Sempre que possível, agende o processamento de subscrição de relatório para execução fora de expediente normal para minimizar o processamento de CPU no Gestor de configuração do servidor de base de dados do site. Esta prática melhora também a disponibilidade para pedidos imprevistos de relatórios.  

## <a name="next-steps"></a>Passos seguintes
[Configurar os relatórios](configuring-reporting.md)

