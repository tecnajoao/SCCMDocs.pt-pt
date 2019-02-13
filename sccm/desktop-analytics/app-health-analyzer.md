---
title: Analisador de estado de funcionamento da aplicação
titleSuffix: Configuration Manager
description: Um guia de procedimentos para avaliar a compatibilidade com o analisador de estado de funcionamento de aplicação no ambiente de trabalho de análise.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2af150a4-0c18-4b40-8492-c04c5d154596
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 122a27276adcaf57461157e9df03ee1092e52af5
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56126630"
---
# <a name="how-to-assess-compatibility-with-app-health-analyzer"></a>Como avaliar a compatibilidade com o analisador de estado de funcionamento da aplicação

> [!Note]  
> Estas informações se relaciona com o serviço de pré-visualização que pode ser substancialmente modificado antes do lançamento comercial. A Microsoft faz não oferece quaisquer garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

Utilize o toolkit de analisador de estado de funcionamento da aplicação para a área de trabalho de análise para avaliar aplicativos de desktop para problemas de compatibilidade. Ele ajuda a concentrar seus esforços de validação para aplicativos de desktop, incluindo aplicações de linha de negócio. A ferramenta fornece uma classificação de risco, juntamente com ações de remediação possíveis. Ele também inclui um relatório de preparação da aplicação para o ajudar a avaliar a preparação da aplicação para as atualizações do Windows 10. 



## <a name="download"></a>Transferência

Transfira o toolkit a partir da [Microsoft Download Center](http://download.microsoft.com/download/3/7/D/37D7E378-D805-4822-A712-4EADBF50FC08/AppHealthAnalyzer.zip)<!-- (https://www.microsoft.com/download/details.aspx?id=57276) -->. Utilize sempre a versão mais atual.

O download é um ficheiro do Windows Installer (MSI). Instale o Kit de ferramentas de analisador de estado de funcionamento da aplicação no computador de um utilizador. Quando executa o Kit de ferramentas, um assistente orienta-o no processo de criação de um relatório de preparação da aplicação. 

O Kit de ferramentas inclui scripts de exemplo. Se precisar de automatizar a coleta de informações sobre a preparação dos dispositivos em toda a organização, utilize o Configuration Manager para implantar esses scripts. Para obter mais informações, consulte [automatização](#automation). 



## <a name="how-it-works"></a>Como funciona

A ferramenta faz uma análise estática de aplicativos que já estejam instaladas num dispositivo. Ele não faz uma análise de um instalador de aplicação do pacote. Um usuário não precisa de executar a aplicação. A ferramenta avalia todas as aplicações instaladas registadas com o Windows no dispositivo. 

Analisador de estado de funcionamento da aplicação não precisa de manter os instaladores de aplicações legadas que não gere ativamente. Ele identifica problemas de compatibilidade com a aplicação no seu estado instalado. Todas as aplicações são avaliadas para regras de compatibilidade predefinido. Esses sinais são problemas comuns de predominantes reportados à Microsoft quando os clientes a atualização para o Windows 10. As informações de compatibilidade também incluem ações de remediação possível ou correções. Se tiver aplicações com problemas, comece com as ações sugeridas.

> [!Important]  
> O Kit de ferramentas não suporta funcionalidades a reparar ou corrigir as suas aplicações. Se criar um relatório de preparação da aplicação, ele fornece informações e orientações para ajudar a remediar as suas aplicações antes de atualizar para o Windows 10.  



## <a name="prerequisites"></a>Pré-requisitos

Antes de instalar e usar o Kit de ferramentas, certifique-se de que o dispositivo cumpre os seguintes requisitos:  

- O Windows 7 Service Pack 1 ou posterior  

- Ter privilégios de administrador no dispositivo  

- Microsoft .NET Framework 4.5.1 ou posterior  

- Inscritos no serviço de análise de ambiente de trabalho, que inclui os seguintes requisitos:  

    - Atualizações mais recentes. Para obter mais informações, consulte [atualizar os dispositivos](/sccm/desktop-analytics/enroll-devices#update-devices).  

    - Nível de dados de diagnóstico. Para obter mais informações, consulte [níveis de dados de diagnóstico](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels).  



## <a name="analyze"></a>Analisar 

1. Instale o analisador de estado de funcionamento da aplicação no dispositivo de destino. Por padrão, ele instala o seguinte caminho: `C:\Program Files\Microsoft Corporation\Microsoft App Health Analyzer`  

2. Vá para o Windows **começar** menu, expanda o **analisador de estado de funcionamento de aplicações do Microsoft** agrupar e abrir o **analisador de estado de funcionamento da aplicação** como administrador. Pode demorar vários minutos para gerar o relatório.  

    > [!Note]  
    > Se qualquer uma das definições de dados de diagnóstico de necessárias não estão configurados, verá um erro. Certifique-se de que configurar corretamente as definições de pré-requisitos. Para obter mais informações, consulte [níveis de dados de diagnóstico](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels).  

3. Quando abre o relatório de preparação da aplicação, ele começa a avaliação de aplicativos. Aguarde que o Kit de ferramentas concluir, que pode demorar algum tempo consoante o número de aplicativos no dispositivo.   

![Captura de ecrã do relatório de preparação de aplicação do analisador de estado de funcionamento da aplicação](media/app-readiness-report-evaluating.png)

Pode minimizar a janela e continuar com outras tarefas enquanto o Kit de ferramentas é executada em segundo plano.


### <a name="app-readiness-report-features"></a>Funcionalidades de relatório de preparação de aplicações

#### <a name="get-started"></a>Introdução
Este separador dá-lhe uma visão geral dos sinais suportadas nesta versão atual. Ele também inclui as ações de remediação possíveis. 

#### <a name="insights"></a>Informações
Este separador fornece uma exibição de todas as aplicações que a ferramenta avaliada. Ele mostra a avaliação de riscos e os sinais de vários utilizados para identificar problemas de compatibilidade. 

- **Sinais** menu: Filtrar estas aplicações por sinais utilizando o menu à esquerda  

- **Exportar CSV**: Exportar essas informações como um ficheiro de valores separados por vírgulas (CSV)   

- **Reanalisar aplicativos**: Se instalar todos os aplicativos novos, utilize esta opção para voltar a executar a ferramenta  

- **ID de resolução de problemas**: Se o dispositivo tiver aplicações instaladas, mas vê que não existem informações no relatório, dar este ID para suportar  

#### <a name="desktop-analytics"></a>Análise de Computadores
Este separador fornece uma visão geral de como pode utilizar o analisador de estado de funcionamento da aplicação para fornecer informações de preparação para aplicações na sua organização.



## <a name="automation"></a>Automatização

Para obter essas informações de aplicação em vários dispositivos, implemente a versão de linha de comandos do analisador de estado de funcionamento da aplicação com o Configuration Manager. Implementá-la a um pequeno conjunto de dispositivos representativos da sua organização. Por exemplo, usar suas análises do ambiente de trabalho *piloto* coleção. O mesmo [pré-requisitos](#prerequisites) aplicam-se para estes dispositivos.


Antes de fazer uma implantação mais ampla, primeiro certifique-se de uma execução com êxito. Certifique-se de que os dados são apresentados no ambiente de trabalho de análise. 

O Kit de ferramentas de analisador de estado de funcionamento da aplicação inclui um script de exemplo, run_silent.cmd. Por predefinição, este script está no seguinte caminho: `C:\Program Files\Microsoft Corporation\Microsoft App Health Analyzer`. Utilize este script para automatizar o processo com o Configuration Manager.


### <a name="tips"></a>Sugestões

- Antes de atualizar para o sistema operacional de destino, implemente o analisador de estado de funcionamento da aplicação para todos os dispositivos no seu projeto-piloto. Para obter informações de preparação em vigor, executá-la, pelo menos, uma vez no grupo piloto para um plano de implantação.  

- Análise de área de trabalho tem uma funcionalidade incorporada para recomendar grupos pilotos para seus planos de implantação. Execute o Kit de ferramentas em todos os dispositivos pilotos para obter total cobertura nas suas aplicações importantes.  

- Agende a ferramenta para executar quando um utilizador não tem sessão iniciado, ou quando não utilizar o dispositivo.  

- Configure uma agenda periódica. Por exemplo, execute cada 30 dias. Esta agenda obtém as informações mais recentes de preparação de seus dispositivos para os ajudar a manter-se atualizado.  



## <a name="desktop-analytics-integration"></a>Integração de análises do ambiente de trabalho

Captura de ecrã seguinte do Analytics de ambiente de trabalho apresenta os detalhes do ContosoApp versão 1.15.25. 
- Ele tem um **médio** avaliação de riscos  
- Está disponível uma versão adotada  
- Ele tem uma dependência de driver  

![Análise de área de trabalho que mostra os fatores de risco de compatibilidade de uma aplicação](media/aha-desktop-analytics-compat-risk-factors.png)



## <a name="troubleshooting"></a>Resolução de Problemas

Esta secção abrange os passos de resolução de problemas e os problemas operacionais mais comuns que poderá ver com o analisador de estado de funcionamento da aplicação. Por exemplo:

- Não vir o ecrã de boas-vindas no analisador de estado de funcionamento da aplicação  

- Existem aplicações instaladas no dispositivo, mas não vir quaisquer informações no relatório de preparação de aplicação  

- Não acontece nada quando executar a ferramenta  


#### <a name="diagnostic-data-settings"></a>Definições de dados de diagnóstico
Verifique novamente as configurações para definições de dados de diagnóstico do Windows. O Configuration Manager deve defina estes valores quando carrega o dispositivo à área de trabalho de análise. Pode utilizar outros métodos, como a política de grupo ou de script como uma solução alternativa. Para obter mais informações, consulte [níveis de dados de diagnóstico](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels).  

#### <a name="verbose-mode"></a>Modo verboso
Execute a ferramenta no modo verboso com o script de run_verbose.cmd. Por predefinição, o script é no seguinte caminho: `C:\Program Files\Microsoft Corporation\Microsoft App Health Analyzer\run_verbose.cmd`

Modo verboso gera registos adicionais, os quais podem ajudar a resolver os problemas potenciais. Este guarda os registos para o `LogCollection` pasta na localização instalada. Por exemplo, o caminho predefinido da coleção de registo é: `C:\Program Files\Microsoft Corporation\Microsoft App Health Analyzer\LogCollection\`

<!--Send the logs to AHASupport, who will follow up for further investigations. --do we really want to include this in public documentation?-->

