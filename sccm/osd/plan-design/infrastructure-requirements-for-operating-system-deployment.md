---
title: Requisitos de infraestrutura do OSD
titleSuffix: Configuration Manager
description: Saiba os requisitos de implementação do sistema operativo e dependências externas e de produto
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 1dc74219-7ff5-4e3b-b4f6-5aad663bb75b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6407344676230c12c66abb02c1394032e102e4b8
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="infrastructure-requirements-for-os-deployment-in-system-center-configuration-manager"></a>Requisitos de infraestrutura para a implementação do sistema operativo no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Implementação do sistema operativo no Configuration Manager tem dependências externas, bem como as dependências de produto. Utilize este artigo para o ajudar a preparar a infraestrutura para a implementação do SO.  



##  <a name="BKMK_ExternalDependencies"></a> Dependências externas ao Configuration Manager  
 Esta secção fornece informações sobre ferramentas externas, kits de instalação e as versões do SO que são necessários para implementar sistemas operativos no Configuration Manager.  

### <a name="windows-adk-for-windows-10"></a>Windows ADK para Windows 10  
 O Windows Assessment and Deployment Kit (ADK) é um conjunto de ferramentas e documentação que suporta a configuração e implementação do Windows. O Configuration Manager utiliza o Windows ADK para automatizar ações como instalação do Windows, capturar imagens e migrar dados e perfis de utilizador.  

 As seguintes funcionalidades do Windows ADK tem de estar instaladas no servidor do site do site de nível superior da hierarquia, no servidor do site de cada site primário na hierarquia e no servidor de sistema de site do fornecedor de SMS:  

-   User State Migration Tool (USMT) <sup>1</sup>  

-   Ferramentas de Implementação do Windows  

-   Ambiente de Pré-instalação do Windows (Windows PE)

Para obter uma lista das versões do Windows 10 ADK que pode utilizar com diferentes versões do Configuration Manager, consulte [suporte para Windows 10](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk).

 <sup>1</sup> USMT não é necessário no servidor de sistema de site do fornecedor de SMS.  

> [!NOTE]  
>  Deve instalar manualmente o Windows ADK em cada servidor de site antes de instalar o site do Configuration Manager.  

 Para obter mais informações, consulte:  

-   [Cenários do Windows ADK para Windows 10 para profissionais de TI](/windows/deployment/windows-adk-scenarios-for-it-pros)  

-   [Transferir o Windows ADK para Windows 10](/windows-hardware/get-started/adk-install)  

-   [Suporte para Windows 10](/sccm/core/plan-design/configs/support-for-windows-10)  


### <a name="user-state-migration-tool-usmt"></a>User State Migration Tool (USMT)  
 O Configuration Manager utiliza um pacote USMT que inclui os ficheiros de origem USMT 10 para capturar e restaurar o estado do utilizador como parte da implementação do SO. Configuração do Configuration Manager no site de nível superior cria automaticamente o pacote USMT. O USMT 10 captura o estado de utilizador do Windows 7, Windows 8, Windows 8.1 e Windows 10.  

 Para obter mais informações, consulte:  

-   [Cenários comuns de migração para o USMT 10](/windows/deployment/usmt/usmt-common-migration-scenarios)  

-   [Gerir o estado do utilizador](../get-started/manage-user-state.md)  

### <a name="windows-pe"></a>Windows PE  
 O Windows PE é utilizado para imagens de arranque para iniciar um computador. É uma versão do Windows com serviços limitados que é utilizada durante a pré-instalação e implementação do Windows. A lista seguinte inclui as versões suportadas do Windows ADK para o Configuration Manager, o ramo atual:  

-   **Versão do Windows ADK**  

     Windows ADK para Windows 10. Para obter mais informações, consulte [suporte para Windows 10](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk).

-   **Versões do Windows PE para imagens de arranque personalizáveis a partir da consola do Configuration Manager**  

     Windows PE 10  

-   **Versões do Windows PE para imagens de arranque não podem ser personalizadas na consola do Configuration Manager**  

     Windows PE 3.1<sup>1</sup> e Windows PE 5  

     <sup>1</sup> só é possível adicionar uma imagem de arranque para o Configuration Manager quando se baseia no Windows PE 3.1. Instale o Suplemento do Windows AIK para o Windows 7 SP1 para atualizar o Windows AIK para o Windows 7 (baseado no Windows PE 3) com o Suplemento do Windows AIK para Windows 7 SP1 (baseado no Windows PE 3.1). Poderá transferir o Suplemento do Windows AIK para Windows 7 SP1 a partir do [Centro de Transferências da Microsoft](https://www.microsoft.com/download/details.aspx?id=5188).  

     Por exemplo, quando tiver do Configuration Manager, pode personalizar imagens de arranque do Windows ADK para Windows 10 (baseado no Windows PE 10) na consola do Configuration Manager. No entanto, embora as imagens de arranque baseadas no Windows PE 5 sejam suportadas, tem de personalizá-las a partir de um computador diferente e utilizar a versão do DISM que é instalada com o Windows ADK para Windows 8. Em seguida, pode adicionar a imagem de arranque à consola do Configuration Manager. Para obter mais informações sobre os passos para personalizar uma imagem de arranque (adicionar componentes e controladores opcionais), ativar suporte de comando para a imagem de arranque, adicionar a imagem de arranque à consola do Configuration Manager e atualizar pontos de distribuição com a imagem de arranque, consulte [personalizar imagens de arranque](../get-started/customize-boot-images.md). Para obter mais informações sobre imagens de arranque, veja [Gerir imagens de arranque](../get-started/manage-boot-images.md).  


### <a name="windows-server-update-services-wsus"></a>Windows Server Update Services (WSUS)  
 O WSUS é necessário para o ponto de atualização de software, o que é necessário para instalar as atualizações de software durante a implementação do SO. Para obter mais informações, consulte [instalar configurar software de um ponto de atualização](/sccm/sum/get-started/install-a-software-update-point).


### <a name="internet-information-services-iis-on-the-site-system-servers"></a>IIS (Serviços de Informação Internet) nos servidores do sistema de sites  
 IIS é necessário para o ponto de distribuição, o ponto de migração de estado e o ponto de gestão. Para obter mais informações, veja [Pré-requisitos de site e sistema de sites](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  


### <a name="windows-deployment-services-wds"></a>Serviços de implementação do Windows (WDS)  
 O WDS é necessário para implementações de PXE e quando for utilizado multicast para otimizar a largura de banda das implementações. Para obter mais informações, consulte [dos serviços de implementação do Windows](#BKMK_WDS) neste artigo.  


### <a name="dynamic-host-configuration-protocol-dhcp"></a>Protocolo DHCP (Dynamic Host Configuration Protocol)  
 O protocolo DHCP é necessário para implementações de PXE. É necessário ter um servidor DHCP a funcionar com um anfitrião ativo para implementar sistemas operativos com PXE. Para obter mais informações sobre implementações de PXE, consulte [utilizar o PXE para implementar o Windows através da rede](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  


### <a name="supported-operating-systems-and-hard-disk-configurations"></a>Sistemas operativos suportados e configurações do disco rígido  
 Para obter mais informações sobre as versões de sistema operativo e as configurações de disco rígido suportados pelo Configuration Manager quando implementar sistemas operativos, consulte [sistemas operativos suportados](#BKMK_SupportedOS) e [suportados as configurações de disco](#BKMK_SupportedDiskConfig).  


### <a name="windows-device-drivers"></a>Controladores de dispositivo do Windows  
 Controladores de dispositivo do Windows podem ser utilizados quando instalar o sistema operativo no computador de destino. Também são utilizadas quando executar o Windows PE numa imagem de arranque. Para obter mais informações, consulte [gerir controladores](../get-started/manage-drivers.md).  



##  <a name="BKMK_InternalDependencies"></a> Dependências do Configuration Manager  
 Esta secção fornece informações sobre o SO do Configuration Manager, os pré-requisitos de implementação.  


### <a name="os-image"></a>Imagem do SO  
 Imagens de SO no Configuration Manager são armazenadas no formato de ficheiro Windows Imaging (WIM). Estes representam uma coleção comprimida de ficheiros de referência e de pastas. Estas imagens são necessários para instalar e configurar o sistema operativo num computador com êxito. Para obter mais informações, consulte [gerir imagens do sistema operativo](../get-started/manage-operating-system-images.md).  


### <a name="driver-catalog"></a>Catálogo de controladores  
 Para implementar um controlador de dispositivo, tem de importar o controlador de dispositivo, ativá-lo e disponibilizá-lo num ponto de distribuição que o cliente do Configuration Manager pode aceder. Para mais informações sobre o catálogo de controladores, consulte [gerir controladores](../get-started/manage-drivers.md).  


### <a name="management-point"></a>Ponto de gestão  
 Pontos de gestão transferem informações entre clientes e o site do Configuration Manager. O cliente utiliza um ponto de gestão para executar a sequência de tarefas para concluir a implementação do SO. Para obter mais informações sobre sequências de tarefas, consulte [considerações sobre planeamento para automatizar tarefas](planning-considerations-for-automating-tasks.md).  


### <a name="distribution-point"></a>Ponto de distribuição  
 Na maioria das implementações, são utilizados pontos de distribuição para armazenar os dados que são utilizados para implementar o sistema operativo, tais como os pacotes de controlador ou imagem. Sequências de tarefas normalmente obtêm dados de um ponto de distribuição para implementar o sistema operativo. Para obter mais informações sobre como instalar pontos de distribuição e gerir conteúdo, consulte [gerir a infraestrutura de conteúdo e conteúda](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  


### <a name="pxe-enabled-distribution-point"></a>Ponto de distribuição com PXE ativado  
 Para realizar implementações iniciadas por PXE, é necessário configurar um ponto de distribuição para aceitar pedidos PXE de clientes. Para obter mais informações, consulte [configurar um ponto de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#pxe).


### <a name="multicast-enabled-distribution-point"></a>Ponto de distribuição com multicast ativado  
 Para otimizar as implementações de SO através de multicast, tem de configurar um ponto de distribuição para suportar multicast. Para obter mais informações, consulte [configurar um ponto de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#multicast).   


### <a name="state-migration-point"></a>Ponto de Migração de Estado  
 Ao capturar e restaurar dados do estado do utilizador para implementações lado a lado e de atualizações, é necessário configurar um ponto de migração de estado para armazenar os dados do estado do utilizador noutro computador.  

 Para obter mais informações sobre como configurar o ponto de migração de estado, veja [Ponto de migração de estado](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

 Para obter informações sobre como capturar e restaurar estado do utilizador, consulte [gerir o estado do utilizador](../get-started/manage-user-state.md).  


### <a name="reporting-services-point"></a>Ponto do Reporting Services  
 Para utilizar relatórios do Configuration Manager para implementações do SO, tem de instalar e configurar um ponto do Reporting Services. Para obter mais informações, consulte [relatórios](../../core/servers/manage/reporting.md).  


### <a name="security-permissions-for-os-deployments"></a>Permissões de segurança para implementações de SO  
 O **Gestor de implementação do sistema operativo** função de segurança é uma função incorporada que não é possível alterar. No entanto, é possível copiar a função, efetuar alterações e, em seguida, guardar estas alterações como uma nova função de segurança personalizada. Aqui estão algumas das permissões que são diretamente aplicam a implementações do SO:  

-   **Pacote de imagem de arranque**: Criar, eliminar, modificar, modificar pasta, mover objeto, ler, definir âmbito de segurança  

-   **Controladores de dispositivo**: Criar, eliminar, modificar, modificar pasta, modificar relatório, mover objeto, ler, executar relatório  

-   **Pacote de controladores**: Criar, eliminar, modificar, modificar pasta, mover objeto, ler, definir âmbito de segurança  

-   **Imagem do sistema operativo**: Criar, eliminar, modificar, modificar pasta, mover objeto, ler, definir âmbito de segurança  

-   **Pacote de instalação do sistema operativo**: Criar, eliminar, modificar, modificar pasta, mover objeto, ler, definir âmbito de segurança  

-   **Pacote de sequência de tarefas**: Criar, criar tarefa de suporte de dados de sequência, eliminar, modificar, modificar pasta, modificar relatório, mover objeto, ler, executar relatório, definir âmbito de segurança  

 Para obter mais informações, consulte [criar funções de segurança personalizadas](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole).  


### <a name="security-scopes-for-os-deployments"></a>Âmbitos de segurança para implementações de SO  
 Utilize âmbitos de segurança para fornecer aos utilizadores administrativos acesso aos objetos com capacidade de segurança utilizados em implementações de SO, por exemplo, o SO e imagens de arranque, pacotes de controladores e pacotes de sequências de tarefas. Para obter mais informações, veja [Âmbitos de segurança](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope).  



##  <a name="BKMK_WDS"></a> Serviços de Implementação do Windows  
 O WDS (Serviços de Implementação do Windows) deve ser instalado no mesmo servidor que os pontos de distribuição configurados para suporte de PXE ou multicast. O WDS está incluído no sistema operativo do servidor. Para implementações de PXE, o WDS é o serviço que executa o arranque PXE. Quando o ponto de distribuição é instalado e ativado para PXE, o Configuration Manager instala um fornecedor no WDS que utiliza as funções de arranque PXE do WDS.  

> [!NOTE]  
>  Se o servidor requer um reinício, a instalação do WDS poderá falhar. 


### <a name="wds-requirements"></a>Requisitos do WDS  

-   A instalação do WDS no servidor requer que o administrador seja um membro do grupo de administradores locais.  

-   O servidor WDS tem de ser membro de um domínio do Active Directory ou de um controlador de domínio para um domínio do Active Directory. Todas as configurações de domínio e de floresta de Windows suportam WDS.  

-   Se o fornecedor estiver instalado num servidor remoto, deve instalar o WDS no servidor do site e o fornecedor remoto.  


###  <a name="BKMK_WDSandDHCP"></a> Considerações sobre quando tiver o WDS e DHCP no mesmo servidor  
 Se planear coalojar o ponto de distribuição num servidor com o DHCP, considere os seguintes problemas de configuração.  

-   Tem de ter um servidor DHCP funcional com um âmbito ativo. O WDS utilizam PXE, que necessita de um servidor DHCP.  

-   DHCP e WDS necessitam da porta número 67. Se coalojar o WDS e DHCP, pode mover o DHCP ou o ponto de distribuição que está configurado para PXE para um servidor separado. Em alternativa, pode utilizar o procedimento seguinte para configurar o servidor WDS para escutar numa porta diferente.  

    #### <a name="to-configure-the-wds-server-to-listen-on-a-different-port"></a>Para configurar o servidor WDS para escutar numa porta diferente  

    1.  Modifique a seguinte chave de registo:  

         `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WDSServer\Providers\WDSPXE`  

    2.  Defina o valor de registo **UseDHCPPorts** para **0**.  

    3.  Para efetivar a nova configuração, execute o seguinte comando no servidor:  

         `WDSUTIL /Set-Server /UseDHCPPorts:No /DHCPOption60:Yes`  

-   Um servidor DNS é necessário para executar o WDS.  

-   As portas UDP seguintes devem estar abertas no servidor WDS.  

    -   Porta 67 (DHCP)  

    -   Porta 69 (TFTP)  

    -   Porta 4011 (PXE)  

    > [!NOTE]  
    >  Se for necessária autorização de DHCP no servidor, terá de porta de cliente DHCP 68 estar aberta no servidor.  



##  <a name="BKMK_SupportedOS"></a> Sistemas operativos suportados  
 Todos os sistemas operativos do Windows listados como suportado clientes [sistemas operativos suportados para os clientes e dispositivos](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md) são suportados para a implementação do SO.  



##  <a name="BKMK_SupportedDiskConfig"></a> Configurações de disco suportadas  
 As combinações de configuração de disco rígido nos computadores de referência e de destino que são suportados para a implementação do SO do Configuration Manager são apresentadas na tabela seguinte:  

|Configuração do disco rígido do computador de referência|Configuração do disco rígido do computador de destino|  
|------------------------------------------------|--------------------------------------------------|  
|Disco básico|Disco básico|  
|Volume simples num disco dinâmico|Volume simples num disco dinâmico|  

 O Configuration Manager suporta capturar uma imagem do SO apenas de computadores que estão configurados com volumes simples. Não são suportadas para as seguintes configurações de disco rígido:  

-   Volumes expandidos  

-   Volumes repartidos (RAID 0)  

-   Volumes espelhados (RAID 1)  

-   Volumes de paridade (RAID 5)  

 A tabela seguinte mostra uma configuração adicional do disco rígido nos computadores de referência e de destino que não é suportada com a implementação do SO do Configuration Manager.  

|Configuração do disco rígido do computador de referência|Configuração do disco rígido do computador de destino|  
|------------------------------------------------|--------------------------------------------------|  
|Disco básico|Disco dinâmico|  



## <a name="next-steps"></a>Passos seguintes
- [Preparar funções do sistema de sites para implementações de SO](/sccm/osd/get-started/prepare-site-system-roles-for-operating-system-deployments)
- [Preparar a implementação do SO](../get-started/prepare-for-operating-system-deployment.md)
