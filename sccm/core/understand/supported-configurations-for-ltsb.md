---
title: "Configurações suportadas para o LTSB | Documentos do Microsoft"
description: "Compreenda o que sistemas operativos e os produtos dependentes funcionam com a longo prazo manutenção ramo do System Center Configuration Manager."
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
ms.sourcegitcommit: f809c9327db9f298168674add2d09820fdecd1b8
ms.openlocfilehash: ec33d5febcbf7b57e220f7fe27db9671080fecff
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="supported-configurations-for-the-long-term-servicing-branch-of-system-center-configuration-manager"></a>Configurações suportadas para o ramo longa duração de manutenção do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramo longa duração de manutenção)*

Utilize as informações deste tópico para compreender quais os sistemas operativos e as dependências de produto são suportadas pela longo prazo manutenção ramo (LTSB) do Configuration Manager.
Se não indicados caso contrário, isto ou os tópicos específicos LTSB, as mesmas configurações e limitações aplicam-se para a versão atual ramo 1606 aplicam-se para o LTSB.  Quando ocorrem conflitos, utilize as informações que se aplica a edição que estiver a utilizar. Normalmente, o LTSB que é mais limitada o ramo atual.

## <a name="general-statement-of-support"></a>Falha da instrução geral de suporte
Os produtos e tecnologias que se seguem são suportadas por este ramo do Configuration Manager. No entanto, a respetiva inclusão neste conteúdo não rápidas uma extensão de suporte para qualquer produto ou a versão para além do ciclo de vida de suporte individuais desse produto. Produtos que se encontram para além do respetivo ciclo de vida de suporte não são suportados para utilização com o Configuration Manager. Para obter mais informações, visite o [ciclo de vida de suporte de Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=208270) Web site e de leitura a [FAQ de política de ciclo de vida de suporte Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=31976).

Além disso, produtos e versões de produto que não forem apresentadas nos tópicos seguintes não são suportadas, a menos que tenha sido comunicadas no [Enterprise Mobility + segurança blogue](https://blogs.technet.microsoft.com/enterprisemobility/).

**Limitações para futura suporte:** O LTSB limitou o suporte para sistemas de operativos de servidor e cliente futuros e dependências de produto. A lista de plataformas para o LTSB é fixo de vida da versão:

**Windows:**
- São suportadas apenas qualidade e segurança atualizações para o Windows.
- Sem suporte é adicionado para ramificações atuais (CB), atuais ramos para empresas (CBB), ou LTSB do Windows 10.
-    Sem suporte para novas versões principais do Windows Server.

**SQL Server:**
- Apenas qualidade e atualizações de segurança ou as atualizações secundárias, como pacotes de serviço, é suportada para o SQL Server.
- Sem suporte para novas versões principais do SQL Server.  

## <a name="site-systems-and-servers"></a>Sistemas de sites e servidores
O LTSB suporta a utilização dos seguintes sistemas de operativos de computador Windows, como sistemas de sites.  Cada sistema operativo tem os mesmos requisitos e limitações, como a entrada na mesma [sistemas operativos suportados para servidores do sistema de sites](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).  Por exemplo, a instalação Server Core do Windows 2012 R2 tem de ser um x64 versão, só é suportada para alojar um ponto de distribuição e não suporta PXE ou Multicast.

**Sistemas operativos suportados:**
- Windows Server 2016
- Windows Server 2012 (x64): Standard, Datacenter
- Windows Server 2008 R2 com SP1 (x64): Standard, Enterprise e Datacenter
- Windows Server 2008 com SP2 (x86, x64): Standard, Enterprise e Datacenter *(ver nota 1)*
- Windows 10 Enterprise 2015 LTSB (x86, x64)
- Windows 10 Enterprise 2016 LTSB (x86, x64)
- Windows 8.1 (x86, x64): Professional, Enterprise
- Windows 7 com SP1 (x86, x64): Professional, Enterprise, Ultimate
- A instalação Server Core do Windows Server 2012
- A instalação Server Core do Windows Server 2012 R2    

*Tenha em atenção 1*: Este sistema operativo não é suportado para servidores de site ou funções de sistema de sites com a exceção do ponto de distribuição e ponto de distribuição de solicitação. Pode continuar a utilizar este sistema operativo como um ponto de distribuição até preterição deste suporte é anunciada ou do período de suporte alargado este sistema operativo. Para obter mais informações, consulte o artigo [instalação do System Center Configuration Manager CB e LTSB falha no Windows Server 2008](https://support.microsoft.com/help/4015095).

## <a name="client-management"></a>Gestão de clientes
As secções seguintes identificam os sistemas operativos cliente que possa gerir com o LTSB. O LTSB não suporta a adição de novos sistemas operativos como clientes suportados.

### <a name="windows-computers"></a>Computadores com o Windows
Pode utilizar o LTSB para gerir os seguintes Windows sistemas operativos dos computadores com o software de cliente do Configuration Manager que está incluído com o Configuration Manager. Para obter mais informações, consulte o artigo [como implementar clientes em computadores com Windows no System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).

**Sistemas operativos suportados:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): Standard, Datacenter (Nota 1)
- Windows Server 2012 (x64): Standard, Datacenter (Nota 1)
- Windows Storage Server 2012 R2 (x64)
- Servidor de armazenamento do Windows 2012 (x64)
- Windows Server 2008 R2 com SP1 (x64): Standard, Enterprise e Datacenter (Nota 1)
- Windows Storage Server 2008 R2 (x86, x64): Grupo de trabalho, Standard, Enterprise
- Windows Server 2008 com SP2 (x86, x64): Standard, Enterprise e Datacenter (Nota 1)
- Windows 10 Enterprise 2015 LTSB (x86, x64)
- Windows 10 Enterprise 2016 LTSB (x86, x64)
- Windows 8.1 (x86, x64): Professional, Enterprise
- Windows 7 com SP1 (x86, x64): Professional, Enterprise, Ultimate
- A instalação Server Core do Windows Server 2012 R2 (x64) (Nota 2)
- A instalação Server Core do Windows Server 2012 (x64) (Nota 2)
- A instalação Server Core do Windows Server 2008 R2 SP1 (x64)
- A instalação Server Core do Windows Server 2008 SP2 (x86, x64)

**(Nota 1)**  Versões do Centro de dados são suportadas mas não estão certificadas para o Configuration Manager.  
**(Nota 2)**  Para suportar a instalação push do cliente, o computador que executa esta versão do sistema operativo tem de executar o serviço de função de servidor de ficheiros para a função de servidor de ficheiros e serviços de armazenamento. Para obter informações sobre a instalação de funcionalidades do Windows num computador Server Core, consulte o artigo [instalar funções e funcionalidades Server num servidor Server Core](https://technet.microsoft.com/library/jj574158(v=ws.11).aspx) na Biblioteca TechNet do Windows Server 2012.

### <a name="windows-embedded"></a>Dispositivos Embedded
Pode utilizar o LTSB para gerir os seguintes dispositivos Windows Embedded ao instalar o software de cliente no dispositivo.  Para obter mais informações, consulte o artigo [planeamento de implementação de cliente em dispositivos Windows Embedded no System Center Configuration Manager](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices).

**Requisitos e limitações:**  

-   Todas as funcionalidades do cliente são suportadas em suportados Windows Embedded sistemas que não tenham filtros de escrita ativados.  

-   Os clientes que utilizam um dos seguintes são suportados para todas as funcionalidades exceto a gestão de energia:  

    -   Filtros de escrita avançado (EWF)    

    -   RAM filtros de escrita baseados em ficheiros (FBWF)    

    -   Filtros de escrita unificado (UWF)  

-   O catálogo de aplicações não é suportado para todos os dispositivos Windows Embedded.  

-   Para poder monitorizar o software maligno detetado em dispositivos Windows Embedded baseados no Windows XP, tem de instalar o pacote de script do Microsoft Windows WMI no dispositivo incorporado. Utilize o Windows Embedded destino Designer para instalar este pacote. O *WBEMDISP. DLL* e *WBEMDISP. TLB* ficheiros tem de existir e estar registados na pasta %windir%\System32\WBEM no dispositivo incorporado para se certificar de que detetado software maligno é comunicado.  

**Sistemas operativos suportados:**  
-   Windows 10 Enterprise 2016 LTSB (x86, x64)  
-   Windows 10 Enterprise 2015 LTSB (x86, x64)  
-   Windows Embedded 8.1 Industry (x86, x64)    
-   Fino PC com Windows (x86, x64)    
-   Windows Embedded POSReady 7 (x86, x64)    
-   Windows Embedded Standard 7 com SP1 (x86, x64)    
-   Windows Embedded POSReady 2009 (x86)   
-   Windows Embedded Standard 2009 (x86)  

### <a name="windows-ce"></a>Windows CE  
 Pode gerir dispositivos Windows CE com o cliente legado de dispositivos móveis do Configuration Manager está incluído com o Configuration Manager.  

**Requisitos e limitações:**  

-   O cliente de dispositivo móvel requer 0.78 MB de espaço de armazenamento instalar o cliente. Um dispositivo móvel pode necessitar de até 256 KB de espaço de armazenamento adicional iniciar sessão.    

-   Funcionalidades para estes dispositivos móveis variam consoante a plataforma e o cliente tipo. Para obter informações sobre o tipo de funções de gestão que o Configuration Manager suporta para um cliente legado do dispositivo móvel, consulte o artigo [escolher uma solução de gestão de dispositivos para o System Center Configuration Manager](/sccm/core/plan-design/choose-a-device-management-solution).  

**Sistemas operativos suportados:**  

-   Windows CE 7.0 (ARM e x86 processadores)  

**Idiomas suportados incluem:**  
-   Chinês (simplificado e tradicional)    
-   Inglês (e.u.a.)    
-   Francês (França)    
-   Alemão    
-   Italiano    
-   Japonês  
-   Coreano  
-   Português (Brasil)  
-   Russo  
-   Espanhol (Espanha)  

### <a name="mac-computers"></a>Computadores Mac  
 Pode utilizar o LTSB para gerir computadores Mac OS X com o cliente do Configuration Manager para Mac.

O pacote de instalação de cliente de Mac não é fornecido com o suporte de dados do Configuration Manager. Pode transferi-lo como parte da transferência de "clientes para sistemas operativos adicionais" a partir de [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkID=525184).  

Suporte para sistemas operativos Mac está limitado às pessoas listados nesta secção. Suporte não inclui os sistemas operativos adicionais que podem ser suportados por uma atualização futura para pacotes de instalação de cliente de Mac para ramificação atual.

Para obter mais informações, consulte o artigo [como implementar clientes no System Center Configuration Manager de Macs](/sccm/core/clients/deploy/deploy-clients-to-macs).

**Versões suportadas:**  
-   Mac OS X 10.9 (Mavericks)  
-   Mac OS X 10.10 (Yosemite)  
-   Mac OS X 10.11 (El Capitan)  

## <a name="linux-and-unix-servers"></a>Servidores Linux e UNIX
Pode utilizar o LTSB para gerir servidores Linux e UNIX com o cliente do Configuration Manager para Linux e UNIX.

Os pacotes de instalação de cliente de Linux e UNIX não sejam fornecidos com o suporte de dados do Configuration Manager. Pode transferi-los como parte da transferência de "clientes para sistemas operativos adicionais" a partir de [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkID=525184). Para além de pacotes de instalação de cliente, o cliente transfira inclui o script de instalação que gere a instalação do cliente em cada computador.

Suporte para sistemas operativos Linux e UNIX está limitado às pessoas listados nesta secção. Suporte não inclui os sistemas operativos adicionais que podem ser suportados por uma atualização futura a pacotes de cliente de Linux e UNIX para ramificação atual.

**Requisitos e limitações:**  

-   Para rever as dependências de ficheiros de sistema operativo para o cliente para Linux e UNIX, consulte o artigo [pré-requisitos para implementação do cliente para servidores Linux e UNIX](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers#bkmk_clientdeployprereqforlnu).  
-   Para obter uma descrição geral das funcionalidades de gestão suportado para computadores que executam o Linux ou UNIX, consulte o artigo [como implementar clientes em servidores UNIX e Linux no System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-unix-and-linux-servers).  
-   Para versões suportadas do Linux e UNIX, a versão indicada inclui todas as versões secundárias subsequentes. Por exemplo, em que o suporte é indicado para a versão de CentOS 6, isto também inclui todas as versões secundárias subsequentes do 6 CentOS, tais como CentOS 6.3. Da mesma forma, quando o suporte está listado para um sistema operativo que utiliza pacotes de serviço, tais como SUSE Linux Enterprise Server 11 SP1, o suporte inclui pacotes de serviço subsequentes à versão do sistema operativo.
-   Para obter informações sobre pacotes de instalação de cliente e o agente Universal, consulte o artigo [como implementar clientes em servidores UNIX e Linux no System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-unix-and-linux-servers).


**Versões suportadas:**   
São suportadas as seguintes versões utilizando o ficheiro .tar indicado.  
### <a name="aix"></a>AIX  

|Versão|Ficheiro|  
|-|-|  
|Versão 5.3 (Power)|CCM-Aix53ppc. &lt;construir\>.tar|  
|Versão 6.1 (Power)|CCM-Aix61ppc. &lt;construir\>.tar|  
|Versão 7.1 (Power)|CCM-Aix71ppc. &lt;construir\>.tar|  

### <a name="centos"></a>CentOS  

|Versão|Ficheiro|  
|-|-|  
|Versão 5 x86|CCM-Universalx86. &lt;construir\>.tar|  
|Versão 5 x64|CCM-Universalx64. &lt;construir\>.tar|  
|Versão 6 x86|CCM-Universalx86. &lt;construir\>.tar|  
|Versão 6 x64|CCM-Universalx64. &lt;construir\>.tar|  
|Versão 7 x64|CCM-Universalx64. &lt;construir\>.tar|  

### <a name="debian"></a>Debian  

|Versão|Ficheiro|    
|-|-|  
|Versão 5 x86|CCM-Universalx86. &lt;construir\>.tar|  
|Versão 5 x64|CCM-Universalx64. &lt;construir\>.tar|  
|Versão 6 x 86|CCM-Universalx86. &lt;construir\>.tar|  
|Versão 6 x64|CCM-Universalx64. &lt;construir\>.tar|  
|Versão 7 x86|CCM-Universalx86. &lt;construir\>.tar|  
|Versão 7 x64|CCM-Universalx64. &lt;construir\>.tar|  
|Versão 8 x86|CCM-Universalx86. &lt;construir\>.tar|  
|Versão 8 x64|CCM-Universalx64. &lt;construir\>.tar|  

### <a name="hp-ux"></a>HP-UX  

|Versão|Ficheiro|  
|-|-|  
|Versão 11iv2 IA64|CCM HpuxB.11.23i64. &lt;compilar\>.tar|  
|Versão 11iv2 PA-RISC|CCM HpuxB.11.23PA. &lt;compilar\>.tar|  
|Versão 11iv3 em IA64|CCM HpuxB.11.31i64. &lt;compilar\>.tar|  
|Versão 11iv3 PA-RISC|CCM HpuxB.11.31PA. &lt;construir\>.tar|  

### <a name="oracle-linux"></a>Oracle Linux  

|Versão|Ficheiro|    
|-|-|  
|Versão 5 x86|CCM-Universalx86. &lt;construir\>.tar|  
|Versão 5 x64|CCM-Universalx64. &lt;construir\>.tar|  
|Versão 6 x86|CCM-Universalx86. &lt;construir\>.tar|  
|Versão 6 x64|CCM-Universalx64. &lt;construir\>.tar|  
|Versão 7 x64|CCM-Universalx64. &lt;construir\>.tar|  

### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|Versão|Ficheiro|  
|-|-|  
|Versão 4 x86|CCM-RHEL4x86. &lt;construir\>.tar|  
|Versão 4 x64|CCM-RHEL4x64. &lt;construir\>.tar|  
|Versão 5 x86|CCM-Universalx86. &lt;construir\>.tar|  
|Versão 5 x64|CCM-Universalx64. &lt;construir\>.tar|  
|Versão 6 x86|CCM-Universalx86. &lt;construir\>.tar|  
|Versão 6 x64|CCM-Universalx64. &lt;construir\>.tar|  
|Versão 7 x64|CCM-Universalx64. &lt;construir\>.tar|  

### <a name="solaris"></a>Solaris  

|Versão|Ficheiro|   
|-|-|  
|Versão 9 SPARC|CCM-Sol9sparc. &lt;construir\>.tar|  
|Versão 10 x86|CCM-Sol10x86. &lt;construir\>.tar|  
|Versão 10 SPARC|CCM-Sol10sparc. &lt;construir\>.tar|  
|Versão 11 x86|CCM-Sol11x86. &lt;construir\>.tar|  
|Versão 11 SPARC|CCM-Sol11sparc. &lt;construir\>.tar|  

### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|Versão|Ficheiro|  
|-|-|  
|Versão 9 x86|CCM-SLES9x86. &lt;construir\>.tar|  
|SP1 versão 10 x86|CCM-Universalx86. &lt;construir\>.tar|  
|Versão 10 SP1 x64|CCM-Universalx64. &lt;construir\>.tar|  
|Versão 11 SP1 x86|CCM-Universalx86. &lt;construir\>.tar|  
|Versão 11 SP1 x64|CCM-Universalx64. &lt;construir\>.tar|  
|Versão 12 x64|CCM-Universalx64. &lt;construir\>.tar|  

### <a name="ubuntu"></a>Ubuntu  

|Versão|Ficheiro|    
|-|-|  
|Versão 10.04 LTS x86|CCM-Universalx86. &lt;construir\>.tar|  
|Versão 10.04 LTS x64|CCM-Universalx64. &lt;construir\>.tar|  
|Versão 12.04 LTS x86|CCM-Universalx86. &lt;construir\>.tar|  
|Versão 12.04 LTS x64|CCM-Universalx64. &lt;construir\>.tar|  
|Versão 14.04 LTS x86|CCM-Universalx86. &lt;construir\>.tar|  
|Versão 14.04 LTS x64|CCM-Universalx64. &lt;construir\>.tar|  

### <a name="exchange-server-connector"></a>Conector do Exchange Server
 O LTSB suporta a gestão limitada de dispositivos que ligam à sua instância do Exchange Server, sem instalar o software de cliente. Para obter mais informações, veja [Gerir dispositivos móveis com o System Center Configuration Manager e o Exchange](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).

 **Requisitos e limitações:**  

-   O Configuration Manager oferece gestão limitada para dispositivos móveis. Gestão limitada está disponível quando utiliza o conector do Exchange Server para dispositivos com capacidade de Exchange Active Sync (EAS) que ligam a um servidor com o Exchange Server ou ao Exchange Online.  

-   Para obter mais informações sobre as funções de gestão que o Configuration Manager suporta para dispositivos móveis que o conector do Exchange Server o gere, consulte o artigo [escolher uma solução de gestão de dispositivos para o System Center Configuration Manager](/sccm/core/plan-design/choose-a-device-management-solution).  

**Versões suportadas do Exchange Server:**  
-   Exchange Server 2010 SP1  
-   Exchange Server 2010 SP2  
-   Exchange Server 2013  

> [!NOTE]
> O LTSB não suporta a gestão de dispositivos que estabelecem ligação através de um serviço online, como o Exchange Online (Office 365).


## <a name="configuration-manager-console"></a>Consola do Configuration Manager
O LTSB suporta os seguintes sistemas operativos para executar a consola do Configuration Manager. Cada computador que aloja a consola tem de ter a versão mínima do .NET Framework do 4.5.2, exceto para o Windows 10, que requer um mínimo de .NET Framework 4.6.

**Sistemas operativos suportados:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): Standard, Datacenter
- Windows Server 2012 (x64): Standard, Datacenter
- Windows Server 2008 R2 com SP1 (x64): Standard, Enterprise e Datacenter
- Windows Server 2008 com SP2 (x86, x64): Standard, Enterprise e Datacenter
- Windows 10 Enterprise 2016 LTSB (x86, x64)
- Windows 10 Enterprise 2015 LTSB (x86, x64)
- Windows 8.1 (x86, x64): Professional, Enterprise
- Windows 7 com SP1 (x86, x64): Professional, Enterprise, Ultimate


## <a name="sql-server-versions-supported-for-the-site-database-and-reporting-point"></a>Versões do SQL Server suportadas para a base de dados do site e o ponto do reporting
O LTSB suporta as seguintes versões do SQL Server para alojar a base de dados do site e ponto do reporting. Para cada suportado versão, os mesmos requisitos de configuração e limitações que aparecem no [suporte das versões do SQL Server](/sccm/core/plan-design/configs/support-for-sql-server-versions) para o ramo atual aplicam-se para o LTSB.  Isto inclui a utilização de um Cluster de servidor do SQL Server ou um grupo de Disponibilidade AlwaysOn do SQL Server.  

**Versões suportadas:**

- SQL Server 2016: Standard, Enterprise
- SQL Server 2014 SP2: Standard, Enterprise
- SQL Server 2014 SP1: Standard, Enterprise
- SQL Server 2012 SP3: Standard, Enterprise
- SQL Server 2008 R2 SP3: Standard, Enterprise e Datacenter
- SQL Server 2016 Express
- SP2 Express do SQL Server 2014
- SQL Server 2014 Express SP1
- SQL Server 2012 Express SP3

## <a name="support-for-active-directory-domains"></a>Suporte para domínios do Active Directory
Todos os sistemas de sites LTSB tem de ser membros de um domínio do Active Directory do Windows suportado. Suporte para domínios do Active Directory tem os requisitos e limitações como aquelas que aparecem no mesmo [suporte para domínios do Active Directory](/sccm/core/plan-design/configs/support-for-active-directory-domains), mas está limitado aos seguintes níveis funcionais de domínio:

**Níveis de suportados:**
- Windows Server 2008
- Windows Server 2008 R2
- Windows Server 2012
- Windows Server 2012 R2

## <a name="additional-support-topics-that-apply-to-the-long-term-servicing-branch"></a>Tópicos de suporte adicionais que se aplicam para o ramo de manutenção de longo prazo
As informações nos seguintes tópicos de ramo atual aplicam-se para o LTSB:
- [Números de tamanho e a escala](/sccm/core/plan-design/configs/size-and-scale-numbers)
- [Site e os pré-requisitos de sistema de sites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)
- [Opções de elevada disponibilidade](/sccm/protect/understand/high-availability-options)
- [Hardware recomendado](/sccm/core/plan-design/configs/recommended-hardware)
- [Suporte para funcionalidades do Windows e as redes](/sccm/core/plan-design/configs/support-for-windows-features-and-networks)
- [Suporte para ambientes de Virtualização](/sccm/core/plan-design/configs/support-for-virtualization-environments)

