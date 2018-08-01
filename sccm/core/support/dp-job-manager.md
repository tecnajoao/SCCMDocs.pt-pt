---
title: Gestor de filas de trabalho de DP
titleSuffix: Configuration Manager
description: Utilize o Gestor de filas de trabalho de DP para resolver problemas e gerir tarefas de distribuição de conteúdo a pontos de distribuição do Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 4b72922a-d11e-4aef-b309-19f5f0716f32
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5218d47ae8699ee0feb0cf59405833ec4cc49569
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39386746"
---
# <a name="dp-job-queue-manager"></a>Gestor de filas de trabalho de DP

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O Gestor de filas de tarefa de ponto de distribuição (DP) é uma da [ferramentas do Configuration Manager](/sccm/core/support/tools). Usá-lo para resolver problemas e gerir tarefas de distribuição de conteúdo em curso para pontos de distribuição do Configuration Manager. 

A ferramenta exibe a lista de tarefas que o componente de Gestor de transferência do pacote tem na sua fila. Ela também mostra o estado das tarefas: pronto para ser executado, em execução ou tentar novamente. Permite-lhe manipular as tarefas na fila, mover o mais elevadas de tarefas na lista, cancelar uma tarefa ou iniciar manualmente a executar uma tarefa.

Também obtém informações do servidor do site no qual ponto de distribuição está a executar uma tarefa. A ferramenta se conectar por meio do provedor para o servidor do site. Ele não ligar a cada ponto de distribuição remoto recolher estas informações. Porque ela aciona as ações e obtém informações por meio do provedor, existe um atraso na que reflete as alterações de pontos de distribuição remotos.



## <a name="usage"></a>Utilização

Execute **DPJobMgr.exe**. Menu principal da ferramenta contém os seguintes separadores: 

- [Ligar](#bkmk_connect): Estabelecer a ligação inicial ao servidor do site primário  

- [Descrição geral](#bkmk_overview): Resume numa única exibição todas as tarefas em execução em todos os pontos de distribuição  

- [Informações de ponto de distribuição](#bkmk_dp-info): Pontos de distribuição de seleção múltipla acompanhá-las e gerir uma tarefa única de interesse  

- [Gerir tarefas](#bkmk_manage-jobs): Estará num simples ver uma lista de todas as tarefas e os respetivos Estados. Manipular tarefas, movê-los a cópia de segurança, cancelar ou iniciar manualmente.  


### <a name="bkmk_connect"></a> Ligar o separador

Utilize este separador para estabelecer a ligação inicial ao servidor do site primário. Utiliza credenciais atualmente com sessão iniciada do utilizador. Não é possível ligar ao site de administração central ou sites secundários. A ligação requer o **administrador total** função de segurança.

Assim que a ferramenta com êxito estabelece uma conexão, uma notificação na parte inferior da ferramenta confirma que está ligado ao servidor do site. 


### <a name="bkmk_overview"></a> Separador de descrição geral

Mostra um resumo de todas as tarefas em todos os pontos de distribuição. Consulte as seguintes colunas:  

- **Ponto de distribuição**: Lista os nomes dos pontos de distribuição  

- **Tarefas em execução**: Mostra o número de tarefas simultâneas em execução num ponto de distribuição específico.  

    > [!Tip]  
    > O número de distribuições de software em simultâneo é uma definição de site. Modificar esta definição nas propriedades de componente de distribuição de Software.  

- **Total de tarefas**: Mostra o número de todas as tarefas direcionadas para um ponto de distribuição específico. Este número inclui as tarefas que estão em execução, tentar novamente ou a aguardar para ser executado.  

- **Total de repetições**: Mostra o número de vezes que tem sido repetir tarefas num ponto de distribuição específico. Um número mais elevado pode representar um problema geral com esse ponto de distribuição específico.  


> [!Tip]  
> - Para classificar cada coluna neste separador, clique no nome da coluna  
> 
> - Atualizar manualmente as informações neste separador, clicando em **atualizar**  
> 
> - Atualizar automaticamente as informações neste separador clicando **começar a atualizar de automático** e definir o intervalo de atualização automática. O intervalo de atualização predefinido é de dois minutos.  


### <a name="bkmk_dp-info"></a> Separador de informações do ponto de distribuição

Mostra a lista de todos os pontos de distribuição no site ligado. O painel esquerdo apresenta uma lista de todos os pontos de distribuição. Clique em **Selecionar tudo** ou **anule a seleção de todos os** como pontos de distribuição específico necessário ou seleção múltipla, nesta lista. O painel no lado direito mostra as tarefas de pontos de distribuição selecionados.

Existem oito colunas:  

- **Ícone de estado**: Existem três ícones de estado possíveis:  

    - **Pronto**: Indica se a uma determinada tarefa foi concluída todos os passos de verificação. Ele está pronto para ser adicionado para as tarefas em execução em simultâneo. Normalmente, são tarefas neste estado numa fase de espera. Esperam que os processos em execução atuais concluir a abrir um espaço para eles.  

    - **Executar**: Indica que uma tarefa específica está atualmente em execução num ponto de distribuição. Para de longa execução tarefas (pacotes grandes), normalmente há é o tempo para obter o progresso (%) em direção à conclusão. Ele mostra esta percentagem na **progresso** coluna nesta vista. Para pacotes pequenos, o **progresso** coluna pode permanecer vazia. A tarefa já pode ser concluída no momento em que recebe o estado do ponto de distribuição remoto.  

    - **Repita**: Indica que uma tarefa específica falhou e está agora num Estado de repetição. Esta tarefa será tentada novamente após o intervalo entre tentativas. Este intervalo é configurável e definido como 30 minutos por predefinição.  

- **Software**: Nome do pacote direcionado a um ponto de distribuição específico  

- **ID do pacote**: ID do pacote do pacote que está direcionado para um ponto de distribuição específico  

- **Tamanho**: Tamanho do pacote no artigo BDC  

- **Curso**: Percentagem de conclusão da tarefa. Para obter mais informações, consulte a **em execução** descrição do ícone de estado.  

- **Hora de início/reinicialização**: Para uma tarefa em execução, este valor é a hora de início (verde). Para uma tarefa de repetição, este valor é o tempo que irá tentar novamente a tarefa.  

- **Repete**: Número de vezes que ele repetiu este pacote.  

- **Nome do ponto de distribuição**: O nome de domínio completamente qualificado (FQDN) do ponto de distribuição  

> [!Tip]  
> - Para classificar cada coluna neste separador, clique no nome da coluna  
> 
> - Atualizar manualmente as informações neste separador, clicando em **atualizar**  
> 
> - Atualizar automaticamente as informações neste separador clicando **começar a atualizar de automático** e definir o intervalo de atualização automática. O intervalo de atualização predefinido é de dois minutos.  
> 
> - Se precisar de modificar uma tarefa específica, a tarefa nesta vista com o botão direito e selecione **gerir trabalho**. Esta ação abre o [separador Manage Jobs](#bkmk_manage-jobs).  


### <a name="bkmk_manage-jobs"></a> Gerir a guia Jobs

Estará num simples ver uma lista de todas as tarefas e os respetivos Estados. Contém as mesmas colunas de oito, como o [separador informações de ponto de distribuição](#bkmk_dp-info). Nesta vista, clique com botão direito as tarefas para as seguintes ações:  

- **Executar**: Inicia uma tarefa que esteja em qualquer Estado que não seja em execução  

- **Mover para cima**: Move uma ou mais tarefas na parte superior da fila. Esta ação pode resultar em tarefas em execução imediatamente. Uma tarefa de prioridade inferior pode colocar em pausa devido a esta ação.  

- **Mover para cima**: Move uma tarefa específica uma linha acima. Uma tarefa de prioridade inferior pode colocar em pausa devido a esta ação a executar.  

- **Mover para baixo**: Move uma tarefa específica uma linha abaixo.  

- **Mover para baixo**: Move uma ou mais tarefas na parte inferior da fila.  

    > [!Tip]  
    > Tarefas de arrastar e largar na lista para movê-los.  

- **Cancelar**: Tenta cancelar uma ou mais tarefas.  

    > [!Note]  
    > Não é possível cancelar tarefas perto do tempo de conclusão final. Se o servidor do site também é um ponto de distribuição, não é possível cancelar tarefas no servidor do site.  



## <a name="see-also"></a>Consulte também

- [Conceitos fundamentais da gestão de conteúdos](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)
- [Gestor de transferência de pacotes](/sccm/core/plan-design/hierarchy/package-transfer-manager)
