---
title: Execute a ferramenta de resumo de medidor
titleSuffix: Configuration Manager
description: Utilize a ferramenta para executar o resumo de medidor para acionar tarefas no Configuration Manager de resumo de medição de software.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d27f88fe-817f-4af4-b290-c16f2e46cf31
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4815b308b1a4c93e3bc9271a3ec3af2f637b11cf
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39387110"
---
# <a name="run-meter-summarization-tool"></a>Execute a ferramenta de resumo de medidor

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

A ferramenta para executar o resumo de medidor é um da [ferramentas do Configuration Manager](/sccm/core/support/tools). Utilize-o para acionar imediatamente as tarefas de manutenção de resumo em sites primários de medição de software. Por predefinição, estas executar como as tarefas agendadas no **manutenção do Site** tarefas, as quais iniciar após 12:00 AM todos os dias. 

Estas tarefas resumem os dados no **MeterData** SQL de tabela e escrever os resultados de resumos para o **FileUsageSummary** e **MonthlyUsageSummary** tabelas. Em seguida, verá os resultados resumidos nos relatórios de medição de software. Qualquer utilizador administrativo do Configuration Manager que se pode ligar à base de dados do site primário pode utilizar esta ferramenta para executar o resumo. 

Essa ferramenta é executada a **resumo de utilização do ficheiro** e **resumo de utilização mensal** tarefas de resumo de dados de medição de software. Ela resume todos os dados de medidores existentes sem o período de espera de 12 horas habitual. Executá-la no SQL server que aloja a base de dados do site. Se o resumo for bem-sucedida, o código de saída está definido `0`. Se tiver ocorrido um erro, o código de saída é `1`.



## <a name="usage"></a>Utilização

### <a name="command-line"></a>Linha de comandos

`runmetersumm  [sms database name]  <delay in hours for summarization <default=0>>`


### <a name="options"></a>Opções

#### <a name="database-name"></a>Nome da base de dados
O nome da base de dados do site no SQL server.

#### <a name="delay-in-hours-for-summarization"></a>Atraso em horas de resumo
A ferramenta resume o software de medição de utilização gerada antes do atraso. Por predefinição, este atraso é de zero.


### <a name="example"></a>Exemplo

#### <a name="summarize-the-software-metering-usage-generated-12-hours-ago"></a>Resumir a utilização de medição de software gerada há 12 horas

`runmetersumm CCM_ABC <12>`



## <a name="see-also"></a>Consulte também

- [Tarefas de manutenção](/sccm/core/servers/manage/maintenance-tasks)
- [Monitorizar a utilização da aplicação com a medição de software](/sccm/apps/deploy-use/monitor-app-usage-with-software-metering)
