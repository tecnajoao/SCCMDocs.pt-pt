---
title: Ativar o Lookout MTP no Intune
titleSuffix: Configuration Manager
description: Ative a proteção de ameaça móveis Lookout na consola de administração do Intune.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 7e4ada34-63bf-4b9f-8246-31816aa44196
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 79a583237d882101d70442cbf6b55a5e3c0e9b11
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
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
[Configurar o Lookout para a aplicação de trabalho ](configure-and-deploy-lookout-for-work-apps.md)
