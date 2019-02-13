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
ms.collection: M365-identity-device-management
ms.openlocfilehash: b2e63720bf4a5e6b2cf2f7d1a034d916c9ca5338
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56133338"
---
# <a name="manage-an-intune-subscription-associated-with-system-center-configuration-manager"></a>Gerir uma subscrição do Intune associada com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Se adicionar um Microsoft Intune (uma subscrição de avaliação ou subscrição paga) ao Configuration Manager e, em seguida, tem de mudar para outra subscrição do Intune, tem de eliminar a **subscrição do Microsoft Intune** e o **Ponto de ligação de serviço** da consola do Configuration Manager antes de poder adicionar uma nova subscrição.

> [!NOTE]
> Pode configurar apenas uma subscrição do Intune num momento na gestão de dispositivos móveis híbrida.

## <a name="how-to-delete-an-intune-subscription-from-configuration-manager"></a>Como eliminar uma subscrição do Intune do Configuration Manager

> [!IMPORTANT]
>  Todos os conteúdos, incluindo inscrições de utilizador, políticas e implementações de aplicações configuradas para dispositivos geridos pela subscrição do Intune são removidos quando eliminar a subscrição.

1.  Na consola do Configuration Manager, aceda a **Administration** > **descrição geral** > **serviços Cloud**  >  **Subscrições do Microsoft Intune**.

2.  Com o botão direito listadas **subscrição do Microsoft Intune**e, em seguida, clique em **eliminar**.

3.   No assistente, clique em **remover subscrição do Microsoft Intune do Configuration Manager**, clique em **próxima**e, em seguida, clique em **seguinte** novamente para remover a subscrição.


## <a name="how-to-remove-the-service-connection-point-role"></a>Como remover a função de ponto de ligação de serviço

1.  Aceda a **Administration** > **descrição geral** > **configuração do Site** > **servidores e funções de sistema de sites** .

2.  Selecione o servidor que aloja a função **Ponto de ligação de serviço**.

3.  Na lista **Funções do Sistema de Sites**, selecione **Ponto de ligação de serviço** e, em seguida, clique em **Remover Função** no friso. Confirme que pretende remover a função. O ponto de ligação de serviço foi eliminado.

Agora pode criar um novo ponto de ligação de serviço, adicione uma nova subscrição do Intune ao Configuration Manager e defina o Configuration Manager como a Autoridade de MDM.

## <a name="how-to-change-mdm-authority-to-intune"></a>Como alterar a autoridade de MDM ao Intune
A partir do Configuration Manager versão 1610 e do Microsoft Intune version 1705, pode alterar a autoridade MDM sem ter de contactar Support da Microsoft e sem ter de anular a inscrição e inscrever novamente os seus dispositivos geridos existentes. Para obter detalhes, consulte [alterar a sua autoridade MDM](/sccm/mdm/deploy-use/change-mdm-authority).
