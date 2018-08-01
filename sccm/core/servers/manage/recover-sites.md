---
title: Recuperação de sites
titleSuffix: Configuration Manager
description: Aprenda a recuperar seus sites no Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 19539f4d-1667-4b4c-99a1-9995f12cf5f7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 76d81694e346384359b21082f16b6ffb26903cb2
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39387068"
---
#  <a name="recover-a-configuration-manager-site"></a>Recuperar um site do Gestor de Configuração

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Executar uma recuperação de site do Configuration Manager após a falha de um site ou ocorrer perda de dados na base de dados do site. Reparar e ressincronizar dados são as tarefas principais de uma recuperação de site e são necessárias para evitar a interrupção das operações.

As secções neste artigo podem ajudá-lo a recuperar um site do Configuration Manager. Para criar uma cópia de segurança, veja [cópia de segurança para o Configuration Manager](/sccm/core/servers/manage/backup-and-recovery).



## <a name="considerations-before-recovering-a-site"></a>Considerações antes de recuperar um site
> [!Important]  
> Estas informações só se aplica a cenários de recuperação de site. Quando estiver a atualizar a infraestrutura no local e não estiver a recuperar um site que falhou, reveja as informações nos seguintes artigos:
> - [Atualizar a infraestrutura no local](/sccm/core/servers/manage/upgrade-on-premises-infrastructure)
> - [Modificar a infraestrutura](/sccm/core/servers/manage/modify-your-infrastructure)


#### <a name="use-the-same-version-and-edition-of-sql-server"></a>Utilizar a mesma versão e edição do SQL Server   
Por exemplo, não é suportado restaurar uma base de dados do SQL Server 2014 para o SQL Server 2016. Da mesma forma, não é suportado restaurar uma base de dados do site do SQL Server 2016 a partir da edição Standard para a Enterprise edition.
- SQL Server não pode ser definido como **modo de utilizador único**.
- Certifique-se de que os ficheiros .MDF e .LDF são válidos. Quando recupera um site, não há nenhuma verificação para o estado dos ficheiros.  

#### <a name="sql-server-always-on-availability-groups"></a>Grupos de disponibilidade Always On do SQL Server   
Se utilizar grupos de disponibilidade Always On do SQL Server para alojar a base de dados do site, modifique seus planos de recuperação conforme descrito em [preparar para utilizar o SQL Server Always On](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#changes-for-site-recovery).

#### <a name="database-replicas"></a>Réplicas de base de dados  
Depois de restaurar uma base de dados do site que foi configurada para réplicas de base de dados, antes de poder utilizar as réplicas de base de dados, reconfigure cada réplica de base de dados para recriar as publicações e subscrições.



## <a name="determine-your-recovery-options"></a>Determinar as opções de recuperação
Existem duas áreas principais a considerar para o servidor de site primário do Configuration Manager e a recuperação de site de administração central: os **servidor do site** e o **base de dados do site**.
As secções seguintes podem ajudá-lo a selecionar as opções melhores para o seu cenário de recuperação.

> [!NOTE]   
> Quando a configuração do Configuration Manager Deteta um site existente no servidor, pode iniciar uma recuperação de site, mas as opções de recuperação para o servidor de site são limitadas. Por exemplo, se executar o Programa de Configuração num servidor de site existente, quando escolher a recuperação, poderá recuperar o servidor de base de dados do site, mas a opção de recuperação do servidor de site é desativada.

### <a name="site-server-recovery-options"></a>Opções de recuperação do servidor do site
Iniciar configuração do Configuration Manager a partir de uma cópia do **CD. Mais recente** pasta que criou fora da pasta de instalação do Configuration Manager.  
-   Se executar a configuração a partir do **começar** menu no servidor do site, o **recuperar um site** opção não está disponível.
-   Se tiver instalado todas as atualizações da consola do Configuration Manager antes de feita a cópia de segurança, não é reinstalado com êxito o site utilizando a configuração a partir de mídia de instalação ou o caminho de instalação do Configuration Manager.

Em seguida, selecione o **recuperar um site** opção. Tem as seguintes opções de recuperação para o servidor de site em falha:  

-   **Recuperar o servidor do site utilizando uma cópia de segurança existente**: Utilize esta opção quando tem uma cópia de segurança do servidor do site do Configuration Manager que foi criada no servidor do site como parte do **servidor do Site de cópia de segurança** tarefa de manutenção antes da falha do site. O site é reinstalado e as definições de site são configuradas com base no site que foi feito backup.  

-   **Reinstalar o servidor do site**: Utilize esta opção quando não tiver uma cópia de segurança do servidor do site. O servidor do site é reinstalado e tem de especificar as definições de site como necessário durante uma instalação inicial.  

     -   Utilize o mesmo código de site e o nome de base de dados do site que foi utilizado quando o site em falha foi instalado pela primeira vez.  

     -   Pode reinstalar o site num novo computador que executa uma nova versão de SO.  

     -   O servidor tem de utilizar o mesmo nome de anfitrião e o nome de domínio completamente qualificado (FQDN) do servidor do site original.   

### <a name="site-database-recovery-options"></a>Opções de recuperação da base de dados do site
Quando executar a configuração do Configuration Manager, tem as seguintes opções de recuperação da base de dados do site:  

- **Recuperar a base de dados do site utilizando um conjunto de cópia de segurança**: Utilize esta opção quando tem uma cópia de segurança da base de dados do site que foi criada como parte dos **servidor do Site de cópia de segurança** tarefa de manutenção executada no site antes da falha de base de dados do site. Numa hierarquia, as alterações efetuadas na base de dados do site após a base de dados do site última cópia de segurança são obtidas a partir do site de administração central para um site primário ou de um site primário de referência para o site de administração central. Quando recuperar a base de dados do site para um site primário autónomo, perderá as alterações do site posteriores à última cópia de segurança.  

     Quando recupera a base de dados de site para um site numa hierarquia, o comportamento da recuperação é diferente para um site de administração central e um site primário, e quando a última cópia de segurança é dentro ou fora do período de retenção de registo de alterações do SQL Server. Para obter mais informações, consulte a [cenários de recuperação de bases de dados do Site](##site-database-recovery-scenarios) secção deste artigo.  

     > [!NOTE]   
     > Se optar por restaurar a base de dados do site com um conjunto de cópias de segurança, mas a base de dados do site já existe, a recuperação falhará.   

- **Criar uma nova base de dados para este site**: Utilize esta opção quando não tiver uma cópia de segurança da base de dados do site. Numa hierarquia, é criada uma nova base de dados do site e os dados são recuperados utilizando dados replicados do site de administração central para um site primário ou um site primário de referência para um site de administração central. Esta opção não está disponível quando estiver a recuperar um site primário autónomo ou um site de administração central que não tenha sites primários.  

- **Utilizar uma base de dados do site que foi recuperado manualmente**: Utilize esta opção quando já tiver recuperado a base de dados do site do Configuration Manager, mas tem de concluir o processo de recuperação.  

     - O Configuration Manager pode recuperar a base de dados de tarefa de manutenção cópia de segurança do Configuration Manager ou de uma cópia de segurança de base de dados de site que efetuar ao utilizar o Data Protection Manager (DPM) ou outro processo. Depois de restaurar a base de dados do site utilizando um método fora do Configuration Manager, execute a configuração e selecione esta opção para concluir a recuperação de base de dados do site.  

     > [!NOTE]   
     > Quando utilizar o DPM para criar cópias de segurança da base de dados do site, utilize os procedimentos do DPM para restaurar a base de dados do site para uma localização especificada antes de continuar o processo de restauração no Configuration Manager. Para obter mais informações sobre o DPM, consulte a [Data Protection Manager](https://docs.microsoft.com/system-center/dpm) biblioteca de documentação.    

     - Numa hierarquia, as alterações efetuadas na base de dados do site após a base de dados do site última cópia de segurança são obtidas a partir do site de administração central para um site primário ou de um site primário de referência para o site de administração central. Quando recuperar a base de dados do site para um site primário autónomo, perderá as alterações do site posteriores à última cópia de segurança.     


- **Ignorar recuperação de base de dados**: Utilize esta opção quando sem perda de dados tiver ocorrido no servidor de base de dados do site do Configuration Manager. Esta opção só é válida quando a base de dados estiver num computador diferente do servidor do site que estiver a recuperar.  

### <a name="sql-server-change-tracking-retention-period"></a>Período de retenção do registo de alterações do SQL Server
O registo de alterações está ativado para a base de dados do site no SQL Server. Controlo de alterações permite que o Gestor de configuração de consulta para obter informações sobre as alterações que foram efetuadas às tabelas de base de dados depois de um ponto anterior no tempo. O período de retenção Especifica o intervalo de tempo alteração informações de controlo é mantida. Por predefinição, a base de dados do site está configurado com um período de retenção de cinco dias. Quando recupera a base de dados de um site, o processo de recuperação procede de forma diferente se a sua cópia de segurança estiver dentro ou fora do período de retenção. Por exemplo, se seu servidor de base de dados do site falha e a última cópia de segurança é sete dias, está fora do período de retenção.

Para obter mais informações sobre elementos internos de controlo de alterações do SQL Server, consulte que as seguinte mensagens de blogue da equipa do SQL Server: [Limpeza - parte 1 de controlo de alterações](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-1/) e [limpeza de alteração de controlo - parte 2](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-2).

### <a name="reinitialization-of-site-or-global-data"></a>Reinicialização do site ou dados globais
O processo para reinicializar um site ou dados globais substitui dados existentes na base de dados do site por dados da base de dados de outro site. Por exemplo, quando o site ABC reinicializa dados do site XYZ, ocorrem os seguintes passos:
- Os dados são copiados do site XYZ para o site ABC.
- Os dados existentes do site XYZ são removidos da base de dados do site no site ABC.
- Os dados copiados do site XYZ são inseridos na base de dados do site ABC.

#### <a name="example-scenario-1-the-primary-site-reinitializes-the-global-data-from-the-central-administration-site"></a>Cenário de exemplo 1: O site primário reinicializa os dados globais a partir do site de administração central  
O processo de recuperação remove os dados globais existentes para o site primário na base de dados do site primário e substitui-pelos dados globais copiados do site de administração central.

#### <a name="example-scenario-2-the-central-administration-site-reinitializes-the-site-data-from-a-primary-site"></a>Cenário de exemplo 2: O site de administração central reinicializa os dados do site de um site primário 
O processo de recuperação remove os dados de site existentes para esse site primário na base de dados de site de administração central e substitui-pelos dados do site copiados do site primário. Os dados do site de outros sites primários não são afetados.

### <a name="site-database-recovery-scenarios"></a>Cenários de recuperação de bases de dados de site
Depois de restaurar uma base de dados do site de uma cópia de segurança, o Configuration Manager tenta restaurar as alterações nos dados globais e de site após a última cópia de segurança de base de dados. O Configuration Manager começa as seguintes ações depois de uma base de dados do site é restaurado a partir de cópia de segurança:  

#### <a name="recovered-site-is-a-central-administration-site"></a>O site recuperado é um site de administração central
- Cópia de segurança da base de dados dentro do período de retenção do registo de alterações  
     - **Dados globais**: As alterações nos dados globais posteriores a cópia de segurança são replicadas a partir de todos os sites primários.  
     - **Dados do site**: As alterações nos dados de site após a cópia de segurança são replicadas a partir de todos os sites primários.  


- Cópia de segurança da base de dados anterior ao período de retenção do registo de alterações  
     - **Dados globais**: O site de administração central reinicializa os dados globais a partir do site primário de referência, caso o especifique. Em seguida, todos os outros sites primários reinicializam os dados globais a partir do site de administração central. Se não for especificado nenhum site de referência, todos os sites primários reinicializam os dados globais a partir do site de administração central (os dados que foram restaurados a partir da cópia de segurança).  
     - **Dados do site**: O site de administração central reinicializa os dados de cada site primário.  


#### <a name="recovered-site-is-a-primary-site"></a>O site recuperado é um site primário
- Cópia de segurança da base de dados dentro do período de retenção do registo de alterações
     - **Dados globais**: As alterações nos dados globais posteriores a cópia de segurança são replicadas a partir do site de administração central.  
     - **Dados do site**: O site de administração central reinicializa os dados do site do site primário. Alterações após a cópia de segurança são perdidas, mas a maior parte dos dados são novamente gerada por clientes que enviam informações para o site primário.  


- Cópia de segurança da base de dados anterior ao período de retenção do registo de alterações
     - **Dados globais**: O site primário reinicializa os dados globais a partir do site de administração central.  
     - **Dados do site**: O site de administração central reinicializa os dados do site do site primário. Alterações após a cópia de segurança são perdidas, mas a maior parte dos dados são novamente gerada por clientes que enviam informações para o site primário.  



## <a name="site-recovery-procedures"></a>Procedimentos de recuperação de sites
Utilize um dos seguintes procedimentos para ajudar a recuperar o servidor de site e base de dados do site:

### <a name="start-a-site-recovery-in-the-setup-wizard"></a>Iniciar uma recuperação de site no Assistente de configuração
1.  Copiar o [CD. Pasta mais recente](/sccm/core/servers/manage/the-cd.latest-folder) para uma localização fora da pasta de instalação do Configuration Manager. Partir da cópia do CD. Pasta mais recente, executar o Assistente de configuração do Configuration Manager.

2.  Na página **Introdução** , selecione **Recuperar um site**e clique em **Seguinte**.  

3.  Conclua o assistente utilizando as opções adequadas para a recuperação do seu site.  

     - Durante a recuperação, a configuração identifica a porta do SQL Server Service Broker (SSB) utilizada pelo SQL Server. Não alterar esta definição de porta durante a recuperação ou a replicação de dados não funcionará corretamente depois de concluir a recuperação.  

     - Pode especificar o original ou um novo caminho a utilizar para a instalação do Configuration Manager no Assistente de configuração.  

### <a name="start-an-unattended-site-recovery"></a>Iniciar uma recuperação automática de site
1. Prepare o script de instalação automática para as opções de que necessita para a recuperação do site. Para obter mais informações, consulte [chaves de ficheiro de script de recuperação automática de site](/sccm/protect/understand/unattended-site-recovery-script-file-keys).  

2. Execute a configuração do Configuration Manager utilizando o `/script` opção da linha de comandos. Por exemplo, se chamar o ficheiro de inicialização do programa de configuração **Configmgrunattend** e guardou-na `C:\Temp` diretório do computador no qual está a executar a configuração, o comando seria da seguinte forma: `setup.exe /script C:\temp\ConfigMgrUnattend.ini`.  


> [!NOTE]   
>  Depois de recuperar um site de administração central, a replicação de alguns dados do site a partir de sites subordinados poderá não ser estabelecida. Estes dados podem incluir inventário de hardware, inventário de software e mensagens de estado.
>
>  Se este problema ocorrer, reinicializar o **ConfigMgrDRSSiteQueue** para a replicação de base de dados. Uso **SQL Server Manager** para executar a consulta seguinte na base de dados de site para o site de administração central:
>
> ``` SQL
> IF EXISTS (SELECT * FROM sys.service_queues WHERE name = 'ConfigMgrDRSSiteQueue' AND is_receive_enabled = 0)  
>  
> ALTER QUEUE [dbo].[ConfigMgrDRSSiteQueue] WITH STATUS = ON
> ```



## <a name="post-recovery-tasks"></a>Tarefas de pós-recuperação
Depois de recuperar o seu site, existem várias tarefas de pós-recuperação a considerar antes da recuperação de site estiver concluída. Utilize as secções seguintes para concluir o processo de recuperação do site.

### <a name="re-enter-user-account-passwords"></a>Reintroduzir palavras-passe de contas de utilizador
Após uma recuperação do servidor de site, palavras-passe para as contas de utilizador especificadas para o site tem de ser reintroduzidas porque são repostas durante a recuperação de site. As contas são listadas na **concluído** página do Assistente de configuração após a conclusão da recuperação de sites. Também é guardada a lista para `C:\ConfigMgrPostRecoveryActions.html` no servidor do site recuperado.

#### <a name="re-enter-user-account-passwords-after-site-recovery"></a>Reintroduzir palavras-passe da conta de utilizador após a recuperação de site

1. Abra a consola do Configuration Manager e ligue ao site recuperado.  

2. Vá para o **Administration** área de trabalho, expanda **segurança**e, em seguida, clique em **contas**.  

3. Para cada conta, siga os passos abaixo para voltar a introduzir a palavra-passe:  

     1. Selecione a conta na lista identificada após a recuperação de site.  

     2. Clique em **propriedades** na faixa de opções.  

     3. Na **gerais** separador, clique em **definir**, e, em seguida, volte a introduzir a palavra-passe para a conta.  

     4. Clique em **Verifique se**, selecione a origem de dados adequada para a conta de utilizador selecionada e, em seguida, clique em **Testar ligação**. Este passo de testes que a conta de utilizador pode ligar à origem de dados e verifica as credenciais.  

     5. Clique em **OK** para guardar as alterações de palavra-passe e, em seguida, clique em **OK** para fechar a página de propriedades da conta.  

### <a name="re-enter-sideloading-keys"></a>Reintroduzir chaves de sideload
Após uma recuperação do servidor de site, volte a introduzir as chaves de sideload do Windows especificadas para o site porque são repostas durante a recuperação de site. Depois de reintroduzir as chaves de sideload, a contagem na **ativações utilizadas** coluna para chaves de sideload do Windows é reposta na consola do Configuration Manager. Por exemplo, se, antes da falha do site do **Total de ativações** contagem é definida como **100** e o número de chaves que foram utilizados por dispositivos como **ativações utilizadas** é **90**. Após a recuperação de site, o **Total de ativações** continua a apresentar **100**, mas o **ativações utilizadas** coluna apresenta incorretamente **0** . Depois de 10 novos dispositivos utilizarem uma chave de sideload, não há nenhuma mais chaves de sideload e o dispositivo 11 não será aplicada uma chave de sideload.

### <a name="recreate-the-microsoft-intune-subscription"></a>Recriar a subscrição do Microsoft Intune
Se estiver a recuperar um servidor de site do Configuration Manager após é recriar a imagem de servidor do site, não é restaurada a subscrição do Microsoft Intune. Voltar a ligar a sua subscrição depois de recuperar o site. Não crie um novo pedido APN, mas em vez disso, carregue o ficheiro. pem válido atual que foi carregado a última vez a gestão de iOS foi configurada ou renovada. Para obter mais informações, veja [Configurar a Subscrição do Microsoft Intune](/sccm/mdm/deploy-use/configure-intune-subscription).

### <a name="configure-ssl-for-site-system-roles-that-use-iis"></a>Configurar o SSL para funções do sistema de sites que utilizam IIS
Ao recuperar sistemas de sites que executam o IIS e estavam configurados para HTTPS antes da falha, reconfigure o IIS para utilizar o certificado de servidor web.

### <a name="reinstall-hotfixes"></a>Reinstalar correções 
Após uma recuperação de site, é necessário reinstalar as correções que foram aplicadas ao servidor do site. Ver a lista de correções instaladas anteriormente sobre o **concluído** página do Assistente de configuração após a recuperação de site. Esta lista também é guardada para `C:\ConfigMgrPostRecoveryActions.html` no servidor do site recuperado.

### <a name="recover-custom-reports"></a>Recuperar relatórios personalizados 
Quando tiver criado relatórios personalizados no SQL Server Reporting Services e este componente falha, pode recuperar os relatórios quando fez backup no servidor de relatórios. Para obter mais informações sobre o restauro de relatórios personalizados no Reporting Services, consulte [cópia de segurança e as operações de restauro de mensagens em fila para o Reporting Services](https://docs.microsoft.com/sql/reporting-services/install-windows/backup-and-restore-operations-for-reporting-services).

### <a name="recover-content-files"></a>Recuperar ficheiros de conteúdo
A base de dados contém informações sobre onde os ficheiros de conteúdo são armazenados no servidor do site, mas os ficheiros de conteúdo não são uma cópia de segurança ou restaurados como parte do processo de cópia de segurança e recuperação. Para recuperar totalmente os ficheiros de conteúdo, restaure os ficheiros de origem de biblioteca e o pacote de conteúdo para a localização original. Existem vários métodos para recuperar os ficheiros de conteúdo, mas o método mais simples consiste em restaurar os ficheiros a partir de uma cópia de segurança do sistema de ficheiros do servidor do site.

 Se não tiver uma cópia de segurança do sistema de ficheiros para os ficheiros de origem do pacote, copiar ou transferir manualmente-los tal como fez quando criou o pacote pela primeira vez. Pode executar a seguinte consulta no SQL Server para encontrar a localização de origem do pacote para todos os pacotes e aplicações: `SELECT * FROM v_Package`. Pode identificar o site de origem do pacote atravésdos primeiros três carateres do ID de pacote. Por exemplo, se o ID de pacote for CEN00001, o código de site do site de origem é CEN. Ao restaurar os ficheiros de origem do pacote, estes devem ser restaurados para a mesma localização em que se encontravam antes da falha.

 Se não tiver uma cópia de segurança de sistema de ficheiro que contém a biblioteca de conteúdos, tem as seguintes opções de restauro:  

- **Importar um ficheiro de conteúdo pré-configurado**: Numa hierarquia do Configuration Manager, pode criar um ficheiro de conteúdo pré-configurado com todos os pacotes e aplicações de outra localização. Em seguida, importe o ficheiro de conteúdo pré-configurado para recuperar a biblioteca de conteúdos no servidor do site.  

- **Atualizar conteúdo**: Quando inicia a ação de conteúdo de atualização para um tipo de implementação do pacote ou aplicação, o conteúdo é copiado da origem do pacote para a biblioteca de conteúdos. Os ficheiros de origem do pacote têm de estar disponíveis na localização original para que esta ação seja concluída com êxito. Efetue esta ação em cada pacote e o aplicativo.

### <a name="recover-custom-software-updates"></a>Recuperar atualizações de software personalizadas
Quando inclui ficheiros de base de dados do System Center Updates Publisher no seu plano de cópia de segurança, pode recuperar as bases de dados se falhar o computador do Updates Publisher. Para obter mais informações sobre o Updates Publisher, consulte [System Center Updates Publisher](/sccm/sum/tools/updates-publisher).

#### <a name="restore-the-updates-publisher-database"></a>Restaurar a base de dados do Updates Publisher
1. Reinstale o Updates Publisher no computador recuperado.  

2. Copie o ficheiro de base de dados **scupdb** do destino da cópia de segurança para `%USERPROFILE%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\` no computador que executa o Updates Publisher.  

3. Quando mais do que um utilizador com o Updates Publisher no computador, copie cada ficheiro de base de dados para a localização do perfil de utilizador adequada.  

### <a name="user-state-migration-data"></a>Dados de migração de estado de utilizador
Como parte das propriedades do sistema de sites do ponto de migração de estado, deve especificar as pastas que armazenam dados de migração de estado de utilizador. Depois de recuperar um servidor com uma pasta que armazena dados de migração de perfil do usuário, restaure manualmente os dados de migração de estado do utilizador no servidor para a mesma pasta que armazenava os dados antes da falha.

### <a name="regenerate-the-certificates-for-distribution-points"></a>Gerar novamente os certificados para pontos de distribuição
Depois de restaurar um site, o **distmgr** pode conter a seguinte entrada para um ou mais pontos de distribuição: `Failed to decrypt cert PFX data`. Esta entrada indica que os dados de certificado de ponto de distribuição não podem ser desencriptados pelo site. Para resolver este problema, voltar a gerar ou importe novamente o certificado para pontos de distribuição afetados. Utilize o [Set-CMDistributionPoint](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmdistributionpoint) cmdlet do PowerShell.

### <a name="update-certificates-used-for-cloud-based-distribution-points"></a>Atualizar certificados utilizados para pontos de distribuição baseado na nuvem
O Configuration Manager requer um certificado de gestão do Azure para o servidor do site comunicar com pontos de distribuição baseado na nuvem. Após uma recuperação de site, atualize os certificados para pontos de distribuição baseado na nuvem.



## <a name="recover-a-secondary-site"></a>Recuperar um site secundário
O Configuration Manager não suporta a cópia de segurança da base de dados num site secundário, mas suporta a recuperação através da reinstalação do site secundário. Recuperação de site secundário é necessária quando ocorre uma falha de um site secundário do Configuration Manager.

### <a name="requirements"></a>Requisitos
- O servidor tem de cumprir todos os pré-requisitos de site secundário e ter segurança adequados direitos configurados.  

- Utilize o mesmo caminho de instalação que foi utilizado para o site que falhou.  

- Utilize um servidor com a mesma configuração no servidor com falha. Esta configuração inclui o respetivo nome de domínio completamente qualificado (FQDN).  

- O servidor tem de ter a mesma configuração do SQL Server como o site que falhou.  

     - Durante uma recuperação de site secundário do Configuration Manager não instalar o SQL Server Express se ainda não estiver instalado no computador.  

     - Utilize a mesma versão do SQL Server e a mesma instância do SQL Server que utilizou para a base de dados do site secundário antes da falha.  

### <a name="procedure"></a>Procedimento
Para recuperar um site secundário, utilize o **recuperar Site secundário** ação por parte da **Sites** nó na consola do Configuration Manager. Ao contrário da recuperação de um site de administração central ou site primário, a recuperação de um site secundário não utiliza um ficheiro de cópia de segurança. Este processo reinstala os ficheiros do site secundário no servidor do site secundário que falhou. Depois do site reinstala, os dados de site secundário são reinicializados com dados do site primário principal.

Durante o processo de recuperação, o Configuration Manager verifica se a biblioteca de conteúdos existe no servidor do site secundário e que o conteúdo apropriado está disponível. O site secundário utiliza a biblioteca de conteúdos existente, se este contiver o conteúdo apropriado. Caso contrário, a recuperação da biblioteca de conteúdos de um site secundário recuperado requer a redistribuição ou pré-configuração do conteúdo para esse site recuperado.

Quando tiver um ponto de distribuição que não está no servidor do site secundário, não são necessários para reinstalar o ponto de distribuição durante uma recuperação do site secundário. Após a recuperação do site secundário, o site sincroniza automaticamente com o ponto de distribuição.

Pode verificar o estado da recuperação de site secundário utilizando a **Mostrar estado da instalação** ação a partir do **Sites** nó na consola do Configuration Manager.
