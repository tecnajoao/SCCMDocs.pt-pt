---
title: Melhores práticas de relatórios
titleSuffix: Configuration Manager
description: Ler algumas dicas úteis sobre como utilizar a capacidade de relatórios do System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 64f9d931-33f1-456f-a4e4-0ec077465bd0
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 87ed3a0591107695a1f418b38f2e3f5cb9168c63
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
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
