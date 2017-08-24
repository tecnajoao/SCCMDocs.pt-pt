---
title: "Sincronizar remotamente política nos dispositivos inscritos no Intune | Microsoft Docs"
description: "Saiba como sincronizar política nos dispositivos inscritos no Intune a partir da consola do Configuration Manager"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b3731ad0-2a24-4042-994e-5e4c1230e3fe
caps.latest.revision: "18"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 337814fd5ba49ed17fc97aba49f79f02df817f4e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="remotely-synchronize-policy-on-intune-enrolled-devices-from-the-configuration-manager-console"></a>Sincronizar remotamente política nos dispositivos inscritos no Intune a partir da consola do Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Pode pedir uma sincronização de política para um dispositivo que está inscrito no Intune a partir da consola do Configuration Manager em vez de ter que pedir uma sincronização da aplicação Portal da empresa no dispositivo propriamente dito. 

Para efetuar este procedimento:

1.  Selecione um dispositivo em **ativos e compatibilidade** > **descrição geral** > **dispositivos**.
2.  Clique em **enviar pedido de sincronização** no **ações do dispositivo remoto** menu.


Após cinco a dez minutos, serão sincronizadas as alterações na política para o dispositivo. Pode ver informações de estado de pedido de sincronização numa nova coluna nas vistas de dispositivo, denominado **estado de sincronização remoto**, bem como na secção de dados de deteção do **propriedades** caixa de diálogo para cada dispositivo.
