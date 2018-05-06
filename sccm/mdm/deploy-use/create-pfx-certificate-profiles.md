---
title: Criar perfis de certificado PFX através de uma autoridade de certificação
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
ms.openlocfilehash: a186e0b2c4b355cabcaaeb3b3124b65d3588fbc8
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-create-pfx-certificate-profiles-using-a-certificate-authority"></a>Como criar perfis de certificado PFX através de uma autoridade de certificação

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Aqui, irá aprender a criar um perfil de certificado que utiliza uma autoridade de certificação para credenciais.

[Perfis de certificado](../../protect/deploy-use/introduction-to-certificate-profiles.md) fornece informações gerais sobre como criar e configurar perfis de certificado. Este tópico realça algumas informações específicas sobre os perfis de certificados relacionados com os certificados PFX.

## <a name="pfx-certificate-profiles"></a>Perfis de certificado PFX
System Center Configuration Manager permite-lhe criar um perfil de certificado PFX utilizando credenciais emitidas por uma autoridade de certificação.  A partir da versão 1706, pode escolher a Microsoft ou Entrust como autoridade de certificado.  Quando implementada em dispositivos de utilizador, o ficheiros personal information exchange (. pfx) geram certificados específicos do utilizador para suportar a troca de dados encriptados.

Para importar as credenciais do certificado de ficheiros de certificado existente, consulte [como criar perfis de certificado PFX através da importação de detalhes do certificado](../../mdm/deploy-use/import-pfx-certificate-profiles.md).

## <a name="create-and-deploy-a-personal-information-exchange-pfx-certificate-profile"></a>Criar e implementar um perfil de certificado do Personal Information (Exchange PFX)  

### <a name="get-started"></a>Introdução

1.  Na consola do System Center Configuration Manager, escolha **ativos e compatibilidade**.  
2.  No **ativos e compatibilidade** área de trabalho, escolha **as definições de compatibilidade** &gt; **acesso a recursos da empresa** &gt; **perfis de certificado**.  

3.  No **home page** separador o **criar** grupo, escolha **criar perfil de certificado**.

4.  Na página **Geral** do Assistente **Criar Perfil de Certificado** , especifique as seguintes informações:  

    -   **Nome**: Introduza um nome exclusivo para o perfil de certificado. Pode utilizar até 256 carateres.  

    -   **Descrição**: Forneça uma descrição que proporcione uma descrição geral do perfil de certificado e outras informações relevantes que ajudem a identificá-lo na consola do System Center Configuration Manager. Pode utilizar até 256 carateres.  

    -   No **especificar o tipo de perfil de certificado que pretende criar**, escolha **Personal Information Exchange - definições do PKCS #12 (PFX) - criar** e, em seguida, escolha a sua autoridade de certificação da lista pendente.  A partir da versão 1706, pode optar por **Microsoft** ou **Entrust**.

### <a name="select-supported-platforms"></a>Selecione as plataformas suportadas

A página de plataformas suportadas identifica os sistemas operativos e dispositivos que suporta o perfil de certificado.  

Certificado perfis podem suportar vários sistemas operativos e dispositivos, no entanto, determinadas sistema operativo ou combinações de dispositivo podem necessitar de definições diferentes.  Nestes casos, é melhor criar perfis separados para cada conjunto exclusivo de definições.  

A partir da versão 1710, estão disponíveis as seguintes opções:

- Windows 10
    - Todas as edições Windows 10 (64-bit)
    - Todas as edições Windows 10 (32-bit)
    - Todas as edições Windows 10 (ARM64)
    - Todos os Windows 10 Holographic Enterprise e superiores
    - Todas as versões do Windows 10 Holographic e superiores
    - Todos os Windows 10 Team e superiores
    - Todos os Windows 10 Mobile e superiores
- iPhone
- iPad
- Android
- Android for Work

> [!Note]  
> Dispositivos de MacOS/OSX não são atualmente suportados.  

Quando não existem outras opções são selecionadas, o **Selecionar tudo** caixa de verificação seleciona todas as opções disponíveis.  Quando uma ou mais opções são selecionadas, **Selecionar tudo** limpa seleções existentes. 

1.  Selecione um ou mais plataformas suportadas pelo perfil de certificado.

1.  Escolha **seguinte** para continuar.  


### <a name="configure-certification-authorities"></a>Configurar as autoridades de certificação

Aqui, escolha o ponto de registo de certificados (CRP) para processar os certificados PFX.  

1.  Do **Site primário** lista, selecione o servidor que contém a função de CRP da AC.
1.  Na lista de **autoridades de certificação**, escolha a AC relevante ao colocar uma marca de verificação na coluna esquerda.
1.  Quando estiver pronto para continuar, escolha **seguinte**.

Para obter mais informações, consulte [infraestrutura de certificados](../../protect/deploy-use/certificate-infrastructure.md).


### <a name="configure-certificate-settings-for-microsoft-ca"></a>Configurar definições de certificado de AC da Microsoft

Para configurar definições de certificado quando utilizar o Microsoft como a AC:

1.  Do **nome do modelo de certificado** pendente, escolha o modelo de certificado.

1.  Ativar o **utilização de certificados** caixa de verificação para utilizar o perfil de certificado de assinatura S/MIME ou encriptação.

    Quando seleciona esta opção ao utilizar o Microsoft como a AC, todos os certificados PFX associados ao utilizador de destino são entregues para todos os dispositivos inscritos pelo utilizador.  Quando esta caixa de verificação está desmarcada, cada dispositivo recebe um certificado exclusivo.  

1.  Definir **formato de nome de requerente** quer **nome comum** ou **nome único totalmente**.  Se não souber que utilizar, contacte o administrador da autoridade de certificado.

1.  Para **nome alternativo do requerente**, ativar o **endereço de correio eletrónico** e **nome principal de utilizador (UPN)** conforme adequado para a AC.

1.  **Limiar de renovação** determina quando os certificados são automaticamente renovada, com base na percentagem de tempo restante antes de expiração.

1.  Definir o **período de validade do certificado** a duração do certificado.  O período é especificado pela definição de um número (1-100) e o período (anos, meses ou dias).

1.  O **publicação no Active Directory** é ativada quando o ponto de registo de certificados Especifica as credenciais do Active Directory.  Ative a opção para publicar o perfil de certificado no Active Directory.

1.  Se tiver selecionado um ou mais plataformas Windows 10, ao especificar as plataformas suportadas:

    1.  Definir **arquivo de certificados do Windows** para **utilizador**.  (O **computador Local** opção e não implementar certificados, a não deve ser selecionada.)
    1.  Selecione o **fornecedor de armazenamento de chaves (KSP)** uma das seguintes opções:

        - **Instalar no Trusted Platform Module (TPM), se estiver presente**  
        - **Instalar no Trusted Platform Module (TPM), caso contrário ocorre uma falha** 
        - **Instalação do Windows Hello para falhar caso contrário, de negócio** 
        - **Instalar no Fornecedor de Armazenamento de Chaves de Software** 

1.  Quando terminar, escolha **seguinte** ou **resumo**.

### <a name="configure-certificate-settings-for-entrust-ca"></a>Configurar definições de certificado de AC Entrust

Para configurar definições de certificado quando utilizar Entrust como AC:

1.  Do **digitais de ID de configuração** pendente, selecione o perfil de configuração.  As opções de configuração de ID digitais são criadas pelo administrador Entrust.

1.  Quando selecionado, o **utilização de certificados** utiliza o perfil de certificado de assinatura S/MIME ou encriptação.

    Quando utilizar Entrust como sendo a AC, todos os certificados PFX associados ao utilizador de destino são entregues para todos os dispositivos inscritos pelo utilizador.    Quando esta opção é *não* opção estiver marcada, cada dispositivo recebe um certificado exclusivo.  (Alterações de comportamento para ACs diferentes; para obter mais informações, consulte a secção correspondente.)

1.  Utilize o **formato** botão para mapear Entrust **formato de nome de requerente** tokens aos campos do ConfigMgr.  

    O **formatação de nome de certificado** caixa de diálogo apresenta uma lista de variáveis de configuração Entrust Digital ID.  Para cada variável Entrust, escolha a variável LDAP adequada na lista pendente associada.

1.  Utilize o **formato** botão para mapear Entrust **nome alternativo do requerente** tokens suportados variáveis de LDAP.  

    O **formatação de nome de certificado** caixa de diálogo apresenta uma lista de variáveis de configuração Entrust Digital ID.  Para cada variável Entrust, escolha a variável LDAP adequada na lista pendente associada.

1.  **Limiar de renovação** determina quando os certificados são automaticamente renovada, com base na percentagem de tempo restante antes de expiração.

1.  Definir o **período de validade do certificado** a duração do certificado.  O período é especificado pela definição de um número (1-100) e o período (anos, meses ou dias).

1.  O **publicação no Active Directory** é ativada quando o ponto de registo de certificados Especifica as credenciais do Active Directory.  Ative a opção para publicar o perfil de certificado no Active Directory.

1.  Se tiver selecionado um ou mais plataformas Windows 10, ao especificar as plataformas suportadas:

    1.  Definir **arquivo de certificados do Windows** para **utilizador**.  (O **computador Local** opção e não implementar certificados, a não deve ser selecionada.)
    1.  Selecione o **fornecedor de armazenamento de chaves (KSP)** uma das seguintes opções:

        - **Instalar no Trusted Platform Module (TPM), se estiver presente**  
        - **Instalar no Trusted Platform Module (TPM), caso contrário ocorre uma falha** 
        - **Instalação do Windows Hello para falhar caso contrário, de negócio** 
        - **Instalar no Fornecedor de Armazenamento de Chaves de Software** 

1.  Quando terminar, escolha **seguinte** ou **resumo**.


### <a name="finish-up"></a>Concluir a cópia de segurança

1.  Na página Resumo, reveja as suas seleções e verifique se as suas escolhas.

1.  Quando estiver pronto, escolha **seguinte** para criar o perfil.  

1.  O perfil do certificado que contém o ficheiro PFX está agora disponível a partir da área de trabalho **Perfis de Certificados** . 

1.  Para implementar o perfil:

    1. Abra o **ativos e compatibilidade** área de trabalho.
    1. Escolha **as definições de compatibilidade** > **acesso a recursos da empresa** > **perfis de certificado**
    1. Faça duplo clique o perfil de certificado pretendido e, em seguida, escolha **implementar**. 


## <a name="see-also"></a>Consulte também
[Criar um novo perfil de certificado](../../protect/deploy-use/create-certificate-profiles.md) orienta-o através do Assistente para criar perfil de certificado.

[Como criar perfis de certificado PFX através da importação de detalhes do certificado](../../mdm/deploy-use/import-pfx-certificate-profiles.md)

[Implementar Wi-Fi, VPN, e-mail e perfis de certificado](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md) descreve como implementar perfis de certificado.