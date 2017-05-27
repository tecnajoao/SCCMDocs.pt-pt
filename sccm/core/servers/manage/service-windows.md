---
title: "Serviço Windows | Documentos do Microsoft"
description: "Utilize as janelas de serviço para controlar quando os sites do System Center Configuration Manager instalarem atualizações."
ms.custom: na
ms.date: 1/11/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ca4886d4-7173-46be-8dcd-1657d5b0deb9
caps.latest.revision: 4
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0d0735c170820259ac8bb6706aac7cc5569a1628
ms.openlocfilehash: d06a2a955ff59fa84bb844033fe31874fc735087
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
#  <a name="service-windows-for-site-servers"></a>Janelas de serviço dos servidores de site

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Poderá configurar janelas de serviço em sites de administração central e sites primários para controlar quando podem instalar as atualizações na consola.  Pode configurar várias janelas, com a janela permitida para a instalação de atualizações de que está a ser determinadas por uma combinação de todas as janelas de serviço para esse servidor do site.

Quando não é configurada nenhuma janela de serviço:
- **No seu site de nível superior** (um site de administração central ou site primário autónomo) que escolher quando iniciar a instalação da atualização.
- **Num site primário subordinado**, a atualização instala automaticamente após a atualização de concluir a instalação do site de administração central.
- **Num site secundário**, atualizações nunca iniciam automaticamente. Em vez disso, tem de iniciar manualmente a instalação da atualização a partir de dentro da consola, depois do site primário principal tem instalada a atualização.

Quando uma janela de serviço está configurada:
- **No seu site de nível superior**, não será possível iniciar a instalação de qualquer nova atualização a partir da consola do Configuration Manager. Mesmo com uma janela de serviço configurada, o site transfere automaticamente atualizações de modo a ficarem prontos para instalar.  
- **Num site primário subordinado**, as atualizações instaladas no site de administração central irão transferir para o site primário, mas não o fizer automaticamente início. Não é possível iniciar manualmente a instalação de uma atualização durante um período de tempo que está bloqueada por utilização de uma janela de serviço. Cada vez ao windows serviço já não bloquear a instalação de atualização, a atualização instala automaticamente iniciado.
- **Os sites secundários** não suportam janelas de serviço e não instalam automaticamente as atualizações. Depois do site primário principal de um site secundário instala uma atualização, pode começar a atualização do site secundário a partir de dentro da consola.

## <a name="to-configure-a-service-window"></a>Para configurar uma janela de serviço

1.  Na consola do Configuration Manager abrir **administração** > **configuração do Site** > **Sites**e, em seguida, selecione o servidor do site onde pretende configurar uma janela de serviço.  

2.  Em seguida, edite as **Propriedades** dos servidores do site e selecione o separador **Período de Administração** , onde pode configurar um ou mais períodos de administração para esse servidor do site.  

