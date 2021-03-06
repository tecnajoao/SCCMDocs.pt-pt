---
title: Gerir o acesso ao Skype para Empresas Online
titleSuffix: Configuration Manager
description: Saiba como utilizar a política de acesso condicional para gerir o acesso ao Skype para empresas Online.
ms.date: 03/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 71c44250-626e-482c-8794-434c6aeb2fb1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 601b58b2f955170e5ab2f038cb49306efe3b499c
ms.sourcegitcommit: ec4411fe30770f90128cf6cbd181047db90040cb
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/14/2019
ms.locfileid: "57881729"
---
# <a name="manage-skype-for-business-online-access"></a>Gerir o acesso ao Skype para Empresas Online

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Utilize a política de acesso condicional para o Skype para empresas Online para gerir o acesso ao Skype para empresas Online, com base nas condições que especificar.  


 Quando um utilizador direcionado tenta utilizar o Skype para Empresas Online no respetivo dispositivo, ocorre a seguinte avaliação:![ConditionalAccess&#95;SFBFlow](media/ConditionalAccess_SFBFlow.png)  

## <a name="prerequisites"></a>Pré-requisitos  

- Ativar [autenticação moderna](https://aka.ms/SkypeModernAuth) para o Skype para empresas Online.   

- Todos os utilizadores devem utilizar o Skype para empresas Online. Se tiver uma implementação com o Skype para empresas Online e Skype para empresas no local, política de acesso condicional não se aplica aos utilizadores no local.  

- O dispositivo que necessita de acesso ao Skype para Empresas Online deve:  

  -   Ser um dispositivo Android ou iOS

  -   Estar inscrito no Microsoft Intune

  -   Estar em conformidade com as políticas de conformidade implementadas do Microsoft Intune

  O Azure Active Directory armazena o estado do dispositivo, o qual concede ou bloqueia o acesso com base nas condições que especificar.  
  Se não for cumprida uma condição, o utilizador vê uma das duas mensagens seguintes quando iniciar sessão:  

- Se o dispositivo não estiver inscrito no Microsoft Intune ou não está registado no Azure Active Directory, o utilizador verá instruções sobre como instalar a aplicação Portal da empresa e inscrevê-lo.  

- Se o dispositivo não estiver em conformidade, o utilizador verá uma mensagem que direciona-los para o site do Portal da empresa ou a aplicação Portal da empresa. O Portal da empresa tem informações sobre o problema e como resolvê-lo.  

## <a name="configure-conditional-access-for-skype-for-business-online"></a>Configurar o acesso condicional do Skype para Empresas Online  

### <a name="step-1-configure-active-directory-security-groups"></a>Passo 1: Configurar grupos de segurança do Active Directory  
 Antes de começar, configure grupos de segurança do Azure Active Directory para a política de acesso condicional. Configure estes grupos no Centro de administração do Microsoft 365. Estes grupos contêm os utilizadores visados ou excluir da política. Quando um utilizador é direcionado por uma política, cada dispositivo que utiliza tem de estar em conformidade para poder aceder aos recursos.  

 Pode especificar dois tipos de grupo a utilizar para o Skype para a política de negócio:  

-   **Grupos visados** contêm os utilizadores aos quais se aplica a política  

-   **Grupos excluídos** contêm os utilizadores a excluir da política  
    Se um utilizador estiver em ambos os grupos, o que são excluídos.  

### <a name="step-2-configure-and-deploy-a-compliance-policy"></a>Passo 2: Configurar e implementar uma política de conformidade  
 Criar e implementar uma política de conformidade a todos os dispositivos aos quais destina-se a política do Skype para empresas Online.  

 Para obter detalhes sobre como configurar a política de conformidade, consulte [gerir políticas de conformidade do dispositivo](../../protect/deploy-use/device-compliance-policies.md).  

> [!NOTE]  
>  Se não tiver implementado uma política de conformidade e, em seguida, ativar a política do Skype para empresas Online, todos os dispositivos visados são permitidos acesso se estiverem inscritos no Microsoft Intune.  


### <a name="step-3-configure-the-skype-for-business-online-policy"></a>Passo 3: Configurar a política do Skype para empresas Online  
 Configurar a política para exigir que apenas geridos e conformes podem aceder ao Skype para empresas Online. Esta política é armazenada no Azure Active Directory.  

1. Na [consola de administração do Microsoft Intune](https://manage.microsoft.com), clique em **Política** > **Acesso Condicional** > **Skype for Business Online Política**.  

    ![ConditionalAccess&#95;SFBPolicy](media/ConditionalAccess_SFBPolicy.png)  

2. Selecione **Ativar política de acesso condicional**.  

3. Em **Acesso a aplicações**, pode optar por aplicar a política de acesso condicional a:  

   -   iOS  

   -   Android  

4. Sob **grupos Direcionados**, clique em **modificar** para selecionar os grupos de segurança do Azure Active Directory aos quais se aplica a política. Pode optar por direcionar esta política para todos os utilizadores ou apenas a um grupo de utilizadores.  

5. Como opção, em **Grupos Excluídos**, clique em **Modificar** para selecionar os grupos de segurança do Azure Active Directory que estão excluídos desta política.  

6. Quando tiver terminado, clique em **Guardar**.  

   Configurou o acesso condicional do Skype para Empresas Online. Não tem de implementar a política de acesso condicional, pois esta entra em vigor imediatamente.  

## <a name="monitor-the-compliance-and-conditional-access-policies"></a>Monitorizar a conformidade e as políticas de acesso condicional  
 Na área de trabalho Grupos, pode ver o estado do acesso condicional dos seus dispositivos.  

 Selecione qualquer grupo de dispositivos móveis e, em seguida, no separador **Dispositivos** , selecione um dos seguintes **Filtros**:  

-   **Dispositivos que não são registados no AAD** estão bloqueados no Skype para empresas Online

-   **Dispositivos que não estejam em conformidade** estão bloqueados no Skype para empresas Online  

-   **Dispositivos que estão registados no AAD e conformes** podem aceder ao Skype para empresas Online  

### <a name="see-also"></a>Consulte também  

 [Gerir políticas de conformidade no System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md)
