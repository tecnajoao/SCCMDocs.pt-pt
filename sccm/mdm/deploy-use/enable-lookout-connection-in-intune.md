---
title: Ativar o Lookout MTD no Intune
titleSuffix: Configuration Manager
description: Ative defesa de ameaça móveis Lookout (MTD) no portal do Microsoft Intune.
ms.date: 05/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 7e4ada34-63bf-4b9f-8246-31816aa44196
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0de1859d97eed804eced58028d6459ab682f9b3f
ms.sourcegitcommit: 9cff0702c2cc0f214173b47ec241f7e5a40f84e6
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 06/04/2018
ms.locfileid: "34745440"
---
# <a name="enable-lookout-mtd-connection-in-the-intune-admin-console"></a>Ativar ligação Lookout MTD na consola de administração do Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo mostra como ativar a ligação de defesa (MTD) Lookout ameaça móveis no Microsoft Intune. Deve já tiver configurado o conector do Intune na consola do Lookout antes de efetuar este passo. Se ainda não o fez, siga os passos descritos no [configurar a sua subscrição com defesa de ameaça móveis Lookout](set-up-your-subscription-with-lookout.md).



## <a name="enable-the-lookout-mtd-connector"></a>Activar o conector Lookout MTD

1. Vá para o [portal do Azure](https://portal.azure.com)e inicie sessão com as suas credenciais do Intune. Depois de com êxito iniciou a sessão, consulte o **Dashboard do Azure**.  

2. No **Dashboard do Azure**, escolha **todos os serviços** no menu à esquerda, em seguida, escreva **Intune** no filtro de caixa de texto.  

3. Escolha **Intune**; o **Dashboard do Intune** abre.  

4. No **Dashboard do Intune**, escolha **conformidade do dispositivo**, em seguida, escolha **Mobile ameaça defesa** sob o **configuração** secção.  

5. No **Mobile ameaça defesa** painel, escolha **adicionar**.  

6. Escolha **Lookout** como o **conector Mobile ameaça defesa à configuração** na lista pendente.  

7. Ative as opções de ativação/desativação, de acordo com requisitos da sua organização.  



## <a name="mtd-toggle-options"></a>Opções de ativação/desativação MTD

Pode decidir quais as opções de ativação/desativação MTD tem de ativar, de acordo com requisitos da sua organização. Seguem-se mais detalhes:

- **Ligar Android 4.1 + dispositivos Lookout para trabalho MTD**: Quando ativa esta opção, pode ter Android 4.1 + dispositivos que reportam o risco de segurança de volta para o Intune.  
    - **Marcar como não conforme se não for recebidos nenhuma dados**: Se o Intune não receber dados sobre um dispositivo nesta plataforma Lookout, considere o dispositivo não compatíveis.  

- **Ligar dispositivos iOS 8.0 + ao Lookout para trabalho MTD**: Quando ativa esta opção, pode ter Android 4.1 + dispositivos que reportam o risco de segurança de volta para o Intune.
    - **Marcar como não conforme se não for recebidos nenhuma dados**: Se o Intune não receber dados sobre um dispositivo nesta plataforma Lookout, considere o dispositivo não compatíveis.  

> [!TIP]  
> Pode ver o **estado da ligação** e **da última sincronização** tempo entre o Intune e Lookout a partir do painel de defesa de ameaça Mobile.



## <a name="next-steps"></a>Passos seguintes
Este passo conclui a configuração da integração Lookout e o Intune. Passos para implementar esta solução envolvem a implementar o [Lookout para aplicações de trabalho](configure-and-deploy-lookout-for-work-apps.md) e configurar o [conformidade](enable-device-threat-protection-rule-compliance-policy.md) política.

>[!IMPORTANT]
> *Tem* configurar o Lookout for Work aplicação antes de criar regras de política de conformidade e configurar o acesso condicional. Esta ação garante que a aplicação está pronta e disponíveis para os utilizadores finais a instalar antes de poder obter acesso ao e-mail ou outros recursos da empresa.

[Configurar o Lookout para a aplicação de trabalho](configure-and-deploy-lookout-for-work-apps.md)
