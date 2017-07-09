---
title: Gerenciar uma assinatura do Intune associada com o System Center Configuration Manager | Microsoft Docs
description: Gerencie uma assinatura do Intune associada com o System Center Configuration Manager.
ms.custom: na
ms.date: 06/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9b494767-68c1-47b1-9a86-591bff0ad491
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 662901e850566756759fcfc61c58f3c0e56bc5aa
ms.openlocfilehash: 2cb4d724c8b78657458a30c0bb020f67c6b62795
ms.contentlocale: pt-pt
ms.lasthandoff: 06/03/2017

---
# <a name="manage-an-intune-subscription-associated-with-system-center-configuration-manager"></a>Gerenciar uma assinatura do Intune associada com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

Se você adicionar um Microsoft Intune (em uma assinatura de avaliação ou assinatura paga) ao Configuration Manager e, em seguida, é necessário alternar para uma assinatura diferente do Intune, será preciso excluir tanto a **assinatura do Microsoft Intune** e **ponto de conexão de serviço** do console do Configuration Manager antes de adicionar uma nova assinatura.

> [!NOTE]
> Você pode configurar apenas uma assinatura do Intune em uma hora no gerenciamento de dispositivo móvel híbrido.

## <a name="how-to-delete-an-intune-subscription-from-configuration-manager"></a>Como eliminar uma subscrição do Intune do Configuration Manager

> [!IMPORTANT]
>  Todo o conteúdo incluindo registros do usuário, políticas e implantações de aplicativo configurados para dispositivos gerenciados por assinatura do Intune são removidos quando você excluir a assinatura.

1.  No console do Configuration Manager, vá para **administração** > **visão geral** > **serviços de nuvem** > **assinaturas do Microsoft Intune**.

2.  Clique com botão direito listado **assinatura do Microsoft Intune**e, em seguida, clique em **excluir**.

3.   No assistente, clique em **remover assinatura do Microsoft Intune do Configuration Manager**, clique em **próximo**e, em seguida, clique em **próximo** novamente para remover a assinatura.


## <a name="how-to-remove-the-service-connection-point-role"></a>Como remover a função de ponto de conexão de serviço

1.  Vá para **administração** > **visão geral** > **configuração de Site** > **servidores e funções de sistema de Site**.

2.  Selecione o servidor que aloja a função **Ponto de ligação de serviço**.

3.  Na lista **Funções do Sistema de Sites**, selecione **Ponto de ligação de serviço** e, em seguida, clique em **Remover Função** no friso. Confirme que pretende remover a função. O ponto de ligação de serviço foi eliminado.

Agora pode criar um novo ponto de ligação de serviço, adicione uma nova subscrição do Intune ao Configuration Manager e defina o Configuration Manager como a Autoridade de MDM.

## <a name="how-to-change-mdm-authority-to-intune"></a>Como alterar a autoridade MDM como Intune
A partir do Configuration Manager versão 1610 e Microsoft Intune version 1705, você pode alterar sua autoridade MDM sem precisar entrar em contato com o Microsoft Support e sem a necessidade de cancelar o registro e registrar novamente os dispositivos gerenciados existentes. Para obter detalhes, consulte [alterar sua autoridade MDM](/sccm/mdm/deploy-use/change-mdm-authority).

