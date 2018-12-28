---
title: Configurar o controlo remoto
titleSuffix: Configuration Manager
description: Configure o controlo remoto no System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 45affc27-aa11-4249-9493-082ac23a3a3d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9fac81f08f4750ab6cc133ddc3a3bb9f73780fcd
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53422543"
---
# <a name="configuring-remote-control-in-system-center-configuration-manager"></a>Configurar o controlo remoto no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

 Este procedimento descreve a configurar as predefinições de cliente para o controlo remoto. Estas definições aplicam-se a todos os computadores na sua hierarquia. Se pretender que estas definições se apliquem apenas a alguns computadores, atribua uma definição para uma coleção que contenha os computadores de cliente de dispositivo personalizado. Para obter mais informações, uma veja [como configurar as definições de cliente no System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md). 

Para utilizar a assistência remota ou ambiente de trabalho remoto, tem de ser instalado e configurado no computador que executa a consola do Configuration Manager. Para mais informações sobre como instalar e configurar a Assistência Remota ou o Ambiente de Trabalho Remoto, consulte a documentação do Windows.  

#### <a name="to-enable-remote-control-and-configure-client-settings"></a>Para ativar o controlo remoto e configurar as definições de cliente  

1. Na consola do Configuration Manager, escolha **Administration** > **definições de cliente** > **predefinições de cliente**.  

2. Sobre o **home page** separador a **propriedades** de grupo, escolha **propriedades**.  

3. Na **predefinido** caixa de diálogo caixa, escolha **ferramentas remotas**.  

4. Configure o controlo remoto, assistência remota e ambiente de trabalho remoto, as definições de cliente. Para obter uma lista das definições de cliente de ferramentas remotas que pode configurar, consulte [ferramentas remotas](../../../../core/clients/deploy/about-client-settings.md#remote-tools).  

   Pode alterar o nome da empresa apresentado na caixa de diálogo **Controlo Remoto do ConfigMgr** ao configurar um valor para **Nome da organização apresentada no Centro de Software** nas definições de cliente do **Agente do Computador** .  

   Os computadores cliente são configurados com estas definições da próxima vez que transferirem a política de cliente. Para iniciar a obtenção da política para um único cliente, consulte [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  

#### <a name="enable-keyboard-translation"></a>Ativar a tradução de teclado

Por predefinição, o Configuration Manager transmite a posição de chave de localização do Visualizador a localização do partidor. Isto pode apresentar um problema para configurações de teclado que diferem das Visualizador para partidor. Por exemplo, um visualizador com um teclado inglês teria de escrever um "A", mas o teclado do partidor francês forneceria uma "P". Tem agora a opção de configurar o controlo remoto para que o próprio caractere é transmitido de teclado o Visualizador para o partidor, e o que o Visualizador tenciona escreva chega do partidor.

Para ativar a tradução de teclado, além **controlo de remoto do Configuration Manager**, escolha **ação**e escolha **ativar a tradução de teclado** transmitir a posição de chave.

> [!NOTE]
>
> Chaves de especial, por exemplo, ~! #@ $%, não serão traduzidas corretamente.


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
