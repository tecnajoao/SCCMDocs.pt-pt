---
title: "Introdução às consultas | Microsoft Docs"
description: "Criar e executar consultas para localizar objetos numa hierarquia do System Center Configuration Manager que correspondam aos critérios de consulta."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 03d1b3a9-41db-4d3a-a70e-e05ab5dc8141
caps.latest.revision: "5"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: a1bb67b786aa452452585f2f7a2aa7c9ca4e12bf
ms.sourcegitcommit: b438515490e04fb09c82a8af642d38e9a0605178
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/15/2017
---
# <a name="introduction-to-queries-in-system-center-configuration-manager"></a>Introdução às consultas no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode criar e executar consultas para localizar objetos numa hierarquia do System Center Configuration Manager que correspondam aos critérios de consulta. Estes objetos incluem itens, tais como tipos específicos de computadores ou grupos de utilizadores. As consultas podem devolver a maior parte dos tipos de objetos do Configuration Manager, que incluem sites, coleções, aplicações e dados de inventário.  

 Quando cria uma consulta, tem de especificar um mínimo de dois parâmetros: onde pretende pesquisar e o que pretende procurar. Por exemplo, para localizar a quantidade de espaço de disco rígido que está disponível em todos os computadores num site do Configuration Manager, pode criar uma consulta para procurar o **disco lógico** classe de atributo e o **espaço livre (MB)** atributo de espaço em disco de rígido disponível.  

 Depois de criar uma consulta inicial, pode especificar critérios de consulta adicionais. Por exemplo, pode especificar que os resultados da consulta incluem apenas os computadores que estão atribuídos a um site especificado. Também pode modificar a forma como os resultados são apresentados, para que possa visualizar os resultados por uma ordem que faça sentido para si. Por exemplo, pode especificar que os resultados são ordenados pela quantidade de espaço livre em disco rígido, por ordem ascendente ou descendente.  

 Quando cria uma consulta, são armazenado pelo Configuration Manager e apresentado no **consultas** no nó de **monitorização** área de trabalho. A partir desta localização, pode criar uma nova consulta e, em seguida, executar, atualizar ou gerir uma consulta existente.  

 Também pode importar uma consulta para uma regra de consulta numa coleção do Configuration Manager. Para obter mais informações, consulte [como criar coleções no System Center Configuration Manager](../../../core/clients/manage/collections/create-collections.md).  

## <a name="see-also"></a>Consulte Também  
 [Referência técnica de consultas para o System Center Configuration Manager](../../../core/servers/manage/queries-technical-reference.md)
