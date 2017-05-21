---
title: "Segurança e privacidade para consultas | Documentos do Microsoft"
description: "Compreenda os procedimentos recomendados de segurança e privacidade quando consultar informações sobre a base de dados do site."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 30080620-20d3-4c38-b8dd-db5516e1acae
caps.latest.revision: 5
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 09f7bdaa29a01fb2a38aa223db56b5bce3bc5205
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="security-and-privacy-for-queries-in-system-center-configuration-manager"></a>Segurança e privacidade para consultas no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Consultas no System Center Configuration Manager permitem-lhe obter informações a partir da base de dados do site com base nos critérios que especificar. O Configuration Manager recolhe as informações de base de dados do site durante o funcionamento normal. Por exemplo, através da utilização de informações que tenham sido recolhidas pela deteção ou inventário, pode configurar uma consulta para identificar os dispositivos que cumprem critérios específicos.  

 Para obter mais informações sobre consultas, consulte o artigo [introdução às consultas no System Center Configuration Manager](../../../core/servers/manage/introduction-to-queries.md). Para obter mais informações sobre as melhores práticas de segurança e informações de privacidade para operações do Configuration Manager que recolhe as informações que pode obter através de consultas, consulte [segurança e privacidade para o System Center Configuration Manager](../../../core/plan-design/security/security-and-privacy.md).  

## <a name="security-best-practices-for-queries"></a>Melhores Práticas de Segurança para Consultas  
 Utilize a melhor prática de segurança seguinte para consultas.  

|Procedimento recomendado de segurança|Mais informações|  
|----------------------------|----------------------|  
|Sempre que exportar ou importar uma consulta guardada numa localização de rede, proteja a localização e o canal de rede.|Limite quem pode aceder à pasta de rede.<br /><br /> Utilize a assinatura SMB (Server Message Block) ou a segurança IPsec entre a localização de rede e o servidor do site para impedir que um atacante adultere os dados da consulta antes de serem importados.|  

## <a name="see-also"></a>Consulte Também  
 [As consultas de referência técnica para o System Center Configuration Manager](../../../core/servers/manage/queries-technical-reference.md)

