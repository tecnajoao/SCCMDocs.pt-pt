---
title: Funcionalidades no Technical Preview versão 1608
titleSuffix: Configuration Manager
description: Saiba mais sobre as funcionalidades disponíveis no Technical Preview do System Center Configuration Manager, versão 1608.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 63e1df5e-637c-4b07-b7ec-95340f43a805
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: 304f5e65d97682914f917bd2e125763156098225
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/24/2019
ms.locfileid: "54896384"
---
# <a name="capabilities-in-technical-preview-1608-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview versão 1608 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo apresenta os recursos que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1608. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu site de pré-visualização técnica do Configuration Manager.      Antes de instalar esta versão do technical preview, consulte o tópico introdutório, [Technical Preview do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos gerais e limitações para a utilização de um Technical preview, como atualizar entre versões e como fornecer comentários sobre os recursos de uma technical preview.    


**Seguem-se os novos recursos, que pode experimentar com esta versão.**  




##  <a name="improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step"></a>Melhoramentos ao passo Preparar ConfigMgr Client para Captura de sequência de tarefas  
O passo preparar ConfigMgr Client agora removerá completamente o cliente do Configuration Manager, em vez de apenas remover informações de chave. Quando a sequência de tarefas implementa a imagem de sistema operativo capturada que irá instalar um novo cliente de Configuration Manager cada vez.  


## <a name="improvements-to-software-center"></a>Melhoramentos ao centro de Software
* O Centro de Software **aplicativos**, **atualizações**, e **sistemas operativos** separadores mostram, agora, que software foi adicionado recentemente. Números no painel de navegação mostram quantas partes novo de software estão em cada separador.
* Os utilizadores podem agora solicitar aprovação para as aplicações e, em seguida, ver o histórico de pedidos na **detalhes da aplicação** vista no Centro de Software. O **pedir** botão na **detalhes da aplicação** já não redireciona para o catálogo de aplicações baseadas na web.

## <a name="improvements-to-asset-intelligence"></a>Melhorias ao Asset Intelligence
Adicionámos um campo para as propriedades de software inventariado que lhe permite definir uma relação de pai e filho com outro software. Na lista Software inventariado, pode ver, em seguida, o principal de qualquer software e também ocultar todo o software subordinado.

### <a name="configure-a-parent-to-child-relationship"></a>Configurar um encarregado de educação para relação de subordinado
  1. Para definir o software de principal, no nó Software inventariado, clique com botão direito num item de software no **Software inventariado** lista e escolha **propriedades**.
  2. Na caixa de diálogo que se abre, selecione o software que pretende definir como o software de principal para a sua seleção inicial.

### <a name="filter-the-software-display"></a>Filtrar a exibição de software
Depois de definir principal para as relações de subordinados, pode filtrar a vista para mostrar apenas o software que é um elemento principal ou que não tem qualquer relação definida. Isso oculta todos os softwares que está definido como subordinado de outro software inventariado. Para fazê-lo:
   1.   Para a barra de pesquisa, optar por **adicionar critérios**
   2. Selecione **Software principal** e, em seguida, altere o valor de critérios para **está vazia**e, em seguida, clique em **pesquisa**.

A exibição mostra agora apenas os itens de software principal ou software que tem não existem relações definidas. Não apresentar o software que é apenas um subordinado de outro título.

## <a name="remote-control-keyboard-translation"></a>Tradução de teclado de controlo remoto
No passado, o Configuration Manager transmitidos a posição de chave de localização do Visualizador a localização do partidor. Isso foi problemático para as configurações de teclado que eram diferentes quanto Visualizador para partidor. Por exemplo, um visualizador com um teclado inglês teria de escrever um "A", mas o teclado do partidor francês forneceria uma "P". Estamos a alterar o comportamento padrão para que o próprio caractere é transmitido de teclado o Visualizador para o partidor, e o que o Visualizador tenciona escreva chega do partidor.

Esse comportamento pode ser desativado pelo visualizador se eles preferem escrever, de acordo com disposição de teclado do partidor. Para alterar o comportamento, no **controlo de remoto do Configuration Manager**, escolha **ação**e escolha **ativar a tradução de teclado** transmitir a posição de chave.

> [!NOTE]
>
> Chaves de especial, por exemplo, ~! #@ $%, não serão traduzidas corretamente.
