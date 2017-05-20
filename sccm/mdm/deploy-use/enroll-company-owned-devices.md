---
title: "Inscrever dispositivos pertencentes à empresa - Configuration Manager | Documentos do Microsoft"
description: "Saiba mais sobre diferentes métodos para inscrever dispositivos pertencentes à empresa para implementações híbridas com o Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e2754ce6-1460-4ddd-9050-2cc87e7964f4
caps.latest.revision: 13
author: mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: f0b503d8c9eba2dd1b6eb4c41ec40c001b727326
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="enroll-company-owned-devices-for-hybrid-deployments-with-configuration-manager"></a>Inscrever dispositivos pertencentes à empresa para implementações híbridas com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Organização ou os dispositivos da empresa (COD) podem ser colocados em gestão numa variedade de modos consoante o dispositivo e como tenha sido comprado.  

## <a name="enroll-device-enrollment-program-ios-devices"></a>Inscrever dispositivos iOS de programa de inscrição de dispositivos  
 Implementa um perfil de inscrição "por ondas eletromagnéticas" dispositivos adquiridos através do programa de inscrição de dispositivos da Apple. Quando o utilizador executa o Assistente de configuração do dispositivo, o dispositivo é inscrito no Intune.  Os dispositivos inscritos através do DEP não podem ser anulados pelos utilizadores. Consulte o artigo [inscrição do iOS programa de inscrição de dispositivos (DEP) para implementações híbridas com o Configuration Manager](../../mdm/deploy-use/ios-device-enrollment-program-for-hybrid.md).  

## <a name="enroll-ios-devices-with-apple-configurator"></a>Inscrever dispositivos iOS com o Apple Configurator  
 Este método requer que o administrador para USB ligar o dispositivo iOS ao computador Mac com o Apple Configurator para preconfigure a inscrição. Em seguida, são entregues dispositivos para os seus utilizadores a executam o processo do Assistente de configuração, configurar o dispositivo com as respetivas credenciais escolar ou profissional e concluir o processo de inscrição. Consulte o artigo [inscrição do iOS híbridos através do Apple Configurator com o Configuration Manager](../../mdm/deploy-use/ios-hybrid-enrollment-using-apple-configurator.md).  

## <a name="device-enrollment-manager"></a>Gestor de inscrição de dispositivos  
 As organizações podem utilizar o Intune para gerir um grande número de dispositivos móveis com uma única conta de utilizador designado por conta do Gestor de inscrição de dispositivos. Depois de criar uma conta de Gestor de inscrição de dispositivos, essa conta pode ser utilizada por um Gestor de inscrever mais do que os dispositivos de cinco padrão permitidos por predefinição para os utilizadores normais. A inscrição de dispositivos com um Gestor de inscrição de dispositivos funciona apenas para dispositivos que não são utilizados por um utilizador específico. Estes dispositivos são boa para ponto de venda ou utilitário de aplicações, por exemplo, mas incorreto para utilizadores que necessitam de aceder a recursos de correio eletrónico ou da empresa. Consulte o artigo [inscrever dispositivos com o Gestor de inscrição de dispositivos com o Configuration Manager](../../mdm/deploy-use/enroll-devices-with-device-enrollment-manager.md).  

## <a name="user-affinity-for-managed-devices"></a>Afinidade de utilizador para dispositivos geridos  
 Quando configurar perfis para os dispositivos da empresa, o administrador pode especificar se os dispositivos geridos suportam *afinidade do utilizador* que identifica um utilizador específico com o dispositivo. Os dispositivos configurados com **user affinity** podem instalar e executar a aplicação Portal da Empresa para transferir aplicações e gerir dispositivos. Consulte o artigo [afinidade do utilizador para uma implementação híbrida geridos dispositivos no Configuration Manager](../../mdm/deploy-use/user-affinity-for-hybrid-managed-devices.md).  

## <a name="manage-devices-with-activation-lock"></a>Gerir dispositivos com o bloqueio de ativação  
 Microsoft Intune pode ajudá-lo a gerir iOS bloqueio de ativação, uma funcionalidade do encontrar a minha aplicação iPhone para iOS 7.1 e dispositivos posteriores. O Bloqueio de Ativação é ativado automaticamente ao utilizar a aplicação Encontrar o Meu iPhone num dispositivo. Consulte o artigo [gerir o iOS bloqueio de ativação com o System Center Configuration Manager](../../mdm/deploy-use/manage-ios-activation-lock.md).

 ## <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>Predeclare dispositivos com números de série IMEI ou iOS

Pode identificar dispositivos pertencentes ao importar os seus números de identidade (IMEI) estação internacional do equipamento móvel ou números de série iOS. Pode carregar um ficheiro de valores separados por vírgulas (. csv) que contenha números IMEI do dispositivo ou pode introduzir manualmente as informações de dispositivo.  Consulte o artigo [Predeclare dispositivos com números de ID de hardware](../../mdm/deploy-use/predeclare-devices-with-hardware-id.md).

