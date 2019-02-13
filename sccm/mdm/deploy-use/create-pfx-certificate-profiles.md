---
title: Criar perfis de certificado PFX com uma autoridade de certificação
titleSuffix: Configuration Manager
description: Saiba como utilizar ficheiros PFX no System Center Configuration Manager para gerar certificados específicos do utilizador que suportam a troca de dados encriptados.
ms.date: 11/01/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: d240a836-c49b-49ab-a920-784c062d6748
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6bbe52a282db016077cb96144938a0d443955f6c
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56127444"
---
# <a name="how-to-create-pfx-certificate-profiles-using-a-certificate-authority"></a>Como criar perfis de certificado PFX com uma autoridade de certificação

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Aqui, irá aprender a criar um perfil de certificado que utiliza uma autoridade de certificação para as credenciais.

[Perfis de certificado](../../protect/deploy-use/introduction-to-certificate-profiles.md) fornece informações gerais sobre como criar e configurar perfis de certificado. Este tópico destaca algumas informações específicas sobre os perfis de certificado relacionadas com certificados PFX.

## <a name="pfx-certificate-profiles"></a>Perfis de certificado PFX
System Center Configuration Manager permite-lhe criar um perfil de certificado PFX com credenciais emitidas por uma autoridade de certificação.  A partir da versão 1706, pode escolher a Microsoft ou da Entrust como sua autoridade de certificação.  Quando implementada em dispositivos de utilizador, ficheiros personal information exchange (. pfx) geram certificados específicos do utilizador para suportar a troca de dados encriptados.

Para importar as credenciais de certificado de ficheiros de certificado existente, consulte [como criar perfis de certificado PFX através da importação de detalhes do certificado](../../mdm/deploy-use/import-pfx-certificate-profiles.md).

## <a name="create-and-deploy-a-personal-information-exchange-pfx-certificate-profile"></a>Criar e implementar um perfil de certificado Personal Information Exchange (PFX)  

### <a name="get-started"></a>Introdução

1.  Na consola do System Center Configuration Manager, escolha **ativos e compatibilidade**.  
2.  Na **ativos e compatibilidade** área de trabalho, escolha **definições de compatibilidade** &gt; **acesso a recursos da empresa** &gt;  **Perfis de certificado**.  

3.  Sobre o **home page** separador a **criar** de grupo, escolha **criar perfil de certificado**.

4.  Na página **Geral** do Assistente **Criar Perfil de Certificado** , especifique as seguintes informações:  

    -   **Nome**: Introduza um nome exclusivo para o perfil de certificado. Pode utilizar até 256 carateres.  

    -   **Descrição**: Forneça uma descrição que proporcione uma descrição geral do perfil de certificado e outras informações relevantes que ajudem a identificá-lo na consola do System Center Configuration Manager. Pode utilizar até 256 carateres.  

    -   Na **especifique o tipo de perfil de certificado que pretende criar**, escolha **Personal Information Exchange – definições PKCS #12 (PFX) - criar** e, em seguida, escolha a sua autoridade de certificação das na lista pendente.  A partir da versão 1706, pode escolher **Microsoft** ou **Entrust**.

### <a name="select-supported-platforms"></a>Selecione as plataformas suportadas

A página de plataformas suportadas identifica os sistemas operativos e dispositivos que suporta o perfil de certificado.  

Certificado de perfis podem suportar vários sistemas operativos e dispositivos, no entanto, determinadas sistema operativo ou combinações de dispositivo podem exigir configurações diferentes.  Nestes casos, é melhor criar perfis separados para cada conjunto exclusivo de definições.  

A partir da versão 1710, as seguintes opções estão disponíveis:

- Windows 10
    - Todos os Windows 10 (64-bit)
    - Todos os Windows 10 (32-bit)
    - All Windows 10 (ARM64)
    - Todos os Windows 10 Holographic Enterprise e superior
    - De de Windows 10 Holographic todas as e superior
    - Todos os Windows 10 Team e superiores
    - De todos os Windows 10 Mobile e superior
- iPhone
- iPad
- Android
- Android for Work

> [!Note]  
> Dispositivos MacOS/OSX não são atualmente suportados.  

Quando não existem outras opções estão selecionadas, o **Selecionar tudo** caixa de verificação seleciona todas as opções disponíveis.  Quando uma ou mais opções estão selecionadas, **Selecionar tudo** limpa seleções existentes. 

1.  Selecione uma ou mais plataformas suportadas pelo perfil do certificado.

1.  Escolher **seguinte** para continuar.  


### <a name="configure-certification-authorities"></a>Configurar autoridades de certificação

Aqui, escolher o ponto de registo de certificados (CRP) para processar os certificados PFX.  

1.  Partir do **Site primário** lista, selecione o servidor que contém a função de CRP para a AC.
1.  Na lista de **autoridades de certificação**, escolha a AC relevante ao colocar uma marca de verificação na coluna esquerda.
1.  Quando estiver pronto para continuar, escolha **seguinte**.

Para obter mais informações, consulte [infraestrutura de certificados](../../protect/deploy-use/certificate-infrastructure.md).


### <a name="configure-certificate-settings-for-microsoft-ca"></a>Configurar definições de certificado de AC da Microsoft

Para configurar definições de certificado ao utilizar o Microsoft da AC:

1.  Partir do **nome do modelo de certificado** pendente, escolha o modelo de certificado.

1.  Ativar a **utilização de certificados** caixa de verificação para utilizar o perfil de certificado para assinatura S/MIME ou encriptação.

    Quando seleciona esta opção, ao utilizar o Microsoft da AC, todos os certificados PFX associados ao utilizador de destino são entregues para todos os dispositivos inscritos pelo utilizador.  Quando esta caixa de verificação estiver desmarcada, cada dispositivo recebe um certificado exclusivo.  

1.  Definir **formato de nome de requerente** a qualquer uma **nome comum** ou **nome único totalmente**.  Se não souber que utilizar, contacte o administrador de autoridade de certificado.

1.  Para **nome alternativo do requerente**, ativar a **endereço de E-Mail** e **nome do principal de utilizador (UPN)** conforme adequado para a sua autoridade de certificação.

1.  **Limiar de renovação** determina quando os certificados são automaticamente renovada, com base na percentagem de tempo restante antes de expirar.

1.  Definir o **período de validade do certificado** do tempo de vida do certificado.  O período é especificado através da definição de um número (1 a 100) e o período (anos, meses ou dias).

1.  O **publicação no Active Directory** é ativada quando o ponto de registo de certificados Especifica credenciais do Active Directory.  Ative a opção para publicar o perfil de certificado no Active Directory.

1.  Se tiver selecionado um ou mais plataformas do Windows 10 ao especificar as plataformas suportadas:

    1.  Definir **arquivo de certificados do Windows** ao **utilizador**.  (A **computador Local** escolha não implementa certificados e não deve ser escolhida.)
    1.  Selecione o **fornecedor de armazenamento de chaves (KSP)** de uma das seguintes opções:

        - **Instalar no Trusted Platform Module (TPM), se estiver presente**  
        - **Instalar no Trusted Platform Module (TPM), caso contrário ocorre uma falha** 
        - **Instalar no Windows Hello para ou não de negócios** 
        - **Instalar no Fornecedor de Armazenamento de Chaves de Software** 

1.  Quando terminar, escolha **próxima** ou **resumo**.

### <a name="configure-certificate-settings-for-entrust-ca"></a>Configurar definições de certificado de CA da Entrust

Para configurar definições de certificado ao utilizar Entrust da AC:

1.  Partir do **configuração do ID Digital** pendente, selecione o perfil de configuração.  As opções de configuração do ID digital são criadas pelo administrador do Entrust.

1.  Quando selecionado, o **utilização de certificados** utiliza o perfil de certificado de assinatura de S/MIME ou encriptação.

    Quando utilizar Entrust da AC, todos os certificados PFX associados ao utilizador de destino são entregues para todos os dispositivos inscritos pelo utilizador.    Quando esta opção está *não* opção estiver marcada, cada dispositivo recebe um certificado exclusivo.  (Comportamento muda para o ACS diferentes; para obter mais informações, consulte a seção correspondente).

1.  Utilize o **formato** botão mapear Entrust **formato de nome de requerente** tokens para os campos do ConfigMgr.  

    O **formatação de nome de certificado** caixa de diálogo lista as variáveis de configuração do Entrust Digital ID.  Para cada variável Entrust, escolha a variável LDAP apropriada na lista pendente associada.

1.  Utilize o **formato** botão mapear Entrust **nome alternativo do requerente** tokens para variáveis suportadas do LDAP.  

    O **formatação de nome de certificado** caixa de diálogo lista as variáveis de configuração do Entrust Digital ID.  Para cada variável Entrust, escolha a variável LDAP apropriada na lista pendente associada.

1.  **Limiar de renovação** determina quando os certificados são automaticamente renovada, com base na percentagem de tempo restante antes de expirar.

1.  Definir o **período de validade do certificado** do tempo de vida do certificado.  O período é especificado através da definição de um número (1 a 100) e o período (anos, meses ou dias).

1.  O **publicação no Active Directory** é ativada quando o ponto de registo de certificados Especifica credenciais do Active Directory.  Ative a opção para publicar o perfil de certificado no Active Directory.

1.  Se tiver selecionado um ou mais plataformas do Windows 10 ao especificar as plataformas suportadas:

    1.  Definir **arquivo de certificados do Windows** ao **utilizador**.  (A **computador Local** escolha não implementa certificados e não deve ser escolhida.)
    1.  Selecione o **fornecedor de armazenamento de chaves (KSP)** de uma das seguintes opções:

        - **Instalar no Trusted Platform Module (TPM), se estiver presente**  
        - **Instalar no Trusted Platform Module (TPM), caso contrário ocorre uma falha** 
        - **Instalar no Windows Hello para ou não de negócios** 
        - **Instalar no Fornecedor de Armazenamento de Chaves de Software** 

1.  Quando terminar, escolha **próxima** ou **resumo**.


### <a name="finish-up"></a>Concluir a cópia de segurança

1.  Na página resumida, reveja as suas seleções e verifique se as suas opções.

1.  Quando estiver pronto, escolha **seguinte** para criar o perfil.  

1.  O perfil do certificado que contém o ficheiro PFX está agora disponível a partir da área de trabalho **Perfis de Certificados** . 

1.  Para implementar o perfil:

    1. Abra o **ativos e compatibilidade** área de trabalho.
    1. Escolher **definições de compatibilidade** > **acesso a recursos da empresa** > **perfis de certificado**
    1. O perfil de certificado pretendido com o botão direito e, em seguida, escolha **Deploy**. 


## <a name="see-also"></a>Consulte também
[Criar um novo perfil de certificado](../../protect/deploy-use/create-certificate-profiles.md) orienta-o Assistente para criar perfil de certificado.

[Como criar perfis de certificado PFX através da importação de detalhes do certificado](../../mdm/deploy-use/import-pfx-certificate-profiles.md)

[Implementar o Wi-Fi, VPN, e-mail e perfis de certificado](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md) descreve como implementar perfis de certificado.
