---
title: "Configurar a gestão de dispositivos do Windows híbrida com o System Center Configuration Manager e o Microsoft Intune | Documentos do Microsoft"
description: "Configure a gestão de dispositivos Windows com o System Center Configuration Manager e o Microsoft Intune."
ms.custom: na
ms.date: 03/17/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: dc1f70f5-64ab-42ab-aa91-d3858803e12f
caps.latest.revision: 9
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 329de5ffb6eb1403c02cd1db634c32f045e82488
ms.openlocfilehash: 47348baeac26bfa2ad5016622fe4dbcb9f572483
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="set-up-windows-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurar a gestão de dispositivos híbridos do Windows com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este tópico informa administradores de TI como podem permitem que os utilizadores trazer Windows PCs e dispositivos móveis para a gestão com o Configuration Manager e o Microsoft Intune.

## <a name="enable-windows-device-management"></a>Ativar a gestão de dispositivos Windows
Para ativar a gestão de dispositivos do Windows para PCs ou dispositivos móveis, utilize os seguintes passos:

1.  Antes de configurar a inscrição para qualquer plataforma, concluir os pré-requisitos e procedimentos [híbrida configuração MDM](setup-hybrid-mdm.md).  
2.  Na consola do Configuration Manager no **administração** área de trabalho, aceda a **descrição geral** > **serviços em nuvem** > **subscrições do Microsoft Intune**.  
3.  No Friso, clique em **configurar platformas**e, em seguida, selecione a plataforma do Windows:
    - **Windows** para Windows PCs e portáteis, em seguida, execute os seguintes passos:
      1. No **geral** , clique a **inscrição ativar Windows** caixa de verificação.
      2. Se utilizar um certificado para assinar código e implementar a aplicação de Portal da empresa, navegue para o **certificado de assinatura de código**. Os utilizadores dos dispositivos também podem instalar a aplicação de Portal da empresa na loja Windows ou pode implementar a aplicação da loja Windows para empresas sem assinatura de código.
      3. Também pode configurar [Windows Hello para definições de empresas](windows-hello-for-business-settings.md).
    - **Windows Phone** para Windows phones e tablets, em seguida, execute os seguintes passos:
      1. No **geral** , clique a **Windows Phone 8.1 e Windows 10 Mobile** caixa de verificação. Windows Phone 8.0 já não é suportada.
      2. Se a sua organização tem de instalar aplicações em sideload da empresa, pode carregar o token necessária ou o ficheiro. Para mais informações sobre aplicações de sideload, consulte o artigo [aplicações do Windows criar](https://docs.microsoft.com/sccm/apps/get-started/creating-windows-applications).
        - **Token de inscrição de aplicações**
        - **ficheiro. pfx**
        - **Nenhum** se utilizar um certificado da Symantec, pode especificar **mostrar um alerta antes de certificados da Symantec expirarem**.
4. Clique em **OK** para fechar a caixa de diálogo.  Para simplificar o processo de inscrição através do Portal da empresa, deve criar um alias de DNS para a inscrição de dispositivos. Em seguida, pode informar utilizadores como inscrever os respetivos dispositivos.

## <a name="choose-how-to-enroll-windows-devices"></a>Escolha como inscrever dispositivos Windows

Assim que atribuiu licenças do Intune aos utilizadores, é possível inscrever dispositivos Windows sem quaisquer passos adicionais, mas pode facilitar a inscrição para utilizadores.

Dois fatores determinam como é possível simplificar a inscrição de dispositivos do Windows:
- **Utiliza o Azure Active Directory Premium?** <br>[Azure AD Premium](https://docs.microsoft.com/azure/active-directory/active-directory-get-started-premium) incluída com o Enterprise Mobility + segurança e outros planos de licenciamento.
- **Quais as versões de clientes Windows irão inscrever?** <br>Dispositivos Windows 10 podem inscrever automaticamente ao adicionar uma conta escolar ou profissional. Versões anteriores têm de estar inscritos utilizando a aplicação do Portal da empresa.

||**Azure AD Premium**|**Outra AD**|
|----------|---------------|---------------|  
|**Windows 10**|[Inscrição automática](#enable-windows-10-automatic-enrollment) |[Inscrição de utilizadores](#enable-windows-enrollment-without-azure-ad-premium)|
|**Versões anteriores do Windows**|[Inscrição de utilizadores](#enable-windows-enrollment-without-azure-ad-premium)|[Inscrição de utilizadores](#enable-windows-enrollment-without-azure-ad-premium)|

## <a name="enable-windows-10-automatic-enrollment"></a>Ativar a inscrição automática do Windows 10

Inscrição automática permite aos utilizadores inscrever pertencentes à empresa ou pessoais PCs do Windows 10 e Windows 10 dispositivos móveis no Intune ao adicionar uma conta escolar ou profissional e aceita para serem geridos. Simples que. Em segundo plano, o dispositivo do utilizador regista e associa o Azure Active Directory. Depois de registada, o dispositivo for gerido com o Intune.

**Pré-requisitos**
- Subscrição do Azure Active Directory Premium ([subscrição de avaliação](http://go.microsoft.com/fwlink/?LinkID=816845))
- Subscrição do Microsoft Intune


### <a name="configure-automatic-mdm-enrollment"></a>Configurar a inscrição automática do MDM

1. Início de sessão para o [portal de gestão do Azure](https://portal.azure.com) (https://manage.windowsazure.com) e selecione **do Azure Active Directory**.

  ![Captura de ecrã do portal do Azure](../media/auto-enroll-azure-main.png)

2. Selecione **mobilidade (MDM e MAM)**.

  ![Captura de ecrã do portal do Azure](../media/auto-enroll-mdm.png)

3. Selecione **do Microsoft Intune**.

  ![Captura de ecrã do portal do Azure](../media/auto-enroll-intune.png)

4. Configurar **âmbito do utilizador de MDM**. Especifique os dispositivos dos utilizadores que deviam ser geridos pelo Microsoft Intune. Dispositivos do Windows 10 destes utilizadores serão automaticamente inscrito para gestão com o Microsoft Intune.

    - **Nenhum**
    - **Alguns**
    - **Todos os**

   ![Captura de ecrã do portal do Azure](../media/auto-enroll-scope.png)

5. Utilize os valores predefinidos para os seguintes URLs:
    - **MDM URL de termos de utilização**
    - **URL de deteção MDM**
    - **URL de compatibilidade de MDM**

6. Selecione **guardar**.


Por predefinição, a autenticação de dois fatores não está ativada para o serviço. No entanto, é recomendada autenticação de dois fatores ao registar um dispositivo. Antes que requerem a autenticação de dois fatores para este serviço, tem de configurar um fornecedor de autenticação de dois fatores no Azure Active Directory e configurar as contas de utilizador para a autenticação multifator. Consulte o artigo [começar a trabalhar com o servidor do Azure multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-cloud).

## <a name="enable-windows-enrollment-without-azure-ad-premium"></a>Ativar a inscrição do Windows sem Azure AD Premium
Pode permitir que os utilizadores inscrevam os respetivos dispositivos sem inscrição automática do Azure AD Premium. Depois de atribuir licenças, os utilizadores podem inscrever depois de adicionar a respetiva conta do trabalho para os respetivos dispositivos pessoais ou participar os respetivos dispositivos pertencentes ao seu Azure AD. Criar um DNS alias (tipo de registo CNAME) torna mais fácil para os utilizadores inscrevam os respetivos dispositivos. Se criar DNS CNAME registos de recursos, os utilizadores ligarem e inscrevam no Intune sem ser necessário introduzir o nome do servidor do Intune.

### <a name="create-cnames-to-simplify-enrollment"></a>Criar CNAMEs para simplificar a inscrição
Crie CNAME DNS registos de recursos de domínio da sua empresa. Por exemplo, se o site da sua empresa fosse contoso.com, criaria um CNAME no DNS que redirecione EnterpriseEnrollment.contoso.com para enterpriseenrollment s.manage.microsoft.com.

Apesar de a criar CNAME DNS entradas é opcional, registos CNAME facilitam a inscrição para utilizadores. Não se for encontrada nenhuma inscrição registo CNAME, os utilizadores recebem um pedido para introduzir manualmente o nome do servidor MDM, enrollment.manage.microsoft.com.

|Tipo|Nome do anfitrião|Aponta para|TTL|  
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.dominio_da_empresa.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 hora|

Se tiver mais do que um sufixo UPN, terá de criar um CNAME para cada nome de domínio e de pontos de cada um para EnterpriseEnrollment s.manage.microsoft.com. Por exemplo, se os utilizadores na Contoso utilizar name@contoso.com, mas também utilizar name@us.contoso.com, e name@eu.constoso.com como respetivo e-mail/UPN, é necessário criar os seguinte CNAMEs o administrador de DNS da Contoso.

|Tipo|Nome do anfitrião|Aponta para|TTL|  
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 hora|
|CNAME|EnterpriseEnrollment.us.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 hora|
|CNAME|EnterpriseEnrollment.eu.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 hora|

`EnterpriseEnrollment-s.manage.microsoft.com`– Suporta o redirecionamento para o serviço Intune com reconhecimento de domínio a partir do nome de domínio do e-mail

Alterações aos registos DNS poderão demorar até 72 horas a propagar. Não é possível verificar a alteração DNS no Intune até propaga o registo DNS.

## <a name="tell-users-how-to-enroll-devices"></a>Informar utilizadores como inscrever dispositivos  

 Assim que estiver configurado, terá de informar os utilizadores como inscrever os respetivos dispositivos. Consulte o artigo [o que dizer aos utilizadores sobre como inscrever os respetivos dispositivos](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune) para obter orientações sobre. Pode direcionar os utilizadores [inscrever o seu dispositivo Windows no Intune](https://docs.microsoft.com/intune/enduser/enroll-your-device-in-intune-windows). Estas informações aplicam-se ao Microsoft Intune e aos dispositivos móveis geridos pelo Configuration Manager.

> [!div class="button"]
[< Passo anterior](create-service-connection-point.md)[junto passo >  ](set-up-additional-management.md)

