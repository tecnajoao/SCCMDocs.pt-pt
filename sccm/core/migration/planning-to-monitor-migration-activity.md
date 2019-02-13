---
title: Monitorizar a migração
titleSuffix: Configuration Manager
description: Saiba como utilizar a consola do Configuration Manager para monitorizar o progresso e êxito das tarefas de migração.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: fc731d3f-edd7-4049-b17b-653d6693a564
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5588afeb02ead302201cc99c8c2ad7558ec4b32e
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56134787"
---
# <a name="planning-to-monitor-migration-activity-in-system-center-configuration-manager"></a>Planear a monitorização da atividade de migração no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Com o System Center Configuration Manager, pode monitorizar a migração na consola do Configuration Manager que liga à hierarquia de destino. Na consola do Configuration Manager nos **administração** área de trabalho, pode usar o **migração** nó para monitorizar o progresso e êxito das tarefas de migração. Pode ver informações de resumo para cada tarefa de migração que identifica os objetos que foram migrados, os objetos que ainda não foram migrados e o número de objetos que estão excluídos de uma tarefa de migração. Também verá detalhes sobre possíveis problemas de migração.  

## <a name="view-migration-progress"></a>Ver progresso da migração  
 Para ver o progresso de uma tarefa de migração, utilize qualquer uma das seguintes ações:  

-   Na **administração** área de trabalho da consola do Configuration Manager, expanda o **tarefas de migração** nó, selecione uma tarefa de migração e, em seguida, selecione o **objetos na tarefa** separador.  

-   Utilize os ficheiros de registo do Configuration Manager para analisar o progresso da migração ou para identificar quaisquer problemas. Gestor de migração é o processo de Configuration Manager que controla as ações de migração e as regista no ficheiro migmctrl o  **\&lt; Caminhodainstalação\>\\registos** pasta no site servidor.  

    > [!NOTE]  
    >  Se uma tarefa de migração falhar, reveja os detalhes no ficheiro migmctrl log logo que possível. As entradas de registo de migração são constantemente adicionadas ao ficheiro e substituem os detalhes antigos. Se as entradas forem substituídas, poderá não conseguir identificar se quaisquer problemas que podem surgir nos objetos migrados se relaciona com problemas de migração. Atividade de migração é registada na parte superior\-site de nível da hierarquia, independentemente do site na consola do Configuration Manager liga-se ao quando configurar a migração.  

-   Utilize relatórios do Configuration Manager. O Configuration Manager fornece vários criado\-nos relatórios para a migração, ou pode editar os relatórios para satisfazer as suas necessidades. Para obter mais informações sobre relatórios do Configuration Manager, consulte [relatórios no System Center Configuration Manager](../../core/servers/manage/reporting.md).  
