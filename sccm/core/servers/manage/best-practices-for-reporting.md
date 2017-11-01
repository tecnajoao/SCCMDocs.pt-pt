---
title: "Melhores práticas de relatórios"
titleSuffix: Configuration Manager
description: "Ler algumas dicas úteis sobre como utilizar a capacidade de relatórios do System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 64f9d931-33f1-456f-a4e4-0ec077465bd0
caps.latest.revision: "4"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: b66e4417658e8a5f25056ed37b5367d57ff72781
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="best-practices-for-reporting-in-system-center-configuration-manager"></a>Melhores práticas para relatórios no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize as seguintes melhores práticas para criar relatórios no System Center Configuration Manager:  

## <a name="for-best-performance-install-the-reporting-services-point-on-a-remote-site-system-server"></a>Para obter o melhor desempenho, instalar o ponto do Reporting Services num servidor do sistema de sites remoto  
 Embora possa instalar o ponto do Reporting Services no servidor do site ou num sistema de sites remoto, o desempenho aumenta quando instala o ponto do Reporting Services num servidor do sistema de sites remoto.  

## <a name="optimize-sql-server-reporting-services-queries"></a>Otimizar as consultas do SQL Server Reporting Services  
 Normalmente, os atrasos na criação de relatórios devem-se ao tempo necessário para executar as consultas e obter os resultados. Se estiver a utilizar o Microsoft SQL Server, ferramentas como o Analisador de Consultas e o Gerador de Perfis podem ajudar a otimizar as consultas.  

## <a name="schedule-report-subscription-processing-to-run-outside-standard-office-hours"></a>Agendar o processamento de subscrição de relatório para ser executado fora do horário de expediente normal  
 Sempre que possível, agende o processamento de subscrição de relatório para execução fora de expediente normal para minimizar o processamento da CPU no Gestor de configuração do servidor de base de dados do site. Esta prática melhora também a disponibilidade para pedidos imprevistos de relatórios.  

## <a name="next-steps"></a>Passos seguintes
[Configurar relatórios](configuring-reporting.md)
