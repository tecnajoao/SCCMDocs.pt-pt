---
title: "Configurar o relatório | Microsoft Docs"
description: "Leia sobre como configurar o relatório em sua hierarquia do Configuration Manager, incluindo informações sobre o SQL Server Reporting Services."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 55ae86a7-f0ab-4c09-b4da-89cd0e7fa0e0
caps.latest.revision: 6
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: f62d969dd49fb00b688602128df74b28ff551135
ms.openlocfilehash: 7ae6bac23e585d6f61aff0f3155d050f1b537620
ms.contentlocale: pt-pt
ms.lasthandoff: 06/07/2017


---
# <a name="configuring-reporting-in-system-center-configuration-manager"></a>Configurar relatórios no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

Antes de criar, modificar e executar relatórios no console do System Center Configuration Manager, você deve executar várias tarefas de configuração. Use as seções a seguir neste tópico para ajudá-lo a configurar o relatório em sua hierarquia do Configuration Manager:  

 Antes de prosseguir com a instalação e configuração do Reporting Services em sua hierarquia, revise o Gerenciador de configuração seguintes tópicos do relatório:  

-   [Introdução à emissão de relatórios no System Center Configuration Manager](../../../core/servers/manage/introduction-to-reporting.md)  

-   [Planejamento para emissão de relatórios no System Center Configuration Manager](../../../core/servers/manage/planning-for-reporting.md)  

##  <a name="BKMK_SQLReportingServices"></a> Serviços de Relatórios do SQL Server  
 O SQL Server Reporting Services é uma plataforma de relatórios baseada em servidor que fornece funcionalidade de relatórios completa para diversas origens de dados. O ponto do reporting services no Configuration Manager se comunica com o SQL Server Reporting Services para copiar relatórios do Configuration Manager para uma pasta de relatório especificado, para definir as configurações do Reporting Services e definir as configurações de segurança do Reporting Services. Reporting Services se conecta ao banco de dados de site do Configuration Manager para recuperar os dados que são retornados ao executar relatórios.  

 Antes de instalar o ponto do reporting services em um site do Configuration Manager, você deve instalar e configurar o SQL Server Reporting Services no sistema de site que hospeda a função de sistema de site do reporting services ponto. Para obter informações sobre a instalação do Reporting Services, consulte a [Biblioteca TechNet do SQL Server](http://go.microsoft.com/fwlink/p/?LinkId=266389).  

 Utilize o procedimento seguinte para verificar se o SQL Server Reporting Services está instalado e em execução sem problemas.  

#### <a name="to-verify-that-sql-server-reporting-services-is-installed-and-running"></a>Para verificar se o SQL Server Reporting Services está instalado e em execução  

1.  No ambiente de trabalho, clique em **Iniciar**, clique em **Todos os Programas**, clique em **Microsoft SQL Server 2008 R2**, clique em **Ferramentas de Configuração**e, em seguida, clique **Gestor de Configuração do Reporting Services**.  

2.  Na caixa de diálogo **Ligação de Configuração do Reporting Services** , especifique o nome do servidor que aloja o SQL Server Reporting Services, no menu, selecione a instância do SQL Server em que instalou o SQL Reporting Services e clique em **Ligar**. É aberto o Gestor de Configuração do Reporting Services.  

3.  Na página **Estado do Servidor de Relatórios** , verifique se **Estado do Serviço de Relatórios** está definido como **Iniciado**. Se não for, clique em **Iniciar**.  

4.  Na página **URL do Serviço Web** , clique no URL em **URLs do Serviço Web do Serviço de Relatórios** para testar a ligação à pasta de relatórios. A caixa de diálogo **Segurança do Windows** poderá abrir e solicitar credenciais de segurança. Por predefinição, é apresentada a sua conta de utilizador. Introduza a palavra-passe e clique em **OK**. Certifique-se de que a página Web é aberta com êxito. Feche a janela do browser.  

5.  Na página **Base de Dados** , verifique se **Modo do Servidor de Relatórios** está definido como **Nativo**.  

6.  Na página **URL do Gestor de Relatórios** , clique no URL em **Identificação de Sites do Gestor de Relatórios** para testar a ligação ao diretório virtual do Gestor de Relatórios. A caixa de diálogo **Segurança do Windows** poderá abrir e solicitar credenciais de segurança. Por predefinição, é apresentada a sua conta de utilizador. Introduza a palavra-passe e clique em **OK**. Certifique-se de que a página Web é aberta com êxito. Feche a janela do browser.  

    > [!NOTE]  
    >  Gerenciador de relatórios do Reporting Services não é exigido para gerar relatórios no Configuration Manager, mas é necessário se você quiser executar relatórios em um navegador da Internet ou gerenciar relatórios usando o Gerenciador de relatórios.  

7.  Clique em **saída** para fechar o Reporting Services Configuration Manager.  

##  <a name="BKMK_ReportBuilder3"></a> Configurar relatórios para utilizar o Report Builder 3.0  

#### <a name="to-change-the-report-builder-manifest-name-to-report-builder-30"></a>Para alterar o nome do manifesto do Report Builder para Report Builder 3.0  

1.  No computador que executa o console do Configuration Manager, abra o Editor de registro do Windows.  

2.  Navegue para **HKEY_LOCAL_MACHINE/SOFTWARE/Wow6432Node/Microsoft/ConfigMgr10/AdminUI/Reporting**.  

3.  Faça duplo clique na chave **ReportBuilderApplicationManifestName** para editar os dados do valor.  

4.  Altere **ReportBuilder_2_0_0_0.application** para **ReportBuilder_3_0_0_0.application**e clique em **OK**.  

5.  Feche o Editor de Registo do Windows.  

##  <a name="BKMK_InstallReportingServicesPoint"></a> Instalar um ponto do Reporting Services  
 O ponto do Reporting Services deve ser instalado num site para gerir relatórios nesse site. O ponto do Reporting Services copia pastas de relatórios e relatórios para o SQL Server Reporting Services, aplica a política de segurança aos relatórios e às pastas e configura definições de configuração no Reporting Services. Você deve configurar um ponto do reporting services antes de relatórios são exibidos no console do Configuration Manager e para poder gerenciar os relatórios no Configuration Manager. O ponto do Reporting Services é uma função de sistema de sites que tem de ser configurada num servidor com o Microsoft SQL Server Reporting Services instalado e em execução. Para obter mais informações sobre pré-requisitos, consulte [pré-requisitos para emissão de relatórios](prerequisites-for-reporting.md).  

> [!IMPORTANT]  
>  Quando selecionar um site para instalar o ponto do Reporting Services, tenha em conta que os utilizadores que irão aceder aos relatórios devem estar abrangidos pelo mesmo âmbito de segurança que o site em que o ponto do Reporting Services é instalado.  

> [!NOTE]  
>  Depois de instalar um ponto do Reporting Services num sistema de sites, não altere o URL do servidor de relatórios. Por exemplo, se você criar o ponto do reporting services e, em seguida, no Reporting Services Configuration Manager você modificar a URL do servidor de relatório, o console do Configuration Manager continuará a usar a antiga URL e não será possível executar, editar ou criar relatórios a partir do console. Quando tiver de alterar o URL do servidor de relatórios, remova o ponto do Reporting Services, altere o URL e, em seguida, reinstale o ponto do Reporting Services.  

> [!IMPORTANT]    
> Quando você instala um ponto do reporting services, você deve especificar uma conta de ponto de serviços de relatório. Posteriormente, quando os usuários de um domínio diferente executar um relatório, o relatório não funcionará a menos que haja uma relação de confiança bidirecional estabelecida entre os domínios.

 Utilize o procedimento seguinte para instalar o ponto do Reporting Services.  

#### <a name="to-install-the-reporting-services-point-on-a-site-system"></a>Para instalar o ponto do Reporting Services num sistema de sites  

1.  Na consola do Configuration Manager, clique em **Administração**.  

2.  Na área de trabalho **Administração** , expanda **Configuração do Site**e clique em **Servidores e Funções de Sistema de Sites**.  

    > [!TIP]  
    >  Para listar apenas os sistemas de sites que alojam a função de site do ponto do Reporting Services, clique com o botão direito do rato em **Servidores e Funções de Sistema de Sites** e selecione **Ponto do Reporting Services**.  

3.  Adicione a função de sistema de sites de ponto do Reporting Services a um servidor de sistema de sites novo ou existente utilizando o passo associado:  

    > [!NOTE]  
    >  Para obter mais informações sobre como configurar sistemas de site, consulte [adicionar funções do sistema de site para o System Center Configuration Manager](../deploy/configure/add-site-system-roles.md).  

    -   **Novo sistema de site**: No separador **Home Page**, no grupo **Criar**, clique em **Criar Servidor do Sistema de Sites**. É aberto o **Assistente para Criar Servidor do Sistema de Sites** .  

    -   **Sistema de site existente**: Clique no servidor no qual você deseja instalar a função de sistema de site do reporting services ponto. Quando clica num servidor, é apresentada no painel de resultados uma lista das funções de sistema de sites que já estão instaladas no servidor.  

         No separador **Home Page** , no grupo **Servidor** , clique em **Adicionar Função do Sistema de Sites**. É aberto o **Assistente para Adicionar Funções ao Sistema de Sites** .  

4.  Na página **Geral** , especifique as definições gerais para o servidor de sistema de sites. Quando adicionar o ponto do Reporting Services a um servidor de sistema de sites existente, verifique os valores que foram anteriormente configurados.  

5.  Na página **Seleção da Função do Sistema** , selecione o **Ponto do Reporting Services** na lista de funções disponíveis e clique em **Seguinte**.  

6.  Na página **Ponto do Reporting Services** , configure as seguintes definições:  

    -   **Nome do servidor de banco de dados de site**: Especifique o nome do servidor que hospeda o banco de dados de site do Configuration Manager. Normalmente, o assistente obtém automaticamente o nome de domínio completamente qualificado (FQDN) do servidor. Para especificar uma instância de banco de dados, use o formato &lt; *nome do servidor*>\&lt; *Nome da instância*>.  

    -   **Nome do banco de dados**: Especifique o nome do banco de dados de site do Configuration Manager e, em seguida, clique em **verificar** para confirmar que o assistente tem acesso ao banco de dados do site.  

        > [!IMPORTANT]  
        >  A conta de utilizador que está a criar o ponto do Reporting Services deve ter acesso de **Leitura** à base de dados do site. Se o teste de ligação falhar, é apresentado um ícone de aviso vermelho. Mova o cursor sobre este ícone para ler detalhes da falha. Corrija a falha e, em seguida, clique novamente em **Testar** .  

    -   **Nome da pasta**: Especifique o nome da pasta que é criado e usado para hospedar os relatórios do Configuration Manager no Reporting Services.  

    -   **Instância de servidor do Reporting Services**: Selecione na lista a instância do SQL Server para o Reporting Services. Quando é encontrada apenas uma instância, por predefinição, é listada e selecionada. Quando não forem encontradas instâncias, certifique-se de que o SQL Server Reporting Services está instalado e configurado e de que o serviço SQL Server Reporting Services foi iniciado no sistema de sites.  

        > [!IMPORTANT]  
        >  Gerenciador de configuração faz uma conexão no contexto do usuário atual para o Windows Management Instrumentation (WMI) no sistema de site selecionado para recuperar a instância do SQL Server para o Reporting Services. O utilizador atual tem de ter acesso de **Leitura** à WMI no sistema de sites ou não será possível obter instâncias do Reporting Services.  

    -   **Reporting Services ponto conta**: Clique em **definir**, e, em seguida, selecione uma conta a ser usado ao ponto de serviços do SQL Server Reporting Services em que o relatório se conecta ao banco de dados de site do Configuration Manager para recuperar os dados que são exibidos em um relatório. Selecione **conta existente** para especificar uma conta de usuário do Windows que tenha sido previamente configurada como uma conta do Configuration Manager, ou selecione **nova conta** para especificar uma conta de usuário do Windows que não esteja configurada como uma conta do Configuration Manager. Gerenciador de configuração concede automaticamente o acesso do usuário especificado para o banco de dados do site. O utilizador é apresentado na subpasta **Contas** do nó **Segurança** da área de trabalho **Administração** com o nome de conta **Ponto do Reporting Services do ConfigMgr** .  

         A conta que executa o Reporting Services deve pertencer ao grupo de segurança local **Grupo de Acessos de Autorização do Windows**do domínio e ter a permissão **Ler tokenGroupsGlobalAndUniversal** definida como **Permitir**. Deve haver uma relação de confiança bidirecional estabelecida para usuários de um domínio diferente do que a conta do ponto de Reporting Servicies a execução de relatórios com êxito.

         A conta de utilizador e palavra-passe do Windows especificadas são encriptadas e armazenadas na base de dados do Reporting Services. O Reporting Services obtém os dados para relatórios na base de dados do site utilizando esta conta e palavra-passe.  

        > [!IMPORTANT]  
        >  A conta que especificar deve ter permissões **Iniciar Sessão Localmente** no computador que aloja a base de dados do Reporting Services.  

7.  Na página **Ponto do Reporting Services** , clique em **Seguinte**.  

8.  Na página **Resumo** , verifique as definições e clique em **Seguinte** para instalar o ponto do Reporting Services.  

     Depois que o assistente for concluído, as pastas de relatório são criadas e relatórios do Configuration Manager são copiados para as pastas de relatório especificado.  

    > [!NOTE]  
    >  Quando as pastas de relatório são criadas e relatórios são copiados para o servidor de relatório, o Configuration Manager determina o idioma apropriado para os objetos. Se o pacote de idiomas associado estiver instalado no site, o Configuration Manager cria os objetos no mesmo idioma em que o sistema operacional executado no servidor de relatório no site. Se o idioma não estiver disponível, os relatórios serão criados e apresentados em inglês. Quando instala um ponto do Reporting Services num site sem pacotes de idiomas, os relatórios são instalados em inglês. Se instalar um pacote de idiomas depois de instalar o ponto do Reporting Services, terá de desinstalar e reinstalar o ponto do Reporting Services para que os relatórios sejam disponibilizados no idioma adequado do pacote de idiomas. Para obter mais informações sobre pacotes de idiomas, consulte [pacotes de idiomas no System Center Configuration Manager](../deploy/install/language-packs.md).  

###  <a name="BKMK_FileInstallationAndSecurity"></a> Instalação de ficheiros e direitos de segurança da pasta de relatórios  
 Configuration Manager executa as seguintes ações para instalar o ponto do reporting services e para configurar o Reporting Services:  

> [!IMPORTANT]  
>  As ações da lista seguinte são efetuadas com as credenciais da conta que está configurada para o serviço SMS_Executive, que é normalmente a conta de sistema local do servidor do site.  

-   Instala a função de site de ponto do Reporting Services.  

-   Cria a origem de dados no Reporting Services com as credenciais armazenadas especificadas no assistente. Esta é a conta de utilizador e a palavra-passe do Windows que o Reporting Services utiliza para ligar à base de dados do site quando são executados relatórios.  

-   Cria a pasta raiz do Configuration Manager no Reporting Services.  

-   Adiciona as funções de segurança **Utilizadores de Relatório do ConfigMgr** e **Administradores de Relatório do ConfigMgr** no Reporting Services.  

-   Cria subpastas e implanta relatórios do Configuration Manager a partir de %ProgramFiles%\SMS_SRSRP no Reporting Services.  

-   Adiciona o **usuários de relatório do ConfigMgr** função no Reporting Services às pastas raiz de todas as contas de usuário no Configuration Manager que têm **leitura do Site** direitos.  

-   Adiciona o **administradores de relatório do ConfigMgr** função no Reporting Services às pastas raiz de todas as contas de usuário no Configuration Manager que têm **modificar do Site** direitos.  

-   Recupera o mapeamento entre as pastas de relatórios e o Configuration Manager tipos de objeto (mantidos no banco de dados de site do Configuration Manager) protegidos.  

-   Configura os seguintes direitos para usuários administrativos no Configuration Manager para pastas específicas de relatório no Reporting Services:  

    -   Adiciona usuários e atribui o **usuários de relatório do ConfigMgr** função para a pasta de relatórios associada para usuários administrativos que têm **executar relatório** permissões para o objeto do Gerenciador de configuração.  

    -   Adiciona usuários e atribui o **administradores de relatório do ConfigMgr** função para a pasta de relatórios associada para usuários administrativos que têm **modificar relatório** permissões para o objeto do Gerenciador de configuração.  

     Configuration Manager se conecta ao Reporting Services e define as permissões para os usuários nas pastas de raiz do Configuration Manager e o Reporting Services e pastas de relatório específico. Após a instalação inicial do ponto do reporting services, o Configuration Manager se conecta ao Reporting Services em um intervalo de 10 minutos para verificar se os direitos de usuário configurados nas pastas de relatório são os direitos associados definidos para usuários do Configuration Manager. Quando os usuários são adicionados ou os direitos de usuário são modificados na pasta de relatórios usando o Gerenciador de relatórios do Reporting Services, o Configuration Manager substitui essas alterações usando as atribuições de função armazenadas no banco de dados do site. Gerenciador de configuração também remove usuários que não têm direitos de relatórios no Configuration Manager.  

##  <a name="BKMK_SecurityRoles"></a> Funções de segurança do Reporting Services para o Configuration Manager  
 Quando o Configuration Manager instala o ponto do reporting services, adiciona as seguintes funções de segurança no Reporting Services:  

-   **Usuários de relatório do ConfigMgr**: Os usuários que recebem essa função de segurança só podem executar relatórios do Configuration Manager.  

-   **Os administradores de relatório do ConfigMgr**: Os usuários que recebem essa função de segurança podem executar todas as tarefas relacionadas a relatórios no Configuration Manager.  

##  <a name="BKMK_VerifyReportingServicesPointInstallation"></a> Verificar a instalação do Ponto do Reporting Services  
 Depois de adicionar a função de site de ponto do Reporting Services, pode verificar a instalação observando mensagens de estado e entradas do ficheiro de registo específicas. Utilize o procedimento seguinte para verificar se a instalação do ponto do Reporting Services foi bem-sucedida.  

> [!WARNING]  
>  Você pode ignorar esse procedimento se os relatórios são exibidos no **relatórios** subpasta do **relatórios** nó o **monitoramento** espaço de trabalho no console do Configuration Manager.  

#### <a name="to-verify-the-reporting-services-point-installation"></a>Para verificar a instalação do ponto do Reporting Services  

1.  No console do Configuration Manager, clique em **monitoramento**.  

2.  Na área de trabalho **Monitorização** , expanda **Estado do Sistema**e clique em **Estado do Componente**.  

3.  Clique em **SMS_SRS_REPORTING_POINT** na lista de componentes.  

4.  No separador **Home Page** , no grupo **Componente** , clique em **Mostrar Mensagens**e em **Todas**.  

5.  Especifique uma data e hora para um período antes da instalação do ponto do Reporting Services e clique em **OK**.  

6.  Verifique se a mensagem de estado com o ID 1015 está listada, o que indica que o ponto do Reporting Services foi instalado com êxito. Como alternativa, você pode abrir o arquivo Srsrp.log, localizado em &lt; *ConfigMgr Installation Path*> \Logs e procure **instalação foi bem-sucedida**.  

     No Windows Explorer, navegue até &lt; *ConfigMgr Installation Path*> \Logs.  

7.  Abra Srsrp.log e percorra o ficheiro de registo a partir da hora em que o ponto do Reporting Services foi instalado com êxito. Verifique se as pastas de relatórios foram criadas, se os relatórios foram implementados e se a política de segurança de cada pasta foi confirmada. Procure **Verificação com êxito de que o serviço Web do SRS tem um bom estado de funcionamento no servidor** depois da última linha de confirmações da política de segurança.  

##  <a name="BKMK_Certificate"></a> Configurar um certificado autoassinado para computadores da consola do Configuration Manager  
 Existem várias opções para a criação de relatórios do SQL Server Reporting Services. Quando você cria ou edita relatórios no console do Configuration Manager, Configuration Manager abre o construtor de relatórios para usar como o ambiente de criação. Independentemente de como você cria seus relatórios do Configuration Manager, um certificado autoassinado é necessário para autenticação de servidor para o servidor de banco de dados do site. Configuration Manager instala automaticamente o certificado no servidor do site e os computadores com o provedor de SMS instalado. Portanto, você pode criar ou editar relatórios a partir do console do Configuration Manager quando ele é executado de um desses computadores. No entanto, quando você cria ou modifica relatórios em um console do Configuration Manager que está instalado em um computador diferente, você deve exportar o certificado do servidor do site e, em seguida, adicioná-lo para o **pessoas confiáveis** repositório de certificados no computador que executa o console do Configuration Manager.  

> [!NOTE]  
>  Para mais informações sobre outros ambientes de criação de relatórios para o SQL Server Reporting Services, consulte [Comparação de Ambientes de Criação de Relatórios](http://go.microsoft.com/fwlink/p/?LinkId=242805) no SQL Server 2008 Books Online.  

 Use o procedimento a seguir como um exemplo de como transferir uma cópia do certificado autoassinado do servidor do site para outro computador que executa o console do Configuration Manager, quando ambos os computadores executarem o Windows Server 2008 R2. Se não for possível seguir este procedimento porque tem uma versão diferente do sistema operativo, consulte a documentação do seu sistema operativo para obter o procedimento equivalente.  

#### <a name="to-transfer-a-copy-of-self-signed-certificate-from-the-site-server-to-another-computer"></a>Para transferir uma cópia do certificado autoassinado do servidor do site para outro computador  

1.  Execute os passos seguintes no servidor do site para exportar o certificado autoassinado:  

    1.  Clique em **Iniciar**, clique em **Executar**e escreva **mmc.exe**. Na consola vazia, clique em **Ficheiro**e clique em **Adicionar/Remover Snap-in**.  

    2.  Na caixa de diálogo **Adicionar ou Remover Snap-ins** , selecione **Certificados** na lista de **Snap-ins disponíveis**e clique em **Adicionar**.  

    3.  Na caixa de diálogo **Snap-in de certificado** , selecione **Conta de computador**e clique em **Seguinte**.  

    4.  Na caixa de diálogo **Selecionar Computador** , certifique-se de que **Computador local: (o computador onde esta consola está a ser executada)** está selecionado e, em seguida, clique em **Concluir**.  

    5.  Na caixa de diálogo **Adicionar ou Remover Snap-ins** , clique em **OK**.  

    6.  Na consola, expanda **Certificados (Computador Local)**, expanda **Pessoas Fidedignas**e selecione **Certificados**.  

    7.  Clique o certificado com o nome amigável do &lt; *FQDN do servidor do site*>, clique em **todas as tarefas**e, em seguida, selecione **exportar**.  

    8.  Conclua o **Assistente para Exportar Certificados** , utilizando as opções predefinidas, e guarde o certificado com a extensão de nome de ficheiro **.cer** .  

2.  Execute as seguintes etapas no computador que executa o console do Configuration Manager para adicionar o certificado autoassinado ao repositório de certificados de pessoas confiáveis:  

    1.  Repita os passos anteriores de 1.a a 1.e Para configurar o **certificado** snap-in do MMC no computador do ponto de gerenciamento.  

    2.  Na consola, expanda **Certificados (Computador Local)**, expanda **Pessoas Fidedignas**, clique com o botão direito do rato em **Certificados**, selecione **Todas as Tarefas**e, em seguida, selecione **Importar** para iniciar o **Assistente para Importar Certificados**.  

    3.  Na página **Ficheiro a Importar** , selecione o certificado guardado no passo 1.h e, em seguida, clique em **Seguinte**.  

    4.  Na página **Arquivo de Certificados** , selecione **Colocar todos os certificados no seguinte arquivo**, com o **Arquivo de certificados** definido para **Pessoas Fidedignas**, e clique em **Seguinte**.  

    5.  Clique em **Concluir** para fechar o assistente e concluir a configuração do certificado no computador.  

##  <a name="BKMK_ModifyReportingServicesPoint"></a> Modificar as definições do Ponto do Reporting Services  
 Após a instalação do ponto do Reporting Services, pode modificar a ligação da base de dados do site e as definições de autenticação nas propriedades do ponto do Reporting Services. Utilize o procedimento seguinte para modificar as definições do ponto do Reporting Services.  

#### <a name="to-modify-reporting-services-point-settings"></a>Para modificar as definições do ponto do Reporting Services  

1.  Na consola do Configuration Manager, clique em **Administração**.  

2.  Na área de trabalho **Administração** , expanda **Configuração do Site**e clique em **Servidores e Funções de Sistema de Sites** para listar os sistemas de sites.  

    > [!TIP]  
    >  Para listar apenas os sistemas de sites que alojam a função de site do ponto do Reporting Services, clique com o botão direito do rato em **Servidores e Funções de Sistema de Sites** e selecione **Ponto do Reporting Services**.  

3.  Selecione o sistema de sites que aloja o ponto do Reporting Services no qual pretende modificar as definições e, em seguida, selecione **Ponto do Reporting Services** em **Funções de Sistema de Sites**.  

4.  No separador **Função do Site** , no grupo **Propriedades** , clique em **Propriedades**.  

5.  Na caixa de diálogo **Propriedades do Ponto do Reporting Services** , é possível modificar as definições seguintes:  

    -   **Nome do servidor de banco de dados de site**: Especifique o nome do servidor que hospeda o banco de dados de site do Configuration Manager. Normalmente, o assistente obtém automaticamente o nome de domínio completamente qualificado (FQDN) do servidor. Para especificar uma instância de banco de dados, use o formato &lt; *nome do servidor*>\&lt; *Nome da instância*>.  

    -   **Nome do banco de dados**: Especifique o nome de banco de dados de site do System Center 2012 Configuration Manager e, em seguida, clique em **verificar** para confirmar que o assistente tem acesso ao banco de dados do site.  

        > [!IMPORTANT]  
        >  A conta de utilizador que está a criar o ponto do Reporting Services deve ter acesso de Leitura à base de dados do site. Se o teste de ligação falhar, é apresentado um ícone de aviso vermelho. Mova o cursor sobre este ícone para ler detalhes da falha. Corrija a falha e, em seguida, clique novamente em **Testar** .  

    -   **Conta de usuário**: Clique em **definir**, e, em seguida, selecione uma conta que é usada quando o ponto de serviços do SQL Server Reporting Services em que o relatório se conecta ao banco de dados de site do Configuration Manager para recuperar os dados que são exibidos em um relatório. Selecione **conta existente** para especificar uma conta de usuário do Windows que tenha direitos existentes do Configuration Manager ou selecione **nova conta** para especificar uma conta de usuário do Windows que atualmente não tem direitos no Configuration Manager. Gerenciador de configuração concede automaticamente o acesso de conta de usuário especificada para o banco de dados do site. A conta é apresentada como a conta do **ponto de relatórios do SRS do ConfigMgr** na subpasta **Contas** do nó **Segurança** da área de trabalho **Administração** .  

         A conta de utilizador e palavra-passe do Windows especificadas são encriptadas e armazenadas na base de dados do Reporting Services. O Reporting Services obtém os dados para relatórios na base de dados do site utilizando esta conta e palavra-passe.  

        > [!IMPORTANT]  
        >  Quando a base de dados do site se encontra num sistema de sites remoto, a conta especificada deve ter a permissão **Iniciar Sessão Localmente** no computador.  

6.  Clique em **OK** para guardar as alterações e sair da caixa de diálogo.  

## <a name="upgrading-sql-server"></a>Atualização do SQL Server  
 Após a atualização do SQL Server e SQL Server Reporting Services que é usada como a fonte de dados para um ponto do reporting services, talvez ocorram alguns erros quando você executa ou edita relatórios no console do Configuration Manager. Para o relatório seja executado adequadamente no console do Configuration Manager, você deve remover a função reporting services point site system para o site e reinstalá-lo. No entanto, após a atualização é possível continuar a executar e editar relatórios com êxito a partir de um browser da Internet.  

##  <a name="BKMK_ConfigureReportOptions"></a> Configurar opções de relatórios  
 Use as opções de relatório para um site do Configuration Manager para selecionar o padrão de ponto do reporting services que é usado para gerenciar seus relatórios. Embora seja possível ter mais do que um ponto do Reporting Services num site, apenas o servidor de relatórios predefinido selecionado nas opções de relatórios é utilizado para gerir relatórios. Utilize o procedimento seguinte para configurar opções de relatórios para o site.  

#### <a name="to-configure-report-options"></a>Para configurar opções de relatórios  

1.  No console do Configuration Manager, clique em **monitoramento**.  

2.  Na área de trabalho **Monitorização** , expanda **Comunicar**e clique em **Relatórios**.  

3.  No separador **Home Page** , no grupo **Definições** , clique em **Opções de Relatórios**.  

4.  Selecione o servidor de relatórios predefinido na lista e, em seguida, clique em **OK**. Se não for apresentado nenhum ponto do Reporting Services na lista, verifique se tem um ponto do Reporting Services corretamente instalado e configurado no site.  

## <a name="next-steps"></a>Passos seguintes
[Operações e manutenção de relatórios](operations-and-maintenance-for-reporting.md)

