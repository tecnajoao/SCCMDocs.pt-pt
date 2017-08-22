---
title: "Cópia de segurança de sites | Microsoft Docs"
description: "Saiba como efetuar cópias dos seus sites antes do evento de falha ou perda de dados no System Center Configuration Manager."
ms.custom: na
ms.date: 6/5/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7832d83-9ae2-4530-8a77-790e0845e12f
caps.latest.revision: "22"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 7deb00d4b67eabf3238907b337a9d0367c3d99cc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="back-up-a-configuration-manager-site"></a>Efetuar uma Cópia de Segurança de um Site do Gestor de Configuração

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Prepare a cópia de segurança e recuperação abordagens para evitar a perda de dados. Para sites do Configuration Manager, uma abordagem de cópia de segurança e recuperação pode ajudar a recuperar sites e hierarquias mais rapidamente bem como as perdas de dados.  

As secções neste tópico podem ajudar a fazer cópia de segurança os sites. Para recuperar um site, consulte [recuperação para o Configuration Manager](/sccm/protect/understand/recover-sites).  

## <a name="considerations-before-creating-a-backup"></a>Considerações sobre antes de criar uma cópia de segurança  
-   **Se utilizar um grupo de disponibilidade SQL Server Always On para alojar a base de dados do site:** Modifique os planos de cópia de segurança e recuperação conforme descrito em [preparar para utilizar o SQL Server Always On](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#changes-for-site-backup).

-   O Configuration Manager pode recuperar a base de dados da tarefa de manutenção cópia de segurança do Configuration Manager ou a partir de uma cópia de segurança de base de dados de site que criar com outro processo.   

    Por exemplo, pode restaurar a base de dados do site de uma cópia de segurança que é criada como parte de um plano de manutenção do Microsoft SQL Server. Também pode utilizar uma cópia de segurança que é criada pelo utilizando o Data Protection Manager para criar cópias de segurança da base de dados do site (DPM).

####  <a name="using-data-protection-manager-to-back-up-your-site-database"></a>Utilizar o Data Protection Manager para efetuar cópias de segurança da base de dados do site
Pode utilizar o System Center 2012 Data Protection Manager (DPM) para criar uma cópia de segurança da base de dados do site.

Terá de criar um novo grupo de proteção no DPM para o computador da base de dados do site. Na página **Selecionar Membros do Grupo** do Assistente de Criação de Novo Grupo de Proteção, selecione o serviço SMS Writer na lista de origens de dados e selecione a base de dados do site como membro apropriado. Para obter mais informações sobre a utilização do DPM na criação de cópias de segurança da base de dados do site, veja a [Biblioteca de Documentação do Data Protection Manager](http://go.microsoft.com/fwlink/?LinkId=272772) na TechNet.  

> [!IMPORTANT]  
>  O Configuration Manager não suporta o DPM volta para um cluster do SQL Server que utilize uma instância nomeada, mas suporta DPM cópia de segurança num cluster do SQL Server que utilize a instância predefinida do SQL Server.  

 Após restaurar a base de dados do site, siga os passos do Programa de Configuração para recuperar o site. Selecione o **utilizar uma base de dados do site que tenha sido recuperada manualmente** opção de recuperação para utilizar a base de dados do site que recuperou com o Data Protection Manager.  

## <a name="backup-maintenance-task"></a>Tarefa de manutenção de cópias de segurança
Pode automatizar a cópia de segurança para sites do Configuration Manager, agendando a tarefa de manutenção predefinida do servidor de Site cópia de segurança. Esta tarefa:

-   É executada de acordo com um agendamento
-   Faz uma cópia de segurança da base de dados do site
-   Faz uma cópia de segurança de chaves de registo específicas
-   Faz uma cópia de segurança de pastas e ficheiros específicos
-   Cria cópias de segurança a [CD. Pasta mais recente](/sccm/core/servers/manage/the-cd.latest-folder)   

Planeie a execução da tarefa predefinida de cópia de segurança do site no mínimo a cada 5 dias. Isto acontece porque o Configuration Manager utiliza um *período de retenção do registo de alterações do SQL Server* de 5 dias.  (Consulte [período de retenção do registo de alterações do SQL Server](/sccm/protect/understand/recover-sites#bkmk_SQLretention) do tópico recuperar sites.)

Para simplificar o processo de cópia de segurança, pode criar um **AfterBackup.bat** ficheiros para executar ações pós-cópia de segurança automaticamente após a tarefa de manutenção cópia de segurança é executada com êxito. O ficheiro AfterBackup.bat é normalmente utilizado para arquivar o instantâneo de cópia de segurança numa localização segura. Também pode utilizar o ficheiro AfterBackup.bat para copiar ficheiros para a pasta de cópia de segurança e iniciar outras, suplementares tarefas de cópia de segurança.  

É possível fazer uma cópia de segurança de um site de administração central e site primário, mas não existe qualquer suporte para cópias de segurança de sites secundários ou servidores do sistema de sites.

Quando o serviço de cópia de segurança do Configuration Manager é executado, segue as instruções definidas no ficheiro de controlo de cópia de segurança (**&lt;ConfigMgrInstallationFolder\>\Inboxes\Smsbkup.box\Smsbkup.ctl**). É possível modificar o ficheiro de controlo da cópia de segurança para alterar o comportamento do serviço de cópia de segurança.  

As informações de estado da cópia de segurança do site são escritas no ficheiro **Smsbkup.log** . Este ficheiro é criado na pasta de destino que especificar nas propriedades da tarefa de manutenção Efetuar Cópia de Segurança do Servidor de Site.  

#### <a name="to-enable-the-site-backup-maintenance-task"></a>Para ativar a tarefa de cópia de segurança de manutenção do site  

1.  Na consola do Configuration Manager, abra **administração** > **configuração do Site** > **Sites**.  

2.  Selecione o site no qual pretende ativar a tarefa de cópia de segurança de manutenção do site.  

3.  No **home page** separador o **definições** grupo, escolha **tarefas de manutenção do Site**.  

4.  Escolha **cópia de segurança do servidor do Site**  >  **editar**.  

5.  Escolha **ativar esta tarefa** > **definir caminhos** para especificar o destino de cópia de segurança. Tem as seguintes opções:  

    > [!IMPORTANT]  
    >  Para ajudar a impedir a adulteração dos ficheiros de cópia de segurança, armazenar os ficheiros numa localização segura. O caminho de cópia de segurança mais seguro é numa unidade local, para que possa definir permissões do sistema de ficheiros NTFS na pasta. O Configuration Manager encripta os dados da cópia de segurança que são armazenados no caminho de cópia de segurança.  

    -   **Unidade local no servidor do site para dados do site e base de dados**: Especifica que os ficheiros de cópia de segurança para o site e base de dados do site são armazenados no caminho especificado na unidade de disco local do servidor do site. Terá de criar a pasta local antes da execução da tarefa de cópia de segurança. A conta do Sistema Local no servidor de site tem de ter permissões de **Escrita** do sistema de ficheiros NTFS na pasta local da cópia de segurança do servidor de site. A conta do Sistema Local no computador com o SQL Server tem de ter permissões de **Escrita** de NTFS na pasta da cópia de segurança da base de dados do site.  

    -   **O caminho de rede (nome UNC) para dados do site e base de dados**: Especifica que os ficheiros de cópia de segurança para o site e base de dados do site são armazenados no caminho UNC especificado. Terá de criar a partilha antes da execução da tarefa de cópia de segurança. A conta de computador do servidor de site e a conta de computador do SQL Server, se este estiver instalado noutro computador, têm de ter permissões de **Escrita** de NTFS e de partilha na pasta da rede partilhada.  

    -   **Unidades locais no servidor do site e o SQL Server**: Especifica que os ficheiros de cópia de segurança para o site são armazenados no caminho especificado na unidade local do servidor do site e os ficheiros de cópia de segurança da base de dados do site são armazenados no caminho especificado na unidade local do servidor de base de dados do site. Terá de criar as pastas locais antes da execução da tarefa de cópia de segurança. A conta de computador do servidor de site tem de ter permissões de **Escrita** de NTFS na pasta que criar no servidor de site. A conta de computador do SQL Server tem de ter permissões de **Escrever** de NTFS na pasta que criar no servidor de base de dados do site. Esta opção só estará disponível se a base de dados do site não estiver instalada no servidor de site.  

    > [!NOTE]  
    >   A opção de navegar para o destino da cópia de segurança só estará disponível se especificar o caminho UNC do destino da cópia de segurança.

    > O nome de pasta ou nome da partilha utilizado para o destino da cópia de segurança não suporta a utilização de carateres Unicode.  

6.  Configure uma agenda para a tarefa de cópia de segurança do site. Como procedimento recomendado, considere uma agenda de cópia de segurança fora do horário de trabalho em vigor. Se tiver uma hierarquia, considere uma agenda que seja executada pelo menos duas vezes por semana, de modo a maximizar a retenção de dados em caso de falha do site.  

    Quando executa a consola do Configuration Manager no mesmo servidor do site que está a configurar para cópia de segurança, a tarefa de manutenção cópia de segurança servidor do Site utiliza a hora local para a agenda. Quando a consola do Configuration Manager é executada a partir de um computador remoto relativamente ao site que está a configurar para cópia de segurança, a tarefa de manutenção cópia de segurança servidor do Site utiliza a hora UTC para a agenda.  

7.  Escolha se pretende criar um alerta caso a tarefa de cópia de segurança do site falhe, clique em **OK**e, em seguida, clique em **OK**. Quando selecionada, o Configuration Manager cria um alerta crítico para a falha da cópia de segurança que poderá consultar no **alertas** no nó de **monitorização** área de trabalho.  

 Em seguida, certifique-se de que a tarefa de manutenção do servidor do Site de cópia de segurança está em execução, para se certificar de que as cópias de segurança estão a ser criadas.  

#### <a name="to-verify-that-the-backup-site-server-maintenance-task-is-running"></a>Para verificar que a tarefa de manutenção do servidor do Site de cópia de segurança está em execução  
Certifique-se de que a tarefa de manutenção cópia de segurança do Site está em execução, verificando uma das seguintes opções:  

-   Verifique o carimbo dos ficheiros da pasta de destino de cópia de segurança que criou a tarefa. Certifique-se de que o timestamp foi atualizado com uma hora que corresponde à hora quando a tarefa foi pela última vez agendada para ser executada.  

-   No nó **Estado do Componente** da área de trabalho **Monitorização** , veja as mensagens de estado de SMS_SITE_BACKUP. Quando a cópia de segurança do site for concluída com êxito, será apresentado o ID de mensagem 5035, indicando que a cópia de segurança do site foi concluída sem erros.  

-   Quando a tarefa de manutenção Efetuar Cópia de Segurança do Servidor de Site estiver configurada para criar um alerta em caso de falha da cópia de segurança, pode ver as falhas da cópia de segurança no nó **Alertas** da área de trabalho **Monitorização** .  

-   No &lt; *ConfigMgrInstallationFolder*> \Logs, reveja Smsbkup.log relativamente a avisos e erros. Quando a cópia de segurança do site for concluída com êxito, será apresentado `Backup completed` com um carimbo de data/hora e o ID de mensagem `STATMSG: ID=5035`.  

    > [!TIP]  
    >  Se a tarefa de cópia de segurança de manutenção falhar, poderá reiniciá-la parando e reiniciando o serviço SMS_SITE_BACKUP.  

## <a name="archive-the-backup-snapshot"></a>Arquivar o instantâneo da cópia de segurança  
Na primeira vez que é executada, a tarefa de manutenção Efetuar Cópia de Segurança do Servidor de Site cria um instantâneo de cópia de segurança que poderá utilizar para recuperar o servidor de site em caso de falha. Quando a tarefa de cópia de segurança é novamente executada nos ciclos subsequentes, cria um novo instantâneo de cópia de segurança que substitui o anterior. Em resultado, o site tem apenas um único instantâneo de cópia de segurança, pelo que não existe forma de recuperar um instantâneo de cópia de segurança anterior.  

Como procedimento recomendado, mantenha vários arquivos do instantâneo de cópia de segurança, pelos seguintes motivos:  

-   É comum para suporte de dados de cópia de segurança falhem, sejam ou contêm apenas uma cópia de segurança parcial. Recuperar um site primário autónomo em falha a partir de uma cópia de segurança mais antiga é melhor do que recuperar sem qualquer cópia de segurança. Para um servidor de site numa hierarquia, a cópia de segurança tem de ter um período de retenção de registo de alterações do SQL Server ou a cópia de segurança não é necessária.  

-   Determinados danos no site podem não ser detetados durante vários ciclos de cópia de segurança. Poderá ter de utilizar uma cópia de segurança do instantâneo antes do site ter ficado danificado. Isto aplica-se a um site primário autónomo e aos sites numa hierarquia onde a cópia de segurança está num SQL Server alterar o período de retenção do registo.  

-   O site poderá não ter nenhum instantâneo de cópia de segurança se, por exemplo, a tarefa de manutenção Cópia de Segurança do Servidor do Site falhar. Uma vez que a tarefa de cópia de segurança remove o instantâneo de cópia de segurança anterior antes de iniciar a cópia de segurança dos dados atuais, não haverá um instantâneo de cópia de segurança válido.  

## <a name="using-the-afterbackupbat-file"></a>Utilizar o Ficheiro AfterBackup.bat  
Depois de efetuar a cópia de segurança do site com êxito, a tarefa Efetuar Cópia de Segurança do Servidor de Site tenta executar automaticamente um ficheiro com o nome AfterBackup.bat. Tem de criar manualmente o ficheiro AfterBackup.bat em &lt; *ConfigMgrInstallationFolder*> \Inboxes\Smsbkup. Se um ficheiro AfterBackup.bat existe e está armazenado na pasta correta, este é executado automaticamente depois de concluída a tarefa de cópia de segurança.

O ficheiro AfterBackup.bat permite arquivar o instantâneo da cópia de segurança no final de cada operação de cópia de segurança e executar automaticamente outras tarefas de pós-cópia de segurança que não fazem parte da tarefa de manutenção Cópia de Segurança do Servidor do Site. O ficheiro AfterBackup.bat integra o arquivo e as operações de cópia de segurança, assegurando que cada novo instantâneo de cópia de segurança é arquivado.

Quando o ficheiro AfterBackup.bat não está presente, a tarefa de cópia de segurança ignora-o sem efeito sobre a operação de cópia de segurança. Para verificar se a tarefa de cópia de segurança do site executou o ficheiro AfterBackup.bat com êxito, veja o nó **Estado do Componente** na área de trabalho **Monitorização** e reveja as mensagens de estado para SMS_SITE_BACKUP. Quando a tarefa tiver iniciado com êxito o ficheiro de comandos AfterBackup.bat, é apresentada a mensagem ID 5040.  

> [!TIP]  
>  Para criar o ficheiro AfterBackup.bat para arquivar os ficheiros de cópia de segurança de servidor de site, tem de utilizar uma ferramenta do comando de cópia, como [Robocopy](http://go.microsoft.com/fwlink/p/?LinkId=228408), no ficheiro batch. Por exemplo, pode criar o ficheiro AfterBackup.bat e na primeira linha, pode adicionar algo semelhante ao seguinte:`Robocopy E:\ConfigMgr_Backup \\ServerName\ShareName\ConfigMgr_Backup /MIR`  

 Embora a utilização prevista de AfterBackup.bat seja arquivar o instantâneo da cópia de segurança, é possível criar um ficheiro AfterBackup.bat para executar tarefas adicionais no final de cada operação de cópia de segurança.  

##  <a name="supplemental-backup-tasks"></a>Tarefas suplementares de cópia de segurança  
A tarefa de manutenção Cópia de Segurança do Servidor do Site fornece um instantâneo de cópia de segurança para os ficheiros do servidor de site e a base de dados do site, mas existem outros itens dos quais não foi efetuada cópia de segurança que deve ter em conta ao criar a sua estratégia de cópia de segurança. Utilize as secções seguintes para ajudar a concluir a estratégia de cópia de segurança do Configuration Manager.  

### <a name="back-up-custom-reporting-services-reports"></a>Cópia de segurança dos relatórios personalizados do Reporting Services  
Depois de modificar relatórios personalizados do Reporting Services predefinidos ou criados, a criação de uma cópia de segurança dos ficheiros da base de dados do servidor de relatórios é uma parte importante da sua estratégia de cópia de segurança. A cópia de segurança do servidor de relatórios deve incluir uma cópia de segurança dos ficheiros de origem para relatórios e modelos, chaves de encriptação, assemblagens ou extensões personalizadas, ficheiros de configuração, vistas personalizadas do SQL Server nos relatórios personalizados, procedimentos armazenados personalizados, etc.  

> [!IMPORTANT]  
>  Quando as atualizações do Configuration Manager para uma versão mais recente, os relatórios predefinidos podem ser substituídos por novos relatórios. Se modificar um relatório predefinido, fazer uma cópia de segurança do relatório e, em seguida, restaure-o no Reporting Services.  

 Para obter mais informações sobre a criação de cópias de segurança dos seus relatórios personalizados no Reporting Services, veja [Backup and Restore Operations for a Reporting Services Installation (Operações de Cópia de Segurança e Restauro de uma Instalação do Reporting Services)](https://technet.microsoft.com/library/ms155814\(v=sql.120\).aspx) na Documentação Online do SQL Server 2014.  

### <a name="back-up-content-files"></a>Cópia de segurança de ficheiros de conteúdo  
A biblioteca de conteúdos no Configuration Manager é a localização onde estão armazenados os ficheiros de conteúdo todas as atualizações de software, aplicações, implementação do sistema operativo e assim sucessivamente. A biblioteca de conteúdos está localizada no servidor do site e em cada ponto de distribuição. A tarefa de manutenção Cópia de Segurança do Servidor do Site não inclui uma cópia de segurança para a biblioteca de conteúdos ou os ficheiros de origem do pacote. Quando um servidor de site falha, as informações sobre os ficheiros da biblioteca de conteúdos são restauradas para a base de dados do site, mas é necessário restaurar os ficheiros da biblioteca de conteúdos e de origem do pacote no servidor do site.  

-   **Biblioteca de conteúdos**: A biblioteca de conteúdos deve ser restaurada antes de pode redistribuir o conteúdo para pontos de distribuição. Quando a redistribuição do conteúdo, o Configuration Manager copia os ficheiros da biblioteca de conteúdos no servidor do site para os pontos de distribuição. A biblioteca de conteúdos para o servidor do site está na pasta SCCMContentLib, que está normalmente localizada na unidade com mais disco espaço livre no momento quando o site foi instalado.  

-   **Ficheiros de origem do pacote**: Os ficheiros de origem do pacote devem ser restaurados antes de poder atualizar conteúdo em pontos de distribuição. Quando iniciar uma atualização de conteúdo, Configuration Manager copia ficheiros novos ou modificados da origem do pacote para a biblioteca de conteúdos, que, por sua vez copia os ficheiros de distribuição associados, pontos. Pode executar a seguinte consulta no SQL Server para encontrar a localização de origem do pacote para todos os pacotes e aplicações: `SELECT * FROM v_Package`. Pode identificar o site de origem do pacote atravésdos primeiros três carateres do ID de pacote. Por exemplo, se o ID de pacote for CEN00001, o código de site do site de origem é CEN. Quando restaurar os ficheiros de origem do pacote, estes devem ser restaurados para a mesma localização em que se encontravam antes da falha.  

 Verifique se está a incluir as localizações da biblioteca de conteúdos e da origem do pacote na cópia de segurança do sistema de ficheiros para o servidor de site.  

### <a name="back-up-custom-software-updates"></a>Cópia de segurança de atualizações de software personalizadas  
 System Center Updates Publisher 2011 é uma ferramenta autónoma que lhe permite publicar atualizações de software personalizadas para o Windows Server Update Services (WSUS), sincronizar as atualizações de software do Configuration Manager, avaliar a compatibilidade de atualizações de software e implementar as atualizações de software personalizadas para os clientes. Publicador de atualizações utiliza uma base de dados local para o repositório de atualização de software. Quando utilizar o Updates Publisher para gerir atualizações de software personalizadas, determine se deve incluir a base de dados do Updates Publisher no seu plano de cópia de segurança. Para obter mais informações sobre o Updates Publisher, veja [System Center Updates Publisher 2011](http://go.microsoft.com/fwlink/p/?LinkId=228726) na Biblioteca TechCenter do System Center.  

 Utilize o procedimento seguinte para criar cópias de segurança da base de dados do Updates Publisher.  

#### <a name="to-back-up-the-updates-publisher-2011-database"></a>Para criar uma cópia de segurança da base de dados do Updates Publisher 2011  

1.  No computador que executa o Updates Publisher, procure o ficheiro de base de dados do Updates Publisher (Scupdb.sdf) em %*USERPROFILE*%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\\. Não há um ficheiro de base de dados diferente para cada utilizador que executa o Updates Publisher.  

2.  Copie o ficheiro de base de dados para o destino de cópia de segurança. Por exemplo, se o destino do backup for E:\ConfigMgr_Backup, você poderá copiar o arquivo de banco de dados do Updates Publisher em e:\configmgr_backup\scup2011.  

    > [!TIP]  
    >  Quando existe mais do que um ficheiro de base de dados num computador, considere armazenar o ficheiro numa subpasta que indica o perfil de utilizador associado ao ficheiro de base de dados. Por exemplo, pode ter um ficheiro de base de dados em E:\ConfigMgr_Backup\SCUP2011\User1 e outro ficheiro de base de dados em E:\ConfigMgr_Backup\SCUP2011\User2.  

## <a name="user-state-migration-data"></a>Dados de migração de estado de utilizador  
Pode utilizar sequências de tarefas do Configuration Manager para capturar e restaurar dados de estado do utilizador em cenários de implementação do sistema operativo em que pretenda manter o estado de utilizador do sistema operativo atual. As pastas que armazenam dados de estado do utilizador são listadas nas propriedades para o ponto de migração de estado. Não é efetuada cópia de segurança destes dados de migração de estado de utilizador como parte da tarefa de manutenção Cópia de Segurança do Servidor do Site. Como parte do seu plano de cópia de segurança, tem de copiar manualmente as pastas que especificar para armazenar os dados de migração de estado do utilizador.   

### <a name="to-determine-the-folders-used-to-store-user-state-migration-data"></a>Para determinar as pastas utilizadas para armazenar dados de migração de estado de utilizador  

1.  Na consola do Configuration Manager, clique em **Administração**.  

2.  No **administração** área de trabalho, expanda **configuração do Site**e escolha **servidores e funções de sistema de sites**.  

3.  Selecione o sistema de sites que aloja a função de migração de estado e escolha **ponto de migração de estado** no **funções do sistema de sites**.  


4.  No separador **Função do Site** , no grupo **Propriedades** , clique em **Propriedades**.  
5.  As pastas que armazenam os dados de migração de estado do utilizador são listadas na secção **Detalhes da pasta** , no separador **Geral** .  



## <a name="about-the-sms-writer-service"></a>Sobre o serviço SMS Writer  
O SMS Writer é um serviço que interage com o Serviço de Cópia Sombra de Volumes (VSS) durante o processo de cópia de segurança. Conclua o SMS Writer serviço tem de executar para cópia de segurança do site do Configuration Manager até com êxito.  

### <a name="purpose"></a>Objetivo  
O SMS Writer é registado junto do serviço VSS, ligando-se às respetivas interfaces e eventos. Quando o VSS difunde eventos ou envia notificações específicas para o SMS Writer, o SMS Writer responde à notificação e executa a ação adequada. O SMS Writer lê o ficheiro de controlo de cópia de segurança (smsbkup.ctl), localizado no &lt; *ConfigMgr Installation Path*> \inboxes\smsbkup.box e determina os ficheiros e dados que está a cópia de segurança. O SMS Writer cria metadados, que consistem em diversos componentes, com base nestas informações, bem como em dados específicos da chave e subchaves de registo do SMS. Quando solicitado, envia os metadados para o VSS. O VSS, em seguida, envia os metadados para a aplicação requerente Gestor de cópia de segurança do Configuration Manager. O Backup Manager seleciona os dados de que será efetuada cópia de segurança e envia-os para o SMS Writer através do VSS. O SMS Writer executa os passos adequados para preparar a cópia de segurança. Mais tarde, quando o VSS estiver pronto para tirar o instantâneo, enviará um evento e o SMS Writer interrompe todos os serviços do Configuration Manager e assegura que as atividades do Configuration Manager são interrompidas durante a criação do instantâneo. Após a conclusão do instantâneo, o SMS Writer reiniciará os serviços e atividades.  

O serviço SMS Writer é instalado automaticamente. Tem de estar em execução quando a aplicação VSS solicita uma cópia de segurança ou restauro.  

### <a name="writer-id"></a>ID do escritor  
O ID de escritor para o SMS Writer é: 03ba67dd-dc6d-4729-a038-251f7018463b.  

### <a name="permissions"></a>Permissões  
O serviço SMS Writer tem de ser executado sob a conta do Sistema Local.  

### <a name="volume-shadow-copy-service"></a>Serviço de Cópia Sombra de Volumes  
O VSS é um conjunto de APIs COM que implementa uma estrutura para permitir a execução de cópias de segurança de volume enquanto as aplicações do sistema continuam a escrever nos volumes. O VSS fornece uma interface consistente que permite coordenar as aplicações de utilizador que atualizam dados no disco (o serviço SMS Writer) com as que efetuam cópias de segurança das aplicações (o serviço Backup Manager). Para obter mais informações, consulte o [serviço de cópia sombra de volumes](http://go.microsoft.com/fwlink/p/?LinkId=241968) tópico no Windows Server TechCenter.  

## <a name="next-steps"></a>Passos seguintes
Depois de criar uma cópia de segurança, restaure [recuperação de sites](/sccm/protect/understand/recover-sites) com essa cópia de segurança. Isto pode ajudar a tornar-se familiarizado com o processo de recuperação antes que seja necessário confiar na mesma e pode ajudar a confirmar a cópia de segurança foi efetuada com êxito para o objetivo pretendido.  
