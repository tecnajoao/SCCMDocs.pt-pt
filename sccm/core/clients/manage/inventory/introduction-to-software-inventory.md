---
title: "Inventário de software | Documentos do Microsoft"
description: "Obter uma introdução ao inventário de software no System Center Configuration Manager."
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 79eb49da-cd2b-4ffc-b355-b595aeba3aea
caps.latest.revision: 5
caps.handback.revision: 0
author: andredm7
ms.author: andredm
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: f9097014c7e988ec8e139e518355c4efb19172b3
ms.openlocfilehash: 969f2d28649853ddc95860fe72597d6d2c9a94e9
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="introduction-to-software-inventory-in-system-center-configuration-manager"></a>Introdução ao inventário de software no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize o inventário de software para recolher informações sobre ficheiros nos dispositivos cliente. Inventário de software também pode recolher ficheiros de dispositivos cliente e armazená-los no servidor do site. Inventário de software é recolhido quando escolhe o **ativar inventário de software nos clientes** definir nas definições de cliente, onde pode também agendar a operação.  

Depois de inventário de software está ativado e os clientes executarem um ciclo de inventário de software, o cliente envia as informações para um ponto de gestão no site do cliente. O ponto em seguida, gestão reencaminha as informações de inventário para o servidor de site do Configuration Manager, que armazena as informações na base de dados do site.   

 Existem formas de ver os dados de inventário de software:  

-   [Criar consultas](../../../../core/servers/manage/queries-technical-reference.md) que devolver dispositivos com ficheiros especificados.   

-   Criar [as coleções baseadas em consulta](../../../../core/clients/manage/collections/introduction-to-collections.md) que incluam dispositivos com ficheiros especificados.   

-   [Executar relatórios](../../../../core/servers/manage/reporting.md) que fornecem detalhes sobre ficheiros nos dispositivos.

-   Utilize [Explorador de recursos](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md) examinar informações detalhadas sobre os ficheiros que foram inventariados e recolhido dos dispositivos cliente.   

 Quando executa o inventário de software num dispositivo cliente, o primeiro relatório é um inventário completo. Relatórios subsequentes conter apenas informações de inventário de diferenças. O servidor do site processa informações de diferenças na ordem recebido. Se não visualizar informações de diferenças para um cliente, o servidor do site rejeita obter mais informações de diferenças e indica ao cliente para executar um inventário completo.  

 O Configuration Manager pode detetar computadores dual-arranque mas devolve apenas as informações de inventário do sistema operativo que estava ativo no momento da inventário.  

**Dispositivos móveis:** Consulte o artigo [inventário de software para dispositivos móveis inscritos com o Microsoft Intune](../../../../mdm/deploy-use/software-inventory-mobile-devices.md) para obter informações sobre a recolha do inventário para as aplicações instaladas em dispositivos móveis.

