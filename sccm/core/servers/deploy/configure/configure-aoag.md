---
title: Configurar grupos de disponibilidade | Microsoft Docs
description: Configurar e gerenciar grupos sempre na disponibilidade do SQL Server com o SCCM.
ms.custom: na
ms.date: 5/26/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 7e4ec207-bb49-401f-af1b-dd705ecb465d
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: dc221ddf547c43ab1f25ff83c3c9bb603297ece6
ms.openlocfilehash: 138834b6cc64332202256961ad1d2f5ab6d176db
ms.contentlocale: pt-pt
ms.lasthandoff: 06/01/2017


---
# <a name="configure-sql-server-always-on-availability-groups-for-configuration-manager"></a>Configurar grupos de disponibilidade do SQL Server Always On do Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

Use as informações neste tópico para configurar e gerenciar os grupos de disponibilidade que você usa com o Configuration Manager.

Antes de começar:  
-   Familiarize-se com as informações do [preparar para usar grupos de disponibilidade do SQL Server Always On com o Configuration Manager](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).
-   Familiarize-se com a documentação do SQL Server que abrange o uso de grupos de disponibilidade e procedimentos relacionados que são necessárias para concluir os cenários a seguir.

> [!TIP]  
>  Links deste tópico para o SQL Server acessem conteúdo para o SQL Server 2016. Se você não usar essa versão do SQL Server, consulte a documentação para obter a versão que você usa.

## <a name="create-and-configure-an-availability-group"></a>Criar e configurar um grupo de disponibilidade
Use o procedimento a seguir para criar um grupo de disponibilidade e, em seguida, mova uma cópia do banco de dados do site para o grupo de disponibilidade.

Para concluir este procedimento, a conta usada deve ser:
-   Membro de **administradores locais** grupo em cada computador que será o grupo de disponibilidade.
-   Um **sysadmin** em cada instância do SQL Server que hospedará o banco de dados do site.

### <a name="to-create-and-configure-an-availability-group-for-configuration-manager"></a>Para criar e configurar um grupo de disponibilidade para o Configuration Manager  
1.    Use o seguinte comando para interromper o site do Configuration Manager: **Preinst.exe /stopsite**. Para obter mais informações sobre como usar o Preinst.exe, consulte [ferramenta de manutenção de hierarquia](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe).

2.    Altere o modelo de cópia de segurança para a base de dados do site de **SIMPLES** para **COMPLETA**.
Veja [Ver ou Alterar o Modelo de Recuperação de uma Base de Dados](/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server) na documentação do SQL Server. (Os grupos de disponibilidade só suportam COMPLETA).

3.    Usar o SQL Server para criar um backup completo do seu banco de dados do site e, em seguida, siga um destes procedimentos, dependendo se o servidor que hospeda seu banco de dados do site será um membro de réplica do novo grupo de disponibilidade ou não:
    -   **Será membro de seu grupo de disponibilidade:**  
        Se você usar esse servidor como o membro de réplica primária inicial do grupo de disponibilidade, você não precisa restaurar uma cópia do banco de dados do site para este ou outro servidor no grupo. O banco de dados já estarão em vigor na réplica primária, e o SQL Server serão replicadas do banco de dados para as réplicas secundárias durante uma etapa posterior.  

      -    **Não será um membro do grupo de disponibilidade:**   
    Você deve restaurar uma cópia do banco de dados do site para o servidor que hospedará a réplica primária do grupo.

    Para obter informações sobre como concluir essa etapa, consulte [criar um Backup completo do banco de dados](/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server) e [restaurar um Backup de banco de dados usando o SSMS](/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)na documentação do SQL Server.

4.    No servidor que hospedará a réplica primária inicial do grupo, use o [Assistente de novo grupo de disponibilidade](/sql/database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio) para criar o grupo de disponibilidade. No assistente:
      -    Sobre o **Selecionar banco de dados** , selecione o banco de dados para que o site do Configuration Manager.  

      -    Na página **Especificar Réplicas** , configure:
          -    **Réplicas:** Especifique os servidores que hospedam réplicas secundárias.

          -    **Ouvinte:** Especifique o **nome DNS do ouvinte** como um nome DNS completo, como  **&lt;Listener_Server >. c o m**. Isso é usado quando você configurar o Configuration Manager para usar o banco de dados no grupo de disponibilidade.

      -    Na página **Selecionar Sincronização de Dados Inicial** , selecione **Completa**. Depois que o assistente cria o grupo de disponibilidade, o Assistente de backup do log de transações e de banco de dados primário e, em seguida, restaurá-los em cada servidor que hospeda uma réplica secundária. (Se você não usar essa etapa, você precisará restaurar uma cópia do banco de dados do site em cada servidor que hospeda uma réplica secundária e unir manualmente esse banco de dados ao grupo.)   

5.    Verifique a configuração em cada réplica:   
  1.    Certifique-se de que a conta de computador do servidor do site é um membro do **administradores locais** grupo em cada computador que seja membro do grupo de disponibilidade.  

  2.  Execute o [script verificação](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#prerequisites) dos pré-requisitos para confirmar se o banco de dados do site em cada réplica está configurado corretamente.

  3.    Se for necessário definir configurações em réplicas secundárias, você deve manualmente o failover da réplica primária para a réplica secundária antes de continuar porque você só pode configurar o banco de dados de uma réplica primária. Para obter mais informações, consulte [realizar um Failover de Manual planejado de um grupo de disponibilidade](/sql/database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server) na documentação do SQL Server.

6.    Depois que todas as réplicas de atender aos requisitos, o grupo de disponibilidade está pronto para ser usado com o Configuration Manager.

## <a name="configure-a-site-to-use-the-database-in-the-availability-group"></a>Configurar um site para usar o banco de dados no grupo de disponibilidade
Depois que você [criar e configurar o grupo de disponibilidade](#create-and-configure-an-availability-group), use a manutenção de site do Configuration Manager para configurar o site para usar o banco de dados que é hospedado pelo grupo de disponibilidade.

Não há suporte para instalar um novo site com o seu banco de dados em um grupo de disponibilidade. Por exemplo, se você usar a mídia de 1702 de linha de base, você deve instalar o site usando uma única instância do SQL Server. Depois de instalar o site, você pode mover o banco de dados do site para o grupo de disponibilidade.

Para concluir este procedimento, a conta usada para executar a instalação do Configuration Manager deve ser:
-   Membro de **administradores locais** grupo em cada computador que seja membro do grupo de disponibilidade.
-   Um **sysadmin** em cada instância do SQL Server que hospeda o banco de dados do site.

> [!IMPORTANT]
> Quando você usa o Microsoft Intune com o Configuration Manager em uma configuração híbrida, mover o banco de dados do site de ou para um grupo de disponibilidade dispara uma ressincronização de dados com a nuvem. Isso não pode ser evitado.

### <a name="to-configure-a-site-to-use-the-availability-group"></a>Para configurar um site para usar o grupo de disponibilidade
1.    Executar **instalação do Configuration Manager** de  **&lt;* pasta de instalação de site do Configuration Manager*> \BIN\X64\setup.exe**.

2.    Na página **Introdução** , selecione **Executar a manutenção do site ou repor este site**e clique em **Seguinte**.

3.    Selecione a opção **Modificar a configuração do SQL Server** e clique em **Seguinte**.

4.    Reconfigure as seguintes opções para a base de dados do site:
    -   **Nome do SQL Server:** Insira o nome virtual para o grupo de disponibilidade **ouvinte** que configurado ao criar o grupo de disponibilidade. O nome virtual deve ser um nome DNS completo, como  **&lt;* ponto*>. fabrikam.com**.  

    -   **Instância:** Esse valor deve estar em branco para especificar a instância padrão para o *ouvinte* do grupo de disponibilidade. Se o banco de dados do site atual estiver instalado em uma instância nomeada, a instância nomeada será listada e deverá ser apagada.

    -   **Banco de dados:** Deixe o nome como ele aparece. Este é o nome da base de dados do site atual.

5.    Depois de fornecer estas informações para a nova localização da base de dados, conclua a Configuração com o procedimento e configurações normais.



## <a name="add-and-remove-replica-members"></a>Adicionar e remover membros de réplica  
Quando o banco de dados do site é hospedado em um grupo de disponibilidade, use os procedimentos a seguir para adicionar ou remover membros de réplica. Configuration Manager dá suporte a um único primário e até dois nós secundários.

Para concluir os procedimentos a seguir, a conta usada deve ser:
-   Membro de **administradores locais** grupo em cada computador que seja membro do grupo de disponibilidade.
-   Um **sysadmin** em cada servidor de SQL que hospeda ou hospedará o banco de dados do site.


### <a name="to-add-a-new-replica-member"></a>Para adicionar um novo membro de réplica
1.    Adicione o novo servidor como réplica secundária ao grupo de disponibilidade. Consulte [adicionar uma réplica secundária a um grupo de disponibilidade (SQL Server)](/sql/database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server) na biblioteca de documentação do SQL Server.

2.    Parar o site do Configuration Manager executando **Preinst.exe /stopsite**. Consulte [ferramenta de manutenção de hierarquia](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe).

3.    Utilize o SQL Server para criar uma cópia de segurança da base de dados do site a partir da réplica primária e, em seguida, restaure essa cópia de segurança para o novo servidor de réplica secundária. Consulte [criar um Backup completo do banco de dados](/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server) e [restaurar um Backup de banco de dados usando o SSMS](/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms) na documentação do SQL Server.

4.    Configure cada réplica secundária. Efetue as seguintes ações para cada réplica secundária no grupo de disponibilidade:

    1.    Certifique-se de que a conta de computador do servidor do site é um membro do **administradores locais** grupo em cada computador que seja membro do grupo de disponibilidade.

    2.    Execute o [script verificação](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#prerequisites) dos pré-requisitos para confirmar se o banco de dados do site em cada réplica está configurado corretamente.

    3.    Se é necessário configurar manualmente o failover da réplica primária para a nova réplica secundária, a nova réplica e, em seguida, verifique as configurações necessárias. Veja [Executar uma Ativação Pós-falha Manual Planeada de um Grupo de Disponibilidade](/sql/database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server) na documentação do SQL Server.

5.    Reinicie o site, iniciando os serviços (**sitecomp**) e **SMS_Executive** do Gestor de Componentes do Site.

### <a name="to-remove-a-replica-member"></a>Para remover um membro de réplica
Para esse procedimento, use as informações em [remover uma réplica secundária de um grupo de disponibilidade](/sql/database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server) na documentação do SQL Server.

## <a name="stop-using-an-availability-group"></a>Parar de usar um grupo de disponibilidade
Utilize o procedimento seguinte quando já não pretender alojar a base de dados do site num grupo de disponibilidade. Isso envolve a mudança do banco de dados do site novamente para uma única instância do SQL Server.

Para concluir este procedimento, a conta usada deve ser:
-   Membro de **administradores locais** grupo em cada computador que seja membro do grupo de disponibilidade
-   Um **sysadmin** em cada instância do SQL Server que hospeda o banco de dados do site.

> [!IMPORTANT]  
> Quando você usa o Microsoft Intune com o Configuration Manager em uma configuração híbrida, mover o banco de dados do site de ou para um grupo de disponibilidade dispara uma ressincronização de dados com a nuvem. Isso não pode ser evitado.

### <a name="to-move-the-site-database-from-an-availability-group-back-to-a-single-instance-sql-server"></a>Para mover a base de dados do site de um grupo de disponibilidade de volta para um SQL Server de instância única
1.    Pare o site do Configuration Manager usando o seguinte comando: **Preinst.exe /stopsite**. Para obter mais informações, consulte [ferramenta de manutenção de hierarquia](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe).

2.    Utilize o SQL Server para criar uma cópia de segurança completa da sua base de dados do site a partir da réplica primária. Para obter informações sobre como executar este passo, veja [Criar uma Cópia de Segurança Completa da Base de Dados](/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server) na documentação do SQL Server.

3.    Se o servidor que é a réplica primária do grupo de disponibilidade hospedará a instância única do banco de dados do site, você poderá ignorar esta etapa:  

    -   Utilize o SQL Server para restaurar a cópia de segurança da base de dados do site para o servidor que irá aloja a base de dados do site. Consulte [restaurar um Backup de banco de dados usando o SSMS](/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms) na documentação do SQL Server.   <br />  <br />

4.    No servidor que hospedará o banco de dados do site (a réplica primária, ou o servidor onde você restaurou o banco de dados do site), altere o modelo de backup de dados do site de **completo** para **simples**. Veja [Ver ou Alterar o Modelo de Recuperação de uma Base de Dados](/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server) na documentação do SQL Server.  

5.    Executar **instalação do Configuration Manager** de  **&lt;* pasta de instalação de site do Configuration Manager >*\BIN\X64\setup.exe**.

6.    Na página **Introdução** , selecione **Executar a manutenção do site ou repor este site**e clique em **Seguinte**.  

7.    Selecione a opção **Modificar a configuração do SQL Server** e clique em **Seguinte**.  

8.    Reconfigure as seguintes opções para a base de dados do site:
    -   **Nome do SQL Server:** Digite o nome do servidor que agora hospeda o banco de dados do site.

    -   **Instância:** Especifique a instância nomeada que hospeda o banco de dados do site ou deixe em branco se o banco de dados na instância padrão.

    -   **Banco de dados:** Deixe o nome como ele aparece. Este é o nome da base de dados do site atual.    

9.    Depois de fornecer estas informações para a nova localização da base de dados, conclua a Configuração com o procedimento e configurações normais. Quando tiver concluído a Configuração, o site é reiniciado e começa a utilizar a nova localização da base de dados.    

10.    Para limpar os servidores que eram membros do grupo de disponibilidade, siga as orientações em [Remover um Grupo de Disponibilidade](/sql/database-engine/availability-groups/windows/remove-an-availability-group-sql-server) na documentação do SQL Server.

