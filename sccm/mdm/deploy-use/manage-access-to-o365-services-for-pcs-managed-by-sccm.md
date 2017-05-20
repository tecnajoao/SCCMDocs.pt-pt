---
title: "Gerir o acesso aos serviços do Office 365 para PCs geridos | Documentos do Microsoft"
description: "Saiba como configurar o acesso condicional para PCs que são geridos pelo System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 34024741-edfa-4088-8599-d6bafc331e62
caps.latest.revision: 15
author: andredm7
ms.author: andredm
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 23b1d24e908d04b64c3bbfa518793a44e696d468
ms.openlocfilehash: e9028a54e538b4ec987dbaeb5ba1ee22ad091728
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="manage-access-to-o365-services-for-pcs-managed-by-system-center-configuration-manager"></a>Gerir o acesso aos serviços do O365 para computadores geridos pelo System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*



 A partir da versão 1602 do Configuration Manager, pode configurar o acesso condicional para PCs geridos pelo System Center Configuration Manager.  

> [!IMPORTANT]  
>  Esta é uma funcionalidade pré-lançamento disponível na atualização 1602, a atualização 1606 e a atualização 1610. As funcionalidades de pré-lançamento estão incluídas no produto para um teste antecipado num ambiente de produção, mas devem não ser consideradas prontas para produção. Para obter mais informações, veja [Utilizar as funcionalidades da versão de pré-lançamento de atualizações](../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease).
> - Depois de instalar a atualização 1602, o tipo de funcionalidade é apresentada como libertada, apesar de é versão de pré-lançamento.
> - Se, em seguida, atualizar a partir do 1602 para 1606, apresenta de tipo funcionalidade como lançadas mesmo através dele permanece versão de pré-lançamento.
> - Se atualizar a partir da versão 1511 diretamente para 1606, o tipo de funcionalidade apresenta como versão de pré-lançamento.

 Se estiver à procura de informações sobre como configurar o acesso condicional para dispositivos inscritos e geridos pelo Intune ou PCs que estão associados a um domínio e não foram avaliados em termos de conformidade, veja [Gerir o acesso aos serviços no System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md).  


## <a name="supported-services"></a>Serviços Suportados  

-   Exchange Online  

-   SharePoint Online  

## <a name="supported-pcs"></a>PC Suportados  

-   Windows 7  

-   Windows 8,1  

-   Windows 10 

## <a name="configure-conditional-access"></a>Configurar o acesso condicional  
 Para configurar o acesso condicional, tem primeiro de criar uma política de conformidade e configurar a política de acesso condicional. Quando configurar as políticas de acesso condicional para PC, pode exigir que os computadores estejam em conformidade com a política de conformidade para aceder aos serviços Exchange Online e SharePoint Online.  

### <a name="prerequisites"></a>Pré-requisitos  

-   Sincronização de ADFS e uma subscrição do O365. A subscrição do O365 serve para configurar o Exchange Online e o SharePoint Online.  

-   Uma Subscrição do Microsoft Intune. A Subscrição do Microsoft Intune deve ser configurada na Consola do Gestor de Configuração. Isto requer que esteja numa implementação híbrida.  

 Os PC devem satisfazer os seguintes requisitos:  

-   [Pré-requisitos](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1) para o registo automático de dispositivos no Azure Active Directory  

     Pode registar PCs no Azure AD através da política de conformidade.  

    -   Para PCs Windows 8.1 e Windows 10, pode utilizar uma Política de Grupo do Active Directory para configurar os dispositivos para serem registados automaticamente no Azure AD.  

    -   o   Para PCs Windows 7, tem de implementar o pacote de software de registo de dispositivos no seu PC Windows 7 através do System Center Configuration Manager. O [registo do dispositivo automática com dispositivos Azure Active Directory for Windows Domain-Joined](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1) tópico tem mais detalhes.  

-   Tem de utilizar o Office 2013 ou o Office 2016 com a autenticação moderna [ativada](https://support.office.com/en-US/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a).  

 Os passos descritos abaixo aplicam-se ao Exchange Online e ao SharePoint Online  

### <a name="step-1-configure-compliance-policy"></a>Passo 1. Configurar a política de compatibilidade  
 Na consola do Configuration Manager, crie uma política de conformidade com as seguintes regras:  

-   Exigir registo no Azure Active Directory: Esta regra verifica se o dispositivo do utilizador é o local de trabalho associados para o Azure AD e se não estiver, o dispositivo está automaticamente registado no Azure AD. O registo automático é suportado apenas no Windows 8.1. Para PCs Windows 7, implemente um MSI para efetuar o registo automático. Para obter mais detalhes, veja [Registo automático do dispositivo com o Azure Active Directory](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1)  

-   **Todas as atualizações necessárias instaladas com um prazo mais antigo do que um determinado número de dias:** Esta regra verifica para ver se o dispositivo do utilizador tiver todas as atualizações necessárias (especificadas na regra necessárias atualizações automáticas) dentro do prazo e período de tolerância especificada por si e instalar automaticamente a quaisquer pendentes atualizações necessárias.  

-   **Exigir encriptação de unidade BitLocker:** Esta é uma verificação de para ver se a unidade principal (por exemplo, c:\\) no dispositivo é BitLocker encriptado. Se a encriptação Bitlocker não estiver ativada no dispositivo primário, o acesso ao e-mail e aos SharePoint Services é bloqueado.  

-   **Exigir proteção contra software maligno:** Esta é uma verificação de para ver se o software antimalware (System Center Endpoint Protection ou apenas o Windows Defender) está ativado e em execução. Se não estiver ativado, o acesso ao e-mail e aos SharePoint Services é bloqueado.  

### <a name="step-2-evaluate-the-effect-of-conditional-access"></a>Passo 2. Avaliar o efeito do acesso condicional  
 Execute o Relatório de Compatibilidade de Acesso. Pode ser encontrada na secção em relatórios de monitorização > conformidade e gestão das definições. Isto apresenta o estado de conformidade de todos os dispositivos.  Os dispositivos comunicados como não compatíveis serão impedidos de aceder ao Exchange Online e ao SharePoint Online.  

 ![CA&#95;relatório de&#95;compatibilidade](media/CA_compliance_report.png)  

### <a name="configure-active-directory-security-groups"></a>Configurar Grupos de Segurança do Active Directory  
 O direcionamento de políticas de acesso condicional para grupos de utilizadores depende dos tipos de política. Estes grupos contêm os utilizadores que serão direcionados ou que estarão excluídos da política. Quando um utilizador é direcionado por uma política, cada dispositivo que utiliza tem de estar em conformidade para poder aceder ao serviço.  

 Grupos de utilizadores de segurança do Active Directory. Estes grupos de utilizadores devem ser sincronizados com o Azure Active Directory. Pode também configurar estes grupos no centro de administração do Office 365 ou no portal de contas do Intune.  

 Pode especificar dois tipos de grupos em cada política. :  

-   **Grupos direcionados** -grupos de utilizadores aos quais é aplicada a política. O mesmo grupo deve ser utilizado tanto para a política de acesso condicional e de conformidade.  

-   **Grupos excluídos** -grupos de utilizadores que são excluídos da política (opcional)  
    Se um utilizador estiver em ambos, estará excluído da política.  

     Apenas os grupos visados pela política de acesso condicional são avaliados.  

### <a name="step-3--create-a-conditional-access-policy-for-exchange-online-and-sharepoint-online"></a>Passo 3.  Crie uma política de acesso condicional para o Exchange Online e o SharePoint Online  

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  

2.  Selecione **Ativar política de acesso condicional para o Exchange Online**para criar uma política para o Exchange Online.  

     Selecione **Ativar política de acesso condicional para o Exchange Online**para criar uma política para o SharePoint Online.  

3.  No separador **Início** , no grupo **Ligações** , clique em **Configurar Política de Acesso Condicional na Consola do Intune**. Poderá ter de fornecer o nome de utilizador e a palavra-passe da conta utilizada para ligar o Gestor de Configuração ao Intune.  

     A consola de administração do Intune irá abrir.  

4.  Para o Exchange Online, na consola de administração do Microsoft Intune, clique em **política > acesso condicional > política do Exchange Online**.  

     Para o SharePoint Online, na consola de administração do Microsoft Intune, clique em **política > acesso condicional > política do SharePoint Online**.  

5.  Defina o requisito do PC Windows como **Os dispositivos têm de estar em conformidade**.  

6.  Em **Grupos Direcionados**, clique em **Modificar** para selecionar os grupos de segurança do Azure Active Directory aos quais será aplicada a política.  

    > [!NOTE]  
    >  O mesmo grupo de utilizadores de segurança deve ser utilizado para implementar a política de compliancy e o grupo de destino para a política de acesso condicional.  

     Como opção, em **Grupos Excluídos**, clique em **Modificar** para selecionar os grupos de segurança do Azure Active Directory que estão excluídos desta política.  

7.  Clique em **Guardar** para criar e guardar a política  

 Os utilizadores finais que estão bloqueados devido a não conformidade irão ver informações de compatibilidade no Centro de Software do System Center Configuration Manager e serão iniciada uma avaliação das políticas do novo quando são remediados problemas de compatibilidade.  

<!---
##  <a name="bkmk_KnownIssues"></a> Known issues  
 You may see the following issues when using this feature:  

-   In this 1602 update,  the 5 day compliance is not enforced. Even if compliance check on the end-user's device has happened more than 5 days ago, users still can access Office 365 and SharePoint online.  

-   When a device is not compliant with the compliance policy, the reason is not automatically displayed. The end- user must go to the new Software Center to find the reason for non-compliance. The reason is displayed in the Device compliance section of the Software Center.  

-   Windows 10 users may see multiple access failures when trying to reach O365 and/or SharePoint online resources. Note that conditional access is not fully supported for Windows 10.  
--->
### <a name="see-also"></a>Consulte também  
 [Proteger a infraestrutura de dados e o site com o System Center Configuration Manager](../../protect/understand/protect-data-and-site-infrastructure.md)
