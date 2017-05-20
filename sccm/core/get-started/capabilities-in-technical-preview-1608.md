---
title: "Capacidades na pré-visualização técnica 1608 do Configuration Manager"
description: "Saiba mais sobre as funcionalidades disponíveis na pré-visualização técnica do System Center Configuration Manager, versão 1608."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 63e1df5e-637c-4b07-b7ec-95340f43a805
caps.latest.revision: 15
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 5d08d1f9ccd995d544c3c21c4af52ede73343077
ms.openlocfilehash: c22e29da8036d69db917205f28a19a69281a64db
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="capabilities-in-technical-preview-1608-for-system-center-configuration-manager"></a>Funcionalidades de pré-visualização técnica 1608 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo apresenta as funcionalidades que estão disponíveis na pré-visualização técnica do System Center Configuration Manager, versão 1608. Pode instalar esta versão para atualizar e adicionar novas capacidades para o seu site de pré-visualização técnica do Configuration Manager.      Antes de instalar esta versão da pré-visualização técnica, consulte o tópico de introdução, [pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com geral requisitos e limitações à utilização de uma pré-visualização técnica, como atualizar entre as versões e como fornecer comentários sobre as funcionalidades numa pré-visualização técnica.    


**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  




##  <a name="improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step"></a>Melhoramentos ao passo Preparar ConfigMgr Client para Captura de sequência de tarefas  
O passo de preparar ConfigMgr Client agora irá remover completamente o cliente do Configuration Manager, em vez de apenas remoção de informações da chave. Quando a sequência de tarefas, implementa a imagem de sistema operativo capturada irá instalar um novo cliente de Configuration Manager cada vez.  


## <a name="improvements-to-software-center"></a>Melhorias efetuadas ao centro de Software
* O Centro de Software **aplicações**, **atualizações**, e **sistemas operativos** separadores agora mostram qual o software foram adicionado recentemente. Números no painel de navegação mostram quantos blocos novo de software são em cada separador.
* Os utilizadores podem agora solicitar aprovação para aplicações e, em seguida, ver o histórico de pedidos no **detalhes da aplicação** vista no Centro de Software. O **pedido** botão **detalhes da aplicação** já não redireciona para o catálogo de aplicações baseadas na web.

## <a name="improvements-to-asset-intelligence"></a>Melhorias do Asset Intelligence
Adicionámos um campo para as propriedades de software inventariado, que permite-lhe definir uma relação principal e subordinada com outro software. Na lista de Software inventariado, localizado, pode, então, ver o elemento principal de qualquer software e também ocultar todo o software de subordinados.

### <a name="configure-a-parent-to-child-relationship"></a>Configurar um elemento principal a relação de subordinados
  1. Para definir o software de principal, no nó Software inventariado, com o botão direito num item de software no **Software inventariado, localizado** lista e selecione **propriedades**.
  2. Na caixa de diálogo que se abre, selecione o software que pretende definir como o software de principal para a sua seleção inicial.

### <a name="filter-the-software-display"></a>Filtrar a apresentação de software
Após ter definido principal para relações subordinado, pode filtrar a vista para mostrar apenas o software que é um elemento principal ou que não tem qualquer relação definida. Este procedimento oculta todo o software que está definido como subordinado de outro software inventariado. Para fazê-lo:
   1.    Para a barra de pesquisa, optar por **adicionar critérios**
   2. Selecione **principal Software** e, em seguida, altere o valor de critérios para **está vazio**e, em seguida, clique em **pesquisa**.

A apresentação agora mostra apenas os itens de software principal ou software que não tem qualquer relação definida. Não é apresentado o software que é apenas um subordinado de outro título.

## <a name="remote-control-keyboard-translation"></a>Tradução de teclado do controlo remoto
No passado, o Configuration Manager transmitidos a posição chave a partir da localização do Visualizador para localização da pessoa que está. Isto foi problemáticas para configurações de teclado que é divergente do Visualizador de partidor. Por exemplo, um visualizador com um teclado inglês teria de escrever "A", mas teclado francês do partidor seria fornece "Q". Para que o caráter próprio é transmitido a partir do teclado o Visualizador a quem e o que vise o Visualizador no tipo chega do partidor estamos está a alterar o comportamento predefinido.

Este comportamento pode ser desativado pelo visualizador se que preferem para o tipo de acordo com a disposição de teclado do partidor Para alterar o comportamento, na **controlo remoto do Configuration Manager**, escolha **ação**e escolha **ativar tradução teclado** transmitir posição chave.

> [!NOTE]
>
> Chaves de especiais, tais como ~! #@ $%, não irá ser convertidos corretamente.

