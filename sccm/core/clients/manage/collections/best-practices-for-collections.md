---
title: "Coleções de melhores práticas | Microsoft Docs"
description: "Obter as melhores práticas para coleções no System Center Configuration Manager."
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7a2abb79-9ae5-4a25-9e18-5dcf528de3bf
caps.latest.revision: "4"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: fd62af3910c0745e0f1105417701b894e10cbbac
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="best-practices-for-collections-in-system-center-configuration-manager"></a>Melhores práticas para coleções no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize as seguintes melhores práticas para coleções no System Center Configuration Manager.  

## <a name="do-not-use-incremental-updates-for-a-large-number-of-collections"></a>Não utilizar atualizações incrementais num grande número de coleções  
 Quando ativa a opção **Utilizar atualizações incrementais para esta coleção** , esta configuração poderá causar atrasos de avaliação se a ativar em muitas coleções. O limite é de cerca de 200 coleções na sua hierarquia. O número exato depende dos seguintes fatores:  

-   O número total de coleções  

-   A frequência de novos recursos a ser adicionados e alterados na hierarquia  

-   O número de clientes na hierarquia  

-   A complexidade das regras de associação de coleções na hierarquia  

## <a name="make-sure-that-maintenance-windows-are-large-enough-to-deploy-critical-software-updates"></a>Certifique-se de que as janelas de manutenção são suficientemente abrangentes para implementar atualizações de software críticas  
 Pode configurar as janelas de manutenção para coleções de dispositivos restringir o número de vezes que o Configuration Manager pode instalar software nestes dispositivos. Se configurar a janela de manutenção para um período pequeno, o cliente pode não conseguir instalar as atualizações de software críticas, o que deixará o cliente vulnerável ao ataque que seria mitigado pela atualização de software.  
