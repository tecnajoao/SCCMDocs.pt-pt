---
title: "Implementar atento para a aplicação de trabalho | Documentos do Microsoft"
description: "Configurar e implementar atento para aplicações de trabalho."
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
caps.latest.revision: 
author: mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 6424fb07802b62820b4dc78a58ab30d3b956abef
ms.openlocfilehash: 59f43c922d1d3bc64625733014b0def1e42c4d2d
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="configure-and-deploy-lookout-for-work-apps"></a>Configure e implemente atento para aplicações de trabalho

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo explica como configurar e implementar o atento para a aplicação de trabalho para dispositivos Android e iOS.

## <a name="android-google-play-store-app"></a>Android (aplicação Google Play Store)
1.  Na consola do Configuration Manager, clique em **biblioteca de Software** > **gestão de aplicações** > **aplicações**.

2.  Na página **Geral** do Assistente de Implementação de Software, especifique as seguintes informações:
  * Tipo: selecione **pacote de aplicação para Android no Google Play**.
  * Localização: Copie atento a ligação de aplicações de trabalho a partir da Google Play store conforme colá-la aqui
  * Publisher: Segurança móveis atento
  * Nome: Atento trabalho
  * Descrição: Atento oferece a melhor proteção contra ameaças móveis para manter o seu dispositivo seguros. Quando a aplicação de atento estiver instalada no dispositivo, a aplicação protege o seu dispositivo de ameaças e emite um alerta e o seu administrador de empresa, caso algum seja localizado.
  * Categoria administrativa: Gestão de computadores

  Após a conclusão com êxito, poderá agora ver atento para a aplicação de trabalho na sua lista de aplicações.

3.  No **base** separador o **implementação** grupo, selecione **implementar** implementar atento para a aplicação de trabalho para os utilizadores.
>[!IMPORTANT]
>Tem de selecionar nos mesmos utilizadores adicionados para a opção de gestão de inscrição na consola do atento MTP.

  Escolha o **instalação necessária** opção para exigir que a aplicação de atento ser instalada no dispositivo do utilizador.

## <a name="ios-enterprise-signed-version-of-lookout-app"></a>iOS (assinado Enterprise versão da aplicação atento)

* **Passo 1:** Certifique-se **gestão de iOS** está configurado no seu dispositivo. Para obter instruções sobre como configurar o seu dispositivo para gestão de iOS, consulte o artigo [configurar o iOS e gestão de dispositivos de Mac]().

* **Passo 2:** **Voltar a assinar** atento a aplicação do iOS de trabalho. Atento distribui respetivo atento trabalho da aplicação do iOS fora iOS App Store. **Antes de distribuir a aplicação**, deve voltar a assinar a aplicação com o seu certificado empresarial de Programador de iOS. Para obter instruções detalhadas voltar a assinar atento trabalho para aplicações para iOS, consulte o artigo [atento novamente o processo de assinatura da aplicação do iOS trabalho](https://personal.support.lookout.com/hc/en-us/articles/114094038714) no site atento.


* **Passo 3:** Ative autenticação do Azure Active Directory para os utilizadores de iOS efetuando o seguinte procedimento:
  1.  Início de sessão para o [portal de gestão do Azure Active Directory](https://manage.windowsazure.com)e navegue para a página de aplicações.
  2.  Adicionar o **atento trabalho iOS app** como um **aplicação cliente nativo**.
  ![captura de ecrã da caixa de diálogo Adicionar aplicações a mostrar o native client a opção de aplicação](media/aad-add-app.png)

  3. Substituir o **com.lookout.enterprise.yourcompanyname** com o cliente que selecionou quando se inscreveu a IPA de ID do pacote.
  4.  Adicionar o URI de redirecionamento adicionais:  **&lt;companyportal://code/ >** seguido por uma versão de URLencoded do seu URI de redirecionamento original.
  5.  Adicionar **delegado permissões** para a sua aplicação.

  Para obter mais detalhes, consulte o artigo [configurar uma aplicação cliente nativo](https://azure.microsoft.com/en-us/documentation/articles/app-service-mobile-how-to-configure-active-directory-authentication/#optional-configure-a-native-client-application).


* **Passo 4:** Carregar o ficheiro. IPA assinado novamente, tal como descrito no [criar aplicações iOS no System Center Configuration Manager tópico](https://docs.microsoft.com/en-us/sccm/apps/get-started/creating-ios-applications) tópico. Defina a versão mínima do SO para iOS 8.0 ou posterior.


* **Passo 5:** Criar a política de configuração da aplicação gerida, tal como descrito no [configurar aplicações iOS com as políticas de configuração da aplicação móvel no System Center Configuration Manager](https://docs.microsoft.com/en-us/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies) tópico.


* **Passo 6:** **Para implementar a aplicação aos utilizadores**, selecione atento para aplicação de trabalho no **aplicações** página, a partir do **base** no separador de **implementação** grupo, selecione **implementar**.

  Tem de selecionar nos mesmos utilizadores que foram adicionados para a opção de gestão de inscrição na consola do atento.  
Escolha o **instalação necessária** opção para exigir que a aplicação de atento ser instalada no dispositivo do utilizador.

## <a name="what-happens-when-the-deployed-app-is-opened-on-the-device"></a>O que acontece quando a aplicação implementada é aberta no dispositivo




Quando o utilizador abre o atento para trabalhar no dispositivo são-lhe pedidos para ativar a aplicação e selecione o início de sessão com a opção do Azure Active Directory. Pode encontrar instruções detalhadas sobre com o fluxo do utilizador final nos seguintes tópicos:

* [Lhe for pedido para instalar atento para trabalhar no seu dispositivo Android](http://docs.microsoft.com/intune/enduser/you-are-prompted-to-install-lookout-for-work-android)

* [Para resolver uma ameaça que atento trabalho encontrado no seu dispositivo Android](http://docs.microsoft.com/intune/enduser/you-need-to-resolve-a-threat-found-by-lookout-for-work-android)

## <a name="next-steps"></a>Passos seguintes
* [Ativar regra de proteção de ameaça de dispositivo a política de conformidade](enable-device-threat-protection-rule-compliance-policy.md)

