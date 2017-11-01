---
title: Acessibilidade
titleSuffix: Configuration Manager
description: "Saiba mais sobre as funcionalidades que tornam o System Center Configuration Manager acessível para pessoas com incapacidades."
ms.custom: na
ms.date: 7/31/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1cb96666-98bf-49a9-85ca-dbb53f0655e9
caps.latest.revision: "6"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 303b58ddea7bc26a38dde2075eb78d1053069c25
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="accessibility-features-in-system-center-configuration-manager"></a>Funcionalidades de acessibilidade no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


System Center Configuration Manager inclui funcionalidades para o ajudar a torná-lo acessível para pessoas com incapacidades.


## <a name="bkmk_aconsole"></a>Funcionalidades de acessibilidade para a consola do Configuration Manager  

**Atalhos e melhoramentos com versão 1706 e posterior**

|Atalho de teclado|  Objetivo|
|--------|--------|  
|CTRL + M|Defina o foco no painel principal (central).|
|CTRL + T|Defina o foco para o nó superior do painel de navegação. Se o foco já foi nesse painel, o foco está definido para o último nó que é visitada.|
|CTRL + I|Defina o foco à barra trilho, abaixo do Friso.|
|CTRL + L|Definir o foco o **pesquisa** campo, quando disponível.|
|CTRL + D|Defina o foco para o painel de detalhes, quando disponível.|
|ALT     |Altere o foco dentro ou fora do Friso.|


- Melhorado navegação no painel de navegação quando escreva as letras de um nome de nó.
- Navegação do teclado através da vista principal e o Friso agora é circular.
- Agora é circular navegação do teclado no painel de detalhes. Para voltar para o objeto anterior ou painel, utilize Ctrl + D, em seguida, Shift + SEPARADOR.
- Depois de atualizar uma vista da área de trabalho, o foco está definido para o painel principal da área de trabalho.
- Foi corrigido um problema ao ativar leitores de ecrã anunciar os nomes dos itens de lista.
- Foram adicionados nomes acessíveis para vários controlos na página que permite aos leitores de ecrã anunciar informações importantes.


**Os seguintes atalhos estão disponíveis para todas as versões**

- Para aceder a uma área de trabalho, utilize os seguintes atalhos de teclado:  

|Atalho de teclado| Área de trabalho|
|--------|--------|  
|CTRL + 1| Ativos e compatibilidade|
|CTRL + 2|  Biblioteca de software|
|CTRL + 3|  Monitorização|
|CTRL + 4|  Administration|


-   Para aceder a um menu da área de trabalho, selecione a tecla Tab até que o ícone expandir/fechar encontrar no foco. Em seguida, selecione a tecla de seta para baixo para aceder ao menu da área de trabalho.  

-   Para navegar através de um menu da área de trabalho, utilize as teclas de seta.  

-   Para aceder a áreas diferentes na área de trabalho, utilize a tecla Tab e as teclas Shift + Tab. Para navegar numa área da área de trabalho, tal como o Friso, utilize as teclas de seta.  

-   Para aceder à barra de endereço quando o foco é o nó da árvore, utilize, por exemplo, três vezes Shift + Tab.  

-   Na página do assistente ou uma propriedade, pode mover entre as caixas com atalhos de teclado. Selecione a tecla Alt plus o caráter de sublinhado (Alt + _) para selecionar uma caixa específica.     

-  Para navegar para os nós de diferentes de uma área de trabalho, introduza a primeira letra do nome de um nó. Cada chave prima move o cursor para o próximo nó que comece com essa letra. Quando estiver a utilizar um leitor de ecrã, lê o leitor de terminar o nome do nó.

> [!NOTE]  
>  As informações nesta secção podem ser aplicadas apenas a utilizadores que licença de produtos da Microsoft nos Estados Unidos. Se tiver adquirido este produto fora dos Estados Unidos, pode utilizar o cartão de informações da subsidiária fornecido com o seu pacote de software ou visitar o [Web site da Microsoft Accessibility](http://go.microsoft.com/fwlink/?LinkId=8431) informações de contacto para a Microsoft suporta os serviços. Pode contactar a sua subsidiária para saber se o tipo de produtos e serviços descritos nesta secção se encontram disponíveis na sua área. Informações sobre acessibilidade estão disponíveis noutros idiomas, incluindo japonês e francês.  

##  <a name="bkmk_ahelp"></a>Funcionalidades de acessibilidade ajuda do Configuration Manager  
 Ajuda do Configuration Manager inclui funcionalidades que tornam acessível a uma vasta gama de utilizadores, incluindo os utilizadores que tenham com destreza limitada, problemas de visão ou outras incapacidades.  

|Para efetuar isto|Utilize este atalho de teclado|  
|----------------|--------------------------------|  
|Visualizar a janela de Ajuda.|F1|  
|Mova o cursor entre o painel de tópicos de ajuda e o painel de navegação (os **conteúdo**, **pesquisa**, e **índice** separadores).|F6|  
|Alternar entre separadores (por exemplo, **conteúdo**, **pesquisa**, e **índice**) no painel de navegação.|ALT + letra sublinhada do separador|  
|Selecionar o texto oculto ou a hiperligação seguinte.|Tecla de Tabulação|  
|Selecionar o texto oculto ou a hiperligação anterior.|SHIFT + Tab|  
|Executar a ação correspondente a Mostrar tudo, Ocultar tudo, texto oculto ou hiperligação.|ENTER|  
|Visualizar o menu **Opções** para aceder a qualquer comando da barra de ferramentas da Ajuda.|ALT + O|  
|Ocultar ou mostrar o painel que contém o **conteúdo**, **pesquisa**, e **índice** separadores.|ALT + O e, em seguida, selecione de T|  
|Visualizar o tópico visualizado anteriormente.|ALT + O e, em seguida, selecione B|  
|Visualizar o tópico seguinte numa sequência de tópicos visualizada anteriormente.|ALT + O e, em seguida, selecione F|  
|Regressar à home page especificada.|ALT + O e, em seguida, selecione de H|  
|Impedir a janela de ajuda de abrir um tópico de ajuda — por exemplo, para parar de transferir uma página Web.|ALT + O e, em seguida, selecione de S|  
|Abrir a caixa de diálogo **Opções da Internet** do Windows Internet Explorer para alterar as definições de acessibilidade.|ALT + O e, em seguida, selecione I|  
|Atualize o tópico, tais como uma página Web ligada.|ALT + O e, em seguida, selecione de R|  
|Imprimir todos os tópicos num livro ou apenas um tópico selecionado.|ALT + O e, em seguida, selecione de P|  
|Fechar a janela de Ajuda.|ALT + F4|  

#### <a name="to-change-the-appearance-of-a-help-topic"></a>Alterar o aspeto de um tópico de Ajuda  

1.  Para se preparar para personalizar as cores, estilos de tipo de letra e tamanhos de tipo de letra na ajuda, abra a janela de ajuda.  

2.  Escolha **opções**e, em seguida, escolha **opções da Internet**.  

3.  No **geral** separador, escolha **acessibilidade**. Escolha **Ignorar cores especificadas em páginas Web**, **Ignorar estilos de tipo de letra especificados em páginas Web**, e **Ignorar tamanhos de tipo de letra especificados em páginas Web**. Também pode optar por utilizar as definições que são especificadas na sua própria folha de estilo.  

#### <a name="to-change-the-color-of-the-background-or-text-in-help"></a>Alterar a cor do fundo ou do texto na Ajuda  

1.  Abra a janela da Ajuda.  

2.  Escolha **opções**e, em seguida, escolha **opções da Internet**.  

3.  No **geral** separador, escolha **acessibilidade**. Em seguida, escolha **Ignorar cores especificadas em páginas Web**. Também pode optar por utilizar as definições que são especificadas na sua própria folha de estilo.  

4.  Para personalizar as cores utilizadas na ajuda, no **geral** separador, escolha **cores**. Desmarque a **utilizar cores do Windows** caixa e, em seguida, escolha as cores de tipo de letra e de fundo que pretende utilizar.  

    > [!NOTE]  
    >  Se alterar a cor de fundo dos tópicos de ajuda na janela da ajuda, a alteração afetará também a cor de fundo das páginas Web no Windows Internet Explorer.  

#### <a name="to-change-the-font-in-help"></a>Alterar o tipo de letra na Ajuda  

1.  Abra a janela da Ajuda.  

2.  Escolha **opções**e, em seguida, escolha **opções da Internet**.  

3.  No **geral** separador, escolha **acessibilidade**. Para utilizar as mesmas definições que são utilizadas na instância do Microsoft Internet Explorer, escolha **Ignorar estilos de tipo de letra especificados em páginas Web** e **Ignorar tamanhos de tipo de letra especificados em páginas Web**. Também pode optar por utilizar as definições que são especificadas na sua própria folha de estilo.  

4.  Para personalizar o estilo de tipo de letra utilizado na ajuda, no **geral** separador, escolha **tipos de letra**e, em seguida, escolha o estilo de tipo de letra pretendido.  

    > [!NOTE]  
    >  Se alterar o tipo de letra dos tópicos de ajuda na janela da ajuda, a alteração afetará também o tipo de letra das páginas Web no Windows Internet Explorer.  
