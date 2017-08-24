---
title: "Segurança e privacidade para consultas | Microsoft Docs"
description: "Compreenda as melhores práticas de segurança e privacidade quando consulta para obter informações da base de dados do site."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 30080620-20d3-4c38-b8dd-db5516e1acae
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: e42b13c68ecaeac94245838c2f42e2790799de2b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-queries-in-system-center-configuration-manager"></a>Segurança e privacidade para consultas no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

As consultas no System Center Configuration Manager permitem-lhe obter as informações da base de dados de site com base nos critérios que especificar. O Configuration Manager recolhe as informações de base de dados do site durante o funcionamento normal. Por exemplo, através da utilização de informações que tenham sido recolhidas pela deteção ou inventário, pode configurar uma consulta para identificar os dispositivos que cumprem critérios específicos.  

 Para obter mais informações sobre consultas, consulte [introdução às consultas no System Center Configuration Manager](../../../core/servers/manage/introduction-to-queries.md). Para obter mais informações sobre melhores práticas de segurança e informações de privacidade para operações do Configuration Manager que recolher as informações que pode obter utilizando consultas, consulte [segurança e privacidade para o System Center Configuration Manager](../../../core/plan-design/security/security-and-privacy.md).  

## <a name="security-best-practices-for-queries"></a>Melhores Práticas de Segurança para Consultas  
 Utilize a melhor prática de segurança seguinte para consultas.  

|Procedimento recomendado de segurança|Mais informações|  
|----------------------------|----------------------|  
|Sempre que exporta ou importar uma consulta que é guardada numa localização de rede, proteja a localização e o canal de rede.|Limite quem pode aceder à pasta de rede.<br /><br /> Utilize a assinatura SMB (Server Message Block) ou a segurança IPsec entre a localização de rede e o servidor do site para impedir que um atacante adultere os dados da consulta antes de serem importados.|  

## <a name="see-also"></a>Consulte também  
 [Referência técnica de consultas para o System Center Configuration Manager](../../../core/servers/manage/queries-technical-reference.md)
