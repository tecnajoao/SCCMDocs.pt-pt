---
title: Dispositivos e clientes suportados
titleSuffix: Configuration Manager
description: Obtenha as versões de SO do Configuration Manager suporta para clientes e dispositivos.
ms.date: 10/02/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 87f4e041-67df-4c61-aa98-7444faffe565
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6f60d7f3a8c3bd81f4de38b2ce4080f54756de14
ms.sourcegitcommit: c60e057075a83f07d1ca2577c3de1c7d7c8e9cec
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/19/2018
ms.locfileid: "53626468"
---
# <a name="supported-os-versions-for-clients-and-devices-for-configuration-manager"></a>Versões de SO suportadas por clientes e dispositivos para o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

 O Configuration Manager suporta a instalação de software de cliente em computadores Windows, Mac, Linux e UNIX.  

#### <a name="requirements-and-limitations-for-all-clients"></a>Requisitos e limitações para todos os clientes  

-   Alterar o tipo de arranque ou **iniciar sessão como** definições para qualquer serviço do Configuration Manager não é suportada. Esta alteração pode impedir que serviços importantes de funcionar corretamente.    

-   Instalar ou executar o cliente do Configuration Manager para Linux ou UNIX ou o cliente para Mac em computadores com uma conta diferente de raiz não é suportada. Se o fizer, pode que serviços importantes deixem de funcionar corretamente.  



##  <a name="windows-computers"></a>Computadores Windows  

 Para gerir as seguintes versões de SO Windows, utilize o cliente que está incluído com o Configuration Manager. Para obter mais informações, consulte [como implementar clientes em computadores Windows](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).  


### <a name="supported-client-os-versions"></a>Versões de SO de cliente suportados

-   **Windows 10**  

    Para obter mais informações, consulte [suporte para Windows 10](/sccm/core/plan-design/configs/support-for-windows-10).  

-   **Windows 8.1** (x86, x64): Professional, Enterprise    

-   **O Windows 7 com SP1** (x86, x64): Professional, Enterprise e Ultimate    


### <a name="supported-server-os-versions"></a>Versões de SO de servidor suportadas

-  **Windows Server 2019**: Standard, Datacenter <sup> [observe 1](#bkmk_note1)</sup>  
    (A partir do Configuration Manager versão 1806.)

-  **Windows Server 2016**: Standard, Datacenter <sup> [observe 1](#bkmk_note1)</sup>  

-   **O Windows Storage Server 2016**: Grupo de trabalho Standard  

-   **Windows Server 2012 R2** (x64): Standard, Datacenter <sup> [observe 1](#bkmk_note1)</sup>    

-   **Windows Storage Server 2012 R2** (x64)    

-   **Windows Server 2012** (x64): Standard, Datacenter <sup> [observe 1](#bkmk_note1)</sup>    

-   **O Windows Storage Server 2012** (x64)    

-   **Windows Server 2008 R2 com SP1** (x64): Standard, Enterprise e Datacenter <sup> [observe 1](#bkmk_note1)</sup>    

-   **Windows Storage Server 2008 R2** (x86, x64): Grupo de trabalho, Standard, Enterprise    

-   **Windows Server 2008 com SP2** (x86, x64): Standard, Enterprise e Datacenter <sup> [observe 1](#bkmk_note1)</sup>    


#### <a name="server-core"></a>Server Core
As seguintes versões especificamente referem-se para a instalação do Server Core do sistema operacional. <sup>[Nota 3](#bkmk_note3)</sup>  

Versões de canal semianual do Windows Server são instalações Server Core, como o Windows Server, versão 1809. Como um cliente do Configuration Manager, eles são suportados o mesmo que a versão associada para o Windows 10 semianual canal. Para obter mais informações, consulte [suporte para Windows 10](/sccm/core/plan-design/configs/support-for-windows-10).


-   **Windows Server 2019** (x64) <sup> [observe 2](#bkmk_note2)</sup>  

-   **Windows Server 2016** (x64) <sup> [observe 2](#bkmk_note2)</sup>   

-   **Windows Server 2012 R2** (x64) <sup> [observe 2](#bkmk_note2)</sup>     

-   **Windows Server 2012** (x64) <sup> [observe 2](#bkmk_note2)</sup>     

-   **Windows Server 2008 R2** sem nenhum service pack ou com SP1 (x64)     

-   **Windows Server 2008 SP2** (x86, x64)   

#### <a name="bkmk_note1"></a> Nota 1
 O Configuration Manager testa e suporta edições de Datacenter do Windows Server, mas não é oficialmente certificado para o Windows Server. Suporte de correção do Gestor de configuração não é disponibilizado para problemas que são específicos para o Windows Server Datacenter Edition. Para obter mais informações sobre o programa de certificação do Windows Server, consulte [Windows Server Catalog](https://www.windowsservercatalog.com/). 

#### <a name="bkmk_note2"></a> Nota 2
 Para suportar [instalação push do cliente](/sccm/core/clients/deploy/plan/client-installation-methods#client-push-installation), adicione o serviço de servidor de ficheiros da função de servidor de ficheiros e serviços de armazenamento. Para obter mais informações sobre como instalar funcionalidades do Windows no Server Core, consulte [instalar funções, serviços de função e funcionalidades utilizando cmdlets do Windows PowerShell](https://docs.microsoft.com/windows-server/administration/server-manager/install-or-uninstall-roles-role-services-or-features#BKMK_installwps).  

#### <a name="bkmk_note3"></a> Nota 3
 A nova aplicação do Centro de Software não é suportada em qualquer versão do Windows Server Core.<!--SCCMDocs issue 683-->



##  <a name="windows-embedded-computers"></a>Computadores Windows Embedded  

 Geri dispositivos Windows Embedded ao instalar o cliente do Configuration Manager no dispositivo. Para obter mais informações, consulte [planejar a implantação de cliente em dispositivos Windows Embedded](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices).  


### <a name="requirements-and-limitations"></a>Requisitos e limitações

-   Todas as funcionalidades de cliente são suportadas no Windows Embedded sistemas que não tenham filtros de escrita ativados.  

-   Os clientes que utilizam um dos seguintes são suportados para todas as funcionalidades, exceto a gestão de energia:  

    -   Filtros de escrita avançados (EWF)    

    -   Filtros de escrita baseados em ficheiros RAM (FBWF)    

    -   Filtros de escrita unificados (UWF)  

-   O catálogo de aplicações não é suportado por dispositivos Windows Embedded.  


### <a name="supported-os-versions"></a>Versões de SO suportadas  

-   **Windows 10 Enterprise** (x86, x64)  

-   **Windows 10 IoT Enterprise** (x86, x64)  
    Esta versão inclui o canal de serviço a longo prazo (LTSC). Para obter mais informações, consulte [descrição geral do Windows 10 IoT Enterprise](https://docs.microsoft.com/windows/iot-core/windows-iot-enterprise).<!--SCCMDocs issue 560-->  

-   **Windows Embedded 8.1 Industry** (x86, x64)    

-   **Windows Embedded 8 Standard** (x86, x64)    

-   **Windows dinâmico PC** (x86, x64)    

-   **Windows Embedded POSReady 7** (x86, x64)    

-   **Windows Embedded Standard 7 com SP1** (x86, x64)    



## <a name="windows-ce-computers"></a>Computadores Windows CE

 Gerir dispositivos Windows CE com o cliente legado de dispositivo móvel do Configuration Manager está incluído com o Configuration Manager.  


### <a name="requirements-and-limitations"></a>Requisitos e limitações  

-   O cliente de dispositivo móvel precisa de 0,78 MB de espaço de armazenamento para a instalação. Início de sessão, pode exigir até 256 KB de espaço de armazenamento adicional.    

-   Recursos para estes dispositivos móveis variam consoante a plataforma e o cliente do tipo. Para obter informações sobre a gestão de que as funções são suportadas, consulte [escolher uma solução de gestão de dispositivos](/sccm/core/plan-design/choose-a-device-management-solution).  


### <a name="supported-os-versions"></a>Versões de SO suportadas  

-   Windows CE 7.0 (ARM e x86 processadores)  

#### <a name="supported-languages-include"></a>Os idiomas suportados incluem

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



## <a name="mac-computers"></a>Computadores Mac  

 Gerir computadores de macOS com o cliente do Configuration Manager para Mac.  

 O pacote de instalação de cliente de Mac não é fornecido com o suporte de dados do Configuration Manager. Transfira o **clientes para sistemas operativos adicionais** partir o [Centro de transferências da Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184).  

 Para obter mais informações, consulte [como implementar clientes em Macs](/sccm/core/clients/deploy/deploy-clients-to-macs).  


### <a name="supported-versions"></a>Versões suportadas

-   **Mac OS X 10.6** (Leopard de neve)

-   **Mac OS X 10.7** (Lion)

-   **Mac OS X 10.8** (Mountain Lion)

-   **Mac OS X 10.9** (Mavericks)

-   **Mac OS X 10.10** (Yosemite)  

-   **Mac OS X 10.11** (El Capitan)  

-   **Mac OS X 10.12** (macOS Sierra)

-   **Mac OS X 10.13** (macOS High Sierra)

- **macOS Mojave (10.14)** 


##  <a name="linux-and-unix-servers"></a>Servidores Linux e UNIX  

> [!Important]  
> A partir de 22 de Março de 2018, os clientes Linux e UNIX para o Configuration Manager foram preteridos. Para obter mais informações, consulte [anúncio de preterição para o suporte de cliente de Linux e Unix](/sccm/core/plan-design/changes/whats-new-in-version-1802#deprecation-announcement-for-linux-and-unix-client-support).  

 Gerir servidores Linux e UNIX com o cliente do Configuration Manager para Linux e UNIX.  

 Os pacotes de instalação de cliente de Linux e UNIX não são fornecidos com o suporte de dados do Configuration Manager. Transfira o **clientes para sistemas operativos adicionais** partir o [Centro de transferências da Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184). Para além de pacotes de instalação de cliente, a transferência do cliente inclui o script que gere a instalação do cliente em cada computador.  


### <a name="requirements-and-limitations"></a>Requisitos e limitações

-   Para rever as dependências de ficheiros de sistema operacional para o cliente para Linux e UNIX, consulte [pré-requisitos para implementação do cliente para servidores Linux e UNIX](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers#BKMK_ClientDeployPrereqforLnU).  

-   Para uma descrição geral das capacidades de gestão suportadas de Linux ou UNIX, consulte [como implementar clientes em servidores UNIX e Linux](/sccm/core/clients/deploy/deploy-clients-to-unix-and-linux-servers).  

-   Para obter versões suportadas do Linux e UNIX, a versão indicada inclui todas a versões secundárias subsequente. Por exemplo, a versão 6 do CentOS inclui o CentOS 6.3. Da mesma forma, o suporte para um sistema operacional que utiliza service packs (como o SUSE Linux Enterprise Server 11 SP1) inclui service packs subsequentes para essa versão do SO.  

-   Para obter informações sobre pacotes de instalação de cliente e do agente Universal, consulte [como implementar clientes em servidores UNIX e Linux](/sccm/core/clients/deploy/deploy-clients-to-unix-and-linux-servers).  


### <a name="supported-versions"></a>Versões suportadas

As seguintes versões são suportadas ao utilizar o ficheiro. tar indicado.  

#### <a name="aix"></a>AIX  

|Versão|Ficheiro de destino|  
|-|-|  
|Versão 6.1 (Power)|ccm-Aix61ppc.&lt;build\>.tar|  
|Versão 7.1 (Power)|ccm-Aix71ppc.&lt;build\>.tar|  

#### <a name="centos"></a>CentOS  

|Versão|Ficheiro de destino|  
|-|-|  
|Versão 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 7 x64|ccm-Universalx64.&lt;build\>.tar|  

#### <a name="debian"></a>Debian  

|Versão|Ficheiro de destino|  
|-|-|  
|Versão 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 7 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 7 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 8 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 8 x64|ccm-Universalx64.&lt;build\>.tar|  

#### <a name="hp-ux"></a>HP-UX  

|Versão|Ficheiro de destino|  
|-|-|  
|Versão 11iv3 IA64|ccm-HpuxB.11.31i64.&lt;build\>.tar|  

#### <a name="oracle-linux"></a>Oracle Linux  

|Versão|Ficheiro de destino|  
|-|-|  
|Versão 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 7 x64|ccm-Universalx64.&lt;build\>.tar|  

#### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|Versão|Ficheiro de destino|  
|-|-|  
|Versão 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 7 x64|ccm-Universalx64.&lt;build\>.tar|  

#### <a name="solaris"></a>Solaris  

|Versão|Ficheiro de destino|  
|-|-|  
|Versão 10 x86|ccm-Sol10x86.&lt;build\>.tar|  
|Versão 10 SPARC|ccm-Sol10sparc.&lt;build\>.tar|  
|Versão 11 x86|ccm-Sol11x86.&lt;build\>.tar|  
|Versão 11 SPARC|ccm-Sol11sparc.&lt;build\>.tar|  

#### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|Versão|Ficheiro de destino|  
|-|-|  
|Versão 10 SP1 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 10 SP1 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 11 SP1 x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 11 SP1 x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 12 x64|ccm-Universalx64.&lt;build\>.tar|  

#### <a name="ubuntu"></a>Ubuntu  

|Versão|Ficheiro de destino|  
|-|-|  
|Versão 10.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 10.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 12.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 12.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 14.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 14.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|Versão 16.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|Versão 16.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  



##  <a name="bkmk_OnpremOS"></a> Gestão de dispositivos móveis no local  

 O Configuration Manager possui capacidades incorporadas para a gestão de dispositivos que estão no local sem instalar o software de cliente. Para obter mais informações, consulte [gerir dispositivos móveis com a infraestrutura no local](/sccm/mdm/understand/manage-mobile-devices-with-on-premises-infrastructure).  


### <a name="requirements-and-limitations"></a>Requisitos e limitações

-   Configurar o **ponto de ligação de serviço** no site de nível superior da sua hierarquia.  


### <a name="supported-operating-systems"></a>Sistemas operativos suportados

- **Windows 10 Pro** (x86, x64)  

- **Enterprise do Windows 10 Pro** (x86, x64)  

- **Windows 10 IoT Enterprise** (x86, x64)  
    Esta versão inclui o canal de serviço a longo prazo (LTSC). Para obter mais informações, consulte [descrição geral do Windows 10 IoT Enterprise](https://docs.microsoft.com/windows/iot-core/windows-iot-enterprise).<!--SCCMDocs issue 560-->  

- **Windows 10 Mobile**  

- **Do Windows 10 Mobile Enterprise**  

- **Windows 10 IoT Mobile Enterprise**  

- **Equipe do Windows 10 para o Surface Hub**  



##  <a name="bkmk_ExSrvConOS"></a> Conector do Exchange Server  

O Configuration Manager suporta a gestão limitada de dispositivos que ligam ao seu Exchange Server, sem instalar o cliente do Configuration Manager. Para obter mais informações, consulte [gerir dispositivos móveis com o Configuration Manager e o Exchange](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).  


### <a name="supported-versions-of-exchange-server"></a>Versões suportadas do Exchange Server

- **Exchange Online (Office 365)**: Esta versão inclui o Business Productivity Online Standard Suite  

- **Exchange Server 2016** (a partir da versão 1802)  

- **Exchange Server 2013**  

- **Exchange Server 2010 SP1** ou **do Exchange Server 2010 SP2** 
