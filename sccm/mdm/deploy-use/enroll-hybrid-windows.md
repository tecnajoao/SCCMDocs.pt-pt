---
title: "Configurar a gestão de dispositivos Windows híbrida com o System Center Configuration Manager e o Microsoft Intune | Microsoft Docs"
description: "Configure a gestão de dispositivos Windows com o System Center Configuration Manager e o Microsoft Intune."
ms.custom: na
ms.date: 03/17/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: dc1f70f5-64ab-42ab-aa91-d3858803e12f
caps.latest.revision: "9"
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 47348baeac26bfa2ad5016622fe4dbcb9f572483
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="set-up-windows-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurar a gestão de dispositivos híbridos do Windows com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este tópico indica aos administradores de TI como podem permitir que os seus utilizadores integrar o Windows PCs e dispositivos móveis na gestão através do Configuration Manager e o Microsoft Intune.

## <a name="enable-windows-device-management"></a>Ativar a gestão de dispositivos do Windows
Para ativar a gestão de dispositivos do Windows para PCs ou dispositivos móveis, utilize os seguintes passos:

1.  Antes de configurar a inscrição para qualquer plataforma, conclua os pré-requisitos e procedimentos [mm híbrida do programa de configuração](setup-hybrid-mdm.md).  
2.  Na consola do Configuration Manager no **administração** área de trabalho, aceda a **descrição geral** > **serviços em nuvem** > **subscrições do Microsoft Intune**.  
3.  No Friso, clique em **configurar plataformas**e, em seguida, selecione a plataforma do Windows:
    - **Windows** para Windows PCs e computadores portáteis, em seguida, execute os seguintes passos:
      1. No **geral** separador, clique em de **ativar inscrição Windows** caixa de verificação.
      2. Se utilizar um certificado para assinar com código e implementar a aplicação Portal da empresa, navegue para o **certificado de assinatura de código**. Os utilizadores de dispositivos também podem instalar a aplicação Portal da empresa da loja Windows ou pode implementar a aplicação da loja Windows para empresas sem assinatura de código.
      3. Também pode configurar [Windows Hello para definições da empresa](windows-hello-for-business-settings.md).
    - **Windows Phone** para dispositivos Windows Phone e tablets, em seguida, execute os seguintes passos:
      1. No **geral** separador, clique em de **Windows Phone 8.1 e Windows 10 Mobile** caixa de verificação. Windows Phone 8.0 já não é suportada.
      2. Se a sua organização tem de instalar aplicações em sideload da empresa, pode carregar o ficheiro ou do token necessária. Para obter mais informações sobre as aplicações de sideload, consulte [aplicações do Windows criar](https://docs.microsoft.com/sccm/apps/get-started/creating-windows-applications).
        - **Token de inscrição de aplicações**
        - **ficheiro. pfx**
        - **Nenhum** se utilizar um certificado da Symantec, pode especificar **mostrar um alerta antes de certificados da Symantec expirarem**.
4. Clique em **OK** para fechar a caixa de diálogo.  Para simplificar o processo de inscrição através do Portal da empresa, deve criar um alias DNS para inscrição de dispositivos. Em seguida, pode informar os utilizadores como inscrever os respetivos dispositivos.

## <a name="choose-how-to-enroll-windows-devices"></a>Escolher como inscrever dispositivos Windows

Assim que atribuiu licenças do Intune aos utilizadores, podem ser inscritos dispositivos Windows sem quaisquer passos adicionais, mas pode facilitar a inscrição para utilizadores.

Dois fatores determinam a forma como pode simplificar a inscrição de dispositivos do Windows:
- **Utilizar Azure Active Directory Premium?** <br>[O Azure AD Premium](https://docs.microsoft.com/azure/active-directory/active-directory-get-started-premium) está incluído com o Enterprise Mobility + de segurança e de outros planos de licenciamento.
- **Quais as versões de clientes do Windows irão inscrever?** <br>Dispositivos Windows 10 podem inscrever automaticamente ao adicionar uma conta escolar ou profissional. Versões anteriores têm de estar inscritos utilizando a aplicação Portal da empresa.

||**O Azure AD Premium**|**Outro AD**|
|----------|---------------|---------------|  
|**Windows 10**|[Inscrição automática](#enable-windows-10-automatic-enrollment) |[Inscrição do utilizador](#enable-windows-enrollment-without-azure-ad-premium)|
|**Versões anteriores do Windows**|[Inscrição do utilizador](#enable-windows-enrollment-without-azure-ad-premium)|[Inscrição do utilizador](#enable-windows-enrollment-without-azure-ad-premium)|

## <a name="enable-windows-10-automatic-enrollment"></a>Ativar a inscrição automática do Windows 10

Inscrição automática permite que os utilizadores inscrevam pertencentes à empresa ou pessoais Windows 10 PCs e Windows 10 dispositivos móveis no Intune ao adicionar uma conta escolar ou profissional e aceita para serem geridos. Simples que. Em segundo plano, o dispositivo do utilizador regista e associa o Azure Active Directory. Depois de registado, o dispositivo é gerido com o Intune.

**Pré-requisitos**
- Subscrição do Azure Active Directory Premium ([subscrição de avaliação](http://go.microsoft.com/fwlink/?LinkID=816845))
- Subscrição do Microsoft Intune


### <a name="configure-automatic-mdm-enrollment"></a>Configurar a inscrição MDM automática

1. Iniciar sessão para o [portal de gestão do Azure](https://portal.azure.com) (https://manage.windowsazure.com) e selecione **do Azure Active Directory**.

  ![Captura de ecrã do portal do Azure](../media/auto-enroll-azure-main.png)

2. Selecione **Mobility (MDM e MAM)**.

  ![Captura de ecrã do portal do Azure](../media/auto-enroll-mdm.png)

3. Selecione **do Microsoft Intune**.

  ![Captura de ecrã do portal do Azure](../media/auto-enroll-intune.png)

4. Configurar **âmbito do utilizador de MDM**. Especifique os dispositivos dos utilizadores que deverão ser geridos pelo Microsoft Intune. Dispositivos do Windows 10 dos utilizadores, estes serão automaticamente inscrito para gestão com o Microsoft Intune.

    - **Nenhum**
    - **Alguns**
    - **Todos os**

   ![Captura de ecrã do portal do Azure](../media/auto-enroll-scope.png)

5. Utilize os valores predefinidos para os seguintes URLs:
    - **Termos de MDM do URL de utilização**
    - **URL de deteção MDM**
    - **URL de conformidade de MDM**

6. Selecione **guardar**.


Por predefinição, a autenticação de dois fatores não está ativada para o serviço. No entanto, a autenticação de dois fatores recomenda ao registar um dispositivo. Antes de exigir autenticação de dois fatores para este serviço, tem de configurar um fornecedor de autenticação de dois fatores no Azure Active Directory e configurar as contas de utilizador para autenticação multifator. Consulte [introdução com o servidor do Azure multi-factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-cloud).

## <a name="enable-windows-enrollment-without-azure-ad-premium"></a>Ativar a inscrição do Windows do Azure AD Premium
Pode permitir que os utilizadores inscrevam os respetivos dispositivos sem inscrição automática do Azure AD Premium. Depois de atribuir licenças, os utilizadores podem inscrever-se depois de adicionar a respetiva conta profissional para os respetivos dispositivos pessoais ou associar os dispositivos pertencentes à empresa ao seu Azure AD. Criar um DNS alias (tipo de registo CNAME) torna mais fácil para os utilizadores inscrever os respetivos dispositivos. Se criar DNS CNAME registos de recursos, os utilizadores ligar e inscritos no Intune sem ter de introduzir o nome de servidor do Intune.

### <a name="create-cnames-to-simplify-enrollment"></a>Criar CNAMEs para simplificar a inscrição
Crie CNAME DNS de registos de recursos para o domínio da sua empresa. Por exemplo, se o site da sua empresa fosse contoso.com, criaria um CNAME em DNS que redireciona EnterpriseEnrollment.contoso.com para enterpriseenrollment-s.manage.microsoft.com.

Embora a criar entradas de CNAME DNS seja opcional, registos CNAME facilitar a inscrição para utilizadores. Não se for encontrada nenhum registo CNAME de inscrição, os utilizadores recebem introduzir manualmente o nome do servidor MDM, enrollment.manage.microsoft.com.

|Tipo|Nome do anfitrião|Aponta para|VALOR DE TTL|  
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.dominio_da_empresa.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 hora|

Se tiver mais do que um sufixo UPN, terá de criar um CNAME para cada nome de domínio e do ponto de cada um para EnterpriseEnrollment-s.manage.microsoft.com. Por exemplo, se os utilizadores contoso utilizar name@contoso.com, mas também utilizar name@us.contoso.com, e name@eu.constoso.com como o e-mail/UPN, o administrador da Contoso DNS é necessário criar o seguimento de CNAMEs.

|Tipo|Nome do anfitrião|Aponta para|VALOR DE TTL|  
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 hora|
|CNAME|EnterpriseEnrollment.us.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 hora|
|CNAME|EnterpriseEnrollment.eu.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 hora|

`EnterpriseEnrollment-s.manage.microsoft.com`– Suporta o redirecionamento para o serviço Intune com reconhecimento de domínio do nome de domínio do e-mail

As alterações para registos DNS poderão demorar até 72 horas a serem propagadas. Não é possível verificar a alteração DNS no Intune até o registo DNS ser propagado.

## <a name="tell-users-how-to-enroll-devices"></a>Informar os utilizadores como inscrever dispositivos  

 Assim que estiver configurado, terá de informar os utilizadores como inscrever os respetivos dispositivos. Consulte [o que dizer aos utilizadores sobre como inscrever os respetivos dispositivos](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune) para obter orientações. Pode direcionar os utilizadores [inscrever o seu dispositivo Windows no Intune](https://docs.microsoft.com/intune/enduser/enroll-your-device-in-intune-windows). Estas informações aplicam-se ao Microsoft Intune e aos dispositivos móveis geridos pelo Configuration Manager.

> [!div class="button"]
[< Anterior passo](create-service-connection-point.md)[passo seguinte >  ](set-up-additional-management.md)
