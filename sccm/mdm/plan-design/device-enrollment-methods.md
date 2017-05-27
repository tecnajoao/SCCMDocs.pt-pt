---
title: "Métodos de inscrição de dispositivos para uma implementação híbrida MDM | Documentos do Microsoft"
description: "Métodos de inscrição de dispositivos para uma implementação híbrida MDM."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: b81d06dc-3844-4117-9937-16732a227994
caps.latest.revision: 9
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 6424fb07802b62820b4dc78a58ab30d3b956abef
ms.openlocfilehash: e09e639e939b846cdc162681f9d7bd4c39cd6fbf
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="overview-of-device-enrollment-methods"></a>Descrição geral dos métodos de inscrição de dispositivos

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Depois de expandir do Configuration Manager com o Intune, pode inscrever e gerir os dispositivos da empresa ou dar aos utilizadores permissão para inscreverem os dispositivos pessoais. Também pode gerir dispositivos pertencentes à empresa com o Intune utilizando o Configuration Manager.

A tabela seguinte mostra métodos de inscrição com as respetivas funcionalidades suportadas. Estas funcionalidades incluem:
- **Apagar** -reposição de fábrica do dispositivo, removendo todos os dados. [Extinguir dispositivos](../deploy-use/wipe-lock-reset-devices.md)
- **Afinidade** -associa dispositivos a utilizadores. Necessário para a gestão de aplicações móveis (MAM) e o acesso condicional para dados da empresa. [Afinidade de utilizador](../deploy-use/user-affinity-for-hybrid-managed-devices.md)
- **Bloqueio** impede os utilizadores de remover o dispositivo de gestão. dispositivos iOS requerem Supervised modo de bloqueio. [Bloqueio remoto](../deploy-use/wipe-lock-reset-devices.md#remote-lock)

**métodos de inscrição de iOS**

| **Método** |    **Eliminação de dados** |    **Afinidade**    |    **Bloqueio** | **Detalhes** |
|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#byod)** | Não|    Sim |    Não | [mais](../deploy-use/enable-platform-enrollment.md)|
|**[DEM](#dem)**|    Não |Não |Não    | [mais](../deploy-use/enroll-devices-with-device-enrollment-manager.md)|
|**[DEP](#dep)**|    Sim |    Opcional |    Opcional|[mais](../deploy-use/ios-device-enrollment-program-for-hybrid.md)|
|**[USB SA](#usb-sa)**|    Sim |    Opcional |    Não| [mais](../deploy-use/ios-hybrid-enrollment-using-apple-configurator.md)|

**Métodos de inscrição do Android e Windows**

| **Método** |    **Eliminação de dados** |    **Afinidade**    |    **Bloqueio** | **Detalhes**|
|:---:|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#byod)** | Não|    Sim |    Não | [mais](../deploy-use/enroll-hybrid-windows.md)|
|**[DEM](#dem)**|    Não |Não |Não    |[mais](../deploy-use/enroll-devices-with-device-enrollment-manager.md)|

Para uma série de perguntas que o ajudam a localizar o método de à direita, consulte o artigo [escolher como inscrever dispositivos](/intune/get-started/choose-how-to-enroll-devices1).

## <a name="byod"></a>BYOD
"Bring your own device" (BYOD) utilizadores instalar a aplicação de Portal da empresa e inscrever o respetivo dispositivo. Isto pode permitir que os utilizadores a ligar à rede da empresa, adesão ao domínio ou do Azure Active Directory. Ativar BYOD inscrição é um pré-requisito muitos cenários de COD para a maioria das plataformas. Consulte o artigo [híbrida configuração MDM](../deploy-use/setup-hybrid-mdm.md). ([Novamente para a tabela](#overview-of-device-enrollment-methods))

## <a name="corporate-owned-devices"></a>Dispositivos pertencentes à empresa
Dispositivos de empresa (COD) podem ser geridos com a consola do Configuration Manager. dispositivos iOS podem ser inscritos diretamente através de ferramentas fornecidas pelo Apple. Todos os tipos de dispositivos podem ser inscritos por um administrador ou gestor utilizando o Gestor de inscrição de dispositivos. Dispositivos com um número IMEI também podem ser identificados e etiquetados como pertencendo à empresa a ativar cenários COD.

[Inscrever dispositivos pertencentes à empresa](../deploy-use/enroll-company-owned-devices.md)

### <a name="dem"></a>DEM
Gestor de inscrição de dispositivos é uma conta de utilizador especial utilizada para inscrever e gerir vários dispositivos pertencentes à empresa. Gestores de podem instalar o Portal da empresa e inscrever vários dispositivos de utilizadores. Saiba mais sobre [DEM](../deploy-use/enroll-devices-with-device-enrollment-manager.md). ([Novamente para a tabela](#overview-of-device-enrollment-methods))

### <a name="dep"></a>DEP
Gestão do programa de inscrição de dispositivos da Apple (DEP) permite-lhe criar e implementar a política "por ondas eletromagnéticas" para dispositivos iOS adquiridos e são geridos com o DEP. O dispositivo é inscrito quando o utilizador liga o dispositivo pela primeira vez e executa o Assistente de configuração de iOS. Este método suporta **iOS Supervised** modo que por sua vez permite:
  -    Inscrição bloqueada
  -    Acesso condicional
  -    Deteção de jailbreak
  -    Gestão de aplicações móveis

Saiba mais sobre [DEP](../deploy-use/ios-device-enrollment-program-for-hybrid.md). ([Novamente para a tabela](#overview-of-device-enrollment-methods))

### <a name="usb-sa"></a>USB SA
Inscrição Assistente de configuração ligados por USB. O administrador cria uma política e exporta-o para o Apple Configurator. Dispositivos ligados por USB, a empresa estão preparados com a política. O administrador têm de inscrever cada dispositivo manualmente. Os utilizadores recebem os respetivos dispositivos e executam o Assistente de configuração, inscrever o respetivo dispositivo. Este método suporta **iOS Supervised** modo que por sua vez permite:
  -    Acesso condicional
  -    Deteção de jailbreak
  -    Gestão de aplicações móveis

Saiba mais sobre [inscrição com o Assistente de configuração com o Apple Configurator](../deploy-use/ios-hybrid-enrollment-using-apple-configurator.md). ([Novamente para a tabela](#overview-of-device-enrollment-methods))

## <a name="mobile-device-management-with-exchange-activesync-and-configuration-manager"></a>Gestão de dispositivos móveis com o Exchange ActiveSync e do Configuration Manager
Dispositivos móveis que não estão inscritos com ligação para o Exchange ActiveSync (EAS) podem ser geridos pelo Intune utilizando a política EAS MDM. Intune utiliza um conector do Exchange para comunicar com EAS, ambos no local e na nuvem alojada.

[Gestão de dispositivos móveis com o Exchange ActiveSync e o Intune](../deploy-use/manage-mobile-devices-with-exchange-activesync.md)

