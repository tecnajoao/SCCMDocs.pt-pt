---
title: Monitorizar conteúdo
titleSuffix: Configuration Manager
description: Compreenda como monitorizar conteúdo distribuído ao utilizar a consola do Configuration Manager.
ms.date: 12/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 82e8a693-9adf-4ca3-8484-7e101c34c7c1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 44ddf230d33759787636e88f6edcdd79744fd7b2
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32338929"
---
# <a name="monitor-content-you-have-distributed-with-system-center-configuration-manager"></a>Monitorizar o conteúdo que distribuiu com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize a consola do System Center Configuration Manager para monitorizar conteúdo distribuído, incluindo:  

-   O estado de todos os tipos de pacotes relativamente aos pontos de distribuição associados.  
-   O estado de validação de conteúdo para o conteúdo num pacote.  
-   O estado dos conteúdos atribuídos a um grupo de pontos de distribuição específico.  
-   O estado dos conteúdos atribuídos a um ponto de distribuição.  
-   O estado das funcionalidades opcionais de cada ponto de distribuição (validação de conteúdo, PXE e multicast).  

> [!NOTE]  
>  O Configuration Manager monitoriza apenas o conteúdo no ponto de distribuição que está na biblioteca de conteúdos. Conteúdo armazenado no ponto de distribuição no pacote ou partilhas personalizadas não é monitorizado.  

##  <a name="BKMK_ContentStatus"></a> Monitorização do estado do conteúdo  
 O nó **Estado do Conteúdo** da área de trabalho **Monitorização** disponibiliza informações sobre pacotes de conteúdos. Na consola do Configuration Manager, pode rever informações como:  

-   O nome do pacote.  
-   O tipo.  
-   Pontos de distribuição quantos um pacote foi enviado para o.  
-   A taxa de conformidade.  
-   Quando o pacote foi criado.  
-   ID de pacote.  
-   A versão de origem.  

Encontrará também informações de estado detalhadas para qualquer pacote, bem como o estado de distribuição para o pacote, incluindo:  

-   O número de falhas.  
-   Distribuições pendentes.  
-   O número de instalações.

Também pode gerir as distribuições que continuam em curso para um ponto de distribuição ou que falhou ao distribuir o conteúdo para um ponto de distribuição com êxito:  

-   A opção para cancelar ou redistribuir conteúdos está disponível quando visualiza a mensagem de estado de implementação de uma tarefa de distribuição para um ponto de distribuição no **detalhes do ativo** painel. Neste painel, pode ser encontrado no **em curso** separador ou **erro** separador do **estado do conteúdo** nó.  
-   Além disso, os detalhes da tarefa apresentam a percentagem do trabalho que foi concluída quando visualiza detalhes de uma tarefa no **em curso** separador. Os detalhes da tarefa também apresentam o número de tentativas que restam para uma tarefa, bem como tempo antes da próxima nova tentativa ocorre quando visualiza detalhes de uma tarefa que está disponível a partir de **erro** separador.  

Se cancelar uma implementação que ainda não está concluída, interrompe a tarefa de distribuição para transferência desse conteúdo:  

-   O estado da implementação será então atualizado para indicar que a distribuição falhou e que foi cancelada por uma ação do utilizador.  
-   Este novo estado é apresentado no **erro** separador.  

> [!TIP]  
>  Quando uma implementação estiver próxima da conclusão, é possível que a ação de cancelamento dessa distribuição não irá processar antes da conclusão da distribuição para o ponto de distribuição. Se isto ocorre, a ação de cancelamento da implementação é ignorada e o estado da implementação apresenta conclusão com êxito.  

> [!NOTE]  
>  Embora possa selecionar a opção para cancelar uma distribuição a um ponto de distribuição que está localizado num servidor do site, isto não tem qualquer efeito. Isto acontece porque o servidor do site e a pontos de distribuição numa partilha de servidor do site o mesmo arquivo de conteúdo de instância única. Não há nenhuma tarefa de distribuição existente para cancelar.  

Quando redistribuir conteúdos cuja transferência para um ponto de distribuição falhado anteriormente, o Configuration Manager começa imediatamente a reimplementação desse conteúdo ao ponto de distribuição. O Configuration Manager atualiza o estado da implementação para refletir o estado dessa reimplementação.  

Utilize os procedimentos seguintes para ver o estado do conteúdo e gerir as distribuições que continuam em curso ou que falharam.  

### <a name="to-monitor-content-status"></a>Para monitorizar o estado do conteúdo  

1.  Na consola do Configuration Manager, clique em **monitorização**.  

2.  No **monitorização** área de trabalho, expanda **estado da distribuição**e, em seguida, clique em **estado do conteúdo**. Os pacotes são apresentados.  

3.  Selecione o pacote que pretende obter informações detalhadas de estado.  

4.  No separador **Home Page** , clique em **Ver Estado**. São apresentadas informações de estado detalhadas sobre o pacote.  

### <a name="to-cancel-a-distribution-that-remains-in-progress"></a>Para cancelar uma distribuição que continua em curso  

1.  Na consola do Configuration Manager, clique em **monitorização**.  

2.  No **monitorização** área de trabalho, expanda **estado da distribuição**e, em seguida, clique em **estado do conteúdo**. Os pacotes são apresentados.  

3.  Selecione o pacote que pretende gerir e, em seguida, no painel de detalhes, clique em **Ver estado**.  

4.  No **detalhes do ativo** painel do **em curso** separador, faça duplo clique na entrada de distribuição que pretende cancelar e selecione **Cancelar**.  

5.  Clique em **Sim** para confirmar a ação e cancelar a tarefa de distribuição a esse ponto de distribuição.  

### <a name="to-redistribute-content-that-failed-to-distribute"></a>Para redistribuir conteúdos que falhou ao distribuir  

1.  Na consola do Configuration Manager, clique em **monitorização**.  

2.  No **monitorização** área de trabalho, expanda **estado da distribuição**e, em seguida, clique em **estado do conteúdo**. Os pacotes são apresentados.  

3.  Selecione o pacote que pretende gerir e, em seguida, no painel de detalhes, clique em **Ver estado**.  

4.  No **detalhes do ativo** painel do **erro** separador, faça duplo clique na entrada de distribuição que pretende redistribuir e selecione **redistribuir**.  

5.  Clique em **Sim** para confirmar a ação e iniciar o processo de redistribuição a esse ponto de distribuição.  

## <a name="distribution-point-group-status"></a>Estado do grupo de pontos de distribuição  
O nó **Estado do Grupo de Pontos de Distribuição** na área de trabalho **Monitorização** fornece informações acerca dos grupos de pontos de distribuição. Pode rever informações como:  

-   O nome de grupo de ponto de distribuição.  
-   A descrição.  
-   Quantos pontos de distribuição sejam membros da distribuição de um grupo de pontos.  
-   O número de pacotes que foram atribuído ao grupo.  
-   O estado de grupo de pontos de distribuição.  
-   A taxa de conformidade.  

Também ver informações detalhadas de estado para o seguinte:  

-   Erros para o grupo de pontos de distribuição.  
-   Quantas distribuições estão em curso.
-   Quantos tiverem sido distribuídos com êxito.  

### <a name="to-monitor-distribution-point-group-status"></a>Para monitorizar o estado do grupo de pontos de distribuição  

1.  Na consola do Configuration Manager, clique em **monitorização**.  

2.  No **monitorização** área de trabalho, expanda **estado da distribuição**e, em seguida, clique em **estado do grupo de pontos de distribuição**. Os grupos de pontos de distribuição são apresentados.  

3.  Selecione o grupo de pontos de distribuição que pretende obter informações detalhadas de estado.  

4.  No separador **Home Page** , clique em **Ver Estado**. São apresentadas informações detalhadas de estado para o grupo de pontos de distribuição.  

## <a name="distribution-point-configuration-status"></a>Estado da configuração de ponto de distribuição  
 O nó **Estado da Configuração do Ponto de Distribuição** na área de trabalho **Monitorização** fornece informações acerca do ponto de distribuição. Pode rever quais os atributos que estão ativados para o ponto de distribuição, como PXE, multicast, conteúdo validação e o estado de distribuição para o ponto de distribuição. Também pode ver informações detalhadas de estado para o ponto de distribuição.  

> [!WARNING]  
>  Estado de configuração de ponto de distribuição é relativo para as últimas 24 horas. Se o ponto de distribuição tem um erro e recuperar, o estado de erro pode ser apresentado até 24 horas depois do ponto de distribuição recuperar.  

Utilize o seguinte procedimento para ver o estado da configuração do ponto de distribuição.  

### <a name="to-monitor-distribution-point-configuration-status"></a>Para monitorizar o estado da configuração do ponto de distribuição  

1.  Na consola do Configuration Manager, clique em **monitorização**.  

2.  No **monitorização** área de trabalho, expanda **estado da distribuição**e, em seguida, clique em **estado de configuração de ponto de distribuição**. Os pontos de distribuição são apresentados.  

3.  Selecione o ponto de distribuição para o qual pretende que as informações de estado do ponto de distribuição.  

4.  No painel de resultados, clique no separador **Detalhes** . São apresentadas informações de estado para o ponto de distribuição.  

## <a name="client-data-sources-dashboard"></a>Dashboard de origens de dados de cliente
A partir da versão 1610, pode utilizar o **origens de dados de cliente** dashboard para ajudar a compreender a utilização de [Cache ponto a ponto](/sccm/core/plan-design/hierarchy/client-peer-cache) no seu ambiente. O dashboard será iniciada a apresentar dados depois dos clientes transferem conteúdo e o relatório de informações de volta para o site. Esta operação pode demorar até 24 horas.

> [!TIP]  
> **A Cache do cliente** e **origens de dados de cliente** dashboard foram primeiro introduzidas na versão 1610 como [funcionalidades de pré-lançamento](/sccm/core/servers/manage/pre-release-features). A partir da versão 1710, estas funcionalidades são já não são funcionalidades de pré-lançamento. Tem de ativar a Cache do cliente para que o dashboard de origens de dados de cliente fica visível na consola.


Na consola, aceda a **monitorização** > **estado da distribuição** > **origens de dados de cliente**. Aqui, pode selecionar um período de tempo para aplicar ao dashboard. Em seguida, no ecrã, pode selecionar o grupo de limites ou o pacote para o qual pretende ver informações. Ao visualizar informações, pode pairar o rato sobre a superfície de para ver mais detalhes sobre o conteúdo diferente ou origens de política.

Os detalhes incluem o seguinte:  
- **Origens de conteúdo de cliente**: Apresenta a partir da qual os clientes recebeu conteúdos de origem.
- **Pontos de distribuição**: Mostra o número de pontos de distribuição que fazem parte do grupo de limites selecionado.
- **Clientes que utilizar um ponto de distribuição**: O número de clientes que estejam no grupo de limites selecionado, esta ação mostra quantos um ponto de distribuição utilizado para aceder a conteúdo.
- **Elemento origens de Cache**: Para o grupo de limites selecionado, esta ação mostra quantos origens de cache ponto a ponto relataram histórico de transferências.
- **Clientes que é utilizado um elemento**: O número de clientes que estejam no grupo de limites selecionado, mostra quantos utilizado uma origem de cache ponto a ponto para aceder a conteúdo.



Também pode utilizar um novo relatório, **origens de dados de cliente - resumo**, para ver um resumo das origens de dados de cliente para cada grupo de limites.
