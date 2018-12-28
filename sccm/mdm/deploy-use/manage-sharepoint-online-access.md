---
title: Gerir o acesso ao SharePoint Online
titleSuffix: Configuration Manager
description: Saiba como utilizar a System Center Configuration Manager SharePoint Online política de acesso condicional para gerir o acesso para o OneDrive.
ms.date: 12/09/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 49cec466-1676-4fe2-a2fe-5004f01d735e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4d00973704ce49a949c89a37e89ed2d39064cbec
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53422917"
---
# <a name="manage-sharepoint-online-access-in-system-center-configuration-manager"></a>Gerir o acesso ao SharePoint Online no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


A política de acesso condicional do Configuration Manager **SharePoint Online** gere o acesso ao OneDrive para empresas para ficheiros, que são armazenados no SharePoint Online. Acesso baseia-se nas condições que especificar.
Pode controlar o acesso ao SharePoint Online a partir das seguintes aplicações para as plataformas indicadas:  

-   Microsoft Office Mobile (Android)  

-   Microsoft OneDrive (Android e iOS)  

-   Microsoft Word (Android e iOS)  

-   Microsoft Excel (Android e iOS)  

-   Microsoft PowerPoint (Android e iOS)  

-   Microsoft OneNote (Android e iOS)

Aplicativos de área de trabalho do Office podem acessar o SharePoint Online em PCs com o:  

-   Ambiente de trabalho do Office 2013 e versões posteriores com [autenticação moderna](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a) ativada.  

-   Windows 7.0 ou Windows 8.1  

> [!NOTE]  
>  Computadores devem estar associados a um domínio ou em conformidade com as políticas definidas no Intune.  



 Quando um utilizador direcionado tenta ligar a um ficheiro através de uma aplicação suportada, como o OneDrive no respetivo dispositivo, ocorre a seguinte avaliação:  

 ![ConditionalAccess8&#45;6](media/ConditionalAccess8-6.png)  

 Para ligar aos ficheiros necessários, o dispositivo com o OneDrive tem de:  

- Estar inscrito no Microsoft Intune ou o PC associado a um domínio.  

- Registe o dispositivo no Azure Active Directory (Azure AD). Este registo ocorre automaticamente quando o dispositivo é inscrito no Intune.  

   Para PCs associados a um domínio, tem de configurá-lo até [registar automaticamente](/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) com o Azure AD.  

- Estar em conformidade com as políticas de conformidade implementada do Configuration Manager  

  Azure AD armazena o estado do dispositivo. Ele concede ou bloqueia o acesso aos ficheiros, com base nas condições que especificar.  

  Se não for cumprida uma condição, o utilizador é apresentado uma das duas mensagens seguintes quando iniciar sessão:  

- Se o dispositivo não estiver inscrito no Intune ou não estiver registado no Azure AD, é apresentada uma mensagem com instruções sobre como instalar a aplicação Portal da empresa e inscrevê-lo.  

- Se o dispositivo não estiver em conformidade, é apresentada uma mensagem que direciona o utilizador para o portal web do Intune. Aqui poderá encontrar informações sobre o problema e como resolvê-lo.  

- Para dispositivos móveis:

  Pode restringir o acesso ao SharePoint Online quando acede a partir de um browser no **iOS** e **Android** dispositivos. Só é permitido o acesso a partir de browsers suportados em dispositivos em conformidade:  
  - Safari (iOS)
  - Chrome (Android)
  - Managed Browser (iOS e Android)  

    Os browsers não suportados são bloqueados.  

- Num PC:  


  -   Se a política estiver definida para exigir a associação de domínio e o PC não estiver associado a um domínio, será apresentada uma mensagem para contactar o administrador de TI.  

  -   Se a política estiver definida para exigir a associação de domínio ou em conformidade e o PC não cumprir nenhum dos requisitos, é apresentada uma mensagem com instruções sobre como instalar a aplicação Portal da empresa e inscrevê-lo.  

Pode bloquear o acesso ao SharePoint Online a partir das seguintes aplicações:  

-   Microsoft Office Mobile (Android)  

-   Microsoft OneDrive (Android e iOS)  

-   Microsoft Word (Android e iOS)  

-   Microsoft Excel (Android e iOS)  

-   Microsoft PowerPoint (Android e iOS)  

-   Microsoft OneNote (Android e iOS)  



## <a name="configure-conditional-access-for-sharepoint-online"></a>Configurar o acesso condicional para o SharePoint Online  

### <a name="step-1-configure-active-directory-security-groups"></a>Passo 1: Configurar grupos de segurança do Active Directory  
 Antes de começar, configure grupos de segurança do Azure AD para a política de acesso condicional. Pode configurar estes grupos no **centro de administração do Office 365**ou no **portal de contas do Intune**. Estes grupos incluem os utilizadores que são visados ou excluídos da política. Quando um utilizador é direcionado por uma política, cada dispositivo que utiliza tem de estar em conformidade para aceder aos recursos.  

 Pode especificar dois tipos de grupos numa política do SharePoint Online:  

- **Grupos visados**: Contém os grupos de utilizadores aos quais se aplica a política  

- **Grupos excluídos**: Contém os grupos de utilizadores excluídos da política (opcional)  

  Se um utilizador estiver em ambos os grupos, eles são excluídos da política.  

### <a name="step-2-configure-and-deploy-a-compliance-policy"></a>Passo 2: Configurar e implementar uma política de conformidade  
 Criar e implementar uma política de conformidade a todos os dispositivos para que a política do SharePoint Online de destino.  

> [!NOTE]   
>  Enquanto as políticas de conformidade são implementadas nos grupos do Intune ou coleções do Configuration Manager, as políticas de acesso condicional são direcionadas para grupos de segurança do Azure AD.  

 Para obter detalhes sobre como configurar a política de conformidade, veja [Gerir políticas de conformidade no System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md).  

> [!IMPORTANT]  
>  Se não tiver implementado uma política de conformidade e, em seguida, ative a política do SharePoint Online, todos os dispositivos visados são permitidos acesso.  

   

###  <a name="BKMK_OneDrive"></a> Passo 3: Configurar a política do SharePoint Online  

 Em seguida, configure a política para exigir que apenas os dispositivos geridos e em conformidade podem aceder ao SharePoint Online. Esta política é armazenada no Azure AD.

 >[!NOTE]
 >Também pode criar a política de acesso condicional na consola de gestão do Azure AD. Consola de gestão do Azure AD permite-lhe criar as políticas de acesso condicional de dispositivo do Intune. O Azure AD se refere a estas políticas como a política de acesso condicional com base no dispositivo. Também pode criar outras políticas de acesso condicional, como autenticação multifator. No portal, pode definir políticas de acesso condicional para aplicações empresariais de terceiros suportadas pelo Azure AD, como o Salesforce e caixa. Para obter mais informações, consulte [aplicativos conectados de como definir a política de acesso condicional com base no dispositivo do Azure AD para controlo de acesso para o Azure AD](/azure/active-directory/active-directory-conditional-access-policy-connected-applications).  

1. Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  

2. Selecione **ativar política de acesso condicional para o SharePoint Online**.  

    ![IntuneSASharePointOnlineCAPolicy](media/IntuneSASharePointOnlineCAPolicy.png)  

3. Em **Acesso de aplicação**, para o Outlook e aplicações que utilizam a autenticação moderna, pode optar por restringir o acesso apenas a dispositivos que estejam em conformidade em cada plataforma.  

   > [!TIP]
   >  **Autenticação moderna** traz baseada no Active Directory Authentication Library ADAL início de sessão para os clientes do Office.  
   > 
   > - A autenticação baseada na ADAL permite que os clientes do Office participem na autenticação baseada no browser (também conhecido como autenticação passiva). Para autenticar, o utilizador é direcionado para uma página Web de início de sessão.  
   >   -   Este novo método de início de sessão permite novos cenários, como o acesso condicional com base na **conformidade do dispositivo**e se **autenticação multifator** foi executada.  
   > 
   >   Para obter mais informações, consulte [como a autenticação moderna funciona para aplicações de cliente do Office 2013 e Office 2016](https://support.office.com/article/How-modern-authentication-works-for-Office-2013-and-Office-2016-client-apps-e4c45989-4b1a-462e-a81b-2a13191cf517).  

    Para windows PCs, o PC tem de estar domínio associado ou inscritos com o Intune e em conformidade. Pode definir os seguintes requisitos:  

   -   **Dispositivos têm de ser um domínio associado ou em conformidade**: Os PCs têm de estar um domínio associado ou em conformidade com as políticas definidas no Intune. Se o PC não cumprir nenhum destes requisitos, é pedido ao utilizador para inscrever o dispositivo com o Intune.  

   -   **Dispositivos têm de estar associados a um domínio**: Os PCs têm de ser associado ao aceder ao Exchange Online. Se o PC não estiver associado a um domínio, o acesso ao e-mail é bloqueado e é pedido ao utilizador que contacte o administrador de TI.  

   -   **Dispositivos têm de estar em conformidade**: Os PCs têm de estar inscritos no Intune e em conformidade. Se o PC não estiver inscrito, será apresentada uma mensagem com instruções sobre como inscrever.  

4. Sob **o acesso ao Browser** ao SharePoint Online e OneDrive para empresas, pode optar por permitir o acesso ao Exchange Online apenas através de browsers suportados: Safari (iOS) e o Chrome (Android). Acesso a partir de outros browsers é bloqueado. As mesmas restrições de plataforma que selecionou para Acesso da aplicação para o OneDrive também se aplicam aqui.

   No **Android** dispositivos, os utilizadores tem de ativar a **ativar o acesso ao Browser** opção no dispositivo inscrito da seguinte forma:
   1.  Inicie a **aplicação Portal da Empresa**.
   2.  Aceda à página **Definições** a partir das reticências (…) ou do botão do menu de hardware.
   3.  Prima o botão **Ativar o Acesso ao Browser**.
   4.  No browser Chrome, termine sessão no Office 365 e reinicie o Chrome.

   No **iOS e Android** plataformas, para identificar o dispositivo que é utilizado para aceder ao serviço, do Azure AD emite um certificado TLS para o dispositivo. O dispositivo apresenta o certificado com uma linha de comandos para o utilizador final para selecionar o certificado, conforme mostrado nas capturas de ecrã seguintes: O utilizador final tem de selecionar este certificado para poder continuar a utilizar o browser.

    **iOS**

    ![captura de ecrã da linha de comandos da certificado num iPad](media/mdm-browser-ca-ios-cert-prompt_v2.png)

    **Android**

     ![captura de ecrã da linha de comandos do certificado num dispositivo Android](media/mdm-browser-ca-android-cert-prompt.png)

5. No separador **Início** , no grupo **Ligações** , clique em **Configurar Política de Acesso Condicional na Consola do Intune**. Poderá ter de fornecer o nome de utilizador e a palavra-passe da conta utilizada para ligar o Gestor de Configuração ao Intune.  

    Abre a consola de administração do Intune.  

6. Na [consola de administração do Microsoft Intune](https://manage.microsoft.com), clique em **Política** > **Acesso Condicional** > **Política do SharePoint Online**.  

7. Selecione **Bloquear aplicações para impedir acesso ao SharePoint Online se o dispositivo não for compatível**.  

8. Sob **grupos Direcionados**, clique em **modificar** para selecionar os grupos de segurança do Azure AD aos quais se aplica a política.  

9. Sob **grupos excluídos**, opcionalmente, clique em **modificar** para selecionar os grupos de segurança do Azure AD que estão excluídos desta política.  

10. Quando tiver terminado, clique em **Guardar**.  

    Não é necessário implementar a política de acesso condicional, pois esta entra em vigor imediatamente.  

    Ver [acesso gerir o SharePoint Online com o Microsoft Intune](/intune-classic/deploy-use/restrict-access-to-sharepoint-online-with-microsoft-intune) para obter informações sobre como pode monitorizar a política a partir da consola do Intune.  

### <a name="see-also"></a>Consulte também  

 [Gerir o acesso a serviços no System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md)
