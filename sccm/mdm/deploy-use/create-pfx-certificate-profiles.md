---
title: Criar perfis de certificado PFX | Documentos do Microsoft
description: "Saiba como utilizar ficheiros PFX no System Center Configuration Manager para gerar os certificados de utilizador específica que suportam intercâmbio de dados encriptados."
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
caps.latest.revision: 5
caps.handback.revision: 0
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 26feb0b166beb7e48cb800a5077d00dbc3eec51a
ms.openlocfilehash: 27435316c6e47531ff989bc8956ca0c874131a0e
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="how-to-create-pfx-certificate-profiles-in-system-center-configuration-manager"></a>Como criar perfis de certificado PFX no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Perfis de certificado funcionam com o serviços de certificados do Active Directory e a função de serviço de inscrição de dispositivos de rede para aprovisionar certificados de autenticação para dispositivos geridos para que os utilizadores forma totalmente integrada podem aceder a recursos da empresa. Por exemplo, pode criar e implementar perfis de certificado para fornecer os certificados necessários para que os utilizadores iniciem as ligações VPN e sem fios.

[Perfis de certificado](../../protect/deploy-use/introduction-to-certificate-profiles.md) disponibiliza informações gerais sobre como criar e configurar perfis de certificado. Este tópico destaca algumas informações específicas sobre perfis de certificado relacionadas com os certificados PFX.

-  O Configuration Manager suporta a implementação de certificados em vários arquivos de certificados, consoante os requisitos, o tipo de dispositivo e o sistema operativo. Os seguintes dispositivos são suportados quando os mesmos estarem inscritos com o Intune:

 -   iOS  

- Para outros pré-requisitos, consulte o artigo [pré-requisitos do perfil de certificado](../../protect/plan-design/prerequisites-for-certificate-profiles.md).

## <a name="pfx-certificate-profiles"></a>Perfis de certificado PFX
System Center Configuration Manager permite-lhe importar e aprovisionar os ficheiros de informações pessoais do exchange (. pfx) para dispositivos do utilizador. Os ficheiros .pfx podem ser utilizados para gerar certificados específicos do utilizador para suportar a troca de dados encriptados.

> [!TIP]  
>  Estão disponíveis instruções passo a passo que descrevem este processo em [Como Criar e Implementar Perfis de Certificado PFX no Configuration Manager](http://blogs.technet.com/b/karanrustagi/archive/2015/09/01/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager.aspx).  

## <a name="create-and-deploy-a-personal-information-exchange-pfx-certificate-profile"></a>Criar e implementar um perfil de certificado do Personal Information (Exchange PFX)  

### <a name="get-started"></a>Introdução

1.  Na consola do System Center Configuration Manager, clique em **ativos e compatibilidade**.  

2.  Na área de trabalho **Ativos e Compatibilidade** , expanda **Definições de Compatibilidade**, expanda **Acesso a Recursos da Empresa**e clique em **Perfis de Certificado**.  

3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Perfil de Certificado**.

4.  Na página **Geral** do Assistente **Criar Perfil de Certificado** , especifique as seguintes informações:  

    -   **Nome**: Introduza um nome exclusivo para o perfil de certificado. Pode utilizar até 256 carateres.  

    -   **Descrição**: Forneça uma descrição que proporcione uma descrição geral sobre o perfil de certificado e outras informações relevantes que ajudem a identificá-lo na consola do System Center Configuration Manager. Pode utilizar até 256 carateres.  

    -   **Especifique o tipo de perfil de certificado que pretende criar**: Para certificados PFX, escolha:  

        -   **Definições de Information Exchange (PKCS #12 PFX) pessoais - importar**: Selecione esta opção para importar um certificado PFX.  
       

### <a name="import-a-pfx-certificate"></a>Importar um certificado PFX

Para importar um certificado PFX, terá do SDK do Configuration Manager. Todos os certificados importados para um utilizador serão implementados para todos os dispositivos que o utilizador inscrever.

1. No **certificado PFX** página do **criar Assistente de perfil de certificado**, especifique onde será armazenado o certificado em dispositivos para os quais implementá-lo:
    -     **Instalar no Trusted Platform Module (TPM), se estiver presente**  
    -   **Instalar no Trusted Platform Module (TPM), caso contrário ocorre uma falha** 
    -   **Instalar no Windows Hello para falhar caso contrário, empresas** 
    -   **Instalar no Fornecedor de Armazenamento de Chaves de Software** 
2. Clique em **Seguinte**. 
3. No **plataformas suportadas** página do assistente, selecione as plataformas de dispositivos nos quais este certificado será instalado, em seguida, clique em **seguinte**.
4. Ao utilizar o SDK para Windows 8.1 disponível no Centro de Transferências ([http://go.microsoft.com/fwlink/?LinkId=613525](http://go.microsoft.com/fwlink/?LinkId=613525)), implemente um Script Criar PFX. O Script Criar PFX adicionado no Configuration Manager 2012 SP2 adiciona uma classe SMS_ClientPfxCertificate ao SDK. Esta classe inclui os seguinte métodos:  

    -   ImportForUser  

    -   DeleteForUser  

     Exemplo de script:  

```  
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

As seguintes variáveis de script têm de ser modificadas no script:  

   -   blob\ = blob de encriptados base64 o PFX  
   -   $Password = A palavra-passe do ficheiro PFX  
   -   $ProfileName = O nome do perfil PFX  
   -   ComputerName = Nome do computador anfitrião   



### <a name="finish-up"></a>Concluir

1.  Clique em **Seguinte**, reveja a página **Resumo** e, em seguida, feche o assistente.  
2.  O perfil do certificado que contém o ficheiro PFX está agora disponível a partir da área de trabalho **Perfis de Certificados** . 
3.  Implementar o perfil, no **ativos e compatibilidade** área de trabalho aberta **definições de compatibilidade** > **acesso a recursos da empresa** > **perfis de certificado**, faça duplo clique no certificado que pretende, clique em **implementar**. 



## <a name="see-also"></a>Consulte também
[Criar um novo perfil de certificado](../../protect/deploy-use/create-certificate-profiles.md#create-a-new-certificate-profile) orienta-o durante o Assistente para criar perfil de certificado.

[Implementar Wi-Fi, VPN, correio eletrónico e perfis de certificado](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md) fornece informações sobre como implementar perfis de certificado.
