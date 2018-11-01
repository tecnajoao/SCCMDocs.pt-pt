---
title: Contas utilizadas
titleSuffix: Configuraton Manager
description: Identificar e gerir os grupos do Windows e as contas utilizadas no Configuration Manager.
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 72d7b174-f015-498f-a0a7-2161b9929198
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 12196f042409a3128736beab78ee8dfab0078d76
ms.sourcegitcommit: 8791bb9be477fe6a029e8a7a76e2ca310acd92e0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/31/2018
ms.locfileid: "50411549"
---
# <a name="accounts-used-in-configuration-manager"></a>Contas utilizadas no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize as seguintes informações para identificar os grupos do Windows e as contas que são utilizadas no Configuration Manager, como são utilizadas e quaisquer requisitos.  

- [Grupos do Windows que o Configuration Manager cria e utiliza](#bkmk_groups)  
    - [ConfigMgr_CollectedFilesAccess](#configmgrcollectedfilesaccess)  
    - [ConfigMgr_DViewAccess](#configmgrdviewaccess)  
    - [Utilizadores do controlo remoto do ConfigMgr](#configmgr-remote-control-users)  
    - [Admins de SMS](#sms-admins)  
    - [SMS_SiteSystemToSiteServerConnection_MP_&lt;sitecode\>](#bkmk_remotemp)  
    - [SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;sitecode\>](#bkmk_remoteprov)  
    - [SMS_SiteSystemToSiteServerConnection_Stat_&lt;sitecode\>](#bkmk_remotestat)  
    - [Sms_sitetositeconnection _&lt;sitecode\>](#bkmk_filerepl)  

- [Contas utilizadas pelo Configuration Manager](#bkmk_accounts)
    - [Conta de deteção de grupo do Active Directory](#active-directory-group-discovery-account)  
    - [Conta de deteção de sistema do Active Directory](#active-directory-system-discovery-account)  
    - [Conta de deteção de utilizador do Active Directory](#active-directory-user-discovery-account)  
    - [Conta de floresta do Active Directory](#active-directory-forest-account)  
    - [Conta de ponto de registo de certificados](#certificate-registration-point-account)  
    - [Conta de imagem do sistema operacional para captura](#capture-os-image-account)  
    - [Conta de instalação push do cliente](#client-push-installation-account)  
    - [Conta de ligação de ponto de registo](#enrollment-point-connection-account)  
    - [Conta de ligação do Exchange Server](#exchange-server-connection-account)  
    - [Conta de ligação de ponto de gestão](#management-point-connection-account)  
    - [Conta de ligação de multicast](#multicast-connection-account)  
    - [Conta de acesso de rede](#network-access-account)  
    - [Conta de acesso do pacote](#package-access-account)  
    - [Conta de ponto do Reporting services](#reporting-services-point-account)  
    - [Contas de Visualizador permitidas por ferramentas remotas](#remote-tools-permitted-viewer-accounts)  
    - [Conta de instalação do site](#site-installation-account)
    - [Conta de instalação do sistema de sites](#site-system-installation-account)  
    - [Conta de proxy de servidor de sistema de sites](#site-system-proxy-server-account)  
    - [Conta de ligação do servidor de SMTP](#smtp-server-connection-account)  
    - [Conta de ligação de ponto de atualização de software](#software-update-point-connection-account)  
    - [Conta de site de origem](#source-site-account)  
    - [Conta de base de dados do site de origem](#source-site-database-account)  
    - [Conta de associação de domínio de sequência de tarefas](#task-sequence-domain-join-account)  
    - [Conta de ligação de pasta de rede de sequência de tarefas](#task-sequence-network-folder-connection-account)  
    - [Conta run as de sequência de tarefas](#task-sequence-run-as-account)  



## <a name="bkmk_groups"></a> Grupos do Windows que o Configuration Manager cria e utiliza  

 O Configuration Manager automaticamente cria e em muitos casos automaticamente mantém os seguintes grupos do Windows:  

> [!NOTE]  
>  Quando o Configuration Manager cria um grupo num computador que seja membro do domínio, o grupo é um grupo de segurança local. Se o computador for um controlador de domínio, o grupo é um grupo local de domínio. Este tipo de grupo é partilhado entre todos os controladores de domínio no domínio.  


### <a name="configmgrcollectedfilesaccess"></a>ConfigMgr_CollectedFilesAccess  

Configuration Manager utiliza este grupo para conceder acesso para ver ficheiros recolhidos pelo inventário de software.  

Para obter mais informações, consulte [introdução ao inventário de software](/sccm/core/clients/manage/inventory/introduction-to-software-inventory).

#### <a name="type-and-location"></a>Tipo e localização
Este grupo é um grupo de segurança local criado no servidor do site primário.

Quando desinstala um site, este grupo não é removido automaticamente. Elimine-o manualmente depois de desinstalar um site.

#### <a name="membership"></a>Associação
O Configuration Manager gerencia automaticamente a associação ao grupo. A associação inclui os utilizadores administrativos que recebem permissão para **Ver Ficheiros Recolhidos** relativamente ao objeto com capacidade de segurança **Recolha** de uma função de segurança atribuída.

#### <a name="permissions"></a>Permissões
Por predefinição, este grupo tem **leitura** permissão para a seguinte pasta no servidor do site: `C:\Program Files\Microsoft Configuration Manager\sinv.box\FileCol`  


### <a name="configmgrdviewaccess"></a>ConfigMgr_DViewAccess  

 Este grupo é um grupo de segurança local do Configuration Manager cria no servidor de base de dados do site ou servidor de réplica de base de dados para um site primário subordinado. O site cria-a quando utiliza vistas distribuídas para a replicação de base de dados entre sites numa hierarquia. Ela contém o servidor do site e as contas de computador do SQL Server do site de administração central.

 Para obter mais informações, consulte [transferências de dados entre sites](/sccm/core/servers/manage/data-transfers-between-sites).


### <a name="configmgr-remote-control-users"></a>Utilizadores do Controlo Remoto do ConfigMgr  

 Ferramentas remotas do Configuration Manager utilizam este grupo para armazenar as contas e grupos que configurou no **visualizadores** lista. O site atribui esta lista para cada cliente.  

Para obter mais informações, consulte [introdução ao controlo remoto](/sccm/core/clients/manage/remote-control/introduction-to-remote-control).

#### <a name="type-and-location"></a>Tipo e localização
Este grupo é um grupo de segurança local criado no cliente do Configuration Manager, quando o cliente recebe uma política que ativa as ferramentas remotas.

Depois de desativar as ferramentas remotas para um cliente, este grupo não é removido automaticamente. Elimine-o manualmente depois de desativar ferramentas remotas.

#### <a name="membership"></a>Associação
Por predefinição, não existem membros neste grupo. Quando adiciona utilizadores para o **visualizadores** lista, estes são automaticamente adicionados a este grupo.

Utilize o **visualizadores** lista para gerir a associação deste grupo em vez de adicionar utilizadores ou grupos diretamente a este grupo.

Além de ser um visualizador autorizado, um utilizador administrativo tem de ter o **controlo remoto** permissão para o **coleção** objeto. Atribuir esta permissão utilizando o **operador de ferramentas remotas** função de segurança.  

#### <a name="permissions"></a>Permissões
Por predefinição, este grupo não tem permissões para todas as localizações no computador. É utilizado apenas para conter o **visualizadores** lista.  


### <a name="sms-admins"></a>Admins de SMS  

 Configuration Manager utiliza este grupo para conceder acesso ao fornecedor de SMS através do WMI. É necessário acesso ao fornecedor de SMS para ver e alterar objetos na consola do Configuration Manager.  

> [!NOTE]  
>  A configuração de administração baseada em funções de um utilizador administrativo determina que objetos podem visualizar e gerir ao utilizarem a consola do Configuration Manager.  

Para obter mais informações, consulte [planear o fornecedor de SMS](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider).

#### <a name="type-and-location"></a>Tipo e localização
Este grupo é um grupo de segurança local criado em cada computador que tem um fornecedor de SMS. 

Quando desinstala um site, este grupo não é removido automaticamente. Elimine-o manualmente depois de desinstalar um site.

#### <a name="membership"></a>Associação
O Configuration Manager gerencia automaticamente a associação ao grupo. Por predefinição, cada utilizador administrativo numa hierarquia e a conta de computador do servidor de site são membros do **Admins de SMS** grupo em cada computador fornecedor de SMS num site.

#### <a name="permissions"></a>Permissões
Pode ver os direitos e permissões para o grupo de Admins de SMS no **controle WMI** MMC snap-in. Por predefinição, este grupo é concedido **ativar conta** e **ativar remoto** sobre o `Root\SMS` espaço de nomes WMI. Usuários autenticados tenham **executar métodos**, **escrita do fornecedor**, e **ativar conta**.

Quando utiliza uma consola remota do Gestor de configuração, configure **ativação remota** permissões de DCOM no computador do servidor do site e o fornecedor de SMS. Conceder estes direitos para o **Admins de SMS** grupo. Esta ação simplifica a administração em vez de conceder estes direitos diretamente a utilizadores ou grupos. Para obter mais informações, consulte [configurar permissões de DCOM para consolas remotas do Configuration Manager](/sccm/core/servers/manage/modify-your-infrastructure#BKMK_ConfigDCOMforRemoteConsole). 


### <a name="bkmk_remotemp"></a> SMS_SiteSystemToSiteServerConnection_MP_&lt;sitecode\>  
 
Pontos de gestão que são remotos a partir do servidor do site utilizam este grupo para ligar à base de dados do site. Este grupo fornece acesso de ponto de gestão às pastas a receber no servidor do site e na base de dados do site.  

#### <a name="type-and-location"></a>Tipo e localização
Este grupo é um grupo de segurança local criado em cada computador que tem um fornecedor de SMS.

Quando desinstala um site, este grupo não é removido automaticamente. Elimine-o manualmente depois de desinstalar um site.

#### <a name="membership"></a>Associação
O Configuration Manager gerencia automaticamente a associação ao grupo. Por predefinição, a associação inclui as contas de computador de computadores remotos que têm um ponto de gestão para o site.

#### <a name="permissions"></a>Permissões
Por predefinição, este grupo tem **leitura**, **leitura & executar**, e **listar conteúdo da pasta** permissão para a seguinte pasta no servidor do site: `C:\Program Files\Microsoft Configuration Manager\inboxes`. Este grupo tem a permissão adicional **escrever** para subpastas **pastas a receber**, para que o ponto de gestão escreve os dados de cliente.


### <a name="bkmk_remoteprov"></a> SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;sitecode\>  
 
Computadores de fornecedor de SMS remotos utilizam este grupo para ligar ao servidor do site.  

#### <a name="type-and-location"></a>Tipo e localização
Este grupo é um grupo de segurança local criado no servidor do site.

Quando desinstala um site, este grupo não é removido automaticamente. Elimine-o manualmente depois de desinstalar um site.

#### <a name="membership"></a>Associação
O Configuration Manager gerencia automaticamente a associação ao grupo. Por predefinição, a associação inclui a conta de computador ou uma conta de utilizador de domínio. Utiliza esta conta para ligar ao servidor do site a partir de cada fornecedor de SMS remoto.

#### <a name="permissions"></a>Permissões
Por predefinição, este grupo tem **leitura**, **leitura & executar**, e **listar conteúdo da pasta** permissão para a seguinte pasta no servidor do site: `C:\Program Files\Microsoft Configuration Manager\inboxes`. Este grupo tem permissões adicionais de **escrever** e **modificar** para subpastas indicadas abaixo as pastas a receber. O fornecedor de SMS requer acesso a essas pastas.

Este grupo também tem **leitura** permissão para as subpastas no servidor do site abaixo `C:\Program Files\Microsoft Configuration Manager\OSD\Bin`. 

Também tem as seguintes permissões para as subpastas `C:\Program Files\Microsoft Configuration Manager\OSD\boot`:
- **Leitura**  
- **Ler e executar**  
- **Listar conteúdo das pastas**  
- **Escrita**  
- **Modificar**   


### <a name="bkmk_remotestat"></a> SMS_SiteSystemToSiteServerConnection_Stat_&lt;sitecode\>  

O componente de Gestor de expedição de ficheiros em computadores de sistemas de sites remoto do Configuration Manager utiliza este grupo para ligar ao servidor do site.  

#### <a name="type-and-location"></a>Tipo e localização
Este grupo é um grupo de segurança local criado no servidor do site.

Quando desinstala um site, este grupo não é removido automaticamente. Elimine-o manualmente depois de desinstalar um site.

#### <a name="membership"></a>Associação
O Configuration Manager gerencia automaticamente a associação ao grupo. Por predefinição, a associação inclui a conta de computador ou a conta de utilizador de domínio. Utiliza esta conta para ligar ao servidor do site a partir de cada sistema de sites remoto que executa o Gestor de distribuição de ficheiros.

#### <a name="permissions"></a>Permissões
Por predefinição, este grupo tem **leitura**, **leitura & executar**, e **listar conteúdo da pasta** permissão para a pasta seguinte e suas subpastas no servidor do site: `C:\Program Files\Microsoft Configuration Manager\inboxes` . 

Este grupo tem permissões adicionais de **escrever** e **modificar** para a seguinte pasta no servidor do site: `C:\Program Files\Microsoft Configuration Manager\inboxes\statmgr.box`.


### <a name="bkmk_filerepl"></a> Sms_sitetositeconnection _&lt;sitecode\>  
 Configuration Manager utiliza este grupo para ativar a replicação baseada em ficheiros entre sites numa hierarquia. Para cada site remoto que transfere diretamente ficheiros para este site, este grupo tem contas configuradas como um **conta de replicação de ficheiros**.  

#### <a name="type-and-location"></a>Tipo e localização
Este grupo é um grupo de segurança local criado no servidor do site.

#### <a name="membership"></a>Associação
Quando instala um novo site como subordinado de outro site, o Configuration Manager adiciona automaticamente a conta de computador do novo servidor do site para este grupo no servidor do site principal. O Configuration Manager também adiciona a conta de computador do site principal para o grupo no novo servidor do site. Se especificar outra conta para transferências de ficheiros, adicione essa conta a este grupo no servidor do site de destino.

Quando desinstala um site, este grupo não é removido automaticamente. Elimine-o manualmente depois de desinstalar um site.

#### <a name="permissions"></a>Permissões
Por predefinição, este grupo tem **controlo total** para a seguinte pasta: `C:\Program Files\Microsoft Configuration Manager\inboxes\despoolr.box\receive`.



## <a name="bkmk_accounts"></a> Contas utilizadas pelo Configuration Manager  

 Pode configurar as seguintes contas para o Configuration Manager.  


### <a name="active-directory-group-discovery-account"></a>Conta de deteção de grupo do Active Directory  

 O site utiliza a **conta de deteção de grupos do Active Directory** para detetar os seguintes objetos a partir de localizações nos serviços de domínio do Active Directory que especificar:
 - Grupos de segurança locais, globais e universais
 - A associação no âmbito desses grupos
 - A associação em grupos de distribuição
    - Grupos de distribuição não são detetados como do grupo de recursos

 Esta conta pode ser uma conta de computador do servidor do site que executa a deteção ou uma conta de utilizador do Windows. Tem de ter **leitura** permissão para localizações do Active Directory que especificou para a deteção de acesso.  

 Para obter mais informações, consulte [deteção de grupos do Active Directory](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutGroup).


### <a name="active-directory-system-discovery-account"></a>Conta de deteção de sistema do Active Directory  

 O site utiliza a **conta de deteção de sistema do Active Directory** para detetar computadores a partir de localizações nos serviços de domínio do Active Directory que especificar.  

 Esta conta pode ser uma conta de computador do servidor do site que executa a deteção ou uma conta de utilizador do Windows. Tem de ter **leitura** permissão para localizações do Active Directory que especificou para a deteção de acesso.  

 Para obter mais informações, consulte [deteção de sistemas do Active Directory](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutSystem).


### <a name="active-directory-user-discovery-account"></a>Conta de deteção de utilizador do Active Directory  
 
 O site utiliza a **conta de deteção de utilizador do Active Directory** para detetar contas de utilizador a partir de localizações nos serviços de domínio do Active Directory que especificar.  

 Esta conta pode ser uma conta de computador do servidor do site que executa a deteção ou uma conta de utilizador do Windows. Tem de ter **leitura** permissão para localizações do Active Directory que especificou para a deteção de acesso.  

 Para obter mais informações, consulte [deteção de utilizadores do Active Directory](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutUser). 


### <a name="active-directory-forest-account"></a>Conta de floresta do Active Directory  

 O site utiliza a **conta de floresta do Active Directory** para detetar infraestruturas de rede a partir de florestas do Active Directory. Sites de administração central e sites primários também usá-lo para publicar dados do site para serviços de domínio do Active Directory para uma floresta.  

 > [!NOTE]  
 >  Os sites secundários utilizam sempre a conta de computador de servidor do site secundário para publicar no Active Directory.  

 Para detetar e publicar em florestas não fidedignas, a conta de floresta do Active Directory tem de ser uma conta global. Se não usar a conta de computador do servidor do site, pode selecionar apenas uma conta global.  

 Esta conta tem de ter permissões de **Leitura** para cada floresta do Active Directory onde pretende detetar infraestruturas de rede.  

 Esta conta tem de ter **controlo total** permissões para o **System Management** contentor e todos os seus objetos subordinados em cada floresta do Active Directory onde pretende publicar dados do site. Para obter mais informações, consulte [preparar o Active Directory para publicação de site](/sccm/core/plan-design/network/extend-the-active-directory-schema).  

 Para obter mais informações, consulte [deteção de florestas do Active Directory](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutForest).


### <a name="certificate-registration-point-account"></a>Conta de ponto de registo de certificados  

 O ponto de registo de certificados utiliza a **conta de ponto de registo de certificados** para ligar à base de dados do Configuration Manager. Ele usa a sua conta de computador por padrão, mas pode configurar uma conta de utilizador. Quando o ponto de registo de certificados está num domínio não fidedigno do servidor do site, tem de especificar uma conta de utilizador. Esta conta apenas necessite **leitura** aceder à base de dados do site, uma vez que o sistema de mensagens de estado manipula tarefas de escrita.  

 Para obter mais informações, consulte [introdução aos perfis de certificado](/sccm/protect/deploy-use/introduction-to-certificate-profiles).


### <a name="capture-os-image-account"></a>Conta de imagem do sistema operacional para captura  

 Ao capturar uma imagem de SO, o Configuration Manager utiliza o **conta de imagem de SO capturar** para aceder à pasta onde armazenar as imagens capturadas. Se adicionar o **Capturar imagem do SO** passo à sequência de tarefas, esta conta é necessário.  

 A conta deve ter **leitura** e **escrever** permissões na partilha de rede onde armazenar as imagens capturadas.  

 Se alterar a palavra-passe para a conta no Windows, atualize a sequência de tarefas com a nova palavra-passe. O cliente do Configuration Manager recebe a nova palavra-passe quando a próxima vez que transferir a política de cliente.  

 Se precisar de utilizar esta conta, crie uma conta de utilizador de domínio. Conceder as permissões mínimas para aceder a recursos de rede necessários e utilizá-lo para todas as sequências de tarefas de captura.  

 > [!IMPORTANT]  
 >  Não atribua as permissões de início de sessão interativas a esta conta.  
 >   
 >  Não utilize a conta de acesso de rede para esta conta.  

 Para obter mais informações, consulte [criar uma sequência de tarefas para capturar um sistema operacional](/sccm/osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system).


### <a name="client-push-installation-account"></a>Conta de instalação push do cliente  

 Ao implementar clientes utilizando o método de instalação push do cliente, o site utiliza a **conta de instalação push do cliente** para ligar a computadores e instalar o software de cliente do Configuration Manager. Se não especificar esta conta, o servidor do site tentará utilizar a sua conta de computador.  

 Esta conta tem de ser um membro do local **administradores** grupo nos computadores de cliente de destino. Esta conta não requer **administrador de domínio** direitos.  

 É possível especificar mais do que uma conta de instalação de push de cliente. O Configuration Manager tenta cada um por sua vez, até uma ter êxito.  

> [!TIP]  
>  Se tiver um ambiente do Active Directory grande e precisar de alterar esta conta, utilize o seguinte processo para coordenar com mais eficiência esta atualização de conta: 
> 1. Criar uma nova conta com um nome diferente   
> 2. Adicionar a nova conta à lista de contas de instalação push do cliente no Configuration Manager  
> 3. Permita tempo suficiente para serviços de domínio do Active Directory replicar a nova conta  
> 4. Em seguida, remover a conta antiga do Configuration Manager e serviços de domínio do Active Directory  

> [!IMPORTANT]  
>  Não conceda a esta conta o direito de iniciar sessão localmente.  

 Para obter mais informações, consulte [instalação push do cliente](/sccm/core/clients/deploy/plan/client-installation-methods#client-push-installation).


### <a name="enrollment-point-connection-account"></a>Conta de ligação de ponto de registo  

 O ponto de registo utiliza o **conta de ligação de ponto de registo** para ligar à base de dados do site do Configuration Manager. Ele usa a sua conta de computador por padrão, mas pode configurar uma conta de utilizador. Quando o ponto de inscrição está num domínio não fidedigno do servidor do site, tem de especificar uma conta de utilizador. Esta conta necessita **leitura** e **escrever** acesso para a base de dados do site.  

 Para obter mais informações, consulte [instalar funções do sistema de sites para MDM no local](/sccm/mdm/get-started/install-site-system-roles-for-on-premises-mdm).


### <a name="exchange-server-connection-account"></a>Conta de ligação do Exchange Server  

 O servidor de site utiliza a **conta de ligação do Exchange Server** para ligar ao servidor Exchange especificado. Utiliza esta ligação para localizar e gerir dispositivos móveis que ligam ao Exchange Server. Esta conta necessita de cmdlets do Exchange PowerShell que forneçam as permissões necessárias ao computador do Exchange Server. Para obter mais informações sobre os cmdlets, consulte [gerir dispositivos móveis com o Configuration Manager e o Exchange](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).  


### <a name="management-point-connection-account"></a>Conta de ligação de ponto de gestão  

 O ponto de gestão utiliza o **conta de ligação de ponto de gestão** para ligar à base de dados do site do Configuration Manager. Utiliza esta ligação para enviar e receber informações de clientes. O ponto de gestão utiliza a sua conta de computador por padrão, mas pode configurar uma conta de utilizador. Quando o ponto de gestão está num domínio não fidedigno do servidor do site, tem de especificar uma conta de utilizador.  

 Crie a conta com direitos restritos, a conta local no computador que executa o Microsoft SQL Server.  

> [!IMPORTANT]  
>  Não conceda direitos de início de sessão interativos a esta conta.  


### <a name="multicast-connection-account"></a>Conta de ligação de multicast  

 Utilização de pontos de distribuição preparados para multicast a **conta de ligação de Multicast** ler informações da base de dados do site. O servidor utiliza a sua conta de computador por padrão, mas pode configurar uma conta de utilizador. Quando a base de dados do site estiver numa floresta não fidedigna, tem de especificar uma conta de utilizador. Por exemplo, se seu centro de dados tiver uma rede de perímetro numa floresta que não seja o servidor do site e base de dados do site, utilize esta conta para ler as informações de multicast da base de dados do site.  

 Se tiver esta conta, crie-a como uma com direitos restritos, uma conta local no computador que executa o Microsoft SQL Server.  

> [!IMPORTANT]  
>  Não conceda direitos de início de sessão interativos a esta conta.  

 Para obter mais informações, consulte [utilizar multicast para implementar o Windows através da rede](/sccm/osd/deploy-use/use-multicast-to-deploy-windows-over-the-network).


### <a name="network-access-account"></a>Conta de acesso à rede  

 Utilização de computadores de cliente do **conta de acesso de rede** quando eles não é possível utilizar a respetiva conta de computador local para aceder ao conteúdo em pontos de distribuição. Ele aplica-se principalmente para clientes de grupo de trabalho e computadores de domínios não fidedignos. Esta conta também é utilizada durante a implementação do sistema operacional, quando o computador que está a instalar o sistema operacional ainda não tiver uma conta de computador no domínio.  

> [!Important]  
>  A conta de acesso à rede nunca é utilizada como o contexto de segurança para executar programas, instalar atualizações de software ou executar sequências de tarefas. É utilizado apenas para aceder a recursos da rede.  

 Um cliente do Configuration Manager primeiro tenta utilizar a sua conta de computador para transferir o conteúdo. Se falhar, em seguida, tentará automaticamente a conta de acesso de rede.  

 A partir da versão 1806, um grupo de trabalho ou o cliente do Azure associados ao AD pode aceder de forma segura conteúdos de pontos de distribuição sem a necessidade de uma conta de acesso de rede. Este comportamento inclui cenários de implementação do sistema operacional com uma sequência de tarefas em execução a partir do suporte de dados, o PXE ou o Centro de Software. Para obter mais informações, consulte [avançada HTTP](/sccm/core/plan-design/hierarchy/enhanced-http).<!--1358228,1358278-->

 > [!Note]  
 > Se habilitar **avançada HTTP** para não exigir a conta de acesso de rede, o ponto de distribuição tem de estar a executar o Windows Server 2008 R2 SP1 ou posterior. <!--SCCMDocs-pr issue #2696-->
>  
> Atualizar clientes para, pelo menos, versão 1806 antes de ativar esta funcionalidade. Se permitir apenas **avançada HTTP** ligações, os clientes antigos não podem autenticar através deste método, para que não é possível transferir o pacote de atualização de cliente de um ponto de distribuição. <!--vso2841213-->   

#### <a name="permissions"></a>Permissões

 Conceda a esta conta o menor número possível de permissões ao nível do conteúdo de que o cliente necessita para aceder ao software. A conta deve ter o **aceder a este computador da rede** diretamente no ponto de distribuição. Pode configurar até 10 contas de acesso de rede por site.  

 Crie a conta em qualquer domínio que fornece o acesso necessário a recursos. A conta de acesso de rede tem de incluir sempre um nome de domínio. Segurança de pass-through não é suportada para esta conta. Se existirem pontos de distribuição em vários domínios, crie a conta num domínio fidedigno.  

> [!TIP]  
> Para evitar bloqueios de conta, não altere a palavra-passe numa conta de acesso de rede existente. Em vez disso, crie uma nova conta e configure a nova conta no Configuration Manager. Quando tiver passado o tempo suficiente para todos os clientes receberem os detalhes da nova conta, remova a conta antiga das pastas partilhadas da rede e elimine a conta.  

> [!IMPORTANT]  
>  Não conceda direitos de início de sessão interativos a esta conta.  
>   
>  Não conceda a esta conta o direito de associar computadores ao domínio. Se tiver de associar computadores ao domínio durante uma sequência de tarefas, utilize o [conta de adesão ao domínio de sequência de tarefas](#task-sequence-domain-join-account).  

#### <a name="configure-the-network-access-account"></a>Configurar a conta de acesso de rede  

1.  Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **configuração do Site**e selecione o **Sites** nó. Em seguida, selecione o site.  

2.  Sobre o **configurações** grupo da faixa de opções, selecione **configurar componentes do Site**e escolha **distribuição de Software**.  

3.  Escolha o **conta de acesso à rede** separador. Configurar uma ou mais contas e, em seguida, escolha **OK**.  


### <a name="package-access-account"></a>Conta de acesso do pacote  

 R **conta de acesso a pacote** permite que definir permissões NTFS para especificar os utilizadores e grupos de utilizadores que podem aceder ao conteúdo em pontos de distribuição do pacote. Por predefinição, o Configuration Manager concede acesso apenas às contas de acesso genérico **usuário** e **administrador**. Pode controlar o acesso para computadores cliente com o Windows contas ou grupos adicionais. Dispositivos móveis obtêm sempre o conteúdo de pacote anonimamente, pelo que não utilizam uma conta de acesso do pacote.  

 Por predefinição, quando o Configuration Manager copia os ficheiros de conteúdo para um ponto de distribuição, concede acesso **leitura** acesso local **utilizadores** grupo, e **controlo total** para o local **administradores** grupo. As permissões reais necessárias dependem do pacote. Se tiver clientes em grupos de trabalho ou em florestas não fidedignas, esses clientes utilizam a conta de acesso de rede para acessar o conteúdo do pacote. Certifique-se de que a conta de acesso de rede tem permissões para o pacote utilizando as contas de acesso a pacote definidas.  

 Utilize contas de um domínio que tenham acesso aos pontos de distribuição. Se criar ou alterar a conta após criar o pacote, necessitará de redistribuir o pacote. A atualização do pacote não altera as permissões de NTFS no pacote.  

 Não tem de adicionar a conta de acesso de rede como uma conta de acesso do pacote, porque a associação do **utilizadores** grupo adiciona automaticamente. Restringir a conta de acesso do pacote para apenas a conta de acesso de rede não impede que os clientes ao pacote.  

#### <a name="manage-package-access-accounts"></a>Gerir contas de acesso do pacote  

1.  Na consola do Configuration Manager, escolha **biblioteca de Software**.  

2.  Na **biblioteca de Software** área de trabalho, determinar o tipo de conteúdo para o qual pretende gerir contas de acesso e siga os passos fornecidos:  

    -   **Aplicação**: Expanda **gestão de aplicações**, escolha **aplicativos**e, em seguida, selecione a aplicação para o qual pretende gerir contas de acesso.  

    -   **Pacote**: Expanda **gestão de aplicações**, escolha **pacotes**e, em seguida, selecione o pacote para o qual pretende gerir contas de acesso.  

    -   **Pacote de implementação de atualização de software**: Expanda **atualizações de Software**, escolha **pacotes de implementação**e, em seguida, selecione o pacote de implementação para o qual pretende gerir contas de acesso.  

    -   **Pacote de controladores**: Expanda **sistemas operativos**, escolha **pacotes de controladores**e, em seguida, selecione o pacote de controladores para cujas contas de acesso pretende gerir.  

    -   **Imagem do SO**: Expanda **sistemas operativos**, escolha **imagens do sistema operativo**e, em seguida, selecione a imagem de sistema operativo para o qual pretende gerir contas de acesso.  

    -   **Pacote de atualização de SO**: Expanda **sistemas operativos**, escolha **pacotes de atualização do sistema operativo**e, em seguida, selecione o pacote de atualização de SO para o qual pretende gerir contas de acesso.  

    -   **Imagem de arranque**: Expanda **sistemas operativos**, escolha **imagens de arranque**e, em seguida, selecione a imagem de arranque para o qual pretende gerir contas de acesso.  

3.  O objeto selecionado com o botão direito e, em seguida, escolha **gerir contas de acesso**.  

4.  Na **adicionar conta** diálogo caixa, especifique o tipo de conta que será concedido acesso ao conteúdo e, em seguida, especifique os direitos de acesso associados à conta.  

    > [!NOTE]  
    >  Quando adicionar um nome de utilizador para a conta e do Configuration Manager localiza uma conta de utilizador local e uma conta de utilizador de domínio com esse nome, o Configuration Manager Define direitos de acesso da conta de utilizador de domínio.  


### <a name="reporting-services-point-account"></a>Conta de ponto do Reporting services  
 
 SQL Server Reporting Services utiliza o **conta de ponto do Reporting services** para recuperar os dados para relatórios do Configuration Manager a partir da base de dados do site. A conta de utilizador do Windows e a palavra-passe que especificar são encriptadas e armazenadas na base de dados do SQL Server Reporting Services.  

 > [!NOTE]  
 > A conta que especificar tem de ter **iniciar sessão localmente** permissões no computador que aloja a base de dados do SQL Reporting Services.

 Para obter mais informações, consulte [introdução aos relatórios](/sccm/core/servers/manage/introduction-to-reporting).


### <a name="remote-tools-permitted-viewer-accounts"></a>Contas de Visualizador permitidas por ferramentas remotas  

 As contas que especificar como **Visualizadores Autorizados** para o controlo remoto são uma lista de utilizadores autorizados a utilizar a funcionalidade de ferramentas remotas em clientes.  

Para obter mais informações, consulte [introdução ao controlo remoto](/sccm/core/clients/manage/remote-control/introduction-to-remote-control).


### <a name="site-installation-account"></a>Conta de instalação do site
<!--SCCMDocs issue #572--> Utilize uma conta de utilizador de domínio para iniciar sessão no servidor onde executar a configuração do Configuration Manager e instalar um novo site.

Esta conta requer os seguintes direitos de:  

- **Administrador** nos seguintes servidores:
    - O servidor do site  
    - Cada servidor que aloja a base de dados do site  
    - Cada instância do fornecedor de SMS para o site  

- **Administrador do sistema** na instância do SQL Server que aloja a base de dados do site  

Configuração do Configuration Manager adiciona automaticamente esta conta para o [Admins de SMS](#sms-admins) grupo.

Após a instalação, esta conta é o único utilizador com direitos para a consola do Configuration Manager. Se precisar de remover esta conta, certifique-se de adicionar os seus direitos para outro utilizador pela primeira vez.

Quando expande um site autónomo para incluir um site de administração central, esta conta necessita **administrador total** ou **administrador de infraestrutura** de direitos de administração baseada em funções no o site primário autónomo.


### <a name="site-system-installation-account"></a>Conta de instalação do sistema de sites  

 O servidor de site utiliza a **conta de instalação do sistema de sites** para instalar, reinstalar, desinstalar e configurar sistemas de sites. Se configurar o sistema de sites para exigir que o servidor do site inicie ligações a este sistema de sites, do Configuration Manager também utiliza esta conta para extrair os dados do sistema de site após a instalação do sistema de sites e de quaisquer funções. Cada sistema de sites pode ter uma conta de instalação diferente, mas pode configurar a conta de uma só instalação para gerir todas as funções de nesse sistema de sites.  

 Esta conta requer permissões administrativas locais nos sistemas de site de destino. Além disso, esta conta tem de ter **aceder a este computador da rede** na política de segurança nos sistemas de site de destino.  

 > [!TIP]  
 >  Se tiver muitos controladores de domínio e essas contas são usadas em vários domínios, antes de configurar o sistema de sites, verifique que o Active Directory foi replicada estas contas.  
 >   
 >  Quando especificar uma conta local em cada sistema de sites para serem geridos, esta configuração é mais segura do que usando contas de domínio. Limita os danos que os invasores podem fazer se a conta for comprometida. No entanto, as contas de domínio são mais fácil de gerenciar. Considere o compromisso entre segurança e administração eficaz.  


### <a name="site-system-proxy-server-account"></a>Conta de proxy de servidor de sistema de sites
<!--SCCMDocs issue #648--> O seguinte uso de funções do sistema de sites do **conta de servidor de proxy do sistema de sites** para aceder à internet através de um proxy de servidor ou de firewall que necessite de acesso autenticado:

- Ponto de sincronização do Asset Intelligence
- Conector do Exchange Server
- Ponto de ligação de serviço
- Ponto de atualização de software

> [!IMPORTANT]  
>  Especifique uma conta que tenha o menor número possível de permissões para a firewall ou o servidor proxy necessário.  

 Para obter mais informações, consulte [suporte de servidor de Proxy](/sccm/core/plan-design/network/proxy-server-support).


### <a name="smtp-server-connection-account"></a>Conta de ligação do servidor de SMTP  

 O servidor de site utiliza a **conta de ligação do servidor de SMTP** para enviar alertas por e-mail quando o servidor SMTP necessita de acesso autenticado.  

> [!IMPORTANT]  
>  Especifique uma conta que tenha o menor número possível de permissões para enviar mensagens de correio eletrónico.  

 Para obter mais informações, consulte [utilizar alertas e o estado do sistema](/sccm/core/servers/manage/use-alerts-and-the-status-system).


### <a name="software-update-point-connection-account"></a>Conta de ligação de ponto de atualização de software  

 O servidor de site utiliza a **conta de ligação de ponto de atualização de Software** para os seguintes serviços de atualização de software dois:  

-   Windows Server Update Services (WSUS), que configura definições como definições de produto, classificações e definições a montante.  

-   WSUS Synchronization Manager, que pede a sincronização a um servidor WSUS a montante ou ao Microsoft Update.  

O [conta de instalação do sistema de sites](#site-system-installation-account) pode instalar componentes para atualizações de software, mas ele não é possível efetuar funções específicas de atualização de software no ponto de atualização de software. Se não conseguir utilizar a conta de computador do servidor de site para esta funcionalidade, uma vez que o ponto de atualização de software estiver numa floresta não fidedigna, tem de especificar esta conta para além da conta de instalação do sistema de sites.  

Esta conta tem de ser um administrador local no computador onde instala o WSUS. Também tem de ser parte do local **administradores WSUS** grupo.  

Para obter mais informações, consulte [planear atualizações de software](/sccm/sum/plan-design/plan-for-software-updates).


### <a name="source-site-account"></a>Conta de site de origem  

 O processo de migração utiliza a **conta de site de origem** para aceder ao fornecedor de SMS do site de origem. Esta conta precisa de permissões de **Leitura** a objetos de site no site de origem para recolher dados para tarefas de migração.  

 Se tiver pontos de distribuição do Configuration Manager 2007 ou sites secundários com pontos de distribuição colocalizados, ao atualizar para pontos de distribuição do Configuration Manager (ramo atual), esta conta também tem de ter **elimine**permissões para o **Site** classe. Esta permissão é remover com sucesso o ponto de distribuição a partir do site do Configuration Manager 2007 durante a atualização.  

> [!NOTE]  
>  Tanto a conta de site de origem e o [conta de base de dados do site de origem](#source-site-database-account) são identificados como **Gestor de migração** no **contas** nó do  **Administração** área de trabalho na consola do Configuration Manager.  

 Para obter mais informações, consulte [migrar dados entre hierarquias](https://docs.microsoft.com/en-us/sccm/core/migration/migrate-data-between-hierarchies).


### <a name="source-site-database-account"></a>Conta de base de dados do site de origem  

 O processo de migração utiliza a **conta de base de dados do site de origem** para acessar o banco de dados do SQL Server para o site de origem. Para recolher dados de base de dados do SQL Server do site de origem, a conta de base de dados do site de origem tem de ter o **leitura** e **Execute** permissões para do SQL Server da base de dados o site de origem.  

 Se utilizar a conta de computador do Configuration Manager (ramo atual), certifique-se de que todas as seguintes são verdadeiras para esta conta:  
   
 - É um membro do **Distributed COM-usuários** grupo de segurança no mesmo domínio que o site do Configuration Manager 2007  
 - É um membro do **Admins de SMS** grupo de segurança  
 - Ele tem o **leitura** permissão a todos os objetos do Configuration Manager 2007  

> [!NOTE]  
>  Tanto a conta de site de origem e o [conta de base de dados do site de origem](#source-site-database-account) são identificados como **Gestor de migração** no **contas** nó do  **Administração** área de trabalho na consola do Configuration Manager.  

 Para obter mais informações, consulte [migrar dados entre hierarquias](https://docs.microsoft.com/en-us/sccm/core/migration/migrate-data-between-hierarchies).


### <a name="task-sequence-domain-join-account"></a>Conta de associação de domínio de sequência de tarefas 

 A configuração do Windows utiliza a **conta de adesão ao domínio de sequência de tarefas** para associar um computador com imagem recentemente duplicada a um domínio. Esta conta é necessária para o [associar domínio ou grupo de trabalho](/sccm/osd/understand/task-sequence-steps#BKMK_JoinDomainorWorkgroup) passo de sequência de tarefas com o **aderir a um domínio** opção. Esta conta também pode ser configurada com o [aplicar definições de rede](/sccm/osd/understand/task-sequence-steps#BKMK_ApplyNetworkSettings) passo, mas não é necessária.  

 Esta conta necessita da **ingresso no domínio** diretamente no domínio de destino.  

> [!TIP]  
>  Criar uma conta de utilizador de domínio com as permissões mínimas para aderir ao domínio e utilizá-lo para todas as sequências de tarefas.  

> [!IMPORTANT]  
>  Não atribua as permissões de início de sessão interativas a esta conta.  
>   
>  Não utilize a conta de acesso de rede para esta conta.  


### <a name="task-sequence-network-folder-connection-account"></a>Conta de ligação de pasta de rede de sequência de tarefas  

 O motor de sequência de tarefas utiliza a **conta de ligação da pasta de rede de sequência de tarefas** para ligar a uma pasta partilhada na rede. Esta conta é necessária para o [ligar à pasta de rede](/sccm/osd/understand/task-sequence-steps#BKMK_ConnectToNetworkFolder) passo de sequência de tarefas.  

 Esta conta requer permissões para aceder à pasta partilhada especificada. Tem de ser uma conta de utilizador de domínio.  

> [!TIP]  
>  Criar uma conta de utilizador de domínio com as permissões mínimas para aceder a recursos de rede necessários e utilizá-lo para todas as sequências de tarefas.  

> [!IMPORTANT]  
>  Não atribua as permissões de início de sessão interativas a esta conta.  
>   
>  Não utilize a conta de acesso de rede para esta conta.  


### <a name="task-sequence-run-as-account"></a>Conta run as de sequência de tarefas  

 O motor de sequência de tarefas utiliza a **uma conta run as de sequência de tarefas** para executar linhas de comandos com credenciais diferentes da conta de sistema Local. Esta conta é necessária para o [executar linha de comandos](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) passo de sequência de tarefas com a opção **executar este passo de como a seguinte conta**.  

 Configure a conta ter as permissões mínimas necessárias para executar a linha de comandos que especificou na sequência de tarefas. A conta requer direitos de início de sessão interativos. Normalmente requer a capacidade de instalar software e aceder aos recursos de rede.  

> [!IMPORTANT]  
>  Não utilize a conta de acesso de rede para esta conta.  
>   
>  Nunca torne a conta do administrador de domínio.  
>   
>  Nunca configure perfis itinerantes para esta conta. Quando a sequência de tarefas é executada, transfere o perfil itinerante para a conta. Isso deixa o perfil vulnerável a acesso no computador local.  
>   
>  Limite o âmbito da conta. Por exemplo, crie contas para cada sequência de tarefas run as de sequência de tarefas diferente. Em seguida, se uma conta for comprometida, apenas os computadores de cliente aos quais essa conta tem acesso sejam comprometidos.  
>   
>  Se a linha de comandos exigir acesso administrativo no computador, considere criar uma conta de administrador local apenas para esta conta em todos os computadores que executam a sequência de tarefas. Elimine a conta quando já não precisam dele.  

