---
title: Fazer backup de sites | Microsoft Docs
description: Saiba como fazer backup de seus sites antes do evento de falha ou perda de dados no System Center Configuration Manager.
ms.custom: na
ms.date: 6/5/2017
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
ms.sourcegitcommit: f7cd9c71287d62c9f5d36e2f032bc2a6065572ae
ms.openlocfilehash: 7deb00d4b67eabf3238907b337a9d0367c3d99cc
ms.contentlocale: pt-pt
ms.lasthandoff: 06/06/2017

---

# <a name="back-up-a-configuration-manager-site"></a>Efetuar uma Cópia de Segurança de um Site do Gestor de Configuração

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

Prepare as abordagens de backup e recuperação para evitar a perda de dados. Para sites do Configuration Manager, uma abordagem de backup e recuperação pode ajudar a recuperar os sites e hierarquias mais rapidamente e com o mínimo de perda de dados.  

As seções neste tópico podem ajudá-lo a fazer backup de seus sites. Para recuperar um site, consulte [recuperação para o Configuration Manager](/sccm/protect/understand/recover-sites).  

## <a name="considerations-before-creating-a-backup"></a>Considerações antes de criar um backup  
-   **Se você usar um grupo de disponibilidade do SQL Server Always On para hospedar o banco de dados do site:** Modifique seus planos de backup e recuperação, conforme descrito em [preparar para usar SQL Server Always On](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#changes-for-site-backup).

-   Configuration Manager pode recuperar o banco de dados do site da tarefa de manutenção de backup do Configuration Manager ou de um backup de banco de dados do site que você cria com outro processo.   

    Por exemplo, você pode restaurar o banco de dados do site de um backup que é criado como parte de um plano de manutenção do Microsoft SQL Server. Você também pode usar um backup que é criado pelo usando o Data Protection Manager para fazer backup de seu banco de dados do site (DPM).

####  <a name="using-data-protection-manager-to-back-up-your-site-database"></a>Utilizar o Data Protection Manager para efetuar cópias de segurança da base de dados do site
Pode utilizar o System Center 2012 Data Protection Manager (DPM) para criar uma cópia de segurança da base de dados do site.

Terá de criar um novo grupo de proteção no DPM para o computador da base de dados do site. Na página **Selecionar Membros do Grupo** do Assistente de Criação de Novo Grupo de Proteção, selecione o serviço SMS Writer na lista de origens de dados e selecione a base de dados do site como membro apropriado. Para obter mais informações sobre a utilização do DPM na criação de cópias de segurança da base de dados do site, veja a [Biblioteca de Documentação do Data Protection Manager](http://go.microsoft.com/fwlink/?LinkId=272772) na TechNet.  

> [!IMPORTANT]  
>  Configuration Manager não oferece suporte ao DPM volta para um cluster do SQL Server que usa uma instância nomeada, mas oferece suporte ao DPM fazer backup em um cluster do SQL Server que usa a instância padrão do SQL Server.  

 Após restaurar a base de dados do site, siga os passos do Programa de Configuração para recuperar o site. Selecione o **usar um banco de dados do site recuperado manualmente** opção de recuperação para usar o banco de dados do site recuperado com o Data Protection Manager.  

## <a name="backup-maintenance-task"></a>Tarefa de manutenção de cópias de segurança
Você pode automatizar o backup de sites do Configuration Manager agendando a tarefa de manutenção do servidor do Site de Backup predefinida. Essa tarefa:

-   É executada de acordo com um agendamento
-   Faz uma cópia de segurança da base de dados do site
-   Faz uma cópia de segurança de chaves de registo específicas
-   Faz uma cópia de segurança de pastas e ficheiros específicos
-   Faz backup de [CD. Pasta mais recente](/sccm/core/servers/manage/the-cd.latest-folder)   

Planeie a execução da tarefa predefinida de cópia de segurança do site no mínimo a cada 5 dias. Isso ocorre porque o Configuration Manager usa um *período de retenção do controle de alterações do SQL Server* de 5 dias.  (Consulte [período de retenção do controle de alterações do SQL Server](/sccm/protect/understand/recover-sites#bkmk_SQLretention) no tópico recuperar sites.)

Para simplificar o processo de backup, você pode criar um **AfterBackup.bat** arquivo para executar ações pós-backup automaticamente depois que a tarefa de manutenção de backup é executado com êxito. O arquivo AfterBackup.bat é usado geralmente para arquivar o instantâneo de backup em um local seguro. Você também pode usar o arquivo AfterBackup.bat para copiar arquivos na pasta de backup e iniciar outras tarefas backup complementares.  

É possível fazer uma cópia de segurança de um site de administração central e site primário, mas não existe qualquer suporte para cópias de segurança de sites secundários ou servidores do sistema de sites.

Quando o serviço de backup do Configuration Manager é executado, ele segue as instruções definidas no arquivo de controle de backup (**&lt;ConfigMgrInstallationFolder\>\Inboxes\Smsbkup.box\Smsbkup.CTL**). É possível modificar o ficheiro de controlo da cópia de segurança para alterar o comportamento do serviço de cópia de segurança.  

As informações de estado da cópia de segurança do site são escritas no ficheiro **Smsbkup.log** . Este ficheiro é criado na pasta de destino que especificar nas propriedades da tarefa de manutenção Efetuar Cópia de Segurança do Servidor de Site.  

#### <a name="to-enable-the-site-backup-maintenance-task"></a>Para ativar a tarefa de cópia de segurança de manutenção do site  

1.  No console do Configuration Manager, abra **administração** > **configuração do Site** > **Sites**.  

2.  Selecione o site no qual pretende ativar a tarefa de cópia de segurança de manutenção do site.  

3.  No **início** guia o **configurações** de grupo, escolha **tarefas de manutenção do Site**.  

4.  Escolha **fazer Backup do servidor de Site**  >  **editar**.  

5.  Escolha **habilitar esta tarefa** > **definir caminhos** para especificar o destino de backup. Tem as seguintes opções:  

    > [!IMPORTANT]  
    >  Para ajudar a impedir a adulteração dos ficheiros de cópia de segurança, armazenar os ficheiros numa localização segura. O caminho de backup mais seguro é uma unidade local, você pode definir permissões de sistema de arquivos NTFS na pasta. Gerenciador de configuração não criptografa os dados de backup são armazenados no caminho de backup.  

    -   **Unidade local no servidor do site para o banco de dados e dados do site**: Especifica que os arquivos de backup para o site e o banco de dados do site são armazenados no caminho especificado na unidade de disco local do servidor do site. Terá de criar a pasta local antes da execução da tarefa de cópia de segurança. A conta do Sistema Local no servidor de site tem de ter permissões de **Escrita** do sistema de ficheiros NTFS na pasta local da cópia de segurança do servidor de site. A conta do Sistema Local no computador com o SQL Server tem de ter permissões de **Escrita** de NTFS na pasta da cópia de segurança da base de dados do site.  

    -   **Caminho de rede (nome UNC) para o banco de dados e dados do site**: Especifica que os arquivos de backup para o site e o banco de dados do site são armazenados no caminho UNC especificado. Terá de criar a partilha antes da execução da tarefa de cópia de segurança. A conta de computador do servidor de site e a conta de computador do SQL Server, se este estiver instalado noutro computador, têm de ter permissões de **Escrita** de NTFS e de partilha na pasta da rede partilhada.  

    -   **Unidades locais no servidor do site e do SQL Server**: Especifica que os arquivos de backup para o site são armazenados no caminho especificado na unidade local do servidor do site, e os arquivos de backup do banco de dados do site são armazenados no caminho especificado na unidade local do servidor de banco de dados do site. Terá de criar as pastas locais antes da execução da tarefa de cópia de segurança. A conta de computador do servidor de site tem de ter permissões de **Escrita** de NTFS na pasta que criar no servidor de site. A conta de computador do SQL Server tem de ter permissões de **Escrever** de NTFS na pasta que criar no servidor de base de dados do site. Esta opção só estará disponível se a base de dados do site não estiver instalada no servidor de site.  

    > [!NOTE]  
    >   A opção de navegar para o destino da cópia de segurança só estará disponível se especificar o caminho UNC do destino da cópia de segurança.

    > O nome de pasta ou nome da partilha utilizado para o destino da cópia de segurança não suporta a utilização de carateres Unicode.  

6.  Configure um agendamento para a tarefa de backup do site. Como procedimento recomendado, considere uma agenda de cópia de segurança fora do horário de trabalho em vigor. Se tiver uma hierarquia, considere uma agenda que seja executada pelo menos duas vezes por semana, de modo a maximizar a retenção de dados em caso de falha do site.  

    Quando você executa o console do Configuration Manager no mesmo servidor do site que você está configurando para backup, a tarefa de manutenção do servidor do Site de Backup usa a hora local para o agendamento. Quando o console do Configuration Manager é executado em um computador remoto do site que você está configurando para backup, a tarefa de manutenção do servidor do Site de Backup usa o horário UTC para a agenda.  

7.  Escolha se deseja criar um alerta se a tarefa de backup do site falhe, clique em **Okey**e, em seguida, clique em **Okey**. Quando selecionada, o Configuration Manager cria um alerta crítico para a falha do backup que você pode examinar no **alertas** nó o **monitoramento** espaço de trabalho.  

 Em seguida, verifique se a tarefa de manutenção do servidor do Site de Backup está em execução, para garantir que os backups estão sendo criados.  

#### <a name="to-verify-that-the-backup-site-server-maintenance-task-is-running"></a>Para verificar se a tarefa de manutenção do servidor do Site de Backup está em execução  
Verifique se a tarefa de manutenção de Backup do Site está em execução, examinando o seguinte:  

-   Verifique se o carimbo de hora dos arquivos na pasta de destino de backup que criou a tarefa. Verifique se que o carimbo de hora foi atualizado com uma hora que coincide com a hora em que a tarefa foi agendada para ser executada.  

-   No nó **Estado do Componente** da área de trabalho **Monitorização** , veja as mensagens de estado de SMS_SITE_BACKUP. Quando a cópia de segurança do site for concluída com êxito, será apresentado o ID de mensagem 5035, indicando que a cópia de segurança do site foi concluída sem erros.  

-   Quando a tarefa de manutenção Efetuar Cópia de Segurança do Servidor de Site estiver configurada para criar um alerta em caso de falha da cópia de segurança, pode ver as falhas da cópia de segurança no nó **Alertas** da área de trabalho **Monitorização** .  

-   Em &lt; *ConfigMgrInstallationFolder*> \Logs, examine Smsbkup.log para erros e avisos. Quando a cópia de segurança do site for concluída com êxito, será apresentado `Backup completed` com um carimbo de data/hora e o ID de mensagem `STATMSG: ID=5035`.  

    > [!TIP]  
    >  Se a tarefa de cópia de segurança de manutenção falhar, poderá reiniciá-la parando e reiniciando o serviço SMS_SITE_BACKUP.  

## <a name="archive-the-backup-snapshot"></a>Arquivar o instantâneo de backup  
Na primeira vez que é executada, a tarefa de manutenção Efetuar Cópia de Segurança do Servidor de Site cria um instantâneo de cópia de segurança que poderá utilizar para recuperar o servidor de site em caso de falha. Quando a tarefa de cópia de segurança é novamente executada nos ciclos subsequentes, cria um novo instantâneo de cópia de segurança que substitui o anterior. Em resultado, o site tem apenas um único instantâneo de cópia de segurança, pelo que não existe forma de recuperar um instantâneo de cópia de segurança anterior.  

Como procedimento recomendado, mantenha vários arquivos do instantâneo de cópia de segurança, pelos seguintes motivos:  

-   É comum para a mídia de backup falhe, se extravie ou conter apenas um backup parcial. Recuperar um site primário autónomo em falha a partir de uma cópia de segurança mais antiga é melhor do que recuperar sem qualquer cópia de segurança. Para um servidor de site numa hierarquia, a cópia de segurança tem de ter um período de retenção de registo de alterações do SQL Server ou a cópia de segurança não é necessária.  

-   Determinados danos no site podem não ser detetados durante vários ciclos de cópia de segurança. Você talvez precise usar um instantâneo de backup anterior do site foi corrompido. Isso se aplica a um site primário autônomo e para sites em uma hierarquia onde o backup está no SQL Server, altere o período de retenção do controle.  

-   O site poderá não ter nenhum instantâneo de cópia de segurança se, por exemplo, a tarefa de manutenção Cópia de Segurança do Servidor do Site falhar. Uma vez que a tarefa de cópia de segurança remove o instantâneo de cópia de segurança anterior antes de iniciar a cópia de segurança dos dados atuais, não haverá um instantâneo de cópia de segurança válido.  

## <a name="using-the-afterbackupbat-file"></a>Utilizar o Ficheiro AfterBackup.bat  
Depois de efetuar a cópia de segurança do site com êxito, a tarefa Efetuar Cópia de Segurança do Servidor de Site tenta executar automaticamente um ficheiro com o nome AfterBackup.bat. Você deve criar manualmente o arquivo AfterBackup.bat em &lt; *ConfigMgrInstallationFolder*> \Inboxes\Smsbkup. Se um arquivo AfterBackup.bat existe e é armazenado na pasta correta, ele será executado automaticamente depois da conclusão da tarefa de backup.

O ficheiro AfterBackup.bat permite arquivar o instantâneo da cópia de segurança no final de cada operação de cópia de segurança e executar automaticamente outras tarefas de pós-cópia de segurança que não fazem parte da tarefa de manutenção Cópia de Segurança do Servidor do Site. O ficheiro AfterBackup.bat integra o arquivo e as operações de cópia de segurança, assegurando que cada novo instantâneo de cópia de segurança é arquivado.

Quando o ficheiro AfterBackup.bat não está presente, a tarefa de cópia de segurança ignora-o sem efeito sobre a operação de cópia de segurança. Para verificar se a tarefa de cópia de segurança do site executou o ficheiro AfterBackup.bat com êxito, veja o nó **Estado do Componente** na área de trabalho **Monitorização** e reveja as mensagens de estado para SMS_SITE_BACKUP. Quando a tarefa tiver iniciado com êxito o ficheiro de comandos AfterBackup.bat, é apresentada a mensagem ID 5040.  

> [!TIP]  
>  Para criar o arquivo AfterBackup.bat para arquivar os arquivos de backup de servidor do site, você deve usar uma ferramenta de comando de cópia, como [Robocopy](http://go.microsoft.com/fwlink/p/?LinkId=228408), arquivo em lotes. Por exemplo, você pode criar o arquivo AfterBackup.bat, e na primeira linha, adicionar algo como:`Robocopy E:\ConfigMgr_Backup \\ServerName\ShareName\ConfigMgr_Backup /MIR`  

 Embora a utilização prevista de AfterBackup.bat seja arquivar o instantâneo da cópia de segurança, é possível criar um ficheiro AfterBackup.bat para executar tarefas adicionais no final de cada operação de cópia de segurança.  

##  <a name="supplemental-backup-tasks"></a>Tarefas suplementares de cópia de segurança  
A tarefa de manutenção Cópia de Segurança do Servidor do Site fornece um instantâneo de cópia de segurança para os ficheiros do servidor de site e a base de dados do site, mas existem outros itens dos quais não foi efetuada cópia de segurança que deve ter em conta ao criar a sua estratégia de cópia de segurança. Use as seções a seguir para ajudá-lo a concluir sua estratégia de backup do Configuration Manager.  

### <a name="back-up-custom-reporting-services-reports"></a>Cópia de segurança dos relatórios personalizados do Reporting Services  
Depois de modificar relatórios personalizados do Reporting Services predefinidos ou criados, a criação de uma cópia de segurança dos ficheiros da base de dados do servidor de relatórios é uma parte importante da sua estratégia de cópia de segurança. A cópia de segurança do servidor de relatórios deve incluir uma cópia de segurança dos ficheiros de origem para relatórios e modelos, chaves de encriptação, assemblagens ou extensões personalizadas, ficheiros de configuração, vistas personalizadas do SQL Server nos relatórios personalizados, procedimentos armazenados personalizados, etc.  

> [!IMPORTANT]  
>  Quando atualizações do Configuration Manager para uma versão mais recente, os relatórios predefinidos podem ser substituídos por novos relatórios. Se você modificar um relatório predefinido, faça backup do relatório e, em seguida, restaurá-lo no Reporting Services.  

 Para obter mais informações sobre a criação de cópias de segurança dos seus relatórios personalizados no Reporting Services, veja [Backup and Restore Operations for a Reporting Services Installation (Operações de Cópia de Segurança e Restauro de uma Instalação do Reporting Services)](https://technet.microsoft.com/library/ms155814\(v=sql.120\).aspx) na Documentação Online do SQL Server 2014.  

### <a name="back-up-content-files"></a>Fazer backup de arquivos de conteúdo  
A biblioteca de conteúdo no Configuration Manager é o local onde todos os arquivos de conteúdo são armazenados para atualizações de software, aplicativos, implantação de sistema operacional e assim por diante. A biblioteca de conteúdo está localizada no servidor do site e em cada ponto de distribuição. A tarefa de manutenção Cópia de Segurança do Servidor do Site não inclui uma cópia de segurança para a biblioteca de conteúdos ou os ficheiros de origem do pacote. Quando um servidor de site falha, as informações sobre os ficheiros da biblioteca de conteúdos são restauradas para a base de dados do site, mas é necessário restaurar os ficheiros da biblioteca de conteúdos e de origem do pacote no servidor do site.  

-   **Biblioteca de conteúdo**: A biblioteca de conteúdo deve ser restaurada antes de redistribuir o conteúdo para pontos de distribuição. Quando você começa a redistribuição do conteúdo, o Configuration Manager copia os arquivos da biblioteca de conteúdo no servidor do site para os pontos de distribuição. A biblioteca de conteúdo para o servidor do site está na pasta SCCMContentLib, que normalmente fica localizada na unidade com o maior espaço de disco no momento em que o site foi instalado.  

-   **Arquivos de origem do pacote**: Os arquivos de origem do pacote devem ser restaurados antes de atualizar o conteúdo nos pontos de distribuição. Quando você inicia uma atualização de conteúdo, o Configuration Manager copia arquivos novos ou modificados da origem do pacote à biblioteca de conteúdo, que por sua vez copia os arquivos de distribuição associados aponta. Pode executar a seguinte consulta no SQL Server para encontrar a localização de origem do pacote para todos os pacotes e aplicações: `SELECT * FROM v_Package`. Pode identificar o site de origem do pacote atravésdos primeiros três carateres do ID de pacote. Por exemplo, se o ID de pacote for CEN00001, o código de site do site de origem é CEN. Quando você restaurar os arquivos de origem do pacote, eles devem ser restaurados no mesmo local em que estavam antes da falha.  

 Verifique se está a incluir as localizações da biblioteca de conteúdos e da origem do pacote na cópia de segurança do sistema de ficheiros para o servidor de site.  

### <a name="back-up-custom-software-updates"></a>Cópia de segurança de atualizações de software personalizadas  
 System Center Updates Publisher 2011 é uma ferramenta autônoma que permite que você publicar atualizações de software personalizadas para o Windows Server Update Services (WSUS), sincronizar as atualizações de software do Configuration Manager, avaliar a conformidade de atualizações de software e implantar as atualizações de software personalizado para clientes. O Updates Publisher usa um banco de dados local para seu repositório de atualização de software. Quando você usar o Updates Publisher para gerenciar atualizações de software personalizadas, determine se você deve incluir o banco de dados do Updates Publisher no seu plano de backup. Para obter mais informações sobre o Updates Publisher, veja [System Center Updates Publisher 2011](http://go.microsoft.com/fwlink/p/?LinkId=228726) na Biblioteca TechCenter do System Center.  

 Use o procedimento a seguir para fazer backup do banco de dados do Updates Publisher.  

#### <a name="to-back-up-the-updates-publisher-2011-database"></a>Para criar uma cópia de segurança da base de dados do Updates Publisher 2011  

1.  No computador que executa o Updates Publisher, navegue até o arquivo de banco de dados do Updates Publisher (Scupdb.sdf) em %*USERPROFILE*%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\\. Há um arquivo de banco de dados diferente para cada usuário que executa o Updates Publisher.  

2.  Copie o ficheiro de base de dados para o destino de cópia de segurança. Por exemplo, se o destino do backup for E:\ConfigMgr_Backup, você poderá copiar o arquivo de banco de dados do Updates Publisher em e:\configmgr_backup\scup2011.  

    > [!TIP]  
    >  Quando há mais de um arquivo de banco de dados em um computador, considere armazenar o arquivo em uma subpasta que indique o perfil de usuário associado ao arquivo de banco de dados. Por exemplo, pode ter um ficheiro de base de dados em E:\ConfigMgr_Backup\SCUP2011\User1 e outro ficheiro de base de dados em E:\ConfigMgr_Backup\SCUP2011\User2.  

## <a name="user-state-migration-data"></a>Dados de migração de estado de utilizador  
Você pode usar sequências de tarefas do Configuration Manager para capturar e restaurar os dados de estado do usuário em cenários de implantação do sistema operacional onde você deseja manter o estado do usuário do sistema operacional atual. As pastas que armazenam dados de estado do utilizador são listadas nas propriedades para o ponto de migração de estado. Não é efetuada cópia de segurança destes dados de migração de estado de utilizador como parte da tarefa de manutenção Cópia de Segurança do Servidor do Site. Como parte do seu plano de cópia de segurança, tem de copiar manualmente as pastas que especificar para armazenar os dados de migração de estado do utilizador.   

### <a name="to-determine-the-folders-used-to-store-user-state-migration-data"></a>Para determinar as pastas utilizadas para armazenar dados de migração de estado de utilizador  

1.  Na consola do Configuration Manager, clique em **Administração**.  

2.  No **administração** espaço de trabalho, expanda **configuração do Site**e escolha **servidores e funções de sistema de Site**.  

3.  Selecione o sistema de site que hospeda a função de migração de estado e escolha **ponto de migração de estado** na **funções do sistema de Site**.  


4.  No separador **Função do Site** , no grupo **Propriedades** , clique em **Propriedades**.  
5.  As pastas que armazenam os dados de migração de estado do utilizador são listadas na secção **Detalhes da pasta** , no separador **Geral** .  



## <a name="about-the-sms-writer-service"></a>Sobre o serviço SMS Writer  
O SMS Writer é um serviço que interage com o Serviço de Cópia Sombra de Volumes (VSS) durante o processo de cópia de segurança. Conclua o SMS Writer deve estar sendo executado para a parte de trás do site do Configuration Manager até com êxito.  

### <a name="purpose"></a>Objetivo  
O SMS Writer é registado junto do serviço VSS, ligando-se às respetivas interfaces e eventos. Quando o VSS difunde eventos ou envia notificações específicas para o SMS Writer, o SMS Writer responde à notificação e executa a ação adequada. O SMS Writer lê o arquivo de controle de backup (smsbkup.ctl), localizado no &lt; *ConfigMgr Installation Path*> \inboxes\smsbkup.box e determina os arquivos e dados de backup. O SMS Writer cria metadados, que consistem em diversos componentes, com base nestas informações, bem como em dados específicos da chave e subchaves de registo do SMS. Quando solicitado, envia os metadados para o VSS. Em seguida, o VSS envia os metadados ao aplicativo solicitante; Gerenciador de Backup do Configuration Manager. O Backup Manager seleciona os dados de que será efetuada cópia de segurança e envia-os para o SMS Writer através do VSS. O SMS Writer executa os passos adequados para preparar a cópia de segurança. Posteriormente, quando o VSS está pronto para capturar o instantâneo, ele envia um evento, o SMS Writer interrompe todos os serviços do Configuration Manager e garante que as atividades do Gerenciador de configuração sejam congeladas enquanto o instantâneo é criado. Após a conclusão do instantâneo, o SMS Writer reiniciará os serviços e atividades.  

O serviço SMS Writer é instalado automaticamente. Tem de estar em execução quando a aplicação VSS solicita uma cópia de segurança ou restauro.  

### <a name="writer-id"></a>ID do escritor  
A ID do gravador do SMS Writer é: 03ba67dd-dc6d-4729-a038-251f7018463b.  

### <a name="permissions"></a>Permissões  
O serviço SMS Writer tem de ser executado sob a conta do Sistema Local.  

### <a name="volume-shadow-copy-service"></a>Serviço de Cópia Sombra de Volumes  
O VSS é um conjunto de APIs COM que implementa uma estrutura para permitir a execução de cópias de segurança de volume enquanto as aplicações do sistema continuam a escrever nos volumes. O VSS fornece uma interface consistente que permite coordenar as aplicações de utilizador que atualizam dados no disco (o serviço SMS Writer) com as que efetuam cópias de segurança das aplicações (o serviço Backup Manager). Para obter mais informações, consulte o [serviço de cópias de sombra de Volume](http://go.microsoft.com/fwlink/p/?LinkId=241968) tópico no Windows Server TechCenter.  

## <a name="next-steps"></a>Passos seguintes
Depois de criar um backup, praticar [recuperação de site](/sccm/protect/understand/recover-sites) com que o backup. Isso pode ajudá-lo a se familiarizar com o processo de recuperação antes de precisar confiar nele e pode ajudar a confirmar que o backup foi bem-sucedida para sua finalidade pretendida.  

