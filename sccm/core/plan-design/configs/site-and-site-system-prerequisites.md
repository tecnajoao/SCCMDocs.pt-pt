---
title: "Pré-requisitos do site | Documentos do Microsoft"
description: Saiba como configurar um computador com o Windows como um servidor de sistema de site do System Center Configuration Manager.
ms.custom: na
ms.date: 1/17/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1392797b-76cb-46b4-a3e4-8f349ccaa078
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 42549b98dd7f418cc3f4543198aaeb90ea8a3efd
ms.openlocfilehash: 0b1d2d619d6cdaf36cc22ef461ea1505b5cacc41
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="site-and-site-system-prerequisites-for-system-center-configuration-manager"></a>Site e os pré-requisitos de sistema de sites para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


 Os computadores baseados em Windows requerem configurações específicas para suportar a utilização como servidores de sistema de sites do System Center Configuration Manager.  


 Para alguns produtos, como o Windows Server Update Services (WSUS) para o software de ponto de atualização, tem de referir-se a documentação do produto para identificar a pré-requisitos adicionais e limitações para utilizam esse produto. Estão incluídas apenas configurações diretamente aplicáveis para utilização com o Configuration Manager.   

> [!NOTE]  
>  Em Janeiro de 2016, suporte expirou para o .NET Framework 4.0, 4.5 e 4.5.1. Para obter mais informações, veja [FAQ sobre a Política de Ciclo de Vida do Suporte Microsoft .NET Framework](https://support.microsoft.com/gp/framework_faq?WT.mc_id=azurebg_email_Trans_943_NET452_Update), em support.microsoft.com.  

## <a name="bkmk_generalprerewq"></a>Requisitos do servidor de sites geral e limitações
**Aplicar o seguinte procedimento para todos os servidores de sistema de sites:**

-   Cada servidor de sistema de sites tem de utilizar um sistema operativo de 64 bits. A única exceção é a função ponto de distribuição site sistema, que pode instalar em alguns sistemas operativos de 32 bits.  

-   Sistemas de sites não são suportados em instalações Server Core do qualquer sistema operativo. Uma exceção a isto é que instalações Server Core são suportadas para a função de sistema de sites do ponto de distribuição, sem PXE ou suporte multicast.  

-   Depois de um servidor de sistema de sites está instalado, não é suportada para alterar:  

    -   O nome de domínio do domínio onde está localizado o computador do sistema de sites (também designado por um **mudar o nome de domínio**).  

    -   A associação de domínio do computador.  

    -   O nome do computador.  

  Se tiver de alterar qualquer uma destas, tem primeiro de remover a função de sistema de sites do computador e, em seguida, reinstale a função após a alteração seja concluída. Se esta ação afeta o computador do servidor do site, tem de desinstalar o site e, em seguida, reinstalar o site após a alteração seja concluída.  

-   Funções do sistema de sites não são suportadas numa instância de um cluster do Windows. A única exceção a isto é o servidor de base de dados do site.  

-   Não é suportada para alterar o tipo de arranque ou "Início de sessão como" definições de qualquer serviço do Configuration Manager. Ao fazê-lo, poderá impedir que os serviços de chave a funcionar corretamente.  

##  <a name="bkmk_2012Prereq"></a>Pré-requisitos para o Windows Server 2012 e sistemas operativos posteriores  
###  <a name="bkmk_2012sspreq"></a>Servidor do site: site de administração central e site primário  
  **Funcionalidades e funções de servidor do Windows:**  

-   .NET framework 3.5 SP1 (ou posterior)  

-   O .NET framework 4.5.2  

-   Compressão de diferencial remota  

**Windows ADK:**  

-   Antes de instalar ou atualizar um site de administração central ou site primário, tem de instalar a versão do Windows Assessment and Deployment Kit (ADK) que requer a versão do Configuration Manager que estiver a instalar ou atualizar para o.  

    -   A versão de 1511 do Configuration Manager requer a versão do Windows 10 RTM (10.0.10240) do Windows ADK.  

-   Para obter mais informações sobre este requisito, consulte o artigo [requisitos de infraestrutura de implementação do sistema operativo](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment).  

**Do Visual C++ Redistributable:**  

-   Configuration Manager instala o Microsoft Visual C++ 2013 Redistributable Package em cada computador que instala um servidor do site.  

-   Sites de administração central e sites primários necessitam de ambas as versões x86 e x64 do ficheiro Redistributable aplicável.  

###  <a name="bkmk_2012secpreq"></a>Servidor do site: site secundário  
**Funcionalidades e funções de servidor do Windows:**  

-   .NET framework 3.5 SP1 (ou posterior)  

-   O .NET framework 4.5.2  

-   Compressão de diferencial remota  

**Do Visual C++ Redistributable:**  

-   Configuration Manager instala o Microsoft Visual C++ 2013 Redistributable Package em cada computador que instala um servidor do site.  

-   Os sites secundários requerem apenas o x64 versão.  

**Funções de sistema de sites predefinidas:**  

-   Por predefinição, um site secundário é instalado um **ponto de gestão** e um **ponto de distribuição**.  

-   Certifique-se de que o servidor de site secundário cumpre os pré-requisitos para estas funções de sistema de sites.  

###  <a name="bkmk_2012dbpreq"></a>Servidor de base de dados  
**Serviço de registo remoto:**  

-   Durante a instalação do site do Configuration Manager, tem de ativar o serviço registo remoto no computador que alojará a base de dados do site.  

**SQL Server:**  

-   Antes de instalar um site de administração central ou site primário, tem de instalar uma versão suportada do SQL Server para alojar a base de dados do site.  

-   Antes de instalar um site secundário, pode instalar uma versão suportada do SQL Server.  

-   Se optar por ter o Configuration Manager instalar o SQL Server Express como parte da instalação do site secundário, certifique-se de que o computador cumpre os requisitos para executar o SQL Server Express.  

###  <a name="bkmk_2012smsprovpreq"></a>Servidor do fornecedor de SMS  
**Windows ADK:**  

-   O computador onde irá instalar uma instância do fornecedor de SMS tem de ter a versão necessária do que requer a versão do Configuration Manager que estiver a instalar ou atualizar para o Windows ADK.  

    -   A versão de 1511 do Configuration Manager requer a versão do Windows 10 RTM (10.0.10240) do Windows ADK.  

-   Para obter mais informações sobre este requisito, consulte o artigo [requisitos de infraestrutura de implementação do sistema operativo](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment).  

###  <a name="bkmk_2012acwspreq"></a>Ponto de Web site do catálogo de aplicações  
**Funcionalidades e funções de servidor do Windows:**  

-   .NET framework 3.5 SP1 (ou posterior)  

-   O .NET framework 4.5.2:  

    -   ASP.NET 4.5  

**Configuração do IIS:**  

-   Funcionalidades HTTP comuns:  

    -   Documento Predefinido  

    -   Conteúdo Estático  

-   Desenvolvimento de aplicações:  

    -   ASP.NET 3.5 (e as opções selecionadas automaticamente)  

    -   ASP.NET 4.5 (e as opções selecionadas automaticamente)  

    -   Extensibilidade .NET 3.5  

    -   Extensibilidade .NET 4.5  

-   Segurança:  

    -   Autenticação do Windows  

-   IIS compatibilidade de gestão 6:  

    -   Compatibilidade com Metabase do IIS 6  

###  <a name="bkmk_2012ACwsitepreq"></a>Ponto de serviço da web de catálogo de aplicações  
**Funcionalidades e funções de servidor do Windows:**  

-   .NET framework 3.5 SP1 (ou posterior)  

-   O .NET framework 4.5.2:  

    -   ASP.NET 4.5:  

        -   Ativação HTTP (e as opções selecionadas automaticamente)  

**Configuração do IIS:**  

-   Funcionalidades HTTP comuns:  

    -   Documento Predefinido  

-   IIS compatibilidade de gestão 6:  

    -   Compatibilidade com Metabase do IIS 6  

-   Desenvolvimento de aplicações:  

    -   ASP.NET 3.5 (e as opções selecionadas automaticamente)  

    -   Extensibilidade .NET 3.5  

    -   ASP.NET 4.5 (e as opções selecionadas automaticamente)  

    -   Extensibilidade .NET 4.5  

**Memória do computador:**  

-   O computador que aloja esta função do sistema de sites tem de ter um mínimo de 5% de memória disponível do computador livre ativar a função de sistema de site para processar os pedidos.  

-   Se esta função do sistema de sites estiver localizada conjuntamente com outra função de sistema de sites que tenham este requisito mesmo, este requisito de memória para o computador não aumenta, mas mantém-se como um mínimo de 5%.  

###  <a name="bkmk_2012AIpreq"></a>Ponto de sincronização do Asset Intelligence  
**Funcionalidades e funções de servidor do Windows:**  

-   O .NET framework 4.5.2  

###  <a name="bkmk_2012crppreq"></a>Ponto de registo de certificados  
**Funcionalidades e funções de servidor do Windows:**  

-   O .NET framework 4.5.2:  

    -   Ativação HTTP  

**Configuração do IIS:**  

-   Desenvolvimento de aplicações:  

    -   ASP.NET 3.5 (e as opções selecionadas automaticamente)  

    -   ASP.NET 4.5 (e as opções selecionadas automaticamente)  

-   IIS compatibilidade de gestão 6:  

    -   Compatibilidade com Metabase do IIS 6  

    -   Compatibilidade com WMI do IIS 6  

###  <a name="bkmk_2012dppreq"></a>Ponto de distribuição  
**Funcionalidades e funções de servidor do Windows:**  

-   Compressão de diferencial remota  

**Configuração do IIS:**  

-   Desenvolvimento de aplicações:  

    -   Extensões ISAPI  

-   Segurança:  

    -   Autenticação do Windows  

-   IIS compatibilidade de gestão 6:  

    -   Compatibilidade com Metabase do IIS 6  

    -   Compatibilidade com WMI do IIS 6  

**PowerShell:**  

-   No Windows Server 2012 ou posterior, o PowerShell 3.0 ou 4.0 é necessário antes de instalar o ponto de distribuição.  

**Do Visual C++ Redistributable:**  

-   Configuration Manager instala o Microsoft Visual C++ 2013 Redistributable Package em cada computador que aloja um ponto de distribuição.  

-   A versão que está instalada depende da plataforma do computador (x86 ou x64).  

**Microsoft Azure:**  

-   Pode utilizar um serviço em nuvem no Microsoft Azure para alojar um ponto de distribuição.  

**Para suportar PXE ou multicast:**  

-   Instalar e configurar a função de servidor de Windows de serviços de implementação do Windows (WDS).  

    > [!NOTE]  
    >  O WDS instala e configura automaticamente quando configura um ponto de distribuição para suportar PXE ou multicast num servidor que executa o Windows Server 2012 ou posterior.  

> [!NOTE]  
> A função de sistema de sites de ponto de distribuição não necessita de serviço de transferência inteligente em segundo plano em segundo plano (BITS). Quando o BITS é configurado no computador do ponto de distribuição, BITS no computador do ponto de distribuição não seja utilizada para facilitar a transferência de conteúdos por clientes que utilizam o BITS.  

###  <a name="bkmk_2012EPPpreq"></a>Ponto de Endpoint Protection  
**Funcionalidades e funções de servidor do Windows:**  

-   .NET framework 3.5 SP1 (ou posterior)  

###  <a name="bkmk_2012Enrollpreq"></a>Ponto de inscrição  
**Funcionalidades e funções de servidor do Windows:**  

-   .NET framework 3.5 (ou posterior)  

-   O .NET framework 4.5.2:  

     Quando instala esta função do sistema de sites, o Configuration Manager instala automaticamente o .NET Framework 4.5.2. Esta instalação pode colocar o servidor para um reinício de estado pendente. Quando está pendente um reinício para o .NET Framework, aplicações de .NET poderão falhar até depois reinicia o servidor e a conclusão da instalação.  

    -   Ativação HTTP (e as opções selecionadas automaticamente)  

    -   ASP.NET 4.5  


**Configuração do IIS:**  

-   Funcionalidades HTTP comuns:  

    -   Documento Predefinido  

-   Desenvolvimento de aplicações:  

    -   ASP.NET 3.5 (e as opções selecionadas automaticamente)  

    -   Extensibilidade .NET 3.5  

    -   ASP.NET 4.5 (e as opções selecionadas automaticamente)  

    -   Extensibilidade .NET 4.5  

-   IIS compatibilidade de gestão 6:  

    -   Compatibilidade com Metabase do IIS 6  

**Memória do computador:**  

-   O computador que aloja esta função do sistema de sites tem de ter um mínimo de 5% de memória disponível do computador livre ativar a função de sistema de site para processar os pedidos.  

-   Se esta função do sistema de sites estiver localizada conjuntamente com outra função de sistema de sites que tenham este requisito mesmo, este requisito de memória para o computador não aumenta, mas mantém-se como um mínimo de 5%.  

###  <a name="bkmk_2012EnrollProxpreq"></a>Ponto proxy de registo  
**Funcionalidades e funções de servidor do Windows:**  

-   .NET framework 3.5 (ou posterior)  

-   O .NET framework 4.5.2  

     Quando instala esta função do sistema de sites, o Configuration Manager instala automaticamente o .NET Framework 4.5.2. Esta instalação pode colocar o servidor para um reinício de estado pendente. Quando está pendente um reinício para o .NET Framework, aplicações de .NET poderão falhar até depois reinicia o servidor e a conclusão da instalação.  

**Configuração do IIS:**  

-   Funcionalidades HTTP comuns:  

    -   Documento Predefinido  

    -   Conteúdo Estático  

-   Desenvolvimento de aplicações:  

    -   ASP.NET 3.5 (e as opções selecionadas automaticamente)  

    -   ASP.NET 4.5 (e as opções selecionadas automaticamente)  

    -   Extensibilidade .NET 3.5  

    -   Extensibilidade .NET 4.5  

-   Segurança:  

    -   Autenticação do Windows  

-   IIS compatibilidade de gestão 6:  

    -   Compatibilidade com Metabase do IIS 6  

**Memória do computador:**  

-   O computador que aloja esta função do sistema de sites tem de ter um mínimo de 5% de memória disponível do computador livre ativar a função de sistema de site para processar os pedidos.  

-   Se esta função do sistema de sites estiver localizada conjuntamente com outra função de sistema de sites que tenham este requisito mesmo, este requisito de memória para o computador não aumenta, mas mantém-se como um mínimo de 5%.  

###  <a name="bkmk_2012FSPpreq"></a>Ponto de estado de contingência  
A configuração predefinida do IIS é necessária com adições seguintes:  

-   IIS compatibilidade de gestão 6:  

    -   Compatibilidade com Metabase do IIS 6  

###  <a name="bkmk_2012MPpreq"></a>Ponto de gestão  
**Funcionalidades e funções de servidor do Windows:**  

-   O .NET framework 4.5.2  

-   Extensões de servidor de BITS (e automaticamente selecionadas opções) ou serviços de transferência inteligente em segundo plano em segundo plano (BITS) (e opções selecionadas automaticamente)  

**Configuração do IIS:**  

-   Desenvolvimento de aplicações:  

    -   Extensões ISAPI  

-   Segurança:  

    -   Autenticação do Windows  

-   IIS compatibilidade de gestão 6:  

    -   Compatibilidade com Metabase do IIS 6  

    -   Compatibilidade com WMI do IIS 6  

###  <a name="bkmk_2012RSpoint"></a>Ponto do Reporting services  
**Funcionalidades e funções de servidor do Windows:**  

-   O .NET framework 4.5.2  

**SQL Server Reporting Services:**  

-   Tem de instalar e configurar pelo menos uma instância do SQL Server para suportar o SQL Server Reporting Services antes de instalar o reporting services ponto.  

-   A instância que utiliza para SQL Server Reporting Services pode ser a mesma instância que utiliza para a base de dados do site.  

-   Além disso, a instância que utiliza pode ser partilhada com outros produtos do System Center, desde que os outros produtos do System Center não possuem restrições para partilhar a instância do SQL Server.  

###  <a name="bkmk_SCPpreq"></a>Ponto de ligação de serviço  
**Funcionalidades e funções de servidor do Windows:**  

-   O .NET framework 4.5.2  

     Quando instala esta função do sistema de sites, o Configuration Manager instala automaticamente o .NET Framework 4.5.2. Esta instalação pode colocar o servidor para um reinício de estado pendente. Quando está pendente um reinício para o .NET Framework, aplicações de .NET poderão falhar até depois reinicia o servidor e a conclusão da instalação.  

**Do Visual C++ Redistributable:**  

-   Configuration Manager instala o Microsoft Visual C++ 2013 Redistributable Package em cada computador que aloja um ponto de distribuição.  

-   A função de sistema de sites requer o x64 versão.  

###  <a name="bkmk_2012SUPpreq"></a>Ponto de atualização de software  
**Funcionalidades e funções de servidor do Windows:**  

-   .NET framework 3.5 SP1 (ou posterior)  

-   O .NET framework 4.5.2  

A configuração predefinida do IIS é necessária.

**Windows Server Update Services:**  

-   Tem de instalar a função de servidor do Windows do Windows Server Update Services num computador antes de instalar um ponto de atualização de software.  

-   Para obter mais informações, veja [Planear atualizações de software no System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).  

### <a name="state-migration-point"></a>Ponto de migração de estado  
A configuração predefinida do IIS é necessária.  

##  <a name="bkmk_2008"></a>Pré-requisitos para o Windows Server 2008 R2 e Windows Server 2008  
Windows Server 2008 e Windows Server 2008 R2 está agora em suporte alargado e já não estão em suporte base, conforme especificado pelo [ciclo de vida de suporte Microsoft](https://support.microsoft.com/lifecycle). Para obter mais informações sobre o suporte de futuro para estes sistemas operativos como servidores de sistema de sites com o Configuration Manager, consulte o artigo [Removed e funcionalidades preteridas para o System Center Configuration Manager](../../../core/plan-design/changes/removed-and-deprecated-features.md).  

**O seguinte procedimento aplica-se a todos os requisitos do .NET Framework:**  

-   Instale a versão completa do .NET Framework antes de instalar as funções de sistema de sites. Por exemplo, consulte o [o Microsoft .NET Framework 4 (programa de instalação autónoma)](http://go.microsoft.com/fwlink/p/?LinkId=193048). O .NET Framework 4 Client Profile é insuficiente para este requisito.  

**O seguinte procedimento aplica-se a todos os requisitos de ativação do Windows Communication Foundation (WCF):**  

-   Pode configurar a ativação do WCF como parte da funcionalidade .NET Framework Windows no servidor do sistema de sites. Por exemplo, no Windows Server 2008 R2, execute o **Assistente para adicionar funcionalidades** para instalar funcionalidades adicionais no servidor. No **selecionar funcionalidades** página, expanda **funcionalidades NET Framework 3.5.1**, expanda **ativação do WCF**e, em seguida, marque as caixas para ambos **ativação HTTP** e **ativação HTTP não** para ativar estas opções.  

###  <a name="bkmk_2008sspreq"></a>Servidor do site: site de administração central e site primário  
**.NET framework:**  

-   .NET framework 3.5 SP1 (ou posterior)  

-   O .NET framework 4.5.2  

**Funcionalidade do Windows:**  

-   Compressão de diferencial remota  

**Windows ADK:**  

-   Antes de instalar ou atualizar um site de administração central ou site primário, tem de instalar a versão do Windows ADK, que requer a versão do Configuration Manager que estiver a instalar ou atualizar para o.  

    -   A versão de 1511 do Configuration Manager requer a versão do Windows 10 RTM (10.0.10240) do Windows ADK.  

-   Para obter mais informações sobre este requisito, consulte o artigo [requisitos de infraestrutura de implementação do sistema operativo](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment).  

**Do Visual C++ Redistributable:**  

-   Configuration Manager instala o Microsoft Visual C++ 2013 Redistributable Package em cada computador que instala um servidor do site.  

-   Sites de administração central e sites primários necessitam de ambas as versões x86 e x64 do ficheiro Redistributable aplicável.  

###  <a name="bkmk_2008secpreq"></a>Servidor do site: site secundário  
**.NET framework:**  

-   .NET framework 3.5 SP1 (ou posterior)  

-   O .NET framework 4.5.2  

**Do Visual C++ Redistributable:**  

-   Configuration Manager instala o Microsoft Visual C++ 2013 Redistributable Package em cada computador que instala um servidor do site.  

-   Os sites secundários requerem apenas o x64 versão.  

**Funções de sistema de sites predefinidas:**  

-   Por predefinição, um site secundário é instalado um **ponto de gestão** e um **ponto de distribuição**.  

-   Certifique-se de que o servidor de site secundário cumpre os pré-requisitos para estas funções de sistema de sites.  

###  <a name="bkmk_2008dbpreq"></a>Servidor de base de dados  
**Serviço de registo remoto:**  

-   Durante a instalação do site do Configuration Manager, tem de ativar o serviço registo remoto no computador que alojará a base de dados do site.  

**SQL Server:**  

-   Antes de instalar um site de administração central ou site primário, tem de instalar uma versão suportada do SQL Server para alojar a base de dados do site.  

-   Antes de instalar um site secundário, pode instalar uma versão suportada do SQL Server.  

-   Se optar por ter o Configuration Manager instalar o SQL Server Express como parte da instalação do site secundário, certifique-se de que o computador cumpre os requisitos para executar o SQL Server Express.  

###  <a name="bkmk_2008smsprovpreq"></a>Servidor do fornecedor de SMS  
**Windows ADK:**  

-   O computador onde irá instalar uma instância do fornecedor de SMS tem de ter a versão necessária do que requer a versão do Configuration Manager que estiver a instalar ou atualizar para o Windows ADK.  

    -   A versão de 1511 do Configuration Manager requer a versão do Windows 10 RTM (10.0.10240) do Windows ADK.  

-   Para obter mais informações sobre este requisito, consulte o artigo [requisitos de infraestrutura de implementação do sistema operativo](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment).  

###  <a name="bkmk_2008acwspreq"></a>Ponto de Web site do catálogo de aplicações  
**.NET framework:**  

-   O .NET framework 4.5.2  

**Configuração do IIS:**

A configuração predefinida do IIS é necessária com adições seguintes:  

-   Funcionalidades HTTP comuns:  

    -   Conteúdo Estático  

    -   Documento Predefinido  

-   Desenvolvimento de aplicações:  

    -   ASP.NET (e as opções selecionadas automaticamente)  

         Em alguns cenários, tais como quando o IIS está instalado ou reconfigurar após instalação do .NET Framework versão 4.5.2, tem de ativar explicitamente ASP.NET versão 4.5. Por exemplo, num computador de 64 bits que é executado o .NET Framework versão 4.0.30319, execute o seguinte comando: **%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i-ativar**  

-   Segurança:  

    -   Autenticação do Windows  

-   IIS compatibilidade de gestão 6:  

    -   Compatibilidade com Metabase do IIS 6  

###  <a name="bkmk_2008ACwsitepreq"></a>Ponto de serviço da web de catálogo de aplicações  
**.NET framework:**  

-   .NET framework 3.5 SP1 (ou posterior)  

-   O .NET framework 4.5.2  

**Ativação do Windows Communication Foundation (WCF):**  

-   Ativação HTTP  

-   Ativação HTTP não  

**Configuração do IIS:**

A configuração predefinida do IIS é necessária com adições seguintes:  

-   Desenvolvimento de aplicações:  

    -   ASP.NET (e as opções selecionadas automaticamente)  

         Em alguns cenários, tais como quando o IIS está instalado ou reconfigurar após instalação do .NET Framework versão 4.5.2, tem de ativar explicitamente ASP.NET versão 4.5. Por exemplo, num computador de 64 bits que é executado o .NET Framework versão 4.0.30319, execute o seguinte comando: **%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i-ativar**  

-   IIS compatibilidade de gestão 6:  

    -   Compatibilidade com Metabase do IIS 6  

**Memória do computador:**  

-   O computador que aloja esta função do sistema de sites tem de ter um mínimo de 5% de memória disponível do computador livre ativar a função de sistema de site para processar os pedidos.  

-   Se esta função do sistema de sites estiver localizada conjuntamente com outra função de sistema de sites que tenham este requisito mesmo, este requisito de memória para o computador não aumenta, mas mantém-se como um mínimo de 5%.  

###  <a name="bkmk_2008AIpreq"></a>Ponto de sincronização do Asset Intelligence  
**.NET framework:**  

-   O .NET framework 4.5.2  

###  <a name="bkmk_2008crppreq"></a>Ponto de registo de certificados  
**.NET framework:**  

-   O .NET framework 4.5.2  

-   Ativação HTTP  

**Configuração do IIS:**

A configuração predefinida do IIS é necessária com adições seguintes:  

-   IIS compatibilidade de gestão 6:  

    -   Compatibilidade com Metabase do IIS 6  

    -   Compatibilidade com WMI do IIS 6  

###  <a name="bkmk_2008dppreq"></a>Ponto de distribuição  
**Configuração do IIS:**

Pode utilizar a configuração predefinida do IIS ou uma configuração personalizada. Para utilizar uma configuração IIS personalizada, tem de ativar as seguintes opções do IIS:  

-   Desenvolvimento de aplicações:  

    -   Extensões ISAPI  

-   Segurança:  

    -   Autenticação do Windows  

-   IIS compatibilidade de gestão 6:  

    -   Compatibilidade com Metabase do IIS 6  

    -   Compatibilidade com WMI do IIS 6  

Quando utiliza uma configuração personalizada do IIS, pode remover as opções que não são necessárias, tal como o seguinte:  

-   Funcionalidades HTTP comuns:  

    -   Redirecionamento HTTP  

-   Ferramentas e Scripts de gestão do IIS  

**Funcionalidade do Windows:**  

-   Compressão de diferencial remota  

**Do Visual C++ Redistributable:**  

-   Configuration Manager instala o Microsoft Visual C++ 2013 Redistributable Package em cada computador que aloja um ponto de distribuição.  

-   A versão que está instalada depende da plataforma do computador (x86 ou x64).  

**Microsoft Azure:**  

-   Pode utilizar um serviço em nuvem no Azure para alojar um ponto de distribuição.  

**Para suportar PXE ou multicast:**  

-   Instalar e configurar a função de servidor de Windows de serviços de implementação do Windows (WDS).  

    > [!NOTE]  
    >  O WDS instala e configura automaticamente quando configura um ponto de distribuição para suportar PXE ou multicast num servidor que executa o Windows Server 2012 ou posterior.  

> [!NOTE]  
> A função de sistema de sites de ponto de distribuição não necessita de serviço de transferência inteligente em segundo plano em segundo plano (BITS). Quando o BITS é configurado no computador do ponto de distribuição, BITS no computador do ponto de distribuição não seja utilizada para facilitar a transferência de conteúdos por clientes que utilizam o BITS.  


###  <a name="bkmk_2008EPPpreq"></a>Ponto de Endpoint Protection  
**.NET framework:**  

-   .NET framework 3.5 SP1 (ou posterior)  

###  <a name="bkmk_2008Enrollpreq"></a>Ponto de inscrição  
**.NET framework:**  

-   O .NET framework 4.5.2  

     Quando instala esta função do sistema de sites, se o servidor já não tem uma versão suportada do .NET Framework instalado, o Configuration Manager instala automaticamente o .NET Framework 4.5.2. Esta instalação pode colocar o servidor para um reinício de estado pendente. Quando está pendente um reinício para o .NET Framework, aplicações de .NET poderão falhar até depois reinicia o servidor e a conclusão da instalação.  

**Ativação do Windows Communication Foundation (WCF):**  

-   Ativação HTTP  

-   Ativação HTTP não  

**Configuração do IIS:**

A configuração predefinida do IIS é necessária com adições seguintes:  

-   Desenvolvimento de aplicações:  

    -   ASP.NET (e as opções selecionadas automaticamente)  

         Em alguns cenários, tais como quando o IIS está instalado ou reconfigurar após instalação do .NET Framework versão 4.5.2, tem de ativar explicitamente ASP.NET versão 4.5. Por exemplo, num computador de 64 bits que é executado o .NET Framework versão 4.0.30319, execute o seguinte comando: **%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i-ativar**  

**Memória do computador:**  

-   O computador que aloja esta função do sistema de sites tem de ter um mínimo de 5% de memória disponível do computador livre ativar a função de sistema de site para processar os pedidos.  

-   Se esta função do sistema de sites estiver localizada conjuntamente com outra função de sistema de sites que tenham este requisito mesmo, este requisito de memória para o computador não aumenta, mas mantém-se como um mínimo de 5%.  

###  <a name="bkmk_2008EnrollProxpreq"></a>Ponto proxy de registo  
**.NET framework:**  

-   O .NET framework 4.5.2  

     Quando instala esta função do sistema de sites, se o servidor já não tem uma versão suportada do .NET Framework instalado, o Configuration Manager instala automaticamente o .NET Framework 4.5.2. Esta instalação pode colocar o servidor para um reinício de estado pendente. Quando está pendente um reinício para o .NET Framework, aplicações de .NET poderão falhar até depois reinicia o servidor e a conclusão da instalação.  

**Ativação do Windows Communication Foundation (WCF):**  

-   Ativação HTTP  

-   Ativação HTTP não  

**Configuração do IIS:**

A configuração predefinida do IIS é necessária com adições seguintes:  

-   Desenvolvimento de aplicações:  

    -   ASP.NET (e as opções selecionadas automaticamente)  

         Em alguns cenários, tais como quando o IIS está instalado ou reconfigurar após instalação do .NET Framework versão 4.5.2, tem de ativar explicitamente ASP.NET versão 4.5. Por exemplo, num computador de 64 bits que é executado o .NET Framework versão 4.0.30319, execute o seguinte comando: **%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i-ativar**  

**Memória do computador:**  

-   O computador que aloja esta função do sistema de sites tem de ter um mínimo de 5% de memória disponível do computador livre ativar a função de sistema de site para processar os pedidos.  

-   Se esta função do sistema de sites estiver localizada conjuntamente com outra função de sistema de sites que tenham este requisito mesmo, este requisito de memória para o computador não aumenta, mas mantém-se como um mínimo de 5%.  

###  <a name="bkmk_2008FSPpreq"></a>Ponto de estado de contingência  
**Configuração do IIS:**

A configuração predefinida do IIS é necessária com adições seguintes:  

-   IIS compatibilidade de gestão 6:  

    -   Compatibilidade com Metabase do IIS 6  

###  <a name="bkmk_2008MPpreq"></a>Ponto de gestão  
**.NET framework:**  

-   O .NET framework 4.5.2  

**Configuração do IIS:**

Pode utilizar a configuração predefinida do IIS ou uma configuração personalizada. Cada ponto de gestão que ative para suportar dispositivos móveis requer a configuração adicional do IIS para ASP.NET (e as opções da mesma automaticamente selecionadas).

Em alguns cenários, tais como quando o IIS está instalado ou reconfigurar após instalação do .NET Framework versão 4.5.2, tem de ativar explicitamente ASP.NET versão 4.5. Por exemplo, num computador de 64 bits que é executado o .NET Framework versão 4.0.30319, execute o seguinte comando: **%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i-ativar**  


Para utilizar uma configuração IIS personalizada, tem de ativar as seguintes opções do IIS:  

-   Desenvolvimento de aplicações:  

    -   Extensões ISAPI  

-   Segurança:  

    -   Autenticação do Windows  

-   IIS compatibilidade de gestão 6:  

    -   Compatibilidade com Metabase do IIS 6  

    -   Compatibilidade com WMI do IIS 6  


Quando utiliza uma configuração personalizada do IIS, pode remover as opções que não são necessárias, tal como o seguinte:  

-   Funcionalidades HTTP comuns:  

    -   Redirecionamento HTTP  

-   Ferramentas e Scripts de gestão do IIS  

**Funcionalidade do Windows:**  

-   BITS extensões de servidor (e automaticamente selecionadas opções) ou serviços de transferência inteligente em segundo plano em segundo plano (BITS) (e opções selecionadas automaticamente)  

###  <a name="bkmk_2008RSpoint"></a>Ponto do Reporting services  
**.NET framework:**  

-   O .NET framework 4.5.2  

**SQL Server Reporting Services:**  

-   Tem de instalar e configurar pelo menos uma instância do SQL Server para suportar o SQL Server Reporting Services antes de instalar o reporting services ponto.  

-   A instância que utiliza para SQL Server Reporting Services pode ser a mesma instância que utiliza para a base de dados do site.  

-   Além disso, a instância que utiliza pode ser partilhada com outros produtos do System Center, desde que os outros produtos do System Center não possuem restrições para partilhar a instância do SQL Server.  

###  <a name="bkmk_2008SCPpreq"></a>Ponto de ligação de serviço  
**.NET framework:**  

-   O .NET framework 4.5.2  

     Quando instala esta função do sistema de sites, se o servidor já não tem uma versão suportada do .NET Framework instalado, o Configuration Manager instala automaticamente o .NET Framework 4.5.2. Esta instalação pode colocar o servidor para um reinício de estado pendente. Quando está pendente um reinício para o .NET Framework, aplicações de .NET poderão falhar até depois reinicia o servidor e a conclusão da instalação.  

**Do Visual C++ Redistributable:**  

-   Configuration Manager instala o Microsoft Visual C++ 2013 Redistributable Package em cada computador que aloja um ponto de distribuição.  

-   A função de sistema de sites requer o x64 versão.  

###  <a name="bkmk_2008SUPpreq"></a>Ponto de atualização de software  
**.NET framework:**  

-   .NET framework 3.5 SP1 (ou posterior)  

-   O .NET framework 4.5.2  

**Configuração do IIS:**

A configuração predefinida do IIS é necessária.  

**Windows Server Update Services:**  

-   Tem de instalar a função de servidor Windows, Windows Server Update Services num computador antes de instalar um ponto de atualização de software.  

-   Para obter mais informações, veja [Planear atualizações de software no System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).

###  <a name="bkmk_2008SMPpreq"></a>Ponto de migração de estado  
**Configuração do IIS:**

A configuração predefinida do IIS é necessária.  

