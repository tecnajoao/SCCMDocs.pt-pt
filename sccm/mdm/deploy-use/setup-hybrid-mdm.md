---
title: Configurar a MDM híbrida
titleSuffix: Configuration Manager
description: Configure a inscrição de dispositivos híbrida com o Configuration Manager e o Intune.
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a69f849d4843ff7a0cf7df4a0b6de044a9506301
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53421812"
---
# <a name="set-up-hybrid-mdm-with-configuration-manager-and-microsoft-intune"></a>Configurar a MDM híbrida com o Configuration Manager e o Microsoft Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Antes de poder gerir dispositivos iOS, Windows e Android com o Configuration Manager, tem de ser inscritos com o Intune. Utilize os seguintes passos para configurar a inscrição de dispositivos híbrida com o Configuration Manager com o Intune. Ao concluir os passos seguintes, irá ativar "bring your own device" inscrição (BYOD) para os seus utilizadores. Estes passos também são os pré-requisitos para [inscrição de dispositivos BYOD](enroll-hybrid-ios-mac.md) e [inscrição de dispositivos pertencentes à empresa](enroll-company-owned-devices.md).

> [!Important]  
> A partir de 14 de Agosto de 2018, gestão de dispositivos móveis híbrida é um [funcionalidade preterida](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Para obter mais informações, consulte [o que é a MDM híbrida](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  



## <a name="set-up-steps"></a>Passos da configuração

 |Passos|Detalhes|  
 |-----------|-------------|  
 |**Passo 1:** [Criar uma coleção de MDM](create-mdm-collection.md)|Criar uma coleção de utilizadores do Configuration Manager com os utilizadores cujos dispositivos podem ser inscritos|  
 |**Passo 2:** [Requisitos de nome de domínio](confirm-dns.md)|Confirme o serviço de nome de domínio (DNS) da sua organização e gestão de utilizadores do Active Directory cumpre os requisitos de MDM|
 |**Passo 3:** [Configurar a subscrição do Intune](configure-intune-subscription.md)|O serviço do Intune permite-lhe gerir dispositivos através da Internet.|  
 |**Passo 4:** [Adicionar termos e condições](terms-and-conditions.md)| Criar termos e condições para o qual os utilizadores têm de aceitar antes de poderem utilizar a aplicação Portal da empresa|
 |**Passo 5:** [Criar um ponto de ligação de serviço](create-service-connection-point.md)|O ponto de ligação de serviço envia definições e informações de implementação de software para o Configuration Manager e obtém mensagens de estado e de inventário de dispositivos móveis. |  
 |**Passo 6:** [Ativar a inscrição da plataforma](enable-platform-enrollment.md)|Inscrição de MDM para iOS e dispositivos do Windows exigem passos adicionais para a comunicação entre o serviço e dispositivos. O Android não precisa nenhuma configuração adicional.|  
 |**Passo 7:** [Configurar gestão adicional](set-up-additional-management.md)|(Opcional) Configurar a itens de configuração e de acesso condicional para dispositivos inscritos|
 |**Passo 8:** [Verificar a configuração da MDM](verify-mdm-configuration.md)|Ver ficheiros de registo para confirmar que o ponto de ligação de serviço foi criado com êxito e contas de utilizador estiver a sincronizar.|



## <a name="enroll-devices"></a>Inscrever dispositivos

Após a conclusão da configuração híbrida, é possível inscrever dispositivos no Configuration Manager de diversas formas:

- **Dispositivos da empresa (COD):** [Inscrever dispositivos pertencentes à empresa](enroll-company-owned-devices.md) fornece orientações sobre as diferentes formas de específicas da plataforma para inscrever dispositivos pertencentes à empresa  

- **Dispositivos detidos pelos (BYOD):** [Inscrever dispositivos detidos pelos (BYOD)](enroll-hybrid-ios-mac.md) fornece orientações sobre as formas de inscrever dispositivos pertencentes ao utilizador  



## <a name="see-also"></a>Consulte também

Está à procura do Intune sem o Configuration Manager?
> [!div class="button"]
> [Ver documentos do Intune >](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune)


