---
title: Versões suportadas do SQL Server
titleSuffix: Configuration Manager
description: Obtenha os requisitos de versão e a configuração do SQL Server para alojar um Gestor de configuração da base de dados do site.
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 35e237b6-9f7b-4189-90e7-8eca92ae7d3d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 43093f38a2769c46d3d96a51afbf47f33ed38b51
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53423801"
---
# <a name="supported-sql-server-versions-for-configuration-manager"></a>Versões suportadas do SQL Server para o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Cada site do System Center Configuration Manager requer uma versão do SQL Server e uma configuração para alojar a base de dados suportados.  



##  <a name="bkmk_Instances"></a> Instâncias e localizações do SQL Server  
 
### <a name="central-administration-site-and-primary-sites"></a>Site de administração central e sites primários  
 A base de dados do site tem de utilizar uma instalação completa do SQL Server.  

 SQL Server pode estar localizado em:  

-   O computador do servidor do site.  
-   Um computador remoto do servidor do site.  

São suportadas as seguintes instâncias:  

-   A instância predefinida ou nomeada do SQL Server.  
-   Configurações de várias instâncias.  
-   Um cluster do SQL Server. Ver [utilizar um cluster do SQL Server para alojar a base de dados do site](/sccm/core/servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database).
-   Um grupo de Disponibilidade AlwaysOn do SQL Server. Para obter mais informações, consulte [SQL Server AlwaysOn para uma base de dados do site de elevada disponibilidade](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).


### <a name="secondary-sites"></a>Sites secundários  
 A base de dados do site pode utilizar a instância predefinida de uma instalação completa do SQL Server ou SQL Server Express.  

 SQL Server tem de estar localizado no computador do servidor do site.  


### <a name="limitations-to-support"></a>Limitações para suportar   
 Não são suportadas as seguintes configurações:
 -   Um cluster do SQL Server numa configuração de cluster de balanceamento de carga na rede (NLB)
 -   Um cluster do SQL Server num Cluster Shared Volume (CSV)
 -   Base de dados do SQL Server espelhamento de tecnologia e a replicação ponto-a-ponto

Replicação transacional do SQL Server é suportada apenas para replicar objetos para pontos de gestão que estão configurados para utilizar [réplicas de base de dados](/sccm/core/servers/deploy/configure/database-replicas-for-management-points).  



##  <a name="bkmk_SQLVersions"></a> Versões suportadas do SQL Server  
 Numa hierarquia com múltiplos sites, cada site pode utilizar diferentes versões do SQL Server para alojar a base de dados do site. Desde que os itens seguintes são verdadeiros:
 -  O Configuration Manager suporta as versões do SQL Server que utilizar.
 -  Versões do SQL Server que utiliza permanecem no suporte pela Microsoft.
 -  SQL Server suporta a replicação entre as duas versões do SQL Server. Por exemplo, SQL Server não suporta a replicação entre o SQL Server 2008 R2 e o SQL Server 2016. Para obter mais informações, consulte [funcionalidades na replicação do SQL Server preteridas](https://docs.microsoft.com/sql/relational-databases/replication/deprecated-features-in-sql-server-replication).



 Salvo especificação em contrário, as seguintes versões do SQL Server são suportadas com todas as versões de Active Directory do Configuration Manager. Se o suporte para uma nova versão do SQL Server ou o pacote de serviço é adicionado, a versão do Configuration Manager que adiciona esse suporte é indicada. Da mesma forma, se o suporte é preterido, procure-se para obter detalhes sobre as versões afetadas do Configuration Manager.   

Suporte para um pacote de serviço específico do SQL Server inclui as atualizações cumulativas, a menos que eles interromper a compatibilidade com versões anteriores para a versão de pacote de serviço de base. Quando não é observado nenhuma versão de service pack, o suporte destina-se a versão do SQL Server sem nenhum service pack. No futuro, se um service pack é lançado para uma versão do SQL Server, uma declaração de suporte separado é declarada para a nova versão do pacote de serviço é suportada.


> [!IMPORTANT]  
>  Quando utilizar o SQL Server Standard para a base de dados no site de administração central, limita o número total de clientes que uma hierarquia consegue suportar. Consulte [Dimensionamento e números da escala](/sccm/core/plan-design/configs/size-and-scale-numbers).

### <a name="sql-server-2017-standard-enterprise"></a>SQL Server 2017: Standard, Enterprise  
Pode utilizar esta versão do SQL Server, com um mínimo de [versão de atualização cumulativa 2](https://support.microsoft.com/help/4052574), que começam com [Configuration Manager versão 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710) para os seguintes sites: 

- Um site de administração central  
- Um site primário  
- Um site secundário  
  <!--SMS.498506-->

### <a name="sql-server-2016-sp2-standard-enterprise"></a>O SQL Server 2016 SP2: Standard, Enterprise  
<!--514985--> Pode utilizar esta versão do SQL Server sem versão de atualização cumulativa mínima para os seguintes sites:  

-   Um site de administração central  
-   Um site primário  
-   Um site secundário  

### <a name="sql-server-2016-sp1-standard-enterprise"></a>SQL Server 2016 SP1: Standard, Enterprise  
Pode utilizar esta versão do SQL Server sem versão de atualização cumulativa mínima para os seguintes sites:  

-   Um site de administração central  
-   Um site primário  
-   Um site secundário  

### <a name="sql-server-2016-standard-enterprise"></a>SQL Server 2016: Standard, Enterprise  
Pode utilizar esta versão do SQL Server sem versão de atualização cumulativa mínima para os seguintes sites:  

-   Um site de administração central  
-   Um site primário  
-   Um site secundário  

### <a name="sql-server-2014-sp3-standard-enterprise"></a>SP3 do SQL Server 2014: Standard, Enterprise  
Pode utilizar esta versão do SQL Server sem versão de atualização cumulativa mínima para os seguintes sites:  

-   Um site de administração central  
-   Um site primário  
-   Um site secundário

### <a name="sql-server-2014-sp2-standard-enterprise"></a>SQL Server 2014 SP2: Standard, Enterprise  
Pode utilizar esta versão do SQL Server sem versão de atualização cumulativa mínima para os seguintes sites:  

-   Um site de administração central  
-   Um site primário  
-   Um site secundário

### <a name="sql-server-2014-sp1-standard-enterprise"></a>SQL Server 2014 SP1: Standard, Enterprise  
 Pode utilizar esta versão do SQL Server sem versão de atualização cumulativa mínima para os seguintes sites:  

-   Um site de administração central  
-   Um site primário  
-   Um site secundário

### <a name="sql-server-2012-sp4-standard-enterprise"></a>SQL Server 2012 SP4: Standard, Enterprise  
 Pode utilizar esta versão do SQL Server sem versão de atualização cumulativa mínima para os seguintes sites:  

-   Um site de administração central  
-   Um site primário  
-   Um site secundário  

### <a name="sql-server-2012-sp3-standard-enterprise"></a>SQL Server 2012 SP3: Standard, Enterprise  
 Pode utilizar esta versão do SQL Server sem versão de atualização cumulativa mínima para os seguintes sites:  

-   Um site de administração central  
-   Um site primário  
-   Um site secundário  

### <a name="sql-server-2008-r2-sp3-standard-enterprise-datacenter"></a>SQL Server 2008 R2 SP3: Standard, Enterprise e Datacenter     
  Não é suportada nesta versão do SQL Server. Para obter mais informações, consulte [preterido suporte para versões do SQL Server como uma base de dados do site](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-support-for-sql-server-versions-as-a-site-database).  

### <a name="sql-server-2017-express"></a>Express do SQL Server 2017   
Pode utilizar esta versão do SQL Server, com um mínimo de [versão de atualização cumulativa 2](https://support.microsoft.com/help/4052574), que começam com [Configuration Manager versão 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710) para os seguintes sites:
-   Um site secundário <!--SMS.498506-->

### <a name="sql-server-2016-express-sp2"></a>SP2 Express do SQL Server 2016  
Pode utilizar esta versão do SQL Server sem versão de atualização cumulativa mínima para os seguintes sites:
-   Um site secundário

### <a name="sql-server-2016-express-sp1"></a>SQL Server 2016 Express SP1  
Pode utilizar esta versão do SQL Server sem versão de atualização cumulativa mínima para os seguintes sites:
-   Um site secundário

### <a name="sql-server-2016-express"></a>SQL Server 2016 Express
Pode utilizar esta versão do SQL Server sem versão de atualização cumulativa mínima para os seguintes sites:
-   Um site secundário

### <a name="sql-server-2014-express-sp3"></a>SP3 Express do SQL Server 2014   
Pode utilizar esta versão do SQL Server sem versão de atualização cumulativa mínima para os seguintes sites:  

-   Um site secundário  

### <a name="sql-server-2014-express-sp2"></a>SQL Server 2014 Express SP2   
Pode utilizar esta versão do SQL Server sem versão de atualização cumulativa mínima para os seguintes sites:  

-   Um site secundário  

### <a name="sql-server-2014-express-sp1"></a>SQL Server 2014 Express SP1   
 Pode utilizar esta versão do SQL Server sem versão de atualização cumulativa mínima para os seguintes sites:  

-   Um site secundário  

### <a name="sql-server-2012-express-sp3"></a>SQL Server 2012 Express SP3  
Pode utilizar esta versão do SQL Server sem versão de atualização cumulativa mínima para os seguintes sites:  

-   Um site secundário  



##  <a name="bkmk_SQLConfig"></a> Configurações necessárias para o SQL Server  
 O seguinte é necessário para todas as instalações do SQL Server que utiliza para uma base de dados do site (incluindo o SQL Server Express). Quando o Configuration Manager instala o SQL Server Express como parte de uma instalação de site secundário, estas configurações são criadas automaticamente para.  

### <a name="sql-server-architecture-version"></a>Versão de arquitetura do SQL Server  
 O Configuration Manager requer uma versão de 64 bits do SQL Server para alojar a base de dados do site.  

### <a name="database-collation"></a>Agrupamento de base de dados  
 Em cada site, a instância do SQL Server que é utilizado para o site e a base de dados do site tem de utilizar o seguinte agrupamento: **SQL_Latin1_General_CP1_CI_AS**.  

 O Configuration Manager suporta duas exceções a este agrupamento para cumprir os padrões definidos na GB18030 para utilização na China. Para obter mais informações, consulte [suporte internacional](/sccm/core/plan-design/hierarchy/international-support).  

### <a name="database-compatibility-level"></a>Nível de compatibilidade de base de dados   
 O Configuration Manager requer que o nível de compatibilidade da base de dados do site é não menos do que o menor versão suportada do SQL Server para a sua versão do Configuration Manager. Por exemplo, a partir da versão 1702, tem de ter uma [nível de compatibilidade de base de dados](https://docs.microsoft.com/sql/relational-databases/databases/view-or-change-the-compatibility-level-of-a-database) igual ou superior para 110. <!-- SMS.506266--> 

### <a name="sql-server-features"></a>Funcionalidades do SQL Server  
 Só é necessária a funcionalidade **Serviços de Motor da Base de Dados** para cada servidor do site.  

 Replicação de base de dados do Configuration Manager não exige a **replicação do SQL Server** funcionalidade. No entanto, esta configuração de SQL Server é necessária quando utiliza [réplicas para pontos de gestão de base de dados](/sccm/core/servers/deploy/configure/database-replicas-for-management-points).  

### <a name="windows-authentication"></a>Autenticação do Windows  
 O Configuration Manager requer **autenticação do Windows** para validar as ligações à base de dados.  

### <a name="sql-server-instance"></a>Instância do SQL Server  
 Utilize uma instância dedicada do SQL Server para cada site. A instância pode ser um **instância nomeada** ou o **instância predefinida**.  

### <a name="sql-server-memory"></a>Memória do SQL Server  
 Reserve memória para o SQL Server, com o SQL Server Management Studio e definindo a **memória de servidor mínima** em **opções de memória de servidor**. Para obter mais informações sobre como configurar esta definição, consulte [opções de configuração de servidor de memória do SQL Server](https://docs.microsoft.com/sql/database-engine/configure-windows/server-memory-server-configuration-options).  

-   **Para um servidor de base de dados que está instalado no mesmo computador que o servidor do site**: Limite a memória do SQL Server para 50 a 80 por cento da memória de sistema acessível disponível.  

-   **Para um servidor de base de dados dedicado (remoto a partir do servidor do site)**: Limite a memória do SQL Server para 80 a 90 por cento da memória de sistema acessível disponível.  

-   **Para uma memória de reserva para o conjunto de memória intermédia de cada instância do SQL Server em utilização**:  

    -   Para um site de administração central: Defina um mínimo de 8 gigabytes (GB).  
    -   Para um site primário: Defina um mínimo de 8 gigabytes (GB).  
    -   Para um site secundário: Defina um mínimo de 4 gigabytes (GB).  

### <a name="sql-nested-triggers"></a>Acionadores aninhados SQL  
 Aninhados SQL acionadores tem de estar ativados. Para obter mais informações, consulte [Configure a opção de configuração do servidor de acionadores aninhados](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option) 

### <a name="sql-server-clr-integration"></a>Integração de CLR do SQL Server  
  A base de dados de sites necessita do tempo de execução de idioma comum (CLR) do SQL Server para ser ativada. Esta opção é ativada automaticamente quando instala o Configuration Manager. Para obter mais informações sobre o CLR, consulte [introdução à integração de CLR do SQL Server](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/introduction-to-sql-server-clr-integration).  



##  <a name="bkmk_optional"></a> Configurações necessárias para o SQL Server  
 As seguintes configurações são opcionais para cada base de dados que utiliza uma instalação completa do SQL Server.  

### <a name="sql-server-service"></a>Serviço do SQL Server  
 Pode configurar o serviço do SQL Server para executar utilizando:  

-   R *utilizador de domínio de direitos baixos* conta:  

    -   Esta configuração é uma prática recomendada e pode implicar a registar manualmente o nome principal de serviço (SPN) para a conta.  

-   O **sistema local** conta do computador que executa o SQL Server:  

    -   Utilize a conta de sistema local para simplificar o processo de configuração.  
    -   Quando utiliza a conta sistema local, o Configuration Manager regista automaticamente o SPN do serviço do SQL Server.  
    -   Com a conta sistema local para o serviço do SQL Server não é uma prática recomendada do SQL Server.  

Quando o computador a executar o SQL Server não utiliza a sua conta do sistema local para executar o serviço SQL Server, configure o SPN da conta que executa o serviço SQL Server nos serviços de domínio do Active Directory. (Quando é utilizada a conta de sistema, o SPN é registrado automaticamente para.)

Para obter informações sobre SPNs para a base de dados do site, consulte [gerir o SPN para o servidor de base de dados do site](/sccm/core/servers/manage/modify-your-infrastructure#bkmk_SPN).  

Para obter informações sobre como alterar a conta que é utilizada pelo serviço do SQL Server, consulte [SCM serviços - alterar a conta de arranque do serviço](https://docs.microsoft.com/sql/database-engine/configure-windows/scm-services-change-the-service-startup-account).  

### <a name="sql-server-reporting-services"></a>Serviços de Relatórios do SQL Server  
SQL Server Reporting Services é necessário para instalar um ponto do reporting services que lhe permita executar relatórios.  

> [!IMPORTANT]  
> Depois de atualizar o SQL Server de uma versão anterior, poderá ver o erro seguinte:  *Report Builder não existe*.  
> Para resolver este erro, terá de reinstalar a função de sistema de sites de ponto do reporting services.  

### <a name="sql-server-ports"></a>Portas do SQL Server  
Para comunicação com o motor de base de dados do SQL Server e para a replicação entre sites, pode utilizar as configurações de porta do SQL Server predefinida ou especificar portas personalizadas:  

-   **Comunicações entre sites** utilizar o SQL Server Service Broker, que utiliza a porta TCP 4022 por predefinição.  
-   **As comunicações** entre o motor de base de dados do SQL Server e o sistema de sites do Configuration Manager várias funções de utilizam a porta TCP 1433, por predefinição. As seguintes funções do sistema de sites comunicam diretamente com a base de dados do SQL Server:  

    -   Ponto de gestão  
    -   Computador do Fornecedor de SMS  
    -   Ponto do Reporting Services  
    -   Servidor do site  

Quando um computador a executar o SQL Server aloja bases de dados de mais de um site, cada base de dados tem de utilizar uma instância separada do SQL Server. Além disso, cada instância tem de ser configurada para utilizar um conjunto exclusivo de portas.  

> [!WARNING]  
>  O Configuration Manager não suporta portas dinâmicas. Uma vez que, por predefinição, as instâncias nomeadas de SQL Server utilizam portas dinâmicas para ligações ao motor da base de dados, quando utilizar uma instância nomeada tem de configurar manualmente a porta estática que pretende utilizar para comunicação entre sites.  

Se tiver uma firewall ativada no computador que está a executar o SQL Server, certifique-se de que está configurado para permitir as portas que estão a ser utilizadas pela sua implementação e quaisquer localizações na rede entre computadores que comunicam com o SQL Server.  

Para obter um exemplo de como configurar o SQL Server para utilizar uma porta específica, consulte [configurar um servidor para escutar numa porta TCP específica](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port).  



## <a name="upgrade-options-for-sql-server"></a>Opções de atualização para o SQL Server

Se precisar de atualizar a sua versão do SQL Server, utilize um dos seguintes métodos, de fácil mais complexas:  

- [Atualizar o SQL Server no local](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#a-namebkmksupconfigupgradedbsrva-upgrade-sql-server-on-the-site-database-server) (recomendado)  

- Instalar uma nova versão do SQL Server num novo computador e, em seguida [utilize a opção de mover base de dados](/sccm/core/servers/manage/modify-your-infrastructure#a-namebkmkdbconfiga-modify-the-site-database-configuration) de configuração do Configuration Manager para apontar o seu servidor do site para o novo SQL Server  

- Uso [cópia de segurança e recuperação](/sccm/protect/understand/backup-and-recovery). A utilização de cópia de segurança e recuperação para um cenário de atualização do SQL é suportada. Pode ignorar o requisito de controle de versão do SQL ao revisar [considerações antes de recuperar um site](/sccm/protect/understand/recover-sites#considerations-before-recovering-a-site). 
