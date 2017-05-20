---
title: "Inscrever dispositivos iOS com o programa de inscrição de dispositivos (DEP) - Configuration Manager | Documentos do Microsoft"
description: "Ative a inscrição do programa de inscrição de dispositivos (DEP) para implementações híbridas no Configuration Manager com o Intune do iOS."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 78d44adc-9b1c-4bc6-b72d-e93873916ea6
caps.latest.revision: 9
author: mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: ae60eb25383f4bd07faaa1265185a471ee79b1e9
ms.openlocfilehash: 5b5eadd7b4026eae59acceaef43cdacd7a33d3ac
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="ios-device-enrollment-program-dep-enrollment-for-hybrid-deployments-with-configuration-manager"></a>inscrição do iOS programa de inscrição de dispositivos (DEP) para implementações híbridas com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

As empresas podem comprar dispositivos iOS através do programa de inscrição de dispositivos da Apple e, em seguida, geri-los através do Microsoft Intune. Para gerir dispositivos iOS pertencentes à empresa com o Programa de Inscrição de Dispositivos (DEP) da Apple, as empresas têm de concluir os passos junto da Apple para participar no programa e adquirir dispositivos através do mesmo. Os detalhes desse processo estão disponíveis em:  [https://deploy.apple.com](https://deploy.apple.com). As vantagens do programa incluem a configuração automatizada de dispositivos sem ligar por USB cada dispositivo a um computador.  

 Antes de poder inscrever dispositivos iOS pertencentes à empresa com o DEP, precisa de um token do DEP da Apple. Este token permite ao Intune sincronizar informações sobre os participantes no DEP dispositivos pertencentes à. Também permite ao Intune carregar perfis de inscrição para a Apple e atribuir dispositivos a esses perfis.  

## <a name="apple-dep-enrollment-for-ios-devices"></a>Inscrição através do Apple DEP de dispositivos iOS  
 Os procedimentos seguintes descrevem como especificar os dispositivos iOS adquiridos através do DEP da Apple como geridos pelo Intune dispositivos pertencentes à empresa. Quando as potências primeiro utilizador até o dispositivo este irá receber o perfil de gestão do DEP e execute o Assistente de configuração e torná-los a gestão.  

###  <a name="enable-dep-enrollment-in-configuration-manager-with-intune"></a>Ativar a inscrição de DEP no Configuration Manager com o Intune  

1.  **Começar a gerir dispositivos iOS com o Configuration Manager**   
    Antes de poder inscrever dispositivos do programa de inscrição de dispositivos (DEP), tem de concluir os passos para [configurar a gestão de dispositivos móveis híbrida](../../mdm/deploy-use/setup-hybrid-mdm.md) incluindo [passos para suportar a inscrição de iOS](../deploy-use/enroll-hybrid-ios-mac.md).

2.  **Criar um pedido de token DEP**   
    Na consola do Configuration Manager, no **administração** área de trabalho, expanda **configuração da hierarquia**, expanda **serviços em nuvem**e clique em **subscrições do Microsoft Intune**. Clique em **Criar Pedido de Token DEP** no separador **Home Page** , clique em **Procurar** para especificar a localização da transferência para o pedido de token DEP e, em seguida, clique em **Transferir**. Guarde o ficheiro de pedido de token do DEP (.pem) localmente. O ficheiro .pem é serve para pedir um token fidedigno (.p7m) a partir do portal do Programa de Inscrição de Dispositivos da Apple.  

3.  **Obter um token do Programa de Inscrição de Dispositivos**   
    Aceda ao [portal do Programa de Inscrição de Dispositivos](https://deploy.apple.com) (https://deploy.apple.com) e inicie sessão com o Apple ID da sua empresa. Este ID Apple tem de ser utilizado no futuro para renovar o seu token do DEP.  

    1.  Na consola do [portal do Programa de Inscrição de Dispositivos](https://deploy.apple.com), aceda a **Programa de Inscrição de Dispositivos** > **Gerir Servidores**e, em seguida, clique em **Adicionar Servidor MDM**.  

    2.  Introduza o **Nome do Servidor MDM**e, em seguida, clique em **Seguinte**. O nome do servidor é uma referência para identificar o servidor MDM. Não é o nome ou o URL do servidor do Intune ou o Configuration Manager.  

    3.  O **adicionar < ServerName\>**  é aberta a caixa de diálogo. Clique em **Escolher ficheiro…** para carregar o ficheiro .pem que criou no passo anterior e, em seguida, clique em **Seguinte**.  

    4.  O **adicionar < ServerName\>**  caixa de diálogo apresenta um **Token do seu servidor** ligação. Transfira o ficheiro de token (.p7m) do servidor para o seu computador e, em seguida, clique em **Concluído**.  

     Este ficheiro de certificado (.p7m) serve para estabelecer uma relação de confiança entre os servidores do Programa de Inscrição de Dispositivos do Intune e da Apple.  

4.  **Adicionar o token do DEP ao Configuration Manager**   
    Na consola do Configuration Manager, no **administração** área de trabalho, expanda **configuração da hierarquia** e clique em **subscrições do Microsoft Intune**. Clique em **Configurar Plataformas** no separador **Home Page** e, em seguida, clique em **iOS**. Selecione **Ativar o Programa de Inscrição de Dispositivos**, procure o ficheiro de certificado (.p7m), clique em **Abrir**, clique em **Carregar**e, em seguida, clique em **OK**.  

#### <a name="set-up-enrollment-for-apple-device-enrollment-program-dep-ios-devices"></a>Configurar a inscrição para dispositivos iOS de programa de inscrição de dispositivos da Apple (DEP)  

1.  **Adicionar uma política de inscrição de dispositivos da empresa**   
    Na consola do Configuration Manager, no **ativos e compatibilidade** área de trabalho, expanda **descrição geral**, expanda **todos os dispositivos pertencentes**, expanda **iOS**e clique em **perfis de inscrição**. Clique em **Criar Perfil** no separador **Home Page** para abrir o assistente Criar Perfil. Configure as definições nas seguintes páginas:  

    1.  On the **Geral** , especifique as seguintes informações e clique em **Seguinte**.  

        -   **Nome** – nome do perfil de inscrição de dispositivos. (Não visível aos utilizadores)  

        -   **Descrição** -descrição do perfil de inscrição de dispositivos. (Não visível aos utilizadores)  

        -   **Afinidade do utilizador** – especifica como os dispositivos são inscritos. Consulte o artigo [afinidade do utilizador para uma implementação híbrida geridos dispositivos no Configuration Manager](../../mdm/deploy-use/user-affinity-for-hybrid-managed-devices.md).  

            -   **Pedido de afinidade de utilizador de**: O dispositivo tem de ser afiliado a um utilizador durante a configuração inicial e, em seguida, foi permitido para aceder ao e-mail desse utilizador e dados da empresa.  A afinidade de utilizador deve ser configurada para dispositivos geridos por DEP que pertencem aos utilizadores e que precisam de utilizar o portal da empresa (por exemplo, para instalar aplicações).  

            > [!NOTE]
            > DEP com afinidade do utilizador necessita de ponto final de ADFS WS-Trust 1.3 Username/Mixed estar ativado para solicitar o token de utilizador.

            -   **Sem afinidade de utilizador**: O dispositivo não está afiliado a um utilizador. Utilize esta afiliação em dispositivos que efetuem tarefas sem aceder aos dados de utilizador locais. As aplicações que precisem da afiliação de utilizador não funcionam.  
             ![Captura de ecrã do DEP nome, descrição e perfil pedido de afinidade do utilizador](../media/dep-general.png)

    2.  No **definições do programa de inscrição de dispositivos** página, especifique as seguintes informações e, em seguida, clique em **seguinte**.  

        -   **Departamento**: Esta informação é apresentada quando os utilizadores toque em "Sobre a configuração de" durante a ativação.  

        -   **Número de telefone de suporte**: Apresentada quando o utilizador clica o **precisar de ajuda** botão durante a ativação.
       ![Captura de ecrã de atribuir o perfil DEP para dispositivos iOS](../media/dep-settings.png)

        -   **Modo de preparação**: Este estado é definido durante a ativação e não pode ser alterado sem as definições de fábrica repor o dispositivo:  

            -   **Unsupervised** -limitada de funcionalidades de gestão  

            -   **Supervisionado** - ativa mais opções de gestão e desativa o bloqueio de ativação por predefinição  

        -   **Bloquear perfil de inscrição para dispositivos**: Este estado é definido durante a ativação e não pode ser alterado sem uma reposição de fábrica.  

            -   **Desativar** -permite que o perfil de gestão ser removido o **definições** menu  

            -   **Ativar** -(requer **preparação modo** = **Supervised**) desativa as definições do iOS que podem permitir a remoção do perfil de gestão  

    3.  Na página **Assistente de Configuração** , configure as definições que personalizam o Assistente de Configuração iOS que inicia quando o dispositivo é ligado pela primeira vez e, em seguida, clique em **Seguinte**. Estas definições incluem:  
        -   **Código de acesso** - pedido de código de acesso durante a ativação. Necessitam sempre de um código de acesso, a menos que o dispositivo vai ser protegidos ou ter acesso controlado de alguma forma (ou seja, a modo de local público que restringe o dispositivo a uma aplicação).  
        -   **Serviços de localização** - se ativada, o Assistente de configuração lhe pedir para o serviço durante a ativação  
        -   **Restaurar** - se ativada, o Assistente de configuração lhe pedir para cópia de segurança do iCloud durante a ativação  
        -   **Apple ID** -um ID Apple é necessário para transferir iOS App Store aplicações, incluindo os instalados através do Intune. Se estiver ativada, iOS pedirá utilizadores para um ID Apple quando Intune tenta instalar uma aplicação sem um ID.  
        -   **Termos e condições** -se ativada, Assistente de configuração solicita-lhe os utilizadores para aceitar os termos e condições da Apple durante a ativação  
        -   **ID de toque** - se ativada, o Assistente de configuração lhe pedir para este serviço durante a ativação
        -   **Apple pagar** - se ativada, o Assistente de configuração lhe pedir para este serviço durante a ativação
        -   **Zoom** - se ativada, o Assistente de configuração lhe pedir para este serviço durante a ativação
        -   **A Siri** - se ativada, o Assistente de configuração lhe pedir para este serviço durante a ativação  
        -   **Enviar dados de diagnóstico para a Apple** - se ativada, o Assistente de configuração lhe pedir para este serviço durante a ativação  
        ![Captura de ecrã de atribuir o perfil DEP para dispositivos iOS](../media/dep-setup-assistant.png)

    4.  No **gestão adicional** página, especifique se uma ligação de USB pode ser utilizada para as definições de gestão adicionais. Quando seleciona **necessitam de certificado**, tem de importar um certificado de gestão do Apple Configurator para utilizar para este perfil.  Definido como **não permitir** para impedir a sincronização de ficheiros com o iTunes ou o gestão através do Apple Configurator. A Microsoft recomenda que definido como **não permitir**, exportar qualquer configuração adicional do Apple Configurator e, em seguida, implementar como um perfil de configuração de iOS personalizadas, em vez de utilizar esta definição para permitir a implementação manual com ou sem um certificado.  

        -   **Não permitir** -impede o dispositivo de comunicar através de USB (desativa emparelhamento)  

        -   **Permitir** -permite que dispositivo comunicar através de ligação de USB com qualquer PC ou Mac  

        -   **Requer certificado**-permite que o emparelhamento com um Mac com um certificado importado para o perfil de inscrição  

2.  **Atribuir dispositivos DEP para gestão**   
    Aceda ao [portal do Programa de Inscrição de Dispositivos](https://deploy.apple.com) (https://deploy.apple.com) e inicie sessão com o Apple ID da sua empresa. Aceda a **Programa de Implementação** > **Programa de Inscrição de Dispositivos** > **Gerir Dispositivos**. Especifique como irá **Escolher Dispositivos**, forneça informações sobre o dispositivo e especifique detalhes por **Número de Série**e **Número da Encomenda**do dispositivo, ou como **Carregar Ficheiro CSV**. Em seguida, selecione **atribuir ao servidor** e selecione o <*ServerName*> especificada no passo 3 e, em seguida, clique em **OK**.  

3.  **Sincronizar dispositivos geridos pelo DEP**   
    No **ativos e compatibilidade** área de trabalho, aceda a **todos os dispositivos pertencentes** > **Predeclared dispositivos**. No separador **Home Page** , clique em **Sincronização DEP**. É enviado um pedido de sincronização para a Apple. Após a conclusão da sincronização, são apresentados os dispositivos geridos pelo DEP.

4.  **Atribua o perfil DEP**<br>No **ativos e compatibilidade** área de trabalho, aceda a **todos os dispositivos pertencentes** > **iOS** > **perfis de inscrição**. Selecione o perfil de inscrição de DEP e, em seguida, no **base** separador, clique em **atribuir aos dispositivos**. Selecione os dispositivos que irão utilizar este perfil de inscrição, clique em **adicionar**e, em seguida, clique em **OK**.   
     ![Captura de ecrã de atribuir o perfil DEP para dispositivos iOS](../media/dep-assign-profile.png)

5.  **Distribuir dispositivos aos utilizadores**   
    Já pode dar os dispositivos pertencentes à empresa aos utilizadores. A caixa de diálogo **Estado de Inscrição** dos dispositivos geridos indica **Não contactado** até que o dispositivo seja ligado e execute o Assistente de Configuração para inscrever o dispositivo. Quando um dispositivo iOS é ativado, será inscrito para gestão pelo Intune.

