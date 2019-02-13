---
title: Ativar o Lookout MTD no Intune
description: Ative o Lookout mobile de defesa contra ameaças (MTD) no portal do Microsoft Intune.
ms.date: 05/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 7e4ada34-63bf-4b9f-8246-31816aa44196
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b36e98edfffcc26b7fb2670cbfdc31c165331f0f
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56139396"
---
# <a name="enable-lookout-mtd-connection-in-the-intune-admin-console"></a>Ativar a ligação da MTD do Lookout na consola de administração do Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo mostra como ativar a ligação do Lookout mobile threat defense (MTD) no Microsoft Intune. Deve ter configurado o conector do Intune na consola do Lookout antes de efetuar este passo. Se ainda não o fez, efetue os passos descritos em [configurar a sua subscrição com a defesa contra ameaças móveis do Lookout](set-up-your-subscription-with-lookout.md).



## <a name="enable-the-lookout-mtd-connector"></a>Ativar o conector de MTD do Lookout

1. Vá para o [portal do Azure](https://portal.azure.com)e inicie sessão com as credenciais do Intune. Depois de se com êxito, consulte a **Dashboard do Azure**.  

2. Sobre o **Dashboard do Azure**, escolha **todos os serviços** no menu à esquerda, em seguida, escreva **Intune** no filtro da caixa de texto.  

3. Escolher **Intune**; o **Dashboard do Intune** abre.  

4. Na **Dashboard do Intune**, escolha **conformidade do dispositivo**, em seguida, escolha **Mobile Threat Defense** sob o **configuração** secção.  

5. Sobre o **Mobile Threat Defense** painel, escolha **Add**.  

6. Escolher **Lookout** como o **conector de defesa contra ameaças móveis a configurar** na lista pendente.  

7. Ative as opções de alternância de acordo com os requisitos da sua organização.  



## <a name="mtd-toggle-options"></a>Opções de alternância da MTD

Pode decidir quais opções de alternância da MTD tem de ativar de acordo com os requisitos da sua organização. Seguem-se mais detalhes:

- **Ligar Android 4.1 dispositivos MTD do Lookout for Work**: Quando ativa esta opção, pode ter Android 4.1 dispositivos a comunicar riscos de segurança de volta para o Intune.  
    - **Marcar como não conforme se não forem recebidos dados**: Se o Intune não receber dados sobre um dispositivo nesta plataforma do Lookout, considere o dispositivo não conforme.  

- **Ligar dispositivos iOS 8.0 + ao Lookout for Work MTD**: Quando ativa esta opção, pode ter dispositivos iOS 8.0 + comunicar riscos de segurança de volta para o Intune.
    - **Marcar como não conforme se não forem recebidos dados**: Se o Intune não receber dados sobre um dispositivo nesta plataforma do Lookout, considere o dispositivo não conforme.  

> [!TIP]  
> Pode ver o **estado da ligação** e o **última sincronização** tempo entre o Intune e o Lookout a partir do painel de defesa contra ameaças móveis.



## <a name="next-steps"></a>Passos seguintes
Este passo conclui a configuração da integração do Lookout e do Intune. Os passos seguintes para implementar esta solução envolvem a implementação do [Lookout for Work apps](configure-and-deploy-lookout-for-work-apps.md) e a configuração a [conformidade](enable-device-threat-protection-rule-compliance-policy.md) política.

>[!IMPORTANT]
> *Tem* configurar o Lookout for Work aplicação antes de criar regras de política de conformidade e configurar o acesso condicional. Esta ação garante que a aplicação está pronta e disponível para os utilizadores finais instalarem antes de poderem aceder ao e-mail ou a outros recursos da empresa.

[Configurar o Lookout for Work aplicação](configure-and-deploy-lookout-for-work-apps.md)
