---
title: Métodos de inscrição de dispositivos para MDM híbrida
titleSuffix: Configuration Manager
description: Métodos de inscrição de dispositivos para híbrida MDM.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: b81d06dc-3844-4117-9937-16732a227994
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: be1221b3448c8a2818f7fd02b5ff2d14218bbeed
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56134032"
---
# <a name="overview-of-device-enrollment-methods"></a>Descrição geral dos métodos de inscrição de dispositivos

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Depois de expandir o Configuration Manager com o Intune, pode inscrever e gerir os dispositivos da empresa ou dar aos utilizadores permissão para inscrever os respetivos dispositivos pessoais. Também pode gerir dispositivos pertencentes à empresa com o Intune com o Configuration Manager.

A tabela seguinte mostra os métodos de inscrição com as respetivas capacidades suportadas. Estas funcionalidades incluem:
- **Apagar** -reposição de fábrica do dispositivo, removendo todos os dados. [Extinguir dispositivos](../deploy-use/wipe-lock-reset-devices.md)
- **Afinidade** -associa dispositivos a utilizadores. É necessário para a gestão de aplicações móveis (MAM) e o acesso condicional aos dados da empresa. [Afinidade de utilizador](../deploy-use/user-affinity-for-hybrid-managed-devices.md)
- **Bloqueio** impede os utilizadores de remover o dispositivo da gestão. dispositivos iOS necessitam do modo supervisionado para bloquear. [Bloqueio remoto](../deploy-use/wipe-lock-reset-devices.md#remote-lock)

**métodos de inscrição de iOS**

| **Método** |  **Wipe** |  **afinidade**    |   **bloqueio** | **Detalhes** |
|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#byod)** | Não|    Sim |   Não | [Mais](../deploy-use/enable-platform-enrollment.md)|
|**[DEM](#dem)**|   Não |Não |Não  | [Mais](../deploy-use/enroll-devices-with-device-enrollment-manager.md)|
|**[DEP](#dep)**|   Sim |   Opcional |  Opcional|[Mais](../deploy-use/ios-device-enrollment-program-for-hybrid.md)|
|**[USB-SA](#usb-sa)**| Sim |   Opcional |  Não| [Mais](../deploy-use/ios-hybrid-enrollment-using-apple-configurator.md)|

**Windows e os métodos de inscrição de dispositivos Android**

| **Método** |  **Wipe** |  **afinidade**    |   **bloqueio** | **Detalhes**|
|:---:|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#byod)** | Não|    Sim |   Não | [Mais](../deploy-use/enroll-hybrid-windows.md)|
|**[DEM](#dem)**|   Não |Não |Não  |[Mais](../deploy-use/enroll-devices-with-device-enrollment-manager.md)|

Para uma série de perguntas que o ajudam a encontrar o método correto, consulte [escolher como inscrever dispositivos](/intune/get-started/choose-how-to-enroll-devices1).

## <a name="byod"></a>BYOD
"Bring your own device" utilizadores (BYOD) instalar a aplicação Portal da empresa e inscrever o respetivo dispositivo. Isso pode permitir que os utilizadores a ligar à rede da empresa e adiram ao domínio ou o Azure Active Directory. Ativar o BYOD inscrição é um pré-requisito para muitos cenários COD na maioria das plataformas. Ver [mm híbrida do programa de configuração](../deploy-use/setup-hybrid-mdm.md). ([Voltar à tabela](#overview-of-device-enrollment-methods))

## <a name="corporate-owned-devices"></a>Dispositivos propriedade da empresa
Dispositivos pertencentes à empresa (COD) podem ser geridos com a consola do Configuration Manager. dispositivos iOS podem ser inscritos diretamente através de ferramentas fornecidas pela Apple. Todos os tipos de dispositivos podem ser inscritos por um administrador ou gestor utilizando o Gestor de inscrição de dispositivos. Dispositivos com um número IMEI também podem ser identificados e marcados como pertencentes à empresa para ativar cenários COD.

[Inscrever dispositivos pertencentes à empresa](../deploy-use/enroll-company-owned-devices.md)

### <a name="dem"></a>DEM
Gestor de inscrição de dispositivos é uma conta de utilizador especial utilizada para inscrever e gerir múltiplos dispositivos pertencentes à empresa. Gestores podem instalar o Portal da empresa e inscrever muitos dispositivos sem utilizador. Saiba mais sobre [DEM](../deploy-use/enroll-devices-with-device-enrollment-manager.md). ([Voltar à tabela](#overview-of-device-enrollment-methods))

### <a name="dep"></a>DEP
Gestão do programa de inscrição de dispositivos da Apple (DEP) permite-lhe criar e implementar a política "over the air" em dispositivos iOS adquiridos e geridos com DEP. O dispositivo é inscrito quando o usuário ativa o dispositivo pela primeira vez e executa o Assistente de configuração de iOS. Este método suporta **iOS supervisionado** modo que por sua vez permite:
  - Inscrição bloqueada
  - Acesso condicional
  - Deteção de jailbreak
  - Gestão de aplicações móveis

Saiba mais sobre [DEP](../deploy-use/ios-device-enrollment-program-for-hybrid.md). ([Voltar à tabela](#overview-of-device-enrollment-methods))

### <a name="usb-sa"></a>USB-SA
Ligados por USB, inscrição do Assistente de configuração. O administrador cria uma política e exporta-o para o Apple Configurator. Dispositivos ligados por USB, a empresa estão preparados com a política. O administrador tem de inscrever cada dispositivo manualmente. Os utilizadores recebem os respetivos dispositivos e executar o Assistente de configuração, inscrever o respetivo dispositivo. Este método suporta **iOS supervisionado** modo que por sua vez permite:
  - Acesso condicional
  - Deteção de jailbreak
  - Gestão de aplicações móveis

Saiba mais sobre [inscrição do Assistente de configuração com o Apple Configurator](../deploy-use/ios-hybrid-enrollment-using-apple-configurator.md). ([Voltar à tabela](#overview-of-device-enrollment-methods))

## <a name="mobile-device-management-with-exchange-activesync-and-configuration-manager"></a>Gestão de dispositivos móveis com o Exchange ActiveSync e o Configuration Manager
Dispositivos móveis que não estão inscritos, mas que se ligam ao Exchange ActiveSync (EAS) podem ser geridos pelo Intune utilizando a política de MDM do EAS. O Intune utiliza um Exchange Connector para comunicar com o EAS, no local e alojado na cloud.

[Gestão de dispositivos móveis com o Exchange ActiveSync e o Intune](../deploy-use/manage-mobile-devices-with-exchange-activesync.md)
