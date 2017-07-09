---
title: "Recuperação de site | Microsoft Docs"
description: Saiba como recuperar seus sites no System Center Configuration Manager.
ms.custom: na
ms.date: 6/5/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 19539f4d-1667-4b4c-99a1-9995f12cf5f7
caps.latest.revision: 
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: f7cd9c71287d62c9f5d36e2f032bc2a6065572ae
ms.openlocfilehash: 49eea15ea2888f8f93c33eb771c09147ba21529e
ms.contentlocale: pt-pt
ms.lasthandoff: 06/06/2017

---

#  <a name="recover-a-configuration-manager-site"></a>Recuperar um site do Gestor de Configuração

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

Execute um Gerenciador de configuração de recuperação de site depois que um site do Configuration Manager falha ou ocorre perda de dados no banco de dados do site. Reparar e ressincronizar dados são as tarefas principais de uma recuperação de site e são necessárias para evitar a interrupção das operações.

As seções neste tópico podem ajudá-lo a recuperar um site do Configuration Manager. Para criar um backup, consulte [Backup para o Configuration Manager](/sccm/protect/understand/backup-and-recovery).

## <a name="considerations-before-recovering-a-site"></a>Considerações antes de recuperar um site
**Você deve usar a mesma versão e edição do SQL Server:** Por exemplo, restaurando um banco de dados executado no SQL Server 2014 para SQL Server 2016is não tem suportada. Da mesma forma, não há suporte para restaurar um banco de dados do site executado em uma Standard edition do SQL Server 2016 para uma edição Enterprise do SQL Server 2016.
-   O SQL Server não pode estar definido como **modo de utilizador único**.
-   Certifique-se de que os ficheiros .MDF e .LDF são válidos. Quando você recupera um site, não há nenhuma verificação para o estado dos arquivos que você está restaurando.

**Se você usar um grupo de disponibilidade do SQL Server Always On para hospedar o banco de dados do site:** Modifique seus planos de recuperação, conforme descrito em [preparar para usar SQL Server Always On](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#changes-for-site-recovery).

**Quando você usar réplicas de banco de dados:** Depois de restaurar uma base de dados do site configurada para réplicas de bases de dados, antes de poder utilizar as réplicas de bases de dados, tem de reconfigurar cada réplica de base de dados, recriando as publicações e as subscrições.

## <a name="determine-your-recovery-options"></a>Determinar as opções de recuperação
Há duas áreas principais a serem consideradas para o servidor de site primário do Configuration Manager e recuperação de site de administração central; o **servidor do site** e **banco de dados do site**.
As seções a seguir podem ajudá-lo a selecionar as melhores opções para seu cenário de recuperação.

> [!NOTE]   
> Quando a instalação detecta um site existente do Configuration Manager no servidor, você pode iniciar uma recuperação de site, mas as opções de recuperação do servidor do site são limitadas. Por exemplo, se executar o Programa de Configuração num servidor de site existente, quando escolher a recuperação, poderá recuperar o servidor de base de dados do site, mas a opção de recuperação do servidor de site é desativada.

### <a name="site-server-recovery-options"></a>Opções de recuperação do servidor do site
Iniciar a instalação de uma cópia do **CD. Última** pasta criada fora da pasta de instalação do Configuration Manager.
-   Se você executar a instalação do Configuration Manager no **iniciar** menu no servidor do site, o **recuperar um site** opção não está disponível.
-   Se você instalou as atualizações de dentro do console do Configuration Manager antes de fazer o backup, será possível reinstalar com êxito o site usando a instalação da mídia de instalação ou o caminho de instalação do Configuration Manager.

Selecione o **recuperar um site** opção. Você tem as seguintes opções de recuperação para o servidor do site com falha:

-   **Recupere o servidor do site usando um backup existente:** Use essa opção quando você tiver um backup do servidor do site do Configuration Manager que foi criado no servidor do site como parte do **servidor do Site de Backup** tarefas de manutenção antes da falha do site. O site é reinstalado e as definições de site são configuradas, com base no site do qual foi efetuada a cópia de segurança.
-   **Reinstale o servidor do site:** Use essa opção quando você não tiver um backup do servidor do site. O servidor local é reinstalado e têm de ser especificadas as definições de site, tal como necessário durante uma instalação inicial.
  -   Você deve usar o mesmo código de site e o nome de banco de dados do site que você usou quando o site com falha foi instalado pela primeira vez.
  -   Você pode reinstalar o site em um novo computador que executa um novo sistema operacional.
  -   O computador deve usar o mesmo nome, o FQDN do servidor do site original.   

### <a name="site-database-recovery-options"></a>Opções de recuperação da base de dados do site
Quando executar o Programa de Configuração, tem as seguintes opções de recuperação da base de dados do site:
-   **Recupere o banco de dados do site usando um conjunto de backup:** Use essa opção quando você tiver um backup de dados do site do Configuration Manager que foi criado como parte do **servidor do Site de Backup** tarefa de manutenção do site antes da falha de banco de dados do site. Quando tem uma hierarquia, as alterações efetuadas à base de dados do site após a última cópia de segurança da mesma são obtidas a partir do site de administração central para um site primário ou de um site primário de referência para um site de administração central. Quando recuperar a base de dados do site para um site primário autónomo, perderá as alterações do site posteriores à última cópia de segurança.

   Quando recupera a base de dados de site para um site numa hierarquia, o comportamento da recuperação é diferente para um site de administração central e um site primário, e quando a última cópia de segurança é dentro ou fora do período de retenção de registo de alterações do SQL Server. Para obter mais informações, veja a secção [Cenários de Recuperação de Bases de Dados de Site](##site-database-recovery-scenarios) deste tópico.
  > [!NOTE]   
  > A recuperação falha se for escolhido o restauro da base de dados do site utilizando um conjunto de cópia de segurança, mas a base de dados do site já existe.  

-   **Crie um novo banco de dados para este site:** Use essa opção quando você não tiver um backup do banco de dados de site do Configuration Manager. Quando tem uma hierarquia, é criada uma nova base de dados do site e os dados são recuperados utilizando dados replicados do site de administração central para um site primário ou de um site primário de referência para um site de administração central. Esta opção não está disponível quando recupera um site primário autónomo ou um site de administração central que não tenha sites primários.

-   **Use um banco de dados do site recuperado manualmente:** Use essa opção quando você já tiver recuperado o banco de dados de site do Configuration Manager, mas deve concluir o processo de recuperação.
    -   Do Configuration Manager pode recuperar o banco de dados do site da tarefa de manutenção de backup do Configuration Manager ou de um backup de banco de dados do site que você pode executar usando o DPM ou outro processo. Depois de restaurar o banco de dados do site usando um método fora do Configuration Manager, você deve executar a instalação e selecione esta opção para concluir a recuperação de banco de dados do site.

    > [!NOTE]   
    > Quando você usa o DPM para fazer backup de seu banco de dados do site, use os procedimentos do DPM para restaurar o banco de dados do site em um local especificado antes de continuar o processo de restauração no Configuration Manager. Para obter mais informações sobre o DPM, veja a [Biblioteca de Documentação do Data Protection Manager]() no TechNet.    

    -   Quando tem uma hierarquia, as alterações efetuadas à base de dados do site após a última cópia de segurança da mesma são obtidas a partir do site de administração central para um site primário ou de um site primário de referência para um site de administração central. Quando recuperar a base de dados do site para um site primário autónomo, perderá as alterações do site posteriores à última cópia de segurança.     


-   **Ignorar a recuperação do banco de dados:** Use essa opção quando nenhuma perda de dados ocorreu no servidor de banco de dados do site do Configuration Manager. Esta opção só é válida quando a base de dados do site estiver num computador diferente do servidor do site que está a recuperar.

### <a name="sql-server-change-tracking-retention-period"></a>Período de retenção do registo de alterações do SQL Server
O registo de alterações está ativado para a base de dados do site no SQL Server. Controle de alterações permite que o Gerenciador de configuração de consulta para obter informações sobre as alterações que foram feitas para tabelas de banco de dados após um ponto anterior no tempo. O período de retenção especifica por quanto tempo as informações de registo de alterações são retidas. Por predefinição, a base de dados do site é configurada com um período de retenção de cinco dias. Quando recupera a base de dados de um site, o processo de recuperação procede de forma diferente se a sua cópia de segurança estiver dentro ou fora do período de retenção. Por exemplo, se o servidor da base de dados do site falhar e a última cópia de segurança tiver sido efetuada há 7 dias, está fora do período de retenção.

Para obter mais informações sobre recursos internos de controle de alterações do SQL Server, consulte os seguintes blogs da equipe do SQL Server: [Limpeza - parte 1 de controle de alterações](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-1/) e [limpeza de controle de alteração - parte 2](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-2).

### <a name="reinitialization-of-site-or-global-data"></a>Reinicialização de site ou dados globais
O processo para reinicializar um site ou dados globais substitui dados existentes na base de dados do site por dados da base de dados de outro site. Por exemplo, quando o site ABC reinicializa dados do site XYZ, ocorrem os seguintes passos:
-   Os dados são copiados do site XYZ para o site ABC.
-   Os dados existentes do site XYZ são removidos da base de dados do site no site ABC.
-   Os dados copiados do site XYZ são inseridos na base de dados do site ABC.

#### <a name="example-scenario-1"></a>Cenário de exemplo 1
**O site primário reinicializa os dados globais do site de administração central:** O processo de recuperação remove os dados globais existentes para o site primário no banco de dados do site primário e substitui os dados pelos dados globais copiados do site de administração central.

#### <a name="example-scenario-2"></a>Cenário de exemplo 2
**O site de administração central reinicializa os dados do site de um site primário:** O processo de recuperação remove os dados existentes desse site primário do banco de dados do site de administração central e substitui os dados pelos dados copiados do site primário. Os dados de site de outros sites primários não são afetados.

### <a name="site-database-recovery-scenarios"></a>Cenários de recuperação de bases de dados de site
Depois que um banco de dados do site é restaurado de um backup, o Configuration Manager tenta restaurar as alterações do site e dados globais após o último backup de banco de dados. A seguir descreve as ações que o Configuration Manager inicia depois que um banco de dados do site é restaurado do backup.

**O site recuperado é um site de administração central:**
-   **Cópia de segurança da base de dados dentro do período de retenção do registo de alterações**
    -   **Dados globais:** As alterações nos dados globais após o backup são replicadas de todos os sites primários.
    -   **Dados do site:** As alterações nos dados do site após o backup são replicadas de todos os sites primários.


-   **Cópia de segurança da base de dados anterior ao período de retenção do registo de alterações**
    -   **Dados globais:** O site de administração central reinicializa os dados globais do site primário de referência se você especificá-lo. Em seguida, todos os outros sites primários reinicializam os dados globais a partir do site de administração central. Se não for especificado nenhum site de referência, todos os sites primários reinicializam os dados globais a partir do site de administração central (os dados que foram restaurados a partir da cópia de segurança).
    -   **Dados do site:** O site de administração central reinicializa os dados do site de cada site primário.


**O site recuperado é um site primário:**
-   **Cópia de segurança da base de dados dentro do período de retenção do registo de alterações**
    -   **Dados globais:** As alterações nos dados globais após o backup são replicadas do site de administração central.
    -   **Dados do site:** O site de administração central reinicializa os dados do site do site primário. As alterações ocorridas após o backup são perdidas, mas a maioria dos dados são geradas novamente pelos clientes que enviam as informações para o site primário.


-   **Cópia de segurança da base de dados anterior ao período de retenção do registo de alterações**
    -   **Dados globais:** O site primário reinicializa os dados globais do site de administração central.
    -   **Dados do site:** O site de administração central reinicializa os dados do site do site primário. As alterações ocorridas após o backup são perdidas, mas a maioria dos dados são geradas novamente pelos clientes que enviam as informações para o site primário.

## <a name="site-recovery-procedures"></a>Procedimentos de recuperação de sites
Utilize um dos seguintes procedimentos para recuperar o servidor e a base de dados do site.

### <a name="to-start-a-site-recovery-in-the-setup-wizard"></a>Para iniciar a recuperação de um site no Assistente de Configuração
1.  Copie o [CD. Última pasta](/sccm/core/servers/manage/the-cd.latest-folde) para um local fora da pasta de instalação do Configuration Manager.
Da cópia do CD. Pasta mais recente, execute o Assistente de instalação do Configuration Manager.

2.  Na página **Introdução** , selecione **Recuperar um site**e clique em **Seguinte**.

3.  Conclua o assistente utilizando as opções adequadas para a recuperação do seu site.

  -   Durante a recuperação, a Configuração identifica a porta do SQL Server Service Broker (SSB) utilizada pelo SQL Server. Não altere esta definição de porta durante a recuperação ou a replicação de dados não funcionará corretamente depois da recuperação ser concluída.

  -   Você pode especificar o original ou um novo caminho a ser usado para a instalação do Configuration Manager no Assistente de instalação.

### <a name="to-start-an-unattended-site-recovery"></a>Para iniciar uma recuperação de site automática
  1.    Prepare o script de instalação automática para as opções de que necessita para a recuperação do site.  Consulte [chaves de arquivo de script de recuperação autônoma do site](/sccm/protect/understand/unattended-site-recovery-script-file-keys).

  2.    Execute a instalação do Configuration Manager usando o comando **/script** opção. Por exemplo, se você nomeasse seu arquivo de inicialização de instalação ConfigMgrUnattend.ini e salvo no diretório C:\Temp do computador no qual você está executando a instalação, o comando será da seguinte maneira: **Setup /script C:\temp\ConfigMgrUnattend.ini**.

  > [!NOTE]   
  >  Depois de recuperar um site de administração central, a replicação de alguns dados do site a partir de sites subordinados poderá não ser estabelecida. Isto pode incluir inventário de hardware, inventário de software e mensagens de estado.
  >
  >  Se esta situação ocorrer, tem de reinicializar **ConfigMgrDRSSiteQueue** para a replicação da base de dados.  Para fazer isso, use **SQL Server Manager** para executar a consulta a seguir no Gerenciador de configuração de banco de dados do site no site de administração central:
  >
  >  **IF EXISTS (SELECIONE \* EM sys.service_queues EM QUE name = “ConfigMgrDRSSiteQueue” AND is_receive_enabled = 0)**
  >
  >  **ALTER QUEUE [dbo].[ConfigMgrDRSSiteQueue] WITH STATUS = ON**


## <a name="post-recovery-tasks"></a>Tarefas de pós-recuperação
Depois de recuperar o seu site, existem várias tarefas pós-recuperação que tem de considerar para concluir a recuperação do site. Utilize as secções seguintes para concluir o processo de recuperação do site.

### <a name="re-enter-user-account-passwords"></a>Reintroduzir palavras-passe de contas de utilizador
Após a recuperação de um servidor do site, as palavras-passe das contas de utilizador especificadas para o site tem de ser reintroduzidas, porque são repostas durante a recuperação do site. As contas são listadas na página **Terminado** do Assistente de Configuração após a recuperação do site ser concluída e guardada em C:\ConfigMgrPostRecoveryActions.html, no servidor de site recuperado.

#### <a name="to-re-enter-user-account-passwords-after-site-recovery"></a>Para reintroduzir palavras-passe de contas de utilizador após a recuperação do site

1.  Abra o console do Configuration Manager e conecte-se ao site recuperado.

2.  Na consola do Configuration Manager, clique em **Administração**.

3.  Na área de trabalho **Administração** , expanda **Segurança**e clique em **Contas**.

4.  Para cada conta em que você insira novamente a senha, faça o seguinte:

    1.  Selecione a conta na lista de contas que foram identificadas depois da recuperação do site. Pode encontrar esta lista em C:\ConfigMgrPostRecoveryActions.html, no servidor do site recuperado.

    2.  No separador **Home page** , no grupo **Propriedades** , clique em **Propriedades** para abrir as propriedades da conta.

    3.  No separador **Geral** , clique em **Definir**e reintroduza as palavras-passe da conta.

    4.  Clique em **Verificar**, selecione a origem de dados adequada para a conta de utilizador selecionada e clique em **Testar ligação** para verificar se a conta de utilizador se consegue ligar à origem de dados.

    5.  Clique em **OK** para guardar as alterações de palavra-passe e, em seguida, clique em **OK**.

### <a name="re-enter-sideloading-keys"></a>Reintroduzir chaves de sideload
Após uma recuperação do servidor do site, é necessário reintroduzir as chaves de sideload do Windows especificadas para o site porque foram repostas durante a recuperação do site. Depois de inserir novamente as chaves de sideload, a contagem no **ativações usadas** coluna para as chaves de sideload do Windows é redefinida no console do Configuration Manager. Por exemplo, digamos que antes da falha do site uma **Total de ativações** contagem definida como **100** e **ativações usadas** no **90** para o número de chaves que foram usados pelos dispositivos. Após a recuperação do site, a coluna **Total de ativações** continua a apresentar **100**, mas a coluna **Ativações utilizadas** apresenta incorretamente **0**. No entanto, depois de 10 novos dispositivos utilizarem uma chave de sideload, não existirão chaves de sideload restantes e o dispositivo seguinte não conseguirá aplicar uma chave de sideload.

### <a name="recreate-the-microsoft-intune-subscription"></a>Recriar a subscrição do Microsoft Intune
 Se você recuperar um servidor de site do Configuration Manager depois que o computador servidor do site é uma imagem, a assinatura do Microsoft Intune não será restaurada. Depois de recuperar o site, você deve reconectar sua assinatura.  Não crie uma nova solicitação de APN, mas em vez disso, carregue o atual. PEM-arquivo válido que foi carregado a última vez em que o gerenciamento de iOS foi configurado ou renovado. Para obter mais informações, veja [Configurar a Subscrição do Microsoft Intune](/sccm/mdm/deploy-use/configure-intune-subscription).

### <a name="configure-ssl-for-site-system-roles-that-use-iis"></a>Configurar o SSL para funções do sistema de sites que utilizam IIS
Ao recuperar sistemas de sites que executam o IIS e estavam configurados para HTTPS antes da falha, é necessário reconfigurar o IIS para utilizar o certificado do servidor Web.

### <a name="reinstall-hotfixes-in-the-recovered-site-server"></a>Reinstalar correções no servidor do site recuperado
Após uma recuperação de site, é necessário reinstalar as correções que foram aplicadas ao servidor do site. Exibir a lista de hotfixes instalados anteriormente no **concluído** página do Assistente de instalação após a recuperação de site. Essa lista também será salva **C:\ConfigMgrPostRecoveryActions.html** no servidor do site recuperado.

### <a name="recover-custom-reports-on-the-computer-running-reporting-services"></a>Recuperar relatórios personalizados no computador com o Reporting Services
Quando tiverem sido criados relatórios personalizados do Reporting Services e o Reporting Services falhar, é possível recuperar os relatórios se tiver sido efetuada uma cópia de segurança do servidor de relatórios. Para obter mais informações sobre o restauro de relatórios personalizados no Reporting Services, veja [Operações de Cópia de Segurança e Restauro de uma Instalação do Reporting Services](http://go.microsoft.com/fwlink/p/?LinkId=228724) na Documentação Online do SQL Server 2008.

### <a name="recover-content-files"></a>Recuperar ficheiros de conteúdo
 A base de dados do site contém informações sobre o local onde os ficheiros de conteúdo estão armazenados no servidor do site, mas a cópia de segurança dos ficheiros de conteúdo e o seu restauro não são efetuados como parte do processo de cópia de segurança e restauro. Para recuperar os ficheiros de conteúdo na totalidade, é necessário restaurar a biblioteca de conteúdos e os ficheiros de origem do pacote para a localização original. Existem vários métodos para recuperar os ficheiros de conteúdo, mas o método mais simples consiste em restaurar os ficheiros a partir de uma cópia de segurança do sistema de ficheiros do servidor do site.

 Se você não tiver um backup de sistema de arquivos para os arquivos de origem do pacote, você deve manualmente copiar ou baixá-los como você fez originalmente quando o pacote foi criado pela primeira vez. Pode executar a seguinte consulta no SQL Server para encontrar a localização de origem do pacote para todos os pacotes e aplicações: `SELECT * FROM v_Package`. Pode identificar o site de origem do pacote atravésdos primeiros três carateres do ID de pacote. Por exemplo, se o ID de pacote for CEN00001, o código de site do site de origem é CEN. Ao restaurar os ficheiros de origem do pacote, estes devem ser restaurados para a mesma localização em que se encontravam antes da falha.

 Se não tiver uma cópia de segurança do sistema de ficheiros que contém a biblioteca de conteúdos, dispõe das seguintes opções de restauro:

-   **Importar um arquivo de conteúdo pré-teste**: Quando você tem uma hierarquia do Configuration Manager, você pode criar um arquivo de conteúdo pré-teste com todos os pacotes e aplicativos de outro local e, em seguida, importe o arquivo de conteúdo pré-teste para recuperar a biblioteca de conteúdo no servidor do site.

-   **Atualizar conteúdo**: Quando você inicia a ação de atualização de conteúdo para um tipo de implantação do pacote ou aplicativo, o conteúdo é copiado da origem do pacote para a biblioteca de conteúdo. Os ficheiros de origem do pacote têm de estar disponíveis na localização original para que esta ação seja concluída com êxito. É necessário executar esta ação em cada pacote e em cada aplicação.

### <a name="recover-custom-software-updates-on-the-computer-running-updates-publisher"></a>Recuperar atualizações de software personalizadas no computador com o Updates Publisher
Ao incluir arquivos de banco de dados do Updates Publisher no seu plano de backup, você pode recuperar os bancos de dados em caso de falha no computador no qual o Updates Publisher é executado. Para obter mais informações sobre o Updates Publisher, veja [System Center Updates Publisher 2011](http://go.microsoft.com/fwlink/p/?LinkId=228726) na Biblioteca TechCenter do System Center.

Use o procedimento a seguir para restaurar o banco de dados do Updates Publisher.

#### <a name="to-restore-the-updates-publisher-2011-database"></a>Para restaurar a base de dados do Updates Publisher 2011
1.  Reinstale o Updates Publisher no computador recuperado.

2.  Copie o arquivo de banco de dados (Scupdb.sdf) de destino de backup para %*USERPROFILE*%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\ no computador que executa o Updates Publisher.

3.  Quando mais de um usuário executa o Updates Publisher no computador, você deve copiar cada arquivo de banco de dados para o local do perfil de usuário apropriado.

### <a name="user-state-migration-data"></a>Dados de migração de estado de utilizador
Como parte das propriedades do sistema de sites do ponto de migração de estado, deve especificar as pastas que armazenam dados de migração de estado de utilizador. Depois de recuperar um servidor com uma pasta que armazena dados de migração de estado de utilizador, tem de restaurar manualmente os dados de migração de estado de utilizador no servidor para a mesma pasta que armazenava os dados antes da falha.

### <a name="regenerate-the-certificates-for-distribution-points"></a>Gerar novamente os certificados para pontos de distribuição
Depois de restaurar um site, o distmgr.log pode conter a seguinte entrada para um ou mais pontos de distribuição: **Falha ao descriptografar dados PFX do certificado**. Esta entrada indica que não é possível desencriptar os dados de certificado do ponto de distribuição pelo site. Para resolver esse problema, você deve gerar novamente ou importar novamente o certificado para pontos de distribuição afetados. Pode fazê-lo com o cmdlet do PowerShell [Set-CMDistributionPoint](https://technet.microsoft.com/library/jj821872\(v=sc.20\).aspx).

### <a name="update-certificates-used-for-cloud-based-distribution-points"></a>Atualizar Certificados Utilizados para pontos de distribuição Baseados na Nuvem
 Configuration Manager exige um certificado de gerenciamento que ele utiliza para o servidor do site para comunicação do ponto de distribuição baseado em nuvem. Após uma recuperação de site, é necessário atualizar os certificados dos pontos de distribuição baseados na nuvem.

## <a name="recover-a-secondary-site"></a>Recuperar um site secundário
 Gerenciador de configuração não suporta o backup do banco de dados em um site secundário, mas oferece suporte à recuperação reinstalando o site secundário. Recuperação de site secundário é necessária quando um site secundário do Configuration Manager falha.

### <a name="requirements-for-reinstalling-a-secondary-site"></a>Requisitos para a reinstalação de um site secundário
-   O computador deve atender a todos os pré-requisitos do site secundário e ter a segurança apropriada direitos configurados.
-   Você deve usar o mesmo caminho de instalação que foi usado para o site com falha.
-   Tem de utilizar um computador com a mesma configuração do computador que falhou, tal como o seu FQDN, para recuperar com êxito o site secundário.
-   O computador deve ter a mesma configuração do SQL Server como o site com falha.
  -   Durante a recuperação de site secundário, Configuration Manager não instalar o SQL Server Express se ele já não estiver instalado no computador.
  -   Tem de utilizar a mesma versão do SQL Server e a mesma instância do SQL Server que utilizou para a base de dados do site secundário antes da falha.

### <a name="to-recover-a-secondary-site"></a>Para recuperar um site secundário:
Para recuperar um site secundário, use o **recuperar Site secundário** ação o **Sites** nó no console do Configuration Manager. Ao contrário da recuperação de um site de administração central ou site primário, a recuperação de um site secundário não utiliza um ficheiro de cópia de segurança e, em vez disso, reinstala os ficheiros do site secundário no computador do site secundário que falhou. Depois que o site reinstala, os dados do site secundário são reinicializados com os dados do site pai primário.

Durante o processo de recuperação, o Configuration Manager verifica se a biblioteca de conteúdo existe no computador do site secundário e se o conteúdo apropriado está disponível. O site secundário utilizará a biblioteca de conteúdos existente, caso contenha o conteúdo apropriado. Caso contrário, a recuperação da biblioteca de conteúdos de um site secundário recuperado requer a redistribuição ou pré-configuração do conteúdo para esse site recuperado.

Quando tem um ponto de distribuição que não se encontra no site secundário, não é necessário reinstalar o ponto de distribuição durante a recuperação do site secundário. Após a recuperação do site secundário, o site sincroniza automaticamente com o ponto de distribuição.

Você pode verificar o status da recuperação do site secundário, usando o **Mostrar Status da instalação** ação o **Sites** nó no console do Configuration Manager.

