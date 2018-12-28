---
title: Funcionalidades no Technical Preview 1603
titleSuffix: Configuration Manager
description: Saiba mais sobre as funcionalidades disponíveis no Technical Preview do System Center Configuration Manager, versão 1603.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5f861b72-9f14-4d17-a512-4a79b660abe6
author: aczechowski
robots: noindex,nofollow
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: c7a0c1438fe08e1efae9d2bfe5fb608214486031
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53423053"
---
# <a name="capabilities-in-technical-preview-1603-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1603 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo apresenta os recursos que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1603. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu site de pré-visualização técnica do Configuration Manager. Em alternativa, quando utiliza o System Center Technical Preview 5, esta versão é instalado como uma versão de linha de base do System Center Configuration Manager Technical Preview. Antes de instalar esta versão do technical preview, consulte o tópico introdutório, [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos gerais e limitações para a utilização de um Technical preview, como atualizar entre versões e como fornecer comentários sobre os recursos de uma technical preview.  

 **Problemas conhecidos desta pré-visualização técnica:**  

- Esta versão inclui atualizações para funcionalidades lançadas anteriormente, mas não introduz recursos novos. Por conseguinte, a página de recursos do Assistente de atualização estará vazia se anteriormente tiver atualizado para a versão 1602 e ativada em todas as funcionalidades incluídas na 1602.  

- Após a atualização de seu servidor do site para o Technical Preview 1603, os clientes não conseguem utilizar quaisquer funcionalidades de controlo remoto até atualizarem também para a versão 1603.  

  **Seguem-se os novos recursos, que pode experimentar com esta versão.**  

##  <a name="BKMK_SC1603"></a> Melhoramentos ao centro de Software  

### <a name="new-tiled-view-for-apps"></a>Nova vista em mosaico para aplicações  
 Os utilizadores finais podem agora escolher entre uma lista de aplicações ou uma vista em mosaico das aplicações no **aplicativos** separador do Centro de Software.  

### <a name="select-multiple-updates-in-software-center"></a>Selecionar múltiplas atualizações no Centro de Software  
 Na **atualizações** separador do Centro de Software, pode agora selecionar múltiplas atualizações ou selecionar **atualizar tudo** para começar a instalar várias atualizações em simultâneo.  

##  <a name="BKMK_RC1603"></a> Melhoramentos no controlo remoto  

### <a name="limit-shared-clipboard-access-in-a-remote-control-session"></a>Limitar o acesso de área de transferência partilhada numa sessão de controlo remoto  
 Agora, pode ativar o nova definição de cliente de ferramentas remoto **pedir ao utilizador permissão de transferência do ficheiro de área de transferência partilhada** para limitar o acesso para a área de transferência partilhada numa sessão de controlo remoto.  

 Quando ativada, o utilizador final que está a partilhar uma sessão remota tem de conceder permissões ao Visualizador dessa sessão antes do Visualizador poder transferir ficheiros da sessão para o seu computador local por meio da área de transferência partilhada.  

 Esta ação adiciona uma camada de proteção para o usuário final como anteriormente, se o Visualizador era concedido controlo total do computador do usuário final, seria possível usar a área de transferência partilhada para transferir os ficheiros da sessão para o respetivo computador local de forma que era totalmente transparen t para o utilizador final.  

##  <a name="BKMK_RamDiskTFTP"></a> Personalizar o tamanho do bloco TFTP do disco de RAM e o tamanho da janela em pontos de distribuição com PXE ativado  
 No 1603 Technical Preview, pode personalizar o tamanho do bloco TFTP do disco e o tamanho de janela para pontos de distribuição com PXE ativado. Se tiver personalizado a rede, poderá fazer com que a transferência da imagem de arranque falhe, com um erro de tempo limite excedido, porque o tamanho do bloco ou da janela é demasiado grande. A personalização do tamanho do bloco TFTP do disco de RAM e do tamanho da janela permitem otimizar o tráfego TFTP ao utilizar o PXE para satisfazer requisitos de rede específicos.   
Terá de testar as definições personalizadas no seu ambiente para determinar o que é mais eficiente.  

-   **Tamanho do bloco TFTP**: O tamanho do bloco é o tamanho dos pacotes de dados que são enviados pelo servidor para o cliente que está a transferir o ficheiro (conforme referido em RFC 2347). Um tamanho de bloco maior permitirá ao servidor enviar menos pacotes, pelo que existem menos atrasos no percurso de ida e volta entre o servidor e o cliente. No entanto, tamanhos de bloco maiores resultam em pacotes fragmentados, não suportados pela maioria das implementações de cliente PXE.  

-   **Tamanho da janela TFTP**: TFTP necessita de um pacote de confirmação (ACK) para cada bloco de dados que são enviados. O servidor não envia o bloco seguinte na sequência até receber o pacote ACK para o bloco anterior. O sistema baseado em janelas do TFTP é uma funcionalidade dos Serviços de Implementação do Windows que permite definir quantos blocos de dados são necessários para preencher uma janela. O servidor envia os blocos de dados continuamente até que a janela seja preenchida e, em seguida, o cliente envia um pacote ACK. O aumento do tamanho desta janela reduz o número de atrasos no percurso de ida e volta entre o cliente e o servidor, e diminui o tempo global que é necessário para transferir uma imagem de arranque.  

### <a name="try-it-out"></a>Experimente!  
 Experimente concluir as seguintes tarefas e, em seguida, utilize as informações de feedback perto da parte superior deste tópico para nos informar como correu:  

-   Consigo personalizar o tamanho da janela de TFTP do disco no ponto de distribuição com PXE ativado.  

-   Consigo personalizar o tamanho do bloco TFTP do disco no ponto de distribuição com PXE ativado.  

### <a name="to-modify-the-ramdisk-tftp-window-size"></a>Para modificar o tamanho da janela de TFTP do disco de RAM  

- Adicione a seguinte chave de registo em pontos de distribuição com PXE ativado para personalizar o tamanho da janela de TFTP do disco de RAM:  

   **Localização**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
  Nome: RamDiskTFTPWindowSize  

   **Tipo de**: REG_DWORD  

   **Valor**: &lt;tamanho de janela personalizado\>  

  O valor predefinido é 1 (1 bloco de dados preenche a janela)  

### <a name="to-modify-the-ramdisk-tftp-block-size"></a>Para modificar o tamanho do bloco de TFTP do disco de RAM  

- Adicione a seguinte chave de registo em pontos de distribuição com PXE ativado para personalizar o tamanho da janela de TFTP do disco de RAM:  

   **Localização**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
  Nome: RamDiskTFTPBlockSize  

   **Tipo de**: REG_DWORD  

   **Valor**: &lt;tamanho de bloco personalizado\>  

  O valor predefinido é 4096 (4k).  
