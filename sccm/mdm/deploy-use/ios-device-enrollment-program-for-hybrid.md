---
title: 'Inscrever dispositivos iOS com o programa de inscrição de dispositivos (DEP) '
titleSuffix: Configuration Manager
description: Ative a inscrição do programa de inscrição de dispositivos (DEP) para implementações híbridas no Configuration Manager com o Intune para iOS.
ms.date: 09/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 78d44adc-9b1c-4bc6-b72d-e93873916ea6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 31c94d3632014110302cb1815f72af0c26245dc9
ms.sourcegitcommit: 95452daa3340d4d0818562bcbb53672cb16f8799
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/11/2018
ms.locfileid: "34063637"
---
# <a name="ios-device-enrollment-program-dep-enrollment-for-hybrid-deployments-with-configuration-manager"></a>inscrição do iOS Device Enrollment Program (DEP) para implementações híbridas com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

As empresas podem comprar dispositivos iOS através do programa de inscrição de dispositivos da Apple e, em seguida, geri-los através do Microsoft Intune. Para gerir dispositivos iOS pertencentes à empresa com o Programa de Inscrição de Dispositivos (DEP) da Apple, as empresas têm de concluir os passos junto da Apple para participar no programa e adquirir dispositivos através do mesmo. Os detalhes desse processo estão disponíveis em: [ https://deploy.apple.com ](https://deploy.apple.com). As vantagens do programa incluem a configuração automatizada de dispositivos sem ligar por USB cada dispositivo a um computador.  

 Antes de poder inscrever dispositivos iOS pertencentes à empresa com o DEP, precisa de um token do DEP da Apple. Este token permite ao Intune sincronizar informações sobre os participantes no DEP dispositivos pertencentes à. Também permite ao Intune carregue perfis de inscrição para a Apple e atribua dispositivos a esses perfis.  

## <a name="apple-dep-enrollment-for-ios-devices"></a>Inscrição através do Apple DEP de dispositivos iOS  
 Os procedimentos seguintes descrevem como especificar os dispositivos iOS adquiridos através do DEP da Apple como gerido do Intune dispositivos pertencentes à empresa. Quando os powers primeiro utilizador até o dispositivo possa receber o perfil de gestão de DEP e executar o Assistente de configuração e colocá-los para gestão.  

##  <a name="enable-dep-enrollment-in-configuration-manager-with-intune"></a>Ativar a inscrição de DEP no Configuration Manager com Intune  

1.  **Começar a gerir dispositivos iOS com o Configuration Manager**   
    Antes de poder inscrever programa de inscrição de dispositivos (DEP) dispositivos iOS, tem de concluir os passos para [configurar a gestão de dispositivos móveis híbridos](../../mdm/deploy-use/setup-hybrid-mdm.md) incluindo [passos para suportar a inscrição do iOS](../deploy-use/enroll-hybrid-ios-mac.md).
2.  **Criar um pedido de token DEP**   
    Na consola do Configuration Manager, no **administração** área de trabalho, expanda **configuração da hierarquia**, expanda **serviços em nuvem**e clique em **subscrições do Microsoft Intune**. Clique em **Criar Pedido de Token DEP** no separador **Home Page** , clique em **Procurar** para especificar a localização da transferência para o pedido de token DEP e, em seguida, clique em **Transferir**. Guarde o ficheiro de pedido de token do DEP (.pem) localmente. O ficheiro .pem é serve para pedir um token fidedigno (.p7m) a partir do portal do Programa de Inscrição de Dispositivos da Apple.  
3.  **Obter um token do Programa de Inscrição de Dispositivos**   
    Vá para o [portal do programa de inscrição de dispositivos](https://deploy.apple.com) (https://deploy.apple.com) e inicie sessão com o ID Apple da empresa Este ID Apple tem de ser utilizado no futuro para renovar o seu token do DEP.  
    1.  Na consola do [portal do Programa de Inscrição de Dispositivos](https://deploy.apple.com), aceda a **Programa de Inscrição de Dispositivos** > **Gerir Servidores**e, em seguida, clique em **Adicionar Servidor MDM**.  
    ![Captura de ecrã do Adicionar servidor MDM no portal do programa de inscrição de dispositivos](../media/enrollment-program-token-add-server.png)
    2.  Introduza o **Nome do Servidor MDM**e, em seguida, clique em **Seguinte**. O nome do servidor é uma referência para identificar o servidor MDM. Não é o nome ou URL do servidor do Intune ou do Configuration Manager.  
    3.  O **adicionar < ServerName\>**  é aberta a caixa de diálogo. Clique em **Escolher ficheiro…** para carregar o ficheiro .pem que criou no passo anterior e, em seguida, clique em **Seguinte**.  
    4.  O **adicionar < ServerName\>**  caixa de diálogo apresenta um **Token do seu servidor** ligação. Transfira o ficheiro de token (.p7m) do servidor para o seu computador e, em seguida, clique em **Concluído**.  

     Este ficheiro de certificado (.p7m) serve para estabelecer uma relação de confiança entre os servidores do Programa de Inscrição de Dispositivos do Intune e da Apple.  
4.  **Adicionar o token do DEP ao Configuration Manager**   
    Na consola do Configuration Manager, no **administração** área de trabalho, expanda **configuração da hierarquia** e clique em **subscrições do Microsoft Intune**. Clique em **Configurar Plataformas** no separador **Home Page** e, em seguida, clique em **iOS**. Selecione **Ativar o Programa de Inscrição de Dispositivos**, procure o ficheiro de certificado (.p7m), clique em **Abrir**, clique em **Carregar**e, em seguida, clique em **OK**.  

## <a name="add-a-corporate-device-enrollment-policy"></a>Adicionar uma política de inscrição de dispositivos da empresa  

1. Na consola do Configuration Manager, no **ativos e compatibilidade** área de trabalho, expanda **descrição geral**, expanda **todos os dispositivos pertencentes**, expanda **iOS**e clique em **perfis de inscrição**. Clique em **Criar Perfil** no separador **Home Page** para abrir o assistente Criar Perfil. Configure as definições nas seguintes páginas:  
2. On the **Geral** , especifique as seguintes informações e clique em **Seguinte**.  
  -   **Nome** – nome do perfil de inscrição de dispositivos. (Não visível aos utilizadores)  
  -   **Descrição** -descrição do perfil de inscrição de dispositivos. (Não visível aos utilizadores)  
  -   **Afinidade do utilizador** – especifica como os dispositivos são inscritos. Consulte [afinidade de utilizador para híbrida geridos dispositivos no Configuration Manager](../../mdm/deploy-use/user-affinity-for-hybrid-managed-devices.md).  

      -  **Pedido de afinidade de utilizador de**: O dispositivo tem de ser afiliado a um utilizador durante a configuração inicial e, em seguida, pode ser autorizado a aceder ao e-mail do utilizador e dados da empresa.  Afinidade de utilizador deve ser configurada para dispositivos geridos por DEP que pertencem aos utilizadores e tem de utilizar o portal da empresa (ou seja, para instalar aplicações).  
      > [!NOTE]
      > DEP com afinidade de utilizador requer o ponto final de nome de utilizador de 1.3 de WS-Trust de ADFS/Mixed esteja ativado para solicitar o token de utilizador.

      -   **Sem afinidade de utilizador**: O dispositivo não está afiliado a um utilizador. Utilize esta afiliação em dispositivos que efetuem tarefas sem aceder aos dados de utilizador locais. As aplicações que precisem da afiliação de utilizador não funcionam.  
    ![Nome do perfil de captura de ecrã do DEP, descrição e o pedido de afinidade de utilizador](../media/dep-general.png)

3. No **definições do programa de inscrição de dispositivos** página, especifique as seguintes informações e, em seguida, clique em **seguinte**.  
    -   **Departamento**: Esta informação é apresentada quando os utilizadores tocam em "Sobre a configuração de" durante a ativação.  
    -   **Número de telefone de suporte**: Apresentado quando o utilizador clica o **precisa de ajuda** botão durante a ativação.
       ![Captura de ecrã de atribuição de perfil do DEP para dispositivos iOS](../media/dep-settings.png)

    - **Modo de preparação**: Este estado é definido durante a ativação e não pode ser alterado sem o dispositivo de reposição de fábrica:  
        -   **Supervisionados** -capacidades de gestão limitadas  
        -   **Supervisionado** - ativa mais opções de gestão e desativa o bloqueio de ativação por predefinição  
    - **Bloquear perfil de inscrição no dispositivo**: Este estado é definido durante a ativação e não pode ser alterado sem uma reposição de fábrica.  
      -   **Desativar** -permite que o perfil de gestão a ser removido o **definições** menu  
      -   **Ativar** -(requer **modo de preparação** = **supervisionado**) desativa as definições do iOS que poderiam permitir a remoção do perfil de gestão  

4.  Na página **Assistente de Configuração** , configure as definições que personalizam o Assistente de Configuração iOS que inicia quando o dispositivo é ligado pela primeira vez e, em seguida, clique em **Seguinte**. Estas definições incluem:  
  -   **Código de acesso** - pedido de código de acesso durante a ativação. Exigir sempre um código de acesso, a menos que o dispositivo esteja protegido ou tenha o acesso controlado de outra forma (ou seja, a modo de local público que restringe o dispositivo a uma aplicação).  
  -   **Os serviços de localização** - se ativado, o Assistente de configuração solicita o serviço durante a ativação  
  -   **Restaurar** - se ativado, o Assistente de configuração solicita para cópia de segurança de iCloud durante a ativação  
  -   **Apple ID** -é necessário um ID Apple para transferir aplicações da loja de aplicações, incluindo as instaladas pelo Intune iOS. Se estiver ativada, iOS irá pedir aos utilizadores um ID Apple quando o Intune tenta instalar uma aplicação sem um ID.  
  -   **Termos e condições** -se ativado, o Assistente de configuração solicita aos utilizadores que aceitem os termos e condições da Apple durante a ativação  
  -   **Touch ID** - se ativado, o Assistente de configuração solicita este serviço durante a ativação
  -   **Apple Pay** - se ativado, o Assistente de configuração solicita este serviço durante a ativação
  -   **Zoom** - se ativado, o Assistente de configuração solicita este serviço durante a ativação
  -   **Siri** - se ativado, o Assistente de configuração solicita este serviço durante a ativação  
  -   **Enviar dados de diagnóstico para a Apple** - se ativado, o Assistente de configuração solicita este serviço durante a ativação  
    ![Captura de ecrã de atribuição de perfil do DEP para dispositivos iOS](../media/dep-setup-assistant.png)
5.  No **gestão adicional** página, especifique se uma ligação USB pode ser utilizada para definições de gestão adicional. Quando seleciona **necessitam de um certificado**, tem de importar um certificado de gestão do Apple Configurator para utilizar este perfil.  Definido como **não permitir** para impedir a sincronização de ficheiros com o iTunes ou de gestão através do Apple Configurator. A Microsoft recomenda que defina para **não permitir**, exporte qualquer configuração adicional do Apple Configurator e, em seguida, implementar como um perfil de configuração iOS personalizada, em vez de utilizar esta definição para permitir a implementação manual com ou sem um certificado.  

  -   **Não permitir** -impede o dispositivo de comunicar através de USB (desativa o emparelhamento)  
  -   **Permitir** -permite que o dispositivo comunique através de uma ligação USB com qualquer PC ou Mac  
  -   **Requer certificado**-permite o emparelhamento com um Mac com um certificado importado para o perfil de inscrição  

## <a name="assign-dep-devices-for-management"></a>Atribuir dispositivos DEP para gestão

1. Vá para o [portal do programa de inscrição de dispositivos](https://deploy.apple.com) (https://deploy.apple.com) e inicie sessão com o ID Apple da empresa
2. Aceda a **Programa de Implementação** > **Programa de Inscrição de Dispositivos** > **Gerir Dispositivos**. Especifique como irá **Escolher Dispositivos**, forneça informações sobre o dispositivo e especifique detalhes por **Número de Série**e **Número da Encomenda**do dispositivo, ou como **Carregar Ficheiro CSV**. Em seguida, selecione **atribuir ao servidor** e selecione o <*ServerName*> que especificou no passo 3 e, em seguida, clique em **OK**.  
![Captura de ecrã do dispositivo inscrição portal do programa Apple adicionar dispositivos](../media/enrollment-program-token-specify-serial.png)

3.  **Sincronizar dispositivos geridos pelo DEP**   
    No **ativos e compatibilidade** área de trabalho, aceda a **todos os dispositivos pertencentes** > **Predeclared dispositivos**. No separador **Home Page** , clique em **Sincronização DEP**. É enviado um pedido de sincronização para a Apple. Após a conclusão da sincronização, são apresentados os dispositivos geridos pelo DEP.

    > [!NOTE]
    > Na configuração híbrida, a operação de sincronização do DEP manualmente é acionada clicando **sincronização do DEP** na consola do Configuration Manager.

4.  **Atribuir perfil do DEP**<br>No **ativos e compatibilidade** área de trabalho, aceda a **todos os dispositivos pertencentes** > **iOS** > **perfis de inscrição**. Selecione o perfil de inscrição de DEP e, em seguida, no **home page** separador, clique em **atribuir aos dispositivos**. Selecione os dispositivos que irá utilizar este perfil de inscrição, clique em **adicionar**e, em seguida, clique em **OK**.

    > [!NOTE]
    > Depois de um perfil do DEP está atribuído a um dispositivo, pode substituir o perfil apenas com outro perfil do DEP. No entanto, não é possível remover a atribuição de perfil do DEP. Para remover um perfil do DEP a partir de um dispositivo, tem de anular a inscrição do dispositivo.  
     ![Captura de ecrã de atribuição de perfil do DEP para dispositivos iOS](../media/dep-assign-profile.png)

## <a name="distribute-devices-to-users"></a>Distribuir dispositivos pelos utilizadores
Já pode dar os dispositivos pertencentes à empresa aos utilizadores. A caixa de diálogo **Estado de Inscrição** dos dispositivos geridos indica **Não contactado** até que o dispositivo seja ligado e execute o Assistente de Configuração para inscrever o dispositivo. Quando um dispositivo iOS é ativado, será inscrito para gestão pelo Intune.
