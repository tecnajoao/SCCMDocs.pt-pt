---
title: "Inventário de software | Microsoft Docs"
description: "Obtenha uma introdução ao inventário de software no System Center Configuration Manager."
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 79eb49da-cd2b-4ffc-b355-b595aeba3aea
caps.latest.revision: "5"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 969f2d28649853ddc95860fe72597d6d2c9a94e9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="introduction-to-software-inventory-in-system-center-configuration-manager"></a>Introdução ao inventário de software no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize o inventário de software para recolher informações sobre ficheiros nos dispositivos cliente. Inventário de software também pode recolher ficheiros de dispositivos cliente e armazená-los no servidor do site. Inventário de software é recolhido quando escolhe o **ativar inventário de software em clientes** definir nas definições do cliente, onde pode também agendar a operação.  

Depois do inventário de software está ativado e os clientes executarem um ciclo de inventário de software, o cliente envia as informações para um ponto de gestão no site do cliente. A gestão de pontos e reencaminha as informações de inventário para o servidor de site do Configuration Manager, que armazena as informações na base de dados do site.   

 Seguem-se formas para ver os dados de inventário de software:  

-   [Criar consultas](../../../../core/servers/manage/queries-technical-reference.md) que devolvam os dispositivos com os ficheiros especificados.   

-   Criar [coleções baseadas em consulta](../../../../core/clients/manage/collections/introduction-to-collections.md) que incluem dispositivos com os ficheiros especificados.   

-   [Executar relatórios](../../../../core/servers/manage/reporting.md) que fornecem detalhes sobre os ficheiros em dispositivos.

-   Utilize [Explorador de recursos](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md) para examinar informações detalhadas sobre os ficheiros que foram inventariados e recolhidos a partir de dispositivos cliente.   

 Quando executa o inventário de software num dispositivo cliente, o primeiro relatório é um inventário completo. Os relatórios subsequentes contêm apenas informações de inventário de diferenças. O servidor do site processa as informações de diferenças pela ordem recebida. Se as informações de diferenças para um cliente estão em falta, o servidor do site rejeita as restantes informações de diferenças e indica ao cliente para executar um inventário completo.  

 O Configuration Manager pode detetar computadores de arranque duplo, mas só devolve informações de inventário do sistema operativo que estava ativo no momento do inventário.  

**Dispositivos móveis:** Consulte [inventário de software para dispositivos móveis inscritos com o Microsoft Intune](../../../../mdm/deploy-use/software-inventory-mobile-devices.md) para obter informações sobre a recolha do inventário para as aplicações instaladas em dispositivos móveis.
