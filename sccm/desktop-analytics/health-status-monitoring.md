---
title: Monitorização de estado de funcionamento
titleSuffix: Configuration Manager
description: Saiba mais sobre como a monitorização de estado de funcionamento funciona no ambiente de trabalho de análise.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 343dbe2a-597c-4719-b7ac-45b1f39b49ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: fcdeab9ff33fefb0340edda5de63bf26ec1ecd1e
ms.sourcegitcommit: ad25a7bdd983c5a0e4c95bffdc61c9a1ebcbb765
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/26/2019
ms.locfileid: "55073393"
---
# <a name="health-status-monitoring-in-desktop-analytics"></a>Análise de ambiente de trabalho de monitorização de estado de funcionamento

Como [implante uma atualização para a produção](/sccm/desktop-analytics/deploy-prod), utilize a análise de ambiente de trabalho para ajudar a monitorizar o estado de funcionamento dos seus dispositivos. Este artigo explica em detalhe como funciona a monitorização de estado de funcionamento.

Para obter mais informações sobre como utilizar esta funcionalidade, consulte [monitorizar o estado de funcionamento de dispositivos atualizados](/sccm/desktop-analytics/deploy-prod#bkmk_monitor).

![Captura de ecrã da página de estado de funcionamento do Monitor de análise de ambiente de trabalho](media/monitor-health.png)

> [!NOTE]  
> Análise de área de trabalho só recolhe dados de estado de funcionamento a partir de dispositivos que fornecem dados de utilização, que pode utilizar como um denominador. Isso significa que ele não inclui dispositivos que executam o Windows 7 e Windows 10 que não estão definidos para partilhar dados de diagnóstico no nível avançado (limitado). Se mais de 10% dos dispositivos com o Windows 10 estiverem definidas para partilhar dados de diagnóstico em níveis que não seja avançado (limitado), o **monitorizar o estado de funcionamento** página apresenta um aviso na área de faixa.  

Para ver mais informações sobre uma aplicação específica, suplementos ou macro consultiva e selecione-a na lista. 



## <a name="apps-and-office-apps"></a>Aplicações e aplicações do Office

![Fatores de estado de funcionamento para uma aplicação no ambiente de trabalho de análise](media/monitor-health-status-factors.png)

Ambiente de trabalho Analytics monitoriza os seguintes fatores de estado de funcionamento para aplicações e aplicações do Office:

- **% Dispositivos com falhas**: Para as duas últimas semanas, o número de dispositivos em que esta aplicação específica falhar dividido pelo número de dispositivos em que a aplicação foi utilizada. Esta vista permite que veja se a estabilidade da aplicação tem aumenta ou diminui a nova versão de SO. Ambiente de trabalho Analytics calcula esta percentagem para os seguintes conjuntos:  

    - **Após a atualização**: Dispositivos que tem atualizado para a versão de SO de destino especificada no plano de implantação. Para reduzir o número de ativos com dados insuficientes, o ambiente de trabalho de análise recolhe estes dados para todos os seus dispositivos atualizados. Este conjunto inclui esses dispositivos não no plano de implantação.  

    - **Antes da atualização**: Dispositivos que estão a utilizar uma versão de SO anterior ao que é especificado no plano de implantação. Esta lista não inclui os dispositivos que executam o Windows 7.   

    - **Média comercial**: A média (média) de taxa de falhas em todos os dispositivos comerciais. Esta média é calculada entre *todos os* versões da aplicação. Se a sua versão mostra uma taxa de falhas acima da média comercial, pode haver uma versão estável mais disponível.  

- **% Sessões com falhas**: Semelhante para o anterior, mas contagens a percentagem de sessões com falhas nas últimas duas semanas.  

Para determinar o estado de funcionamento de uma aplicação, análise de ambiente de trabalho requer que os dados de, pelo menos, 20 dispositivos. Caso contrário, reporta **dados insuficientes** para a aplicação. O serviço calcula o estado de funcionamento com base na *taxa de falhas de sessão* partir destes dispositivos. A taxa de falhas de dispositivos é fornecida apenas para informação. Ele não é usado no cálculo de estado de funcionamento.

Na parte inferior da página de detalhes da aplicação, os três separadores seguintes podem ajudar a resolver problemas:

- **Outras versões**: Uma lista das versões alternativas desta aplicação. Para cada versão, ele mostra as alterações relativas as taxas de falhas dentro da sua organização e a média comercial. Se encontrar uma versão posterior da aplicação com uma menor taxa de falhas, atualizar a aplicação pode ajudar.  

    Ela também mostra se a versão tem um **pronto para Windows** sinal. Para obter mais informações, consulte [risco de compatibilidade das aplicações de Windows](/sccm/desktop-analytics/compat-risk#risk-assessment-engine).  

- **Principais problemas**: Uma lista da falha mais frequente IDs por contagem de instâncias. Um ID de falha identifica o rastreio de pilha associado com a falha. Pode utilizar este ID quando chama o fornecedor da aplicação para o suporte.  

- **Falhas recentes**:  Uma lista de dispositivos em que a aplicação recentemente falhados. Pode filtrar por ID de falha e outros critérios. Utilize estas informações para resolver o problema por recolha de registos ou tentar correções em dispositivos específicos antes de tentar uma implementação mais abrangente.  

Se encontrar uma regressão de estado de funcionamento graves que não for possível corrigir, alterar a aplicação **decisão de atualização** ao **não é possível**. Esta ação impede a implementação futura da atualização para dispositivos com este recurso.



## <a name="office-add-ins"></a>Suplementos do Office

![Captura de ecrã de fatores de estado de funcionamento para um suplemento do Office](media/office-add-in-health-status-factors.png)

Ambiente de trabalho Analytics monitoriza os seguintes fatores de estado de funcionamento para os suplementos do Office:

- **% Dispositivos com incidentes**: Um incidente é algo que impede que um suplemento a funcionar corretamente. Por exemplo, não conseguir carregar ou deixar de responder. Esta secção mostra, para as últimas duas semanas, o número de dispositivos em que o suplemento selecionado tinha um incidente dividido pelo número de dispositivos em que o suplemento está instalado. Ambiente de trabalho Analytics calcula esta percentagem para os seguintes conjuntos:  

    - **Após a atualização**: Dispositivos que tem atualizado para a versão do Office de destino especificada no plano de implantação. Para reduzir o número de ativos com dados insuficientes, o ambiente de trabalho de análise recolhe estes dados para todos os seus dispositivos atualizados. Este conjunto inclui esses dispositivos não no plano de implantação.  

    - **Antes da atualização**: Dispositivos com qualquer versão do Office anterior à versão que a implementação do plano de destinos. <!-- This does not include {include min version of Office}  --> Para avaliar o estado de funcionamento do add-in, compare esta métrica para o **após a atualização** percentagem.  

    - **Média comercial**: A taxa de incidentes média (média) em todos os dispositivos comerciais que utilizam a mesma versão do suplemento na mesma versão do Office. Utilize essa taxa de comparação de dispositivos na sua organização. Se esta versão do suplemento é ter uma taxa elevada de incidente que a média comercial, pode ter alguns fatores ambientais que contribuem para os incidentes.  

- **% Sessões com incidentes**: Semelhante para o anterior, mas contagens a percentagem de sessões com falhas nas últimas duas semanas.  

Para determinar o estado de funcionamento dos suplementos, o ambiente de trabalho de análise requer, pelo menos, três dispositivos para a taxa de incidentes do dispositivo e, pelo menos, 10 sessões para a taxa de incidente de sessão. Para ambas as taxas, ele compara os valores para determinar se existe uma regressão antes e depois. Não existem regressão é considerado em direção a cumprir os objetivos. 

Ambiente de trabalho Analytics calcula o estado de funcionamento geral do suplemento do Office com base numa combinação de dispositivo e sessão de taxas de incidentes usando a matriz seguinte:

|  | Dados insuficientes para falhas de dispositivo  | Métricas de falhas de dispositivo em bom estado | Regressão nas métricas de falhas de dispositivo |
|----------------|---------------------|-----------------------|------------------------|
| **Dados insuficientes para as sessões com incidentes**| Dados insuficientes| Objetivos da reunião | Dados insuficientes |
| **Métricas de bom estado de funcionamento de sessões com incidentes** | Objetivos da reunião | Objetivos da reunião | Objetivos da reunião |
| **Regressão nas métricas para as sessões com incidentes** | Dados insuficientes | Objetivos da reunião | Atenção necessária |


A página de detalhes do suplemento do Office também inclui os seguintes detalhes para ajudar a resolver: 

- **Incidentes recentes**: Uma lista dos dispositivos em que um incidente de suplemento ocorreu recentemente. Utilize esta lista para resolver o problema por recolha de registos ou tentar correções nesses dispositivos específicos antes de tentar uma implementação mais abrangente.  



## <a name="office-macros"></a>Macros do Office

![Captura de ecrã de fatores de estado de funcionamento para uma macro do Office consultoria](media/office-macros-health-status-factors.png)

Estado de funcionamento de relatórios de análise de área de trabalho no *consultorias de macro*. As consultorias de macro são problemas potenciais detetados nos ficheiros do Office com macros contêm. Estes problemas são específicos para uma aplicação do Office. Por exemplo, Word, Excel, PowerPoint ou Visio. 

Ambiente de trabalho Analytics monitoriza os seguintes fatores de estado de funcionamento para macros do Office:

- **% Dispositivos com o erro de compilação**: Para as últimas duas semanas, o número de dispositivos nos quais erros relacionados com o aconselhamento ocorreu durante a ativação de macro dividida pelo número de dispositivos nos quais foi detetada a consultoria. Ambiente de trabalho Analytics calcula esta percentagem para os seguintes conjuntos: 

    - **Após a atualização**: Os dispositivos em que a versão do Office é o mesmo como destino o plano de implantação  

    - **Antes da atualização**: Os dispositivos que executam qualquer versão do Office mais antiga que o destino o plano de implantação  

    - **Média comercial**: A média (média) de todos os dispositivos comerciais, executar a mesma versão do Office como destino o plano de implantação  

- **% Dispositivos com o erro de tempo de execução** é semelhante ao anterior, mas para as últimas duas semanas, os dispositivos nos quais erros relacionados com o aconselhamento ocorreram durante a execução de macro dividida pelo número de dispositivos nos quais foi detetada a consultoria.  

A página de detalhes de macros do Office também inclui os seguintes detalhes para ajudar a resolver: 

- **Incidentes recentes**: Uma lista de dispositivos em que macro erros de tempo de execução e compilação ocorreram recentemente. Utilize esta lista para resolver o problema por recolha de registos ou tentar correções nesses dispositivos específicos antes de tentar uma implementação mais abrangente.



## <a name="see-also"></a>Consulte também

- [Risco de compatibilidade de aplicações do Windows no ambiente de trabalho de análise](/sccm/desktop-analytics/compat-risk)  

- [Como implementar em produção com a análise de ambiente de trabalho](/sccm/desktop-analytics/deploy-prod)  
