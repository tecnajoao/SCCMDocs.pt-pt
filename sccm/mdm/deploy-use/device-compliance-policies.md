---
title: Políticas de conformidade do dispositivo
titleSuffix: Configuration Manager
description: Saiba como gerir políticas de conformidade no Configuration Manager para tornar os dispositivos em conformidade com acesso condicional políticas.
ms.date: 03/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: ad8fa94d-45bb-4c94-8d86-31234c5cf21c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4e225b7ab54a1061387d1c8ee369641f68bd7889
ms.sourcegitcommit: f38ef9afb0c608c0153230ff819e5f5e0fb1520c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/19/2019
ms.locfileid: "58196879"
---
# <a name="device-compliance-policies-in-system-center-configuration-manager"></a>Políticas de conformidade no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Políticas de conformidade no Configuration Manager definem as regras e definições que um dispositivo tem de cumprir para ser considerado conforme pelas políticas de acesso condicional. Também pode utilizar as políticas de conformidade para monitorizar e resolver problemas de conformidade com dispositivos independentemente do acesso condicional.  


> [!IMPORTANT]  
>  Este artigo descreve as políticas de conformidade para dispositivos geridos pelo Microsoft Intune. As políticas de conformidade para dispositivos geridos pelo cliente do Configuration Manager é descrito em [gerir o acesso aos serviços do Office 365 para dispositivos geridos pelo Configuration Manager](/sccm/protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm).  

 Estas regras incluem requisitos, como:  

-   PINS e palavras-passe para aceder a dispositivos  

-   Encriptação de dados armazenados no dispositivo  

-   Se o dispositivo está desbloqueado por jailbrake ou rooting  

-   Se o e-mail no dispositivo é gerido por uma política do Intune, ou se o dispositivo é considerado como mau estado de funcionamento pelo serviço de atestado de estado de funcionamento do dispositivo de Windows.  

-   Aplicações que não podem ser instaladas no dispositivo.  


 As políticas de conformidade são implementas em coleções de utilizadores. Quando uma política de conformidade é implementada num utilizador, todos os dispositivos do utilizador são verificados relativamente à conformidade.  



## <a name="supported-device-types"></a>Tipos de dispositivos suportadas

 A tabela seguinte lista o tipos suportados pelas políticas de conformidade e definições como não conformes são geridos quando a política é utilizada com uma política de acesso condicional de dispositivo.  

|Regra|Windows 8.1 e posterior|Windows Phone 8.1 e posterior|iOS 6.0 e posterior|Android 4.0 e posterior Samsung KNOX Standard 4.0 e posterior, o Android for Work|  
|----------|---------------------------|---------------------------------|-----------------------|---------------------------|-----------------------------------------|  
|**Configuração do PIN ou da palavra-passe**|Corrigido|Corrigido|Corrigido|Em quarentena|  
|**Encriptação do dispositivo**|N/D|Corrigido|Corrigido (ao definir um PIN)|Em quarentena<br>(Android for Work são sempre encriptado)|  
|**Dispositivo desbloqueado por jailbreak ou obtenção de controlo de raiz**|N/D|N/D|Em quarentena (não é uma definição)|Em quarentena (não é uma definição)|  
|**Perfil de e-mail**|N/D|N/D|Em quarentena|N/D|  
|**Versão mínima do SO**|Em quarentena|Em quarentena|Em quarentena|Em quarentena|  
|**Versão máxima do SO**|Em quarentena|Em quarentena|Em quarentena|Em quarentena|  
|**Atestado de estado de funcionamento do dispositivo (atualização 1602)**|Definição não é aplicável ao Windows 8.1<br /><br /> O Windows 10 e o Windows 10 Mobile foram estão Em Quarentena.|N/D|N/D|N/D|  
|**Aplicações que não não possível instalar**|N/D|N/D|Em quarentena|Em quarentena|

 **Remediado** = conformidade é imposta pelo SO do dispositivo. Por exemplo, o utilizador é forçado a definir um PIN. Nunca se dá um caso a configuração está em conformidade.  

 **Em quarentena** = dispositivo SO não impõe a conformidade. Por exemplo, os dispositivos Android não forçam o utilizador a encriptar o dispositivo. Neste caso:  

-   Se o utilizador é direcionado por uma política de acesso condicional, o dispositivo está bloqueado.  

-   O portal da empresa ou o web portal notifica o utilizador sobre eventuais problemas de conformidade.  



## <a name="devices-without-any-assigned-compliance-policy"></a>Dispositivos sem qualquer política de conformidade atribuída
<!--2520152-->
A partir de Julho de 2018, configure se todos os dispositivos que não tenham nenhuma política de conformidade atribuída serão considerados em conformidade ou não conformes. Por predefinição, os dispositivos sem política de conformidade atribuída são considerados conformes. Utilize os seguintes passos para alterar esta definição no portal do Azure:

1. Inicie sessão para o [no portal do Azure](https://aka.ms/intuneportal).  

2. Selecione **conformidade do dispositivo**e, em seguida, selecione **definições de política de conformidade** no grupo de configuração.  

3. Para a definição **marcar os dispositivos sem política de conformidade atribuída como**, selecione uma das seguintes opções:  

     - **Em conformidade** (predefinição) - os dispositivos sem política de conformidade atribuída são considerados em conformidade com a política. Se o acesso condicional estiver ativado, estes dispositivos têm acesso a recursos internos.  

     - **Não conforme** -dispositivos sem política de conformidade atribuída são considerados não conformes com a política. Se o acesso condicional estiver ativado, estes dispositivos estão bloqueados no recursos internos, pelas condições na política de acesso condicional.  

4. Clique em Guardar.  

Recomendamos vivamente que implemente pelo menos uma política de conformidade para cada plataforma para todos os utilizadores no seu ambiente. Em seguida, configure esta definição para **não conformes** para garantir a segurança dos seus recursos internos. Para obter mais informações, consulte a [melhorias de segurança no serviço do Intune](https://aka.ms/compliance_policies) postagem de blog.



## <a name="next-steps"></a>Passos Seguintes  
[Criar e implementar uma política de conformidade do dispositivo](/sccm/mdm/deploy-use/create-compliance-policy)

### <a name="see-also"></a>Consulte também  
 [Gerir o acesso a serviços no Configuration Manager](/sccm/protect/deploy-use/manage-access-to-services)
