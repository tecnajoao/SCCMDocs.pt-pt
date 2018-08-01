---
title: Gerir e monitorizar as implementações faseadas
titleSuffix: Configuration Manager
description: Compreenda como gerir e monitorizar as implementações faseadas de software no Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: dc245916-bc11-4983-9c4d-015f655007c1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1889ba3ea19d27676089f2a9a24cef812c9f526c
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39386767"
---
# <a name="manage-and-monitor-phased-deployments"></a>Gerir e monitorizar as implementações faseadas

Este artigo descreve como gerir e monitorizar as implementações faseadas. Tarefas de gestão incluem manualmente iniciar a fase seguinte e suspender ou retomar uma fase. 

Primeiro, precisa [criar uma implementação faseada](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence). 



## <a name="bkmk_move"></a> Mover para a próxima fase

Quando seleciona a definição **iniciar manualmente a segunda fase da implementação**, o site não iniciar automaticamente a próxima fase com base nos critérios de sucesso. Tem de mover a implementação faseada para a próxima fase.  

1. Como iniciar esta ação varia com base no tipo de software implementadas:  

    - **Aplicação** (apenas na versão 1806 ou posterior): Vá para o **biblioteca de Software**, expanda **gestão de aplicações**e selecione **aplicativos**.   

    - **Sequência de tarefas**: Vá para o **biblioteca de Software** área de trabalho, expanda **sistemas operativos**e selecione **sequências de tarefas**.   

2. Selecione o software com a implementação faseada.  

3. No painel de detalhes, mude para o **implementações faseadas** separador.  

4. Selecione a implementação faseada e clique em **mover para a próxima fase** na faixa de opções.  

    ![Com o botão direito ações de Mostrar menu numa implementação faseada](media/Suspend-phased-deployment.PNG)



## <a name="bkmk_suspend"></a> Suspender e retomar fases 

Se pretender manualmente suspender ou retomar uma implementação faseada. Por exemplo, criar uma implementação faseada para uma sequência de tarefas. Ao monitorizar a fase de para o grupo piloto, observe um grande número de falhas. Suspender a implementação faseada para parar a dispositivos de executar a sequência de tarefas. Depois de resolver o problema, retome a implementação faseada para continuar a implementação. 

1. Como iniciar esta ação varia com base no tipo de software implementadas:  

    - **Aplicação** (apenas na versão 1806 ou posterior): Vá para o **biblioteca de Software**, expanda **gestão de aplicações**e selecione **aplicativos**.   

    - **Sequência de tarefas**: Vá para o **biblioteca de Software** área de trabalho, expanda **sistemas operativos**e selecione **sequências de tarefas**. Selecione uma sequência já existente e, em seguida, clique em **criar implementação faseada** na faixa de opções.  

2. Selecione o software com a implementação faseada.  

3. No painel de detalhes, mude para o **implementações faseadas** separador.  

4. Selecione a implementação faseada e clique em **Suspend** ou **retomar** na faixa de opções.  

<!-- Removed for 1806, need to clarify behavior with engineering
When you suspend a phased deployment, it sets the available and deadline times on the active deployments to a future time. When you resume, it generates a new schedule based on when you resume the phased deployment. The new schedule helps to avoid problems if you resume after the original deadline. For example, the initial schedule has the required deadline seven days after the deployment is available. You suspend it on the second day. If you aren't ready to resume it until day eight, you don't want the deployment to be immediately past the deadline. So it generates a new deadline starting from when you resume the phased deployment on day eight. 
-->


## <a name="bkmk_monitor"></a> Monitor
<!--1358577-->

A partir da versão 1806, as implementações faseadas tem uma experiência de monitorização nativa. Do **implementações** nó a **monitorização** área de trabalho, selecione uma implementação faseada e, em seguida, clique em **estado da implementação por fases** na faixa de opções.

![Dashboard de estado de implementação por fases que mostra o estado de duas fases](media/1358577-phased-deployment-status.png)

Este dashboard mostra as seguintes informações para cada fase da implementação:  

- **Total de dispositivos**: O número de dispositivos visado por esta fase.  

- **Estado**: O estado atual desta fase. Cada fase pode ter um dos seguintes Estados:  

    - **Implementação criada**: A implementação faseada criou uma implementação do software para a coleção para esta fase. Os clientes são direcionados ativamente com este software.  

    - **A aguardar**: Fase anterior ainda não tiver atingido os critérios de êxito para a implementação continuar para esta fase.  

    - **Suspenso**: Um administrador suspensa a implementação.  

- **Curso**: Os Estados de implementação codificados por cores de clientes. Por exemplo: Êxito no curso, erro, requisitos não cumpridos e desconhecido. 

#### <a name="success-criteria-tile"></a>Mosaico de critérios de êxito

Utilize o **selecione fase** na lista pendente para alterar a apresentação da **critérios de sucesso** mosaico. Este mosaico compara o **objetivo da fase** contra a conformidade atual da implantação. Com as configurações padrão, o objetivo de fase é 95%. Este valor significa que a implementação precisa a conformidade de 95% para mover para a próxima fase. 

Neste exemplo, o objetivo de fase é 65% e a conformidade atual é 66,7%. A implementação faseada movida automaticamente para a segunda fase, uma vez que a primeira fase cumpre os critérios de sucesso.
![Critérios de sucesso de exemplo mosaico de estado da implementação por fases](media/pod-status-success-criteria-tile.png)

O objetivo da fase é igual a **percentagem de êxito da implementação** nas definições de fase para o *seguinte* fase. Para a implementação faseada iniciar a fase seguinte, essa segunda fase define os critérios de êxito da primeira fase. Para ver esta definição: 

1. Vá para o objeto de implementação por fases no software e abra as propriedades de implementação por fases.  

2. Mude para o **fases** separador. Selecione **fase 2** e clique em **vista**.  

3. Na janela de propriedades da fase, mude para o **definições de fase** separador.  

4. Ver o valor **percentagem de êxito da implementação** no *critérios para o êxito da fase anterior* grupo.  

Por exemplo, as seguintes propriedades são para a fase mesmo como o sucesso mosaico de critérios mostradas acima em que os critérios é 65%:  
![Separador de definições de fase nas propriedades da fase](media/phase-properties-phase-settings.png)

