---
title: SQL Server Always On | Microsoft Docs
description: Planear utilizar um SQL Server sempre no grupo de disponibilidade com o SCCM.
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 58d52fdc-bd18-494d-9f3b-ccfc13ea3d35
caps.latest.revision: "16"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: c746365238e1255d73387a9496521bb03a56b21b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="prepare-to-use-sql-server-always-on-availability-groups-with-configuration-manager"></a>Preparar para utilizar grupos de disponibilidade SQL Server Always On com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Prepare para utilizar o SQL Server Always On nos grupos de disponibilidade como uma solução de recuperação após desastre e disponibilidade elevada para a base de dados do site do System Center Configuration Manager.  
O Configuration Manager suporta a utilização de grupos de disponibilidade:
-     Em sites primários e o site de administração central.
-     No local, ou no Microsoft Azure.

Quando utiliza grupos de disponibilidade no Microsoft Azure, pode aumentar ainda mais a disponibilidade da sua base de dados do site utilizando *conjuntos de disponibilidade do Azure*. Para obter mais informações sobre Conjuntos de Disponibilidade do Azure, veja [Gerir a disponibilidade das máquinas virtuais](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-manage-availability/).

>  [!Important]   
>  Antes de continuar, ser confortável com a configuração do SQL Server e grupos de disponibilidade do SQL Server. As informações que se segue faz referência a biblioteca de documentação do SQL Server e procedimentos.

## <a name="supported-scenarios"></a>Cenários suportados
Seguem-se cenários suportados para utilizar grupos de disponibilidade com o Configuration Manager. Detalhes e procedimentos para cada podem ser encontrados na [configurar grupos de disponibilidade do Configuration Manager](/sccm/core/servers/deploy/configure/configure-aoag).


-      [Criar um grupo de disponibilidade para utilização com o Configuration Manager](/sccm/core/servers/deploy/configure/configure-aoag#create-and-configure-an-availability-group).
-     [Configurar um site para utilizar um grupo de disponibilidade](/sccm/core/servers/deploy/configure/configure-aoag#configure-a-site-to-use-the-database-in-the-availability-group).
-     [Adicionar ou remover membros de réplica síncrona a partir de um grupo de disponibilidade que aloja uma base de dados do site](/sccm/core/servers/deploy/configure/configure-aoag#add-and-remove-synchronous-replica-members).
-     [Configurar réplicas com consolidação assíncrona](/sccm/core/servers/deploy/configure/configure-aoag#configure-an-asynchronous-commit-repilca) (requer o Configuration Manager versão 1706 ou posterior.)
-     [Recuperar um site a partir de uma réplica de consolidação assíncrona](/sccm/core/servers/deploy/configure/configure-aoag#use-the-asynchronous-replica-to-recover-your-site) (requer o Configuration Manager versão 1706 ou posterior.)
-     [Mover uma base de dados fora de um grupo de disponibilidade para um predefinido ou com o nome de instância do SQL Server autónomo](/sccm/core/servers/deploy/configure/configure-aoag#stop-using-an-availability-group).


## <a name="prerequisites"></a>Pré-requisitos
Os seguintes pré-requisitos aplicam-se a todos os cenários. Se aplicam pré-requisitos adicionais para um cenário específico, às serão detalhadas com esse cenário.   

### <a name="configuration-manager-accounts-and-permissions"></a>O Configuration Manager contas e permissões
**Servidor do site para o acesso de membro de réplica:**   
A conta de computador do servidor do site tem de ser membro do grupo **Administradores Locais** em todos os computadores membros do grupo de disponibilidade.

### <a name="sql-server"></a>SQL Server
**Versão:**  
Cada réplica no grupo de disponibilidade tem de executar uma versão do SQL Server que é suportada pela versão do Configuration Manager. Quando suportado pelo SQL Server, outros nós de um grupo de disponibilidade podem executar diferentes versões do SQL Server.

**Edição:**  
Tem de utilizar um *Enterprise* edição do SQL Server.

**Conta:**  
Cada instância do SQL Server pode ser executado sob uma conta de utilizador de domínio (**conta de serviço**) ou uma conta de domínio. Cada réplica num grupo pode ter uma configuração diferente. Por [melhores práticas do SQL Server](/sql/sql-server/install/security-considerations-for-a-sql-server-installation#before-installing-includessnoversionincludesssnoversion-mdmd), utilizar uma conta com o mais baixo possível de permissões.

-   Para configurar as permissões para o SQL Server 2016 e contas de serviço, consulte o artigo [configurar contas de serviço do Windows e permissões](/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions) no MSDN.
-   Para utilizar uma conta de domínio, tem de utilizar certificados. Para obter mais informações, consulte [utilizar certificados para um Endpoint de espelhamento da base de dados (Transact-SQL)](https://docs.microsoft.com/sql/database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql).


Para obter mais informações consulte [criar um ponto final de espelhamento de base de dados para grupos de disponibilidade Always](/sql/database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell).

### <a name="availability-group-configurations"></a>Configurações de grupo de disponibilidade
**Membros de réplica:**  
-   O grupo de disponibilidade tem de ter uma réplica primária.
-   Antes de versão 1706, pode ter até duas réplicas secundárias síncronas.
-   A partir da versão 1706, pode utilizar o mesmo número e tipo de réplicas num grupo de disponibilidade como suportada pela versão do SQL Server que utilizar.

    Pode utilizar uma réplica de consolidação assíncrona para recuperar a réplica síncrona. Consulte [opções de recuperação de base de dados do site]( /sccm/protect/understand/backup-and-recovery#BKMK_SiteDatabaseRecoveryOption) no tópico cópia de segurança e recuperação para obter informações sobre como efetuar este procedimento.
    > [!CAUTION]  
    > O Configuration Manager não suporta a ativação pós-falha para utilizar a réplica de consolidação assíncrona como a base de dados do site.
Porque o Configuration Manager não valide o estado da réplica de consolidação assíncrona para confirmar a sua atual, e [por predefinição, este tipo uma réplica pode ser sincronizada]( https://msdn.microsoft.com/library/ff877884(SQL.120).aspx(d=robot)#Availability%20Modes), utilização de uma réplica de consolidação assíncrona, como a base de dados do site pode colocar a integridade do seu site e os dados em risco.

Tem de cada membro de réplica:
-   Utilizar a **instância predefinida**  
    *A partir da versão 1702, pode utilizar um* ***instância nomeada***.

-     Ter **ligações na função primária** definido como **Sim**
-     Ter **secundário legível** definido como **Sim**  
-     Estar definida para **Ativação Pós-falha Manual**      

    >  [!TIP]
    >  Suporte do Configuration Manager utilizando a disponibilidade de réplicas síncronas quando definidas como do grupo **ativação pós-falha automática**. No entanto, **ativação pós-falha do Manual** tem de ser definida quando:
    >  -  Execute a configuração para especificar a utilização da base de dados do site no grupo de disponibilidade.
    >  -  Quando instalar qualquer atualização para o Configuration Manager (não apenas as atualizações aplicáveis à base de dados do site).  

**Localização de membro de réplica:**  
Todas as réplicas num grupo de disponibilidade tem de ser alojado no local ou alojado no Microsoft Azure. Não é suportado um grupo que inclua um membro no local e o membro no Azure.     

Quando configurar um grupo de disponibilidade no Azure e o grupo está atrás de um balanceador de carga internos ou externos, seguem-se portas predefinidas, tem de abrir para ativar o programa de configuração acesso para cada réplica:   

-     Mapeador de pontos finais RCP - **TCP 135**   
-     Bloco de mensagem de servidor – **TCP 445**  
    *Pode remover esta porta depois de concluir a movimentação de base de dados. A partir da versão 1702, esta porta já não é necessária.*
-     SQL Server Service Broker - **TCP 4022**
-     SQL sobre TCP – **TCP 1433**   

Após a conclusão da configuração, as portas seguintes têm de permanecer acessíveis:
-     SQL Server Service Broker - **TCP 4022**
-     SQL sobre TCP – **TCP 1433**

A partir da versão 1702, pode utilizar portas personalizadas para estas configurações. As mesmas portas tem de ser utilizadas pelo ponto final e, em todas as réplicas no grupo de disponibilidade.


**Serviço de escuta:**   
O grupo de disponibilidade tem de ter, pelo menos, um **serviço de escuta do grupo de disponibilidade**. O nome virtual deste serviço de escuta é utilizado quando configurar o Configuration Manager para utilizar a base de dados do site no grupo de disponibilidade. Apesar de um grupo de disponibilidade pode conter vários serviços de escuta, o Configuration Manager só pode efetuar utilizar um. Consulte [criar ou configurar um serviço de escuta do grupo de disponibilidade (SQL Server)](/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server) para obter mais informações.

**Caminhos de ficheiro:**   
Quando executar a configuração do Configuration Manager para configurar um site para utilizar a base de dados num grupo de disponibilidade, cada servidor de réplica secundária tem de ter um caminho de ficheiro do SQL Server que é idêntico para o caminho de ficheiro para os ficheiros de base de dados do site como foi encontrado na réplica primária atual.
-   Se não existir um caminho idêntico, o programa de configuração falhará adicionar a instância para o grupo de disponibilidade como a nova localização da base de dados do site.
-   Além disso, a conta de serviço do SQL Server local tem de ter **controlo total** permissão para esta pasta.

Os servidores de réplica secundária apenas exigem este caminho de ficheiro enquanto estiver a utilizar a Configuração para especificar a instância de base de dados no grupo de disponibilidade. Depois da configuração conclui a configuração de base de dados do site no grupo de disponibilidade, pode eliminar o caminho não utilizado do secundário servidores de réplica.

Por exemplo, considere os seguintes cenários:
-   Criar um grupo de disponibilidade que utiliza três SQL Servers.

-   O servidor de réplica primária é uma nova instalação do SQL Server 2014. Por predefinição, a base de dados. MDF e. Ficheiros LDF são armazenados em C:\Program Files\Microsoft SQL Server\MSSQL12. MSSQLSERVER\MSSQL\DATA.

-   Ambos os servidores de réplica secundária foram atualizados para o SQL Server 2014 de versões anteriores e manter o caminho original do ficheiro para armazenar ficheiros de base de dados de: C:\Program Files\Microsoft SQL Server\MSSQL10. MSSQLSERVER\MSSQL\DATA.

-   Antes de tentar mover a base de dados do site a este grupo de disponibilidade, em cada servidor de réplica secundária tem de criar o seguinte caminho de ficheiro, mesmo se réplicas secundárias não irão utilizar esta localização de ficheiro: C:\Program Files\Microsoft SQL Server\MSSQL12. MSSQLSERVER\MSSQL\DATA (este é um duplicado do caminho que está a ser utilizado na réplica primária).

-   Em seguida, conceder a conta de serviço do SQL Server no acesso de controlo total cada réplica secundária para a localização do ficheiro recém-criado nesse servidor.

-   Agora pode executar a configuração do Configuration Manager para configurar o site para utilizar a base de dados do site no grupo de disponibilidade com êxito.

**Configure a base de dados numa nova réplica:**   
 A base de dados de cada réplica tem de ser definido com o seguinte:
-   **A integração do CLR** tem de ser *ativada*
-     **Tamanho máximo de repl de texto** tem de ser *2147483647*
-     O proprietário da base de dados tem de ser o *conta SA*
-     **TRUSTWORTY** tem de ser **ON**
-     **Mediador de serviço** tem de ser *ativada*

Pode efetuar estas configurações em apenas uma réplica primária. Para configurar uma réplica secundária, deve primeiro ativação pós-falha principal para secundário para tornar o secundário tornando secundário nova réplica primária.   

Utilize a documentação do SQL Server quando for necessário para o ajudar a configurar as definições. Por exemplo, consulte [TRUSTWORTHY](/sql/relational-databases/security/trustworthy-database-property) ou [integração do CLR](/sql/relational-databases/clr-integration/clr-integration-enabling) na documentação do SQL Server.

### <a name="verification-script"></a>Script de verificação
Pode executar o script seguinte para verificar as configurações de base de dados para réplicas primárias e secundárias. Pode corrigir um problema numa réplica secundária, tem de alterar essa réplica secundária a réplica primária.

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
As seguintes limitações aplicam-se a todos os cenários.   

**Grupos de disponibilidade básico não são suportados:**  
Introduzida com o SQL Server 2016 Standard edition, [grupos de disponibilidade básico](https://msdn.microsoft.com/library/mt614935.aspx) não suportam o acesso de leitura para as réplicas secundárias, um requisito para utilização com o Configuration Manager.

**Servidores SQL que alojam os grupos de disponibilidade adicionais:**   
Antes do Configuration Manager versão 1610, quando um grupo de disponibilidade em anfitriões um SQL Server um ou mais grupos de disponibilidade para além do grupo a utilizar para o Configuration Manager, cada réplica em cada um desses grupos de disponibilidade adicionais tem de ter as seguintes configurações definido no momento em que executar a configuração do Configuration Manager ou instala uma atualização para o Configuration Manager:
-   **Ativação Pós-falha Manual**
-   **permitir todas as ligações só de leitura**

**Utilização de base de dados não suportados:**
-   **O Configuration Manager suporta apenas a base de dados num grupo de disponibilidade:** Os seguintes não são suportados:
    -   Base de dados de relatórios
    -   Base de dados do WSUS
-   **Base de dados previamente existente:** Não é possível utilizar a nova base de dados criada na réplica. Em vez disso, tem de restaurar uma cópia da base de dados existente do Configuration Manager para a réplica primária quando configurar um grupo de disponibilidade.

**Erros no ficheiro configmgrsetup.log, localizado o programa de configuração:**  
Quando executar a configuração para mover uma base de dados do site para um grupo de disponibilidade, a configuração tenta processar as funções de base de dados nas réplicas secundárias do grupo de disponibilidade e regista erros, como o seguinte:
-   ERRO: Erro de servidor de SQL: [25000] [3906] [Microsoft] [SQL Server Native cliente 11.0] [SQL Server] Falha ao atualizar a base de dados "CM_AAA", porque a base de dados é só de leitura. Programa de configuração do Configuration Manager 21/1/2016 4:54 em: 59 PM 7344 (0x1CB0)  

Estes erros são seguros ignorar.

## <a name="changes-for-site-backup"></a>Alterações para cópia de segurança do site
**Ficheiros de base de dados de cópia de segurança:**  
Quando uma base de dados do site é executada num grupo de disponibilidade, deve executar incorporada **servidor do Site de cópia de segurança** tarefa de manutenção efetuar cópia de segurança comuns ficheiros e definições de Configuration Manager. No entanto, não utilize o. MDF ou. Ficheiros LDF criados por essa cópia de segurança. Em vez disso, tornar diretas cópias de segurança destes ficheiros de base de dados utilizando o SQL Server.

**Registo de transações:**  
O modelo de recuperação da base de dados do site tem de ser definido como **completa** (um requisito para utilização num grupo de disponibilidade). Com esta configuração, planeie a monitorizar e manter o tamanho do registo de transações de base de dados do site. No modelo de recuperação completa, as transações não são protegidas até ser feita uma cópia de segurança completa da base de dados ou do registo de transações. Consulte [cópia de segurança e restauro de bases de dados](/sql/relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases) na documentação do SQL Server para obter mais informações.

## <a name="changes-for-site-recovery"></a>Alterações para a recuperação de site
Pode utilizar a opção de recuperação de site **ignorar recuperação de base de dados (Utilize esta opção se a base de dados do site não tiver sido afetada)** se pelo menos um nó do grupo de disponibilidade permaneça funcional.

 Para poder recuperar o site quando todos os nós de um grupo de disponibilidade tem sido perdidos, tem de recriar o grupo de disponibilidade. O Configuration Manager não consegue reconstruir ou restaurar o nó de disponibilidade. Depois do grupo é recriado e uma cópia de segurança restaurada e reconfigurada, em seguida, pode utilizar a opção de recuperação de site **ignorar recuperação de base de dados (Utilize esta opção se a base de dados do site não tiver sido afetada)**.

Para obter mais informações, consulte [cópia de segurança e recuperação para o System Center Configuration Manager](/sccm/protect/understand/backup-and-recovery).

## <a name="changes-for-reporting"></a>Alterações para relatórios
**Instale o ponto de serviço Reporting Services:**  
Ponto do reporting services não suporta a utilizar o nome virtual do serviço de escuta do grupo de disponibilidade ou o alojamento de base de dados do Reporting Services num grupo de disponibilidade SQL Server Always On:
-   Por predefinição, do Reporting Services conjuntos de instalação do ponto de **nome do servidor de base de dados de sites** para o nome virtual que está especificado como o serviço de escuta. Altere esta opção para especificar um nome de computador e a instância de uma réplica no grupo de disponibilidade.
-   Para descarregar a carga de relatórios e para aumentar a disponibilidade, quando um nó de réplica estiver offline, considere a instalação de pontos do Reporting Services em cada nó de réplica e configurar cada do Reporting Services ponto a ponto para o seu próprio nome de computador adicionais.

Quando instala um ponto de serviço Reporting Services em cada réplica do grupo de disponibilidade, Reporting Services podem sempre ligar a um servidor de ponto de Reporting Services Active Directory.

**Mude ponto do reporting services utilizado pela consola:**  
Para executar relatórios, na consola do aceda a **monitorização** > **descrição geral** > **reporting** > **relatórios**e, em seguida, escolha **opções de relatórios**. Na caixa de diálogo Opções de relatório, selecione o ponto do Reporting Services pretendido.

## <a name="next-steps"></a>Passos seguintes
Depois de compreender os pré-requisitos, limitações e as alterações para tarefas comuns que são necessárias quando utiliza grupos de disponibilidade, consulte o artigo [configurar grupos de disponibilidade do Configuration Manager](/sccm/core/servers/deploy/configure/configure-aoag), para obter os procedimentos definir e configurar o seu site para utilizar grupos de disponibilidade.
