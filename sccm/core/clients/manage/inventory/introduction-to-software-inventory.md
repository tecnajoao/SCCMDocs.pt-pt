---
title: Inventário de software
titleSuffix: Configuration Manager
description: Obtenha uma introdução ao inventário de software no System Center Configuration Manager.
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 79eb49da-cd2b-4ffc-b355-b595aeba3aea
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4fe27423391cbdc4767e18a06c73b23cbb302ab5
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32332515"
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
