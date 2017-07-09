---
title: Atualizar infraestrutura local | Microsoft Docs
description: Saiba como atualizar o sistema operacional do site dos sistemas de site e infraestrutura, como o SQL Server.
ms.custom: na
ms.date: 06/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8ca970dd-e71c-404f-9435-d36e773a0db2
caps.latest.revision: 7
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0564cb678200d17d97c0f1d111c0b4b41d8ba40e
ms.openlocfilehash: 188b7f2537dd0e569a5c00995620124512cf311b
ms.contentlocale: pt-pt
ms.lasthandoff: 06/30/2017


---
# <a name="upgrade-on-premises-infrastructure-that-supports-system-center-configuration-manager"></a>Atualizar a infraestrutura no local que suporta o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

Use as informações neste tópico para ajudá-lo a atualizar a infraestrutura de servidor que executa o System Center Configuration Manager.  

 - Se você quiser atualizar de uma versão anterior do Configuration Manager para o System Center Configuration Manager, consulte [atualizar para o System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager).

- Se você quiser atualizar sua infraestrutura do System Center Configuration Manager para uma nova versão, consulte [atualizações para o System Center Configuration Manager](/sccm/core/servers/manage/updates).

##  <a name="BKMK_SupConfigUpgradeSiteSrv"></a>Atualizar o sistema operacional de sistemas de site  
 Configuration Manager dá suporte a atualização in-loco do sistema operacional de servidores que hospedam um servidor do site e de servidores remotos que hospedam qualquer função de sistema de site, nas seguintes situações:  

-   Atualização in-loco para um service pack mais recente do Windows Server se o nível de service pack resultante do Windows permanece com suporte pelo Configuration Manager.  
-   Atualização in-loco de:
    - Windows Server 2012 R2 para o Windows Server 2016 ([ver detalhes adicionais](#bkmk_2016)).
    - Windows Server 2012 para Windows Server 2016 ([ver detalhes adicionais](#bkmk_2016)).
    - Windows Server 2012 para Windows Server 2012 R2 ([ver detalhes adicionais](#bkmk_2012r2)).
    - Quando você usar o Configuration Manager versão 1602 ou posterior, também há suporte para atualizar o Windows Server 2008 R2 para o Windows Server 2012 R2 ([ver detalhes adicionais](#bkmk_from2008r2).

    > [!WARNING]  
    >  Antes de atualizar para o Windows Server 2012 R2, *tem de desinstalar o WSUS 3.2* do servidor.  
    >   
    >  Para obter informações sobre esta etapa crítica, consulte a seção "Funcionalidades novas e alteradas" [visão geral do Windows Server Update Services](https://technet.microsoft.com/library/hh852345.aspx) na documentação do Windows Server.  

Para atualizar um servidor, use os procedimentos de atualização fornecidos pelo sistema operacional que você está atualizando.  Consulte o seguinte:
  -  [Atualizar opções para o Windows Server 2012 R2](https://technet.microsoft.com/library/dn303416.aspx) na documentação do Windows Server.  
  - [Opções de atualização e conversão para o Windows Server 2016](https://technet.microsoft.com/windows-server-docs/get-started/supported-upgrade-paths) na documentação do Windows Server.

### <a name="bkmk_2016"></a>Atualizar o Windows Server 2012 ou Windows Server 2012 R2 para 2016
Quando você atualiza o Windows Server 2012 ou Windows Server 2012 R2 para Windows Server 2016, a seguir se aplicarem:


**Antes da atualização:**  
-   Remova o cliente do System Center Endpoint Protection (SCEP). Windows Server 2016 tem o Windows Defender interna, que substitui o cliente do protocolo SCEP. A presença do cliente do protocolo SCEP pode impedir que uma atualização para o Windows Server 2016.

**Após a atualização:**
-   Certifique-se de que o Windows Defender estiver habilitado, definido para inicialização automática e em execução.
-   Certifique-se de que executam os seguintes serviços do Configuration Manager:
  -     SMS_EXECUTIVE
  -     SMS_SITE_COMPONENT_MANAGER


-   Verifique se o **ativação de processos do Windows** e **WWW/W3svc** serviços estão habilitado, definido para início automático e em execução para as seguintes funções de sistema de site (esses serviços são desabilitados durante a atualização):
  -     Servidor do site
  -     Ponto de gestão
  -     Ponto de serviço Web do Catálogo de Aplicações
  -     Ponto de site do Catálogo de Aplicações

-   Certifique-se de que cada servidor que hospeda uma função de sistema de site continua a atender a todas as [pré-requisitos para funções do sistema de site](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) que são executados no servidor. Por exemplo, você precisará reinstalar o BITS, o WSUS, ou definir as configurações específicas para o IIS.

-   Depois de restaurar todos os pré-requisitos ausentes, reinicie o servidor mais uma vez para garantir que os serviços são iniciados e operacionais.

**Problema conhecido para consoles remotos do Configuration Manager:**  
Depois de atualizar o servidor do site ou um servidor que hospeda uma instância de SMS_Provider para o Windows Server 2016, os usuários administrativos não poderá conectar um console do Configuration Manager para o site. Para contornar esse problema, você deve restaurar manualmente as permissões para o grupo de administradores de SMS no WMI. As permissões devem ser definidas no servidor do site e, em cada servidor remoto que hospeda uma instância do SMS_Provider:

1. Nos servidores aplicável, abra o Console de gerenciamento Microsoft (MMC) e adicionar o snap-in para **Controle WMI**e, em seguida, selecione **computador Local**.
2. No MMC, abra o **propriedades** de **Controle WMI (Local)** e selecione o **segurança** guia.
3. Expanda a árvore abaixo da raiz, selecione o **SMS** nó e, em seguida, escolha **segurança**.  Verifique se o **administradores de SMS** grupo tem as seguintes permissões:
  -     Habilitar conta
  -     Ativação remota
4. No **guia Segurança** abaixo o **SMS** nó, selecione o **site_&lt;sitecode**> nó e, em seguida, escolha **segurança**. Verifique se o **administradores de SMS** grupo tem as seguintes permissões:
  -   Métodos de execução
  -   Gravação de provedor
  -   Habilitar conta
  -   Ativação remota
5. Salve as permissões para restaurar o acesso do console do Configuration Manager.

### <a name="bkmk_2012r2"></a>No Windows Server 2012 para Windows Server 2012 R2

**Antes da atualização:**
-  Ao contrário de outros cenários com suporte, esse cenário não requer considerações adicionais antes da atualização.

**Após a atualização:**
  - Certifique-se de que o serviço de implantação do Windows foi iniciado e está em execução para as seguintes funções de sistema de site (esse serviço for interrompido durante atualização):
    - Servidor do site
    - Ponto de gestão
    - Ponto de serviço Web do Catálogo de Aplicações
    - Ponto de site do Catálogo de Aplicações

  -     Verifique se o **ativação de processos do Windows** e **WWW/W3svc** serviços estão habilitado, definido para início automático e em execução para as seguintes funções de sistema de site (esses serviços são desabilitados durante a atualização):
    -   Servidor do site
    -   Ponto de gestão
    -   Ponto de serviço Web do Catálogo de Aplicações
    -   Ponto de site do Catálogo de Aplicações


  -     Certifique-se de que cada servidor que hospeda uma função de sistema de site continua a atender a todas as [pré-requisitos para funções do sistema de site](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) que são executados no servidor. Por exemplo, você precisará reinstalar o BITS, o WSUS, ou definir as configurações específicas para o IIS.

  Depois de restaurar todos os pré-requisitos ausentes, reinicie o servidor mais uma vez para garantir que os serviços são iniciados e operacionais.

### <a name="bkmk_from2008r2"></a>Atualizar o Windows Server 2008 R2 para o Windows Server 2012 R2
Este cenário de atualização do sistema operacional tem as seguintes condições:  

**Antes da atualização:**
-   Desinstale o WSUS 3.2.  
    Antes de atualizar um sistema operacional Windows Server 2012 R2, você deve desinstalar o WSUS 3.2 do servidor. Para obter informações sobre esta etapa crítica, consulte a seção nova e alterada funcionalidade na visão geral do Windows Server Update Services na documentação do Windows Server.

**Após a atualização:**
  - Certifique-se de que o serviço de implantação do Windows foi iniciado e está em execução para as seguintes funções de sistema de site (esse serviço for interrompido durante atualização):
    - Servidor do site
    - Ponto de gestão
    - Ponto de serviço Web do Catálogo de Aplicações
    - Ponto de site do Catálogo de Aplicações


  -     Verifique se o **ativação de processos do Windows** e **WWW/W3svc** serviços estão habilitado, definido para início automático e em execução para as seguintes funções de sistema de site (esses serviços são desabilitados durante a atualização):
    -   Servidor do site
    -   Ponto de gestão
    -   Ponto de serviço Web do Catálogo de Aplicações
    -   Ponto de site do Catálogo de Aplicações


  -     Certifique-se de que cada servidor que hospeda uma função de sistema de site continua a atender a todos os [pré-requisitos para funções do sistema de site](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) que são executados no servidor. Por exemplo, você precisará reinstalar o BITS, o WSUS, ou definir as configurações específicas para o IIS.

  Depois de restaurar todos os pré-requisitos ausentes, reinicie o servidor mais uma vez para garantir que os serviços são iniciados e operacionais.


### <a name="unsupported-upgrade-scenarios"></a>Não há suporte para cenários de atualização
Os seguintes cenários de atualização do Windows Server são geralmente perguntados sobre, mas não tem suporte pelo Configuration Manager:  

-   Windows Server 2008 para o Windows Server 2012 ou posterior  
-   Windows Server 2008 R2 para o Windows Server 2012



##  <a name="BKMK_SupConfigUpgradeClient"></a>Atualizar o sistema operacional de clientes do Configuration Manager  
 Configuration Manager dá suporte a uma atualização in-loco do sistema operacional para clientes do Configuration Manager nas seguintes situações:  

-   Atualização in-loco para um service pack mais recente do Windows se o nível de service pack resultante permanece com suporte pelo Configuration Manager.  

-   Atualização in-loco do Windows de uma versão com suporte para Windows 10. Para obter mais informações, consulte [Atualizar o Windows para a versão mais recente com o System Center Configuration Manager](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md).  

-   Atualizações de serviços de compilação a compilação do Windows 10.  Para obter mais informações, consulte [Gerir o Windows como um serviço com o System Center Configuration Manager](../../../osd/deploy-use/manage-windows-as-a-service.md).  

##  <a name="BKMK_SupConfigUpgradeDBSrv"></a>Atualize o SQL Server no servidor de banco de dados do site  
  Configuration Manager dá suporte a uma atualização in-loco do SQL Server de uma versão com suporte do SQL no servidor de banco de dados do site. Os cenários de atualização do SQL Server nesta seção são suportados pelo Configuration Manager e incluem os requisitos para cada cenário.

 Para obter informações sobre as versões do SQL Server com suporte pelo Configuration Manager, consulte [suporte para versões do SQL Server para o System Center Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md).  

 **Atualize a versão do service pack do SQL Server:**    
 Configuration Manager dá suporte a atualização in-loco do SQL Server para um service pack mais recente, se o nível de service pack do SQL Server resultante permanece com suporte pelo Configuration Manager.

 Quando você tiver vários sites do Configuration Manager em uma hierarquia, cada site poderá executar uma versão do pacote de serviço diferente do SQL Server, e não há nenhuma limitação na ordem em que sites são atualizados para a versão do service pack do SQL Server que é usado para o banco de dados do site.

 **Atualizar para uma nova versão do SQL Server:**   
 Configuration Manager dá suporte a atualização in-loco do SQL Server para as seguintes versões:

 - SQL Server 2012  
 - SQL Server 2014  
 - SQL Server 2016  

Quando você atualiza a versão do SQL Server que hospeda o banco de dados do site, você deve atualizar a versão do SQL Server que é usada nos sites na seguinte ordem:

 1. Atualize primeiro o SQL Server no site de administração central.
 2. Atualize sites secundários antes de atualizar o site primário do pai do site secundário.
 3. Por último, atualize os sites primários principais. Isso inclui os sites primários filho que relatam para um site de administração central e sites primários autônomos que são o site de nível superior de uma hierarquia.

**Nível de estimativa de cardinalidade do SQL Server e o banco de dados do site:**   
Quando um banco de dados do site é atualizado de uma versão anterior do SQL Server, o banco de dados retém seu nível de estimativa de cardinalidade do SQL (CE) existente se ele é o mínimo permitido para essa instância do SQL Server. Atualizando o SQL Server com um banco de dados em um nível de compatibilidade menor do que o nível permitido automaticamente define o banco de dados para o nível de compatibilidade mais baixo permitido pelo SQL Server.

A tabela a seguir identifica os níveis de compatibilidade recomendadas para bancos de dados de site do Configuration Manager:

|Versão do SQL Server | Níveis de compatibilidade com suporte |Nível recomendado|
|----------------|--------------------|--------|
| SQL Server 2016| 130, 120, 110, 100 | 130|
| SQL Server 2014| 120, 110, 100      | 110|

Para identificar o nível de compatibilidade do SQL Server CE em uso para seu banco de dados do site, execute a seguinte consulta SQL no servidor de banco de dados do site:  **Selecione o nome de sys. Databases FROM de compatibility_level**

 Para obter mais informações sobre níveis de compatibilidade do SQL CE e como defini-las, consulte [alterar o nível de compatibilidade do banco de dados (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx).


Para obter mais informações sobre o SQL Server, consulte a documentação do SQL Server no TechNet:
-   [Atualizar para o SQL Server 2012](http://technet.microsoft.com/library/ms143393\(v=sql.110))
-   [Atualizar para o SQL Server 2014](http://technet.microsoft.com/library/ms143393\(v=sql.120))  
-   [Atualizar para o SQL Server 2016](https://technet.microsoft.com/library/bb677622(v=sql.130))



### <a name="to-upgrade-sql-server-on-the-site-database-server"></a>Para atualizar o SQL Server no servidor da base de dados do site  

1.  Pare todos os serviços do Configuration Manager no site.  
2.  Atualize o SQL Server para uma versão suportada.  
3.  Reinicie os serviços do Configuration Manager.  

> [!NOTE]  
>  Quando altera a edição do SQL Server em utilização no site de administração central de uma edição Standard para uma edição Datacenter ou Enterprise, a partição da base de dados que limita o número de clientes que a hierarquia suporta não se altera.

