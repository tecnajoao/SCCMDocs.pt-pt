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
ms.collection: M365-identity-device-management
ms.openlocfilehash: 54bcd177d228e67748f561be556ff4219523711a
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56130416"
---
# <a name="introduction-to-software-inventory-in-system-center-configuration-manager"></a>Introdução ao inventário de software no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize o inventário de software para recolher informações sobre ficheiros nos dispositivos cliente. Inventário de software também pode recolher ficheiros de dispositivos cliente e armazená-los no servidor do site. Inventário de software é recolhido ao escolher o **ativar o inventário de software nos clientes** definição nas definições do cliente, onde também pode agendar a operação.  

Depois do inventário de software está ativado e os clientes executarem um ciclo de inventário de software, o cliente envia as informações para um ponto de gestão no site do cliente. A gestão de ponto, em seguida, reencaminha as informações de inventário para o servidor de site do Configuration Manager, que armazena as informações da base de dados do site.   

 Seguem-se as formas de ver os dados de inventário de software:  

- [Criar consultas](../../../../core/servers/manage/queries-technical-reference.md) que devolvam os dispositivos com ficheiros especificados.   

- Crie [coleções baseadas em consulta](../../../../core/clients/manage/collections/introduction-to-collections.md) que incluem dispositivos com ficheiros especificados.   

- [Executar relatórios](../../../../core/servers/manage/reporting.md) que fornecem detalhes sobre os ficheiros em dispositivos.

- Uso [Explorador de recursos](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md) para examinem informações detalhadas sobre os ficheiros que foram inventariados e recolhidos a partir de dispositivos cliente.   

  Quando executa o inventário de software no dispositivo cliente, o primeiro relatório é um inventário completo. Relatórios de subsequentes contêm apenas informações de inventário de diferenças. O servidor do site processa as informações de diferenças pela ordem recebida. Se as informações de diferenças para um cliente estão em falta, o servidor do site rejeita as restantes informações de diferenças e indica ao cliente para executar um inventário completo.  

  O Configuration Manager pode detetar computadores de arranque duplo, mas só devolve informações de inventário do sistema operativo que estava ativo no momento do inventário.  

**Dispositivos móveis:** Ver [inventário de software para dispositivos móveis inscritos com o Microsoft Intune](../../../../mdm/deploy-use/software-inventory-mobile-devices.md) para obter informações sobre a recolha de inventário de aplicações instaladas em dispositivos móveis.
