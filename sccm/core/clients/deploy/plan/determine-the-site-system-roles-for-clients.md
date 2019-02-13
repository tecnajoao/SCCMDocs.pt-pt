---
title: Funções de sistema de sites para clientes
titleSuffix: Configuration Manager
description: Determine as funções de sistema de sites para clientes no System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 984e8d92-7327-4b08-9228-0c955e6ac778
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5a7df7b8c1ff14e8783b6f988f315a477cc7065c
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56122122"
---
# <a name="determine-the-site-system-roles-for-system-center-configuration-manager-clients"></a>Determinar as funções de sistema de sites para clientes do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este tópico pode ajudá-lo a determinar as funções de sistema de sites que precisa para implementar clientes do Configuration Manager:  

 Para obter mais informações sobre onde é necessária instalação funções de sistema de sites na hierarquia, consulte [estruturar uma hierarquia de sites para o System Center Configuration Manager](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md).  

 Para obter mais informações sobre como instalar e configurar as funções de sistema de sites que necessita, consulte [instalar funções do sistema de sites](../../../../core/servers/deploy/configure/install-site-system-roles.md).  

##  <a name="determine-if-you-need-a-management-point"></a>Determinar se necessita de um ponto de gestão  
 Por predefinição, todos os computadores de cliente do Windows utilizam um ponto de distribuição para instalar o cliente do Configuration Manager e podem reverter para um ponto de gestão quando um ponto de distribuição não estiver disponível. No entanto, poderá instalar clientes do Windows em computadores a partir de uma origem alternativa quando utiliza a propriedade da linha de comandos do CCMSetup **/Source: < caminho\>**. Por exemplo, pode fazê-lo se instalar clientes na Internet. Outro cenário é quando deseja evitar o envio de pacotes de rede entre o computador e o ponto de gestão durante a instalação de cliente, talvez porque um firewall bloquear as portas necessárias ou porque tem uma ligação de largura de banda baixa. No entanto, todos os clientes têm de comunicar com um ponto de gestão para atribuir a um site e para ser gerido pelo Configuration Manager.  

 Para obter mais informações sobre a propriedade da linha de comandos do CCMSetup **/Source: < caminho\>**, consulte [acerca das propriedades de instalação de cliente no System Center Configuration Manager](../../../../core/clients/deploy/about-client-installation-properties.md).  

 Quando instalar mais do que um ponto de gestão na hierarquia, os clientes ligam-se automaticamente para um ponto com base na respetiva localização de rede e de associação de floresta. Não é possível instalar mais do que um ponto de gestão num site secundário.  

 Os clientes de computador Mac e os clientes de dispositivos móveis que inscrever com o Configuration Manager sempre necessitam de um ponto de gestão para a instalação do cliente. Este ponto de gestão tem de ser um site primário, tem de ser configurado para suportar dispositivos móveis e aceita ligações de cliente a partir da Internet. Estes clientes não podem utilizar pontos de gestão em sites secundários nem ligar a pontos de gestão de outros sites primários.  

##  <a name="determine-if-you-need-a-fallback-status-point"></a>Determinar se necessita de um ponto de estado de contingência  
 Pode utilizar um ponto de estado de contingência para monitorizar a implementação do cliente para computadores Windows. Também pode identificar os clientes de computador do Windows que não são geridos porque não conseguem comunicar com um ponto de gestão. Computadores Mac, dispositivos móveis inscritos pelo Configuration Manager e dispositivos móveis que são geridos utilizando o conector do Exchange Server não utilizam um ponto de estado de contingência.  

 Um ponto de estado de contingência não é necessário para monitorizar a atividade do cliente e o estado de funcionamento do cliente.  

 O ponto de estado de contingência comunica sempre com os clientes por HTTP, que utiliza ligações não autenticadas e envia os dados em texto não encriptado. Isso torna o ponto de estado de contingência vulnerável a ataques, especialmente quando é utilizado com gestão de clientes baseados na Internet. Para ajudar a reduzir a superfície de ataque, dedique sempre um servidor a executar o ponto de estado de contingência e não instale outras funções de sistema de sites no mesmo servidor num ambiente de produção.  

 Instale um ponto de estado de contingência se todas as seguintes condições:  

- Quer erros de comunicação de cliente de computadores Windows sejam enviados para o site, mesmo que estes computadores cliente não consegue comunicar com um ponto de gestão.  

- Que pretende utilizar os relatórios de implementação de cliente do Configuration Manager, que apresentam os dados que são enviados pelo ponto de estado de contingência.  

- Tiver um servidor dedicado para esta função de sistema de sites e tiver medidas de segurança adicionais para ajudar a proteger o servidor contra ataques.  

- As vantagens de utilizar um ponto de estado de contingência compensam os eventuais riscos de segurança associados a ligações não autenticadas e texto não encriptado sobre tráfego HTTP as transferências.  

  Não instale um ponto de estado de contingência se os riscos de segurança da execução de um Web site com ligações de não autenticadas e transferências em texto não encriptado suplantam as vantagens da identificação de problemas de comunicação de cliente.  

##  <a name="determine-whether-you-need-a-reporting-services-point"></a>Determinar se necessita de um relatório dos serviços de ponto  
 O Configuration Manager fornece muitos relatórios para ajudar a monitorizar a instalação, atribuição e gestão de clientes na consola do Configuration Manager. Alguns dos relatórios de implementação de cliente requerem que os clientes são atribuídos a um ponto de estado de contingência.  

 Embora os relatórios não são necessários para implementar clientes e pode ver algumas informações de implementação na consola do Configuration Manager ou utilizar os ficheiros de registo de cliente para obter informações detalhadas, os relatórios de cliente fornecem informações valiosas para ajudar a monitorizar e resolver problemas de implementação do cliente.  

##  <a name="determine-if-you-need-an-enrollment-point-and-an-enrollment-proxy-point"></a>Determinar se necessita de um ponto de registo e um ponto de proxy de registo  
 O Configuration Manager requer que o ponto de inscrição e o proxy de inscrição ponto para inscrever dispositivos móveis e para inscrever certificados para computadores Mac. Estas funções de sistema de sites não são necessárias se gerir os dispositivos móveis utilizando o conector do Exchange Server, ou se instalar o cliente legado de dispositivo móvel (por exemplo, para Windows CE) ou se solicitar e instalar o certificado de cliente em computadores Mac independentemente do Configuration Manager.  

##  <a name="determine-if-you-need-a-distribution-point"></a>Determinar se necessita de um ponto de distribuição  
 Não é necessário um ponto de distribuição para instalar clientes do Configuration Manager em computadores Windows. No entanto, por predefinição, o Configuration Manager utiliza um ponto de distribuição para instalar os ficheiros de origem do cliente em computadores Windows, mas pode reverter para a transferência desses ficheiros a partir de um ponto de gestão. Pontos de distribuição não são utilizados para instalar clientes de dispositivos móveis inscritos pelo Configuration Manager, mas são utilizados se instalar o cliente legacy de dispositivo móvel. Se instalar o cliente do Configuration Manager como parte da implementação do sistema operativo, a imagem do sistema operativo é armazenada e obtida de um ponto de distribuição.  

 Embora não poderá ter pontos de distribuição para instalar a maioria dos clientes do Configuration Manager, precisará-los para instalar o software como aplicações e atualizações de software nos clientes.  

##  <a name="determine-if-you-need-an-application-catalog-website-point-and-an-application-catalog-web-services-point"></a>Determinar se necessita de um ponto de Web site do catálogo de aplicações e um ponto de serviços Web do catálogo de aplicações  
 O ponto de Web site do catálogo de aplicações e o ponto de serviço Web do catálogo de aplicações não são necessários para a implementação do cliente. No entanto, talvez queira instalá-los como parte do seu processo de implementação do cliente, para que os utilizadores podem efetuar as seguintes ações assim que o cliente do Configuration Manager está instalado em computadores Windows:  

-   Apagar os seus dispositivos móveis.  

-   Procurar e instalar aplicações a partir do catálogo de aplicações.  

-   Implementar aplicações em utilizadores e dispositivos com o objetivo de implementação **disponível**.  

##  <a name="determine-whether-you-require-a-cloud-management-gateway-connector-point"></a>Determinar se necessita de um ponto do conector de Gateway de gestão na Cloud 

Tem um ponto de conector do gateway de gestão na cloud, se estiver a configurar uma [gateway de gestão na cloud](/sccm/core/clients/manage/setup-cloud-management-gateway) ao [gerir clientes na Internet](/sccm/core/clients/manage/manage-clients-internet).


 
