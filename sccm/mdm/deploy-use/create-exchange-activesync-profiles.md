---
title: Criar perfis de e-mail do Exchange ActiveSync | Documentos do Microsoft
description: Saiba como criar e configurar perfis de e-mail no System Center Configuration Manager que funcionam com o Microsoft Intune.
ms.custom: na
ms.date: 03/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 120442be-179e-450c-a0c4-284046895da3
caps.latest.revision: 4
caps.handback.revision: 0
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 761c3f58f7c57d8f87ee802da37821895062546d
ms.openlocfilehash: bcf337d2abbcd5aad0f99098f6afd4a73ada3a0b
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---

# <a name="exchange-activesync-email-profiles-in-system-center-configuration-manager"></a>Perfis de e-mail do Exchange ActiveSync no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Ao utilizar o Microsoft Intune e Exchange ActiveSync, pode configurar dispositivos com perfis de e-mail e restrições. Isto permite aos seus utilizadores acesso um e-mail empresarial nos respetivos dispositivos com um mínimo de informações de configuração por parte dos mesmos.  

 Pode configurar os seguintes tipos de dispositivos com perfis de e-mail:  

- Windows 10
- Windows Phone 8.1
- Windows Phone 8.0
- iPhones a executar o iOS 5, iOS 6, iOS 7 e iOS 8  
- iPads a executar o iOS 5, iOS 6, iOS 7 e iOS 8  
- Samsung KNOX Standard (4 e posterior)
- Android for Work

Para implementar perfis de e-mail em dispositivos, têm de inscrever os dispositivos no Intune. Para obter mais informações sobre como inscrever os seus dispositivos, consulte [Gerir dispositivos móveis com o Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx).

> [!NOTE]
> Intune fornece dois Android para perfis de e-mail de trabalho, uma cada para a aplicação de correio eletrónico do Gmail e a aplicação de correio eletrónico nove trabalho. Estas aplicações estão disponíveis no Google Play Store e suportam ligações ao Exchange. Para ativar a conectividade de e-mail, implemente uma destas aplicações de correio eletrónico para os dispositivos dos utilizadores e, em seguida, criar e implementar o perfil adequado. As aplicações de e-mail como o trabalho nove poderão não estar livres. Do revisão da aplicação licenciamento detalhes ou contacte a empresa de aplicação com todas as perguntas.

 Para além de configurar uma conta de e-mail no dispositivo, pode configurar as definições de sincronização para contactos, calendários e tarefas.  

 Quando cria um perfil de e-mail, pode incluir um vasto leque de definições de segurança. Estas definições incluem certificados para identidade, encriptação e assinatura que configurou através da utilização de perfis de certificado do System Center Configuration Manager. Para obter mais informações sobre perfis de certificado, veja [Perfis de certificado no System Center Configuration Manager](/sccm/protect/deploy-use/introduction-to-certificate-profiles).    

## <a name="create-an-exchange-activesync-email-profile"></a>Criar um perfil de e-mail do Exchange ActiveSync  

Para criar um perfil, utilize o Exchange ActiveSync E-Mail Assistente para criar perfil. 

1.  Na consola do Configuration Manager, escolha **ativos e compatibilidade**.  

2.  No **ativos e compatibilidade** área de trabalho, expanda **definições de compatibilidade**, expanda **acesso a recursos da empresa**e, em seguida, escolha **perfis de E-Mail**.  

3.  No **base** separador o **criar** grupo, selecione **criar perfil de E-Mail do Exchange ActiveSync** para iniciar o assistente.

4.  No **geral** página do assistente, configure as seguintes opções:

    - **Nome**. Forneça um nome descritivo para o perfil de e-mail.

    - **Descrição**. Opcionalmente, forneça uma descrição para o perfil de e-mail que irão ajudar a identificá-la na consola do Configuration Manager.

    - **Este perfil de e-mail é para Android para trabalhar**. Escolha esta opção se irá implementar este perfil de correio eletrónico apenas Android para dispositivos de trabalho. Se selecionar esta caixa, o **plataformas suportadas** não é apresentada a página do assistente. Android apenas para perfis de e-mail de trabalho estão configurados.

4.  No **do Exchange ActiveSync** página do assistente, especifique as seguintes informações:  

    -   **Anfitrião do Exchange ActiveSync**. Especifique o nome de anfitrião do Exchange server da empresa que aloja serviços do Exchange ActiveSync.  

    -   **Nome da conta**. Especifique o nome a apresentar para a conta de correio eletrónico tal como será apresentado aos utilizadores nos respetivos dispositivos.  

    -   **Nome da conta de utilizador**. Escolha a forma como o nome de utilizador de conta de e-mail está configurado nos dispositivos cliente. É possível escolher uma das seguintes opções da lista pendente:  

        -   **Nome Principal de utilizador**. Utilize o nome principal de utilizador completo para iniciar sessão no Exchange.  

        -   **AccountName**. Utilize o nome de conta de utilizador completo do Active Directory.

        -   **Endereço SMTP principal**. Utilize o endereço SMTP principal do utilizador para iniciar sessão no Exchange.  

    -   **Endereço de correio eletrónico**. Escolha como é gerado o endereço de e-mail para o utilizador em cada dispositivo cliente. É possível escolher uma das seguintes opções da lista pendente:  

        -   **Endereço SMTP principal**. Utilize o endereço SMTP principal do utilizador para iniciar sessão no Exchange.  

        -   **Nome Principal de utilizador**. Utilize o nome principal de utilizador completo como o endereço de correio eletrónico.  

    -   **Domínio da conta**. Escolha uma das seguintes opções:  

        -   **Obter do Active Directory**  

        -   **Personalizar**  

         Este campo é aplicável apenas se **sAMAccountName** está selecionada no **nome da conta de utilizador** na lista pendente.  

    -   **Método de autenticação**. Escolha um dos seguintes métodos de autenticação que serão utilizados para autenticar a ligação ao Exchange ActiveSync:  

        -   **Certificados**. Um certificado de identidade será utilizado para autenticar a ligação do Exchange ActiveSync.  

        -   **Nome de utilizador e palavra-passe**. O utilizador do dispositivo tem de fornecer uma palavra-passe para ligar ao Exchange ActiveSync. (O nome de utilizador é configurado como parte do perfil de e-mail.)  

    -   **Certificado de identidade**. Escolher **selecione** e, em seguida, selecione um certificado a utilizar para a identidade.  

        > [!NOTE]  
        > Antes de poder escolher o certificado de identidade, deve configurá-lo primeiro como um perfil de certificado Simple Certificate Enrollment Protocol (SCEP). Para obter mais informações sobre perfis de certificado, veja [Perfis de certificado no System Center Configuration Manager](/sccm/protect/deploy-use/introduction-to-certificate-profiles).  

         Esta opção só está disponível se optou por **certificados** em **método de autenticação**.  

    -   **Utilizar S/MIME**. Envie e-mail de envio utilizando a encriptação S/MIME. Esta opção só é aplicável a dispositivos iOS. Pode escolher uma das seguintes opções:

        -   **Certificados de encriptação**. Escolher **selecione** e, em seguida, selecione um certificado a utilizar para encriptação. Pode escolher apenas um certificado PFX para utilizar como um certificado de encriptação.

        Se escolher um certificado de encriptação e um certificado de assinatura, estas devem ser ambos no formato PFX.

        > [!NOTE]  
        > Antes de poder escolher certificados, tem primeiro de configurá-los como um perfil de certificado SCEP ou PFX. Para obter mais informações sobre perfis de certificado, veja [Perfis de certificado no System Center Configuration Manager](/sccm/protect/deploy-use/introduction-to-certificate-profiles).  

## <a name="configure-synchronization-settings-for-the-exchange-activesync-email-profile"></a>Configurar definições de sincronização para o perfil de e-mail do Exchange ActiveSync  

Na página **Configurar definições de sincronização** do Assistente para Criar um Perfil de E-mail do Exchange ActiveSync, especifique as seguintes informações:  

-   **Agenda**. Escolha o agendamento através do qual dispositivos irão sincronizar dados do Exchange server. Esta opção só é aplicável a dispositivos Windows Phone. Escolha entre:  

    -   **Não configurado**. Não é imposto um agendamento de sincronização. Isto permite que os utilizadores configurem o seu próprio agendamento de sincronização.  

    -   **Chegarem novas mensagens**. Dados, tal como itens de calendário e mensagens de correio eletrónico serão automaticamente sincronizados quando chegarem.  

    -   **15 minutos**. Os dados como itens de calendário e mensagens de correio eletrónico serão automaticamente sincronizados a cada 15 minutos.  

    -   **30 minutos**. Os dados como itens de calendário e mensagens de correio eletrónico serão automaticamente sincronizados a cada 30 minutos.  

    -   **60 minutos**. Os dados como itens de calendário e mensagens de correio eletrónico serão automaticamente sincronizados a cada 60 minutos.  

    -   **Manual**. O utilizador do dispositivo tem de Iniciar sincronização manualmente.  

-   **Número de dias de e-mail a sincronizar**. Na lista pendente, escolha o número de dias de e-mail que pretende sincronizar. Escolha um dos seguintes valores:  

    -   **Não configurado**. A definição não é imposta. -Permite que os utilizadores configurem a quantidade de e-mails é transferido para o respetivo dispositivo.  

    -   **Ilimitado**. Sincronize todos os e-mails disponíveis.  

    -   **1 dia**  

    -   **3 dias**  

    -   **1 semana**  

    -   **2 semanas**  

    -   **1 mês**  

-   **Permitir que as mensagens sejam movidas para outras contas de e-mail**. Escolha esta opção para permitir que os utilizadores movam mensagens de e-mail entre contas diferentes configuradas nos respetivos dispositivos. Esta opção só é aplicável a dispositivos iOS.  

-   **Permitir que o e-mail seja enviado a partir de aplicações de terceiros**. Escolha esta opção para permitir que os utilizadores enviem e-mails de determinadas aplicações de e-mail de terceiros não predefinidas. Esta opção só é aplicável a dispositivos iOS.  

-   **Sincronizar endereços de e-mail utilizados recentemente**. Escolha esta opção para sincronizar a lista de endereços de e-mail que foram utilizados recentemente no dispositivo. Esta opção só é aplicável a dispositivos iOS.  

-   **Utilizar SSL**. Escolha esta opção para utilizar a comunicação de Secure Sockets Layer (SSL) para mensagens de correio eletrónico a enviar, receber e-mails e ao comunicar com o Exchange server.  

-   **Tipo para sincronizar de conteúdo**. Escolha os tipos de conteúdo que pretende sincronizar nos dispositivos. Esta opção só é aplicável a dispositivos Windows Phone. Escolha entre:  

    -   **E-mail**  

    -   **Contactos**  

    -   **Calendário**  

    -   **Tarefas**  

## <a name="specify-supported-platforms-for-the-exchange-activesync-email-profile"></a>Especificar as plataformas suportadas para o perfil de e-mail do Exchange ActiveSync  

1.  No **plataformas suportadas** página do Exchange ActiveSync perfil Assistente para criar E-Mail, selecione os sistemas operativos nos quais o perfil de e-mail será instalado. Em alternativa, selecione **Selecionar tudo** para instalar o perfil de e-mail em todos os sistemas operativos disponíveis.  

2.  Conclua o assistente.

Para obter informações sobre como implementar os perfis de e-mail do Exchange ActiveSync, consulte o artigo [como implementar perfis no System Center Configuration Manager](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md).  

