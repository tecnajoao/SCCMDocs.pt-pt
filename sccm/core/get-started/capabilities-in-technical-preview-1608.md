---
title: Funcionalidades no Technical Preview 1608
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
ms.openlocfilehash: d2a55ed81017bc8deb10ec9af74278d35b2eea39
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32333812"
---
# <a name="capabilities-in-technical-preview-1608-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1608 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (Technical Preview)*

Este artigo apresenta as funcionalidades que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1608. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu local de pré-visualização técnica do Configuration Manager.      Antes de instalar esta versão do technical preview, reveja o tópico introdutórias, [pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md), para se familiarizar com os requisitos gerais e limitações para utilizar como uma pré-visualização técnica, ao atualizar entre versões e como fornecer comentários sobre as funcionalidades de um technical preview.    


**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  




##  <a name="improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step"></a>Melhoramentos ao passo Preparar ConfigMgr Client para Captura de sequência de tarefas  
O passo de preparar ConfigMgr Client agora removerá totalmente o cliente do Configuration Manager, em vez de apenas remover informações de chave. Quando a sequência de tarefas, implementa a imagem do sistema operativo capturada, instalará um novo cliente de Configuration Manager cada vez.  


## <a name="improvements-to-software-center"></a>Melhoramentos ao centro de Software
* O Centro de Software **aplicações**, **atualizações**, e **sistemas operativos** separadores agora mostram o tipo de software foram adicionada recentemente. Números no painel de navegação mostram quantos peças novo de software são em cada separador.
* Os utilizadores podem agora solicitar aprovação para aplicações e, em seguida, ver o histórico de pedidos no **detalhes da aplicação** vista no Centro de Software. O **pedido** clique no botão no **detalhes da aplicação** já não redireciona para o catálogo de aplicações baseadas na web.

## <a name="improvements-to-asset-intelligence"></a>Melhoramentos ao Asset Intelligence
Foi adicionado um campo para as propriedades de software inventariado, que permite-lhe definir uma relação principal e subordinada com outro software. Na lista de Software inventariado, pode, em seguida, ver o principal de qualquer software e também ocultariam todo o software de subordinados.

### <a name="configure-a-parent-to-child-relationship"></a>Configurar um principal para a relação de subordinados
  1. Para definir o software de principal, no nó Software inventariado, faça duplo clique num item de software no **Software inventariado** lista e escolha **propriedades**.
  2. Na caixa de diálogo que se abre, selecione o software que pretende definir como o software de principal para a sua seleção inicial.

### <a name="filter-the-software-display"></a>Filtrar a apresentação de software
Depois de ter definido principal para relações de subordinados, pode filtrar a vista para mostrar apenas o software que é um elemento principal ou que não tem qualquer relação definida. Isso oculta todo o software que está definido como subordinado de outro software inventariado. Para fazê-lo:
   1.   Para a barra de pesquisa, optar por **adicionar critérios**
   2. Selecione **principal Software** e, em seguida, altere o valor de critérios para **está vazio**e, em seguida, clique em **pesquisa**.

O ecrã agora mostra apenas os itens de principal de software, ou o software que tenha não existem relações definidas. Não apresentar o software que é apenas um subordinado de outro título.

## <a name="remote-control-keyboard-translation"></a>Tradução de teclado do controlo remoto
No passado, o Configuration Manager transmitidos a posição chave a partir da localização do Visualizador para localização de sharer. Isto foi problemático para configurações de teclado que tabelas diferiu do Visualizador de sharer. Por exemplo, um visualizador com um teclado inglês teria de escrever uma "A", mas teclado francês o sharer iria fornecer um "P". Para que o caráter próprio é transmitido a partir de teclado o Visualizador para o sharer e que o Visualizador pretende escreva chega a sharer iremos estiver a alterar o comportamento predefinido.

Este comportamento pode ser desativado pelo visualizador se que preferem para o tipo de acordo com a disposição de teclado a sharer. Para alterar o comportamento em **controlo remoto do Configuration Manager**, escolha **ação**e escolha **ativar a tradução de teclado** para transmitir posição chave.

> [!NOTE]
>
> Oferta especial de chaves, tais como ~! #@ $%, não será possível converter corretamente.
