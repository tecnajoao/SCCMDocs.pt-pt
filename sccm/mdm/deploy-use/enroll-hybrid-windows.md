---
title: Configurar a gestão de dispositivos Windows híbrida com o Microsoft Intune
titleSuffix: Configuration Manager
description: Configure a gestão de dispositivos do Windows com o System Center Configuration Manager e o Microsoft Intune.
ms.date: 03/17/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: dc1f70f5-64ab-42ab-aa91-d3858803e12f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 26529460498d10fb4ee747059ca050cd6af9db54
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53415964"
---
# <a name="set-up-windows-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurar a gestão de dispositivos híbridos do Windows com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este tópico informa os administradores de TI como eles podem permitir que os utilizadores trazer Windows PCs e dispositivos móveis para gestão com o Configuration Manager e o Microsoft Intune.

## <a name="enable-windows-device-management"></a>Ativar a gestão de dispositivos do Windows
Para ativar a gestão de dispositivos do Windows para PCs ou dispositivos móveis, utilize os seguintes passos:

1. Antes de configurar a inscrição para qualquer plataforma, conclua os pré-requisitos e procedimentos [mm híbrida do programa de configuração](setup-hybrid-mdm.md).  
2. Na consola do Configuration Manager nos **administração** área de trabalho, aceda a **descrição geral** > **serviços Cloud**  >   **Subscrições do Microsoft Intune**.  
3. No Friso, clique em **configurar plataformas**e, em seguida, selecione a plataforma do Windows:
   - **Windows** para Windows PCs e computadores portáteis, em seguida, execute os seguintes passos:
     1. Na **gerais** separador, clique no **inscrição de Windows ativar** caixa de verificação.
     2. Se utilizar um certificado para assinar com código e implementar a aplicação Portal da empresa, navegue para o **certificado de assinatura de código**. Os utilizadores de dispositivos também podem instalar a aplicação Portal da empresa a partir da Microsoft Store, ou pode implementar a aplicação a partir da Microsoft Store para empresas sem assinatura de código.
     3. Também pode configurar [Windows Hello para empresas](windows-hello-for-business-settings.md).
   - **Windows Phone** para telemóveis Windows e tablets, em seguida, execute os seguintes passos:
     1. Na **gerais** separador, clique nas **Windows Phone 8.1 e Windows 10 Mobile** caixa de verificação. Windows Phone 8.0 já não é suportada.
     2. Se sua organização precisa de fazer sideload de aplicativos da empresa, pode carregar o token solicitado ou o ficheiro. Para obter mais informações sobre as aplicações de sideload, consulte [aplicações do Windows criar](https://docs.microsoft.com/sccm/apps/get-started/creating-windows-applications).
        - **Token de inscrição de aplicações**
        - **ficheiro. pfx**
        - **NONE** se utilizar um certificado da Symantec, pode especificar **mostrar um alerta antes de expirarem certificados da Symantec**.
4. Clique em **OK** para fechar a caixa de diálogo.  Para simplificar o processo de inscrição com o Portal da empresa, deve criar um alias de DNS para inscrição de dispositivos. Pode, em seguida, informar os utilizadores como devem inscrever os dispositivos.

## <a name="choose-how-to-enroll-windows-devices"></a>Escolher como inscrever dispositivos Windows

Uma vez que atribuiu licenças do Intune aos utilizadores, dispositivos Windows podem ser inscritos sem passos adicionais, mas pode facilitar a inscrição para os utilizadores.

Dois fatores determinam como pode simplificar a inscrição de dispositivos do Windows:
- **Utiliza o Azure Active Directory Premium?** <br>O [Azure AD Premium](https://docs.microsoft.com/azure/active-directory/active-directory-get-started-premium) está incluído com o Enterprise Mobility + Security e outros planos de licenciamento.
- **Que versões de clientes do Windows serão inscritas?** <br>Os dispositivos Windows 10 podem ser inscritos automaticamente ao adicionar uma conta escolar ou profissional. As versões anteriores têm de ser inscritas através da aplicação Portal da Empresa.

||**Azure AD Premium**|**Outros AD**|
|----------|---------------|---------------|  
|**Windows 10**|[Inscrição automática](#enable-windows-10-automatic-enrollment) |[Inscrição de utilizadores](#enable-windows-enrollment-without-azure-ad-premium)|
|**Versões do Windows anteriores**|[Inscrição de utilizadores](#enable-windows-enrollment-without-azure-ad-premium)|[Inscrição do utilizador](#enable-windows-enrollment-without-azure-ad-premium)|

## <a name="enable-windows-10-automatic-enrollment"></a>Ativar a inscrição automática do Windows 10

A inscrição automática permite aos utilizadores inscrever pertencentes à empresa ou pessoais Windows 10 PCs e Windows 10 dispositivos móveis no Intune ao adicionar uma conta escolar ou profissional e aceitar que sejam geridos. Simples assim. Em segundo plano, o dispositivo do utilizador regista e associa o Azure Active Directory. Depois de registado, o dispositivo é gerido com o Intune.

**Pré-requisitos
- Subscrição do Azure Active Directory Premium ([subscrição de avaliação](http://go.microsoft.com/fwlink/?LinkID=816845))
- Subscrição do Microsoft Intune


### <a name="configure-automatic-mdm-enrollment"></a>Configurar a inscrição MDM automática

1. Iniciar sessão para o [portal de gestão do Azure](https://portal.azure.com) (https://manage.windowsazure.com) e selecione **do Azure Active Directory**.

   ![Captura de ecrã do portal do Azure](../media/auto-enroll-azure-main.png)

2. Selecione **Mobilidade (MDM e MAM)**.

   ![Captura de ecrã do portal do Azure](../media/auto-enroll-mdm.png)

3. Selecione **Microsoft Intune**.

   ![Captura de ecrã do portal do Azure](../media/auto-enroll-intune.png)

4. Configurar **âmbito do utilizador MDM**. Especifique dispositivos de utilizadores que devem ser geridos pelo Microsoft Intune. Dispositivos do Windows 10 dos utilizadores, estes serão automaticamente inscritos para gestão com o Microsoft Intune.

    - **Nenhum**
    - **Alguns**
    - **Todos**

   ![Captura de ecrã do portal do Azure](../media/auto-enroll-scope.png)

5. Utilize os valores predefinidos para os seguintes URLs:
    - **URL dos Termos de utilização de MDM**
    - **URL de Deteção de MDM**
    - **URL de Conformidade de MDM**

6. Selecione **Guardar**.


Por predefinição, a autenticação de dois fatores não está ativada para o serviço. No entanto, a autenticação de dois fatores recomenda ao registar um dispositivo. Antes de exigir a autenticação de dois fatores para este serviço, tem de configurar um fornecedor de autenticação de dois fatores no Azure Active Directory e configurar as contas de utilizador para a autenticação multifator. Ver [guia de introdução do servidor de multi-factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-cloud).

## <a name="enable-windows-enrollment-without-azure-ad-premium"></a>Ativar a inscrição do Windows sem o Azure AD Premium
Pode permitir que os utilizadores inscrevam os respetivos dispositivos sem a inscrição automática do Azure AD Premium. Após atribuir licenças, os utilizadores podem inscrever-se depois de adicionar a conta profissional aos seus dispositivos pessoais ou de associarem os dispositivos pertencentes à empresa com o Azure AD. Criar um DNS alias (tipo de registo CNAME) torna mais fácil para os utilizadores inscrever os respetivos dispositivos. Se criar registos de recursos a DNS CNAME, os utilizadores ligar-se e se inscrever no Intune sem ter de introduzir o nome de servidor do Intune.

### <a name="create-cnames-to-simplify-enrollment"></a>Criar CNAMEs para simplificar a inscrição
Crie registos de recursos DNS CNAME para o domínio da sua empresa. Por exemplo, se o site da sua empresa for contoso.com, deverá criar um CNAME no DNS para redirecionar EnterpriseEnrollment.contoso.com para enterpriseenrollment-s.manage.microsoft.com.

Apesar de a criação de entradas DNS CNAME ser opcional, os registos CNAME facilitam a inscrição para os utilizadores. Se não for encontrado nenhum registo CNAME de inscrição, os utilizadores receberão um pedido para introduzir manualmente o nome do servidor MDM, enrollment.manage.microsoft.com.

|Type|Nome do anfitrião|Aponta para|TTL|  
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.dominio_da_empresa.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 hora|

Se tiver mais do que um sufixo UPN, terá de criar um CNAME para cada nome de domínio e apontar cada um para enterpriseenrollment-s.Manage.microsoft.com. Por exemplo, se os utilizadores na Contoso utilizarem name@contoso.com, mas também usar name@us.contoso.com, e name@eu.constoso.com como e-mail/UPN, o administrador de DNS da Contoso seria necessário criar os seguintes CNAMEs.

|Type|Nome do anfitrião|Aponta para|TTL|  
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 hora|
|CNAME|EnterpriseEnrollment.us.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 hora|
|CNAME|EnterpriseEnrollment.eu.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 hora|

`EnterpriseEnrollment-s.manage.microsoft.com` – suporta o redirecionamento para o serviço Intune com reconhecimento de domínio a partir do nome de domínio do e-mail

As alterações aos registos DNS podem demorar até 72 horas a serem propagadas. Não é possível verificar a alteração DNS no Intune até que o registo DNS ser propagado.

## <a name="tell-users-how-to-enroll-devices"></a>Informar os utilizadores sobre como inscrever dispositivos  

 Assim que estiver configurado, terá de informar os utilizadores como inscrever os respetivos dispositivos. Ver [o que dizer aos utilizadores sobre como inscrever os respetivos dispositivos](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune) para obter orientações. Pode direcionar os utilizadores [inscrever o seu dispositivo Windows no Intune](https://docs.microsoft.com/intune/enduser/enroll-your-device-in-intune-windows). Estas informações aplicam-se ao Microsoft Intune e aos dispositivos móveis geridos pelo Configuration Manager.

> [!div class="button"]
> [< Anterior passo](create-service-connection-point.md)[passo seguinte >  ](set-up-additional-management.md)
