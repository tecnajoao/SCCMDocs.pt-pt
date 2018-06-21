---
title: Atualizar infraestrutura no local
titleSuffix: Configuration Manager
description: Saiba como atualizar a infraestrutura, tais como o SQL Server e o SO dos sistemas de sites.
ms.date: 05/23/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8ca970dd-e71c-404f-9435-d36e773a0db2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: dc433d63eb647ef7a0a88ada212f949783ac25c0
ms.sourcegitcommit: 4b8afbd08ecf8fd54950eeb630caf191d3aa4767
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 06/21/2018
ms.locfileid: "34474256"
---
# <a name="upgrade-on-premises-infrastructure-that-supports-system-center-configuration-manager"></a>Atualizar a infraestrutura no local que suporta o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize as informações neste artigo para o ajudar a atualizar a infraestrutura de servidor que executa o Configuration Manager.  

 - Se pretender *atualizar* de uma versão anterior do Configuration Manager para System Center Configuration Manager, o ramo atual, consulte [atualizar para o System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager).

- Se pretender *atualizar* o System Center Configuration Manager, o ramo atual, a infraestrutura para uma nova versão, consulte [atualizações para o System Center Configuration Manager](/sccm/core/servers/manage/updates).



##  <a name="BKMK_SupConfigUpgradeSiteSrv"></a> Atualizar o sistema operativo dos sistemas de sites  
 O Configuration Manager suporta a atualização no local do sistema operativo (SO) dos servidores que alojam um servidor de site e dos servidores remotos que alojar qualquer função de sistema de sites, nas seguintes situações:  

-   Atualização no local para um service pack posterior do Windows Server se o nível do Windows continua a ser suportado pelo Configuration Manager.  
-   Atualização no local de:
    - Windows Server 2012 R2 para Windows Server 2016 ([ver detalhes adicionais](#bkmk_2016)).
    - Windows Server 2012 para o Windows Server 2016 ([ver detalhes adicionais](#bkmk_2016)).
    - Windows Server 2012 para o Windows Server 2012 R2 ([ver detalhes adicionais](#bkmk_2012r2)).
    - Windows Server 2008 R2 para o Windows Server 2012 R2 ([ver detalhes adicionais](#bkmk_from2008r2).

    > [!WARNING]  
    >  Antes de atualizar para um SO diferente, *tem de desinstalar o WSUS* do servidor. Pode manter o SUSDB e reattach-lo assim que o WSUS é reinstalado. Para obter mais informações sobre este passo crítico, consulte a secção "Funcionalidades novas e alteradas" [descrição geral do Windows Server Update Services](https://technet.microsoft.com/library/hh852345.aspx) na documentação do Windows Server.  

Para atualizar um servidor, utilize os procedimentos de atualização fornecidos pelo sistema operativo que estiver a atualizar a. Consulte os artigos seguintes:
  -  [Atualizar opções para o Windows Server 2012 R2](https://technet.microsoft.com/library/dn303416.aspx) na documentação do Windows Server.  
  - [Opções de atualização e a conversão para o Windows Server 2016](/windows-server/get-started/supported-upgrade-paths) na documentação do Windows Server.

### <a name="bkmk_2016"></a>  Atualizar o Windows Server 2012 ou Windows Server 2012 R2 para 2016
Quando atualizar o Windows Server 2012 ou Windows Server 2012 R2 para Windows Server 2016, situações seguintes:


#### <a name="before-upgrade"></a>Antes da atualização  
-   Remova o cliente do System Center Endpoint Protection (SCEP). Windows Server 2016 tem o Windows Defender incorporada, que substitui o cliente SCEP. A presença do cliente SCEP pode impedir uma atualização ao Windows Server 2016.
-   Remova a função WSUS do servidor se estiver instalado. Pode manter o SUSDB e reattach-lo assim que o WSUS é reinstalado.

#### <a name="after-upgrade"></a>Após a atualização   
-   Certifique-se de que o Windows Defender estiver ativado, definido para o início automático e em execução.
-   Certifique-se de que os seguintes serviços do Configuration Manager em execução:
  -     SMS_EXECUTIVE
  -     SMS_SITE_COMPONENT_MANAGER


-   Certifique-se a **ativação de processos do Windows** e **WWW/W3svc** serviços estão ativado, definido para início automático e em execução para que as seguintes funções de sistema de sites (estes serviços estão desativados durante a atualização):
  -     Servidor do site
  -     Ponto de gestão
  -     Ponto de serviço Web do Catálogo de Aplicações
  -     Ponto de site do Catálogo de Aplicações

-   Certifique-se de que cada servidor que aloja uma função de sistema de sites continua a corresponder a todos os o [pré-requisitos para funções do sistema de sites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) que são executadas nesse servidor. Por exemplo, poderá ter de reinstalar o BITS, o WSUS, ou configurar definições específicas do IIS.

-   Depois de restaurar os pré-requisitos em falta, reinicie o servidor mais uma vez para garantir que os serviços são iniciadas e operacional.

-   Se estiver a atualizar o servidor de site primário, em seguida, [executar uma reposição do site](/sccm/core/servers/manage/modify-your-infrastructure#bkmk_reset).

#### <a name="known-issue-for-remote-configuration-manager-consoles"></a>Problema conhecido para consolas remotas do Configuration Manager   
Depois de atualizar o servidor do site ou um servidor que aloja uma instância de SMS_Provider para Windows Server 2016, os utilizadores administrativos poderão não conseguir ligar uma consola do Configuration Manager para o site. Para contornar este problema, tem de restaurar manualmente as permissões para o grupo de Admins de SMS no WMI. Tem de ser definidas permissões no servidor do site e, em cada servidor remoto que aloja uma instância do SMS_Provider:

1. Nos servidores aplicáveis, abra a consola de gestão da Microsoft (MMC) e adicione o snap-in **controlo WMI**e, em seguida, selecione **computador Local**.
2. Na MMC, abra o **propriedades** de **controlo WMI (Local)** e selecione o **segurança** separador.
3. Expandir a árvore abaixo raiz, selecione o **SMS** nó e, em seguida, escolha **segurança**.  Certifique-se a **Admins de SMS** grupo tem as seguintes permissões:
  -     Ativar conta
  -     Ativar remoto
4. No **separador segurança** abaixo o **SMS** nó, selecione o **site_&lt;sitecode**> nó e, em seguida, escolha **segurança**. Certifique-se a **Admins de SMS** grupo tem as seguintes permissões:
  -   Executar métodos
  -   Escrita de fornecedor
  -   Ativar conta
  -   Ativar remoto
5. Guarde as permissões para restaurar o acesso para a consola do Configuration Manager.


### <a name="bkmk_2012r2"></a> Windows Server 2012 para o Windows Server 2012 R2

#### <a name="before-upgrade"></a>Antes da atualização  
-   Remova a função WSUS do servidor se estiver instalado. Pode manter o SUSDB e reattach-lo assim que o WSUS é reinstalado.

#### <a name="after-upgrade"></a>Após a atualização  
  - Certifique-se de que o serviço de implementação do Windows está iniciado e em execução para as seguintes funções de sistema de sites (este serviço for parado durante a atualização):
    - Servidor do site
    - Ponto de gestão
    - Ponto de serviço Web do Catálogo de Aplicações
    - Ponto de site do Catálogo de Aplicações

  -     Certifique-se a **ativação de processos do Windows** e **WWW/W3svc** serviços estão ativado, definido para início automático e em execução para que as seguintes funções de sistema de sites (estes serviços estão desativados durante a atualização):
    -   Servidor do site
    -   Ponto de gestão
    -   Ponto de serviço Web do Catálogo de Aplicações
    -   Ponto de site do Catálogo de Aplicações


  -     Certifique-se de que cada servidor que aloja uma função de sistema de sites continua a corresponder a todos os o [pré-requisitos para funções do sistema de sites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) que são executadas nesse servidor. Por exemplo, poderá ter de reinstalar o BITS, o WSUS, ou configurar definições específicas do IIS.

  Depois de restaurar os pré-requisitos em falta, reinicie o servidor mais uma vez para garantir que os serviços são iniciadas e operacional.

### <a name="bkmk_from2008r2"></a>  Atualizar o Windows Server 2008 R2 para o Windows Server 2012 R2
Neste cenário de atualização do SO tem as seguintes condições:  

#### <a name="before-upgrade"></a>Antes da atualização  
-   Desinstale o WSUS 3.2.  
    Antes de atualizar um servidor de SO para o Windows Server 2012 R2, tem de desinstalar o WSUS 3.2 a partir do servidor. Para obter informações sobre este passo crítico, consulte a secção novas e alteradas da funcionalidade em [descrição geral do Windows Server Update Services](https://technet.microsoft.com/library/hh852345.aspx) na documentação do Windows Server.

#### <a name="after-upgrade"></a>Após a atualização  
  - Certifique-se de que o serviço de implementação do Windows está iniciado e em execução para as seguintes funções de sistema de sites (este serviço for parado durante a atualização):
    - Servidor do site
    - Ponto de gestão
    - Ponto de serviço Web do Catálogo de Aplicações
    - Ponto de site do Catálogo de Aplicações


  -     Certifique-se a **ativação de processos do Windows** e **WWW/W3svc** serviços estão ativado, definido para início automático e em execução para que as seguintes funções de sistema de sites (estes serviços estão desativados durante a atualização):
    -   Servidor do site
    -   Ponto de gestão
    -   Ponto de serviço Web do Catálogo de Aplicações
    -   Ponto de site do Catálogo de Aplicações


  -     Certifique-se de que cada servidor que aloja uma função de sistema de sites continua a corresponder a todos os [os pré-requisitos para funções de sistema de sites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) que são executadas nesse servidor. Por exemplo, poderá ter de reinstalar o BITS, o WSUS, ou configurar definições específicas do IIS.

  Depois de restaurar os pré-requisitos em falta, reinicie o servidor mais uma vez para garantir que os serviços são iniciadas e operacional.


### <a name="unsupported-upgrade-scenarios"></a>Cenários de atualização não suportados
Os cenários de atualização do Windows Server seguintes são geralmente mais frequentes sobre, mas não suportados pelo Configuration Manager:  

-   Windows Server 2008 para o Windows Server 2012 ou posterior  
-   Windows Server 2008 R2 para o Windows Server 2012



##  <a name="BKMK_SupConfigUpgradeClient"></a> Atualizar clientes do SO do Configuration Manager  
 O Configuration Manager suporta uma atualização no local do SO para clientes do Configuration Manager nas seguintes situações:  

-   Atualização no local para um service pack posterior do Windows se o nível de service pack resultante continua a ser suportado pelo Configuration Manager.  

-   Atualização no local do Windows de uma versão suportada do Windows 10. Para obter mais informações, consulte [atualizar o Windows para a versão mais recente](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md).  

-   Atualizações de manutenção de compilação em compilação do Windows 10. Para obter mais informações, consulte [gerir o Windows como um serviço](../../../osd/deploy-use/manage-windows-as-a-service.md).  



##  <a name="BKMK_SupConfigUpgradeDBSrv"></a> Atualizar o SQL Server no servidor de base de dados do site  
  O Configuration Manager suporta uma atualização no local do SQL Server de uma versão suportada do SQL Server no servidor de base de dados do site. Os cenários de atualização do SQL Server nesta secção são suportados pelo Configuration Manager e incluem os requisitos para cada cenário.

 Para obter informações sobre as versões do SQL Server que são suportadas pelo Configuration Manager, consulte [suporte para versões do SQL Server](../../../core/plan-design/configs/support-for-sql-server-versions.md).  

 ### <a name="upgrade-the-service-pack-version-of-sql-server"></a>Atualizar a versão do service pack do SQL Server    
 O Configuration Manager suporta a atualização no local do SQL Server para um service pack posterior se o nível de pacote de serviço do SQL Server resultante continua a ser suportado pelo Configuration Manager.

 Quando tiver vários sites do Configuration Manager numa hierarquia, cada site pode executar uma versão de pacote de serviço diferente do SQL Server. Não há nenhum limitações para a ordem na qual os sites atualizam a versão de service pack do SQL Server que é utilizado para a base de dados do site.

### <a name="upgrade-to-a-new-version-of-sql-server"></a>Atualizar para uma nova versão do SQL Server   
 O Configuration Manager suporta a atualização no local do SQL Server para as seguintes versões:

 - SQL Server de 2017
 - SQL Server 2016  
 - SQL Server 2014  

Ao atualizar a versão do SQL Server que aloja a base de dados do site, tem de atualizar a versão do SQL Server que é utilizada nos sites na seguinte ordem:

 1. Atualize primeiro o SQL Server no site de administração central.
 2. Atualize sites secundários antes de atualizar o site primário principal do site secundário.
 3. Por último, atualize os sites primários principais. Estes sites incluem ambos os sites primários subordinados que dependem de um site de administração central e sites primários autónomos que são o site de nível superior de uma hierarquia.

### <a name="sql-server-cardinality-estimation-level-and-the-site-database"></a>Nível de estimativa de cardinalidade do SQL Server e a base de dados do site   
Quando uma base de dados do site é atualizado a partir de uma versão anterior do SQL Server, a base de dados mantém o nível de estimativa de cardinalidade do SQL (CE) existente se, no mínimo permitido para essa instância do SQL Server. Atualizar automaticamente o SQL Server com uma base de dados a um nível de compatibilidade inferior ao nível de permitido define a base de dados para o nível de compatibilidade inferior permitido pelo SQL Server.

A tabela seguinte identifica os níveis de compatibilidade recomendada de bases de dados do Configuration Manager sites:

|Versão do SQL Server | Níveis de compatibilidade suportado |Nível recomendado|
|----------------|--------------------|--------|
| SQL Server de 2017 | 140, 130, 120, 110  | 140 |
| SQL Server 2016 | 130, 120, 110  | 130 |
| SQL Server 2014 | 120, 110      | 110 |

Para identificar o nível de compatibilidade do SQL Server CE em utilização para a base de dados do site, execute a seguinte consulta SQL no servidor de base de dados do site:  
`SELECT name, compatibility_level FROM sys.databases`

 Para obter mais informações sobre níveis de compatibilidade de SQL CE e como colocá-los, consulte [ALTER a nível de compatibilidade da base de dados (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level?view=sql-server-2017).


Para obter mais informações sobre a atualização do SQL Server, consulte a seguinte documentação do SQL Server:
-   [Atualizar para o SQL Server de 2017](/sql/database-engine/install-windows/supported-version-and-edition-upgrades-2017)
-   [Atualizar para o SQL Server 2016](/sql/database-engine/install-windows/supported-version-and-edition-upgrades)
-   [Atualizar para o SQL Server 2014](http://technet.microsoft.com/library/ms143393\(v=sql.120))  



### <a name="to-upgrade-sql-server-on-the-site-database-server"></a>Para atualizar o SQL Server no servidor da base de dados do site  

1.  Pare todos os serviços do Configuration Manager no site.  
2.  Atualize o SQL Server para uma versão suportada.  
3.  Reinicie os serviços do Configuration Manager.  

> [!NOTE]  
>  Quando altera a edição do SQL Server em utilização no site de administração central de uma edição Standard para uma edição Datacenter ou Enterprise, a partição da base de dados que limita o número de clientes que a hierarquia suporta não se altera.
