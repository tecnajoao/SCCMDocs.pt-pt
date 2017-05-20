---
title: As contas utilizadas pelo Configuration Manager | Documentos do Microsoft
description: Identificar e gerir os grupos do Windows e as contas no System Center Configuration Manager.
ms.custom: na
ms.date: 2/9/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 72d7b174-f015-498f-a0a7-2161b9929198
caps.latest.revision: 7
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 72263ec5e7104924a1ca46dc2000be9f8568599f
ms.openlocfilehash: a776667cc9f24bd4a468afea76e466c34ce66864
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="accounts-used-in-system-center-configuration-manager"></a>Contas utilizadas no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize as seguintes informações para identificar os grupos do Windows e as contas que são utilizadas no System Center Configuration Manager, como são utilizados bem como os requisitos.  

## <a name="windows-groups-that-configuration-manager-creates-and-uses"></a>Grupos do Windows Criados e Utilizados pelo Configuration Manager  
 O Configuration Manager automaticamente cria e, em muitos casos mantém automaticamente, os seguintes grupos do Windows.  

> [!NOTE]  
>  Quando o Configuration Manager cria um grupo num computador que seja um membro de domínio, o grupo é um grupo de segurança local. Se o computador for um controlador de domínio, o grupo é um grupo local de domínio que é partilhado entre todos os controladores de domínio no domínio.  


### <a name="configmgrcollectedfilesaccess"></a>ConfigMgr_CollectedFilesAccess  
Para conceder acesso para ver ficheiros recolhidos pelo inventário de software, o Configuration Manager utiliza este grupo.  

A tabela seguinte lista os detalhes adicionais para este grupo:  

|Detalhe|Mais informações|  
|------------|----------------------|  
|Tipo e localização|Este grupo é um grupo de segurança local criado no servidor do site primário.<br /><br /> Quando desinstala um site, este grupo não é removido automaticamente. Tem de ser manualmente eliminado.|  
|Associação|O Configuration Manager gere automaticamente a associação ao grupo. A associação inclui os utilizadores administrativos que recebem permissão para **Ver Ficheiros Recolhidos** relativamente ao objeto com capacidade de segurança **Recolha** de uma função de segurança atribuída.|  
|Permissões|Por predefinição, este grupo tem **leitura** permissão para a seguinte pasta no servidor do site: **%path%\Microsoft configuração Manager\sinv.box\FileCol**.|  

### <a name="configmgrdviewaccess"></a>ConfigMgr_DViewAccess  
 Este grupo é um grupo de segurança local do Configuration Manager cria no servidor de base de dados do site ou servidor de réplica de base de dados. Este não é utilizada atualmente mas está reservado para utilização futura.  

### <a name="configmgr-remote-control-users"></a>Utilizadores do Controlo Remoto do ConfigMgr  
 Ferramentas remotas do Configuration Manager utilizam este grupo para armazenar contas e grupos que configura na lista de visualizadores permitidos que está atribuída a cada cliente.  

 A tabela seguinte lista os detalhes adicionais para este grupo:  

|Detalhe|Mais informações|  
|------------|----------------------|  
|Tipo e localização|Este grupo é um grupo de segurança local criado no cliente do Configuration Manager quando o cliente recebe uma política que ativa as ferramentas remotas.<br /><br /> Depois de desativar as ferramentas remotas para um cliente, este grupo não é removido automaticamente. -Tem de ser eliminado manualmente a partir de cada computador cliente.|  
|Associação|Por predefinição, não existem membros neste grupo. Quando são adicionados utilizadores à lista de Visualizadores Autorizados, eles são automaticamente adicionados a este grupo.<br /><br /> Pode utilizar a lista de Visualizadores Autorizados para gerir a associação a este grupo, em vez de adicionar utilizadores ou grupos diretamente a este grupo.<br /><br /> Além de ser um visualizadores autorizados, um utilizador administrativo tem de ter o **controlo remoto** permissão para o **coleção** objeto. Pode atribuir esta permissão utilizando a função de segurança Operador de Ferramentas Remotas.|  
|Permissões|Por predefinição, este grupo não tem permissões para localizações no computador. É utilizado apenas para conter a lista de visualizadores permitidos.|  

### <a name="sms-admins"></a>Admins de SMS  
 O Configuration Manager utiliza este grupo para conceder acesso ao fornecedor de SMS, através do Windows Management Instrumentation (WMI). É necessário acesso ao fornecedor de SMS para ver e alterar objetos na consola do Configuration Manager.  

> [!NOTE]  
>  A configuração de administração baseada em funções de um utilizador administrativo determina que objetos podem visualizar e gerir ao utilizarem a consola do Configuration Manager.  

 A tabela seguinte lista os detalhes adicionais para este grupo:  

|Detalhe|Mais informações|  
|------------|----------------------|  
|Tipo e localização|Este grupo é um grupo de segurança local criado em cada computador que tem um fornecedor de SMS.<br /><br /> Quando desinstala um site, este grupo não é removido automaticamente. Tem de ser manualmente eliminado.|  
|Associação|O Configuration Manager gere automaticamente a associação ao grupo. Por predefinição, cada utilizador administrativo numa hierarquia e a conta do computador do servidor de site são membros do grupo Admins de SMS em cada computador do Fornecedor de SMS num site.|  
|Permissões|Admins de SMS direitos e permissões são definidos no snap-in MMC de controlo WMI. Por predefinição, o grupo Admins de SMS é concedido **ativar conta** e **ativar remoto** no espaço de nomes root\sms. Os utilizadores autenticados tem **executar métodos**, **escrita no fornecedor**, e **ativar conta**.<br /><br /> Os utilizadores administrativos que irão utilizar uma consola remota do Configuration Manager necessitam de permissões de ativação remota DCOM no computador do servidor do site e o computador do fornecedor de SMS. É um procedimento recomendado conceder estes direitos a Admins de SMS para simplificar a administração em vez de conceder estes direitos diretamente a utilizadores ou grupos. Para obter mais informações, veja a secção [Configurar permissões de DCOM para consolas remotas do Configuration Manager](../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ConfigDCOMforRemoteConsole) do tópico [Modificar a infraestrutura do System Center Configuration Manager](../../../core/servers/manage/modify-your-infrastructure.md).|  

### <a name="smssitesystemtositeserverconnectionmpltsitecode"></a>SMS_SiteSystemToSiteServerConnection_MP_&lt;sitecode\>  
 Pontos de gestão do Configuration Manager que são remotos, a partir do servidor do site utilizam este grupo para ligar à base de dados do site. Este grupo fornece acesso de ponto de gestão às pastas a receber no servidor do site e na base de dados do site.  

 A tabela seguinte lista os detalhes adicionais para este grupo:  

|Detalhe|Mais informações|  
|------------|----------------------|  
|Tipo e localização|Este grupo é um grupo de segurança local criado em cada computador que tem um fornecedor de SMS.<br /><br /> Quando desinstala um site, este grupo não é removido automaticamente. Tem de ser manualmente eliminado.|  
|Associação|O Configuration Manager gere automaticamente a associação ao grupo. Por predefinição, a associação inclui as contas de computador de computadores remotos que têm um ponto de gestão para o site.|  
|Permissões|Por predefinição, este grupo tem **leitura**, **leitura & executar**, e **listar conteúdo das pastas** permissão para o **%path%\Microsoft configuração Manager\inboxes** pasta no servidor do site. Este grupo tem permissão adicional de **escrever** para subpastas o **as pastas a receber** para as quais o ponto de gestão escreve dados de cliente.|  

### <a name="smssitesystemtositeserverconnectionsmsprovltsitecode"></a>SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;sitecode\>  
 Computadores de fornecedor de SMS do Configuration Manager que são remotos, a partir do servidor do site utilizam este grupo para ligar ao servidor do site.  

 A tabela seguinte lista os detalhes adicionais para este grupo:  

|Detalhe|Mais informações|  
|------------|----------------------|  
|Tipo e localização|Este grupo é um grupo de segurança local criado no servidor do site.<br /><br /> Quando desinstala um site, este grupo não é removido automaticamente. Tem de ser manualmente eliminado.|  
|Associação|O Configuration Manager gere automaticamente a associação ao grupo. Por predefinição, a associação inclui a conta de computador ou a conta de utilizador de domínio que é utilizada para ligar ao servidor do site a partir de cada computador remoto que tem instalado um fornecedor de SMS para o site.|  
|Permissões|Por predefinição, este grupo tem **leitura**, **leitura & executar**, e **listar conteúdo das pastas** permissão para o **%path%\Microsoft configuração Manager\inboxes** pasta no servidor do site. Este grupo tem permissão adicional de **escrever** ou as permissões de **escrever** e **modificar** para subpastas o **as pastas a receber** para as quais o fornecedor de SMS requer acesso.<br /><br /> Este grupo tem **leitura**, **leitura & executar**, **listar conteúdo das pastas**, **escrever**, e **modificar** permissões para as pastas em **%path%\Microsoft configuração Manager\OSD\boot** e **leitura** permissão para as pastas em **%path%\Microsoft configuração Manager\OSD\Bin** no servidor do site.|  

### <a name="smssitesystemtositeserverconnectionstatltsitecode"></a>SMS_SiteSystemToSiteServerConnection_Stat_&lt;sitecode\>  
 O Gestor de distribuição de ficheiros em computadores de sistemas de sites remoto do Configuration Manager utiliza este grupo para ligar ao servidor do site.  

 A tabela seguinte lista os detalhes adicionais para este grupo:  

|Detalhe|Mais informações|  
|------------|----------------------|  
|Tipo e localização|Este grupo é um grupo de segurança local criado no servidor do site.<br /><br /> Quando desinstala um site, este grupo não é removido automaticamente. Tem de ser manualmente eliminado.|  
|Associação|O Configuration Manager gere automaticamente a associação ao grupo. Por predefinição, a associação inclui a conta do computador ou a conta do utilizador de domínio que é usada para ligar ao servidor do site a partir de cada computador do servidor de site remoto que executa o Gestor de Distribuição de Ficheiros.|  
|Permissões|Por predefinição, este grupo tem **leitura**, **leitura & executar**, e **listar conteúdo das pastas** permissão para o **%path%\Microsoft configuração Manager\inboxes** pasta e subpastas na localização no servidor do site. Este grupo tem permissões adicionais de **escrever** e **modificar** para o **%path%\Microsoft configuração Manager\inboxes\statmgr.box** pasta no servidor do site.|  

### <a name="smssitetositeconnectionltsitecode"></a>Sms_sitetositeconnection _&lt;sitecode\>  
 Para ativar a replicação baseada em ficheiros entre sites numa hierarquia, o Configuration Manager utiliza este grupo. Para cada site remoto que transfere diretamente ficheiros para este site, este grupo tem contas configuradas como uma **conta de replicação de ficheiros**.  

 A tabela seguinte lista os detalhes adicionais para este grupo:  

|Detalhe|Mais informações|  
|------------|----------------------|  
|Tipo e localização|Este grupo é um grupo de segurança local criado no servidor do site.|  
|Associação|Quando instala um novo site como subordinado de outro site, o Configuration Manager adiciona automaticamente a conta de computador do novo site ao grupo no servidor do site principal. Do Configuration Manager também adiciona a conta de computador do site principal para o grupo no novo servidor de sites. Se especificar outra conta para transferências baseadas em ficheiros, adicione essa conta a este grupo no servidor do site de destino.<br /><br /> Quando desinstala um site, este grupo não é removido automaticamente. Tem de ser manualmente eliminado.|  
|Permissões|Por predefinição, este grupo tem **controlo total** para o **%path%\Microsoft configuração Manager\inboxes\despoolr.box\receive** pasta.|  

## <a name="accounts-that-configuration-manager-uses"></a>Contas que o Configuration Manager Utiliza  
 Pode configurar as seguintes contas para o Configuration Manager.  

### <a name="active-directory-group-discovery-account"></a>Conta de Deteção de Grupos do Active Directory  
 O **conta de deteção de grupo do Active Directory** é utilizada para detetar grupos de segurança locais, globais e universais, as associações nesses grupos e as associações em grupos de distribuição das localizações especificadas nos serviços de domínio do Active Directory. Os grupos de distribuição não são detetados como recursos de grupo.  

 Esta conta pode ser uma conta de computador do servidor do site que executa a deteção ou uma conta de utilizador do Windows. Tem de ter permissão de acesso de **Leitura** às localizações do Active Directory que são especificadas para deteção.  

### <a name="active-directory-system-discovery-account"></a>Conta de Deteção de Sistemas do Active Directory  
 A **Conta de Deteção de Sistemas do Active Directory** serve para detetar computadores a partir de localizações especificadas nos Serviços de Domínio do Active Directory.  

 Esta conta pode ser uma conta de computador do servidor do site que executa a deteção ou uma conta de utilizador do Windows. Tem de ter permissão de acesso de **Leitura** às localizações do Active Directory que são especificadas para deteção.  

### <a name="active-directory-user-discovery-account"></a>Conta de Deteção de Utilizadores do Active Directory  
 A **Conta de Deteção de Utilizadores do Active Directory** serve para detetar contas de utilizador a partir de localizações especificadas nos Serviços de Domínio do Active Directory.  

 Esta conta pode ser uma conta de computador do servidor do site que executa a deteção ou uma conta de utilizador do Windows. Tem de ter permissão de acesso de **Leitura** às localizações do Active Directory que são especificadas para deteção.  

### <a name="active-directory-forest-account"></a>Conta de Floresta do Active Directory  
 O **conta de floresta do Active Directory** é utilizada para detetar infraestruturas de rede a partir de florestas do Active Directory. Sites de administração central e sites primários também utilizá-lo ao publicar dados do site nos serviços de domínio do Active Directory de uma floresta.  

> [!NOTE]  
>  Os sites secundários utilizam sempre a conta de computador de servidor do site secundário para publicar no Active Directory.  

> [!NOTE]  
>  Conta de floresta do Active Directory tem de ser uma conta global para detetar e publicar em florestas não fidedignas. Se não utilizar a conta de computador do servidor do site, pode selecionar apenas uma conta global.  

 Esta conta tem de ter permissões de **Leitura** para cada floresta do Active Directory onde pretende detetar infraestruturas de rede.  

 Esta conta tem de ter permissões de **Controlo Total** para o contentor de Gestão do Sistema e todos os respetivos objetos subordinados em cada floresta do Active Directory onde pretende publicar os dados do site.  

### <a name="asset-intelligence-synchronization-point-proxy-server-account"></a>Conta de Servidor Proxy do Ponto de Sincronização do Asset Intelligence  
 O ponto de sincronização do Asset Intelligence utiliza o **conta de servidor de Proxy de ponto de sincronização do Intelligence Asset** para aceder à Internet através de um proxy de servidor ou firewall que necessite de acesso autenticado.  

> [!IMPORTANT]  
>  Especifique uma conta que tenha o menor número possível de permissões para a firewall ou o servidor proxy necessário.  

### <a name="certificate-registration-point-account"></a>Conta de Ponto de Registo de Certificados  
 O **conta de ponto de registo de certificados** liga o ponto de registo de certificado na base de dados do Configuration Manager. A conta de computador do servidor de ponto de registo de certificados é utilizada por predefinição, mas pode configurar uma conta de utilizador em vez disso. Tem de especificar uma conta de utilizador sempre que o ponto de registo de certificados está num domínio não fidedigno do servidor do site. Esta conta apenas necessite **leitura** aceder à base de dados do site, porque o sistema de mensagens de estado processa as tarefas de escrita.  

### <a name="capture-operating-system-image-account"></a>Conta para Captura de Imagem do Sistema Operativo  
 O Configuration Manager utiliza o **capturar conta de imagem de sistema operativo** para aceder à pasta onde as imagens capturadas estão armazenadas ao implementar sistemas operativos. Esta conta é necessária se adicionar o passo **Capturar Imagem do Sistema Operativo** a uma sequência de tarefas.  

 A conta tem de ter permissões de **Leitura** e **Escrita** na partilha de rede onde a imagem capturada está armazenada.  

 Se a palavra-passe para a conta for alterada no Windows, tem de atualizar a sequência de tarefas com a nova palavra-passe. Cliente do Configuration Manager irá receber a nova palavra-passe quando transferir a política de cliente.  

 Se utilizar esta conta, pode criar uma conta de utilizador de conta de domínio com as permissões mínimas para aceder aos recursos de rede necessários e utilizá-la para todas as contas de sequência de tarefas.  

> [!IMPORTANT]  
>  Não atribua permissões de início de sessão interativas a esta conta.  
>   
>  Não utilize a Conta de Acesso à Rede para esta conta.  

### <a name="client-push-installation-account"></a>Conta de instalação para ligar cliente  
 O **conta de instalação de Push de cliente** é utilizada para ligar a computadores e instalar o software de cliente do Configuration Manager, se implementar clientes utilizando a instalação push do cliente. Se esta conta não for especificada, é utilizada a conta de servidor do site para tentar instalar o software de cliente.  

 Esta conta tem de ser um membro do local **administradores** grupo nos computadores onde será instalado o software de cliente do Configuration Manager. Esta conta necessita de **Admin de domínio** direitos.  

 Pode especificar um ou mais Push contas de instalação cliente, que o Configuration Manager tenta por ordem até uma ter êxito.  

> [!TIP]  
>  Para coordenar de forma mais eficaz atualizações de conta em grandes implementações de Active Directory, crie uma nova conta com um nome diferente e, em seguida, adicione a conta de novo à lista de contas de instalação Push do cliente no Configuration Manager. Permita tempo suficiente para serviços de domínio do Active Directory repliquem a nova conta e, em seguida, remover a conta antiga do Configuration Manager e os serviços de domínio do Active Directory.  

> [!IMPORTANT]  
>  Não conceda a esta conta o direito de iniciar sessão localmente.  

### <a name="enrollment-point-connection-account"></a>Conta de Ligação do Ponto de Registo  
 O **conta de ligação de ponto de registo** liga o ponto de inscrição para a base de dados do site do Configuration Manager. A conta de computador do ponto de inscrição é utilizada por predefinição, mas pode configurar uma conta de utilizador em vez disso. Tem de especificar uma conta de utilizador sempre que o ponto de registo está num domínio não fidedigno do servidor do site. Esta conta necessita de **leitura** e **escrever** acesso à base de dados do site.  

### <a name="exchange-server-connection-account"></a>Conta de ligação a Exchange Server  
 A **Conta de Ligação a Exchange Server** liga o servidor do site ao computador do Exchange Server especificado para localizar e gerir dispositivos móveis que ligam ao Exchange Server. Esta conta necessita de cmdlets do Exchange PowerShell que forneçam as permissões necessárias ao computador do Exchange Server. Para obter mais informações sobre os cmdlets, veja [Gerir dispositivos móveis com o System Center Configuration Manager e o Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

### <a name="exchange-server-connector-proxy-server-account"></a>Conta de servidor proxy de conector do Exchange Server  
 O conector do Exchange Server utiliza o **conta de servidor de Proxy de conector do Exchange Server** para aceder à Internet através de um proxy de servidor ou firewall que necessite de acesso autenticado.  

> [!IMPORTANT]  
>  Especifique uma conta que tenha o menor número possível de permissões para a firewall ou o servidor proxy necessário.  

### <a name="management-point-connection-account"></a>Conta de Ligação de Ponto de Gestão  
 O **conta de ligação de ponto de gestão** é utilizada para ligar o ponto de gestão para a base de dados do site do Configuration Manager para que possa enviar e receber informações de clientes. A conta de computador do ponto de gestão é utilizada por predefinição, mas pode configurar uma conta de utilizador em vez disso. Tem de especificar uma conta de utilizador sempre que o ponto de gestão está num domínio não fidedigno do servidor do site.  

 Crie a conta como com direitos restritos, uma conta local no computador que executa o Microsoft SQL Server.  

> [!IMPORTANT]  
>  Não conceda direitos de início de sessão interativos a esta conta.  

### <a name="multicast-connection-account"></a>Conta de ligação de multicast  
 Pontos de distribuição que estão configurados para utilizar multicast o **conta de ligação de Multicast** ler informações da base de dados do site. A conta de computador do ponto de distribuição é utilizada por predefinição, mas pode configurar uma conta de utilizador em vez disso. Tem de especificar uma conta de utilizador sempre que a base de dados do site estiver numa floresta não fidedigna. Por exemplo, se o seu centro de dados possuir uma rede de perímetro numa floresta que não é o servidor do site e a base de dados do site, pode utilizar esta conta para ler as informações de multicast da base de dados do site.  

 Se criar esta conta, crie-a como uma conta de direitos restritos, local no computador que executa o Microsoft SQL Server.  

> [!IMPORTANT]  
>  Não conceda direitos de início de sessão interativos a esta conta.  

### <a name="network-access-account"></a>Conta de Acesso à Rede  
 Utilização de computadores cliente a **conta de acesso à rede** quando estes não podem utilizar a respetiva conta de computador local para aceder ao conteúdo em pontos de distribuição. Por exemplo, isto aplica-se a clientes e computadores de grupo de trabalho de domínios não fidedignos. Esta conta também pode ser utilizada durante a implementação do sistema operativo quando o computador que está a instalar o sistema operativo ainda não possui uma conta de computador no domínio.  

> [!NOTE]  
>  A conta de acesso à rede nunca é utilizada como o contexto de segurança para executar programas, instalar atualizações de software ou executar sequências de tarefas. É utilizado apenas para aceder a recursos na rede.  

 Conceda a esta conta o menor número possível de permissões ao nível do conteúdo de que o cliente necessita para aceder ao software. A conta tem de ter o direito de **Aceder a este computador a partir da rede** no ponto de distribuição ou outro servidor que contém o conteúdo de pacote. Pode configurar até 10 Contas de Acesso de Rede por site.  

> [!WARNING]  
>  Quando o Configuration Manager tenta utilizar a conta nomedocomputador$ para transferir o conteúdo sem êxito, volta a tentar automaticamente a conta de acesso a rede, mesmo que tenta tentado sem êxito anteriormente.  

 Crie a conta em qualquer domínio que forneça o acesso necessário a recursos. A Conta de Acesso à Rede tem de incluir sempre um nome de domínio. Segurança pass-through não é suportada para esta conta. Se existirem pontos de distribuição em vários domínios, crie a conta num domínio fidedigno.  

> [!TIP]  
>  Para evitar bloqueios de conta, não altere a palavra-passe de uma Conta de Acesso à Rede existente. Em vez disso, crie uma nova conta e configure a conta do novo no Configuration Manager. Quando tiver passado o tempo suficiente para todos os clientes receberem os detalhes da nova conta, remova a conta antiga das pastas partilhadas da rede e elimine a conta.  

> [!IMPORTANT]  
>  Não conceda direitos de início de sessão interativos a esta conta.
>   
>  Não conceda a esta conta o direito de associar computadores ao domínio. Se tiver de associar computadores ao domínio durante uma sequência de tarefas, utilize a Conta de Adesão ao Domínio do Editor de Sequência de Tarefas.  

### <a name="package-access-account"></a>Conta de acesso a pacote  
 Um **conta de acesso a pacote** permite-lhe definir permissões NTFS para especificar os utilizadores e grupos de utilizadores que podem aceder a uma pasta de pacote em pontos de distribuição. Por predefinição, o Configuration Manager concede acesso apenas às contas de acesso genéricas **utilizadores** e **administradores**. Pode controlar o acesso de computadores cliente utilizando o Windows contas ou grupos adicionais. Dispositivos móveis obtêm sempre conteúdo dos pacotes anonimamente, pelo que não utilizam as contas de acesso do pacote.  

 Por predefinição, quando o Configuration Manager cria a partilha de pacote num ponto de distribuição, concede acesso **leitura** acesso local **utilizadores** grupo e **controlo total** local **administradores** grupo. As permissões reais necessárias vão depender do pacote. Se tiver clientes localizados em grupos de trabalho ou em florestas não fidedignas, esses clientes utilizam a Conta de Acesso à Rede para aceder ao conteúdo dos pacotes. Certifique-se de que a conta de acesso a rede possui permissões para o pacote utilizando as contas de acesso a pacote definidas.  

 Utilize contas de um domínio que tenham acesso aos pontos de distribuição. Se criar ou alterar a conta após a criação do pacote, necessitará de redistribuir o pacote. A atualização do pacote não altera as permissões NTFS no pacote.  

 Não é necessário adicionar a conta de acesso a rede como uma conta de acesso a pacote, pois a associação do grupo de Utilizadores adiciona-a automaticamente. Restringir a Contas de Acesso a Pacotes Apenas à Conta de Acesso à Rede não impedirá o acesso dos clientes ao pacote.  

### <a name="reporting-services-point-account"></a>Conta do ponto do Reporting Services  
 SQL Server Reporting Services utiliza o **conta ao ponto do Reporting Services** para obter os dados para relatórios do Configuration Manager a partir da base de dados do site. A conta de utilizador do Windows e a palavra-passe que especificar são encriptadas e armazenadas na base de dados do SQL Server Reporting Services.  

### <a name="remote-tools-permitted-viewer-accounts"></a>Contas de visualizador permitidas por ferramentas remotas  
 As contas que especificar como **Visualizadores Autorizados** para o controlo remoto são uma lista de utilizadores autorizados a utilizar a funcionalidade de ferramentas remotas em clientes.  

### <a name="site-system-installation-account"></a>Conta de Instalação de Sistema de Sites  
 O servidor de site utiliza a **conta de instalação do sistema de sites** para instalar, reinstalar, desinstalar e configurar sistemas de sites. Se configurar o sistema de sites para exigir que o servidor do site inicie ligações a este sistema de sites do Configuration Manager também utiliza esta conta para retirar dados a partir do computador do sistema de site após a instalação de sistema de sites e quaisquer funções de sistema de sites. Cada sistema de sites pode ter uma diferente conta de instalação do sistema de sites, mas pode configurar apenas uma conta de instalação de sistema de sites para gerir todas as funções de sistema de sites nesse sistema de sites.  

 Esta conta necessita de permissões administrativas locais nos sistemas de sites que irão instalar e configurar os administradores. Além disso, esta conta tem de ter **aceder a este computador a partir da rede** na política de segurança nos sistemas de site que irão instalar e configurar os administradores.  

> [!TIP]  
>  Se tiver muitos controladores de domínio e estas contas forem utilizadas em vários domínios, verifique se as contas foram replicadas antes de configurar o sistema de sites.  
>   
>  Quando especificar uma conta local em cada sistema de sites a gerir, esta configuração é mais segura do que utilizar contas de domínio, pois limita os danos que podem ser feitos por atacantes se a conta for comprometida. No entanto, as contas de domínio são mais fáceis de gerir. Considere os diferentes aspetos de segurança e uma administração eficiente.  

### <a name="smtp-server-connection-account"></a>Conta da ligação ao servidor SMTP  
 O servidor de site utiliza a **a conta de ligação de servidor de SMTP** para enviar alertas de correio eletrónico quando o servidor SMTP necessita de acesso autenticado.  

> [!IMPORTANT]  
>  Especifique uma conta que tenha o menor número possível de permissões para enviar mensagens de correio eletrónico.  

### <a name="software-update-point-connection-account"></a>Conta de ligação de ponto de atualização de software  
 O servidor de site utiliza a **conta de ligação de ponto de atualização de Software** dos serviços de atualização de software duas seguintes:  

-   Windows Server Update Services (WSUS) do Configuration Manager, que configura definições como definições de produto, classificações e definições a montante.  

-   WSUS Synchronization Manager, que pede a sincronização a um servidor WSUS a montante ou ao Microsoft Update.  

Conta de instalação do sistema de sites pode instalar componentes para atualizações de software, mas que não pode efetuar funções específicas de atualização de software no ponto de atualização de software. Se não for possível utilizar a conta de computador do servidor de site para esta funcionalidade porque o ponto de atualização de software está numa floresta não fidedigna, tem de especificar esta conta para além da conta de instalação de sistema de sites.  

Esta conta tem de ser um administrador local no computador onde o WSUS está instalado. Também tem de ser parte do grupo de administradores do WSUS local.  

### <a name="software-update-point-proxy-server-account"></a>Conta de servidor proxy de ponto de atualização de software  
 O ponto de atualização de software utiliza o **conta atualização de Software do ponto de Proxy de servidor** para aceder à Internet através de um proxy de servidor ou firewall que necessite de acesso autenticado.  

> [!IMPORTANT]  
>  Especifique uma conta que tenha o menor número possível de permissões para a firewall ou o servidor proxy necessário.  

### <a name="source-site-account"></a>Conta de site de origem  
 O processo de migração utiliza a **conta Site de origem** para aceder ao fornecedor de SMS do site de origem. Esta conta precisa de permissões de **Leitura** a objetos de site no site de origem para recolher dados para tarefas de migração.  

 Se atualizar pontos de distribuição do Configuration Manager 2007 ou sites secundários que tenham colocalizado pontos de distribuição e pontos de distribuição do System Center Configuration Manager, esta conta também tem de ter **eliminar** permissões para o **Site** classe para remover com sucesso o ponto de distribuição do site do Configuration Manager 2007 durante a atualização.  

> [!NOTE]  
>  A conta de Site de origem e a conta de base de dados do Site de origem são identificadas como **Gestor de migração** no **contas** nó do **administração** área de trabalho na consola do Configuration Manager.  

### <a name="source-site-database-account"></a>Conta de base de dados do site de origem  
 O processo de migração utiliza a **conta de base de dados do Site de origem** para aceder à base de dados do SQL Server para o site de origem. Para recolher dados da base de dados do SQL Server do site de origem, a conta de base de dados do Site de origem tem de ter o **leitura** e **executar** permissões para do SQL Server da base de dados o site de origem.  

> [!NOTE]  
>  Se utilizar a conta de computador do System Center Configuration Manager, certifique-se de que todas as opções seguintes são verdadeiras para esta conta:  
>   
> -   É um membro do grupo de segurança **utilizadores COM distribuídos** no domínio onde reside o site do Configuration Manager 2007.  
> -   É um membro do grupo de segurança **Admins de SMS**.  
> -   Tem a **leitura** permissão para todos os objetos do Configuration Manager 2007.  

> [!NOTE]  
>  A conta de Site de origem e a conta de base de dados do Site de origem são identificadas como **Gestor de migração** no **contas** nó do **administração** área de trabalho na consola do Configuration Manager.  

### <a name="task-sequence-editor-domain-joining-account"></a>Conta de adesão ao domínio do editor de sequência de tarefas  
 A **Conta de Associação de Domínio do Editor de Sequência de Tarefas** é utilizada numa sequência de tarefas para associar um computador com imagem recentemente duplicada a um domínio. Esta conta é necessária se adicionar o passo **Associar Domínio ou Grupo de Trabalho** a uma sequência de tarefas e selecionar **Aderir a um domínio**. Esta conta também pode ser configurada se adicionar o passo **aplicar definições de rede** a uma tarefa sequência, mas não é necessária.  

 Esta conta precisa do direito **Associação a um Domínio** no domínio ao qual o computador será associado.  

> [!TIP]  
>  Se necessitar desta conta para as sequências de tarefas, pode criar uma conta de utilizador de domínio com as permissões mínimas para aceder aos recursos de rede necessários e utilizá-la para todas as contas de sequências de tarefas.  

> [!IMPORTANT]  
>  Não atribua permissões de início de sessão interativas a esta conta.  
>   
>  Não utilize a Conta de Acesso à Rede para esta conta.  

### <a name="task-sequence-editor-network-folder-connection-account"></a>Conta de ligação à pasta de rede do editor de sequência de tarefas  
 Uma sequência de tarefas utiliza a **conta de ligação de pasta de rede Editor de sequência de tarefas** para ligar para uma pasta partilhada na rede. Esta conta é necessária se adicionar o passo **Ligar à Pasta de Rede** a uma sequência de tarefas.  

 Esta conta necessita de permissões para aceder à pasta partilhada especificada. Tem de ser uma conta de domínio do utilizador.  

> [!TIP]  
>  Se necessitar desta conta para as sequências de tarefas, pode criar uma conta de utilizador de domínio com as permissões mínimas para aceder aos recursos de rede necessários e utilizá-la para todas as contas de sequências de tarefas.  

> [!IMPORTANT]  
>  Não atribua permissões de início de sessão interativas a esta conta.  
>   
>  Não utilize a Conta de Acesso à Rede para esta conta.  

### <a name="task-sequence-run-as-account"></a>Conta Run As de sequência de tarefas  
 A **Conta Run As de Sequência de Tarefas** é utilizada para executar linhas de comandos em sequências de tarefas e utilizar credenciais diferentes da conta do sistema local. Esta conta é necessária se adicionar o passo **executar linha de comandos** a uma sequência de tarefas, mas não pretender que a sequência de tarefas seja executada com permissões de conta de sistema local no computador gerido.  

 Configure a conta para ter as permissões mínimas necessárias para executar a linha de comandos especificada na sequência de tarefas. A conta necessita de direitos de início de sessão interativos e normalmente requer a capacidade de instalar software e aceder a recursos de rede.  

> [!IMPORTANT]  
>  Não utilize a Conta de Acesso à Rede para esta conta.  
>   
>  Nunca torne a conta de um administrador de domínio.  
>   
>  Nunca configure perfis itinerantes para essa conta. Quando a sequência de tarefas é executada, transferirá o perfil itinerante para a conta. Isto deixará o perfil vulnerável a acesso no computador local.  
>   
>  Limite o âmbito da conta. Por exemplo, crie Contas Run As de Sequência de Tarefas diferentes para cada sequência de tarefas, de modo a que, se uma conta for comprometida, apenas sejam comprometidos os computadores cliente a que essa conta tenha acesso.  
>   
>  Se a linha de comandos exigir acesso administrativo no computador, considere a criação de uma conta de administrador local apenas para a sequência de conta Run As tarefas em todos os computadores que executarão a sequência de tarefas. Elimina a conta assim que já não precisar dele.  

