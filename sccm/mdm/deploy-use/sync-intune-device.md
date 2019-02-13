---
title: Remotamente sincronizar política em dispositivos inscritos com o Intune
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
ms.collection: M365-identity-device-management
ms.openlocfilehash: eab8f812b8772be0812437359275b80702f5760c
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56137750"
---
# <a name="remotely-synchronize-policy-on-intune-enrolled-devices-from-the-configuration-manager-console"></a>Remotamente sincronizar política nos dispositivos inscritos no Intune a partir da consola do Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Pode pedir uma sincronização de política para um dispositivo que está inscrito no Intune a partir da consola do Configuration Manager em vez de precisar de pedir uma sincronização a partir da aplicação Portal da empresa no próprio dispositivo. 

Para efetuar este procedimento:

1.  Selecione um dispositivo sob **ativos e compatibilidade** > **descrição geral** > **dispositivos**.
2.  Clique em **enviar pedido de sincronização** no **ações do dispositivo remoto** menu.


Depois de cinco a dez minutos, quaisquer alterações na política serão sincronizadas com o dispositivo. Pode ver informações de estado do pedido de sincronização numa nova coluna em modos de exibição do dispositivo, chamado **estado de sincronização de remoto**, bem como na seção de dados de deteção do **propriedades** caixa de diálogo para cada dispositivo.
