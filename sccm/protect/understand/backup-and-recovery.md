---
title: "Cópia de segurança e recuperação | Documentos do Microsoft"
description: "Saiba como criar cópias de segurança e recuperar os seus sites em caso de falha ou perda de dados no System Center Configuration Manager."
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7832d83-9ae2-4530-8a77-790e0845e12f
caps.latest.revision: 22
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: ea6668ee7ee6b209b659426a0dc2c0be605ceaf1
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---

# <a name="backup-and-recovery"></a>Cópia de segurança e recuperação

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Prepare a cópia de segurança e recuperação abordagens para evitar a perda de dados. Para sites do Configuration Manager, uma abordagem de cópia de segurança e recuperação pode ajudar a recuperar sites e hierarquias mais rapidamente e com as perdas de dados. As secções deste tópico podem ajudar a criar uma cópia de segurança as sites e recuperar um site em caso de falha ou perda de dados.  



- [Efetuar uma Cópia de Segurança de um Site do Gestor de Configuração](#BKMK_SiteBackup)   

  - [Tarefa de manutenção de cópias de segurança](#BKMK_BackupMaintenanceTask)   

  - [Utilizar o Data Protection Manager para efetuar cópias de segurança da base de dados do site](#BKMK_DPMBackup)   

  -  [Arquivar o instantâneo de cópia de segurança](#BKMK_ArchivingBackupSnapshot)   

  -  [Utilizar o Ficheiro AfterBackup.bat](#BKMK_UsingAfterBackup)   

  -  [Tarefas suplementares de cópia de segurança](#BKMK_SupplementalBackup)   

-  [Recuperar um site do Gestor de Configuração](#BKMK_RecoverSite)   

  -   [Determinar as opções de recuperação](#BKMK_DetermineRecoveryOptions)   

         -   [Opções de recuperação do servidor do site](#BKMK_SiteServerRecoveryOptions)   

         -   [Opções de recuperação da base de dados do site](#BKMK_SiteDatabaseRecoveryOption)   

         -   [Período de retenção do registo de alterações do SQL Server](#bkmk_SQLretention)   

         -   [Processo para reinicializar um site ou dados globais](#bkmk_reinit)   

         -   [Cenários de recuperação de bases de dados de site](#BKMK_SiteDBRecoveryScenarios)  

  -   [Chaves de ficheiro de script de recuperação automática de site](#BKMK_UnattendedSiteRecoveryKeys)  

  -   [Tarefas de pós-recuperação](#BKMK_PostRecovery)  

  -   [Recuperar um site secundário](#BKMK_RecoverSecondarySite)  

-   [Serviço SMS Writer](#BKMK_SMSWriterService)  

> [!NOTE]  
>  Se utilizar um grupo de Disponibilidade AlwaysOn do SQL Server para alojar a base de dados do site, modifique os planos de cópia de segurança e recuperação conforme descrito no [as alterações à cópia de segurança e recuperação quando utilizar um grupo de Disponibilidade AlwaysOn do SQL Server](../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#bkmk_BnR) secção a [SQL Server AlwaysOn numa base de dados do site elevada para o System Center Configuration Manager](../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md) tópico.  

##  <a name="BKMK_SiteBackup"></a> Efetuar uma Cópia de Segurança de um Site do Gestor de Configuração  
 O Configuration Manager possui uma manutenção de cópia de segurança de tarefas que:  

-   É executada de acordo com um agendamento  

-   Faz uma cópia de segurança da base de dados do site  

-   Faz uma cópia de segurança de chaves de registo específicas  

-   Faz uma cópia de segurança de pastas e ficheiros específicos  

-   Faz uma cópia de segurança da pasta **CD.Latest** (veja [The CD.Latest folder for System Center Configuration Manager (A pasta CD.Latest para o System Center Configuration Manager)](../../core/servers/manage/the-cd.latest-folder.md))  

 Planeie a execução da tarefa predefinida de cópia de segurança do site no mínimo a cada 5 dias. Isto acontece porque o Configuration Manager utiliza um [período de retenção do registo de alterações do SQL Server](#bkmk_SQLretention) período de 5 dias.  

 Para simplificar o processo de cópia de segurança, pode criar um **Afterbackup** ficheiro para executar automaticamente ações pós-cópia de segurança após a tarefa de manutenção cópia de segurança é executada com êxito. O ficheiro Afterbackup bat é normalmente utilizado para arquivar o instantâneo da cópia de segurança para uma localização segura. Também pode utilizar o ficheiro Afterbackup bat para copiar ficheiros para a pasta de cópia de segurança e iniciar suplementares, outras tarefas de cópia de segurança.

Utilize as secções seguintes para o ajudar a criar a sua estratégia de cópia de segurança do Configuration Manager.  

> [!NOTE]  
>  O Configuration Manager pode recuperar a base de dados do site, a tarefa de manutenção cópia de segurança do Configuration Manager ou a partir de uma cópia de segurança de base de dados de site que criou com outro processo. Por exemplo, pode restaurar a base de dados do site a partir de uma cópia de segurança que é criada como parte de um plano de manutenção do Microsoft SQL Server. Pode restaurar a base de dados do site a partir de uma cópia de segurança é criada utilizando o System Center 2012 Data Protection Manager (DPM). Para obter mais informações, veja [Utilizar o Data Protection Manager para Efetuar Cópias de Segurança da Base de Dados do Site](#BKMK_DPMBackup).  

###  <a name="BKMK_BackupMaintenanceTask"></a> Tarefa de manutenção de cópias de segurança  
 Pode automatizar a cópia de segurança para sites do Configuration Manager, agendando a tarefa de manutenção cópia de segurança do servidor do Site predefinida. É possível fazer uma cópia de segurança de um site de administração central e site primário, mas não existe qualquer suporte para cópias de segurança de sites secundários ou servidores do sistema de sites. Quando o serviço de cópia de segurança do Configuration Manager é executado, segue as instruções definidas no ficheiro de controlo de cópia de segurança (**&lt;Pastadeinstalaçãodoconfigmgr\>\Inboxes\Smsbkup.box\Smsbkup.ctl**). É possível modificar o ficheiro de controlo da cópia de segurança para alterar o comportamento do serviço de cópia de segurança. As informações de estado da cópia de segurança do site são escritas no ficheiro **Smsbkup.log** . Este ficheiro é criado na pasta de destino que especificar nas propriedades da tarefa de manutenção Efetuar Cópia de Segurança do Servidor de Site.  


##### <a name="to-enable-the-site-backup-maintenance-task"></a>Para ativar a tarefa de cópia de segurança de manutenção do site  

1.  Na consola do Configuration Manager, abra **administração** > **configuração do Site**  

     \> **Sites**.  

2.  Selecione o site no qual pretende ativar a tarefa de cópia de segurança de manutenção do site.  

3.  No **base** separador o **definições** grupo, selecione **tarefas de manutenção do Site**.  

4.  Escolher **cópia de segurança do servidor do Site**  >  **editar**.  

5.  Escolher **ativar esta tarefa** > **definir caminhos** para especificar o destino de cópia de segurança. Tem as seguintes opções:  

    > [!IMPORTANT]  
    >  Para ajudar a impedir a adulteração dos ficheiros de cópia de segurança, armazenar os ficheiros numa localização segura. O caminho de cópia de segurança mais seguro é numa unidade local, para que possa definir permissões do sistema de ficheiros NTFS na pasta. O Configuration Manager encripta os dados da cópia de segurança que são armazenados no caminho de cópia de segurança.  

    -   **Unidade local no servidor do site para dados do site e base de dados**: Especifica que os ficheiros de cópia de segurança do site e base de dados do site são armazenados no caminho especificado na unidade de disco local do servidor do site. Terá de criar a pasta local antes da execução da tarefa de cópia de segurança. A conta do Sistema Local no servidor de site tem de ter permissões de **Escrita** do sistema de ficheiros NTFS na pasta local da cópia de segurança do servidor de site. A conta do Sistema Local no computador com o SQL Server tem de ter permissões de **Escrita** de NTFS na pasta da cópia de segurança da base de dados do site.  

    -   **O caminho de rede (nome UNC) para dados do site e base de dados**: Especifica que os ficheiros de cópia de segurança do site e base de dados do site são armazenados no caminho UNC especificado. Terá de criar a partilha antes da execução da tarefa de cópia de segurança. A conta de computador do servidor de site e a conta de computador do SQL Server, se este estiver instalado noutro computador, têm de ter permissões de **Escrita** de NTFS e de partilha na pasta da rede partilhada.  

    -   **Unidades locais no servidor do site e do SQL Server**: Especifica que os ficheiros de cópia de segurança para o site são armazenados no caminho especificado na unidade local do servidor do site e os ficheiros de cópia de segurança da base de dados do site são armazenados no caminho especificado na unidade local do servidor de base de dados do site. Terá de criar as pastas locais antes da execução da tarefa de cópia de segurança. A conta de computador do servidor de site tem de ter permissões de **Escrita** de NTFS na pasta que criar no servidor de site. A conta de computador do SQL Server tem de ter permissões de **Escrever** de NTFS na pasta que criar no servidor de base de dados do site. Esta opção só estará disponível se a base de dados do site não estiver instalada no servidor de site.  

    > [!NOTE]  
    >    - A opção de navegar para o destino da cópia de segurança só estará disponível se especificar o caminho UNC do destino da cópia de segurança.

    > - O nome de pasta ou nome da partilha utilizado para o destino da cópia de segurança não suporta a utilização de carateres Unicode.  


6.  Configure uma agenda para a tarefa de cópia de segurança do site. Como procedimento recomendado, considere uma agenda de cópia de segurança fora do horário de trabalho em vigor. Se tiver uma hierarquia, considere uma agenda que seja executada pelo menos duas vezes por semana, de modo a maximizar a retenção de dados em caso de falha do site.  

    Quando executa a consola do Configuration Manager no mesmo servidor do site que está a configurar para cópia de segurança, a tarefa de manutenção cópia de segurança do servidor do Site utiliza a hora local para a agenda. Quando a consola do Configuration Manager é executada a partir de um computador remoto relativamente ao site que está a configurar para cópia de segurança, a tarefa de manutenção cópia de segurança do servidor do Site utiliza a hora UTC para a agenda.  

7.  Escolha se pretende criar um alerta se falhar a tarefa de cópia de segurança do site, clique em **OK**e, em seguida, clique em **OK**. Quando selecionada, o Configuration Manager cria um alerta crítico da falha de cópia de segurança que poderá consultar no **alertas** nó o **monitorização** área de trabalho.  

 Em seguida, certifique-se de que a tarefa de manutenção do servidor do Site de cópia de segurança está em execução, para se certificar de que a criação de cópias de segurança.  

##### <a name="to-verify-that-the-backup-site-server-maintenance-task-is-running"></a>Para verificar que a tarefa de manutenção do servidor do Site de cópia de segurança está em execução  

-   Certifique-se de que a tarefa de manutenção cópia de segurança do Site está em execução, verificando uma das seguintes ações:  

    -   Verifique o timestamp dos ficheiros na pasta de destino de cópia de segurança que criou a tarefa. Certifique-se de que o timestamp foi atualizado com uma hora que corresponde ao tempo quando a tarefa última foi agendada para ser executada.  

    -   No nó **Estado do Componente** da área de trabalho **Monitorização** , veja as mensagens de estado de SMS_SITE_BACKUP. Quando a cópia de segurança do site for concluída com êxito, será apresentado o ID de mensagem 5035, indicando que a cópia de segurança do site foi concluída sem erros.  

    -   Quando a tarefa de manutenção Efetuar Cópia de Segurança do Servidor de Site estiver configurada para criar um alerta em caso de falha da cópia de segurança, pode ver as falhas da cópia de segurança no nó **Alertas** da área de trabalho **Monitorização** .  

    -   No &lt; *Pastadeinstalaçãodoconfigmgr*> \Logs, consulte smsbkup de avisos e erros. Quando a cópia de segurança do site for concluída com êxito, será apresentado `Backup completed` com um carimbo de data/hora e o ID de mensagem `STATMSG: ID=5035`.  

    > [!TIP]  
    >  Se a tarefa de cópia de segurança de manutenção falhar, poderá reiniciá-la parando e reiniciando o serviço SMS_SITE_BACKUP.  

###  <a name="BKMK_DPMBackup"></a> Utilizar o Data Protection Manager para efetuar cópias de segurança da base de dados do site  
 Pode utilizar o System Center 2012 Data Protection Manager (DPM) para criar uma cópia de segurança da base de dados do site. Terá de criar um novo grupo de proteção no DPM para o computador da base de dados do site. Na página **Selecionar Membros do Grupo** do Assistente de Criação de Novo Grupo de Proteção, selecione o serviço SMS Writer na lista de origens de dados e selecione a base de dados do site como membro apropriado. Para obter mais informações sobre a utilização do DPM na criação de cópias de segurança da base de dados do site, veja a [Biblioteca de Documentação do Data Protection Manager](http://go.microsoft.com/fwlink/?LinkId=272772) na TechNet.  

> [!IMPORTANT]  
>  O Configuration Manager não suporta a cópia de segurança do DPM para um cluster do SQL Server que utilize uma instância nomeada, mas suporta a cópia de segurança do DPM num cluster do SQL Server que utilize a instância predefinida do SQL Server.  

 Após restaurar a base de dados do site, siga os passos do Programa de Configuração para recuperar o site. Selecione o **utilizar uma base de dados do site que tenha sido recuperada manualmente** opção de recuperação para utilizar a base de dados do site que recuperou com o Data Protection Manager.  

###  <a name="BKMK_ArchivingBackupSnapshot"></a> Arquivar o instantâneo de cópia de segurança  
 Na primeira vez que é executada, a tarefa de manutenção Efetuar Cópia de Segurança do Servidor de Site cria um instantâneo de cópia de segurança que poderá utilizar para recuperar o servidor de site em caso de falha. Quando a tarefa de cópia de segurança é novamente executada nos ciclos subsequentes, cria um novo instantâneo de cópia de segurança que substitui o anterior. Em resultado, o site tem apenas um único instantâneo de cópia de segurança, pelo que não existe forma de recuperar um instantâneo de cópia de segurança anterior.  

 Como procedimento recomendado, mantenha vários arquivos do instantâneo de cópia de segurança, pelos seguintes motivos:  

-   É comum de cópia de segurança suporte de dados falhar, sejam perdidos ou contêm apenas uma cópia de segurança parcial. Recuperar um site primário autónomo em falha a partir de uma cópia de segurança mais antiga é melhor do que recuperar sem qualquer cópia de segurança. Para um servidor de site numa hierarquia, a cópia de segurança tem de ter um período de retenção de registo de alterações do SQL Server ou a cópia de segurança não é necessária.  

-   Determinados danos no site podem não ser detetados durante vários ciclos de cópia de segurança. Poderá ter de utilizar uma cópia de segurança do instantâneo antes do site ter ficado danificado. Isto aplica-se a um site primário autónomo e aos sites numa hierarquia onde a cópia de segurança está no SQL Server registo de alterações período de retenção.  

-   O site poderá não ter nenhum instantâneo de cópia de segurança se, por exemplo, a tarefa de manutenção Cópia de Segurança do Servidor do Site falhar. Uma vez que a tarefa de cópia de segurança remove o instantâneo de cópia de segurança anterior antes de iniciar a cópia de segurança dos dados atuais, não haverá um instantâneo de cópia de segurança válido.  

###  <a name="BKMK_UsingAfterBackup"></a> Utilizar o Ficheiro AfterBackup.bat  
 Depois de efetuar a cópia de segurança do site com êxito, a tarefa Efetuar Cópia de Segurança do Servidor de Site tenta executar automaticamente um ficheiro com o nome AfterBackup.bat. Tem de criar manualmente o ficheiro Afterbackup bat em &lt; *Pastadeinstalaçãodoconfigmgr*> \inboxes\smsbkup. Se um ficheiro Afterbackup bat e é armazenado na pasta correta, este é executado automaticamente depois de concluída a tarefa de cópia de segurança. O ficheiro AfterBackup.bat permite arquivar o instantâneo da cópia de segurança no final de cada operação de cópia de segurança e executar automaticamente outras tarefas de pós-cópia de segurança que não fazem parte da tarefa de manutenção Cópia de Segurança do Servidor do Site. O ficheiro AfterBackup.bat integra o arquivo e as operações de cópia de segurança, assegurando que cada novo instantâneo de cópia de segurança é arquivado. Quando o ficheiro AfterBackup.bat não está presente, a tarefa de cópia de segurança ignora-o sem efeito sobre a operação de cópia de segurança. Para verificar se a tarefa de cópia de segurança do site executou o ficheiro AfterBackup.bat com êxito, veja o nó **Estado do Componente** na área de trabalho **Monitorização** e reveja as mensagens de estado para SMS_SITE_BACKUP. Quando a tarefa tiver iniciado com êxito o ficheiro de comandos AfterBackup.bat, é apresentada a mensagem ID 5040.  

> [!TIP]  
>  Para criar o ficheiro Afterbackup bat para arquivar os ficheiros de cópia de segurança de servidor de site, tem de utilizar uma ferramenta do comando de cópia, tal como Robocopy, no ficheiro batch. Por exemplo, pode criar o ficheiro AfterBackup.bat e, na primeira linha, pode adicionar algo semelhante a: `Robocopy E:\ConfigMgr_Backup \\ServerName\ShareName\ConfigMgr_Backup /MIR`. Para obter mais informações sobre o Robocopy, veja a página Web de referência da linha de comandos [Robocopy](http://go.microsoft.com/fwlink/p/?LinkId=228408) .  

 Embora a utilização prevista de AfterBackup.bat seja arquivar o instantâneo da cópia de segurança, é possível criar um ficheiro AfterBackup.bat para executar tarefas adicionais no final de cada operação de cópia de segurança.  

###  <a name="BKMK_SupplementalBackup"></a> Tarefas suplementares de cópia de segurança  
 A tarefa de manutenção Cópia de Segurança do Servidor do Site fornece um instantâneo de cópia de segurança para os ficheiros do servidor de site e a base de dados do site, mas existem outros itens dos quais não foi efetuada cópia de segurança que deve ter em conta ao criar a sua estratégia de cópia de segurança. Utilize as secções seguintes para o ajudar a concluir a sua estratégia de cópia de segurança do Configuration Manager.  

#### <a name="back-up-custom-reporting-services-reports"></a>Cópia de segurança dos relatórios personalizados do Reporting Services  
 Depois de modificar relatórios personalizados do Reporting Services predefinidos ou criados, a criação de uma cópia de segurança dos ficheiros da base de dados do servidor de relatórios é uma parte importante da sua estratégia de cópia de segurança. A cópia de segurança do servidor de relatórios deve incluir uma cópia de segurança dos ficheiros de origem para relatórios e modelos, chaves de encriptação, assemblagens ou extensões personalizadas, ficheiros de configuração, vistas personalizadas do SQL Server nos relatórios personalizados, procedimentos armazenados personalizados, etc.  

> [!IMPORTANT]  
>  Quando as atualizações do Configuration Manager para uma versão mais recente, os relatórios predefinidos podem ser substituídos por novos relatórios. Se modificar um relatório predefinido, agregar o relatório e, em seguida, restaure-a no Reporting Services.  

 Para obter mais informações sobre a criação de cópias de segurança dos seus relatórios personalizados no Reporting Services, veja [Backup and Restore Operations for a Reporting Services Installation (Operações de Cópia de Segurança e Restauro de uma Instalação do Reporting Services)](https://technet.microsoft.com/library/ms155814\(v=sql.120\).aspx) na Documentação Online do SQL Server 2014.  

#### <a name="backup-content-files"></a>Cópia de segurança de ficheiros de conteúdo  
 A biblioteca de conteúdos no Configuration Manager é a localização onde são armazenados todos os ficheiros de conteúdo para atualizações de software, aplicações, implementação do sistema operativo e assim sucessivamente. A biblioteca de conteúdos está localizada no servidor do site e em cada ponto de distribuição. A tarefa de manutenção Cópia de Segurança do Servidor do Site não inclui uma cópia de segurança para a biblioteca de conteúdos ou os ficheiros de origem do pacote. Quando um servidor de site falha, as informações sobre os ficheiros da biblioteca de conteúdos são restauradas para a base de dados do site, mas é necessário restaurar os ficheiros da biblioteca de conteúdos e de origem do pacote no servidor do site.  

-   **Biblioteca de conteúdos**: A biblioteca de conteúdos deve ser restaurada antes de que pode redistribuir conteúdos a pontos de distribuição. Quando a redistribuição do conteúdo, o Configuration Manager copia os ficheiros da biblioteca de conteúdos no servidor do site para os pontos de distribuição. A biblioteca de conteúdos para o servidor do site está na pasta SCCMContentLib, que está normalmente localizada na unidade com mais disco espaço livre no momento quando o site foi instalado.  

-   **Ficheiros de origem do pacote**: Os ficheiros de origem do pacote devem ser restaurados antes de poder atualizar conteúdo em pontos de distribuição. Quando inicia uma atualização de conteúdo, do Configuration Manager copia ficheiros novos ou modificados da origem do pacote para a biblioteca de conteúdos, que aponta cópias transformam-se os ficheiros para distribuição associados. Pode executar a seguinte consulta no SQL Server para encontrar a localização de origem do pacote para todos os pacotes e aplicações: `SELECT * FROM v_Package`. Pode identificar o site de origem do pacote atravésdos primeiros três carateres do ID de pacote. Por exemplo, se o ID de pacote for CEN00001, o código de site do site de origem é CEN. Ao restaurar os ficheiros de origem do pacote, estes devem ser restaurados para a mesma localização em que se encontravam antes da falha.  

 Verifique se está a incluir as localizações da biblioteca de conteúdos e da origem do pacote na cópia de segurança do sistema de ficheiros para o servidor de site.  

#### <a name="back-up-custom-software-updates"></a>Cópia de segurança de atualizações de software personalizadas  
 System Center Updates Publisher 2011 é uma ferramenta autónoma que lhe permite publicar atualizações de software personalizadas para o Windows Server Update Services (WSUS), sincronizar as atualizações de software do Configuration Manager, avaliar a compatibilidade de atualizações de software e implementar as atualizações de software personalizadas para os clientes. Updates Publisher utiliza uma base de dados local para o repositório de atualização de software. Quando utilizar o Updates Publisher para gerir atualizações de software personalizadas, determine se tem de incluir a base de dados do Updates Publisher no seu plano de cópia de segurança. Para obter mais informações sobre o Updates Publisher, veja [System Center Updates Publisher 2011](http://go.microsoft.com/fwlink/p/?LinkId=228726) na Biblioteca TechCenter do System Center.  

 Utilize o procedimento seguinte para agregar a base de dados do Updates Publisher.  

###### <a name="to-back-up-the-updates-publisher-2011-database"></a>Para criar uma cópia de segurança da base de dados do Updates Publisher 2011  

1.  No computador que executa o Updates Publisher, procure o ficheiro de base de dados do Updates Publisher (scupdb) em %*USERPROFILE*%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\\. Existe um ficheiro de base de dados diferente para cada utilizador que executa o Updates Publisher.  

2.  Copie o ficheiro de base de dados para o destino de cópia de segurança. Por exemplo, se o destino de cópia de segurança for E:\ConfigMgr_Backup, pode copiar o ficheiro de base de dados do Updates Publisher para e:\configmgr_backup\scup2011.  

    > [!TIP]  
    >  Quando existe mais do que um ficheiro de base de dados num computador, considere armazenar o ficheiro numa subpasta que indica o perfil de utilizador associado ao ficheiro da base de dados. Por exemplo, pode ter um ficheiro de base de dados em E:\ConfigMgr_Backup\SCUP2011\User1 e outro ficheiro de base de dados em E:\ConfigMgr_Backup\SCUP2011\User2.  

### <a name="user-state-migration-data"></a>Dados de migração de estado de utilizador  
 Pode utilizar sequências de tarefas do Configuration Manager para capturar e restaurar dados de estado do utilizador em cenários de implementação do sistema operativo em que pretende manter o estado de utilizador do sistema operativo atual. As pastas que armazenam dados de estado do utilizador são listadas nas propriedades para o ponto de migração de estado. Não é efetuada cópia de segurança destes dados de migração de estado de utilizador como parte da tarefa de manutenção Cópia de Segurança do Servidor do Site. Como parte do seu plano de cópia de segurança, tem de copiar manualmente as pastas que especificar para armazenar os dados de migração de estado do utilizador.   

#### <a name="to-determine-the-folders-used-to-store-user-state-migration-data"></a>Para determinar as pastas utilizadas para armazenar dados de migração de estado de utilizador  

1.  Na consola do Configuration Manager, clique em **Administração**.  

2.  No **administração** área de trabalho, expanda **configuração do Site**e escolha **servidores e funções de sistema de sites**.  

3.  Selecione o sistema de sites que aloja a função de migração de estado e escolha **ponto de migração de estado** no **funções do sistema de sites**.  


4.  No separador **Função do Site** , no grupo **Propriedades** , clique em **Propriedades**.  
5.  As pastas que armazenam os dados de migração de estado do utilizador são listadas na secção **Detalhes da pasta**, no separador **Geral**.  

## <a name="recover-a-configuration-manager-site"></a>Recuperar um site do Gestor de Configuração
 Não é necessária uma recuperação de site do Configuration Manager sempre que um site do Configuration Manager falha ou ocorrer perda de dados na base de dados do site. Reparar e ressincronizar dados são as tarefas principais de uma recuperação de site e são necessárias para evitar a interrupção das operações.  

> [!IMPORTANT]  
>  Quando recuperar a base de dados para um site:  

>  -   Tem de utilizar a mesma versão e edição do SQL Server. Por exemplo, a restaurar uma base de dados que foi executada no SQL Server 2012 para o SQL Server 2014 não é suportada. Do mesmo modo, a restaurar uma base de dados do site que foi executada numa edição Standard do SQL Server 2014 edição Enterprise do SQL Server 2014 não é suportada.  
> -   O SQL Server não pode estar definido como **modo de utilizador único**.  
> -   Certifique-se de que os ficheiros .MDF e .LDF são válidos. Quando recupera um site, não existe verificação para o estado dos ficheiros que está a restaurar.  


 Recuperação de site é iniciada, executando o Assistente de configuração do Configuration Manager a partir do CD. Pasta mais recente.  Pode também configurar o script de instalação automática e, em seguida, utilize o comando do programa de configuração **/script** opção para executar a configuração a partir do CD mesmo. Pasta mais recente. As opções de recuperação variam consoante tenha ou uma cópia de segurança da base de dados do site do Configuration Manager. Para obter mais informações, veja [The CD.Latest folder for System Center Configuration Manager (A pasta CD.Latest do System Center Configuration Manager)](../../core/servers/manage/the-cd.latest-folder.md).  

> [!IMPORTANT]  
>  Se executar a configuração do Configuration Manager a partir de **iniciar** menu no servidor do site, o **recuperar um site** opção não está disponível.  

>  Se instalou as atualizações a partir da consola do Configuration Manager antes de efetuar a cópia de segurança, é possível reinstalar com êxito o site utilizando o programa de configuração a partir do suporte de instalação ou o caminho de instalação do Configuration Manager.  

> [!NOTE]  
>  Depois de restaurar uma base de dados do site configurada para réplicas de bases de dados, antes de poder utilizar as réplicas de bases de dados, tem de reconfigurar cada réplica de base de dados, recriando as publicações e as subscrições.  

###  <a name="BKMK_DetermineRecoveryOptions"></a> Determinar as opções de recuperação  
 Existem duas áreas principais que tem de considerar para o servidor de site primário do Configuration Manager e a recuperação de site de administração central; o servidor de site e a base de dados do site. Utilize as secções seguintes para determinar as opções que tem à disposição para selecionar para o cenário de recuperação.  

> [!NOTE]  

####  <a name="BKMK_SiteServerRecoveryOptions"></a> Opções de recuperação do servidor do site  
 Tem de iniciar o programa de configuração a partir de uma cópia do CD. Pasta mais recente que criar fora da pasta de instalação do Configuration Manager. Em seguida, selecione a opção **Recuperar um site** . Quando executar o Programa de Configuração, tem as seguintes opções de recuperação para o servidor de site em falha:  

-   **Recuperar o servidor do site utilizando uma cópia de segurança existente**: Utilize esta opção quando tiver uma cópia de segurança do servidor do site do Configuration Manager que foi criado no servidor do site como parte do **cópia de segurança do servidor do Site** tarefa de manutenção antes da falha do site. O site é reinstalado e as definições de site são configuradas, com base no site do qual foi efetuada a cópia de segurança.  

-   **Reinstalar o servidor do site**: Utilize esta opção quando não tiver uma cópia de segurança do servidor do site. O servidor local é reinstalado e têm de ser especificadas as definições de site, tal como necessário durante uma instalação inicial. Para recuperar o site com êxito, tem de utilizar o mesmo código de site e o nome de base de dados do site que utilizou quando o site em falha foi inicialmente instalado.  

> [!NOTE]  
>  Quando o programa de configuração Deteta um site existente do Configuration Manager no servidor, pode iniciar uma recuperação de site, mas as opções de recuperação para o servidor de site são limitadas. Por exemplo, se executar o Programa de Configuração num servidor de site existente, quando escolher a recuperação, poderá recuperar o servidor de base de dados do site, mas a opção de recuperação do servidor de site é desativada.  

####  <a name="BKMK_SiteDatabaseRecoveryOption"></a> Opções de recuperação da base de dados do site  
 Quando executar o Programa de Configuração, tem as seguintes opções de recuperação da base de dados do site:  

-   **Recuperar a base de dados do site utilizando um conjunto de cópia de segurança**: Utilize esta opção quando tiver uma cópia de segurança da base de dados de site do Configuration Manager que foi criada como parte do **cópia de segurança do servidor do Site** tarefa de manutenção executada no site antes da falha de base de dados do site. Quando tem uma hierarquia, as alterações efetuadas à base de dados do site após a última cópia de segurança da mesma são obtidas a partir do site de administração central para um site primário ou de um site primário de referência para um site de administração central. Quando recuperar a base de dados do site para um site primário autónomo, perderá as alterações do site posteriores à última cópia de segurança.  

     Quando recupera a base de dados de site para um site numa hierarquia, o comportamento da recuperação é diferente para um site de administração central e um site primário, e quando a última cópia de segurança é dentro ou fora do período de retenção de registo de alterações do SQL Server. Para obter mais informações, veja a secção [Cenários de Recuperação de Bases de Dados de Site](#BKMK_SiteDBRecoveryScenarios) deste tópico.  

    > [!NOTE]  
    >  A recuperação falha se for escolhido o restauro da base de dados do site utilizando um conjunto de cópia de segurança, mas a base de dados do site já existe.  

-   **Criar uma nova base de dados para este site**: Utilize esta opção quando não tiver uma cópia de segurança da base de dados do site do Configuration Manager. Quando tem uma hierarquia, é criada uma nova base de dados do site e os dados são recuperados utilizando dados replicados do site de administração central para um site primário ou de um site primário de referência para um site de administração central. Esta opção não está disponível quando recupera um site primário autónomo ou um site de administração central que não tenha sites primários.  

-   **Utilizar uma base de dados do site que tenha sido recuperada manualmente**: Utilize esta opção quando já tiver recuperado a base de dados do site do Configuration Manager, mas tem de concluir o processo de recuperação. O Configuration Manager pode recuperar a base de dados do site, a tarefa de manutenção cópia de segurança do Configuration Manager ou a partir de uma cópia de segurança de base de dados de site efetuada com o DPM ou outro processo. Depois de restaurar a base de dados do site utilizando um método fora do Configuration Manager, tem de executar a configuração e selecionar esta opção para concluir a recuperação de base de dados do site. Quando tem uma hierarquia, as alterações efetuadas à base de dados do site após a última cópia de segurança da mesma são obtidas a partir do site de administração central para um site primário ou de um site primário de referência para um site de administração central. Quando recuperar a base de dados do site para um site primário autónomo, perderá as alterações do site posteriores à última cópia de segurança.  

    > [!NOTE]  
    >  Quando utilizar o DPM para agregar a sua base de dados do site, utilize os procedimentos do DPM para restaurar a base de dados do site para uma localização especificada antes de continuar o processo de restauro no Configuration Manager. Para obter mais informações sobre o DPM, veja a [Biblioteca de Documentação do Data Protection Manager](http://go.microsoft.com/fwlink/?LinkId=272772) no TechNet.  

-   **Ignorar recuperação da base de dados**: Utilize esta opção quando tiver ocorrido sem perda de dados no servidor de base de dados do site do Configuration Manager. Esta opção só é válida quando a base de dados do site estiver num computador diferente do servidor do site que está a recuperar.  

####  <a name="bkmk_SQLretention"></a> Período de retenção do registo de alterações do SQL Server  
 O registo de alterações está ativado para a base de dados do site no SQL Server. Registo de alterações permite ao Configuration Manager consulta para obter informações sobre as alterações que foram efetuadas às tabelas de base de dados após um ponto anterior no tempo. O período de retenção especifica por quanto tempo as informações de registo de alterações são retidas. Por predefinição, a base de dados do site é configurada com um período de retenção de cinco dias. Quando recupera a base de dados de um site, o processo de recuperação procede de forma diferente se a sua cópia de segurança estiver dentro ou fora do período de retenção. Por exemplo, se o servidor da base de dados do site falhar e a última cópia de segurança tiver sido efetuada há 7 dias, está fora do período de retenção.

 Para mais informações sobre os aspetos internos de registo de alterações do SQL Server, consulte os seguintes blogues da equipa do SQL Server: [Registo de alterações limpeza - parte 1](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-1) e [Alterar controlo limpeza – parte 2](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-2).



####  <a name="bkmk_reinit"></a> Processo para reinicializar um site ou dados globais  
 O processo para reinicializar um site ou dados globais substitui dados existentes na base de dados do site por dados da base de dados de outro site. Por exemplo, quando o site ABC reinicializa dados do site XYZ, ocorrem os seguintes passos:  

-   Os dados são copiados do site XYZ para o site ABC.  

-   Os dados existentes do site XYZ são removidos da base de dados do site no site ABC.  

-   Os dados copiados do site XYZ são inseridos na base de dados do site ABC.  

##### <a name="example-scenario-1"></a>Cenário de exemplo 1  
 **O site primário reinicializa os dados globais a partir do site de administração central**: O processo de recuperação remove os dados globais existentes para o site primário na base de dados do site primário e substitui os dados com os dados globais copiados do site de administração central.  

##### <a name="example-scenario-2"></a>Cenário de exemplo 2  
 **O site de administração central reinicializa os dados do site a partir de um site primário**: O processo de recuperação remove os dados de site existentes para esse site primário na base de dados do site de administração central e substitui os dados com os dados de site copiados do site primário. Os dados de site de outros sites primários não são afetados.  

####  <a name="BKMK_SiteDBRecoveryScenarios"></a> Cenários de recuperação de bases de dados de site  
 Depois de restaurar uma base de dados do site a partir de uma cópia de segurança, o Configuration Manager tenta restaurar as alterações no site e aos dados globais depois da última cópia de segurança da base de dados. As seguintes descrevem as ações que o Configuration Manager começará após o restauro de uma base de dados do site a partir da cópia de segurança.  

 **O site recuperado é um site de administração central:**  

-   **Cópia de segurança da base de dados dentro do período de retenção do registo de alterações**  

    -   **Dados globais:** As alterações nos dados globais posteriores a cópia de segurança são replicadas a partir de todos os sites primários.  

    -   **Dados do site:** As alterações nos dados de site após a cópia de segurança são replicadas a partir de todos os sites primários.  

-   **Cópia de segurança da base de dados anterior ao período de retenção do registo de alterações**  

    -   **Dados globais:** O site de administração central reinicializa os dados globais a partir do site primário de referência, caso o especifique. Em seguida, todos os outros sites primários reinicializam os dados globais a partir do site de administração central. Se não for especificado nenhum site de referência, todos os sites primários reinicializam os dados globais a partir do site de administração central (os dados que foram restaurados a partir da cópia de segurança).  

    -   **Dados do site:** O site de administração central reinicializa os dados do site a partir de cada site primário.  

 **O site recuperado é um site primário:**  

-   **Cópia de segurança da base de dados dentro do período de retenção do registo de alterações**  

    -   **Dados globais:** As alterações nos dados globais posteriores a cópia de segurança são replicadas a partir do site de administração central.  

    -   **Dados do site:** O site de administração central reinicializa os dados do site do site primário. As alterações posteriores à cópia de segurança são perdidas, mas a maioria dos dados é novamente gerada por clientes que enviam informações para o site primário.  

-   **Cópia de segurança da base de dados anterior ao período de retenção do registo de alterações**  

    -   **Dados globais:** O site primário reinicializa os dados globais a partir do site de administração central.  

    -   **Dados do site:** O site de administração central reinicializa os dados do site do site primário. As alterações posteriores à cópia de segurança são perdidas, mas a maioria dos dados é novamente gerada por clientes que enviam informações para o site primário.  

### <a name="site-recovery-procedures"></a>Procedimentos de recuperação de sites  
 Utilize um dos seguintes procedimentos para recuperar o servidor e a base de dados do site.  

##### <a name="to-start-a-site-recovery-in-the-setup-wizard"></a>Para iniciar a recuperação de um site no Assistente de Configuração  

1.  Copie o CD. Pasta mais recente para uma localização fora da pasta de instalação do Configuration Manager. (Veja [The CD.Latest folder for System Center Configuration Manager (A pasta CD.Latest do System Center Configuration Manager)](../../core/servers/manage/the-cd.latest-folder.md))  

     A partir da cópia do CD. Pasta mais recente, execute o Assistente de configuração do Configuration Manager.  

2.  Na página **Introdução** , selecione **Recuperar um site**e clique em **Seguinte**.  

3.  Conclua o assistente utilizando as opções adequadas para a recuperação do seu site.  

    > [!IMPORTANT]  
    >  Durante a recuperação, a Configuração identifica a porta do SQL Server Service Broker (SSB) utilizada pelo SQL Server. Não altere esta definição de porta durante a recuperação ou a replicação de dados não funcionará corretamente depois da recuperação ser concluída.  

    > [!NOTE]  
    >  Pode especificar o original ou um novo caminho a utilizar para a instalação do Configuration Manager no Assistente de configuração.  

##### <a name="to-start-an-unattended-site-recovery"></a>Para iniciar uma recuperação de site automática  

1.  Prepare o script de instalação automática para as opções de que necessita para a recuperação do site.  

2.  Execute a configuração do Configuration Manager utilizando o comando **/script** opção. Por exemplo, se atribuiu o ficheiro de inicialização da configuração Configmgrunattend e guardou no diretório C:\Temp do computador no qual está a executar o programa de configuração, o comando seria o seguinte: **Configuração /script C:\temp\ConfigMgrUnattend.ini**.  

> [!NOTE]  
>  Depois de recuperar um site de administração central, a replicação de alguns dados do site a partir de sites subordinados poderá não ser estabelecida. Isto pode incluir inventário de hardware, inventário de software e mensagens de estado.  
>   
>  Se esta situação ocorrer, tem de reinicializar **ConfigMgrDRSSiteQueue** para a replicação da base de dados.  Para tal, utilize **Manager do SQL Server** para executar a seguinte consulta no Configuration Manager da base de dados do site no site de administração central:  
>   
>  **IF EXISTS (SELECIONE \* EM sys.service_queues EM QUE name = “ConfigMgrDRSSiteQueue” AND is_receive_enabled = 0)**  
>   
>  **ALTER QUEUE [dbo].[ConfigMgrDRSSiteQueue] WITH STATUS = ON**  

###  <a name="BKMK_UnattendedSiteRecoveryKeys"></a> Chaves de ficheiro de script de recuperação automática de site  
 Para efetuar uma recuperação automática de um site de administração central do Configuration Manager ou o site primário, pode criar um script de instalação automática e utilizar a configuração com a opção /script do comando. O script fornece o mesmo tipo de informações pedidas pelo Assistente de configuração, mas não existem predefinições. Tem de especificar todos os valores para as chaves de configuração que se aplicam ao tipo de recuperação que está a utilizar.  

 Pode executar a configuração do Configuration Manager autónoma, utilizando um ficheiro de inicialização com a opção /script da configuração da linha de comandos. A configuração automática é suportada para recuperação de um site de administração central do Configuration Manager e o site primário. Para utilizar a opção da linha de comandos /script de configuração, tem de criar um ficheiro de inicialização e especificar o respetivo nome após esta opção da linha de comandos. O nome do ficheiro é indiferente, desde que tenha a extensão de nome de ficheiro .ini. Quando referenciar o ficheiro de inicialização da configuração na linha de comandos, tem de fornecer o caminho completo do ficheiro. Por exemplo, se o ficheiro de inicialização da configuração tiver o nome Setup.ini e estiver armazenado na pasta C:\setup, a linha de comandos será:  

 **setup /script c:\setup\setup.ini**.  

> [!IMPORTANT]  
>  Tem de ter direitos de Administrador para executar a Configuração. Quando executar a Configuração com o script automático, inicie a Linha de Comandos num contexto de Administrador através de **Executar como administrador**.  

 O script contém nomes de secções, nomes de chaves e valores. Os nomes de chaves de secção necessários variam consoante o tipo de recuperação que pretende realizar com o script. A ordem das chaves dentro das secções e a ordem das secções no ficheiro não são importantes. As chaves não são sensíveis a maiúsculas e minúsculas. Quando fornece valores de chaves, o nome da chave tem de ser seguido de um sinal de igual (=) e do valor da chave.  

 Utilize as secções seguintes para criar o script para a recuperação de site automática. As tabelas apresentam as chaves de script de configuração disponíveis, os valores correspondentes, se são necessárias, para que tipo de instalação são utilizadas e uma descrição breve da chave.  

#### <a name="recover-a-central-administration-site-unattended"></a>Recuperar um site de administração central automática  
 Utilize as seguintes informações para configurar um ficheiro de script de configuração automática para recuperar um site de administração central.  

 **Identificação**  

-   **Nome da chave:** Ação  

    -   **Necessário:** Sim  

    -   **Valores:** RecoverCCAR  

    -   **Detalhes:** Recupera um site de administração central  

-   **Nome da chave:** CDLatest  

    -   **Necessário:** Sim – apenas quando utilizar suportes de dados a partir do CD. Pasta mais recente.    

    -   **Valores:** 1. qualquer valor diferente de 1 é considerada como não estar a utilizar o CD. Mais recente.

    -   **Detalhes:** O script tem de incluir este valor e chave quando executa a configuração a partir do suporte no CD. Pasta mais recente para efeitos de instalação de um site primário ou de administração central ou a recuperar um site primário ou de administração central. Este valor informa o programa de configuração que o suporte de dados de formulário CD. Está a ser utilizada a versão mais recente.  

**RecoveryOptions**  

-   **Nome da chave:** ServerRecoveryOptions  

    -   **Necessário:** Sim  

    -   **Valores:** 1, 2 ou 4  

         1 = Servidor de site de recuperação e SQL Server.  

         2 = Recuperar apenas servidor de site.  

         4 = Recuperar apenas SQL Server.  

    -   **Detalhes:** Especifica se o programa de configuração irá recuperar o servidor do site, do SQL Server ou ambos. As chaves associadas são necessárias quando define o seguinte valor para a definição ServerRecoveryOptions:  

        -   **Valor = 1** : tem a opção de especificar um valor para a chave **SiteServerBackupLocation** para recuperar o site com uma cópia de segurança do site. Se não especificar um valor, o site será reinstalado sem ser restaurado a partir de um conjunto de cópias de segurança.  

             A chave **BackupLocation** é obrigatória se configurar o valor **10** para a chave **DatabaseRecoveryOptions** , para restaurar a base de dados do site a partir de uma cópia de segurança.  

        -   **Valor = 2** : tem a opção de especificar um valor para a chave **SiteServerBackupLocation** para recuperar o site com uma cópia de segurança do site. Se não especificar um valor, o site será reinstalado sem ser restaurado a partir de um conjunto de cópias de segurança.  

        -   **Valor = 4** : a chave **BackupLocation** é obrigatória se configurar o valor **10** para a chave **DatabaseRecoveryOptions** , que serve para restaurar a base de dados do site a partir de uma cópia de segurança.  

-   **Nome da chave:** DatabaseRecoveryOptions  

    -   **Necessário:** Talvez  

    -   **Valores:** 10, 20, 40, 80  

         10 = Restaurar a base de dados do site a partir de cópia de segurança.  

         20 = Utilizar uma base de dados do site que tenha sido recuperada manualmente utilizando outro método.  

         40 = Criar uma nova base de dados para o site. Utilize esta opção quando não estiver disponível nenhuma cópia de segurança da base de dados do site. Os dados globais e de site são recuperados através da replicação a partir de outros sites.  

         80 = ignorar recuperação da base de dados.  

    -   **Detalhes:** Especifica a forma como a configuração irá recuperar a base de dados do site no SQL Server. Esta chave é necessária quando a definição **ServerRecoveryOptions** tem o valor **1** ou **4**  

-   **Nome da chave:** ReferenceSite  

    -   **Necessário:** Talvez  

    -   **Valores:** &lt;Fqdndositedereferência\>  

    -   **Detalhes:** Especifica o site primário de referência que utiliza o site de administração central para recuperar dados globais se a cópia de segurança da base de dados for anterior ao período de retenção do registo de alterações ou quando a recuperação de site sem uma cópia de segurança.  

         Quando não especificar um site de referência e a cópia de segurança da base de dados for anterior ao período de retenção do registo de alterações, todos os sites primário serão reinicializados com os dados restaurados a partir do site de administração central.  

         Quando não especificar um site de referência e a cópia de segurança da base de dados estiver dentro do período de retenção do registo de alterações, só serão replicadas a partir dos sites primários as alterações posteriores à cópia de segurança. Quando existirem alterações de diferentes sites primários em conflito, o site de administração central utilizará a primeira que receber.  

         Esta chave é obrigatória se a definição **DatabaseRecoveryOptions** tiver o valor **40**.  

-   **Nome da chave:** SiteServerBackupLocation  

    -   **Necessário:** Não  

    -   **Valores:** &lt;PathToSiteServerBackupSet\>  

    -   **Detalhes:** Especifica o caminho para o conjunto de cópia de segurança de servidor de site. Esta chave é opcional se a definição **ServerRecoveryOptions** tiver o valor **1** ou **2**. Especifique um valor para a chave **SiteServerBackupLocation** para recuperar o site com uma cópia de segurança do mesmo. Se não especificar um valor, o site será reinstalado sem ser restaurado a partir de um conjunto de cópias de segurança.  

-   **Nome da chave:** BackupLocation  

    -   **Necessário:** Talvez  

    -   **Valores:** &lt;PathToSiteDatabaseBackupSet\>  

    -   **Detalhes:** Especifica o caminho para o conjunto de cópia de segurança de base de dados de site. A chave **BackupLocation** é obrigatória se configurar o valor **1** ou **4** na chave **ServerRecoveryOptions** e configurar o valor **10** na chave **DatabaseRecoveryOptions** .  

**Opções**  

-   **Nome da chave:** Iddoproduto  

    -   **Necessário:** Sim  

    -   **Valores:**  

         xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  

         Eval  

    -   **Detalhes:** O Configuration Manager instalação chave de produto, incluindo os traços. Introduza **Eval** pode instalar a versão de avaliação do Configuration Manager.  

-   **Nome da chave:** Código do site  

    -   **Necessário:** Sim  

    -   **Valores:** &lt;Código do site\>  

    -   **Detalhes:** Três carateres de alfanuméricos que identificam o site na sua hierarquia. Tem de especificar o código do site que era utilizado pelo site antes da falha.  

-   **Nome da chave:** SiteName  

    -   **Necessário:** Sim  

    -   **Valores:** SiteName  

    -   **Detalhes:** Descrição para este site.  

-   **Nome da chave:** SMSInstallDir  

    -   **Necessário:** Sim  

    -   **Valores:** &lt;*ConfigMgrInstallationPath*>  

    -   **Detalhes:** Especifica a pasta de instalação para os ficheiros de programa do Configuration Manager.  

        > [!NOTE]  
        >  Pode especificar o caminho original ou um novo caminho a utilizar para a instalação do Configuration Manager.  

-   **Nome da chave:** SDKServer  

    -   **Necessário:** Sim  

    -   **Valores:** &lt;*FQDN do fornecedor de SMS*>  

    -   **Detalhes:** Especifica o FQDN do servidor que alojará o fornecedor de SMS. Terá de especificar o servidor que hospedava o Fornecedor de SMS antes da falha.  

         Pode configurar Fornecedores de SMS adicionais para o site após a instalação inicial.  

-   **Nome da chave:** PrerequisiteComp  

    -   **Necessário:** Sim  

    -   **Valores:** 0 ou 1  

         0 = transferir  

         1 = já transferido  

    -   **Detalhes:** Especifica se os ficheiros de pré-requisitos de configuração já foram transferidos. Por exemplo, se utilizar o valor 0, o Programa de Configuração transferirá os ficheiros.  

-   **Nome da chave:** PrerequisitePath  

    -   **Necessário:** Sim  

    -   **Valores:** &lt;*PathToSetupPrerequisiteFiles*>  

    -   **Detalhes:** Especifica o caminho para os ficheiros de pré-requisitos do programa de configuração. Conforme o valor de **PrerequisiteComp** , a Configuração utiliza este caminho para armazenar os ficheiros transferidos ou localizar os ficheiros transferidos anteriormente.  

-   **Nome da chave:** AdminConsole  

    -   **Necessário:** Talvez  

    -   **Valores:** 0 ou 1  

         0 = não instalar  

         1 = instalar  

    -   **Detalhes:** Especifica se pretende instalar a consola do Configuration Manager. Esta chave é necessária, exceto se a definição **ServerRecoveryOptions** tiver o valor **4**.  

-   **Nome da chave:** JoinCEIP  

    -   **Necessário:** Sim  

    -   **Valores:** 0 ou 1  

         0 = não aderir  

         1 = aderir  

    -   **Detalhes:** Especifica se pretende aderir o programa de melhoramento da experiência do cliente.  

**SQLConfigOptions**  

-   **Nome da chave:** SQLServerName  

    -   **Necessário:** Sim  

    -   **Valores:** *&lt;SQLServerName\>*  

    -   **Detalhes:** O nome do servidor ou nome da instância em cluster, a executar o SQL Server que alojará a base de dados do site. Terá de especificar o mesmo servidor que alojava a base de dados do site antes da falha.  

-   **Nome da chave:** DatabaseName  

    -   **Necessário:** Sim  

    -   **Valores:**  

         *&lt;SiteDatabaseName\>*  

         ou  

         *&lt;InstanceName\>*\\*&lt;SiteDatabaseName\>*  

    -   **Detalhes:** O nome da base de dados do SQL Server para criar ou utilizar para instalar a base de dados do site de administração central. Terá de especificar o nome da mesma base de dados que foi utilizada antes da falha.  

        > [!IMPORTANT]  
        >  Se não utilizar a instância predefinida, terá de especificar o nome da instância e o nome da base de dados do site.  

-   **Nome da chave:** SQLSSBPort  

    -   **Necessário:** Não  

    -   **Valores:** &lt;*SSBPortNumber*>  

    -   **Detalhes:** Especifique a porta do SQL Server Service Broker (SSB) utilizada pelo SQL Server. Normalmente, o SSB está configurado para utilizar a porta TCP 4022, mas são suportadas outras portas. Tem de especificar a mesma porta do SSB que foi utilizada antes da falha.  

#### <a name="recover-a-primary-site-unattended"></a>Recuperar um Site Primário em Modo Automático  
 Utilize as seguintes informações para configurar um ficheiro de script de configuração automática para recuperar um site de administração central.  

 **Identificação**  

-   **Nome da chave:** Ação  

    -   **Necessário:** Sim  

    -   **Valores:** RecoverPrimarySite  

    -   **Detalhes:** Recupera um site primário  

-   **Nome da chave:** CDLatest  

    -   **Necessário:** Sim – apenas quando utilizar suportes de dados a partir do CD. Pasta mais recente.    

    -   **Valores:** 1. qualquer valor diferente de 1 é considerada como não estar a utilizar o CD. Mais recente.

    -   **Detalhes:** O script tem de incluir este valor e chave quando executa a configuração a partir do suporte no CD. Pasta mais recente para efeitos de instalação de um site primário ou de administração central ou a recuperar um site primário ou de administração central. Este valor informa o programa de configuração que o suporte de dados de formulário CD. Está a ser utilizada a versão mais recente.

**RecoveryOptions**  

-   **Nome da chave:** ServerRecoveryOptions  

    -   **Necessário:** Sim  

    -   **Valores:** 1, 2 ou 4  

         1 = Servidor de site de recuperação e SQL Server.  

         2 = Recuperar apenas servidor de site.  

         4 = Recuperar apenas SQL Server.  

    -   **Detalhes:** Especifica se o programa de configuração irá recuperar o servidor do site, do SQL Server ou ambos. As chaves associadas são necessárias quando define o seguinte valor para a definição ServerRecoveryOptions:  

        -   **Valor = 1** : tem a opção de especificar um valor para a chave **SiteServerBackupLocation** para recuperar o site com uma cópia de segurança do site. Se não especificar um valor, o site será reinstalado sem ser restaurado a partir de um conjunto de cópias de segurança.  

             A chave **BackupLocation** é obrigatória se configurar o valor **10** para a chave **DatabaseRecoveryOptions** , para restaurar a base de dados do site a partir de uma cópia de segurança.  

        -   **Valor = 2** : tem a opção de especificar um valor para a chave **SiteServerBackupLocation** para recuperar o site com uma cópia de segurança do site. Se não especificar um valor, o site será reinstalado sem ser restaurado a partir de um conjunto de cópias de segurança.  

        -   **Valor = 4** : a chave **BackupLocation** é obrigatória se configurar o valor **10** para a chave **DatabaseRecoveryOptions** , que serve para restaurar a base de dados do site a partir de uma cópia de segurança.  

-   **Nome da chave:** DatabaseRecoveryOptions  

    -   **Necessário:** Talvez  

    -   **Valores:** 10, 20, 40, 80  

         10 = Restaurar a base de dados do site a partir de cópia de segurança.  

         20 = Utilizar uma base de dados do site que tenha sido recuperada manualmente utilizando outro método.  

         40 = Criar uma nova base de dados para o site. Utilize esta opção quando não estiver disponível nenhuma cópia de segurança da base de dados do site. Os dados globais e de site são recuperados através da replicação a partir de outros sites.  

         80 = ignorar recuperação da base de dados.  

    -   **Detalhes:** Especifica a forma como a configuração irá recuperar a base de dados do site no SQL Server. Esta chave é necessária quando a definição **ServerRecoveryOptions** tem o valor **1** ou **4**  

-   **Nome da chave:** SiteServerBackupLocation  

    -   **Necessário:** Não  

    -   **Valores:** &lt;PathToSiteServerBackupSet\>  

    -   **Detalhes:** Especifica o caminho para o conjunto de cópia de segurança de servidor de site. Esta chave é opcional se a definição **ServerRecoveryOptions** tiver o valor **1** ou **2**. Especifique um valor para a chave **SiteServerBackupLocation** para recuperar o site com uma cópia de segurança do mesmo. Se não especificar um valor, o site será reinstalado sem ser restaurado a partir de um conjunto de cópias de segurança.  

-   **Nome da chave:** BackupLocation  

    -   **Necessário:** Talvez  

    -   **Valores:** &lt;PathToSiteDatabaseBackupSet\>  

    -   **Detalhes:** Especifica o caminho para o conjunto de cópia de segurança de base de dados de site. A chave **BackupLocation** é obrigatória se configurar o valor **1** ou **4** na chave **ServerRecoveryOptions** e configurar o valor **10** na chave **DatabaseRecoveryOptions** .  

**Opções**  

-   **Nome da chave:** Iddoproduto  

    -   **Necessário:** Sim  

    -   **Valores:**  

         xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  

         Eval  

    -   **Detalhes:** O Configuration Manager instalação chave de produto, incluindo os traços. Introduza **Eval** pode instalar a versão de avaliação do Configuration Manager.  

-   **Nome da chave:** Código do site  

    -   **Necessário:** Sim  

    -   **Valores:** &lt;Código do site\>  

    -   **Detalhes:** Três carateres de alfanuméricos que identificam o site na sua hierarquia. Tem de especificar o código do site que era utilizado pelo site antes da falha.  

-   **Nome da chave:** SiteName  

    -   **Necessário:** Sim  

    -   **Valores:** SiteName  

    -   **Detalhes:** Descrição para este site.  

-   **Nome da chave:** SMSInstallDir  

    -   **Necessário:** Sim  

    -   **Valores:** &lt;*ConfigMgrInstallationPath*>  

    -   **Detalhes:** Especifica a pasta de instalação para os ficheiros de programa do Configuration Manager.  

        > [!NOTE]  
        >  Pode especificar o caminho original ou um novo caminho a utilizar para a instalação do Configuration Manager.  

-   **Nome da chave:** SDKServer  

    -   **Necessário:** Sim  

    -   **Valores:** &lt;*FQDN do fornecedor de SMS*>  

    -   **Detalhes:** Especifica o FQDN do servidor que alojará o fornecedor de SMS. Terá de especificar o servidor que hospedava o Fornecedor de SMS antes da falha.  

         Pode configurar Fornecedores de SMS adicionais para o site após a instalação inicial.  

-   **Nome da chave:** PrerequisiteComp  

    -   **Necessário:** Sim  

    -   **Valores:** 0 ou 1  

         0 = transferir  

         1 = já transferido  

    -   **Detalhes:** Especifica se os ficheiros de pré-requisitos de configuração já foram transferidos. Por exemplo, se utilizar o valor 0, o Programa de Configuração transferirá os ficheiros.  

-   **Nome da chave:** PrerequisitePath  

    -   **Necessário:** Sim  

    -   **Valores:** &lt;*PathToSetupPrerequisiteFiles*>  

    -   **Detalhes:** Especifica o caminho para os ficheiros de pré-requisitos do programa de configuração. Conforme o valor de **PrerequisiteComp** , a Configuração utiliza este caminho para armazenar os ficheiros transferidos ou localizar os ficheiros transferidos anteriormente.  

-   **Nome da chave:** AdminConsole  

    -   **Necessário:** Talvez  

    -   **Valores:** 0 ou 1  

         0 = não instalar  

         1 = instalar  

    -   **Detalhes:** Especifica se pretende instalar a consola do Configuration Manager. Esta chave é necessária, exceto se a definição **ServerRecoveryOptions** tiver o valor **4**.  

-   **Nome da chave:** JoinCEIP  

    -   **Necessário:** Sim  

    -   **Valores:** 0 ou 1  

         0 = não aderir  

         1 = aderir  

    -   **Detalhes:** Especifica se pretende aderir o programa de melhoramento da experiência do cliente.  

**SQLConfigOptions**  

-   **Nome da chave:** SQLServerName  

    -   **Necessário:** Sim  

    -   **Valores:** *&lt;SQLServerName\>*  

    -   **Detalhes:** O nome do servidor ou nome da instância em cluster, a executar o SQL Server que alojará a base de dados do site. Terá de especificar o mesmo servidor que alojava a base de dados do site antes da falha.  

-   **Nome da chave:** DatabaseName  

    -   **Necessário:** Sim  

    -   **Valores:**  

         *&lt;SiteDatabaseName\>*  

         ou  

         *&lt;InstanceName\>*\\*&lt;SiteDatabaseName\>*  

    -   **Detalhes:** O nome da base de dados do SQL Server para criar ou utilizar para instalar a base de dados do site de administração central. Terá de especificar o nome da mesma base de dados que foi utilizada antes da falha.  

        > [!IMPORTANT]  
        >  Se não utilizar a instância predefinida, terá de especificar o nome da instância e o nome da base de dados do site.  

-   **Nome da chave:** SQLSSBPort  

    -   **Necessário:** Não  

    -   **Valores:** &lt;*SSBPortNumber*>  

    -   **Detalhes:** Especifique a porta do SQL Server Service Broker (SSB) utilizada pelo SQL Server. Normalmente, o SSB está configurado para utilizar a porta TCP 4022, mas são suportadas outras portas. Tem de especificar a mesma porta do SSB que foi utilizada antes da falha.  

**ExpansionOption de hierarquia**  

-   **Nome da chave:** CCARSiteServer  

    -   **Necessário:** Talvez  

    -   **Valores:** &lt;*Códigodositedeadministraçãocentral*>  

    -   **Detalhes:** Especifica o site de administração central que um site primário se ligará quando aderir hierarquia do Configuration Manager. Esta definição é necessária se o site primário estava ligado a um site de administração central antes da falha. Tem de especificar o código do site que era utilizado para o site de administração central antes da falha.  

-   **Nome da chave:** CASRetryInterval  

    -   **Necessário:** Não  

    -   **Valores:** &lt;*Intervalo*>  

    -   **Detalhes:** Especifica o intervalo entre tentativas (em minutos) para estabelecer uma ligação para o site de administração central após a ligação falha. Por exemplo, se a ligação ao site de administração central falhar, o site primário aguarda o número de minutos que especificar para CASRetryInterval e, em seguida, tenta restabelecer a ligação.  

-   **Nome da chave:** WaitForCASTimeout  

    -   **Necessário:** Não  

    -   **Valores:** &lt;*Tempo limite*>  

    -   **Detalhes:** Especifica o valor de tempo limite máximo (em minutos) para um site primário ligar ao site de administração central. Por exemplo, se um site primário não conseguir ligar a um site de administração central, tenta efetuar de novo a ligação com base no CASRetryInterval, até atingir o WaitForCASTimeout. Pode especificar um valor entre 0 e 100.  

###  <a name="BKMK_PostRecovery"></a> Tarefas de pós-recuperação  
 Depois de recuperar o seu site, existem várias tarefas pós-recuperação que tem de considerar para concluir a recuperação do site. Utilize as secções seguintes para concluir o processo de recuperação do site.  

#### <a name="re-enter-user-account-passwords"></a>Reintroduzir palavras-passe de contas de utilizador  
 Após a recuperação de um servidor do site, as palavras-passe das contas de utilizador especificadas para o site tem de ser reintroduzidas, porque são repostas durante a recuperação do site. As contas são listadas na página **Terminado** do Assistente de Configuração após a recuperação do site ser concluída e guardada em C:\ConfigMgrPostRecoveryActions.html, no servidor de site recuperado.  

###### <a name="to-re-enter-user-account-passwords-after-site-recovery"></a>Para reintroduzir palavras-passe de contas de utilizador após a recuperação do site  

1.  Abra a consola do Configuration Manager e ligar ao site recuperado.  

2.  Na consola do Configuration Manager, clique em **Administração**.  

3.  Na área de trabalho **Administração** , expanda **Segurança**e clique em **Contas**.  

4.  Para cada conta na qual tenha de reintroduzir a palavra-passe, proceda do seguinte modo:  

    1.  Selecione a conta na lista de contas que foram identificadas depois da recuperação do site. Pode encontrar esta lista em C:\ConfigMgrPostRecoveryActions.html, no servidor do site recuperado.  

    2.  No separador **Home page** , no grupo **Propriedades** , clique em **Propriedades** para abrir as propriedades da conta.  

    3.  No separador **Geral** , clique em **Definir**e reintroduza as palavras-passe da conta.  

    4.  Clique em **Verificar**, selecione a origem de dados adequada para a conta de utilizador selecionada e clique em **Testar ligação** para verificar se a conta de utilizador se consegue ligar à origem de dados.  

    5.  Clique em **OK** para guardar as alterações de palavra-passe e, em seguida, clique em **OK**.  

#### <a name="re-enter-sideloading-keys"></a>Reintroduzir chaves de sideload  
 Após uma recuperação do servidor do site, é necessário reintroduzir as chaves de sideload do Windows especificadas para o site porque foram repostas durante a recuperação do site. Depois de introduzir novamente as chaves de sideload, a contagem no **ativações utilizadas** coluna de chaves de sideload do Windows é reposta na consola do Configuration Manager. Por exemplo, vamos supor que, antes da falha do site tem um **Total de ativações** estava definido como **100** e **ativações utilizadas** está **90** para o número de chaves que foram utilizadas pelos dispositivos. Após a recuperação do site, a coluna **Total de ativações** continua a apresentar **100**, mas a coluna **Ativações utilizadas** apresenta incorretamente **0**. No entanto, depois de 10 novos dispositivos utilizarem uma chave de sideload, não existirão chaves de sideload restantes e o dispositivo seguinte não conseguirá aplicar uma chave de sideload.  

#### <a name="recreate-the-microsoft-intune-subscription"></a>Recriar a subscrição do Microsoft Intune  
 Se recuperar um servidor de site do Configuration Manager após o computador do servidor de site é novamente instalado, a subscrição do Microsoft Intune não é restaurada. Tem de voltar a subscrição depois de recuperar o site.  Não crie um novo pedido de APN, mas em vez disso, carregar o atual válido ficheiro. pem-que foi carregado a última vez em gestão de iOS foi configurado ou renovada. Para obter mais informações, veja [Configurar a Subscrição do Microsoft Intune](/sccm/mdm/deploy-use/configure-intune-subscription).  

#### <a name="configure-ssl-for-site-system-roles-that-use-iis"></a>Configurar o SSL para funções do sistema de sites que utilizam IIS  
 Ao recuperar sistemas de sites que executam o IIS e estavam configurados para HTTPS antes da falha, é necessário reconfigurar o IIS para utilizar o certificado do servidor Web.  

#### <a name="reinstall-hotfixes-in-the-recovered-site-server"></a>Reinstalar correções no servidor do site recuperado  
 Após uma recuperação de site, é necessário reinstalar as correções que foram aplicadas ao servidor do site. Na página **Terminado** do Assistente de Configuração, é apresentada uma lista das correções instaladas anteriormente após a recuperação do site e guardada em **C:\ConfigMgrPostRecoveryActions.html** no servidor do site recuperado.  

#### <a name="recover-custom-reports-on-the-computer-running-reporting-services"></a>Recuperar relatórios personalizados no computador com o Reporting Services  
 Quando tiverem sido criados relatórios personalizados do Reporting Services e o Reporting Services falhar, é possível recuperar os relatórios se tiver sido efetuada uma cópia de segurança do servidor de relatórios. Para obter mais informações sobre o restauro de relatórios personalizados no Reporting Services, veja [Operações de Cópia de Segurança e Restauro de uma Instalação do Reporting Services](http://go.microsoft.com/fwlink/p/?LinkId=228724) na Documentação Online do SQL Server 2008.  

#### <a name="recover-content-files"></a>Recuperar ficheiros de conteúdo  
 A base de dados do site contém informações sobre o local onde os ficheiros de conteúdo estão armazenados no servidor do site, mas a cópia de segurança dos ficheiros de conteúdo e o seu restauro não são efetuados como parte do processo de cópia de segurança e restauro. Para recuperar os ficheiros de conteúdo na totalidade, é necessário restaurar a biblioteca de conteúdos e os ficheiros de origem do pacote para a localização original. Existem vários métodos para recuperar os ficheiros de conteúdo, mas o método mais simples consiste em restaurar os ficheiros a partir de uma cópia de segurança do sistema de ficheiros do servidor do site.  

 Se não possui uma cópia de segurança do sistema de ficheiros para os ficheiros do pacote de origem, terá de os copiar ou transferir manualmente tal como fez quando criou o pacote inicialmente. Pode executar a seguinte consulta no SQL Server para encontrar a localização de origem do pacote para todos os pacotes e aplicações: `SELECT * FROM v_Package`. Pode identificar o site de origem do pacote atravésdos primeiros três carateres do ID de pacote. Por exemplo, se o ID de pacote for CEN00001, o código de site do site de origem é CEN. Ao restaurar os ficheiros de origem do pacote, estes devem ser restaurados para a mesma localização em que se encontravam antes da falha.  

 Se não tiver uma cópia de segurança do sistema de ficheiros que contém a biblioteca de conteúdos, dispõe das seguintes opções de restauro:  

-   **Importar um ficheiro de conteúdo pré-configurado**: Quando tiver uma hierarquia do Configuration Manager, pode criar um ficheiro de conteúdo pré-configurado com todos os pacotes e aplicações a partir de outra localização e, em seguida, importar o ficheiro de conteúdo pré-configurado para recuperar a biblioteca de conteúdos no servidor do site.  

-   **Atualizar o conteúdo**: Quando inicia a ação de conteúdo da atualização para um tipo de implementação do pacote ou aplicação, o conteúdo é copiado da origem do pacote para a biblioteca de conteúdos. Os ficheiros de origem do pacote têm de estar disponíveis na localização original para que esta ação seja concluída com êxito. É necessário executar esta ação em cada pacote e em cada aplicação.  

#### <a name="recover-custom-software-updates-on-the-computer-running-updates-publisher"></a>Recuperar atualizações de software personalizadas no computador com o Updates Publisher  
 Quando tiver incluído os ficheiros de base de dados do Updates Publisher no seu plano de cópia de segurança, pode recuperar as bases de dados em caso de falha no computador no qual é executado o Updates Publisher. Para obter mais informações sobre o Updates Publisher, veja [System Center Updates Publisher 2011](http://go.microsoft.com/fwlink/p/?LinkId=228726) na Biblioteca TechCenter do System Center.  

 Utilize o procedimento seguinte para restaurar a base de dados do Updates Publisher.  

###### <a name="to-restore-the-updates-publisher-2011-database"></a>Para restaurar a base de dados do Updates Publisher 2011  

1.  Reinstale o Updates Publisher no computador recuperado.  

2.  Copie o ficheiro de base de dados (scupdb) do destino da cópia de segurança para %*USERPROFILE*%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\ no computador que executa o Updates Publisher.  

3.  Quando mais do que um utilizador com o Updates Publisher no computador, tem de copiar cada ficheiro de base de dados para a localização de perfil de utilizador adequada.  

#### <a name="user-state-migration-data"></a>Dados de migração de estado de utilizador  
 Como parte das propriedades do sistema de sites do ponto de migração de estado, deve especificar as pastas que armazenam dados de migração de estado de utilizador. Depois de recuperar um servidor com uma pasta que armazena dados de migração de estado de utilizador, tem de restaurar manualmente os dados de migração de estado de utilizador no servidor para a mesma pasta que armazenava os dados antes da falha.  

#### <a name="regenerate-the-certificates-for-distribution-points"></a>Gerar novamente os certificados para pontos de distribuição  
 Depois de restaurar um site, o distmgr pode conter a seguinte entrada para um ou mais pontos de distribuição: **Falha ao desencriptar certificado PFX dados**. Esta entrada indica que não é possível desencriptar os dados de certificado do ponto de distribuição pelo site. Para resolver este problema tem de voltar a gerar ou voltar a importar o certificado dos pontos de distribuição afetados. Pode fazê-lo com o cmdlet do PowerShell [Set-CMDistributionPoint](https://technet.microsoft.com/library/jj821872\(v=sc.20\).aspx).  

#### <a name="update-certificates-used-for-cloud-based-distribution-points"></a>Atualizar Certificados Utilizados para pontos de distribuição Baseados na Nuvem  
 O Configuration Manager requer um certificado de gestão que é utilizado para o servidor de sites para comunicação de ponto de distribuição baseado na nuvem. Após uma recuperação de site, é necessário atualizar os certificados dos pontos de distribuição baseados na nuvem.  

####  <a name="BKMK_RecoverSecondarySite"></a> Recuperar um site secundário  
 O Configuration Manager não suporta a cópia de segurança da base de dados num site secundário, mas suporta a recuperação através da reinstalação do site secundário. Recuperação do site secundário é necessária quando ocorre uma falha num site secundário do Configuration Manager. Pode recuperar um site secundário utilizando a **recuperar Site secundário** ação a partir de **Sites** nó na consola do Configuration Manager. Ao contrário da recuperação de um site de administração central ou site primário, a recuperação de um site secundário não utiliza um ficheiro de cópia de segurança e, em vez disso, reinstala os ficheiros do site secundário no computador do site secundário que falhou. Em seguida, os dados do site secundário são reinicializados com dados do site primário principal. Durante o processo de recuperação, o Gestor de configuração verifica se a biblioteca de conteúdos existe no computador do site secundário e que o conteúdo apropriado está disponível. O site secundário utilizará a biblioteca de conteúdos existente, caso contenha o conteúdo apropriado. Caso contrário, a recuperação da biblioteca de conteúdos de um site secundário recuperado requer a redistribuição ou pré-configuração do conteúdo para esse site recuperado. Quando tem um ponto de distribuição que não se encontra no site secundário, não é necessário reinstalar o ponto de distribuição durante a recuperação do site secundário. Após a recuperação do site secundário, o site sincroniza automaticamente com o ponto de distribuição.  

 Pode verificar o estado da recuperação de site secundário, utilizando o **Mostrar estado da instalação** ação a partir de **Sites** nó na consola do Configuration Manager.  

> [!IMPORTANT]  
>  Tem de utilizar um computador com a mesma configuração do computador que falhou, tal como o seu FQDN, para recuperar com êxito o site secundário. O computador também tem de cumprir todos os pré-requisitos de site secundário e ter direitos de segurança apropriados configurados. Além disso, utilize o mesmo caminho de instalação que foi utilizado para o site que falhou.  

> [!IMPORTANT]  
>  Durante uma recuperação de site secundário, do Configuration Manager instala o SQL Server Express se não estiver instalado no computador. Por conseguinte, antes de recuperar um site secundário, tem de instalar manualmente o SQL Server Express ou o SQL Server. Tem de utilizar a mesma versão do SQL Server e a mesma instância do SQL Server que utilizou para a base de dados do site secundário antes da falha.  

##  <a name="BKMK_SMSWriterService"></a> Serviço SMS Writer  
 O SMS Writer é um serviço que interage com o Serviço de Cópia Sombra de Volumes (VSS) durante o processo de cópia de segurança. Conclua o SMS Writer serviço tem de executar para trás de site do Configuration Manager até com êxito.  

### <a name="purpose"></a>Objetivo  
 O SMS Writer é registado junto do serviço VSS, ligando-se às respetivas interfaces e eventos. Quando o VSS difunde eventos ou envia notificações específicas para o SMS Writer, o SMS Writer responde à notificação e executa a ação adequada. O SMS Writer lê o ficheiro de controlo de cópia de segurança (smsbkup), localizado no &lt; *caminho de instalação do ConfigMgr*> \inboxes\smsbkup.box e determina os ficheiros e dados que está a ser efetuada a cópia de segurança. O SMS Writer cria metadados, que consistem em diversos componentes, com base nestas informações, bem como em dados específicos da chave e subchaves de registo do SMS. Quando solicitado, envia os metadados para o VSS. O VSS, em seguida, envia os metadados para a aplicação requerente, Gestor de cópia de segurança do Configuration Manager. O Backup Manager seleciona os dados de que será efetuada cópia de segurança e envia-os para o SMS Writer através do VSS. O SMS Writer executa os passos adequados para preparar a cópia de segurança. Mais tarde, quando o VSS estiver pronto para tirar o instantâneo, enviará um evento e o SMS Writer deixa de todos os serviços do Configuration Manager e assegura que as atividades do Configuration Manager são interrompidas durante a criação do instantâneo. Após a conclusão do instantâneo, o SMS Writer reiniciará os serviços e atividades.  

 O serviço SMS Writer é instalado automaticamente. Tem de estar em execução quando a aplicação VSS solicita uma cópia de segurança ou restauro.  

### <a name="writer-id"></a>ID do escritor  
 O ID de escritor para o SMS Writer é: 03ba67dd-dc6d-4729-a038-251f7018463b.  

### <a name="permissions"></a>Permissões  
 O serviço SMS Writer tem de ser executado sob a conta do Sistema Local.  

### <a name="volume-shadow-copy-service"></a>Serviço de Cópia Sombra de Volumes  
 O VSS é um conjunto de APIs COM que implementa uma estrutura para permitir a execução de cópias de segurança de volume enquanto as aplicações do sistema continuam a escrever nos volumes. O VSS fornece uma interface consistente que permite coordenar as aplicações de utilizador que atualizam dados no disco (o serviço SMS Writer) com as que efetuam cópias de segurança das aplicações (o serviço Backup Manager). Para obter mais informações sobre o VSS, veja o tópico [Volume Shadow Copy Service (Serviço de Cópia Sombra de Volumes)](http://go.microsoft.com/fwlink/p/?LinkId=241968) no Windows Server TechCenter.  

