---
title: Ativar o Lookout MTP no Intune | Microsoft Docs
description: "Ative a proteção de ameaça móveis Lookout na consola de administração do Intune."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7e4ada34-63bf-4b9f-8246-31816aa44196
caps.latest.revision: 
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: f9ddbcc981fa1274a41ae16a6a939c0cdf739c3e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="enable-lookout-mtp-connection-in-the-intune-admin-console"></a>Ativar ligação Lookout MTP na consola de administração do Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este tópico mostra como ativar a ligação de Lookout MTP no Intune. Deve já tiver configurado o conector do Intune na consola do Lookout antes de efetuar este passo.  Se ainda não o fez, siga os passos descritos no [configurar a sua subscrição com a proteção de ameaça móveis Lookout](set-up-your-subscription-with-lookout.md).

Para ativar a ligação de Lookout MTP no Intune, o **administração** página no [consola de administrador do Microsoft Intune](https://manage.microsoft.com), escolha **integração de serviço de terceiros**. Escolha **Estado Lookout** e ativar **sincronização com MTP** com o botão de alternar.

![captura de ecrã da página de sincronização de Lookout com o botão de alternar ativar realçado](media/lookout-intune-synchronization.png)

Este passo conclui a configuração da integração Lookout e o Intune na consola de administrador do Intune.  Passos para implementar esta solução envolvem a implementar o [Lookout para aplicações de trabalho](configure-and-deploy-lookout-for-work-apps.md) e configurar o [conformidade](enable-device-threat-protection-rule-compliance-policy.md) política.

>[!IMPORTANT]
> **Tem** configurar o Lookout for Work aplicação antes de criar regras de política de conformidade e configurar o acesso condicional. Isto garante que a aplicação está pronta e disponíveis para os utilizadores finais a instalar antes de poder obter acesso ao e-mail ou outros recursos da empresa.

## <a name="next-steps"></a>Passos seguintes
[Configurar o Lookout para a aplicação de trabalho](configure-and-deploy-lookout-for-work-apps.md)
