---
title: "Inventário de hardware – Configuration Manager | Documentos do Microsoft"
description: "Obter uma introdução ao inventário de hardware no System Center Configuration Manager."
ms.custom: na
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3969952e-9d05-49c9-82a2-e7e90ccef511
caps.latest.revision: 6
caps.handback.revision: 0
author: andredm7
ms.author: andredm
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 9c5d1e48b76392beaf54b5377c69b648537e86f8
ms.openlocfilehash: c64f0b42bff25e8e91cf9101d6fbb538634eab15
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="introduction-to-hardware-inventory-in-system-center-configuration-manager"></a>Introdução ao inventário de hardware no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize o inventário de hardware no System Center Configuration Manager para recolher informações sobre a configuração de hardware dos dispositivos cliente na sua organização. Para recolher o i inventário de hardware, a definição **Ativar inventário de hardware nos clientes** tem de estar ativada nas definições de cliente.  

 Depois de inventário de hardware é ativado e um ciclo de inventário de hardware é executado pelo cliente, o cliente envia as informações para um ponto de gestão no site do cliente. O ponto em seguida, gestão reencaminha as informações de inventário para o servidor do site do Configuration Manager que armazena as informações de inventário na base de dados do site. O inventário de hardware é executado nos clientes, de acordo com a agenda que especificou nas definições de cliente.  

 Pode utilizar vários métodos para ver os dados de inventário de hardware que recolhe do Configuration Manager. Os mesmos incluem os seguintes:  

-   [Criar consultas que devolvem os dispositivos que se baseiam numa configuração de hardware específico](../../../../core/servers/manage/queries-technical-reference.md).  

-   [Criar coleções baseadas em consulta que se baseiam numa configuração de hardware específico](../../../../core/clients/manage/collections/introduction-to-collections.md). As adesões a coleções baseadas em consultas são atualizadas automaticamente segundo uma agenda. Pode utilizar coleções para várias tarefas, que inclui a implementação de software. .  

-   [Executar relatórios que apresentam detalhes específicos sobre configurações de hardware na sua organização](../../../../core/servers/manage/reporting.md).   

-   [Utilize o Explorador de recursos](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md) para ver informações detalhadas sobre o inventário de hardware que é recolhida a partir dos dispositivos cliente.   

 Quando executa o inventário de hardware num dispositivo cliente, os primeiros dados de inventário devolvidos pelo cliente são sempre um inventário completo. As informações de inventário subsequentes contêm apenas informações de inventário diferencial. O servidor do site processa as informações de inventário de diferenças pela ordem em que são recebidas. Se não visualizar informações de diferenças para um cliente, o servidor do site rejeita informações adicionais de diferenças e indica ao cliente de executar um ciclo de inventário completo.  

 O Configuration Manager oferece suporte limitado para computadores de arranque duplo. O Configuration Manager pode detetar computadores dual-arranque mas só devolve informações sobre o inventário do sistema operativo que estava ativo no momento em que o ciclo de inventário foi executada.  

> [!NOTE]  
>  Para obter informações sobre como utilizar o inventário de hardware com clientes que executam o Linux e UNIX, consulte o artigo [inventário de Hardware para Linux e UNIX no System Center Configuration Manager](../../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md).  

## <a name="extending-configuration-manager-hardware-inventory"></a>Expandir o inventário de hardware do Configuration Manager  
 Para além do inventário de hardware incorporadas no Configuration Manager, também pode utilizar um dos seguintes métodos para expandir o inventário de hardware para recolher informações adicionais:  

- Pode ativar, desativar, adicionar e remover classes de inventário para o inventário de hardware a partir da consola do Configuration Manager. |  
- Utilize os ficheiros NOIDMIF para recolher informações sobre os dispositivos cliente que não pode ser inventariado pelo Configuration Manager. Por exemplo, pode pretender recolher informações sobre o número de ativos de dispositivo existentes apenas como uma etiqueta no dispositivo. O inventário NOIDMIF é automaticamente associado ao dispositivo cliente a partir do qual foi recolhido.  
- Utilize os ficheiros IDMIF para recolher informações sobre elementos que não estão associados um cliente do Configuration Manager, por exemplo, projetores, photocopiers e impressoras de rede.  

 Para obter mais informações sobre como utilizar estes métodos para expandir o inventário de hardware do Configuration Manager, consulte o artigo [como configurar inventário de hardware no System Center Configuration Manager](../../../../core/clients/manage/inventory/configure-hardware-inventory.md).  

