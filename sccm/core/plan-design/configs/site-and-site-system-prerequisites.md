---
title: "Pré-requisitos do site"
titleSuffix: Configuration Manager
description: Saiba como configurar um computador com o Windows como um servidor de sistema de sites do System Center Configuration Manager.
ms.custom: na
ms.date: 8/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1392797b-76cb-46b4-a3e4-8f349ccaa078
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 8e55af275a2c585273602f9b9308eaed03679ae4
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="site-and-site-system-prerequisites-for-system-center-configuration-manager"></a>Site e os pré-requisitos do sistema de site para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


 Computadores baseados em Windows requerem configurações específicas para suportar a sua utilização como servidores de sistema de sites do System Center Configuration Manager.  

 
 Para alguns produtos, como o Windows Server Update Services (WSUS) para o software de um ponto de atualização, tem de referir-se a documentação do produto para identificar pré-requisitos adicionais e limitações para utilizam esse produto. São incluídas apenas configurações diretamente aplicáveis para utilização com o Configuration Manager.   

> [!NOTE]  
>  Janeiro de 2016, o suporte expirou para o .NET Framework 4.0, 4.5 e 4.5.1. Para obter mais informações, veja [FAQ sobre a Política de Ciclo de Vida do Suporte Microsoft .NET Framework](https://support.microsoft.com/gp/framework_faq?WT.mc_id=azurebg_email_Trans_943_NET452_Update), em support.microsoft.com.  

## <a name="bkmk_generalprerewq"></a>Requisitos do servidor de site geral e limitações
**Aplicar o seguinte a todos os servidores de sistema de sites:**

-   Cada servidor do sistema de sites tem de utilizar um sistema operativo de 64 bits. A única exceção é a função ponto de distribuição site sistema, que pode instalar em alguns sistemas operativos de 32 bits.  

-   Os sistemas de sites não são suportados nas instalações Server Core de qualquer sistema operativo. Uma exceção a isto é que as instalações Server Core são suportadas para a função de sistema de sites do ponto de distribuição, sem suporte multicast ou de PXE.  

-   Depois de um servidor de sistema de sites está instalado, não é suportado para alterar:  

    -   O nome de domínio do domínio onde está localizado o computador do sistema de sites (também designado por um **mudança de nome de domínio**).  

    -   A associação de domínio do computador.  

    -   O nome do computador.  

  Se tiver de alterar qualquer uma destas, tem de remover primeiro a função de sistema de sites do computador e, em seguida, reinstalar a função após concluir a alteração. Se esta ação afetar o computador do servidor de site, tem de desinstalar o site e, em seguida, reinstalar o site após concluir a alteração.  

-   Funções do sistema de sites não são suportadas numa instância de um cluster do Windows Server. A única exceção é o servidor de base de dados do site.  

-   Não é suportada para alterar o tipo de arranque ou "Iniciar sessão como" definições a qualquer serviço do Configuration Manager. Se o fizer, poderá impedir os serviços de chaves de funcionar corretamente.  

##  <a name="bkmk_2012Prereq"></a>Pré-requisitos para o Windows Server 2012 e sistemas operativos posteriores  
###  <a name="bkmk_2012sspreq"></a>Servidor do site: site de administração central e site primário  
  **Funcionalidades e funções de servidor do Windows:**  

-   .NET framework 3.5 SP1 (ou posterior)  

-   .NET framework 4.5.2  

-   Compressão de diferencial remota  

**Windows ADK:**  

-   Antes de instalar ou atualizar um site de administração central ou site primário, tem de instalar a versão do Windows Assessment and Deployment Kit (ADK) que requer a versão do Configuration Manager está a instalar ou atualizar para o. Consulte [Windows 10 ADK](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk) no suporte para Windows 10 como um tópico de cliente.  

-   Para obter mais informações sobre este requisito, consulte [requisitos de infraestrutura de implementação do sistema operativo](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment).  

**Do Visual C++ Redistributable:**  

-   Configuration Manager instala o pacote Microsoft Visual C++ 2013 Redistributable em cada computador que instala um servidor do site.  

-   Sites de administração central e sites primários precisam de ambas as versões x86 e x64 do ficheiro Redistributable aplicável.  

###  <a name="bkmk_2012secpreq"></a>Servidor do site: site secundário  
**Funcionalidades e funções de servidor do Windows:**  

-   .NET framework 3.5 SP1 (ou posterior)  

-   .NET framework 4.5.2  

-   Compressão de diferencial remota  

**Do Visual C++ Redistributable:**  

-   Configuration Manager instala o pacote Microsoft Visual C++ 2013 Redistributable em cada computador que instala um servidor do site.  

-   Os sites secundários necessitam apenas de x64 versão.  

**Funções de sistema de sites predefinidas:**  

-   Por predefinição, um site secundário instala um **ponto de gestão** e um **ponto de distribuição**.  

-   Certifique-se de que o servidor do site secundário cumpre os pré-requisitos destas funções do sistema de sites.  

###  <a name="bkmk_2012dbpreq"></a>Servidor de base de dados  
**Serviço de registo remoto:**  

-   Durante a instalação do site do Configuration Manager, tem de ativar o serviço registo remoto no computador que alojará a base de dados do site.  

**SQL Server:**  

-   Antes de instalar um site de administração central ou site primário, tem de instalar uma versão suportada do SQL Server para alojar a base de dados do site.  

-   Antes de instalar um site secundário, pode instalar uma versão suportada do SQL Server.  

-   Se optar por instalar o SQL Server Express como parte da instalação do site secundário com o Configuration Manager, certifique-se de que o computador cumpre os requisitos para executar o SQL Server Express.  

###  <a name="bkmk_2012smsprovpreq"></a>Servidor do fornecedor de SMS  
**Windows ADK:**  

-   O computador onde instala uma instância do fornecedor de SMS tem de ter a versão necessária do Windows ADK que requer a versão do Configuration Manager está a instalar ou atualizar para o. Consulte [Windows 10 ADK](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk) no suporte para Windows 10 como um tópico de cliente.

-   Para obter mais informações sobre este requisito, consulte [requisitos de infraestrutura de implementação do sistema operativo](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment).  

###  <a name="bkmk_2012acwspreq"></a>Ponto de Web site do catálogo de aplicações  
**Funcionalidades e funções de servidor do Windows:**  

-   .NET framework 3.5 SP1 (ou posterior)  

-   .NET framework 4.5.2:  

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

-   Compatibilidade do IIS 6 de gestão:  

    -   Compatibilidade com Metabase do IIS 6  

###  <a name="bkmk_2012ACwsitepreq"></a>Ponto de serviço da web de catálogo de aplicações  
**Funcionalidades e funções de servidor do Windows:**  

-   .NET framework 3.5 SP1 (ou posterior)  

-   .NET framework 4.5.2:  

    -   ASP.NET 4.5:  

        -   Ativação HTTP (e as opções selecionadas automaticamente)  

**Configuração do IIS:**  

-   Funcionalidades HTTP comuns:  

    -   Documento Predefinido  

-   Compatibilidade do IIS 6 de gestão:  

    -   Compatibilidade com Metabase do IIS 6  

-   Desenvolvimento de aplicações:  

    -   ASP.NET 3.5 (e as opções selecionadas automaticamente)  

    -   Extensibilidade .NET 3.5  

    -   ASP.NET 4.5 (e as opções selecionadas automaticamente)  

    -   Extensibilidade .NET 4.5  

**Memória do computador:**  

-   O computador que aloja esta função de sistema de sites tem de ter um mínimo de 5% da memória disponível do computador livre para permitir que a função de sistema de sites processe pedidos.  

-   Quando esta função de sistema de sites estiver colocalizada com outra função de sistema de sites que tem o mesmo requisito, este requisito de memória para o computador não aumenta, mas mantém-se como um mínimo de 5%.  

###  <a name="bkmk_2012AIpreq"></a>Ponto de sincronização do Asset Intelligence  
**Funcionalidades e funções de servidor do Windows:**  

-   .NET framework 4.5.2  

###  <a name="bkmk_2012crppreq"></a>Ponto de registo de certificados  
**Funcionalidades e funções de servidor do Windows:**  

-   .NET framework 4.5.2:  

    -   Ativação HTTP  

**Configuração do IIS:**  

-   Desenvolvimento de aplicações:  

    -   ASP.NET 3.5 (e as opções selecionadas automaticamente)  

    -   ASP.NET 4.5 (e as opções selecionadas automaticamente)  

-   Compatibilidade do IIS 6 de gestão:  

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

-   Compatibilidade do IIS 6 de gestão:  

    -   Compatibilidade com Metabase do IIS 6  

    -   Compatibilidade com WMI do IIS 6  

**PowerShell:**  

-   No Windows Server 2012 ou posterior, PowerShell 3.0 ou 4.0 é necessário antes de instalar o ponto de distribuição.  

**Do Visual C++ Redistributable:**  

-   Configuration Manager instala o pacote Microsoft Visual C++ 2013 Redistributable em cada computador que aloja um ponto de distribuição.  

-   A versão instalada depende da plataforma do computador (x86 ou x64).  

**Microsoft Azure:**  

-   Pode utilizar um serviço em nuvem no Microsoft Azure para alojar um ponto de distribuição.  

**Para suportar PXE ou multicast:**  

-   Instalar e configurar a função de servidor do Windows de serviços de implementação do Windows (WDS).  

    > [!NOTE]  
    >  O WDS é instalado e configurado automaticamente quando configura um ponto de distribuição para suportar PXE ou multicast num servidor que executa o Windows Server 2012 ou posterior.  

> [!NOTE]  
> A função de sistema de sites de ponto de distribuição não necessita de serviço de transferência inteligente em segundo plano (BITS). Quando BITS estiver configurado no computador do ponto de distribuição, BITS no computador do ponto de distribuição não é utilizada para facilitar a transferência do conteúdo por clientes que utilizam o BITS.  

###  <a name="bkmk_2012EPPpreq"></a>Ponto de Endpoint Protection  
**Funcionalidades e funções de servidor do Windows:**  

-   .NET framework 3.5 SP1 (ou posterior)  

###  <a name="bkmk_2012Enrollpreq"></a>Ponto de registo  
**Funcionalidades e funções de servidor do Windows:**  

-   .NET framework 3.5 (ou posterior)  

-   .NET framework 4.5.2:  

     Quando instala esta função de sistema de sites, o Configuration Manager instala automaticamente o .NET Framework 4.5.2. Esta instalação pode colocar o servidor para um Estado de reinício pendente. Quando está pendente um reinício para o .NET Framework, as aplicações .NET poderão falhar até o servidor ser reiniciado e a conclusão da instalação.  

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

-   Compatibilidade do IIS 6 de gestão:  

    -   Compatibilidade com Metabase do IIS 6  

**Memória do computador:**  

-   O computador que aloja esta função de sistema de sites tem de ter um mínimo de 5% da memória disponível do computador livre para permitir que a função de sistema de sites processe pedidos.  

-   Quando esta função de sistema de sites estiver colocalizada com outra função de sistema de sites que tem o mesmo requisito, este requisito de memória para o computador não aumenta, mas mantém-se como um mínimo de 5%.  

###  <a name="bkmk_2012EnrollProxpreq"></a>Ponto proxy de registo  
**Funcionalidades e funções de servidor do Windows:**  

-   .NET framework 3.5 (ou posterior)  

-   .NET framework 4.5.2  

     Quando instala esta função de sistema de sites, o Configuration Manager instala automaticamente o .NET Framework 4.5.2. Esta instalação pode colocar o servidor para um Estado de reinício pendente. Quando está pendente um reinício para o .NET Framework, as aplicações .NET poderão falhar até o servidor ser reiniciado e a conclusão da instalação.  

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

-   Compatibilidade do IIS 6 de gestão:  

    -   Compatibilidade com Metabase do IIS 6  

**Memória do computador:**  

-   O computador que aloja esta função de sistema de sites tem de ter um mínimo de 5% da memória disponível do computador livre para permitir que a função de sistema de sites processe pedidos.  

-   Quando esta função de sistema de sites estiver colocalizada com outra função de sistema de sites que tem o mesmo requisito, este requisito de memória para o computador não aumenta, mas mantém-se como um mínimo de 5%.  

###  <a name="bkmk_2012FSPpreq"></a>Ponto de estado de contingência  
A configuração predefinida do IIS é necessária com as seguintes adições:  

-   Compatibilidade do IIS 6 de gestão:  

    -   Compatibilidade com Metabase do IIS 6  

###  <a name="bkmk_2012MPpreq"></a>Ponto de gestão  
**Funcionalidades e funções de servidor do Windows:**  

-   .NET framework 4.5.2  

-   As extensões de servidor do BITS (e as opções selecionadas automaticamente) ou serviços de transferência inteligente em segundo plano (BITS) (e as opções selecionadas automaticamente)  

**Configuração do IIS:**  

-   Desenvolvimento de aplicações:  

    -   Extensões ISAPI  

-   Segurança:  

    -   Autenticação do Windows  

-   Compatibilidade do IIS 6 de gestão:  

    -   Compatibilidade com Metabase do IIS 6  

    -   Compatibilidade com WMI do IIS 6  

###  <a name="bkmk_2012RSpoint"></a>Ponto do Reporting Services  
**Funcionalidades e funções de servidor do Windows:**  

-   .NET framework 4.5.2  

**SQL Server Reporting Services:**  

-   Tem de instalar e configurar pelo menos uma instância do SQL Server para suportar o SQL Server Reporting Services antes de instalar o reporting services ponto.  

-   A instância que utiliza para SQL Server Reporting Services pode ser a mesma instância que utiliza para a base de dados do site.  

-   Além disso, a instância que utiliza pode ser partilhada com outros produtos do System Center desde que outros produtos do System Center não tenham restrições de partilha da instância do SQL Server.  

###  <a name="bkmk_SCPpreq"></a>Ponto de ligação de serviço  
**Funcionalidades e funções de servidor do Windows:**  

-   .NET framework 4.5.2  

     Quando instala esta função de sistema de sites, o Configuration Manager instala automaticamente o .NET Framework 4.5.2. Esta instalação pode colocar o servidor para um Estado de reinício pendente. Quando está pendente um reinício para o .NET Framework, as aplicações .NET poderão falhar até o servidor ser reiniciado e a conclusão da instalação.  

**Do Visual C++ Redistributable:**  

-   Configuration Manager instala o pacote Microsoft Visual C++ 2013 Redistributable em cada computador que aloja um ponto de distribuição.  

-   A função de sistema de sites requer o x64 versão.  

###  <a name="bkmk_2012SUPpreq"></a>Ponto de atualização de software  
**Funcionalidades e funções de servidor do Windows:**  

-   .NET framework 3.5 SP1 (ou posterior)  

-   .NET framework 4.5.2  

A configuração predefinida do IIS é necessária.

**Windows Server Update Services:**  

-   Tem de instalar a função de servidor do Windows do Windows Server Update Services num computador antes de instalar um ponto de atualização de software.  

-   Para obter mais informações, veja [Planear atualizações de software no System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).  

### <a name="state-migration-point"></a>Ponto de migração de estado  
A configuração predefinida do IIS é necessária.  

##  <a name="bkmk_2008"></a>Pré-requisitos para o Windows Server 2008 R2 e Windows Server 2008  
Windows Server 2008 e Windows Server 2008 R2 são agora suporte alargado e já não estão em suporte base, conforme especificado pelo [ciclo de vida de suporte Microsoft](https://support.microsoft.com/lifecycle). Para obter mais informações sobre suporte futuro para estes sistemas operativos como servidores de sistema de sites com o Configuration Manager, consulte [removidas e funcionalidades preteridas para o System Center Configuration Manager](../../../core/plan-design/changes/removed-and-deprecated-features.md).  

**O seguinte aplica-se a todos os requisitos do .NET Framework:**  

-   Instale a versão completa do .NET Framework antes de instalar as funções de sistema de sites. Por exemplo, consulte o [o Microsoft .NET Framework 4 (instalador autónomo)](http://go.microsoft.com/fwlink/p/?LinkId=193048). O .NET Framework 4 Client Profile não é suficiente para este requisito.  

**O seguinte aplica-se a todos os requisitos de ativação do Windows Communication Foundation (WCF):**  

-   Pode configurar a ativação do WCF como parte da funcionalidade do Windows do .NET Framework no servidor do sistema de sites. Por exemplo, no Windows Server 2008 R2, execute o **Assistente para adicionar funcionalidades** para instalar funcionalidades adicionais no servidor. No **selecionar funcionalidades** página, expanda **NET Framework 3.5.1 Features**, expanda **ativação do WCF**e, em seguida, selecione as caixas de ambos **ativação HTTP** e **ativação não HTTP** para ativar estas opções.  

###  <a name="bkmk_2008sspreq"></a>Servidor do site: site de administração central e site primário  
**.NET framework:**  

-   .NET framework 3.5 SP1 (ou posterior)  

-   .NET framework 4.5.2  

**Funcionalidade do Windows:**  

-   Compressão de diferencial remota  

**Windows ADK:**  

-   Antes de instalar ou atualizar um site de administração central ou site primário, tem de instalar a versão do Windows ADK, que requer a versão do Configuration Manager está a instalar ou atualizar para o.  Consulte [Windows 10 ADK](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk) no suporte para Windows 10 como um tópico de cliente.  

-   Para obter mais informações sobre este requisito, consulte [requisitos de infraestrutura de implementação do sistema operativo](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment).  

**Do Visual C++ Redistributable:**  

-   Configuration Manager instala o pacote Microsoft Visual C++ 2013 Redistributable em cada computador que instala um servidor do site.  

-   Sites de administração central e sites primários precisam de ambas as versões x86 e x64 do ficheiro Redistributable aplicável.  

###  <a name="bkmk_2008secpreq"></a>Servidor do site: site secundário  
**.NET framework:**  

-   .NET framework 3.5 SP1 (ou posterior)  

-   .NET framework 4.5.2  

**Do Visual C++ Redistributable:**  

-   Configuration Manager instala o pacote Microsoft Visual C++ 2013 Redistributable em cada computador que instala um servidor do site.  

-   Os sites secundários necessitam apenas de x64 versão.  

**Funções de sistema de sites predefinidas:**  

-   Por predefinição, um site secundário instala um **ponto de gestão** e um **ponto de distribuição**.  

-   Certifique-se de que o servidor do site secundário cumpre os pré-requisitos destas funções do sistema de sites.  

###  <a name="bkmk_2008dbpreq"></a>Servidor de base de dados  
**Serviço de registo remoto:**  

-   Durante a instalação do site do Configuration Manager, tem de ativar o serviço registo remoto no computador que alojará a base de dados do site.  

**SQL Server:**  

-   Antes de instalar um site de administração central ou site primário, tem de instalar uma versão suportada do SQL Server para alojar a base de dados do site.  

-   Antes de instalar um site secundário, pode instalar uma versão suportada do SQL Server.  

-   Se optar por instalar o SQL Server Express como parte da instalação do site secundário com o Configuration Manager, certifique-se de que o computador cumpre os requisitos para executar o SQL Server Express.  

###  <a name="bkmk_2008smsprovpreq"></a>Servidor do fornecedor de SMS  
**Windows ADK:**  

-   O computador onde instala uma instância do fornecedor de SMS tem de ter a versão necessária do Windows ADK que requer a versão do Configuration Manager está a instalar ou atualizar para o. Consulte [Windows 10 ADK](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk) no suporte para Windows 10 como um tópico de cliente.  

-   Para obter mais informações sobre este requisito, consulte [requisitos de infraestrutura de implementação do sistema operativo](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment).  

###  <a name="bkmk_2008acwspreq"></a>Ponto de Web site do catálogo de aplicações  
**.NET framework:**  

-   .NET framework 4.5.2  

**Configuração do IIS:**

A configuração predefinida do IIS é necessária com as seguintes adições:  

-   Funcionalidades HTTP comuns:  

    -   Conteúdo Estático  

    -   Documento Predefinido  

-   Desenvolvimento de aplicações:  

    -   ASP.NET (e as opções selecionadas automaticamente)  

         Em alguns cenários, como o IIS está instalado ou reconfigurado após a versão 4.5.2 do .NET Framework está instalada, tem de ativar explicitamente ASP.NET versão 4.5. Por exemplo, num computador de 64 bits que executa a versão 4.0.30319 do .NET Framework, execute o seguinte comando: **%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i-permitir**  

-   Segurança:  

    -   Autenticação do Windows  

-   Compatibilidade do IIS 6 de gestão:  

    -   Compatibilidade com Metabase do IIS 6  

###  <a name="bkmk_2008ACwsitepreq"></a>Ponto de serviço da web de catálogo de aplicações  
**.NET framework:**  

-   .NET framework 3.5 SP1 (ou posterior)  

-   .NET framework 4.5.2  

**Ativação do Windows Communication Foundation (WCF):**  

-   Ativação HTTP  

-   Ativação não HTTP  

**Configuração do IIS:**

A configuração predefinida do IIS é necessária com as seguintes adições:  

-   Desenvolvimento de aplicações:  

    -   ASP.NET (e as opções selecionadas automaticamente)  

         Em alguns cenários, como o IIS está instalado ou reconfigurado após a versão 4.5.2 do .NET Framework está instalada, tem de ativar explicitamente ASP.NET versão 4.5. Por exemplo, num computador de 64 bits que executa a versão 4.0.30319 do .NET Framework, execute o seguinte comando: **%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i-permitir**  

-   Compatibilidade do IIS 6 de gestão:  

    -   Compatibilidade com Metabase do IIS 6  

**Memória do computador:**  

-   O computador que aloja esta função de sistema de sites tem de ter um mínimo de 5% da memória disponível do computador livre para permitir que a função de sistema de sites processe pedidos.  

-   Quando esta função de sistema de sites estiver colocalizada com outra função de sistema de sites que tem o mesmo requisito, este requisito de memória para o computador não aumenta, mas mantém-se como um mínimo de 5%.  

###  <a name="bkmk_2008AIpreq"></a>Ponto de sincronização do Asset Intelligence  
**.NET framework:**  

-   .NET framework 4.5.2  

###  <a name="bkmk_2008crppreq"></a>Ponto de registo de certificados  
**.NET framework:**  

-   .NET framework 4.5.2  

-   Ativação HTTP  

**Configuração do IIS:**

A configuração predefinida do IIS é necessária com as seguintes adições:  

-   Compatibilidade do IIS 6 de gestão:  

    -   Compatibilidade com Metabase do IIS 6  

    -   Compatibilidade com WMI do IIS 6  

###  <a name="bkmk_2008dppreq"></a>Ponto de distribuição  
**Configuração do IIS:**

Pode utilizar a configuração predefinida do IIS ou uma configuração personalizada. Para utilizar uma configuração personalizada do IIS, tem de ativar as seguintes opções do IIS:  

-   Desenvolvimento de aplicações:  

    -   Extensões ISAPI  

-   Segurança:  

    -   Autenticação do Windows  

-   Compatibilidade do IIS 6 de gestão:  

    -   Compatibilidade com Metabase do IIS 6  

    -   Compatibilidade com WMI do IIS 6  

Quando utiliza uma configuração personalizada do IIS, pode remover opções que não são obrigatórias, como as seguintes:  

-   Funcionalidades HTTP comuns:  

    -   Redirecionamento HTTP  

-   Ferramentas e Scripts de gestão do IIS  

**Funcionalidade do Windows:**  

-   Compressão de diferencial remota  

**Do Visual C++ Redistributable:**  

-   Configuration Manager instala o pacote Microsoft Visual C++ 2013 Redistributable em cada computador que aloja um ponto de distribuição.  

-   A versão instalada depende da plataforma do computador (x86 ou x64).  

**Microsoft Azure:**  

-   Pode utilizar um serviço em nuvem no Azure para alojar um ponto de distribuição.  

**Para suportar PXE ou multicast:**  

-   Instalar e configurar a função de servidor do Windows de serviços de implementação do Windows (WDS).  

    > [!NOTE]  
    >  O WDS é instalado e configurado automaticamente quando configura um ponto de distribuição para suportar PXE ou multicast num servidor que executa o Windows Server 2012 ou posterior.  

> [!NOTE]  
> A função de sistema de sites de ponto de distribuição não necessita de serviço de transferência inteligente em segundo plano (BITS). Quando BITS estiver configurado no computador do ponto de distribuição, BITS no computador do ponto de distribuição não é utilizada para facilitar a transferência do conteúdo por clientes que utilizam o BITS.  


###  <a name="bkmk_2008EPPpreq"></a>Ponto de Endpoint Protection  
**.NET framework:**  

-   .NET framework 3.5 SP1 (ou posterior)  

###  <a name="bkmk_2008Enrollpreq"></a>Ponto de registo  
**.NET framework:**  

-   .NET framework 4.5.2  

     Quando esta função de sistema de sites é instalada, se o servidor já não tem uma versão suportada do .NET Framework instalado, o Configuration Manager instala automaticamente o .NET Framework 4.5.2. Esta instalação pode colocar o servidor para um Estado de reinício pendente. Quando está pendente um reinício para o .NET Framework, as aplicações .NET poderão falhar até o servidor ser reiniciado e a conclusão da instalação.  

**Ativação do Windows Communication Foundation (WCF):**  

-   Ativação HTTP  

-   Ativação não HTTP  

**Configuração do IIS:**

A configuração predefinida do IIS é necessária com as seguintes adições:  

-   Desenvolvimento de aplicações:  

    -   ASP.NET (e as opções selecionadas automaticamente)  

         Em alguns cenários, como o IIS está instalado ou reconfigurado após a versão 4.5.2 do .NET Framework está instalada, tem de ativar explicitamente ASP.NET versão 4.5. Por exemplo, num computador de 64 bits que executa a versão 4.0.30319 do .NET Framework, execute o seguinte comando: **%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i-permitir**  

**Memória do computador:**  

-   O computador que aloja esta função de sistema de sites tem de ter um mínimo de 5% da memória disponível do computador livre para permitir que a função de sistema de sites processe pedidos.  

-   Quando esta função de sistema de sites estiver colocalizada com outra função de sistema de sites que tem o mesmo requisito, este requisito de memória para o computador não aumenta, mas mantém-se como um mínimo de 5%.  

###  <a name="bkmk_2008EnrollProxpreq"></a>Ponto proxy de registo  
**.NET framework:**  

-   .NET framework 4.5.2  

     Quando esta função de sistema de sites é instalada, se o servidor já não tem uma versão suportada do .NET Framework instalado, o Configuration Manager instala automaticamente o .NET Framework 4.5.2. Esta instalação pode colocar o servidor para um Estado de reinício pendente. Quando está pendente um reinício para o .NET Framework, as aplicações .NET poderão falhar até o servidor ser reiniciado e a conclusão da instalação.  

**Ativação do Windows Communication Foundation (WCF):**  

-   Ativação HTTP  

-   Ativação não HTTP  

**Configuração do IIS:**

A configuração predefinida do IIS é necessária com as seguintes adições:  

-   Desenvolvimento de aplicações:  

    -   ASP.NET (e as opções selecionadas automaticamente)  

         Em alguns cenários, como o IIS está instalado ou reconfigurado após a versão 4.5.2 do .NET Framework está instalada, tem de ativar explicitamente ASP.NET versão 4.5. Por exemplo, num computador de 64 bits que executa a versão 4.0.30319 do .NET Framework, execute o seguinte comando: **%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i-permitir**  

**Memória do computador:**  

-   O computador que aloja esta função de sistema de sites tem de ter um mínimo de 5% da memória disponível do computador livre para permitir que a função de sistema de sites processe pedidos.  

-   Quando esta função de sistema de sites estiver colocalizada com outra função de sistema de sites que tem o mesmo requisito, este requisito de memória para o computador não aumenta, mas mantém-se como um mínimo de 5%.  

###  <a name="bkmk_2008FSPpreq"></a>Ponto de estado de contingência  
**Configuração do IIS:**

A configuração predefinida do IIS é necessária com as seguintes adições:  

-   Compatibilidade do IIS 6 de gestão:  

    -   Compatibilidade com Metabase do IIS 6  

###  <a name="bkmk_2008MPpreq"></a>Ponto de gestão  
**.NET framework:**  

-   .NET framework 4.5.2  

**Configuração do IIS:**

Pode utilizar a configuração predefinida do IIS ou uma configuração personalizada. Cada ponto de gestão que ativar para suportar dispositivos móveis requer configuração adicional do IIS para ASP.NET (e das opções selecionadas automaticamente).

Em alguns cenários, como o IIS está instalado ou reconfigurado após a versão 4.5.2 do .NET Framework está instalada, tem de ativar explicitamente ASP.NET versão 4.5. Por exemplo, num computador de 64 bits que executa a versão 4.0.30319 do .NET Framework, execute o seguinte comando: **%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i-permitir**  


Para utilizar uma configuração personalizada do IIS, tem de ativar as seguintes opções do IIS:  

-   Desenvolvimento de aplicações:  

    -   Extensões ISAPI  

-   Segurança:  

    -   Autenticação do Windows  

-   Compatibilidade do IIS 6 de gestão:  

    -   Compatibilidade com Metabase do IIS 6  

    -   Compatibilidade com WMI do IIS 6  


Quando utiliza uma configuração personalizada do IIS, pode remover opções que não são obrigatórias, como as seguintes:  

-   Funcionalidades HTTP comuns:  

    -   Redirecionamento HTTP  

-   Ferramentas e Scripts de gestão do IIS  

**Funcionalidade do Windows:**  

-   BITS extensões de servidor (e as opções selecionadas automaticamente) ou serviços de transferência inteligente em segundo plano (BITS) (e as opções selecionadas automaticamente)  

###  <a name="bkmk_2008RSpoint"></a>Ponto do Reporting Services  
**.NET framework:**  

-   .NET framework 4.5.2  

**SQL Server Reporting Services:**  

-   Tem de instalar e configurar pelo menos uma instância do SQL Server para suportar o SQL Server Reporting Services antes de instalar o reporting services ponto.  

-   A instância que utiliza para SQL Server Reporting Services pode ser a mesma instância que utiliza para a base de dados do site.  

-   Além disso, a instância que utiliza pode ser partilhada com outros produtos do System Center desde que outros produtos do System Center não tenham restrições de partilha da instância do SQL Server.  

###  <a name="bkmk_2008SCPpreq"></a>Ponto de ligação de serviço  
**.NET framework:**  

-   .NET framework 4.5.2  

     Quando esta função de sistema de sites é instalada, se o servidor já não tem uma versão suportada do .NET Framework instalado, o Configuration Manager instala automaticamente o .NET Framework 4.5.2. Esta instalação pode colocar o servidor para um Estado de reinício pendente. Quando está pendente um reinício para o .NET Framework, as aplicações .NET poderão falhar até o servidor ser reiniciado e a conclusão da instalação.  

**Do Visual C++ Redistributable:**  

-   Configuration Manager instala o pacote Microsoft Visual C++ 2013 Redistributable em cada computador que aloja um ponto de distribuição.  

-   A função de sistema de sites requer o x64 versão.  

###  <a name="bkmk_2008SUPpreq"></a>Ponto de atualização de software  
**.NET framework:**  

-   .NET framework 3.5 SP1 (ou posterior)  

-   .NET framework 4.5.2  

**Configuração do IIS:**

A configuração predefinida do IIS é necessária.  

**Windows Server Update Services:**  

-   Tem de instalar a função de servidor do Windows do Windows Server Update Services num computador antes de instalar um ponto de atualização de software.  

-   Para obter mais informações, veja [Planear atualizações de software no System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).

###  <a name="bkmk_2008SMPpreq"></a>Ponto de migração de estado  
**Configuração do IIS:**

A configuração predefinida do IIS é necessária.  
