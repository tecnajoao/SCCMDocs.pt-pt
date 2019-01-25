---
title: Technical Preview 1804
titleSuffix: Configuration Manager
description: Saiba mais sobre novas funcionalidades disponíveis na versão do Configuration Manager Technical Preview 1804.
ms.date: 05/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8af43618-ec60-4c3e-a007-12399d1335b9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 80f16244c10899ed264b83f6c7a9a050fba7a224
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/24/2019
ms.locfileid: "54898312"
---
# <a name="capabilities-in-technical-preview-1804-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1804 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo apresenta os recursos que estão disponíveis no Technical Preview no Configuration Manager, versão 1804. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu site de pré-visualização técnica. 

Reveja os [Technical Preview](/sccm/core/get-started/technical-preview) artigo antes de instalar esta atualização. Nesse artigo familiariza com os requisitos gerais e limitações para a utilização de uma technical preview, como ao atualizar entre versões e como fornecer comentários.     


<!--  Known Issues Template   -->
## <a name="known-issues-in-this-technical-preview"></a>Problemas conhecidos neste Technical Preview

### <a name="bkmk_ki-prereqs"></a> Ligação de configuração para transferir as atualizações não está a funcionar
<!--514334--> Se executar a configuração do suporte de dados, a página inicial inclui uma ligação intitulada **obter as últimas atualizações do Configuration Manager**, que não funciona nesta versão. Esta ligação é para transferir os ficheiros necessários para a configuração.

#### <a name="workaround"></a>Solução
Para transferir os ficheiros necessários para a configuração, execute o Assistente de configuração. Na página de Downloads de pré-requisito, utilize a opção para **transferir ficheiros necessários**. 


### <a name="bkmk_appcathttps"></a> Ponto de serviço web do catálogo de aplicações não pode ser ativado para HTTPS
<!--512637--> Se o ponto de serviço de web do catálogo de aplicações é ativado para HTTPS:

- Aplicações implementadas como disponíveis para os utilizadores não mostram no Centro de Software  

- Mostra o erro seguinte no awebsctl.log:  

     `Call to HttpSendRequestSync failed for port 443 with status code 500, text: Internal Server Error`

#### <a name="workaround"></a>Solução
Reconfigure o ponto de serviço de web ao catálogo de aplicações para comunicar através de ligações HTTP.  




</br>

**Seguem-se os novos recursos, que pode experimentar com esta versão.**  


## <a name="configure-a-remote-content-library-for-the-site-server"></a>Configurar uma biblioteca de conteúdos remota para o servidor do site  
<!--1357525--> Para libertar espaço no disco rígido no seu servidor de site primário, alteração da localização da sua [biblioteca de conteúdos](/sccm/core/plan-design/hierarchy/the-content-library) para outra localização de armazenamento. Pode mover a biblioteca de conteúdos para outra unidade no servidor do site, um servidor separado ou discos tolerante a falhas na rede de armazenamento (SAN). Recomendamos uma SAN, pois fornece armazenamento elástico que aumenta ou diminui ao longo do tempo para atender às suas necessidades em constante mudança conteúdas. 

Nesta biblioteca de conteúdos remota é um pré-requisito de novo para [disponibilidade elevada da função de servidor do site](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability). 

> [!Note]  
> Esta ação só mova a biblioteca de conteúdos no servidor do site. Não afetar a localização da biblioteca de conteúdos em pontos de distribuição. 

### <a name="prerequisites"></a>Pré-requisitos  
- A conta de computador do servidor de site precisa **ler** e **escrever** permissões para o caminho de rede à qual está a mover a biblioteca de conteúdos. Não estão instalados componentes no sistema remoto. 

### <a name="try-it-out"></a>Experimente!
 Experimente concluir as tarefas. Em seguida, envie [comentários](#bkmk_feedback) nos informar como correu.

1. Na consola do Configuration Manager, mude para o **administração** área de trabalho. Expanda **configuração do Site** e selecione **Sites**. Sobre o **resumo** separador na parte inferior do painel de detalhes, observe que uma nova coluna para o **biblioteca de conteúdos**.  

2. Clique em **biblioteca de conteúdos de gerir** da faixa de opções.  

3. Selecione **numa partilha de rede** e introduza um caminho de rede válido. Este caminho é a localização a que o site move a biblioteca de conteúdos. Clique em **OK**.  

4. Tenha em atenção a **estado** propriedade na coluna de biblioteca de conteúdos no painel de detalhes. Atualiza para mostrar o progresso do site em mover a biblioteca de conteúdos. Quando está em curso é apresentada a percentagem concluída. Se houver um Estado de erro, apresenta o erro. Erros comuns incluem `access denied` ou `disk full`. Quando terminar apresenta `OK`. Consulte a **distmgr** para obter detalhes. Para obter mais informações, consulte [registos do servidor de sistema de site e o servidor do Site](/sccm/core/plan-design/hierarchy/log-files#BKMK_SiteSiteServerLog).  

Se precisar de mover a biblioteca de conteúdos de volta ao servidor do site, repita este processo, mas selecione a opção **Local no servidor de site**.  

> [!Tip]  
> Para mover o conteúdo para outra unidade no servidor do site, utilize o **transferência da biblioteca de conteúdos** ferramenta. Para obter mais informações, consulte [Configuration Manager Toolkit](#configuration-manager-toolkit).  



## <a name="bkmk_feedback"></a> Enviar comentários a partir da consola do Configuration Manager  
<!--1357542-->

Envie um sorriso! Pode agora diretamente informar a equipa do Configuration Manager sobre as suas experiências. Envio de comentários é fácil partir da consola do Configuration Manager. Queremos ouvir todos os seus comentários: elogios, os problemas e sugestões.  

### <a name="try-it-out"></a>Experimente!
 Experimente concluir as tarefas. Em seguida, envie **comentários** nos informar como correu.  

1. Na consola do Configuration Manager, clique no botão de sorriso no canto superior direito acima do Friso.  

2. Na lista pendente, selecione uma das opções disponíveis:  

   - **Enviar um sorriso**: Realmente gostou de algo! Para esta opção, introduza os detalhes dos seus comentários. Em seguida, opcionalmente, inclua uma captura de ecrã e o seu endereço de e-mail.  

   - **Enviar comentários negativos**: Encontrou um problema na consola ou algo não funciona conforme esperado. Para esta opção, introduza os detalhes do potencial problema de produto. Em seguida, opcionalmente, inclua uma captura de ecrã, seu endereço de e-mail e dados de diagnóstico.  

   - **Enviar uma sugestão**: Tem uma ideia para alterar e melhorar o Configuration Manager. Esta opção abre-se nosso [UserVoice](https://configurationmanager.uservoice.com) site no seu browser.  

Estes comentários vai diretamente para a equipe de produto da Microsoft para o Configuration Manager. Embora ainda seja suportada através do Hub de comentários do Windows 10, é recomendado que utilize o mecanismo de comentários na consola.  

As seguintes informações anónimas sempre estão incluídas com os comentários para o contexto:  

 - Versão da consola do Configuration Manager e de idioma  

 - Versão do site do Configuration Manager  

 - ID de suporte, também conhecido como o ID de hierarquia  

 - Versão do SO e de idioma para o sistema no qual o console é executado  

 - A localização exata na consola do qual clicou no sorriso  

Estes dados são consistentes com a coleção de nossos diagnósticos e dados de utilização. Para obter mais informações, consulte [diagnósticos e dados de utilização](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).

### <a name="known-issues"></a>Problemas conhecidos

Se está tentando enviar comentários a partir de um dispositivo que não é possível aceder à internet, o aplicativo inesperadamente poderá fechar. Para enviar um sorriso ou comentário negativo, certificar-se de que o dispositivo é capaz de acessar petrol.office.microsoft.com.



## <a name="support-center"></a>Centro de Suporte
<!--1357489-->

Utilize o Centro de suporte para resolução de problemas e em tempo real registo de cliente visualizando ou capturar o estado de um computador de cliente do Configuration Manager para análise posterior. Centro de suporte é uma ferramenta única para consolidar administrador muitas ferramentas de resolução de problemas. Uma pré-visualização da versão mais recente do Centro de suporte com correções de erros, melhorias e uma pré-visualização do nosso novo Visualizador de log está disponível no technical preview. Localizar o instalador do Support Center no servidor do site no **cd.latest\SMSSETUP\Tools\SupportCenter** pasta.

 > [!Tip]  
 > Documentação herdada para a funcionalidade existente no Centro de suporte está disponível no [TechNet](https://technet.microsoft.com/library/dn688621.aspx). As informações relevantes estão em curso para migrar para a biblioteca do docs.microsoft.com.  

### <a name="new-support-center-features"></a>Novos recursos do Centro de suporte  

 - Um novo log viewer, OneTrace. Ele funciona de maneira semelhante, a CMTrace e inclui aprimoramentos como uma exibição com guias e windows encaixáveis parecidos.  

 - Um novo recurso de recoletor de dados recolhe registos de diagnóstico a partir do computador local ou um cliente remoto do Configuration Manager. Ele fornece diagnóstico em tempo real de inventário (substitui espião do cliente), a política (substitui espião de política) e a cache do cliente.  



## <a name="configuration-manager-toolkit"></a>Kit de ferramentas do Configuration Manager
<!--1357145-->

As ferramentas de servidor e cliente do Configuration Manager estão agora incluídos com o technical preview. Encontrá-los no **cd.latest\SMSSETUP\Tools** pasta no servidor do site. Não são necessárias mais necessária a instalação.

#### <a name="server-tools"></a>Ferramentas do servidor  

 - **Gestor de trabalho de DP**: Soluciona problemas em tarefas de distribuição de conteúdo para pontos de distribuição  

 - **Visualizador de avaliação de coleção**: Ver detalhes de avaliação de coleção  

 - **Explorador de biblioteca de conteúdos**: Ver o conteúdo do arquivo de instância única biblioteca de conteúdos  

 - **Biblioteca de transferência de conteúdo**: Transfere conteúdos a biblioteca de unidades  

 - **Ferramenta de propriedade de conteúdo**: Propriedade de alterações de pacotes órfãos. Esses pacotes existem no site sem um servidor de site proprietário.  

 - **Administração baseada em funções e a ferramenta de auditoria**: Ajuda os administradores de configuração de funções de auditoria  

#### <a name="client-tools"></a>Ferramentas de cliente

 - **CMTrace**: Ver registos  

 - **Ferramenta de monitoramento de implementação**: Resolver problemas de aplicações, atualizações e implementações de linha de base  

 - **Política espião**: Atribuições de política do Vista  

 - **Ferramenta de visualização de energia**: Ver o estado da funcionalidade de gestão de energia  

 - **Enviar a ferramenta de agendamento**: Agendas de Acionador e avaliações de linhas de base do DCM  

> [!Important]  
> [Centro de suporte](#support-center) é recomendado para a maioria usa casos, pois inclui a funcionalidade melhorada ou mesmo para as seguintes ferramentas:  
>  - Espião do Cliente
>  - CMTrace<sup>1</sup> 
>  - Ferramenta de Monitorização da Implementação
>  - Espião de Política
>  - Ferramenta de Envio de Agendamento
> 
> <sup>1</sup> CMTrace não depende do .NET ou o Windows Presentation Foundation (WPF), portanto, ainda é utilizada nas imagens de arranque do Windows PE.

### <a name="known-issues"></a>Problemas conhecidos
Algumas ferramentas de cliente e servidor de podem sair inesperadamente ao iniciar. Este problema é devido a um ficheiro em falta no suporte de dados. Como solução, copie os **Microsoft.Diagnostics.Tracing.EventSource.dll** ficheiro a partir do diretório de AdminConsole\bin nos diretórios SMSSETUP\Tools\ClientTools e ServerTools. Este ficheiro tem de ser a mesma versão que utilizados pela consola do Configuration Manager. Outras versões podem não funcionar. <!--513977-->



## <a name="uninstall-application-on-approval-revocation"></a>Desinstalar a aplicação mediante a revogação de aprovação
<!--1357891-->

Esse comportamento foi alterado quando revogar a aprovação de um aplicativo. Agora quando negar o pedido para a aplicação, o cliente desinstala a aplicação do dispositivo do utilizador. 

### <a name="prerequisites"></a>Pré-requisitos
- Ativar a funcionalidade **aprovar pedidos de aplicações para utilizadores por dispositivo**.

### <a name="try-it-out"></a>Experimente!
 Experimente concluir as tarefas. Em seguida, envie [comentários](#bkmk_feedback) nos informar como correu.

1. Na consola do Configuration Manager, implemente uma aplicação que necessite de aprovação para um utilizador. Sobre o **definições de implementação** separador da implementação, ative a opção **um administrador tem de aprovar um pedido para esta aplicação no dispositivo**.  

2. No cliente do Configuration Manager no Centro de Software, o utilizador solicita a aprovação para instalar a aplicação.  

3. Na consola do Configuration Manager, aprove o pedido para este utilizador instalar a aplicação no dispositivo. Pedidos de aprovação de aplicação são apresentados no **biblioteca de Software** área de trabalho, em **gestão de aplicações**, no **pedidos de aprovação** nó.  

4. No cliente no Centro de Software, o utilizador instala a aplicação.  

5. Na consola do Configuration Manager, negar o pedido do utilizador para a aplicação no dispositivo.  

### <a name="known-issues"></a>Problemas conhecidos
- Depois do utilizador instala a aplicação no cliente, atualize a política de utilizador. No Centro de Software, mude para o **opções** separador, expanda **manutenção do computador** e clique em **sincronizar política**.<!--480609-->  

- Ponto de serviço web do catálogo de aplicações tem de ser HTTP. Para obter mais informações, consulte [problemas conhecidos desta pré-visualização técnica](#bkmk_appcathttps).<!--512637-->  



## <a name="exclude-active-directory-containers-from-discovery"></a>Excluir contentores do Active Directory da deteção
<!--1358143--> Para reduzir o número de objetos detetados, agora pode excluir contentores específicos de deteção de sistemas do Active Directory. Esta funcionalidade é um resultado da sua [comentários do UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8414520-exclude-virtual-cluster-and-ou-from-discovery).

### <a name="try-it-out"></a>Experimente!
 Experimente concluir as tarefas. Em seguida, envie [comentários](#bkmk_feedback) nos informar como correu.

1. Na consola do Configuration Manager, vá para o **administração** área de trabalho. Expanda **configuração da hierarquia** e selecione **métodos de deteção**. Selecione **deteção de sistema do Active Directory** e clique em **propriedades** na faixa de opções.  

2. Clique no ícone novo para especificar um novo contentor do Active Directory.   

3. Na caixa de diálogo de contentor do Active Directory, navegue para ou introduza o **caminho** na secção de localização para iniciar a deteção.  

4. Na secção de opções de pesquisa, ative a opção para **recursivamente contentores subordinados do Active Directory de pesquisa**. Em seguida, clique em **adicionar** para selecionar os subcontentores a serem excluídos desta deteção.  

5. Na caixa de diálogo Selecionar novo contentor, selecione um contentor de subordinados para excluir. Clique em **OK** para fechar a caixa de diálogo Selecionar novo contentor.  

6. Clique em **OK** para fechar a caixa de diálogo de contentor do Active Directory.  

7. Na janela de propriedades de deteção de sistema do Active Directory, consulte o caminho do contentor do Active Directory em que é iniciada de deteção. O **recursiva** coluna mostra **Sim**e o novo **tem exclusões** coluna também mostra **Sim**. Clique em **OK** para fechar a janela de propriedades de deteção de sistema do Active Directory.  



## <a name="specify-the-visibility-of-the-application-catalog-website-link-in-software-center"></a>Especifique a visibilidade da ligação de site do catálogo de aplicações no Centro de Software
<!--1358214-->

Agora pode controlar se a ligação para **abrir o web site do catálogo de aplicações** é apresentado na **estado da instalação** nó do Centro de Software.  

> [!Note]  
> Suporte para o catálogo de aplicações termina a experiência do usuário de Web site com a primeira atualização lançada após 1 de Junho de 2018. Para obter mais informações, consulte [funcionalidades removidas e preteridas](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  

### <a name="try-it-out"></a>Experimente!
 Experimente concluir as tarefas. Em seguida, envie [comentários](#bkmk_feedback) nos informar como correu.

1. Na consola do Configuration Manager, **Administration** área de trabalho **definições de cliente** nó, criar uma política de definições personalizadas de cliente.  

2. Selecione o **Centro de Software** grupo.  

3. Para **definições do Centro de Software**, clique em **personalizar**.  

4. Ativar a opção para **ocultar a ligação de site da web do catálogo de aplicações no Centro de Software**.   

Para obter mais informações sobre as definições de cliente, consulte [configurar definições de cliente](/sccm/core/clients/deploy/configure-client-settings).




## <a name="filter-automatic-deployment-rules-by-software-update-architecture"></a>Filtrar regras de implementação automática pela arquitetura de atualização de software
 <!--1322266--> Agora pode filtrar regras de implementação automática para excluri arquiteturas como Itanium e ARM64.

### <a name="try-it-out"></a>Experimente!
Experimente concluir as tarefas. Em seguida, envie [comentários](#bkmk_feedback) nos informar como correu.

1. Na consola do Configuration Manager, mude para o **biblioteca de Software** área de trabalho. Expanda **atualizações de Software** e selecione **regras de implementação automática**. No Friso, selecione **criar regra de implementação automática**.  

2. Preencha as configurações apropriadas para o **gerais** separador e o **definições de implementação** separador.  

3. Na **atualizações de Software** separador, selecione **arquitetura** , em seguida, clique em **itens para localizar** no **critérios de pesquisa**.  

4. Selecione as arquiteturas de que pretende incluir na regra de implementação automática.  

5. Clique em **seguinte** e continue com a criação de regra de implementação automática.  

> [!IMPORTANT]  
> Lembre-se de que existem aplicativos de 32 bits (x86) e componentes em execução em sistemas de 64 bits (x64). A menos que tem a certeza de que não precisa x86, ativá-la também de ao escolher x64.  

### <a name="known-issues"></a>Problemas conhecidos
Depois de adicionar os critérios de arquitetura, as propriedades da regra de implementação automática página mostra **Title** nos critérios de pesquisa. A regra de implementação automática ainda funciona como esperado e seleciona as atualizações de software correto. No entanto, não pode incluir ambos **arquitetura** e **Title** critérios neste momento. <!--512634,512632-->



## <a name="improvements-to-os-deployment"></a>Melhorias para implementação do SO
Fizemos as seguintes melhorias à implantação de sistema operacional, alguns dos quais foram o resultado dos seus comentários de voz do utilizador.  

 - [Mascarar dados confidenciais armazenados em variáveis de sequência de tarefas](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15282795-secret-task-sequence-variable-value-exposed): Na [Set Task Sequence Variable](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable) passo, selecione a opção nova para **não apresentar este valor**. Por exemplo, quando especificar uma palavra-passe.<!--1358330--> Os comportamentos seguintes aplicam-se quando ativa esta opção:
   - O valor da variável não é apresentado no smsts.
   - A consola do Configuration Manager e o fornecedor de SMS lidar com esse valor igual a outros segredos como palavras-passe.
   - O valor não está incluído ao exportar a sequência de tarefas.
   - O editor de sequência de tarefas não ler este valor ao editar o passo. Volte a escrever o valor inteiro para fazer alterações.

   > [!Important]  
   > As variáveis e os respetivos valores são guardadas com a sequência de tarefas como XML e oculto na base de dados. Quando o cliente solicita uma política de sequência de tarefas do ponto de gestão, é encriptada em trânsito e quando armazenada no cliente. No entanto, todos os valores das variáveis são texto simples no ambiente de sequência de tarefas na memória durante o tempo de execução no cliente. Se a sequência de tarefas inclui um passo para o valor da variável de saída, esta saída é em texto simples. Esse comportamento requer uma ação explícita pelo administrador para incluir esse um passo na sequência de tarefas. 


 - [Nome do programa de máscara durante a executar o comando passo de sequência de tarefas](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15282795-secret-task-sequence-variable-value-exposed): Para impedir que os dados potencialmente confidenciais sejam apresentadas ou com sessão iniciada, defina a variável de sequência de tarefas **OSDDoNotLogCommand** para `TRUE`. Esta variável dissimula o nome do programa no smsts durante uma [executar linha de comandos](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) passo de sequência de tarefas. <!--1358493-->  



## <a name="improvements-to-the-configuration-manager-console"></a>Melhorias à consola do Configuration Manager
- Informações de utilizador primário agora estão visíveis quando visualizar os membros de uma coleção em **ativos e compatibilidade**, **coleções de dispositivos**.<!--510252-->  



## <a name="next-steps"></a>Passos seguintes
Para obter informações sobre a instalação ou a atualizar o ramo de pré-visualização técnica, veja [Technical Preview do System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
