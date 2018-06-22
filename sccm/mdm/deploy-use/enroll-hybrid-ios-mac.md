---
title: Configurar a gestão iOS e Mac híbrida dispositivo com o Microsoft Intune
titleSuffix: Configuration Manager
description: Configure a gestão de dispositivos iOS com o System Center Configuration Manager e o Microsoft Intune.
ms.date: 08/11/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 5eae4400-58ca-4c71-804c-6a585cd3df5d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9407180df12902c17f4de8e52be13229ce35c60b
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32348832"
---
# <a name="set-up-ios-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurar a gestão de dispositivos iOS híbrida com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Com o Configuration Manager e o Intune, ativar a inscrição de dispositivos iOS e macOS dar acesso ao e-mail da empresa e recursos para iPhone, iPad e os utilizadores de Mac. Assim que os utilizadores instalarem a aplicação do portal da empresa do Intune, os respetivos dispositivos podem ser visados pela política. Antes de poder gerir dispositivos iOS e Mac, tem de importar um certificado do serviço Apple Push Notification (APNs) da Apple. Este certificado permite ao Intune gerir dispositivos iOS e Mac ao estabelecer uma ligação com o serviço de gestão de dispositivos da Apple.  

 Também pode inscrever dispositivos iOS pertencentes à empresa.  Consulte [inscrever dispositivos pertencentes à empresa](enroll-company-owned-devices.md).  

**Pré-requisitos**<br>
Antes de poder configurar a inscrição para qualquer plataforma, conclua os pré-requisitos e procedimentos [mm híbrida do programa de configuração](setup-hybrid-mdm.md).

Para suportar a inscrição de dispositivos iOS, tem de seguir estes passos:  

## <a name="download-a-certificate-signing-request"></a>Transferir um pedido de assinatura de certificado
É necessário um ficheiro de pedido de assinatura de certificado para pedir um certificado do APNs da Apple.  

1.  Na consola do Configuration Manager, na área de trabalho **Administração** , aceda a **Serviços Cloud**> **Subscrições do Microsoft Intune**.  

2.  No separador **Home Page** , clique em **Criar pedido de certificado do APNs**. É aberta a caixa de diálogo **Pedido de Assinatura de Certificado do Serviço Apple Push Notification** .  

3.  **Procurar** para o caminho onde pretende guardar o ficheiro de pedido de assinatura de certificado novo. Guarde o ficheiro localmente do pedido de assinatura de certificado.  

4.  Clique em **Transferir**. A assinatura de certificado de novo Microsoft Intune, pedir as transferências de ficheiros e é guardado pelo Configuration Manager. O ficheiro de pedido de assinatura de certificado é utilizado para pedir um certificado de relação de fidedignidade do Apple Push Certificates Portal.  

## <a name="request-an-mdm-push-certificate-from-apple"></a>Pedir um certificado MDM Push da Apple
O certificado Push de MDM é utilizado para estabelecer uma relação de confiança entre o serviço de gestão, o Intune e a dispositivos móveis iOS inscritos.  

1.  Num browser, aceda ao [Portal de Certificados Apple Push](http://go.microsoft.com/fwlink/?LinkId=269844) e inicie sessão com o ID Apple da sua empresa. Este ID Apple tem de ser utilizado no futuro para renovar o certificado APNs.  

2.  Conclua o assistente utilizando o ficheiro de pedido de assinatura de certificado (.csr). Transfira o certificado Push de MDM e guarde o ficheiro pem localmente. Este ficheiro de certificado (. pem) é utilizado para estabelecer uma relação de confiança entre o servidor de notificação Push da Apple e a autoridade de gestão de dispositivos móveis do Intune.  

> [!NOTE]  
>  Não carregue o certificado do Apple Push Notification (APNs) do serviço Intune até, ativar a inscrição do iOS na consola do Configuration Manager.  

## <a name="enable-enrollment-and-upload-the-mdm-push-certificate"></a>Ativar a inscrição e carregar o certificado Push de MDM
Para ativar a inscrição de iOS, carregue o certificado do APNs.  

1.  Na consola do Configuration Manager, na área de trabalho **Administração** , aceda a **Serviços Cloud** > **Subscrição do Microsoft Intune**.  

2.  No separador **Home Page** no grupo **Subscrição** , clique em **Configurar Plataformas** > **iOS**.  

3.  Na caixa de diálogo **Propriedades da Subscrição do Windows Intune** , selecione o separador **iOS** e clique para selecionar a caixa de verificação **Ativar a inscrição iOS** .  
4.  Clique em **Procurar**e aceda ao ficheiro do certificado APNs (.cer) transferido a partir da Apple. O Configuration Manager apresenta as informações do certificado APNs. Clique em **OK** para guardar o certificado APNs no Intune.  

Depois da configurar, terá de informar os utilizadores como inscrever os respetivos dispositivos. Veja [O que dizer aos utilizadores finais sobre a utilização do Microsoft Intune](https://docs.microsoft.com/intune/end-user-educate). Estas informações aplicam-se ao Microsoft Intune e aos dispositivos móveis geridos pelo Configuration Manager.

## <a name="configure-enrollment-restrictions"></a>Configurar restrições de inscrição

Pode limitar os dispositivos que podem inscrever por bloquear dispositivos de propriedade pessoal. Isto impede que os utilizadores inscrever os respetivos dispositivos através do Portal da empresa. Se bloquear dispositivos pessoais, podem inscrever os seguintes dispositivos:
- [Dispositivos predeclared](predeclare-devices-with-hardware-id.md)
- [Apple Configurator para dispositivos geridos](ios-hybrid-enrollment-using-apple-configurator.md)
- [Dispositivos geridos pelo programa de inscrição de dispositivos (DEP)](ios-device-enrollment-program-for-hybrid.md)
- Os dispositivos inscritos com uma [conta do Gestor de inscrição de dispositivos](enroll-devices-with-device-enrollment-manager.md)

### <a name="to-enable-enrollment-restrictions"></a>Para ativar restrições de inscrição
1.  Na consola do Configuration Manager, na área de trabalho **Administração** , aceda a **Serviços Cloud** > **Subscrição do Microsoft Intune**.
2.  No separador **Home Page** no grupo **Subscrição** , clique em **Configurar Plataformas** > **iOS**.
3.  Escolha **bloco pessoal dispositivos pertencentes à empresa** para limitar a inscrição de dispositivos pertencentes à empresa.

> [!div class="button"]
[< Anterior passo](create-service-connection-point.md)[passo seguinte >](set-up-additional-management.md)
