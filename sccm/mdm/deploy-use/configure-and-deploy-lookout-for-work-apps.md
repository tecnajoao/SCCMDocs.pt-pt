---
title: Implementar o Lookout para a aplicação de trabalho
titleSuffix: Configuration Manager
description: Configurar e implementar o Lookout para aplicações de trabalho.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3f62b763-4347-453d-b0a7-1f4a0d1d4105
caps.latest.revision: ''
author: dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 01c388377948ab362d60951cb8398a9276e668fb
ms.sourcegitcommit: a19e12d5c3198764901d44f4df7c60eb542e765f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/28/2018
---
# <a name="configure-and-deploy-lookout-for-work-apps"></a>Configure e implemente o Lookout para aplicações de trabalho

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo explica como configurar e implementar o Lookout para aplicação de trabalho para dispositivos Android e iOS.

## <a name="android-google-play-store-app"></a>Android (aplicação loja do Google Play)
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

- **Passo 1:** Certifique-se **gestão de iOS** está configurado no seu dispositivo. Para obter instruções sobre como configurar o seu dispositivo para gestão de iOS, consulte [configurar a gestão iOS e Mac dispositivo](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac).

- **Passo 2:** **Voltar a assinar** o Lookout for Work aplicação para iOS. Lookout distribui o Lookout for Work iOS aplicações fora da iOS App Store. **Antes de distribuir a aplicação**, deve voltar a assinar a aplicação com o seu certificado empresarial de Programador de iOS. Para obter instruções detalhadas voltar a assinar o Lookout para aplicações de iOS de trabalho, consulte [Lookout trabalho para aplicação para iOS voltar a assinar processo](https://personal.support.lookout.com/hc/articles/114094038714) no Lookout site.


- **Passo 3:** Ative a autenticação do Azure Active Directory para os utilizadores do iOS efetuando os seguintes passos:
  1.  Inicie sessão no [portal de gestão do Azure Active Directory](https:/portal.azure.com)e navegue para a página da aplicação.
  2.  Adicionar o **Lookout for Work iOS app** como um **aplicação cliente nativa**.
  ![captura de ecrã da caixa de diálogo de aplicações adicionar que mostra o native client a opção de aplicação](media/aad-add-app.png)

  3. Substitua o **com.lookout.enterprise.yourcompanyname** com o cliente que selecionou quando se inscreveu o IPA de ID do pacote.
  4.  Adicionar URI de redirecionamento adicional:  **&lt;companyportal://code/ >** seguido por uma versão de URLencoded do seu URI de redirecionamento original.
  5.  Adicionar **permissões delegadas** à sua aplicação.

  Para obter mais informações, consulte [configurar uma aplicação cliente nativa](/azure/app-service/app-service-mobile-how-to-configure-active-directory-authentication#optional-configure-a-native-client-application).


- **Passo 4:** Carregar o ficheiro. IPA reassinada, conforme descrito no [criar aplicações iOS no System Center Configuration Manager tópico](/sccm/apps/get-started/creating-ios-applications) tópico. Defina a versão mínima do SO para o iOS 8.0 ou posterior.


- **Passo 5:** Criar a política de configuração de aplicação gerida, conforme descrito no [configurar aplicações iOS com políticas de configuração de aplicações móveis no System Center Configuration Manager](/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies) tópico.


- **Passo 6:** **Para implementar a aplicação aos utilizadores**, selecione o Lookout para a aplicação de trabalho no **aplicações** página, do **home page** separador o **implementação** grupo, escolha  **Implementar**.

  Selecione os mesmos utilizadores que foram adicionados para a opção de gestão de inscrição na consola do Lookout. Escolha o **instalação necessária** opção. Esta opção requer que a aplicação de Lookout para instalar no dispositivo do utilizador.



## <a name="what-happens-when-the-deployed-app-is-opened-on-the-device"></a>O que acontece quando a aplicação implementada é aberta no dispositivo

Quando o utilizador abre o Lookout for Work no dispositivo, solicita-lhe-los para ativar a aplicação. Deve escolherem para iniciar sessão com a opção do Azure Active Directory. Instruções detalhadas sobre o fluxo de utilizador final é nos seguintes artigos:

- [É-lhe pedido que instale o Lookout for Work no seu dispositivo Android](/intune-user-help/you-are-prompted-to-install-lookout-for-work-android)

- [É necessário resolver uma ameaça que Lookout for Work, foi encontrado no seu dispositivo Android](/intune-user-help/you-need-to-resolve-a-threat-found-by-lookout-for-work-android)



## <a name="next-steps"></a>Passos seguintes
- [Ativar regra de proteção de ameaça do dispositivo na política de conformidade](enable-device-threat-protection-rule-compliance-policy.md)
