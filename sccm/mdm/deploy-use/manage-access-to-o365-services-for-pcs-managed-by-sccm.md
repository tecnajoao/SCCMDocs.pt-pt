---
title: Gerir o acesso aos serviços do Office 365
titleSuffix: Configuration Manager
description: Saiba como configurar o acesso condicional para serviços do Office 365 para PCs geridos pelo System Center Configuration Manager.
ms.date: 03/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 34024741-edfa-4088-8599-d6bafc331e62
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 434801b170ed5efcbbafa046a3ac1e94a615ed3d
ms.sourcegitcommit: f38ef9afb0c608c0153230ff819e5f5e0fb1520c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/19/2019
ms.locfileid: "58196777"
---
# <a name="manage-access-to-office-365-services-for-pcs-managed-by-system-center-configuration-manager"></a>Gerir o acesso aos serviços do Office 365 para PC geridos pelo System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

<!--1191496-->
Configure o acesso condicional para serviços do Office 365 para PC geridos pelo Configuration Manager.  

> [!Important]  
> Incluindo de MDM híbrida no local são de acesso condicional [funcionalidades preteridas](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Para obter mais informações, consulte [o que é a MDM híbrida](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  
> 
> Se utilizar o acesso condicional em dispositivos geridos com o cliente do Configuration Manager, para se certificar de que ainda estão protegidos, primeiro ative o acesso condicional no Intune para os dispositivos antes de migrar. Ativar a cogestão no Configuration Manager, mover a carga de trabalho de política de conformidade para o Intune e, em seguida, conclua a migração do Intune híbrido para o Intune autónomo. Para obter mais informações, consulte [acesso condicional com cogestão](https://docs.microsoft.com/sccm/comanage/quickstart-conditional-access). 


Para obter informações sobre como configurar o acesso condicional para dispositivos inscritos e geridos pelo Microsoft Intune, consulte [gerir o acesso a serviços no System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md). Esse artigo também aborda os dispositivos que têm um domínio associado e não avaliados quanto à conformidade.

> [!Note]  
> O Configuration Manager não permite esta funcionalidade opcional por predefinição. Tem de ativar esta funcionalidade antes de o utilizar. Para mais informações, consulte [Enable optional features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


## <a name="supported-services"></a>Serviços Suportados  

-   Exchange Online
-   SharePoint Online

## <a name="supported-pcs"></a>PC Suportados  

-   Windows 7
-   Windows 8,1
-   Windows 10

## <a name="supported-windows-servers"></a>Servidores do Windows suportadas

-   Windows Server 2008 R2
-   Windows Server 2012
-   Windows Server 2012 R2
-   Windows Server 2016

    > [!IMPORTANT]
    > Para servidores de Windows que pode ter vários utilizadores com sessão iniciados em simultâneo, implemente as mesmas políticas de acesso condicional para todos esses usuários.

## <a name="configure-conditional-access"></a>Configurar o acesso condicional  
 Para configurar o acesso condicional, tem primeiro de criar uma política de conformidade e configurar a política de acesso condicional. Ao configurar políticas de acesso condicional para PCs, pode exigir que os computadores estejam em conformidade para poder aceder aos serviços Exchange Online e SharePoint Online.  

### <a name="prerequisites"></a>Pré-requisitos  

- Sincronização de ADFS e uma subscrição do Office 365. A subscrição do Office 365 é para configurar o Exchange Online e SharePoint Online.  

- Uma Subscrição do Microsoft Intune. A Subscrição do Microsoft Intune deve ser configurada na Consola do Gestor de Configuração. A subscrição do Intune é utilizada para retransmitir o estado de conformidade do dispositivo ao Azure Active Directory e para licenciamento de utilizadores.  

  Os PC devem satisfazer os seguintes requisitos:  

- [Pré-requisitos](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) para o registo automático de dispositivos no Azure Active Directory  

   Pode registar PCs no Azure AD através da política de conformidade.  

  -   Para PCs Windows 8.1 e Windows 10, pode utilizar uma Política de Grupo do Active Directory para configurar os dispositivos para serem registados automaticamente no Azure AD.  

  -   o   Para PCs Windows 7, tem de implementar o pacote de software de registo de dispositivos no seu PC Windows 7 através do System Center Configuration Manager. O [registo automático de dispositivos com dispositivos associados a domínio](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) artigo inclui mais detalhes.  

- Tem de utilizar o Office 2013 ou o Office 2016 com a autenticação moderna [ativada](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a).  

  Os seguintes passos aplicam-se ao Exchange Online e SharePoint Online  

### <a name="step-1-configure-compliance-policy"></a>Passo 1. Configurar a política de compatibilidade  
 Na consola do Configuration Manager, crie uma política de conformidade com as seguintes regras:  

-   **Exigir registo no Azure Active Directory:** Esta regra verifica se o dispositivo do utilizador é o local de trabalho associados ao Azure AD e, se não estiver, o dispositivo é automaticamente registado no Azure AD. O registo automático é suportado apenas no Windows 8.1. Para PCs Windows 7, implemente um MSI para efetuar o registo automático. Para obter mais informações, consulte [registo automático de dispositivos com o Azure Active Directory](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup)  

-   **Todas as atualizações necessárias instaladas com um prazo mais antigo do que um determinado número de dias:** Especifica o valor para o período de tolerância do prazo de implementação para as atualizações necessárias no dispositivo do utilizador. Adicionar esta regra também automaticamente instala quaisquer atualizações necessárias pendentes. Especificar as atualizações necessárias no **atualizações automáticas necessárias** regra.   

-   **Exigir encriptação de unidade de disco BitLocker:** Esta regra verifica se a unidade principal (por exemplo, c:\\) no dispositivo é encriptada por BitLocker. Se o BitLocker encriptação não está ativada no dispositivo primário, o acesso ao e-mail e aos SharePoint services é bloqueado.  

-   **Exigir Antimalware:** Esta regra verifica se o System Center Endpoint Protection ou o Windows Defender está ativado e em execução. Se não estiver ativado, o acesso ao e-mail e aos SharePoint Services é bloqueado.  

-   **Comunicado como bom estado de funcionamento pelo serviço de atestado de estado de funcionamento:** Esta condição inclui quatro subrules para verificar a conformidade do dispositivo contra o serviço de atestado de estado de funcionamento do dispositivo. Para obter mais informações, consulte [atestado de estado de funcionamento](/sccm/core/servers/manage/health-attestation). 

    - **Exigir o BitLocker seja ativado no dispositivo**
    - **Exigir que o arranque seguro seja ativado no dispositivo** 
    - **Exigir integridade de código ser ativada no dispositivo**
    - **Exigir antecipada início antecipado seja ativado no dispositivo**  

    >[!Tip]  
    > Os critérios de acesso condicional para o atestado de estado de funcionamento do dispositivo foi introduzido pela primeira vez na versão 1710 como um [funcionalidade de pré-lançamento](/sccm/core/servers/manage/pre-release-features). A partir da versão 1802, esta funcionalidade já não é uma funcionalidade de pré-lançamento.<!--1235616-->  

    > [!Note]  
    > O Configuration Manager não permite esta funcionalidade opcional por predefinição. Tem de ativar esta funcionalidade antes de o utilizar. Para mais informações, consulte [Enable optional features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  

### <a name="step-2-evaluate-the-effect-of-conditional-access"></a>Passo 2. Avaliar o efeito do acesso condicional  
 Executar o **relatório de conformidade de acesso condicional**. Podem ser encontrados na **monitorização** área de trabalho sob **relatórios** > **definições de gestão de compatibilidade e**. Este relatório apresenta o estado de conformidade para todos os dispositivos. Dispositivos que reportem como não conforme são bloqueados de aceder ao Exchange Online e SharePoint Online.  

 ![Consola do Configuration Manager, área de trabalho de monitorização, relatórios, relatórios, gestão de compatibilidade e definições: Relatório de conformidade de acesso condicional](media/CA_compliance_report.png)  

### <a name="configure-active-directory-security-groups"></a>Configurar Grupos de Segurança do Active Directory  
 O direcionamento de políticas de acesso condicional para grupos de utilizadores depende dos tipos de política. Estes grupos contêm os utilizadores que o visados pela política, ou excluir da política. Quando uma política destina-se um utilizador, cada dispositivo que utiliza tem de ser em conformidade para poder aceder ao serviço.  

 Grupos de utilizadores de segurança do Active Directory. Estes grupos de utilizadores devem ser sincronizados com o Azure Active Directory. Também pode configurar estes grupos no Centro de administração do Microsoft 365 ou o portal de contas do Intune.  

 Pode especificar dois tipos de grupos em cada política. :  

-   **Grupos visados** -grupos de utilizadores aos quais é aplicada a política. O mesmo grupo deve ser usado para conformidade e a política de acesso condicional.  

-   **Grupos excluídos** -grupos de utilizadores excluídos da política (opcional).  
    Se um utilizador estiver em ambos, o que são excluídos da política.  

     Apenas os grupos visados pela política de acesso condicional são avaliados.  

### <a name="step-3-create-a-conditional-access-policy-for-exchange-online-and-sharepoint-online"></a>Passo 3. Crie uma política de acesso condicional para o Exchange Online e o SharePoint Online  

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  

2.  Selecione **Ativar política de acesso condicional para o Exchange Online**para criar uma política para o Exchange Online.  

     Selecione **Ativar política de acesso condicional para o Exchange Online**para criar uma política para o SharePoint Online.  

3.  No separador **Início** , no grupo **Ligações** , clique em **Configurar Política de Acesso Condicional na Consola do Intune**. Poderá ter de fornecer o nome de utilizador e a palavra-passe da conta utilizada para ligar o Gestor de Configuração ao Intune.  

     Abre a consola de administração do Intune.  

4.  Para o Exchange Online, na consola de administração do Microsoft Intune, clique em **política > acesso condicional > política do Exchange Online**.  

     Para o SharePoint Online, na consola de administração do Microsoft Intune, clique em **política > acesso condicional > política do SharePoint Online**.  

5.  Defina o requisito do PC Windows como **Os dispositivos têm de estar em conformidade**.  

6.  Sob **grupos Direcionados**, clique em **modificar** para selecionar os grupos de segurança do Azure Active Directory aos quais se aplica a política.  

    > [!NOTE]  
    >  O mesmo grupo de utilizadores de segurança deve ser usado para implementar a política de conformidade e o grupo de destino para a política de acesso condicional.  

     Como opção, em **Grupos Excluídos**, clique em **Modificar** para selecionar os grupos de segurança do Azure Active Directory que estão excluídos desta política.  

7.  Clique em **Guardar** para criar e guardar a política  

Os utilizadores ver as informações de conformidade no Centro de Software. Quando bloqueado devido a não conformidade, inicie uma nova avaliação de política depois de corrigir os problemas de conformidade.  


## <a name="see-also"></a>Consulte também

- [Proteger a infraestrutura de dados e do site com o System Center Configuration Manager](../../protect/understand/protect-data-and-site-infrastructure.md)
- [Resolução de problemas de acesso condicional fluxograma para o Configuration Manager](https://gallery.technet.microsoft.com/Conditional-access-fd747c1a?redir=0)
