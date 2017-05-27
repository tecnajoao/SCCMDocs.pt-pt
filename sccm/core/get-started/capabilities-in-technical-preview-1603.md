---
title: "Capacidades na pré-visualização técnica 1603 do Configuration Manager"
description: "Saiba mais sobre as funcionalidades disponíveis na pré-visualização técnica do System Center Configuration Manager, versão 1603."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5f861b72-9f14-4d17-a512-4a79b660abe6
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: noindex,nofollow
ms.translationtype: Machine Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: dee2b4ce042bb4a434bb019e17a6b16e2807945c
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="capabilities-in-technical-preview-1603-for-system-center-configuration-manager"></a>Funcionalidades de pré-visualização técnica 1603 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo apresenta as funcionalidades que estão disponíveis na pré-visualização técnica do System Center Configuration Manager, versão 1603. Pode instalar esta versão para atualizar e adicionar novas capacidades para o seu site de pré-visualização técnica do Configuration Manager. Em alternativa, quando utilizar o System Center Technical Preview 5, esta versão instalado como uma versão de linha de base do System Center Configuration Manager Technical Preview. Antes de instalar esta versão da pré-visualização técnica, consulte o tópico de introdução, [pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com geral requisitos e limitações à utilização de uma pré-visualização técnica, como atualizar entre as versões e como fornecer comentários sobre as funcionalidades numa pré-visualização técnica.  

 **Problemas conhecidos para esta pré-visualização técnica:**  

-   Nesta versão inclui atualizações para funcionalidades lançadas anteriormente, mas não introduz novas funcionalidades. Por conseguinte, a página de funcionalidades do Assistente de atualização estará vazia se anteriormente tiver atualizado para 1602 e todas as funcionalidades incluídas no 1602 ativada.  

-   Após o servidor do site de atualizações para o 1603 de pré-visualização técnica, os clientes não conseguem utilizar as funcionalidades de controlo remoto até que também de atualizar para versão 1603.  

 **Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

##  <a name="BKMK_SC1603"></a>Melhorias efetuadas ao centro de Software  

### <a name="new-tiled-view-for-apps"></a>Nova vista mosaico para aplicações  
 Os utilizadores finais agora pode escolher entre uma lista de aplicações ou uma vista de aplicações no mosaico do **aplicações** separador do Centro de Software.  

### <a name="select-multiple-updates-in-software-center"></a>Selecionar múltiplas atualizações no Centro de Software  
 No **atualizações** separador do Centro de Software, pode agora selecionar múltiplas atualizações, ou selecionar **atualizar tudo** para começar a instalar várias atualizações em simultâneo.  

##  <a name="BKMK_RC1603"></a>Melhoramentos para controlo remoto  

### <a name="limit-shared-clipboard-access-in-a-remote-control-session"></a>Limitar o acesso de área de transferência partilhado numa sessão de controlo remoto  
 Atualmente, pode ativar a nova definição de cliente de ferramentas remotas **pedir ao utilizador permissão de transferência de ficheiro de área de transferência partilhado** para limitar o acesso à área de transferência partilhado numa sessão de controlo remoto.  

 Quando ativada, o utilizador final quem está a partilhar uma sessão remota tem de conceder permissões para o Visualizador nessa sessão antes do Visualizador pode transferir ficheiros proveniente da sessão para a respetiva máquina local através de área de transferência partilhada.  

 Esta ação adiciona uma camada de proteção para o utilizador final, como anteriormente, se o Visualizador foi concedido controlo total do computador do utilizador final, seria capaz de utilizar a área de transferência partilhada para transferir ficheiros proveniente da sessão para o respetivo computador local de uma forma que foi completamente transparente para o utilizador final.  

##  <a name="BKMK_RamDiskTFTP"></a> Personalizar o tamanho do bloco TFTP do disco de RAM e o tamanho da janela em pontos de distribuição com PXE ativado  
 No 1603 pré-visualização técnica, pode personalizar o tamanho de bloco de TFTP de disco de RAM e o tamanho da janela de pontos de distribuição com PXE ativado. Se tiver personalizado a rede, poderá fazer com que a transferência da imagem de arranque falhe, com um erro de tempo limite excedido, porque o tamanho do bloco ou da janela é demasiado grande. A personalização do tamanho do bloco TFTP do disco de RAM e do tamanho da janela permitem otimizar o tráfego TFTP ao utilizar o PXE para satisfazer requisitos de rede específicos.   
Terá de testar as definições personalizadas no seu ambiente para determinar o que é mais eficiente.  

-   **Tamanho de bloco TFTP**: O tamanho de bloco é o tamanho dos pacotes de dados que são enviadas pelo servidor para o cliente que está a transferir o ficheiro (tal como explicado em RFC 2347). Um tamanho de bloco maior permitirá ao servidor enviar menos pacotes, pelo que existem menos atrasos no percurso de ida e volta entre o servidor e o cliente. No entanto, tamanhos de bloco maiores resultam em pacotes fragmentados, não suportados pela maioria das implementações de cliente PXE.  

-   **Tamanho da janela TFTP**: TFTP necessita de um pacote de confirmação (confirmação) para cada bloco de dados que são enviados. O servidor não envia o bloco seguinte na sequência até receber o pacote ACK para o bloco anterior. O sistema baseado em janelas do TFTP é uma funcionalidade dos Serviços de Implementação do Windows que permite definir quantos blocos de dados são necessários para preencher uma janela. O servidor envia os blocos de dados continuamente até que a janela seja preenchida e, em seguida, o cliente envia um pacote ACK. O aumento do tamanho desta janela reduz o número de atrasos no percurso de ida e volta entre o cliente e o servidor, e diminui o tempo global que é necessário para transferir uma imagem de arranque.  

### <a name="try-it-out"></a>Experimente!  
 Experimente concluir as seguintes tarefas e, em seguida, utilize as informações de comentários perto da parte superior deste tópico para nos transmitir como trabalhou:  

-   Pode personalizar ao tamanho da janela de disco de RAM TFTP no ponto de distribuição com PXE ativado.  

-   Pode personalizar o tamanho do bloco de disco de RAM TFTP no ponto de distribuição com PXE ativado.  

### <a name="to-modify-the-ramdisk-tftp-window-size"></a>Para modificar o tamanho da janela de TFTP do disco de RAM  

-   Adicione a seguinte chave de registo em pontos de distribuição com PXE ativado para personalizar o tamanho da janela de TFTP do disco de RAM:  

     **Localização**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
    Nome: RamDiskTFTPWindowSize  

     **Tipo de**: REG_DWORD  

     **Valor**: &lt;personalizado tamanho da janela\>  

 O valor predefinido é 1 (1 bloco de dados preenche a janela)  

### <a name="to-modify-the-ramdisk-tftp-block-size"></a>Para modificar o tamanho do bloco de TFTP do disco de RAM  

-   Adicione a seguinte chave de registo em pontos de distribuição com PXE ativado para personalizar o tamanho da janela de TFTP do disco de RAM:  

     **Localização**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
    Nome: RamDiskTFTPBlockSize  

     **Tipo de**: REG_DWORD  

     **Valor**: &lt;personalizado tamanho de bloco\>  

 O valor predefinido é 4096 (4k).  

