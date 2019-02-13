---
title: Perfis VPN
titleSuffix: Configuration Manager
description: Saiba como utilizar perfis VPN no System Center Configuration Manager para implementar definições VPN em utilizadores na sua organização.
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: c0f094f1-852e-4606-91db-97846d8f0772
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6c3217dee8406b46aeb93925c368f18f402bfb70
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56123598"
---
# <a name="vpn-profiles-in-system-center-configuration-manager"></a>Perfis VPN no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

<!--1283610--> Para implementar definições VPN em utilizadores na sua organização, utilize perfis VPN no Configuration Manager. Ao implementar estas definições, estará a minimizar o esforço do utilizador final para se ligar aos recursos na rede da empresa.  

 Por exemplo, que pretende configurar todos os dispositivos Windows 10 com as definições necessárias para ligar a uma partilha de ficheiros na rede empresarial. Pode criar um perfil VPN com as definições necessárias para ligar à rede empresarial. Em seguida, implemente este perfil em todos os utilizadores com dispositivos com o Windows 10. Estes utilizadores veem a ligação de VPN na lista de redes disponíveis e podem ligar-se com pouco esforço.  

 Quando cria um perfil VPN, pode incluir uma grande variedade de definições de segurança. Estas definições incluem certificados para validação do servidor e autenticação de cliente que for aprovisionado com perfis de certificado do Configuration Manager. Para obter mais informações, consulte [perfis de certificado](introduction-to-certificate-profiles.md).  

> [!Note]  
> O Configuration Manager não permite esta funcionalidade opcional por predefinição. Tem de ativar esta funcionalidade antes de o utilizar. Para obter mais informações, consulte [ativar funcionalidades opcionais de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


 Ver [perfis VPN em dispositivos móveis](/sccm/mdm/deploy-use/create-vpn-profiles) para rever os dispositivos que pode configurar quando utilizar o Configuration Manager com o Microsoft Intune.  

## <a name="vpn-profiles-when-using-configuration-manager"></a>Perfis VPN, quando utilizar o Configuration Manager  
 A tabela seguinte descreve os perfis VPN, que pode configurar para várias plataformas de dispositivos.  

|Tipo de ligação|Windows 8,1|Windows RT|Windows RT 8.1|Windows 10|  
|---------------------|-----------------|----------------|--------------------|----------------|  
|**Cisco AnyConnect**|Não|Não|Não|Não|  
|**Pulse Secure**|Sim|Não|Sim|Sim|  
|**F5 Edge Client**|Sim|Não|Sim|Sim|  
|**Dell SonicWALL Mobile Connect**|Sim|Não|Sim|Sim|  
|**Check Point Mobile VPN**|Sim|Não|Sim|Sim|  
|**Microsoft SSL (SSTP)**|Sim|Sim|Sim|Não|  
|**Microsoft Automatic**|Sim|Sim|Sim|Não|  
|**IKEv2**|Sim|Sim|Sim|Não|  
|**PPTP**|Sim|Sim|Sim|Não|  
|**L2TP**|Sim|Sim|Sim|Não|  

### <a name="next-steps"></a>Passos seguintes  
 Utilize os tópicos seguintes para o ajudar a planear, configurar, operar e manter perfis VPN no Configuration Manager.  

-   [Pré-requisitos para perfis VPN no System Center Configuration Manager](../plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [Segurança e privacidade para perfis VPN no System Center Configuration Manager](../plan-design/security-and-privacy-for-wifi-vpn-profiles.md)
