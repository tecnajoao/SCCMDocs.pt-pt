---
title: "Noções básicas do System Center Configuration Manager | Microsoft Docs"
description: "Saiba mais sobre conceitos básicos para o System Center Configuration Manager."
ms.custom: na
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc4cdb35-f0b4-42b5-9cec-6431a8c30793
caps.latest.revision: "11"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 662ac092746f37c354e5accf288e3375c16b9c72
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="fundamentals-of-system-center-configuration-manager"></a>Noções Básicas do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Se não estiver familiarizado para o System Center Configuration Manager, leia os tópicos fundamentais para saber mais sobre conceitos básicos para o Configuration Manager antes de executar o programa de configuração para instalar o primeiro site. Se estiver familiarizado com o Configuration Manager, em seguida, pode começar à direita em. Recomendamos que comece com [que há de novo no System Center Configuration Manager](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012).  

 Para obter mais informações sobre sistemas operativos e ambientes suportados, requisitos de hardware e informações de capacidade, veja [Configurações suportadas do System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md).  

 Quando implementar o Configuration Manager, implementar um ou mais sites:  

-   **Quando implementa vários sites**, os sites formam relações de subordinados para principais, coletivamente referidas como hierarquias. Utilize uma hierarquia para gerir centralmente um grande número de sites e dispositivos.  Dados e as informações fluem no sentido descendente da hierarquia para chegarem aos dispositivos que gere. Informações sobre dispositivos e resultados de configuração tarefas e os pedidos fluem no sentido ascendente da hierarquia.  

-   **Ao implementar um único site**, este também é referido como uma hierarquia.  

 Algumas tarefas e definições de configuração serão aplicadas a todos os sites numa hierarquia, enquanto outras se aplicam a sites individuais.  

## <a name="fundamental-concepts-for-system-center-configuration-manager"></a>Conceitos fundamentais do System Center Configuration Manager
Ver os seguintes tópicos para saber mais sobre conceitos fundamentais do System Center Configuration Manager:  

-   [Noções básicas sobre sites e hierarquias do System Center Configuration Manager](../../core/understand/fundamentals-of-sites-and-hierarchies.md)  

-   [Noções básicas de gestão de dispositivos com o System Center Configuration Manager](../../core/understand/fundamentals-of-managing-devices.md)  

-   [Noções básicas de tarefas de gestão de cliente para o System Center Configuration Manager](../../core/understand/fundamentals-of-client-management-tasks.md)  

-   [Noções básicas de segurança para o System Center Configuration Manager](../../core/understand/fundamentals-of-security.md)  
