---
title: Configuração do iOS e Mac gestão híbrida de dispositivos com o Microsoft Intune
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
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8e7baf5d26bb823f3b02efb8e71cf4d34330d899
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56121214"
---
# <a name="set-up-ios-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurar a gestão de dispositivos iOS híbrida com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Com o Configuration Manager e o Intune, ativar a inscrição de dispositivos iOS e macOS dar acesso ao e-mail da empresa e recursos para iPhone, iPad e usuários de Mac. Assim que os utilizadores instalarem a aplicação do portal da empresa do Intune, os respetivos dispositivos podem ser visados pela política. Antes de poder gerir dispositivos iOS e Mac, tem de importar um certificado do serviço Apple Push Notification (APNs) da Apple. Este certificado permite ao Intune gerir dispositivos iOS e Mac ao estabelecer uma ligação com o serviço de gestão de dispositivos da Apple.  

 Também pode inscrever dispositivos iOS pertencentes à empresa.  Ver [inscrever dispositivos pertencentes à empresa](enroll-company-owned-devices.md).  

**Pré-requisitos**<br>
Antes de poder configurar a inscrição para qualquer plataforma, conclua os pré-requisitos e procedimentos [mm híbrida do programa de configuração](setup-hybrid-mdm.md).

Para suportar a inscrição de dispositivos iOS, tem de seguir estes passos:  

## <a name="download-a-certificate-signing-request"></a>Transferir um pedido de assinatura de certificado
Um ficheiro de pedido de assinatura de certificado é necessário para pedir um certificado do APNs da Apple.  

1.  Na consola do Configuration Manager, na área de trabalho **Administração** , aceda a **Serviços Cloud**> **Subscrições do Microsoft Intune**.  

2.  No separador **Home Page** , clique em **Criar pedido de certificado do APNs**. É aberta a caixa de diálogo **Pedido de Assinatura de Certificado do Serviço Apple Push Notification** .  

3.  **Procurar** para o caminho para guardar o ficheiro de pedido de assinatura de certificado novo. Guarde o certificado de assinatura de ficheiro de pedido localmente.  

4.  Clique em **Transferir**. A nova assinatura de certificado de Microsoft Intune, pedir transferências de ficheiros e é guardado pelo Configuration Manager. O ficheiro de pedido de assinatura de certificado é utilizado para pedir um certificado de relação de confiança a partir do Portal Apple Push Certificates.  

## <a name="request-an-mdm-push-certificate-from-apple"></a>Pedir um certificado Push de MDM da Apple
O certificado Push de MDM é utilizado para estabelecer uma relação de confiança entre o serviço de gestão do Intune e dispositivos móveis iOS inscritos.  

1.  Num browser, aceda ao [Portal de Certificados Apple Push](http://go.microsoft.com/fwlink/?LinkId=269844) e inicie sessão com o ID Apple da sua empresa. Este ID Apple tem de ser utilizado no futuro para renovar o certificado APNs.  

2.  Conclua o assistente utilizando o ficheiro de pedido de assinatura de certificado (.csr). Transfira o certificado Push de MDM e guarde o ficheiro pem localmente. Este ficheiro de certificado (. pem) é utilizado para estabelecer uma relação de confiança entre o servidor de Apple Push Notification e a autoridade de gestão de dispositivos móveis do Intune.  

> [!NOTE]  
>  Não carregue o certificado do Apple Push Notification service (APNs) para o Intune até ativar a inscrição do iOS na consola do Configuration Manager.  

## <a name="enable-enrollment-and-upload-the-mdm-push-certificate"></a>Ativar a inscrição e carregar o certificado Push de MDM
Para ativar a inscrição iOS, carregue o certificado do APNs.  

1.  Na consola do Configuration Manager, na área de trabalho **Administração** , aceda a **Serviços Cloud** > **Subscrição do Microsoft Intune**.  

2.  No separador **Home Page** no grupo **Subscrição** , clique em **Configurar Plataformas** > **iOS**.  

3.  Na caixa de diálogo **Propriedades da Subscrição do Windows Intune** , selecione o separador **iOS** e clique para selecionar a caixa de verificação **Ativar a inscrição iOS** .  
4.  Clique em **Procurar**e aceda ao ficheiro do certificado APNs (.cer) transferido a partir da Apple. O Configuration Manager apresenta as informações do certificado APNs. Clique em **OK** para guardar o certificado APNs no Intune.  

Depois de configurá-lo, terá de informar os utilizadores como devem inscrever os dispositivos. Veja [O que dizer aos utilizadores finais sobre a utilização do Microsoft Intune](https://docs.microsoft.com/intune/end-user-educate). Estas informações aplicam-se ao Microsoft Intune e aos dispositivos móveis geridos pelo Configuration Manager.

## <a name="configure-enrollment-restrictions"></a>Configurar restrições de inscrição

Pode limitar a dispositivos que pode inscrever-se ao bloquear dispositivos pessoais. Isto impede que os utilizadores inscrever os respetivos dispositivos com o Portal da empresa. Se bloquear dispositivos pessoais, podem inscrever apenas os seguintes dispositivos:
- [Dispositivos pré-declarados](predeclare-devices-with-hardware-id.md)
- [Dispositivos geridos pelo Apple Configurator](ios-hybrid-enrollment-using-apple-configurator.md)
- [Dispositivos geridos pelo programa de inscrição de dispositivos (DEP)](ios-device-enrollment-program-for-hybrid.md)
- Dispositivos inscritos com um [conta do Gestor de inscrição de dispositivos](enroll-devices-with-device-enrollment-manager.md)

### <a name="to-enable-enrollment-restrictions"></a>Para ativar restrições de inscrição
1.  Na consola do Configuration Manager, na área de trabalho **Administração** , aceda a **Serviços Cloud** > **Subscrição do Microsoft Intune**.
2.  No separador **Home Page** no grupo **Subscrição** , clique em **Configurar Plataformas** > **iOS**.
3.  Escolher **bloquear dispositivos pessoais** para limite de inscrição para dispositivos pertencentes à empresa.

> [!div class="button"]
> [< Anterior passo](create-service-connection-point.md)[passo seguinte >](set-up-additional-management.md)
