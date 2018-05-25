---
title: Pré-visualização técnica 1804
titleSuffix: Configuration Manager
description: Saiba mais sobre as novas funcionalidades disponíveis na versão 1804 Configuration Manager Technical Preview.
ms.date: 05/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8af43618-ec60-4c3e-a007-12399d1335b9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a796c8cc23ab15e3fbeb09fca6ffa6f1dbd45bc3
ms.sourcegitcommit: fe41e2b3a7d0c735c72252fc817c5b946e25bc3d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/24/2018
---
# <a name="capabilities-in-technical-preview-1804-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1804 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (Technical Preview)*

Este artigo apresenta as funcionalidades que estão disponíveis no Technical Preview para o Configuration Manager, versão 1804. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu local de pré-visualização técnica. 

Reveja o [Technical Preview](/sccm/core/get-started/technical-preview) artigo antes de instalar esta atualização. Esse artigo familiarizes, com os requisitos gerais e limitações para utilizar como uma pré-visualização técnica, ao atualizar entre versões e como os seus comentários.     


<!--  Known Issues Template   -->
## <a name="known-issues-in-this-technical-preview"></a>Problemas conhecidos nesta pré-visualização técnica

### <a name="bkmk_ki-prereqs"></a> Ligação de configuração para transferir as atualizações não está a funcionar
<!--514334-->
Se executar a configuração do suporte de dados, a página inicial inclui uma ligação intitulada **obter as últimas atualizações do Configuration Manager**, que não funciona nesta versão. Esta ligação é para transferir os ficheiros necessários para a configuração.

#### <a name="workaround"></a>Solução
Para transferir os ficheiros necessários para a configuração, execute o Assistente de configuração. Na página de transferências de pré-requisitos, utilize a opção de **transferir ficheiros necessários**. 


### <a name="bkmk_appcathttps"></a> Ponto de serviço web do catálogo de aplicações não pode ser ativado para HTTPS
<!--512637-->
Se o ponto de serviço de web do catálogo de aplicações está ativado para HTTPS:

- Não mostram as aplicações implementadas como disponíveis para os utilizadores no Centro de Software  

- Mostra o erro seguinte no awebsctl.log:  

     `Call to HttpSendRequestSync failed for port 443 with status code 500, text: Internal Server Error`

#### <a name="workaround"></a>Solução
Reconfigure o ponto de serviço de web ao catálogo de aplicações para comunicar utilizando ligações HTTP.  




</br>

**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  


## <a name="configure-a-remote-content-library-for-the-site-server"></a>Configure uma biblioteca de conteúdos remota para o servidor do site  
<!--1357525-->
Para libertar espaço no disco rígido no seu servidor de site primário, altere a localização da respetiva [biblioteca de conteúdos](/sccm/core/plan-design/hierarchy/the-content-library) para outra localização de armazenamento. Pode mover a biblioteca de conteúdos para outra unidade no servidor do site, um servidor separado ou discos com tolerância a falhas numa rede de armazenamento (SAN). Recomendamos uma SAN como fornece armazenamento elástico que aumenta ou diminui ao longo do tempo para satisfazer os requisitos de alteração de conteúdo. 

Nesta biblioteca de conteúdos remota é um pré-requisito de novo para [disponibilidade elevada da função de servidor do site](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability). 

> [!Note]  
> Esta ação só mova a biblioteca de conteúdos no servidor do site. Não afetar a localização da biblioteca de conteúdos nos pontos de distribuição. 

### <a name="prerequisites"></a>Pré-requisitos  
- Conta de computador do servidor do site tem **ler** e **escrever** permissões para o caminho de rede à qual está a mover a biblioteca de conteúdos. Não estão instalados componentes no sistema remoto. 

### <a name="try-it-out"></a>Experimente!
 Experimente concluir as tarefas. Em seguida, enviar [comentários](#bkmk_feedback) nos informar como correu.

1. Na consola do Configuration Manager, mude para o **administração** área de trabalho. Expanda **configuração do Site** e selecione **Sites**. No **resumo** separador na parte inferior do painel de detalhes, repare uma nova coluna para o **biblioteca de conteúdos**.  

2. Clique em **biblioteca de conteúdos de gerir** no Friso.  

3. Selecione **numa partilha de rede** e introduza um caminho de rede válido. Este caminho é a localização a que o site move a biblioteca de conteúdos. Clique em **OK**.  

4. Tenha em atenção o **estado** propriedade na coluna de biblioteca de conteúdos no painel de detalhes. Atualiza a mostrar progresso do site mover a biblioteca de conteúdos. Quando em curso é apresentada a percentagem de conclusão. Se existir um Estado de erro, é apresentado o erro. Erros comuns incluem `access denied` ou `disk full`. Quando concluir apresenta `OK`. Consulte o **distmgr.log** para obter mais detalhes. Para obter mais informações, consulte [registos do servidor de sistema de servidor e o site do Site](/sccm/core/plan-design/hierarchy/log-files#BKMK_SiteSiteServerLog).  

Se precisar de mover a biblioteca de conteúdos de volta para o servidor do site, repita este processo, mas seleciona a opção **Local no servidor de site**.  

> [!Tip]  
> Para mover o conteúdo para outra unidade no servidor do site, utilize o **transferência da biblioteca de conteúdos** ferramenta. Para obter mais informações, consulte [Toolkit do Configuration Manager](#configuration-manager-toolkit).  



## <a name="bkmk_feedback"></a> Submeter comentários sobre a partir da consola do Configuration Manager  
<!--1357542-->

Envie um smile! Agora pode dizer diretamente a equipa do Gestor de configuração sobre as suas experiências. Enviar comentários são fácil a partir da consola do Configuration Manager. Queremos ouvi todos os seus comentários: praise, problemas e sugestões.  

### <a name="try-it-out"></a>Experimente!
 Experimente concluir as tarefas. Em seguida, enviar **comentários** nos informar como correu.  

1. Na consola do Configuration Manager, clique no botão de smile no canto superior direito acima do Friso.  

2. Na lista pendente, selecione uma das opções disponíveis:  

   - **Enviar um smile**: De que realmente gostou algo! Para esta opção, introduza os detalhes dos seus comentários. Em seguida, opcionalmente, inclua uma captura de ecrã e o seu endereço de e-mail.  

   - **Enviar um negativos**: Encontrado um problema na consola ou algo não funcionar conforme esperado. Para esta opção, introduza os detalhes do potencial problema de produto. Em seguida, opcionalmente, inclua uma captura de ecrã, o endereço de e-mail e dados de diagnóstico.  

   - **Enviar uma sugestão**: Ter uma ideia para alterar e melhorar o Configuration Manager. Esta opção abre nosso [UserVoice](https://configurationmanager.uservoice.com) site no seu browser.  

Estes comentários vai diretamente para a equipa de produto da Microsoft para o Configuration Manager. Ao utilizar o Hub de comentários do Windows 10 ainda é suportada, está encorajados a utilizar o mecanismo de comentários na consola.  

As seguintes informações anónimas sempre estão incluídas com os comentários para o contexto:  

 - Versão da consola do Configuration Manager e de idioma  

 - Versão do site do Configuration Manager  

 - ID de suporte, também conhecido como o ID de hierarquia  

 - Versão do SO e de idioma para o sistema no qual está a executar a consola do  

 - A localização exata na consola do que em que clicou o smile  

Estes dados são consistentes com a coleção dos nossos diagnósticos e dados de utilização. Para obter mais informações, consulte [diagnósticos e dados de utilização](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).

### <a name="known-issues"></a>Problemas conhecidos

Se tentar enviar comentários a partir de um dispositivo que não é possível aceder à internet, a aplicação inesperadamente poderá fechar. Para enviar um smile ou negativos, certifique-se de que o dispositivo é capaz de aceder petrol.office.microsoft.com.



## <a name="support-center"></a>Centro de suporte
<!--1357489-->

Utilize o Centro de suporte para resolução de problemas, em tempo real registo de cliente visualizar ou capturar o estado de um computador de cliente do Configuration Manager para análise posterior. Centro de suporte é uma ferramenta única para consolidar o administrador de muitas ferramentas de resolução de problemas. A versão mais recente do Support Center com correções de erros, melhoramentos e uma versão de pré-visualização do nosso novo Visualizador do registo de uma versão de pré-visualização está disponível no technical preview. Localizar o instalador do Support Center no servidor do site no **cd.latest\SMSSETUP\Tools\SupportCenter** pasta.

 > [!Tip]  
 > Documentação legada para a funcionalidade existente no Centro de suporte está disponível no [TechNet](https://technet.microsoft.com/library/dn688621.aspx). Informações relevantes estão no processo de migrar para a biblioteca de docs.microsoft.com.  

### <a name="new-support-center-features"></a>Novas funcionalidades do Support Center  

 - Um novo registo Visualizador, OneTrace. Funciona semelhante a ferramenta CMTrace e inclui melhoramentos, tais como uma vista de separadores e dockable windows.  

 - Uma nova funcionalidade de recoletor de dados recolhe registos de diagnóstico do computador local ou um cliente remoto do Configuration Manager. Fornece diagnóstico em tempo real de inventário (substitui Spy de cliente), a política (substitui política Spy) e a cache do cliente.  



## <a name="configuration-manager-toolkit"></a>Toolkit do Configuration Manager
<!--1357145-->

As ferramentas de servidor e o cliente do Configuration Manager estão agora incluídas com o technical preview. Encontrá-los no **cd.latest\SMSSETUP\Tools** pasta no servidor do site. Não são necessárias mais necessária a instalação.

#### <a name="server-tools"></a>Ferramentas do servidor  

 - **Gestor de tarefas de ponto de distribuição**: Resolve tarefas de distribuição de conteúdo para pontos de distribuição  

 - **Visualizador de avaliação de coleção**: Ver detalhes de avaliação de coleção  

 - **Explorador de biblioteca de conteúdos**: Ver o conteúdo do arquivo de instância única biblioteca de conteúdos  

 - **Transferência de biblioteca de conteúdos**: Transfere conteúdos a biblioteca de unidades  

 - **Ferramenta de propriedade de conteúdo**: Altera a propriedade dos pacotes órfãos. Estes pacotes existem no site sem um servidor de site proprietário.  

 - **Ferramentas de auditoria e de administração baseada em funções**: Ajuda os administradores de configuração de funções de auditoria  

#### <a name="client-tools"></a>Ferramentas de cliente

 - **CMTrace**: Ver registos  

 - **Ferramenta de monitorização da implementação**: Resolver problemas de aplicações, atualizações e implementações de linha de base  

 - **Política Spy**: Atribuições de política do Vista  

 - **Ferramenta de Visualizador de energia**: Ver o estado da funcionalidade de gestão de energia  

 - **Enviar agenda ferramenta**: As agendas de Acionador e avaliações de linhas de base DCM  

> [!Important]  
> [Support Center](#support-center) é recomendada para a maior parte dos casos, de utilização, que inclui a funcionalidade melhorada ou mesma para as ferramentas seguintes:  
>  - Spy de cliente
>  - CMTrace<sup>1</sup> 
>  - Ferramenta de monitorização de implementação
>  - Política Spy
>  - Enviar a ferramenta de agenda
> 
> <sup>1</sup> CMTrace não dependem do .NET ou Windows Presentation Foundation (WPF), pelo que continua a ser utilizada nas imagens de arranque do Windows PE.

### <a name="known-issues"></a>Problemas conhecidos
Algumas ferramentas de cliente e servidor podem sair inesperadamente ao iniciar. Este problema é devido a um ficheiro em falta no suporte de dados. Como solução, copie o **Microsoft.Diagnostics.Tracing.EventSource.dll** ficheiro a partir do diretório AdminConsole\bin em diretórios SMSSETUP\Tools\ClientTools e ServerTools. Este ficheiro tem de ser a mesma versão que o utilizado pela consola do Configuration Manager. Outras versões podem não funcionar. <!--513977-->



## <a name="uninstall-application-on-approval-revocation"></a>Desinstalar a aplicação na revogação de aprovação
<!--1357891-->

Mudou o comportamento ao revogar aprovação para uma aplicação. Agora quando negar o pedido para a aplicação, o cliente desinstala a aplicação de dispositivo do utilizador. 

### <a name="prerequisites"></a>Pré-requisitos
- Ativar a funcionalidade **aprovar pedidos de aplicações para os utilizadores por dispositivo**.

### <a name="try-it-out"></a>Experimente!
 Experimente concluir as tarefas. Em seguida, enviar [comentários](#bkmk_feedback) nos informar como correu.

1. Na consola do Configuration Manager, implemente uma aplicação que requer aprovação de um utilizador. No **definições de implementação** separador da implementação, ative a opção **um administrador tem de aprovar um pedido para esta aplicação no dispositivo**.  

2. No cliente do Configuration Manager no Centro de Software, o utilizador solicitar aprovação para instalar a aplicação.  

3. Na consola do Configuration Manager, aprove o pedido para este utilizador instalar a aplicação no dispositivo. Pedidos de aprovação de aplicações são apresentados no **biblioteca de Software** área de trabalho, em **gestão de aplicações**, no **pedidos de aprovação** nós.  

4. No cliente no Centro de Software, o utilizador instala a aplicação.  

5. Na consola do Configuration Manager, negar o pedido do utilizador para a aplicação no dispositivo.  

### <a name="known-issues"></a>Problemas conhecidos
- Depois do utilizador instala a aplicação no cliente, atualização de política de utilizador. No Centro de Software, mude para o **opções** separador, expanda **manutenção do computador** e clique em **sincronizar política**.<!--480609-->  

- Ponto de serviço web do catálogo de aplicações tem de ser HTTP. Para obter mais informações, consulte [problemas nesta pré-visualização técnica conhecidos](#bkmk_appcathttps).<!--512637-->  



## <a name="exclude-active-directory-containers-from-discovery"></a>Excluir os contentores do Active Directory da deteção
<!--1358143-->
Para reduzir o número de objetos detetados, agora pode excluir contentores específicos de deteção de sistemas do Active Directory. Esta funcionalidade é um resultado da sua [comentários do UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8414520-exclude-virtual-cluster-and-ou-from-discovery).

### <a name="try-it-out"></a>Experimente!
 Experimente concluir as tarefas. Em seguida, enviar [comentários](#bkmk_feedback) nos informar como correu.

1. Na consola do Configuration Manager, vá para o **administração** área de trabalho. Expanda **configuração da hierarquia** e selecione **métodos de deteção**. Selecione **deteção de sistema do Active Directory** e clique em **propriedades** no Friso.  

2. Clique no ícone novo para especificar um novo contentor do Active Directory.   

3. Na caixa de diálogo contentor do Active Directory, procurar ou introduzir o **caminho** na secção de localização para iniciar a deteção.  

4. Na secção Opções de pesquisa, ative a opção para **recursivamente contentores subordinados do Active Directory de pesquisa**. Em seguida, clique em **adicionar** para selecionar subcontainers a serem excluídos esta deteção.  

5. Na caixa de diálogo Selecionar novo contentor, selecione um contentor de subordinados para excluir. Clique em **OK** para fechar a caixa de diálogo Selecionar novo contentor.  

6. Clique em **OK** para fechar a caixa de diálogo contentor do Active Directory.  

7. Na janela de propriedades de deteção de sistema do Active Directory, consulte o caminho do contentor do Active Directory em que começa de deteção. O **recursiva** coluna mostra **Sim**e o novo **tem exclusões** coluna também mostra **Sim**. Clique em **OK** para fechar a janela de propriedades de deteção de sistema do Active Directory.  



## <a name="specify-the-visibility-of-the-application-catalog-website-link-in-software-center"></a>Especifique a visibilidade da ligação de Web site do catálogo de aplicações no Centro de Software
<!--1358214-->

Agora pode controlar se a ligação para **abrir o web site do catálogo de aplicações** aparece no **estado da instalação** nó do Centro de Software.  

> [!Note]  
> Suporte para o catálogo de aplicações, experiência de utilizador do Web site termina com a primeira atualização lançada após 1 de Junho de 2018. Para obter mais informações, consulte [removidas e funcionalidades preteridas](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  

### <a name="try-it-out"></a>Experimente!
 Experimente concluir as tarefas. Em seguida, enviar [comentários](#bkmk_feedback) nos informar como correu.

1. Na consola do Configuration Manager, **administração** área de trabalho, **as definições de cliente** nó, criar uma política de definições de dispositivos de cliente personalizadas.  

2. Selecione o **Centro de Software** grupo.  

3. Para **definições do Centro de Software**, clique em **personalizar**.  

4. Ativar a opção para **ocultar a ligação de web site do catálogo de aplicações no Centro de Software**.   

Para obter mais informações sobre as definições de cliente, consulte [configurar definições de cliente](/sccm/core/clients/deploy/configure-client-settings).




## <a name="filter-automatic-deployment-rules-by-software-update-architecture"></a>Regras de implementação automática pela arquitetura de atualização de software de filtro
 <!--1322266-->
Agora, pode filtrar as regras de implementação automática para excluir arquiteturas como ARM64 e Itanium.

### <a name="try-it-out"></a>Experimente!
Experimente concluir as tarefas. Em seguida, enviar [comentários](#bkmk_feedback) nos informar como correu.

1. Na consola do Configuration Manager, mude para o **biblioteca de Software** área de trabalho. Expanda **atualizações de Software** e selecione **regras de implementação automática**. No Friso, selecione **criar regra de implementação automática**.  

2. Preencha as definições apropriadas para o **geral** separador e **definições de implementação** separador.  

3. No **atualizações de Software** separador, selecione **arquitetura** , em seguida, clique em **itens para localizar** no **os critérios de pesquisa**.  

4. Selecione as arquiteturas que pretende incluir na regra de implementação automática.  

5. Clique em **seguinte** e continue com a criação de regra de implementação automática.  

> [!IMPORTANT]  
> Lembre-se de que existem componentes executados em sistemas de 64 bits (x64) e aplicações de 32 bits (x86). A menos que tem a certeza de que não precisa de x86, ativá-la, bem como de quando escolhe x64.  

### <a name="known-issues"></a>Problemas conhecidos
Depois de adicionar os critérios de arquitetura, as propriedades da regra de implementação automática página mostra **título** nos critérios de pesquisa. A regra de implementação automática ainda funciona como esperado e seleciona as atualizações de software correto. No entanto, não pode incluir os **arquitetura** e **título** critérios neste momento. <!--512634,512632-->



## <a name="improvements-to-os-deployment"></a>Melhorias para implementação do SO
Iremos efetuadas as seguintes melhorias para implementação do SO, algumas das quais foram o resultado dos seus comentários de voz do utilizador.  

 - [Mascarar dados confidenciais armazenados em variáveis de sequência de tarefas](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15282795-secret-task-sequence-variable-value-exposed): No [Set Task Sequence Variable](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable) passo, selecione a opção nova para **não apresentar este valor**. Por exemplo, quando especificar uma palavra-passe.<!--1358330--> Os comportamentos seguintes aplicam-se ao ativar esta opção:
   - O valor da variável não for apresentado na smsts.log.
   - O fornecedor de SMS e consola do Configuration Manager processam este valor igual a outros segredos como palavras-passe.
   - O valor não é incluído ao exportar a sequência de tarefas.
   - O editor de sequência de tarefas não ler este valor quando editar o passo. Volte a escrever o valor inteiro para fazer alterações.

   > [!Important]  
   > As variáveis e os respetivos valores são guardados com a sequência de tarefas como XML e ocultados na base de dados. Quando o cliente solicita uma política de sequência de tarefas do ponto de gestão, são encriptado em trânsito e quando armazenados no cliente. No entanto, todos os valores de variáveis são texto simples no ambiente de sequência de tarefas na memória durante o tempo de execução no cliente. Se a sequência de tarefas inclui um passo para o valor da variável de saída, este resultado é em texto simples. Este comportamento requer uma ação explícita pelo administrador para incluir esse um passo da sequência de tarefas. 


 - [Nome do programa de máscara durante a executar o comando passo da sequência de tarefas](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15282795-secret-task-sequence-variable-value-exposed): Para impedir que os dados potencialmente confidenciais que está a ser apresentada ou com sessão iniciada, defina a variável de sequência de tarefas **OSDDoNotLogCommand** para `TRUE`. Esta variável dissimula o nome do programa no smsts.log durante um [executar linha de comandos](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) passo de sequência de tarefas. <!--1358493-->  



## <a name="improvements-to-the-configuration-manager-console"></a>Melhorias à consola do Configuration Manager
- Informações de utilizador primário agora estão visível quando visualiza os membros de uma coleção em **ativos e compatibilidade**, **coleções de dispositivos**.<!--510252-->  



## <a name="next-steps"></a>Passos seguintes
Para obter informações sobre instalar ou atualizar o ramo de pré-visualização técnica, consulte [pré-visualização técnica do System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
