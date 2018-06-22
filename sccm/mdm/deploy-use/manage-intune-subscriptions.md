---
title: Gerir uma subscrição do Intune
titleSuffix: Configuration Manager
description: Gerir uma subscrição do Intune associada com o System Center Configuration Manager.
ms.date: 06/02/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 9b494767-68c1-47b1-9a86-591bff0ad491
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1b8390faa557f37b2ee148299079df81d3c13299
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32346744"
---
# <a name="manage-an-intune-subscription-associated-with-system-center-configuration-manager"></a>Gerir uma subscrição do Intune associada com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Se adicionar um Microsoft Intune (uma subscrição de avaliação ou uma subscrição paga) para o Configuration Manager e, em seguida, tem de mudar para outra subscrição do Intune, tem de eliminar o **subscrição do Microsoft Intune** e **ponto de ligação de serviço** partir da consola do Configuration Manager antes de poder adicionar uma nova subscrição.

> [!NOTE]
> Pode configurar apenas uma subscrição do Intune num momento na gestão de dispositivos móveis híbridos.

## <a name="how-to-delete-an-intune-subscription-from-configuration-manager"></a>Como eliminar uma subscrição do Intune do Configuration Manager

> [!IMPORTANT]
>  Todo o conteúdo, incluindo inscrições através do utilizador, políticas e implementações de aplicações configuradas para dispositivos geridos pela subscrição do Intune são removidos quando eliminar a subscrição.

1.  Na consola do Configuration Manager, vá para **administração** > **descrição geral** > **serviços em nuvem** > **subscrições do Microsoft Intune**.

2.  Clique com botão direito do listadas **subscrição do Microsoft Intune**e, em seguida, clique em **eliminar**.

3.   No assistente, clique em **remover a subscrição do Microsoft Intune do Configuration Manager**, clique em **seguinte**e, em seguida, clique em **seguinte** novamente para remover a subscrição.


## <a name="how-to-remove-the-service-connection-point-role"></a>Como remover a função de ponto de ligação de serviço

1.  Aceda a **administração** > **descrição geral** > **configuração do Site** > **servidores e funções de sistema de sites**.

2.  Selecione o servidor que aloja a função **Ponto de ligação de serviço**.

3.  Na lista **Funções do Sistema de Sites**, selecione **Ponto de ligação de serviço** e, em seguida, clique em **Remover Função** no friso. Confirme que pretende remover a função. O ponto de ligação de serviço foi eliminado.

Agora pode criar um novo ponto de ligação de serviço, adicione uma nova subscrição do Intune ao Configuration Manager e defina o Configuration Manager como a Autoridade de MDM.

## <a name="how-to-change-mdm-authority-to-intune"></a>Como alterar a autoridade de MDM ao Intune
A partir do Configuration Manager versão 1610 e Microsoft Intune version 1705, pode alterar a autoridade de MDM sem ter de contactar o Support da Microsoft e sem ter de anular a inscrição e inscrever-se novamente os seus dispositivos geridos existentes. Para obter mais informações, consulte [alterar a autoridade de MDM](/sccm/mdm/deploy-use/change-mdm-authority).
