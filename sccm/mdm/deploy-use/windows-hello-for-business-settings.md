---
title: "Windows Hello para definições de empresas | Documentos do Microsoft"
description: Saiba como integrar o Windows Hello para empresas com o System Center Configuration Manager.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c0593c07-5dd7-4d23-a0d8-d30165f49ef7
caps.latest.revision: 17
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 8c7bf901caa49c8585a9ed3913d4a5a2aac57013
ms.openlocfilehash: 7ac2baeb3c10ce90eb643fa28a953186b571d037
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="windows-hello-for-business-settings-in-system-center-configuration-manager-hybrid"></a>Windows Hello para definições de negócio no System Center Configuration Manager (híbrido)

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager permite-lhe integrar com o Windows Hello para empresas (anteriormente Microsoft Passport para Windows), que é um método alternativo início de sessão para dispositivos Windows 10. O Hello para Empresas utiliza o Active Directory ou uma conta do Azure Active Directory para substituir uma palavra-passe, um smart card ou um smart card virtual.  

Com o Hello para Empresas, pode utilizar um **gesto de utilizador** para iniciar sessão, em vez de uma palavra-passe. Um gesto de utilizador pode ser um PIN simples, uma autenticação biométrica ou um dispositivo externo, como um leitor de impressões digitais.  

 O Configuration Manager é integrada com o Windows Hello para empresas de duas formas:  

-   Pode utilizar o Configuration Manager para controlar que utilizadores de gestos podem e não podem utilizar para iniciar sessão.  

-   Pode armazenar certificados de autenticação no fornecedor de armazenamento de chaves (KSP) do Windows Hello para Empresas. Para obter mais informações, consulte o artigo [perfis de certificado](create-pfx-certificate-profiles.md).  

- Pode implementar o Windows Hello para as políticas de negócio para dispositivos Windows 10 associados a um domínio, que executam o cliente do Configuration Manager. Esta configuração é descrita no [configurar Windows Hello para empresas em dispositivos Windows 10 associados a domínios](../../protect/deploy-use/windows-hello-for-business-settings.md#configure-windows-hello-for-business-on-domain-joined-windows-10-devices). Quando estiver a utilizar o Configuration Manager com o Intune (híbrido), pode configurar estas definições em dispositivos Windows 10 Mobile e Windows 10, mas não no dispositivos associados a um domínio que executam o cliente do Configuration Manager.   

Para obter informações gerais sobre a configuração do Windows Hello para definições de empresas, consulte o artigo [Windows Hello para definições de negócio no System Center Configuration Manager](../../protect/deploy-use/windows-hello-for-business-settings.md).

## <a name="configure-windows-hello-for-business-settings-hybrid"></a>Configurar o Windows Hello para empresas definições (híbrido)  

1.  Na consola do Configuration Manager, clique em **administração** > **serviços em nuvem** > **subscrições do Microsoft Intune**.  

3.  Na lista, selecione a sua subscrição do Microsoft Intune e, em seguida, no separador **Base** , no grupo **Subscrição** , clique em **Configurar Plataformas** > **Windows (MDM)**.  

4.  No separador **Windows Hello para Empresas** da caixa de diálogo **Propriedades de Subscrição do Microsoft Intune** , escolha de entre os valores seguintes que irão afetar todos os dispositivos Windows 10 e Windows 10 Mobile inscritos:  

    -   **Desativar o Windows Hello para Empresas para dispositivos inscritos** ou **Ativar o Windows Hello para Empresas para dispositivos inscritos** - Ativa ou desativa a utilização do Windows Hello para Empresas em todos os dispositivos Windows 10 e Windows 10 Mobile inscritos.  

    -   **Utilizar um Trusted Platform Module (TPM)** - Um chip Trusted Platform Module (TPM) fornece uma camada adicional de segurança de dados. Escolha um dos seguintes valores:  

        -   **Necessário** (predefinição) - Apenas os dispositivos com um TPM acessível podem aprovisionar o Windows Hello para Empresas.  

        -   **Preferido** - Os dispositivos tentam utilizar primeiro um TPM. Se não estiver disponível, podem utilizar a encriptação de software  

    -   **Requerer comprimento mínimo do PIN** - Permite especificar o número mínimo de carateres necessários para o PIN do Windows Hello para Empresas. Tem de utilizar, pelo menos, 4 carateres (o valor predefinido é 6 carateres).  

    -   **Requerer comprimento máximo do PIN** - Permite especificar o número máximo de carateres permitidos para o PIN do Windows Hello para Empresas. Pode utilizar até 127 carateres.  

    -   **Requer letras minúsculas no PIN** - Permite especificar se têm de ser utilizadas letras em minúsculas no PIN do Windows Hello para Empresas. Escolha entre:  

        -   **Permitido** - Os utilizadores podem utilizar carateres minúsculos no PIN.  

        -   **Necessário** - Os utilizadores têm de incluir, pelo menos, um caráter minúsculo no PIN.  

        -   **Não permitido** (predefinição) - Os utilizadores não podem utilizar carateres minúsculos no PIN.  

    -   **Requer letras maiúsculas no PIN** - Permite especificar se têm de ser utilizadas letras em maiúsculas no PIN do Windows Hello para Empresas. Escolha entre:  

        -   **Permitido** - Os utilizadores podem utilizar carateres maiúsculos no PIN.  

        -   **Necessário** - Os utilizadores têm de incluir, pelo menos, um caráter maiúsculo no PIN.  

        -   **Não permitido** (predefinição) - Os utilizadores não podem utilizar carateres maiúsculos no PIN.  

    -   **Requerer carateres especiais** - Especifica a utilização de carateres especiais no PIN. Escolha entre:  

        -   **Permitido** - Os utilizadores podem utilizar carateres especiais no PIN.  

        -   **Necessário** - Os utilizadores têm de incluir, pelo menos, um caráter especial no PIN.  

        -   **Não permitido** (predefinição) - Os utilizadores não podem utilizar carateres especiais no PIN (este é também o comportamento se a definição não estiver configurada).  

         Os carateres especiais incluem: **! " # $ % & ' ( ) \* + , - . / : ; < = > ? @ [ \ ] ^ _ ` { &#124; } ~**.  

    -   **Requerer expiração do PIN (dias)** - Especifica o número de dias antes de ser necessário alterar o PIN do dispositivo. A predefinição é de 41 dias.  

    -   **Prevenir a reutilização de PINs anteriores** - Utilize esta definição para restringir a reutilização de PINs utilizados anteriormente. A predefinição é a impossibilidade de reutilizar os últimos cinco PINs utilizados.  

    -   **Ativar gestos biométricos** - Permite a autenticação biométrica, como reconhecimento facial ou impressão digital, como alternativa a um PIN para o Windows Hello para Empresas. Os utilizadores continuam a ter de configurar um PIN, para a eventualidade de a autenticação biométrica falhar.  

         Se estiver definido como **Ativado**, o Windows Hello para Empresas permite a autenticação biométrica.  Se estiver definido como **Desativado**, o Windows Hello para Empresas impede a autenticação biométrica (para todos os tipos de conta).  

    -   **Utilizar anti-spoofing avançado, quando disponível** - Configura se o anti-spoofing avançado é utilizado em dispositivos que o suportam.  

         Se estiver definido como **Ativado**, o Windows exige que todos os utilizadores utilizem anti-spoofing para funcionalidades faciais, quando suportado.  

    -   **Utilizar Passport Remoto** - Se esta opção estiver definida como **Ativado**, os utilizadores podem utilizar um Hello para Empresas remoto para servir de dispositivo complementar portátil para autenticação de computadores de secretária. O computador de secretária tem de estar associado ao Azure Active Directory e o dispositivo complementar tem de ser configurado com um PIN do Windows Hello para Empresas.  

5.  Quando concluir o procedimento, clique em **OK**.  

### <a name="see-also"></a>Consulte também  
 [Proteger a infraestrutura de dados e o site com o System Center Configuration Manager](../../protect/understand/protect-data-and-site-infrastructure.md)

 [Gerir a verificação de identidade com o Windows Hello for Business](https://technet.microsoft.com/itpro/windows/keep-secure/manage-identity-verification-using-microsoft-passport).  
