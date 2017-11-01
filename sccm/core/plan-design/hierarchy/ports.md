---
title: "Portas utilizadas para ligações"
titleSuffix: Configuration Manager
description: "Saiba mais sobre as portas necessárias e personalizáveis, que utiliza o System Center Configuration Manager para ligações."
ms.custom: na
ms.date: 09/19/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c6777fb0-0754-4abf-8a1b-7639d23e9391
caps.latest.revision: "8"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 663c64926e4653da3f7ee580ff01abb39cb85bee
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="ports-used-in-system-center-configuration-manager"></a>Portas utilizadas no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager é um sistema cliente/servidor distribuído. A natureza distribuída do Configuration Manager, significa que podem estabelecer ligações entre servidores de sites, sistemas de sites e clientes. Algumas ligações utilizam portas que não são configuráveis e outras suportam portas personalizadas que especificar. Tem de verificar que as portas necessárias estão disponíveis se utilizar qualquer porta de filtragem de tecnologia, tais como firewalls, routers, servidores proxy ou IPsec.  
    
> [!NOTE]  
>  Se suportar clientes baseados na Internet utilizando o protocolo de bridge SSL, para além dos requisitos de porta, também terá de permitir que alguns verbos e cabeçalhos HTTP para atravessem a firewall.   

 As listagens de porta que se seguem são utilizadas pelo Configuration Manager e não incluem informações relativas a serviços padrão do Windows, tais como definições de política de grupo para serviços de domínio do Active Directory ou a autenticação Kerberos. Para informações sobre serviços e portas do Windows Server, consulte [Descrição geral dos serviços e requisitos de portas de rede para o sistema do Windows Server](http://go.microsoft.com/fwlink/p/?LinkID=123652).  

##  <a name="BKMK_ConfigurablePorts"></a> Portas que pode configurar  
 O Configuration Manager permite-lhe configurar as portas para os seguintes tipos de comunicação:  

-   Ponto de Web site do catálogo de aplicações para o ponto de serviço web do catálogo de aplicações  

-   Ponto proxy de registo com o ponto de registo  

-   Sistemas de site de cliente que executam o IIS  

-   Cliente com a Internet (como definições do servidor proxy)  

-   Ponto de atualização de software com a Internet (como definições do servidor proxy)  

-   Ponto de atualização de software com o servidor WSUS  

-   Servidor do site com o servidor da base de dados do site  

-   Pontos do Reporting Services  

    > [!NOTE]  
    >  As portas que estão em utilização para a função de sistema de sites de ponto do Reporting Services serviços estão configuradas no SQL Server Reporting Services. Estas portas são depois utilizadas pelo Configuration Manager durante as comunicações com o ponto do Reporting Services. Lembre-se de que reveja estas portas que definem as informações de filtro IP para políticas IPsec ou para configurar firewalls.  

Por predefinição, a porta HTTP que é utilizada para comunicação do sistema de site de cliente é a porta 80 e a porta HTTPS predefinida é 443. Portas para comunicação do sistema de site de cliente por HTTP ou HTTPS podem ser alteradas durante a configuração ou nas propriedades do site para o seu site do Configuration Manager.  

As portas que estão em utilização para a função de sistema de sites de ponto do Reporting Services serviços estão configuradas no SQL Server Reporting Services. Estas portas são depois utilizadas pelo Configuration Manager durante as comunicações com o ponto do Reporting Services. Lembre-se de que reveja estas portas quando estiver a definir as informações de filtro IP para políticas IPsec ou para configurar firewalls.  

##  <a name="BKMK_NonConfigurablePorts"></a> Portas não configuráveis  
O Configuration Manager permite configurar portas para os seguintes tipos de comunicação:  

-   Site para site  

-   Servidor do site com o sistema de sites  

-   Consola do Configuration Manager para o fornecedor de SMS  

-   Consola do Configuration Manager para a Internet  

-   Ligações a serviços em nuvem, como o Microsoft Intune e pontos de distribuição baseado na nuvem  

##  <a name="BKMK_CommunicationPorts"></a> Portas utilizadas por clientes e sistemas de sites do Configuration Manager  
As secções seguintes pormenorizadamente as portas que são utilizadas para comunicação no Configuration Manager. As setas no título da secção representam a direção da comunicação:  

-   -> Indica que um computador inicia a comunicação e o outro computador responde sempre  

-   &lt;-> Indica que ambos os computadores podem iniciar comunicações  

###  <a name="BKMK_PortsAI"></a>Ponto de sincronização do Asset Intelligence-- > Microsoft  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTPS (Secure Hypertext Transfer Protocol)|--|443|  

###  <a name="BKMK_PortsAI-to-SQL"></a>Ponto de sincronização do Asset Intelligence-- > SQL Server  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 (ver nota 2, **alternativa porta disponível**)|  

###  <a name="BKMK_PortsAppCatalogService-SQL"></a>Ponto de serviço de web de catálogo de aplicações-- > SQL Server  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 (ver nota 2, **alternativa porta disponível**)|  

###  <a name="BKMK_PortsAppCatalogWebSitePoint_AppCatalogWebServicePoint"></a>Ponto de Web site do catálogo de aplicações-- > ponto de serviço web do catálogo de aplicações  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTP (Hypertext Transfer Protocol)|--|80 (ver nota 2, **alternativa porta disponível**)|  
|Protocolo HTTPS (Secure Hypertext Transfer Protocol)|--|443 (ver nota 2, **alternativa porta disponível**)|  

###  <a name="BKMK_PortsClient-AppCatalogWebsitePoint"></a>Cliente--> Ponto de Web site do catálogo de aplicações  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTP (Hypertext Transfer Protocol)|--|80 (ver nota 2, **alternativa porta disponível**)|  
|Protocolo HTTPS (Secure Hypertext Transfer Protocol)|--|443 (ver nota 2, **alternativa porta disponível**)|  

###  <a name="BKMK_PortsClient-ClientWakeUp"></a> Cliente -- &gt; Cliente  
 Além das portas que estão listadas na seguinte tabela, proxy de reativação também utiliza mensagens de pedido de eco do controlo mensagem ICMP (Internet Protocol) de um cliente a outro cliente quando são configurados para proxy de reativação.

Esta comunicação é utilizada para confirmar se o outro computador cliente está ativo na rede. Por vezes, o ICMP é também referido como comandos ping de TCP/IP. O ICMP não tem um número de protocolo UDP ou TCP e, por isso, não está listado na tabela a seguir. No entanto, as firewalls baseadas no anfitrião existentes nestes computadores cliente ou em dispositivos de rede intervenientes na sub-rede devem permitir o tráfego ICMP para que a comunicação de proxy de reativação tenha êxito.  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Reativação Por LAN|9 (ver nota 2, **alternativa porta disponível**)|--|  
|Proxy de reativação|25536 (ver nota 2, **alternativa porta disponível**)|--|  

###  <a name="BKMK_PortsClient-PolicyModule"></a> Cliente -- &gt; Módulo de Política do Configuration Manager (Serviço de Inscrição de Dispositivos de Rede)  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTP (Hypertext Transfer Protocol)||80|  
|Protocolo HTTPS (Secure Hypertext Transfer Protocol)|--|443|  

###  <a name="BKMK_PortsClient-CloudDP"></a>Cliente--> Ponto de distribuição baseados na nuvem  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTPS (Secure Hypertext Transfer Protocol)|--|443|  

###  <a name="BKMK_PortsClient-DP"></a>Cliente--> Ponto de distribuição  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTP (Hypertext Transfer Protocol)|--|80 (ver nota 2, **alternativa porta disponível**)|  
|Protocolo HTTPS (Secure Hypertext Transfer Protocol)|--|443 (ver nota 2, **alternativa porta disponível**)|  

###  <a name="BKMK_PortsClient-DP2"></a>Cliente--> Ponto de distribuição configurado para multicast  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Protocolo multicast|63000-64000|--|  

###  <a name="BKMK_PortsClient-DP3"></a>Cliente--> Ponto de distribuição configurado para PXE  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo DHCP (Dynamic Host Configuration Protocol)|67 e 68|--|  
|Protocolo TFTP (Trivial File Transfer Protocol)|69 (ver nota 4, **Daemon Trivial FTP (TFTP)**)|--|  
|Boot Information Negotiation Layer (BINL)|4011|--|  

###  <a name="BKMK_PortsClient-FSP"></a>Cliente--> Ponto de estado de contingência  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTP (Hypertext Transfer Protocol)|--|80 (ver nota 2, **alternativa porta disponível**)|  

###  <a name="BKMK_PortsClient-GCDC"></a>Cliente--> Controlador de domínio de Catálogo Global  
 Um cliente do Configuration Manager não contacta um servidor de catálogo global quando é um computador de grupo de trabalho ou quando está configurado para comunicação apenas através da Internet.  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|LDAP de catálogo global|--|3268|  


###  <a name="BKMK_PortsClient-MP"></a>Cliente--> Ponto de gestão  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Notificação de cliente (comunicação predefinida antes de reverter para HTTP ou HTTPS)|--|10123 (ver nota 2, **alternativa porta disponível**)|  
|Protocolo HTTP (Hypertext Transfer Protocol)|--|80 (ver nota 2, **alternativa porta disponível**)|  
|Protocolo HTTPS (Secure Hypertext Transfer Protocol)|--|443 (ver nota 2, **alternativa porta disponível**)|  

###  <a name="BKMK_PortsClient-SUP"></a>Cliente--> Ponto de atualização de Software  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTP (Hypertext Transfer Protocol)|--|80 ou 8530 (Ver nota 3, **Windows Server Update Services**)|  
|Protocolo HTTPS (Secure Hypertext Transfer Protocol)|--|443 ou 8531 (Ver nota 3, **Windows Server Update Services**)|  

###  <a name="BKMK_PortsClient-SMP"></a>Cliente--> Ponto de migração de estado  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTP (Hypertext Transfer Protocol)|--|80 (ver nota 2, **alternativa porta disponível**)|  
|Protocolo HTTPS (Secure Hypertext Transfer Protocol)|--|443 (ver nota 2, **alternativa porta disponível**)|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  

###  <a name="BKMK_PortsConsole-Client"></a>Consola do Configuration Manager-- > cliente  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Controlo Remoto (controlo)|--|2701|  
|Assistência Remota (RDP e RTC)|--|3389|  

###  <a name="BKMK_PortsConsole-Internet"></a>Consola do Configuration Manager-- > Internet  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTP (Hypertext Transfer Protocol)|--|80|  

###  <a name="BKMK_PortsConsole-RSP"></a>Consola do Configuration Manager-- > ponto do Reporting Services  


|Descrição|UDP|TCP|
|-----------------|---------|---------|   
|Protocolo HTTP (Hypertext Transfer Protocol)|--|80 (ver nota 2, **alternativa porta disponível**)|  
|Protocolo HTTPS (Secure Hypertext Transfer Protocol)|--|443 (ver nota 2, **alternativa porta disponível**)|  

###  <a name="BKMK_PortsConsole-Site"></a>Consola do Configuration Manager-- > servidor do Site  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|RPC (ligação inicial ao WMI para localizar o sistema do fornecedor)|--|135|  

###  <a name="BKMK_PortsConsole-Provider"></a>Consola do Configuration Manager-- > fornecedor de SMS  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|DINÂMICAS (Ver nota 6, **Portas dinâmicas**)|  

###  <a name="BKMK_PortsCertificateRegistationPoint_PolicyModule"></a>Módulo de política do Configuration Manager (serviço dispositivos de rede inscrição) - > Ponto de registo de certificados  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTPS (Secure Hypertext Transfer Protocol)|--|443 (ver nota 2, **alternativa porta disponível**)|  

###  <a name="BKMK_PortsDist_MP"></a>Ponto de distribuição-- > ponto de gestão  
 Um ponto de distribuição comunica com o ponto de gestão nos seguintes cenários:  

-   Para comunicar o estado do conteúdo pré-configurado  

-   Para reportar dados de resumo de utilização  

-   Para reportar validação de conteúdo  

-   Para comunicar o estado de transferências do pacote (ponto de distribuição de solicitação)

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTP (Hypertext Transfer Protocol)|--|80 (ver nota 2, **alternativa porta disponível**)|  
|Protocolo HTTPS (Secure Hypertext Transfer Protocol)|--|443 (ver nota 2, **alternativa porta disponível**)|  

###  <a name="BKMK_PortsEndpointProtection_Internet"></a>Ponto do Endpoint Protection-- > Internet  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTP (Hypertext Transfer Protocol)|--|80|  

###  <a name="BKMK_PortsEP-to-SQL"></a>Ponto do Endpoint Protection-- > SQL Server  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 (ver nota 2, **alternativa porta disponível**)|  

###  <a name="BKMK_PortsEnrollmentProxyEnrollmentPoint"></a>Ponto de proxy de registo-- > ponto de registo  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTPS (Secure Hypertext Transfer Protocol)|--|443 (ver nota 2, **alternativa porta disponível**)|  

###  <a name="BKMK_PortsEnrollmentEnrollmentSQL"></a>Ponto de registo-- > SQL Server  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 (ver nota 2, **alternativa porta disponível**)|  

###  <a name="BKMK_PortsExchangeConnectorHosted"></a> Conector do Exchange Server -- &gt; Exchange Online  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Gestão Remota do Windows através de HTTPS|--|5986|  

###  <a name="BKMK_PortsExchangeConnectorOnPrem"></a>Conector do Exchange Server - > Exchange Server no local  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Gestão Remota do Windows através de HTTP|--|5985|  

###  <a name="BKMK_PortsMacEnrollmentProxyPoint"></a>Computador Mac-- > ponto proxy de registo  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTPS (Secure Hypertext Transfer Protocol)|--|443|  

###  <a name="BKMK_PortsMP-DC"></a>Ponto de gestão-- > controlador de domínio  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|LDAP (Lightweight Directory Access Protocol)|--|389|  
|LDAP de catálogo global|--|3268|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|DINÂMICAS (Ver nota 6, **Portas dinâmicas**)|  

###  <a name="BKMK_PortsMP-Site"></a>Ponto de gestão &lt; -> servidor do Site  
 (Ver nota 5, **Comunicação entre o servidor do site e os sistemas de site**)  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Mapeador de Pontos Finais RPC|--|135|  
|RPC|--|DINÂMICAS (Ver nota 6, **Portas dinâmicas**)|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  

###  <a name="BKMK_PortsMP-SQL"></a>Ponto de gestão-- > SQL Server  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 (ver nota 2, **alternativa porta disponível**)|  

###  <a name="BKMK_PortsMobileDeviceClient-EnrollmentProxyPoint"></a>Dispositivo móvel-- > ponto proxy de registo  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTPS (Secure Hypertext Transfer Protocol)|--|443|  

###  <a name="BKMK_PortsMobileDeviceClient-WindowsIntune"></a>Dispositivo móvel-- > Microsoft Intune  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTPS (Secure Hypertext Transfer Protocol)|--|443|  

###  <a name="BKMK_PortsRSP-SQL"></a>Relatório de ponto de serviços-- > SQL Server  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 (ver nota 2, **alternativa porta disponível**)|  

###  <a name="BKMK_PortsIntuneConnector-WindowsIntune"></a>Serviço de ponto de ligação-- > Microsoft Intune  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTPS (Secure Hypertext Transfer Protocol)|--|443|
Para obter mais informações consulte [requisitos de acesso à Internet](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_urls) para o ponto de ligação de serviço.

###  <a name="BKMK_PortsAppCatalogWebServicePoint_SiteServer"></a>Servidor do site &lt; -> ponto de serviço web do catálogo de aplicações  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|DINÂMICAS (Ver nota 6, **Portas dinâmicas**)|  

###  <a name="BKMK_PortsAppCatalogWebSitePoint_SiteServer"></a>Servidor do site &lt; -> ponto de Web site do catálogo de aplicações  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|DINÂMICAS (Ver nota 6, **Portas dinâmicas**)|  

###  <a name="BKMK_PortsSite-AISP"></a>Servidor do site &lt; -> ponto de sincronização do Asset Intelligence  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|DINÂMICAS (Ver nota 6, **Portas dinâmicas**)|  

###  <a name="BKMK_PortsSite-Client"></a>Servidor do site-- > cliente  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Reativação Por LAN|9 (ver nota 2, **alternativa porta disponível**)|--|  

###  <a name="BKMK_PortsSiteServer-CloudDP"></a>Servidor do site-- > ponto de distribuição baseado na nuvem  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTPS (Secure Hypertext Transfer Protocol)|--|443|  

###  <a name="BKMK_PortsSite-DP"></a>Servidor do site-- > ponto de distribuição  
 (Ver nota 5, **Comunicação entre o servidor do site e os sistemas de site**)  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|DINÂMICAS (Ver nota 6, **Portas dinâmicas**)|  

###  <a name="BKMK_PortsSite-DC"></a>Servidor do site-- > controlador de domínio  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|LDAP (Lightweight Directory Access Protocol)|--|389|  
|LDAP de catálogo global|--|3268|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|DINÂMICAS (Ver nota 6, **Portas dinâmicas**)|  

###  <a name="BKMK_PortsCertificateRegistrationPoint_SiteServer"></a>Servidor do site &lt; -> ponto de registo de certificados  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|DINÂMICAS (Ver nota 6, **Portas dinâmicas**)|  

###  <a name="BKMK_PortsEndpointProtection_SiteServer"></a>Servidor do site &lt; -> ponto de Endpoint Protection  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|DINÂMICAS (Ver nota 6, **Portas dinâmicas**)|  

###  <a name="BKMK_EnrollmentPoint_SiteServer"></a>Servidor do site &lt; -> ponto de registo  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|DINÂMICAS (Ver nota 6, **Portas dinâmicas**)|  

###  <a name="BKMK_EnrollmentProxyPoint_SiteServer"></a>Servidor do site &lt; -> ponto proxy de registo  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|DINÂMICAS (Ver nota 6, **Portas dinâmicas**)|  

###  <a name="BKMK_PortsSite-FSP"></a>Servidor do site &lt; -> ponto de estado de contingência  
 (Ver nota 5, **Comunicação entre o servidor do site e os sistemas de site**)  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|DINÂMICAS (Ver nota 6, **Portas dinâmicas**)|  

###  <a name="BKMK_PortSite-Internet"></a>Servidor do site-- > Internet  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTP (Hypertext Transfer Protocol)|--|80 (ver nota 1, **porta do servidor Proxy**)|  

###  <a name="BKMK_PortsIssuingCA_SiteServer"></a>Servidor do site &lt; -> autoridade de certificação (AC) emissora  
 Esta comunicação é utilizada na implementação de perfis de certificado, utilizando o ponto de registo de certificados. A comunicação não é utilizada para cada servidor do site na hierarquia. Em vez disso, é utilizado apenas para o servidor do site na parte superior da hierarquia.  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC (DCOM)|--|DINÂMICAS (Ver nota 6, **Portas dinâmicas**)|  

###  <a name="BKMK_PortsSite-RSP"></a>Servidor do site &lt; -> ponto do Reporting Services  
 (Ver nota 5, **Comunicação entre o servidor do site e os sistemas de site**)  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|DINÂMICAS (Ver nota 6, **Portas dinâmicas**)|  

###  <a name="BKMK_PortsSite-Site"></a>Servidor do site &lt; -> servidor do Site  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  

###  <a name="BKMK_PortsSite-SQL"></a>Servidor do site-- > SQL Server  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 (ver nota 2, **alternativa porta disponível**)|  

 Durante a instalação de um site que utiliza o SQL Server remoto para alojar a base de dados do site, tem de abrir as seguintes portas entre o servidor do site e o SQL Server:  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|DINÂMICAS (Ver nota 6, **Portas dinâmicas**)|  

###  <a name="BKMK_PortsSite-Provider"></a>Servidor do site-- > fornecedor de SMS  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Mapeador de Pontos Finais RPC|135|135|  
|RPC|--|DINÂMICAS (Ver nota 6, **Portas dinâmicas**)|  

###  <a name="BKMK_PortsSite-SUP"></a>Servidor do site &lt; -> ponto de atualização de Software  
 (Ver nota 5, **Comunicação entre o servidor do site e os sistemas de site**)  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Protocolo HTTP (Hypertext Transfer Protocol)|--|80 ou 8530 (Ver nota 3, **Windows Server Update Services**)|  
|Protocolo HTTPS (Secure Hypertext Transfer Protocol)|--|443 ou 8531 (Ver nota 3, **Windows Server Update Services**)|  

###  <a name="BKMK_PortsSite-SMP"></a>Servidor do site &lt; -> ponto de migração de estado  
 (Ver nota 5, **Comunicação entre o servidor do site e os sistemas de site**)  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  
|Mapeador de Pontos Finais RPC|135|135|  

###  <a name="BKMK_PortsProvider-SQL"></a> Fornecedor de SMS -- &gt; SQL Server  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 (ver nota 2, **alternativa porta disponível**)|  

###  <a name="BKMK_PortsSUP-Internet"></a>Ponto de atualização de software-- > Internet  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTP (Hypertext Transfer Protocol)|--|80 (ver nota 1, **porta do servidor Proxy**)|  

###  <a name="BKMK_PortsSUP-WSUS"></a>Ponto de atualização de software-- > servidor WSUS a montante  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Protocolo HTTP (Hypertext Transfer Protocol)|--|80 ou 8530 (Ver nota 3, **Windows Server Update Services**)|  
|Protocolo HTTPS (Secure Hypertext Transfer Protocol)|--|443 ou 8531 (Ver nota 3, **Windows Server Update Services**)|  

###  <a name="BKMK_PortsSQL-SQL"></a> SQL Server --&gt; SQL Server  
 A replicação de base de dados entre sites requer o SQL Server num site para comunicar diretamente com o SQL Server no respetivo site principal ou subordinado.  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Serviço do SQL Server|--|1433 (ver nota 2, **alternativa porta disponível**)|  
|SQL Server Service Broker|--|4022 (ver nota 2, **alternativa porta disponível**)|  

> [!TIP]  
>  O Configuration Manager não requer o SQL Server Browser, que utiliza a porta UDP 1434.  

###  <a name="BKMK_PortsStateMigrationPoint-to-SQL"></a>Estado do ponto de migração - > SQL Server  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sobre TCP|--|1433 (ver nota 2, **alternativa porta disponível**)|  



###  <a name="BKMY_PortNotes"></a> Notas relativas às portas utilizadas por clientes e sistemas de sites do Configuration Manager  

1.  **Porta do servidor proxy**: Esta porta não pode ser configurada, mas pode ser encaminhada através de um servidor proxy configurado.  

2.  **Alternate porta disponível**: Uma porta alternativa pode ser definida no Configuration Manager para este valor. Se tiver sido definida uma porta personalizada, substitua-a quando definir as informações de filtro IP para políticas IPsec ou para configurar firewalls.  

3.  **Windows Server Update Services (WSUS)**: WSUS pode ser instaladas para utilizar as portas 80/443 ou as portas 8530/8531 para comunicações de clientes. Quando executar o WSUS no Windows Server 2012 ou Windows Server 2016, o WSUS está configurado por predefinição para utilizar a porta 8530 para HTTP e a porta 8531 para HTTPS.  

     Após a instalação, a porta pode ser alterada. Não é necessário utilizar o mesmo número de porta ao longo da hierarquia do site.  

    -   Se a porta HTTP for 80, a porta HTTPS tem de ser 443.  

    -   Se a porta HTTP for qualquer outra, a porta HTTPS tem de ser 1 ou superior, por exemplo, 8530 e 8531.   

    > [!NOTE]  
    >  Quando configura o ponto de atualização de software para utilizar HTTPS, a porta HTTP também tem de estar aberta. Os dados não encriptados, como o EULA para atualizações específicas, utilizam a porta HTTP.  

4.  **Daemon trivial FTP (TFTP)**: O serviço de sistema do Daemon Trivial FTP (TFTP) não requer um nome de utilizador ou palavra-passe e é uma parte integral de serviços de implementação do Windows (WDS). O serviço do Trivial FTP Daemon implementa suporte para o protocolo TFTP definido pelos RFC seguintes:  

    -   RFC 350: TFTP  

    -   RFC 2347: Extensão de opção  

    -   RFC 2348: Opção de tamanho de bloco  

    -   RFC 2349: Opções de tamanho de intervalo e transferência do tempo limite  

     O Protocolo TFTP (Trivial File Transfer Protocol) foi concebido para suportar ambientes de arranque sem disco. Os Daemons TFTP escutam a porta UDP 69 mas respondem a partir de uma porta alta alocada dinamicamente. Por conseguinte, a ativação desta porta permite que o serviço TFTP receber pedidos de TFTP de entrada mas não permite que o servidor selecionado responda a esses pedidos. Não é possível ativar o servidor selecionado responda a pedidos TFTP de entrada, a menos que o servidor TFTP esteja configurado para responder na porta 69.  

5.  **Comunicação entre o servidor do site e sistemas de sites**: Por predefinição, a comunicação entre o servidor do site e sistemas de sites é bidirecional. O servidor do site inicia a comunicação para configurar o sistema de sites e, em seguida, a maioria dos sistemas de sites restabelece ligação ao servidor do site para enviar informações de estado. Os pontos do Reporting Services e os pontos de distribuição não enviam informações de estado. Se selecionar **exigir que o servidor do site inicie ligações a este sistema de sites** nas propriedades do sistema de sites após a instalação do sistema de sites, o sistema de sites não irá iniciar a comunicação com o servidor do site. Em vez disso, o servidor do site inicia a comunicação e utiliza a conta de instalação do sistema de sites para autenticação para o servidor de sistema de sites.  

6.  **Portas dinâmicas**: Portas dinâmicas (também conhecidas como portas efémeras) utilizam um intervalo de números de porta que são definidos pela versão do sistema operativo. Para mais informações sobre os intervalos de portas predefinidos, consulte [Descrição geral do serviço e requisitos de portas de rede para o Windows](http://go.microsoft.com/fwlink/p/?LinkId=317965).  

##  <a name="BKMK_AdditionalPorts"></a> Listas de portas adicionais  
 As secções seguintes fornecem informações adicionais sobre as portas que são utilizadas pelo Configuration Manager.  

###  <a name="BKMK_ClientShares"></a> Partilhas de cliente para servidor  
 Os clientes utilizam o Bloco de Mensagens de Servidor (SMB) sempre que ligam a partilhas UNC. Por exemplo:  

-   Instalação de cliente manual que especifica o CCMSetup.exe **/Source:** propriedade da linha de comandos  

-   Clientes do Endpoint Protection que transferem ficheiros de definição de um caminho UNC

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Bloco de Mensagem de Servidor (SMB)|--|445|  

###  <a name="BKMK_SQLPorts"></a> Ligações ao Microsoft SQL Server  
 Para comunicação com o motor de base de dados do SQL Server e para replicação entre sites, pode utilizar a porta predefinida do SQL Server ou especificar portas personalizadas:  

-   As comunicações entre sites utilizam:  

    -   SQL Server Service Broker, que utiliza por predefinição a porta TCP 4022.  

    -   Serviço do SQL Server, que utiliza por predefinição a porta TCP 1433.  

-   Comunicações intra-site entre o motor de base de dados do SQL Server e várias funções de sistema de site do Configuration Manager, será assumida a porta TCP 1433.  

- O Configuration Manager utiliza as mesmas portas e protocolos para comunicar com cada réplica de grupo de disponibilidade do SQL Server que aloja a base de dados do site, como se a réplica estava uma instância do SQL Server autónomo.

Quando utiliza o Azure e a base de dados do site estiver atrás de um interno ou o Balanceador de carga externo, configure as seguintes exceções de firewall em cada réplica e adicione regras para as seguintes portas de balanceamento de carga:
 - SQL sobre TCP: TCP 1433
 - SQL Server Service Broker: TCP 4022
 - Bloco de mensagem de servidor (SMB): TCP 445
 - Mapeador de pontos finais RPC: TCP 135

> [!WARNING]  
>  O Configuration Manager não suporta portas dinâmicas. Uma vez que, por predefinição, as instâncias nomeadas de SQL Server utilizam portas dinâmicas para ligações ao motor da base de dados, quando utilizar uma instância nomeada tem de configurar manualmente a porta estática que pretende utilizar para comunicação entre sites.  

 As seguintes funções do sistema de sites comunicam diretamente com a base de dados do SQL Server:  

-   Ponto de serviço Web do Catálogo de Aplicações  

-   Função de ponto de registo de certificados  

-   Função de ponto de registo  

-   Ponto de gestão  

-   Servidor do site  

-   Ponto do Reporting Services  

-   Fornecedor de SMS  

-   SQL Server--> SQL Server  

Quando um SQL Server aloja bases de dados de mais de um site, cada base de dados deve utilizar uma instância separada do SQL Server e cada instância deve ser configurada com um conjunto exclusivo de portas.  

Se tiver uma firewall ativada no computador do SQL Server, certifique-se de que está configurado para permitir que as portas utilizadas pela sua implementação. Também configure firewalls que estão em localizações adicionais na rede entre computadores que comunicam com o SQL Server para permitir estas portas do mesmas.  

Para obter um exemplo de como configurar o SQL Server para utilizar uma porta específica, consulte [como: Configurar um servidor para escutar numa porta TCP específica (SQL Server Configuration Manager)](http://go.microsoft.com/fwlink/p/?LinkID=226349) na Biblioteca TechNet do SQL Server.  


### <a name="bkmk_discovery"></a> Deteção e de publicação
As seguintes portas são utilizadas para a deteção e a publicação de informações do site:
 - Lightweight Directory Access Protocol (LDAP): 389
 - LDAP de catálogo global: 3268
 - Mapeador de pontos finais RPC: 135
 - RPC: Atribuído dinamicamente portas TCP elevada
 - TCP: 1024: 5000
 - TCP:  49152: 65535


###  <a name="BKMK_External"></a> Ligações externas efetuadas pelo Configuration Manager  
 Clientes do Configuration Manager ou sistemas de sites podem efetuar as seguintes ligações externas:  

-   [Ponto de sincronização do Asset Intelligence-- &gt; Microsoft](#BKMK_PortsAI)  

-   [Ponto do Endpoint Protection-- &gt; Internet](#BKMK_PortsEndpointProtection_Internet)  

-   [Cliente-- &gt; controlador de domínio de Catálogo Global](#BKMK_PortsClient-GCDC)  

-   [Consola do Configuration Manager-- &gt; Internet](#BKMK_PortsConsole-Internet)  

-   [Ponto de gestão-- &gt; controlador de domínio](#BKMK_PortsMP-DC)  

-   [Servidor do site-- &gt; controlador de domínio](#BKMK_PortsSite-DC)  

-   [Servidor do site &lt;  --  &gt; autoridade de certificação emissora (AC)](#BKMK_PortsIssuingCA_SiteServer)  

-   [Ponto de atualização de software-- &gt; Internet](#BKMK_PortsSUP-Internet)  

-   [Ponto de atualização de software-- &gt; servidor WSUS a montante](#BKMK_PortsSUP-WSUS)  

-   [Serviço de ponto de ligação – &gt; Microsoft Intune](#BKMK_PortsIntuneConnector-WindowsIntune)  

###  <a name="BKMK_IBCMports"></a> Requisitos de instalação para sistemas de sites que suportam clientes baseados na Internet  
 Pontos de gestão e pontos de distribuição que suportam clientes baseados na Internet, o ponto de atualização de software e o ponto de estado de contingência utilizam as seguintes portas para instalação e reparação:  

-   Servidor do site--> sistema de sites: Mapeador de ponto final RPC utilizando a porta UDP e TCP 135.  

-   Servidor do site--> sistema de sites: Portas TCP dinâmicas de RPC  

-   Servidor do site &lt; --> sistema de sites: Blocos de mensagens de servidor (SMB) através de TCP a porta 445

As instalações de aplicações e pacotes em pontos de distribuição exigem as seguintes portas RPC:  

-   Servidor do site--> ponto de distribuição: Mapeador de ponto final RPC utilizando a porta UDP e TCP 135

-   Servidor do site--> ponto de distribuição: Portas TCP dinâmicas de RPC  

Utilize o IPsec para ajudar a proteger o tráfego entre o servidor do site e os sistemas de sites. Se for preciso restringir as portas dinâmicas utilizadas com RPC, pode utilizar a ferramenta de configuração Microsoft RPC (rpccfg.exe) para configurar um intervalo limitado de portas para estes pacotes RPC. Para obter mais informações sobre a ferramenta de configuração RPC, consulte [Como configurar o RPC para utilizar determinadas portas e como ajudar a proteger essas portas utilizando o IPsec](http://go.microsoft.com/fwlink/p/?LinkId=124096).  

> [!IMPORTANT]  
>  Antes de instalar estes sistemas de sites, certifique-se de que o serviço registo remoto está em execução no servidor do sistema de site e que especificou uma conta de instalação do sistema de sites se o sistema de sites noutra floresta do Active Directory sem uma relação de fidedignidade.  

###  <a name="BKMK_PortsClientInstall"></a> Portas utilizadas pela instalação do cliente do Configuration Manager  
As portas utilizadas durante a instalação do cliente dependem do método de implementação do cliente. Para obter uma lista de portas para cada método de implementação do cliente, consulte **portas utilizadas durante a implementação de cliente do Configuration Manager** no [Firewall do Windows e definições de porta para clientes no System Center Configuration Manager](../../../core/clients/deploy/windows-firewall-and-port-settings-for-clients.md) tópico. Para obter informações sobre como configurar a Firewall do Windows no cliente para a instalação de cliente e comunicação pós-instalação, consulte [Firewall do Windows e definições de porta para clientes no System Center Configuration Manager](../../../core/clients/deploy/windows-firewall-and-port-settings-for-clients.md).  

###  <a name="BKMK_MigrationPorts"></a> Portas utilizadas pela migração  
O servidor do site que executa a migração utiliza várias portas para ligar a sites aplicáveis na hierarquia de origem para recolher dados de bases de dados sites de origem e para partilhar pontos de distribuição.  

 Para obter informações sobre estas portas, consulte o [configurações necessárias para a migração](../../../core/migration/prerequisites-for-migration.md#BKMK_Required_Configurations) secção o [pré-requisitos para migração no System Center Configuration Manager](../../../core/migration/prerequisites-for-migration.md) tópico.  

###  <a name="BKMK_ServerPorts"></a> Portas utilizadas pelo Windows Server  
 A tabela seguinte lista algumas das principais portas utilizadas pelo Windows Server, juntamente com as respetivas funções. Para obter uma lista mais completa dos serviços e dos requisitos de portas de rede do Windows Server, consulte [Descrição geral dos serviços e requisitos de portas de rede para o sistema do Windows Server](http://go.microsoft.com/fwlink/p/?LinkID=123652).  

|Descrição|UDP|TCP|  
|-----------------|---------|---------|  
|Sistema de Nomes de Domínio (DNS)|53|53|  
|Protocolo DHCP (Dynamic Host Configuration Protocol)|67 e 68|--|  
|Resolução de Nomes NetBIOS|137|--|  
|Serviço de Datagrama NetBIOS|138|--|  
|Serviço de Sessão NetBIOS|--|139|  
