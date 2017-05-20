---
title: Os clientes e dispositivos suportados | Documentos do Microsoft
description: Saiba que sistemas de operativos System Center Configuration Manager suporta para os clientes e dispositivos.
ms.custom: na
ms.date: 2/6/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 87f4e041-67df-4c61-aa98-7444faffe565
caps.latest.revision: 5
author: arob98
ms.author: angrobe
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: d5166b16ffbe46af561b1ce98c0494cc4aaa72a8
ms.openlocfilehash: cd7b8bf35aeb26c8b7b37f6faa51c9a09138fdb9
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="supported-operating-systems-for-clients-and-devices-for-system-center-configuration-manager"></a>Sistemas operativos suportados para os clientes e dispositivos para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


 System Center Configuration Manager suporta a instalação de software de cliente numa variedade de computadores Windows, Mac, Linux e UNIX.  

 **Requisitos e limitações para todos os clientes:**  

-   Alterar o tipo de arranque ou **iniciar sessão como** definições para qualquer Configuration Manager service não é suportado e pode impedir que a chave serviços a partir da funcionar corretamente.    

-   Instalar ou a executar o cliente do Configuration Manager para Linux e UNIX ou o cliente de Mac em computadores através de uma conta diferente de raiz não é suportada. Fazê-lo pode impedir que os serviços de chave a funcionar corretamente.  

##  <a name="windows-computers"></a>Computadores com o Windows  
 Pode utilizar o cliente do Configuration Manager que está incluído com o Configuration Manager para gerir os seguintes sistemas operativos Windows. Para obter mais informações, consulte o artigo [como implementar clientes em computadores com Windows no System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-windows-computers.md).  

**Sistemas operativos suportados:**  


-  **Windows Server 2016**: Standard, Datacenter <sup>1</sup>
  - Este sistema operativo é suportado a partir do Configuration Manager versão 1606, com o rollup de correção de KB3186654 (ou a versão de linha de base do 1606, que foi lançada em Outubro de 2016).  

-   **Windows Server 2012 R2** (x64): Standard, Datacenter <sup>1</sup>    

-   **Armazenamento do Windows Server 2012 R2** (x64)    

-   **Windows Server 2012** (x64): Standard, Datacenter <sup>1</sup>    

-   **Servidor de armazenamento do Windows 2012** (x64)    

-   **Windows Server 2008 R2 com SP1** (x64): Standard, Enterprise e Datacenter <sup>1</sup>    

-   **Windows Storage Server 2008 R2** (x86, x64): Grupo de trabalho, Standard, Enterprise    

-   **Windows Server 2008 com SP2** (x86, x64): Standard, Enterprise e Datacenter <sup>1</sup>    

-   **Windows 10**: Pro, Enterprise  
   Consulte o artigo [suporte das versões do Windows 10](/sccm/core/plan-design/configs/support-for-windows-10) para obter detalhes sobre os diferentes versões do Windows 10 que são suportadas pelas diversas versões do Configuration Manager da versão.

-   **Windows 8.1** (x86, x64): Professional, Enterprise    

-   **Windows 8** (x86, x64): Professional, Enterprise    

-   **Windows 7 com SP1** (x86, x64): Professional, Enterprise e Ultimate    

-   **A instalação Server Core do Windows Server 2016** (x64) <sup>2</sup>
  - Este sistema operativo é suportado a partir versão 1606 com o rollup de correção da KB3186654 (ou a versão de linha de base do 1606, que foi lançada em Outubro de 2016). 


-   **A instalação Server Core do Windows Server 2012 R2** (x64) <sup>2</sup>    

-   **A instalação Server Core do Windows Server 2012** (x64) <sup>2</sup>    

-   **A instalação Server Core do Windows Server 2008 R2**  
    **(sem nenhum service pack ou com o SP1)**  (x64)    

-   **A instalação Server Core do Windows Server 2008 SP2** (x86, x64)  

 <sup>1</sup> versões do Centro de dados são suportadas mas não estão certificadas para o Configuration Manager. Suporte de correção não lhe é oferecido para problemas que são específicos para o Windows Server Datacenter Edition.  

 <sup>2</sup> para suportar a instalação push do cliente, o computador que executa esta versão do sistema operativo tem de executar o serviço de função de servidor de ficheiros para a função de servidor de ficheiros e serviços de armazenamento. Para obter informações sobre a instalação de funcionalidades do Windows num computador Server Core, consulte o artigo [instalar funções e funcionalidades Server num servidor Server Core](http://go.microsoft.com/fwlink/p/?LinkId=299359) na Biblioteca TechNet do Windows Server 2012.  


##  <a name="windows-embedded-computers"></a>Computadores Windows Embedded  
 Pode gerir dispositivos Windows Embedded ao instalar o software de cliente do Configuration Manager no dispositivo.  Para obter mais informações, consulte o artigo [planeamento de implementação de cliente em dispositivos Windows Embedded no System Center Configuration Manager](../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

**Requisitos e limitações:**  

-   Todas as funcionalidades do cliente são suportadas num Windows Embedded sistemas que não tenham filtros de escrita ativados.  

-   Os clientes que utilizam um dos seguintes são suportados para todas as funcionalidades exceto a gestão de energia:  

    -   Filtros de escrita avançado (EWF)    

    -   RAM filtros de escrita baseados em ficheiros (FBWF)    

    -   Filtros de escrita unificado (UWF)  

-   O catálogo de aplicações não é suportado para todos os dispositivos Windows Embedded.  

-   Para poder monitorizar o software maligno detetado em dispositivos Windows Embedded que são baseados no Windows XP, tem de instalar o pacote de script do Microsoft Windows WMI no dispositivo. Utilize o Windows Embedded destino Designer para instalar este pacote.
Os ficheiros **WBEMDISP. DLL** e **WBEMDISP. TLB** tem de existir e estar registado na pasta **%windir%\System32\WBEM** no dispositivo incorporado para se certificar de que detetado software maligno é comunicado.  

**Sistemas operativos suportados:**  

-   **Windows 10 Enterprise** (x86, x64)  

-   **Windows 10 Enterprise IoT** (x86, x64)  

-   **Windows Embedded 8.1 Industry** (x86, x64)    

-   **Windows Embedded 8 Industry** (x86, x64)    

-   **Windows Embedded 8 Standard** (x86, x64)    

-   **Windows Embedded 8 Pro** (x86, x64)    

-   **Windows dinâmico PC** (x86, x64)    

-   **Windows Embedded POSReady 7** (x86, x64)    

-   **Windows Embedded Standard 7 com SP1** (x86, x64)    

-   **WEPOS 1.1 com SP3** (x86)    

-   **Windows Embedded POSReady 2009** (x86)    

-   **Noções básicas do Windows para PCs legados (WinFLP)** (x86)    

-   **Windows XP Embedded SP3** (x86)    

-   **Windows Embedded Standard 2009** (x86)  

## <a name="windows-ce-computers"></a>Computadores Windows CE
 Pode gerir dispositivos Windows CE com o cliente legado de dispositivos móveis do Configuration Manager está incluído com o Configuration Manager.  

**Requisitos e limitações**  

-   O cliente de dispositivo móvel requer 0.78 MB de espaço de armazenamento para a instalação. Início de sessão pode necessitar de até 256 KB de espaço de armazenamento adicional.    

-   Funcionalidades para estes dispositivos móveis variam consoante a plataforma e o cliente tipo. Para obter informações sobre a gestão de que as funções são suportadas, consulte o artigo [escolher uma solução de gestão de dispositivos para o System Center Configuration Manager](../../../core/plan-design/choose-a-device-management-solution.md).  

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

## <a name="mac-computers"></a>Computadores Mac  
 Pode gerir computadores Mac OS X com o cliente do Configuration Manager para Mac.  

 O pacote de instalação de cliente de Mac não é fornecido com o suporte de dados do Configuration Manager. Transferir o **clientes para sistemas operativos adicionais** a partir de [Centro de transferências da Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184).  

 Para obter mais informações, consulte o artigo [como implementar clientes no System Center Configuration Manager de Macs](../../../core/clients/deploy/deploy-clients-to-macs.md).  

**Versões suportadas:**  

-   **Mac OS X 10.6** (Snow Leopard)

-   **Mac OS X 10.7** (Lion)

-   **Mac OS X 10.8** (montanha Lion)

-   **Mac OS X 10.9** (Mavericks)

-   **Mac OS X 10.10** (Yosemite)  

-   **Mac OS X 10.11** (El Capitan)  

-   **Mac OS X 10.12** (macOS Sierra)

##  <a name="linux-and-unix-servers"></a>Servidores Linux e UNIX  
 Pode gerir servidores Linux e UNIX com o cliente do Configuration Manager para Linux e UNIX.  

 A instalação de cliente de Linux e UNIX, os pacotes não são sejam fornecidos com o suporte de dados do Configuration Manager. Transferir o **clientes para sistemas operativos adicionais** a partir de [Centro de transferências da Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184). Para além de pacotes de instalação de cliente, o cliente transfira inclui o script que gere a instalação do cliente em cada computador.  

**Requisitos e limitações:**  

-   Para rever as dependências de ficheiros de sistema operativo para o cliente para Linux e UNIX, consulte o artigo [pré-requisitos para implementação do cliente para servidores Linux e UNIX](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_ClientDeployPrereqforLnU).  

-   Para obter uma descrição geral das funcionalidades de gestão suportado para Linux ou UNIX, consulte o artigo [como implementar clientes em servidores UNIX e Linux no System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

-   Para versões suportadas do Linux e UNIX, a versão indicada inclui todas as versões secundárias subsequentes. Por exemplo, a versão de CentOS 6 inclui CentOS 6.3. Da mesma forma, suporte para um sistema operativo que utiliza pacotes de serviço (por exemplo, o SUSE Linux Enterprise Server 11 SP1) inclui pacotes de serviço subsequentes à versão do sistema operativo.  

-   Para obter informações sobre pacotes de instalação de cliente e o agente Universal, consulte o artigo [como implementar clientes em servidores UNIX e Linux no System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

**Versões suportadas:** São suportadas as seguintes versões utilizando o ficheiro .tar indicado.  

### <a name="aix"></a>AIX  

|||  
|-|-|  
|Versão 5.3 (Power)|CCM-Aix53ppc. &lt;construir\>.tar|  
|Versão 6.1 (Power)|CCM-Aix61ppc. &lt;construir\>.tar|  
|Versão 7.1 (Power)|CCM-Aix71ppc. &lt;construir\>.tar|  

### <a name="centos"></a>CentOS  

|||  
|-|-|  
|Versão 5 x86|CCM-Universalx86. &lt;construir\>.tar|  
|Versão 5 x64|CCM-Universalx64. &lt;construir\>.tar|  
|Versão 6 x86|CCM-Universalx86. &lt;construir\>.tar|  
|Versão 6 x64|CCM-Universalx64. &lt;construir\>.tar|  
|Versão 7 x64|CCM-Universalx64. &lt;construir\>.tar|  

### <a name="debian"></a>Debian  

|||  
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

|||  
|-|-|  
|Versão 11iv2 IA64|CCM-HpuxB.11.23i64. &lt;compilar\>.tar|  
|Versão 11iv2 PA-RISC|CCM HpuxB.11.23PA. &lt;compilar\>.tar|  
|Versão 11iv3 em IA64|CCM-HpuxB.11.31i64. &lt;construir\>.tar|  
|Versão 11iv3 PA-RISC|CCM-HpuxB.11.31PA. &lt;construir\>.tar|  

### <a name="oracle-linux"></a>Oracle Linux  

|||  
|-|-|  
|Versão 5 x86|CCM-Universalx86. &lt;construir\>.tar|  
|Versão 5 x64|CCM-Universalx64. &lt;construir\>.tar|  
|Versão 6 x86|CCM-Universalx86. &lt;construir\>.tar|  
|Versão 6 x64|CCM-Universalx64. &lt;construir\>.tar|  
|Versão 7 x64|CCM-Universalx64. &lt;construir\>.tar|  

### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|||  
|-|-|  
|Versão 4 x86|CCM-RHEL4x86. &lt;construir\>.tar|  
|Versão 4 x64|CCM-RHEL4x64. &lt;construir\>.tar|  
|Versão 5 x86|CCM-Universalx86. &lt;construir\>.tar|  
|Versão 5 x64|CCM-Universalx64. &lt;construir\>.tar|  
|Versão 6 x86|CCM-Universalx86. &lt;construir\>.tar|  
|Versão 6 x64|CCM-Universalx64. &lt;construir\>.tar|  
|Versão 7 x64|CCM-Universalx64. &lt;construir\>.tar|  

### <a name="solaris"></a>Solaris  

|||  
|-|-|  
|Versão 9 SPARC|CCM-Sol9sparc. &lt;construir\>.tar|  
|Versão 10 x86|CCM-Sol10x86. &lt;construir\>.tar|  
|Versão 10 SPARC|CCM-Sol10sparc. &lt;construir\>.tar|  
|Versão 11 x86|CCM-Sol11x86. &lt;construir\>.tar|  
|Versão 11 SPARC|CCM-Sol11sparc. &lt;construir\>.tar|  

### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|||  
|-|-|  
|Versão 9 x86|CCM-SLES9x86. &lt;construir\>.tar|  
|SP1 versão 10 x86|CCM-Universalx86. &lt;construir\>.tar|  
|Versão 10 SP1 x64|CCM-Universalx64. &lt;construir\>.tar|  
|Versão 11 SP1 x86|CCM-Universalx86. &lt;construir\>.tar|  
|Versão 11 SP1 x64|CCM-Universalx64. &lt;construir\>.tar|  
|Versão 12 x64|CCM-Universalx64. &lt;construir\>.tar|  

### <a name="ubuntu"></a>Ubuntu  

|||  
|-|-|  
|Versão 10.04 LTS x86|CCM-Universalx86. &lt;construir\>.tar|  
|Versão 10.04 LTS x64|CCM-Universalx64. &lt;construir\>.tar|  
|Versão 12.04 LTS x86|CCM-Universalx86. &lt;construir\>.tar|  
|Versão 12.04 LTS x64|CCM-Universalx64. &lt;construir\>.tar|  
|Versão 14.04 LTS x86|CCM-Universalx86. &lt;construir\>.tar|  
|Versão 14.04 LTS x64|CCM-Universalx64. &lt;construir\>.tar|  

##  <a name="mobile-devices-enrolled-by-microsoft-intune"></a>Dispositivos móveis inscritos pelo Microsoft Intune  
 Para obter detalhes sobre os computadores e dispositivos que podem ser geridos quando integrar o Microsoft Intune com o Configuration Manager, consulte os tópicos seguintes dois na biblioteca de documentação do Microsoft Intune:  

-   [Funcionalidades de gestão de dispositivos móveis no Microsoft Intune](https://docs.microsoft.com/intune/get-started/choose-how-to-manage-devices)  
-   [Funcionalidades de gestão do Windows PC no Microsoft Intune](https://docs.microsoft.com/intune/get-started/windows-pc-management-capabilities-in-microsoft-intune)  

##  <a name="bkmk_OnpremOS"></a>Gestão de dispositivos móveis no local  
 O Configuration Manager possui capacidades incorporadas para gestão de dispositivos que estão no local sem instalar o software de cliente.  Para obter mais informações, consulte o artigo [gerir dispositivos móveis com a infraestrutura no local no System Center Configuration Manager](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

 **Requisitos e limitações:**  

-   Tem de configurar o **ponto de ligação de serviço** no site de nível superior da hierarquia.  

**Sistemas operativos suportados:**  

- **Windows 10 Pro** (x86, x64)  

- **Windows 10 Pro Enterprise** (x86, x64)  

- **Windows 10 Enterprise IoT** (x86, x64)

- **Windows 10 Mobile**  

- **Windows 10 Enterprise móveis**  

- **Windows 10 IoT Mobile Enterprise**

- **Equipa do Windows 10 para Hub superfície**

##  <a name="bkmk_ExSrvConOS"></a>Conector do Exchange Server  
O Configuration Manager suporta a gestão limitada de dispositivos que ligam ao Exchange Server, sem instalar o cliente do Configuration Manager. Para obter mais informações, veja [Gerir dispositivos móveis com o System Center Configuration Manager e o Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

 **Requisitos e limitações:**  

-   O Configuration Manager oferece gestão limitada para dispositivos móveis ao utilizar dispositivos com o conector do Exchange Server para Exchange Active Sync ligar a um servidor que está a executar o Exchange Server ou ao Exchange Online.  

-   Para obter mais informações sobre que funções de gestão do Configuration Manager suporta para dispositivos móveis que gere o conector do Exchange Server, consulte o artigo determinar como gerir dispositivos móveis no Configuration Manager.  

**Versões suportadas do Exchange Server:**  

-   **Exchange Server 2010 SP1**  

-   **Exchange Server 2010 SP2**  

-   **Exchange Server 2013**  

-   **Exchange Online (Office 365)**: Isto inclui Business Productivity Online Standard Suite  

