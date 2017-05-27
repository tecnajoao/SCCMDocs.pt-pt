---
title: "Capacidades na pré-visualização técnica 1511 do Configuration Manager"
description: "Saiba mais sobre as funcionalidades disponíveis na pré-visualização técnica do System Center Configuration Manager, versão 1511."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 69473706-21b3-498b-a67e-670fdc988f0d
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: noindex,nofollow
ms.translationtype: Machine Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: d0bde2c085cc9b330bc772e68081d629ca9e2f11
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="capabilities-in-technical-preview-1511-for-system-center-configuration-manager"></a>Funcionalidades de pré-visualização técnica 1511 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo apresenta as funcionalidades que estão disponíveis na pré-visualização técnica do System Center Configuration Manager, versão 1511. Esta versão é uma linha de base de instalação para a pré-visualização técnica que pode utilizar instalar um novo site de pré-visualização técnica ou atualizar a partir de uma versão anterior da pré-visualização técnica.   Antes de instalar esta versão da pré-visualização técnica, consulte o tópico de introdução, [pré-visualização técnica do System Center Configuration Manager](/sccm/core/get-started/technical-preview), para se familiarizar com geral requisitos e limitações à utilização de uma pré-visualização técnica, como atualizar entre as versões e como fornecer comentários sobre as funcionalidades numa pré-visualização técnica.  

Seguem-se novas funcionalidades que pode experimentar com esta versão.  

##  <a name="BKMK_WUfB"></a>Integração com o Windows Update para empresas no Windows 10  
 O Configuration Manager tem agora a capacidade para diferenciar num computador Windows 10 que está diretamente ligada através do Windows Update para empresas (WUfB) versus aqueles ligado ao WSUS para obter atualizações do Windows 10 e atualizações.  Para computadores ligadas via WUfB, as atualizações e as atualizações podem ser geridas em cadence definido por um utilizador administrativo através das políticas de políticas de grupo ou MDM e estas atualizações/atualizações pode ser instaladas diretamente a partir do WUfB.    
Para computadores ligadas via WUfB, Configuration Manager não será possível reportar o estado de conformidade (incluindo as atualizações do Windows e atualizações de definições). Também do Configuration Manager não será possível implementar o Microsoft Updates ou atualizações de terceiros 3º nestes computadores.  

 **Pré-requisitos para este cenário:**  

-   Versão do Windows 10 ambiente de trabalho Pro ou Windows 10 Enterprise Edition 1511 ou posterior  

-   Computadores para serem geridos através de [Windows Update para empresas](https://technet.microsoft.com/library/mt622730\(v=vs.85\).aspx).  

### <a name="try-it-out"></a>Experimente!  
 Tente concluir a tarefa seguinte e, em seguida, utilize as informações de comentários perto da parte superior deste tópico para nos transmitir como trabalhou:  

1.  Desative o Agente do Windows Update para que não faça análises no WSUS, se tiver sido ativado previamente.   
    A chave de registo **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\useWSUSServer** pode ser definida para indicar se o computador é análise contra WSUS ou o Windows Update.  Quando o valor é 2, não está a analisar no WSUS.  

2.  Tome nota do atributo novo **UseWUServer**, no **Windows Update** nó no Explorador de recursos do Configuration Manager.  

3.  Crie uma coleção com base no atributo **UseWUServer** para todos os computadores ligados através de WUfB para obter atualizações e melhoramentos.  

4.  Crie uma definição de agente de cliente para desativar o fluxo de trabalho de atualização de software e implemente-a na coleção de computadores ligados diretamente ao WUfB.  

5.  O estado de conformidade dos computadores geridos através de WUfB é **Desconhecido** e estes não serão considerados parte da percentagem de conformidade geral.  

##  <a name="BKMK_Office365ProPlus"></a>Gerir o Office 365 ProPlus cliente atualização através do System Center Configuration Manager  
 O Configuration Manager tem agora a capacidade para gerir atualizações de cliente de ambiente de trabalho do Office 365 com o fluxo de trabalho de gestão de atualização de Software do Configuration Manager.    
Quando Microsoft publica uma nova atualização de cliente de ambiente de trabalho do Office 365 para Windows Server atualizações Services (WSUS), o Configuration Manager poderão sincronizar a atualização para o catálogo, se a atualização do Office 365 está configurada para ser parte a sincronização do catálogo.  O servidor do site do Configuration Manager irá transferir as atualizações de cliente do Office 365 e distribuir o pacote para pontos de distribuição do Configuration Manager.  O cliente do Configuration Manager irá, em seguida, informar sobre clientes de ambiente de trabalho do Office 365 onde obter as atualizações e quando iniciar o processo de instalação de atualização.  

**Pré-requisitos para este cenário:**  

### <a name="try-it-out"></a>Experimente!  
 Tente concluir a tarefa seguinte e, em seguida, utilize as informações de comentários perto da parte superior deste tópico para nos transmitir como trabalhou:  

1.  Pode sincronizar as atualizações do Office 365 para o servidor do site do Configuration Manager e visualizá-los a partir da consola do Configuration Manager.  

2.  Pode aprovar e implementar atualizações do Office 365 com êxito.  

3.  Pode transferir e com êxito atualizações do Office 365 para clientes.  

4.  Pode verificar a compatibilidade de atualizações do Office 365 através de monitorização na consola ou relatórios.  

 Para obter passos detalhados, consulte o artigo [atualizações de cliente do Office 365 gerir com o System Center Configuration Manager Technical Preview](https://technet.microsoft.com/library/mt628083.aspx).  

##  <a name="BKMK_AlwasyOn"></a>Suporte para AlwaysOn do SQL Server para as bases de dados de elevada disponibilidade  
 O Configuration Manager suporta agora a utilizar um grupos de Disponibilidade AlwaysOn do SQL Server para alojar a base de dados do site.  Quando instala um novo site, pode direcionar o programa de configuração para utilizar o grupo de disponibilidade em vez de uma instância do SQL Server normal.  

> [!NOTE]  
>  Configuração concluída com êxito e a utilização de grupos de disponibilidade de requer que esteja familiarizado com a configuração de grupos de disponibilidade do SQL Server e depende da documentação e procedimentos fornecidos na biblioteca de documentação do SQL Server.  

O processo de alto nível para configurar e utilizar grupos de disponibilidade inclui:  

1.  Configure o grupo de disponibilidade do SQL Server.  

2.  Instalar um novo site do Configuration Manager e durante a configuração direcionar o site para utilizar o grupo de disponibilidade, especificando os grupos de ponto final.  

**Pré-requisitos para este cenário:**  

-   Necessita de uma versão do SQL Server suportadas pelo Configuration Manager Technical Preview  

-   Tem de criar e configurar o grupo de disponibilidade do SQL Server antes de instalar o Configuration Manager  

-   O grupo de disponibilidade tem de ter uma réplica primária e pode ter até duas réplicas secundárias síncronas  

-   O grupo de disponibilidade tem de ter, pelo menos, um ponto final  

-   Tem de ter uma localização de rede que pode aceder a cada SQL Server no grupo de disponibilidade. Esta localização é utilizada pelo programa de configuração quando configurar o grupo de disponibilidade e pode ser removida após a conclusão da configuração.  

**Problemas conhecidos para esta versão:**  

-   Com êxito, é possível adicionar um novo membro de réplica num grupo de disponibilidade que já está a ser utilizado como uma base de dados do site. Em vez disso, terá de reinstalar o site após é adicionado o novo membro de réplica.  

-   Para este cenário poderá ser necessário instalar o **cliente nativo SQL Server 2012** ([a partir do SQL Server 2012 Feature Pack](http://www.microsoft.com/download/details.aspx?id=29065)) no servidor de ponto de gestão. Isto evita que os erros de ligação do SQL Server (que são registadas no **mp_getauth.log** no servidor de ponto de gestão).  

### <a name="try-it-out"></a>Experimente!  
Experimente concluir as seguintes tarefas e, em seguida, utilize as informações de comentários perto da parte superior deste tópico para nos transmitir como trabalharam:  

-   Posso pode instalar um site primário que utiliza um servidor de base de dados configurado para grupos de Disponibilidade AlwaysOn do SQL Server  

-   Posso foi capaz de ativação pós-falha grupo meu Disponibilidade AlwaysOn do SQL Server para uma nova réplica do grupo e o site primário ainda se encontra operacional  

### <a name="configuring-sql-server-alwayson-for-configuration-manager"></a>Configurar AlwaysOn do SQL Server para o Configuration Manager  
 Utilize os procedimentos seguintes para criar e configurar o grupo de disponibilidade pela primeira vez e, em seguida, instale um novo site do Configuration Manager que utiliza o grupo de disponibilidade.  

#### <a name="to-create-a-sql-server-alwayson-availability-group"></a>Para criar um grupo de Disponibilidade AlwaysOn do SQL Server  
O processo para [criar um grupo de disponibilidade do SQL Server](https://technet.microsoft.com/library/ff878265\(v=sql.120\).aspx) é descrita na biblioteca de documentação do SQL Server.  Ao criar o grupo de disponibilidade, certifique-se de que são cumpridos os seguintes requisitos para utilização com o Configuration Manager:  

-   Um máximo de três membros:  

    -   Uma réplica primária e até duas réplicas secundárias  

    -   Tem de ser síncronas réplicas secundárias.  

        > [!TIP]  
        >  Recomendamos que as réplicas secundárias ser configurado para ser só de leitura. Isto permite-lhe utilizar uma réplica secundária para as funções como relatórios enquanto mantém o desempenho da réplica primária operações do site.  

-   Pelo menos um ponto final. O nome virtual deste ponto final será utilizado quando instala o site do Configuration Manager.  

    > [!TIP]  
    >  Embora o grupo pode conter vários pontos finais, o Configuration Manager só pode efetuar utilizar de um.  

#### <a name="to-install-a-configuration-manager-site-that-uses-the-availability-group"></a>Para instalar um site do Configuration Manager que utiliza o grupo de disponibilidade  
Para instalar um site que utiliza um grupo de disponibilidade do SQL Server:  

1.  Substitua o seguinte quando lhe for pedido pelo programa de configuração do Configuration Manager:  

    -   **Nome do SQL Server**: Introduza o nome virtual para o ponto final que configurou ao criar o grupo de disponibilidade. O nome virtual deve ser um nome DNS completo, como  **&lt;endpointServer\>. fabrikam.com**.  

    -   **Instância**:  Este valor deve permanecer em branco. Não existe nenhuma instância nesta configuração.  

    -   **Base de dados**: Introduza o nome da base de dados que criou na réplica primária do grupo de disponibilidade.  

2.  Em seguida, tem de fornecer uma localização de rede que pode aceder a cada SQL Server no grupo:  

    -   A conta de computador e a conta de serviço a partir de cada SQL Server necessitam de acesso de controlo total para esta localização.  

    -   Esta localização só é utilizada durante a configuração e pode ser as ou eliminada após a conclusão da configuração e a instalação do site.  

3.  Depois de fornecer estas informações, conclua a configuração com o seu processo normal e configurações.  

##  <a name="BKMK_ClusterServerUpdates"></a>Serviço de um cluster de servidores  
Pode agora criar uma coleção que contenha servidores num cluster e, em seguida, configure as definições de cluster para utilizar ao implementar atualizações para o cluster. Pode controlar a percentagem de servidores que estão online em qualquer momento, bem como para configurar a implementação pré e pós-implementação de scripts do PowerShell para executar as ações personalizadas.  

**Problemas conhecidos para esta versão:**  

-   Relatórios não está disponível para verificar o estado de implementação de atualizações de software para servidores de cluster.  

-   A opção de sequência de manutenção no **definições de Cluster** página está desativado e não está disponível nesta versão.  

### <a name="try-it-out"></a>Experimente!  
Tente concluir a tarefa seguinte e, em seguida, utilize as informações de comentários perto da parte superior deste tópico para nos transmitir como trabalhou:  

-   Posso pode criar uma coleção que representa um cluster de servidores. Para este teste, pode configurar as regras de associação de recolher com 2 máquinas nesta coleção.  

-   Posso pode especificar que apenas 50% dos servidores no cluster pode ser offline em qualquer ponto no cluster de manutenção. Utilize os scripts de exemplo no procedimento para especificar os scripts de pré-implementação e pós-implementação.  

-   Implemente uma atualização a esta coleção. Rever os ficheiros start.txt e end.txt em C:\temp e verifique se as horas de início e fim para a implementação de servidores no cluster. Reveja o ficheiro de UpdatesDeployment.log para obter mais informações.  

#### <a name="to-create-a-collection-for-a-server-cluster"></a>Para criar uma coleção para um cluster de servidores  

1.  [Criar uma coleção de dispositivos](https://technet.microsoft.com/library/gg712295.aspx) que contenha os servidores no cluster.  

2.  No **ativos e compatibilidade** área de trabalho, clique em **coleções de dispositivos**, faça duplo clique na coleção que contém os servidores no cluster e, em seguida, clique em **propriedades**.  

3.  No **geral** separador, selecione **todos os dispositivos fazem parte do mesmo cluster de servidores**e, em seguida, clique em **definições**.  

4.  No **definições de Cluster** página, selecione a percentagem de servidores que pode ser colocado offline ao mesmo tempo para que as atualizações de software instaladas. Um servidor de cluster poderá ficar offline cada vez, independentemente da percentagem que indicar. O Configuration Manager irá arredondar por defeito quando selecionar o número de servidores para servir de uma só vez. Por exemplo, se escolher 51% e existem 4 servidores no cluster, 2 servidores serão colocadas offline ao mesmo tempo.  

5.  Especifique se pretende utilizar um script de pré-implementação (drenagem de nó) ou scripts pós-implementação (currículo de nó).  

    > [!TIP]  
    >  Seguem-se exemplos que pode utilizar testes de pré-implementação e scripts pós-implementação que escreverem a hora atual para um ficheiro de texto:  
    >   
    >  **Pré-implementação**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\start.txt`  
    >   
    >  **Pós-implementação**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\end.txt`  

#### <a name="to-deploy-software-updates-to-the-server-cluster"></a>Para implementar atualizações de software para o cluster de servidor  

1.  [Implementar atualizações de software](https://technet.microsoft.com/library/gg712304.aspx) na coleção de cluster de servidor.  

2.  [Monitorizar a implementação de atualização de software](https://technet.microsoft.com/library/gg712304.aspx).  

