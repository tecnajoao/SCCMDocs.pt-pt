---
title: "Introdução às consultas | Documentos do Microsoft"
description: "Criar e executar consultas para localizar objetos numa hierarquia do System Center Configuration Manager que correspondem aos seus critérios de consulta."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 03d1b3a9-41db-4d3a-a70e-e05ab5dc8141
caps.latest.revision: 5
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: f84d518670c0ece3c08c890d2293335518f7f8e9
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="introduction-to-queries-in-system-center-configuration-manager"></a>Introdução às consultas no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode criar e executar consultas para localizar objetos numa hierarquia do System Center Configuration Manager que correspondem aos seus critérios de consulta. Estes objetos incluem itens, tais como tipos específicos de computadores ou grupos de utilizadores. Consultas poderá devolver a maioria dos tipos de objetos do Configuration Manager, que incluem sites, coleções, aplicações e dados de inventário.  

 Quando cria uma consulta, tem de especificar um mínimo de dois parâmetros: onde pretende pesquisar e o que pretende procurar. Por exemplo, para localizar a quantidade de espaço de disco rígido que está disponível em todos os computadores num site do Configuration Manager, pode criar uma consulta para procurar o **disco lógico** atributo de classe e o **espaço livre (MB)** atributo para o espaço em disco rígido.  

 Depois de criar uma consulta inicial, pode especificar critérios de consulta adicionais. Por exemplo, pode especificar que os resultados da consulta incluem apenas os computadores que estão atribuídos a um site especificado. Também pode modificar a forma como os resultados são apresentados, para que possa visualizar os resultados por uma ordem que faça sentido para si. Por exemplo, pode especificar que os resultados são ordenados pela quantidade de espaço livre em disco rígido, por ordem ascendente ou descendente.  

 Quando cria uma consulta, é armazenado pelo Configuration Manager e apresentado no **consultas** nó o **monitorização** área de trabalho. A partir desta localização, pode criar uma nova consulta e, em seguida, executar, atualizar ou gerir uma consulta existente.  

 Também pode importar uma consulta para uma regra de consulta numa coleção do Configuration Manager. Para obter mais informações, consulte o artigo [como criar coleções no System Center Configuration Manager](../../../core/clients/manage/collections/create-collections.md).  

## <a name="see-also"></a>Consulte Também  
 [As consultas de referência técnica para o System Center Configuration Manager](../../../core/servers/manage/queries-technical-reference.md)

