---
title: "Migração do monitor"
titleSuffix: Configuration Manager
description: "Saiba como utilizar a consola do Configuration Manager para monitorizar o progresso e o sucesso das tarefas de migração."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fc731d3f-edd7-4049-b17b-653d6693a564
caps.latest.revision: "4"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 1782e8abaf01cf8097393fa45db999a6a02c6cb5
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="planning-to-monitor-migration-activity-in-system-center-configuration-manager"></a>Planear para monitorizar a atividade de migração no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Com o System Center Configuration Manager, pode monitorizar a migração na consola do Configuration Manager que liga à hierarquia de destino. Na consola do Configuration Manager no **administração** área de trabalho, pode utilizar o **migração** nó para monitorizar o progresso e o sucesso das tarefas de migração. Pode ver informações de resumo para cada tarefa de migração que identifica os objetos que foram migrados, os objetos que ainda não foram migrados e o número de objetos que foram excluídos de uma tarefa de migração. Também poderá ver detalhes sobre possíveis problemas de migração.  

## <a name="view-migration-progress"></a>Progresso da migração de vista  
 Para ver o progresso de uma tarefa de migração, utilize qualquer uma das seguintes ações:  

-   No **administração** área de trabalho da consola do Configuration Manager, expanda o **tarefas de migração** nó, selecione uma tarefa de migração e, em seguida, selecione o **objetos na tarefa** separador.  

-   Utilize os ficheiros de registo do Configuration Manager para rever o progresso da migração ou para identificar quaisquer problemas. Gestor de migração é o processo do Configuration Manager que controla as ações de migração e as regista no ficheiro migmctrl.log o  **\&lt; Caminhodainstalação\>\\registos** pasta no servidor do site.  

    > [!NOTE]  
    >  Se uma tarefa de migração falhar, reveja os detalhes no ficheiro migmctrl.log logo que possível. As entradas de registo de migração são constantemente adicionadas ao ficheiro e substituem os detalhes antigos. Se as entradas forem substituídas, poderá não conseguir identificar se os problemas que podem surgir com os objetos migrados referem-se a problemas de migração. Atividade de migração é registada na parte superior\-site ao nível da hierarquia independentemente do site com a consola do Configuration Manager liga-se ao quando configura a migração.  

-   Utilize os relatórios do Configuration Manager. O Configuration Manager fornece vários incorporada\-nos relatórios de migração, mas pode editar os relatórios para satisfazerem as suas necessidades. Para mais informações sobre relatórios do Configuration Manager, consulte [relatórios no System Center Configuration Manager](../../core/servers/manage/reporting.md).  
