---
title: Administrar remotamente o computador com o Windows
titleSuffix: Configuration Manager
description: Administrar um computador de cliente remoto do Windows utilizando o System Center Configuration Manager.
ms.date: 07/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3c9648c4-645e-4e47-ae10-2da817b8c83b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4437ef8f88b18b7148eadbc3d125d8ac72fb240a
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-remotely-administer-a-windows-client-computer-by-using-system-center-configuration-manager"></a>Como administrar remotamente um computador cliente Windows utilizando o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Antes de começar a utilizar o controlo remoto, certifique-se de que reviu as informações nos seguintes tópicos:  

-   [Pré-requisitos para controlo remoto no System Center Configuration Manager](../../../../core/clients/manage/remote-control/prerequisites-for-remote-control.md)  

-   [Configurar o controlo remoto no System Center Configuration Manager](../../../../core/clients/manage/remote-control/configuring-remote-control.md)  

Seguem-se três formas de iniciar o Visualizador de controlo remoto:  

-   Na consola do Configuration Manager.  

-   Na linha de comandos do Windows.  

-   O Windows **iniciar** menu num computador que executa a consola do Configuration Manager do **Microsoft System Center** grupo de programas.  

### <a name="to-remotely-administer-a-client-computer-from-the-configuration-manager-console"></a>Para administrar remotamente um computador cliente a partir da consola do Configuration Manager  

1.  Na consola do Configuration Manager, escolha **ativos e compatibilidade** > **dispositivos** ou **coleções de dispositivos**.  

3.  Selecione o computador que pretende administrar remotamente e, em seguida, no **home page** separador o **dispositivo** grupo, escolha **iniciar** > **controlo remoto**.  

    > [!IMPORTANT]  
    >  Se a permissão de cliente **Solicitar ao utilizador permissão do Controlo Remoto** estiver definida como **Verdadeiro**, a ligação não inicia até o utilizador no computador remoto aceitar o pedido de controlo remoto. Para obter mais informações, consulte [configurar o controlo remoto no System Center Configuration Manager](../../../../core/clients/manage/remote-control/configuring-remote-control.md).  

4.  Depois de a janela **Controlo Remoto do Configuration Manager** ser aberta, pode administrar remotamente o computador cliente. Utilize as opções seguintes para configurar a ligação.  

    > [!NOTE]  
    >  Se o computador se ligar à tiver vários monitores, a apresentação de todos os monitores é apresentada na janela do controlo remoto.  

    -   **Ficheiro - ligar** -ligar a outro computador. Esta opção não está disponível quando uma sessão de controlo remoto está ativa.  

    -   **Ficheiro - desligar** - desliga a sessão ativa de controlo remoto, mas não fecha a **controlo remoto do Configuration Manager** janela.  

    -   **Ficheiro - sair** - desliga a sessão de controlo remoto ativa e fecha o **controlo remoto do Configuration Manager** janela.  

        > [!NOTE]  
        >  Quando desligar uma sessão de controlo remoto, o conteúdo da Área de Transferência do Windows no computador que está a visualizar é eliminado.  

    -   **Vista - ecrã inteiro** -maximiza o **controlo remoto do Configuration Manager** janela.  

        > [!NOTE]  
        >  Para sair do modo de ecrã inteiro, prima Ctrl+Alt+Break.  

    -   **Vista - Ajustar** -dimensiona a apresentação do computador remoto para ajustar o tamanho do **controlo remoto do Configuration Manager** janela.  

    -   **Vista - barra de estado** -alterna a apresentação do **controlo remoto do Configuration Manager** barra de estado de janela.  

    -   **Ação - Enviar Ctrl + Alt + Del chave** -envia uma combinação de teclas Ctrl + Alt + Del para o computador remoto.  

    -   **Ação - ativar partilha de área de transferência** -lhe permite copiar e colar itens de e para o computador remoto. Se alterar este valor, tem de reiniciar a sessão de controlo remoto para que a alteração tenha efeito.  

        > [!NOTE]  
        >  Se não pretender que a área de transferência partilha esteja ativado na consola do Configuration Manager, no computador que executa a consola, defina o valor da chave de registo, **HKEY_CURRENT_USER\Software\Microsoft\ConfigMgr10\Remote Control\Clipboard partilha** para **0**.  

    -   **Ação - bloquear teclado e rato remotos** -bloqueia o teclado e rato remotos para impedir que o utilizador se o computador remoto.  

    -   **Ajuda - acerca do controlo remoto** -versão atual do ithe apresenta do Visualizador de.  

5.  Os utilizadores ao computador remoto, podem ver mais informações sobre a sessão de controlo remoto ao clicarem o Gestor de configuração**controlo remoto** ícone na área de notificação do Windows ou no ícone na barra de sessão de controlo remoto.  

### <a name="to-start-the-remote-control-viewer-from-the-windows-command-line"></a>Para iniciar o visualizador de controlo remoto a partir da linha de comandos do Windows  

-   A linha de comandos do Windows, escreva *< pasta de instalação do Configuration Manager\>***\AdminConsole\Bin\x64\CmRcViewer.exe**  

CmRcViewer.exe suporta as seguintes opções da linha de comandos:  

- *Endereço* -Especifica o nome NetBIOS, o nome de domínio completamente qualificado (FQDN) ou o endereço IP do computador cliente que pretende ligar.
- *Nome do servidor do site* -Especifica o nome do servidor do site do System Center Configuration Manager para o qual pretende enviar mensagens de estado relacionadas com a sessão de controlo remoto.
- **/?** -Apresenta as opções da linha de comandos para o Visualizador de controlo remoto.  
     
**Example:CmRcViewer.exe** *< endereço\>*   *< \\\Site o nome do servidor >*  
