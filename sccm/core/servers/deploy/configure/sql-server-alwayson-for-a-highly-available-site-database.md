---
title: SQL Server AlwaysOn
titleSuffix: Configuration Manager
description: Planear a utilização de um grupo de disponibilidade Always On do SQL Server com o Configuration Manager
ms.date: 08/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 58d52fdc-bd18-494d-9f3b-ccfc13ea3d35
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 08f5e0d9986c59d9a2a37c26f3ed9e245ac62f41
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56120049"
---
# <a name="prepare-to-use-sql-server-always-on-availability-groups-with-configuration-manager"></a>Preparar a utilização de grupos de disponibilidade Always On do SQL Server com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize este artigo para preparar o Configuration Manager para utilizar grupos de disponibilidade Always On do SQL Server. Esta funcionalidade fornece uma solução de recuperação após desastre e de disponibilidade elevada para a base de dados do site.  

O Configuration Manager suporta a utilização de grupos de disponibilidade:
- Em sites primários e o site de administração central.
- No local, ou no Microsoft Azure.

Quando utiliza grupos de disponibilidade no Microsoft Azure, pode aumentar ainda mais a disponibilidade da sua base de dados do site utilizando *conjuntos de disponibilidade do Azure*. Para obter mais informações sobre Conjuntos de Disponibilidade do Azure, veja [Gerir a disponibilidade das máquinas virtuais](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-manage-availability/).

> [!Important]
>  Antes de continuar, ser confortável com a configuração do SQL Server e os grupos de disponibilidade do SQL Server. As informações que se segue faz referência a biblioteca de documentação do SQL Server e os procedimentos.



## <a name="supported-scenarios"></a>Cenários suportados

São suportados os seguintes cenários para utilizar grupos de disponibilidade com o Configuration Manager. Para obter mais informações e procedimentos para cada cenário, consulte [configurar grupos de disponibilidade para o Configuration Manager](/sccm/core/servers/deploy/configure/configure-aoag).

- [Criar um grupo de disponibilidade para utilização com o Configuration Manager](/sccm/core/servers/deploy/configure/configure-aoag#create-and-configure-an-availability-group)  
- [Configurar um site para utilizar um grupo de disponibilidade](/sccm/core/servers/deploy/configure/configure-aoag#configure-a-site-to-use-the-database-in-the-availability-group)  
- [Adicionar ou remover membros de réplicas síncrono de um grupo de disponibilidade que aloja uma base de dados do site](/sccm/core/servers/deploy/configure/configure-aoag#add-and-remove-synchronous-replica-members)  
- [Configurar réplicas de consolidação assíncrona](/sccm/core/servers/deploy/configure/configure-aoag#configure-an-asynchronous-commit-repilca)  
- [Recuperar um site a partir de uma réplica de consolidação assíncrona](/sccm/core/servers/deploy/configure/configure-aoag#use-the-asynchronous-replica-to-recover-your-site)  
- [Mover uma base de dados fora de um grupo de disponibilidade para um padrão ou com o nome instância do SQL Server autónomo](/sccm/core/servers/deploy/configure/configure-aoag#stop-using-an-availability-group)  



## <a name="prerequisites"></a>Pré-requisitos

Os seguintes pré-requisitos se aplicam a todos os cenários. Se os pré-requisitos adicionais que se aplicam a um cenário específico, eles são detalhados com esse cenário.   

### <a name="configuration-manager-accounts-and-permissions"></a>Permissões e contas do Configuration Manager

#### <a name="site-server-to-replica-member-access"></a>Servidor do site para o acesso de membro de réplica   
A conta de computador do servidor do site tem de ser um membro do **administradores locais** grupo em cada computador que seja membro do grupo de disponibilidade.


### <a name="sql-server"></a>SQL Server

#### <a name="version"></a>Versão  
Cada réplica no grupo de disponibilidade tem de executar uma versão do SQL Server que é suportado pela versão do Configuration Manager. Quando suportado pelo SQL Server, nós diferentes de um grupo de disponibilidade podem executar diferentes versões do SQL Server. Para obter mais informações, consulte [versões do SQL Server suportadas para o Configuration Manager](/sccm/core/plan-design/configs/support-for-sql-server-versions).<!--SCCMDocs issue 656-->

#### <a name="edition"></a>Edição  
Utilize um *Enterprise* edição do SQL Server.

#### <a name="account"></a>Conta  
Cada instância do SQL Server pode ser executado sob uma conta de utilizador de domínio (**conta de serviço**) ou uma conta de domínio. Cada réplica num grupo pode ter uma configuração diferente. 

- Utilize uma conta com o mais baixo possível de permissões. Para obter mais informações, consulte [considerações de segurança para uma instalação do SQL Server](https://docs.microsoft.com/sql/sql-server/install/security-considerations-for-a-sql-server-installation).  

- Para obter mais informações sobre como configurar contas de serviço e as permissões para o SQL Server, consulte [contas e permissões de serviço de configurar o Windows](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions).  

- Para utilizar uma conta de domínio, tem de utilizar certificados. Para obter mais informações, consulte [utilizar certificados para um ponto final (Transact-SQL) de espelhamento de banco de dados](https://docs.microsoft.com/sql/database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql).  

- Para obter mais informações, consulte [criar um ponto final de espelhamento de banco de dados para grupos de Disponibilidade AlwaysOn](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell).  


### <a name="availability-group-configurations"></a>Configurações de grupo de disponibilidade

#### <a name="replica-members"></a>Membros de réplicas  
- O grupo de disponibilidade tem de ter uma réplica primária.  

- Utilize o mesmo número e tipo de réplicas num grupo de disponibilidade que oferece suporte a sua versão do SQL Server.

- Pode utilizar uma réplica de consolidação assíncrona para recuperar sua réplica síncrona. Para obter mais informações, consulte [opções de recuperação de base de dados do site](/sccm/core/servers/manage/backup-and-recovery#BKMK_SiteDatabaseRecoveryOption).  

    > [!Warning]  
    > O Configuration Manager não suporta *ativação pós-falha* para utilizar a réplica de consolidação assíncrona como a base de dados do site. Para obter mais informações, consulte [modos de ativação pós-falha e ativação pós-falha (sempre em grupos de disponibilidade)](https://docs.microsoft.com/en-us/sql/database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups?view=sql-server-2014).  

O Configuration Manager não valide o estado da réplica de consolidação assíncrona para confirmar que é atual. Utilização de uma réplica de consolidação assíncrona, como a base de dados do site pode colocar a integridade do seu site e os dados em risco. Por design, tal uma réplica pode ser sincronizada. Para obter mais informações, consulte [grupos de disponibilidade de descrição geral do SQL Server AlwaysOn](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server).

Cada membro de réplica tem de ter a seguinte configuração:

- Utilize o *instância predefinida* ou um *instância nomeada*  

- O **ligações na função primária** definição é **permitir todas as ligações**  

- O **secundário legível** definição é **Sim**  

- Ativado para **ativação pós-falha Manual**     

  > [!TIP]
  >  Suporta a do Configuration Manager com a disponibilidade do grupo réplicas quando definidas como **a ativação pós-falha automática**. Definir **ativação pós-falha Manual** quando:
  >  -  Executar a configuração do Configuration Manager para especificar a utilização da base de dados do site no grupo de disponibilidade.  
  >  -  Instalar qualquer atualização para o Configuration Manager. (Não apenas as atualizações aplicáveis à base de dados do site).  

#### <a name="replica-member-location"></a>Localização de membro de réplica
Quer alojar todas as réplicas de disponibilidade no local do grupo, ou hospedá-los todos no Microsoft Azure. Não é suportado um grupo que inclua um membro no local e um membro no Azure.     

Configuração do Configuration Manager tem de ligar a cada réplica. Quando configurar um grupo de disponibilidade no Azure e o grupo está por trás de um balanceador de carga interno ou externo, abra as portas predefinidas seguintes:   

- Mapeador de pontos finais RPC: **TCP 135**   

- SQL Server Service Broker: **TCP 4022**  

- SQL sobre TCP: **TCP 1433**   


Após a conclusão da configuração, as seguintes portas devem permanecer abertas para o Configuration Manager:  

- SQL Server Service Broker: **TCP 4022**  

- SQL sobre TCP: **TCP 1433**  

Pode usar portas personalizadas para essas configurações. Utilize as mesmas portas personalizadas pelo ponto final e em todas as réplicas no grupo de disponibilidade.


#### <a name="listener"></a>Serviço de escuta   
O grupo de disponibilidade tem de ter, pelo menos, um *serviço de escuta do grupo de disponibilidade*. Quando configurar o Configuration Manager para utilizar a base de dados do site no grupo de disponibilidade, ele usa o nome virtual deste serviço de escuta. Embora um grupo de disponibilidade possa conter várias escutas, Configuration Manager pode fazer apenas utilizar um. Para obter mais informações, consulte [criar ou configurar um serviço de escuta do grupo de disponibilidade do SQL Server](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server).

#### <a name="file-paths"></a>Caminhos de ficheiro   
Quando executar a configuração do Configuration Manager para configurar um site para utilizar a base de dados num grupo de disponibilidade, cada servidor de réplica secundária tem de ter um caminho de ficheiro do SQL Server que é idêntico ao caminho do arquivo para os ficheiros de base de dados do site na réplica primária atual. Se não existir um caminho idêntico, a configuração não consegue adicionar a instância para o grupo de disponibilidade como a nova localização da base de dados do site.  

A conta de serviço do SQL Server local tem de ter **controlo total** permissão para esta pasta.

Os servidores de réplica secundária apenas exigem este caminho de ficheiro enquanto estiver a utilizar o programa de configuração do Configuration Manager para especificar a instância de base de dados no grupo de disponibilidade. Após a conclusão da configuração de base de dados do site no grupo de disponibilidade, pode eliminar o caminho não utilizado a partir do secundário servidores de réplica.

Por exemplo, considere os seguintes cenários:

- Criar um grupo de disponibilidade que utiliza três SQL Servers.  

- O servidor de réplica primária é uma nova instalação do SQL Server 2014. Por padrão, ele armazena a base de dados. MDF e. Os ficheiros LDF no `C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA`.  

- Atualizado ambos os servidores de réplica secundária para o SQL Server 2014 de versões anteriores. Com a atualização, estes servidores mantêm o caminho do ficheiro original para armazenar os ficheiros de base de dados: `C:\Program Files\Microsoft SQL Server\MSSQL10.MSSQLSERVER\MSSQL\DATA`.  

- Antes de mover a base de dados para este grupo de disponibilidade, em cada servidor de réplica secundária, crie o seguinte caminho de ficheiro: `C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA`. Este caminho é um duplicado do caminho utilizado na réplica primária, mesmo que as réplicas secundárias não irá utilizar esta localização do ficheiro.  

- Em seguida, conceder a conta de serviço do SQL Server em cada acesso de controlo total de réplica secundária para a localização do ficheiro recentemente criado nesse servidor.  

- Agora pode executar com êxito a configuração do Configuration Manager para configurar o site para utilizar a base de dados do site no grupo de disponibilidade.  

#### <a name="configure-the-database-on-a-new-replica"></a>Configurar a base de dados numa nova réplica   
 Configure a base de dados de cada réplica com as seguintes definições:  

- Ativar **a integração do CLR**. Para obter mais informações, consulte [a integração do CLR](https://docs.microsoft.com/sql/relational-databases/clr-integration/clr-integration-enabling).  

- Definir **tamanho de replicação de texto máx** para `2147483647`  

- Definir o proprietário de base de dados o *conta SA*  

- Ative **ON** a **TRUSTWORTY** definição. Para obter mais informações, consulte a [propriedade de base de dados TRUSTWORTHY](https://docs.microsoft.com/sql/relational-databases/security/trustworthy-database-property).   

- Ativar o **Mediador de serviço**  

Apenas fazer estas configurações numa réplica primária. Para configurar uma réplica secundária, primeiro a ativação pós-falha primário para o secundário. Esta ação torna o secundário, a nova réplica primária.   


### <a name="verification-script"></a>Script de verificação

Execute o seguinte script SQL para verificar as configurações de base de dados para réplicas primárias e secundárias. Antes de poder corrigir um problema numa réplica secundária, altere o dessa réplica secundária a ser a réplica primária.

```SQL
    SET NOCOUNT ON

    DECLARE @dbname NVARCHAR(128)

    SELECT @dbname = sd.name FROM sys.sysdatabases sd WHERE sd.dbid = DB_ID()

    IF (@dbname = N'master' OR @dbname = N'model' OR @dbname = N'msdb' OR @dbname = N'tempdb' OR @dbname = N'distribution' ) BEGIN
    RAISERROR(N'ERROR: Script is targetting a system database.  It should be targeting the DB you created instead.', 0, 1)
    GOTO Branch_Exit;
    END ELSE
    PRINT N'INFO: Targeted database is ' + @dbname + N'.'

    PRINT N'INFO: Running verifications....'

    IF NOT EXISTS (SELECT * FROM sys.configurations c WHERE c.name = 'clr enabled' AND c.value_in_use = 1)
    PRINT N'ERROR: CLR is not enabled!'
    ELSE
    PRINT N'PASS: CLR is enabled.'

    DECLARE @repltable TABLE (
    name nvarchar(max),
    minimum int,
    maximum int,
    config_value int,
    run_value int )

    INSERT INTO @repltable
    EXEC sp_configure 'max text repl size (B)'

    IF NOT EXISTS(SELECT * from @repltable where config_value = 2147483647 and run_value = 2147483647 )
    PRINT N'ERROR: Max text repl size is not correct!'
    ELSE
    PRINT N'PASS: Max text repl size is correct.'

    IF NOT EXISTS (SELECT db.owner_sid FROM sys.databases db WHERE db.database_id = DB_ID() AND db.owner_sid = 0x01)
    PRINT N'ERROR: Database owner is not sa account!'
    ELSE
    PRINT N'PASS: Database owner is sa account.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_trustworthy_on = 1 )
    PRINT N'ERROR: Trustworthy bit is not on!'
    ELSE
    PRINT N'PASS: Trustworthy bit is on.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_broker_enabled = 1 )
    PRINT N'ERROR: Service broker is not enabled!'
    ELSE
    PRINT N'PASS: Service broker is enabled.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_honor_broker_priority_on = 1 )
    PRINT N'ERROR: Service broker priority is not set!'
    ELSE
    PRINT N'PASS: Service broker priority is set.'

    PRINT N'Done!'

    Branch_Exit:
```



## <a name="limitations-and-known-issues"></a>Limitações e problemas conhecidos

As seguintes limitações aplicam-se a todos os cenários.   

#### <a name="unsupported-sql-server-options-and-configurations"></a>Configurações e opções não suportadas do SQL Server

- **Grupos de disponibilidade básica**: Introduzida com o SQL Server 2016 Standard edition, grupos de disponibilidade básica não suportam acesso de leitura a réplicas secundárias. Configuração requer este acesso. Para obter mais informações, consulte [grupos de disponibilidade do servidor de SQL básico](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups?view=sql-server-2017).  

- **Instância de cluster de ativação pós-falha**: Instâncias de cluster de ativação pós-falha não são suportadas para uma réplica que utiliza com o Configuration Manager. Para obter mais informações, consulte [SQL Server Always On instâncias de cluster de ativação pós-falha](https://docs.microsoft.com/sql/sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server).  

- **MultiSubnetFailover**: Não é suportado para utilizar um grupo de disponibilidade com o Configuration Manager numa configuração com várias sub-redes. Também não é possível utilizar o [MutliSubnetFailover](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server#MultiSubnetFailover) cadeia de ligação de palavra-chave.  

#### <a name="sql-servers-that-host-additional-availability-groups"></a>Servidores SQL que alojam os grupos de disponibilidade adicionais
<!--SCCMDocs issue 649--> Quando o SQL Server aloja uma ou mais grupos de disponibilidade juntamente com o grupo que utilizar para o Configuration Manager, ele precisa de definições específicas no momento em que executa a configuração do Configuration Manager. Estas definições também são necessários para instalar uma atualização para o Configuration Manager. Cada réplica em cada grupo de disponibilidade tem de ter as seguintes configurações:

- Ativação pós-falha manual  
- Permitir todas as ligações só de leitura  

#### <a name="unsupported-database-use"></a>Utilização da base de dados não suportado

- **O Configuration Manager suporta apenas a base de dados do site num grupo de disponibilidade:** As bases de dados seguintes não são suportadas pelo Configuration Manager num grupo de disponibilidade Always On do SQL Server:  
    - Base de dados de relatórios  
    - Base de dados do WSUS  

- **Base de dados já existente:** Não é possível utilizar uma nova base de dados criada na réplica. Quando configura um grupo de disponibilidade, restaure uma cópia de uma base de dados existente do Configuration Manager para a réplica primária.  

#### <a name="setup-errors-in-configmgrsetuplog"></a>Erros de configuração em configmgrsetup. log  
Quando executar a configuração do Configuration Manager para mover uma base de dados do site para um grupo de disponibilidade, este tenta processar as funções de base de dados nas réplicas secundárias do grupo de disponibilidade. O **configmgrsetup. log** ficheiro mostra o erro seguinte:  

`ERROR: SQL Server error: [25000][3906][Microsoft][SQL Server Native Client 11.0][SQL Server]Failed to update database "CM_AAA" because the database is read-only. Configuration Manager Setup 1/21/2016 4:54:59 PM 7344 (0x1CB0)`  

Estes erros são seguros ignorar.

#### <a name="site-expansion"></a>Expansão do site
<!--SCCMDocs issue 568--> Se configurar a base de dados do site para um site primário de autónomo utilizar o SQL Always On, não é possível expandir o site para incluir um site de administração central. Se tentar este processo, falhará. Para expandir o site, remova temporariamente a base de dados do site primário do grupo de disponibilidade.



## <a name="changes-for-site-backup"></a>Alterações para cópia de segurança do site

### <a name="backup-database-files"></a>Ficheiros de cópia de segurança da base de dados
  
Quando uma base de dados do site utiliza um grupo de disponibilidade, execute o incorporado **servidor do Site de cópia de segurança** tarefa de manutenção para fazer cópias de segurança de ficheiros e definições comuns do Configuration Manager. Não utilize o. MDF ou. Ficheiros LDF criados por essa cópia de segurança. Em vez disso, torne diretas cópias de segurança destes ficheiros de base de dados usando o SQL Server.


### <a name="transaction-log"></a>Registo de transações  

Definir o modelo de recuperação de base de dados do site para **completo**. Esta configuração é um requisito para utilização do Configuration Manager num grupo de disponibilidade. Planear monitorizar e manter o tamanho do log de transação de base de dados do site. No modelo de recuperação completo, as transações não são protegidas até que o torna um completo cópia de segurança do registo de base de dados ou a transação. Para obter mais informações, consulte [fazer cópias de segurança e restauro de bases de dados do SQL Server](https://docs.microsoft.com/sql/relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases).



## <a name="changes-for-site-recovery"></a>Alterações para o site recovery

Se, pelo menos, um nó do grupo de disponibilidade ainda está funcional, utilize a opção de recuperação de site para **ignorar recuperação de base de dados (Utilize esta opção se a base de dados tiver sido afetada)**.

Quando perde todos os nós de um grupo de disponibilidade, para poder recuperar o site, primeiro recrie o grupo de disponibilidade. O Configuration Manager não consegue reconstruir ou restaurar o nó de disponibilidade. Recriar o grupo, restaurar a cópia de segurança e reconfigurar o SQL. Em seguida, utilize a opção de recuperação de site para **ignorar recuperação de base de dados (Utilize esta opção se a base de dados tiver sido afetada)**.

Para obter mais informações, consulte [cópia de segurança e recuperação](/sccm/core/servers/manage/backup-and-recovery).



## <a name="changes-for-reporting"></a>Alterações para relatórios

### <a name="install-the-reporting-service-point"></a>Instalar o ponto do service reporting

O ponto do reporting services não suporta a usando o nome virtual do serviço de escuta do grupo de disponibilidade. Também não suporta a alojar a respetiva base de dados num grupo de disponibilidade Always On do SQL Server.  

- Por predefinição, do reporting services conjuntos de instalação do ponto do **nome do servidor de base de dados de sites** para o nome virtual que é especificado como o serviço de escuta. Altere esta definição para especificar um nome de computador e instância de uma réplica no grupo de disponibilidade.  

- A descarga de relatórios e para aumentar a disponibilidade, quando um nó de réplica estiver offline, considere a instalação de pontos do reporting services adicionais em cada nó de réplica. Em seguida, configure cada ponto do reporting services para utilizar o seu próprio nome do computador. Quando instala um ponto do service reporting em todas as réplicas do grupo de disponibilidade, o reporting sempre pode ligar a um servidor de ponto de reporting Active Directory.  


### <a name="switch-the-reporting-services-point-used-by-the-console"></a>Mudar ponto do reporting services utilizado pela consola do

1. Na consola do Configuration Manager, vá para o **monitorização** área de trabalho.  

2. Expanda **Reporting** e selecione **relatórios**.  

3. Clique em **opções de relatório**.  

4. Na caixa de diálogo de opções de relatório, selecione o ponto do reporting services que pretende utilizar.  



## <a name="next-steps"></a>Passos seguintes

Este artigo descreveu os pré-requisitos, limitações e as alterações para tarefas comuns que o Configuration Manager requer quando utiliza grupos de disponibilidade. Para obter os procedimentos preparar e configurar o seu site para utilizar grupos de disponibilidade, consulte [configurar grupos de disponibilidade](/sccm/core/servers/deploy/configure/configure-aoag).
