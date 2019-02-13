---
title: Pré-requisitos do site
titleSuffix: Configuration Manager
description: Saiba como configurar um computador Windows como um servidor de sistema de sites do Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1392797b-76cb-46b4-a3e4-8f349ccaa078
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5b1a5a5e27108debe4f9f055da889d5b7a031ece
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56128454"
---
# <a name="site-and-site-system-prerequisites-for-configuration-manager"></a>Site e pré-requisitos de sistema de sites do Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Computadores baseados em Windows requerem configurações específicas para suportar a sua utilização como servidores de sistema de sites do Configuration Manager. 

Este artigo concentra-se principalmente nas [Windows Server 2012 e versões posterior](#bkmk_2012Prereq). [Windows Server 2008 R2 e Windows Server 2008](#bkmk_2008) são suportadas para a função de sistema de sites de ponto de distribuição. Para obter mais informações, consulte [sistemas operativos suportados para servidores do sistema de sites](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers). 

Para alguns produtos, como o Windows Server Update Services (WSUS) para o ponto de atualização de software, terá de consultar a documentação do produto para identificar pré-requisitos adicionais e limitações para utilizam. Estão incluídas apenas configurações diretamente aplicáveis para utilização com o Configuration Manager.   

> [!NOTE]  
>  Em Janeiro de 2016, o suporte a expirou para o .NET Framework 4.0, 4.5 e 4.5.1. Para obter mais informações, consulte [FAQ de política do ciclo de vida de suporte do Microsoft .NET Framework](https://support.microsoft.com/gp/framework_faq?WT.mc_id=azurebg_email_Trans_943_NET452_Update).  



## <a name="bkmk_generalprerewq"></a> Requisitos gerais e limitações

Os seguintes requisitos de aplicam a todos os servidores de sistema de sites:

- Cada servidor de sistema de sites tem de utilizar um sistema operacional de 64 bits. A única exceção é a função ponto de distribuição site system, que pode instalar em alguns sistemas de operativos de 32 bits.  

- Sistemas de sites não são suportados nas instalações Server Core de qualquer sistema operativo. Uma exceção é que as instalações Server Core são suportadas para a função de sistema de sites de ponto de distribuição. Para obter mais informações, consulte [sistemas operativos suportados para servidores de sistema de sites do Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).  

- Após a instalação de um servidor de sistema de sites, não é suportada a alteração:  

    - O nome de domínio do domínio onde está localizado o computador do sistema de sites (também chamado de um **renomeação de domínio**).  

    - A associação de domínio do computador.  

    - O nome do computador.  

  Se tiver de alterar qualquer um desses itens, remova primeiro a função de sistema de sites do computador. Em seguida, reinstale a função após concluir a alteração. Para que as alterações que afetam o servidor do site, primeiro de desinstalar o site. Em seguida, reinstale o site após concluir a alteração.  

- Funções de sistema de sites não são suportadas numa instância de um cluster do Windows Server. A única exceção é o servidor de base de dados do site. Para obter mais informações, consulte [utilizar um cluster do SQL Server para a base de dados do site do Configuration Manager](/sccm/core/servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database).  

- Não é suportada para alterar o tipo de arranque ou "Iniciar sessão como" definições para qualquer serviço do Configuration Manager. Se o fizer, poderá que serviços importantes deixem de funcionar corretamente.  


###  <a name="bkmk_2012Prereq"></a> Pré-requisitos para o Windows Server 2012 e sistemas operativos posteriores  

Consulte as secções principais neste artigo, para as pré-requisitos específicos para servidores de sistema de sites e funções no Windows Server 2012 e posterior:

- [Site de administração central e os servidores de site primário](#bkmk_2012sspreq)
- [Servidor do site secundário](#bkmk_2012secpreq)
- [Servidor de base de dados](#bkmk_2012dbpreq)
- [Servidor do fornecedor de SMS](#bkmk_2012smsprovpreq)
- [Ponto de Web site do catálogo de aplicações](#bkmk_2012acwspreq)
- [Ponto de serviço da web de catálogo de aplicações](#bkmk_2012ACwsitepreq)
- [Ponto de sincronização do Asset Intelligence](#bkmk_2012AIpreq)
- [Ponto de registo de certificados](#bkmk_2012crppreq)
- [Ponto de distribuição](#bkmk_2012dppreq)
- [Ponto de Endpoint Protection](#bkmk_2012EPPpreq)
- [Ponto de registo](#bkmk_2012Enrollpreq)
- [Ponto proxy de registo](#bkmk_2012EnrollProxpreq)
- [Ponto de estado de contingência](#bkmk_2012FSPpreq)
- [Ponto de gestão](#bkmk_2012MPpreq)
- [Ponto do Reporting services](#bkmk_2012RSpoint)
- [Ponto de ligação de serviço](#bkmk_SCPpreq)
- [Ponto de atualização de software](#bkmk_2012SUPpreq)
- [Ponto de migração de estado](#bkmk_2012SMPpreq)

##  <a name="bkmk_2012sspreq"></a> Site de administração central e os servidores de site primário 

#### <a name="windows-server-roles-and-features"></a>Funcionalidades e funções do Windows Server  

- .NET framework 3.5 SP1 (ou posterior)  

- .NET framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 ou 4.7.2  

    - Para obter mais informações sobre as versões do .NET Framework, consulte [.NET Framework versões e dependências](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies).

- Compressão de diferencial remota  

#### <a name="windows-adk"></a>Windows ADK  

- Antes de instalar ou atualizar um site de administração central ou site primário, instale a versão do Windows Assessment and Deployment Kit (ADK) que seja necessária para a versão do Configuration Manager está a instalar ou atualizar para o. Para obter mais informações, consulte [Windows 10 ADK](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk).  

- Para obter mais informações sobre este requisito, consulte [requisitos de infraestrutura para implementação do sistema operativo](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment).  

#### <a name="visual-c-redistributable"></a>Visual C++ Redistributable  

- Configuration Manager instala o pacote Microsoft Visual C++ 2013 Redistributable em cada computador que instala um servidor do site.  

- Sites de administração central e sites primários exigem ambas as versões x86 e x64 do ficheiro redistributable aplicável.  



##  <a name="bkmk_2012secpreq"></a> Servidor do site secundário   

#### <a name="windows-server-roles-and-features"></a>Funcionalidades e funções do Windows Server  

- .NET framework 3.5 SP1 (ou posterior)  

- .NET framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 ou 4.7.2  

    - Para obter mais informações sobre as versões do .NET Framework, consulte [.NET Framework versões e dependências](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies).  

- Compressão de diferencial remota  

#### <a name="visual-c-redistributable"></a>Visual C++ Redistributable  

- Configuration Manager instala o pacote Microsoft Visual C++ 2013 Redistributable em cada computador que instala um servidor do site.  

- Sites secundários precisam apenas x64 versão.  

#### <a name="default-site-system-roles"></a>Funções de sistema de sites predefinidas  

- Por predefinição, um site secundário instala um **ponto de gestão** e uma **ponto de distribuição**.  

- Certifique-se de que o servidor do site secundário cumpre os pré-requisitos destas funções de sistema de sites.  



##  <a name="bkmk_2012dbpreq"></a> Servidor de base de dados  

#### <a name="remote-registry-service"></a>Serviço de Registo Remoto  

- Durante a instalação do site do Configuration Manager, ativar a **registo remoto** serviço no computador que aloja a base de dados do site.  

#### <a name="sql-server"></a>SQL Server  

- Antes de instalar um site de administração central ou site primário, instale uma versão suportada do SQL Server para alojar a base de dados do site. Para obter mais informações, consulte [versões do SQL Server suportada](/sccm/core/plan-design/configs/support-for-sql-server-versions).  

- Antes de instalar um site secundário, pode instalar uma versão suportada do SQL Server.  

- Se optar por instalar o SQL Server Express como parte da instalação do site secundário do Configuration Manager, certifique-se de que o computador cumpre os requisitos para executar o SQL Server Express.  



##  <a name="bkmk_2012smsprovpreq"></a> Servidor do fornecedor de SMS  

#### <a name="windows-adk"></a>Windows ADK  

- O computador onde instala uma instância do fornecedor de SMS tem de ter a versão necessária do Windows ADK que requer a versão do Configuration Manager está a instalar ou atualizar para o. Para obter mais informações, consulte [Windows 10 ADK](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk).  

- Para obter mais informações sobre este requisito, consulte [requisitos de infraestrutura para implementação do sistema operativo](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment).  



##  <a name="bkmk_2012acwspreq"></a> Ponto de Web site do catálogo de aplicações  

#### <a name="windows-server-roles-and-features"></a>Funcionalidades e funções do Windows Server  

- .NET framework 3.5 SP1 (ou posterior)  

- .NET framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 ou 4.7.2  

    - ASP.NET 4.5  

    - Para obter mais informações sobre as versões do .NET Framework, consulte [.NET Framework versões e dependências](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies).  


#### <a name="iis-configuration"></a>Configuração do IIS  

-   Funcionalidades HTTP comuns:  

    -   Documento Predefinido  

    -   Conteúdo Estático  

-   Desenvolvimento de aplicativos:  

    -   ASP.NET 3.5 (e as opções selecionadas automaticamente)  

    -   ASP.NET 4.5 (e as opções selecionadas automaticamente)  

    -   Extensibilidade do .NET 3.5  

    -   Extensibilidade do .NET 4.5  

-   Segurança:  

    -   Autenticação do Windows  

-   Compatibilidade de gestão 6 do IIS:  

    -   Compatibilidade com Metabase do IIS 6  



##  <a name="bkmk_2012ACwsitepreq"></a> Ponto de serviço da web de catálogo de aplicações  

#### <a name="windows-server-roles-and-features"></a>Funcionalidades e funções do Windows Server  

-   .NET framework 3.5 SP1 (ou posterior)  

-   .NET framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 ou 4.7.2:  

    -   ASP.NET 4.5:  

        -   Ativação HTTP (e as opções selecionadas automaticamente)  

#### <a name="iis-configuration"></a>Configuração do IIS  

-   Funcionalidades HTTP comuns:  

    -   Documento Predefinido  

-   Compatibilidade de gestão 6 do IIS:  

    -   Compatibilidade com Metabase do IIS 6  

-   Desenvolvimento de aplicativos:  

    -   ASP.NET 3.5 (e as opções selecionadas automaticamente)  

    -   Extensibilidade do .NET 3.5  

    -   ASP.NET 4.5 (e as opções selecionadas automaticamente)  

    -   Extensibilidade do .NET 4.5  

#### <a name="computer-memory"></a>Memória do computador  

-   O computador que aloja esta função de sistema de sites tem de ter um mínimo de 5% da memória disponível do computador livre para permitir que a função de sistema de sites processe pedidos.  

-   Quando esta função de sistema de sites é foi colocalizada com a outra função de sistema de sites que tem o mesmo requisito, este requisito de memória para o computador não aumenta, mas permanece no mínimo de 5%.  



##  <a name="bkmk_2012AIpreq"></a> Ponto de sincronização do Asset Intelligence  

#### <a name="windows-server-roles-and-features"></a>Funcionalidades e funções do Windows Server  

-   .NET framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 ou 4.7.2 



##  <a name="bkmk_2012crppreq"></a> Ponto de registo de certificados  

#### <a name="windows-server-roles-and-features"></a>Funcionalidades e funções do Windows Server  

-   .NET framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 ou 4.7.2:  

    -   Ativação HTTP  

#### <a name="iis-configuration"></a>Configuração do IIS  

-   Desenvolvimento de aplicativos:  

    -   ASP.NET 3.5 (e as opções selecionadas automaticamente)  

    -   ASP.NET 4.5 (e as opções selecionadas automaticamente)  

-   Compatibilidade de gestão 6 do IIS:  

    -   Compatibilidade com Metabase do IIS 6  

    -   Compatibilidade com WMI do IIS 6  



##  <a name="bkmk_2012dppreq"></a> Ponto de distribuição  

#### <a name="windows-server-roles-and-features"></a>Funcionalidades e funções do Windows Server  

-   Compressão de diferencial remota  

#### <a name="iis-configuration"></a>Configuração do IIS  

-   Desenvolvimento de aplicativos:  

    -   Extensões ISAPI  

-   Segurança:  

    -   Autenticação do Windows  

-   Compatibilidade de gestão 6 do IIS:  

    -   Compatibilidade com Metabase do IIS 6  

    -   Compatibilidade com WMI do IIS 6  

#### <a name="powershell"></a>PowerShell  

-   No Windows Server 2012 ou posterior, PowerShell 3.0 ou 4.0 é necessária antes de instalar o ponto de distribuição.  

#### <a name="visual-c-redistributable"></a>Visual C++ Redistributable  

-   Configuration Manager instala o pacote Microsoft Visual C++ 2013 Redistributable em cada computador que aloja um ponto de distribuição.  

-   A versão instalada depende da plataforma do computador (x86 ou x64).  

#### <a name="microsoft-azure"></a>Microsoft Azure  

-   Pode usar um serviço em nuvem no Microsoft Azure para alojar um ponto de distribuição.  

#### <a name="to-support-pxe-or-multicast"></a>Para suportar PXE ou multicast  

-   Instalar e configurar a função de servidor de Windows do Windows Deployment Services (WDS).  

    > [!NOTE]  
    >  O WDS é instalado e configurado automaticamente quando configura um ponto de distribuição para suportar PXE ou multicast num servidor que executa o Windows Server 2012 ou posterior.  

-   A partir da versão 1806, ative o dispositivo de resposta PXE num ponto de distribuição sem o serviço de implementação do Windows.  

Para obter mais informações, consulte [instalar e configurar pontos de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).

<!--sms.503672 -Clarified BITS use-->
> [!NOTE]  
> Quando o ponto de distribuição transfere conteúdo, transferirá o utilizando o **serviço de transferência inteligente em segundo plano** (BITS) incorporadas no Windows. A função de ponto de distribuição não requer a funcionalidade de extensão de servidor de IIS de BITS opcional a serem instalados, uma vez que o cliente não carregar informações para o mesmo.  



##  <a name="bkmk_2012EPPpreq"></a> Ponto de Endpoint Protection  

#### <a name="windows-server-roles-and-features"></a>Funcionalidades e funções do Windows Server  

-   .NET framework 3.5 SP1 (ou posterior)  

-   Funcionalidades do Windows Defender (Windows Server 2016 ou posterior)  



##  <a name="bkmk_2012Enrollpreq"></a> Ponto de registo  

#### <a name="windows-server-roles-and-features"></a>Funcionalidades e funções do Windows Server  

-   .NET framework 3.5 (ou posterior)  

-   .NET framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 ou 4.7.2:  

     Quando esta função do sistema de site é instalado, o Configuration Manager instala automaticamente o .NET Framework 4.5.2. Esta instalação pode colocar o servidor num Estado de reinício pendente. Se está pendente um reinício para o .NET Framework, as aplicações .NET poderão falhar até depois do servidor ser reiniciado e a conclusão da instalação.  

    -   Ativação HTTP (e as opções selecionadas automaticamente)  

    -   ASP.NET 4.5  

#### <a name="iis-configuration"></a>Configuração do IIS  

-   Funcionalidades HTTP comuns:  

    -   Documento Predefinido  

-   Desenvolvimento de aplicativos:  

    -   ASP.NET 3.5 (e as opções selecionadas automaticamente)  

    -   Extensibilidade do .NET 3.5  

    -   ASP.NET 4.5 (e as opções selecionadas automaticamente)  

    -   Extensibilidade do .NET 4.5  

-   Compatibilidade de gestão 6 do IIS:  

    -   Compatibilidade com Metabase do IIS 6  

#### <a name="computer-memory"></a>Memória do computador  

-   O computador que aloja esta função de sistema de sites tem de ter um mínimo de 5% da memória disponível do computador livre para permitir que a função de sistema de sites processe pedidos.  

-   Quando esta função de sistema de sites é foi colocalizada com a outra função de sistema de sites que tem o mesmo requisito, este requisito de memória para o computador não aumenta, mas permanece no mínimo de 5%.  



##  <a name="bkmk_2012EnrollProxpreq"></a> Ponto proxy de registo  

#### <a name="windows-server-roles-and-features"></a>Funcionalidades e funções do Windows Server  

-   .NET framework 3.5 (ou posterior)  

-   .NET framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 ou 4.7.2 

     Quando esta função do sistema de site é instalado, o Configuration Manager instala automaticamente o .NET Framework 4.5.2. Esta instalação pode colocar o servidor num Estado de reinício pendente. Se está pendente um reinício para o .NET Framework, as aplicações .NET poderão falhar até depois do servidor ser reiniciado e a conclusão da instalação.  

#### <a name="iis-configuration"></a>Configuração do IIS  

-   Funcionalidades HTTP comuns:  

    -   Documento Predefinido  

    -   Conteúdo Estático  

-   Desenvolvimento de aplicativos:  

    -   ASP.NET 3.5 (e as opções selecionadas automaticamente)  

    -   ASP.NET 4.5 (e as opções selecionadas automaticamente)  

    -   Extensibilidade do .NET 3.5  

    -   Extensibilidade do .NET 4.5  

-   Segurança:  

    -   Autenticação do Windows  

-   Compatibilidade de gestão 6 do IIS:  

    -   Compatibilidade com Metabase do IIS 6  

#### <a name="computer-memory"></a>Memória do computador  

-   O computador que aloja esta função de sistema de sites tem de ter um mínimo de 5% da memória disponível do computador livre para permitir que a função de sistema de sites processe pedidos.  

-   Quando esta função de sistema de sites é foi colocalizada com a outra função de sistema de sites que tem o mesmo requisito, este requisito de memória para o computador não aumenta, mas permanece no mínimo de 5%.  



##  <a name="bkmk_2012FSPpreq"></a> Ponto de estado de contingência 

#### <a name="windows-server-roles-and-features"></a>Funcionalidades e funções do Windows Server 

-   As extensões de servidor de BITS (e as opções selecionadas automaticamente) ou serviços de transferência inteligente em segundo plano (BITS) (e as opções selecionadas automaticamente) 

#### <a name="iis-configuration"></a>Configuração do IIS 

A configuração predefinida do IIS é necessária com as seguintes adições:  

-   Compatibilidade de gestão 6 do IIS:  

    -   Compatibilidade com Metabase do IIS 6  



##  <a name="bkmk_2012MPpreq"></a> Ponto de gestão  

#### <a name="windows-server-roles-and-features"></a>Funcionalidades e funções do Windows Server  

-   .NET framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 ou 4.7.2 

-   As extensões de servidor de BITS (e as opções selecionadas automaticamente) ou serviços de transferência inteligente em segundo plano (BITS) (e as opções selecionadas automaticamente)  

#### <a name="iis-configuration"></a>Configuração do IIS  

-   Desenvolvimento de aplicativos:  

    -   Extensões ISAPI  

-   Segurança:  

    -   Autenticação do Windows  

-   Compatibilidade de gestão 6 do IIS:  

    -   Compatibilidade com Metabase do IIS 6  

    -   Compatibilidade com WMI do IIS 6  



##  <a name="bkmk_2012RSpoint"></a> Ponto do Reporting services  

#### <a name="windows-server-roles-and-features"></a>Funcionalidades e funções do Windows Server  

-   .NET framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 ou 4.7.2 

#### <a name="sql-server-reporting-services"></a>Serviços de Relatórios do SQL Server  

-   Instale e configure pelo menos uma instância do SQL Server para suportar o SQL Server Reporting Services antes de instalar o ponto do reporting.  

-   A instância que utiliza para o SQL Server Reporting Services pode ser a mesma instância que utiliza para a base de dados do site.  

-   Além disso, a instância que utiliza pode ser partilhada com outros produtos do System Center, desde que os outros produtos do System Center não tenham restrições de partilha da instância do SQL Server.  



##  <a name="bkmk_SCPpreq"></a> Ponto de ligação de serviço  

#### <a name="windows-server-roles-and-features"></a>Funcionalidades e funções do Windows Server  

-   .NET framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 ou 4.7.2 

     Quando esta função do sistema de site é instalado, o Configuration Manager instala automaticamente o .NET Framework 4.5.2. Esta instalação pode colocar o servidor num Estado de reinício pendente. Se está pendente um reinício para o .NET Framework, as aplicações .NET poderão falhar até depois do servidor ser reiniciado e a conclusão da instalação.  

#### <a name="visual-c-redistributable"></a>Visual C++ Redistributable  

-   Configuration Manager instala o pacote Microsoft Visual C++ 2013 Redistributable em cada computador que aloja um ponto de distribuição.  

-   A função de sistema de sites requer o x64 versão.  



##  <a name="bkmk_2012SUPpreq"></a> Ponto de atualização de software  

#### <a name="windows-server-roles-and-features"></a>Funcionalidades e funções do Windows Server  

-   .NET framework 3.5 SP1 (ou posterior)  

-   .NET framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 ou 4.7.2 

A configuração predefinida do IIS é necessária.

#### <a name="windows-server-update-services"></a>Windows Server Update Services  

-   Instale a função de servidor do Windows do Windows Server Update Services num computador antes de instalar um ponto de atualização de software.  

-   Para obter mais informações, consulte [planear atualizações de software](/sccm/sum/plan-design/plan-for-software-updates).  



##  <a name="bkmk_2012SMPpreq"></a> Ponto de migração de estado  
<!--SCCMDocs issue 645-->
#### <a name="windows-server-roles-and-features"></a>Funcionalidades e funções do Windows Server  

-   .NET framework 3.5 (ou posterior)  

-   .NET framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 ou 4.7.2:  

     Quando esta função do sistema de site é instalado, o Configuration Manager instala automaticamente o .NET Framework 4.5.2. Esta instalação pode colocar o servidor num Estado de reinício pendente. Se está pendente um reinício para o .NET Framework, as aplicações .NET poderão falhar até depois do servidor ser reiniciado e a conclusão da instalação.  

    -   Ativação HTTP (e as opções selecionadas automaticamente)  

    -   ASP.NET 4.5  

#### <a name="iis-configuration"></a>Configuração do IIS  

-   Funcionalidades HTTP comuns:  

    -   Documento Predefinido  

-   Desenvolvimento de aplicativos:  

    -   ASP.NET 3.5 (e as opções selecionadas automaticamente)  

    -   Extensibilidade do .NET 3.5  

    -   ASP.NET 4.5 (e as opções selecionadas automaticamente)  

    -   Extensibilidade do .NET 4.5  

-   Compatibilidade de gestão 6 do IIS:  

    -   Compatibilidade com Metabase do IIS 6  



##  <a name="bkmk_2008"></a> Pré-requisitos para o Windows Server 2008 R2 e Windows Server 2008  

Windows Server 2008 e Windows Server 2008 R2 estão agora suporte alargado e já não estão em suporte base, conforme especificado pelos [Microsoft Support Lifecycle](https://support.microsoft.com/lifecycle). Para obter mais informações sobre suporte futuro para estes sistemas operativos como servidores de sistema de sites com o Configuration Manager, consulte [foi removido e sistemas de operativos do servidor preteridos](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems).  

Estas versões de SO não são suportados para servidores do site ou a maioria das funções de sistema de sites. Elas ainda têm suporte para a função de sistema de sites da ponto de distribuição, incluindo pontos de distribuição de extração e para PXE e multicast.


###  <a name="bkmk_2008dppreq"></a> Ponto de distribuição  

#### <a name="iis-configuration"></a>Configuração do IIS

Pode utilizar a configuração predefinida do IIS ou uma configuração personalizada. Para utilizar uma configuração personalizada do IIS, tem de ativar as seguintes opções para o IIS:  

-   Desenvolvimento de aplicativos:  

    -   Extensões ISAPI  

-   Segurança:  

    -   Autenticação do Windows  

-   Compatibilidade de gestão 6 do IIS:  

    -   Compatibilidade com Metabase do IIS 6  

    -   Compatibilidade com WMI do IIS 6  

Quando utiliza uma configuração personalizada do IIS, pode remover opções que não são necessárias, como os itens seguintes:  

-   Funcionalidades HTTP comuns:  

    -   Redirecionamento HTTP  

-   Ferramentas e Scripts de gestão do IIS  

#### <a name="windows-feature"></a>Funcionalidade do Windows  

-   Compressão de diferencial remota  

#### <a name="visual-c-redistributable"></a>Visual C++ Redistributable  

-   Configuration Manager instala o pacote Microsoft Visual C++ 2013 Redistributable em cada computador que aloja um ponto de distribuição.  

-   A versão instalada depende da plataforma do computador (x86 ou x64).  

#### <a name="microsoft-azure"></a>Microsoft Azure  

-   Pode utilizar um serviço em nuvem no Azure para alojar um ponto de distribuição.  

#### <a name="to-support-pxe-or-multicast"></a>Para suportar PXE ou multicast  

-   Instalar e configurar a função de servidor de Windows do Windows Deployment Services (WDS).  

    > [!NOTE]  
    >  O WDS é instalado e configurado automaticamente quando configura um ponto de distribuição para suportar PXE ou multicast num servidor que executa o Windows Server 2012 ou posterior.  

-   A partir da versão 1806, ative o dispositivo de resposta PXE num ponto de distribuição sem o serviço de implementação do Windows.  

Para obter mais informações, consulte [instalar e configurar pontos de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).

<!--sms.503672 -Clarified BITS use-->
> [!NOTE]  
> Quando o ponto de distribuição transfere conteúdo, transferirá o utilizando o **serviço de transferência inteligente em segundo plano** (BITS) incorporadas no sistema operativo Windows. A função de ponto de distribuição não requer a funcionalidade de extensão de servidor de IIS de BITS opcional para ser instalado porque o cliente não carregar informações para o mesmo.   

