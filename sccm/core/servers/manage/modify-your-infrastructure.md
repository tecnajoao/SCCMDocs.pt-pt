---
title: Modificar a infraestrutura
titleSuffix: Configuration Manager
description: Saiba como efetuar alterações nem executar ações que afetam a infraestrutura do Configuration Manager que implementou.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a7975dc8-46ab-4dae-86b6-dc3e3cf3b2f0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0b65f5fb8790f907699a26e36c1ffe41b7e0eb03
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53418650"
---
# <a name="modify-your-system-center-configuration-manager-infrastructure"></a>Modificar a infraestrutura do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Depois de instalar um ou mais sites, poderá ser necessário modificar configurações ou executar ações que afetam a infraestrutura implementada.  


##  <a name="BKMK_ManageSMSprovider"></a> Gerir o fornecedor SMS  
 O fornecedor de SMS (um ficheiro de biblioteca de ligação dinâmica: smsprov) fornece o ponto de contacto administrativo para uma ou mais consolas do Configuration Manager. Ao instalar múltiplos Fornecedores de SMS, poderá fornecer redundância de pontos de contacto, ao administrar o site e a hierarquia.  

 Em cada site do Configuration Manager, pode voltar a executar a configuração para:  

- Adicionar uma instância adicional do fornecedor de SMS (cada instância adicional do fornecedor de SMS tem de ser num computador separado)  

- Remover uma instância do fornecedor de SMS (para remover o último fornecedor de SMS de um site, tem de desinstalar o site)  

  Pode monitorizar a instalação ou remoção do Fornecedor de SMS, visualizando o **ConfigMgrSetup.log** na pasta raiz do servidor de site onde executa a Configuração.  

  Antes de modificar o Fornecedor de SMS num site, deve estar familiarizado com as informações em [Planear o Fornecedor de SMS para o System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

#### <a name="to-manage-the-sms-provider-configuration-for-a-site"></a>Para gerir a configuração do Fornecedor de SMS num site  

1. Execute **configuração do Configuration Manager** partir  **&lt;pasta de instalação de site do Configuration Manager\>\BIN\X64\setup.exe**.  

2. Na página **Introdução**, selecione **Executar a manutenção do site ou repor este site** e clique em **Seguinte**.  

3. Na página **Manutenção do Site**, selecione **Modificar a configuração do Fornecedor de SMS** e clique em **Seguinte**.  

4. Na página **Gerir Fornecedores de SMS**, selecione uma das seguintes opções e conclua o assistente através de uma das duas opções seguintes:  

   -   Para adicionar um Fornecedor de SMS adicional a este site:  

        Selecione **Adicionar um novo Fornecedor de SMS**, especifique o FQDN de um computador que irá alojar o Fornecedor de SMS, e que não aloje nenhum atualmente, e clique em **Seguinte**.  

   -   Para remover um Fornecedor de SMS de um servidor:  

        Selecione **Desinstalar o Fornecedor de SMS especificado**, selecione o nome do computador do qual pretende remover o Fornecedor de SMS, clique em **Seguinte** e confirme a ação.  

       > [!TIP]  
       >  Para mover o Fornecedor de SMS entre dois computadores, tem de instalar o Fornecedor de SMS no novo computador e remover o Fornecedor de SMS da localização original. Não existe uma opção dedicada para mover o Fornecedor de SMS entre computadores num único processo.  

   Depois da conclusão do Assistente de Configuração, a configuração do Fornecedor de SMS está concluída. No separador **Geral**, na caixa de diálogo **Propriedades** do site, pode verificar os computadores que têm um Fornecedor de SMS instalado para um site.  

##  <a name="bkmk_Console"></a> Gerir a consola do Configuration Manager  
 Seguem-se tarefas que pode realizar para gerir a consola do Configuration Manager:  

-   **Modificar o idioma que é apresentado na consola do Configuration Manager** - para modificar os idiomas instalados, consulte [idioma da consola do Configuration Manager/gerir](#BKMK_ManageConsoleLanguages) neste tópico.  

-   **Instalar consolas adicionais** - para instalar consolas adicionais, consulte [consolas de instalar o System Center Configuration Manager](/sccm/core/servers/deploy/install/install-consoles).  

-   **Configurar DCOM** - para configurar as permissões de DCOM para ativar as consolas que são remotas a partir do servidor do site para ligar, veja [configurar permissões de DCOM para consolas remotas do Configuration Manager](#BKMK_ConfigDCOMforRemoteConsole) neste tópico.  

-   **Modificar permissões para limitar o que os utilizadores administrativos podem ver na consola do** - para modificar as permissões administrativas, limitando o que os utilizadores podem ver e fazer na consola, consulte [modificar o âmbito administrativo de um utilizador administrativo ](/sccm/core/servers/deploy/configure/configure-role-based-administration#BKMK_ModAdminUser).     

###  <a name="BKMK_ManageConsoleLanguages"></a> Gerir o idioma da consola do Configuration Manager  
 Durante a instalação de servidor do site, os ficheiros de instalação de consola do Configuration Manager e os pacotes de idiomas suportados para o site são copiados para o  **&lt;Caminhodeinstalaçãodoconfigmgr\>\tools\consolesetup.** subpasta no servidor do site.  

-   Quando inicia a instalação da consola do Configuration Manager a partir desta pasta no servidor do site, a consola do Configuration Manager e os ficheiros do pacote de idiomas suportados são copiados para o computador  

-   Quando um pacote de idiomas está disponível para a definição de idioma atual no computador, a consola do Configuration Manager será aberta nesse idioma  

-   Se o pacote de idiomas associado não está disponível para a consola do Configuration Manager, a consola será aberta em inglês  

Por exemplo, considere um cenário em que instalar consola do Configuration Manager a partir de um servidor de site que suporte inglês, alemão e francês. Se abrir a consola do Configuration Manager num computador com uma definição de idioma configurada de francês, a consola será aberta em francês. Se abrir a consola do Configuration Manager num computador com idioma configurada como japonês, a consola será aberta em inglês, porque o pacote de idiomas de japonês não está disponível.  

 Sempre que abre a consola do Configuration Manager, ele determina as definições de idioma configurada para o computador, verifica se um pacote de idiomas associado está disponível para a consola do Configuration Manager e, em seguida, abre a consola utilizando o pacote de idiomas apropriado. Quando deseja abrir a consola do Configuration Manager em inglês, independentemente de definições de idioma configuradas no computador, tem manualmente de remover ou renomear os arquivos do pacote de idiomas no computador.  

 Utilize os procedimentos seguintes para iniciar a consola do Configuration Manager em inglês, independentemente da definição de região configurada no computador.  

##### <a name="to-install-an-english-only-version-of-the-configuration-manager-console-on-computers"></a>Para instalar uma versão apenas em inglês da consola do Configuration Manager em computadores  

1.  No Explorador do Windows, navegue para  **&lt;Caminhodeinstalaçãodoconfigmgr\>\tools\consolesetup\languagepack.**  

2.  Mude o nome dos ficheiros **.msp** e **.mst**. Por exemplo, pode alterar **&lt;nome do ficheiro\>.MSP** para **&lt;nome do ficheiro\>.MSP.disabled**.  

3.  Instale a consola do Configuration Manager no computador.  

    > [!IMPORTANT]  
    >  Quando são configurados novos idiomas de servidor para o servidor do site, os arquivos. msp e. mst são novamente copiados para o **LanguagePack** pasta e terá de repetir este procedimento para instalar novas consolas do Configuration Manager apenas em inglês.  

##### <a name="to-temporarily-disable-a-console-language-on-an-existing-configuration-manager-console-installation"></a>Para desativar temporariamente um idioma de consola numa instalação existente de consola do Configuration Manager  

1.  No computador que está a executar a consola do Configuration Manager, feche a consola do Configuration Manager.  

2.  No Explorador do Windows, navegue para &lt; *ConsoleInstallationPath*> \Bin\ no computador da consola do Configuration Manager.  

3.  Mude o nome da pasta de idiomas apropriada para o idioma que se encontra configurado no computador. Por exemplo, se as definições de idioma do computador tiverem sido definidas para alemão, poderá mudar o nome da pasta **de** para **de.disabled**.  

4.  Para abrir a consola do Configuration Manager no idioma que está configurado para o computador, renomeie a pasta para o nome original. Por exemplo, mude o nome **de.disabled** para **de**.  

##  <a name="BKMK_ConfigDCOMforRemoteConsole"></a> Configurar permissões de DCOM para consolas remotas do Configuration Manager  
 A conta de utilizador que executa a consola do Configuration Manager requer permissão para aceder à base de dados do site utilizando o fornecedor de SMS. No entanto, um utilizador administrativo que utilize uma consola remota do Gestor de configuração também requer **ativação remota** permissões de DCOM em:  

- O computador do servidor do site  

- Cada computador que aloja uma instância do Fornecedor de SMS  

  O grupo de segurança com o nome **Admins de SMS** concede acesso ao Fornecedor de SMS num computador e também pode ser utilizado para conceder as permissões de DCOM necessárias. (Este grupo é local no computador quando o fornecedor de SMS é executado num servidor membro e é um grupo local de domínio quando o fornecedor de SMS é executado num controlador de domínio.)  

> [!IMPORTANT]  
>  Consola do Configuration Manager utiliza Windows Management Instrumentation (WMI) para ligar ao fornecedor de SMS e a WMI utiliza o DCOM internamente. Por conseguinte, o Configuration Manager requer permissões para ativar um servidor DCOM no computador do fornecedor de SMS se a consola do Configuration Manager está em execução num computador diferente do computador do fornecedor de SMS. Por predefinição, a ativação remota é concedida apenas aos membros do grupo Administradores incorporado. Se permitir que o grupo Admins de SMS tenha a permissão Ativação Remota, um membro deste grupo pode tentar ataques DCOM contra o computador do Fornecedor de SMS. Esta configuração também aumenta a superfície de ataque do computador. Para atenuar esta ameaça, monitorize cuidadosamente os membros do grupo Admins de SMS.  

 Utilize o procedimento seguinte para configurar cada site de administração central, servidor de site primário e cada computador onde está instalado o fornecedor de SMS para conceder acesso à consola para os utilizadores administrativos a remoto do Configuration Manager.  

#### <a name="to-configure-dcom-permissions-for-remote-configuration-manager-console-connections"></a>Para configurar permissões de DCOM para ligações de consolas remotas do Configuration Manager  

1. Abra **Serviços de Componentes**, executando **Dcomcnfg.exe**.  

2. Na **serviços de componentes**, clique em **raiz da consola** >  **serviços de componentes** > **computadores**e, em seguida, Clique em **meu computador**. No menu **Ação**, clique em **Propriedades**.  

3. Na caixa de diálogo **Propriedades de O Meu Computador**, na secção **Permissões de Lançamento e Ativação** do separador **Segurança COM**, clique em **Editar Limites**.  

4. Na caixa de diálogo **Permissões de Lançamento e Ativação**, clique em **Adicionar**.  

5. Na **selecionar utilizadores, computadores, contas de serviço ou grupos** caixa de diálogo a **introduzir os nomes de objeto a selecionar (exemplos)** , escreva **Admins de SMS**e, em seguida, clique em  **OK**.  

   > [!NOTE]  
   >  Poderá ter de alterar a definição **Desta localização** para localizar o grupo Admins de SMS. Este grupo é local no computador quando o Fornecedor de SMS é executado num servidor membro e é um grupo local do domínio quando o Fornecedor de SMS é executado num controlador de domínio.  

6. Na secção **Permissões para Admins de SMS**, para permitir a ativação remota, selecione a caixa de verificação **Ativação Remota**.  

7. Clique em **OK** e clique novamente em **OK** e, em seguida, feche **Gestão de Computadores**. O computador está agora configurado para permitir o acesso à consola para membros do grupo Admins de SMS remoto do Configuration Manager.  

   Repita este procedimento em cada computador fornecedor de SMS que possa suportar consolas remotas do Configuration Manager.  

##  <a name="bkmk_dbconfig"></a> Modificar a configuração de base de dados do site  
 Após instalar um site, poderá modificar a configuração de base de dados do site e o servidor da base de dados do site executando o Programa de Configuração num servidor de site de administração central ou servidor de site primário. Pode mover a base de dados do site para uma nova instância do SQL Server no mesmo computador, ou para outro computador que execute uma versão suportada do SQL Server. Estas e as alterações relacionadas não são suportadas para a configuração da base de dados em sites secundários.  

 Para obter mais informações sobre os limites do suporte, veja [Política de suporte para alterações manuais da base de dados num ambiente do Configuration Manager](https://support.microsoft.com/kb/3106512).  

> [!NOTE]  
>  Ao modificar a configuração de base de dados para um site, o Configuration Manager será reiniciado e reinstalará os serviços do Configuration Manager no servidor de site e servidores do sistema de sites remotos que comunicam com a base de dados.  

**Para alterar a configuração da base de dados**, terá de executar a Configuração no servidor do site e selecionar a opção **Executar a manutenção do site ou repor este site**. Em seguida, selecione a opção **Modificar a configuração do SQL Server**. Pode alterar as seguintes configurações de bases de dados do site:  

-   O servidor baseado em Windows que aloja a base de dados.  

-   A instância do SQL Server utilizada num servidor que aloja a base de dados do SQL Server.  

-   O nome da base de dados.  

-   Porta do SQL Server em utilização pelo Configuration Manager  

-   Porta do SQL Server Service Broker utilizado pelo Configuration Manager  

**Se mover a base de dados do site, tem de configurar o seguinte:**  

-   **Configure o acesso:** Ao mover a base de dados do site para um novo computador, adicione a conta de computador do servidor do site para o **administradores locais** grupo no computador que executa o SQL Server. Se utilizar um cluster do SQL Server para a base de dados do site, terá de adicionar a conta de computador ao grupo **Administradores Locais** de cada computador com nós de cluster do Windows Server.  

-   **Ative a integração do common language runtime (CLR):**  Ao mover a base de dados para uma nova instância do SQL Server ou para um novo computador do SQL Server, tem de ativar integração common language runtime (CLR). Para ativar o CLR, utilize **SQL Server Management Studio** para ligar à instância do SQL Server que aloja a base de dados do site e execute o seguinte procedimento armazenado como uma consulta: **sp_configure 'clr enabled', 1; reconfigure**.  
-  **Certifique-se de que o novo SQL Server tem acesso para a localização de cópia de segurança:** Quando utiliza um UNC para armazenar a cópia de segurança de base de dados do site, depois de mover a base de dados para um novo servidor, incluindo uma mudança de um grupo de Disponibilidade AlwaysOn do SQL Server ou para um cluster do SQL Server, certifique-se a conta de computador do novo SQL Server tem **escrever**permissões para a localização UNC.  


> [!IMPORTANT]  
>  Antes de mover uma base de dados que tenha uma ou mais réplicas de base de dados para pontos de gestão, necessitará primeiro de remover as réplicas de base de dados. Após concluir a mudança da base de dados, poderá reconfigurar as réplicas de base de dados. Para obter mais informações, veja [Réplicas de bases de dados para pontos de gestão do System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

##  <a name="bkmk_SPN"></a> Gerir o SPN para o servidor de base de dados do site  
Pode selecionar a conta que executa o SQL Services para a base de dados do site:  

-   Quando os serviços são executados com a conta de sistema de computadores, o SPN é registado automaticamente para si.  

-   Quando os serviços são executados com uma conta de utilizador local de domínio, tem de registar manualmente o SPN para garantir que os clientes de SQL e outro sistema de sites podem executar a autenticação Kerberos. Sem autenticação Kerberos, a comunicação com a base de dados poderá falhar.  

A documentação do SQL Server pode ajudá-lo a [registar manualmente o SPN](https://technet.microsoft.com/library/ms191153\(v=sql.120\).aspx) e fornecer informações adicionais sobre SPNs e ligações Kerberos.  

> [!IMPORTANT]
> - Ao criar um SPN para um SQL Server em cluster, deverá especificar o nome virtual do Cluster do SQL Server como o nome de computador do SQL Server  
>   -   O comando para registar um SPN para uma instância nomeada do SQL Server é igual ao utilizado para registar um SPN para uma instância predefinida, com exceção do facto de o número de porta ter de corresponder à porta que é utilizada pela instância nomeada  

Pode registar um SPN para a conta de serviço do SQL Server do servidor de base de dados do site através da ferramenta **Setspn**. Deverá executar a ferramenta Setspn num computador que resida no domínio do SQL Server, a qual deverá utilizar credenciais de Administrador de Domínio ao ser executada.  

 Utilize os seguintes procedimentos como exemplos de como gerir o SPN para a conta de serviço do SQL Server que utiliza a ferramenta Setspn no Windows Server 2008 R2. Para obter instruções específicas sobre o Setspn, veja [Descrição Geral do Setspn](http://go.microsoft.com/fwlink/p/?LinkId=226343) ou outra documentação semelhante, específica do seu sistema operativo.  

> [!NOTE]  
>  Os seguintes procedimentos fazem referência a ferramenta de linha de comandos Setspn. A ferramenta de linha de comandos Setspn está incluída na instalação ferramentas de suporte do Windows Server 2003 para a partir do CD de produto ou a partir da [Microsoft Download Center](http://go.microsoft.com/fwlink/p/?LinkId=100114). Para obter mais informações sobre como instalar as Ferramentas de Suporte do Windows a partir do CD de produto, veja [Instalar as Ferramentas de Suporte do Windows](http://go.microsoft.com/fwlink/p/?LinkId=62270).  

#### <a name="to-manually-create-a-domain-user-service-principal-name-spn-for-the-sql-server-service-account"></a>Para criar manualmente um utilizador de domínio nome Principal de serviço (SPN) para a conta de serviço do SQL Server  

1.  No menu **Início**, clique em **Executar** e, em seguida, introduza **cmd** na caixa de diálogo Executar.  

2.  Na linha de comandos, navegue para o diretório de instalação das ferramentas de suporte do Windows Server. Por predefinição, estas ferramentas estão localizadas no **C:\Program Files\Support Tools** diretório.  

3.  Introduza um comando válido para criar o SPN. Para criar o SPN, pode utilizar o nome NetBIOS ou o nome de domínio completamente qualificado (FQDN) do computador a executar o SQL Server. No entanto, precisará de criar um SPN tanto para o nome NetBIOS como para o FQDN.  

    > [!IMPORTANT]  
    >  Ao criar um SPN para um SQL Server em cluster, deverá especificar o nome virtual do Cluster do SQL Server como o nome de computador do SQL Server.  

    -   Para criar um SPN para o nome NetBIOS do computador do SQL Server, escreva o seguinte comando: **setspn - A MSSQLSvc /&lt;nome de computador do SQL Server\>: 1433 &lt;domínio \ conta >**  

    -   Para criar um SPN para o FQDN do computador do SQL Server, escreva o seguinte comando: **setspn - A MSSQLSvc /&lt;FQDN do SQL Server\>: 1433 &lt;domínio \ conta >**  

    > [!NOTE]  
    >  O comando para registar um SPN para uma instância nomeada do SQL Server é igual ao utilizado para registar um SPN para uma instância predefinida, com exceção do fato de o número de porta ter de corresponder à porta que é utilizada pela instância nomeada.  

#### <a name="to-verify-the-domain-user-spn-is-registered-correctly-by-using-the-setspn-command"></a>Para verificar se o SPN do utilizador de domínio está corretamente registado utilizando o comando Setspn  

1.  No menu **Início**, clique em **Executar** e, em seguida, introduza **cmd** na caixa de diálogo **Executar**.  

2.  Na linha de comandos, introduza o seguinte comando: **setspn -L &lt;domínio \ conta do serviço SQL >**.  

3.  Reveja o **ServicePrincipalName** registado para certificar-se de que foi criado um SPN válido para o SQL Server.  

#### <a name="to-verify-the-domain-user-spn-is-registered-correctly-when-using-the-adsiedit-mmc-console"></a>Para verificar se o SPN do utilizador de domínio está corretamente registado utilizando a consola ADSIEdit do MMC  

1.  No menu **Início**, clique em **Executar** e, em seguida, introduza **adsiedit.msc** para iniciar a consola ADSIEdit do MMC.  

2.  Se necessário, ligue estabeleça a ligação ao domínio do servidor do site.  

3.  No painel da consola, expanda o domínio do servidor de site, expanda **DC =&lt;nome único do servidor\>**, expanda **CN = Users**, clique com botão direito **CN =&lt;Utilizador da conta de serviço\>** e, em seguida, clique em **propriedades**.  

4.  No **CN =&lt;utilizador da conta de serviço\> propriedades** caixa de diálogo, reveja o **servicePrincipalName** valor para se certificar de que um SPN válido foi criado e associado a computador correto do SQL Server.  

#### <a name="to-change-the-sql-server-service-account-from-local-system-to-a-domain-user-account"></a>Para alterar a conta de serviço do SQL Server de sistema local para uma conta de utilizador de domínio  

1.  Crie ou selecione a conta de utilizador de domínio ou de sistema local que pretende utilizar como a conta de serviço do SQL Server.  

2.  Abra o **Gestor de Configuração do SQL Server**.  

3.  Clique em **SQL Server Services**e, em seguida, faça duplo clique em **do SQL Server&lt;nome da instância\>**.  

4.  No separador **Início de sessão**, selecione **Esta conta** e, em seguida, introduza o nome de utilizador e a palavra-passe da conta de utilizador de domínio criada no passo 1, ou clique em **Procurar** para localizar a conta de utilizador nos Serviços de Domínio do Active Directory e, em seguida, clique em **Aplicar**.  

5.  Clique em **Sim** na caixa de diálogo **Confirmar Alteração da Conta** para confirmar a alteração da conta de serviço e reiniciar o serviço do SQL Server.  

6.  Clique em **OK** após a alteração com êxito da conta de serviço.  

##  <a name="bkmk_reset"></a> Executar uma reposição do site  
 Quando uma reposição do site é executada num site de administração central ou site primário, o site:  

-   Volta a aplicar as permissões de arquivo e registro de Configuration Manager do padrão  

-   Reinstala todos os componentes do site e todas as funções de sistema de site no site  

Os sites secundários não suportam uma reposição de site.  

As reposições do site podem ser executadas manualmente, quando assim o decidir, mas também podem ser executadas automaticamente depois de modificar a configuração do site.  

Por exemplo, se tiver ocorrido uma alteração às contas utilizadas por componentes do Configuration Manager, deve considerar uma reposição para garantir que os componentes do site são atualizados para utilizarem os novos detalhes de conta manual do site. No entanto, se modificar os idiomas de cliente ou servidor num site, o Configuration Manager executa automaticamente um reposição do site devido a reposição é necessária um site pode utilizar esta alteração.  

> [!NOTE]  
>  Uma reposição do site não repor permissões de acesso não - objetos do Configuration Manager.  

Quando uma reposição do site é executada:  

1.  Configuração interrompe e reinicia o **SMS_SITE_COMPONENT_MANAGER** serviço e os componentes de thread a **SMS_EXECUTIVE** serviço.  

2.  A configuração remove e, em seguida, recria o sistema de sites partilha, pasta e o **SMS Executive** componente no computador local e em computadores de sistema de sites remotos.  

3.  Configuração reinicia o **SMS_SITE_COMPONENT_MANAGER** serviço, este serviço instala os **SMS_EXECUTIVE** e o **SMS_SQL_MONITOR** serviços.  

Além disso, uma reposição do site restaura os seguintes objetos:  

-   As chaves de registo **SMS** ou **NAL**, bem como outras subchaves predefinidas sob destas chaves.  

-   Na árvore de diretórios do ficheiro de Configuration Manager e quaisquer arquivos padrão ou subdiretórios dessa árvore de diretório do ficheiro.  

**Pré-requisitos para executar uma reposição do site**  

A conta utilizada para efetuar uma reposição do site tem de ter as seguintes permissões:  

-   A conta utilizada para efetuar uma reposição do site tem de ter as seguintes permissões:  

    -   **Site de administração central**: A conta que utilizar para executar uma reposição do site tem de ser um administrador local no servidor do site de administração central e deve possuir privilégios equivalentes da **administrador total** administração baseada em funções função de segurança.  

    -   **Site primário**: A conta que utilizar para executar uma reposição do site tem de ser um administrador local no servidor do site primário e deve possuir privilégios equivalentes da **administrador total** função de segurança da administração baseada em funções. Se o site primário estiver numa hierarquia com um site de administração central, esta conta também deverá ser um administrador local no servidor do site de administração central.  

**Limitações para uma reposição do site**
  - A partir da versão 1602, não é possível utilizar uma reposição para alterar o servidor do site ou pacotes de idiomas de cliente, que é instalado em sites, desde que a hierarquia está configurada para suportar [testar as atualizações de cliente numa coleção de pré-produção](/sccm/core/clients/manage/upgrade/test-client-upgrades).

#### <a name="to-perform-a-site-reset"></a>Para efetuar uma reposição do site  

1.  Execute **configuração do Configuration Manager** partir  **&lt;pasta de instalação de site do Configuration Manager\>\BIN\X64\setup.exe**.  

    > [!TIP]  
    >  Também pode executar um reposição do site ao iniciar a configuração do Configuration Manager nos **iniciar** menu do computador do servidor do site ou a partir do suporte de dados de origem do Configuration Manager.  

2.  Na página **Introdução** , selecione **Executar a manutenção do site ou repor este site**e clique em **Seguinte**.  

3.  Na página **Manutenção do Site**, selecione **Repor o site sem alterações de configuração** e clique em **Seguinte**.  

4.  Clique em **Sim** para iniciar a reposição do site.  

Quando a reposição do site estiver concluída, clique em **Fechar** para concluir este procedimento.  

##  <a name="bkmk_sitelang"></a> Gerir pacotes de idiomas num site  
Após a instalação de um site, pode alterar os pacotes de idioma de servidor e cliente que estão em utilização:  

**Pacotes de idiomas de servidor:**  

-   **Aplica-se a:**  

     Instalações da consola do Configuration Manager  

     Novas instalações de funções do sistema de sites aplicáveis  

-   **Detalhes:**  

     Depois de atualizar os pacotes de idiomas de servidor num site, pode adicionar suporte para os pacotes de idiomas para consolas do Configuration Manager.  

     Para adicionar suporte para um pacote de idiomas de servidor a uma consola do Configuration Manager, tem de instalar a consola do Configuration Manager a partir da **ConsoleSetup** pasta num servidor do site que inclua o pacote de idiomas que pretende utilizar. Se já estiver instalada a consola do Configuration Manager, tem primeiro de desinstalar para permitir a instalação de novo identificar a lista atual de pacotes de idiomas suportados.  

**Pacotes de idiomas de cliente:**  

-   **Aplica-se a:**  

     As alterações de pacotes de idiomas de cliente atualizam os ficheiros de origem da instalação do cliente para que as novas instalações e atualizações do cliente adicionem suporte à lista atualizada de idiomas do cliente.  

-   **Detalhes:**  

     Após atualizar os pacotes de idiomas de cliente num site, instale cada cliente que utilizará os pacotes de idiomas utilizando os ficheiros de origem que incluem os pacotes de idiomas de cliente.  

Para obter informações sobre os idiomas de cliente e servidor que são suportadas pelo Configuration Manager, consulte [pacotes de idiomas no System Center Configuration Manager](../../../core/servers/deploy/install/language-packs.md)  

#### <a name="to-modify-the-language-packs-that-are-supported-at-a-site"></a>Para modificar os pacotes de idiomas suportados num site  

1.  No servidor do site, execute a configuração do Configuration Manager partir  **&lt;pasta de instalação de site do Configuration Manager\>\BIN\X64\setup.exe.**  

2.  Na página **Introdução**, selecione **Executar a manutenção do site ou repor este site** e clique em **Seguinte**.  

3.  Na página **Manutenção do Site**, selecione **Modificar a configuração do idioma** e clique em **Seguinte**.  

4.  Na página **Transferências de Pré-requisitos**, selecione **Transferir ficheiros necessários** para adquirir atualizações de pacotes de idiomas ou selecione **Utilizar ficheiros anteriormente transferidos** para utilizar ficheiros transferidos anteriormente que incluem os pacotes de idiomas que pretende adicionar ao site. Clique em **Seguinte** para validar os ficheiros e continuar.  

5.  Na página **Seleção do Idioma do Servidor**, selecione a caixa de verificação dos idiomas do servidor suportados por este site e clique em **Seguinte**.  

6.  Na página **Seleção de Idioma do Cliente**, selecione a caixa de verificação dos idiomas do cliente suportados por este site e clique em **Seguinte**.  

7.  Clique em **Seguinte** para modificar o suporte de idiomas no site.  

    > [!NOTE]  
    >  Inicia de Gestor de configuração uma reposição do site que também reinstala todas as funções de sistema de sites no site.  

8.  Clique em **Fechar** para concluir este procedimento.  

##  <a name="BKMK_ModDBAlert"></a> Modifique o limiar de alerta de servidor de base de dados  
 Por predefinição, o Configuration Manager gera alertas quando o espaço livre em disco num servidor de base de dados do site está baixo. As predefinições estão definidas para emitir um aviso quando existirem 10 GB ou menos de espaço livre em disco e um alerta crítico quando existirem menos de 5 GB de espaço livre em disco. Pode modificar estes valores ou desativar os alertas para cada site.  

 Para alterar estas definições:  

1.  Na área de trabalho **Administração** , expanda **Configuração do Site**e clique em **Sites**.  

2.  Selecione o site que pretende configurar e abra desse site **propriedades**.  

3.  Do site **propriedades** caixa de diálogo, selecione a **alerta** separador e, em seguida, edite as definições.  

4.  Clique em **OK** para fechar a caixa de diálogo de propriedades do site.  
