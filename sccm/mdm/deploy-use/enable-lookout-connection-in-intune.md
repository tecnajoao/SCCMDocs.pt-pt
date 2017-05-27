---
title: Ativar atento MTP no Intune | Documentos do Microsoft
description: "Ative a proteção de ameaça móveis atento na consola de administração do Intune."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7e4ada34-63bf-4b9f-8246-31816aa44196
caps.latest.revision: 
author: mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 6424fb07802b62820b4dc78a58ab30d3b956abef
ms.openlocfilehash: f9ddbcc981fa1274a41ae16a6a939c0cdf739c3e
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="enable-lookout-mtp-connection-in-the-intune-admin-console"></a>Ativar atento MTP ligação na consola de administração do Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este tópico mostra como ativar a ligação de atento MTP no Intune. Deve já configurou o conector do Intune na consola do atento antes de efetuar este passo.  Se ainda não o fez, efetue os passos descritos no [configurar a sua subscrição com a proteção de ameaça móveis atento](set-up-your-subscription-with-lookout.md).

Para ativar a ligação de atento MTP no Intune, o **administração** página no [consola de administrador do Microsoft Intune](https://manage.microsoft.com), escolha **integração de serviço de terceiros**. Escolher **Estado atento** e ativar **sincronização com MTP** utilizando o botão de alternar.

![captura de ecrã da página de sincronização de atento com o botão de alternar ativar realçado](media/lookout-intune-synchronization.png)

Este passo conclui o programa de configuração da integração atento e o Intune na consola do administrador do Intune.  Os próximos passos para implementar esta solução envolvem implementar o [atento aplicações trabalho](configure-and-deploy-lookout-for-work-apps.md) e configurar o [conformidade](enable-device-threat-protection-rule-compliance-policy.md) política.

>[!IMPORTANT]
> **Tem** configurar atento para a aplicação de trabalho antes de criar regras de política de conformidade e configurar o acesso condicional. Isto garante que a aplicação está pronta e disponíveis para os utilizadores finais instalar antes que podem aceder a e-mail ou outros recursos da empresa.

## <a name="next-steps"></a>Passos seguintes
[Configurar atento para a aplicação de trabalho](configure-and-deploy-lookout-for-work-apps.md)

