---
title: Definições do Windows Hello para Empresas
titleSuffix: Configuration Manager
description: Saiba como integrar o Windows Hello para empresas com o Configuration Manager.
ms.date: 12/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: c0593c07-5dd7-4d23-a0d8-d30165f49ef7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 71f853034133e2ec73a4d8e606c2e0c0c94841a4
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56134083"
---
# <a name="windows-hello-for-business-settings-in-configuration-manager-hybrid"></a>Windows Hello para empresas no Configuration Manager (híbrido)

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O Configuration Manager permite integrar com o Windows Hello para empresas (anteriormente chamado Microsoft Passport para Windows), que é um método de-de início de sessão alternativo para dispositivos Windows 10. O Hello para Empresas utiliza o Active Directory ou uma conta do Azure Active Directory para substituir uma palavra-passe, um smart card ou um smart card virtual. Com o Hello para Empresas, pode utilizar um **gesto de utilizador** para iniciar sessão, em vez de uma palavra-passe. Um gesto de utilizador pode ser um PIN simples, uma autenticação biométrica ou um dispositivo externo, como um leitor de impressões digitais.  

> [!Important]  
> A partir de Dezembro de 2017, Windows Hello para empresas no Configuration Manager é uma [funcionalidade preterida](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Implantação do Windows Server 2016 Active Directory Federation serviços autoridade de registo (RA-ADFS) é mais simples, fornece uma melhor experiência de utilizador e tem uma experiência de inscrição de certificados mais determinística. Para obter mais informações, consulte [Windows Hello para empresas](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-identity-verification).  


O Configuration Manager integra-se com o Windows Hello para empresas de duas formas:  

- Pode utilizar o Configuration Manager para controlar que utilizadores de gestos podem em não podem utilizar para iniciar sessão.  

- Pode armazenar certificados de autenticação no fornecedor de armazenamento de chaves (KSP) do Windows Hello para Empresas. Para obter mais informações, consulte [perfis de certificado](create-pfx-certificate-profiles.md).  

- Pode implantar Windows Hello para políticas de negócio para dispositivos Windows 10 associados a um domínio, que executam o cliente do Configuration Manager. Esta configuração está descrita no [configurar o Windows Hello para empresas em dispositivos do Windows 10 associados a um domínio](/sccm/protect/deploy-use/windows-hello-for-business-settings#configure-windows-hello-for-business-on-domain-joined-windows-10-devices). Quando estiver a utilizar o Configuration Manager com o Intune (híbrido), pode configurar estas definições em dispositivos Windows 10 Mobile e Windows 10, mas não em dispositivos associados a um domínio que executam o cliente do Configuration Manager.   

Para obter informações gerais sobre como configurar o Windows Hello para empresas, consulte [Windows Hello para empresas no Configuration Manager](/sccm/protect/deploy-use/windows-hello-for-business-settings).



## <a name="configure-windows-hello-for-business-settings-hybrid"></a>Configurar o Windows Hello para empresas (híbrido) de definições  

1. Na consola do Configuration Manager, clique em **Administration** > **serviços Cloud** > **subscrições do Microsoft Intune**.  

2. Na lista, selecione a sua subscrição do Microsoft Intune e, em seguida, no separador **Base** , no grupo **Subscrição** , clique em **Configurar Plataformas** > **Windows (MDM)**.  

3. No separador **Windows Hello para Empresas** da caixa de diálogo **Propriedades de Subscrição do Microsoft Intune** , escolha de entre os valores seguintes que irão afetar todos os dispositivos Windows 10 e Windows 10 Mobile inscritos:  

   - **Desativar o Windows Hello para Empresas para dispositivos inscritos** ou **Ativar o Windows Hello para Empresas para dispositivos inscritos** - Ativa ou desativa a utilização do Windows Hello para Empresas em todos os dispositivos Windows 10 e Windows 10 Mobile inscritos.  

   - **Utilizar um Trusted Platform Module (TPM)** - Um chip Trusted Platform Module (TPM) fornece uma camada adicional de segurança de dados. Escolha um dos seguintes valores:  

     -   **Necessário** (predefinição) - Apenas os dispositivos com um TPM acessível podem aprovisionar o Windows Hello para Empresas.  

     -   **Preferido** - Os dispositivos tentam utilizar primeiro um TPM. Se não estiver disponível, podem utilizar a encriptação de software  

   - **Requerer comprimento mínimo do PIN** - Permite especificar o número mínimo de carateres necessários para o PIN do Windows Hello para Empresas. Tem de utilizar, pelo menos, 4 carateres (o valor predefinido é 6 carateres).  

   - **Requerer comprimento máximo do PIN** - Permite especificar o número máximo de carateres permitidos para o PIN do Windows Hello para Empresas. Pode utilizar até 127 carateres.  

   - **Requer letras minúsculas no PIN** - Permite especificar se têm de ser utilizadas letras em minúsculas no PIN do Windows Hello para Empresas. Escolha entre:  

     -   **Permitido** - Os utilizadores podem utilizar carateres minúsculos no PIN.  

     -   **Necessário** - Os utilizadores têm de incluir, pelo menos, um caráter minúsculo no PIN.  

     -   **Não permitido** (predefinição) - Os utilizadores não podem utilizar carateres minúsculos no PIN.  

   - **Requer letras maiúsculas no PIN** - Permite especificar se têm de ser utilizadas letras em maiúsculas no PIN do Windows Hello para Empresas. Escolha entre:  

     -   **Permitido** - Os utilizadores podem utilizar carateres maiúsculos no PIN.  

     -   **Necessário** - Os utilizadores têm de incluir, pelo menos, um caráter maiúsculo no PIN.  

     -   **Não permitido** (predefinição) - Os utilizadores não podem utilizar carateres maiúsculos no PIN.  

   - **Requerer carateres especiais** - Especifica a utilização de carateres especiais no PIN. Escolha entre:  

     - **Permitido** - Os utilizadores podem utilizar carateres especiais no PIN.  

     - **Necessário** - Os utilizadores têm de incluir, pelo menos, um caráter especial no PIN.  

     - **Não permitido** (predefinição) - Os utilizadores não podem utilizar carateres especiais no PIN (este é também o comportamento se a definição não estiver configurada).  

       Os carateres especiais incluem: **! " # $ % & ' ( ) \* + , - . / : ; < = > ? @ [ \ ] ^ _ ` { &#124; } ~**.  

   - **Requerer expiração do PIN (dias)** - Especifica o número de dias antes de ser necessário alterar o PIN do dispositivo. A predefinição é de 41 dias.  

   - **Prevenir a reutilização de PINs anteriores** - Utilize esta definição para restringir a reutilização de PINs utilizados anteriormente. A predefinição é a impossibilidade de reutilizar os últimos cinco PINs utilizados.  

   - **Ativar gestos biométricos** - Permite a autenticação biométrica, como reconhecimento facial ou impressão digital, como alternativa a um PIN para o Windows Hello para Empresas. Os utilizadores continuam a ter de configurar um PIN, para a eventualidade de a autenticação biométrica falhar.  

      Se estiver definido como **Ativado**, o Windows Hello para Empresas permite a autenticação biométrica.  Se estiver definido como **Desativado**, o Windows Hello para Empresas impede a autenticação biométrica (para todos os tipos de conta).  

   - **Utilizar anti-spoofing avançado, quando disponível** - Configura se o anti-spoofing avançado é utilizado em dispositivos que o suportam.  

      Se estiver definido como **Ativado**, o Windows exige que todos os utilizadores utilizem anti-spoofing para funcionalidades faciais, quando suportado.  

   - **Utilizar Passport Remoto** - Se esta opção estiver definida como **Ativado**, os utilizadores podem utilizar um Hello para Empresas remoto para servir de dispositivo complementar portátil para autenticação de computadores de secretária. O computador de secretária tem de estar associado ao Azure Active Directory e o dispositivo complementar tem de ser configurado com um PIN do Windows Hello para Empresas.  

4. Quando concluir o procedimento, clique em **OK**.  



## <a name="see-also"></a>Consulte também  

[Proteger a infraestrutura de dados e do site](/sccm/protect/understand/protect-data-and-site-infrastructure)

[Windows Hello para Empresas](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification)  
