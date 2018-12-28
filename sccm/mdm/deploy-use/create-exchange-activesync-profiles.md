---
title: Criar perfis de e-mail do Exchange ActiveSync
titleSuffix: Configuration Manager
description: Saiba como criar e configurar perfis de e-mail no System Center Configuration Manager que funcionam com o Microsoft Intune.
ms.date: 07/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 120442be-179e-450c-a0c4-284046895da3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: decd16a03a0381718ada3e4c977d10c159c6be25
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53417069"
---
# <a name="exchange-activesync-email-profiles-in-system-center-configuration-manager"></a>Perfis de e-mail do Exchange ActiveSync no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Ao utilizar o Microsoft Intune e o Exchange ActiveSync, pode configurar dispositivos com perfis de e-mail e restrições. Isso permite que o seu e-mail empresarial de acesso de utilizadores nos respetivos dispositivos com requisitos mínimos de configuração por parte dos mesmos.  

 Pode configurar os seguintes tipos de dispositivos com perfis de e-mail:  

- Windows 10
- Windows Phone 8.1
- iPhones, com o iOS 9 e posterior 
- iPads com o iOS 9 e posteriores 
- Samsung KNOX Standard (4 e posterior)
- Android for Work

Para implementar perfis de e-mail em dispositivos, têm de inscrever os dispositivos no Intune. Para obter mais informações sobre como inscrever os seus dispositivos, consulte [Gerir dispositivos móveis com o Microsoft Intune](https://technet.microsoft.com/library/dn646962.aspx).

> [!NOTE]
> O Intune fornece dois Android para perfis de e-mail de trabalho, um para a aplicação de e-mail Gmail e a aplicação de e-mail Nine Work. Estas aplicações estão disponíveis na Store de Play Google e suportam ligações ao Exchange. Para ativar a conectividade de e-mail, implemente uma destas aplicações de e-mail nos dispositivos dos seus utilizadores e, em seguida, crie e implemente o perfil adequado. Aplicações de e-mail, como o Nine Work poderão não ser gratuitas. Do revisão da aplicação detalhes de licenciamento ou entre em contato com a empresa da aplicação com as suas questões.

 Além de configurar uma conta de e-mail no dispositivo, pode configurar as definições de sincronização para contactos, calendários e tarefas.  

 Quando cria um perfil de e-mail, pode incluir uma grande variedade de definições de segurança. Estas definições incluem certificados para identidade, encriptação e assinatura que foram configurados ao utilizar perfis de certificado do System Center Configuration Manager. Para obter mais informações sobre perfis de certificado, veja [Perfis de certificado no System Center Configuration Manager](/sccm/protect/deploy-use/introduction-to-certificate-profiles.md).    

## <a name="create-an-exchange-activesync-email-profile"></a>Criar um perfil de e-mail do Exchange ActiveSync  

Para criar um perfil, use o Exchange ActiveSync Email Assistente para criar perfil. 

1. Na consola do Configuration Manager, escolha **ativos e compatibilidade**.  

2. Na **ativos e compatibilidade** área de trabalho, expanda **definições de compatibilidade**, expanda **acesso a recursos da empresa**e, em seguida, escolha **osperfisdeE-Mail**.  

3. Sobre o **home page** separador a **criar** de grupo, escolha **criar perfil de E-Mail do Exchange ActiveSync** para iniciar o assistente.

4. Sobre o **gerais** página do assistente, configure o seguinte:

   - **Nome**. Forneça um nome descritivo para o perfil de e-mail.

   - **Descrição**. Opcionalmente, forneça uma descrição para o perfil de e-mail que irá ajudar a identificá-la na consola do Configuration Manager.

   - **Este perfil de e-mail é para Android for Work**. Escolha esta opção se implantará este perfil de e-mail apenas dispositivos Android for Work. Se selecionar esta caixa, o **plataformas suportadas** não é apresentada a página do assistente. Android apenas para perfis de e-mail de trabalho são configurados.

5. Sobre o **Exchange ActiveSync** página do assistente, especifique as seguintes informações:  

   - **Anfitrião do Exchange ActiveSync**. Especifique o nome de anfitrião do servidor do Exchange da empresa que aloja serviços do Exchange ActiveSync.  

   - **Nome da conta**. Especifique o nome a apresentar para a conta de e-mail conforme será apresentado aos utilizadores nos respetivos dispositivos.  

   - **Nome da conta de utilizador**. Escolha a forma como o nome de utilizador de conta de e-mail está configurado nos dispositivos cliente. Pode escolher uma das seguintes opções da lista pendente:  

     -   **Nome Principal de utilizador**. Utilize o nome de principal de utilizador completo para iniciar sessão no Exchange.  

     -   **AccountName**. Utilize o nome de conta de utilizador completo do Active Directory.

     -   **Endereço SMTP principal**. Utilize o endereço SMTP principal do utilizador para iniciar sessão no Exchange.  

   - **Endereço de e-mail**. Escolha como é gerado o endereço de e-mail para o utilizador em cada dispositivo cliente. Pode escolher uma das seguintes opções da lista pendente:  

     -   **Endereço SMTP principal**. Utilize o endereço SMTP principal do utilizador para iniciar sessão no Exchange.  

     -   **Nome Principal de utilizador**. Utilize o nome principal de utilizador completo como o endereço de e-mail.  

   - **Domínio da conta**. Escolha uma das seguintes opções:  

     - **Obter do Active Directory**  

     - **Personalizar**  

       Este campo é aplicável apenas se for **sAMAccountName** está selecionado na **nome da conta de utilizador** na lista pendente.  

   - **Método de autenticação**. Escolha um dos seguintes métodos de autenticação que serão utilizados para autenticar a ligação ao Exchange ActiveSync:  

     -   **Certificados**. Um certificado de identidade será utilizado para autenticar a ligação do Exchange ActiveSync.  

     -   **Nome de utilizador e palavra-passe**. O utilizador do dispositivo tem de fornecer uma palavra-passe para ligar ao Exchange ActiveSync. (O nome de utilizador é configurado como parte do perfil de e-mail).  

   - **Certificado de identidade**. Escolher **selecione** e, em seguida, escolha um certificado a utilizar para a identidade.  

      Certificados de identidade tem de ser certificados SCEP; Não é possível utilizar um certificado PFX.  Para obter mais informações, consulte [no System Center Configuration Manager de perfis de certificado](/sccm/protect/deploy-use/introduction-to-certificate-profiles).  

      Esta opção está disponível apenas se escolheu **certificados** sob **método de autenticação**.  

   - **Utilizar S/MIME**. Envie e-mails utilizando a encriptação S/MIME. Esta opção só é aplicável a dispositivos iOS. Pode escolher uma das seguintes opções:

     - **Certificados de assinatura**.  Escolher **selecione** e, em seguida, escolha um perfil de certificado a utilizar para encriptação.  

       O perfil pode ser um SCEP ou PFX de certificado.  No entanto, se forem utilizadas simultaneamente assinatura e encriptação, tem de selecionar os perfis de certificado PFX para *ambos* assinatura e encriptação.

     - **Certificados de encriptação**. Escolher **selecione** e, em seguida, escolha um certificado a utilizar para a encriptação. Pode escolher apenas um certificado PFX para utilizar como um certificado de encriptação.

     - Para encriptar todas as mensagens de e-mail em dispositivos iOS, ative o **exigir encriptação** caixa de verificação.    

       Tem de criar perfis de certiciate antes de pode selecioná-los aqui.  Para obter mais informações, consulte [no System Center Configuration Manager de perfis de certificado](/sccm/protect/deploy-use/introduction-to-certificate-profiles).  

## <a name="configure-synchronization-settings-for-the-exchange-activesync-email-profile"></a>Configurar definições de sincronização para o perfil de e-mail do Exchange ActiveSync  

Na página **Configurar definições de sincronização** do Assistente para Criar um Perfil de E-mail do Exchange ActiveSync, especifique as seguintes informações:  

-   **Agenda**. Escolha a agenda através do qual os dispositivos irão sincronizar dados do Exchange server. Esta opção só é aplicável a dispositivos Windows Phone. Escolha entre:  

    -   **Não configurado**. Não foi imposto um agendamento de sincronização. Isso permite que os utilizadores configurem o seu próprio agendamento de sincronização.  

    -   **Quando chegarem novas mensagens**. Dados como itens de calendário e os e-mails serão automaticamente sincronizados quando chegarem.  

    -   **15 minutos**. Dados, como itens de calendário e os e-mails serão automaticamente sincronizados a cada 15 minutos.  

    -   **30 minutos**. Dados, como itens de calendário e os e-mails serão automaticamente sincronizados a cada 30 minutos.  

    -   **60 minutos**. Dados, como itens de calendário e os e-mails serão automaticamente sincronizados a cada 60 minutos.  

    -   **Manual**. O utilizador do dispositivo tem de Iniciar sincronização manualmente.  

-   **Número de dias de e-mail a sincronizar**. Na lista pendente, escolha o número de dias de e-mail que pretende sincronizar. Escolha um dos seguintes valores:  

    -   **Não configurado**. A definição não é imposta. Ele permite que os utilizadores configurem a quantidade de e-mails é transferido para o respetivo dispositivo.  

    -   **Ilimitado**. Sincronize todos os e-mails disponíveis.  

    -   **1 dia**  

    -   **3 dias**  

    -   **1 semana**  

    -   **2 semanas**  

    -   **1 mês**  

-   **Permitir que as mensagens sejam movidas para outras contas de e-mail**. Escolha esta opção para permitir que os utilizadores movam mensagens de e-mail entre contas diferentes configuradas nos respetivos dispositivos. Esta opção só é aplicável a dispositivos iOS.  

-   **Permitir que o e-mail seja enviado a partir de aplicações de terceiros**. Escolha esta opção para permitir que os utilizadores enviem e-mails de determinadas aplicações de e-mail de terceiros não predefinidas. Esta opção só é aplicável a dispositivos iOS.  

-   **Sincronizar endereços de e-mail utilizados recentemente**. Escolha esta opção para sincronizar a lista de endereços de e-mail que foram recentemente utilizados no dispositivo. Esta opção só é aplicável a dispositivos iOS.  

-   **Utilizar SSL**. Escolha esta opção para utilizar a comunicação de Secure Sockets Layer (SSL) para enviar e-mails, receber e-mails e ao comunicar com o Exchange server.  

-   **Tipo de conteúdo a sincronizar**. Escolha os tipos de conteúdo que pretende sincronizar nos dispositivos. Esta opção só é aplicável a dispositivos Windows Phone. Escolha entre:  

    -   **E-mail**  

    -   **Contactos**  

    -   **Calendário**  

    -   **Tarefas**  

## <a name="specify-supported-platforms-for-the-exchange-activesync-email-profile"></a>Especificar as plataformas suportadas para o perfil de e-mail do Exchange ActiveSync  

1.  Sobre o **plataformas suportadas** página do Exchange ActiveSync Email Assistente para criar perfil, selecione os sistemas operativos em que o perfil de e-mail será instalado. Ou escolha **Selecionar tudo** para instalar o perfil de e-mail em todos os sistemas operativos disponíveis.  

2.  Conclua o assistente.

Para obter informações sobre como implementar perfis de e-mail do Exchange ActiveSync, consulte [como implementar perfis no System Center Configuration Manager](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md).  
