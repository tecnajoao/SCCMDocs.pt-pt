---
title: "Gerir uma subscrição do Intune associada com o System Center Configuration Manager | Documentos do Microsoft"
description: "Gerir uma subscrição do Intune associada com o System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
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
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 2e0b3cd1070d0f8adb1219acd33c3126d2758a49
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="manage-an-intune-subscription-associated-with-system-center-configuration-manager"></a>Gerir uma subscrição do Intune associada com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Se adicionar um Microsoft Intune (uma subscrição de avaliação ou subscrição paga) do Configuration Manager e, em seguida, ter de mudar para outra subscrição do Intune, tem de eliminar ambos o **subscrição do Windows Intune** e **ponto de ligação de serviço** a partir da consola do Configuration Manager antes de poder adicionar uma nova subscrição.

> [!NOTE]
> Pode configurar apenas uma subscrição do Intune cada vez em gestão de dispositivos móveis híbrida.

## <a name="how-to-delete-an-intune-subscription-from-configuration-manager"></a>Como eliminar uma subscrição do Intune do Configuration Manager

> [!IMPORTANT]
>  Todo o conteúdo incluindo inscrições através do utilizador, as políticas e as implementações das aplicações configuradas para dispositivos geridos pela subscrição do Intune são removidas quando eliminar a subscrição.

1.  Na consola do Configuration Manager, aceda a **administração** > **descrição geral** > **serviços em nuvem** > **subscrições do Microsoft Intune**.

2.  Com o botão direito do indicadas **subscrição do Windows Intune**e, em seguida, clique em **eliminar**.

3.   No assistente, clique em **remover subscrição do Windows Intune do Configuration Manager**, clique em **seguinte**e, em seguida, clique em **seguinte** novamente para remover a subscrição.


## <a name="how-to-remove-the-service-connection-point-role"></a>Como remover a função de ponto de ligação de serviço

1.  Aceda a **administração** > **descrição geral** > **configuração do Site** > **servidores e funções de sistema de sites**.

2.  Selecione o servidor que aloja a função **Ponto de ligação de serviço**.

3.  Na lista **Funções do Sistema de Sites**, selecione **Ponto de ligação de serviço** e, em seguida, clique em **Remover Função** no friso. Confirme que pretende remover a função. O ponto de ligação de serviço foi eliminado.

Agora pode criar um novo ponto de ligação de serviço, adicione uma nova subscrição do Intune ao Configuration Manager e defina o Configuration Manager como a Autoridade de MDM.

## <a name="how-to-change-mdm-authority-to-intune"></a>Como alterar a autoridade de MDM do Intune

A partir na versão 1610, pode mudar a autoridade de MDM do Configuration Manager para o Intune. Informações sobre esta funcionalidade estará disponível em breve.

