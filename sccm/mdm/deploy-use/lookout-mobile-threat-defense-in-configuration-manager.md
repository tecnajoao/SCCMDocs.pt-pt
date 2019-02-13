---
title: Restringir o acesso com base no risco
titleSuffix: Configuration Manager
description: Restringir o acesso aos recursos da empresa com base em riscos de aplicações, redes e dispositivos.
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 9083c571-f4fc-4a78-adc5-8aec84dabcbd
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 62db216d2047ee0272c6b3fa226493b5e8af5f84
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56128726"
---
# <a name="manage-access-to-company-resource-based-on-device-network-and-application-risk"></a>Gerir o acesso a recursos da empresa com base em riscos de aplicações, redes e dispositivos

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Controlar o acesso de dispositivos móveis a recursos empresariais com base na avaliação de riscos realizada pelo Lookout. Lookout é uma solução de proteção de ameaças de dispositivos integrada no Microsoft Intune. O risco baseia-se nos dados recolhidos pelo serviço do Lookout. Ele coleta dados a partir de dispositivos para vulnerabilidades do SO, aplicações maliciosas instaladas e perfis de rede maliciosos. 

Com base na avaliação de risco comunicados do Lookout ativada através de políticas de conformidade do Configuration Manager, configurar políticas de acesso condicional. Estas políticas permitem ou bloquear dispositivos que o Gestor de configuração determina como não conforme devido a ameaças detetadas nesses dispositivos.

> [!Important]  
> A partir de 14 de Agosto de 2018, gestão de dispositivos móveis híbrida é um [funcionalidade preterida](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Para obter mais informações, consulte [o que é a MDM híbrida](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  



## <a name="how-does-it-work"></a>Como funciona?

Como é a implementação de MDM híbrida e a proteção de ameaças de dispositivos do Lookout ajudam a proteger recursos da empresa?

Aplicação móvel do lookout (Lookout for Work) é executado em dispositivos móveis. Ele captura o sistema de ficheiros, pilha de rede e dados de utilização de aplicações e dispositivos onde disponível. A aplicação envia estes dados para o serviço de nuvem de proteção de ameaças de dispositivos do Lookout para calcular o risco de um dispositivo de agregação para ameaças contra dispositivos móveis. Utilize a consola do Lookout para alterar a classificação do nível de risco das ameaças atender às suas necessidades.  

A política de conformidade no Configuration Manager inclui agora uma nova regra para o Lookout mobile threat protection que se baseia a avaliação de riscos de ameaças de dispositivos do Lookout. Quando ativar esta regra, o Configuration Manager avalia a conformidade do dispositivo.

Se o dispositivo estiver em conformidade com a política de conformidade, pode bloquear o acesso a recursos, como o Exchange Online e SharePoint Online através de políticas de acesso condicional. Quando o acesso é bloqueado, o utilizador final recebe um passo a passo para ajudar a resolver o problema e obter acesso aos recursos da empresa. O utilizador inicia este passo a passo através do Lookout for Work a aplicação.



## <a name="supported-platforms"></a>Plataformas suportadas

- **Android 4.1 e posterior**e inscritos no Microsoft Intune.  

- **iOS 8 e posterior**e inscritos no Microsoft Intune.  


Para obter informações sobre as plataformas e idiomas suportados pelo Lookout, consulte esta [artigo de suporte do Lookout](https://personal.support.lookout.com/hc/articles/114094140253).



## <a name="prerequisites"></a>Pré-requisitos

- [MDM híbrida](/sccm/mdm/understand/hybrid-mobile-device-management)  

- Uma subscrição do Microsoft Intune e Azure Active Directory.  

- Uma subscrição do enterprise para o Lookout Mobile EndPoint Security. Para obter mais informações, consulte [Lookout Mobile Endpoint Security](https://www.lookout.com/products/mobile-endpoint-security).  



## <a name="example-scenarios"></a>Cenários de exemplo


### <a name="control-access-based-on-threat-from-malicious-apps"></a>Controlar o acesso com base em ameaças de aplicações maliciosas

Quando são detetadas aplicações maliciosas como software maligno no dispositivo, pode bloquear esses dispositivos de:

- Ligar ao e-mail empresarial antes de resolver a ameaça  

- Sincronizar ficheiros empresariais utilizando o OneDrive para a aplicação de trabalho  

- Aceder a aplicações críticas para a empresa  

#### <a name="access-blocked-when-malicious-apps-are-detected"></a>Acesso bloqueado quando são detetadas aplicações maliciosas

![Política de acesso condicional a bloquear o acesso quando aplicações maliciosas detetadas](media/config-mgr-maliciousapps_blocked.png)

#### <a name="device-unblocked-and-is-able-to-access-company-resources-when-the-threat-is-remediated"></a>Dispositivo desbloqueado e consegue aceder a recursos da empresa quando a ameaça é corrigida

![Política de acesso condicional a conceder acesso quando o dispositivo está em conformidade](media/config-mgr-maliciousapps-unblocked.png)


### <a name="control-access-based-on-threat-to-network"></a>Controlar o acesso com base em ameaças à rede

Detete ameaças à sua rede, tal como ataques man-in-the-middle e restrinja o acesso a redes Wi-Fi com base no risco do dispositivo.

#### <a name="access-to-network-through-wifi-blocked"></a>Acesso à rede através de Wi-Fi bloqueado

![Acesso condicional a bloquear o acesso Wi-Fi com base em ameaças à rede](media/config-mgr-network-wifi-blocked.png)

#### <a name="access-granted-on-remediation"></a>Acesso concedido na remediação

![Acesso condicional a permitir o acesso na remediação da ameaça](media/config-mgr-network-wifi-unblocked.png)


### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Controlar o acesso ao SharePoint Online com base em ameaças à rede

Detete ameaças à sua rede, tal como ataques man-in-the-middle e impeça a sincronização de ficheiros empresariais com base no risco do dispositivo.

#### <a name="access-blocked-sharepoint-online-based-on-network-threat-detected-on-the-device"></a>Acesso bloqueado ao SharePoint Online com base na ameaça de rede detetada no dispositivo

![Acesso condicional a bloquear o acesso de dispositivo ao SharePoint Online](media/config-mgr-network-spo-blocked.png)


#### <a name="access-granted-on-remediation"></a>Acesso concedido na remediação

![Acesso condicional a permitir o acesso após a ameaça é corrigida](media/config-mgr-network-spo-unblocked.png)



## <a name="next-steps"></a>Passos seguintes

Para implementar esta solução, utilize os seguintes passos:  

1.  [Configurar a sua subscrição com proteção contra ameaças móveis do Lookout](set-up-your-subscription-with-lookout.md)
2.  [Ativar a ligação Lookout MTP no Intune](enable-lookout-connection-in-intune.md)
3.  [Configurar e implementar o Lookout para a aplicação de trabalho](configure-and-deploy-lookout-for-work-apps.md)
4.  [Configurar política de conformidade](enable-device-threat-protection-rule-compliance-policy.md)
5.  [Resolução de problemas de integração do Lookout](troubleshoot-lookout-integration.md)
