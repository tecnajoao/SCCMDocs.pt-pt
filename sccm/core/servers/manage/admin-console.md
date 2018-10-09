---
title: Consola do Configuration Manager
titleSuffix: Configuration Manager
description: Saiba mais sobre como navegar através da consola do Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 463ce307-59dd-4abd-87b8-42ca9db178d7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 793ba0f05c7a188a6bda9649c9d25922ce27d42c
ms.sourcegitcommit: 3dfe3f4401651afa9dc65d14a8944ae4e4198b3e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/08/2018
ms.locfileid: "48862469"
---
# <a name="using-the-system-center-configuration-manager-console"></a>Utilizando a consola do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Os administradores de utilizam a consola do System Center Configuration Manager para gerir o ambiente do Configuration Manager. Este artigo abrange os conceitos básicos de navegação da consola. Melhorias na consola estão listadas por versão na parte inferior deste artigo. 

## <a name="connect-the-console-to-a-site-server"></a>Ligue a consola a um servidor de site
A consola estabelece ligação ao seu servidor de site de administração central ou para os seus servidores de site primário. No entanto, não é possível ligar uma consola do Configuration Manager para um site secundário. Se for necessário, [instalar a consola do Configuration Manager](../deploy/install/install-consoles.md). Durante a instalação, que especificou o nome de domínio completamente qualificado (FQDN) do servidor do site ao qual se liga a consola do Configuration Manager. Para ligar a um servidor de site diferente, utilize as instruções seguintes: 

1. Clique na seta na parte superior da faixa de opções e selecione **ligar a um novo Site**.
    ![Ligue a consola a um novo site](media/connect-to-a-new-site.png)
2. Escreva o FQDN do servidor do site. Se anteriormente tiver ligado ao servidor do site, selecione o servidor da lista pendente.  
    ![Escreva o FQDN do servidor do site](media/site-server-fqdn.png)
3. Clique em **Ligar**. 

## <a name="navigate-the-console"></a>Navegue até a consola do
Algumas opções sob a consola podem não ser visíveis dependendo da sua função de segurança atribuídas. Para obter mais informações sobre as funções, consulte [Noções básicas da administração baseada em funções](../../understand/fundamentals-of-role-based-administration.md). 

### <a name="workspaces"></a>Áreas de trabalho
Consola do Configuration Manager tem quatro **áreas de trabalho**: 
   - **Ativos e compatibilidade**
   - **Biblioteca de software**
   - **Monitorização**
   - **Administração**

 ![Áreas de trabalho do Configuration Manager](media/configuration-manager-workspaces.png)

Reordenar os botões de área de trabalho ao clicar na seta para baixo e selecionar **opções do painel de navegação**. Selecione um item à **mover para cima** ou **mover para baixo**. Clique em **repor** para restaurar a ordem de botão de predefinição. 

 ![Reordenar as áreas de trabalho do Configuration Manager](media/navigation-pane-options.png)

Pode minimizar um botão de área de trabalho, selecionando **mostrar menos botões**. A última área de trabalho na lista de área de trabalho é minimizada pela primeira vez. Clicar num botão minimizado e selecionando **mostrar mais botões** restaura o botão ao tamanho original.  

![Áreas de trabalho do Configuration Manager](media/workspace-buttons.png)


### <a name="nodes"></a>Nós
Áreas de trabalho são uma coleção de **nós**. Um exemplo de um nó é o **grupos de atualização de Software** nó. Assim que estiver no nó, pode clicar na seta para minimizar o painel de navegação. 

![Áreas de trabalho do Configuration Manager](media/software-update-groups-node.png)

Pode utilizar o **barra de navegação** para mover-se a consola quando o painel de navegação é minimizado. 

![Painel de Navegação minimizado de Gestor de configuração](media/minimized-navigation-pane.png)

Na consola do, nós são, às vezes, organizados em pastas. Clicar diretamente na pasta, normalmente, leva-o para um **índice de navegação** ou uma **dashboard**.

![Índice de navegação de atualizações de software do Configuration Manager](media/software-updates-navigation-index.png)

### <a name="ribbon"></a>Faixa de opções 
A faixa de opções está na parte superior da consola do Configuration Manager. A faixa de opções pode ter mais de um separador e pode ser minimizada com a seta à direita. Os botões na alteração da faixa de opções com base no nó. A maioria dos botões na faixa de opções também está disponível no botão direito do rato clique em menus. 
 
![Índice de navegação de atualizações de software do Configuration Manager](media/ribbon.png)

### <a name="details-pane"></a>Painel de detalhes
Pode obter informações adicionais sobre itens ao rever o painel de detalhes. O painel de detalhes, pode ter um ou mais guias. Os separadores variam consoante o nó. 
![Painel de detalhes do Configuration Manager](media/details-pane.png)

### <a name="columns"></a>Colunas 
Pode adicionar, remover, reordenar e redimensionar colunas. Estas ações permitem-lhe apresentar os dados que preferir. Colunas disponíveis irão variar consoante o nó. Com o botão direito num cabeçalho de coluna existente, em seguida, clique num item para adicionar ou remover da vista. Reordene colunas ao arrastar o cabeçalho da coluna em que gostaria que ela seja. 
![Adicionar coluna a gerentes de configuração](media/add-columns.png)

Na parte inferior da coluna com o botão direito clique menu, pode classificar ou agrupar por uma coluna. Além disso, pode ordenar por uma coluna ao clicar no respetivo cabeçalho. 

![Grupo do Configuration Manager por coluna](media/column-group-by.png)

##<a name="console-command-line-options"></a>Opções da linha de comandos da consola
A consola do Microsoft System Center Configuration Manager tem as seguintes opções da linha de comandos.

|Opção|Descrição|  
|------------|-----------------|  
|**/SMS:debugview = 1**|Um DebugView está incluído no ResultViews todos os que especifique um modo de exibição. DebugView mostra as propriedades não processadas (nomes e valores).|  
|**/SMS:NamespaceView = 1**|Mostra a vista de espaço de nomes na consola do System Center Configuration Manager.|  
|**/SMS:ResetSettings**|A consola do System Center Configuration Manager ignora a usuário persistente Estados de ligação e o modo de exibição (tamanho da janela de Console de gerenciamento Microsoft não é reposto).|  
|**/SMS:IgnoreExtensions**|Desativa quaisquer extensões do System Center Configuration Manager.|  
|**/SMS:NoRestore**|A consola do System Center Configuration Manager ignora a navegação de nó persistentes anteriores.|  

## <a name="console-improvements-in-version-1806"></a>Melhorias da consola na versão 1806
No Configuration Manager versão 1806, são adicionadas as seguintes melhorias de consola:

- **Utilizadores primários** está disponível como uma coluna no nó de dispositivos. <!--1357280-->
- **Sessão iniciada no utilizador** está disponível como uma coluna no nó de dispositivos.<!--1358202-->
- Copiar informações a partir da **detalhes do ativo** painel para as seguintes vistas de monitorização: <!--1357856-->
    - Estado de distribuição de conteúdo
    - Estado da implementação 

    ![Detalhes de ativo de cópia do Configuration Manager](media/1810-deployment-status.PNG)

 - Envie comentários a partir da consola. Pode salvar uma cópia para submeter mais tarde, se não tiver acesso à internet. <!--1357542-->
   
    - **Enviar um sorriso**: Envie comentários sobre o que gostou.
    - **Enviar comentários negativos**: Envie comentários sobre o que não gostou. 
    - **Enviar uma sugestão**: Leva-o para o UserVoice para compartilhar sua ideia. 
 
       ![Enviar comentários para o Configuration Manager](media/1810-send-a-smile.PNG)
![formulário de comentários do Configuration Manager](media/1810-feedback-form.PNG)

## <a name="next-steps"></a>Passos seguintes
> [!div class="nextstepaction"]
> [Funcionalidades de acessibilidade](/sccm/core/understand/accessibility-features.md)

