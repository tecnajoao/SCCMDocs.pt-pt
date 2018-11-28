---
title: Criar implementações faseadas
titleSuffix: Configuration Manager
description: Utilize as implementações faseadas para automatizar a implementação de software para várias coleções.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b634ff68-b909-48d2-9e2c-0933486673c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7d103f7f7b92003605d92d34d6294ed06009118c
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52456520"
---
# <a name="create-phased-deployments-with-configuration-manager"></a>Criar implementações faseadas com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

As implementações faseadas automatizam uma implementação coordenada e sequenciada de software entre várias coleções. Por exemplo, implementar software para uma coleção piloto e, em seguida, continuar automaticamente a implementação com base nos critérios de sucesso. Criar implementações faseadas com a predefinição de duas fases ou configurar manualmente as várias fases. 

Crie implementações faseadas para os seguintes objetos:
- **Sequência de tarefas**  
    - A implementação faseada de sequências de tarefas não suporta a instalação de PXE ou suportes de dados   
- **Aplicação** (a partir da versão 1806) <!--1358147-->  
- **Atualização de software** (a partir da versão 1810) <!--1358146-->  
    - Não é possível utilizar uma regra de implementação automática com uma implementação faseada

> [!Tip]  
> A funcionalidade de implementação faseada foi introduzido pela primeira vez na versão 1802 como um [funcionalidade de pré-lançamento](/sccm/core/servers/manage/pre-release-features). A partir da versão 1806, ele não se encontra uma funcionalidade de pré-lançamento.<!--1356837-->  



## <a name="prerequisites"></a>Pré-requisitos

#### <a name="security-scope"></a>Âmbito de segurança
Implementações criadas por implementações faseadas não são visíveis para qualquer utilizador administrativo que não tem o **todos os** âmbito de segurança. Para obter mais informações, veja [Âmbitos de segurança](/sccm/core/understand/fundamentals-of-role-based-administration#bkmk_PlanScope).

#### <a name="distribute-content"></a>Distribuir conteúdo
Antes de criar uma implementação faseada, distribua o conteúdo associado a um ponto de distribuição.<!--518293-->  

- **Aplicação**: Selecione a aplicação de destino na consola e utilizar o **distribuir conteúdo** ação no Friso. Para obter mais informações, consulte [implementar e gerir conteúdos](/sccm/core/servers/deploy/configure/deploy-and-manage-content).   

- **Sequência de tarefas**: Tem de criar referenciado pacote de atualização de objetos, como o sistema operacional antes de criar a sequência de tarefas. Distribua estes objetos antes de criar uma implementação. Utilize o **distribuir conteúdo** ação em cada objeto ou a sequência de tarefas. Para ver o estado dos conteúdos referenciados tudo, selecione a sequência de tarefas e mude para o **referências** separador no painel de detalhes. Para obter mais informações, consulte o objeto específico, escreva [preparar a implementação do sistema operacional](/sccm/osd/get-started/prepare-for-operating-system-deployment).   

- **Atualização de software**: criar o pacote de implementação e distribuí-la. Utilize o Assistente de atualizações de Software de Download. Para obter mais informações, consulte [transferir atualizações de software](/sccm/sum/deploy-use/download-software-updates).  



## <a name="bkmk_settings"></a> Definições da fase

Estas definições são exclusivas para implementações faseadas. Configure estas definições ao criar ou editar fases para controlar o agendamento e comportamento do processo de implementação por fases. 


#### <a name="criteria-for-success-of-the-first-phase"></a>Critérios para o êxito da primeira fase  

- **Percentagem de êxito da implementação**: Especifique a percentagem de dispositivos que precisam para concluir com êxito a implementação para a primeira fase com êxito. Por predefinição, este valor é 95%. Em outras palavras, o site considera a primeira fase com êxito quando o estado de conformidade para 95% dos dispositivos é **êxito** para esta implementação. O site, em seguida, continua a segunda fase e cria uma implementação do software para a próxima coleta.  


#### <a name="conditions-for-beginning-second-phase-of-deployment-after-success-of-the-first-phase"></a>Condições para iniciar a segunda fase da implementação, após o êxito da primeira fase  

- **Iniciar automaticamente esta fase após um período de diferimento (em dias)**: Escolha o número de dias a aguardar antes de iniciar a segunda fase após o êxito da primeira. Por predefinição, este valor é um dia.  

- **Iniciar manualmente a segunda fase da implementação**: O site automaticamente não começa a segunda fase após a primeira fase ser bem sucedida. Esta opção requer que inicie manualmente a segunda fase. Para obter mais informações, consulte [mover para a próxima fase](/sccm/osd/deploy-use/manage-monitor-phased-deployments#bkmk_move).  

    > [!Note]  
    > Esta opção não está disponível para implementações faseadas de aplicativos.  


#### <a name="gradually-make-this-software-available-over-this-period-of-time-in-days"></a>Gradualmente tornar este software disponível durante este período de tempo (em dias)
<!--1358578--> A partir da versão 1806, configure esta definição para a distribuição em cada fase gradualmente a acontecer. Este comportamento ajuda a mitigar o risco de problemas de implantação e diminui a carga na rede que seja causada pela distribuição de conteúdo aos clientes. O site gradualmente faz com que o software disponível dependendo da configuração para cada fase. Todos os clientes numa fase têm um prazo em relação ao tempo que o software é disponibilizado. A janela de tempo entre o tempo disponível e o prazo é o mesmo para todos os clientes numa fase. O valor predefinido desta definição é zero, portanto, por predefinição não está limitada a implementação. Não defina o valor superior a 30.<!--SCCMDocs-pr issue 2767--> 


#### <a name="configure-the-deadline-behavior-relative-to-when-the-software-is-made-available"></a>Configurar o comportamento do prazo em relação a quando o software é disponibilizado  

- **É necessária a instalação logo que possível**: Defina o prazo de instalação do dispositivo assim que o dispositivo é direcionado.  

- **É necessária a instalação após este período de tempo**: Defina um prazo para a instalação de um determinado número de dias após o dispositivo é direcionado. Por predefinição, este valor é de sete dias.   


<!--### Examples
Include a timeline diagram
-->



## <a name="bkmk_auto"></a> Criar automaticamente uma implementação de duas fases predefinida

1. Inicie o Assistente de criar implementação faseada na consola do Configuration Manager. Esta ação varia consoante o tipo de software que estiver a implementar:  

    - **Aplicação** (apenas na versão 1806 ou posterior): Vá para o **biblioteca de Software**, expanda **gestão de aplicações**e selecione **aplicativos**. Selecione uma aplicação existente e, em seguida, escolha **criar implementação faseada** na faixa de opções.  

    - **Atualização de software** (apenas na versão 1810 ou posterior): Vá para o **biblioteca de Software**, expanda **atualizações de Software**e selecione **todas as atualizações de Software**. Selecione uma ou mais atualizações e, em seguida, escolha **criar implementação faseada** na faixa de opções.  

        Esta ação está disponível para atualizações de software a partir os seguintes nós:  
        - Atualizações de Software  
            - **Todas as atualizações de Software**  
            - **Grupos de atualização de software**   
        - Manutenção do Windows 10, **todas as atualizações do Windows 10**  
        - Gestão de clientes do Office 365, **atualizações do Office 365**  

    - **Sequência de tarefas**: Vá para o **biblioteca de Software** área de trabalho, expanda **sistemas operativos**e selecione **sequências de tarefas**. Selecione uma sequência já existente e, em seguida, escolha **criar implementação faseada** na faixa de opções.  

2. Sobre o **gerais** página, dê a implementação faseada um **nome**, **Descrição** (opcional) e selecione **criar automaticamente uma predefinição fase dois implementação**.  

3. Selecione **procurar** e escolha uma coleção de destino para ambos os **primeira coleção** e **segunda coleção** campos. Para uma sequência de tarefas e atualizações de software, selecione a partir de coleções de dispositivos. Para uma aplicação, selecione as coleções de utilizadores ou dispositivos. Selecione **seguinte**.  

    > [!Important]  
    > O Assistente para criar implementação por fases não notificá-lo se uma implementação é potencialmente alto risco. Para obter mais informações, consulte [definições para gerir implementações de alto risco](/sccm/core/servers/manage/settings-to-manage-high-risk-deployments) e a nota quando [implementar uma sequência de tarefas](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS).  

4. Sobre o **definições** página, selecione uma opção para cada uma das definições de agendamento. Para obter mais informações, consulte [fase definições](#bkmk_settings). Selecione **seguinte** quando terminar.  

5. Sobre o **fases** página, consulte as duas fases que o assistente cria para coleções especificadas. Selecione **seguinte**.   

    > [!Note]  
    > Esta secção abrange o procedimento para criar automaticamente uma implementação de duas fases predefinida. O assistente permite-lhe adicionar, remover, reordenar, editar ou ver as fases de uma implementação faseada. Para obter mais informações sobre estas ações adicionais, consulte [criar uma implementação faseada com fases configurados manualmente](#bkmk_manual).  

6. Confirme as suas seleções no **resumo** separador e, em seguida, selecione **próxima** para concluir o assistente.  



## <a name="bkmk_manual"></a> Criar uma implementação faseada com fases configurados manualmente
<!--1358148--> 

A partir da versão 1806, crie uma implementação faseada com fases configurados manualmente para uma sequência de tarefas. Adicionar fases adicionais até 10 do **fases** separador do Assistente para criar implementação por fases. 

> [!Note]  
> Atualmente manualmente, é possível criar fases para uma aplicação. O assistente cria automaticamente duas fases para implementações de aplicações.


1. Inicie o assistente criar implementação faseada para uma sequência de tarefas ou atualizações de software.  

2. Sobre o **gerais** página do Assistente para criar implementação por fases, dar a implementação faseada um **nome**, **Descrição** (opcional) e selecione **manualmente configurar todas as fases**.  

3. Partir do **fases** página do Assistente para criar implementação por fases, estão disponíveis as seguintes ações:  

    - **Filtro** a lista das fases de implementação. Introduza uma cadeia de caracteres para uma correspondência de maiúsculas e minúsculas das colunas de ordem, o nome ou coleção. 

    - **Adicionar** uma nova fase:  

        1. Na **gerais** página do Assistente para adicionar fase, especifique um **nome** para a fase e, em seguida, navegue para o destino **coleção de fase**. As definições adicionais nesta página são iguais ao normalmente implementar uma sequência de tarefas ou atualizações de software.  

        2. Sobre o **definições da fase** página do Assistente para adicionar fase, configurar as definições de agendamento e selecione **próxima** quando terminar. Para obter mais informações, consulte [definições](#bkmk_settings).   

            > [!Note]  
            > Não é possível editar a definição de fase **percentagem de êxito da implementação**, na primeira fase. Esta definição só se aplica a fases que têm uma fase anterior.  

        3. As definições do **experiência de utilizador** e **pontos de distribuição** páginas do Assistente para adicionar fase são os mesmos quando atualiza a normalmente implementar uma sequência de tarefas ou software.  

        4. Reveja as definições na **resumo** página e, em seguida, conclua o Assistente para adicionar fase.  

    - **Editar**: Esta ação abre a janela de propriedades a fase de selecionada, que tem as guias o mesmo que as páginas do Assistente para adicionar fase.  

    - **Remover**: Esta ação elimina a fase de selecionado.  

       > [!Warning]  
       > Não existe nenhuma confirmação e nenhuma forma de anular esta ação.  

    - **Mover para cima** ou **mover para baixo**: O assistente ordena as fases por como adicioná-los. A fase mais recentemente adicionada seja a última na lista. Para alterar a ordem, selecione uma fase e, em seguida, utilize estes botões para mover a localização a fase na lista.  

       > [!Important]  
       > Reveja as definições de fase depois de alterar a ordem. Certifique-se de que as definições seguintes são ainda consistentes com os seus requisitos para esta implementação por fases:  
       > 
       > - Critérios para o êxito da fase anterior  
       > - Condições para iniciar esta fase de implementação após o êxito da fase anterior   

5. Selecione **seguinte**. Reveja as definições na **resumo** página e, em seguida, conclua o Assistente para criar implementação por fases.  


Depois de criar uma implementação faseada, abra as respetivas propriedades para efetuar alterações:  

- **Adicionar** implementação por fases de fases adicionais para um existente.  

- Se uma fase não está ativa, pode **edite**, **remover**, ou **mover** -la ou reduzir verticalmente. Não é possível movê-lo antes de uma fase de Active Directory.  

- Quando uma fase está ativa, é só de leitura. Não é possível editá-lo, removê-lo ou mover a localização da lista. A única opção é **vista** as propriedades da fase.  

- Uma implementação de aplicações por fases sempre é só de leitura.  



## <a name="next-steps"></a>Passos seguintes

Gerir e monitorizar as implementações faseadas:
- [Aplicação](/sccm/osd/deploy-use/manage-monitor-phased-deployments?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  
- [Atualização de software](/sccm/osd/deploy-use/manage-monitor-phased-deployments?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json)  
- [Sequência de tarefas](/sccm/osd/deploy-use/manage-monitor-phased-deployments)  

