---
title: "Sincronizar remotamente política em dispositivos inscritos com o Intune | Documentos do Microsoft"
description: "Saiba como sincronizar a política em dispositivos inscritos do Intune a partir da consola do Configuration Manager"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b3731ad0-2a24-4042-994e-5e4c1230e3fe
caps.latest.revision: 18
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 337814fd5ba49ed17fc97aba49f79f02df817f4e
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="remotely-synchronize-policy-on-intune-enrolled-devices-from-the-configuration-manager-console"></a>Sincronizar remotamente política em dispositivos inscritos do Intune a partir da consola do Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Pode pedir uma sincronização de política para um dispositivo é inscrito com o Intune a partir da consola do Configuration Manager em vez de ter que pedir uma sincronização da aplicação Portal da empresa no dispositivo automaticamente. 

Para efetuar este procedimento:

1.    Selecione um dispositivo em **ativos e compatibilidade** > **descrição geral** > **dispositivos**.
2.    Clique em **enviar pedido de sincronização** no **ações de dispositivo remotas** menu.


Depois de cinco a dez minutos, quaisquer alterações na política serão sincronizadas para o dispositivo. Pode ver informações de estado do pedido de sincronização numa nova coluna em vistas de dispositivo, denominado **estado da sincronização de remoto**, também, na secção de dados de deteção do **propriedades** caixa de diálogo para cada dispositivo.

