---
title: Restringir o acesso com base em risco | Documentos do Microsoft
description: "Restringir o acesso aos recursos da empresa com base em risco de dispositivo, rede e de aplicações."
ms.custom: na
ms.date: 04/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9083c571-f4fc-4a78-adc5-8aec84dabcbd
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: c6a6137fa978e1ea28aefea2aea4e29ba661efd6
ms.openlocfilehash: 21841d97387f07f53993d957641f9ad892d723c2
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="manage-access-to-company-resource-based-on-device-network-and-application-risk"></a>Gerir o acesso aos recursos da empresa com base no dispositivo, rede e o risco de aplicação

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode controlar o acesso a partir de dispositivos móveis aos recursos empresariais, com base na avaliação de riscos feita atento, uma solução de proteção de ameaça de dispositivo que está integrado com o Microsoft Intune. O risco baseia-se a telemetria do que o serviço de atento recolhe a partir de dispositivos para vulnerabilidades de sistema operativo (OS), aplicações maliciosas instaladas e perfis de rede malicioso. 

Com base na avaliação de riscos comunicado do atento ativada através de políticas de conformidade do System center configuration manager (SCCM), pode configurar políticas de acesso condicional e permitir ou impedir que os dispositivos que foram identificados como for compatível devido a ameaças detetadas nesses dispositivos.

O [MDM implementação (SCCM com o Intune) híbrida](https://docs.microsoft.com/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management) soluções de proteção como atento fornece da ameaça disponibiliza a capacidade de controlar o acesso a recursos da empresa e os dados com base na avaliação de riscos desse dispositivo.

## <a name="how-do-the-hybrid-mdm-deployment-and-lookout-device-threat-protection-help-protect-company-resources"></a>Como a implementação híbrida do MDM e proteção de ameaça de dispositivo de atento ajudar a proteger recursos da empresa?
Aplicação móvel do atento (atento trabalho), em execução em dispositivos móveis, captura de sistema de ficheiros, a pilha de rede, a telemetria de aplicações e de dispositivos (onde disponível) e envia-a para o serviço de nuvem de proteção do atento dispositivo ameaça para calcular um risco de agregado de dispositivo móvel de ameaças. Também pode alterar a classificação do nível de risco para as ameaças na consola do atento para se adequarem às suas necessidades.  

A política de conformidade do SCCM inclui agora uma nova regra para proteção de ameaça móveis atento que se baseia a avaliação de riscos atento dispositivo ameaça. Quando esta regra estiver ativada, o dispositivo é avaliado relativamente à compatibilidade.

Se o dispositivo é determinado como não compatíveis com a política de conformidade, o acesso a recursos, como o Exchange Online e no SharePoint Online podem bloqueada através de políticas de acesso condicional. Quando o acesso é bloqueado, os utilizadores finais são fornecidos com instruções para ajudar a resolver o problema e obter acesso aos recursos da empresa. Estas instruções são iniciada através de atento para a aplicação de trabalho.

## <a name="supported-platforms"></a>Plataformas suportadas:
* **Android 4.1 e posterior**e inscritos no Microsoft Intune.
* **iOS 8 e posterior**e inscritos no Microsoft Intune.
Para obter informações sobre as plataformas e idiomas que atento suporta, consulte este [artigo](https://personal.support.lookout.com/hc/en-us/articles/114094140253).

## <a name="prerequisites"></a>Pré-requisitos:
* [Implementação híbrida do MDM](https://docs.microsoft.com/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management)
* Uma subscrição do Microsoft Intune e Azure Active Directory.
* Uma subscrição enterprise atento Mobile ponto final de segurança.  Para obter mais informações, consulte o artigo [atento Mobile ponto final de segurança](https://www.lookout.com/products/mobile-endpoint-security)

## <a name="example-scenarios"></a>Cenários de exemplo
Seguem-se alguns cenários comuns:
### <a name="control-access-based-on-threat-from-malicious-apps"></a>Controlar o acesso com base no ameaça a partir das aplicações maliciosas:
Quando maliciosas aplicações, como o software maligno é detetado no dispositivo, pode bloquear o esses dispositivos:
* A ligar ao correio eletrónico da empresa antes de resolver a ameaça.
* A sincronizar ficheiros empresarias com o OneDrive para aplicação de trabalho.
* Aceder a aplicações empresariais críticos.

**Acesso ao bloqueado quando maliciosas aplicações são detetadas:**

![diagrama que mostra o acesso de bloqueio de política de acesso condicional quando o dispositivo é determinado como não conformes devido a maliciosas aplicações no dispositivo](media/config-mgr-maliciousapps_blocked.png)

**Dispositivo desbloqueado e é capaz de aceder a recursos da empresa quando for remediada a ameaça:**

![diagrama que mostra a política de acesso condicional conceder acesso ao dispositivo é determinado para serem compatíveis após a remediação](media/config-mgr-maliciousapps-unblocked.png)
### <a name="control-access-based-on-threat-to-network"></a>Controlar o acesso com base no ameaça à rede:
Detetar ameaças à sua rede, tais como ataques Man-in-the-middle e restringir o acesso às redes Wi-Fi com base no risco de dispositivo.

**Acesso à rede através de Wi-Fi bloqueado:**

![diagrama que mostra condicional aceder bloquear acesso de Wi-Fi com base no ameaças de rede](media/config-mgr-network-wifi-blocked.png)

**Acesso concedido na remediação:**

![diagrama que mostra o acesso condicional permitir o acesso na remediação a ameaça](media/config-mgr-network-wifi-unblocked.png)
### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Controlar o acesso ao SharePoint Online com base no ameaça à rede:

Detetar ameaças à sua rede, tais como ataques Man-in-the-middle e evitar uma sincronização de ficheiros empresarias com base no risco de dispositivo.

**Acesso bloqueado SharePoint Online com base no ameaça de rede detetada no dispositivo:**

![Diagrama que mostra a bloquear o acesso de dispositivo para o SharePoint Online com base em deteção ameaça de acesso condicional](media/config-mgr-network-spo-blocked.png)


**Acesso concedido na remediação:**

![Diagrama que mostra o que lhe permitirá aceder depois da ameaça de rede for remediada de acesso condicional](media/config-mgr-network-spo-unblocked.png)

## <a name="next-steps"></a>Passos seguintes
Eis os passos principais que tem de efetuar para implementar esta solução:
1.    [Configurar a sua subscrição com a proteção de ameaça móveis atento](set-up-your-subscription-with-lookout.md)
2.    [Ativar ligação atento MTP no Intune](enable-lookout-connection-in-intune.md)
3.  [Configure e implemente atento para aplicação de trabalho](configure-and-deploy-lookout-for-work-apps.md)
4.    [Configurar política de conformidade](enable-device-threat-protection-rule-compliance-policy.md)
5.    [Resolver problemas relacionados com a integração de atento](troubleshoot-lookout-integration.md)

