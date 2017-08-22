---
title: Perfis VPN no System Center Configuration Manager | Microsoft Docs
description: "Saiba como utilizar perfis VPN no System Center Configuration Manager para implementar definições VPN em utilizadores da sua organização."
ms.custom: na
ms.date: 11/27/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c0f094f1-852e-4606-91db-97846d8f0772
caps.latest.revision: "6"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: e07a80c1a59043b74cda7219f78c5fef66989ba8
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="vpn-profiles-in-system-center-configuration-manager"></a>Perfis VPN no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Utilize perfis VPN no System Center Configuration Manager (também conhecido como do ConfigMgr ou SCCM) para implementar definições VPN em utilizadores da sua organização. Ao implementar estas definições, estará a minimizar o esforço do utilizador final para se ligar aos recursos na rede da empresa.  

 Por exemplo, pretende aprovisionar todos os dispositivos que executam o sistema operativo do Windows RT com as definições necessárias para ligar a uma partilha de ficheiros na rede empresarial. Pode criar um perfil da VPN com as definições necessárias para ligar à rede empresarial e, em seguida, implementar este perfil em todos os utilizadores com dispositivos que executam o Windows RT na sua hierarquia. Os utilizadores de dispositivos Windows RT veem a ligação VPN na lista de redes disponíveis e podem ligar a esta rede com esforços mínimos.  

 Quando cria um perfil da VPN, pode incluir um vasto leque de definições de segurança, incluindo certificados para validação do servidor e autenticação de cliente que foram aprovisionados através da utilização de perfis de certificado do System Center Configuration Manager. Para obter mais informações sobre perfis de certificado, veja [Perfis de certificado no System Center Configuration Manager](introduction-to-certificate-profiles.md).  

 As secções abaixo explicam o que pode configurar com perfis da VPN se estiver a utilizar o Gestor de configuração de dispositivos.

 Consulte [perfis VPN em dispositivos móveis](/sccm/mdm/deploy-use/create-vpn-profiles) para rever os dispositivos que pode configurar quando utilizar o Configuration Manager com o Microsoft Intune.  

## <a name="vpn-profiles-when-using-configuration-manager"></a>Perfis VPN, ao utilizar o Gestor de configuração  
 A tabela seguinte descreve os perfis VPN, pode configurar para várias plataformas de dispositivos.  

|Tipo de ligação|Windows 8,1|Windows RT|Windows RT 8.1|Windows 10|  
|---------------------|-----------------|----------------|--------------------|----------------|  
|**Cisco AnyConnect**|Não|Não|Não|Não|  
|**Pulse Secure**|Sim|Não|Sim|Sim|  
|**F5 Edge Client**|Sim|Não|Sim|Sim|  
|**Dell SonicWALL Mobile Connect**|Sim|Não|Sim|Sim|  
|**VPN móvel do ponto de verificação**|Sim|Não|Sim|Sim|  
|**Microsoft SSL (SSTP)**|Sim|Sim|Sim|Não|  
|**Microsoft Automatic**|Sim|Sim|Sim|Não|  
|**IKEv2**|Sim|Sim|Sim|Não|  
|**PPTP**|Sim|Sim|Sim|Não|  
|**L2TP**|Sim|Sim|Sim|Não|  

### <a name="next-steps"></a>Passos seguintes  
 Utilize os tópicos seguintes para o ajudar a planear, configurar, operar e manter perfis VPN no Configuration Manager.  

-   [Pré-requisitos para perfis VPN no System Center Configuration Manager](../plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [Segurança e privacidade para perfis VPN no System Center Configuration Manager](../plan-design/security-and-privacy-for-wifi-vpn-profiles.md)
