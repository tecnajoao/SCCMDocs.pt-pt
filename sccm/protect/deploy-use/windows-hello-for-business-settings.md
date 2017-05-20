---
title: "Windows Hello para definições de empresas | Documentos do Microsoft"
description: Saiba como integrar o Windows Hello para empresas com o System Center Configuration Manager.
ms.custom: na
ms.date: 04/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a95bc292-af10-4beb-ab56-2a815fc69304
caps.latest.revision: 17
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 699b79b68440b61904a9053e5004318a2a248bfd
ms.openlocfilehash: 75def95561feb35f2f060f0daa72291983324d4f
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="windows-hello-for-business-settings-in-system-center-configuration-manager"></a>Definições do Windows Hello para Empresas no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager permite-lhe integrar com o Windows Hello para empresas (anteriormente Microsoft Passport para Windows), que é um método alternativo início de sessão para dispositivos Windows 10. O Hello para Empresas utiliza o Active Directory ou uma conta do Azure Active Directory para substituir uma palavra-passe, um smart card ou um smart card virtual.  

Com o Hello para Empresas, pode utilizar um **gesto de utilizador** para iniciar sessão, em vez de uma palavra-passe. Um gesto de utilizador pode ser um PIN simples, uma autenticação biométrica ou um dispositivo externo, como um leitor de impressões digitais.

[Saiba mais sobre o Windows Hello para empresas](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-identity-verification)

 O Configuration Manager é integrada com o Windows Hello para empresas de duas formas:  

-   Pode utilizar o Configuration Manager para controlar que utilizadores de gestos podem e não podem utilizar para iniciar sessão.  

-   Pode armazenar certificados de autenticação no fornecedor de armazenamento de chaves (KSP) do Windows Hello para Empresas. Para obter mais informações, consulte o artigo [perfis de certificado](introduction-to-certificate-profiles.md).  

- Pode implementar o Windows Hello para as políticas de negócio para dispositivos Windows 10 associados a um domínio, que executam o cliente do Configuration Manager. Esta configuração é descrita no [configurar Windows Hello para empresas em dispositivos Windows 10 associados a domínios](#configure-windows-hello-for-business-on-domain-joined-windows-10-devices), abaixo. Quando estiver a utilizar o Configuration Manager com o Intune (híbrido), pode configurar estas definições em dispositivos Windows 10 Mobile e Windows 10, mas não no dispositivos associados a um domínio que executam o cliente do Configuration Manager. Consulte o artigo [configurar Windows Hello para empresas definições (híbrido)](../../mdm/deploy-use/windows-hello-for-business-settings.md) para obter mais informações.

## <a name="configure-windows-hello-for-business-on-domain-joined-windows-10-devices"></a>Configurar o Windows Hello para empresas no associados a um domínio dispositivos Windows 10
Pode controlar o Windows Hello para definições de negócios nos dispositivos Windows 10 associados a um domínio três formas:

- Pode criar e implementar um Windows Hello do perfil de negócio. Esta é a abordagem recomendada.
- Pode utilizar a política de grupo.  
- Pode utilizar um script do PowerShell.

Tenha em atenção que, além desta configuração, tem também de implementar um perfil de certificado, conforme descrito em [configurar um perfil de certificado](#configure-a-certificate-profile).

## <a name="configure-a-windows-hello-for-business-profile"></a>Configurar um Windows Hello do perfil de negócio  

Na consola do Configuration Manager, sob **acesso a recursos da empresa**, com o botão direito **Windows Hello para perfis de empresas** e escolha **novo** para iniciar o Assistente do perfil. Forneça as definições do pedido pelo assistente, reveja e confirme as definições na última página e clique em **fechar**. Eis um exemplo de que as suas definições poderão ser semelhante a:  

![Definições do Windows Hello para Empresas](../media/Hello-for-Business-settings.png)

## <a name="configure-windows-hello-for-business-with-group-policy-in-active-directory"></a>Configurar o Windows Hello para empresas com a política de grupo no Active Directory  

Pode utilizar uma política de grupo do Active Directory para configurar os dispositivos Windows 10 associados a um domínio para aprovisionar utilizador Olá para credenciais de negócio quando um utilizador iniciar sessão para o Windows:

1.  Num computador Windows Server, abra o Gestor de servidor e navegue para **ferramentas** > **gestão de políticas de grupo**.    

2.  No **gestão de políticas de grupo** diálogo caixa, expanda o domínio no qual pretende ativar automática associação.    

3.  Com o botão direito **objetos de política de grupo**e, em seguida, clique em **novo**.  

4.  No **novo GPO** diálogo caixa, introduza um nome para o novo objeto de política de grupo, como **ativar Windows Hello para empresas**e, em seguida, clique em **OK**.  

5.  No **objetos de política de grupo** nó, o objeto que acaba de contexto criado e, em seguida, clique em **editar**.  

6.  No **Editor de gestão de política de grupo** diálogo caixa, navegue até à **configuração do computador** > **políticas** > **modelos administrativos** > **componentes do Windows** > **Windows Hello para empresas**.  

7.  Com o botão direito **ativar Windows Hello para empresas** e, em seguida, clique em **editar**.   

8.  Selecione **ativado**, clique em **aplicar**e, em seguida, clique em **OK**.

Agora pode ligar o objeto de política de grupo que acabou de criar para uma localização da sua preferência. Por exemplo:    

   Um específico unidade organizacional (UO) no AD em que os computadores associados a um domínio do Windows 10 ficará localizados.    

   Um grupo de segurança específicas que contém Windows 10 computadores associados a um domínio que serão registados automaticamente com o Azure AD.    

## <a name="configure-windows-hello-for-business-by-deploying-a-powershell-script-with-configuration-manager"></a>Configurar o Windows Hello para empresas através da implementação de um script do PowerShell com o Configuration Manager    
Pode criar e implementar o seguinte script do PowerShell, utilizando a gestão de aplicações do Configuration Manager.    

**PowerShell.exe - ExecutionPolicy omissão - NoLogo - NoProfile-comando "& {"HKLM:\Software\Policies\Microsoft\PassportForWork"nova ItemProperty-Name"activado"-"DWord"o valor de 1 - PropertyType-Force}" * * 

Para mais informações sobre a gestão de aplicações do Configuration Manager, consulte o artigo [introdução à gestão de aplicações no System Center Configuration Manager](/sccm/apps/understand/introduction-to-application-management).  

## <a name="configure-a-certificate-profile-to-enroll-the-windows-hello-for-business-enrollment-certificate-in-configuration-manager"></a>Configurar um perfil de certificado para inscrever o certificado de inscrição do Windows Hello para Empresas no Configuration Manager  
 Se quiser utilizar o início de sessão baseado em certificado do Windows Hello para Empresas ou o Microsoft Hello, configure o seguinte:  

-   Um perfil de certificado do Configuration Manager.  

-   No perfil de certificado, selecione um modelo que utilize a EKU de início de sessão do Smart Card.  

-    Se tenciona guardar os perfis de certificado no Windows Hello do contentor de chaves de negócio e utiliza o perfil de certificado a **início de sessão de Smart Card** EKU, tem de configurar as seguintes permissões para o registo de chave garantir que o certificado é validado corretamente.
Primeiro tem de ter criado o **chave administradores** agrupar e adicionado a gestão do Configuration Manager todos os computadores do ponto como membros a este grupo.

    1.    Início de sessão para um domínio ou gestão de controlador estações de trabalho com o administrador de domínio ou credenciais equivalentes.
    2.    Abrir **computadores e utilizadores do Active Directory**.
    3.    No painel de navegação, faça duplo clique o nome de domínio e, em seguida, clique em **propriedades**.
    4.    No **segurança** separador do  *<domain name>*  **propriedades** caixa de diálogo, clique em **avançadas**. Se o **segurança** separador não for apresentado, ative a funcionalidade **funcionalidades avançadas** a partir do **vista** menu de **utilizadores e Active Directory computadores**.
    5.    Clique em **Adicionar**.
    6.    No **entrada de permissão para**  *<domain name>*  caixa de diálogo, clique em **selecione um principal**.
    7.    No **Seleccionar utilizador, computador, conta de serviço ou grupo** caixa de diálogo, escreva **administradores de chave** no **introduza o nome de objeto para selecionar** caixa de texto.  Clique em **OK**.
    8.    A partir de **aplica-se a** lista, selecione **objetos de utilizador Descendant**.
    9.    Desloque para a parte inferior da página e clique em **Desmarcar tudo**.
    10.    No **propriedades** secção, selecione **ler msDS-KeyCredentialLink**.
    11.    Clique em **OK** três vezes para concluir a tarefa.


 Para obter mais informações, consulte o artigo [perfis de certificado](introduction-to-certificate-profiles.md).  





