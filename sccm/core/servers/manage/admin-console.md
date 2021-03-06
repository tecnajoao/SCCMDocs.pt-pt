---
title: Consola do Configuration Manager
titleSuffix: Configuration Manager
description: Saiba mais sobre como navegar através da consola do Configuration Manager.
ms.date: 03/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 463ce307-59dd-4abd-87b8-42ca9db178d7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0f9c06f40af1134055d4038fd23954b3f4c59682
ms.sourcegitcommit: 544f335cfd1bfd0a1d4973439780e9f5e9ee8bed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/07/2019
ms.locfileid: "57562113"
---
# <a name="using-the-configuration-manager-console"></a>Utilizando a consola do Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Os administradores de utilizam a consola do Configuration Manager para gerir o ambiente do Configuration Manager. Este artigo abrange os conceitos básicos de navegação da consola.  



## <a name="connect-to-a-site-server"></a>Ligar a um servidor de site

A consola estabelece ligação ao seu servidor de site de administração central ou para os seus servidores de site primário. Não é possível ligar uma consola do Configuration Manager para um site secundário. Pode [instalar a consola do Configuration Manager](/sccm/core/servers/deploy/install/install-consoles). Durante a instalação, que especificou o nome de domínio completamente qualificado (FQDN) do servidor do site ao qual se liga a consola. 

Para ligar a um servidor de site diferente, utilize os seguintes passos: 

1. Selecione a seta na parte superior a [faixa de opções](#ribbon)e escolha **ligar a um novo Site**.  

    ![Ligue a consola a um novo site](media/connect-to-a-new-site.png)  

2. Escreva o FQDN do servidor do site. Se anteriormente tiver ligado ao servidor do site, selecione o servidor da lista pendente.  

    ![Janela de ligação do site, introduza o FQDN do servidor do site](media/site-server-fqdn.png)  

3. Selecione **Ligar**.  


A partir da versão 1810, pode especificar o nível mínimo de autenticação para os administradores aceder a sites do Configuration Manager. Esta funcionalidade aplica os administradores para iniciar sessão no Windows com o nível necessário. Para obter mais informações, consulte [planear o fornecedor de SMS](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#bkmk_auth). <!--1357013-->  



## <a name="navigation"></a>Navegação

Algumas áreas da consola poderão não estar visíveis dependendo da sua função de segurança atribuída. Para obter mais informações sobre as funções, consulte [Noções básicas da administração baseada em funções](/sccm/core/understand/fundamentals-of-role-based-administration). 


### <a name="workspaces"></a>Áreas de trabalho

Consola do Configuration Manager tem quatro **áreas de trabalho**:  

- **Ativos e compatibilidade**  

- **Biblioteca de software**  

- **Monitorização**  

- **Administração**  

![Áreas de trabalho do Configuration Manager com o menu de contexto](media/configuration-manager-workspaces.png)  

Reordenar os botões de área de trabalho ao selecionar a seta para baixo e escolher **opções do painel de navegação**. Selecione um item à **mover para cima** ou **mover para baixo**. Selecione **repor** para restaurar a ordem de botão de predefinição.  

 ![Janela de opções do painel de navegação para reordenar as áreas de trabalho](media/navigation-pane-options.png)  

Minimizar um botão de área de trabalho, selecionando **mostrar menos botões**. A última área de trabalho na lista é minimizada pela primeira vez. Selecione um botão minimizado e escolha **mostrar mais botões** para restaurar o botão ao tamanho original.   

![Minimizado áreas de trabalho na consola do Configuration Manager](media/workspace-buttons.png)  


### <a name="nodes"></a>Nós

Áreas de trabalho são uma coleção de **nós**. Um exemplo de um nó é o **grupos de atualização de Software** nó a **biblioteca de Software** área de trabalho. 

Assim que estiver no nó, pode selecionar a seta para minimizar o painel de navegação.  

![Nó de exemplo e realçar minimizar seta](media/software-update-groups-node.png)  

Utilize o **barra de navegação** para mover-se a consola quando minimizar o painel de navegação.  

![Painel de Navegação minimizado de Gestor de configuração](media/minimized-navigation-pane.png)  

Na consola do, nós são, às vezes, organizados em pastas. Clicar diretamente na pasta, normalmente, leva-o para um **índice de navegação** ou uma **dashboard**.  

![Índice de navegação de atualizações de software do Configuration Manager](media/software-updates-navigation-index.png)  


### <a name="ribbon"></a>Faixa de opções 

A faixa de opções está na parte superior da consola do Configuration Manager. A faixa de opções pode ter mais de um separador e pode ser minimizada com a seta à direita. Os botões na alteração da faixa de opções com base no nó. A maioria dos botões na faixa de opções também está disponível nos menus de contexto.  

![Faixa de opções de exemplo, realce vários separadores e minimizar a seta](media/ribbon.png)   


### <a name="details-pane"></a>Painel de detalhes

Pode obter informações adicionais sobre itens ao rever o painel de detalhes. O painel de detalhes, pode ter um ou mais guias. Os separadores variam consoante o nó.  

![Painel de detalhes de exemplo do Configuration Manager](media/details-pane.png)   


### <a name="columns"></a>Colunas 

Pode adicionar, remover, reordenar e redimensionar colunas. Estas ações permitem-lhe apresentar os dados que preferir. Colunas disponíveis variam consoante o nó. Para adicionar ou remover uma coluna da vista, clique com o botão direito num cabeçalho de coluna existente e selecione um item. Reordene colunas ao arrastar o cabeçalho da coluna em que gostaria que ela seja.  

![Adicionar coluna a gerentes de configuração](media/add-columns.png)  

Na parte inferior do menu de contexto de coluna, pode classificar ou agrupar por uma coluna. Além disso, pode ordenar por uma coluna, selecionando o respetivo cabeçalho.  

![Grupo do Configuration Manager por coluna](media/column-group-by.png)  



## <a name="command-line-options"></a>Opções da linha de comandos

Consola do Configuration Manager tem as seguintes opções da linha de comandos:

|Opção|Descrição|  
|------------|-----------------|  
|`/sms:debugview=1`|Um DebugView está incluído no ResultViews todos os que especifique um modo de exibição. DebugView mostra as propriedades não processadas (nomes e valores).|  
|`/sms:NamespaceView=1`|Mostra a vista de espaço de nomes na consola do.|  
|`/sms:ResetSettings`|A consola ignora os Estados de ligação e a vista persistentes de utilizador. O tamanho da janela não for redefinido.|  
|`/sms:IgnoreExtensions`|Desativa quaisquer extensões do Configuration Manager.|  
|`/sms:NoRestore`|A consola ignora a navegação de nó persistentes anteriores.|  



## <a name="tips"></a>Sugestões

### <a name="send-feedback"></a>Enviar feedback
<!--1357542-->

A partir da versão 1806, submeta comentários sobre o produto a partir da consola.  

- **Enviar um sorriso**: Enviar comentários sobre o que gostou  

- **Enviar comentários negativos**: Enviar comentários sobre o que não gostou  

- **Enviar uma sugestão**: Leva-o para o UserVoice para compartilhar sua ideia  
 
Para obter mais informações, consulte [comentários sobre o produto](/sccm/core/understand/find-help#BKMK_1806Feedback).


### <a name="assets-and-compliance-workspace"></a>Ativos e área de trabalho de conformidade

#### <a name="view-users-for-a-device"></a>Ver utilizadores para um dispositivo
A partir da versão 1806, as colunas seguintes estão disponíveis no **dispositivos** nó:  

- **Utilizadores primários** <!--1357280-->  

- **Sessão iniciada no utilizador** <!--1358202-->  
    > [!NOTE]  
    > Visualização requer que o usuário atualmente conectado [deteção de utilizadores](/sccm/core/servers/deploy/configure/configure-discovery-methods#bkmk_config-adud) e [afinidade dispositivo / utilizador](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity).  

Para obter mais informações sobre como mostrar uma coluna não predefinido, consulte [colunas](#columns).

#### <a name="improvement-to-device-search-performance"></a>Melhoria para o desempenho de pesquisa do dispositivo
<!-- 3614690 --> A partir da versão 1806, ao pesquisar numa coleção de dispositivos, não faz a pesquisa a palavra-chave em relação a todas as propriedades do objeto. Quando não específico sobre o que procurar, este procura entre as seguintes quatro propriedades:
- Nome
- Utilizadores primários
- Sessão iniciada no utilizador
- Nome de utilizador do último início de sessão

Este comportamento melhora significativamente o tempo que demora para procurar por nome, especialmente num ambiente grande. As pesquisas personalizadas por critérios específicos não são afetadas por esta alteração. 


### <a name="monitoring-workspace"></a>Área de trabalho monitorização

#### <a name="copy-details-in-monitoring-views"></a>Copiar detalhes em vistas de monitorização
<!--1357856--> A partir da versão 1806, copie as informações a partir da **detalhes do ativo** painel para os seguintes nós de monitorização:  

- **Estado de distribuição de conteúdo**  

- **Estado da implementação**  

![Vista de estado de implementação, detalhes do ativo de cópia](media/1810-deployment-status.PNG)



## <a name="next-steps"></a>Passos seguintes

[Funções de acessibilidade](/sccm/core/understand/accessibility-features)

