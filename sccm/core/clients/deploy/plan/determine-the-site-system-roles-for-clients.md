---
title: "Funções de sistema de sites para clientes | Microsoft Docs"
description: "Determine as funções do sistema de sites para clientes no System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 984e8d92-7327-4b08-9228-0c955e6ac778
caps.latest.revision: "9"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 9f2dda834f23b2ee85c4c301c7e1b6a3a54ebc97
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="determine-the-site-system-roles-for-system-center-configuration-manager-clients"></a>Determinar as funções de sistema de sites para clientes do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este tópico pode ajudá-lo a determinar as funções de sistema de sites que tem de implementar clientes do Configuration Manager:  

 Para obter mais informações sobre onde instalar necessário funções de sistema de sites na hierarquia, consulte [estruturar uma hierarquia de sites para o System Center Configuration Manager](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md).  

 Para mais informações sobre como instalar e configurar as funções de sistema de sites que precisa, consulte [instalar funções do sistema de sites](../../../../core/servers/deploy/configure/install-site-system-roles.md).  

##  <a name="determine-if-you-need-a-management-point"></a>Determinar se necessita de um ponto de gestão  
 Por predefinição, todos os computadores de cliente do Windows utilizam um ponto de distribuição para instalar o cliente do Configuration Manager e podem reverter para um ponto de gestão quando não está disponível um ponto de distribuição. No entanto, pode instalar clientes Windows em computadores a partir de uma origem alternativa ao utilizar a propriedade da linha de comandos CCMSetup **/Source: < caminho\>**. Por exemplo, pode fazê-se instalar clientes na Internet. Outro cenário é quando pretender evitar o envio de pacotes de rede entre o computador e o ponto de gestão durante a instalação de cliente, talvez porque uma firewall bloquear as portas necessárias ou porque tem uma ligação de largura de banda baixa. No entanto, todos os clientes têm de comunicar com um ponto de gestão para atribuir a um site e para serem geridos pelo Configuration Manager.  

 Para obter mais informações sobre a propriedade da linha de comandos CCMSetup **/Source: < caminho\>**, consulte [acerca das propriedades de instalação de cliente no System Center Configuration Manager](../../../../core/clients/deploy/about-client-installation-properties.md).  

 Quando instalar mais do que um ponto de gestão na hierarquia, os clientes ligam-se automaticamente a um ponto com base na respetiva localização de rede e associação de floresta. Não é possível instalar mais do que um ponto de gestão num site secundário.  

 Os clientes de computador Mac e os clientes de dispositivos móveis que inscrever com o Configuration Manager sempre necessitam de um ponto de gestão para a instalação do cliente. Este ponto de gestão tem de ser um site primário, tem de ser configurado para suportar dispositivos móveis e tem de aceitar ligações de cliente a partir da Internet. Estes clientes não é possível utilizar pontos de gestão em sites secundários ou ligar a pontos de gestão em outros sites primários.  

##  <a name="determine-if-you-need-a-fallback-status-point"></a>Determinar se necessita de um ponto de estado de contingência  
 Pode utilizar um ponto de estado de contingência para monitorizar a implementação do cliente para computadores Windows. Também pode identificar os clientes de computador do Windows que são geridos porque não conseguem comunicar com um ponto de gestão. Computadores Mac, dispositivos móveis que são inscritos pelo Configuration Manager e dispositivos móveis que são geridos utilizando o conector do Exchange Server não utilizar um ponto de estado de contingência.  

 Um ponto de estado de contingência não é necessário para monitorizar a atividade do cliente e o estado de funcionamento do cliente.  

 O ponto de estado de contingência comunica sempre com os clientes através de HTTP, que utiliza ligações não autenticadas e envia os dados em texto não encriptado. Isto faz com que o ponto de estado de contingência vulnerável a ataques, especialmente quando é utilizado com gestão de clientes baseados na Internet. Para ajudar a reduzir a superfície de ataque, dedique sempre um servidor a executar o ponto de estado de contingência e não instalar outras funções de sistema de sites no mesmo servidor num ambiente de produção.  

 Instale um ponto de estado de contingência se todas as seguintes condições:  

-   Pretende erros de comunicação de cliente de computadores Windows sejam enviados para o site, mesmo que estes computadores cliente não consegue comunicar com um ponto de gestão.  

-   Pretende utilizar os relatórios de implementação de cliente do Configuration Manager, que apresentam os dados que são enviados pelo ponto de estado de contingência.  

-   Tiver um servidor dedicado para esta função de sistema de sites e tiver medidas de segurança adicionais para ajudar a proteger o servidor contra ataques.  

-   As vantagens de utilizar um ponto de estado de contingência prevalecem sobre eventuais riscos de segurança associados a ligações não autenticadas e desmarque o texto transferências sobre tráfego HTTP.  

 Não instale um ponto de estado de contingência se os riscos de segurança da execução de um Web site com ligações não autenticadas e transferências de texto não encriptado suplantam as vantagens da identificação de problemas de comunicação de cliente.  

##  <a name="determine-whether-you-need-a-reporting-services-point"></a>Determinar se necessita de um relatório de ponto do  
 Configuration Manager fornece muitos relatórios para ajudar a monitorizar a instalação, atribuição e gestão de clientes na consola do Configuration Manager. Alguns dos relatórios de implementação de cliente necessitam que os clientes são atribuídos a um ponto de estado de contingência.  

 Embora os relatórios não são necessários para implementar clientes e pode consultar algumas informações de implementação na consola do Configuration Manager ou utilizar os ficheiros de registo de cliente para obter informações detalhadas, os relatórios dos clientes fornecem informações valiosas para ajudar a monitorizar e resolver problemas de implementação do cliente.  

##  <a name="determine-if-you-need-an-enrollment-point-and-an-enrollment-proxy-point"></a>Determinar se necessita de um ponto de registo e um ponto de proxy de inscrição  
 O Configuration Manager requer que o ponto de inscrição e o proxy de inscrição ponto para inscrever dispositivos móveis e para inscrever certificados para computadores Mac. Estas funções de sistema de sites não são necessárias se gerir dispositivos móveis utilizando o conector do Exchange Server, se instalar o cliente legado de dispositivos móveis (por exemplo, para o Windows CE) ou se solicitar e instalar o certificado de cliente em computadores Mac independentemente do Configuration Manager.  

##  <a name="determine-if-you-need-a-distribution-point"></a>Determinar se necessita de um ponto de distribuição  
 Não precisa de um ponto de distribuição para instalar clientes do Configuration Manager em computadores Windows. No entanto, por predefinição, o Configuration Manager utiliza um ponto de distribuição para instalar os ficheiros de origem do cliente em computadores Windows, mas pode reverter para a transferência desses ficheiros a partir de um ponto de gestão. Pontos de distribuição não são utilizados para instalar clientes de dispositivos móveis inscritos pelo Configuration Manager, mas serão utilizados se instalar o cliente legado de dispositivos móveis. Se instalar o cliente do Configuration Manager como parte da implementação do sistema operativo, a imagem do sistema operativo é armazenada e obtida de um ponto de distribuição.  

 Apesar de não poderá precisar de pontos de distribuição para instalar a maioria dos clientes do Configuration Manager, vai precisar deles para instalar software como aplicações e atualizações de software nos clientes.  

##  <a name="determine-if-you-need-an-application-catalog-website-point-and-an-application-catalog-web-services-point"></a>Determinar se necessita de um ponto de Web site do catálogo de aplicações e um ponto de serviços Web do catálogo de aplicações  
 O ponto de Web site do catálogo de aplicações e o ponto de serviço Web do catálogo de aplicações não são necessários para a implementação do cliente. No entanto, pode querer instalá-los como parte do processo de implementação de cliente, para que os utilizadores podem realizar as seguintes ações assim que o cliente do Configuration Manager está instalado em computadores Windows:  

-   Apagar os seus dispositivos móveis.  

-   Procurar e instalar aplicações a partir do catálogo de aplicações.  

-   Implementar aplicações em utilizadores e dispositivos com um objetivo de implementação **disponível**.  

##  <a name="determine-whether-you-require-a-cloud-management-gateway-connector-point"></a>Determinar se necessita de um ponto do conector do Gateway de gestão de nuvem 

Precisa de um ponto de conector do gateway de gestão na nuvem se estiver a configurar um [gateway de gestão de nuvem](/sccm/core/clients/manage/setup-cloud-management-gateway) para [gerir clientes na Internet](/sccm/core/clients/manage/manage-clients-internet).


 