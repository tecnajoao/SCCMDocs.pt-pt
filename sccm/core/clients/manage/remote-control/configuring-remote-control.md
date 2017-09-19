---
title: Configurar o controlo remoto | Microsoft Docs
description: Configure o controlo remoto no System Center Configuration Manager.
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: dudeso
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45affc27-aa11-4249-9493-082ac23a3a3d
caps.latest.revision: "4"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 633336049feca35f76e3a57e14cc42088a303f8d
ms.sourcegitcommit: f6a428a8db7145affa388f59e0ad880bdfcf17b5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/14/2017
---
# <a name="configuring-remote-control-in-system-center-configuration-manager"></a>Configurar o controlo remoto no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

 Este procedimento descreve a configurar as predefinições de cliente para o controlo remoto. Estas definições se aplicam a todos os computadores na sua hierarquia. Se pretender que estas definições se apliquem apenas a alguns computadores, atribua uma definição para uma coleção que contenha os computadores de cliente de dispositivo personalizada. Para obter mais informações a consulte [como configurar as definições de cliente no System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md). 

Para utilizar a assistência remota ou ambiente de trabalho remoto, tem de ser instalado e configurado no computador que executa a consola do Configuration Manager. Para mais informações sobre como instalar e configurar a Assistência Remota ou o Ambiente de Trabalho Remoto, consulte a documentação do Windows.  

#### <a name="to-enable-remote-control-and-configure-client-settings"></a>Para ativar o controlo remoto e configurar as definições de cliente  

1.  Na consola do Configuration Manager, escolha **administração** > **as definições de cliente** > **predefinições de cliente**.  

4.  No **home page** separador o **propriedades** grupo, escolha **propriedades**.  

5.  No **predefinido** diálogo caixa, escolha **ferramentas remotas**.  

6.  Configure o controlo remoto, assistência remota e ambiente de trabalho remoto, as definições de cliente. Para obter uma lista das definições de cliente de ferramentas remotas que pode configurar, consulte [ferramentas remotas](../../../../core/clients/deploy/about-client-settings.md#remote-tools).  

    Pode alterar o nome da empresa apresentado na caixa de diálogo **Controlo Remoto do ConfigMgr** ao configurar um valor para **Nome da organização apresentada no Centro de Software** nas definições de cliente do **Agente do Computador** .  

 Os computadores cliente são configurados com estas definições da próxima vez que transferirem a política de cliente. Para iniciar a obtenção da política para um único cliente, veja [Como gerir clientes no System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  

#### <a name="enable-keyboard-translation"></a>Ativar a tradução de teclado

Por predefinição, o Configuration Manager transmite a posição chave a partir da localização do Visualizador para localização de sharer. Isto pode apresentar um problema para configurações de teclado que sejam diferentes do Visualizador de sharer. Por exemplo, um visualizador com um teclado inglês teria de escrever uma "A", mas teclado francês o sharer iria fornecer um "P". Tem agora a opção de configurar o controlo remoto para que o caráter próprio é transmitido a partir de teclado o Visualizador para o sharer e que o Visualizador pretende escreva chega a sharer.

Para ativar a tradução de teclado, no **controlo remoto do Configuration Manager**, escolha **ação**e escolha **ativar a tradução de teclado** para transmitir posição chave.

> [!NOTE]
>
> Oferta especial de chaves, tais como ~! #@ $%, não será possível converter corretamente.


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
