---
title: "Serviço Windows | Microsoft Docs"
description: "Utilize as janelas de serviço para controlar quando o System Center Configuration Manager sites instalam atualizações."
ms.custom: na
ms.date: 1/11/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ca4886d4-7173-46be-8dcd-1657d5b0deb9
caps.latest.revision: "4"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: d06a2a955ff59fa84bb844033fe31874fc735087
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
#  <a name="service-windows-for-site-servers"></a>Janelas de serviço dos servidores de site

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode configurar as janelas de serviço em sites de administração central e sites primários para controlar quando podem instalar atualizações na consola.  Pode configurar várias janelas, com a janela de permissão para instalar as atualizações que está a ser determinadas por uma combinação de todas as janelas de serviço para esse servidor de site.

Quando não estiver configurada nenhuma janela de serviço:
- **No seu site de nível superior** (um site de administração central ou site primário autónomo) que escolher quando iniciar a instalação da atualização.
- **Num site primário subordinado**, a atualização instala automaticamente após a conclusão da atualização instalação no site de administração central.
- **Num site secundário**, as atualizações nunca iniciam automaticamente. Em vez disso, tem de iniciar manualmente a instalação de atualização a partir da consola, depois do site primário principal tem de instalar a atualização.

Quando uma janela de serviço estiver configurada:
- **No seu site de nível superior**, não será possível iniciar a instalação de qualquer nova atualização a partir da consola do Configuration Manager. Mesmo com uma janela de serviço configurada, o site transfere automaticamente as atualizações para estas estão prontas para instalação.  
- **Num site primário subordinado**, as atualizações que têm instalado um site de administração central irão transferir para o site primário, mas não o fizer automaticamente início. Não é possível iniciar manualmente a instalação de uma atualização durante um período de tempo que está bloqueado pela utilização de uma janela de serviço. Cada vez quando janelas de serviço já não bloco da instalação da atualização, a atualização são instalados automaticamente é iniciado.
- **Os sites secundários** não suportam janelas de serviço e instalar atualizações automaticamente. Depois do site primário principal de um site secundário instala uma atualização, pode iniciar a atualização do site secundário da consola do.

## <a name="to-configure-a-service-window"></a>Para configurar uma janela de serviço

1.  Na consola do Configuration Manager abra **administração** > **configuração do Site** > **Sites**e, em seguida, selecione o servidor do site onde pretende configurar uma janela de serviço.  

2.  Em seguida, edite as **Propriedades** dos servidores do site e selecione o separador **Período de Administração** , onde pode configurar um ou mais períodos de administração para esse servidor do site.  
