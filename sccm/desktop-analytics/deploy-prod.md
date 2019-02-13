---
title: Como implementar em produção
titleSuffix: Configuration Manager
description: Um guia de procedimentos para implementar num grupo de produção de análise de ambiente de trabalho.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 637fbd8e-b8ea-4c7e-95ee-a60a323c496e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 599da20674c581501d69333f85ad0e91ee158da2
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56124718"
---
# <a name="how-to-deploy-to-production-with-desktop-analytics"></a>Como implementar em produção com a análise de ambiente de trabalho

> [!Note]  
> Estas informações se relaciona com o serviço de pré-visualização que pode ser substancialmente modificado antes do lançamento comercial. A Microsoft faz não oferece quaisquer garantias, expressas ou implícitas, quanto às informações fornecidas aqui.  

Depois que [implementada para piloto](/sccm/desktop-analytics/deploy-pilot) e rever o estado dos seus recursos, está pronto para atualizar o resto do seu ambiente de produção. 

[!INCLUDE [Definition of pilot and production](includes/define-pilot-prod.md)]


Existem três partes principais para realizar a implantação de atualizações para dispositivos de produção:

1. [Reveja os recursos de que precisam de uma decisão de atualização](#bkmk_review): Para tornar os dispositivos prontos para a implantação de produção, seus ativos (aplicações, aplicações do Office, os suplementos do Office e macros do Office) tem de ter sua decisão de atualização definido como **pronto** ou **pronto, a remediações necessárias**.  

2. [Implementar em dispositivos que estão prontos](#bkmk_deploy): Utilize o Gestor de configuração para atualizar os dispositivos que estão prontos. A análise de área de trabalho fornece a lista de dispositivos prontos para implantação em produção e relatórios para monitorizar o êxito da implementação.  

3. [Monitorizar o estado de funcionamento de dispositivos atualizados](#bkmk_monitor): Conforme o andamento da implementação de atualização, monitorizar o estado de funcionamento ativos importantes. Se alguns que necessitam de atenção, solucionar problemas e corrigir esses problemas. Se decidir não não possível corrigir os problemas, parar a implementação nos dispositivos afetados, definindo as respetivas decisão de atualização **não é possível**.  

> [!NOTE]  
> Quando estiver confiam o sucesso da implantação piloto, inicie a implementação de produção em qualquer altura. Não é necessário que todos os dispositivos pilotos alcance o estado "concluído" em primeiro lugar.  



## <a name="bkmk_review"></a> Reveja os recursos de que precisam de uma decisão de atualização

Análise de área de trabalho orienta-o pelo processo de revisão de seus ativos para a implementação de produção. No portal do Azure, aceda a **planos de implantação**, selecione um plano de implantação e, em seguida, selecione **preparar produção** no menu à esquerda.

![Vista de preparar captura de ecrã de produção no ambiente de trabalho de análise](media/prepare-production.png)

Reveja o estado de aplicações, aplicações do Office, os suplementos do Office e macros do Office. Utilize essas informações para definir o decisão de atualização para cada um desses ativos.

Utilize cada um dos separadores para rever o estado de aplicações, aplicações do Office, os suplementos do Office e macros do Office. Em cada vista com separadores, pode filtrar os resultados para mostrar os dispositivos que estão no caminho certo para a atualização, tem de sua atenção, os dispositivos com resultados misturados e esses dispositivos num Estado indeterminado.

O **Macros do Office** vista mostra as consultorias de relacionados com o arquivo habilitado para macro. Ele não mostra os arquivos reais habilitado para macro. Selecione uma recomendação específica para ver detalhes adicionais. <!-- You can also export this list for later use, such as to run the Readiness Toolkit on this subgroup for still more detail about reported issues like the names of the files for which the advisories were raised. -->

Selecione **objetivos de reunião** para filtrar a vista para ativos que são provavelmente pronto para implantação de produção com base nos seguintes critérios:

- : Uma pré-atualização avaliação de risco dos riscos conhecidos para atualizar os dispositivos que tenham este recurso instalado  

- Estado de funcionamento: uma avaliação após a atualização dos dispositivos em outras implementações e se eles experimentado problemas após a atualização foi instalada. Para obter mais informações sobre o estado de funcionamento, consulte [monitorizar o estado de funcionamento de dispositivos atualizados](#montor-the-health-of-updated-devices).  

Para aprovar um recurso de atualização, selecione o nome na lista e, em seguida, selecione uma das seguintes opções do **decisão de atualização** lista:
- Revisão em curso
- Pronto
- Pronto (com a remediação)
- Não é possível
- Não revisto

Para definir este valor para várias aplicações ao mesmo tempo, utilize a primeira coluna **Selecione este item**e, em seguida, escolha **definir decisão atualizar**. 

![Definir a opção de atualizar decisão em várias aplicações](media/prep-prod-set-upgrade-decision.png)

Selecione **nenhum dado** a recursos de exibição que não foi possível ser classificados. Esses ativos são geralmente ativos que não têm suficiente cobertura para análise de ambiente de trabalho executar uma análise do Estado de risco ou estado de funcionamento. Para melhorar a cobertura, adicionar dispositivos adicionais com estes recursos para o piloto ou peça aos utilizadores pilotos para experimentar esses recursos.

Poderá também estar ativos no **atenção necessária** ou **resultados misturados** estado. Estes recursos podem exigir revisão adicional antes de tomar uma decisão de atualização para os mesmos. 

Reveja todas as aplicações, aplicações do Office e os suplementos do Office. Após um determinado dispositivo tem uma decisão de atualização positiva para todos os recursos, em seguida, seu estado é alterado para "pronto para produção." Ver a contagem atual na página principal para o plano de implementação ao selecionar o terceiro passo de implementação **Deploy**.



## <a name="bkmk_deploy"></a> Implementar em dispositivos que estão prontos

O Configuration Manager utiliza os dados da análise de ambiente de trabalho para criar uma coleção para a implementação de produção. Não implemente a sequência de aplicativo ou uma tarefa através de uma implementação tradicional. Utilize o procedimento seguinte para criar uma implementação integrada de análise de ambiente de trabalho:

1. Na consola do Configuration Manager, vá para o **biblioteca de Software**, expanda **manutenção de análise de ambiente de trabalho**e selecione o **planos de implantação** nó.  

2. Selecione o seu plano de implementação e, em seguida, selecione **detalhes do plano de implementação** na faixa de opções.  

3. Na **estado de produção** mosaico, selecione um dos seguintes tipos de objeto da lista pendente:  

    - **Aplicação** para o Office 365 ProPlus  

    - **Sequência de tarefas** para o Windows 10  
  
   Selecione **implementar**. Esta ação inicia o Assistente para implementar Software para o tipo de objeto selecionado. 


Para obter mais informações, veja os artigos seguintes:  

- [Implementar uma aplicação](/sccm/apps/deploy-use/deploy-applications#bkmk_deploy)  

- [Implementar uma sequência de tarefas](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS)  


Se o seu plano de implementação do Windows 10 e Office 365, repita este processo para criar uma segunda implementação. Por exemplo, se for a primeira implementação para a sequência de tarefas, crie uma segunda implementação para a aplicação.


### <a name="address-deployment-alerts"></a>Alerta de implementação do endereço

Como com a implementação piloto, análise de ambiente de trabalho aconselha de quaisquer problemas que precisam da sua atenção durante a implementação de produção. Na área de trabalho de análise, vá para o plano de implantação e selecione **estado de implementação** no menu à esquerda. A vista de estado de implementação apresenta uma lista de dispositivos nas seguintes categorias:  

- Não iniciadas
- Em curso
- Concluída
- Necessita de atenção - dispositivos (classificados por nome de dispositivo)
- Necessita de atenção - problemas (classificados por tipo de problema)

![Produção de análise de captura de ecrã da área de trabalho estado da implementação](media/prod-deployment-status.png)



## <a name="bkmk_monitor"></a> Monitorizar o estado de funcionamento de dispositivos atualizados

O **preparar produção** página se concentra em ajudar a tornar a atualização de decisões para os seus ativos. Essa página por predefinição mostra apenas esses ativos que não estão ainda na **pronto** estado. O **monitorizar o estado de funcionamento** página apresenta problemas de estado de funcionamento em qualquer recurso digno de nota, mesmo os recursos que estão marcados **pronto**. Se descobrir problemas, que pode resolver problemas e corrigir o problema ou altere a decisão de atualização de **não é possível**. Quando altera o decisão de atualização, esta ação impede que as atualizações futuras em dispositivos com esse recurso.

Filtre esta página por recursos com os seguintes Estados de funcionamento:

| Filtro de estado de funcionamento | Descrição |
|----------------------|-------------|
| **Atenção necessária** | (Filtro predefinido) Ambiente de trabalho Analytics Deteta uma regressão estatisticamente significativa para algumas métricas de estado de funcionamento para esse recurso
| **Objetivos da reunião** | Análise de área de trabalho Deteta não regressão de comportamento |
| **Dados insuficientes** | Análise de área de trabalho não tem dados suficientes sobre esse recurso para efetuar recomendações |
| **Sem dados** | Não existem dados de utilização ainda está disponível para este recurso | 

Para mostrar uma vista não filtrada de todos os ativos, selecione o filtro atual. Esta ação remove esse filtro.

> [!NOTE]  
> Para reduzir o número de ativos com dados insuficientes, análise de ambiente de trabalho monitoriza os ativos em todos os seus dispositivos que tenham atualizado para o Windows de destino ou a versão do Office especificada no seu plano de implementação. Estes dispositivos incluem os não incluídos no plano de implantação específicos.  

A ordem de classificação padrão é o número de dispositivos que tenha tido um incidente com esse recurso em questão, para que possa ver rapidamente quais as que estão a causar a maior parte dos problemas. Por exemplo, ao exibir **aplicações**, ordena por **duas últimas semanas de falhas de dispositivos com aplicação**.

Se desejar examinar o estado de funcionamento de todos os recursos, mesmo os recursos com dados insuficientes para análise de ambiente de trabalho fazer inferências estatísticas, utilize o seguinte processo:

1. Selecione o menu suspenso na **dispositivos com incidentes nas últimas duas semanas** coluna. Adicione um filtro a apenas esses ativos que tenham tido a incidentes algum número mínimo de dispositivos para que seja interessante. Por exemplo, mostrar os itens com valores **superior a** 100.  

2. Selecione o menu suspenso na **% de dispositivos com incidentes nas últimas duas semanas** coluna e selecionar a opção para ordenar por **descendente**.  

    O modo de exibição resultante mostra os ativos com a tarifa mais elevada de incidente com um número mínimo de incidentes.  

3. Selecione um recurso para obter mais detalhes ou alterar a sua decisão de atualização.  


Para obter mais informações, consulte [monitorização de estado de funcionamento](/sccm/desktop-analytics/health-status-monitoring).
