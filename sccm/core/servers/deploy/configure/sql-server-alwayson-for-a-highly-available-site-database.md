---
title: SQL Server AlwaysOn | Microsoft Docs
description: Planeje usar um grupo sempre na disponibilidade do SQL Server com o SCCM.
ms.custom: na
ms.date: 5/26/2017
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
ms.sourcegitcommit: dc221ddf547c43ab1f25ff83c3c9bb603297ece6
ms.openlocfilehash: 188ae877368a6cb2ec9998bff74259b4e5b5e7ce
ms.contentlocale: pt-pt
ms.lasthandoff: 06/01/2017


---
# <a name="prepare-to-use-sql-server-always-on-availability-groups-with-configuration-manager"></a>Preparar para usar grupos de disponibilidade do SQL Server Always On com o Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

Prepare o System Center Configuration Manager para usar grupos de disponibilidade do SQL Server Always On como uma solução de recuperação de desastres e disponibilidade alta para o banco de dados do site.  
Configuration Manager dá suporte usando grupos de disponibilidade:
-     Em sites primários e o site de administração central.
-     No local, ou no Microsoft Azure.

Quando você usa grupos de disponibilidade no Microsoft Azure, você pode aumentar ainda mais a disponibilidade do seu banco de dados do site usando *conjuntos de disponibilidade do Azure*. Para obter mais informações sobre Conjuntos de Disponibilidade do Azure, veja [Gerir a disponibilidade das máquinas virtuais](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-manage-availability/).

>  [!Important]   
>  Antes de continuar, esteja familiarizado com a configuração do SQL Server e grupos de disponibilidade do SQL Server. As informações a seguir faz referência a biblioteca de documentação do SQL Server e procedimentos.

## <a name="supported-scenarios"></a>Cenários suportados
A seguir estão os cenários com suporte para usar grupos de disponibilidade com o Configuration Manager. Detalhes e procedimentos para cada um podem ser encontrados em [configurar grupos de disponibilidade para o Configuration Manager](/sccm/core/servers/deploy/configure/configure-aoag).


-      [Criar um grupo de disponibilidade para uso com o Configuration Manager](/sccm/core/servers/deploy/configure/configure-aoag#create-and-configure-an-availability-group).
-     [Configurar um site para usar um grupo de disponibilidade](/sccm/core/servers/deploy/configure/configure-aoag#configure-a-site-to-use-the-database-in-the-availability-group).
-     [Adicionar ou remover membros de réplica de um grupo de disponibilidade que hospeda um banco de dados do site](/sccm/core/servers/deploy/configure/configure-aoag#add-and-remove-replica-members).
-     [Mover um banco de dados fora de um grupo de disponibilidade para um padrão ou instância nomeada de um SQL Server autônomo](/sccm/core/servers/deploy/configure/configure-aoag#stop-using-an-availability-group).


## <a name="prerequisites"></a>Pré-requisitos
Os pré-requisitos a seguir se aplicam a todos os cenários. Se os pré-requisitos adicionais se aplicam a um cenário específico, aqueles serão detalhadas com esse cenário.   

### <a name="configuration-manager-accounts-and-permissions"></a>Permissões e contas do configuration Manager
**Servidor do site para acesso de membro de réplica:**   
A conta de computador do servidor do site tem de ser membro do grupo **Administradores Locais** em todos os computadores membros do grupo de disponibilidade.

### <a name="sql-server"></a>SQL Server
**Versão:**  
Cada réplica no grupo de disponibilidade deve executar uma versão do SQL Server que é compatível com sua versão do Configuration Manager. Quando o suporte do SQL Server, nós diferentes de um grupo de disponibilidade podem executar versões diferentes do SQL Server.

**Edição:**  
Você deve usar um *Enterprise* edição do SQL Server.

**Conta:**  
Cada instância do SQL Server pode ser executado sob uma conta de usuário de domínio (**conta de serviço**) ou **sistema Local**. Cada réplica em um grupo pode ter uma configuração diferente. Por [práticas recomendadas do SQL Server](/sql/sql-server/install/security-considerations-for-a-sql-server-installation#before-installing-includessnoversionincludesssnoversion-mdmd), use uma conta com as menores permissões possíveis.

Por exemplo, para configurar contas de serviço e permissões para o SQL Server 2016, consulte [configurar contas de serviço do Windows e permissões](/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions) no MSDN.

  Se você usar **sistema Local** para executar uma réplica, você deve configurar a autenticação de ponto de extremidade. Isso inclui a delegação de direitos para habilitar uma conexão para o ponto de extremidade do servidor de réplica.
  -     Delegar os direitos do SQL Server, adicionando a conta de computador de cada SQL Server como um logon nos outros servidores SQL no nó e conceder essa conta direitos SA.  
  -     Delegar os direitos de ponto de extremidade para cada servidor remoto no ponto de extremidade local executando o seguinte script em cada réplica:    

              GRANT CONNECT ON endpoint::[endpoint_name]  
              TO [domain\servername$]

Para obter mais informações, consulte [criar um ponto de extremidade de espelhamento de banco de dados para grupos de disponibilidade AlwaysOn](/sql/database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell).

### <a name="availability-group-configurations"></a>Configurações de grupo de disponibilidade
**Membros de réplica:**  
O grupo de disponibilidade deve ter uma réplica primária e pode ter até duas réplicas secundárias síncronas.  Cada membro de réplica deve:
-   Utilizar a **instância predefinida**  
    *A partir da versão 1702, você pode usar um* ***instância nomeada***.

-      Ter **conexões na função primária** definida como **Sim**
-      Ter **secundária legível** definida como **Sim**  
-      Estar definida para **Ativação Pós-falha Manual**       

    >  [!TIP]
    >  Configuration Manager oferece suporte ao uso de réplicas de grupo de disponibilidade quando definidas como **Failover automático**. No entanto, **Failover Manual** deve ser definido quando:
    >  -  Execute a instalação para especificar o uso do banco de dados do site no grupo de disponibilidade.
    >  -  Quando você instala qualquer atualização para o Configuration Manager (não apenas as atualizações que se aplicam ao banco de dados do site).  

**Local do membro de réplica:**  
Todas as réplicas de um grupo de disponibilidade devem ser hospedado no local ou hospedado no Microsoft Azure. Não há suporte para um grupo que inclui um membro local e um membro no Azure.     

Quando você configurar um grupo de disponibilidade no Azure e o grupo estiver atrás de um balanceador de carga internos ou externos, esses são portas padrão precisam ser abertas para habilitar o acesso de instalação para cada réplica:   

-      Mapeador de ponto de extremidade RCP - **TCP 135**   
-      Server Message Block – **TCP 445**  
    *Você pode remover essa porta após a movimentação do banco de dados. A partir da versão 1702, essa porta não é mais necessária.*
-      SQL Server Service Broker - **TCP 4022**
-      SQL sobre TCP – **TCP 1433**   

Após a conclusão da instalação, as seguintes portas devem permanecer acessíveis:
-      SQL Server Service Broker - **TCP 4022**
-      SQL sobre TCP – **TCP 1433**

A partir da versão 1702, você pode usar portas personalizadas para essas configurações. As mesmas portas devem ser usadas pelo ponto de extremidade e em todas as réplicas no grupo de disponibilidade.


**Ouvinte:**   
O grupo de disponibilidade tem de ter, pelo menos, um **serviço de escuta do grupo de disponibilidade**. O nome virtual desse ouvinte é usado quando você configura o Configuration Manager para usar o banco de dados do site no grupo de disponibilidade. Embora um grupo de disponibilidade possa conter vários ouvintes, o Configuration Manager só pode fazer uso de um. Consulte [criar ou configurar um ouvinte de grupo de disponibilidade (SQL Server)](/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server) para obter mais informações.

**Caminhos de arquivo:**   
Quando você executar a instalação do Configuration Manager para configurar um site para usar o banco de dados em um grupo de disponibilidade, cada servidor de réplica secundária deve ter um caminho de arquivo do SQL Server que é idêntico ao caminho do arquivo para os arquivos de banco de dados do site como encontradas na réplica primária atual.
-   Se não existir um caminho idêntico, a instalação falhará ao adicionar a instância do grupo de disponibilidade como o novo local do banco de dados do site.
-   Além disso, a conta de serviço local do SQL Server deve ter **controle total** permissão para esta pasta.

Os servidores de réplica secundária apenas exigem este caminho de ficheiro enquanto estiver a utilizar a Configuração para especificar a instância de base de dados no grupo de disponibilidade. Após a instalação conclui a configuração do banco de dados de site no grupo de disponibilidade, você pode excluir o caminho não utilizado de secundário os servidores de réplica.

Por exemplo, considere os seguintes cenários:
-    Criar um grupo de disponibilidade que usa três SQL Servers.

-    O servidor de réplica primária é uma nova instalação do SQL Server 2014. Por padrão, o banco de dados. MDF e. Arquivos LDF são armazenados no Server \ mssql12 do C:\Program Files\Microsoft SQL. MSSQLSERVER\MSSQL\DATA.

-    Ambos os servidores de réplica secundária foram atualizados para o SQL Server 2014 de versões anteriores e mantém o caminho do arquivo original para armazenar arquivos de banco de dados do: C:\Program Files\Microsoft SQL Server\MSSQL10. MSSQLSERVER\MSSQL\DATA.

-    Antes de tentar mover o banco de dados do site para esse grupo de disponibilidade, em cada servidor de réplica secundária você deve criar o seguinte caminho de arquivo mesmo se as réplicas secundárias não usará o local do arquivo: Server \ mssql12 SQL de Programas\Microsoft C:\Program. MSSQLSERVER\MSSQL\DATA (Esta é uma duplicata do caminho que está em uso na réplica primária).

-    Você, em seguida, conceder a conta de serviço do SQL Server em cada réplica secundária completa controlar o acesso ao local do arquivo criado recentemente no servidor.

-    Agora você pode executar com êxito a instalação do Configuration Manager para configurar o site para usar o banco de dados do site no grupo de disponibilidade.

**Configure o banco de dados em uma nova réplica:**   
 O banco de dados de cada réplica deve ser definido com o seguinte:
-     **Integração CLR** devem ser *habilitado*
-      **Tamanho máximo de repl de texto** devem ser *2147483647*
-      O proprietário do banco de dados deve ser o *conta SA*
-      **TRUSTWORTY** devem ser **ON**
-      **O Service Broker** devem ser *habilitado*

Você pode fazer essas configurações em apenas uma réplica primária. Para configurar uma réplica secundária, você deve primeiro o primário para o secundário para tornar o secundário que torna a nova réplica primária de secundário de failover.   

Use a documentação do SQL Server, quando necessário, para ajudá-lo a definir as configurações. Por exemplo, consulte [TRUSTWORTHY](/sql/relational-databases/security/trustworthy-database-property) ou [integração CLR](/sql/relational-databases/clr-integration/clr-integration-enabling) na documentação do SQL Server.

### <a name="verification-script"></a>Script de verificação
Você pode executar o script a seguir para verificar as configurações de banco de dados para réplicas primárias e secundárias. Antes de você pode corrigir um problema em uma réplica secundária, você deve alterar essa réplica secundária para ser a réplica primária.

    SET NOCOUNT ON

    DECLARE @dbname NVARCHAR(128)

    SELECT @dbname = sd.name FROM sys.sysdatabases sd WHERE sd.dbid = DB_ID()

    IF (@dbname = N'master' OR @dbname = N'model' OR @dbname = N'msdb' OR @dbname = N'tempdb' OR @dbname = N'distribution' ) BEGIN
    RAISERROR(N'ERROR: Script is targetting a system database.  It should be targeting the DB you created instead.', 0, 1)
    GOTO Branch_Exit;
    END ELSE
    PRINT N'INFO: Targetted database is ' + @dbname + N'.'

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

## <a name="limitations-and-known-issues"></a>Limitações e problemas conhecidos
As seguintes limitações se aplicam a todos os cenários.   

**Não há suporte para grupos de disponibilidade básica:**  
Introduzido com o SQL Server 2016 Standard edition, [grupos de disponibilidade básica](https://msdn.microsoft.com/library/mt614935.aspx) não oferecem suporte a acesso de leitura a réplicas secundárias, um requisito para uso com o Configuration Manager.

**Servidores SQL que hospedam os grupos de disponibilidade adicional:**   
Antes do Configuration Manager versão 1610, quando um grupo de disponibilidade em um host do SQL Server que um ou mais grupos de disponibilidade, além do grupo que você usa para o Configuration Manager, cada réplica em cada um desses grupos de disponibilidade adicional devem ter as seguintes configurações definida no momento em que você execute a instalação do Configuration Manager ou instala uma atualização para o Configuration Manager:
-   **Ativação Pós-falha Manual**
-     **permitir todas as ligações só de leitura**

**Uso do banco de dados não são suportados:**
-   **Configuration Manager dá suporte a apenas o banco de dados do site em um grupo de disponibilidade:** O exemplo a seguir não têm suporte:
    -   Base de dados de relatórios
    -   Banco de dados do WSUS
-   **O banco de dados já existente:** Você não pode usar o novo banco de dados que criou na réplica. Em vez disso, você deve restaurar uma cópia de um banco de dados existente do Configuration Manager para a réplica primária ao configurar um grupo de disponibilidade.

**Erros de instalação em ConfigMgrSetup.log:**  
Quando você executa a instalação para mover um banco de dados do site para um grupo de disponibilidade, a instalação tenta processar funções de banco de dados nas réplicas secundárias do grupo de disponibilidade e logs de erros, como o seguinte:
-   ERRO: Erro do SQL Server: [25000] [3906] [Microsoft] [SQL Server Native Client 11.0] [SQL Server] Falha ao atualizar o banco de dados "CM_AAA" porque o banco de dados é somente leitura. Gerenciador de configurações de instalação 1/21/2016 4:54:59 PM 7344 (0x1CB0)  

Esses erros são seguros ignorar.

## <a name="changes-for-site-backup"></a>Alterações para o backup do site
**Arquivos de backup do banco de dados:**  
Quando um banco de dados do site é executado em um grupo de disponibilidade, você deve executar o interno **servidor do Site de Backup** tarefas de manutenção para fazer backup de arquivos e configurações do Gerenciador de configuração comuns. No entanto, não use o. MDF ou. Arquivos LDF criados por esse backup. Em vez disso, fazer backups diretos desses arquivos de banco de dados usando o SQL Server.

**Log de transações:**  
O modelo de recuperação do banco de dados do site deve ser definido como **completo** (um requisito para uso em um grupo de disponibilidade). Com essa configuração, planeje monitorar e manter o tamanho do log de transações de banco de dados de site. No modelo de recuperação completa, as transações não são protegidas até ser feita uma cópia de segurança completa da base de dados ou do registo de transações. Consulte [Back Up and Restore of SQL Server Databases](/sql/relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases) na documentação do SQL Server para obter mais informações.

## <a name="changes-for-site-recovery"></a>Alterações para a recuperação de site
Você pode usar a opção de recuperação de site **ignorar a recuperação do banco de dados (Use esta opção se o banco de dados do site tiver sido afetado)** se pelo menos um nó do grupo de disponibilidade permaneça funcionando.

 Antes de recuperar o site quando todos os nós de um grupo de disponibilidade tiveram sido perdidos, você deve recriar o grupo de disponibilidade. Gerenciador de configuração não pode recriar nem restaurar o nó de disponibilidade. Depois que o grupo é recriado, e um backup restaurado e reconfigurado, você pode usar a opção de recuperação de site **ignorar a recuperação do banco de dados (Use esta opção se o banco de dados do site tiver sido afetado)**.

Para obter mais informações, consulte [Backup e recuperação para o System Center Configuration Manager](/sccm/protect/understand/backup-and-recovery).

## <a name="changes-for-reporting"></a>Alterações para relatórios
**Instale o ponto do reporting service:**  
O ponto do reporting services não oferece suporte usando o nome virtual do ouvinte do grupo de disponibilidade ou o que hospeda o banco de dados de serviços de relatórios em um grupo de disponibilidade do SQL Server Always On:
-   Por padrão, o reporting services conjuntos de instalação do ponto de **nome do servidor de banco de dados de Site** para o nome virtual que é especificado como o ouvinte. Altere essa opção para especificar um nome de computador e a instância de uma réplica no grupo de disponibilidade.
-   Para descarregar a carga de emissão de relatórios e para aumentar a disponibilidade quando um nó de réplica estiver offline, considere a instalação de pontos do reporting services em cada nó de réplica adicional e configurando o cada ponto a ponto para seu próprio nome de computador do reporting services.

Quando você instala um ponto do reporting service em cada réplica do grupo de disponibilidade, relatórios sempre podem se conectar a um servidor ativo de ponto de relatório.

**Alterne o ponto do reporting services usado pelo console do:**  
Para executar relatórios, no console, vá para **monitoramento** > **visão geral** > **reporting** > **relatórios**e, em seguida, escolha **opções de relatório**. Na caixa de diálogo Opções de relatório, selecione o ponto do reporting services desejado.

## <a name="next-steps"></a>Passos seguintes
Depois de entender os pré-requisitos, limitações e as alterações para tarefas comuns que são necessárias quando você usa grupos de disponibilidade, consulte [configurar grupos de disponibilidade para o Configuration Manager](/sccm/core/servers/deploy/configure/configure-aoag), para os procedimentos para instalar e configurar seu site para usar grupos de disponibilidade.

