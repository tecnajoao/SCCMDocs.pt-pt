---
title: "Planear a implementação do cliente para computadores Mac | Microsoft Docs"
description: "Planear a implementação do cliente para computadores Mac no System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 8d15ae3f-de42-461f-a907-c43873da22d2
caps.latest.revision: "6"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 75bddb41d4d1cf209fa7595c52b5a6aa831ba3dd
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="planning-for-client-deployment-to-mac-computers-in-system-center-configuration-manager"></a>Planear a implementação do cliente para computadores Mac no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode instalar o cliente do Configuration Manager em computadores Mac que executam o sistema de operativo Mac OS X e utilizam as seguintes capacidades de gestão:  

-   **Inventário de hardware**  

     Pode utilizar o inventário de hardware do Configuration Manager para recolher informações sobre o hardware e aplicações instaladas em computadores Mac. Estas informações podem ser visualizadas no Explorador de recursos na consola do Configuration Manager e utilizadas para criar coleções, consultas e relatórios. Para obter mais informações, consulte [como utilizar o Explorador de recursos para ver o inventário de hardware no System Center Configuration Manager](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).  

     O Configuration Manager recolhe as seguintes informações de hardware de computadores Mac:  

    -   Processador  

    -   Sistema de computador  

    -   Unidade de disco  

    -   Partição de disco  

    -   Adaptador de rede  

    -   Sistema Operativo  

    -   Serviço  

    -   Processo  

    -   Software instalado  

    -   Produto de sistema do computador  

    -   Controlador USB  

    -   Dispositivo USB  

    -   Unidade de CD-ROM  

    -   Controlador de vídeo  

    -   Monitor de secretária  

    -   Bateria portátil  

    -   Memória física  

    -   Impressora  

    > [!IMPORTANT]  
    >  Não é possível expandir as informações de hardware recolhidas de computadores Mac durante o inventário de hardware.  

-   **Definições de compatibilidade**  

     Pode utilizar as definições de compatibilidade do Configuration Manager para ver a compatibilidade e remediar as definições de preferência (. plist) do Mac OS X. Por exemplo, pode impor definições para a home page do Safari browser ou certifique-se de que a firewall Apple está ativada. Também pode utilizar scripts de shell para monitorizar e remediar as definições no MAC OS X.  

-   **Gestão de aplicações**  

     O Configuration Manager pode implementar software em computadores Mac. Pode implementar os seguintes formatos de software para computadores Mac:  

    -   Imagem de disco Apple (. DMG)  

    -   Ficheiro de pacote meta (. MPKG)  

    -   Mac pacote instalador OS X (. PKG)  

    -   Aplicação do Mac OS X (. APLICAÇÃO)  

 Quando instalar o cliente do Configuration Manager em computadores Mac, não é possível utilizar as seguintes capacidades de gestão que são suportadas pelo cliente do Configuration Manager em computadores baseados em Windows:  

-   Instalação push do cliente  

-   Implementação do sistema operativo  

-   Atualizações de software  

    > [!NOTE]  
    >  Pode utilizar a gestão de aplicações do Configuration Manager para implementar atualizações de software necessárias do Mac OS X em computadores Mac. Além disso, pode utilizar as definições de compatibilidade para se certificar de que os computadores têm todas as atualizações de software necessárias.  

-   Janelas de manutenção  

-   Controlo remoto  

-   Gestão de energia  

-   Verificação de cliente do estado do cliente e remediação  

 Para obter mais informações sobre como instalar e configurar o cliente do Configuration Manager Mac, consulte [como implementar clientes em Mac no System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-macs.md).
