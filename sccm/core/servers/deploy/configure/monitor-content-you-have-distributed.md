---
title: "Monitorizar o conteúdo | Documentos do Microsoft"
description: "Compreenda como monitorizar conteúdo distribuído ao utilizar a consola do Configuration Manager."
ms.custom: na
ms.date: 4/17/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 82e8a693-9adf-4ca3-8484-7e101c34c7c1
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: dda2f4c01078fbbd174cbcb30357554c24f6abeb
ms.openlocfilehash: 7659d5789b8ce4e9e0b585a331c8f68869c9492d
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="monitor-content-you-have-distributed-with-system-center-configuration-manager"></a>Monitorizar o conteúdo que ter distribuídas com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilizar a consola do System Center Configuration Manager para monitorizar o conteúdo distribuído, incluindo:  

-   O estado de todos os tipos de pacotes relativamente aos pontos de distribuição associados.  
-   O estado de validação de conteúdos para o conteúdo de um pacote.  
-   O estado dos conteúdos atribuídos a um grupo de pontos de distribuição específico.  
-   O estado dos conteúdos atribuídos a um ponto de distribuição.  
-   O estado das funcionalidades opcionais de cada ponto de distribuição (validação de conteúdos, PXE e multicast).  

> [!NOTE]  
>  O Configuration Manager monitoriza apenas o conteúdo num ponto de distribuição que esteja na biblioteca de conteúdos. Não é monitorizado conteúdo armazenado no ponto de distribuição em partilhas personalizadas ou pacote.  

##  <a name="BKMK_ContentStatus"></a> Monitorização do estado do conteúdo  
 O nó **Estado do Conteúdo** da área de trabalho **Monitorização** disponibiliza informações sobre pacotes de conteúdos. Na consola do Configuration Manager, pode rever as informações como:  

-   O nome do pacote.  
-   O tipo.  
-   Um pacote de pontos de distribuição quantos foi enviada para.  
-   A taxa de conformidade.  
-   Quando o pacote foi criado.  
-   O ID do pacote.  
-   A versão de origem.  

Encontrará também informações de estado detalhadas para qualquer pacote, bem como o estado de distribuição para o pacote, incluindo:  

-   O número de falhas.  
-   Distribuições pendentes.  
-   O número de instalações.

Também pode gerir as distribuições que continuam em curso para um ponto de distribuição ou que falharam a distribuir com êxito os conteúdos para um ponto de distribuição:  

-   A opção para cancelar ou redistribuir conteúdos está disponível quando visualiza a mensagem de estado de implementação de uma tarefa de distribuição para um ponto de distribuição no **detalhes do ativo** painel. Neste painel, pode ser encontrado no **em curso** separador ou **erro** separador do **estado do conteúdo** nó.  
-   Além disso, os detalhes da tarefa apresentam a percentagem da tarefa que está concluída quando visualizar os detalhes de uma tarefa no **em curso** separador. Os detalhes da tarefa também apresentam o número de tentativas restantes para uma tarefa, bem como o tempo restante até à próxima tentativa quando visualizar os detalhes de uma tarefa que está disponível a partir de **erro** separador.  

Se cancelar uma implementação que ainda não está concluída, a tarefa de distribuição para transferência desse conteúdo é interrompida:  

-   O estado da implementação será então atualizado para indicar que a distribuição falhou e foi cancelada por uma ação do utilizador.  
-   Este novo estado é apresentado no **erro** separador.  

> [!TIP]  
>  Quando uma implementação estiver próxima da conclusão, é possível que a ação de cancelamento dessa distribuição não processará antes da distribuição ao ponto de distribuição estar concluída. Quando isto ocorre, a ação de cancelamento da implementação será ignorada e o estado da implementação indicará a conclusão com êxito.  

> [!NOTE]  
>  Embora possa selecionar a opção para cancelar uma distribuição a um ponto de distribuição que esteja localizado num servidor do site, isto não tem qualquer efeito. Isto acontece porque o servidor do site e a pontos de distribuição numa partilha de servidor do site o mesmo arquivo de conteúdos de instância única. Não existe uma tarefa de distribuição existente a cancelar.  

Se redistribuir conteúdos que tinha falhado para transferir para um ponto de distribuição, o Configuration Manager começa imediatamente é que o conteúdo ao ponto de distribuição. O estado da implementação para refletir o estado dessa redeployment de atualizações do Configuration Manager.  

Utilize os procedimentos seguintes para ver o estado do conteúdo e gerir as distribuições que continuam em curso ou que falharam.  

### <a name="to-monitor-content-status"></a>Para monitorizar o estado do conteúdo  

1.  Na consola do Configuration Manager, clique em **monitorização**.  

2.  No **monitorização** área de trabalho, expanda **estado da distribuição**e, em seguida, clique em **estado do conteúdo**. Os pacotes são apresentados.  

3.  Selecione o pacote para o qual pretende obter informações detalhadas de estado.  

4.  No separador **Home Page** , clique em **Ver Estado**. São apresentadas informações de estado detalhadas sobre o pacote.  

### <a name="to-cancel-a-distribution-that-remains-in-progress"></a>Para cancelar uma distribuição que continua em curso  

1.  Na consola do Configuration Manager, clique em **monitorização**.  

2.  No **monitorização** área de trabalho, expanda **estado da distribuição**e, em seguida, clique em **estado do conteúdo**. Os pacotes são apresentados.  

3.  Selecione o pacote que pretende gerir e, em seguida, no painel de detalhes, clique em **Ver estado**.  

4.  No **detalhes do ativo** painel do **em curso** separador, faça duplo clique na entrada correspondente à distribuição que pretende cancelar e selecione **Cancelar**.  

5.  Clique em **Sim** para confirmar a ação e cancelar a tarefa de distribuição a esse ponto de distribuição.  

### <a name="to-redistribute-content-that-failed-to-distribute"></a>Para redistribuir conteúdos que não foi possível distribuir  

1.  Na consola do Configuration Manager, clique em **monitorização**.  

2.  No **monitorização** área de trabalho, expanda **estado da distribuição**e, em seguida, clique em **estado do conteúdo**. Os pacotes são apresentados.  

3.  Selecione o pacote que pretende gerir e, em seguida, no painel de detalhes, clique em **Ver estado**.  

4.  No **detalhes do ativo** painel do **erro** separador, faça duplo clique na entrada correspondente à distribuição que pretende redistribuir e selecione **redistribuir**.  

5.  Clique em **Sim** para confirmar a ação e iniciar o processo de redistribuição a esse ponto de distribuição.  

## <a name="distribution-point-group-status"></a>Estado do grupo de pontos de distribuição  
O nó **Estado do Grupo de Pontos de Distribuição** na área de trabalho **Monitorização** fornece informações acerca dos grupos de pontos de distribuição. Pode rever as informações como:  

-   O nome de grupo de pontos de distribuição.  
-   A descrição.  
-   Grupo de pontos de quantos pontos de distribuição sejam membros da distribuição.  
-   O número de pacotes que foram atribuído ao grupo.  
-   O estado de grupo de pontos de distribuição.  
-   A taxa de conformidade.  

Também ver informações detalhadas de estado para o seguinte:  

-   Erros para o grupo de pontos de distribuição.  
-   Quantas distribuições estão em curso.
-   Quantos tenham sido distribuídos com êxito.  

### <a name="to-monitor-distribution-point-group-status"></a>Para monitorizar o estado do grupo de pontos de distribuição  

1.  Na consola do Configuration Manager, clique em **monitorização**.  

2.  No **monitorização** área de trabalho, expanda **estado da distribuição**e, em seguida, clique em **estado do grupo de pontos de distribuição**. Os grupos de pontos de distribuição são apresentados.  

3.  Selecione o grupo de pontos de distribuição para o qual pretende obter informações detalhadas de estado.  

4.  No separador **Home Page** , clique em **Ver Estado**. São apresentadas informações detalhadas de estado para o grupo de pontos de distribuição.  

## <a name="distribution-point-configuration-status"></a>Estado da configuração do ponto de distribuição  
 O nó **Estado da Configuração do Ponto de Distribuição** na área de trabalho **Monitorização** fornece informações acerca do ponto de distribuição. Pode rever quais os atributos que estão ativados para o ponto de distribuição, como PXE, multicast conteúdo validação e o estado de distribuição para o ponto de distribuição. Também pode ver informações detalhadas de estado para o ponto de distribuição.  

> [!WARNING]  
>  Estado de configuração do ponto de distribuição é relativo às últimas 24 horas. Se o ponto de distribuição tiver um erro e recuperar, o estado de erro poderá ser apresentado até 24 horas após o ponto de distribuição recuperar.  

Utilize o seguinte procedimento para ver o estado da configuração do ponto de distribuição.  

### <a name="to-monitor-distribution-point-configuration-status"></a>Para monitorizar o estado da configuração do ponto de distribuição  

1.  Na consola do Configuration Manager, clique em **monitorização**.  

2.  No **monitorização** área de trabalho, expanda **estado da distribuição**e, em seguida, clique em **estado de configuração do ponto de distribuição**. Os pontos de distribuição são apresentados.  

3.  Selecione o ponto de distribuição para o qual pretende que as informações de estado do ponto de distribuição.  

4.  No painel de resultados, clique no separador **Detalhes** . São apresentadas informações de estado para o ponto de distribuição.  

## <a name="client-data-sources-dashboard"></a>Dashboard de origens de dados do cliente
A partir da versão 1610, pode utilizar o **origens de dados de cliente** dashboard para ajudar a compreender a utilização de [cache de elementos da](/sccm/core/plan-design/hierarchy/client-peer-cache) no seu ambiente. O dashboard será iniciada a apresentar dados depois dos clientes transferem conteúdo e de relatório que informações novamente o site. Esta ação pode demorar até 24 horas.

> [!TIP]  
> **Cache de elemento de rede do cliente** e **origens de dados de cliente** dashboard são funcionalidades de versão de pré-lançamento introduzidas na versão 1610. Tem de ativar a Cache do cliente ponto a ponto antes do dashboard de origens de dados de cliente torna-se visíveis na consola. Para ativar a Cache de elemento de rede do cliente, consulte o artigo [utilizar funcionalidades de pré-lançamento das atualizações da](/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease). Pode demorar até 24 horas depois de ativá-la para começar a apresentar dados.

Na consola, vá para **monitorização** > **estado da distribuição** > **origens de dados de cliente**. Aqui pode selecionar um período de tempo para aplicar ao dashboard. Em seguida, no ecrã, pode selecionar o grupo de limites ou o pacote para o qual pretende visualizar as informações. Ao visualizar informações, pode passar o rato sobre a superfície de para ver mais detalhes sobre os conteúdos diferentes ou origens de política.

Os detalhes incluem o seguinte:  
- **Fontes de conteúdo de cliente**: Apresenta a origem a partir da qual os clientes tem conteúdos.
- **Pontos de distribuição**: Apresenta o número de pontos de distribuição que fazem parte do grupo de limites selecionado.
- **Os clientes que utilizado um ponto de distribuição**: O número de clientes que se encontram no grupo de limites selecionado, isto mostra quantos utilizado um ponto de distribuição para obter conteúdo.
- **Origens de Cache de elemento**: Para o grupo de limites selecionada, é apresentada como várias origens de cache ponto a ponto reportaram histórico de transferência.
- **Os clientes que utilizado um elemento**: O número de clientes que estão num grupo de limites selecionada, mostra quantos utilizada uma origem de cache ponto a ponto para obter conteúdo.



Também pode utilizar um novo relatório, **origens de dados de cliente - resumo**, para ver um resumo das origens de dados de cliente para cada grupo de limites.

