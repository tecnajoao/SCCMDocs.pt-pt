---
title: Gerir o acesso ao SharePoint Online
titleSuffix: Configuration Manager
description: "Saiba como utilizar a System Center Configuration Manager SharePoint Online política de acesso condicional para gerir o acesso ao OneDrive."
ms.custom: na
ms.date: 12/09/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 49cec466-1676-4fe2-a2fe-5004f01d735e
caps.latest.revision: "11"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 99b2aca418b7ce28a4216b38e711b3d38973e2b7
ms.sourcegitcommit: 372171a5cd8d143d6d47b651018cda0c91cad67c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/09/2017
---
# <a name="manage-sharepoint-online-access-in-system-center-configuration-manager"></a>Gerir o acesso ao SharePoint Online no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Utilizar o System Center Configuration Manager **SharePoint Online** política de acesso condicional para gerir o acesso para o OneDrive para ficheiros de empresas localizados no SharePoint online, com base nas condições que especificar.
Pode controlar o acesso ao SharePoint Online a partir das seguintes aplicações para as plataformas indicadas:  

-   Microsoft Office Mobile (Android)  

-   Microsoft OneDrive (Android e iOS)  

-   Microsoft Word (Android e iOS)  

-   Microsoft Excel (Android e iOS)  

-   Microsoft PowerPoint (Android e iOS)  

-   Microsoft OneNote (Android e iOS)

Aplicações de ambiente de trabalho do Office podem aceder ao SharePoint Online em computadores que executam:  

-   Ambiente de trabalho do Office 2013 e versões posteriores com [autenticação moderna](https://support.office.com/en-US/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a) ativada.  

-   Windows 7.0 ou Windows 8.1  

> [!NOTE]  
>  Os computadores devem estar associados a um domínio ou em conformidade com as políticas definidas no Intune.  



 Quando um utilizador direcionado se tentar ligar a um ficheiro através de uma aplicação suportada, como o OneDrive, no respetivo dispositivo, ocorre a seguinte avaliação:  

 ![ConditionalAccess8&#45;6](media/ConditionalAccess8-6.png)  

 Para ligar aos ficheiros necessários, o dispositivo com o OneDrive tem de:  

-   Estar inscrito no Microsoft Intune ou PC associado a um domínio.  

-   Registar o dispositivo no Azure Active Directory (isto ocorre automaticamente quando o dispositivo é inscrito no Intune.  

     Para PCs associados a um domínio, tem de configurá-los para serem [registados automaticamente](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/) no Azure Active Directory.  

-   Ser compatível com todas políticas de conformidade implementadas do Configuration Manager  

 O estado do dispositivo é armazenado no Azure Active Directory, o qual concede ou bloqueia o acesso aos ficheiros, com base nas condições que especificar.  

 Se não for cumprida uma condição, é apresentada ao utilizador uma das duas mensagens seguintes quando iniciar sessão:  

-   Se o dispositivo não estiver inscrito no Intune ou registado no Azure Active Directory, será apresentada uma mensagem com instruções sobre como instalar a aplicação do portal da empresa e inscrevê-la.  

-   Se o dispositivo não for conforme, será apresentada uma mensagem que direciona o utilizador para o portal web do Intune onde é possível localizar informações sobre o problema e como resolvê-lo.  

- Para dispositivos móveis:

  Pode restringir o acesso ao SharePoint Online quando o acesso é feito a partir de um browser de dispositivos **iOS** e **Android**.  O acesso só será permitido a partir de browsers suportados em dispositivos conformes:
* Safari (iOS)
* Chrome (Android)
* Managed Browser (iOS e Android)

  Os browsers não suportados serão bloqueados.
-   Num PC:  


    -   Se a política estiver definida para exigir a associação a um domínio e o PC não estiver associado a qualquer domínio, será apresentada uma mensagem para contactar o administrador de TI.  

    -   Se a política estiver definida para exigir a associação a um domínio ou estar em conformidade, o PC não cumpre nenhum dos requisitos e será apresentada uma mensagem com instruções sobre como instalar o portal da empresa e inscrevê-lo.  

 Pode bloquear o acesso ao SharePoint Online a partir das seguintes aplicações:  

-   Microsoft Office Mobile (Android)  

-   Microsoft OneDrive (Android e iOS)  

-   Microsoft Word (Android e iOS)  

-   Microsoft Excel (Android e iOS)  

-   Microsoft PowerPoint (Android e iOS)  

-   Microsoft OneNote (Android e iOS)  

## <a name="configure-conditional-access-for-sharepoint-online"></a>Configurar o acesso condicional do SharePoint Online  

### <a name="step-1-configure-active-directory-security-groups"></a>Passo 1: Configurar grupos de segurança do Active Directory  
 Antes de começar, configure grupos de segurança do Azure Active Directory para a política de acesso condicional. Pode configurar estes grupos no **centro de administração do Office 365** ou no **portal de contas do Intune**. Estes grupos contêm os utilizadores que serão direcionados ou que estarão excluídos da política. Quando um utilizador é direcionado por uma política, cada dispositivo que utiliza tem de estar em conformidade para poder aceder aos recursos.  

 Pode especificar dois tipos de grupos numa política do SharePoint Online:  

-   **Grupos direcionados** â €"contém os grupos de utilizadores aos quais será aplicada a política  

-   **Grupos excluídos** â €"contém os grupos de utilizadores excluídos da política (opcional)  

 Se um utilizador estiver em ambos os grupos, estará excluído da política.  

### <a name="step-2-configure-and-deploy-a-compliance-policy"></a>Passo 2: Configurar e implementar uma política de conformidade  
 Certifique-se de que cria e implementa uma política de conformidade em todos os dispositivos para os quais será direcionada a política do SharePoint Online.  

> [!NOTE]  
>  Enquanto as políticas de conformidade são implementadas nos grupos do Intune ou coleções do Configuration Manager, as políticas de acesso condicional são direcionadas para grupos de segurança do Azure Active Directory.  

 Para obter detalhes sobre como configurar a política de conformidade, veja [Gerir políticas de conformidade no System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md).  

> [!IMPORTANT]  
>  Se não tiver implementado uma política de conformidade e, em seguida, ativar uma política do SharePoint Online, todos os dispositivos direcionados terão permissão de acesso.  

 Quando estiver pronto, avance para o **Passo 3**.  

###  <a name="BKMK_OneDrive"></a>Passo 3: Configurar a política do SharePoint Online  


 Em seguida, configure a política para exigir que apenas os dispositivos geridos e em conformidade podem aceder ao SharePoint Online. Esta política será armazenada no Azure Active Directory.

 >[!NOTE]
 >Também pode criar política de acesso condicional na consola de gestão do Azure AD. Consola de gestão do Azure AD permite-lhe criar políticas de acesso condicional (referidas como a política de acesso condicional baseado no dispositivo no Azure AD) para além de outras políticas de acesso condicional, como a autenticação multifator do dispositivo do Intune. Também pode definir políticas de acesso condicional para aplicações da empresa de terceiros, como o Salesforce e suporta a caixa de que o Azure AD. Para obter mais detalhes, consulte [como definir a política de acesso condicional baseado no dispositivo do Azure Active Directory para o controlo de acesso ao Azure Active Directory ligado aplicações](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-policy-connected-applications/).  

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  

2.  Selecione **Ativar política de acesso condicional do SharePoint Online**.  

     ![IntuneSASharePointOnlineCAPolicy](media/IntuneSASharePointOnlineCAPolicy.png)  

3.  Em **Acesso de aplicação**, para o Outlook e aplicações que utilizam a autenticação moderna, pode optar por restringir o acesso apenas a dispositivos que estejam em conformidade em cada plataforma.  

    > [!TIP]  
    >  A **Autenticação moderna** fornece um início de sessão baseado na ADAL (Active Directory Authentication Library) aos clientes do Office.  
    >   
    >  -   A autenticação baseada na ADAL permite que os clientes do Office participem na autenticação baseada no browser (também conhecido como autenticação passiva).  Para autenticar, o utilizador é direcionado para uma página Web de início de sessão.  
    > -   Este novo método de início de sessão permite novos cenários, como o acesso condicional, com base na **conformidade do dispositivo** e no facto de a **autenticação multifator** ter sido ou não executada.  
    >   
    >  Este [artigo](https://support.office.com/en-US/article/How-modern-authentication-works-for-Office-2013-and-Office-2016-client-apps-e4c45989-4b1a-462e-a81b-2a13191cf517) tem informações mais detalhadas sobre como funciona a autenticação moderna.  

     Para windows PCs, o PC tem de ser um domínio associado ou inscritos no Intune e em conformidade. Pode definir os seguintes requisitos:  

    -   **Os dispositivos têm de estar associados a um domínio ou em conformidade.** Isto significa que os PCs têm de estar domínio associado ou em conformidade com as políticas definidas no Intune. Se o PC não cumprir nenhum destes requisitos, é pedido ao utilizador para inscrever o dispositivo no Intune.  

    -   **Os dispositivos têm de estar associados a um domínio.** Isto significa que os PCs têm de estar associados a um domínio para acederem ao Exchange Online. Se o PC não estiver associado a um domínio, o acesso ao e-mail é bloqueado e é pedido ao utilizador para contactar o administrador de TI.  

    -   **Os dispositivos têm de estar em conformidade.** Isto significa que os PCs têm de estar inscritos no Intune e conformes. Se o PC não estiver inscrito, será apresentada uma mensagem com instruções sobre como inscrevê-lo.  

4.  Em **acesso ao Browser** ao SharePoint Online e OneDrive para empresas, pode optar por permitir o acesso ao Exchange Online apenas através de browsers suportados: Safari (iOS) e o Chrome (Android). O acesso a partir de outros browsers será bloqueado.  As mesmas restrições de plataforma que selecionou para Acesso da aplicação para o OneDrive também se aplicam aqui.

    Em dispositivos **Android** , os utilizadores têm de ativar o acesso ao browser.  Para tal, o utilizador final tem de ativar o **ativar o acesso ao Browser** opção no dispositivo inscrito da seguinte forma:
    1.  Inicie a **aplicação Portal da Empresa**.
    2.  Vá para o **definições** página a partir das reticências (â €¦) ou no botão do menu de hardware.
    3.  Prima o botão **Ativar acesso ao browser** .
    4.  No browser Chrome, termine sessão no Office 365 e reinicie o Chrome.

    Nas plataformas **iOS e Android** , para identificar o dispositivo que é utilizado para aceder ao serviço, o Azure Active Directory emitirá um certificado Transport Layer Security (TLS) para o dispositivo.  O dispositivo apresenta o certificado com uma linha de comandos ao utilizador final para selecionar o certificado, tal como mostram as capturas de ecrã abaixo. O utilizador final tem de selecionar este certificado para poder continuar a utilizar o browser.

     **iOS**

     ![captura de ecrã da linha de comandos do certificado num ipad](media/mdm-browser-ca-ios-cert-prompt_v2.png)

     **Android**

      ![captura de ecrã da linha de comandos do certificado num dispositivo Android](media/mdm-browser-ca-android-cert-prompt.png)

4.  No separador **Início** , no grupo **Ligações** , clique em **Configurar Política de Acesso Condicional na Consola do Intune**. Poderá ter de fornecer o nome de utilizador e a palavra-passe da conta utilizada para ligar o Gestor de Configuração ao Intune.  

     A consola de administração do Intune irá abrir.  

5.  Na [consola de administração do Microsoft Intune](https://manage.microsoft.com), clique em **Política** > **Acesso Condicional** > **Política do SharePoint Online**.  

6.  Selecione **Bloquear aplicações para impedir acesso ao SharePoint Online se o dispositivo não for compatível**.  

7.  Em **Grupos Direcionados**, clique em **Modificar** para selecionar os grupos de segurança do Azure Active Directory aos quais será aplicada a política.  

8.  Como opção, em **Grupos Excluídos**, clique em **Modificar** para selecionar os grupos de segurança do Azure Active Directory que estão excluídos desta política.  

9. Quando tiver terminado, clique em **Guardar**.  

 Não tem de implementar a política de acesso condicional, pois esta entra em vigor imediatamente.  

 Consulte [acesso gerir o SharePoint Online com o Microsoft Intune](https://technet.microsoft.com/library/dn705844.aspx) para obter informações sobre como pode monitorizar a política a partir da consola do Intune.  

### <a name="see-also"></a>Consulte também  

 [Gerir o acesso a serviços no System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md)
