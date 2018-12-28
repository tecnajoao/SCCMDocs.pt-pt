---
title: Configurar grupos de disponibilidade
titleSuffix: Configuration Manager
description: Configurar e gerir o SQL Server sempre em grupos de disponibilidade com o SCCM.
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7e4ec207-bb49-401f-af1b-dd705ecb465d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 10b15f8463bb54df859f09379f41a809a45fc5b9
ms.sourcegitcommit: 81e3666c41eb976cc7651854042dafe219e2e467
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/21/2018
ms.locfileid: "53747131"
---
# <a name="configure-sql-server-always-on-availability-groups-for-configuration-manager"></a>Configurar grupos de disponibilidade Always On do SQL Server para o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize as informações neste tópico para configurar e gerir os grupos de disponibilidade que utiliza com o Configuration Manager.

Antes de começar:  
-   Estar familiarizado com as informações a partir [preparar a utilização de grupos de disponibilidade Always On do SQL Server com o Configuration Manager](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).
-   Estar familiarizado com a documentação do SQL Server sobre a utilização de grupos de disponibilidade e os procedimentos relacionados. Essa informação é necessária para concluir os seguintes cenários.

> [!TIP]  
>  Ligações a partir deste tópico para o SQL Server, aceda ao conteúdo, para o SQL Server 2016. Se não utilizar essa versão do SQL Server, consulte a documentação para a versão que utilizar.

## <a name="create-and-configure-an-availability-group"></a>Criar e configurar um grupo de disponibilidade
Utilize o procedimento seguinte para criar um grupo de disponibilidade e, em seguida, mover uma cópia da base de dados do site para esse grupo de disponibilidade.

Para concluir este procedimento, tem de ser a conta que utiliza:
-   Um membro do **administradores locais** grupo em cada computador que está no grupo de disponibilidade.
-   R **sysadmin** em cada instância do SQL Server que aloja a base de dados do site.

### <a name="to-create-and-configure-an-availability-group-for-configuration-manager"></a>Para criar e configurar um grupo de disponibilidade para o Configuration Manager  
1. Utilize o seguinte comando para parar o site do Configuration Manager: **Preinst.exe /stopsite**. Para obter mais informações sobre como utilizar Preinst.exe, consulte [ferramenta manutenção da hierarquia](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe).

2. Altere o modelo de cópia de segurança para a base de dados do site de **SIMPLES** para **COMPLETA**.
   Veja [Ver ou Alterar o Modelo de Recuperação de uma Base de Dados](/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server) na documentação do SQL Server. (Os grupos de disponibilidade só suportam COMPLETA).

3. Utilize o SQL Server para criar uma cópia de segurança completa da sua base de dados do site. Em seguida, efetue um dos seguintes, dependendo se o servidor que aloja a base de dados do site irá ser um membro de réplica do novo grupo de disponibilidade ou não:
   - **Será o membro do grupo de disponibilidade:**  
     Se utilizar este servidor como membro de réplica primária inicial do grupo de disponibilidade, não é necessário restaurar uma cópia da base de dados do site para este ou outro servidor no grupo. A base de dados já estará em vigor na réplica primária e do SQL Server irá replicar a base de dados para as réplicas secundárias durante um passo posterior.  

     -    **Não será um membro do grupo de disponibilidade:**   
     Restaure uma cópia da base de dados do site para o servidor que irá alojar a réplica primária do grupo.

   Para obter informações sobre como concluir este passo, consulte [criar uma cópia de segurança da base de dados completa](/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server) e [restaurar uma cópia de segurança da base de dados com o SSMS](/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms) na documentação do SQL Server.

4. No servidor que irá alojar a réplica primária inicial do grupo, utilize o [Assistente de novo grupo de disponibilidade](/sql/database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio) para criar o grupo de disponibilidade. No assistente:
   - Sobre o **selecionar base de dados** , selecione a base de dados para o seu site do Configuration Manager.  

   - Na página **Especificar Réplicas** , configure:
     -    **Réplicas:** Especifique os servidores que irão alojar réplicas secundárias.

     -    **Serviço de escuta:** Especifique a **nome de DNS do serviço de escuta** como um nome DNS completo, como  **&lt;Listener_Server >. fabrikam.com**. Isto é utilizado quando configurar o Configuration Manager para utilizar a base de dados no grupo de disponibilidade.

   - Na página **Selecionar Sincronização de Dados Inicial** , selecione **Completa**. Depois do assistente cria o grupo de disponibilidade, o assistente irá criar cópias de segurança o registo de transações e a base de dados primário. O Assistente de restaurá-los em cada servidor que aloja uma réplica secundária. (Se não utilizar este passo, terá de restaurar uma cópia da base de dados do site para cada servidor que aloja uma réplica secundária e associar manualmente essa base de dados ao grupo.)   

5. Verifique a configuração em todas as réplicas:   
   1.    Certifique-se de que a conta de computador do servidor do site é um membro do **administradores locais** grupo em cada computador que seja membro do grupo de disponibilidade.  

   2.  Executar o [script de verificação](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#prerequisites) de pré-requisitos para confirmar que a base de dados em todas as réplicas está corretamente configurada.

   3.    Se for necessário definir configurações nas réplicas secundárias, tem manualmente ativação pós-falha da réplica primária para a réplica secundária antes de continuar. Só pode configurar a base de dados de uma réplica primária. Para obter mais informações, consulte [realizar uma ativação pós-falha da Manual planeada de um grupo de disponibilidade](/sql/database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server) na documentação do SQL Server.

6. Depois de todas as réplicas de cumprir os requisitos, o grupo de disponibilidade está pronto para ser utilizado com o Configuration Manager.

## <a name="configure-a-site-to-use-the-database-in-the-availability-group"></a>Configurar um site para utilizar a base de dados no grupo de disponibilidade
Depois de [criar e configurar o grupo de disponibilidade](#create-and-configure-an-availability-group), utilize a manutenção do site do Configuration Manager para configurar o site para utilizar a base de dados que está alojado pelo grupo de disponibilidade.

Não é suportada para instalar um novo site com a respetiva base de dados num grupo de disponibilidade. Por exemplo, se utilizar a linha de base de dados de 1702, tem de instalar o site utilizando uma única instância do SQL Server. Após a instalação do site, em seguida, pode mover a base de dados do site ao grupo de disponibilidade.

Para concluir este procedimento, tem de ser a conta que utiliza para executar a configuração do Configuration Manager:
-   Um membro do **administradores locais** grupo em cada computador que seja membro do grupo de disponibilidade.
-   R **sysadmin** em cada instância do SQL Server que aloja a base de dados do site.

> [!IMPORTANT]
> Ao utilizar o Microsoft Intune com o Configuration Manager numa configuração híbrida, mover a base de dados de ou para um grupo de disponibilidade aciona uma ressincronização de dados com a cloud. Este ressincronização não pode ser evitada.

### <a name="to-configure-a-site-to-use-the-availability-group"></a>Para configurar um site para utilizar o grupo de disponibilidade
1.  Execute **configuração do Configuration Manager** partir  **&lt; *pasta de instalação de site do Configuration Manager*> \BIN\X64\setup.exe**.

2.  Na página **Introdução** , selecione **Executar a manutenção do site ou repor este site**e clique em **Seguinte**.

3.  Selecione a opção **Modificar a configuração do SQL Server** e clique em **Seguinte**.

4.  Reconfigure as seguintes opções para a base de dados do site:
    -   **Nome do SQL Server:** Introduza o nome virtual para o grupo de disponibilidade **serviço de escuta** que configurou quando criou o grupo de disponibilidade. O nome virtual deve ser um nome DNS completo, como  **&lt; *endpointServer*>. fabrikam.com**.  

    -   **Instância:** Este valor tem de estar em branco para especificar a instância predefinida para o *serviço de escuta* do grupo de disponibilidade. Se a base de dados do site atual for executada numa instância nomeada, a instância nomeada está listada e tem de estar desmarcada.

    -   **Base de dados:** Deixe o nome, tal como é apresentado. Este é o nome da base de dados do site atual.

5.  Depois de fornecer estas informações para a nova localização da base de dados, conclua a Configuração com o procedimento e configurações normais.



## <a name="add-or-remove-synchronous-replica-members"></a>Adicionar ou remover membros de réplica síncrona  
Quando a sua base de dados do site estiver alojada num grupo de disponibilidade, utilize os procedimentos seguintes para adicionar ou remover membros de réplicas síncrona. Para obter informações sobre o tipo e número de réplicas que são suportados, consulte **as configurações do grupo de disponibilidade** sob [pré-requisitos](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#prerequisites) na preparar para utilizar o tópico do grupo de disponibilidade.

Para concluir os procedimentos seguintes, tem de ser a conta que utiliza:
-   Um membro do **administradores locais** grupo em cada computador que seja membro do grupo de disponibilidade.
-   R **sysadmin** em cada servidor de SQL que aloja ou irá alojar a base de dados do site.


### <a name="to-add-a-new-synchronous-replica-member"></a>Para adicionar um novo membro de réplica síncrona  
O processo para adicionar a réplica secundária a um grupo de disponibilidade que utiliza com o Configuration Manager pode ser complexa, dinâmica e requerem passos e procedimentos que alterações com base nos ambientes individuais. Estamos a trabalhar em melhoramentos para o Configuration Manager para simplificar o processo. Entretanto, se precisar de adicionar réplicas secundárias, consulte o blogue seguinte no TechNet para obter orientações
-   [ConfigMgr 1702: Adicionar um novo nó (réplica secundária) para um AG de pedidos de SQL existente](https://blogs.technet.microsoft.com/umairkhan/2017/07/17/configmgr-1702-adding-a-new-node-secondary-replica-to-an-existing-sql-ao-ag/)

### <a name="to-remove-a-replica-member"></a>Para remover um membro de réplica
Para este procedimento, utilize as informações em [remover uma réplica secundária de um grupo de disponibilidade](/sql/database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server) na documentação do SQL Server.  


## <a name="configure-an-asynchronous-commit-replica"></a>Configurar uma réplica de consolidação assíncrona
A partir do Configuration Manager versão 1706, pode adicionar uma réplica assíncrona para um grupo de disponibilidade que utiliza com o Configuration Manager. Para fazer isso, não é necessário executar os scripts de configuração necessários para configurar uma réplica síncrona. (Isso é porque não há suporte para utilizar essa réplica assíncrona como a base de dados do site.) Consulte a [documentação do SQL Server](https://msdn.microsoft.com/library/hh213247(v=sql.120).aspx(d=robot)) para obter informações sobre como adicionar réplicas secundárias para grupos de disponibilidade.

## <a name="use-the-asynchronous-replica-to-recover-your-site"></a>Utilizar a réplica assíncrona para recuperar o seu site
Com o Configuration Manager versão 1706 e posterior, pode utilizar uma réplica assíncrona para recuperar a base de dados do site. Para tal, tem de parar o site primário Active Directory para impedir que escritas adicionais para a base de dados do site. Depois de parar o site, pode utilizar uma réplica assíncrona em vez de utilizar um [base de dados recuperada manualmente](/sccm/protect/understand/backup-and-recovery#BKMK_SiteDatabaseRecoveryOption).

Para parar o site, pode utilizar o [ferramenta manutenção da hierarquia](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe) parar os serviços de chave no servidor do site. Utilize a linha de comando: **Preinst.exe /stopsite**   

A parar o site é equivalente a parar o serviço de Gestor de componentes do Site (sitecomp) seguido pelo serviço do SMS_Executive, no servidor do site.

<!-- For inclusion with passive primary site support:
> [!TIP]  
> If you use a primary passive replica (introduced in version [TBD],  you do not need to stop the passive replica. Only the active primary site must be stopped.
-->  

## <a name="stop-using-an-availability-group"></a>Parar de utilizar um grupo de disponibilidade
Utilize o procedimento seguinte quando já não pretender alojar a base de dados do site num grupo de disponibilidade. Isso envolve mover a base de dados de volta para uma única instância do SQL Server.

Para concluir este procedimento, tem de ser a conta que utiliza:
-   Um membro do **administradores locais** grupo em cada computador que seja membro do grupo de disponibilidade
-   R **sysadmin** em cada instância do SQL Server que aloja a base de dados do site.

> [!IMPORTANT]  
> Ao utilizar o Microsoft Intune com o Configuration Manager numa configuração híbrida, mover a base de dados de ou para um grupo de disponibilidade aciona uma ressincronização de dados com a cloud. Isso não pode ser evitado.

### <a name="to-move-the-site-database-from-an-availability-group-back-to-a-single-instance-sql-server"></a>Para mover a base de dados do site de um grupo de disponibilidade de volta para um SQL Server de instância única
1.  Pare o site do Configuration Manager ao utilizar o seguinte comando: **Preinst.exe /stopsite**. Para obter mais informações, consulte [ferramenta manutenção da hierarquia](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe).

2.  Utilize o SQL Server para criar uma cópia de segurança completa da sua base de dados do site a partir da réplica primária. Para obter informações sobre como executar este passo, veja [Criar uma Cópia de Segurança Completa da Base de Dados](/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server) na documentação do SQL Server.

3.  Se o servidor que é a réplica primária do grupo de disponibilidade irá alojar a única instância da base de dados do site, pode ignorar este passo:  

    -   Utilize o SQL Server para restaurar a cópia de segurança da base de dados do site para o servidor que irá aloja a base de dados do site. Ver [restaurar uma cópia de segurança da base de dados com o SSMS](/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms) na documentação do SQL Server.   <br />  <br />

4.  No servidor que irá alojar a base de dados (a réplica primária ou o servidor em que tiver restaurado a base de dados do site), altere o modelo de cópia de segurança da base de dados do site do **completo** ao **simples**. Veja [Ver ou Alterar o Modelo de Recuperação de uma Base de Dados](/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server) na documentação do SQL Server.  

5.  Execute **configuração do Configuration Manager** partir  **&lt; *pasta de instalação de site do Configuration Manager >* \BIN\X64\setup.exe**.

6.  Na página **Introdução** , selecione **Executar a manutenção do site ou repor este site**e clique em **Seguinte**.  

7.  Selecione a opção **Modificar a configuração do SQL Server** e clique em **Seguinte**.  

8.  Reconfigure as seguintes opções para a base de dados do site:
    -   **Nome do SQL Server:** Introduza o nome do servidor que aloja agora a base de dados do site.

    -   **Instância:** Especifique a instância nomeada que aloja a base de dados do site ou deixe em branco se a base de dados estiver na instância predefinida.

    -   **Base de dados:** Deixe o nome, tal como é apresentado. Este é o nome da base de dados do site atual.    

9.  Depois de fornecer estas informações para a nova localização da base de dados, conclua a Configuração com o procedimento e configurações normais. Quando tiver concluído a Configuração, o site é reiniciado e começa a utilizar a nova localização da base de dados.    

10. Para limpar os servidores que eram membros do grupo de disponibilidade, siga as orientações em [Remover um Grupo de Disponibilidade](/sql/database-engine/availability-groups/windows/remove-an-availability-group-sql-server) na documentação do SQL Server.
