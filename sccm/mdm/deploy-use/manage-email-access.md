---
title: Gerir o acesso ao e-mail
titleSuffix: Configuration Manager
description: Saiba como utilizar o acesso condicional do Configuration Manager para gerir o acesso ao e-mail do Exchange.
ms.date: 03/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: fa648e73-5fb8-4818-ab57-7466ffaf888e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2ee4ed8f102507b4d62a1ccbfe1cc38240e85df9
ms.sourcegitcommit: f38ef9afb0c608c0153230ff819e5f5e0fb1520c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/19/2019
ms.locfileid: "58196862"
---
# <a name="manage-email-access-in-configuration-manager"></a>Gerir o acesso ao e-mail no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize o Gestor de configuração, acesso condicional para gerir o acesso ao e-mail do Exchange com base nas condições que especificar.  

Pode gerir o acesso ao:  

- Microsoft Exchange No Local  

- Microsoft Exchange Online  

- Exchange Online Dedicado  

Pode controlar o acesso ao Exchange Online e ao Exchange No Local a partir do cliente de e-mail incorporado nas seguintes plataformas:  

- Android 4.0 e posterior, Samsung KNOX Standard 4.0 e posterior  

- iOS 9.0 e posterior  

- Windows Phone 8.1 e posterior  

- Aplicação de correio no Windows 8.1 e posterior  

Aplicativos de área de trabalho do Office podem acessar o Exchange Online em PCs com o:  

- Ambiente de trabalho do Office 2013 e versões posteriores com [autenticação moderna](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a) ativada.  

- Windows 7.0 ou Windows 8.1  

> [!NOTE]  
> PCs devem ser associado a um domínio ou estar em conformidade com as políticas definidas no Intune.  


## <a name="device-requirements"></a>Requisitos de dispositivos
Se configurar o acesso condicional, antes de um utilizador se poder ligar ao respetivo e-mail, o dispositivo que ele utiliza deve:  

- Estar inscrito no Intune ou o PC associado a um domínio.  

- Registar o dispositivo no Azure Active Directory (isto ocorre automaticamente quando o dispositivo é inscrito no Intune (apenas para o Exchange Online). Além disso, o ID do Exchange ActiveSync cliente tem de estar registado no Azure Active Directory (não se aplica a dispositivos Windows e Windows Phone que se liguem ao Exchange No Local).  

    Para um PC associado a um domínio, tem de defini-lo para ser registado automaticamente no Azure Active Directory. O **acesso condicional para PCs** secção a [gerir o acesso aos serviços](../../protect/deploy-use/manage-access-to-services.md) artigo lista o conjunto completo de requisitos para ativar o acesso condicional para PCs.  

- Estar em conformidade com as políticas de conformidade do Configuration Manager implementadas nesse dispositivo  

    Se não for cumprida uma condição de acesso condicional, o utilizador é apresentado uma das duas mensagens seguintes quando iniciar sessão:  

- Se o dispositivo não estiver inscrito no Intune ou não estiver registado no Azure Active Directory, é apresentada uma mensagem com instruções sobre como instalar a aplicação do portal da empresa, inscrever o dispositivo e (para dispositivos Android e iOS), ativar o e-mail, que associa o ID de ActiveSync do Exchange do dispositivo com o registo do dispositivo no Azure Active Directory.  

- Se o dispositivo não estiver em conformidade, é apresentada uma mensagem que direciona o utilizador para o portal web do Intune onde pode encontrar informações sobre o problema e como resolvê-lo.  

#### <a name="for-mobile-devices"></a>Para dispositivos móveis

Pode restringir o acesso ao **Outlook Web Access (OWA)** no Exchange Online quando o acesso for feito a partir de um browser em dispositivos **iOS** e **Android** . O acesso só será permitido a partir de browsers suportados em dispositivos em conformidade:  

- Safari (iOS)  
- Chrome (Android)  
- Managed Browser (iOS e Android)  

Os browsers não suportados serão bloqueados. As aplicações do OWA para iOS e Android não são suportadas. Devem ser bloqueadas através de regras de afirmações do ADFS:  

- Configure regras de afirmações do ADFS para bloquear protocolos de autenticação não moderna. São fornecidas instruções detalhadas no cenário 3 para [bloquear todo o acesso ao Office 365, exceto aplicações baseadas no browser](https://technet.microsoft.com/library/dn592182.aspx).  

#### <a name="for-pcs"></a>Para PCs

- Se o requisito de política de acesso condicional permitir a **associação a um domínio** ou a **conformidade**, será apresentada uma mensagem com instruções sobre como inscrever o dispositivo. Se o PC não cumprir nenhum dos requisitos, será pedido ao utilizador para inscrever o dispositivo com o Intune.  

- Se o requisito da política de acesso condicional estiver definido para permitir apenas dispositivos Windows associados a um domínio, o dispositivo será bloqueado e será apresentada uma mensagem para contactar o administrador de TI.  

Pode bloquear o acesso ao e-mail do Exchange no cliente de e-mail Exchange ActiveSync incorporado no dispositivo nas seguintes plataformas:  

- Android 4.0 e posterior, Samsung KNOX Standard 4.0 e posterior  

- iOS 9.0 e posterior  

- Windows Phone 8.1 e posterior  

- A aplicação **Correio** no Windows 8.1 e posterior  

A aplicação Outlook para iOS e Android e o Outlook desktop 2013 e versões posteriores é suportada para apenas Exchange Online.  

O **conector do Exchange no local** entre o Configuration Manager e o Exchange é necessário para o acesso condicional funcionar.  

Pode configurar uma política de acesso condicional para o Exchange no local a partir da consola do Configuration Manager. Ao configurar uma política de acesso condicional para o Exchange Online, pode iniciar o processo na consola do Configuration Manager, que inicia a consola do Intune, onde poderá concluir o processo.  



## <a name="configure-conditional-access"></a>Configurar o acesso condicional

### <a name="step-1-evaluate-the-effect-of-the-conditional-access-policy"></a>Passo 1: Avaliar o efeito da política de acesso condicional  

Depois de ter configurado o **conector do Exchange no local**, pode utilizar o Gestor de configuração **lista de dispositivos por Estado de acesso condicional** relatório para identificar dispositivos que serão impedidos de aceder ao Exchange após configurar a política de acesso condicional. Este relatório também requer:  

- Uma subscrição do Intune  

- O ponto de ligação de serviço deve ser configurado e implementado  

Nos parâmetros do relatório, selecione o grupo do Intune que pretende avaliar e, se necessário, as plataformas de dispositivos aos quais será aplicada a política.  

Para obter mais informações sobre como executar relatórios, consulte [relatórios no Configuration Manager](/sccm/core/servers/manage/reporting).  

Depois de executar o relatório, examine estas quatro colunas para determinar se um utilizador será bloqueado:  

- **Canal de gestão**: O dispositivo é gerido pelo Intune, o Exchange ActiveSync ou ambos.  

- **Registado com AAD**: O dispositivo está registado no Azure Active Directory (conhecido como associação à área de trabalho).  

- **Em conformidade**: O dispositivo está em conformidade com as políticas de conformidade implementadas.  

- **EAS ativado**: dispositivos iOS e Android têm de ter o ID do Exchange ActiveSync associado ao registo do dispositivo no Azure Active Directory. Isto acontece quando o utilizador clica na ligação **Ativar E-mail** no e-mail de quarentena.  

    > [!NOTE]  
    > Os dispositivos Windows Phone apresentam sempre um valor nesta coluna.  

Os dispositivos que fazem parte de uma coleção ou grupo de destino serão impedidos de aceder ao Exchange, exceto se os valores da coluna corresponderem aos listados na seguinte tabela:  

|Canal de Gestão|Registado no AAD|conformidade|EAS Ativado|Ação resultante|  
|------------------------|--------------------|---------------|-------------------|----------------------|  
|**Gerido pelo Microsoft Intune e pelo Exchange ActiveSync**|Sim|Sim|É apresentado**Sim** ou **Não** |Acesso ao e-mail permitido|  
|Qualquer outro valor|Não|Não|Não é apresentado nenhum valor|Acesso ao e-mail bloqueado|  

Pode exportar os conteúdos do relatório e utilizar a coluna **Endereço de E-mail** para ajudar a informar os utilizadores de que serão bloqueados.  


### <a name="step-2-configure-user-groups-or-collections-for-the-conditional-access-policy"></a>Passo 2: Configurar grupos de utilizadores ou de coleções para a política de acesso condicional  

O direcionamento de políticas de acesso condicional para diferentes coleções ou grupos de utilizadores depende dos tipos de políticas. Estes grupos contêm os utilizadores que serão direcionados ou que estarão excluídos da política. Quando um utilizador é direcionado por uma política, cada dispositivo que utiliza tem de estar em conformidade para poder aceder ao e-mail.  

- **Para a política do Exchange Online**: a grupos de utilizadores de segurança do Azure Active Directory. Pode configurar estes grupos no **Centro de administração do Microsoft 365**, ou o **portal de contas do Intune**.  

- **Para a política do Exchange no local**: para coleções de utilizadores do Configuration Manager. Pode configurá-los na área de trabalho **Ativos e Compatibilidade** .  

Pode especificar dois tipos de grupos em cada política:  

- **Grupos visados**: Grupos de utilizadores ou coleções para os quais é aplicada a política  

- **Grupos excluídos**: Grupos de utilizadores ou de coleções que são excluídas da política (opcional)  

Se um utilizador estiver em ambos, estará excluído da política.  

Apenas os grupos ou coleções direcionados pela política de acesso condicional são avaliados para acesso ao Exchange.  


### <a name="step-3-configure-and-deploy-a-compliance-policy"></a>Passo 3: Configurar e implementar uma política de conformidade  

Certifique-se de que criou e implementou uma política de conformidade em todos os dispositivos para os quais será direcionada a política de acesso condicional do Exchange.  

Para obter detalhes sobre como configurar a política de conformidade, consulte [gerir políticas de conformidade do dispositivo](device-compliance-policies.md).  

> [!IMPORTANT]  
> Se não tiver implementado uma política de conformidade e, em seguida, ativar uma política de acesso condicional do Exchange, todos os dispositivos direcionados terão permissão de acesso.  


### <a name="step-4-configure-the-conditional-access-policy"></a>Passo 4: Configurar a política de acesso condicional  

#### <a name="for-exchange-online-and-tenants-in-the-new-exchange-online-dedicated-environment"></a>Para o Exchange Online (e inquilinos no novo ambiente do Exchange Online Dedicado)

> [!NOTE]  
> Também pode criar a política de acesso condicional na consola de gestão do Azure AD. Consola de gestão do Azure AD permite-lhe criar políticas de acesso condicional (referidas como política de acesso condicional com base no dispositivo no Azure AD), além de outras políticas de acesso condicional, como a autenticação multifator do dispositivo do Intune. Também pode definir políticas de acesso condicional para aplicações empresariais de terceiros como o Salesforce e oferece suporte a caixa de que o Azure AD. Para obter mais detalhes, consulte [como: Exigir que os dispositivos geridos para aceder à aplicação de cloud com o acesso condicional](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices).  

As políticas de acesso condicional para o Exchange Online utilizam o fluxo seguinte para avaliar se os dispositivos devem ser permitidos ou bloqueados.  

![Fluxo de acesso condicional](media/ConditionalAccess8-1.png)  

Para aceder ao e-mail, o dispositivo tem de:  

- Inscrever com o Intune  

- PCs terá de ser associado a um domínio ou ser inscritos e em conformidade com as políticas definidas no Intune  

- Registe o dispositivo no Azure AD. Isto ocorre automaticamente quando o dispositivo é inscrito no Intune. Para PCs associados a um domínio, tem de configurá-lo até [registar automaticamente o dispositivo](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-manual-steps) com o Azure AD.  

- Ter o e-mail, que associa o ID do dispositivo do Exchange ActiveSync ao registo do dispositivo no Azure Active Directory (aplica-se a dispositivos iOS e Android apenas) ativado.  

- Ser compatível com todas as políticas de conformidade implementadas  

O estado do dispositivo é armazenado no Azure Active Directory, o qual concede ou bloqueia o acesso ao e-mail, com base nas condições avaliadas.  

Se não for cumprida uma condição, o utilizador é apresentado uma das duas mensagens seguintes quando iniciar sessão:  

- Se o dispositivo não estiver inscrito ou registado no Azure AD, é apresentada uma mensagem com instruções sobre como instalar a aplicação do portal da empresa e inscrevê-lo  

- Se o dispositivo não estiver em conformidade, é apresentada uma mensagem que direciona o utilizador para o site de Portal da empresa do Intune ou a aplicação Portal da empresa, onde poderá encontrar informações sobre o problema e como resolvê-lo.  

- Num PC:  

    - Se a política estiver definida para exigir a associação de domínio e o PC não estiver associado a um domínio, será apresentada uma mensagem para contactar o administrador de TI.  

    - Se a política estiver definida para exigir a associação de domínio ou em conformidade e o PC não cumprir nenhum dos requisitos, é apresentada uma mensagem com instruções sobre como instalar a aplicação do portal da empresa e inscrevê-lo.  

A mensagem é apresentada no dispositivo para os utilizadores do Exchange Online e os inquilinos no novo ambiente do Exchange Online Dedicado e é enviada para a caixa de entrada de e-mail dos utilizadores do Exchange No Local e dos dispositivos legados do Exchange Online Dedicado.  

> [!NOTE]  
> Substituem regras de acesso condicional, o Configuration Manager permitem, bloqueiam e colocar em quarentena regras que são definidas na consola de administração do Exchange Online.  
> 
> A política de acesso condicional deve ser configurada na consola do Intune. Os seguintes passos começam por aceder à consola do Intune através do Configuration Manager. Se lhe for pedido, inicie sessão com as mesmas credenciais que foram utilizadas para configurar o ponto de ligação entre o Configuration Manager e o Intune.  

##### <a name="to-enable-the-exchange-online-policy"></a>Para ativar a política do Exchange Online  

1. Na consola do Configuration Manager, selecione **ativos e compatibilidade**.  

2. Expanda **definições de compatibilidade**, expanda **acesso condicional**e, em seguida, selecione **Exchange Online**.  

3. Sobre o **home page** separador a **Links** grupo, selecione **configurar política de acesso condicional na consola do Intune**. Poderá ter de fornecer o nome de utilizador e palavra-passe da conta utilizada para ligar o Configuration Manager com qualquer administrador global para o serviço do Intune. Abre a consola de administração do Intune.  

4. No portal do Microsoft Intune, selecione **diretiva** > **acesso condicional** > **política do Exchange Online**.  

    ![HybridOnlineSetupIntune](media/HybridOnlineSetupIntune.png)  

5. Na página **Política do Exchange Online** , selecione **Ativar política de acesso condicional no Exchange Online**. Se selecionar esta opção, o dispositivo tem de estar em conformidade. Se isso não é a opção estiver marcado, em seguida, acesso condicional não é aplicado.  

    > [!NOTE]  
    > Se não tiver implementado uma política de conformidade e, em seguida, ativar a política do Exchange Online, todos os dispositivos visados são comunicados como estando em conformidade.  
   >   
   >  Independentemente do Estado de conformidade, todos os utilizadores visados pela política terão a ter de inscrever os respetivos dispositivos com o Intune.  

6. Sob **acesso a aplicações**, para o Outlook e outras aplicações que utilizam autenticação moderna, pode optar por restringir o acesso apenas a dispositivos que estão em conformidade com cada plataforma. Os dispositivos Windows têm de estar associados a um domínio ou inscritos no Intune e em conformidade.  

    > [!TIP]  
    > A **Autenticação moderna** fornece um início de sessão baseado na ADAL (Active Directory Authentication Library) aos clientes do Office.  
    > 
    > - A autenticação baseada na ADAL permite que os clientes do Office participem na autenticação baseada no browser (também conhecido como autenticação passiva). Para autenticar, o utilizador é direcionado para uma página Web de início de sessão.  
    > - Este novo método de início de sessão permite novos cenários, como o acesso condicional, com base na **conformidade do dispositivo** e no facto de a **autenticação multifator** ter sido ou não executada.  
    > 
    >  Para obter mais informações, consulte [como a autenticação moderna funciona para aplicações de cliente do Office 2013 e Office 2016](https://docs.microsoft.com/office365/enterprise/modern-auth-for-office-2013-and-2016).  

    Utilizar o Exchange Online com o Configuration Manager e o Intune não só pode gerir dispositivos móveis com acesso condicional, mas também com computadores de secretária. PCs devem estar associado a um domínio, ou ser inscritos no Intune e em conformidade. Pode definir os seguintes requisitos:  

    - **Os dispositivos têm de estar associados a um domínio ou em conformidade.** Os PCs estejam associados a um domínio ou em conformidade com as políticas. Se um PC não cumprir nenhum destes requisitos, é pedido ao utilizador para inscrever o dispositivo com o Intune.  

    - **Os dispositivos têm de estar associados a um domínio.** PCs têm de ser associado a um domínio para aceder ao Exchange Online. Se um PC não estiver associado a um domínio, o acesso ao e-mail é bloqueado e é pedido ao utilizador que contacte o administrador de TI.  

    - **Os dispositivos têm de estar em conformidade.** PCs têm de estar inscritos no Intune e em conformidade. Se um PC não estiver inscrito, será apresentada uma mensagem com instruções sobre como inscrever.  

7. Sob **OWA (OWA)**, pode optar por permitir acesso ao Exchange Online apenas através de browsers suportados: Safari (iOS) e o Chrome (Android). O acesso a partir de outros browsers será bloqueado. As mesmas restrições de plataforma que selecionou para Acesso da aplicação para o Outlook também se aplicam aqui.  

    - Em dispositivos **Android** , os utilizadores têm de ativar o acesso ao browser. Para efetuar esta ação, o utilizador tem de ativar a opção "Ativar o acesso ao Browser" no dispositivo inscrito da seguinte forma:  

        1. Inicie a **aplicação Portal da Empresa**.  

        2. Aceda à página **Definições** a partir das reticências (…) ou do botão do menu de hardware.  

        3. Prima o botão **Ativar o Acesso ao Browser**.  

        4. No browser Chrome, termine sessão no Office 365 e reinicie o Chrome.  

    - No **iOS e Android** plataformas, para identificar o dispositivo que é utilizado para aceder ao serviço, do Azure AD irão emitir um certificado TLS para o dispositivo. O dispositivo apresenta o certificado com uma linha de comandos para o utilizador selecionar o certificado, conforme mostrado nas capturas de ecrã abaixo. O utilizador tem de selecionar este certificado para poder continuar a utilizar o browser.  

        - **iOS**  

        ![captura de ecrã da linha de comandos do certificado num ipad](media/mdm-browser-ca-ios-cert-prompt_v2.png)  

        - **Android**  

        ![captura de ecrã da linha de comandos do certificado num dispositivo Android](media/mdm-browser-ca-android-cert-prompt.png)  

8. Em**aplicações de correio do Exchange ActiveSync**, pode optar por bloquear o acesso do e-mail ao Exchange Online se o dispositivo não estiver em conformidade e selecionar se pretende permitir ou bloquear o acesso ao e-mail quando não for possível ao Intune gerir o dispositivo.  

9. Em **Grupos Visados**, selecione os grupos de segurança do Active Directory dos utilizadores aos quais será aplicada a política.  

    > [!NOTE]  
    > Para os utilizadores que estão nos grupos direcionados, a políticas do Intune irão substituir as regras do Exchange e as políticas.  
    > 
    > O Exchange só irá impor permissões, bloqueios, regras de quarentena e políticas do Exchange se:  
    > 
    > - O utilizador não estiver licenciado para o Intune.  
    > - O utilizador está licenciado para o Intune, mas não pertencer a quaisquer grupos de segurança direcionados na política de acesso condicional.  

10. Em **Grupos Excluídos**, selecione os grupos de segurança do Active Directory dos utilizadores que estão excluídos desta política. Se um utilizador estiver em ambos os grupos visados e excluídos, eles serão excluídos da política e terão acesso ao respetivo e-mail.  

11. Quando terminar, clique em **Guardar**.  


Reveja as seguintes notas sobre esta política:  

- Não é necessário implementar a política de acesso condicional; ele entra em vigor imediatamente.  

- Depois de um utilizador criar uma conta de e-mail, o dispositivo é bloqueado de imediato.  

- Se um utilizador bloqueado inscreve o dispositivo no Intune (ou corrige a não conformidade), acesso ao e-mail é desbloqueado em dois minutos.  

- Se o utilizador anular a inscrição do respetivo dispositivo, o e-mail é bloqueado após aproximadamente 6 horas.  


### <a name="for-exchange-on-premises-and-tenants-in-the-legacy-exchange-online-dedicated-environment"></a>Para o Exchange no local (e inquilinos no ambiente legado do Exchange Online Dedicado)  
As políticas de acesso condicional para o Exchange no local e os inquilinos no ambiente legado do Exchange Online Dedicado utilizam o fluxo seguinte para avaliar se os dispositivos devem ser permitidos ou bloqueados.  

![ConditionalAccess8&#45;2](media/ConditionalAccess8-2.png)  

#### <a name="to-enable-the-exchange-on-premises-policy"></a>Para ativar a política do Exchange No Local  

1. Na consola do Configuration Manager, selecione **ativos e compatibilidade**.  

2. Expanda **definições de compatibilidade**, expanda **acesso condicional**e, em seguida, selecione **Exchange no local**.  

3. Sobre o **home page** separador a **Exchange no local** grupo, selecione **configurar política de acesso condicional**.  

4. Na **gerais** página do **configurar Assistente de política de acesso condicional**, especifique se pretende substituir a regra predefinida do Exchange Active Sync. Selecione esta opção se desejar inscritos e aceder a dispositivos em conformidade tenham sempre acesso ao e-mail, mesmo quando a regra predefinida está definida para colocar em quarentena ou bloquear.  

    > [!NOTE]  
    > Existe um problema com a substituição predefinida de dispositivos Android. Se a regra de acesso predefinida do Exchange Server estiver definida como **Bloquear** e a política de acesso condicional do Exchange estiver ativada com a opção de substituição de regras predefinida, os dispositivos Android dos utilizadores visados podem não ficar desbloqueados, mesmo depois de os dispositivos estarem inscritos no Intune e estarem em conformidade. Para resolver este problema, defina a regra de acesso predefinida do Exchange como **Quarentena**. O dispositivo não obter acesso ao Exchange por predefinição e o administrador pode obter um relatório do servidor do Exchange na lista de dispositivos que estão a ser colocados em quarentena.  

    Se ainda não o programa de configuração uma conta de e-mail de notificação quando configurar o conector do Exchange, verá um aviso nesta página e o **seguinte** botão está desativado.  Para poder continuar, tem primeiro de configurar as definições de e-mail de notificação no Exchange Connector e, em seguida, voltar ao **Assistente para Configurar Política de Acesso Condicional** para concluir o processo.  

     ![HybridCondAccessWiz1](media/HybridCondAccessWiz1.PNG)  

5. Na página **Coleções Direcionadas** , adicione uma ou mais coleções de utilizadores. Para aceder ao Exchange, os utilizadores nestas coleções tem de inscrever os respetivos dispositivos com o Intune e estar em conformidade com as políticas de conformidade implementadas.  

     ![HybridCondAccessWiz2](media/HybridCondAccessWiz2.PNG)  

6. Na página **Coleções Isentas** , adicione as coleções de utilizadores que pretende isentar da política de acesso condicional. Os utilizadores nestes grupos, não tem de inscrever os respetivos dispositivos com o Intune e precisa de estar em conformidade com as políticas de conformidade implementadas para aceder ao Exchange.  

     ![HybridCondAccessWiz3](media/HybridCondAccessWiz3.png)  

    Se um utilizador aparecer em ambos os grupos, estará excluído da política de acesso condicional.  

7. Sobre o **editar notificação do utilizador** página, configure o e-mail que o Intune envia com instruções sobre como desbloquear o dispositivo (para além do e-mail que o Exchange envia).  

    Pode editar a mensagem predefinida e utilizar tags de HTML para formatar a apresentação do texto. Também pode enviar uma mensagem de e-mail antecipadamente aos seus funcionários para notificá-los sobre alterações futuras e fornecer-lhes instruções sobre como inscrever os respetivos dispositivos.  

     ![HybridCondAccessWiz4](media/HybridCondAccessWiz4.PNG)  

    > [!NOTE]  
    > Como o e-mail de notificação do Intune com as instruções de correção é entregue à caixa de correio do Exchange do utilizador, no caso do dispositivo do utilizador ficar bloqueado antes de receber a mensagem de e-mail, este pode utilizar um dispositivo desbloqueado ou outro método para aceder a O Exchange e ver a mensagem.  
    > 
    > Por ordem para a troca de enviar o e-mail de notificação, configure a conta que será utilizada para enviar o e-mail de notificação. Pode efetuar esta ação quando configurar as propriedades do conector do Exchange Server.  
    >   
    > Para obter mais informações, consulte [gerir dispositivos móveis com o Configuration Manager e o Exchange](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).  

8. Sobre o **resumo** página, reveja as definições e, em seguida, conclua o assistente.  


Reveja as seguintes notas sobre esta política:  

- Não é necessário implementar a política de acesso condicional, pois esta entra em vigor imediatamente.  

- Depois de um utilizador configurar um perfil do Exchange ActiveSync, poderá demorar um a três horas para que o dispositivo ser bloqueado (se não for gerido pelo Intune).  

- Se um utilizador bloqueado, em seguida, inscreve o dispositivo no Intune (ou corrige a não conformidade), acesso ao e-mail será desbloqueado em dois minutos.  

- Se o utilizador anular-é inscrito no Intune, pode demorar um a três horas para o dispositivo ser bloqueado.  


## <a name="see-also"></a>Consulte também  

[Gerir o acesso aos serviços](/sccm/protect/deploy-use/manage-access-to-services)
