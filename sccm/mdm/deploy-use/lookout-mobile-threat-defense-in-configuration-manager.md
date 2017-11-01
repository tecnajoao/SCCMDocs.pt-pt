---
title: Restringir o acesso baseado em risco
titleSuffix: Configuration Manager
description: "Restringir o acesso aos recursos da empresa com base em risco de dispositivo, rede e de aplicação."
ms.custom: na
ms.date: 04/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9083c571-f4fc-4a78-adc5-8aec84dabcbd
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 41ac07550bdabe35533e00d1071db4cb967766a3
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="manage-access-to-company-resource-based-on-device-network-and-application-risk"></a>Gerir o acesso aos recursos da empresa com base no dispositivo, rede e o risco de aplicação

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode controlar o acesso de dispositivos móveis a recursos da empresa, com base na avaliação de risco efetuada pelo Lookout, uma solução de proteção de ameaça de dispositivo que está integrada com o Microsoft Intune. O risco é com base na telemetria que o serviço de Lookout recolhe a partir de dispositivos de vulnerabilidades de sistema operativo (SO), aplicações maliciosas instaladas e perfis de rede malicioso. 

Com base na avaliação de risco comunicado do Lookout ativada através de políticas de conformidade do System center configuration manager (SCCM), pode configurar políticas de acesso condicional e permitir ou bloquear dispositivos que foram identificados não for compatível devido a ameaças detetadas nesses dispositivos.

O [(SCCM com o Intune) de implementação de MDM híbrida](https://docs.microsoft.com/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management) soluções de proteção como Lookout fornece da ameaça oferece a capacidade para controlar o acesso a recursos da empresa e dados com base na avaliação de riscos que o dispositivo.

## <a name="how-do-the-hybrid-mdm-deployment-and-lookout-device-threat-protection-help-protect-company-resources"></a>Como a implementação de MDM híbrida e a proteção contra ameaças do Lookout dispositivo ajudar a proteger recursos da empresa?
Aplicação móvel do lookout (Lookout for work,), em execução em dispositivos móveis, captura o sistema de ficheiros, a pilha de rede, a telemetria de aplicações e de dispositivos (quando disponível) e envia-a para o serviço de nuvem de proteção do Lookout dispositivos ameaça para calcular um risco de agregação de dispositivo móveis ameaças. Também pode alterar a classificação do nível de risco para as ameaças na consola do Lookout de acordo com as suas necessidades.  

A política de conformidade do SCCM inclui agora uma nova regra para proteção de ameaça móveis Lookout com base na avaliação de riscos Lookout dispositivo ameaça. Quando esta regra está ativada, o dispositivo for avaliado a compatibilidade.

Se o dispositivo é determinado como não compatível com a política de conformidade, o acesso aos recursos, tal como o Exchange Online e SharePoint Online podem bloqueado através de políticas de acesso condicional. Quando o acesso é bloqueado, os utilizadores finais são fornecidos com uma explicação passo a passo para ajudar a resolver o problema e obter acesso aos recursos da empresa. Estas instruções é iniciada através de Lookout para a aplicação de trabalho.

## <a name="supported-platforms"></a>Plataformas suportadas:
* **Android 4.1 e posterior**e inscritos no Microsoft Intune.
* **iOS 8 e posterior**e inscritos no Microsoft Intune.
Para obter informações sobre as plataformas e idiomas Lookout suporta, consulte este [artigo](https://personal.support.lookout.com/hc/en-us/articles/114094140253).

## <a name="prerequisites"></a>Pré-requisitos:
* [Implementação de MDM híbrida](https://docs.microsoft.com/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management)
* Uma subscrição do Microsoft Intune e o Azure Active Directory.
* Uma subscrição do enterprise Lookout Mobile ponto final de segurança.  Para obter mais informações, consulte [Lookout Mobile ponto final de segurança](https://www.lookout.com/products/mobile-endpoint-security)

## <a name="example-scenarios"></a>Cenários de exemplo
Seguem-se alguns cenários comuns:
### <a name="control-access-based-on-threat-from-malicious-apps"></a>Controlo de acesso com base no ameaça de aplicações maliciosas:
Quando as aplicações maliciosas como software maligno é detetado no dispositivo, pode bloquear a esses dispositivos a partir do:
* A ligar ao e-mail empresarial antes de resolver a ameaça.
* Os ficheiros empresariais com o OneDrive para a aplicação de trabalho de sincronização.
* Aceder a aplicações empresariais vitais.

**Acesso bloqueado quando são detetadas aplicações maliciosas:**

![diagrama que mostra o acesso de bloqueio de política de acesso condicional quando o dispositivo é determinado para ser incompatíveis devido a aplicações maliciosas no dispositivo](media/config-mgr-maliciousapps_blocked.png)

**Dispositivo desbloqueado e é capaz de aceder a recursos da empresa quando é remediar a ameaça:**

![diagrama que mostra a política de acesso condicional conceder o acesso quando o dispositivo é determinado para ser compatíveis após a remediação](media/config-mgr-maliciousapps-unblocked.png)
### <a name="control-access-based-on-threat-to-network"></a>Controlo de acesso com base no ameaça à rede:
Detetar ameaças à sua rede, tais como ataques Man-in-the-middle e restringir o acesso a redes Wi-Fi com base no risco de dispositivo.

**Acesso à rede através de Wi-Fi bloqueado:**

![diagrama que mostra condicional aceder bloqueio acesso Wi-Fi com base no ameaças de rede](media/config-mgr-network-wifi-blocked.png)

**Acesso concedido na remediação:**

![diagrama que mostra o acesso condicional permitir o acesso na remediação de ameaça](media/config-mgr-network-wifi-unblocked.png)
### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Controlar o acesso ao SharePoint Online com base no ameaça à rede:

Detetar ameaças à sua rede, tais como ataques Man-in-the-middle e impedir que a sincronização de ficheiros empresariais com base no risco de dispositivo.

**Acesso bloqueado SharePoint Online com base no ameaças de rede detetadas no dispositivo:**

![Diagrama que mostra o acesso condicional a bloquear o dispositivo de acesso ao SharePoint Online com base na deteção de ameaças](media/config-mgr-network-spo-blocked.png)


**Acesso concedido na remediação:**

![Diagrama que mostra o acesso condicional permitir o acesso depois da ameaça de rede é remediada](media/config-mgr-network-spo-unblocked.png)

## <a name="next-steps"></a>Passos seguintes
Eis os passos principais que terá de efetuar para implementar esta solução:
1.  [Configurar a sua subscrição com a proteção de ameaça móveis Lookout](set-up-your-subscription-with-lookout.md)
2.  [Ativar ligação Lookout MTP no Intune](enable-lookout-connection-in-intune.md)
3.  [Configure e implemente o Lookout para aplicação de trabalho](configure-and-deploy-lookout-for-work-apps.md)
4.  [Configurar política de conformidade](enable-device-threat-protection-rule-compliance-policy.md)
5.  [Resolução de problemas de integração do Lookout](troubleshoot-lookout-integration.md)
