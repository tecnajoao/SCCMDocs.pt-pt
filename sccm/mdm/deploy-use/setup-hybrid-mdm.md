---
title: Configurar a mm híbrida
titleSuffix: Configuration Manager
description: Configure a inscrição de dispositivos híbrida do Configuration Manager e o Intune.
ms.date: 03/08/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fbc5b9abf63d95185795716cfcb9ebfaf3e2ec3d
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="setup-hybrid-mobile-device-management-mdm-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurar a gestão de dispositivos móveis híbridos (MDM) com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Antes de poder gerir dispositivos iOS, Windows e Android com o Configuration Manager, tem de ser inscritos no Intune. Utilize os seguintes passos para inscrição de dispositivos do programa de configuração híbrido com o Configuration Manager com o Intune. Ao concluir os passos seguintes irá permitir "bring your own device" inscrição (BYOD) para os seus utilizadores. Estes passos também são pré-requisitos para [inscrição de dispositivos BYOD](enroll-hybrid-ios-mac.md) e [inscrever dispositivos pertencentes à empresa](enroll-company-owned-devices.md).

 |Passos|Detalhes|  
 |-----------|-------------|  
 |**Passo 1:** [Criar uma coleção de MDM](create-mdm-collection.md)|Criar uma coleção de utilizador do Configuration Manager com os utilizadores cujos dispositivos podem ser inscritos|  
 |**Passo 2:** [Requisitos de nome de domínio](confirm-dns.md)|Confirmar o serviço de nome de domínio (DNS) da sua organização e gestão de utilizadores do Active Directory cumpre os requisitos de MDM|
 |**Passo 3:** [Configurar a subscrição do Intune](configure-intune-subscription.md)|O serviço do Intune permite-lhe gerir dispositivos através da Internet.|  
 |**Passo 4:** [Adicionar termos e condições](terms-and-conditions.md)| Criar termos e condições para que os utilizadores têm de aceitar antes de poder utilizar a aplicação Portal da empresa|
 |**Passo 5:** [Criar um ponto de ligação de serviço](create-service-connection-point.md)|O ponto de ligação de serviço envia definições e informações de implementação de software do Configuration Manager e obtém mensagens de estado e de inventário de dispositivos móveis. |  
 |**Passo 6:** [Ativar a inscrição da plataforma](enable-platform-enrollment.md)|Inscrição na MDM para iOS e dispositivos Windows exigem passos adicionais para a comunicação entre o serviço e dispositivos. O Android não requer nenhuma configuração adicional.|  
 |**Passo 7:** [Configurar gestão adicional](set-up-additional-management.md)|(Opcional) Configurar itens de configuração e de acesso condicional para dispositivos inscritos|
 |**Passo 8:** [Verificar a configuração da MDM](verify-mdm-configuration.md)|Ver ficheiros de registo para confirmar que o ponto de ligação de serviço foi criado com êxito e contas de utilizador estiver a sincronizar.|

A procurar Intune sem o Configuration Manager?
> [!div class="button"]
[Ver documentos do Intune >](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune)


## <a name="enroll-devices"></a>Inscrever dispositivos
Após a conclusão da configuração híbrida, é possível inscrever dispositivos no Configuration Manager de diversas formas:
- **Dispositivos da empresa (COD):** [Inscrever dispositivos pertencentes à empresa](enroll-company-owned-devices.md) fornece orientações sobre diferentes formas de plataforma específica para inscrever dispositivos pertencentes à empresa.
- **Utilizador (BYOD) dispositivos:** [Inscrever dispositivos (BYOD) detidos](enroll-hybrid-ios-mac.md) fornece orientações para formas de inscrição de dispositivos de propriedade do utilizador.
