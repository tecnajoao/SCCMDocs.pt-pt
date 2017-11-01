---
title: Acesso condicional
titleSuffix: Configuration Manager
description: "Saiba como utilizar o acesso condicional no System Center Configuration Manager para ajudar a proteger o e-mail e outros serviços."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b04727b-d563-422f-8d59-4dd66215d0b3
caps.latest.revision: "26"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 4a14f18007524421058c6caf1ec8947cf34328e4
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="manage-access-to-services-in-system-center-configuration-manager"></a>Gerir o acesso a serviços no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


## <a name="conditional-access-in-system-center-configuration-manager"></a>Acesso condicional no System Center Configuration Manager
Utilize **acesso condicional** para ajudar a proteger o e-mail e outros serviços em dispositivos que estão inscritos no Microsoft Intune, dependendo das condições que especifica.  

 Para obter informações sobre **acesso condicional em PCs geridos com o System Center Configuration Manager** e avaliados em termos de compatibilidade, consulte [gerir o acesso aos serviços do O365 para PCs geridos pelo System Center Configuration Manager](../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md).  


 Um fluxo típico de acesso condicional poderá ter o seguinte aspeto:  

 ![ConditionalAccess4](media/ConditionalAccess4.png)  

 Utilize o acesso condicional para gerir o acesso aos seguintes serviços:  

-   Microsoft Exchange No Local  

-   Microsoft Exchange Online  

-   Exchange Online Dedicado  

-   SharePoint Online  

-   Skype para Empresas Online

-   Dynamics CRM Online

 Para implementar o acesso condicional, configure dois tipos de políticas no Configuration Manager:  

-   As**políticas de conformidade** são políticas opcionais que pode implementar nas coleções de utilizadores e permitem avaliar definições como:  

    -   Código de acesso  

    -   Encriptação  

    -   Se o dispositivo está desbloqueado por jailbrake ou rooting  

    -   Indica se o e-mail no dispositivo é gerido por uma política do Configuration Manager ou o Intune  

     **Se for implementada nenhuma política de conformidade num dispositivo, em seguida, as políticas de acesso condicional aplicáveis irão tratar o dispositivo como compatível**.  

-   **Políticas de acesso condicional** estão configuradas para um serviço específico e definem regras tais como o Azure Active Directory de grupos de utilizadores de segurança ou coleções de utilizadores do Configuration Manager serão visadas ou excluídos.  

     Configurar a política de acesso condicional do Exchange no local da consola do Configuration Manager. No entanto, quando configurar uma política de Exchange Online ou o SharePoint Online, esta ação abre a consola de administração do Intune onde pode configura a política.  

     Ao contrário de outras políticas do Intune ou do Configuration Manager, o utilizador implementa políticas de acesso condicional. Em alternativa, configura estas políticas uma vez, e estas são aplicadas a todos os utilizadores visados.  

 Quando os dispositivos não cumprem as condições que configura, o utilizador é orientado através do processo de inscrição do dispositivo e da correção do problema que impede o dispositivo de ser compatível.  

**Antes de** começar a utilizar o acesso condicional, certifique-se de que tem o correto **requisitos** no local:  

## <a name="requirements-for-exchange-online-using-the-shared-multi-tenant-environment"></a>Requisitos para o Exchange Online (utilizando o ambiente multi-inquilino partilhado)
O acesso condicional para o Exchange Online suporta dispositivos que executam:
-   Windows 8.1 e posterior (quando inscrito com o Intune)
-   Windows 7.0 ou Windows 8.1 (quando associado a um domínio)
-   Windows Phone 8.1 e posterior
-   iOS 7.1 e posterior
-   Android 4.0 e posterior, Samsung KNOX Standard 4.0 e posterior

 **Além disso**:
-   Tem de ser dispositivos à área de trabalho associada, que regista o dispositivo com o serviço de registo de dispositivos de diretório Active Directory do Azure (AAD DRS).<br />     
- Os computadores que estiverem a um domínio têm de ser registados automaticamente no Azure Active Directory através de política de grupo ou MSI.

  A secção **Acesso condicional para computadores** neste tópico descreve todos os requisitos para ativar o acesso condicional para um computador.<br />     
  O AAD DRS será automaticamente ativado para os clientes do Intune e do Office 365. Os clientes que já implementaram o Serviço de Registos de Dispositivos do ADFS não verão dispositivos registados no respetivo Active Directory no local.
-   Tem de utilizar uma subscrição do Office 365 que inclua o Exchange Online (como o plano E3) e os utilizadores têm de estar licenciados para o Exchange Online.
-   O opcional **conector do Exchange Server** é opcional e liga o Configuration Manager ao Microsoft Exchange Online e ajuda-o a monitorizar informações de dispositivos através da consola do Configuration Manager (consulte [gerir dispositivos móveis com o System Center Configuration Manager e o Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)).
Não tem de utilizar o conector para utilizar políticas de conformidade ou políticas de acesso condicional, mas é necessário executar relatórios que ajudam a avaliar o impacto do acesso condicional.

## <a name="requirements-for-exchange-online-dedicated"></a>Requisitos para o Exchange Online dedicado
O acesso condicional para o Exchange Online Dedicado suporta dispositivos que executam:
-   Windows 8 e posterior (quando inscrito com o Intune)
-   Windows 7.0 ou Windows 8.1 (quando associado a um domínio)

  Acesso condicional a computadores associados a domínios apenas para inquilinos no novo ambiente dedicado do Exchange Online.
-   Windows Phone 8 e posterior
-   Todos os dispositivos iOS que utilizem um cliente de e-mail do Exchange ActiveSync (EAS)
-   Android 4 e posterior.
-   Para inquilinos no **ambiente Exchange Online dedicado legado**:    

  Tem de utilizar o **conector do Exchange Server** que liga o Configuration Manager ao Microsoft Exchange no local. Este procedimento permite-lhe gerir dispositivos móveis e ativa o acesso condicional (consulte [Gerir dispositivos móveis com o System Center Configuration Manager e o Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)).
-   Para inquilinos no **novo ambiente Exchange Online dedicado**:     
  O opcional **conector do Exchange Server** liga o Configuration Manager ao Microsoft Exchange Online e ajuda-o a gerir informações de dispositivos (consulte [gerir dispositivos móveis com o System Center Configuration Manager e o Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)). Não tem de utilizar o conector para utilizar políticas de conformidade ou políticas de acesso condicional, mas é necessário executar relatórios que ajudam a avaliar o impacto do acesso condicional.  

## <a name="requirements-for-exchange-on-premises"></a>Requisitos para o Exchange no local
O acesso condicional para o Exchange No Local suporta:
-   Windows 8 e posterior (quando inscrito com o Intune)
-   Windows Phone 8 e posterior
-   Aplicação de e-mail nativa no iOS
-   Aplicação de e-mail nativa no Android 4 ou posterior
-   A aplicação Microsoft Outlook não é suportada (Android e iOS).

**Além disso**:

-  Versão do Exchange tem de ser o Exchange 2010 ou posterior. Matriz de Servidor de Acesso de Cliente (CAS) do Exchange Server é suportada.

> [!TIP]
> Se o seu ambiente do Exchange estiver numa configuração de servidor CAS, tem de configurar o conector do Exchange no local para apontar para um dos servidores CAS.
- Tem de utilizar o **conector do Exchange Server** que liga o Configuration Manager ao Microsoft Exchange no local. Este procedimento permite-lhe gerir dispositivos móveis e ativa o acesso condicional (consulte [Gerir dispositivos móveis com o System Center Configuration Manager e o Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)).
  - Certifique-se de que está a utilizar a versão mais recente do **conector do Exchange no local**. O conector do Exchange no local deve ser configurado através da consola do Configuration Manager. Para obter instruções detalhadas, veja [Gerir dispositivos móveis com o System Center Configuration Manager e o Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).
  - O conector tem de estar configurado apenas no Site Primário do System Center Configuration Manager.</li><li>Este conector suporta o ambiente do Exchange CAS. <br />        Quando configurar o conector, tem de defini-lo para que comunique com um dos servidores do Exchange CAS.

- O Exchange ActiveSync pode ser configurado com a autenticação baseada em certificado ou com a entrada de credencial de utilizador


## <a name="requirements-for-skype-for-business-online"></a>Requisitos para o Skype para empresas Online
O acesso condicional para o SharePoint Online suporta dispositivos que executam:
 -   iOS 7.1 e posterior
 -   Android 4.0 e posterior
 -   Samsung KNOX Standard 4.0 ou posterior

**Além disso,** tem de ativar a autenticação moderna do Skype para empresas Online. Preencha este [formulário de ligação](https://connect.microsoft.com/office/Survey/NominationSurvey.aspx?SurveyID=17299&ProgramID=8715) para ser inscrito no programa de autenticação moderna.

Todos os utilizadores finais devem utilizar o Skype para Empresas Online. Se tiver uma implementação com o Skype para Empresas Online e o Skype para Empresas no local, a política de acesso condicional não será aplicada aos utilizadores finais que estejam no âmbito da implementação no local.

## <a name="requirements-for-sharepoint-online"></a>Requisitos para o SharePoint Online
O acesso condicional para o SharePoint Online suporta dispositivos que executam:
 -   Windows 8.1 e posterior (quando inscrito com o Intune)
 -   Windows 7.0 ou Windows 8.1 (quando associado a um domínio)
 -   Windows Phone 8.1 e posterior
 -   iOS 7.1 e posterior
 -   Android 4.0 e posterior, Samsung KNOX Standard 4.0 e posterior

 **Além disso**:
 -   Tem de ser dispositivos à área de trabalho associada, que regista o dispositivo com o serviço de registo de dispositivos de diretório Active Directory do Azure (AAD DRS).

 Os computadores que estiverem a um domínio têm de ser registados automaticamente no Azure Active Directory através de política de grupo ou MSI. A secção **Acesso condicional para computadores** neste tópico descreve todos os requisitos para ativar o acesso condicional para um computador.

 O AAD DRS será automaticamente ativado para os clientes do Intune e do Office 365. Os clientes que já implementaram o Serviço de Registos de Dispositivos do ADFS não verão dispositivos registados no respetivo Active Directory no local.
 -   É necessária uma subscrição do SharePoint Online e os utilizadores têm de estar licenciados para o SharePoint Online.

 ### <a name="conditional-access-for-pcs"></a>Acesso condicional para computadores

 Pode configurar o acesso condicional para computadores que executem aplicações de ambiente de trabalho do Office para aceder ao **Exchange Online** e ao **SharePoint Online** para computadores que cumpram os requisitos seguintes:
 -   O PC tem de estar em execução no Windows 7.0 ou Windows 8.1.
 -   O PC tem de ser um domínio associado ou em conformidade.

 Para poder estar em conformidade, o PC tem de estar inscritos no Intune e cumprir as políticas.

 Para um PC associado a um domínio, tem de defini-lo para [registar automaticamente o dispositivo](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/) no Azure Active Directory.
 -   A [Autenticação moderna do office 365 tem de estar ativada](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/), e tem de ter instaladas todas as atualizações mais recentes do Office.<br />     A autenticação moderna inclui o início de sessão baseado na Active Directory Authentication Library (ADAL) para clientes do Office 2013 Windows e permite uma maior segurança como **multi-factor authentication**e **autenticação baseada em certificado**.
 -   Configure regras de afirmações do ADFS para bloquear protocolos de autenticação não moderna.  

## <a name="next-steps"></a>Passos Seguintes  
 Leia os seguintes tópicos para saber como configurar as políticas de conformidade e as políticas de acesso condicional para o seu cenário necessário:  

-   [Gerir políticas de conformidade de dispositivos no System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md)  

-   [Gerir o acesso ao e-mail no System Center Configuration Manager](../../protect/deploy-use/manage-email-access.md)  

-   [Gerir o acesso ao SharePoint Online no System Center Configuration Manager](../../protect/deploy-use/manage-sharepoint-online-access.md)  

-   [Gerir o acesso ao Skype para Empresas Online](../../protect/deploy-use/manage-skype-for-business-online-access.md)  

### <a name="see-also"></a>Consulte também  

 [Introdução às definições de compatibilidade no System Center Configuration Manager](../../compliance/get-started/get-started-with-compliance-settings.md)
