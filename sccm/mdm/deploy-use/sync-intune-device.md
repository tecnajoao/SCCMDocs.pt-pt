---
title: Sincronizar remotamente política nos dispositivos inscritos no Intune
titleSuffix: Configuration Manager
description: Saiba como sincronizar política nos dispositivos inscritos no Intune a partir da consola do Configuration Manager
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: b3731ad0-2a24-4042-994e-5e4c1230e3fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3ecd2c480ab67a82539edff6daa18ef0f93628c6
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32345720"
---
# <a name="remotely-synchronize-policy-on-intune-enrolled-devices-from-the-configuration-manager-console"></a>Sincronizar remotamente política nos dispositivos inscritos no Intune a partir da consola do Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Pode pedir uma sincronização de política para um dispositivo que está inscrito no Intune a partir da consola do Configuration Manager em vez de ter que pedir uma sincronização da aplicação Portal da empresa no dispositivo propriamente dito. 

Para efetuar este procedimento:

1.  Selecione um dispositivo em **ativos e compatibilidade** > **descrição geral** > **dispositivos**.
2.  Clique em **enviar pedido de sincronização** no **ações do dispositivo remoto** menu.


Após cinco a dez minutos, serão sincronizadas as alterações na política para o dispositivo. Pode ver informações de estado de pedido de sincronização numa nova coluna nas vistas de dispositivo, denominado **estado de sincronização remoto**, bem como na secção de dados de deteção do **propriedades** caixa de diálogo para cada dispositivo.
