---
title: Introdução às consultas
titleSuffix: Configuration Manager
description: Criar e executar consultas para localizar objetos numa hierarquia do System Center Configuration Manager que correspondem aos seus critérios de consulta.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 03d1b3a9-41db-4d3a-a70e-e05ab5dc8141
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3812953df11daff9d768aa808edd0bcb08ab66f5
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56124818"
---
# <a name="introduction-to-queries-in-system-center-configuration-manager"></a>Introdução às consultas no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode criar e executar consultas para localizar objetos numa hierarquia do System Center Configuration Manager que correspondem aos seus critérios de consulta. Estes objetos incluem itens, tais como tipos específicos de computadores ou grupos de utilizadores. As consultas podem devolver a maioria dos tipos de objetos do Configuration Manager, que incluem sites, coleções, aplicações e dados de inventário.  

 Quando cria uma consulta, tem de especificar um mínimo de dois parâmetros: onde pretende pesquisar e o que pretende procurar. Por exemplo, para localizar a quantidade de espaço de disco rígido que está disponível em todos os computadores num site do Configuration Manager, pode criar uma consulta para procurar o **disco lógico** classe de atributo e o **espaço livre (MB)** atributo de espaço em disco disponível.  

 Depois de criar uma consulta inicial, pode especificar critérios de consulta adicionais. Por exemplo, pode especificar que os resultados da consulta incluem apenas os computadores que estão atribuídos a um site especificado. Também pode modificar a forma como os resultados são apresentados, para que possa visualizar os resultados por uma ordem que faça sentido para si. Por exemplo, pode especificar que os resultados são ordenados pela quantidade de espaço livre em disco rígido, por ordem ascendente ou descendente.  

 Quando cria uma consulta, são armazenado pelo Configuration Manager e apresentado no **consultas** nó a **monitorização** área de trabalho. A partir desta localização, pode criar uma nova consulta e, em seguida, executar, atualizar ou gerir uma consulta existente.  

 Também pode importar uma consulta para uma regra de consulta numa coleção do Configuration Manager. Para obter mais informações, consulte [como criar coleções no System Center Configuration Manager](../../../core/clients/manage/collections/create-collections.md).  

## <a name="see-also"></a>Consulte Também  
 [Referência técnica para consultas no System Center Configuration Manager](../../../core/servers/manage/queries-technical-reference.md)
