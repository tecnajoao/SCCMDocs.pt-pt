---
title: 'Configurações suportadas para o LTSB '
titleSuffix: Configuration Manager
description: Compreenda o que sistemas operacionais e produtos dependentes funcionam com a longo prazo de manutenção ramo do System Center Configuration Manager.
ms.date: 5/10/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: f0f818d4-7f45-402f-8758-dc88bc024953
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e185244bda88c317e0157618f066056a817a1a82
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56141896"
---
# <a name="supported-configurations-for-the-long-term-servicing-branch-of-system-center-configuration-manager"></a>Configurações suportadas do Long term Servicing Branch do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (Long term Servicing Branch)*

Utilize as informações neste tópico para compreender que sistemas operativos e dependências de produto são suportadas pelo term Servicing Branch (LTSB) do Configuration Manager.
Se não indicação em contrário esta ou os tópicos específicos de LTSB, as mesmas configurações e limitações que se aplicam para a versão do Current Branch 1606 aplicam-se para o LTSB.  Quando ocorrem conflitos, utilize as informações que aplica-se para a edição que está a utilizar. Normalmente, o LTSB é mais limitado do que o ramo atual.

## <a name="general-statement-of-support"></a>Declaração de geral de suporte
Produtos e tecnologias que se seguem são suportadas por este ramo do Configuration Manager. No entanto, sua inclusão neste conteúdo não expressam uma extensão de suporte para qualquer produto ou versão além do ciclo de vida de suporte individual desse produto. Produtos que estejam fora do respetivo ciclo de vida de suporte não são suportados para utilização com o Configuration Manager. Para obter mais informações, visite o [ciclo de vida de suporte de Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=208270) Web site e leia a [FAQ sobre a política de ciclo de vida de suporte de Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=31976).

Além disso, produtos e versões de produto que não estão listadas nos tópicos seguintes não são suportadas a menos que foram anunciados no [blogue Enterprise Mobility + Security](https://blogs.technet.microsoft.com/enterprisemobility/).

**Limitações para futuro suporte:** O LTSB tem suporte limitado para futuros sistemas de operativos de servidor e cliente e dependências de produto. A lista de plataformas para o LTSB é fixa para o ciclo de vida da versão:

**Windows:**
- São suportadas apenas as atualizações qualidade e segurança para Windows.
- Não é adicionado nenhum suporte para ramificações atuais (CB), ramificações atuais for business (CBB), ou LTSB do Windows 10.
-   Não há suporte para novas versões principais do Windows Server.

**SQL Server:**
- Apenas qualidade e atualizações de segurança ou pequenas atualizações, como os service packs, é suportada para o SQL Server.
- Não há suporte para novas versões principais do SQL Server.  

## <a name="site-systems-and-servers"></a>Sistemas de sites e servidores
O LTSB suporta a utilização dos seguintes sistemas de operativos de computador Windows, como sistemas de sites.  Cada sistema operativo tem os mesmos requisitos e limitações, como a mesma entrada na [sistemas operativos suportados para servidores do sistema de sites](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).  Por exemplo, a instalação do Server Core do Windows 2012 R2 tem de ser um x64 versão, só é suportado para alojar um ponto de distribuição e não oferece suporte a PXE ou Multicast.

**Sistemas operativos suportados:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): Standard, Datacenter
- Windows Server 2012 (x64): Standard, Datacenter
- Windows Server 2008 R2 com SP1 (x64): Standard, Enterprise e Datacenter
- Windows Server 2008 with SP2 (x86, x64): Standard, Enterprise e Datacenter *(ver nota 1)*
- Windows 10 Enterprise 2015 LTSB (x86, x64)
- Windows 10 Enterprise 2016 LTSB (x86, x64)
- Windows 8.1 (x86, x64): Professional, Enterprise
- Windows 7 com SP1 (x86, x64): Professional, Enterprise, Ultimate
- A instalação do Server Core do Windows Server 2012
- A instalação do Server Core do Windows Server 2012 R2    

*Tenha em atenção 1*: Este sistema operativo não é suportado para servidores do site ou funções de sistema de sites com a exceção do ponto de distribuição e ponto de distribuição de extração. Pode continuar a utilizar este sistema operativo como um ponto de distribuição, até que a desaprovação deste suporte é anunciada ou o período de suporte expandido deste sistema operativo expira. Para obter mais informações, consulte [instalação do System Center Configuration Manager CB e LTSB falha no Windows Server 2008](https://support.microsoft.com/help/4015095).

## <a name="client-management"></a>Gestão de clientes
As seguintes secções identificam os sistemas de operativos de cliente que pode gerir com o LTSB. O LTSB não suporta a adição de novos sistemas operacionais, como clientes suportados.

### <a name="windows-computers"></a>Computadores Windows
Pode usar o LTSB para gerir os seguintes sistemas de operativos de computador de Windows com o software de cliente do Configuration Manager que está incluído com o Configuration Manager. Para obter mais informações, consulte [como implementar clientes em computadores do Windows no System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).

**Sistemas operativos suportados:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): Standard, Datacenter (Nota 1)
- Windows Server 2012 (x64): Standard, Datacenter (Nota 1)
- Windows Storage Server 2012 R2 (x64)
- Windows Storage Server 2012 (x64)
- Windows Server 2008 R2 com SP1 (x64): Standard, Enterprise e Datacenter (Nota 1)
- Windows Storage Server 2008 R2 (x86, x64): Workgroup, Standard, Enterprise
- Windows Server 2008 with SP2 (x86, x64): Standard, Enterprise e Datacenter (Nota 1)
- Windows 10 Enterprise 2015 LTSB (x86, x64)
- Windows 10 Enterprise 2016 LTSB (x86, x64)
- Windows 8.1 (x86, x64): Professional, Enterprise
- Windows 7 com SP1 (x86, x64): Professional, Enterprise, Ultimate
- A instalação do Server Core do Windows Server 2012 R2 (x64) (Nota 2)
- A instalação do Server Core do Windows Server 2012 (x64) (Nota 2)
- A instalação do Server Core do Windows Server 2008 R2 SP1 (x64)
- A instalação do Server Core do Windows Server 2008 SP2 (x86, x64)

**(Nota 1)**  Versões Datacenter têm suporte mas não estão certificadas para o Configuration Manager.  
**(Nota 2)**  Para suportar a instalação push do cliente, o computador que executa esta versão do sistema operativo tem de executar o serviço de função de servidor de ficheiros para a função de servidor de ficheiros e serviços de armazenamento. Para obter informações sobre como instalar funcionalidades do Windows num computador Server Core, consulte [instalar funções de servidor e funcionalidades num servidor Server Core](https://technet.microsoft.com/library/jj574158(v=ws.11).aspx) na Biblioteca TechNet do Windows Server 2012.

### <a name="windows-embedded"></a>Dispositivos Embedded
Pode utilizar o LTSB para gerir os seguintes dispositivos Windows Embedded ao instalar o software de cliente no dispositivo.  Para obter mais informações, consulte [planear a implementação do cliente em dispositivos Windows Embedded no System Center Configuration Manager](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices).

**Requisitos e limitações:**  

-   Todas as funcionalidades de cliente são suportadas em Embedded Windows suportados sistemas que não tenham filtros de escrita ativados.  

-   Os clientes que utilizam um dos seguintes são suportados para todas as funcionalidades, exceto a gestão de energia:  

    -   Filtros de escrita avançados (EWF)    

    -   Filtros de escrita baseados em ficheiros RAM (FBWF)    

    -   Filtros de escrita unificados (UWF)  

-   O catálogo de aplicações não é suportado por dispositivos Windows Embedded.  

-   Para poder monitorizar software maligno detetado em dispositivos Windows Embedded baseados no Windows XP, tem de instalar o pacote de criação de scripts do Microsoft Windows WMI no dispositivo incorporado. Utilize o Windows Embedded Target Designer para instalar este pacote. O *WBEMDISP. DLL* e *WBEMDISP. TLB* ficheiros deve existir e estar registados na pasta %windir%\System32\WBEM no dispositivo incorporado para garantir que o malware é comunicado a deteção.  

**Sistemas operativos suportados:**  
-   Windows 10 Enterprise 2016 LTSB (x86, x64)  
-   Windows 10 Enterprise 2015 LTSB (x86, x64)  
-   Windows Embedded 8.1 Industry (x86, x64)    
-   Windows Thin PC (x86, x64)    
-   Windows Embedded POSReady 7 (x86, x64)    
-   Windows Embedded Standard 7 com SP1 (x86, x64)    
-   Windows Embedded POSReady 2009 (x86)   
-   Windows Embedded Standard 2009 (x86)  

### <a name="windows-ce"></a>Windows CE  
 Pode gerir dispositivos Windows CE com o cliente legado de dispositivo móvel do Configuration Manager está incluído com o Configuration Manager.  

**Requisitos e limitações:**  

-   O cliente de dispositivo móvel precisa de 0,78 MB de espaço de armazenamento instalar o cliente. Um dispositivo móvel pode exigir até 256 KB de espaço de armazenamento adicional iniciar sessão.    

-   Recursos para estes dispositivos móveis variam consoante a plataforma e o cliente do tipo. Para obter informações sobre o tipo de funções de gestão do Configuration Manager suporta para um cliente legacy de dispositivo móvel, consulte [escolher uma solução de gestão de dispositivos para o System Center Configuration Manager](/sccm/core/plan-design/choose-a-device-management-solution).  

**Sistemas operativos suportados:**  

-   Windows CE 7.0 (ARM e x86 processadores)  

**Idiomas suportados incluem:**  
-   Chinês (simplificado e tradicional)    
-   English (US)    
-   Francês (França)    
-   Alemão    
-   Italiano    
-   Japonês  
-   Coreano  
-   Português (Brasil)  
-   Russo  
-   Espanhol (Espanha)  

### <a name="mac-computers"></a>Computadores Mac  
 Pode usar o LTSB para gerir computadores Mac OS X com o cliente do Configuration Manager para Mac.

O pacote de instalação de cliente de Mac não é fornecido com o suporte de dados do Configuration Manager. Pode baixá-lo como parte do download do "clientes para sistemas operativos adicionais" a partir da [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkID=525184).  

Suporte para sistemas de operativos Mac está limitado às apresentadas nesta secção. Suporte não inclui os sistemas operativos adicionais que pode ser suportados por uma atualização futura para pacotes de instalação de cliente Mac para o ramo atual.

Para obter mais informações, consulte [como implementar clientes em Macs no System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-macs).

**Versões suportadas:**  
-   Mac OS X 10.9 (Mavericks)  
-   Mac OS X 10.10 (Yosemite)  
-   Mac OS X 10.11 (El Capitan)  

## <a name="linux-and-unix-servers"></a>Servidores Linux e UNIX
Pode utilizar o LTSB para gerir servidores Linux e UNIX com o cliente do Configuration Manager para Linux e UNIX.

Os pacotes de instalação de cliente de Linux e UNIX não são fornecidos com o suporte de dados do Configuration Manager. Pode transferi-los como parte do download do "clientes para sistemas operativos adicionais" a partir da [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkID=525184). Para além de pacotes de instalação de cliente, a transferência do cliente inclui o script de instalação que gere a instalação do cliente em cada computador.

Suporte para sistemas operativos Linux e UNIX é limitado às apresentadas nesta secção. Suporte não inclui os sistemas operativos adicionais que pode ser suportados por uma atualização futura para pacotes de cliente para Linux e UNIX para o ramo atual.

**Requisitos e limitações:**  

-   Para rever as dependências de ficheiros de sistema operativo para o cliente para Linux e UNIX, consulte [pré-requisitos para implementação do cliente para servidores Linux e UNIX](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers#bkmk_clientdeployprereqforlnu).  
-   Para uma descrição geral das capacidades de gestão suportadas dos computadores que executam o Linux ou UNIX, consulte [como implementar clientes em servidores UNIX e Linux no System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-unix-and-linux-servers).  
-   Para obter versões suportadas do Linux e UNIX, a versão indicada inclui todas a versões secundárias subsequente. Por exemplo, em que o suporte é indicado para a versão do CentOS 6, isso também inclui todas as versões secundárias subsequentes do CentOS 6, como o CentOS 6.3. Da mesma forma, quando o suporte está listado para um sistema operativo que utiliza service packs, como o SUSE Linux Enterprise Server 11 SP1, o suporte inclui service packs subsequentes para essa versão do sistema operativo.
-   Para obter informações sobre pacotes de instalação de cliente e do agente Universal, consulte [como implementar clientes em servidores UNIX e Linux no System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-unix-and-linux-servers).


**Versões suportadas:**   
As seguintes versões são suportadas ao utilizar o ficheiro. tar indicado.  
### <a name="aix"></a>AIX  

|Versão|Ficheiro|  
|-|-|  
|Versão 5.3 (Power)|ccm-Aix53ppc.&lt;build\>.tar|  
|Versão 6.1 (Power)|ccm-Aix61ppc.&lt;build\>.tar|  
|Versão 7.1 (Power)|ccm-Aix71ppc.&lt;build\>.tar|  

### <a name="centos"></a>CentOS  

|Versão|Ficheiro|  
|-|-|  
|Versão 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 7 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="debian"></a>Debian  

|Versão|Ficheiro|    
|-|-|  
|Versão 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 6x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 7 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 7 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 8 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 8 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="hp-ux"></a>HP-UX  

|Versão|Ficheiro|  
|-|-|  
|Versão 11iv2 IA64|ccm-HpuxB.11.23i64.&lt;build\>.tar|  
|Versão 11iv2 PA-RISC|ccm-HpuxB.11.23PA.&lt;build\>.tar|  
|Versão 11iv3 IA64|ccm-HpuxB.11.31i64.&lt;build\>.tar|  
|Versão 11iv3 PA-RISC|ccm-HpuxB.11.31PA.&lt;build\>.tar|  

### <a name="oracle-linux"></a>Oracle Linux  

|Versão|Ficheiro|    
|-|-|  
|Versão 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 7 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|Versão|Ficheiro|  
|-|-|  
|Versão 4 x86|ccm-RHEL4x86.&lt;build\>.tar|  
|Versão 4 x64|ccm-RHEL4x64.&lt;build\>.tar|  
|Versão 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 7 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="solaris"></a>Solaris  

|Versão|Ficheiro|   
|-|-|  
|Versão 9 SPARC|ccm-Sol9sparc.&lt;build\>.tar|  
|Versão 10 x86|ccm-Sol10x86.&lt;build\>.tar|  
|Versão 10 SPARC|ccm-Sol10sparc.&lt;build\>.tar|  
|Versão 11 x86|ccm-Sol11x86.&lt;build\>.tar|  
|Versão 11 SPARC|ccm-Sol11sparc.&lt;build\>.tar|  

### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|Versão|Ficheiro|  
|-|-|  
|Versão 9 x86|ccm-SLES9x86.&lt;build\>.tar|  
|Versão 10 SP1 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 10 SP1 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 11 SP1 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 11 SP1 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 12 x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="ubuntu"></a>Ubuntu  

|Versão|Ficheiro|    
|-|-|  
|Versão 10.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 10.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 12.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 12.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 14.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 14.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  

### <a name="exchange-server-connector"></a>Conector do Exchange Server
 O LTSB suporta a gestão limitada de dispositivos que se ligam à sua instância do Exchange Server, sem instalar o software de cliente. Para obter mais informações, veja [Gerir dispositivos móveis com o System Center Configuration Manager e o Exchange](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).

 **Requisitos e limitações:**  

-   O Configuration Manager oferece gestão limitada para dispositivos móveis. Gestão limitada está disponível quando utiliza o conector do Exchange Server para dispositivos compatíveis com o Exchange Active Sync (EAS) que se ligam a um servidor com o Exchange Server ou o Exchange Online.  

-   Para obter mais informações sobre as funções de gerenciamento do Configuration Manager suporta para dispositivos móveis que gere o conector do Exchange Server, consulte [escolher uma solução de gestão de dispositivos do System Center Configuration Manager](/sccm/core/plan-design/choose-a-device-management-solution).  

**Versões suportadas do Exchange Server:**  
-   Exchange Server 2010 SP1  
-   Exchange Server 2010 SP2  
-   Exchange Server 2013  

> [!NOTE]
> O LTSB não suporta a gestão de dispositivos que ligam através de um serviço online, como o Exchange Online (Office 365).


## <a name="configuration-manager-console"></a>Consola do Configuration Manager
O LTSB suporta os seguintes sistemas operativos para executar a consola do Configuration Manager. Cada computador que aloja a consola tem de ter uma versão mínima do .NET Framework 4.5.2, exceto para o Windows 10, que requer um mínimo de .NET Framework 4.6.

**Sistemas operativos suportados:**
- Windows Server 2016
- Windows Server 2012 R2 (x64): Standard, Datacenter
- Windows Server 2012 (x64): Standard, Datacenter
- Windows Server 2008 R2 com SP1 (x64): Standard, Enterprise e Datacenter
- Windows Server 2008 with SP2 (x86, x64): Standard, Enterprise e Datacenter
- Windows 10 Enterprise 2016 LTSB (x86, x64)
- Windows 10 Enterprise 2015 LTSB (x86, x64)
- Windows 8.1 (x86, x64): Professional, Enterprise
- Windows 7 com SP1 (x86, x64): Professional, Enterprise, Ultimate


## <a name="sql-server-versions-supported-for-the-site-database-and-reporting-point"></a>Versões do SQL Server suportadas para a base de dados do site e o ponto do reporting
O LTSB suporta as seguintes versões do SQL Server para alojar a base de dados do site e o ponto do reporting. Para cada suportada a versão, os mesmos requisitos de configuração e as limitações que são apresentados no [suporte para versões do SQL Server](/sccm/core/plan-design/configs/support-for-sql-server-versions) para o ramo atual aplicam-se para o LTSB.  Isto inclui o uso de um Cluster do SQL Server ou um grupo de Disponibilidade AlwaysOn do SQL Server.  

**Versões suportadas:**

- SQL Server 2016: Standard, Enterprise
- SQL Server 2014 SP2: Standard, Enterprise
- SQL Server 2014 SP1: Standard, Enterprise
- SQL Server 2012 SP3: Standard, Enterprise
- SQL Server 2008 R2 SP3: Standard, Enterprise e Datacenter
- SQL Server 2016 Express
- SQL Server 2014 Express SP2
- SQL Server 2014 Express SP1
- SQL Server 2012 Express SP3

## <a name="support-for-active-directory-domains"></a>Suporte para domínios do Active Directory
Todos os sistemas de sites LTSB têm de ser membros de um domínio do Active Directory do Windows suportado. Suporte para domínios do Active Directory tem os requisitos e limitações que os que são apresentados no mesmo [suporte para domínios do Active Directory](/sccm/core/plan-design/configs/support-for-active-directory-domains), mas está limitado aos seguintes níveis funcionais de domínio:

**Níveis de suporte:**
- Windows Server 2008
- Windows Server 2008 R2
- Windows Server 2012
- Windows Server 2012 R2

## <a name="additional-support-topics-that-apply-to-the-long-term-servicing-branch"></a>Tópicos de suporte adicionais que se aplicam a term Servicing Branch
As informações nos tópicos seguintes do Current Branch aplicam-se para o LTSB:
- [Dimensionamento e números da escala](/sccm/core/plan-design/configs/size-and-scale-numbers)
- [Pré-requisitos do site e sistema de sites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)
- [Opções de elevada disponibilidade](/sccm/protect/understand/high-availability-options)
- [Hardware recomendado](/sccm/core/plan-design/configs/recommended-hardware)
- [Suporte para funcionalidades e redes do Windows](/sccm/core/plan-design/configs/support-for-windows-features-and-networks)
- [Suporte para ambientes de Virtualização](/sccm/core/plan-design/configs/support-for-virtualization-environments)
