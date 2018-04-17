---
title: Acesso condicional
titleSuffix: Configuration Manager
description: Saiba como utilizar o acesso condicional no System Center Configuration Manager para ajudar a proteger o e-mail e outros serviços.
ms.custom: na
ms.date: 12/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b04727b-d563-422f-8d59-4dd66215d0b3
caps.latest.revision: 26
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 7fea8d0e47fff5288a58232eb9bd17171481b3a3
ms.sourcegitcommit: fb84bcb31d825f454785e3d9d8be669e00fe2b27
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/16/2018
---
# <a name="manage-access-to-services-in-system-center-configuration-manager"></a>Gerir o acesso a serviços no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


## <a name="conditional-access-in-system-center-configuration-manager"></a>Acesso condicional no System Center Configuration Manager
Utilizar o acesso condicional para especificar condições para ajudar a proteger o e-mail e outros serviços em dispositivos inscritos com o Microsoft Intune.  

 Para obter informações sobre o acesso condicional em dispositivos que são geridos com o cliente do Configuration Manager, consulte [gerir o acesso aos serviços do O365 para PCs geridos pelo System Center Configuration Manager](../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md).  


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

    -   Indica se o e-mail no dispositivo é gerido por uma política do Configuration Manager ou o Microsoft Intune  

     Um dispositivo de relatórios em conformidade com as políticas de acesso condicional aplicáveis se o utilizador não implementa nenhuma política de conformidade ao mesmo.

-   **Políticas de acesso condicional** são para um serviço específico. Estas políticas definem regras como o Azure Active Directory grupos de utilizadores de segurança ou coleções de utilizadores do Configuration Manager para visar ou excluir.  

     Configurar a política de acesso condicional do Exchange no local da consola do Configuration Manager. No entanto, quando configurar uma política de Exchange Online ou o SharePoint Online, abre a consola do Microsoft Intune para configurar a política.  

     Ao contrário de outras políticas do Microsoft Intune ou do Configuration Manager, o utilizador implementa políticas de acesso condicional. Em vez disso, configura estas políticas uma vez, e estas são aplicadas a todos os utilizadores visados.  

 Quando os dispositivos não cumprem as condições configuradas, o utilizador é orientada embora a inscrição do dispositivo e corrigir o problema de conformidade do dispositivo.  

Antes de começar a utilizar o acesso condicional, certifique-se de que tem os requisitos corretos em funcionamento:  

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

  O **acesso condicional para PCs** secção deste artigo descreve todos os requisitos para ativar o acesso condicional para PC.<br />     
  O AAD DRS ativa automaticamente para os clientes do Microsoft Intune e do Office 365. Os clientes que já tem implementado o serviço de registo de dispositivos do ADFS não pode vir dispositivos registados no seu Active Directory no local.
-   Utilize uma subscrição do Office 365 que inclua o Exchange Online (como o plano E3). Os utilizadores têm de estar licenciados para o Exchange Online.
-   Conector do Exchange Server é opcional e liga o Configuration Manager ao Microsoft Exchange Online. Este conector ajuda-o a monitorizar informações de dispositivos através da consola do Configuration Manager. Para obter mais informações, veja [Gerir dispositivos móveis com o System Center Configuration Manager e o Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).
Não é necessário o conector para utilizar políticas de conformidade ou políticas de acesso condicional. A execução de relatórios sobre o impacto do acesso condicional requer o conector.

## <a name="requirements-for-exchange-online-dedicated"></a>Requisitos para o Exchange Online dedicado
O acesso condicional para o Exchange Online Dedicado suporta dispositivos que executam:
-   Windows 8 e posterior (quando inscrito com o Intune)
-   Windows 7.0 ou Windows 8.1 (quando associado a um domínio)

  Acesso condicional a computadores associados a domínios apenas para inquilinos no novo ambiente dedicado do Exchange Online.
-   Windows Phone 8 e posterior
-   Todos os dispositivos iOS que utilizem um cliente de e-mail do Exchange ActiveSync (EAS)
-   Android 4 e posterior.
-   Para inquilinos no ambiente legado do Exchange Online dedicado:    

  Utilize o conector do Exchange Server, que liga o Configuration Manager ao Microsoft Exchange no local. O conector permite-lhe gerir dispositivos móveis e ativa o acesso condicional. Para obter mais informações, veja [Gerir dispositivos móveis com o System Center Configuration Manager e o Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).
-   Para inquilinos no novo ambiente Exchange Online dedicado:     
  Conector do Exchange Server é opcional, que liga o Configuration Manager ao Microsoft Exchange Online e ajuda-o a gerir informações de dispositivos. Para obter mais informações, veja [Gerir dispositivos móveis com o System Center Configuration Manager e o Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md). Não é necessário o conector para utilizar políticas de conformidade ou políticas de acesso condicional. A execução de relatórios sobre o impacto do acesso condicional requer o conector.  

## <a name="requirements-for-exchange-on-premises"></a>Requisitos para o Exchange no local
Acesso condicional ao Exchange no local suporta:
-   Windows 8 e posterior (quando inscrito com o Intune)
-   Windows Phone 8 e posterior
-   Aplicação de e-mail nativa no iOS
-   Aplicação de e-mail nativa no Android 4 ou posterior
-   A aplicação Microsoft Outlook não é suportada (Android e iOS)

**Além disso**:

- Versão do Exchange tem de ser o Exchange 2010 ou posterior
- Matriz de servidor de acesso de cliente (CAS) do Exchange server é suportada

> [!TIP]
> Se o seu ambiente do Exchange estiver numa configuração de servidor CAS, tem de configurar o conector do Exchange no local para apontar para um dos servidores CAS.
- Utilize o conector do Exchange Server, que liga o Configuration Manager ao Microsoft Exchange no local. O conector permite-lhe gerir dispositivos móveis e ativa o acesso condicional. Para obter mais informações, veja [Gerir dispositivos móveis com o System Center Configuration Manager e o Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).
  - Certifique-se de que está a utilizar a versão mais recente do conector do Exchange no local. Configure o conector do Exchange no local através da consola do Configuration Manager. Para obter instruções detalhadas, veja [Gerir dispositivos móveis com o System Center Configuration Manager e o Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).
  - Apenas de configurar o conector no site primário do Configuration Manager

- Exchange ActiveSync pode ser configurado com a autenticação baseada em certificado ou a entrada de credenciais de utilizador


## <a name="requirements-for-skype-for-business-online"></a>Requisitos para o Skype para empresas Online
O acesso condicional para o SharePoint Online suporta dispositivos que executam:
 -   iOS 7.1 e posterior
 -   Android 4.0 e posterior
 -   Samsung KNOX Standard 4.0 ou posterior

Ativar [autenticação moderna](https://aka.ms/SkypeModernAuth) para o Skype para empresas Online. 

Todos os utilizadores devem utilizar o Skype para empresas Online. Se tiver uma implementação com o Skype para empresas Online e Skype para empresas no local, a política de acesso condicional não é aplicável aos utilizadores no local.

## <a name="requirements-for-sharepoint-online"></a>Requisitos para o SharePoint Online
O acesso condicional para o SharePoint Online suporta dispositivos que executam:
 -   Windows 8.1 e posterior (quando inscrito com o Intune)
 -   Windows 7.0 ou Windows 8.1 (quando associado a um domínio)
 -   Windows Phone 8.1 e posterior
 -   iOS 7.1 e posterior
 -   Android 4.0 e posterior, Samsung KNOX Standard 4.0 e posterior

 **Além disso**:
 -   Tem de ser dispositivos à área de trabalho associada, que regista o dispositivo com o serviço de registo de dispositivos de diretório Active Directory do Azure (AAD DRS).

 Os computadores que estiverem a um domínio têm de ser registados automaticamente no Azure Active Directory através de política de grupo ou MSI. O **acesso condicional para PCs** secção deste artigo descreve todos os requisitos para ativar o acesso condicional para PC.

 O AAD DRS ativa automaticamente para os clientes do Microsoft Intune e do Office 365. Os clientes que já tem implementado o serviço de registo de dispositivos do ADFS não pode vir dispositivos registados no seu Active Directory no local.
 -   É necessária uma subscrição do SharePoint Online e os utilizadores têm de estar licenciados para o SharePoint Online.

 ### <a name="conditional-access-for-pcs"></a>Acesso condicional para computadores

 Pode configurar o acesso condicional para computadores que executem aplicações de ambiente de trabalho do Office e aceder ao Exchange Online ou o SharePoint Online. Os PC devem satisfazer os seguintes requisitos:
 -   O computador deve ser executar o Windows 7.0 ou Windows 8.1
 -   O PC tem de ser um domínio associado ou em conformidade

 Para poder estar em conformidade, o PC tem de estar inscrito no Microsoft Intune e cumprir as políticas.

 Para um PC associado a um domínio, tem de defini-lo para [registar automaticamente o dispositivo](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access-automatic-device-registration/) no Azure Active Directory.
 -   A [Autenticação moderna do office 365 tem de estar ativada](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/), e tem de ter instaladas todas as atualizações mais recentes do Office.<br />     A autenticação moderna inclui o baseada no Active Directory Authentication Library ADAL início de sessão para clientes do Office 2013 Windows e permite uma maior segurança como autenticação multifator e autenticação baseada em certificado.
 -   Configure regras de afirmações do ADFS para bloquear protocolos de autenticação não moderna.  

## <a name="next-steps"></a>Passos Seguintes  
 Leia os seguintes tópicos para saber como configurar as políticas de conformidade e as políticas de acesso condicional para o seu cenário necessário:  

-   [Gerir políticas de conformidade de dispositivos no System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md)  

-   [Gerir o acesso ao e-mail no System Center Configuration Manager](../../protect/deploy-use/manage-email-access.md)  

-   [Gerir o acesso ao SharePoint Online no System Center Configuration Manager](../../protect/deploy-use/manage-sharepoint-online-access.md)  

-   [Gerir o acesso ao Skype para Empresas Online](../../protect/deploy-use/manage-skype-for-business-online-access.md)  

### <a name="see-also"></a>Consulte também  

 [Introdução às definições de compatibilidade no System Center Configuration Manager](../../compliance/get-started/get-started-with-compliance-settings.md)
