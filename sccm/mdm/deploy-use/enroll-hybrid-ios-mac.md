---
title: "Configurar o iOS e gestão de dispositivos de híbrida Mac com o System Center Configuration Manager e o Microsoft Intune | Documentos do Microsoft"
description: "Configure a gestão de dispositivos iOS com o System Center Configuration Manager e o Microsoft Intune."
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
ms.sourcegitcommit: 02af275ede0ab8578adb0615458b285819d65c9c
ms.openlocfilehash: 848721b564316234ad900fcbf968098002a4bb4e
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="set-up-ios-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurar a gestão de dispositivos iOS híbrida com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Com o Configuration Manager e o Intune, pode ativar BYOD iOS ("bring your own device") e de inscrição de dispositivos do Mac OS X para dar acesso ao e-mail da empresa e recursos para os utilizadores de Mac, iPad e iPhone. Assim que os utilizadores instalarem a aplicação do portal da empresa do Intune, os respetivos dispositivos podem ser visados pela política. Antes de poder gerir dispositivos iOS e Mac, tem de importar um certificado do serviço Apple Push Notification (APNs) da Apple. Este certificado permite ao Intune gerir os dispositivos iOS e Mac e estabelece uma ligação IP autorizada e encriptada com os serviços de autoridade de gestão de dispositivos móveis.  

 Também pode inscrever dispositivos iOS pertencentes à empresa.  Consulte o artigo [inscrever dispositivos pertencentes à empresa](enroll-company-owned-devices.md).  

## <a name="enable-ios-device-enrollment"></a>Ativar a inscrição de dispositivos iOS  
 Para suportar a inscrição de dispositivos iOS, tem de seguir estes passos:  

#### <a name="set-up-ios-device-enrollment-in-configuration-manager"></a>Configurar a inscrição de dispositivos iOS no Configuration Manager  

1.  **Pré-requisitos** - o para poder configurar a inscrição para qualquer plataforma, concluir os pré-requisitos e procedimentos [híbrida configuração MDM](setup-hybrid-mdm.md).    

2.  **Transferir um pedido de assinatura de certificado** -É necessário um ficheiro de pedido de assinatura de certificado (.csr) para pedir um certificado APNs da Apple.  

    1.  Na consola do Configuration Manager, na área de trabalho **Administração** , aceda a **Serviços Cloud**> **Subscrições do Microsoft Intune**.  

    2.  No separador **Home Page** , clique em **Criar pedido de certificado do APNs**. É aberta a caixa de diálogo **Pedido de Assinatura de Certificado do Serviço Apple Push Notification** .  

    3.  **Navegue** para o caminho onde pretende guardar o ficheiro de pedido de assinatura de certificado novo (.csr). Guarde o ficheiro de pedido de assinatura de certificado (.csr) localmente.  

    4.  Clique em **Transferir**. O novo ficheiro .csr do Microsoft Intune é transferido e guardado pelo Configuration Manager. O ficheiro .csr é utilizado para pedir um certificado de relação de confiança do Portal de Certificados Apple Push.  

3.  **Pedir um certificado APNs da Apple** - O certificado do serviço Apple Push Notification (APNs) é utilizado para estabelecer uma relação de confiança entre o serviço de gestão, o Intune e os dispositivos móveis iOS inscritos.  

    1.  Num browser, aceda ao [Portal de Certificados Apple Push](http://go.microsoft.com/fwlink/?LinkId=269844) e inicie sessão com o ID Apple da sua empresa. Este ID Apple tem de ser utilizado no futuro para renovar o certificado APNs.  

    2.  Conclua o assistente utilizando o ficheiro de pedido de assinatura de certificado (.csr). Transfira o certificado APNs e guarde o ficheiro .pem localmente. Este ficheiro de certificado (. pem) de APNs é utilizado para estabelecer uma relação de confiança entre o servidor do Apple Push Notification e autoridade de gestão de dispositivos móveis do Intune.  

4.  **Ativar a inscrição e carregar o certificado APNs** - Para ativar a inscrição iOS, carregue o certificado APNs.  

    1.  Na consola do Configuration Manager, na área de trabalho **Administração** , aceda a **Serviços Cloud** > **Subscrição do Microsoft Intune**.  

    2.  No separador **Home Page** no grupo **Subscrição** , clique em **Configurar Plataformas** > **iOS**.  

        > [!NOTE]  
        >  Não carregue o certificado do serviço Apple Push Notification (APNs) até que tenha ativado a inscrição iOS na consola do Configuration Manager.  

    3.  Na caixa de diálogo **Propriedades da Subscrição do Windows Intune** , selecione o separador **iOS** e clique para selecionar a caixa de verificação **Ativar a inscrição iOS** .  

    4.  Clique em **Procurar**e aceda ao ficheiro do certificado APNs (.cer) transferido a partir da Apple. O Configuration Manager apresenta as informações do certificado APNs. Clique em **OK** para guardar o certificado APNs no Intune.  

 Assim que estiver configurado, terá de informar os utilizadores como inscrever os respetivos dispositivos. Veja [O que dizer aos utilizadores finais sobre a utilização do Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). Estas informações aplicam-se ao Microsoft Intune e aos dispositivos móveis geridos pelo Configuration Manager.

> [!div class="button"]
[< Passo anterior](create-service-connection-point.md)[junto passo >  ](set-up-additional-management.md)

