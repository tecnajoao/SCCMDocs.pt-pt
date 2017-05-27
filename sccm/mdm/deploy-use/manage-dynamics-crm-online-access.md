---
title: Gerir o acesso Dynamics CRM Online | Documentos do Microsoft
description: Saiba como controlar o acesso ao Microsoft Dynamics CRM Online a partir de dispositivos iOS e Android com acesso condicional do Microsoft Intune.
ms.custom: na
ms.date: 03/05/2017
ms.reviewer: na
ms.prod: configuration-manager
ms.technology:
- configmgr-hybrid
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bfc4c51-b25c-4c70-b81e-8a3b6ddf02c8
caps.latest.revision: 5
author: andredm7
ms.author: andredm
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 6424fb07802b62820b4dc78a58ab30d3b956abef
ms.openlocfilehash: bd00f12ae3bc14a34d24c22c3d5277d275d51e85
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="manage-dynamics-crm-online-access-in-system-center-configuration-manager"></a>Gerir o acesso Dynamics CRM Online no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode controlar o acesso ao Microsoft Dynamics CRM Online a partir de dispositivos iOS e Android com acesso condicional do Microsoft Intune.  Acesso condicional do Intune tem dois componentes:
* [Política de conformidade do dispositivo](../../protect/deploy-use/device-compliance-policies.md) que o dispositivo tem de cumprir para ser considerado compatível.
* [Política de acesso condicional](../../protect/deploy-use/manage-access-to-services.md) que onde pode especificar as condições que o dispositivo tem de cumprir para poder aceder ao serviço.

Para saber mais sobre como condicional funciona de acesso, consulte o [gerir o acesso aos serviços](../../protect/deploy-use/manage-access-to-services.md) artigo.


Quando um utilizador direcionado se tentar utilizar a aplicação do Dynamics CRM no respetivo dispositivo, ocorre a seguinte avaliação:

![Diagrama de mostrar os pontos de decisão, utilizados para determinar se um dispositivo é permitido o acesso a um serviço ou está bloqueado](media/mdm-ca-dynamics-crm-flow-diagram.png)

Tem do dispositivo que precisa de acesso à Dynamics CRM Online:
* Ser um **Android** ou **iOS** dispositivo.
* Ser **inscritos** com o Microsoft Intune.
* Ser **compatíveis** com qualquer uma implementadas políticas de conformidade do Microsoft Intune.

O estado do dispositivo é armazenado no Azure Active Directory, o qual concede ou bloqueia o acesso, com base nas condições que especificar.

Se não for cumprida uma condição, é apresentada ao utilizador uma das duas mensagens seguintes quando iniciar sessão:
* Se o dispositivo não estiver inscrito no Microsoft Intune ou não está registado no Azure Active Directory, será apresentada uma mensagem com instruções sobre como instalar a aplicação do portal da empresa e inscrevê-lo.
* Se o dispositivo não for conforme, será apresentada uma mensagem que direciona o utilizador para o Web site do Portal da empresa do Microsoft Intune ou a aplicação Portal da empresa onde pode encontrar informações sobre o problema e como resolvê-lo.

## <a name="configure-conditional-access-for-dynamics-crm-online"></a>Configurar o acesso condicional para o Dynamics CRM Online  
### <a name="step-1-configure-active-directory-security-groups"></a>Passo 1: Configurar grupos de segurança do Active Directory

Antes de começar, configure grupos de segurança do Azure Active Directory para a política de acesso condicional. Pode configurar estes grupos no **Centro de administração do Office 365**. Estes grupos serão utilizado para o destino, ou utilizadores excluídos da política. Quando um utilizador é direcionado por uma política, cada dispositivo que utiliza tem de estar em conformidade para poder aceder aos recursos.

Pode especificar dois tipos de grupo a utilizar para a política de Dynamics CRM:
* **Grupos direcionados** – contém os grupos de utilizadores aos quais será aplicada a política.
* **Grupos excluídos** – contém os grupos de utilizadores que são excluídos da política.

Se um utilizador estiver em ambos os grupos, estará excluído da política.

### <a name="step-2-configure-and-deploy-a-compliance-policy"></a>Passo 2: Configure e implemente uma política de conformidade
[Criar e implementar](../../protect/deploy-use/device-compliance-policies.md) uma política de conformidade em todos os dispositivos que serão afetadas pela política. Seriam todos os dispositivos que são utilizados pelos utilizadores nos grupos de destino.

> [!NOTE]
> Enquanto as políticas de conformidade são implementadas para grupos do Microsoft Intune, políticas de acesso condicional são direcionadas para grupos de segurança do Azure Active Directory.

> [!IMPORTANT]
> Se não tiver implementado uma política de conformidade, os dispositivos serão tratados como estando em conformidade.

Quando estiver pronto, avance para o Passo 3.
### <a name="step-3-configure-the-dynamics-crm-policy"></a>Passo 3: Configurar a política de Dynamics CRM
Em seguida, configure a política para exigir que os dispositivos apenas geridos e conformes podem aceder Dynamics CRM. Esta política será armazenada no Azure Active Directory.

1.  Na consola de administração do Microsoft Intune, escolha **política > acesso condicional > política do Dynamics CRM Online**.

     ![Captura de ecrã da página de política de acesso condicional Dynamics CRM Online](media/mdm-ca-dynamics-crm-policy-configuration.png)

2.  Selecione **ativar o acesso condicional** política.
3.  Em **Acesso a aplicações**, pode optar por aplicar a política de acesso condicional a:
  * **iOS**
  * **Android**
4.  Em **grupos Direcionados**, escolha **modificar** para selecionar os grupos de segurança do Azure Active Directory aos quais será aplicada a política. Pode optar por direcionar esta opção para todos os utilizadores ou apenas para um grupos específico de utilizadores.
5.  Em **grupos excluídos**, opcionalmente, selecione **modificar** para selecionar os grupos de segurança do Azure Active Directory que estão excluídos desta política.
6.  Quando tiver terminado, selecione **guardar**.

Agora que foram configuradas acesso condicional Dynamics CRM. Não tem de implementar a política de acesso condicional, pois esta entra em vigor imediatamente.
##  <a name="monitor-the-compliance-and-conditional-access-policies"></a>Monitorizar a conformidade e as políticas de acesso condicional

No **grupos** área de trabalho, pode ver o estado de acesso condicional dos seus dispositivos.

Selecione qualquer grupo de dispositivos móveis e, em seguida, no separador **Dispositivos** , selecione um dos seguintes **Filtros**:
* **Dispositivos não registados no AAD** – estes dispositivos estão bloqueados a partir do Dynamics CRM.
* **Dispositivos que não são compatíveis** – estes dispositivos estão bloqueados a partir do Dynamics CRM.
* **Dispositivos que são registados no AAD e conformes** – estes dispositivos podem aceder ao Dynamics CRM.

###  <a name="see-also"></a>Consulte também
[Gerir o acesso ao correio eletrónico](../../protect/deploy-use/manage-email-access.md)

[Gerir o acesso ao SharePoint Online](../../protect/deploy-use/manage-sharepoint-online-access.md)

[Gerir o acesso ao Skype para empresas Online](../../protect/deploy-use/manage-skype-for-business-online-access.md)

