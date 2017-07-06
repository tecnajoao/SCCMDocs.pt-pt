---
title: Gerir consultas | Documentos do Microsoft
description: "Saiba como gerir as suas consultas. Inclui uma tabela de referência detalhada."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e562e2a0-8df8-4952-952f-e8c38461c612
caps.latest.revision: 6
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 738dcf0b52f18b38b732bf8ca5d7a87369b1c468
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="how-to-manage-queries-in-system-center-configuration-manager"></a>Como gerir consultas no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize as informações deste tópico para o ajudar a gerir consultas no System Center Configuration Manager.  

 Para obter informações sobre como criar consultas, consulte o artigo [como criar consultas no System Center Configuration Manager](../../../core/servers/manage/create-queries.md).  

## <a name="how-to-manage-queries"></a>Como gerir consultas  
 Na área de trabalho **Monitorização** , selecione **Consultas**, selecione a consulta que pretende gerir e, em seguida, selecione uma tarefa de gestão.  

 Utilize a tabela seguinte para obter mais informações sobre as tarefas de gestão que podem necessitar de algumas informações antes de as selecionar.  

|Tarefa de gestão|Detalhes|Mais informações|  
|---------------------|-------------|----------------------|  
|**Executar**|A consulta selecionada é executada e apresenta os resultados na consola do Configuration Manager.|Não existem informações adicionais.|  
|**Instalar Cliente**|Abre o **Assistente de instalação do cliente** que permite-lhe instalar o cliente do Configuration Manager em computadores devolvidos pela consulta selecionada.<br /><br /> Esta opção não está disponível para consultas que devolvem dispositivos móveis, utilizadores ou grupos de utilizadores.|Para obter mais informações sobre como instalar clientes do Configuration Manager utilizando push de cliente, consulte o artigo [implementar clientes em computadores com o Windows](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).|  
|**Exportarar**|Abre o **Assistente Exportar Objetos** que permite exportar esta consulta para um ficheiro de formato MOF (Managed Object Format) que pode, em seguida, ser importado noutro site.|Não existem informações adicionais.|  
|**Moverr**|Abre a caixa de diálogo **Mover Itens Selecionados** , na qual pode mover a consulta selecionada para uma pasta que criou anteriormente sob o nó **Consultas** .|Não existem informações adicionais.|  

## <a name="see-also"></a>Consulte Também  
 [Operações e manutenção de consultas no System Center Configuration Manager](../../../core/servers/manage/operations-and-maintenance-for-queries.md)
