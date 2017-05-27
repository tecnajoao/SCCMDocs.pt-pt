---
title: "Híbrida configuração MDM | Documentos do Microsoft"
description: "Configure a inscrição de dispositivos de híbrida com o Configuration Manager e do Intune."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
caps.latest.revision: 34
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: c494fcc38955571c06507278a1ae88e5777b5708
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---

# <a name="setup-hybrid-mobile-device-management-mdm-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurar a gestão de dispositivos móveis (MDM) híbrida com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Antes de poder gerir dispositivos Android com o Configuration Manager, iOS e Windows, tem de ser inscritos com o Intune. Utilize os seguintes passos para inscrição de dispositivos do programa de configuração híbrida com o Configuration Manager através do Intune. Concluindo os seguintes passos ativará "bring your own device" inscrição (BYOD) para os seus utilizadores. Estes passos também são pré-requisitos para [a inscrição de dispositivos BYOD](enroll-hybrid-ios-mac.md) e [inscrever dispositivos pertencentes à empresa](enroll-company-owned-devices.md).

 |Passos|Detalhes|  
 |-----------|-------------|  
 |**Passo 1:** [Criar uma coleção de MDM](create-mdm-collection.md)|Crie uma coleção de utilizador do Configuration Manager com utilizadores cujos dispositivos poderem ser inscritos|  
 |**Passo 2:** [Requisitos de nome de domínio](confirm-dns.md)|Confirmar o serviço de nome de domínio (DNS) da sua organização e gestão de utilizadores do Active Directory cumpre os requisitos de MDM|
 |**Passo 3:** [Configurar a subscrição do Intune](configure-intune-subscription.md)|O serviço Intune permite-lhe gerir dispositivos através da Internet.|  
 |**Passo 4:** [Adicionar termos e condições](terms-and-conditions.md)| Criar termos e condições ao qual os utilizadores devem aceitar antes de poderem utilizar a aplicação de Portal da empresa|
 |**Passo 5:** [Criar ponto de ligação de serviço](create-service-connection-point.md)|O ponto de ligação de serviço envia definições e informações de implementação de software do Configuration Manager e obtém mensagens de estado e de inventário de dispositivos móveis. |  
 |**Passo 6:** [Ativar a inscrição de plataforma](enable-platform-enrollment.md)|Inscrição na MDM para Windows dispositivos iOS e necessitam de passos adicionais para comunicação entre o serviço e dispositivos. Android não requer nenhuma configuração adicional.|  
 |**Passo 7:** [Configurar a gestão adicional](set-up-additional-management.md)|(Opcional) Configurar o acesso condicional para dispositivos inscritos e itens de configuração|
 |**Passo 8:** [Verificar a configuração de MDM](verify-mdm-configuration.md)|Ver ficheiros de registo para confirmar que o ponto de ligação de serviço foi criado com êxito e contas de utilizador estão a sincronizar.|

Está à procura do Intune sem o Configuration Manager?
> [!div class="button"]
[Ver documentos do Intune >](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune)


## <a name="enroll-devices"></a>Inscrever dispositivos
Após a conclusão da configuração híbrida, é possível inscrever dispositivos no Configuration Manager de diversas formas:
- **Dispositivos da empresa (COD):** [Inscrever dispositivos pertencentes à empresa](enroll-company-owned-devices.md) fornece orientação sobre formas específicas da plataforma diferentes para inscrever dispositivos pertencentes à empresa.
- **Utilizador (BYOD) dispositivos:** [Inscrever dispositivos de propriedade do utilizador de (BYOD)](enroll-hybrid-ios-mac.md) fornece orientação sobre formas de inscrição de dispositivos detidos pelos utilizadores.

