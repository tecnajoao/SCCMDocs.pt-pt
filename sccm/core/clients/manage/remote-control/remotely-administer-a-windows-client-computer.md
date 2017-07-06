---
title: Administrar remotamente o computador com o Windows | Documentos do Microsoft
description: Administrar um computador de cliente remoto do Windows utilizando o System Center Configuration Manager.
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3c9648c4-645e-4e47-ae10-2da817b8c83b
caps.latest.revision: 5
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 690d03d9c8c49a815bd318df549d7401a855bc5d
ms.openlocfilehash: 63113a2928c0aca292e6ca07ffe1187324801b7b
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="how-to-remotely-administer-a-windows-client-computer-by-using-system-center-configuration-manager"></a>Como administrar remotamente o computador cliente Windows utilizando o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Antes de começar a utilizar o controlo remoto, certifique-se de que reviu as informações nos seguintes tópicos:  

-   [Pré-requisitos para controlo remoto no System Center Configuration Manager](../../../../core/clients/manage/remote-control/prerequisites-for-remote-control.md)  

-   [Configurar o controlo remoto no System Center Configuration Manager](../../../../core/clients/manage/remote-control/configuring-remote-control.md)  

Seguem-se três formas de iniciar o Visualizador de controlo remoto:  

-   Na consola do Configuration Manager.  

-   Numa linha de comandos Windows comando.  

-   No Windows **iniciar** menu num computador que executa a consola do Configuration Manager a partir de **Microsoft System Center** grupo de programas.  

### <a name="to-remotely-administer-a-client-computer-from-the-configuration-manager-console"></a>Para administrar remotamente um computador cliente a partir da consola do Configuration Manager  

1.  Na consola do Configuration Manager, escolha **ativos e compatibilidade** > **dispositivos** ou **coleções de dispositivos**.  

3.  Selecione o computador que pretende administrar remotamente e, em seguida, no **base** separador o **dispositivo** grupo, selecione **iniciar** > **controlo remoto**.  

    > [!IMPORTANT]  
    >  Se a permissão de cliente **Solicitar ao utilizador permissão do Controlo Remoto** estiver definida como **Verdadeiro**, a ligação não inicia até o utilizador no computador remoto aceitar o pedido de controlo remoto. Para obter mais informações, consulte o artigo [configurar o controlo remoto no System Center Configuration Manager](../../../../core/clients/manage/remote-control/configuring-remote-control.md).  

4.  Depois de a janela **Controlo Remoto do Configuration Manager** ser aberta, pode administrar remotamente o computador cliente. Utilize as opções seguintes para configurar a ligação.  

    > [!NOTE]  
    >  Se o computador que se liga ao tiver vários monitores, a apresentação a partir de todos os monitores é apresentada na janela de controlo remoto.  

    -   **Ficheiro - ligar** -ligar-se para outro computador. Esta opção não está disponível quando uma sessão de controlo remoto está ativa.  

    -   **Ficheiro - desligar** - termina a sessão ativa de controlo remoto, mas não feche a **controlo remoto do Configuration Manager** janela.  

    -   **Ficheiro - sair** - termina a sessão ativa de controlo remoto e fecha o **controlo remoto do Configuration Manager** janela.  

        > [!NOTE]  
        >  Quando desligar uma sessão de controlo remoto, o conteúdo da Área de Transferência do Windows no computador que está a visualizar é eliminado.  

    -   **Vista - ecrã inteiro** -maximiza o **controlo remoto do Configuration Manager** janela.  

        > [!NOTE]  
        >  Para sair do modo de ecrã inteiro, prima Ctrl+Alt+Break.  

    -   **Vista - Ajustar tamanho** -dimensiona a apresentação do computador remoto para ajustar o tamanho do **controlo remoto do Configuration Manager** janela.  

    -   **Vista - barra de estado** -alterna a apresentação do **controlo remoto do Configuration Manager** barra de estado de janela.  

    -   **Ação - Enviar Ctrl + Alt + Del chave** -envia uma combinação de teclas Ctrl + Alt + Del para o computador remoto.  

    -   **Ação - ativar a partilha da área de transferência** -permite-lhe copiar e colar itens de e para o computador remoto. Se alterar este valor, tem de reiniciar a sessão de controlo remoto para que a alteração tenha efeito.  

        > [!NOTE]  
        >  Se não pretender que área de transferência de partilha para ser ativada na consola do Configuration Manager, no computador que executa a consola, defina o valor da chave de registo, **HKEY_CURRENT_USER\Software\Microsoft\ConfigMgr10\Remote Control\Clipboard partilha** para **0**.  

    -   **Ação - bloqueio remoto teclado e rato** -bloqueia o teclado remoto e o rato para impedir que o utilizador a partir do computador remoto a funcionar.  

    -   **Ajuda - sobre o controlo remoto** -versão atual de ithe apresenta do Visualizador de.  

5.  Os utilizadores ao computador remoto podem ver mais informações acerca da sessão de controlo remoto ao clicarem o Configuration Manager**controlo remoto** ícone na área de notificação do Windows ou o ícone na barra de sessão de controlo remoto.  

### <a name="to-start-the-remote-control-viewer-from-the-windows-command-line"></a>Para iniciar o visualizador de controlo remoto a partir da linha de comandos do Windows  

-   Na linha de comandos do Windows, escreva *< pasta de instalação do Configuration Manager\>***\AdminConsole\Bin\x64\CmRcViewer.exe**  

    > [!NOTE]  
    >  CmRcViewer.exe suporta as seguintes opções da linha de comandos:  
    >   
    >  -   *< endereço\>*  -Especifica o nome NetBIOS, o nome de domínio completamente qualificado (FQDN) ou o endereço IP do computador cliente que pretende ligar.  
    > -   *< nome do servidor de site\>*  -Especifica o nome do servidor do site do System Center Configuration Manager para o qual pretende enviar mensagens de estado que estão relacionados com a sessão de controlo remoto.  
    > -   **/?** -Apresenta as opções da linha de comandos para o Visualizador de controlo remoto.  
    >   
    >  **Example:CmRcViewer.exe** *< endereço\>*   *< \\\Site nome do servidor >*  
