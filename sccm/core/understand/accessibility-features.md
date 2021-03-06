---
title: Acessibilidade
titleSuffix: Configuration Manager
description: Saiba mais sobre os recursos que tornam o System Center Configuration Manager acessível para pessoas portadoras de deficiência.
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1cb96666-98bf-49a9-85ca-dbb53f0655e9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2f52e903f730590cd9e0b3c8e6f53982ac24fc1b
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56136248"
---
# <a name="accessibility-features-in-system-center-configuration-manager"></a>Funcionalidades de acessibilidade no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


System Center Configuration Manager inclui recursos para ajudar a torná-lo acessível para pessoas com incapacidades.


## <a name="bkmk_aconsole"></a> Funcionalidades de acessibilidade para a consola do Configuration Manager  

**Atalhos e melhorias na versão 1706 e posterior**

|Atalho de teclado|  Objetivo|
|--------|--------|  
|Ctrl + M|Defina o foco no painel principal (central).|
|Ctrl + T|Defina o foco para o nó superior no painel de navegação. Se o foco já foi nesse painel, o foco está definido para o último nó que visitou.|
|Ctrl + I|Defina o foco para a barra de navegação estrutural, abaixo da faixa de opções.|
|Ctrl + L|Definir o foco o **pesquisa** campo, quando disponível.|
|Ctrl + D|Defina o foco para o painel de detalhes, quando disponível.|
|Alt     |Altere o foco dentro e fora da faixa de opções.|


- Melhorada a navegação no painel de navegação quando o utilizador escreve as letras de um nome de nó.
- Navegação do teclado por meio de exibição principal e a faixa de opções está agora circular.
- Navegação do teclado no painel de detalhes é agora circular. Para voltar para o objeto anterior ou o painel, utilize Ctrl + D, em seguida, Shift + SEPARADOR.
- Depois de atualizar uma exibição de área de trabalho, o foco está definido para o painel principal da área de trabalho.
- Foi corrigido um problema para permitir que os leitores de ecrã de anunciar os nomes de itens de lista.
- Foi adicionados nomes acessíveis para vários controles na página que permite que os leitores de ecrã de anunciar a informações importantes.


**Os seguintes atalhos estão disponíveis para todas as versões**

- Para aceder a uma área de trabalho, utilize os seguintes atalhos de teclado:  

|Atalho de teclado| Área de trabalho|
|--------|--------|  
|Ctrl + 1| Ativos e compatibilidade|
|Ctrl + 2|  Biblioteca de software|
|Ctrl + 3|  Monitorização|
|Ctrl + 4|  Administration|


-   Para acessar um menu de área de trabalho, selecione a tecla Tab até que o ícone expandir/fechar fique realçado. Em seguida, selecione a tecla de seta para baixo para aceder ao menu de área de trabalho.  

-   Para navegar num menu de área de trabalho, utilize as teclas de seta.  

-   Para aceder a áreas diferentes na área de trabalho, utilize a tecla Tab e as teclas Shift + Tab. Para navegar numa área de trabalho, como a faixa de opções, utilize as teclas de seta.  

-   Para aceder à barra de endereço quando o nó da árvore estiver realçado, utilize, por exemplo, três vezes Shift + Tab.  

-   Na página de assistente ou uma propriedade, pode mover entre as caixas com atalhos de teclado. Selecione a tecla Alt juntamente com o caráter de sublinhado (Alt + _) para selecionar uma caixa específica.     

-  Para navegar para os nós de diferentes de uma área de trabalho, introduza a primeira letra do nome de um nó. Cada pressionamento de tecla move o cursor para o próximo nó que começa com essa letra. Quando estiver usando um leitor de tela, o leitor lê o nome de um nó.

> [!NOTE]  
>  As informações nesta secção podem aplicar-se somente a usuários que licenciarem os produtos da Microsoft nos Estados Unidos. Se tiver adquirido este produto fora dos Estados Unidos, pode utilizar o cartão de informações da subsidiária fornecido com o seu pacote de software ou visitar o [Web site da Microsoft Accessibility](http://go.microsoft.com/fwlink/?LinkId=8431) informações de contacto para suporte da Microsoft serviços. Pode contactar a sua subsidiária para saber se o tipo de produtos e serviços que são descritos nesta secção estão disponíveis na sua área. Informações sobre acessibilidade estão disponíveis em outros idiomas, incluindo japonês e francês.  

##  <a name="bkmk_ahelp"></a> Funcionalidades de acessibilidade ajuda do Configuration Manager  
 Ajuda do Configuration Manager inclui funcionalidades que o tornam acessível a um maior número de utilizadores, incluindo os utilizadores que têm destreza limitada, visão reduzida ou outras incapacidades.  

|Para efetuar isto|Utilize este atalho de teclado|  
|----------------|--------------------------------|  
|Visualizar a janela de Ajuda.|F1|  
|Mova o cursor entre o painel de tópicos de ajuda e o painel de navegação (os **conteúdo**, **pesquisa**, e **índice** separadores).|F6|  
|Alternar entre separadores (por exemplo, **conteúdo**, **pesquisa**, e **índice**) no painel de navegação.|ALT + letra sublinhada do separador|  
|Selecionar o texto oculto ou a hiperligação seguinte.|Tecla de Tabulação|  
|Selecionar o texto oculto ou a hiperligação anterior.|SHIFT + Tab|  
|Executar a ação correspondente a Mostrar tudo, Ocultar tudo, texto oculto ou hiperligação.|ENTER|  
|Visualizar o menu **Opções** para aceder a qualquer comando da barra de ferramentas da Ajuda.|ALT + O|  
|Ocultar ou mostrar o painel que contém o **conteúdo**, **pesquisa**, e **índice** separadores.|ALT + O e, em seguida, selecione T|  
|Visualizar o tópico visualizado anteriormente.|ALT + O e, em seguida, selecione B|  
|Visualizar o tópico seguinte numa sequência de tópicos visualizada anteriormente.|ALT + O e, em seguida, selecione F|  
|Regressar à home page especificada.|ALT + O e, em seguida, selecione H|  
|Impedir a janela de ajuda de abrir um tópico de ajuda — por exemplo, para parar uma página Web a transferência.|ALT + O e, em seguida, selecione S|  
|Abrir a caixa de diálogo **Opções da Internet** do Windows Internet Explorer para alterar as definições de acessibilidade.|ALT + O e, em seguida, selecione eu|  
|Atualize o tópico, como uma página Web ligada.|ALT + O e, em seguida, selecione R|  
|Imprimir todos os tópicos num livro ou apenas um tópico selecionado.|ALT + O e, em seguida, selecione P|  
|Fechar a janela de Ajuda.|Alt+F4|  

#### <a name="to-change-the-appearance-of-a-help-topic"></a>Alterar o aspeto de um tópico de Ajuda  

1.  Para se preparar para personalizar as cores, estilos de tipo de letra e tamanhos de tipo de letra na ajuda, abrem a janela de ajuda.  

2.  Escolher **opções**e, em seguida, escolha **opções da Internet**.  

3.  Sobre o **gerais** separador, escolha **acessibilidade**. Escolher **Ignorar cores especificadas em páginas da Web**, **Ignorar estilos de tipo de letra especificados em páginas da Web**, e **Ignorar tamanhos de tipo de letra especificados em páginas da Web**. Também pode optar por utilizar as definições especificadas na sua própria folha de estilo.  

#### <a name="to-change-the-color-of-the-background-or-text-in-help"></a>Alterar a cor do fundo ou do texto na Ajuda  

1.  Abra a janela da Ajuda.  

2.  Escolher **opções**e, em seguida, escolha **opções da Internet**.  

3.  Sobre o **gerais** separador, escolha **acessibilidade**. Em seguida, escolha **Ignorar cores especificadas em páginas da Web**. Também pode optar por utilizar as definições especificadas na sua própria folha de estilo.  

4.  Para personalizar as cores utilizadas na ajuda, no **gerais** separador, escolha **cores**. Desmarque os **utilizar cores do Windows** caixa e, em seguida, escolha as cores de fonte e em segundo plano que pretende utilizar.  

    > [!NOTE]  
    >  Se alterar a cor de fundo dos tópicos de ajuda na janela da ajuda, a alteração afetará também a cor de fundo das páginas Web no Windows Internet Explorer.  

#### <a name="to-change-the-font-in-help"></a>Alterar o tipo de letra na Ajuda  

1.  Abra a janela da Ajuda.  

2.  Escolher **opções**e, em seguida, escolha **opções da Internet**.  

3.  Sobre o **gerais** separador, escolha **acessibilidade**. Para utilizar as mesmas definições que são utilizados na sua instância do Windows Internet Explorer, escolha **Ignorar estilos de tipo de letra especificados em páginas da Web** e **Ignorar tamanhos de tipo de letra especificados em páginas da Web**. Também pode optar por utilizar as definições especificadas na sua própria folha de estilo.  

4.  Para personalizar o estilo de tipo de letra utilizado na ajuda, na **gerais** separador, escolha **fontes**e, em seguida, selecione o estilo de tipo de letra que pretende.  

    > [!NOTE]  
    >  Se alterar o tipo de letra dos tópicos de ajuda na janela da ajuda, a alteração afetará também o tipo de letra das páginas Web no Windows Internet Explorer.  
