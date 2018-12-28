---
title: Gerir o acesso ao Dynamics CRM Online
titleSuffix: Configuration Manager
description: Saiba como controlar o acesso ao Microsoft Dynamics CRM Online a partir de dispositivos iOS e Android com acesso condicional do Microsoft Intune.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 2bfc4c51-b25c-4c70-b81e-8a3b6ddf02c8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5e2c8ab4f8dc0b544a79b2113c278f97444357bf
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53420962"
---
# <a name="manage-dynamics-crm-online-access-in-system-center-configuration-manager"></a>Gerir o acesso ao Dynamics CRM Online no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode controlar o acesso ao Microsoft Dynamics CRM Online de dispositivos iOS e Android com acesso condicional do Microsoft Intune.  Acesso condicional do Intune tem dois componentes:
* [Política de conformidade do dispositivo](../../protect/deploy-use/device-compliance-policies.md) que o dispositivo tem de cumprir para ser considerado conforme.
* [Política de acesso condicional](../../protect/deploy-use/manage-access-to-services.md) que onde especifica as condições que o dispositivo tem de cumprir para poder aceder ao serviço.

Para saber mais sobre como funciona o acesso condicional como, leia os [gerir o acesso aos serviços](../../protect/deploy-use/manage-access-to-services.md) artigo.


Quando um utilizador direcionado tenta utilizar a aplicação do Dynamics CRM no respetivo dispositivo, ocorre a seguinte avaliação:

![Diagrama que mostra os pontos de decisão utilizados para determinar se um dispositivo tem permissão para aceder a um serviço ou está bloqueado](media/mdm-ca-dynamics-crm-flow-diagram.png)

Tem do dispositivo que necessita de acesso ao Dynamics CRM Online:
* Ser um **Android** ou **iOS** dispositivo.
* Ser **inscritos** com o Microsoft Intune.
* Ser **em conformidade** com todas políticas de conformidade do Microsoft Intune implementadas.

O estado do dispositivo é armazenado no Azure Active Directory, o qual concede ou bloqueia o acesso, com base nas condições que especificar.

Se não for cumprida uma condição, é apresentada ao utilizador uma das duas mensagens seguintes quando iniciar sessão:
* Se o dispositivo não estiver inscrito no Microsoft Intune ou não está registado no Azure Active Directory, é apresentada uma mensagem com instruções sobre como instalar a aplicação do portal da empresa e inscrevê-lo.
* Se o dispositivo não estiver em conformidade, é apresentada uma mensagem que direciona o utilizador para o Web site do Portal da empresa do Microsoft Intune ou a aplicação Portal da empresa, onde pode encontrar informações sobre o problema e como resolvê-lo.

## <a name="configure-conditional-access-for-dynamics-crm-online"></a>Configurar o acesso condicional para o Dynamics CRM Online  
### <a name="step-1-configure-active-directory-security-groups"></a>Passo 1: Configurar grupos de segurança do Active Directory

Antes de começar, configure grupos de segurança do Azure Active Directory para a política de acesso condicional. Pode configurar estes grupos no **Centro de administração do Office 365**. Estes grupos serão utilizados para visar ou excluir os utilizadores, da política. Quando um utilizador é direcionado por uma política, cada dispositivo que utiliza tem de estar em conformidade para poder aceder aos recursos.

Pode especificar dois tipos de grupo a utilizar para a política do Dynamics CRM:
* **Grupos visados** – contém os grupos de utilizadores aos quais será aplicada a política.
* **Grupos excluídos** – contém os grupos de utilizadores excluídos da política.

Se um utilizador estiver em ambos os grupos, estará excluído da política.

### <a name="step-2-configure-and-deploy-a-compliance-policy"></a>Passo 2: Configurar e implementar uma política de conformidade
[Criar e implementar](../../protect/deploy-use/device-compliance-policies.md) uma política de conformidade a todos os dispositivos que serão afetados pela política. Estes seriam todos os dispositivos que são utilizados pelos utilizadores nos grupos visados.

> [!NOTE]
> Enquanto as políticas de conformidade são implementadas nos grupos do Microsoft Intune, as políticas de acesso condicional são direcionadas para grupos de segurança do Azure Active Directory.

> [!IMPORTANT]
> Se não tiver implementado uma política de conformidade, os dispositivos serão tratados como conformes.

Quando estiver pronto, avance para o Passo 3.
### <a name="step-3-configure-the-dynamics-crm-policy"></a>Passo 3: Configurar a política do Dynamics CRM
Em seguida, configure a política para exigir que dispositivos apenas geridos e compatíveis podem aceder ao Dynamics CRM. Esta política será armazenada no Azure Active Directory.

1. Na consola de administração do Microsoft Intune, escolha **política > acesso condicional > política Dynamics CRM Online**.

    ![Captura de ecrã da página de política de acesso condicional do Dynamics CRM Online](media/mdm-ca-dynamics-crm-policy-configuration.png)

2. Selecione **ativar o acesso condicional** política.
3. Em **Acesso a aplicações**, pode optar por aplicar a política de acesso condicional a:
   * **iOS**
   * **Android**
4. Sob **grupos Direcionados**, escolha **modificar** para selecionar os grupos de segurança do Azure Active Directory aos quais será aplicada a política. Pode optar por direcionar esta opção para todos os utilizadores ou apenas para um grupos específico de utilizadores.
5. Sob **grupos excluídos**, opcionalmente, escolha **modificar** para selecionar os grupos de segurança do Azure Active Directory que estão excluídos desta política.
6. Quando tiver terminado, escolha **guardar**.

Agora tiver configurado o acesso condicional para o Dynamics CRM. Não tem de implementar a política de acesso condicional, pois esta entra em vigor imediatamente.
##  <a name="monitor-the-compliance-and-conditional-access-policies"></a>Monitorizar a conformidade e as políticas de acesso condicional

Na **grupos** área de trabalho, pode ver o estado de acesso condicional dos seus dispositivos.

Selecione qualquer grupo de dispositivos móveis e, em seguida, no separador **Dispositivos** , selecione um dos seguintes **Filtros**:
* **Dispositivos que não são registados no AAD** – estes dispositivos estão bloqueados no Dynamics CRM.
* **Dispositivos que não estejam em conformidade** – estes dispositivos estão bloqueados no Dynamics CRM.
* **Dispositivos que estão registados no AAD e conformes** – estes dispositivos podem aceder ao Dynamics CRM.

###  <a name="see-also"></a>Consulte também
[Gerir o acesso ao e-mail](../../protect/deploy-use/manage-email-access.md)

[Gerir o acesso ao SharePoint Online](../../protect/deploy-use/manage-sharepoint-online-access.md)

[Gerir o acesso ao Skype para empresas Online](../../protect/deploy-use/manage-skype-for-business-online-access.md)
