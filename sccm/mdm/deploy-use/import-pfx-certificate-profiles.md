---
title: "Criar perfis de certificado PFX através da importação de detalhes do certificado"
titleSuffix: Configuration Manager
description: "Saiba como utilizar ficheiros PFX no System Center Configuration Manager para gerar certificados específicos do utilizador que suportam a troca de dados encriptados."
ms.custom: na
ms.date: 04/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e3bb3e13-3037-4122-93bc-504bfd080a4d
caps.latest.revision: 
caps.handback.revision: 
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.openlocfilehash: 25c6927698e409ff3b0c3f846e2cc567a6f458ab
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="how-to-create-pfx-certificate-profiles-by-importing-certificate-details"></a>Como criar perfis de certificado PFX através da importação de detalhes do certificado

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Aqui, irá aprender a criar um perfil de certificado através da importação de credenciais de certificados externos.  

[Perfis de certificado](../../protect/deploy-use/introduction-to-certificate-profiles.md) fornecer informações gerais sobre como criar e configurar perfis de certificado. Este tópico realça algumas informações específicas sobre os perfis de certificados relacionados com os certificados PFX.

-  Gestor de configuração de uma variedade de arquivos de certificados adequados para diferentes dispositivos e sistemas operativos.  Estas atualizações incluem:

 -   iOS e MacOS/OSX
 -   Android e Android para o trabalho
 -   Windows 10, incluindo o Windows 10 mobile.

Para obter mais informações, consulte [pré-requisitos de perfil de certificado](../../protect/plan-design/prerequisites-for-certificate-profiles.md).

## <a name="pfx-certificate-profiles"></a>Perfis de certificado PFX
System Center Configuration Manager permite-lhe importar as credenciais do certificado e, em seguida, aprovisionar ficheiros de personal information exchange (. pfx) para dispositivos de utilizador. Os ficheiros .pfx podem ser utilizados para gerar certificados específicos do utilizador para suportar a troca de dados encriptados.

> [!TIP]  
>  Estão disponíveis instruções passo a passo que descrevem este processo em [Como Criar e Implementar Perfis de Certificado PFX no Configuration Manager](http://blogs.technet.com/b/karanrustagi/archive/2015/09/01/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager.aspx).  

## <a name="create-import-and-deploy-a-personal-information-exchange-pfx-certificate-profile"></a>Criar, importar e implementar um perfil de certificado do Personal Information (Exchange PFX)  

### <a name="get-started"></a>Introdução

1.  Na consola do System Center Configuration Manager, clique em **ativos e compatibilidade**.  
2.  Na área de trabalho **Ativos e Compatibilidade** , expanda **Definições de Compatibilidade**, expanda **Acesso a Recursos da Empresa**e clique em **Perfis de Certificado**.  

3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Perfil de Certificado**.

4.  Na página **Geral** do Assistente **Criar Perfil de Certificado** , especifique as seguintes informações:  

    -   **Nome**: Introduza um nome exclusivo para o perfil de certificado. Pode utilizar até 256 carateres.  

    -   **Descrição**: Forneça uma descrição que proporcione uma descrição geral do perfil de certificado e outras informações relevantes que ajudem a identificá-lo na consola do System Center Configuration Manager. Pode utilizar até 256 carateres.  

    -   **Especifique o tipo de perfil de certificado que pretende criar**: Para os certificados PFX, escolha uma das seguintes opções:  

        -   **Definições de informações Exchange PKCS #12 (PFX) pessoais - importar**: Cria um perfil de certificado através da importação programaticamente informações dos certificados existentes.  

        -   **Personal Information Exchange - definições do PKCS #12 (PFX) - criar**: Cria um perfil de certificado PFX utilizando as credenciais fornecidas por uma autoridade de certificação.  Para obter mais informações, consulte [como criar perfis de certificado PFX através de uma autoridade de certificação](../../mdm/deploy-use/create-pfx-certificate-profiles.md).


### <a name="create-a-pfx-certificate-profile-for-the-imported-credentials"></a>Criar um perfil de certificado PFX para as credenciais importados

Para importar um certificado PFX, pode utilizar o SDK do Configuration Manager para implementar um script criar PFX. 

Certificados importados mais tarde são implementados em dispositivos inscritos.

1. No **certificado PFX** página do **certificado Assistente para criar perfil**, especifique onde o fornecedor de armazenamento de chaves de dispositivo:
    -   **Instalar no Trusted Platform Module (TPM), se estiver presente**  
    -   **Instalar no Trusted Platform Module (TPM), caso contrário ocorre uma falha** 
    -   **Instalação do Windows Hello para falhar caso contrário, de negócio** 
    -   **Instalar no Fornecedor de Armazenamento de Chaves de Software** 
2. Clique em **Seguinte**. 
3. No **plataformas suportadas** página do assistente, escolha as plataformas de dispositivos suportados e, em seguida, clique em **seguinte**.

### <a name="finish-the-profile"></a>Concluir o perfil

1.  Clique em **Seguinte**, reveja a página **Resumo** e, em seguida, feche o assistente.  
2.  O perfil do certificado que contém o ficheiro PFX está agora disponível a partir da área de trabalho **Perfis de Certificados** . 
3.  Implementar o perfil, no **ativos e compatibilidade** área de trabalho abrir **as definições de compatibilidade** > **acesso a recursos da empresa** > **perfis de certificado**, clique no certificado que pretende e clique em **implementar**. 

### <a name="deploy-a-create-pfx-script"></a>Implementar um criar PFX Script

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
[Criar um novo perfil de certificado](../../protect/deploy-use/create-certificate-profiles.md) orienta-o através do Assistente para criar perfil de certificado.

[Como criar perfis de certificado PFX através da importação de detalhes do certificado](../../mdm/deploy-use/create-pfx-certificate-profiles.md)

[Implementar Wi-Fi, VPN, e-mail e perfis de certificado](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md) descreve Mostrar para implementar perfis de certificado.