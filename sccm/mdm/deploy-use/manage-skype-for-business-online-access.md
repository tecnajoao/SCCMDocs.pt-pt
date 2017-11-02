---
title: Gerir o acesso ao Skype para Empresas Online
titleSuffix: Configuration Manager
description: "Saiba como utilizar a política de acesso condicional para gerir o acesso ao Skype para empresas Online."
ms.custom: na
ms.date: 03/05/2017
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
ms.openlocfilehash: b7886d3e8f181d6d9316c5438dd948b21a658648
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="manage-skype-for-business-online-access"></a>Gerir o acesso ao Skype para Empresas Online

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Utilize a política de acesso condicional do  **Skype para Empresas Online** para gerir o acesso ao Skype para Empresas Online, com base em condições que especificar.  


 Quando um utilizador direcionado tenta utilizar o Skype para Empresas Online no respetivo dispositivo, ocorre a seguinte avaliação:![ConditionalAccess&#95;SFBFlow](media/ConditionalAccess_SFBFlow.png)  

## <a name="prerequisites"></a>Pré-requisitos  

-   Ative autenticação moderna do Skype para Empresas Online. Preencha este [formulário de ligação](https://connect.microsoft.com/office/Survey/NominationSurvey.aspx?SurveyID=17299&ProgramID=8715) para ser inscrito no programa de autenticação moderna.  

-   Todos os utilizadores finais devem utilizar o Skype para empresas Online. Se tiver uma implementação com o Skype para empresas Online e Skype para empresas no local, política de acesso condicional não será aplicada aos utilizadores finais.  

-   O dispositivo que necessita de acesso ao Skype para Empresas Online deve:  

    -   Ser um dispositivo Android ou iOS.  

    -   Estar inscrito no Intune.  

    -   Ser compatível com todas políticas de conformidade do Intune implementadas.  

 O estado do dispositivo é armazenado no Azure Active Directory, o qual concede ou bloqueia o acesso, com base nas condições que especificar.  
Se não for cumprida uma condição, é apresentada ao utilizador uma das duas mensagens seguintes quando iniciar sessão:  

-   Se o dispositivo não estiver inscrito no Intune ou registado no Azure Active Directory, será apresentada uma mensagem com instruções sobre como instalar a aplicação do portal da empresa e inscrevê-la.  

-   Se o dispositivo não for conforme, será apresentada uma mensagem que direciona o utilizador para o Website do portal da empresa do Intune ou para a aplicação do Portal da Empresa, onde é possível obter informações sobre o problema e como resolvê-lo.  

## <a name="configure-conditional-access-for-skype-for-business-online"></a>Configurar o acesso condicional do Skype para Empresas Online  

### <a name="step-1-configure-active-directory-security-groups"></a>Passo 1: Configurar grupos de segurança do Active Directory  
 Antes de começar, configure grupos de segurança do Azure Active Directory para a política de acesso condicional. Pode configurar estes grupos no centro de administração do Office 365. Estes grupos contêm os utilizadores que serão direcionados ou que estarão excluídos da política. Quando um utilizador é direcionado por uma política, cada dispositivo que utiliza tem de estar em conformidade para poder aceder aos recursos.  

 Pode especificar dois tipos de grupo a utilizar para o Skype para a política de negócio:  

-   Direcionados grupos â €"contém os grupos de utilizadores aos quais será aplicada a política  

-   Excluídos grupos â €"contém os grupos de utilizadores excluídos da política (opcional)  
    Se um utilizador estiver em ambos os grupos, estará excluído da política.  

### <a name="step-2-configure-and-deploy-a-compliance-policy"></a>Passo 2: Configurar e implementar uma política de conformidade  
 Certifique-se de que cria e implementa uma política de conformidade em todos os dispositivos para os quais será direcionada a política do Skype para Empresas Online.  

 Para obter detalhes sobre como configurar a política de conformidade, veja [Gerir políticas de conformidade no System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md).  

> [!NOTE]  
>  Se não tiver implementado uma política de conformidade e, em seguida, ativar uma política do Skype para Empresas Online, todos os dispositivos direcionados terão permissão de acesso se estiverem inscritos no Intune.  

 Quando estiver pronto, avance para o Passo 3.  

### <a name="step-3-configure-the-skype-for-business-online-policy"></a>Passo 3: Configurar a política do Skype para empresas Online  
 Em seguida, configure a política para exigir que apenas os dispositivos geridos e em conformidade podem aceder ao Skype para Empresas Online. Esta política será armazenada no Azure Active Directory.  

1.  Na [consola de administração do Microsoft Intune](https://manage.microsoft.com), clique em **Política** > **Acesso Condicional** > **Skype for Business Online Política**.  

     ![ConditionalAccess&#95;SFBPolicy](media/ConditionalAccess_SFBPolicy.png)  

2.  Selecione **Ativar política de acesso condicional**.  

3.  Em **Acesso a aplicações**, pode optar por aplicar a política de acesso condicional a:  

    -   iOS  

    -   Android  

4.  Em **Grupos Direcionados**, clique em **Modificar** para selecionar os grupos de segurança do Azure Active Directory aos quais será aplicada a política. Pode optar por direcionar esta opção para todos os utilizadores ou apenas para um grupos específico de utilizadores.  

5.  Como opção, em **Grupos Excluídos**, clique em **Modificar** para selecionar os grupos de segurança do Azure Active Directory que estão excluídos desta política.  

6.  Quando tiver terminado, clique em **Guardar**.  

 Configurou o acesso condicional do Skype para Empresas Online. Não tem de implementar a política de acesso condicional, pois esta entra em vigor imediatamente.  

## <a name="monitor-the-compliance-and-conditional-access-policies"></a>Monitorizar a conformidade e as políticas de acesso condicional  
 Na área de trabalho Grupos, pode ver o estado do acesso condicional dos seus dispositivos.  

 Selecione qualquer grupo de dispositivos móveis e, em seguida, no separador **Dispositivos** , selecione um dos seguintes **Filtros**:  

-   **Dispositivos que não são registados no AAD** â €"estes dispositivos estão bloqueados no Skype para empresas Online.  

-   **Dispositivos não conformes** â €"estes dispositivos estão bloqueados no Skype para empresas Online.  

-   **Dispositivos que são registados no AAD e conformes** â €"estes dispositivos podem aceder ao Skype para empresas Online.  

### <a name="see-also"></a>Consulte também  

 [Gerir políticas de conformidade de dispositivos no System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md)
