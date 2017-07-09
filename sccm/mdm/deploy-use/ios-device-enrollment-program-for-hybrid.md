---
title: Registrar dispositivos iOS com dispositivo registro programa (DEP) - Configuration Manager | Microsoft Docs
description: "Habilite o registro de dispositivo registro programa (DEP) para implantações híbridas no Configuration Manager com Intune do iOS."
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
ms.sourcegitcommit: 255249332350843ba0b78128423482e260974521
ms.openlocfilehash: 1ea0360b5b182b92e11ea9dfe78b5a3552ae4845
ms.contentlocale: pt-pt
ms.lasthandoff: 05/30/2017

---
# <a name="ios-device-enrollment-program-dep-enrollment-for-hybrid-deployments-with-configuration-manager"></a>registro do programa de registro de dispositivo (DEP) iOS para implantações híbridas com o Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

As empresas podem adquirir dispositivos iOS por meio do programa de registro de dispositivo da Apple e, em seguida, gerenciá-los usando o Microsoft Intune. Para gerir dispositivos iOS pertencentes à empresa com o Programa de Inscrição de Dispositivos (DEP) da Apple, as empresas têm de concluir os passos junto da Apple para participar no programa e adquirir dispositivos através do mesmo. Os detalhes desse processo estão disponíveis em:  [https://deploy.apple.com](https://deploy.apple.com). As vantagens do programa incluem a configuração automatizada de dispositivos sem ligar por USB cada dispositivo a um computador.  

 Antes de poder inscrever dispositivos iOS pertencentes à empresa com o DEP, precisa de um token do DEP da Apple. Este token permite que Intune sincronize informações sobre dispositivos participantes no DEP pertencentes à sua empresa. Ele também permite que Intune carregue perfis de registro para a Apple e atribua dispositivos a esses perfis.  

## <a name="apple-dep-enrollment-for-ios-devices"></a>Inscrição através do Apple DEP de dispositivos iOS  
 Os procedimentos a seguir descrevem como especificar dispositivos iOS adquiridos por meio do DEP da Apple como dispositivos da empresa gerenciados pelo Intune. Quando as potências de primeiro do usuário até o dispositivo ele receberá o perfil de gerenciamento de DEP e execute o Assistente de configuração e colocá-los em gerenciamento.  

###  <a name="enable-dep-enrollment-in-configuration-manager-with-intune"></a>Habilitar o registro de DEP no Configuration Manager com Intune  

1.  **Começar a gerir dispositivos iOS com o Configuration Manager**   
    Antes de poder registrar dispositivos no programa de registro de dispositivo (DEP) iOS, você deve concluir as etapas [configurar o gerenciamento de dispositivo móvel híbrido](../../mdm/deploy-use/setup-hybrid-mdm.md) incluindo [etapas para dar suporte ao registro do iOS](../deploy-use/enroll-hybrid-ios-mac.md).

2.  **Criar um pedido de token DEP**   
    No console do Configuration Manager, no **administração** espaço de trabalho, expanda **configuração da hierarquia**, expanda **serviços de nuvem**e clique em **assinaturas do Microsoft Intune**. Clique em **Criar Pedido de Token DEP** no separador **Home Page** , clique em **Procurar** para especificar a localização da transferência para o pedido de token DEP e, em seguida, clique em **Transferir**. Guarde o ficheiro de pedido de token do DEP (.pem) localmente. O ficheiro .pem é serve para pedir um token fidedigno (.p7m) a partir do portal do Programa de Inscrição de Dispositivos da Apple.  

3.  **Obter um token do Programa de Inscrição de Dispositivos**   
    Aceda ao [portal do Programa de Inscrição de Dispositivos](https://deploy.apple.com) (https://deploy.apple.com) e inicie sessão com o Apple ID da sua empresa. Este ID Apple tem de ser utilizado no futuro para renovar o seu token do DEP.  

    1.  Na consola do [portal do Programa de Inscrição de Dispositivos](https://deploy.apple.com), aceda a **Programa de Inscrição de Dispositivos** > **Gerir Servidores**e, em seguida, clique em **Adicionar Servidor MDM**.  

    2.  Introduza o **Nome do Servidor MDM**e, em seguida, clique em **Seguinte**. O nome do servidor é uma referência para identificar o servidor MDM. Não é o nome ou URL do servidor Intune ou Configuration Manager.  

    3.  O **adicionar < ServerName\>**  caixa de diálogo é aberta. Clique em **Escolher ficheiro…** para carregar o ficheiro .pem que criou no passo anterior e, em seguida, clique em **Seguinte**.  

    4.  O **adicionar < ServerName\>**  caixa de diálogo exibe uma **seu Token do servidor** link. Transfira o ficheiro de token (.p7m) do servidor para o seu computador e, em seguida, clique em **Concluído**.  

     Este ficheiro de certificado (.p7m) serve para estabelecer uma relação de confiança entre os servidores do Programa de Inscrição de Dispositivos do Intune e da Apple.  

4.  **Adicionar o token do DEP ao Configuration Manager**   
    No console do Configuration Manager, no **administração** espaço de trabalho, expanda **configuração da hierarquia** e clique em **assinaturas do Microsoft Intune**. Clique em **Configurar Plataformas** no separador **Home Page** e, em seguida, clique em **iOS**. Selecione **Ativar o Programa de Inscrição de Dispositivos**, procure o ficheiro de certificado (.p7m), clique em **Abrir**, clique em **Carregar**e, em seguida, clique em **OK**.  

#### <a name="set-up-enrollment-for-apple-device-enrollment-program-dep-ios-devices"></a>Configurar o registro para dispositivos iOS de Apple dispositivo registro programa (DEP)  

1.  **Adicionar uma política de registro de dispositivo corporativo**   
    No console do Configuration Manager, no **ativos e conformidade** espaço de trabalho, expanda **visão geral**, expanda **todos os dispositivos corporativos**, expanda **iOS**e clique em **perfis de registro**. Clique em **Criar Perfil** no separador **Home Page** para abrir o assistente Criar Perfil. Configure as definições nas seguintes páginas:  

    1.  On the **Geral** , especifique as seguintes informações e clique em **Seguinte**.  

        -   **Nome** – nome do perfil de inscrição de dispositivos. (Não visível aos utilizadores)  

        -   **Descrição** -descrição do perfil de registro do dispositivo. (Não visível aos utilizadores)  

        -   **Afinidade do utilizador** – especifica como os dispositivos são inscritos. Consulte [afinidade de usuário para híbrida gerenciado dispositivos no Configuration Manager](../../mdm/deploy-use/user-affinity-for-hybrid-managed-devices.md).  

            -   **Solicitar afinidade do usuário**: O dispositivo deve ser afiliado a um usuário durante a instalação inicial e depois receber permissão para acessar dados da empresa e email como esse usuário.  A afinidade de utilizador deve ser configurada para dispositivos geridos por DEP que pertencem aos utilizadores e que precisam de utilizar o portal da empresa (por exemplo, para instalar aplicações).  

            > [!NOTE]
            > DEP com afinidade de usuário requer o ponto de extremidade do ADFS WS-Trust 1.3 nome de usuário/misto deve ser habilitada a solicitação de token de usuário.

            -   **Sem afinidade de usuário**: O dispositivo não está afiliado a um usuário. Utilize esta afiliação em dispositivos que efetuem tarefas sem aceder aos dados de utilizador locais. As aplicações que precisem da afiliação de utilizador não funcionam.  
             ![Nome do perfil de captura de tela de DEP, a descrição e o prompt de afinidade de usuário](../media/dep-general.png)

    2.  Sobre o **configurações do programa de registro de dispositivo** página, especifique as seguintes informações e, em seguida, clique em **próximo**.  

        -   **Departamento**: Essas informações são exibidas quando os usuários tocam em "Sobre a configuração" durante a ativação.  

        -   **Número de telefone de suporte**: Exibido quando o usuário clica o **precisa de Ajuda** botão durante a ativação.
       ![Captura de tela da atribuição de perfil DEP para dispositivos iOS](../media/dep-settings.png)

        -   **Modo de preparação**: Esse estado é definido durante a ativação e não pode ser alterado sem redefinir o dispositivo de fábrica:  

            -   **Sem supervisão** -recursos de gerenciamento limitados  

            -   **Supervisionado** - permite mais opções de gerenciamento e desabilita o bloqueio de ativação por padrão  

        -   **Bloquear perfil de registro de dispositivo**: Esse estado é definido durante a ativação e não pode ser alterado sem uma redefinição de fábrica.  

            -   **Desabilitar** -permite que o perfil de gerenciamento a ser removido do **configurações** menu  

            -   **Habilitar** -(requer **modo de preparação** = **supervisionado**) desabilita as configurações do iOS que podem permitir a remoção do perfil de gerenciamento  

    3.  Na página **Assistente de Configuração** , configure as definições que personalizam o Assistente de Configuração iOS que inicia quando o dispositivo é ligado pela primeira vez e, em seguida, clique em **Seguinte**. Estas definições incluem:  
        -   **Senha** - solicitar senha durante a ativação. Sempre exigir uma senha, a menos que o dispositivo esteja protegido ou tenha acesso controlado de alguma outra forma (ou seja, modo de quiosque que restringe o dispositivo a um aplicativo).  
        -   **Serviços de localização** - se habilitado, o Assistente de instalação solicitará o serviço durante a ativação  
        -   **Restaurar** - se habilitado, o Assistente de instalação solicitará backup do iCloud durante a ativação  
        -   **ID da Apple** -uma ID da Apple é exigida para baixar iOS da App Store, incluindo aqueles instalados pelo Intune. Se habilitada, o iOS solicitará aos usuários para uma ID da Apple ao Intune tenta instalar um aplicativo sem uma ID.  
        -   **Termos e condições** -se habilitado, o Assistente de instalação solicitará os usuários aceitem os termos e condições da Apple durante a ativação  
        -   **ID de toque** - se habilitado, o Assistente de instalação solicitará o serviço durante a ativação
        -   **Pagamento da Apple** - se habilitado, o Assistente de instalação solicitará o serviço durante a ativação
        -   **Zoom** - se habilitado, o Assistente de instalação solicitará o serviço durante a ativação
        -   **Siri** - se habilitado, o Assistente de instalação solicitará o serviço durante a ativação  
        -   **Enviar dados de diagnóstico para a Apple** - se habilitado, o Assistente de instalação solicitará o serviço durante a ativação  
        ![Captura de tela da atribuição de perfil DEP para dispositivos iOS](../media/dep-setup-assistant.png)

    4.  Sobre o **gerenciamento adicional** página, especifique se uma conexão USB pode ser usado para configurações de gerenciamento adicional. Quando você seleciona **exigir certificado**, você deve importar um certificado de gerenciamento do Apple Configurator a ser usado para este perfil.  Definido como **não permitir** para impedir a sincronização de arquivos com iTunes ou gerenciamento por meio do Apple Configurator. A Microsoft recomenda que você defina como **não permitir**, exportar qualquer configuração adicional do Apple Configurator e, em seguida, implantar como um perfil de configuração do iOS personalizado, em vez de usar essa configuração para permitir a implantação manual com ou sem um certificado.  

        -   **Não permitir** -impede que o dispositivo se comunique via USB (desabilita emparelhamento)  

        -   **Permitir** -permite que dispositivos se comuniquem via conexão USB com qualquer PC ou Mac  

        -   **Exigir certificado**-permite o emparelhamento com um Mac com um certificado importado para o perfil de registro  

2.  **Atribuir dispositivos DEP para gerenciamento**   
    Aceda ao [portal do Programa de Inscrição de Dispositivos](https://deploy.apple.com) (https://deploy.apple.com) e inicie sessão com o Apple ID da sua empresa. Aceda a **Programa de Implementação** > **Programa de Inscrição de Dispositivos** > **Gerir Dispositivos**. Especifique como irá **Escolher Dispositivos**, forneça informações sobre o dispositivo e especifique detalhes por **Número de Série**e **Número da Encomenda**do dispositivo, ou como **Carregar Ficheiro CSV**. Em seguida, selecione **atribuir ao servidor** e selecione o <*ServerName*> que você especificou na etapa 3 e, em seguida, clique em **Okey**.  

3.  **Sincronizar dispositivos geridos pelo DEP**   
    No **ativos e conformidade** , vá para **todos os dispositivos corporativos** > **dispositivos declaradas previamente**. No separador **Home Page** , clique em **Sincronização DEP**. É enviado um pedido de sincronização para a Apple. Após a conclusão da sincronização, são apresentados os dispositivos geridos pelo DEP.

> [!NOTE]
> Na configuração híbrida, a operação de sincronização DEP é disparada manualmente clicando **sincronização DEP** no console do Configuration Manager.

4.  **Atribuir perfil de DEP**<br>No **ativos e conformidade** , vá para **todos os dispositivos corporativos** > **iOS** > **perfis de registro**. Selecione o perfil de registro de DEP e, em seguida, no **início** , clique em **atribuir a dispositivos**. Selecione os dispositivos que usarão este perfil de registro, clique em **adicionar**e, em seguida, clique em **Okey**.   
     ![Captura de tela da atribuição de perfil DEP para dispositivos iOS](../media/dep-assign-profile.png)

5.  **Distribuir dispositivos aos utilizadores**   
    Já pode dar os dispositivos pertencentes à empresa aos utilizadores. A caixa de diálogo **Estado de Inscrição** dos dispositivos geridos indica **Não contactado** até que o dispositivo seja ligado e execute o Assistente de Configuração para inscrever o dispositivo. Quando um dispositivo iOS é ativado, será inscrito para gestão pelo Intune.

