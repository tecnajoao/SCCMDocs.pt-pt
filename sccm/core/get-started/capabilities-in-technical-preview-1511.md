---
title: Funcionalidades no Technical Preview 1511
titleSuffix: Configuration Manager
description: Saiba mais sobre as funcionalidades disponíveis no Technical Preview do System Center Configuration Manager, versão 1511.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 69473706-21b3-498b-a67e-670fdc988f0d
author: aczechowski
robots: noindex,nofollow
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: d58a780ecf6232bd8ef6e7f0d9851ead34486177
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53414757"
---
# <a name="capabilities-in-technical-preview-1511-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1511 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (pré-visualização técnica)*

Este artigo apresenta os recursos que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1511. Esta versão é uma linha de base de instalação do technical preview que pode utilizar instalar um novo site de pré-visualização técnica ou para atualizar a partir de uma versão anterior do technical preview.   Antes de instalar esta versão do technical preview, consulte o tópico introdutório, [Technical Preview do System Center Configuration Manager](/sccm/core/get-started/technical-preview), para se familiarizar com os requisitos gerais e limitações para a utilização de um Technical preview, como atualizar entre versões e como fornecer comentários sobre os recursos de uma technical preview.  

Seguem-se os novos recursos, que pode experimentar com esta versão.  

##  <a name="BKMK_WUfB"></a> Integração com o Windows Update for Business no Windows 10  
 O Configuration Manager tem agora capacidade para diferenciar computadores Windows 10 que estejam ligados diretamente através do Windows Update for Business (WUfB) versus que estão ligados ao WSUS para obter atualizações do Windows 10.  Para computadores ligados através de WUfB, as atualizações e melhoramentos podem ser geridos de cadência definida por um utilizador administrativo através das políticas de políticas de grupo ou a MDM e estas atualizações/melhoramentos podem ser instalados diretamente a partir do WUfB.    
Para computadores ligados através de WUfB, Configuration Manager não será capaz de gerar relatórios sobre o estado de conformidade (incluindo atualizações do Windows ou atualizações de definições). Também o Configuration Manager não será capaz de implantar o Microsoft Updates ou 3º atualizações de terceiros nestes computadores.  

 **Pré-requisitos para este cenário:**  

-   Windows 10 Desktop Pro ou Windows 10 Enterprise Edition, versão 1511 ou posterior  

-   Computadores que serão geridos através de [Windows Update para empresas](https://technet.microsoft.com/library/mt622730\(v=vs.85\).aspx).  

### <a name="try-it-out"></a>Experimente!  
 Experimente concluir a tarefa seguinte e, em seguida, utilize as informações de feedback perto da parte superior deste tópico para nos informar como correu:  

1.  Desative o Agente do Windows Update para que não faça análises no WSUS, se tiver sido ativado previamente.   
    A chave de registo **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\useWSUSServer** pode ser definida para indicar se o computador está a analisar no WSUS ou no Windows Update.  Quando o valor é 2, não está a analisar no WSUS.  

2.  Tome nota do novo atributo **UseWUServer**, sob o **Windows Update** nó no Explorador de recursos do Configuration Manager.  

3.  Crie uma coleção com base no atributo **UseWUServer** para todos os computadores ligados através de WUfB para obter atualizações e melhoramentos.  

4.  Crie uma definição de agente de cliente para desativar o fluxo de trabalho de atualização de software e implemente-a na coleção de computadores ligados diretamente ao WUfB.  

5.  O estado de conformidade dos computadores geridos através de WUfB é **Desconhecido** e estes não serão considerados parte da percentagem de conformidade geral.  

##  <a name="BKMK_Office365ProPlus"></a> Gerir o Office 365 ProPlus Client Update através do System Center Configuration Manager  
 O Configuration Manager tem agora capacidade para gerir atualizações de cliente de desktop do Office 365 com o fluxo de trabalho de gestão de atualizações de Software do Configuration Manager.    
Quando a Microsoft publica uma nova atualização de cliente de desktop do Office 365 para Windows Server atualiza Services (WSUS), o Configuration Manager poderão sincronizar a atualização com o respetivo catálogo se a atualização do Office 365 estiver configurada para ser parte da sincronização do catálogo.  Servidor de site do Configuration Manager irá transferir as atualizações de cliente do Office 365 e distribuir o pacote para pontos de distribuição do Configuration Manager.  O cliente do Configuration Manager irá, em seguida, informar os clientes de ambiente de trabalho do Office 365 onde pode obter as atualizações e quando iniciar o processo de instalação de atualização.  

**Pré-requisitos para este cenário:**  

### <a name="try-it-out"></a>Experimente!  
 Experimente concluir a tarefa seguinte e, em seguida, utilize as informações de feedback perto da parte superior deste tópico para nos informar como correu:  

1. Pode sincronizar as atualizações do Office 365 para o servidor de site do Configuration Manager e visualizá-los a partir da consola do Configuration Manager.  

2. Pode aprovar e implementar com êxito as atualizações do Office 365.  

3. Pode baixar e do Office 365 atualizado com êxito para os clientes.  

4. Pode verificar a compatibilidade de atualizações do Office 365, utilizando a monitorização na consola ou relatórios.  

   Para obter passos detalhados, consulte [atualizações de cliente de gerir o Office 365 com o System Center Configuration Manager Technical Preview](https://technet.microsoft.com/library/mt628083.aspx).  

##  <a name="BKMK_AlwasyOn"></a> Suporte para o SQL Server AlwaysOn para bases de dados de elevada disponibilidade  
 Do Configuration Manager agora suporta a utilização de um grupo de Disponibilidade AlwaysOn do SQL Server para alojar a base de dados do site.  Quando instala um novo site, pode direcionar a configuração para utilizar o grupo de disponibilidade em vez de uma instância normal do SQL Server.  

> [!NOTE]  
>  Configuração concluída com êxito e a utilização de grupos de disponibilidade exige que esteja familiarizado com a configuração de grupos de disponibilidade do SQL Server e depende de documentação e procedimentos fornecidos na biblioteca de documentação do SQL Server.  

O processo de alto nível para configurar e utilizar grupos de disponibilidade inclui:  

1.  Configure o grupo de disponibilidade no SQL Server.  

2.  Instalar um novo site do Configuration Manager e durante a configuração, reencaminhar o site para utilizar o grupo de disponibilidade ao especificar o ponto final dos grupos.  

**Pré-requisitos para este cenário:**  

-   Requer uma versão do SQL Server suportada pelo Configuration Manager Technical Preview  

-   Tem de criar e configurar o grupo de disponibilidade do SQL Server antes de instalar o Configuration Manager  

-   O grupo de disponibilidade tem de ter uma réplica primária e pode ter até duas réplicas secundárias síncronas  

-   O grupo de disponibilidade tem de ter, pelo menos, um ponto final  

-   Tem de ter uma localização de rede que cada SQL Server no grupo de disponibilidade possa aceder. Esta localização é utilizada pela configuração ao configurar o grupo de disponibilidade e pode ser removida depois de concluída a configuração.  

**Problemas conhecidos nesta versão:**  

-   Não é possível adicionar com êxito um novo membro de réplica para um grupo de disponibilidade que já está a ser utilizada como uma base de dados do site. Em vez disso, terá de reinstalar o site depois do novo membro de réplica é adicionado.  

-   Para este cenário poderá ter de instalar o **cliente nativo do SQL Server 2012** ([do SQL Server 2012 Feature Pack](http://www.microsoft.com/download/details.aspx?id=29065)) no servidor de ponto de gestão. Isto impede que os erros de ligação de SQL (que têm sessão iniciado a **mp_getauth** no servidor de ponto de gestão).  

### <a name="try-it-out"></a>Experimente!  
Experimente concluir as seguintes tarefas e, em seguida, utilize as informações de feedback perto da parte superior deste tópico para nos informar como correu:  

-   Posso instalar um site primário que utiliza um servidor de base de dados configurado para grupos de disponibilidade do AlwaysOn de SQL  

-   Eu consegui o grupo de disponibilidade do AlwaysOn do SQL para uma nova réplica no grupo de ativação pós-falha e o site primário ainda está operacional  

### <a name="configuring-sql-server-alwayson-for-configuration-manager"></a>Configurar o AlwaysOn do SQL Server para o Configuration Manager  
 Utilize os seguintes procedimentos para primeiro criar e configurar o grupo de disponibilidade e, em seguida, instale um novo site do Configuration Manager que utiliza o grupo de disponibilidade.  

#### <a name="to-create-a-sql-server-alwayson-availability-group"></a>Para criar um grupo de Disponibilidade AlwaysOn do SQL Server  
O processo para [criar um grupo de disponibilidade do SQL Server](https://technet.microsoft.com/library/ff878265\(v=sql.120\).aspx) está documentado na biblioteca de documentação do SQL Server.  Ao criar o grupo de disponibilidade, certifique-se de que são cumpridos os seguintes requisitos para utilização com o Configuration Manager:  

-   Um máximo de três membros:  

    -   Uma réplica primária e até duas réplicas secundárias  

    -   As réplicas secundárias têm de ser síncronas.  

        > [!TIP]  
        >  Recomendamos que as réplicas secundárias sejam configuradas como só de leitura. Isto permite-lhe utilizar uma réplica secundária para funções como registo enquanto mantém o desempenho da réplica primária de operações do site.  

-   Pelo menos um ponto final. O nome virtual deste ponto final será utilizado quando instalar o site do Configuration Manager.  

    > [!TIP]  
    >  Apesar do grupo pode conter vários pontos de extremidade, o Configuration Manager pode fazer apenas utilizar um.  

#### <a name="to-install-a-configuration-manager-site-that-uses-the-availability-group"></a>Para instalar um site do Configuration Manager que utiliza o grupo de disponibilidade  
Para instalar um site que utiliza um grupo de disponibilidade do SQL Server:  

1.  Substitua o seguinte quando pedido pela configuração do Configuration Manager:  

    -   **Nome do SQL Server**: Introduza o nome virtual para o ponto final que configurou quando criou o grupo de disponibilidade. O nome virtual deve ser um nome DNS completo, como  **&lt;endpointServer\>. fabrikam.com**.  

    -   **Instância**:  Este valor deve permanecer em branco. Nesta configuração, não existe nenhuma instância.  

    -   **Base de dados**: Introduza o nome da base de dados que criou na réplica primária do grupo de disponibilidade.  

2.  Em seguida, tem de fornecer uma localização de rede que cada SQL Server no grupo possa aceder:  

    -   A conta de computador e a conta de serviço de cada SQL Server necessitam de acesso de controlo total para esta localização.  

    -   Esta localização só é utilizada durante a configuração e pode ser partilhada ou eliminada depois de concluída a configuração e a instalação do site.  

3.  Depois de fornecer estas informações, conclua a configuração com o seu procedimento e configurações normais.  

##  <a name="BKMK_ClusterServerUpdates"></a> Serviço de um cluster de servidores  
Pode agora criar uma coleção que contém servidores num cluster e, em seguida, configure as definições de cluster para utilizar ao implementar atualizações para o cluster. Pode controlar a percentagem de servidores que estão online em qualquer momento, bem como para configurar os scripts do PowerShell de pré e pós-implementação para executar ações personalizadas.  

**Problemas conhecidos nesta versão:**  

-   Os relatórios não estão disponíveis para verificar o estado de implementação de atualizações de software para servidores de cluster.  

-   A opção de sequência de manutenção no **definições do Cluster** página está desativada e não está disponível nesta versão.  

### <a name="try-it-out"></a>Experimente!  
Experimente concluir a tarefa seguinte e, em seguida, utilize as informações de feedback perto da parte superior deste tópico para nos informar como correu:  

-   Posso criar uma coleção que representa um cluster de servidores. Para este teste, pode configurar as regras de associação recolhidas para ter 2 computadores nesta coleção.  

-   Posso especificar que apenas 50% dos servidores no cluster pode ser offline a qualquer momento no cluster de manutenção. Utilize os scripts de exemplo no procedimento para especificar os scripts de pré e pós-implementação.  

-   Implemente uma atualização para esta coleção. Consulte os ficheiros txt e Start em C:\temp e certifique-se de horas de início e de fim para a implementação nos servidores no cluster. Reveja o ficheiro Updatesdeployment log para obter mais informações.  

#### <a name="to-create-a-collection-for-a-server-cluster"></a>Para criar uma coleção para um cluster de servidores  

1.  [Criar uma coleção de dispositivos](https://technet.microsoft.com/library/gg712295.aspx) que contenha os servidores no cluster.  

2.  Na **ativos e compatibilidade** área de trabalho, clique em **coleções de dispositivos**, clique com o botão direito na coleção que contém os servidores no cluster e, em seguida, clique em **propriedades** .  

3.  Sobre o **gerais** separador, selecione **todos os dispositivos fazem parte do mesmo cluster de servidor**e, em seguida, clique em **definições**.  

4.  Sobre o **definições do Cluster** , selecione a percentagem de servidores que podem ser colocados offline ao mesmo tempo para que as atualizações de software instaladas. Um servidor de cluster poderá ser colocado offline por vez, independentemente da percentagem que indicar. O Configuration Manager irá arredondar para baixo ao selecionar o número de servidores para fazer a manutenção de uma só vez. Por exemplo, se escolher 51% e existirem 4 servidores no cluster, 2 servidores serão colocados offline ao mesmo tempo.  

5.  Especifique se pretende utilizar um script de pré-implementação (drenagem do nó) ou o script de pós-implementação (retoma do nó).  

    > [!TIP]  
    >  Seguem-se exemplos que pode utilizar em testes de pré-implantação e os scripts de pós-implementação escrevem a hora atual num arquivo de texto:  
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

1.  [Implementar atualizações de software](https://technet.microsoft.com/library/gg712304.aspx) para a coleção de cluster de servidor.  

2.  [Monitorizar a implementação de atualização de software](https://technet.microsoft.com/library/gg712304.aspx).  
