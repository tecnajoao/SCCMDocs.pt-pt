---
title: Portas utilizadas para ligações
titleSuffix: Configuration Manager
description: Saiba mais sobre as portas de rede necessários e personalizáveis que o Configuration Manager utiliza para ligações.
ms.date: 01/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c6777fb0-0754-4abf-8a1b-7639d23e9391
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7aaadae5feaff2aa55e521c4b7438f4f1d24209a
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56156819"
---
# <a name="ports-used-in-configuration-manager"></a>Portas utilizadas no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo lista as portas de rede utilizadas pelo Configuration Manager. Algumas ligações utilizam portas que não são configuráveis e outras suportam portas personalizadas que especificar. Se usar qualquer tecnologia de filtragem de portas, certifique-se de que as portas necessárias estão disponíveis. Estas tecnologias de filtragem de porta incluem firewalls, routers, servidores proxy ou IPsec.   

> [!NOTE]  
>  Se oferecer suporte a clientes baseados na internet ao utilizar o protocolo de bridge SSL, para além dos requisitos de porta, também poderá ter de permitir que alguns verbos e cabeçalhos HTTP atravessem a firewall.   



##  <a name="BKMK_ConfigurablePorts"></a> Portas que pode configurar  
 O Configuration Manager permite-lhe configurar as portas para os seguintes tipos de comunicação:  

-   Ponto de Web site do catálogo de aplicações para o ponto de serviço web do catálogo de aplicações  

-   Ponto proxy de registo com o ponto de registo  

-   Sistemas de site de cliente que executam o IIS  

-   Cliente com a internet (como definições do servidor proxy)  

-   Ponto de atualização de software para internet (como definições do servidor proxy)  

-   Ponto de atualização de software com o servidor WSUS  

-   Servidor do site com o servidor da base de dados do site  

-   Pontos do Reporting Services  

    > [!NOTE]  
    >  As portas que estão a ser utilizados para a função de sistema de sites de ponto do reporting services são configuradas no SQL Server Reporting Services. Estas portas, em seguida, são utilizadas pelo Configuration Manager durante as comunicações com o ponto do reporting services. Certifique-se de que revê estas portas que definem as informações de filtro IP para políticas IPsec ou para configurar firewalls.  

Por predefinição, a porta HTTP que é utilizada para comunicação cliente-para-site system é a porta 80 e a porta HTTPS predefinida é 443. Portas para comunicações do sistema de cliente-para-site por HTTP ou HTTPS podem ser alteradas durante a configuração ou nas propriedades do site para o seu site do Configuration Manager.  

As portas que estão a ser utilizados para a função de sistema de sites de ponto do reporting services são configuradas no SQL Server Reporting Services. Estas portas, em seguida, são utilizadas pelo Configuration Manager durante as comunicações com o ponto do reporting services. Certifique-se de que revê estas portas, quando está a definir as informações de filtro IP para políticas IPsec ou para configurar firewalls.  



##  <a name="BKMK_NonConfigurablePorts"></a> Portas não configuráveis  

O Configuration Manager não permite configurar portas para os seguintes tipos de comunicação:  

-   Site para site  

-   Servidor do site com o sistema de sites  

-   Consola do Configuration Manager para o fornecedor de SMS  

-   Consola do Configuration Manager para a internet  

-   Ligações a serviços em nuvem, como pontos de distribuição do Microsoft Intune e na cloud  



##  <a name="BKMK_CommunicationPorts"></a> Portas utilizadas por clientes e sistemas de sites do Configuration Manager  

As secções seguintes detalham as portas que são utilizadas para comunicação no Configuration Manager. As setas no título da secção mostram a direção da comunicação:  

-   -> Indica que um computador inicia a comunicação e o outro computador responde sempre  

-   &lt; -> Indica que ambos os computadores podem iniciar comunicações  


###  <a name="BKMK_PortsAI"></a> Ponto de sincronização do Asset Intelligence-- > Microsoft  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  


###  <a name="BKMK_PortsAI-to-SQL"></a> Ponto de sincronização do Asset Intelligence-- > SQL Server  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 <sup> [nota 2](#bkmk_note2) alternativo porta disponível</sup>|  


###  <a name="BKMK_PortsAppCatalogService-SQL"></a> Ponto de serviço de web de catálogo de aplicações-- > SQL Server  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 <sup> [nota 2](#bkmk_note2) alternativo porta disponível</sup>|  


###  <a name="BKMK_PortsAppCatalogWebSitePoint_AppCatalogWebServicePoint"></a> Ponto de Web site do catálogo de aplicações-- > ponto de serviço web do catálogo de aplicações  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup> [nota 2](#bkmk_note2) alternativo porta disponível</sup>|  
|HTTPS|--|443 <sup> [nota 2](#bkmk_note2) alternativo porta disponível</sup>|  


###  <a name="BKMK_PortsClient-AppCatalogWebsitePoint"></a> Cliente--> Ponto de Web sites do catálogo de aplicações  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup> [nota 2](#bkmk_note2) alternativo porta disponível</sup>|  
|HTTPS|--|443 <sup> [nota 2](#bkmk_note2) alternativo porta disponível</sup>|  


###  <a name="BKMK_PortsClient-ClientWakeUp"></a> Cliente -- &gt; Cliente  

Além das portas que estão listadas nesta tabela, o proxy de reativação também utiliza mensagens de pedido de eco do ICMP de um cliente para outro cliente. Os clientes utilizam esta comunicação para confirmar se a outro cliente está ativo na rede. ICMP é por vezes referido como comandos de ping. ICMP não tem um número de protocolo UDP ou TCP e, portanto, não está listado na tabela a seguir. No entanto, as firewalls baseadas no anfitrião existentes nestes computadores cliente ou em dispositivos de rede intervenientes na sub-rede devem permitir o tráfego ICMP para que a comunicação de proxy de reativação tenha êxito.  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Reativação Por LAN|9 <sup> [nota 2](#bkmk_note2) alternativo porta disponível</sup>|--|  
|Proxy de reativação|25536 <sup> [nota 2](#bkmk_note2) alternativo porta disponível</sup>|--|  
|Difusão de cache ponto a ponto do Windows PE|8004|--|  
|Download de cache ponto a ponto do Windows PE|--|8003|  

Para obter mais informações, consulte [a Cache ponto a ponto do Windows PE](/sccm/osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md#-requirements-for-a-client-to-use-a--windows-pe-peer-cache-source).


###  <a name="BKMK_PortsClient-PolicyModule"></a> Cliente--> Módulo de política do Configuration Manager dispositivo inscrição serviço rede (NDES)   

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP||80|  
|HTTPS|--|443|  


###  <a name="BKMK_PortsClient-CloudDP"></a> Cliente--> Ponto de distribuição de nuvem  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

Para obter mais informações, consulte [fluxo de dados e de portas](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#bkmk_dataflow).


###  <a name="bkmk_client-cmg"></a> Cliente--> Gateway de gestão na Cloud (CMG)  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

Para obter mais informações, consulte [fluxo de dados e de portas de CMG](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#ports-and-data-flow).


###  <a name="BKMK_PortsClient-DP"></a> Cliente--> Ponto de distribuição  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup> [nota 2](#bkmk_note2) alternativo porta disponível</sup>|  
|HTTPS|--|443 <sup> [nota 2](#bkmk_note2) alternativo porta disponível</sup>|  


###  <a name="BKMK_PortsClient-DP2"></a> Cliente--> Ponto de distribuição configurado para multicast  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Protocolo multicast|63000-64000|--|  

###  <a name="BKMK_PortsClient-DP3"></a> Cliente--> Ponto de distribuição configurado para PXE  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|DHCP|67 e 68|--|  
|TFTP|69 <sup> [observe 4](#bkmk_note4)</sup> |--|  
|Boot Information Negotiation Layer (BINL)|4011|--|  

> [!Important]  
> Se habilitar uma firewall baseada no anfitrião, certifique-se de que as regras de permitir que o servidor enviar e receber nessas portas. Quando ativa um ponto de distribuição para PXE, o Configuration Manager pode ativar a entrada (recepção) regras na Firewall do Windows. Ele não configure as regras de saída (enviar).<!--SCCMDocs issue #744-->  


###  <a name="BKMK_PortsClient-FSP"></a> Cliente--> Ponto de estado de contingência  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup> [nota 2](#bkmk_note2) alternativo porta disponível</sup>|  


###  <a name="BKMK_PortsClient-GCDC"></a> Cliente--> Controlador de domínio de Catálogo Global  
 Um cliente do Configuration Manager não contacta um servidor de catálogo global, quando ele é um computador de grupo de trabalho ou quando está configurado para comunicação apenas na internet.  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|LDAP de catálogo global|--|3268|  


###  <a name="BKMK_PortsClient-MP"></a> Cliente--> Ponto de gestão  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Notificação de cliente (comunicação predefinida antes de reverter para HTTP ou HTTPS)|--|10123 <sup> [nota 2](#bkmk_note2) alternativo porta disponível</sup>|  
|HTTP|--|80 <sup> [nota 2](#bkmk_note2) alternativo porta disponível</sup>|  
|HTTPS|--|443 <sup> [nota 2](#bkmk_note2) alternativo porta disponível</sup>|  


###  <a name="BKMK_PortsClient-SUP"></a> Cliente--> Ponto de atualização de Software  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 ou 8530 <sup> [observe 3](#bkmk_note3)</sup>|  
|HTTPS|--|443 ou 8531 <sup> [observe 3](#bkmk_note3)</sup>|  


###  <a name="BKMK_PortsClient-SMP"></a> Cliente--> Ponto de migração de estado  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup> [nota 2](#bkmk_note2) alternativo porta disponível</sup>|  
|HTTPS|--|443 <sup> [nota 2](#bkmk_note2) alternativo porta disponível</sup>|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  


###  <a name="bkmk_cmgcp-cmg"></a> Ponto de ligação do CMG-- > serviço cloud do CMG  

O Configuration Manager utiliza estas ligações para criar o canal CMG. Para obter mais informações, consulte [fluxo de dados e de portas de CMG](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#ports-and-data-flow).

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|TCP-TLS (preferidas)|--|10140-10155|  
|HTTPS (contingência com uma VM)|--|443|  
|HTTPS (contingência com duas ou mais VMs)|--|10124-10139|  


###  <a name="bkmk_cmgcp-mp"></a> Ponto de ligação do CMG-- > ponto de gestão  

#### <a name="version-1706-or-1710"></a>Versão 1706 ou 1710
A porta específica depende da configuração de ponto de gestão. 

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|
|HTTP|--|80|  

#### <a name="version-1802"></a>Versão 1802

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|

Para obter mais informações, consulte [fluxo de dados e de portas de CMG](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#ports-and-data-flow).


###  <a name="bkmk_cmgcp-sup"></a> Ponto de ligação do CMG-- > ponto de atualização de Software  

A porta específica depende da configuração de ponto de atualização de software. 

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|
|HTTP|--|80|  

Para obter mais informações, consulte [fluxo de dados e de portas de CMG](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#ports-and-data-flow).


###  <a name="BKMK_PortsConsole-Client"></a> Consola do Configuration Manager-- > cliente  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Controlo Remoto (controlo)|--|2701|  
|Assistência Remota (RDP e RTC)|--|3389|  


###  <a name="BKMK_PortsConsole-Internet"></a> Consola do Configuration Manager-- > Internet  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80|  
|HTTPS|--|443|

Consola do Configuration Manager utiliza o acesso à internet para as seguintes ações: 
- A transferir atualizações de software do Microsoft Update para pacotes de implementação.
- O item de comentário na faixa de opções.
- Ligações para documentação da consola do.
<!--506823-->


###  <a name="BKMK_PortsConsole-RSP"></a> Consola do Configuration Manager-- > ponto do Reporting services  


|Descrição|UDP|TCP|
|-----------------|---------|---------|   
|HTTP|--|80 <sup> [nota 2](#bkmk_note2) alternativo porta disponível</sup>|  
|HTTPS|--|443 <sup> [nota 2](#bkmk_note2) alternativo porta disponível</sup>|  


###  <a name="BKMK_PortsConsole-Site"></a> Consola do Configuration Manager-- > servidor do Site  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|RPC (ligação inicial ao WMI para localizar o sistema do fornecedor)|--|135|  


###  <a name="BKMK_PortsConsole-Provider"></a> Consola do Configuration Manager-- > fornecedor de SMS  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|DINÂMICA <sup> [observe 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_PortsCertificateRegistationPoint_PolicyModule"></a> Módulo de política do Configuration Manager dispositivo inscrição serviço rede (NDES) - > ponto de registo de certificados  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443 <sup> [nota 2](#bkmk_note2) alternativo porta disponível</sup>|  


###  <a name="BKMK_PortsDWSPSQL"></a> Armazém de dados do ponto de serviço-- > SQL Server  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 <sup> [nota 2](#bkmk_note2) alternativo porta disponível</sup>|  


###  <a name="BKMK_PortsDist_MP"></a> Ponto de distribuição-- > ponto de gestão  
 Um ponto de distribuição comunica com o ponto de gestão nos seguintes cenários:  

-   Comunicar o estado de conteúdo pré-configurado  

-   Para reportar dados de resumo de utilização  

-   Para reportar validação de conteúdo  

-   Comunicar o estado de downloads de pacote (ponto de distribuição de extração)

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup> [nota 2](#bkmk_note2) alternativo porta disponível</sup>|  
|HTTPS|--|443 <sup> [nota 2](#bkmk_note2) alternativo porta disponível</sup>|  


###  <a name="BKMK_PortsEndpointProtection_Internet"></a> Ponto do Endpoint Protection-- > Internet  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80|  


###  <a name="BKMK_PortsEP-to-SQL"></a> Ponto do Endpoint Protection-- > SQL Server  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 <sup> [nota 2](#bkmk_note2) alternativo porta disponível</sup>|  


###  <a name="BKMK_PortsEnrollmentProxyEnrollmentPoint"></a> Ponto de proxy de registo-- > ponto de registo  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443 <sup> [nota 2](#bkmk_note2) alternativo porta disponível</sup>|  


###  <a name="BKMK_PortsEnrollmentEnrollmentSQL"></a> Ponto de inscrição-- > SQL Server  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 <sup> [nota 2](#bkmk_note2) alternativo porta disponível</sup>|  


###  <a name="BKMK_PortsExchangeConnectorHosted"></a> Conector do Exchange Server -- &gt; Exchange Online  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Gestão Remota do Windows através de HTTPS|--|5986|  


###  <a name="BKMK_PortsExchangeConnectorOnPrem"></a> Conector do Exchange Server – > On-Premises Exchange Server  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Gestão Remota do Windows através de HTTP|--|5985|  


###  <a name="BKMK_PortsMacEnrollmentProxyPoint"></a> Computador Mac-- > ponto proxy de registo  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  


###  <a name="BKMK_PortsMP-DC"></a> Ponto de gestão-- > controlador de domínio  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|LDAP (Lightweight Directory Access Protocol)|389|389|  
|LDAP de catálogo global|--|3268|  
|Mapeador de Pontos Finais RPC|--|135|  
|RPC|--|DINÂMICA <sup> [observe 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_PortsMP-Site"></a> Ponto de gestão &lt; -> servidor do Site  
 <sup>[Nota 5](#bkmk_note5)</sup>   

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Mapeador de Pontos Finais RPC|--|135|  
|RPC|--|DINÂMICA <sup> [observe 6](#bkmk_note6)</sup>|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  


###  <a name="BKMK_PortsMP-SQL"></a> Ponto de gestão-- > SQL Server  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 <sup> [nota 2](#bkmk_note2) alternativo porta disponível</sup>|  


###  <a name="BKMK_PortsMobileDeviceClient-EnrollmentProxyPoint"></a> Dispositivo móvel-- > ponto proxy de registo  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  


###  <a name="BKMK_PortsMobileDeviceClient-WindowsIntune"></a> Dispositivo móvel-- > Microsoft Intune  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  


###  <a name="BKMK_PortsRSP-SQL"></a> Ponto do Reporting Services - > SQL Server  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 <sup> [nota 2](#bkmk_note2) alternativo porta disponível</sup>|  


###  <a name="BKMK_PortsIntuneConnector-WindowsIntune"></a> Serviço de ponto de ligação-- > Microsoft Intune  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|

Para obter mais informações, consulte [requisitos de acesso de Internet](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_urls) para o ponto de ligação de serviço.


###  <a name="bkmk_scp-cmg"></a> Serviço de ponto de ligação-- > do Azure (CMG)  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS para implementação do serviço CMG|--|443|

Para obter mais informações, consulte [fluxo de dados e de portas de CMG](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#ports-and-data-flow).


###  <a name="BKMK_PortsAppCatalogWebServicePoint_SiteServer"></a> Servidor do site &lt; -> ponto de serviço web do catálogo de aplicações  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|DINÂMICA <sup> [observe 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_PortsAppCatalogWebSitePoint_SiteServer"></a> Servidor do site &lt; -> ponto de Web sites do catálogo de aplicações  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|DINÂMICA <sup> [observe 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_PortsSite-AISP"></a> Servidor do site &lt; -> ponto de sincronização do Asset Intelligence  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|DINÂMICA <sup> [observe 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_PortsSite-Client"></a> Servidor do site-- > cliente  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Reativação Por LAN|9 <sup> [nota 2](#bkmk_note2) alternativo porta disponível</sup>|--|  


###  <a name="BKMK_PortsSiteServer-CloudDP"></a> Servidor do site-- > ponto de distribuição da nuvem  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

Para obter mais informações, consulte [fluxo de dados e de portas](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#bkmk_dataflow).


###  <a name="BKMK_PortsSite-DP"></a> Servidor do site-- > ponto de distribuição  
 <sup>[Nota 5](#bkmk_note5)</sup>  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|DINÂMICA <sup> [observe 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_PortsSite-DC"></a> Servidor do site-- > controlador de domínio  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|LDAP (Lightweight Directory Access Protocol)|389|389|  
|LDAP de catálogo global|--|3268|  
|Mapeador de Pontos Finais RPC|--|135|  
|RPC|--|DINÂMICA <sup> [observe 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_PortsCertificateRegistrationPoint_SiteServer"></a> Servidor do site &lt; -> ponto de registo de certificados  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|DINÂMICA <sup> [observe 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_PortsEndpointProtection_SiteServer"></a> Servidor do site &lt; -> ponto do Endpoint Protection  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|DINÂMICA <sup> [observe 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_EnrollmentPoint_SiteServer"></a> Servidor do site &lt; -> ponto de registo  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|DINÂMICA <sup> [observe 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_EnrollmentProxyPoint_SiteServer"></a> Servidor do site &lt; -> ponto proxy de registo  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|DINÂMICA <sup> [observe 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_PortsSite-FSP"></a> Servidor do site &lt; -> ponto de estado de contingência  
 <sup>[Nota 5](#bkmk_note5)</sup>  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|DINÂMICA <sup> [observe 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_PortSite-Internet"></a> Servidor do site-- > Internet  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup> [observe 1](#bkmk_note1)</sup>|  


###  <a name="BKMK_PortsIssuingCA_SiteServer"></a> Servidor do site &lt; -> autoridade de certificação (AC) emissora  
 Esta comunicação é utilizada na implementação de perfis de certificado, utilizando o ponto de registo de certificados. A comunicação não é utilizada para cada servidor do site na hierarquia. Em vez disso, é utilizado apenas para o servidor de site na parte superior da hierarquia.  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC (DCOM)|--|DINÂMICA <sup> [observe 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_PortsSite-RSP"></a> Servidor do site &lt; -> ponto do Reporting services  
 <sup>[Nota 5](#bkmk_note5)</sup>  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|DINÂMICA <sup> [observe 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_PortsSite-Site"></a> Servidor do site &lt; -> servidor do Site  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  


###  <a name="BKMK_PortsSite-SQL"></a> Servidor do site-- > SQL Server  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 <sup> [nota 2](#bkmk_note2) alternativo porta disponível</sup>|  

 Durante a instalação de um site que utiliza um SQL Server remoto para alojar a base de dados do site, abra as seguintes portas entre o servidor do site e o SQL Server:  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|DINÂMICA <sup> [observe 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_PortsSite-Provider"></a> Servidor do site-- > fornecedor de SMS  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|DINÂMICA <sup> [observe 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_PortsSite-SUP"></a> Servidor do site &lt; -> ponto de atualização de Software  
 <sup>[Nota 5](#bkmk_note5)</sup>  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|HTTP|--|80 ou 8530 <sup> [observe 3](#bkmk_note3)</sup>|  
|HTTPS|--|443 ou 8531 <sup> [observe 3](#bkmk_note3)</sup>|  


###  <a name="BKMK_PortsSite-SMP"></a> Servidor do site &lt; -> ponto de migração de estado  
 <sup>[Nota 5](#bkmk_note5)</sup>  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Mapeador de Pontos Finais RPC|135|135|  


###  <a name="BKMK_PortsProvider-SQL"></a> Fornecedor de SMS -- &gt; SQL Server  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 <sup> [nota 2](#bkmk_note2) alternativo porta disponível</sup>|  


###  <a name="BKMK_PortsSUP-Internet"></a> Ponto de atualização de software-- > Internet  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup> [observe 1](#bkmk_note1)</sup>|  


###  <a name="BKMK_PortsSUP-WSUS"></a> Ponto de atualização de software-- > servidor WSUS a montante  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 ou 8530 <sup> [observe 3](#bkmk_note3)</sup>|  
|HTTPS|--|443 ou 8531 <sup> [observe 3](#bkmk_note3)</sup>|  


###  <a name="BKMK_PortsSQL-SQL"></a> SQL Server --&gt; SQL Server  
 Replicação de base de dados entre sites requer o SQL Server num site comunicar diretamente com o SQL Server no seu site principal ou subordinado.  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Serviço do SQL Server|--|1433 <sup> [nota 2](#bkmk_note2) alternativo porta disponível</sup>|  
|SQL Server Service Broker|--|4022 <sup> [nota 2](#bkmk_note2) alternativo porta disponível</sup>|  

> [!TIP]  
>  O Configuration Manager não requer o SQL Server Browser, que utiliza a porta UDP 1434.  


###  <a name="BKMK_PortsStateMigrationPoint-to-SQL"></a> Estado do ponto de migração-- > SQL Server  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 <sup> [nota 2](#bkmk_note2) alternativo porta disponível</sup>|  


###  <a name="BKMY_PortNotes"></a> Notas relativas às portas utilizadas por clientes e sistemas de sites do Configuration Manager  

#### <a name="bkmk_note1"></a> Nota 1: Porta do servidor proxy
Esta porta não pode ser configurada, mas pode ser encaminhada através de um servidor proxy configurado.  

#### <a name="bkmk_note2"></a> Nota 2: Porta alternativa disponível
Uma porta alternativa pode ser definida dentro do Configuration Manager para este valor. Se tiver sido definida uma porta personalizada, substitua-a quando definir as informações de filtro IP para políticas IPsec ou para configurar firewalls.  

#### <a name="bkmk_note3"></a> Tenha em atenção 3: Windows Server Update Services (WSUS)
WSUS pode ser instalado para utilizar portas 80/443 ou as portas 8530/8531 para comunicações de clientes. Quando executar o WSUS no Windows Server 2012 ou Windows Server 2016, o WSUS é configurado por predefinição para utilizar a porta 8530 para HTTP e a porta 8531 para HTTPS.  

Após a instalação, é possível alterar a porta. Não precisa usar o mesmo número de porta em toda a hierarquia do site.  

- Se a porta HTTP for 80, a porta HTTPS tem de ser 443.  

- Se a porta HTTP for qualquer outra coisa, a porta HTTPS tem de ser 1 ou superior, por exemplo, 8530 e 8531.   

    > [!NOTE]  
    >  Quando configura o ponto de atualização de software para utilizar HTTPS, a porta HTTP também tem de estar aberta. Os dados não encriptados, como o EULA para atualizações específicas, utilizam a porta HTTP.  

#### <a name="bkmk_note4"></a> Tenha em atenção 4: Daemon trivial FTP (TFTP)
O serviço de sistema do Daemon Trivial FTP (TFTP) não requer um nome de utilizador ou palavra-passe e faz parte integrante do Windows Deployment Services (WDS). O serviço de Trivial FTP Daemon implementa suporte para o protocolo TFTP definido pelos RFC seguintes:  

- RFC 350: TFTP  

- RFC 2347: Extensão de opção  

- RFC 2348: Opção de tamanho de bloco  

- RFC 2349: Opções de tamanho de intervalo e a transferência de limite de tempo  

TFTP foi concebido para suportar ambientes de arranque sem disco. Os Daemons TFTP escutam a porta UDP 69 mas respondem a partir de uma porta alta alocada dinamicamente. Por conseguinte, a ativação desta porta permite que o serviço TFTP receber pedidos de TFTP de entrada mas não permite que o servidor selecionado responda a esses pedidos. Não é possível ativar o servidor selecionado responda a pedidos TFTP de entrada, a menos que o servidor TFTP esteja configurado para responder na porta 69.  

O ponto de distribuição com PXE ativado e o cliente no Windows PE selecione alocadas dinamicamente portas de elevada para transferências do TFTP. Estas portas são definidas pelo Microsoft entre 49152 e 65535. Para obter mais informações, consulte [descrição geral dos serviços e requisitos de portas para o Windows de rede](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows)

No entanto, durante o arranque PXE real, a placa de rede no dispositivo seleciona a porta alta alocada dinamicamente, que ele usa durante a transferência do TFTP. A placa de rede no dispositivo não está vinculada às portas de alta alocadas dinamicamente definidas pela Microsoft. Apenas está vinculado às portas definidas no RFC 350. Esta porta pode ser qualquer um de 0 a 65535. Para obter informações sobre o que atribuído dinamicamente portas de elevada as utilizações de placa de rede, contacte o fabricante de hardware do dispositivo.


#### <a name="bkmk_note5"></a> Tenha em atenção 5: Comunicação entre o servidor do site e sistemas de sites
Por predefinição, a comunicação entre o servidor do site e sistemas de sites é bidirecional. O servidor do site inicia a comunicação para configurar o sistema de sites e, em seguida, a maioria dos sistemas de sites restabelece ligação ao servidor do site para enviar informações de estado. Pontos do Reporting Services e pontos de distribuição não enviam informações de estado. Se selecionou **exigir que o servidor do site inicie ligações a este sistema de sites** nas propriedades do sistema de sites após instalação do sistema de sites, o sistema de sites não iniciar a comunicação com o servidor do site. Em vez disso, o servidor do site inicia a comunicação e utiliza a conta de instalação do sistema de sites para autenticação para o servidor de sistema de sites.  

#### <a name="bkmk_note6"></a> Tenha em atenção 6: Portas dinâmicas
As portas dinâmicas utilizam um intervalo de números de porta que são definidos pela versão do SO. Estas portas são também conhecidas como portas efêmeras. Para mais informações sobre os intervalos de portas predefinidos, consulte [Descrição geral do serviço e requisitos de portas de rede para o Windows](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows).  



##  <a name="BKMK_AdditionalPorts"></a> Listas de portas adicionais  

 As secções seguintes fornecem informações adicionais sobre as portas que são utilizadas pelo Configuration Manager.  

###  <a name="BKMK_ClientShares"></a> Partilhas de cliente para servidor  

 Os clientes utilizam o Bloco de Mensagens de Servidor (SMB) sempre que ligam a partilhas UNC. Por exemplo:  

-   Instalação de cliente manual que especifica o CCMSetup.exe **/Source:** propriedade da linha de comandos  

-   Clientes do Endpoint Protection que transferir ficheiros de definição a partir de um caminho UNC

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  


###  <a name="BKMK_SQLPorts"></a> Ligações ao Microsoft SQL Server  

 Para comunicação com o motor de base de dados do SQL Server e para replicação entre sites, pode utilizar a porta predefinida do SQL Server ou especificar portas personalizadas:  

-   As comunicações entre sites utilizam:  

    -   SQL Server Service Broker, que utiliza por predefinição a porta TCP 4022.  

    -   Serviço do SQL Server, que utiliza por predefinição a porta TCP 1433.  

-   Comunicação entre sites entre o motor de base de dados do SQL Server e várias funções de sistema de sites do Configuration Manager por predefinição a porta TCP 1433.  

- O Configuration Manager utiliza as mesmas portas e protocolos para comunicar com cada réplica de grupo de disponibilidade SQL que aloja a base de dados, como se a réplica foi uma instância do SQL Server autónomo.

Quando utiliza o Azure e a base de dados do site estiver atrás de um balanceador de carga interno ou externo, configure os seguintes componentes:
- Exceções de firewall em cada réplica
- Regras de balanceamento de carga 

Configure as seguintes portas:
 - SQL sobre TCP: TCP 1433
 - SQL Server Service Broker: TCP 4022
 - Server Message Block (SMB): TCP 445
 - Mapeador de pontos finais RPC: TCP 135

> [!WARNING]  
>  O Configuration Manager não suporta portas dinâmicas. Por predefinição, o SQL Server denominada instâncias utilizam portas dinâmicas para ligações ao motor da base de dados. Quando utilizar uma instância nomeada, configure manualmente a porta estática para comunicação entre sites.  

 As seguintes funções do sistema de sites comunicam diretamente com a base de dados do SQL Server:  

-   Ponto de serviço Web do Catálogo de Aplicações  

-   Função de ponto de registo de certificados  

-   Função de ponto de registo  

-   Ponto de gestão  

-   Servidor do site  

-   Ponto do Reporting Services  

-   Fornecedor de SMS  

-   SQL Server--> SQL Server  

Quando um SQL Server aloja bases de dados de mais de um site, cada base de dados tem de utilizar uma instância separada do SQL Server. Configure cada instância com um conjunto exclusivo de portas.  

Se habilitar uma firewall baseada no anfitrião no SQL server, configurá-la para permitir que as portas corretas. Também configure firewalls de rede entre computadores que comunicam com o SQL server.  

Para obter um exemplo de como configurar o SQL Server para utilizar uma porta específica, consulte [configurar um servidor para escutar numa porta TCP específica](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port).  


### <a name="bkmk_discovery"> </a> Deteção e a publicação

O Configuration Manager utiliza as seguintes portas para a deteção e a publicação de informações do site:
 - Lightweight Directory Access Protocol (LDAP): 389
 - LDAP de catálogo global: 3268
 - Mapeador de pontos finais RPC: 135
 - RPC: Atribuído dinamicamente portas TCP elevada
 - TCP: 1024: 5000
 - TCP:  49152: 65535


###  <a name="BKMK_External"></a> Ligações externas efetuadas pelo Configuration Manager  

Clientes do Configuration Manager no local ou sistemas de sites, podem efetuar as seguintes ligações externas:  

-   [Ponto de sincronização do Asset Intelligence-- &gt; Microsoft](#BKMK_PortsAI)  

-   [Ponto do Endpoint Protection-- &gt; Internet](#BKMK_PortsEndpointProtection_Internet)  

-   [Cliente-- &gt; controlador de domínio de Catálogo Global](#BKMK_PortsClient-GCDC)  

-   [Consola do Configuration Manager-- &gt; Internet](#BKMK_PortsConsole-Internet)  

-   [Ponto de gestão-- &gt; controlador de domínio](#BKMK_PortsMP-DC)  

-   [Servidor do site-- &gt; controlador de domínio](#BKMK_PortsSite-DC)  

-   [Servidor do site &lt;  --  &gt; autoridade de certificação emissora (AC)](#BKMK_PortsIssuingCA_SiteServer)  

-   [Ponto de atualização de software-- &gt; Internet](#BKMK_PortsSUP-Internet)  

-   [Ponto de atualização de software-- &gt; servidor WSUS a montante](#BKMK_PortsSUP-WSUS)  

-   [Ponto de ligação – serviço &gt; Microsoft Intune](#BKMK_PortsIntuneConnector-WindowsIntune)  

- [Serviço de ponto de ligação-- > Azure](#bkmk_scp-cmg)  

- [Ponto de ligação do CMG-- > serviço cloud do CMG](#bkmk_cmgcp-cmg)  


###  <a name="BKMK_IBCMports"></a> Requisitos de instalação para sistemas de sites que suportam clientes baseados na internet  

 > [!Note]  
 > Esta secção aplica-se apenas a gestão de clientes baseados na internet (IBCM). Não se aplica para o gateway de gestão na cloud. Para obter mais informações, consulte [gerir clientes na internet](/sccm/core/clients/manage/manage-clients-internet).  

 Pontos de gestão baseado na Internet e pontos de distribuição que suportam clientes baseados na internet, o ponto de atualização de software e o ponto de estado de contingência utilizam as seguintes portas para instalação e reparação:  

-   Servidor do site--> sistema de sites: Mapeador de ponto de extremidade RPC utilizando a porta UDP e TCP 135.  

-   Servidor do site--> sistema de sites: Portas TCP dinâmicas de RPC  

-   Servidor do site &lt; --> sistema de sites: Blocos de mensagens de servidor (SMB) através de TCP da porta 445

As instalações de aplicações e pacotes em pontos de distribuição exigem as seguintes portas RPC:  

-   Servidor do site--> ponto de distribuição: Mapeador de ponto de extremidade RPC utilizando a porta UDP e TCP 135

-   Servidor do site--> ponto de distribuição: Portas TCP dinâmicas de RPC  

Utilize o IPsec para ajudar a proteger o tráfego entre o servidor do site e os sistemas de sites. Se for preciso restringir as portas dinâmicas utilizadas com RPC, pode utilizar a ferramenta de configuração Microsoft RPC (rpccfg.exe) para configurar um intervalo limitado de portas para estes pacotes RPC. Para obter mais informações sobre a ferramenta de configuração RPC, consulte [Como configurar o RPC para utilizar determinadas portas e como ajudar a proteger essas portas utilizando o IPsec](https://support.microsoft.com/help/908472/how-to-configure-rpc-to-use-certain-ports-and-how-to-help-secure-those).  

> [!IMPORTANT]  
>  Antes de instalar estes sistemas de sites, certifique-se de que o serviço registo remoto está em execução no servidor do sistema de site e especificou uma conta de instalação do sistema de sites se o sistema de sites estiver numa floresta do Active Directory diferente sem uma relação de confiança .  


###  <a name="BKMK_PortsClientInstall"></a> Portas utilizadas pela instalação do cliente do Configuration Manager  

As portas utilizadas pelo Configuration Manager durante a instalação de cliente depende do método de implantação. 

- Para obter uma lista de portas para cada método de implementação do cliente, consulte [portas utilizadas durante a implementação de cliente do Configuration Manager](/sccm/core/clients/deploy/windows-firewall-and-port-settings-for-clients#ports-used-during-configuration-manager-client-deployment)  

- Para obter mais informações sobre como configurar a Firewall do Windows no cliente para a instalação de cliente e comunicação pós-instalação, consulte [Firewall do Windows e definições de porta para clientes](/sccm/core/clients/deploy/windows-firewall-and-port-settings-for-clients)  


###  <a name="BKMK_MigrationPorts"></a> Portas utilizadas pela migração  

O servidor do site que executa a migração utiliza várias portas para ligar a sites aplicáveis na hierarquia de origem. Para obter mais informações, consulte [necessárias configurações para a migração](/sccm/core/migration/prerequisites-for-migration#BKMK_Required_Configurations).  


###  <a name="BKMK_ServerPorts"></a> Portas utilizadas pelo Windows Server  

 A tabela seguinte lista algumas das principais portas utilizadas pelo Windows Server. 

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|DNS|53|53|  
|DHCP|67 e 68|--|  
|Resolução de Nomes NetBIOS|137|--|  
|Serviço de Datagrama NetBIOS|138|--|  
|Serviço de Sessão NetBIOS|--|139|  
|Autenticação Kerberos|--|88|

Para obter mais informações, veja os artigos seguintes:
- [Descrição geral dos serviços e requisitos de portas para o sistema Windows Server de rede](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows).  

- [Como configurar uma firewall de domínios e confianças](https://support.microsoft.com/help/179442/how-to-configure-a-firewall-for-domains-and-trusts)
