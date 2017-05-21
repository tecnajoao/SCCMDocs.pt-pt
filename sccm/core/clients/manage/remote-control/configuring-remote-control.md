---
title: Configurar o controlo remoto | Documentos do Microsoft
description: Configure o controlo remoto no System Center Configuration Manager.
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: dudeso
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45affc27-aa11-4249-9493-082ac23a3a3d
caps.latest.revision: 4
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 690d03d9c8c49a815bd318df549d7401a855bc5d
ms.openlocfilehash: 3a386c23c81f413d7d161780bdc0ab3a5b9eccae
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="configuring-remote-control-in-system-center-configuration-manager"></a>Configurar o controlo remoto no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

 Este procedimento descreve configurar as predefinições de cliente de controlo remoto. Estas definições aplicam-se a todos os computadores na sua hierarquia. Se pretender que estas definições se apliquem a apenas alguns utilizadores, atribua uma definição para uma coleção que contém os computadores de cliente personalizada do dispositivo. Para obter mais informações a ver [como configurar as definições de cliente no System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md). 

Para utilizar a assistência remota ou ambiente de trabalho remoto, tem de ser instalado e configurado no computador que executa a consola do Configuration Manager. Para mais informações sobre como instalar e configurar a Assistência Remota ou o Ambiente de Trabalho Remoto, consulte a documentação do Windows.  

#### <a name="to-enable-remote-control-and-configure-client-settings"></a>Para ativar o controlo remoto e configurar as definições de cliente  

1.  Na consola do Configuration Manager, escolha **administração** > **definições de cliente** > **predefinições de cliente**.  

4.  No **base** separador o **propriedades** grupo, selecione **propriedades**.  

5.  No **predefinido** diálogo caixa, selecione **ferramentas remotas**.  

6.  Configure o controlo remoto, assistência remota e ambiente de trabalho remoto, as definições de cliente. Para obter uma lista das definições de cliente de ferramentas remotas que pode configurar, consulte o artigo [ferramentas remotas](../../../../core/clients/deploy/about-client-settings.md#remote-tools).  

    Pode alterar o nome da empresa apresentado na caixa de diálogo **Controlo Remoto do ConfigMgr** ao configurar um valor para **Nome da organização apresentada no Centro de Software** nas definições de cliente do **Agente do Computador** .  

 Os computadores cliente são configurados com estas definições da próxima vez que transferirem a política de cliente. Para iniciar a obtenção da política para um único cliente, veja [Como gerir clientes no System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  

#### <a name="enable-keyboard-translation"></a>Ativar a tradução de teclado

Por predefinição, o Configuration Manager transmite a posição chave a partir da localização do Visualizador para a localização da pessoa. Isto pode apresentar um problema para configurações de teclado que forem diferentes, a partir do viewer para partidor. Por exemplo, um visualizador com um teclado inglês teria de escrever "A", mas teclado francês do partidor seria fornece "Q". Tem agora a opção de configuração de controlo remoto para que o caráter próprio é transmitido a partir do teclado o Visualizador a quem e o que vise o Visualizador no tipo chega a quem.

Para ativar na tradução de teclado, **controlo remoto do Configuration Manager**, escolher **ação**e selecione **ativar tradução teclado** transmitir posição chave.

> [!NOTE]
>
> Chaves de especiais, tais como ~! #@ $%, não irá ser convertidos corretamente.


## <a name="keyboard-shortcuts-for-the-remote-control-viewer"></a>Atalhos de teclado para o Visualizador de controlo remoto

|Atalho de teclado|Descrição|  
|-----------------------|-----------------|  
|Alt+Page Up|Alterna entre executar programas da esquerda para a direita.|  
|Alt+Page Down|Alterna entre executar programas da direita para a esquerda.|  
|Alt+Insert|Percorre a execução de programas pela ordem em que foram abertos.|  
|Alt+Home|Apresenta o menu **Início** .|  
|Ctrl+Alt+End|Apresenta a caixa de diálogo Segurança do Windows (Ctrl+Alt+Del).|  
|Alt+Delete|Apresenta o menu do Windows.|  
|Ctrl+Alt+Sinal de Subtração (no teclado numérico)|Copia a janela ativa no computador local para a Área de transferência do computador remoto.|  
|Ctrl+Alt+Sinal de Adição (no teclado numérico)|Copia toda a área da janela do computador local para a Área de transferência do computador remoto.|  

