---
title: "Requisitos de infraestrutura para a implementação do sistema de operativo | Microsoft Docs"
description: "Certifique-se de que deve saber dependências externas e dependências de produto antes de utilizar o System Center 2012 Configuration Manager para a implementação de sistema operativo."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 1dc74219-7ff5-4e3b-b4f6-5aad663bb75b
caps.latest.revision: "24"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: 167e639cdb9995fd743787cc9fbf364ec70f6ed9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="infrastructure-requirements-for-operating-system-deployment-in-system-center-configuration-manager"></a>Requisitos de infraestrutura para a implementação do sistema operativo no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Implementação do sistema operativo no System Center 2012 Configuration Manager tem dependências externas e dependências no produto. Utilize as secções seguintes para o ajudar a preparar a implementação do sistema operativo.  

##  <a name="BKMK_ExternalDependencies"></a> Dependências Externas ao Configuration Manager  
 O seguinte fornece informações sobre ferramentas externas, kits de instalação e sistemas operativos que são necessários para implementar sistemas operativos no Configuration Manager.  

### <a name="windows-adk-for-windows-10"></a>Windows ADK para Windows 10  
 O Windows ADK é um conjunto de ferramentas e documentação que suporta a configuração e implementação de sistemas operativos Windows. O Configuration Manager utiliza o Windows ADK para automatizar as instalações do Windows, capturar imagens do Windows, migrar dados e perfis de utilizador e assim sucessivamente.  

 As seguintes funcionalidades do Windows ADK tem de ser instalado server no local de site de nível superior da hierarquia, no servidor do site de cada site primário na hierarquia e no servidor de sistema de site do fornecedor de SMS:  

-   User State Migration Tool (USMT) <sup>1</sup>  

-   Ferramentas de Implementação do Windows  

-   Ambiente de Pré-instalação do Windows (Windows PE)

Para obter uma lista das versões do Windows 10 ADK que pode utilizar com diferentes versões do Configuration Manager, consulte [suporte para Windows 10 como um cliente](https://docs.microsoft.com/en-us/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk).

 <sup>1</sup> O USMT não é necessário no servidor do sistema de sites do Fornecedor de SMS.  

> [!NOTE]  
>  Tem de instalar manualmente o Windows ADK em cada computador que irá alojar um site de administração central ou o servidor do site primário antes de instalar o site do Configuration Manager.  

 Para obter mais informações, consulte:  

-   [Cenários do Windows ADK para Windows 10 para Profissionais de TI](https://technet.microsoft.com/library/mt280162\(v=vs.85\).aspx)  

-   [Transferir o Windows ADK para Windows 10](https://msdn.microsoft.com/windows/hardware/dn913721.aspx#adkwin10)  

-   [Suporte para Windows 10](/sccm/core/plan-design/configs/support-for-windows-10)  


### <a name="user-state-migration-tool-usmt"></a>User State Migration Tool (USMT)  
 O Configuration Manager utiliza um pacote USMT que contém os ficheiros de origem USMT 10 para capturar e restaurar o estado do utilizador como parte da implementação do sistema operativo. Configuração do Configuration Manager no site de nível superior cria automaticamente o pacote USMT. O USMT 10 consegue capturar o estado de utilizador do Windows 7, Windows 8, Windows 8.1 e Windows 10. O USMT 10 é distribuído no Windows Assessment and Deployment Kit (Windows ADK) para Windows 10.  

 Para obter mais informações, consulte:  

-   [Cenários Comuns de Migração do USMT 10](https://technet.microsoft.com/library/mt299169\(v=vs.85\).aspx)  

-   [Gerir o estado do utilizador](../get-started/manage-user-state.md)  

### <a name="windows-pe"></a>Windows PE  
 O Windows PE é utilizado para imagens de arranque para iniciar um computador. É um sistema operativo Windows com serviços limitados que é utilizado durante a pré-instalação e implementação de sistemas operativos Windows. O seguinte fornece a versão do Configuration Manager e a versão suportada do Windows ADK, a versão do Windows PE nas quais se baseia a imagem de arranque que pode ser personalizada a partir da consola do Configuration Manager e as versões do Windows PE na qual se baseia a imagem de arranque que pode personalizar com o DISM e depois adicione a imagem para a versão especificada do Configuration Manager.  

#### <a name="configuration-manager-version-1511"></a>Versão do Configuration Manager 1511  
 O seguinte fornece a versão suportada do Windows ADK, a versão do Windows PE nas quais se baseia a imagem de arranque que pode ser personalizada a partir da consola do Configuration Manager e as versões do Windows PE na qual se baseia a imagem de arranque que pode personalizar com o DISM e depois adicione a imagem para o Configuration Manager.  

-   **Versão do Windows ADK**  

     Windows ADK para Windows 10  

-   **Versões do Windows PE para imagens de arranque personalizáveis a partir da consola do Configuration Manager**  

     Windows PE 10  

-   **Versões do Windows PE para imagens de arranque não podem ser personalizadas na consola do Configuration Manager**  

     Windows PE 3.1<sup>1</sup> e Windows PE 5  

     <sup>1</sup> só é possível adicionar uma imagem de arranque para o Configuration Manager quando se baseia no Windows PE 3.1. Instale o Suplemento do Windows AIK para o Windows 7 SP1 para atualizar o Windows AIK para o Windows 7 (baseado no Windows PE 3) com o Suplemento do Windows AIK para Windows 7 SP1 (baseado no Windows PE 3.1). Poderá transferir o Suplemento do Windows AIK para Windows 7 SP1 a partir do [Centro de Transferências da Microsoft](http://www.microsoft.com/download/details.aspx?id=5188).  

     Por exemplo, quando tiver do Configuration Manager, pode personalizar imagens de arranque do Windows ADK para Windows 10 (baseado no Windows PE 10) na consola do Configuration Manager. No entanto, embora as imagens de arranque baseadas no Windows PE 5 sejam suportadas, tem de personalizá-las a partir de um computador diferente e utilizar a versão do DISM que é instalada com o Windows ADK para Windows 8. Em seguida, pode adicionar a imagem de arranque à consola do Configuration Manager. Para obter mais informações sobre os passos para personalizar uma imagem de arranque (adicionar componentes e controladores opcionais), ativar suporte de comando para a imagem de arranque, adicionar a imagem de arranque à consola do Configuration Manager e atualizar pontos de distribuição com a imagem de arranque, consulte [personalizar imagens de arranque](../get-started/customize-boot-images.md). Para obter mais informações sobre imagens de arranque, veja [Gerir imagens de arranque](../get-started/manage-boot-images.md).  

### <a name="windows-server-update-services-wsus"></a>Windows Server Update Services (WSUS)  
Tem de instalar as seguintes correções WSUS 4.0:
  - [Hotfix 3095113](https://support.microsoft.com/kb/3095113) é necessário para manutenção do Windows 10, que utiliza a infraestrutura de atualizações de software para obter as atualizações de funcionalidades do Windows 10. Se tiver o WSUS 3.2, tem de utilizar sequências de tarefas para atualizar o Windows 10. Para obter mais informações, consulte [gerir o Windows como um serviço](../deploy-use/manage-windows-as-a-service.md).  
  - [Correção 3159706](https://support.microsoft.com/kb/3159706) é necessário utilizar manutenção para atualizar computadores para a atualização de aniversário do Windows 10, bem como para versões subsequentes do Windows 10. Existem passos manuais descritos no artigo de suporte que tem de efetuar para instalar esta correção. Para obter mais informações, consulte [gerir o Windows como um serviço](../deploy-use/manage-windows-as-a-service.md).


### <a name="internet-information-services-iis-on-the-site-system-servers"></a>IIS (Serviços de Informação Internet) nos servidores do sistema de sites  
 O IIS é necessário para o ponto de distribuição, o ponto de migração de estado e o ponto de gestão. Para obter mais informações sobre este requisito, consulte [Site e os pré-requisitos de sistema de site](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

### <a name="windows-deployment-services-wds"></a>Serviços de implementação do Windows (WDS)  
 O WDS é necessário para implementações de PXE e quando for utilizado multicast para otimizar a largura de banda das implementações e para o funcionamento offline das mensagens. Se o fornecedor estiver instalado num servidor remoto, deve instalar o WDS no servidor do site e o fornecedor remoto. Para obter mais informações, veja [Serviços de Implementação do Windows](#BKMK_WDS) neste tópico.  

### <a name="dynamic-host-configuration-protocol-dhcp"></a>Protocolo DHCP (Dynamic Host Configuration Protocol)  
 O protocolo DHCP é necessário para implementações de PXE. É necessário ter um servidor DHCP a funcionar com um anfitrião ativo para implementar sistemas operativos com PXE. Para obter mais informações sobre implementações de PXE, consulte [utilizar o PXE para implementar o Windows através da rede](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

### <a name="supported-operating-systems-and-hard-disk-configurations"></a>Sistemas operativos suportados e configurações do disco rígido  
 Para obter mais informações sobre as versões de sistema operativo e as configurações de disco rígido suportados pelo Configuration Manager quando implementar sistemas operativos, consulte [sistemas operativos suportados pelo](#BKMK_SupportedOS) e [configurações de disco suportadas](#BKMK_SupportedDiskConfig).  

### <a name="windows-device-drivers"></a>Controladores de dispositivo do Windows  
 É possível utilizar controladores de dispositivo do Windows ao instalar o sistema operativo no computador de destino e ao executar o Windows PE utilizando uma imagem de arranque. Para obter mais informações sobre controladores de dispositivo, consulte [gerir controladores](../get-started/manage-drivers.md).  

##  <a name="BKMK_InternalDependencies"></a> Dependências do Configuration Manager  
 O seguinte fornece informações sobre o sistema do Configuration Manager os pré-requisitos de implementação.  

### <a name="operating-system-image"></a>Imagem do sistema operativo  
 As imagens de sistema operativo no Configuration Manager são armazenadas no formato de ficheiro Windows Imaging (WIM) e representam uma coleção comprimida de ficheiros e pastas de referência que são necessários para instalar e configurar com êxito um sistema operativo num computador. Para obter mais informações, consulte [gerir imagens do sistema operativo](../get-started/manage-operating-system-images.md).  

### <a name="driver-catalog"></a>Catálogo de controladores  
 Para implementar um controlador de dispositivo, tem de importar o controlador de dispositivo, ativá-lo e disponibilizá-lo num ponto de distribuição que o cliente do Configuration Manager pode aceder. Para mais informações sobre o catálogo de controladores, consulte [gerir controladores](../get-started/manage-drivers.md).  

### <a name="management-point"></a>Ponto de gestão  
 Pontos de gestão transferem informações entre computadores cliente e o site do Configuration Manager. O cliente utiliza um ponto de gestão para executar as sequências de tarefas que são necessárias para concluir a implementação do sistema operativo.  

 Para obter mais informações sobre sequências de tarefas, consulte [considerações sobre planeamento para automatizar tarefas](planning-considerations-for-automating-tasks.md).  

### <a name="distribution-point"></a>Ponto de distribuição  
 Os pontos de distribuição são utilizados na maioria das implementações para armazenar os dados utilizados para implementar um sistema operativo, tais como a imagem do sistema operativo ou pacotes de controladores de dispositivo. Normalmente, as sequências de tarefas obtêm dados de um ponto de distribuição para implementar o sistema operativo.  

 Para obter mais informações sobre como instalar pontos de distribuição e gerir conteúdo, consulte [gerir a infraestrutura de conteúdo e conteúda](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

### <a name="pxe-enabled-distribution-point"></a>Ponto de distribuição com PXE ativado  
 Para realizar implementações iniciadas por PXE, é necessário configurar um ponto de distribuição para aceitar pedidos PXE de clientes. Para obter mais informações sobre como configurar o ponto de distribuição, consulte [configurar um ponto de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#pxe).  

### <a name="multicast-enabled-distribution-point"></a>Ponto de distribuição com multicast ativado  
 Para otimizar as implementações do sistema operativo através de multicast, é necessário configurar um ponto de distribuição para suportar multicast. Para obter mais informações sobre como configurar o ponto de distribuição, consulte [configurar um ponto de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#multicast).   

### <a name="state-migration-point"></a>Ponto de migração de estado  
 Ao capturar e restaurar dados do estado do utilizador para implementações lado a lado e de atualizações, é necessário configurar um ponto de migração de estado para armazenar os dados do estado do utilizador noutro computador.  

 Para obter mais informações sobre como configurar o ponto de migração de estado, veja [Ponto de migração de estado](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

 Para obter informações sobre como capturar e restaurar estado do utilizador, consulte [gerir o estado do utilizador](../get-started/manage-user-state.md).  

### <a name="service-connection-point"></a>Ponto de ligação de serviço  
 Ao utilizar o Windows como um serviço (WaaS) para implementar o Windows 10 Current Branch, tem de ter o ponto de ligação de serviço instalado. Para obter mais informações, consulte [gerir o Windows como um serviço](../deploy-use/manage-windows-as-a-service.md).  

### <a name="reporting-services-point"></a>Ponto do Reporting Services  
 Para utilizar relatórios do Configuration Manager para implementações do sistema operativo, tem de instalar e configurar um ponto do Reporting Services. Para obter mais informações, consulte [relatórios](../../core/servers/manage/reporting.md).  

### <a name="security-permissions-for-operating-system-deployments"></a>Permissões de segurança para implementações do sistema operativo  
 A função de segurança do **Gestor de Implementação do Sistema Operativo** é uma função incorporada que não pode ser alterada. No entanto, é possível copiar a função, efetuar alterações e, em seguida, guardar estas alterações como uma nova função de segurança personalizada. São apresentadas, a seguir, algumas das permissões que são diretamente aplicáveis a implementações do sistema operativo:  

-   **Pacote de imagem de arranque**: Criar, eliminar, modificar, modificar pasta, mover objeto, ler, definir âmbito de segurança  

-   **Controladores de dispositivo**: Criar, eliminar, modificar, modificar pasta, modificar relatório, mover objeto, ler, executar relatório  

-   **Pacote de controladores**: Criar, eliminar, modificar, modificar pasta, mover objeto, ler, definir âmbito de segurança  

-   **Imagem do sistema operativo**: Criar, eliminar, modificar, modificar pasta, mover objeto, ler, definir âmbito de segurança  

-   **Pacote de instalação do sistema operativo**: Criar, eliminar, modificar, modificar pasta, mover objeto, ler, definir âmbito de segurança  

-   **Pacote de sequência de tarefas**: Criar, criar tarefa de suporte de dados de sequência, eliminar, modificar, modificar pasta, modificar relatório, mover objeto, ler, executar relatório, definir âmbito de segurança  

 Para obter mais informações sobre funções de segurança personalizadas, veja [Criar funções de segurança personalizadas](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole).  

### <a name="security-scopes-for-operating-system-deployments"></a>Âmbitos de segurança para implementações do sistema operativo  
 Utilize âmbitos de segurança para fornecer aos utilizadores administrativos acesso aos objetos com capacidade de segurança utilizados em implementações do sistema operativo, tais como imagens de sistemas operativos e imagens de arranque, pacotes de controladores e pacotes de sequências de tarefas. Para obter mais informações, veja [Âmbitos de segurança](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope).  

##  <a name="BKMK_WDS"></a> Serviços de Implementação do Windows  
 O WDS (Serviços de Implementação do Windows) deve ser instalado no mesmo servidor que os pontos de distribuição configurados para suporte de PXE ou multicast. O WDS está incluído no sistema operativo do servidor. Para implementações de PXE, o WDS é o serviço que executa o arranque PXE. Quando o ponto de distribuição é instalado e ativado para PXE, o Configuration Manager instala um fornecedor no WDS que utiliza as funções de arranque PXE do WDS.  

> [!NOTE]  
>  Se o servidor requer um reinício, a instalação do WDS poderá falhar. 

 Outras configurações do WDS que devem ser consideradas incluem:  

-   A instalação do WDS no servidor requer que o administrador seja um membro do grupo local de Administradores.  

-   O servidor WDS tem de ser membro de um domínio do Active Directory ou de um controlador de domínio para um domínio do Active Directory. Todas as configurações de domínio e de floresta de Windows suportam WDS.  

-   Se o fornecedor estiver instalado num servidor remoto, deve instalar o WDS no servidor do site e o fornecedor remoto.  

###  <a name="BKMK_WDSandDHCP"></a> Considerações sobre quando tiver o WDS e DHCP no mesmo servidor  
 Se planear coalojar o ponto de distribuição num servidor com o DHCP, considere os seguintes problemas de configuração.  

-   Tem de ter um servidor DHCP funcional com um âmbito ativo. Os Serviços de Implementação do Windows utilizam o PXE, que necessita de um servidor DHCP.  

-   O DHCP e os Serviços de Implementação do Windows necessitam da porta número 67. Se coalojar os Serviços de Implementação do Windows e o DHCP, pode mover o DHCP ou o ponto de distribuição configurado para PXE para um servidor separado. Ou pode utilizar o procedimento seguinte para configurar o servidor dos Serviços de Implementação do Windows para escutar numa porta diferente.  

    #### <a name="to-configure-the-windows-deployment-services-server-to-listen-on-a-different-port"></a>Para configurar o servidor dos Serviços de Implementação do Windows para escutar numa porta diferente  

    1.  Modifique a seguinte chave de registo:  

         **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WDSServer\Providers\WDSPXE**  

    2.  Defina o valor de registo como: **UseDHCPPorts = 0**  

    3.  Para efetivar a nova configuração, execute o seguinte comando no servidor:  

         `WDSUTIL /Set-Server /UseDHCPPorts:No /DHCPOption60:Yes`  

-   É necessário um servidor DNS para executar os Serviços de Implementação do Windows.  

-   As portas UDP seguintes devem estar abertas no servidor dos Serviços de Implementação do Windows.  

    -   Porta 67 (DHCP)  

    -   Porta 69 (TFTP)  

    -   Porta 4011 (PXE)  

    > [!NOTE]  
    >  Além disso, se for necessária autorização de DHCP no servidor, a porta 68 do cliente DHCP precisa de estar aberta no servidor.  

##  <a name="BKMK_SupportedOS"></a> Sistemas Operativos Suportados  
 Todos os sistemas operativos do Windows listados como suportado nos sistemas operativos de cliente no [sistemas operativos suportados para os clientes e dispositivos](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md) são suportadas para implementações do sistema operativo.  

##  <a name="BKMK_SupportedDiskConfig"></a> Configurações de disco suportadas  
 As combinações de configuração de disco rígido nos computadores de referência e de destino que são suportados para implementação do sistema operativo do Configuration Manager são apresentadas na tabela seguinte.  

|Configuração do disco rígido do computador de referência|Configuração do disco rígido do computador de destino|  
|------------------------------------------------|--------------------------------------------------|  
|Disco básico|Disco básico|  
|Volume simples num disco dinâmico|Volume simples num disco dinâmico|  

 O Configuration Manager suporta capturar uma imagem do sistema operativo apenas de computadores que estão configurados com volumes simples. Não existe suporte para as seguintes configurações do disco rígido:  

-   Volumes expandidos  

-   Volumes repartidos (RAID 0)  

-   Volumes espelhados (RAID 1)  

-   Volumes de paridade (RAID 5)  

 A tabela seguinte mostra uma configuração adicional do disco rígido nos computadores de referência e de destino que não é suportado com a implementação do sistema operativo do Configuration Manager.  

|Configuração do disco rígido do computador de referência|Configuração do disco rígido do computador de destino|  
|------------------------------------------------|--------------------------------------------------|  
|Disco básico|Disco dinâmico|  

## <a name="next-steps"></a>Passos seguintes
[Preparar a implementação do sistema operativo](../get-started/prepare-for-operating-system-deployment.md)
