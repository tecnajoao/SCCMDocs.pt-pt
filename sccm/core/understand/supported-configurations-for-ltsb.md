---
title: "Configurações com suporte para o LTSB | Microsoft Docs"
description: "Entenda quais sistemas operacionais e produtos dependentes funcionam com a longo prazo manutenção ramificação do System Center Configuration Manager."
ms.custom: na
ms.date: 5/10/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f0f818d4-7f45-402f-8758-dc88bc024953
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: b0ba955aa7f854c3fa2c06ccf9ccd8ed354758b0
ms.openlocfilehash: 31bddee83b2365cfa903077ffaa1d7116b194378
ms.contentlocale: pt-pt
ms.lasthandoff: 06/12/2017


---
# <a name="supported-configurations-for-the-long-term-servicing-branch-of-system-center-configuration-manager"></a>Configurações com suporte para a ramificação de manutenção a longo prazo do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramificação de manutenção de longo prazo)*

Use as informações neste tópico para entender quais sistemas operacionais e as dependências de produto são suportadas pela longo prazo manutenção LTSB (Branch) do Configuration Manager.
Se não especificado o contrário nesta ou os tópicos específicos da LTSB, as mesmas configurações e limitações que se aplicam à versão da ramificação atual 1606 se aplicam ao LTSB.  Quando ocorrem conflitos, use as informações que se aplica à edição que você está usando. Normalmente, o LTSB é mais limitado que o Branch atual.

## <a name="general-statement-of-support"></a>Instrução geral de suporte
Os produtos e tecnologias a seguir têm suporte por esta ramificação do Configuration Manager. No entanto, sua inclusão nesse conteúdo não expressam a extensão de suporte para qualquer produto ou a versão além do ciclo de vida de suporte individual do produto. Não há suporte para produtos que estão além de seu ciclo de vida de suporte para uso com o Configuration Manager. Para obter mais informações, visite o [Microsoft Support Lifecycle](http://go.microsoft.com/fwlink/p/?LinkId=208270) site e ler o [perguntas frequentes sobre política de ciclo de vida do suporte Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=31976).

Além disso, os produtos e versões do produto que não estão listadas nos tópicos a seguir não têm suporte, a menos que eles foram apresentados no [Enterprise Mobility + segurança Blog](https://blogs.technet.microsoft.com/enterprisemobility/).

**Limitações de suporte futuro:** O LTSB tem suporte limitado para sistemas operacionais cliente e servidor futuros e dependências de produto. A lista de plataformas para o LTSB é fixo durante a vida útil da versão:

**Windows:**
- Há suporte para atualizações somente qualidade e segurança do Windows.
- Não há suporte é adicionada para ramificações atuais CB (), ramificações atuais para negócios (CBB) ou LTSB do Windows 10.
-   Não há suporte para novas versões principais do Windows Server.

**SQL Server:**
- Somente qualidade e atualizações de segurança ou atualizações secundárias como pacotes de serviço, há suporte para o SQL Server.
- Não há suporte para novas versões principais do SQL Server.  

## <a name="site-systems-and-servers"></a>Servidores e sistemas de site
O LTSB suporta o uso dos seguintes sistemas operacionais de computador Windows como sistemas de site.  Cada sistema operacional tem os mesmos requisitos e limitações, como a mesma entrada [sistemas operacionais com suporte para servidores de sistema de site](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).  Por exemplo, a instalação do Server Core do Windows 2012 R2 deve ser x64, somente há suporte para hospedar um ponto de distribuição e não oferece suporte a PXE ou Multicast.

**Sistemas operacionais com suporte:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): Standard, Datacenter
- Windows Server 2012 (x64): Standard, Datacenter
- Windows Server 2008 R2 com SP1 (x64): Standard, Enterprise e Datacenter
- Windows Server 2008 com SP2 (x86, x64): Standard, Enterprise e Datacenter *(veja a Observação 1)*
- Windows 10 Enterprise 2015 LTSB (x86, x64)
- Windows 10 Enterprise 2016 LTSB (x86, x64)
- Windows 8.1 (x86, x64): Professional, Enterprise
- Windows 7 com SP1 (x86, x64): Professional, Enterprise, Ultimate
- A instalação do Server Core do Windows Server 2012
- A instalação do Server Core do Windows Server 2012 R2    

*Observe 1*: Não há suporte para este sistema operacional para servidores do site ou funções de sistema de site com a exceção do ponto de distribuição e ponto de distribuição de recepção. Você pode continuar a usar este sistema operacional como um ponto de distribuição até que a desaprovação desse suporte seja anunciada ou o período de suporte estendido deste sistema operacional expire. Para obter mais informações, consulte [LTSB e instalação do System Center Configuration Manager CB falhar no Windows Server 2008](https://support.microsoft.com/help/4015095).

## <a name="client-management"></a>Gerenciamento de clientes
As seções a seguir identificam os sistemas operacionais de cliente que você pode gerenciar com o LTSB. O LTSB não oferece suporte à adição de novos sistemas operacionais como clientes com suporte.

### <a name="windows-computers"></a>Computadores com Windows
Você pode usar o LTSB para gerenciar os seguintes sistemas de operacionais de computador Windows com o software cliente do Configuration Manager que está incluído com o Configuration Manager. Para obter mais informações, consulte [como implantar clientes em computadores com Windows no System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).

**Sistemas operacionais com suporte:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): Standard, Datacenter (Observação 1)
- Windows Server 2012 (x64): Standard, Datacenter (Observação 1)
- Windows Storage Server 2012 R2 (x64)
- O Windows Storage Server 2012 (x64)
- Windows Server 2008 R2 com SP1 (x64): Standard, Enterprise e Datacenter (Observação 1)
- Windows Storage Server 2008 R2 (x86, x64): Workgroup, Standard, Enterprise
- Windows Server 2008 com SP2 (x86, x64): Standard, Enterprise e Datacenter (Observação 1)
- Windows 10 Enterprise 2015 LTSB (x86, x64)
- Windows 10 Enterprise 2016 LTSB (x86, x64)
- Windows 8.1 (x86, x64): Professional, Enterprise
- Windows 7 com SP1 (x86, x64): Professional, Enterprise, Ultimate
- A instalação do Server Core do Windows Server 2012 R2 (x64) (Observação 2)
- A instalação do Server Core do Windows Server 2012 (x64) (Observação 2)
- A instalação do Server Core do Windows Server 2008 R2 SP1 (x64)
- A instalação do Server Core do Windows Server 2008 SP2 (x86, x64)

**(Observação 1)**  Datacenter versões têm suporte, mas não de certificados para o Configuration Manager.  
**(Observação 2)**  Para dar suporte à instalação por push de cliente, o computador que executa esta versão do sistema operacional deve executar o serviço de função de servidor de arquivos para a função de servidor Serviços de arquivo e armazenamento. Para obter informações sobre como instalar recursos do Windows em um computador Server Core, consulte [instalar funções de servidor e recursos em um servidor Server Core](https://technet.microsoft.com/library/jj574158(v=ws.11).aspx) na biblioteca do TechNet do Windows Server 2012.

### <a name="windows-embedded"></a>Dispositivos Embedded
Você pode usar o LTSB para gerenciar os seguintes dispositivos Windows Embedded ao instalar o software cliente no dispositivo.  Para obter mais informações, consulte [planejar a implantação de cliente para dispositivos Windows Embedded no System Center Configuration Manager](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices).

**Requisitos e limitações:**  

-   Todos os recursos de cliente são suportados em Windows Embedded com suporte sistemas que não têm filtros de gravação habilitados.  

-   Os clientes que usam um dos procedimentos a seguir têm suporte para todos os recursos, exceto o gerenciamento de energia:  

    -   Filtros de gravação de EFW)    

    -   Filtros de gravação com base em arquivo de RAM (FBWF)    

    -   Filtros de gravação unificados UWF)  

-   Não há suporte para o catálogo de aplicativos para qualquer dispositivo Windows Embedded.  

-   Antes de você pode monitorar o malware detectado em dispositivos Windows Embedded baseados no Windows XP, você deve instalar o pacote de script WMI do Microsoft Windows no dispositivo inserido. Use o Windows Embedded Target Designer para instalar este pacote. O *WBEMDISP. DLL* e *WBEMDISP. TLB* arquivos deve existir e estar registrados na pasta %windir%\System32\WBEM no dispositivo inserido para garantir que o malware detectado seja relatado.  

**Sistemas operacionais com suporte:**  
-   Windows 10 Enterprise 2016 LTSB (x86, x64)  
-   Windows 10 Enterprise 2015 LTSB (x86, x64)  
-   Windows Embedded 8.1 Industry (x86, x64)    
-   Computador dinâmico do Windows (x86, x64)    
-   Windows Embedded POSReady 7 (x86, x64)    
-   Windows Embedded Standard 7 com SP1 (x86, x64)    
-   Windows Embedded POSReady 2009 (x86)   
-   Windows Embedded Standard 2009 (x86)  

### <a name="windows-ce"></a>Windows CE  
 Você pode gerenciar dispositivos com Windows CE com o cliente herdado do dispositivo móvel do Configuration Manager que está incluído com o Configuration Manager.  

**Requisitos e limitações:**  

-   O cliente de dispositivo móvel requer 0,78 MB de espaço de armazenamento instalar o cliente. Um dispositivo móvel pode exigir até 256 KB de espaço de armazenamento adicional entrar.    

-   Recursos para esses dispositivos móveis variam por plataforma e o cliente de tipo. Para obter informações sobre o tipo de funções de gerenciamento do Configuration Manager oferece suporte para um cliente herdado do dispositivo móvel, consulte [escolher uma solução de gerenciamento de dispositivo para o System Center Configuration Manager](/sccm/core/plan-design/choose-a-device-management-solution).  

**Sistemas operacionais com suporte:**  

-   Windows CE 7.0 (ARM e x86 processadores)  

**Idiomas com suporte incluem:**  
-   Chinês (simplificado e tradicional)    
-   Inglês (EUA)    
-   Francês (França)    
-   Alemão    
-   Italiano    
-   Japonês  
-   Coreano  
-   Português (Brasil)  
-   Russo  
-   Espanhol (Espanha)  

### <a name="mac-computers"></a>Computadores Mac  
 Você pode usar o LTSB para gerenciar computadores Mac OS X com o cliente do Configuration Manager para Mac.

O pacote de instalação do cliente Mac não é fornecido com a mídia do Configuration Manager. Você pode baixá-lo como parte do download "clientes para sistemas operacionais adicionais" o [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkID=525184).  

Suporte para sistemas operacionais de Mac é limitado aos listados nesta seção. O suporte não inclui os sistemas operacionais adicionais que podem ter suporte por uma atualização futura para pacotes de instalação do cliente Mac para a ramificação atual.

Para obter mais informações, consulte [como implantar clientes em Macs no System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-macs).

**Versões com suporte:**  
-   Mac OS X 10.9 (Mavericks)  
-   Mac OS X 10.10 (Yosemite)  
-   Mac OS X 10.11 (El Capitan)  

## <a name="linux-and-unix-servers"></a>Servidores Linux e UNIX
Você pode usar o LTSB para gerenciar servidores Linux e UNIX com o cliente do Configuration Manager para Linux e UNIX.

Os pacotes de instalação de cliente do Linux e UNIX não são fornecidos com a mídia do Configuration Manager. Você pode baixá-los como parte do download "clientes para sistemas operacionais adicionais" o [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkID=525184). Além dos pacotes de instalação do cliente, o download do cliente inclui o script de instalação que gerencia a instalação do cliente em cada computador.

Suporte para sistemas operacionais Linux e UNIX é limitado aos listados nesta seção. O suporte não inclui os sistemas operacionais adicionais que podem ter suporte por uma atualização futura para os pacotes de cliente Linux e UNIX para a ramificação atual.

**Requisitos e limitações:**  

-   Para examinar as dependências de arquivo do sistema operacional do cliente para Linux e UNIX, consulte [pré-requisitos para implantação de cliente para servidores Linux e UNIX](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers#bkmk_clientdeployprereqforlnu).  
-   Para obter uma visão geral dos recursos de gerenciamento com suporte para computadores que executam Linux ou UNIX, consulte [como implantar clientes para servidores UNIX e Linux no System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-unix-and-linux-servers).  
-   Para versões com suporte do Linux e UNIX, a versão listada inclui todas as versões secundárias subsequentes. Por exemplo, quando o suporte é indicado para o CentOS versão 6, isso também inclui qualquer versão secundária subsequente do CentOS 6, como o CentOS 6.3. Da mesma forma, quando o suporte for listado para um sistema operacional que usa service packs, como o SUSE Linux Enterprise Server 11 SP1, o suporte inclui service packs subsequentes para essa versão do sistema operacional.
-   Para obter informações sobre pacotes de instalação do cliente e o Universal Agent, consulte [como implantar clientes para servidores UNIX e Linux no System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-unix-and-linux-servers).


**Versões com suporte:**   
As seguintes versões têm suporte usando o arquivo. tar indicado.  
### <a name="aix"></a>AIX  

|Versão|Ficheiro|  
|-|-|  
|Versão 5.3 (Power)|CCM-Aix53ppc. &lt;build\>. tar|  
|Versão 6.1 (Power)|CCM-Aix61ppc. &lt;build\>. tar|  
|Versão 7.1 (Power)|CCM-Aix71ppc. &lt;build\>. tar|  

### <a name="centos"></a>CentOS  

|Versão|Ficheiro|  
|-|-|  
|Versão 5 x86|CCM-Universalx86. &lt;build\>. tar|  
|Versão 5 x64|CCM-Universalx64. &lt;build\>. tar|  
|Versão 6 x86|CCM-Universalx86. &lt;build\>. tar|  
|Versão 6 x64|CCM-Universalx64. &lt;build\>. tar|  
|Versão 7 x64|CCM-Universalx64. &lt;build\>. tar|  

### <a name="debian"></a>Debian  

|Versão|Ficheiro|    
|-|-|  
|Versão 5 x86|CCM-Universalx86. &lt;build\>. tar|  
|Versão 5 x64|CCM-Universalx64. &lt;build\>. tar|  
|Versão 6 x86|CCM-Universalx86. &lt;build\>. tar|  
|Versão 6 x64|CCM-Universalx64. &lt;build\>. tar|  
|Versão 7 x86|CCM-Universalx86. &lt;build\>. tar|  
|Versão 7 x64|CCM-Universalx64. &lt;build\>. tar|  
|Versão 8 x86|CCM-Universalx86. &lt;build\>. tar|  
|Versão 8 x64|CCM-Universalx64. &lt;build\>. tar|  

### <a name="hp-ux"></a>HP-UX  

|Versão|Ficheiro|  
|-|-|  
|Versão 11iv2 IA64|CCM-HpuxB.11.23i64. &lt;build\>. tar|  
|Versão 11iv2 PA-RISC|CCM-HpuxB.11.23PA. &lt;build\>. tar|  
|Versão 11iv3 IA64|CCM-HpuxB.11.31i64. &lt;build\>. tar|  
|Versão 11iv3 PA-RISC|CCM-HpuxB.11.31PA. &lt;build\>. tar|  

### <a name="oracle-linux"></a>Oracle Linux  

|Versão|Ficheiro|    
|-|-|  
|Versão 5 x86|CCM-Universalx86. &lt;build\>. tar|  
|Versão 5 x64|CCM-Universalx64. &lt;build\>. tar|  
|Versão 6 x86|CCM-Universalx86. &lt;build\>. tar|  
|Versão 6 x64|CCM-Universalx64. &lt;build\>. tar|  
|Versão 7 x64|CCM-Universalx64. &lt;build\>. tar|  

### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|Versão|Ficheiro|  
|-|-|  
|Versão 4 x86|CCM-RHEL4x86. &lt;build\>. tar|  
|Versão 4 x64|CCM-RHEL4x64. &lt;build\>. tar|  
|Versão 5 x86|CCM-Universalx86. &lt;build\>. tar|  
|Versão 5 x64|CCM-Universalx64. &lt;build\>. tar|  
|Versão 6 x86|CCM-Universalx86. &lt;build\>. tar|  
|Versão 6 x64|CCM-Universalx64. &lt;build\>. tar|  
|Versão 7 x64|CCM-Universalx64. &lt;build\>. tar|  

### <a name="solaris"></a>Solaris  

|Versão|Ficheiro|   
|-|-|  
|Versão 9 SPARC|CCM-Sol9sparc. &lt;build\>. tar|  
|Versão 10 x86|CCM-Sol10x86. &lt;build\>. tar|  
|Versão 10 SPARC|CCM-Sol10sparc. &lt;build\>. tar|  
|Versão 11 x86|CCM-Sol11x86. &lt;build\>. tar|  
|Versão 11 SPARC|CCM-Sol11sparc. &lt;build\>. tar|  

### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|Versão|Ficheiro|  
|-|-|  
|Versão 9 x86|CCM-SLES9x86. &lt;build\>. tar|  
|Versão 10 SP1 x86|CCM-Universalx86. &lt;build\>. tar|  
|Versão 10 SP1 x64|CCM-Universalx64. &lt;build\>. tar|  
|Versão 11 SP1 x86|CCM-Universalx86. &lt;build\>. tar|  
|Versão 11 SP1 x64|CCM-Universalx64. &lt;build\>. tar|  
|Versão 12 x64|CCM-Universalx64. &lt;build\>. tar|  

### <a name="ubuntu"></a>Ubuntu  

|Versão|Ficheiro|    
|-|-|  
|Versão 10.04 LTS x86|CCM-Universalx86. &lt;build\>. tar|  
|Versão 10.04 LTS x64|CCM-Universalx64. &lt;build\>. tar|  
|Versão 12.04 LTS x86|CCM-Universalx86. &lt;build\>. tar|  
|Versão 12.04 LTS x64|CCM-Universalx64. &lt;build\>. tar|  
|Versão 14.04 LTS x86|CCM-Universalx86. &lt;build\>. tar|  
|Versão 14.04 LTS x64|CCM-Universalx64. &lt;build\>. tar|  

### <a name="exchange-server-connector"></a>Conector do Exchange Server
 O LTSB oferece suporte a gerenciamento limitado de dispositivos que se conectam à instância do Exchange Server, sem instalar o software cliente. Para obter mais informações, veja [Gerir dispositivos móveis com o System Center Configuration Manager e o Exchange](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).

 **Requisitos e limitações:**  

-   Configuration Manager oferece gerenciamento limitado para dispositivos móveis. Gerenciamento limitado está disponível quando você usar o conector do Exchange Server para dispositivos habilitados para EAS Exchange Active Sync () que se conectam a um servidor que executa o Exchange Server ou Exchange Online.  

-   Para obter mais informações sobre as funções de gerenciamento do Configuration Manager oferece suporte para dispositivos móveis que gerencia o conector do Exchange Server, consulte [escolher uma solução de gerenciamento de dispositivo para o System Center Configuration Manager](/sccm/core/plan-design/choose-a-device-management-solution).  

**Versões com suporte do Exchange Server:**  
-   Exchange Server 2010 SP1  
-   O Exchange Server 2010 SP2  
-   Exchange Server 2013  

> [!NOTE]
> O LTSB não dá suporte para o gerenciamento de dispositivos que se conectam por meio de um serviço online, como o Exchange Online (Office 365).


## <a name="configuration-manager-console"></a>Consola do Configuration Manager
O LTSB oferece suporte a sistemas operacionais a seguir para executar o console do Configuration Manager. Cada computador que hospeda o console deve ter uma versão do .NET Framework mínima de 4.5.2, exceto o Windows 10, que requer um mínimo de .NET Framework 4.6.

**Sistemas operacionais com suporte:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): Standard, Datacenter
- Windows Server 2012 (x64): Standard, Datacenter
- Windows Server 2008 R2 com SP1 (x64): Standard, Enterprise e Datacenter
- Windows Server 2008 com SP2 (x86, x64): Standard, Enterprise e Datacenter
- Windows 10 Enterprise 2016 LTSB (x86, x64)
- Windows 10 Enterprise 2015 LTSB (x86, x64)
- Windows 8.1 (x86, x64): Professional, Enterprise
- Windows 7 com SP1 (x86, x64): Professional, Enterprise, Ultimate


## <a name="sql-server-versions-supported-for-the-site-database-and-reporting-point"></a>Versões do SQL Server com suporte para o banco de dados do site e ponto de relatório
O LTSB suporta as seguintes versões do SQL Server para hospedar o banco de dados do site e o ponto de relatório. Para cada um com suporte de versão, os mesmos requisitos de configuração e limitações que aparecem no [suporte para versões do SQL Server](/sccm/core/plan-design/configs/support-for-sql-server-versions) para a ramificação atual aplicar o LTSB.  Isso inclui o uso de um Cluster do SQL Server ou um grupo de disponibilidade do AlwaysOn do SQL Server.  

**Versões com suporte:**

- SQL Server 2016: Standard, Enterprise
- SQL Server 2014 SP2: Standard, Enterprise
- SQL Server 2014 SP1: Standard, Enterprise
- SQL Server 2012 SP3: Standard, Enterprise
- O SQL Server 2008 R2 SP3: Standard, Enterprise e Datacenter
- SQL Server 2016 Express
- SQL Server 2014 Express SP2
- SQL Server 2014 Express SP1
- SQL Server 2012 Express SP3

## <a name="support-for-active-directory-domains"></a>Suporte para domínios do Active Directory
Todos os sistemas de site LTSB devem ser membros de um domínio do Active Directory do Windows com suporte. Suporte para domínios do Active Directory tem os mesmos requisitos e limitações que aparecem no [suporte para domínios do Active Directory](/sccm/core/plan-design/configs/support-for-active-directory-domains), mas é limitado para os seguintes níveis funcionais de domínio:

**Níveis com suporte:**
- Windows Server 2008
- Windows Server 2008 R2
- Windows Server 2012
- Windows Server 2012 R2

## <a name="additional-support-topics-that-apply-to-the-long-term-servicing-branch"></a>Tópicos de suporte adicionais que se aplicam a ramificação de manutenção a longo prazo
Aplicar as informações nos tópicos a seguir de ramificação atual para o LTSB:
- [Dimensionamento e números da escala](/sccm/core/plan-design/configs/size-and-scale-numbers)
- [Pré-requisitos do site e sistema de sites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)
- [Opções de elevada disponibilidade](/sccm/protect/understand/high-availability-options)
- [Hardware recomendado](/sccm/core/plan-design/configs/recommended-hardware)
- [Suporte para funcionalidades e redes do Windows](/sccm/core/plan-design/configs/support-for-windows-features-and-networks)
- [Suporte para ambientes de virtualização](/sccm/core/plan-design/configs/support-for-virtualization-environments)

