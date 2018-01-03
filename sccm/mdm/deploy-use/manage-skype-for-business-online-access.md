---
title: Gerir o acesso ao Skype para Empresas Online
titleSuffix: Configuration Manager
description: "Saiba como utilizar a política de acesso condicional para gerir o acesso ao Skype para empresas Online."
ms.custom: na
ms.date: 12/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 71c44250-626e-482c-8794-434c6aeb2fb1
caps.latest.revision: "6"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 3c1d0c84dc28fb886048cf8d7ea310c2b4dfc4aa
ms.sourcegitcommit: 92c3f916e6bbd35b6208463ff406e0247664543a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/02/2018
---
# <a name="manage-skype-for-business-online-access"></a>Gerir o acesso ao Skype para Empresas Online

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Utilize a política de acesso condicional para o Skype para empresas Online para gerir o acesso ao Skype para empresas Online, com base nas condições que especificar.  


 Quando um utilizador direcionado tenta utilizar o Skype para Empresas Online no respetivo dispositivo, ocorre a seguinte avaliação:![ConditionalAccess&#95;SFBFlow](media/ConditionalAccess_SFBFlow.png)  

## <a name="prerequisites"></a>Pré-requisitos  

-   Ativar [autenticação moderna](https://aka.ms/SkypeModernAuth) para o Skype para empresas Online.   

-   Todos os utilizadores devem utilizar o Skype para empresas Online. Se tiver uma implementação com o Skype para empresas Online e Skype para empresas no local, a política de acesso condicional não é aplicável aos utilizadores no local.  

-   O dispositivo que necessita de acesso ao Skype para Empresas Online deve:  

    -   Ser um dispositivo Android ou iOS

    -   Estar inscrito no Microsoft Intune

    -   Ser compatível com todas políticas de conformidade implementadas do Microsoft Intune

 Azure Active Directory armazena o estado do dispositivo, o qual concede ou bloqueia o acesso com base nas condições que especificar.  
Se não for cumprida uma condição, o utilizador verá uma das mensagens seguintes quando iniciar sessão:  

-   Se o dispositivo não estiver inscrito no Microsoft Intune ou não está registado no Azure Active Directory, o utilizador verá instruções sobre como instalar a aplicação Portal da empresa e inscrevê-lo.  

-   Se o dispositivo não estiver em conformidade, o utilizador verá uma mensagem que direciona-los para o Web site do Portal da empresa ou a aplicação Portal da empresa. O Portal da empresa tem informações sobre o problema e como resolvê-lo.  

## <a name="configure-conditional-access-for-skype-for-business-online"></a>Configurar o acesso condicional do Skype para Empresas Online  

### <a name="step-1-configure-active-directory-security-groups"></a>Passo 1: Configurar grupos de segurança do Active Directory  
 Antes de começar, configure grupos de segurança do Azure Active Directory para a política de acesso condicional. Configure estes grupos no Centro de administração do Office 365. Estes grupos contêm os utilizadores para dirigir ou excluir da política. Quando um utilizador é direcionado por uma política, cada dispositivo que utiliza tem de estar em conformidade para poder aceder aos recursos.  

 Pode especificar dois tipos de grupo a utilizar para o Skype para a política de negócio:  

-   **Grupos direcionados** contêm os utilizadores aos quais se aplica a política  

-   **Grupos excluídos** contêm os utilizadores a serem excluídos da política  
    Se um utilizador estiver em ambos os grupos, que são excluídos.  

### <a name="step-2-configure-and-deploy-a-compliance-policy"></a>Passo 2: Configurar e implementar uma política de conformidade  
 Criar e implementar uma política de conformidade em todos os dispositivos para o qual é direcionada a política do Skype para empresas Online.  

 Para obter mais informações sobre como configurar a política de conformidade, consulte [gerir políticas de conformidade do dispositivo](../../protect/deploy-use/device-compliance-policies.md).  

> [!NOTE]  
>  Se não tiver implementado uma política de conformidade e, em seguida, ativar a política do Skype para empresas Online, todos os dispositivos visados são permissão de acesso se estiverem inscritos no Microsoft Intune.  


### <a name="step-3-configure-the-skype-for-business-online-policy"></a>Passo 3: Configurar a política do Skype para empresas Online  
 Configurar a política para exigir que apenas geridos e conformes podem aceder ao Skype para empresas Online. Esta política é armazenada no Azure Active Directory.  

1.  Na [consola de administração do Microsoft Intune](https://manage.microsoft.com), clique em **Política** > **Acesso Condicional** > **Skype for Business Online Política**.  

     ![ConditionalAccess&#95;SFBPolicy](media/ConditionalAccess_SFBPolicy.png)  

2.  Selecione **Ativar política de acesso condicional**.  

3.  Em **Acesso a aplicações**, pode optar por aplicar a política de acesso condicional a:  

    -   iOS  

    -   Android  

4.  Em **grupos Direcionados**, clique em **modificar** para selecionar os grupos de segurança do Azure Active Directory aos quais se aplica a política. Pode optar por direcionar esta política para todos os utilizadores ou apenas a um grupo de utilizadores.  

5.  Como opção, em **Grupos Excluídos**, clique em **Modificar** para selecionar os grupos de segurança do Azure Active Directory que estão excluídos desta política.  

6.  Quando tiver terminado, clique em **Guardar**.  

 Configurou o acesso condicional do Skype para Empresas Online. Não tem de implementar a política de acesso condicional, pois esta entra em vigor imediatamente.  

## <a name="monitor-the-compliance-and-conditional-access-policies"></a>Monitorizar a conformidade e as políticas de acesso condicional  
 Na área de trabalho Grupos, pode ver o estado do acesso condicional dos seus dispositivos.  

 Selecione qualquer grupo de dispositivos móveis e, em seguida, no separador **Dispositivos** , selecione um dos seguintes **Filtros**:  

-   **Dispositivos que não são registados no AAD** estão bloqueados no Skype para empresas Online

-   **Dispositivos não conformes** estão bloqueados no Skype para empresas Online  

-   **Dispositivos que são registados no AAD e conformes** podem aceder ao Skype para empresas Online  

### <a name="see-also"></a>Consulte também  

 [Gerir políticas de conformidade de dispositivos no System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md)
