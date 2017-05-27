---
title: "Políticas de conformidade do dispositivo | Documentos do Microsoft"
description: "Saiba como gerir políticas de conformidade no System Center Configuration Manager, para que os dispositivos fique em conformidade com acesso condicional políticas."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ad8fa94d-45bb-4c94-8d86-31234c5cf21c
caps.latest.revision: 18
caps.handback.revision: 0
author: andredm7
ms.author: andredm
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: bcaa2a9b5474e06bf344dc4fd47dbb160ea36297
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="device-compliance-policies-in-system-center-configuration-manager"></a>Políticas de conformidade do dispositivo no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

**Políticas de conformidade** no System Center Configuration Manager definem as regras e as definições que um dispositivo tem de cumprir para ser considerado conforme pelo acesso condicional políticas. Também pode utilizar as políticas de conformidade para monitorizar e resolver problemas de conformidade com dispositivos independentemente do acesso condicional.  


> [!IMPORTANT]  
>  Este artigo descreve as políticas de conformidade de dispositivos geridos pelo Microsoft Intune.    As políticas de conformidade para PCs geridos pelo System Center Configuration Manager estão descritas em [Gerir o acesso aos serviços do O365 para PCs geridos pelo System Center Configuration Manager](../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md).  

 Estas regras incluem requisitos como:  

-   PINS e palavras-passe para aceder a um dispositivo

-   Encriptação de dados armazenados no dispositivo

-   Se o dispositivo está desbloqueado por jailbrake ou rooting  

-   Se o e-mail no dispositivo é gerido por uma política do Intune, ou se o dispositivo é considerado como mau pelo serviço de atestado de estado de funcionamento de dispositivo do Windows.
-   Aplicações que não podem ser instaladas no dispositivo.


 As políticas de conformidade são implementas em coleções de utilizadores. Quando uma política de conformidade é implementada num utilizador, todos os dispositivos do utilizador são verificados relativamente à conformidade.  

 A tabela seguinte lista os tipos de dispositivos suportados pelas políticas de conformidade e como são geridas as definições não conformes quando as políticas são utilizadas com uma política de acesso condicional.  

|Regra|Windows 8.1 e posterior|Windows Phone 8.1 e posterior|iOS 6.0 e posterior|Android 4.0 e posterior Samsung KNOX Standard 4.0 e posterior, Android para trabalhar|  
|----------|---------------------------|---------------------------------|-----------------------|---------------------------|-----------------------------------------|  
|**Configuração do PIN ou palavra-passe**|Corrigido|Corrigido|Corrigido|Em quarentena|  
|**Encriptação do dispositivo**|N/D|Corrigido|Corrigido (ao definir um PIN)|Em quarentena<br>(Android para trabalhar sempre encriptado)|  
|**Desbloqueado por Jailbreak ou rooting**|N/D|N/D|Em quarentena (não é uma definição)|Em quarentena (não é uma definição)|  
|**Perfil de e-mail**|N/D|N/D|Em quarentena|N/D|  
|**Versão mínima do SO**|Em quarentena|Em quarentena|Em quarentena|Em quarentena|  
|**Versão do SO máximo**|Em quarentena|Em quarentena|Em quarentena|Em quarentena|  
|**Atestado de estado de funcionamento do dispositivo (1602 atualizar)**|A definição não é aplicável ao Windows 8.1<br /><br /> O Windows 10 e o Windows 10 Mobile foram estão Em Quarentena.|N/D|N/D|N/D|  
|**Aplicações que não podem ser instaladas**|N/D|N/D|Em quarentena|Em quarentena|

 **Remediado** = a conformidade é imposta pelo sistema operativo do dispositivo (por exemplo, o utilizador é forçado a definir um PIN).  Nunca se dá o caso de a definição não ser conforme.  

 **Em Quarentena** = o sistema operativo do dispositivo não impõe a conformidade (por exemplo, os dispositivos Android não forçam o utilizador a encriptar o dispositivo).  Neste caso:  

-   O dispositivo será bloqueado se for aplicada uma política de acesso condicional ao utilizador.  

-   O portal da empresa ou o portal Web notificará o utilizador sobre eventuais problemas de conformidade.  


### <a name="next-steps"></a>Passos Seguintes  
[Criar e implementar uma política de conformidade do dispositivo](create-compliance-policy.md)
### <a name="see-also"></a>Consulte também  
 [Gerir o acesso aos serviços no System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md)

