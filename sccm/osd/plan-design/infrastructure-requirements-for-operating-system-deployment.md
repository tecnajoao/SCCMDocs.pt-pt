---
title: Requisitos de infraestrutura do OSD
titleSuffix: Configuration Manager
description: Conhecer as dependências externas e de produto e os requisitos para a implementação do sistema operacional no Configuration Manager
ms.date: 10/02/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 1dc74219-7ff5-4e3b-b4f6-5aad663bb75b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 03ec9c046e1b32f137777f15393b5d26b49e5520
ms.sourcegitcommit: 265d38d55ca0db043e3a7131a56f123e1d98aa5b
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/03/2018
ms.locfileid: "48236162"
---
# <a name="infrastructure-requirements-for-os-deployment-in-configuration-manager"></a>Requisitos de infraestrutura para implementação do sistema operacional no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Implementação de sistema operacional no Configuration Manager tem dependências externas, bem como as dependências do produto. Utilize este artigo para ajudar a preparar a infraestrutura de implementação do SO.  



##  <a name="BKMK_ExternalDependencies"></a> Dependências externas ao Configuration Manager  

Esta seção fornece informações sobre ferramentas externas, kits de instalação e as versões de SO que são necessárias para implementar sistemas operativos no Configuration Manager.  

### <a name="windows-adk-for-windows-10"></a>Windows ADK para Windows 10  

Windows Assessment and Deployment Kit (ADK) é um conjunto de ferramentas e documentação que suporta a configuração e implantação do Windows. Configuration Manager utiliza o Windows ADK para automatizar ações como instalar o Windows, capturar imagens e migrar perfis de utilizador e dados.  

Para obter mais informações, consulte os artigos seguintes:  

- [Cenários do Windows ADK para Windows 10 para profissionais de TI](https://docs.microsoft.com/windows/deployment/windows-adk-scenarios-for-it-pros)  

- [Transferir o Windows ADK para Windows 10](https://docs.microsoft.com/windows-hardware/get-started/adk-install)  

- [Suporte para Windows 10](/sccm/core/plan-design/configs/support-for-windows-10)  


#### <a name="site-systems"></a>Sistema de sites
O Windows ADK é um pré-requisito para os seguintes servidores de sistemas do site:

- O servidor do site do site de nível superior na hierarquia  

- O servidor do site de cada site primário na hierarquia  

- Todas as instâncias do fornecedor de SMS  


> [!NOTE]  
> Instale manualmente o Windows ADK em cada servidor de site antes de instalar o site do Configuration Manager.  

#### <a name="windows-adk-features"></a>Funcionalidades do Windows ADK
Instale as seguintes funcionalidades do Windows ADK:  

-   User State Migration Tool (USMT)  

    > [!Note]  
    > USMT não é necessário no fornecedor de SMS.

-   Ferramentas de Implementação do Windows  

-   Ambiente de Pré-instalação do Windows (Windows PE)  

    > [!Important]  
    > A partir do Windows 10 versão 1809, o Windows PE é um instalador separado. Caso contrário, não existe nenhuma diferença funcional.<!--SCCMDocs-pr issue 2908-->  

Para obter uma lista das versões do Windows 10 ADK que pode utilizar com diferentes versões do Configuration Manager, consulte [suporte para Windows 10](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk).


### <a name="user-state-migration-tool-usmt"></a>User State Migration Tool (USMT)  

O Configuration Manager utiliza um pacote USMT que inclui os ficheiros de origem USMT 10 para capturar e restaurar o estado do utilizador como parte da implementação do sistema operacional. Configuração do Configuration Manager no site de nível superior cria automaticamente o pacote USMT. O USMT 10 captura o estado de utilizador do Windows 7, Windows 8, Windows 8.1 e Windows 10.  

Para obter mais informações, consulte os artigos seguintes:  

- [Cenários comuns de migração do USMT 10](https://docs.microsoft.com/windows/deployment/usmt/usmt-common-migration-scenarios)  

- [Gerir o estado do utilizador](/sccm/osd/get-started/manage-user-state)  


### <a name="windows-pe"></a>Windows PE  

O Windows PE é utilizado para imagens de arranque para iniciar um computador. É uma versão do Windows com serviços limitados que é utilizada durante a pré-instalação e implantação do Windows. A lista seguinte inclui as versões suportadas do Windows ADK para o Configuration Manager, ramo atual:  

#### <a name="windows-adk-version"></a>Versão do Windows ADK  
Windows ADK para Windows 10. Para obter mais informações, consulte [suporte para Windows 10](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk).

#### <a name="windows-pe-versions-for-boot-images-customizable-from-the-configuration-manager-console"></a>Versões do Windows PE para imagens de arranque podem ser personalizadas na consola do Configuration Manager  
Windows PE 10  

#### <a name="supported-windows-pe-versions-for-boot-images-not-customizable-from-the-configuration-manager-console"></a>Versões suportadas do Windows PE para imagens de arranque não podem ser personalizadas na consola do Configuration Manager  
Windows PE 3.1<sup>1</sup> e Windows PE 5  

<sup>1</sup> só pode adicionar uma imagem de arranque para o Configuration Manager quando se baseia no Windows PE 3.1. Instale o Suplemento do Windows AIK para o Windows 7 SP1 para atualizar o Windows AIK para o Windows 7 (baseado no Windows PE 3) com o Suplemento do Windows AIK para Windows 7 SP1 (baseado no Windows PE 3.1). Transferir o suplemento do Windows AIK para Windows 7 SP1 a partir da [Centro de transferências da Microsoft](https://www.microsoft.com/download/details.aspx?id=5188).  

Por exemplo, quando tem o Configuration Manager, pode personalizar imagens de arranque do Windows ADK para Windows 10 (baseado no Windows PE 10) na consola do Configuration Manager. No entanto, embora as imagens de arranque baseadas no Windows PE 5 sejam suportadas, tem de personalizá-las a partir de um computador diferente e utilizar a versão do DISM que é instalada com o Windows ADK para Windows 8. Em seguida, adicione a imagem de arranque à consola do Configuration Manager. Para obter mais informações sobre os passos para personalizar uma imagem de arranque (adicionar componentes e controladores opcionais), ativar suporte de comando para a imagem de arranque, adicionar a imagem de arranque à consola do Configuration Manager e atualizar pontos de distribuição com a imagem de arranque, consulte [Personalizar imagens de arranque](/sccm/osd/get-started/customize-boot-images). Para obter mais informações sobre imagens de arranque, veja [Gerir imagens de arranque](/sccm/osd/get-started/manage-boot-images).  


### <a name="windows-server-update-services-wsus"></a>Windows Server Update Services (WSUS)  

O WSUS é necessário para o ponto de atualização de software, o que é necessário para instalar atualizações de software durante a implementação do sistema operacional. Para obter mais informações, consulte [instale um configurar um software de ponto de atualização](/sccm/sum/get-started/install-a-software-update-point).


### <a name="internet-information-services-iis-on-the-site-system-servers"></a>IIS (Serviços de Informação Internet) nos servidores do sistema de sites  

O IIS é necessário para o ponto de distribuição, o ponto de migração de estado e o ponto de gestão. Para obter mais informações, veja [Pré-requisitos de site e sistema de sites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).  


### <a name="windows-deployment-services-wds"></a>Serviços de implementação do Windows (WDS)  

Na versão 1802 e anterior, o WDS é necessário para implementações de PXE. A partir da versão 1806, pode ativar o PXE num ponto de distribuição sem WDS. Para obter mais informações, consulte [dos serviços de implantação do Windows](#BKMK_WDS) neste artigo. 


### <a name="dynamic-host-configuration-protocol-dhcp"></a>Protocolo DHCP (Dynamic Host Configuration Protocol)  

O protocolo DHCP é necessário para implementações de PXE. É necessário ter um servidor DHCP a funcionar com um anfitrião ativo para implementar sistemas operativos com PXE. Para obter mais informações sobre implementações de PXE, consulte [utilizar o PXE para implementar o Windows na rede](/sccm/osd/deploy-use/use-pxe-to-deploy-windows-over-the-network).  


### <a name="supported-operating-systems-and-hard-disk-configurations"></a>Sistemas operativos suportados e configurações do disco rígido  

Para obter mais informações sobre as versões de SO e as configurações de disco rígido suportados pelo Configuration Manager quando implementar sistemas operativos, consulte [sistemas operativos suportados](#BKMK_SupportedOS) e [disco suportados configurações](#BKMK_SupportedDiskConfig).  


### <a name="windows-device-drivers"></a>Controladores de dispositivo do Windows  

Controladores de dispositivo do Windows podem ser utilizados quando instalar o sistema operacional no computador de destino. Eles também são usados ao executar o Windows PE numa imagem de arranque. Para obter mais informações, consulte [gerir controladores](/sccm/osd/get-started/manage-drivers).  



##  <a name="BKMK_InternalDependencies"></a> Dependências do Configuration Manager  

Esta seção fornece informações sobre o Configuration Manager OS pré-requisitos de implementação.  


### <a name="os-image"></a>Imagem do SO  

Imagens do sistema operacional no Configuration Manager são armazenadas no formato de ficheiro Windows Imaging (WIM). Eles representam uma coleção comprimida de ficheiros de referência e pastas. Estas imagens são necessários para instalar e configurar um sistema operacional num computador com êxito. Para obter mais informações, consulte [imagens do sistema operacional de gerir](/sccm/osd/get-started/manage-operating-system-images).  


### <a name="driver-catalog"></a>Catálogo de controladores  

Para implementar um controlador de dispositivo, importar o controlador de dispositivo, ativá-la e torná-la disponível num ponto de distribuição que o cliente do Configuration Manager pode aceder. Para obter mais informações sobre o catálogo de controladores, consulte [gerir controladores](/sccm/osd/get-started/manage-drivers).  


### <a name="management-point"></a>Ponto de gestão  

Pontos de gestão transferem informações entre clientes e o site do Configuration Manager. O cliente utiliza um ponto de gestão para executar a sequência de tarefas para concluir a implementação do sistema operacional. Para obter mais informações sobre sequências de tarefas, consulte [considerações sobre planeamento para automatizar tarefas](/sccm/osd/plan-design/planning-considerations-for-automating-tasks).  


### <a name="distribution-point"></a>Ponto de distribuição  

Pontos de distribuição são utilizados na maioria das implementações para armazenar os dados que são utilizados para implementar um sistema operacional, como os pacotes de imagem ou driver. Sequências de tarefas normalmente obtêm dados de um ponto de distribuição para implantar o sistema operacional. Para obter mais informações sobre como instalar pontos de distribuição e gerir conteúdo, consulte [gerir a infraestrutura de conteúdo e conteúda](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure).  


### <a name="pxe-enabled-distribution-point"></a>Ponto de distribuição com PXE ativado  

Para implementar as implementações iniciadas por PXE, configure um ponto de distribuição para aceitar pedidos PXE de clientes. Para obter mais informações, consulte [configurar um ponto de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).


### <a name="multicast-enabled-distribution-point"></a>Ponto de distribuição com multicast ativado  

Para otimizar as suas implementações do sistema operacional por multicast, configure um ponto de distribuição para suportar multicast. Para obter mais informações, consulte [configurar um ponto de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-multicast).   


### <a name="state-migration-point"></a>Ponto de Migração de Estado  

Quando capturar e restaurar dados de estado de utilizador para implementações lado a lado e atualização, configure um ponto de migração de estado para armazenar os dados de estado do utilizador noutro computador.  

Para obter mais informações sobre como configurar o ponto de migração de estado, veja [Ponto de migração de estado](/sccm/osd/get-started/prepare-site-system-roles-for-operating-system-deployments#BKMK_StateMigrationPoints).  

Para obter mais informações sobre como capturar e restaurar estado do utilizador, consulte [gerir o estado do utilizador](/sccm/osd/get-started/manage-user-state).  


### <a name="reporting-services-point"></a>Ponto do Reporting Services  

Para utilizar relatórios do Configuration Manager para Implantações de SO, instalar e configurar um ponto do reporting. Para obter mais informações, consulte [relatórios](/sccm/core/servers/manage/reporting).  


### <a name="security-permissions-for-os-deployments"></a>Permissões de segurança para Implantações de SO  

O **Gestor de implementação do sistema operativo** função de segurança é uma função incorporada que não pode alterar. No entanto, é possível copiar a função, efetuar alterações e, em seguida, guardar estas alterações como uma nova função de segurança personalizada. Aqui estão algumas das permissões que se aplicam diretamente para Implantações de SO:  

- **Pacote de imagem de arranque**: Criar, eliminar, modificar, modificar pasta, mover objeto, ler, definir âmbito de segurança  

- **Controladores de dispositivo**: Criar, eliminar, modificar, modificar pasta, modificar relatório, mover objeto, ler, executar relatório  

- **Pacote de controladores**: Criar, eliminar, modificar, modificar pasta, mover objeto, ler, definir âmbito de segurança  

- **Imagem do sistema operativo**: Criar, eliminar, modificar, modificar pasta, mover objeto, ler, definir âmbito de segurança  

- **Pacote de atualização do sistema operativo**: Criar, eliminar, modificar, modificar pasta, mover objeto, ler, definir âmbito de segurança  

- **Pacote de sequência de tarefas**: Criar, criar tarefa de suporte de dados de sequência, eliminar, modificar, modificar pasta, modificar relatório, mover objeto, ler, executar relatório, definir âmbito de segurança  

Para obter mais informações, consulte [criar funções de segurança personalizadas](/sccm/core/servers/deploy/configure/configure-role-based-administration#BKMK_CreateSecRole).  


### <a name="security-scopes-for-os-deployments"></a>Âmbitos de segurança para Implantações de SO  

Utilize âmbitos de segurança para fornecer aos utilizadores administrativos acesso aos objetos com capacidade de segurança utilizados em implementações de sistema operacional, como o SO e imagens de arranque, pacotes de controladores e pacotes de sequência de tarefas. Para obter mais informações, veja [Âmbitos de segurança](/sccm/core/understand/fundamentals-of-role-based-administration#bkmk_PlanScope).  



##  <a name="BKMK_WDS"></a> Serviços de Implementação do Windows  

Na versão 1802 e anterior, o Windows Deployment Services (WDS) tem de estar instalado no mesmo servidor que os pontos de distribuição que pode configurar para suportar PXE ou multicast. O WDS está incluído no servidor do sistema operacional. Para implementações de PXE, o WDS é o serviço que executa o arranque PXE. Quando o ponto de distribuição é instalado e ativado para PXE, o Configuration Manager instala um fornecedor no WDS que utiliza as funções de arranque de PXE do WDS.  

A partir da versão 1806, pode ativar o PXE num ponto de distribuição sem WDS. Para obter mais informações, consulte a **ativar o dispositivo de resposta PXE sem o serviço de implementação do Windows** opção [instalar e configurar pontos de distribuição](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).


> [!NOTE]  
>  Se o servidor exigir um reinício, a instalação do WDS poderá falhar. 


### <a name="wds-requirements"></a>Requisitos do WDS  

-   A instalação do WDS no servidor requer que o administrador é um membro do grupo Administradores local.  

-   O servidor WDS tem de ser membro de um domínio do Active Directory ou de um controlador de domínio para um domínio do Active Directory. Todas as configurações de domínio e de floresta de Windows suportam WDS.  

-   Se o fornecedor é instalado num servidor remoto, instale o WDS no servidor do site e o fornecedor remoto.  


###  <a name="BKMK_WDSandDHCP"></a> Considerações sobre quando tiver o WDS e DHCP no mesmo servidor  

Se planear coalojar o ponto de distribuição num servidor com o DHCP, considere os seguintes problemas de configuração:  

-   Tem de ter um servidor DHCP funcional com um âmbito ativo. O WDS usa PXE, que requer um servidor DHCP.  

-   Um servidor DNS é necessário para executar o WDS.  

-   As portas UDP seguintes devem estar abertas no servidor do WDS:  

    -   Porta 67 (DHCP)  

    -   Porta 69 (TFTP)  

    -   Porta 4011 (PXE)  

    > [!NOTE]  
    >  Se a autorização de DHCP é necessário no servidor, tem de porta de cliente DHCP 68 estar abertas no servidor.  

-   DHCP e WDS necessitam da porta número 67. Se coalojar o WDS e DHCP, pode mover o DHCP ou o ponto de distribuição que está configurado para PXE para um servidor separado. Em alternativa, pode utilizar o procedimento seguinte para configurar o servidor WDS para escutar numa porta diferente.  

#### <a name="to-configure-the-wds-server-to-listen-on-a-different-port"></a>Para configurar o servidor WDS para escutar numa porta diferente  

1.  Modifique a seguinte chave de registo:  

     `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WDSServer\Providers\WDSPXE`  

2.  Defina o valor de registo **UseDHCPPorts** ao **0**.  

3.  Para efetivar a nova configuração, execute o seguinte comando no servidor:  

     `WDSUTIL /Set-Server /UseDHCPPorts:No /DHCPOption60:Yes`  



##  <a name="BKMK_SupportedOS"></a> Sistemas operativos suportados  

Todos os sistemas de operativos Windows listados como suportado clientes [sistemas operativos suportados por clientes e dispositivos](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices) são suportadas para implementação do sistema operacional.  



##  <a name="BKMK_SupportedDiskConfig"></a> Configurações de disco suportadas  

As combinações de configuração de disco rígido nos computadores de referência e de destino que são suportadas para implementação do SO do Configuration Manager são mostradas na tabela a seguir:  

|Configuração do disco rígido do computador de referência|Configuração do disco rígido do computador de destino|  
|------------------------------------------------|--------------------------------------------------|  
|Disco básico|Disco básico|  
|Volume simples num disco dinâmico|Volume simples num disco dinâmico|  

O Configuration Manager suporta a captura de uma imagem de sistema operacional apenas a partir de computadores que estão configurados com volumes simples. Não há suporte para as seguintes configurações de disco rígido:  

-   Volumes expandidos  

-   Volumes repartidos (RAID 0)  

-   Volumes espelhados (RAID 1)  

-   Volumes de paridade (RAID 5)  

A tabela seguinte mostra uma configuração de disco rígido adicional nos computadores de referência e de destino que não é suportada com a implementação do SO do Configuration Manager.  

|Configuração do disco rígido do computador de referência|Configuração do disco rígido do computador de destino|  
|------------------------------------------------|--------------------------------------------------|  
|Disco básico|Disco dinâmico|  



## <a name="next-steps"></a>Passos seguintes

- [Preparar funções do sistema de sites para implementações de SO](/sccm/osd/get-started/prepare-site-system-roles-for-operating-system-deployments)
- [Preparar a implementação do SO](/sccm/osd/get-started/prepare-for-operating-system-deployment)
