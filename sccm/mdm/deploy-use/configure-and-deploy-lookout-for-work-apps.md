---
title: Implementar o Lookout para a aplicação de trabalho
titleSuffix: Configuration Manager
description: Configurar e implementar o Lookout para aplicações de trabalho.
ms.date: 05/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 3f62b763-4347-453d-b0a7-1f4a0d1d4105
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 87ad7a768128cb11a1fc361c90a6eccac454a28c
ms.sourcegitcommit: 9cff0702c2cc0f214173b47ec241f7e5a40f84e6
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 06/04/2018
ms.locfileid: "34752595"
---
# <a name="configure-and-deploy-lookout-for-work-apps"></a>Configure e implemente o Lookout para aplicações de trabalho

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo explica como configurar e implementar o Lookout para aplicação de trabalho para dispositivos Android e iOS.



## <a name="android-google-play-store-app"></a>Android (aplicação da loja Google Play)
1.  Na consola do Configuration Manager, clique em **biblioteca de Software** > **gestão de aplicações** > **aplicações**.  

2.  Na página **Geral** do Assistente de Implementação de Software, especifique as seguintes informações:  
    - Tipo: selecione **pacote de aplicação para Android no Google Play**.
    - Localização: copiar o Lookout for work ligação da aplicação da loja do Google Play, cole-o aqui
    - Publisher: Segurança móvel lookout
    - Nome: Lookout for Work
    - Descrição: Lookout oferece a melhor proteção contra ameaças móveis para manter o seu dispositivo seguro. Quando a aplicação de Lookout for instalada, a aplicação protege os dispositivos contra ameaças. Se encontrar qualquer ameaças, alertas e o administrador de TI.
    - Categoria administrativa: Gestão de computadores  

    Após a conclusão com êxito, verá o Lookout para a aplicação de trabalho na sua lista de aplicações.  

3.  No **home page** separador o **implementação** grupo, escolha **implementar** para implementar o Lookout for Work aplicações em utilizadores.   
    >[!IMPORTANT]  
    >Tem de selecionar os mesmos utilizadores que adicionou para a opção de gestão de inscrição na consola do Lookout MTP.  

    Escolha o **instalação necessária** opção. Esta opção requer que a aplicação de Lookout para instalar no dispositivo do utilizador.  



## <a name="ios-enterprise-signed-version-of-lookout-app"></a>iOS (versão enterprise-assinado da aplicação Lookout)

1. Certifique-se a gestão de iOS é definida nos seus dispositivos. Para obter instruções sobre como configurar o seu dispositivo para gestão de iOS, consulte [configurar a gestão iOS e Mac dispositivo](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac).  

2. Voltar a assinar o Lookout for Work aplicação para iOS. Lookout distribui o Lookout for Work iOS aplicações fora da iOS App Store. Antes de distribuir a aplicação, tem de assinar novamente a aplicação com o seu certificado empresarial de Programador de iOS. Para obter instruções detalhadas voltar a assinar o Lookout para aplicações de iOS de trabalho, consulte [Lookout trabalho para aplicação para iOS voltar a assinar processo](https://personal.support.lookout.com/hc/articles/114094038714) no Lookout site.  

3. Ative a autenticação do Azure Active Directory (Azure AD) para os utilizadores do iOS.
   1.  Iniciar sessão para o [painel do Azure AD do portal do Azure](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)e navegue para a página de registos de aplicação.  
   2.  Especifique o nome como **Lookout for Work iOS app**e selecione **nativo** como o tipo de aplicação.  
  ![captura de ecrã da caixa de diálogo de aplicações adicionar que mostra o native client a opção de aplicação](media/aad-add-app-reg.png)

   3.  Para este URI de redirecionamento, utilize o seguinte formato: `lookoutwork://com.lookout.enterprise.<yourcompanyname>`, substituindo `<yourcompanyname>` com o nome da sua empresa. Por exemplo: `lookoutwork://com.lookout.enterprise.contoso`
   4. Clique em **criar** para criar a aplicação. 
   5.  Abra a nova aplicação, clique em **definições**, e adicione um URI de redirecionamento adicionais. Utilize o seguinte formato: `companyportal://code/<originalURI>`, onde `<originalURI>` é uma versão com codificação URL do seu URI de redirecionamento original. Por exemplo, `companyportal://code/lookoutwork%3A%2F%2Fcom.lookout.enterprise.contoso`
   6.  Nas definições da aplicação, aceda a **as permissões necessárias** e clique em **adicionar**. Selecione as seguintes permissões delegadas:  

       | API  | Permissão  |
       |---------|---------|
       | Lookout MTP     | Acesso Lookout MTP         |
       | Microsoft Graph     | A iniciar sessão e ler o perfil de utilizador        |  

   Para obter mais informações, consulte [configurar uma aplicação cliente nativa](/azure/app-service/app-service-mobile-how-to-configure-active-directory-authentication#optional-configure-a-native-client-application).  


4. No Configuration Manager, carregue o ficheiro de reassinada. IPA. Defina a versão mínima do SO para o iOS 8.0 ou posterior. Para obter mais informações, consulte [criar aplicações iOS](/sccm/apps/get-started/creating-ios-applications).   


5. Crie a política de configuração de aplicação gerida. Para obter mais informações, consulte [configurar aplicações iOS com políticas de configuração de aplicação móvel](/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies).  


6. Implemente o Lookout for Work aplicação aos utilizadores. Para obter mais informações, consulte [implementar aplicações](/sccm/apps/deploy-use/deploy-applications).  

  Selecione os mesmos utilizadores que foram adicionados para a opção de gestão de inscrição na consola do Lookout. Escolha o **instalação necessária** opção. Esta opção requer que a aplicação de Lookout para instalar no dispositivo do utilizador.



## <a name="what-happens-when-the-deployed-app-is-opened-on-the-device"></a>O que acontece quando a aplicação implementada é aberta no dispositivo

Quando o utilizador abre o Lookout for Work no dispositivo, solicita-lhe-los para ativar a aplicação. Deve escolherem para iniciar sessão com a opção do Azure AD. Instruções detalhadas sobre o fluxo de utilizador final é nos seguintes artigos:

- [É-lhe pedido que instale o Lookout for Work no seu dispositivo Android](/intune-user-help/you-are-prompted-to-install-lookout-for-work-android)

- [É necessário resolver uma ameaça que Lookout for Work, foi encontrado no seu dispositivo Android](/intune-user-help/you-need-to-resolve-a-threat-found-by-lookout-for-work-android)



## <a name="next-steps"></a>Passos seguintes
- [Ativar regra de proteção de ameaça do dispositivo na política de conformidade](enable-device-threat-protection-rule-compliance-policy.md)
