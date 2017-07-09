---
title: "Configurar o gerenciamento de iOS e Mac híbrida dispositivo com o System Center Configuration Manager e o Microsoft Intune | Microsoft Docs"
description: Configure o gerenciamento de dispositivo do iOS com o System Center Configuration Manager e o Microsoft Intune.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5eae4400-58ca-4c71-804c-6a585cd3df5d
caps.latest.revision: 10
caps.handback.revision: 0
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: ed6b65a1a5aabc0970cd0333cb033405cf6d2aea
ms.openlocfilehash: 52596b211acb1182cb38259cba267bdd0846de80
ms.contentlocale: pt-pt
ms.lasthandoff: 07/03/2017


---
# <a name="set-up-ios-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurar a gestão de dispositivos iOS híbrida com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

Com o Configuration Manager e o Intune, você habilitar o registro de dispositivo iOS e macOS dar acesso ao email da empresa e recursos para usuários do Mac, iPhone e iPad. Assim que os utilizadores instalarem a aplicação do portal da empresa do Intune, os respetivos dispositivos podem ser visados pela política. Antes de poder gerir dispositivos iOS e Mac, tem de importar um certificado do serviço Apple Push Notification (APNs) da Apple. Este certificado permite que o Intune gerenciar dispositivos iOS e Mac, estabelecendo uma conexão com o serviço de gerenciamento de dispositivos da Apple.  

 Também pode inscrever dispositivos iOS pertencentes à empresa.  Consulte [registrar dispositivos da empresa](enroll-company-owned-devices.md).  

## <a name="enable-ios-device-enrollment"></a>Ativar a inscrição de dispositivos iOS  
 Para suportar a inscrição de dispositivos iOS, tem de seguir estes passos:  

#### <a name="set-up-ios-device-enrollment-in-configuration-manager"></a>Configurar a inscrição de dispositivos iOS no Configuration Manager  

1.  **Pré-requisitos** - antes de você configurar o registro para qualquer plataforma, conclua os pré-requisitos e procedimentos [MDM híbrido do programa de instalação](setup-hybrid-mdm.md).    

2.  **Baixar uma solicitação de assinatura de certificado** -um arquivo de solicitação de assinatura de certificado é necessário para solicitar um certificado APNs da Apple.  

    1.  Na consola do Configuration Manager, na área de trabalho **Administração** , aceda a **Serviços Cloud**> **Subscrições do Microsoft Intune**.  

    2.  No separador **Home Page** , clique em **Criar pedido de certificado do APNs**. É aberta a caixa de diálogo **Pedido de Assinatura de Certificado do Serviço Apple Push Notification** .  

    3.  **Procurar** até o caminho para salvar o novo arquivo de solicitação de assinatura de certificado. Salve o certificado de assinatura de arquivo de solicitação localmente.  

    4.  Clique em **Transferir**. A assinatura do Microsoft Intune certificado novo solicitar downloads de arquivo e é salvo pelo Configuration Manager. O arquivo de solicitação de assinatura de certificado é usado para solicitar um certificado de relação de confiança do Portal de certificados por Push da Apple.  

3.  **Pedir um certificado APNs da Apple** - O certificado do serviço Apple Push Notification (APNs) é utilizado para estabelecer uma relação de confiança entre o serviço de gestão, o Intune e os dispositivos móveis iOS inscritos.  

    1.  Num browser, aceda ao [Portal de Certificados Apple Push](http://go.microsoft.com/fwlink/?LinkId=269844) e inicie sessão com o ID Apple da sua empresa. Este ID Apple tem de ser utilizado no futuro para renovar o certificado APNs.  

    2.  Conclua o assistente utilizando o ficheiro de pedido de assinatura de certificado (.csr). Baixe o certificado APNs e salve o arquivo pem localmente. Este arquivo de certificado (. PEM) APNs é usado para estabelecer uma relação de confiança entre o servidor do Apple Push Notification e a autoridade de gerenciamento de dispositivo móvel do Intune.  

4.  **Ativar a inscrição e carregar o certificado APNs** - Para ativar a inscrição iOS, carregue o certificado APNs.  

    1.  Na consola do Configuration Manager, na área de trabalho **Administração** , aceda a **Serviços Cloud** > **Subscrição do Microsoft Intune**.  

    2.  No separador **Home Page** no grupo **Subscrição** , clique em **Configurar Plataformas** > **iOS**.  

        > [!NOTE]  
        >  Não carregue o certificado do serviço Apple Push Notification (APNs) até que tenha ativado a inscrição iOS na consola do Configuration Manager.  

    3.  Na caixa de diálogo **Propriedades da Subscrição do Windows Intune** , selecione o separador **iOS** e clique para selecionar a caixa de verificação **Ativar a inscrição iOS** .  

    4.  Clique em **Procurar**e aceda ao ficheiro do certificado APNs (.cer) transferido a partir da Apple. O Configuration Manager apresenta as informações do certificado APNs. Clique em **OK** para guardar o certificado APNs no Intune.  

 Depois de você configurá-lo, você precisa permitir que os usuários saibam como registrar seus dispositivos. Veja [O que dizer aos utilizadores finais sobre a utilização do Microsoft Intune](https://docs.microsoft.com/intune/end-user-educate). Estas informações aplicam-se ao Microsoft Intune e aos dispositivos móveis geridos pelo Configuration Manager.

> [!div class="button"]
[< Anterior etapa](create-service-connection-point.md)[próxima etapa >  ](set-up-additional-management.md)

