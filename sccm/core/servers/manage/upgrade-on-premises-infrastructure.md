---
title: Atualizar infraestrutura no local
titleSuffix: Configuration Manager
description: Saiba como atualizar a infraestrutura, como o SQL Server e o sistema operacional dos sistemas de sites.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8ca970dd-e71c-404f-9435-d36e773a0db2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2d51774688b80faf808653cde77aa3b651ea210c
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53422594"
---
# <a name="upgrade-on-premises-infrastructure-that-supports-configuration-manager"></a>Atualizar a infraestrutura no local que suporta o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize as informações neste artigo para o ajudar a atualizar a infraestrutura de servidor que executa o Configuration Manager.  

- Se quiser *atualizar* de uma versão anterior ao Configuration Manager, ramo atual, veja [atualizar para o Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager).  

- Se quiser *atualizar* seu Gestor de configuração, o ramo atual, a infraestrutura para uma nova versão, consulte [atualiza para o Configuration Manager](/sccm/core/servers/manage/updates).  



## <a name="BKMK_SupConfigUpgradeSiteSrv"></a> Atualizar o sistema operacional dos sistemas de sites  

O Configuration Manager suporta a atualização no local do servidor do sistema operacional que aloja um servidor de site e qualquer função de sistema de sites, nas seguintes situações:  

- Se o Configuration Manager suporta ainda o nível do Windows, ele oferece suporte a atualização no local para um service pack posterior do Windows Server.  

- Atualização in-loco a partir de:  

    - Windows Server 2016 para o Windows Server de 2019   

    - Windows Server 2012 R2 para o Windows Server de 2019   

    - Windows Server 2012 R2 para o Windows Server 2016   

    - Windows Server 2012 para o Windows Server 2016   

    - Windows Server 2012 para Windows Server 2012 R2   

    - Windows Server 2008 R2 para o Windows Server 2012 R2   

Para atualizar um servidor, utilize os procedimentos de atualização fornecidos pelo sistema operacional que está a atualizar. Consulte os seguintes artigos:  

- [Centro de atualização do Windows Server](http://aka.ms/upgradecenter)  

- [Atualização e opções de conversão do Windows Server 2016](https://docs.microsoft.com/windows-server/get-started/supported-upgrade-paths)  

- [Opções de atualização do Windows Server 2012 R2](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn303416(v=ws.11))   


### <a name="bkmk_2016-2019"></a> Atualizar para o Windows Server 2016 ou de 2019

Utilize os passos nesta secção para qualquer um dos seguintes cenários de atualização:  

- Atualizar o Windows Server 2012 R2 ou Windows Server 2016 para o Windows Server de 2019  

- Atualizar o Windows Server 2012 ou Windows Server 2012 R2 para o Windows Server 2016  


#### <a name="before-upgrade"></a>Antes da atualização  
- (Windows Server 2012 ou Windows Server 2012 R2): Remova o cliente do System Center Endpoint Protection (SCEP). Windows Server tem agora o Windows Defender incorporada, que substitui o cliente SCEP. A presença de cliente SCEP pode impedir que uma atualização para o Windows Server.  

- Remova a função WSUS do servidor se estiver instalado. Pode manter o SUSDB e voltar a ligá-lo assim que o WSUS é reinstalado.  

#### <a name="after-upgrade"></a>Após a atualização   
- Certifique-se de que o Windows Defender estiver ativado, definir para o início automático e em execução.  

- Certifique-se de que executem os seguintes serviços do Configuration Manager:  

    - SMS_EXECUTIVE  

    - SMS_SITE_COMPONENT_MANAGER  

- Certifique-se de que o **ativação de processos do Windows** e **WWW/W3svc** serviços estiverem ativados e definidos para início automático. O processo de atualização desativa esses serviços, por isso, certifique-se de que estão a executar para as seguintes funções de sistema de sites:  

    - Servidor do site  

    - Ponto de gestão  

    - Ponto de serviço Web do Catálogo de Aplicações  

    - Ponto de site do Catálogo de Aplicações  

- Certifique-se de que cada servidor que aloje uma função de sistema de sites continua a corresponder a todos [pré-requisitos](/sccm/core/plan-design/configs/site-and-site-system-prerequisites). Por exemplo, poderá ter de reinstalar o BITS, WSUS, ou configurar definições específicas do IIS.  

- Depois de restaurar os pré-requisitos em falta, reinicie o servidor mais uma vez para se certificar de que os serviços são iniciadas e operacional.  

- Se estiver a atualizar o servidor de site primário, em seguida, [executar uma reposição do site](/sccm/core/servers/manage/modify-your-infrastructure#bkmk_reset).  

#### <a name="known-issue-for-remote-configuration-manager-consoles"></a>Problema conhecido para consolas remotas do Configuration Manager   
Depois de atualizar o servidor do site ou uma instância do fornecedor de SMS, não é possível ligar com a consola do Configuration Manager. Para contornar este problema, restaurar manualmente as permissões para o **Admins de SMS** grupo no WMI. Tem de definir as permissões no servidor do site e, em cada servidor remoto que aloja uma instância do fornecedor de SMS:

1. Nos servidores aplicável, abra a consola de gestão da Microsoft (MMC) e adicione o snap-in para **controle WMI**e, em seguida, selecione **computador Local**.  

2. Na MMC, abra a **propriedades** dos **controlo WMI (Local)** e selecione o **segurança** separador.  

3. Expandir a árvore abaixo da raiz, selecione o **SMS** nó e, em seguida, escolha **segurança**.  Certifique-se de que o **Admins de SMS** grupo tem as seguintes permissões:  

    - Ativar conta  

    - Ativar remoto  

4. Sobre o **separador segurança** abaixo a **SMS** nó, selecione o **site_&lt;sitecode**> nó e, em seguida, escolha **segurança**. Certifique-se de que o **Admins de SMS** grupo tem as seguintes permissões:  

    - Executar métodos  

    - Escrita do fornecedor  

    - Ativar conta  

    - Ativar remoto  

5. Guarde as permissões para restaurar o acesso para a consola do Configuration Manager.  


### <a name="bkmk_2012r2"></a> Atualização para o Windows Server 2012 R2

Quando atualizar do Windows Server 2008 R2 ou Windows Server 2012 para Windows Server 2012 R2, aplicam-se as seguintes condições:

#### <a name="before-upgrade"></a>Antes da atualização  
- No Windows Server 2012: Remova a função WSUS do servidor se estiver instalado. Pode manter o SUSDB e voltar a ligá-lo assim que o WSUS é reinstalado.  

- No Windows Server 2008 R2: Antes de atualizar para o Windows Server 2012 R2, tem de desinstalar o WSUS 3.2 do servidor. Pode manter o SUSDB e voltar a ligá-lo assim que o WSUS é reinstalado. Para obter mais informações, consulte [descrição geral do Windows Server Update Services](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh852345(v=ws.11)#new-and-changed-functionality).  

#### <a name="after-upgrade"></a>Após a atualização  
- O processo de atualização desativa os serviços de implantação do Windows. Certifique-se de que este serviço é iniciado e em execução para as seguintes funções de sistema de sites:  

    - Servidor do site  

    - Ponto de gestão  

    - Ponto de serviço Web do Catálogo de Aplicações  

    - Ponto de site do Catálogo de Aplicações  

- Certifique-se de que o **ativação de processos do Windows** e **WWW/W3svc** serviços estiverem ativados e definidos para início automático. O processo de atualização desativa esses serviços, por isso, certifique-se de que estão a executar para as seguintes funções de sistema de sites:  

    - Servidor do site  

    - Ponto de gestão  

    - Ponto de serviço Web do Catálogo de Aplicações  

    - Ponto de site do Catálogo de Aplicações  

- Certifique-se de que cada servidor que aloje uma função de sistema de sites continua a corresponder a todos [pré-requisitos](/sccm/core/plan-design/configs/site-and-site-system-prerequisites). Por exemplo, poderá ter de reinstalar o BITS, WSUS, ou configurar definições específicas do IIS.  

    Depois de restaurar os pré-requisitos em falta, reinicie o servidor mais uma vez para se certificar de que os serviços são iniciadas e operacional.  


### <a name="unsupported-upgrade-scenarios"></a>Cenários de atualização não suportados

Os seguintes cenários de atualização do Windows Server são mais frequentes sobre, mas não suportados pelo Configuration Manager:  

- Windows Server 2008 para o Windows Server 2012 ou posterior  

- Windows Server 2008 R2 para o Windows Server 2012  



##  <a name="BKMK_SupConfigUpgradeClient"></a> Atualize o sistema operativo de clientes  

O Configuration Manager suporta uma atualização no local do sistema operacional para clientes do Configuration Manager nas seguintes situações:  

- Se o Configuration Manager suporta o nível, suporta a atualização no local para um service pack posterior do Windows.  

- Atualização no local do Windows de uma versão suportada para o Windows 10. Para obter mais informações, consulte [atualizar o Windows para a versão mais recente](/sccm/osd/deploy-use/upgrade-windows-to-the-latest-version).  

- Atualizações de manutenção de compilação para compilação do Windows 10. Para obter mais informações, consulte [gerir o Windows como um serviço](/sccm/osd/deploy-use/manage-windows-as-a-service).  



##  <a name="BKMK_SupConfigUpgradeDBSrv"></a> Atualizar o SQL Server  

O Configuration Manager suporta uma atualização no local do SQL Server no servidor de base de dados do site. 

Para obter informações sobre as versões do SQL Server que o Configuration Manager suporta, consulte [suporte para versões do SQL Server](/sccm/core/plan-design/configs/support-for-sql-server-versions).  


### <a name="upgrade-the-service-pack-version-of-sql-server"></a>Atualizar a versão do service pack do SQL Server    

Se o Configuration Manager ainda suporta o nível de pacote de serviço resultante do SQL Server, ele oferece suporte a atualização no local do SQL Server para um service pack posterior.

Quando tiver mais do que um site do Configuration Manager numa hierarquia, cada site pode executar uma versão de pacote de serviço diferentes do SQL Server. Não há nenhuma limitação para a ordem na qual os sites atualizam a versão de service pack do SQL Server.


### <a name="upgrade-to-a-new-version-of-sql-server"></a>Atualizar para uma nova versão do SQL Server   

O Configuration Manager suporta a atualização no local do SQL Server para as seguintes versões:

- SQL Server 2017  

- SQL Server 2016  

- SQL Server 2014  

Quando atualizar a versão do SQL Server que aloja a base de dados do site, tem de atualizar a versão do SQL Server que é utilizada nos sites na seguinte ordem:

1. Atualize primeiro o SQL Server no site de administração central  

2. Atualize os sites secundários antes de atualizar o site primário principal do site secundário  

3. Por último, atualize os sites primários principais. Esses sites incluem os sites primários subordinados que dependem de um site de administração central e sites primários autónomos que são o site de nível superior de uma hierarquia.  


### <a name="sql-server-cardinality-estimation-level"></a>Nível de estimativa de cardinalidade do SQL Server   

Ao atualizar uma base de dados do site de uma versão anterior do SQL Server, a base de dados mantém seu nível estimativa de cardinalidade da SQL existente, se é no mínimo permitido para essa instância do SQL Server. Atualização do SQL Server com uma base de dados num nível de compatibilidade inferior que o nível permitido automaticamente define a base de dados para o nível de compatibilidade inferior permitido pelo SQL Server.

A tabela seguinte identifica os níveis de compatibilidade recomendadas para bases de dados do Configuration Manager site:

|Versão do SQL Server | Níveis de compatibilidade suportado | Nível recomendado |
|----------------|--------------------|--------|
| SQL Server 2017 | 140, 130, 120, 110  | 140 |
| SQL Server 2016 | 130, 120, 110  | 130 |
| SQL Server 2014 | 120, 110      | 110 |

Para identificar o nível de compatibilidade de estimativa de cardinalidade do SQL Server em utilização para a base de dados do site, execute a seguinte consulta SQL no servidor de base de dados do site:  
```SQL
SELECT name, compatibility_level FROM sys.databases
```

Para obter mais informações sobre níveis de compatibilidade do SQL CE e como configurá-los, consulte [alterar o nível de compatibilidade do banco de dados (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level?view=sql-server-2017).


Para obter mais informações sobre a atualização do SQL Server, consulte os seguintes artigos do SQL Server:  

- [Atualizar para o SQL Server 2017](https://docs.microsoft.com/sql/database-engine/install-windows/supported-version-and-edition-upgrades-2017)  

- [Atualizar para o SQL Server 2016](https://docs.microsoft.com/sql/database-engine/install-windows/supported-version-and-edition-upgrades?view=sql-server-2016)  

- [Atualizar para o SQL Server 2014](https://docs.microsoft.com/sql/database-engine/install-windows/supported-version-and-edition-upgrades?view=sql-server-2014)  



### <a name="to-upgrade-sql-server-on-the-site-database-server"></a>Para atualizar o SQL Server no servidor da base de dados do site  

1. Parar todos os serviços do Configuration Manager no site  

2. Atualizar o SQL Server para uma versão suportada  

3. Reinicie os serviços do Configuration Manager  

> [!NOTE]  
> Quando altera a edição do SQL Server utilizada no site de administração central de Standard para um Datacenter ou Enterprise, a partição da base de dados não é alterado. Esta partição da base de dados limita o número de clientes que a hierarquia suporta.  
