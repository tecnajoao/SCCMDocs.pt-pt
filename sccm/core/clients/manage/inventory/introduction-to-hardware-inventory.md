---
title: 'Inventário de Hardware '
titleSuffix: Configuration Manager
description: Obtenha uma introdução ao inventário de hardware no System Center Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3969952e-9d05-49c9-82a2-e7e90ccef511
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 688bb6dc57f5d50e1807bff40a1d1a4c66f4b349
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="introduction-to-hardware-inventory-in-system-center-configuration-manager"></a>Introdução ao inventário de hardware no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize o inventário de hardware no System Center Configuration Manager para recolher informações sobre a configuração de hardware dos dispositivos cliente na sua organização. Para recolher o i inventário de hardware, a definição **Ativar inventário de hardware nos clientes** tem de estar ativada nas definições de cliente.  

 Depois do inventário de hardware está ativado e o cliente é executar um ciclo de inventário de hardware, o cliente envia as informações para um ponto de gestão no site do cliente. A gestão de pontos e reencaminha as informações de inventário para o servidor do site do Configuration Manager que armazena as informações de inventário na base de dados do site. O inventário de hardware é executado nos clientes, de acordo com a agenda que especificou nas definições de cliente.  

 Pode utilizar vários métodos para ver os dados de inventário de hardware recolhe do Configuration Manager. Os mesmos incluem os seguintes:  

-   [Criar consultas que devolvam os dispositivos que se baseiam numa configuração de hardware específico](../../../../core/servers/manage/queries-technical-reference.md).  

-   [Criar coleções baseadas em consultas que se baseiam numa configuração de hardware específico](../../../../core/clients/manage/collections/introduction-to-collections.md). As adesões a coleções baseadas em consultas são atualizadas automaticamente segundo uma agenda. Pode utilizar coleções para várias tarefas, que inclui a implementação de software. .  

-   [Executar relatórios que apresentam detalhes específicos sobre configurações de hardware na sua organização](../../../../core/servers/manage/reporting.md).   

-   [Utilize o Explorador de recursos](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md) para ver informações detalhadas sobre o inventário de hardware que é recolhido dos dispositivos cliente.   

 Quando executa o inventário de hardware num dispositivo cliente, os primeiros dados de inventário devolvidos pelo cliente são sempre um inventário completo. As informações de inventário subsequentes contêm apenas informações de inventário diferencial. O servidor do site processa as informações de inventário de diferenças pela ordem em que são recebidas. Se as informações de diferenças para um cliente estão em falta, o servidor do site rejeita informações adicionais de diferenças e indica ao cliente para executar um ciclo de inventário completo.  

 O Configuration Manager fornece suporte limitado para computadores de arranque duplo. O Configuration Manager pode detetar computadores de arranque duplo, mas só devolve informações de inventário do sistema operativo que estava ativo no momento o ciclo de inventário foi executada.  

> [!NOTE]  
>  Para obter informações sobre como utilizar o inventário de hardware com clientes que executam o Linux e UNIX, consulte [inventário de Hardware para Linux e UNIX no System Center Configuration Manager](../../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md).  

## <a name="extending-configuration-manager-hardware-inventory"></a>Expandir o inventário de hardware do Configuration Manager  
 Para além do inventário de hardware incorporado no Configuration Manager, também pode utilizar um dos seguintes métodos para expandir o inventário de hardware para recolher informações adicionais:  

- Pode ativar, desativar, adicionar e remover classes de inventário de hardware a partir da consola do Configuration Manager. |  
- Utilize ficheiros NOIDMIF para recolher informações sobre dispositivos cliente que não podem ser inventariados pelo Configuration Manager. Por exemplo, pode pretender recolher informações sobre o número de ativos de dispositivo existentes apenas como uma etiqueta no dispositivo. O inventário NOIDMIF é automaticamente associado ao dispositivo cliente a partir do qual foi recolhido.  
- Utilize ficheiros IDMIF para recolher informações sobre os recursos que não estão associados um cliente de Configuration Manager, por exemplo, projetores, fotocopiadoras e impressoras de rede.  

 Para obter mais informações sobre como utilizar estes métodos para expandir o inventário de hardware do Configuration Manager, consulte [como configurar inventário de hardware no System Center Configuration Manager](../../../../core/clients/manage/inventory/configure-hardware-inventory.md).  
