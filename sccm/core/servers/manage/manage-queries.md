---
title: Gerir consultas
titleSuffix: Configuration Manager
description: Saiba como gerir as suas consultas. Inclui uma tabela de referência detalhada.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e562e2a0-8df8-4952-952f-e8c38461c612
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 87b92bb857f6a39a99e3aee1e4bc862904bcc4ef
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56126920"
---
# <a name="how-to-manage-queries-in-system-center-configuration-manager"></a>Como gerir consultas no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize as informações neste tópico para o ajudar a gerir consultas no System Center Configuration Manager.  

 Para obter informações sobre como criar consultas, consulte [como criar consultas no System Center Configuration Manager](../../../core/servers/manage/create-queries.md).  

## <a name="how-to-manage-queries"></a>Como gerir consultas  
 Na área de trabalho **Monitorização** , selecione **Consultas**, selecione a consulta que pretende gerir e, em seguida, selecione uma tarefa de gestão.  

 Utilize a tabela seguinte para obter mais informações sobre as tarefas de gestão que podem necessitar de algumas informações antes de as selecionar.  

|Tarefa de gestão|Detalhes|Mais informações|  
|---------------------|-------------|----------------------|  
|**Executar**|Executa a consulta selecionada e apresenta os resultados na consola do Configuration Manager.|Não existem informações adicionais.|  
|**Instalar Cliente**|Abre o **Assistente de instalação do cliente** que permite instalar o cliente do Configuration Manager nos computadores devolvidos pela consulta selecionada.<br /><br /> Esta opção não está disponível para consultas que devolvem dispositivos móveis, utilizadores ou grupos de utilizadores.|Para obter mais informações sobre como instalar clientes do Configuration Manager utilizando push de cliente, consulte [implementar clientes em computadores Windows](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).|  
|**Exportarar**|Abre o **Assistente Exportar Objetos** que permite exportar esta consulta para um ficheiro de formato MOF (Managed Object Format) que pode, em seguida, ser importado noutro site.|Não existem informações adicionais.|  
|**Moverr**|Abre a caixa de diálogo **Mover Itens Selecionados** , na qual pode mover a consulta selecionada para uma pasta que criou anteriormente sob o nó **Consultas** .|Não existem informações adicionais.|  

## <a name="see-also"></a>Consulte Também  
 [Operações e manutenção de consultas no System Center Configuration Manager](../../../core/servers/manage/operations-and-maintenance-for-queries.md)
