---
title: Segurança e privacidade para consultas
titleSuffix: Configuration Manager
description: Compreenda as melhores práticas para segurança e privacidade quando consulta para obter informações da base de dados do site.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 30080620-20d3-4c38-b8dd-db5516e1acae
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7cdd9731b2ae34e096159b9e73c730fcbd7ac728
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56121537"
---
# <a name="security-and-privacy-for-queries-in-system-center-configuration-manager"></a>Segurança e privacidade para consultas no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Consultas no System Center Configuration Manager permitem-lhe obter informações a partir da base de dados do site com base nos critérios que especificar. O Configuration Manager recolhe as informações de base de dados do site durante o funcionamento normal. Por exemplo, através da utilização de informações que tenham sido recolhidas pela deteção ou inventário, pode configurar uma consulta para identificar os dispositivos que cumprem critérios específicos.  

 Para obter mais informações sobre consultas, consulte [introdução às consultas no System Center Configuration Manager](../../../core/servers/manage/introduction-to-queries.md). Para obter mais informações sobre melhores práticas de segurança e informações de privacidade para operações do Configuration Manager que recolhem as informações que pode obter utilizando consultas, consulte [segurança e privacidade para a configuração do System Center Manager](../../../core/plan-design/security/security-and-privacy.md).  

## <a name="security-best-practices-for-queries"></a>Melhores Práticas de Segurança para Consultas  
 Utilize a melhor prática de segurança seguinte para consultas.  

|Procedimento recomendado de segurança|Mais informações|  
|----------------------------|----------------------|  
|Sempre que exportar ou importar uma consulta que é guardada numa localização de rede, proteja a localização e o canal de rede.|Limite quem pode aceder à pasta de rede.<br /><br /> Utilize a assinatura SMB (Server Message Block) ou a segurança IPsec entre a localização de rede e o servidor do site para impedir que um atacante adultere os dados da consulta antes de serem importados.|  

## <a name="see-also"></a>Consulte também  
 [Referência técnica para consultas no System Center Configuration Manager](../../../core/servers/manage/queries-technical-reference.md)
