---
title: Coleções de melhores práticas
titleSuffix: Configuration Manager
description: Obtenha melhores práticas para coleções no System Center Configuration Manager.
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 7a2abb79-9ae5-4a25-9e18-5dcf528de3bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1c685cf4efd5eca5f93694edd4a01715120df9a8
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56140580"
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
 Pode configurar janelas de manutenção para coleções de dispositivos restringir os tempos de que o Configuration Manager pode instalar software nestes dispositivos. Se configurar a janela de manutenção para um período pequeno, o cliente pode não conseguir instalar as atualizações de software críticas, o que deixará o cliente vulnerável ao ataque que seria mitigado pela atualização de software.  
