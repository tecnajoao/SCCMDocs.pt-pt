---
title: "Métodos de inscrição de dispositivos para MDM híbrida"
titleSuffix: Configuration Manager
description: "Métodos de inscrição de dispositivos para híbrida MDM."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: b81d06dc-3844-4117-9937-16732a227994
caps.latest.revision: "9"
caps.handback.revision: "0"
author: dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 180f7699f184779d98db5ccedb296b409a119a30
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="overview-of-device-enrollment-methods"></a>Descrição geral dos métodos de inscrição de dispositivos

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Depois de expandir o Configuration Manager com o Intune, pode inscrever e gerir dispositivos pertencentes à empresa ou conceder aos utilizadores permissão para inscreverem os respetivos dispositivos pessoais. Também pode gerir dispositivos pertencentes à empresa com o Intune com o Configuration Manager.

A tabela seguinte mostra os métodos de inscrição com as respetivas capacidades suportadas. Estas funcionalidades incluem:
- **Apagar** -reposição de fábrica do dispositivo, removendo todos os dados. [Extinguir dispositivos](../deploy-use/wipe-lock-reset-devices.md)
- **Afinidade** -associa dispositivos de utilizadores. Necessário para a gestão de aplicações móveis (MAM) e acesso condicional aos dados da empresa. [Afinidade de utilizador](../deploy-use/user-affinity-for-hybrid-managed-devices.md)
- **Bloqueio** impede os utilizadores de remover o dispositivo da gestão. dispositivos iOS requerem o modo supervisionado para bloqueio. [Bloqueio remoto](../deploy-use/wipe-lock-reset-devices.md#remote-lock)

**métodos de inscrição de iOS**

| **Método** |  **Eliminação de dados** |  **Afinidade**    |   **Bloqueio** | **Detalhes** |
|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#byod)** | Não|    Sim |   Não | [mais](../deploy-use/enable-platform-enrollment.md)|
|**[DEM](#dem)**|   Não |Não |Não  | [mais](../deploy-use/enroll-devices-with-device-enrollment-manager.md)|
|**[DEP](#dep)**|   Sim |   Opcional |  Opcional|[mais](../deploy-use/ios-device-enrollment-program-for-hybrid.md)|
|**[USB SA](#usb-sa)**| Sim |   Opcional |  Não| [mais](../deploy-use/ios-hybrid-enrollment-using-apple-configurator.md)|

**Métodos de inscrição de dispositivos Android e Windows**

| **Método** |  **Eliminação de dados** |  **Afinidade**    |   **Bloqueio** | **Detalhes**|
|:---:|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#byod)** | Não|    Sim |   Não | [mais](../deploy-use/enroll-hybrid-windows.md)|
|**[DEM](#dem)**|   Não |Não |Não  |[mais](../deploy-use/enroll-devices-with-device-enrollment-manager.md)|

Para uma série de pergunta que o ajudam a localizar o método adequado, consulte [escolher como inscrever dispositivos](/intune/get-started/choose-how-to-enroll-devices1).

## <a name="byod"></a>BYOD
"Bring your own device" utilizadores (BYOD) instale a aplicação Portal da empresa e inscrever o respetivo dispositivo. Isto pode permitir que os utilizadores a ligar à rede da empresa, associar o domínio ou o Azure Active Directory. Permitir o BYOD inscrição é um pré-requisito para vários cenários de COD para a maioria das plataformas. Consulte [mm híbrida do programa de configuração](../deploy-use/setup-hybrid-mdm.md). ([Voltar à tabela](#overview-of-device-enrollment-methods))

## <a name="corporate-owned-devices"></a>Dispositivos pertencentes à empresa
Dispositivos pertencentes à empresa (COD) podem ser geridos com a consola do Configuration Manager. dispositivos iOS podem ser inscritos diretamente através de ferramentas fornecidas pelo Apple. Todos os tipos de dispositivos podem ser inscritos por um administrador ou gestor utilizando o Gestor de inscrição de dispositivos. Também podem ser identificados e marcados como pertencentes à empresa para permitir cenários de COD dispositivos com um número IMEI.

[Inscrever dispositivos pertencentes à empresa](../deploy-use/enroll-company-owned-devices.md)

### <a name="dem"></a>DEM
Gestor de inscrição de dispositivos é uma conta de utilizador especial utilizada para inscrever e gerir vários dispositivos pertencentes à empresa. Os gestores podem instalar o Portal da empresa e inscrever vários dispositivos sem utilizador. Saiba mais sobre [DEM](../deploy-use/enroll-devices-with-device-enrollment-manager.md). ([Voltar à tabela](#overview-of-device-enrollment-methods))

### <a name="dep"></a>DEP
Gestão do programa de inscrição de dispositivos da Apple (DEP) permite-lhe criar e implementar a política "por ondas eletromagnéticas" para dispositivos iOS adquiridos e geridos com o DEP. O dispositivo é inscrito quando o utilizador passa no dispositivo pela primeira vez e executa o Assistente de configuração de iOS. Este método suporta **iOS supervisionado** modo que por sua vez permite:
  - Inscrição bloqueada
  - Acesso condicional
  - Deteção de jailbreak
  - Gestão de aplicações móveis

Saiba mais sobre [DEP](../deploy-use/ios-device-enrollment-program-for-hybrid.md). ([Voltar à tabela](#overview-of-device-enrollment-methods))

### <a name="usb-sa"></a>USB SA
Inscrição do Assistente de configuração ligada por USB. O administrador cria uma política e exporta-a para o Apple Configurator. Estão preparados dispositivos ligados por USB, pertencentes à empresa com a política. O administrador tem de inscrever cada dispositivo manualmente. Os utilizadores recebem os respetivos dispositivos e executar o Assistente de configuração, inscrever o respetivo dispositivo. Este método suporta **iOS supervisionado** modo que por sua vez permite:
  - Acesso condicional
  - Deteção de jailbreak
  - Gestão de aplicações móveis

Saiba mais sobre [a inscrição do Assistente de configuração com o Apple Configurator](../deploy-use/ios-hybrid-enrollment-using-apple-configurator.md). ([Voltar à tabela](#overview-of-device-enrollment-methods))

## <a name="mobile-device-management-with-exchange-activesync-and-configuration-manager"></a>Gestão de dispositivos móveis com o Exchange ActiveSync e o Configuration Manager
Dispositivos móveis que não estão inscritos, mas que se ligar ao Exchange ActiveSync (EAS) podem ser geridos pelo Intune utilizando a política EAS de MDM. O Intune utiliza um Exchange Connector para comunicar com o EAS, no local e alojado na nuvem.

[Gestão de dispositivos móveis com o Exchange ActiveSync e o Intune](../deploy-use/manage-mobile-devices-with-exchange-activesync.md)
