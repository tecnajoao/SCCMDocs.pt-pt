---
title: Gerir o acesso ao e-mail | Documentos do Microsoft
description: Saiba como utilizar o acesso condicional do System Center Configuration Manager para gerir o acesso ao e-mail do Exchange.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fa648e73-5fb8-4818-ab57-7466ffaf888e
caps.latest.revision: 24
author: andredm7
ms.author: andredm
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 6424fb07802b62820b4dc78a58ab30d3b956abef
ms.openlocfilehash: a5c2a8912cd2ef95a778b81d0b7f1f98315b8413
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="manage-email-access-in-system-center-configuration-manager"></a>Gerir o acesso ao e-mail no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilização do System Center Configuration Manager o acesso condicional para gerir o acesso ao e-mail do Exchange com base em condições que especificar.  

Pode gerir o acesso ao:  

-   Microsoft Exchange No Local  

-   Microsoft Exchange Online  

-   Exchange Online Dedicado

Pode controlar o acesso ao Exchange Online e ao Exchange No Local a partir do cliente de e-mail incorporado nas seguintes plataformas:  

-   Android 4.0 e posterior, Samsung KNOX Standard 4.0 e posterior  

-   iOS 7.1 e posterior  

-   Windows Phone 8.1 e posterior  

-   Aplicação de correio no Windows 8.1 e posterior

Aplicações de ambiente de trabalho do Office podem aceder ao Exchange Online em PCs a executar:  

-   Ambiente de trabalho do Office 2013 e versões posteriores com [autenticação moderna](https://support.office.com/en-US/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a) ativada.  

-   Windows 7.0 ou Windows 8.1  

> [!NOTE]  
>  PCs devem ser domínio associado ou ser conformidade com as políticas definidas no Intune.  


## <a name="device-requirements"></a>Requisitos de dispositivo
 Se configurar o acesso condicional, antes de um utilizador se poder ligar ao respetivo e-mail, o dispositivo que ele utiliza deve:  

-   Inscrito com o Intune ou PC associado a um domínio.  

-   Registar o dispositivo no Azure Active Directory (isto ocorre automaticamente quando o dispositivo é inscrito com o Intune (apenas para Exchange Online). Além disso, o ID do Exchange ActiveSync cliente tem de estar registado no Azure Active Directory (não se aplica a dispositivos Windows e Windows Phone que se liguem ao Exchange No Local).  

     Para um PC associado a um domínio, tem de defini-lo para ser registado automaticamente no Azure Active Directory.  A secção **Acesso Condicional para PCs** do tópico [Gerir o acesso a serviços no System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md) apresenta uma lista do conjunto completo de requisitos para ativar o acesso condicional em PCs.  

-   Ser compatível com as políticas de conformidade do Configuration Manager implementadas nesse dispositivo  

 Se não for cumprida uma condição de acesso condicional, é apresentada ao utilizador uma das duas mensagens seguintes quando iniciar sessão:  

-   Se o dispositivo não estiver inscrito com o Intune ou não está registado no Azure Active Directory, será apresentada uma mensagem com instruções sobre como instalar a aplicação do portal da empresa, inscrever o dispositivo e (para dispositivos Android e iOS), ativar o e-mail, o qual associa o ID do Exchange ActiveSync ao registo do dispositivo no Azure Active Directory.  

-   Se o dispositivo não for conforme, será apresentada uma mensagem que direciona o utilizador para o portal web do Intune onde pode encontrar informações sobre o problema e como resolvê-lo.  

**Para dispositivos móveis:**

Pode restringir o acesso ao **Outlook Web Access (OWA)** no Exchange Online quando o acesso for feito a partir de um browser em dispositivos **iOS** e **Android** .  O acesso só será permitido a partir de browsers suportados em dispositivos conformes:

* Safari (iOS)
* Chrome (Android)
* Managed Browser (iOS e Android)

Os browsers não suportados serão bloqueados. As aplicações do OWA para iOS e Android não são suportadas.  Devem ser bloqueadas através de regras de afirmações do ADFS:
* Configure regras de afirmações do ADFS para bloquear protocolos de autenticação não moderna. O cenário 3 - [bloquear todos os acessos ao O365 exceto aplicações baseadas no browser](https://technet.microsoft.com/library/dn592182.aspx)fornece instruções detalhadas.

 **Para PCs:**  

-   Se o requisito de política de acesso condicional permitir a **associação a um domínio** ou a **conformidade**, será apresentada uma mensagem com instruções sobre como inscrever o dispositivo. Se o PC não cumprir nenhum dos requisitos, será pedido ao utilizador para inscrever o dispositivo no Intune.  

-   Se o requisito da política de acesso condicional estiver definido para permitir apenas dispositivos Windows associados a um domínio, o dispositivo será bloqueado e será apresentada uma mensagem para contactar o administrador de TI.  

 Pode bloquear o acesso ao e-mail do Exchange no cliente de e-mail Exchange ActiveSync incorporado no dispositivo nas seguintes plataformas:  

-   Android 4.0 e posterior, Samsung KNOX Standard 4.0 e posterior  

-   iOS 7.1 e posterior  

-   Windows Phone 8.1 e posterior  

-   A aplicação **Correio** no Windows 8.1 e posterior  

 A aplicação Outlook para iOS e Android, e o Outlook Desktop 2013 e posterior é suportada apenas para o Exchange Online.  

 O **conector do Exchange no local** entre o Configuration Manager e o Exchange é necessário para o acesso condicional para o seu trabalho.  

 Pode configurar uma política de acesso condicional para Exchange no local a partir da consola do Configuration Manager. Quando configura uma política de acesso condicional para o Exchange Online, pode começar o processo na consola do Configuration Manager, que inicia a consola do Intune onde pode concluir o processo.  

## <a name="configure-conditional-access"></a>Configurar o acesso condicional
### <a name="step-1-evaluate-the-effect-of-the-conditional-access-policy"></a>Passo 1: Avaliar o efeito da política de acesso condicional  
 Assim que tiver configurado o **conector do Exchange no local**, pode utilizar o Gestor de configuração**lista de dispositivos por Estado de acesso condicional** relatório para identificar os dispositivos que serão impedidos de aceder ao Exchange após configurar a política de acesso condicional. Este relatório também requer:  

-   Uma subscrição do Intune  

-   O ponto de ligação de serviço deve ser configurado e implementado  

 Nos parâmetros do relatório, selecione o grupo do Intune que pretende avaliar e, se necessário, as plataformas de dispositivos às quais será aplicada a política.  

 Para obter mais informações sobre como executar relatórios, veja [Os relatórios do System Center Configuration Manager](../../core/servers/manage/reporting.md).  

 Depois de executar o relatório, examine estas quatro colunas para determinar se um utilizador será bloqueado:  

-   **Canal de gestão** -indica se o dispositivo é gerido pelo Intune, o Exchange ActiveSync ou ambos.  

-   **Registado no AAD** -indica se o dispositivo está registado no Azure Active Directory (conhecido como associação).  

-   **Conformidade** -indica se o dispositivo está em conformidade com as políticas de conformidade implementadas.  

-   **Ativado EAS** -dispositivos iOS e Android são necessários para que os respetivos ID do Exchange ActiveSync associado ao registo de registo do dispositivo no Azure Active Directory. Isto acontece quando o utilizador clica na ligação **Ativar E-mail** no e-mail de quarentena.  

    > [!NOTE]  
    >  Os dispositivos Windows Phone apresentam sempre um valor nesta coluna.  

 Os dispositivos que fazem parte de uma coleção ou grupo de destino serão impedidos de aceder ao Exchange, exceto se os valores da coluna corresponderem aos listados na seguinte tabela:  

|Canal de Gestão|Registado no AAD|conformidade|EAS Ativado|Ação resultante|  
|------------------------|--------------------|---------------|-------------------|----------------------|  
|**Gerido pelo Microsoft Intune e pelo Exchange ActiveSync**|Sim|Sim|É apresentado**Sim** ou **Não** |Acesso ao e-mail permitido|  
|Qualquer outro valor|Não|Não|Não é apresentado nenhum valor|Acesso ao e-mail bloqueado|  

 Pode exportar os conteúdos do relatório e utilizar a coluna **Endereço de E-mail** para ajudar a informar os utilizadores de que serão bloqueados.  

### <a name="step-2-configure-user-groups-or-collections-for-the-conditional-access-policy"></a>Passo 2: Configurar grupos de utilizadores ou de coleções para a política de acesso condicional  
 O direcionamento de políticas de acesso condicional para diferentes coleções ou grupos de utilizadores depende dos tipos de políticas. Estes grupos contêm os utilizadores que serão direcionados ou que estarão excluídos da política. Quando um utilizador é direcionado por uma política, cada dispositivo que utiliza tem de estar em conformidade para poder aceder ao e-mail.  

-   **Para a política do Exchange Online** – para grupos de utilizadores de segurança do Azure Active Directory. Pode configurar estes grupos no **centro de administração do Office 365**ou no **portal de contas do Intune**.  

-   **Para a política do Exchange no local** - Configuration Manager em coleções de utilizadores. Pode configurá-los na área de trabalho **Ativos e Compatibilidade** .  

 Pode especificar dois tipos de grupos em cada política:  

-   **Grupos direcionados** -grupos de utilizadores ou coleções para os quais é aplicada a política  

-   **Grupos excluídos** -grupos de utilizadores ou as coleções que estão excluídas da política (opcional)  

 Se um utilizador estiver em ambos, estará excluído da política.  

 Apenas os grupos ou coleções direcionados pela política de acesso condicional são avaliados para acesso ao Exchange.  

### <a name="step-3-configure-and-deploy-a-compliance-policy"></a>Passo 3: Configure e implemente uma política de conformidade  
 Certifique-se de que criou e implementou uma política de conformidade em todos os dispositivos para os quais será direcionada a política de acesso condicional do Exchange.  

 Para obter detalhes sobre como configurar a política de conformidade, veja [Gerir políticas de conformidade no System Center Configuration Manager](device-compliance-policies.md).  

> [!IMPORTANT]  
>  Se não tiver implementado uma política de conformidade e, em seguida, ativar uma política de acesso condicional do Exchange, todos os dispositivos direcionados terão permissão de acesso.  

 Quando estiver pronto, avance para o **Passo 4**.  

### <a name="step-4-configure-the-conditional-access-policy"></a>Passo 4: Configurar a política de acesso condicional  

#### <a name="for-exchange-online-and-tenants-in-the-new-exchange-online-dedicated-environment"></a>Para o Exchange Online (e inquilinos no novo ambiente do Exchange Online Dedicado)

>[!NOTE]
>Também pode criar a política de acesso condicional na consola de gestão do Azure AD. Consola de gestão do Azure AD permite-lhe criar políticas de acesso condicional (referidas como a política de acesso condicional baseada no dispositivo no Azure AD), além de outras políticas de acesso condicional, como a autenticação multifator de dispositivo do Intune. Também pode configurar políticas de acesso condicional para aplicações de empresa de terceiros como Salesforce e suporta a caixa que o Azure AD. Para obter mais detalhes, consulte o artigo [como definir a política de acesso condicional baseada no dispositivo do Azure Active Directory para controlo de acesso ao Azure Active Directory ligado aplicações](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-policy-connected-applications/).

 As políticas de acesso condicional para o Exchange Online utilizam o fluxo seguinte para avaliar se os dispositivos devem ser permitidos ou bloqueados.  

 ![ConditionalAccess8&#45;1](media/ConditionalAccess8-1.png)  

 Para aceder ao e-mail, o dispositivo tem de:  

-   Inscrever-se com o Intune  

-   PCs têm de estar associados a um domínio ou a ser inscritos e em conformidade com as políticas definidas no Intune.  

-   Registar o dispositivo no Azure Active Directory (isto ocorre automaticamente quando o dispositivo é inscrito com o Intune.  

     Para um PC associado a um domínio, tem de defini-lo para [registar automaticamente o dispositivo](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/) no Azure Active Directory.  

-   Ter o e-mail ativado, que associa o ID do Exchange ActiveSync ao registo do dispositivo no Azure Active Directory (aplica-se a dispositivos iOS e Android apenas).  

-   Ser compatível com todas as políticas de conformidade implementadas  

 O estado do dispositivo é armazenado no Azure Active Directory, o qual concede ou bloqueia o acesso ao e-mail, com base nas condições avaliadas.  

 Se não for cumprida uma condição, será apresentada ao utilizador uma das duas mensagens seguintes quando iniciar sessão:  

-   Se o dispositivo não estiver inscrito ou registado no Azure Active Directory, será apresentada uma mensagem com instruções sobre como instalar a aplicação do portal da empresa e inscrevê-la  

-   Se o dispositivo não for conforme, será apresentada uma mensagem que direciona o utilizador para o site do Portal de empresa do Intune ou a aplicação de Portal da empresa onde é possível localizar informações sobre o problema e como resolvê-lo.  

-   Num PC:  

    -   Se a política estiver definida para exigir a associação a um domínio e o PC não estiver associado a qualquer domínio, será apresentada uma mensagem para contactar o administrador de TI.  

    -   Se a política estiver definida para exigir a associação a um domínio ou estar em conformidade, o PC não cumpre nenhum dos requisitos e será apresentada uma mensagem com instruções sobre como instalar o portal da empresa e inscrevê-lo.  

 A mensagem é apresentada no dispositivo para os utilizadores do Exchange Online e os inquilinos no novo ambiente do Exchange Online Dedicado e é enviada para a caixa de entrada de e-mail dos utilizadores do Exchange No Local e dos dispositivos legados do Exchange Online Dedicado.  

> [!NOTE]  
>  Substituição de regras de acesso condicional, o Configuration Manager permitem, bloqueiam e colocam em quarentena regras que são definidas na consola de administração do Exchange Online.  

> [!NOTE]  
>  A política de acesso condicional deve ser configurada na consola do Intune. Os seguintes passos começam por aceder à consola do Intune através do Configuration Manager. Se lhe for solicitado, inicie sessão com as mesmas credenciais que foram utilizadas para configurar o ponto de ligação do serviço entre o Configuration Manager e o Intune.  

##### <a name="to-enable-the-exchange-online-policy"></a>Para ativar a política do Exchange Online  

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  

2.  Expanda **Definições de Compatibilidade**, expanda **Acesso Condicional**e, em seguida, clique em **Exchange Online**.  

3.  No separador **Início** , no grupo **Ligações** , clique em **Configurar Política de Acesso Condicional na Consola do Intune**. Poderá ter de fornecer o nome de utilizador e palavra-passe da conta utilizada para ligar o Configuration Manager com qualquer administrador global para o serviço Intune.  

     Abre a consola de administração do Intune.  

4.  Na [consola de administração do Microsoft Intune](https://manage.microsoft.com), clique em **Política** > **Acesso Condicional** > **Política do Exchange Online**.  

     ![HybridOnlineSetupIntune](media/HybridOnlineSetupIntune.png)  

5.  Na página **Política do Exchange Online** , selecione **Ativar política de acesso condicional no Exchange Online**. Se selecionar esta opção, o dispositivo tem de estar em conformidade. Se não estiver selecionada, o acesso condicional não é aplicado.  

    > [!NOTE]  
    >  Se não tiver implementado uma política de conformidade e, em seguida, ativar a política do Exchange Online, todos os dispositivos direcionados serão comunicados como estando em conformidade.  
    >   
    >  Independentemente do Estado de conformidade, será exigido a todos os utilizadores direcionados pela política de inscrever os respetivos dispositivos com o Intune.  

6.  Em **Acesso da aplicação**, para o Outlook e outras aplicações com autenticação moderna, pode optar por restringir o acesso apenas a dispositivos em conformidade com cada plataforma.  Os dispositivos Windows têm de estar associados a um domínio ou inscritos no Intune e em conformidade.  

    > [!TIP]  
    >  A **Autenticação moderna** fornece um início de sessão baseado na ADAL (Active Directory Authentication Library) aos clientes do Office.  
    >   
    >  -   A autenticação baseada na ADAL permite que os clientes do Office participem na autenticação baseada no browser (também conhecido como autenticação passiva).  Para autenticar, o utilizador é direcionado para uma página Web de início de sessão.  
    > -   Este novo método de início de sessão permite novos cenários, como o acesso condicional, com base na **conformidade do dispositivo** e no facto de a **autenticação multifator** ter sido ou não executada.  
    >   
    >  Este [artigo](https://support.office.com/en-US/article/How-modern-authentication-works-for-Office-2013-and-Office-2016-client-apps-e4c45989-4b1a-462e-a81b-2a13191cf517) tem informações mais detalhadas sobre como funciona a autenticação moderna.  

     Utilizar o Exchange Online com o Configuration Manager e o Intune não só pode gerir dispositivos móveis com acesso condicional, mas também com computadores de secretária. Os PCs têm de estar associados a um domínio ou inscritos no Intune e em conformidade. Pode definir os seguintes requisitos:  

    -   **Os dispositivos têm de estar associados a um domínio ou em conformidade.** Os PC têm de estar associados a um domínio ou em conformidade com as políticas. Se o PC não cumprir nenhum destes requisitos, solicitadas ao utilizador para inscrever o dispositivo no Intune.  

    -   **Os dispositivos têm de estar associados a um domínio.** Os PC têm de estar associados a um domínio para acederem ao Exchange Online. Se o PC não estiver associado a um domínio, o acesso ao e-mail é bloqueado e é pedido ao utilizador para contactar o administrador de TI.  

    -   **Os dispositivos têm de estar em conformidade.** PCs têm de estar inscritos no Intune e em conformidade. Se um PC não estiver inscrito, será apresentada uma mensagem com instruções sobre como inscrevê-lo.  

7.  Em **acesso web do Outlook (OWA)**, pode optar por permitir acesso ao Exchange Online apenas através de browsers suportados: Safari (iOS) e no Chrome (Android). O acesso a partir de outros browsers será bloqueado. As mesmas restrições de plataforma que selecionou para Acesso da aplicação para o Outlook também se aplicam aqui.

    Em dispositivos **Android** , os utilizadores têm de ativar o acesso ao browser.  Para efetuar esta ação do utilizador final tem de ativar a opção "Ativar o acesso ao Browser" nos dispositivos da seguinte forma:
     1. Inicie a **aplicação Portal da Empresa**.
     2. Aceda ao **definições** página a partir de pontos triplo (…) ou o botão do menu de hardware.
      3.    Prima o botão **Ativar acesso ao browser** .
      4.    No browser Chrome, termine sessão no Office 365 e reinicie o Chrome.

     Nas plataformas **iOS e Android** , para identificar o dispositivo que é utilizado para aceder ao serviço, o Azure Active Directory emitirá um certificado Transport Layer Security (TLS) para o dispositivo.  O dispositivo apresenta o certificado com uma linha de comandos ao utilizador final para selecionar o certificado, tal como mostram as capturas de ecrã abaixo. O utilizador final tem de selecionar este certificado para poder continuar a utilizar o browser.

     **iOS**

     ![captura de ecrã da linha de comandos do certificado num ipad](media/mdm-browser-ca-ios-cert-prompt_v2.png)

    **Android**

    ![captura de ecrã da linha de comandos do certificado num dispositivo Android](media/mdm-browser-ca-android-cert-prompt.png)

7.  Em**aplicações de correio do Exchange ActiveSync**, pode optar por bloquear o acesso do e-mail ao Exchange Online se o dispositivo não estiver em conformidade e selecionar se pretende permitir ou bloquear o acesso ao e-mail quando não for possível ao Intune gerir o dispositivo.  

8.  Em **Grupos Visados**, selecione os grupos de segurança do Active Directory dos utilizadores aos quais será aplicada a política.  

    > [!NOTE]  
    >  Para utilizadores que estão nos grupos de Destino, as políticas do Intune irão substituir as regras e as políticas do Exchange.  
    >   
    >  O Exchange só irá impor permissões, bloqueios, regras de quarentena e políticas do Exchange se:  
    >   
    >  -   O utilizador não estiver licenciado para o Intune.  
    > -   O utilizador estiver licenciado para o Intune, mas não pertencer a quaisquer grupos de segurança direcionados na política de acesso condicional.  

9. Em **Grupos Excluídos**, selecione os grupos de segurança do Active Directory dos utilizadores que estão excluídos desta política. Se um utilizador estiver em ambos os grupos, estará excluído da política e terá acesso ao respetivo e-mail.  

10. Quando terminar, clique em **Guardar**.  

-   Não tem de implementar a política de acesso condicional, pois esta entra em vigor imediatamente.  

-   Depois de um utilizador criar uma conta de e-mail, o dispositivo é bloqueado de imediato.  

-   Se um utilizador bloqueado inscreve o dispositivo no Intune (ou corrigir a não conformidade), acesso ao e-mail é desbloqueado em dois minutos.  

-   Se o utilizador anular a inscrição do respetivo dispositivo, o e-mail é bloqueado após aproximadamente 6 horas.  

### <a name="for-exchange-on-premises-and-tenants-in-the-legacy-exchange-online-dedicated-environment"></a>Para o Exchange no local (e inquilinos no ambiente legado do Exchange Online Dedicado)  
 As políticas de acesso condicional para o Exchange no local e os inquilinos no ambiente legado do Exchange Online Dedicado utilizam o fluxo seguinte para avaliar se os dispositivos devem ser permitidos ou bloqueados.  

 ![ConditionalAccess8&#45;2](media/ConditionalAccess8-2.png)  

##### <a name="to-enable-the-exchange-on-premises-policy"></a>Para ativar a política do Exchange No Local  

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  

2.  Expanda **Definições de Compatibilidade**, expanda **Acesso Condicional**e, em seguida, clique em **Exchange no Local**.  

3.  No separador **Home Page** , no grupo **Exchange no Local** , clique em **Configurar Política de Acesso Condicional**.  

4.  **A partir da versão 1602 do Configuration Manager**, na página **Geral** do **Assistente para Configurar Política de Acesso Condicional**, especifique se pretende substituir a regra predefinida do Exchange Active Sync. Clique nesta opção se pretender que os dispositivos inscritos e compatíveis tenham sempre acesso ao e-mail, mesmo quando a regra predefinida está definida para colocar em quarentena ou bloquear o acesso.  

    > [!NOTE]  
    >  Ocorreu um problema com a substituição predefinida de dispositivos Android. Se a regra de acesso predefinida do Exchange Server estiver definida como **Bloquear** e a política de acesso condicional do Exchange estiver ativada com a opção de substituição de regras predefinida, os dispositivos Android dos utilizadores visados podem não ficar desbloqueados, mesmo depois de os dispositivos estarem inscritos no Intune e estarem em conformidade.  Para resolver este problema, defina a regra de acesso predefinida do Exchange como **Quarentena**. O dispositivo não consegue aceder ao Exchange por predefinição e o administrador pode obter um relatório do servidor do Exchange na lista dos dispositivos que estão a ser colocados em quarentena.  

     Se não tiver configurado uma conta de e-mail de notificação quando configurar o Exchange Connector, será apresentado um aviso nesta página e o botão **Seguinte** é desativado.  Para poder continuar, tem primeiro de configurar as definições de e-mail de notificação no Exchange Connector e, em seguida, voltar ao **Assistente para Configurar Política de Acesso Condicional** para concluir o processo.  

     ![HybridCondAccessWiz1](media/HybridCondAccessWiz1.PNG)  

     Clique em **Seguinte**.  

5.  Na página **Coleções Direcionadas** , adicione uma ou mais coleções de utilizadores. Para aceder ao Exchange, os utilizadores nestas coleções tem de inscrever os respetivos dispositivos com o Intune e também estar em conformidade com as políticas de conformidade implementadas.  

     ![HybridCondAccessWiz2](media/HybridCondAccessWiz2.PNG)  

     Clique em **Seguinte**.  

6.  Na página **Coleções Isentas** , adicione as coleções de utilizadores que pretende isentar da política de acesso condicional. Utilizadores estes grupos, não precisa de inscrever os respetivos dispositivos com o Intune não precisam de estar em conformidade com as políticas de conformidade implementadas para aceder ao Exchange.  

     ![HybridCondAccessWiz3](media/HybridCondAccessWiz3.png)  

     Se um utilizador aparecer em ambos os grupos, estará excluído da política de acesso condicional.  

     Clique em **Seguinte**.  

7.  No **notificação do utilizador editar** página, configure o e-mail que o Intune envia aos utilizadores com instruções sobre como desbloquear o dispositivo (além de mensagem de correio eletrónico enviada pelo Exchange).  

     Pode editar a mensagem predefinida e utilizar tags de HTML para formatar a apresentação do texto. Também pode enviar uma mensagem de e-mail antecipadamente aos seus funcionários para notificá-los sobre alterações futuras e fornecer-lhes instruções sobre como inscrever os respetivos dispositivos.  

     ![HybridCondAccessWiz4](media/HybridCondAccessWiz4.PNG)  

    > [!NOTE]  
    >  Como o e-mail de notificação do Intune com as instruções de correção é enviado para a caixa de correio do Exchange do utilizador, no caso do dispositivo do utilizador ficar bloqueado antes de receber a mensagem de correio eletrónico, estes podem utilizar um dispositivo desbloqueado ou outro método para aceder ao Exchange e ver a mensagem.  

    > [!NOTE]  
    >  Para o Exchange poder enviar o e-mail de notificação, tem de configurar a conta que será utilizada para enviá-lo. Pode efetuar esta ação quando configurar as propriedades do conector do Exchange Server.  
    >   
    >  Para obter detalhes, veja [Gerir dispositivos móveis com o System Center Configuration Manager e o Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

     Clique em **Seguinte**.  

8.  Na página  **Resumo** , verifique as definições e, em seguida, feche o assistente.  

-   Não tem de implementar a política de acesso condicional, pois esta entra em vigor imediatamente.  

-   Depois de um utilizador configura um perfil do Exchange ActiveSync, pode demorar entre 1 a 3 horas até o dispositivo ser bloqueado (se não for gerido pelo Intune).  

-   Se um utilizador bloqueado, em seguida, inscreve o dispositivo no Intune (ou corrigir a não conformidade), acesso ao e-mail será desbloqueado em dois minutos.  

-   Se o utilizador anular-inscrição do Intune, pode demorar entre 1 a 3 horas até o dispositivo ser bloqueado.  

### <a name="see-also"></a>Consulte também  
 [Gerir o acesso aos serviços no System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md)
