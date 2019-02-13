---
title: Monitorizar conteúdos
titleSuffix: Configuration Manager
description: Saiba como monitorizar conteúdo distribuído ao utilizar a consola do Configuration Manager.
ms.date: 12/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 82e8a693-9adf-4ca3-8484-7e101c34c7c1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f6bc81a1aa6d8464094195c33faeecfeaf2d46f0
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56123935"
---
# <a name="monitor-content-you-have-distributed-with-system-center-configuration-manager"></a>Monitorizar conteúdo distribuído com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilizar a consola do System Center Configuration Manager para monitorizar conteúdo distribuído, incluindo:  

-   O estado de todos os tipos de pacotes relativamente aos pontos de distribuição associados.  
-   O estado de validação de conteúdo para o conteúdo num pacote.  
-   O estado dos conteúdos atribuídos a um grupo de pontos de distribuição específico.  
-   O estado dos conteúdos atribuídos a um ponto de distribuição.  
-   O estado das funcionalidades opcionais de cada ponto de distribuição (validação de conteúdo, PXE e multicast).  

> [!NOTE]  
>  O Configuration Manager monitoriza apenas o conteúdo num ponto de distribuição que esteja na biblioteca de conteúdos. Conteúdo armazenado no ponto de distribuição no pacote ou partilhas personalizadas não é monitorizado.  

##  <a name="BKMK_ContentStatus"></a> Monitorização do estado do conteúdo  
 O nó **Estado do Conteúdo** da área de trabalho **Monitorização** disponibiliza informações sobre pacotes de conteúdos. Na consola do Configuration Manager, pode rever informações como:  

-   O nome do pacote.  
-   O tipo.  
-   Pontos de distribuição quantos um pacote foi enviado para.  
-   A taxa de conformidade.  
-   Quando o pacote foi criado.  
-   O ID do pacote.  
-   A versão de origem.  

Encontrará também informações de estado detalhadas para qualquer pacote, bem como o estado de distribuição para o pacote, incluindo:  

-   O número de falhas.  
-   Distribuições pendentes.  
-   O número de instalações.

Também pode gerir as distribuições que continuam em curso para um ponto de distribuição ou não tenha sido distribuído conteúdo a um ponto de distribuição com êxito:  

-   A opção para cancelar ou redistribuir o conteúdo está disponível quando visualiza a mensagem de estado de implementação de uma tarefa de distribuição para um ponto de distribuição no **detalhes do ativo** painel. Neste painel pode ser encontrado em qualquer um de **em curso** separador ou o **erro** separador do **estado do conteúdo** nó.  
-   Além disso, os detalhes da tarefa apresentam a percentagem da tarefa que está concluída quando visualizar os detalhes de uma tarefa no **em curso** separador. Os detalhes da tarefa também exibem o número de tentativas restantes para uma tarefa, bem como a forma como tempo restante até a próxima tentativa quando visualizar os detalhes de uma tarefa que está disponível a partir da **erro** separador.  

Quando cancela uma implementação que ainda não está concluída, interrompe a tarefa de distribuição para transferência desse conteúdo:  

-   O estado da implementação será então atualizado para indicar que a distribuição falhou e que foi cancelada por uma ação do utilizador.  
-   Este novo estado é apresentado no **erro** separador.  

> [!TIP]  
>  Quando uma implementação estiver quase concluída, é possível que a ação de cancelamento dessa distribuição não irá processar antes da conclusão da distribuição ao ponto de distribuição. Quando isto ocorrer, a ação de cancelamento da implementação é ignorada e o estado da implementação apresenta conclusão com êxito.  

> [!NOTE]  
>  Embora possa selecionar a opção de cancelar uma distribuição a um ponto de distribuição que esteja localizado num servidor do site, isto não tem qualquer efeito. Isto acontece porque o servidor do site e a ponto de distribuição numa partilha de servidor do site o mesmo arquivo de conteúdo de instância única. Não há nenhuma tarefa de distribuição existente para cancelar.  

Se redistribuir conteúdos que anteriormente não conseguiu transferir para um ponto de distribuição, o Configuration Manager começa imediatamente a Reimplementar esse conteúdo ao ponto de distribuição. O Configuration Manager atualiza o estado da implementação para refletir o estado atual de que a reimplementação.  

Utilize os procedimentos seguintes para ver o estado do conteúdo e gerir as distribuições que continuam em curso ou que falhou.  

### <a name="to-monitor-content-status"></a>Para monitorizar o estado do conteúdo  

1.  Na consola do Configuration Manager, clique em **monitorização**.  

2.  Na **monitorização** área de trabalho, expanda **estado de distribuição**e, em seguida, clique em **estado do conteúdo**. Os pacotes são apresentados.  

3.  Selecione o pacote para o qual pretende obter informações detalhadas de estado.  

4.  No separador **Home Page** , clique em **Ver Estado**. São apresentadas informações de estado detalhadas sobre o pacote.  

### <a name="to-cancel-a-distribution-that-remains-in-progress"></a>Para cancelar uma distribuição que continua em curso  

1.  Na consola do Configuration Manager, clique em **monitorização**.  

2.  Na **monitorização** área de trabalho, expanda **estado de distribuição**e, em seguida, clique em **estado do conteúdo**. Os pacotes são apresentados.  

3.  Selecione o pacote que pretende gerir e, em seguida, no painel de detalhes, clique em **ver o estado**.  

4.  Na **detalhes do ativo** painel da **em curso** separador, clique com o botão direito a entrada para a distribuição que pretende cancelar e selecione **Cancelar**.  

5.  Clique em **Sim** para confirmar a ação e cancelar a tarefa de distribuição a esse ponto de distribuição.  

### <a name="to-redistribute-content-that-failed-to-distribute"></a>Para redistribuir conteúdos que não tenha sido distribuído  

1.  Na consola do Configuration Manager, clique em **monitorização**.  

2.  Na **monitorização** área de trabalho, expanda **estado de distribuição**e, em seguida, clique em **estado do conteúdo**. Os pacotes são apresentados.  

3.  Selecione o pacote que pretende gerir e, em seguida, no painel de detalhes, clique em **ver o estado**.  

4.  Na **detalhes do ativo** painel da **erro** separador, clique com o botão direito a entrada para a distribuição que pretende redistribuir e selecione **redistribuir**.  

5.  Clique em **Sim** para confirmar a ação e iniciar o processo de redistribuição a esse ponto de distribuição.  

## <a name="distribution-point-group-status"></a>Estado do grupo de pontos de distribuição  
O nó **Estado do Grupo de Pontos de Distribuição** na área de trabalho **Monitorização** fornece informações acerca dos grupos de pontos de distribuição. Pode rever informações como:  

-   O nome de grupo de pontos de distribuição.  
-   A descrição.  
-   O número de pontos de distribuição são membros da distribuição de um grupo de pontos.  
-   O número de pacotes foram atribuído ao grupo.  
-   O estado de grupo de pontos de distribuição.  
-   A taxa de conformidade.  

Também exibir informações detalhadas de estado para o seguinte:  

-   Erros para o grupo de pontos de distribuição.  
-   Quantas distribuições estão em curso.
-   Quantos tiveram sido distribuídos com êxito.  

### <a name="to-monitor-distribution-point-group-status"></a>Para monitorizar o estado do grupo de pontos de distribuição  

1.  Na consola do Configuration Manager, clique em **monitorização**.  

2.  Na **monitorização** área de trabalho, expanda **estado de distribuição**e, em seguida, clique em **estado do grupo de pontos de distribuição**. Os grupos de pontos de distribuição são apresentados.  

3.  Selecione o grupo de pontos de distribuição para o qual pretende obter informações detalhadas de estado.  

4.  No separador **Home Page** , clique em **Ver Estado**. São apresentadas informações detalhadas de estado para o grupo de pontos de distribuição.  

## <a name="distribution-point-configuration-status"></a>Estado da configuração do ponto de distribuição  
 O nó **Estado da Configuração do Ponto de Distribuição** na área de trabalho **Monitorização** fornece informações acerca do ponto de distribuição. Pode rever quais os atributos que estão ativados para o ponto de distribuição, como PXE, multicast, conteúdo validação e o estado de distribuição para o ponto de distribuição. Também pode ver informações detalhadas de estado para o ponto de distribuição.  

> [!WARNING]  
>  Estado de configuração do ponto de distribuição é relativo ao último 24 horas. Se o ponto de distribuição tem um erro e recuperar, o estado de erro poderá ser apresentado até 24 horas após o ponto de distribuição recuperar.  

Utilize o seguinte procedimento para ver o estado da configuração do ponto de distribuição.  

### <a name="to-monitor-distribution-point-configuration-status"></a>Para monitorizar o estado da configuração do ponto de distribuição  

1.  Na consola do Configuration Manager, clique em **monitorização**.  

2.  Na **monitorização** área de trabalho, expanda **estado de distribuição**e, em seguida, clique em **estado de configuração do ponto de distribuição**. Os pontos de distribuição são apresentados.  

3.  Selecione o ponto de distribuição para o qual pretende que as informações de estado do ponto de distribuição.  

4.  No painel de resultados, clique no separador **Detalhes** . São apresentadas informações de estado para o ponto de distribuição.  

## <a name="client-data-sources-dashboard"></a>Dashboard de origens de dados do cliente
A partir da versão 1610, pode utilizar o **origens de dados do cliente** dashboard para ajudar a compreender a utilização de [Cache ponto a ponto](/sccm/core/plan-design/hierarchy/client-peer-cache) no seu ambiente. O dashboard será iniciado a exibição de dados depois dos clientes transferem conteúdo e o relatório de informações de volta para o site. Esta ação pode demorar até 24 horas.

> [!TIP]  
> **Cache do cliente ponto a ponto** e o **origens de dados do cliente** dashboard foram primeiro introduzidas na versão 1610 como [funcionalidades de pré-lançamento](/sccm/core/servers/manage/pre-release-features). A partir da versão 1710, estas funcionalidades não estão mais funcionalidades de pré-lançamento. Tem de ativar a Cache de elemento de rede do cliente antes do dashboard de origens de dados do cliente torna-se visíveis na consola.


Na consola, aceda a **monitorização** > **estado da distribuição** > **origens de dados do cliente**. Aqui, pode selecionar um período de tempo para aplicar ao dashboard. Em seguida, no ecrã, pode selecionar o grupo de limites ou o pacote para o qual pretende ver informações. Ao visualizar informações, pode passar o rato sobre a superfície para ver mais detalhes sobre o conteúdo diferente ou origens de política.

Esses detalhes incluem o seguinte:  
- **Fontes de conteúdo de cliente**: Apresenta a partir do qual os clientes tem conteúdos de origem.
- **Pontos de distribuição**: Mostra o número de pontos de distribuição que fazem parte do grupo de limites selecionado.
- **Clientes que utilizaram um ponto de distribuição**: Do número de clientes que estejam no grupo de limite selecionado, isso mostra quantas um ponto de distribuição usado na obtenção de conteúdo.
- **Configurar o peering entre origens de Cache**: Para o grupo de limite selecionado, esta ação mostra quantos origens da cache ponto a ponto que comunicaram o histórico de transferências.
- **Os clientes que utilizaram um elemento**: Do número de clientes que estejam no grupo de limite selecionado, esta ação mostra quantos usado uma origem de cache ponto a ponto na obtenção de conteúdo.



Também pode utilizar um novo relatório **origens de dados de cliente - resumo**, para ver um resumo das origens de dados do cliente para cada grupo de limites.
