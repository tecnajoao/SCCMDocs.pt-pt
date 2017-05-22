---
title: AlwaysOn do SQL Server | Documentos do Microsoft
ms.custom: na
ms.date: 1/4/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 58d52fdc-bd18-494d-9f3b-ccfc13ea3d35
caps.latest.revision: 16
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: aaaab003ddd22f18160d4be63cfeab3a7e7f6b03
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="sql-server-alwayson-for-a-highly-available-site-database-for-system-center-configuration-manager"></a>SQL Server AlwaysOn para uma base de dados de site de elevada disponibilidade para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


 Iniciar com o System Center Configuration Manager versão 1602, pode utilizar SQL Server [grupos de Disponibilidade AlwaysOn](https://msdn.microsoft.com/library/hh510230\(v=sql.120\).aspx) para alojar a base de dados do site em sites primários e o site de administração central como uma solução de elevada disponibilidade e recuperação de desastres. O grupo de disponibilidade pode ser alojado no local ou no Microsoft Azure.  

 Quando utiliza o Microsoft Azure para alojar o grupo de disponibilidade, pode aumentar ainda mais a disponibilidade da sua base de dados do site através da utilização de Grupos de Disponibilidade AlwaysOn do SQL Server com Conjuntos de Disponibilidade do Azure. Para obter mais informações sobre Conjuntos de Disponibilidade do Azure, veja [Gerir a disponibilidade das máquinas virtuais](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-manage-availability/).  

 O Configuration Manager suporta a alojar a base de dados do site num grupo de disponibilidade do SQL Server que está atrás um internas ou externas Balanceador de carga. Para além de configurar exceções de firewall em cada réplica, terá de adicionar regras para as seguintes portas de balanceamento de carga:
  - SQL sobre TCP: TCP 1433
  - SQL Server Service Broker: TCP 4022
  - Bloco de mensagem de servidor (SMB): TCP 445
  - Mapeador de pontos finais RPC: TCP 135


Seguem-se alguns cenários que são suportados com grupos de disponibilidade:  

-   Pode mover a base de dados do site para a instância predefinida do grupo de disponibilidade  

-   Pode adicionar ou remover membros de réplicas de um grupo de disponibilidade que aloja uma base de dados do site  

-   Pode mover a base de dados do site de um grupo de disponibilidade para uma instância predefinida ou nomeada de um SQL Server autónomo  

> [!Important]  
> Quando utilizar o Microsoft Intune com o Configuration Manager numa configuração híbrida, a deslocação da base de dados do site ou para um acionadores do grupo de disponibilidade uma ressincronização de dados com a nuvem. Não pode ser evitado. 



> [!NOTE]  
>  A configuração com êxito e a utilização de grupos de disponibilidade exige que esteja familiarizado com a configuração do SQL Server e com os grupos de disponibilidade do SQL Server. Os procedimentos para o System Center Configuration Manager neste tópico baseiam-se em obter documentação adicional e procedimentos que se encontram na biblioteca de documentação do SQL Server.  

 **Problemas conhecidos quando utiliza grupos de disponibilidade AlwaysOn com o Configuration Manager:**  

-   **Todos os servidores de réplica exigem um caminho de ficheiro idêntico no momento em que define o Configuration Manager para utilizar o grupo de disponibilidade:**  

    -   No momento que executar a configuração do Configuration Manager para redirecionar o site para utilizar a base de dados num grupo de disponibilidade, cada servidor de réplica secundária no grupo tem de ter um caminho de ficheiro que é idêntico do caminho do ficheiro utilizado para alojar os ficheiros de base de dados do site na réplica primária atual. Se não existir um caminho idêntico em réplicas secundárias, a Configuração não irá adicionar a instância de grupos de disponibilidade como a nova localização da base de dados do site.  

         Além disso, em cada servidor de réplica secundária, a conta de serviço do SQL Server local tem de ter a permissão **Controlo Total** para esta pasta.  

         Os servidores de réplica secundária apenas exigem este caminho de ficheiro enquanto estiver a utilizar a Configuração para especificar a instância de base de dados no grupo de disponibilidade.  Após a Configuração concluir a alteração para utilizar a base de dados do site no grupo de disponibilidade, pode eliminar o caminho não utilizado dos servidores de réplica secundária.  

         Por exemplo, considere os seguintes cenários:  

        -   Cria um grupo de disponibilidade que utiliza três SQL Servers  

        -   O servidor de réplica primária é uma nova instalação do SQL Server 2014.  Por predefinição, os ficheiros .MDF e .LDF de base de dados são armazenados em C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA  

        -   Ambos os servidores de réplica secundária foram atualizados para o SQL Server 2014 de versões anteriores e mantêm o caminho de ficheiro original para armazenar ficheiros de base de dados de: C:\Program Files\Microsoft SQL Server\MSSQL10. MSSQLSERVER\MSSQL\DATA  

        -   Antes de tentar mover a base de dados do site para este grupo de disponibilidade, em cada servidor de réplica secundária tem de criar o seguinte caminho de ficheiro mesmo se réplicas secundárias não irão utilizar esta localização do ficheiro:  C:\Program Files\Microsoft SQL Server\MSSQL12. MSSQLSERVER\MSSQL\DATA (isto é um duplicado do caminho que está a ser utilizado na réplica primária)  

        -   Em seguida, concede à conta de serviço do SQL Server em cada réplica secundária acesso de controlo total à localização do ficheiro recentemente criado nesse servidor  

        -   Agora pode com êxito executar a configuração do Configuration Manager para direcionar o site para utilizar a base de dados do site no grupo de disponibilidade  

-   **Quando a Configuração é executada para direcionar a base de dados do site para utilizar o grupo de disponibilidade, erros semelhantes ao seguinte poderão ser registados no ficheiro ConfigMgrSetup.log:**  

    -   ERRO: Erro do SQL Server: [25000] [3906] [Microsoft] [SQL Server Native cliente 11.0] [SQL Server] Falha ao atualizar a base de dados "CM_AAA" porque a base de dados é só de leitura.   Configuração do Configuration Manager 1/21/2016 4:54:59 PM  7344 (0x1CB0)  

     Estes erros são registados quando a Configuração tenta processar as funções de base de dados nas réplicas secundárias do grupo de disponibilidade. Estes erros podem ser ignorados com segurança.
- **Servidores SQL que alojam os grupos de disponibilidade adicionais:**

  Antes de instalar a versão 1610, quando utilizar um grupo de disponibilidade e, em seguida, execute a configuração do Configuration Manager ou instalar uma atualização para o Configuration Manager, cada réplica em cada grupo de disponibilidade adicionais no SQL Server que aloja o grupo de disponibilidade do Configuration Manager tem de ter as seguintes configurações:
    - **Ativação Pós-falha Manual**
    - **permitir todas as ligações só de leitura**


##  <a name="bkmk_BnR"></a> Alterações à Cópia de Segurança e Recuperação quando utiliza um grupo de disponibilidade AlwaysOn do SQL Server  
 **Cópia de segurança:**  

 Quando uma base de dados do site é executada num grupo de disponibilidade, deve continuar a executar o incorporado **Site de reserva** tarefa de manutenção do servidor para cópia de segurança de ficheiros e definições do Configuration Manager comuns, mas pretende utilizar não o. MDF ou. Ficheiros LDF criados dessa cópia de segurança. Em alternativa, planeie efetuar cópias de segurança diretas da base de dados do site utilizando o SQL Server.  

 Além disso, dado que o modelo de recuperação da base de dados está definido como completa, terá de planear a monitorização e manutenção do tamanho do registo de transações da base de dados do site.  No modelo de recuperação completa, as transações não são protegidas até ser feita uma cópia de segurança completa da base de dados ou do registo de transações. Um modelo de recuperação de completo é um requisito de utilizar a base de dados do site num grupo de disponibilidade e o conjunto ao configurar o grupo para utilização com o Configuration Manager. Para obter mais informações sobre a cópia de segurança e o restauro do SQL Server, veja [Cópia de Segurança e Restauro de Bases de Dados do SQL Server](https://msdn.microsoft.com/library/ms187048\(v=sql.120\).aspx) na documentação do SQL Server.  

 **Recuperação:**  

 Durante uma recuperação de site, desde que um nó do grupo de disponibilidade permaneça funcional, pode utilizar a opção de recuperação de sites **Ignorar recuperação de base de dados (Utilize esta opção se a base de dados não tiver sido afetada)**.  

 No entanto, se todos os nós de um grupo de disponibilidade tem sido perdidos, para poder recuperar o site, tem de recriar o grupo de disponibilidade (System Center Configuration Manager não é possível reconstruir ou restaurar o nó de disponibilidade.)  Depois de o grupo ter sido recriado com uma cópia de segurança restaurada e reconfigurada, em seguida, pode utilizar a opção de recuperação de sites **Ignorar recuperação de base de dados (Utilize esta opção se a base de dados não tiver sido afetada)**.  

 Para obter mais informações sobre cópia de segurança e recuperação, veja [Cópia de segurança e recuperação no System Center Configuration Manager](../../../../protect/understand/backup-and-recovery.md).  

##  <a name="bkmk_create"></a> Configurar um grupo de disponibilidade para utilização com o Configuration Manager  
 Antes de começar o procedimento seguinte, estar familiarizado com os procedimentos de SQL Server necessários para concluir esta configuração e os seguintes detalhes que se aplicam a grupos de disponibilidade que configura para ser utilizado com o Configuration Manager.  

 **Requisitos para grupos de disponibilidade AlwaysOn que utiliza com o System Center Configuration Manager:**  

-  *Versão*: Cada nó (ou a réplica) no grupo de disponibilidade tem de executar uma versão do SQL Server suportadas pelo System Center Configuration Manager. Se suportado pelo SQL Server, diferentes nós do grupo de disponibilidade podem executar diferentes versões do SQL Server.   

- *Edição*: Tem de utilizar uma edição Enterprise do SQL Server.  SQL Server 2016 Standard edition introduz grupos de disponibilidade básica, que não são suportados pelo Configuration Manager.


-   O grupo de disponibilidade tem de ter uma réplica primária e pode ter até duas réplicas secundárias síncronas.  

-  Depois de adicionar uma base de dados a um grupo de disponibilidade, tem de fazer a ativação pós-falha da réplica primária para uma secundária (tornando-a na nova réplica primária) e, em seguida, configurar a base de dados com o seguinte:
    - Ativar Trustworthy: igual a VERDADEIRO
    - Ativar o Service Broker: igual a VERDADEIRO
    - Definir o dbowner: igual a SA

    Pode executar o seguinte script para configurar estas definições, em que cm_ABC é o nome da sua base de dados do site:  

    >     Modelo global de utilização  
    >     Cm_ABC ALTER DATABASE SET NEW_BROKER   
    >     ALTER DATABASE cm_ABC definir ativar_broker  
    >     ALTER DATABASE cm_ABC ON definir fidedigna;  
    >     UTILIZAR cm_ABC  
    >     EXEC sp_changedbowner "sa"  
    >     Exec sp_configure ' max text repl size (B)', 2147483647 reconfigurar



-   O grupo de disponibilidade tem de ter, pelo menos, um **serviço de escuta do grupo de disponibilidade**.  O nome virtual deste serviço de escuta é utilizado quando configurar o Configuration Manager para utilizar a base de dados do site no grupo de disponibilidade. Apesar de um grupo de disponibilidade pode conter vários serviços de escuta, o Configuration Manager só pode efetuar utilizam um  

-   Cada réplica primária e secundária tem de:  
    - Estar definida para **permitir todas as ligações só de leitura**
    - Utilizar a **instância predefinida**
    - Estar definida para **Ativação Pós-falha Manual**  

        > [!TIP]  
        >  Suporta o System Center Configuration Manager utilizando as réplicas do grupo de disponibilidade quando definidas para ativação pós-falha automática. No entanto, a ativação pós-falha Manual deve ser definida quando executar a configuração para especificar a utilização da base de dados do site no grupo de disponibilidade e o momento instalar quaisquer atualizações do Configuration Manager (não apenas as atualizações aplicáveis a base de dados do site).  

  **Limitações para grupos de disponibilidade**
   - Grupos de disponibilidade básica (introduzidos com o SQL Server 2016 Standard edition) não são suportados. Isto acontece porque os grupos de disponibilidade básicas não suportam o acesso de leitura para réplicas secundárias, um requisito para utilização com o Configuration Manager. Para obter mais informações, consulte o artigo [básicas grupos de disponibilidade (sempre no grupos de disponibilidade)](https://msdn.microsoft.com/en-us/library/mt614935.aspx).

   - Grupos de disponibilidade são suportados apenas para a base de dados do site e não para o software de atualização de base de dados ou base de dados de relatórios.   
   - Quando utiliza um grupo de disponibilidade, tem de configurar manualmente o ponto de relato para utilizar a réplica primária atual e não o serviço de escuta do grupo de disponibilidade. Se a réplica primária fizer a ativação pós-falha para outra réplica, terá de reconfigurar o ponto de relato para utilizar a nova réplica primária.  
   - Antes de instalar atualizações, como a versão 1606, certifique-se de que o grupo de disponibilidade está definido para ativação pós-falha manual. Após a atualização do site, pode restaurar a ativação pós-falha para ser automática.



 **Permissões necessárias para configurar e utilizar grupos de disponibilidade:**  

-   A conta de computador do servidor do site tem de ser membro do grupo **Administradores Locais** em todos os computadores membros do grupo de disponibilidade.  

#### <a name="to-configure-an-availability-group-to-host-a-site-database"></a>Para configurar um grupo de disponibilidade para alojar uma base de dados do site  

1.  Utilize o seguinte comando para parar o site do Configuration Manager:  
     **Preinst.exe /stopsite**  

     Para obter mais informações sobre a utilização de Preinst.exe, veja [Ferramenta Manutenção da Hierarquia (Preinst.exe) para o System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md).  

2.  Altere o modelo de cópia de segurança para a base de dados do site de **SIMPLES** para **COMPLETA**.  

     Veja [Ver ou Alterar o Modelo de Recuperação de uma Base de Dados](https://msdn.microsoft.com/library/ms189272\(v=sql.120\).aspx) na documentação do SQL Server. (Os grupos de disponibilidade só suportam COMPLETA).  

3.  No servidor que irá alojar a réplica primária do grupo, utilize o **Assistente de Novo Grupo de Disponibilidade** para criar o grupo de disponibilidade. No assistente:  

    -   No **selecionar base de dados** página, selecione a base de dados para que o site do Configuration Manager  

    -   Na página **Especificar Réplicas** , configure:  

        -   **Réplicas**: Especifique os servidores que irão alojar réplicas secundárias  

        -   **Serviço de escuta**: Especifique o **nome de DNS do serviço de escuta** como um nome DNS completo, como  **&lt;Listener_Server >. fabrikam.com**. Isto é utilizado quando configurar o Configuration Manager para utilizar a base de dados no grupo de disponibilidade.

    -   Na página **Selecionar Sincronização de Dados Inicial** , selecione **Completa**. Depois de o assistente criar o grupo de disponibilidade, o assistente irá criar cópias de segurança da base de dados primária e do registo de transações e restaurá-las em cada servidor que aloja uma réplica secundária. Se não utilizar este passo, terá de restaurar uma cópia da base de dados do site para cada servidor que aloja uma réplica secundária e associar manualmente essa base de dados ao grupo.  

    Para obter mais informações, veja [Utilizar o Assistente de Grupo de Disponibilidade](https://msdn.microsoft.com/library/hh403415\(v=sql.120\).aspx) na documentação do SQL Server.  

4.  Depois de o grupo de disponibilidade estar configurado, configure a base de dados do site na réplica primária com a propriedade **TRUSTWORTHY** e, em seguida, **ative a integração do CLR**. Para obter informações sobre como fazer estas configurações, veja [Propriedade de Base de Dados TRUSTWORTHY](https://msdn.microsoft.com/library/ms187861\(v=sql.120\).aspx) e  [Ativar a Integração do CLR](https://msdn.microsoft.com/library/ms131048\(v=sql.120\).aspx) na documentação do SQL Server.  

5.  Efetue as seguintes ações para configurar cada réplica secundária no grupo de disponibilidade:  

    1.  Manualmente, execute a ativação pós-falha da réplica primária atual para uma réplica secundária. Veja [Executar uma Ativação Pós-falha Manual Planeada de um Grupo de Disponibilidade](https://msdn.microsoft.com/library/hh231018\(v=sql.120\).aspx) na documentação do SQL Server.  

    2.  Configure a base de dados na nova réplica primária com a propriedade **TRUSTWORTHY** e, em seguida, **ative a integração do CLR**.  

6.  Depois de todas as réplicas são promovidas para réplicas primárias e as bases de dados configuradas, o grupo de disponibilidade está pronto para ser utilizado com o Configuration Manager.  





##  <a name="bkmk_direct"></a> Mover uma base de dados do site para um grupo de disponibilidade  
 Pode mover uma base de dados de site de um site anteriormente instalado para um grupo de disponibilidade. Primeiro tem de criar o grupo de disponibilidade e, em seguida, configurar a base de dados para funcionamento no grupo de disponibilidade.  

 Para concluir este procedimento, a conta de utilizador que executa a configuração do Configuration Manager tem de ser um membro do **administradores locais** grupo em cada computador que seja um membro do grupo de disponibilidade.  

#### <a name="to-move-a-site-database-to-an-availability-group"></a>Para mover uma base de dados do site para um grupo de disponibilidade  

1.  Executar **configuração do Configuration Manager** de  **&lt;pasta de instalação de site do Configuration Manager\>\bin\x64\setup.exe.**.  

2.  Na página **Introdução** , selecione **Executar a manutenção do site ou repor este site**e clique em **Seguinte**.  

3.  Selecione a opção **Modificar a configuração do SQL Server** e clique em **Seguinte**.  

4.  Reconfigure as seguintes opções para a base de dados do site:  

    -   **Nome do SQL Server:** Introduza o nome virtual para o serviço de escuta de grupo de disponibilidade que configurou ao criar o grupo de disponibilidade. O nome virtual deve ser um nome DNS completo, como  **&lt;endpointServer\>. fabrikam.com**  

    -   **Instância:** Este valor tem de estar em branco para especificar a instância predefinida para o serviço de escuta de grupo de disponibilidade do grupo de disponibilidade.  Se a base de dados atual estiver instalada numa instância nomeada, a instância nomeada será listada e tem de ser desmarcada  

    -   **Base de dados:** Mantenha o nome, tal como é apresentado. Este é o nome da base de dados do site atual.  

5.  Depois de fornecer estas informações para a nova localização da base de dados, conclua a Configuração com o procedimento e configurações normais.  

##  <a name="bkmk_change"></a> Adicionar ou remover membros de um grupo de disponibilidade ativo  
 Depois do Configuration Manager está a utilizar uma base de dados do site alojado num grupo de disponibilidade pode remover um membro de réplica ou adicionar um membro de réplica adicionais (não deve exceder um site primário e dois nós secundários).  

#### <a name="to-add-a-new-replica-member"></a>Para adicionar um novo membro de réplica  

1.  Adicione o novo servidor como réplica secundária ao grupo de disponibilidade. Veja  [Adicionar uma Réplica Secundária a um Grupo de Disponibilidade (SQL Server)](https://msdn.microsoft.com/library/hh213247\(v=sql.120\).aspx)na biblioteca de documentação do SQL Server.  

2.  Parar o site do Configuration Manager, executando **Preinst.exe /stopsite** consulte [ferramenta de manutenção da hierarquia (Preinst.exe) para o System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md).  

3.  Configure cada réplica secundária. Efetue as seguintes ações para cada réplica secundária no grupo de disponibilidade:  

    1.  Manualmente, execute a ativação pós-falha da réplica primária para a nova réplica secundária. Veja [Executar uma Ativação Pós-falha Manual Planeada de um Grupo de Disponibilidade](https://msdn.microsoft.com/library/hh231018\(v=sql.120\).aspx) na documentação do SQL Server.  

    2.  Configure a base de dados no novo servidor para ser Trustworthy e ative a integração do CLR. Veja [Propriedade de Base de Dados TRUSTWORTHY](https://msdn.microsoft.com/library/ms187861\(v=sql.120\).aspx) e  [Ativar a Integração do CLR](https://msdn.microsoft.com/library/ms131048\(v=sql.120\).aspx)na documentação do SQL Server.  

4.  Reinicie o site, iniciando os serviços (**sitecomp**) e **SMS_Executive** do Gestor de Componentes do Site.  

#### <a name="to-remove-a-replica-member-from-the-availability-group"></a>Para remover um membro de réplica do grupo de disponibilidade  

-   Utilize as informações em [Remover uma Réplica Secundária de um Grupo de Disponibilidade](https://msdn.microsoft.com/library/hh213149\(v=sql.120\).aspx) na documentação do SQL Server.  

##  <a name="bkmk_remove"></a> Mover a base de dados do site de um grupo de disponibilidade de volta para um SQL Server de instância única  
 Utilize o procedimento seguinte quando já não pretender alojar a base de dados do site num grupo de disponibilidade.  

#### <a name="to-move-the-site-database-from-an-availability-group-back-to-a-single-instance-sql-server"></a>Para mover a base de dados do site de um grupo de disponibilidade de volta para um SQL Server de instância única  

1.  Pare o site do Configuration Manager, utilizando o seguinte comando:  
     **Preinst.exe /stopsite**.  Para obter mais informações, veja [Ferramenta Manutenção da Hierarquia (Preinst.exe) para o System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md).  

2.  Utilize o SQL Server para criar uma cópia de segurança completa da sua base de dados do site a partir da réplica primária. Para obter informações sobre como executar este passo, veja [Criar uma Cópia de Segurança Completa da Base de Dados](https://msdn.microsoft.com/library/ms187510\(v=sql.120\).aspx) na documentação do SQL Server.  

3.  Se o servidor que aloja a réplica primária do grupo de disponibilidade alojar agora a instância única da base de dados do site, pode ignorar este passo:  

    -   Utilize o SQL Server para restaurar a cópia de segurança da base de dados do site para o servidor que irá aloja a base de dados do site.  Veja [Restaurar uma Cópia de Segurança da Base de Dados (SQL Server Management Studio)](https://msdn.microsoft.com/library/ms177429\(v=sql.120\).aspx) na documentação do SQL Server.  

4.  Na base de dados do site restaurada, altere o modelo de cópia de segurança para a base de dados do site de **COMPLETA** para **SIMPLES**.  Veja [Ver ou Alterar o Modelo de Recuperação de uma Base de Dados](https://msdn.microsoft.com/library/ms189272\(v=sql.120\).aspx) na documentação do SQL Server.  

5.  Executar **configuração do Configuration Manager** de  **&lt;pasta de instalação de site do Configuration Manager\>\bin\x64\setup.exe.**.  

6.  Na página **Introdução** , selecione **Executar a manutenção do site ou repor este site**e clique em **Seguinte**.  

7.  Selecione a opção **Modificar a configuração do SQL Server** e clique em **Seguinte**.  

8.  Reconfigure as seguintes opções para a base de dados do site:  

    -   **Nome do SQL Server:** Introduza o nome do servidor que aloja agora a base de dados do site.  

    -   **Instância:** Especifique a instância com nome que aloja a base de dados do site ou deixe em branco, se a base de dados estiver na instância predefinida.  

    -   **Base de dados:** Mantenha o nome, tal como é apresentado. Este é o nome da base de dados do site atual.  

9. Depois de fornecer estas informações para a nova localização da base de dados, conclua a Configuração com o procedimento e configurações normais. Quando tiver concluído a Configuração, o site é reiniciado e começa a utilizar a nova localização da base de dados.  

10. Para limpar os servidores que eram membros do grupo de disponibilidade, siga as orientações em [Remover um Grupo de Disponibilidade](https://msdn.microsoft.com/library/ff878113\(v=sql.120\).aspx) na documentação do SQL Server.

