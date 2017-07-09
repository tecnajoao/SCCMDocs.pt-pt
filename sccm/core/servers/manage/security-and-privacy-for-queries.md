---
title: "Segurança e privacidade de consultas | Microsoft Docs"
description: "Entenda as melhores práticas de segurança e privacidade quando você consulta para obter informações do banco de dados do site."
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
ms.sourcegitcommit: 2087badc9dd1d216352dce232b145a786783ac89
ms.openlocfilehash: e42b13c68ecaeac94245838c2f42e2790799de2b
ms.contentlocale: pt-pt
ms.lasthandoff: 05/18/2017


---
# <a name="security-and-privacy-for-queries-in-system-center-configuration-manager"></a>Segurança e privacidade de consultas no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

Consultas no System Center Configuration Manager permitem recuperar informações do banco de dados de site com base nos critérios que você especificar. Gerenciador de configuração coleta as informações de banco de dados do site durante a operação padrão. Por exemplo, através da utilização de informações que tenham sido recolhidas pela deteção ou inventário, pode configurar uma consulta para identificar os dispositivos que cumprem critérios específicos.  

 Para obter mais informações sobre consultas, consulte [Introdução a consultas no System Center Configuration Manager](../../../core/servers/manage/introduction-to-queries.md). Para obter mais informações sobre práticas recomendadas de segurança e informações de privacidade para operações do Configuration Manager que coletam as informações que podem ser recuperadas por meio de consultas, consulte [segurança e privacidade para o System Center Configuration Manager](../../../core/plan-design/security/security-and-privacy.md).  

## <a name="security-best-practices-for-queries"></a>Melhores Práticas de Segurança para Consultas  
 Utilize a melhor prática de segurança seguinte para consultas.  

|Procedimento recomendado de segurança|Mais informações|  
|----------------------------|----------------------|  
|Quando você exportar ou importa uma consulta salva em um local de rede, proteja o local e o canal de rede.|Limite quem pode aceder à pasta de rede.<br /><br /> Utilize a assinatura SMB (Server Message Block) ou a segurança IPsec entre a localização de rede e o servidor do site para impedir que um atacante adultere os dados da consulta antes de serem importados.|  

## <a name="see-also"></a>Consulte também  
 [Referência técnica de consultas para o System Center Configuration Manager](../../../core/servers/manage/queries-technical-reference.md)

