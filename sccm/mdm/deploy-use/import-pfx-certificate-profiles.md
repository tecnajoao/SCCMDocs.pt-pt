---
title: Criar perfis de certificado PFX através da importação de detalhes do certificado
titleSuffix: Configuration Manager
description: Saiba como utilizar ficheiros PFX no System Center Configuration Manager para gerar certificados específicos do utilizador que suportam a troca de dados encriptados.
ms.date: 04/04/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: e3bb3e13-3037-4122-93bc-504bfd080a4d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 214dcdca927e515f776e99f005f968a4b98f4112
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53418837"
---
# <a name="how-to-create-pfx-certificate-profiles-by-importing-certificate-details"></a>Como criar perfis de certificado PFX através da importação de detalhes do certificado

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Aqui, irá aprender a criar um perfil de certificado ao importar as credenciais de certificados externos.  

[Perfis de certificado](../../protect/deploy-use/introduction-to-certificate-profiles.md) fornecer informações gerais sobre como criar e configurar perfis de certificado. Este tópico destaca algumas informações específicas sobre os perfis de certificado relacionadas com certificados PFX.

- Uma variedade de arquivos de certificados adequadas para diferentes dispositivos e sistemas operacionais do Configuration Manager.  Estas atualizações incluem:

  -   iOS e MacOS/OSX
  -   Android e Android for Work
  -   Windows 10, incluindo o Windows 10 mobile.

Para obter mais informações, consulte [pré-requisitos de perfil de certificado](../../protect/plan-design/prerequisites-for-certificate-profiles.md).

## <a name="pfx-certificate-profiles"></a>Perfis de certificado PFX
System Center Configuration Manager permite-lhe importar as credenciais de certificado e, em seguida, aprovisionar ficheiros do personal information exchange (. pfx) para dispositivos do utilizador. Os ficheiros .pfx podem ser utilizados para gerar certificados específicos do utilizador para suportar a troca de dados encriptados.

> [!TIP]  
>  Estão disponíveis instruções passo a passo que descrevem este processo em [Como Criar e Implementar Perfis de Certificado PFX no Configuration Manager](http://blogs.technet.com/b/karanrustagi/archive/2015/09/01/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager.aspx).  

## <a name="create-import-and-deploy-a-personal-information-exchange-pfx-certificate-profile"></a>Criar, importar e implementar um perfil de certificado Personal Information Exchange (PFX)  

### <a name="get-started"></a>Introdução

1.  Na consola do System Center Configuration Manager, clique em **ativos e compatibilidade**.  
2.  Na área de trabalho **Ativos e Compatibilidade** , expanda **Definições de Compatibilidade**, expanda **Acesso a Recursos da Empresa**e clique em **Perfis de Certificado**.  

3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Perfil de Certificado**.

4.  Na página **Geral** do Assistente **Criar Perfil de Certificado** , especifique as seguintes informações:  

    -   **Nome**: Introduza um nome exclusivo para o perfil de certificado. Pode utilizar até 256 carateres.  

    -   **Descrição**: Forneça uma descrição que proporcione uma descrição geral do perfil de certificado e outras informações relevantes que ajudem a identificá-lo na consola do System Center Configuration Manager. Pode utilizar até 256 carateres.  

    -   **Especifique o tipo de perfil de certificado que pretende criar**: Para certificados PFX, escolha uma das seguintes opções:  

        -   **Configurações pessoais de informações Exchange PKCS #12 (PFX) - importar**: Cria um perfil de certificado através da importação por meio de programação de informações de certificados existentes.  

        -   **Personal Information Exchange – definições PKCS #12 (PFX) - criar**: Cria um perfil de certificado PFX com as credenciais fornecidas por uma autoridade de certificação.  Para obter mais informações, consulte [como criar perfis de certificado PFX com uma autoridade de certificação](../../mdm/deploy-use/create-pfx-certificate-profiles.md).


### <a name="create-a-pfx-certificate-profile-for-the-imported-credentials"></a>Criar um perfil de certificado PFX para as credenciais importados

Para importar um certificado PFX, use o SDK do Configuration Manager para implementar um script criar PFX. 

Certificados importados posteriormente são implementados em dispositivos inscritos.

1. Na **certificado PFX** página do **Create Certificate Profile Wizard**, especifique onde o fornecedor de armazenamento de chaves de dispositivo:
    -   **Instalar no Trusted Platform Module (TPM), se estiver presente**  
    -   **Instalar no Trusted Platform Module (TPM), caso contrário ocorre uma falha** 
    -   **Instalar no Windows Hello para ou não de negócios** 
    -   **Instalar no Fornecedor de Armazenamento de Chaves de Software** 
2. Clique em **Seguinte**. 
3. Sobre o **plataformas suportadas** página do assistente, selecione as plataformas de dispositivos suportadas e, em seguida, clique em **próxima**.

### <a name="finish-the-profile"></a>Concluir o perfil

1.  Clique em **Seguinte**, reveja a página **Resumo** e, em seguida, feche o assistente.  
2.  O perfil do certificado que contém o ficheiro PFX está agora disponível a partir da área de trabalho **Perfis de Certificados** . 
3.  Implementar o perfil, na **ativos e compatibilidade** área de trabalho open **definições de compatibilidade** > **acesso a recursos da empresa**  >   **Perfis de certificado**, clique com o botão direito do certificado que pretende e clique em **Deploy**. 

### <a name="deploy-a-create-pfx-script"></a>Implementar um criar Script PFX

Utilize o [SDK do Configuration Manager](http://go.microsoft.com/fwlink/?LinkId=613525) para implementar um Script criar PFX. 

O Script Criar PFX adicionado no Configuration Manager 2012 SP2 adiciona uma classe SMS_ClientPfxCertificate ao SDK. Esta classe inclui os seguinte métodos:  

    -   `ImportForUser`  

    -   `DeleteForUser`  

O exemplo seguinte importa as credenciais para um perfil de certificado PFX.

``` powershell
    $EncryptedPfxBlob = "<blob>"  
    $Password = "abc"  
    $ProfileName = "PFX_Profile_Name"  
    $UserName = "ComputerName\Administrator"  

    #New pfx  
    $WMIConnection = ([WMIClass]"\\nksccm\root\SMS\Site_MDM:SMS_ClientPfxCertificate")  
        $NewEntry = $WMIConnection.psbase.GetMethodParameters("ImportForUser")  
        $NewEntry.EncryptedPfxBlob = $EncryptedPfxBlob  
        $NewEntry.Password = $Password  
        $NewEntry.ProfileName = $ProfileName  
        $NewEntry.UserName = $UserName  
    $Resource = $WMIConnection.psbase.InvokeMethod("ImportForUser",$NewEntry,$null)  
```  

Para utilizar este exemplo, Atualize as seguintes variáveis de script:  

   -   **blob**\-blob de encriptado em base64 o PFX  
   -   **$Password** -a palavra-passe para o ficheiro PFX  
   -   **$ProfileName** -o nome do perfil PFX  
   -   **ComputerName** -nome do computador anfitrião   

## <a name="see-also"></a>Consulte também
[Criar um novo perfil de certificado](../../protect/deploy-use/create-certificate-profiles.md) orienta-o Assistente para criar perfil de certificado.

[Como criar perfis de certificado PFX através da importação de detalhes do certificado](../../mdm/deploy-use/create-pfx-certificate-profiles.md)

[Implementar o Wi-Fi, VPN, e-mail e perfis de certificado](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md) descreve show para implementar perfis de certificado.