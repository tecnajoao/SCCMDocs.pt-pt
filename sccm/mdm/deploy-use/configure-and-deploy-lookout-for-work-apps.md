---
title: Implementar o Lookout for Work aplicação
titleSuffix: Configuration Manager
description: Configurar e implementar o Lookout for Work aplicações.
ms.date: 05/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 3f62b763-4347-453d-b0a7-1f4a0d1d4105
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 00fa7e538f6156f0dacee00feeb4b767a3c83a5c
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53417630"
---
# <a name="configure-and-deploy-lookout-for-work-apps"></a>Configurar e implementar o Lookout for Work aplicações

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo explica como configurar e implementar o Lookout for Work de aplicação para dispositivos Android e iOS.



## <a name="android-google-play-store-app"></a>Android (aplicação da loja Google Play)
1.  Na consola do Configuration Manager, clique em **biblioteca de Software** > **gestão de aplicações** > **aplicativos**.  

2.  Na página **Geral** do Assistente de Implementação de Software, especifique as seguintes informações:  
    - Tipo: selecione **pacote de aplicação para Android no Google Play**.
    - Localização: copiar o Lookout for work ligação da aplicação da loja Google Play, cole-o aqui
    - Publicador: Segurança móvel do lookout
    - Nome: Lookout for Work
    - Descrição: Lookout oferece a melhor proteção contra ameaças contra dispositivos móveis para manter o seu dispositivo seguro. Quando a aplicação Lookout está instalada, a aplicação protege o seu dispositivo de ameaças. Se forem detetadas ameaças, alerta-o e o administrador de TI.
    - Categoria administrativa: Gestão de computadores  

    Após a conclusão com êxito, verá o Lookout for Work a aplicação na sua lista de aplicações.  

3.  Na **home page** separador a **implantação** de grupo, escolha **implementar** para implementar o Lookout for Work aplicação aos utilizadores.   
    >[!IMPORTANT]  
    >Tem de selecionar os mesmos utilizadores adicionados na opção de gestão de inscrições na consola do Lookout MTP.  

    Escolha o **instalação necessária** opção. Esta opção requer que a aplicação Lookout para instalar no dispositivo do utilizador.  



## <a name="ios-enterprise-signed-version-of-lookout-app"></a>iOS (versão enterprise da aplicação Lookout)

1. Certifique-se de gestão de iOS está configurada nos seus dispositivos. Para obter instruções sobre como configurar o seu dispositivo para gestão de iOS, veja [configurar a gestão de dispositivos Mac e iOS](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac).  

2. Voltar a assinar o Lookout for Work iOS app. Lookout distribui o Lookout for Work iOS app fora da iOS App Store. Antes de distribuir a aplicação, deve voltar a assinar a aplicação com o seu iOS Enterprise Developer Certificate. Para obter instruções detalhadas voltar a assinar o Lookout for Work iOS aplicações, consulte [Lookout for Work iOS aplicação voltar a assinar processo](https://personal.support.lookout.com/hc/articles/114094038714) no site da Lookout.  

3. Ative a autenticação do Azure Active Directory (Azure AD) para os utilizadores do iOS.
   1.  Inicie sessão para o [painel do Azure AD do portal do Azure](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)e navegue para a página de registos de aplicações.  
   2.  Especifique o nome como **Lookout for Work iOS app**e selecione **nativo** como o tipo de aplicação.  
   ![captura de ecrã da caixa de diálogo de aplicações adicionar que mostra o cliente nativo a opção de aplicação](media/aad-add-app-reg.png)

   3.  Para este URI de redirecionamento, utilize o seguinte formato: `lookoutwork://com.lookout.enterprise.<yourcompanyname>`, substituindo `<yourcompanyname>` com o nome da sua empresa. Por exemplo: `lookoutwork://com.lookout.enterprise.contoso`
   4. Clique em **criar** para criar a aplicação. 
   5.  Abra a nova aplicação, clique em **definições**, e adicione um URI de redirecionamento adicional. Utilize o seguinte formato: `companyportal://code/<originalURI>`, onde `<originalURI>` é uma versão com codificação URL do seu URI de redirecionamento original. Por exemplo, `companyportal://code/lookoutwork%3A%2F%2Fcom.lookout.enterprise.contoso`
   6.  Nas definições da aplicação, aceda a **permissões obrigatórias** e clique em **Add**. Selecione as seguintes permissões de delegado:  

       | API  | Permissão  |
       |---------|---------|
       | Lookout MTP     | Aceder ao Lookout MTP         |
       | Microsoft Graph     | Iniciar sessão e ler o perfil de utilizador        |  

   Para obter mais informações, consulte [configurar uma aplicação cliente nativa](/azure/app-service/app-service-mobile-how-to-configure-active-directory-authentication#optional-configure-a-native-client-application).  


4. No Configuration Manager, carregue o ficheiro. IPA assinado novamente. Defina a versão mínima do SO para o iOS 8.0 ou posterior. Para obter mais informações, consulte [criar aplicações iOS](/sccm/apps/get-started/creating-ios-applications).   


5. Crie a política de configuração de aplicações geridas. Para obter mais informações, consulte [configurar aplicações iOS com políticas de configuração de aplicações móveis](/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies).  


6. Implemente o Lookout for Work aplicação aos utilizadores. Para obter mais informações, consulte [implementar aplicações](/sccm/apps/deploy-use/deploy-applications).  

   Selecione os mesmos utilizadores que foram adicionados à opção gestão de inscrições na consola do Lookout. Escolha o **instalação necessária** opção. Esta opção requer que a aplicação Lookout para instalar no dispositivo do utilizador.



## <a name="what-happens-when-the-deployed-app-is-opened-on-the-device"></a>O que acontece quando a aplicação implementada é aberta no dispositivo

Quando o utilizador abre o Lookout for Work no dispositivo, ele lhe pede para ativar a aplicação. Eles devem optar por iniciar sessão com a opção do Azure AD. Instruções detalhadas sobre o fluxo do utilizador final é nos seguintes artigos:

- [Lhe for pedido para instalar o Lookout for Work no seu dispositivo Android](/intune-user-help/you-are-prompted-to-install-lookout-for-work-android)

- [Tem de resolver uma ameaça que o Lookout for Work encontrou no seu dispositivo Android](/intune-user-help/you-need-to-resolve-a-threat-found-by-lookout-for-work-android)



## <a name="next-steps"></a>Passos seguintes
- [Ativar a regra de proteção contra ameaças de dispositivo na política de conformidade](enable-device-threat-protection-rule-compliance-policy.md)
