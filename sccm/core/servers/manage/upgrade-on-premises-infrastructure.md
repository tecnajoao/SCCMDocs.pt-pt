---
title: Atualizar a infraestrutura no local | Documentos do Microsoft
description: Saiba como atualizar a infraestrutura, como o SQL Server e o sistema operativo do site dos sistemas de sites.
ms.custom: na
ms.date: 2/14/2017
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
ms.sourcegitcommit: 2e711cce2435957f3e85dad08f17260e1a224fc2
ms.openlocfilehash: c6448932e91a02984ca57cef0b75c10ea3f43fa1
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="upgrade-on-premises-infrastructure-that-supports-system-center-configuration-manager"></a>Atualizar a infraestrutura no local que suporta o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize as informações deste tópico para o ajudar a atualizar a infraestrutura de servidor que executa o System Center Configuration Manager.  

 - Se pretender atualizar a partir de uma versão anterior do Configuration Manager para System Center Configuration Manager, consulte o artigo [atualizar para o System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager).

- Se pretender atualizar a sua infraestrutura do System Center Configuration Manager para uma nova versão, consulte o artigo [atualizações para o System Center Configuration Manager](/sccm/core/servers/manage/updates).

##  <a name="BKMK_SupConfigUpgradeSiteSrv"></a>Atualize o sistema operativo dos sistemas de sites  
 O Configuration Manager suporta a atualização no local do sistema operativo dos servidores que alojam um servidor de site e dos servidores remotos que alojam qualquer função de sistema de sites, nas seguintes situações:  

-   Atualização no local para um service pack posterior do Windows Server se o nível de service pack resultante do Windows permanece suportado pelo Configuration Manager.  
-   Atualização no local a partir de:
    - Windows Server 2012 R2 para Windows Server 2016 ([ver detalhes adicionais](#upgrade-windows-server-2012-r2-to-2016)).
    - Windows Server 2012 para o Windows Server 2012 R2 ([ver detalhes adicionais](#upgrade-windows-server-2012-to-windows-server-2012-r2)).
    - Quando utilizar o Configuration Manager versão 1602 ou posterior, também é suportada para atualizar o Windows Server 2008 R2 para o Windows Server 2012 R2 ([ver detalhes adicionais](#upgrade-windows-server-2008-r2-to-windows-server-2012-r2)).

    > [!WARNING]  
    >  Antes de atualizar para o Windows Server 2012 R2, *tem de desinstalar o WSUS 3.2* do servidor.  
    >   
    >  Para obter informações sobre este passo crítico, consulte a secção "Novas e alteradas" [descrição geral do Windows Server Update Services](https://technet.microsoft.com/library/hh852345.aspx) na documentação do Windows Server.  

Para atualizar um servidor, utilize os procedimentos de atualização fornecidos pelo sistema operativo que está a atualizar.  Consulte o seguinte:
  -  [Atualizar opções para o Windows Server 2012 R2](https://technet.microsoft.com/library/dn303416.aspx) na documentação do Windows Server.  
  - [Opções de atualização e a conversão para Windows Server 2016](https://technet.microsoft.com/windows-server-docs/get-started/supported-upgrade-paths) na documentação do Windows Server.

### <a name="upgrade-windows-server-2012-r2-to-2016"></a>Atualizar o Windows Server 2012 R2 para 2016  
Neste cenário de atualização do sistema operativo tem as seguintes condições:

**Antes da atualização:**  
-     Remova o cliente do System Center Endpoint Protection (SCEP). Windows Server 2016 tem o Windows Defender incorporada, que substitui o cliente SCEP. A presença do cliente SCEP pode impedir que uma atualização para o Windows Server 2016.

**Após a atualização:**
-     Certifique-se de que o Windows Defender estiver ativado, definir para início automático e em execução.
-     Certifique-se de que os seguintes serviços do Configuration Manager estão em execução:
  -     SMS_EXECUTIVE
  -     SMS_SITE_COMPONENT_MANAGER


-     Certifique-se a **ativação de processos do Windows** e **WWW/W3svc** serviços estão ativado, configure para início automático e a executar para as seguintes funções de sistema de sites (estes serviços são desativados durante a atualização):
  -     Servidor do site
  -     Ponto de gestão
  -     Ponto de serviço Web do Catálogo de Aplicações
  -     Ponto de site do Catálogo de Aplicações


-     Certifique-se de que cada servidor que aloje uma função de sistema de sites continua a satisfazer todas as [prequisites para funções do sistema de sites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) que são executadas nesse servidor. Por exemplo, poderá necessitar reinstalar o BITS, o WSUS, ou configurar as definições específicas do IIS.

  Depois de restaurar os pré-requisitos em falta, reinicie o servidor mais uma vez para garantir que serviços são iniciadas e operacional.

**Problemas conhecidos para consolas remotas do Configuration Manager:**  
Depois de atualizar o servidor do site ou um servidor que aloja uma instância do SMS_Provider para Windows Server 2016, os utilizadores administrativos poderão não conseguir ligar uma consola do Configuration Manager para o site. Para solucionar este problema, tem de restaurar manualmente as permissões para o grupo Admins de SMS no WMI. As permissões têm de ser definidas no servidor do site e, em cada servidor remoto que aloja uma instância do SMS_Provider:

1. Nos servidores aplicáveis, abra a consola de gestão da Microsoft (MMC) e adicionar o snap-in para **controlo WMI**e, em seguida, selecione **computador Local**.
2. Na MMC, abra o **propriedades** de **controlo WMI (Local)** e selecione o **segurança** separador.
3. Expandir a árvore abaixo raiz, selecione o **SMS** nó e, em seguida, escolha **segurança**.  Certifique-se a **Admins de SMS** grupo tem as seguintes permissões:
  -     Ativar conta
  -     Ativar remoto
4. No **separador segurança** abaixo o **SMS** nó, selecione o **site_**&lt;*sitecode*> nó e, em seguida, escolha **segurança**. Certifique-se a **Admins de SMS** grupo tem as seguintes permissões:
  -   Executar métodos
  -   Fornecedor de escrita
  -   Ativar conta
  -   Ativar remoto
5. Guarde as permissões para restaurar o acesso a consola do Configuration Manager.

### <a name="windows-server-2012-to-windows-server-2012-r2"></a>Windows Server 2012 para o Windows Server 2012 R2

**Antes da atualização:**
-  Ao contrário de outros cenários suportados, este cenário não necessitar de considerações adicionais antes de atualizar.

**Após a atualização:**
  -    Certifique-se de que o serviço de implementação do Windows está iniciado e em execução para as seguintes funções de sistema de sites (este serviço for parado durante a atualização):
    - Servidor do site
    - Ponto de gestão
    - Ponto de serviço Web do Catálogo de Aplicações
    - Ponto de site do Catálogo de Aplicações


  -     Certifique-se a **ativação de processos do Windows** e **WWW/W3svc** serviços estão ativado, configure para início automático e a executar para as seguintes funções de sistema de sites (estes serviços são desativados durante a atualização):
    -     Servidor do site
    -     Ponto de gestão
    -     Ponto de serviço Web do Catálogo de Aplicações
    -     Ponto de site do Catálogo de Aplicações


  -     Certifique-se de que cada servidor que aloje uma função de sistema de sites continua a satisfazer todas as [prequisites para funções do sistema de sites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) que são executadas nesse servidor. Por exemplo, poderá necessitar reinstalar o BITS, o WSUS, ou configurar as definições específicas do IIS.

  Depois de restaurar os pré-requisitos em falta, reinicie o servidor mais uma vez para garantir que serviços são iniciadas e operacional.

### <a name="upgrade-windows-server-2008-r2-to-windows-server-2012-r2"></a>Atualizar o Windows Server 2008 R2 para o Windows Server 2012 R2
Neste cenário de atualização do sistema operativo tem as seguintes condições:  

**Antes da atualização:**
-     Desinstale o WSUS 3,2.  
    Antes de atualizar um sistema operativo do servidor para o Windows Server 2012 R2, tem de desinstalar 3,2 de WSUS a partir do servidor. Para obter informações sobre este passo crítico, veja as novas e alteradas secção Descrição geral do Windows Server Update Services na documentação do Windows Server.

**Após a atualização:**
  -    Certifique-se de que o serviço de implementação do Windows está iniciado e em execução para as seguintes funções de sistema de sites (este serviço for parado durante a atualização):
    - Servidor do site
    - Ponto de gestão
    - Ponto de serviço Web do Catálogo de Aplicações
    - Ponto de site do Catálogo de Aplicações


  -     Certifique-se a **ativação de processos do Windows** e **WWW/W3svc** serviços estão ativado, configure para início automático e a executar para as seguintes funções de sistema de sites (estes serviços são desativados durante a atualização):
    -     Servidor do site
    -     Ponto de gestão
    -     Ponto de serviço Web do Catálogo de Aplicações
    -     Ponto de site do Catálogo de Aplicações


  -     Certifique-se de que cada servidor que aloje uma função de sistema de sites continua a satisfazer todas [os pré-requisitos de funções do sistema de sites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) que são executadas nesse servidor. Por exemplo, poderá necessitar reinstalar o BITS, o WSUS, ou configurar as definições específicas do IIS.

  Depois de restaurar os pré-requisitos em falta, reinicie o servidor mais uma vez para garantir que serviços são iniciadas e operacional.


### <a name="unsupported-upgrade-scenarios"></a>Cenários de atualização não suportados
Os seguintes cenários de atualização de servidor do Windows são normalmente mais frequentes sobre, mas não suportados pelo Configuration Manager:  

-   Windows Server 2008 para o Windows Server 2012 ou posterior  
-   Windows Server 2008 R2 para Windows Server 2012



##  <a name="BKMK_SupConfigUpgradeClient"></a>Atualize o sistema operativo dos clientes do Configuration Manager  
 O Configuration Manager suporta uma atualização no local do sistema operativo para clientes do Configuration Manager nas seguintes situações:  

-   Atualização no local para um service pack posterior do Windows se o nível de service pack resultante permanece suportado pelo Configuration Manager.  

-   Atualização no local do Windows a partir de uma versão suportada do Windows 10. Para obter mais informações, consulte [Atualizar o Windows para a versão mais recente com o System Center Configuration Manager](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md).  

-   Construir a compilação manutenção as atualizações do Windows 10.  Para obter mais informações, consulte [Gerir o Windows como um serviço com o System Center Configuration Manager](../../../osd/deploy-use/manage-windows-as-a-service.md).  

##  <a name="BKMK_SupConfigUpgradeDBSrv"></a>Atualize o SQL Server no servidor de base de dados do site  
  O Configuration Manager suporta uma atualização no local do SQL Server a partir de uma versão suportada do SQL Server no servidor de base de dados do site. Os cenários de atualização do SQL Server nesta secção são suportados pelo Configuration Manager e incluem requisitos para cada cenário.

 Para obter informações sobre as versões do SQL Server que são suportadas pelo Configuration Manager, consulte o artigo [suporte para versões do SQL Server para o System Center Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md).  

 **Atualize a versão de pacote de serviço do SQL Server:**    
 O Configuration Manager suporta a atualização no local do SQL Server para um service pack posterior se o nível de pacote de serviço do SQL Server resultante permanece suportado pelo Configuration Manager.

 Quando tiver vários sites do Configuration Manager numa hierarquia, cada site pode executar uma versão de pacote de serviço diferente do SQL Server e não existe nenhum limitação para a ordem em que sites atualizados a versão de pacote de serviço do SQL Server que é utilizada para a base de dados do site.

 **Atualizar para uma nova versão do SQL Server:**   
 O Configuration Manager suporta a atualização no local do SQL Server para as seguintes versões:

 - SQL Server 2012  
 - SQL Server 2014  
 - SQL Server 2016  

Ao atualizar a versão do SQL Server que aloja a base de dados do site, tem de atualizar a versão do SQL Server que é utilizada em sites pela seguinte ordem:

 1. Atualize primeiro o SQL Server no site de administração central.
 2. Atualize os sites secundários antes de atualizar o site primário principal do site secundário.
 3. Por último, atualize os sites primários principais. Isto inclui dois sites primários subordinados que reportam a um site de administração central e sites primários autónomos que são o site de nível superior de uma hierarquia.

**Nível de Estimation de cardinalidade do SQL Server e a base de dados do site:**   
Quando uma base de dados do site for atualizado de uma versão anterior do SQL Server, a base de dados retém o respetivo nível existente do SQL Server cardinalidade Estimation (CE) se estiver no mínimo permitido para essa instância do SQL Server. Atualizar automaticamente o SQL Server com uma base de dados a um nível de compatibilidade inferior o nível permitido define a base de dados para o nível de compatibilidade inferior permitido pelo SQL Server.

A tabela seguinte identifica os níveis de compatibilidade recomendado para bases de dados do site do Configuration Manager:

|Versão do SQL Server | Níveis de compatibilidade suportados |Nível recomendado|
|----------------|--------------------|--------|
| SQL Server 2016| 130, 120, 110, 100 | 130|
| SQL Server 2014| 120, 110, 100      | 110|

Para identificar o nível de compatibilidade do SQL Server CE utilizado para a base de dados do site, execute a seguinte consulta SQL no servidor de base de dados do site:  **SELECIONE o nome, compatibility_level FROM Databases**

 Para obter mais informações sobre níveis de compatibilidade de SQL CE e como pode defini-las, consulte o artigo [ALTER a nível de compatibilidade da base de dados (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx).


Para mais informações sobre o SQL Server, consulte a documentação do SQL Server na TechNet:
-   [Atualização para o SQL Server 2012](http://technet.microsoft.com/library/ms143393\(v=sql.110))
-   [Atualização para o SQL Server 2014](http://technet.microsoft.com/library/ms143393\(v=sql.120))  
-   [Atualização para o SQL Server 2016](https://technet.microsoft.com/library/bb677622(v=sql.130))



### <a name="to-upgrade-sql-server-on-the-site-database-server"></a>Para atualizar o SQL Server no servidor da base de dados do site  

1.  Pare todos os serviços do Configuration Manager no site.  
2.  Atualize o SQL Server para uma versão suportada.  
3.  Reinicie os serviços do Configuration Manager.  

> [!NOTE]  
>  Quando altera a edição do SQL Server em utilização no site de administração central de uma edição Standard para uma edição Datacenter ou Enterprise, a partição da base de dados que limita o número de clientes que a hierarquia suporta não se altera.

