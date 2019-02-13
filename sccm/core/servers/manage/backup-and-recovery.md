---
title: Sites de cópia de segurança
titleSuffix: Configuration Manager
description: Aprenda a criar cópias de segurança dos sites antes do evento de falha ou perda de dados no Configuration Manager.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: f7832d83-9ae2-4530-8a77-790e0845e12f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e876e34929479654240ff220c3cad91043da0f83
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56123142"
---
# <a name="back-up-a-configuration-manager-site"></a>Efetuar uma Cópia de Segurança de um Site do Gestor de Configuração

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Prepare a cópia de segurança e recuperação abordagens para evitar a perda de dados. Para sites do Configuration Manager, uma abordagem de cópia de segurança e recuperação pode ajudá-lo a recuperar sites e hierarquias mais rapidamente e com as perdas de dados.  

As secções neste artigo podem ajudá-lo a cópia de segurança de seus sites. Para recuperar um site, consulte [recuperação no Configuration Manager](/sccm/core/servers/manage/recover-sites).  



## <a name="considerations-before-creating-a-backup"></a>Considerações antes de criar uma cópia de segurança  

-   Se utilizar um grupo de disponibilidade Always On do SQL Server para alojar a base de dados do site: Modificar seus planos de cópia de segurança e recuperação conforme descrito em [preparar para utilizar o SQL Server Always On](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#changes-for-site-backup).  

-   O Configuration Manager pode recuperar a base de dados do site da tarefa de cópia de segurança do Configuration Manager. Ele também pode utilizar uma cópia de segurança da base de dados do site que criar com outro processo.   

     Por exemplo, pode restaurar a base de dados a partir de uma cópia de segurança que é criada como parte de um plano de manutenção do Microsoft SQL Server. Também pode utilizar uma cópia de segurança que é criada utilizando o Data Protection Manager para criar cópias de segurança da base de dados do site.  

-   A partir da versão 1806, instalar um servidor de sites adicionais na *passivo* modo. O servidor de site em modo passivo está além do seu servidor de sites existente no *Active Directory* modo. Um servidor de site em modo passivo está disponível para uso imediato, quando necessário. Para obter mais informações, consulte [elevada disponibilidade do servidor do Site](/sccm/core/servers/deploy/configure/site-server-high-availability). Embora esta função não remove a necessidade de operações de cópia de segurança e recuperação de prática e de plano para, reduz consideravelmente o esforço para recuperar um site quando necessário.  
  

####  <a name="using-data-protection-manager-to-back-up-your-site-database"></a>Utilizar o Data Protection Manager para efetuar cópias de segurança da base de dados do site
Pode utilizar o System Center Data Protection Manager (DPM) para criar cópias de segurança da base de dados do site do Configuration Manager.

Crie um novo grupo de proteção no DPM para o computador de base de dados do site. Sobre o **selecionar membros do grupo** página a criar novo grupo do Assistente de proteção, selecionar o serviço SMS Writer na lista de origem de dados. Em seguida, selecione a base de dados do site como membro apropriado. Para obter mais informações sobre como utilizar o DPM, consulte a [Data Protection Manager](https://docs.microsoft.com/system-center/dpm) biblioteca de documentação.  

> [!IMPORTANT]  
>  O Configuration Manager não suporta a cópia de segurança do DPM para um cluster de SQL Server que utiliza uma instância nomeada. Ele oferece suporte a cópia de segurança do DPM num cluster do SQL Server que utiliza a instância predefinida do SQL Server.  

Depois de restaurar a base de dados, siga os passos de configuração para recuperar o site. Para utilizar a base de dados que criou cópias de segurança com o Data Protection Manager, selecione a opção de recuperação para **utilizar uma base de dados do site que foi recuperado manualmente**.  



## <a name="backup-maintenance-task"></a>Tarefa de manutenção de cópias de segurança
Pode automatizar a cópia de segurança para sites do Configuration Manager ao agendar a tarefa de manutenção do servidor do Site de cópia de segurança predefinida. Esta tarefa tem as seguintes funcionalidades:

-   É executada de acordo com um agendamento
-   Faz uma cópia de segurança da base de dados do site
-   Faz uma cópia de segurança de chaves de registo específicas
-   Faz uma cópia de segurança de pastas e ficheiros específicos
-   Cria cópias de segurança a [CD. Pasta mais recente](/sccm/core/servers/manage/the-cd.latest-folder)   

Plano para executar a tarefa de cópia de segurança do site predefinido no mínimo a cada cinco dias. Esta agenda é porque o Configuration Manager utiliza um *alterações do SQL Server, o período de retenção do registo* de cinco dias. Para obter mais informações, consulte [alterações do SQL Server, o período de retenção do registo](/sccm/protect/understand/recover-sites#bkmk_SQLretention).

Para simplificar o processo de cópia de segurança, pode criar uma **Afterbackup** ficheiro. Este script é executado automaticamente ações pós-cópia de segurança depois da tarefa de cópia de segurança é concluída com êxito. Utilize o ficheiro Afterbackup bat para arquivar o instantâneo da cópia de segurança para uma localização segura. Também pode utilizar o ficheiro Afterbackup bat para copiar ficheiros para a pasta de cópia de segurança ou para iniciar outras tarefas de cópia de segurança.  

Pode fazer backup de um site de administração central e site primário. Os sites secundários ou servidores de sistema de sites não tem tarefas de cópia de segurança.

Quando o serviço de cópia de segurança do Configuration Manager é executado, segue as instruções definidas no ficheiro de controlo de cópia de segurança: `<ConfigMgrInstallationFolder>\Inboxes\Smsbkup.box\Smsbkup.ctl`. É possível modificar o ficheiro de controlo da cópia de segurança para alterar o comportamento do serviço de cópia de segurança.  

As informações de estado da cópia de segurança do site são escritas no ficheiro **Smsbkup.log** . Este ficheiro é criado na pasta de destino que especificar nas propriedades da tarefa de manutenção do servidor do Site de cópia de segurança.  

#### <a name="to-enable-the-site-backup-maintenance-task"></a>Para ativar a tarefa de cópia de segurança de manutenção do site  
1.  Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **configuração do Site**e selecione o **Sites** nó.  

2.  Selecione o site para o qual pretende ativar a tarefa de manutenção cópia de segurança do site.  

3.  Clique em **tarefas de manutenção do Site** na faixa de opções.  

4.  Selecione o **servidor do Site de cópia de segurança** de tarefas e clique em **editar**.  

5.  Selecione a opção para **ativar esta tarefa**. Clique em **definir caminhos** para especificar o destino de cópia de segurança. Tem as seguintes opções:  

    > [!IMPORTANT]  
    >  Para ajudar a impedir a adulteração dos ficheiros de cópia de segurança, armazenar os ficheiros numa localização segura. O caminho de cópia de segurança mais seguro é numa unidade local, para que possa definir permissões de ficheiros NTFS na pasta. O Configuration Manager não encriptar os dados de cópia de segurança que são armazenados no caminho de cópia de segurança.  

    -   **Unidade local no servidor do site para dados do site e base de dados**: Especifica que a tarefa armazena os ficheiros de cópia de segurança para o site e base de dados do site no caminho especificado na unidade de disco local do servidor do site. Crie a pasta local antes da tarefa de cópia de segurança é executada. A conta Sistema Local no servidor do site tem de ter **escrever** permissões de ficheiros NTFS na pasta local para a cópia de segurança do servidor do site. A conta Sistema Local no computador que está a executar o SQL Server deve ter **escrever** permissões NTFS para a pasta para a cópia de segurança de base de dados do site.  

    -   **O caminho de rede (nome UNC) para dados do site e base de dados**: Especifica que a tarefa armazena os ficheiros de cópia de segurança para o site e base de dados do site no caminho de rede especificado. Crie a partilha antes da tarefa de cópia de segurança é executada. A conta de computador do servidor do site tem de ter **escrever** permissões de NTFS e de partilha para a pasta de rede partilhada. Se o SQL Server estiver instalado noutro computador, a conta de computador do SQL Server tem de ter as mesmas permissões.  

    -   **Unidades locais no servidor do site e o SQL Server**: Especifica que a tarefa armazena os ficheiros de cópia de segurança para o site no caminho especificado na unidade local do servidor do site. A tarefa armazena os ficheiros de cópia de segurança da base de dados do site no caminho especificado na unidade local do servidor de base de dados do site. Crie as pastas locais antes da tarefa de cópia de segurança é executada. A conta de computador do servidor de site tem de ter permissões de **Escrita** de NTFS na pasta que criar no servidor de site. A conta de computador do SQL Server tem de ter permissões de **Escrever** de NTFS na pasta que criar no servidor de base de dados do site. Esta opção só está disponível quando a base de dados do site não está instalado no servidor do site.  

    > [!NOTE]  
    >   A opção de navegar para o destino de cópia de segurança só está disponível quando especificar o caminho de rede do destino de cópia de segurança.  
    >  
    > O nome da pasta ou o nome de partilha que é utilizado para o destino de cópia de segurança não suporta a utilização de carateres Unicode.  

6.  Configure um agendamento para a tarefa de cópia de segurança do site. Considere uma agenda de cópia de segurança que está fora horário de trabalho. Se tiver uma hierarquia, considere uma agenda que é executado, pelo menos, duas vezes por semana. Se o site falhar, esta agenda garante retenção máxima de dados.  

    Quando executa a consola do Configuration Manager no mesmo servidor do site que estiver a configurar para cópia de segurança, a tarefa de cópia de segurança utiliza a hora local para a agenda. Quando executa a consola do Configuration Manager a partir de outro computador, a tarefa de cópia de segurança utiliza Hora Universal Coordenada (UTC) para a agenda.  

7.  Escolha se pretende criar um alerta se a tarefa de cópia de segurança do site falhar. Quando selecionada, o Configuration Manager cria um alerta crítico para a falha da cópia de segurança. Pode rever estes alertas no **alertas** nó da **monitorização** área de trabalho.  

#### <a name="verify-that-the-backup-site-server-maintenance-task-is-running"></a>Certifique-se de que a tarefa de manutenção do servidor do Site de cópia de segurança está em execução  

-   Verifique o carimbo de hora nos ficheiros na pasta de destino de cópia de segurança que a tarefa de criar. Certifique-se de que o período de tempo de atualizações para a hora quando a tarefa pela última vez foi agendada para ser executada.  

-   Vá para o **estado do componente** nó da **monitorização** área de trabalho. Consulte as mensagens de estado para **SMS_SITE_BACKUP**. Quando a cópia de segurança do site for concluída com êxito, verá o ID da mensagem **5035**. Esta mensagem indica que a cópia de segurança do site foi concluída sem erros.  

-   Ao configurar a tarefa de cópia de segurança para criar um alerta quando ocorre uma falha, procure os alertas de falhas de cópia de segurança no **alertas** nó da **monitorização** área de trabalho.  

-   Abra o Explorador do Windows no servidor do site e navegue para `<ConfigMgrInstallationFolder>\Logs`. Revisão **smsbkup** avisos e erros. Quando a cópia de segurança do site é concluída com êxito, o log mostra `Backup completed` com o ID de mensagem `STATMSG: ID=5035`.  

    > [!TIP]  
    >  Quando a tarefa de manutenção cópia de segurança falhar, reinicie a tarefa de cópia de segurança, interromper e reiniciar o **SMS_SITE_BACKUP** serviço do Windows.  



## <a name="archive-the-backup-snapshot"></a>Arquivar o instantâneo da cópia de segurança  
A tarefa de cópia de segurança cria um instantâneo de cópia de segurança na primeira vez que ele é executado. Pode utilizar este instantâneo para recuperar o servidor de site se falhar. Quando a tarefa de cópia de segurança é novamente executada numa agenda, ele cria um novo instantâneo de cópia de segurança que substitui o anterior. Como resultado, o site tem apenas um único instantâneo de cópia de segurança, e não tem nenhuma forma de recuperar um instantâneo de cópia de segurança anteriormente.  

Mantenha vários arquivos de instantâneo de cópia de segurança pelos seguintes motivos:  

-   É comum para suporte de dados de cópia de segurança efetuar a ativação, sejam perdidos ou incluir apenas uma cópia de segurança parcial. Recuperar um site primário autónomo em falha a partir de uma cópia de segurança mais antiga é melhor do que recuperar sem qualquer cópia de segurança. Para um servidor de site numa hierarquia, a cópia de segurança tem de estar no período de retenção do registo de alterações do SQL Server ou a cópia de segurança não é necessária.  

-   Determinados danos no site podem não ser detetados durante vários ciclos de cópia de segurança. Pode ter de utilizar uma cópia de segurança instantâneo antes do site ter ficado danificado. Esta razão aplica-se a um site primário autónomo e a sites numa hierarquia onde a cópia de segurança está no SQL Server alterar o período de retenção do registo.  

-   O site não pode ter nenhum instantâneo de cópia de segurança de todo. Por exemplo, se falhar a tarefa de manutenção do servidor do Site de cópia de segurança. Uma vez que a tarefa de cópia de segurança remove o instantâneo de cópia de segurança anterior antes de iniciar a cópia de segurança dos dados atuais, não haverá um instantâneo de cópia de segurança válido.  



## <a name="using-the-afterbackupbat-file"></a>Utilizar o Ficheiro AfterBackup.bat  
Depois de backup com êxito o site, a tarefa de cópia de segurança automaticamente tenta executar um script chamado **Afterbackup**. Criar manualmente o ficheiro Afterbackup bat no servidor do site no `<ConfigMgrInstallationFolder>\Inboxes\Smsbkup.box`. Se existir um ficheiro Afterbackup bat na pasta correta, ele será executado automaticamente depois de concluída a tarefa de cópia de segurança.

O ficheiro Afterbackup bat permite arquivar o instantâneo da cópia de segurança no final de cada operação de cópia de segurança. Pode executar automaticamente outras tarefas de pós-cópia de segurança que não fazem parte da tarefa de manutenção do servidor do Site de cópia de segurança. O ficheiro AfterBackup.bat integra o arquivo e as operações de cópia de segurança, assegurando que cada novo instantâneo de cópia de segurança é arquivado.

Se o ficheiro Afterbackup bat não estiver presente, a tarefa de cópia de segurança ignora-o sem efeito sobre a operação de cópia de segurança. Para verificar se a tarefa de cópia de segurança executou com êxito este script, vá para o **estado do componente** nó a **monitorização** área de trabalho e reveja as mensagens de estado para **SMS_SITE_BACKUP**. Quando a tarefa ser iniciada com êxito o ficheiro de comandos Afterbackup, consulte o ID da mensagem **5040**.  

> [!TIP]  
>  Para arquivar os seus ficheiros de cópia de segurança de servidor de site com Afterbackup, tem de utilizar uma ferramenta de comando de cópia do arquivo em lotes. Uma dessas ferramentas é [Robocopy](https://docs.microsoft.com/windows-server/administration/windows-commands/robocopy) no Windows Server. Por exemplo, crie o ficheiro Afterbackup bat com o seguinte comando: `Robocopy E:\ConfigMgr_Backup \\ServerName\ShareName\ConfigMgr_Backup /MIR`  

Embora a utilização prevista do Afterbackup seja arquivar instantâneos de cópia de segurança, pode criar um ficheiro Afterbackup bat para executar tarefas adicionais no final de cada operação de cópia de segurança.  



##  <a name="supplemental-backup-tasks"></a>Tarefas suplementares de cópia de segurança  
A tarefa de manutenção cópia de segurança do Site Server fornece um instantâneo de cópia de segurança para os ficheiros de servidor de site e base de dados do site. Existem outros itens não uma cópia de segurança que tem de considerar ao criar a sua estratégia de cópia de segurança. Utilize estas secções para ajudar a concluir sua estratégia de cópia de segurança do Configuration Manager.  

### <a name="back-up-custom-reports"></a>Fazer uma cópia de segurança dos relatórios personalizados   
Se modificar predefinidos ou criados relatórios personalizados no SQL Server Reporting Services, crie uma cópia de segurança para o relatório de arquivos de banco de dados do servidor. A cópia de segurança do servidor de relatório tem de incluir os seguintes componentes:
- Os ficheiros de origem para relatórios e modelos
- Chaves de encriptação
- Assemblagens ou extensões personalizadas
- Ficheiros de configuração
- Vistas personalizadas do SQL Server utilizadas nos relatórios personalizados
- Procedimentos armazenados personalizados  

> [!IMPORTANT]  
>  Quando o Configuration Manager atualiza-se numa versão mais recente, os relatórios predefinidos podem ser substituídos por novos relatórios. Se modificar um relatório predefinido, certifique-se fazer uma cópia de segurança do relatório e, em seguida, restaure-o no Reporting Services.  

Para obter mais informações sobre cópias de segurança relatórios personalizados no Reporting Services, consulte [cópia de segurança e as operações de restauro de mensagens em fila para o Reporting Services](https://docs.microsoft.com/sql/reporting-services/install-windows/backup-and-restore-operations-for-reporting-services).  

### <a name="back-up-content-files"></a>Fazer cópias de segurança de ficheiros de conteúdo  
A biblioteca de conteúdos no Configuration Manager é a localização onde todos os ficheiros de conteúdo são armazenados para todas as implementações de software. A biblioteca de conteúdos está localizada no servidor do site e em cada ponto de distribuição. A tarefa de manutenção do servidor do Site de cópia de segurança não fazer cópias de segurança a biblioteca de conteúdos ou ficheiros de origem do pacote. Quando um servidor de site falha, as informações sobre a biblioteca de conteúdos são restauradas para a base de dados do site, mas tem de restaurar os ficheiros de origem de biblioteca e o pacote de conteúdos.  

-   A biblioteca de conteúdos tem de ser restaurada antes de pode redistribuir o conteúdo para pontos de distribuição. Quando começa a redistribuição de conteúdo, o Configuration Manager copia os ficheiros da biblioteca de conteúdos do servidor do site para os pontos de distribuição. Para obter mais informações, consulte [a biblioteca de conteúdos](/sccm/core/plan-design/hierarchy/the-content-library).  

-   Os ficheiros de origem do pacote devem ser restaurados antes de poder atualizar conteúdo em pontos de distribuição. Quando iniciar uma atualização de conteúdo, o Configuration Manager copia ficheiros novos ou modificados da origem do pacote para a biblioteca de conteúdos. Em seguida, copia os ficheiros para pontos de distribuição associados. Execute a seguinte consulta do SQL Server na base de dados do site para encontrar a localização de origem do pacote para todos os pacotes e aplicações: `SELECT * FROM v_Package`. Pode identificar o site de origem do pacote atravésdos primeiros três carateres do ID de pacote. Por exemplo, se o ID de pacote for CEN00001, o código de site do site de origem é CEN. Ao restaurar os ficheiros de origem do pacote, estes devem ser restaurados para a mesma localização em que eram antes da falha.  

Certifique-se de que inclui tanto os conteúdo biblioteca e o pacote de ficheiros de origem na sua cópia de segurança do sistema de ficheiros para o servidor do site.  

### <a name="back-up-custom-software-updates"></a>Cópia de segurança de atualizações de software personalizadas  
System Center Updates Publisher é uma ferramenta autónoma que lhe permite gerir atualizações de software personalizadas. Publicador de atualizações utiliza uma base de dados local para o repositório de atualização de software. Quando utilizar o Updates Publisher para gerir atualizações de software personalizadas, determine se deve incluir a base de dados do Updates Publisher no seu plano de cópia de segurança. Para obter mais informações, consulte [System Center Updates Publisher](/sccm/sum/tools/updates-publisher).  

Utilize o procedimento seguinte para criar cópias de segurança da base de dados do Updates Publisher.  

#### <a name="back-up-the-updates-publisher-database"></a>Criar cópias de segurança da base de dados do Updates Publisher  

1.  No computador que executa o Updates Publisher, procure o ficheiro de base de dados do Updates Publisher **scupdb** no `%USERPROFILE%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\`. Existe um ficheiro de base de dados diferente para cada utilizador que executa o Updates Publisher.  

2.  Copie o ficheiro de base de dados para o destino de cópia de segurança. Por exemplo, se for do seu destino de cópia de segurança `E:\ConfigMgr_Backup`, pode copiar o ficheiro de base de dados do Updates Publisher para `E:\ConfigMgr_Backup\SCUP`.  

    > [!TIP]  
    >  Quando existe mais do que um ficheiro de base de dados num computador, considere armazenar o ficheiro numa subpasta que indica o perfil de utilizador associado ao ficheiro de base de dados. Por exemplo, poderia ter um ficheiro de base de dados `E:\ConfigMgr_Backup\SCUP\User1` e o outro ficheiro de base de dados na `E:\ConfigMgr_Backup\SCUP\User2`.  



## <a name="user-state-migration-data"></a>Dados de migração de estado de utilizador  
Pode utilizar sequências de tarefas do Configuration Manager para capturar e restaurar dados de perfil do usuário nos cenários de implementação do sistema operacional. As propriedades do ponto de migração de estado de listam as pastas que armazenam os dados de estado do utilizador. Estes dados não não uma cópia de segurança como parte da tarefa de manutenção cópia de segurança de servidor de Site. Como parte do seu plano de cópia de segurança, tem de copiar manualmente as pastas que especificar para armazenar os dados de migração de estado do utilizador.   

### <a name="determine-the-folders-used-to-store-user-state-migration-data"></a>Determinar as pastas utilizadas para armazenar dados de migração de perfil do usuário  

1.  Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **configuração do Site**e selecione o **servidores e funções de sistema de sites** nó.  

2.  Selecione o sistema de sites que aloja a função de migração de estado. Em seguida, selecione **ponto de migração de estado** no **funções do sistema de sites** painel.  

3.  Clique em **propriedades** na faixa de opções.  

4.  As pastas que armazenam os dados de migração de estado do utilizador são listadas na secção **Detalhes da pasta** , no separador **Geral** .  



## <a name="about-the-sms-writer-service"></a>Sobre o serviço SMS Writer  
O SMS Writer é um serviço que interage com o Windows Volume de cópia sombra Service (VSS) durante o processo de cópia de segurança. O serviço SMS Writer tem de executar para o site do Configuration Manager até concluída com êxito.  

### <a name="process"></a>Processo  
1. O SMS Writer é registado junto do serviço VSS, ligando-se às respetivas interfaces e eventos. 
2. Quando o VSS difunde eventos ou envia notificações específicas para o SMS Writer, o SMS Writer responde à notificação e executa a ação adequada. 
3. O SMS Writer lê o ficheiro de controlo da cópia de segurança **smsbkup** localizados em `<ConfigMgrInstallationPath>\inboxes\smsbkup.box`e determina os ficheiros e dados para criar cópias de segurança. 
4. O SMS Writer cria metadados, que consiste em vários componentes, incluindo dados específicos da chave de registo SMS e subchaves. 
    a. Quando solicitado, envia os metadados para o VSS. 
    b. Em seguida, o VSS envia os metadados para a aplicação requerente, o Gestor de cópia de segurança do Configuration Manager. 
5. Backup Manager seleciona os dados de cópia de segurança e envia estes dados para o SMS Writer através do VSS. 
6. O SMS Writer executa os passos adequados para preparar a cópia de segurança. 
7. Posteriormente, quando o VSS estiver pronto para tirar o instantâneo: um. Envia um evento b. O SMS Writer interromperá todos os c de serviços do Configuration Manager. Ele garante que as atividades do Configuration Manager são interrompidas durante a criação do instantâneo. 
8. Após a conclusão do instantâneo, o SMS Writer reiniciará os serviços e atividades.

O serviço SMS Writer é instalado automaticamente. Tem de estar em execução quando a aplicação VSS solicita uma cópia de segurança ou restauro.  

### <a name="writer-id"></a>ID do escritor  
O ID de escritor para o SMS Writer é **03ba67dd-dc6d-4729-a038-251f7018463b**.  

### <a name="permissions"></a>Permissões  
O serviço SMS Writer tem de ser executado sob a conta do Sistema Local.  

### <a name="volume-shadow-copy-service"></a>Serviço de Cópia Sombra de Volumes  
O VSS é um conjunto de APIs COM que implementa uma estrutura para permitir a execução de cópias de segurança de volume enquanto as aplicações do sistema continuam a escrever nos volumes. O VSS fornece uma interface consistente que permite coordenar as aplicações de utilizador que atualizam dados no disco (o serviço SMS Writer) com as que efetuam cópias de segurança das aplicações (o serviço Backup Manager). Para obter mais informações, consulte a [serviço de cópia de sombra de volumes](https://go.microsoft.com/fwlink/p/?LinkId=241968).  



## <a name="next-steps"></a>Passos seguintes
Depois de criar uma cópia de segurança, praticar [recuperação de sites](/sccm/protect/understand/recover-sites) com essa cópia de segurança. Esta prática pode ajudá-lo a se familiarizar com o processo de recuperação antes de precisa contar com ele. Também pode ajudar a confirmar que a cópia de segurança foi concluída com êxito para o objetivo pretendido.  
