---
title: "Configurar as portas de comunicação de cliente | Documentos do Microsoft"
description: "Definir portas de comunicação de cliente no System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 406bbdbf-ab4a-4121-a68b-154f96ea14ec
caps.latest.revision: 5
caps.handback.revision: 0
author: robstack
ms.author: robstackmsft
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 690d03d9c8c49a815bd318df549d7401a855bc5d
ms.openlocfilehash: 63e033fdb436930ac5f37e7408ca9292bc444560
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="how-to-configure-client-communication-ports-in-system-center-configuration-manager"></a>Como configurar as portas de comunicação de clientes no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode alterar os números de porta de pedido que os clientes do System Center Configuration Manager utilizam para comunicar com sistemas de sites que utilizem HTTP e HTTPS para comunicações. Embora HTTP ou HTTPS é mais provável que já esteja configurado para firewalls, a notificação do cliente que utiliza HTTP ou HTTPS necessita de mais CPU e memória no computador do ponto de gestão que se utilizar um número de porta personalizado. Também pode especificar o número de porta de site a utilizar se reativar clientes utilizando pacotes de reativação tradicionais.  

 Quando especificar portas de pedido de HTTP e HTTPS, pode especificar um número de porta predefinido e um número de porta alternativo. Os clientes tentam automaticamente a porta alternativa após a falha de comunicação com a porta predefinida. Pode especificar definições para comunicações de dados HTTP e HTTPS.  

 Os valores predefinidos para as portas de pedido do cliente são **80** para tráfego HTTP e **443** para tráfego HTTPS. Altere-as apenas se não pretender utilizar estes valores predefinidos. Um cenário típico de utilização de portas personalizadas é quando utiliza um Web site personalizado no IIS, em vez do Web site predefinido. Se alterar os números de porta predefinidos para o Web site predefinido no IIS e outras aplicações também utilizarem o Web site predefinido, é provável que falhem.  

> [!IMPORTANT]  
>  Não altere os números de porta no Configuration Manager sem compreender as consequências. Exemplos:  
>   
>  -   Se alterar os números de porta para os serviços de pedidos de cliente como uma configuração do site e não reconfigurar clientes existentes para utilizarem os novos números de porta, estes clientes se tornarem não geridos.  
> -   Antes de configurar um número de porta não predefinido, certifique-se de que as firewalls e todos os dispositivos de rede intervenientes suportam esta configuração e reconfigure-os conforme necessário. Se for gerir clientes na Internet e alterar o número da porta HTTPS predefinida da 443, os routers e firewalls na Internet poderão bloquear estas comunicações.  

 Para se certificar de que os clientes não deixam de ser geridos depois de alterar os números de porta de pedido, os clientes devem ser configurados para utilizarem os novos números de porta de pedido. Quando alterar as portas de pedido num site primário, quaisquer sites secundários ligados herdarão automaticamente a mesma configuração de portas. Utilize o procedimento neste tópico para configurar as portas de pedido no site primário.  

> [!NOTE]  
>  Para obter informações sobre como configurar as portas de pedido para clientes em computadores que executam o Linux e UNIX, consulte o artigo [configurar as portas de pedido do cliente para Linux e UNIX](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md#BKMK_ConfigLnUClientCommuincations).  

 Quando o site do Configuration Manager é publicado para serviços de domínio do Active Directory, os clientes novos e existentes que podem aceder a estas informações serão automaticamente configurados com as definições de porta do site e não necessita de ação adicional. Os clientes que não é possível aceder estas informações publicadas serviços de domínio do Active Directory incluem clientes de grupo de trabalho, clientes de outra floresta do Active Directory, os clientes que estão configurados para apenas de Internet e os clientes que se encontram atualmente na Internet. Se alterar os números de porta predefinidos após a instalação destes clientes, reinstale-os e instale quaisquer clientes novos utilizando um dos seguintes métodos:  

-   Reinstale os clientes utilizando o Assistente de instalação Push do cliente. Instalação push do cliente configura automaticamente os clientes com a configuração de portas atual do site. Para obter mais informações sobre como utilizar o Assistente de instalação Push do cliente, consulte o artigo [como instalar clientes do Configuration Manager utilizando a emissão de cliente](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).  

-   Reinstale os clientes utilizando CCMSetup.exe e as propriedades de instalação CCMHTTPPORT e CCMHTTPSPORT. Para obter mais informações sobre estas propriedades, consulte o artigo [acerca das propriedades de instalação de cliente no System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

-   Reinstale os clientes utilizando um método que procura serviços de domínio do Active Directory para propriedades de instalação de cliente do Configuration Manager. Para obter mais informações, veja [Acerca das propriedades de instalação de cliente publicadas nos Serviços de Domínio do Active Directory no System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

 Para reconfigurar os números de porta para clientes existentes, também pode utilizar o script PORTSWITCH. VBS fornecido com o suporte de dados de instalação na pasta smssetup\tools\portconfiguration.  

> [!IMPORTANT]  
>  Para clientes novos e existentes que estão atualmente na Internet, tem de configurar os números de porta não predefinidos utilizando as propriedades de Client. msi CCMSetup.exe de CCMHTTPPORT e CCMHTTPSPORT.  

 Depois de alterar as portas de pedido no site, os clientes novos que sejam instalados utilizando o método de instalação de push de cliente em todo o site serão automaticamente configurados com os números de porta atuais do site.  

#### <a name="to-configure-the-client-communication-port-numbers-for-a-site"></a>Para configurar os números de porta de comunicação de cliente para um site  

1.  Na consola do Configuration Manager, clique em **Administração**.  

2.  No **administração** área de trabalho, expanda **configuração do Site**, clique em **Sites**e selecione o site primário a configurar.  

3.  No **base** separador, clique em **propriedades**e, em seguida, clique na **portas** separador.  

4.  Selecione qualquer um dos itens e clique no ícone propriedades para apresentar o **detalhes da porta** caixa de diálogo.  

5.  No **detalhes da porta** caixa de diálogo, especifique o número de porta e a descrição para o item e, em seguida, clique em **OK**.  

6.  Selecione **utilizar um web site personalizado** se pretender utilizar o nome do Web site personalizado do **SMSWeb** para sistemas de sites que executam o IIS.  

7.  Clique em **OK** para fechar a caixa de diálogo de propriedades do site.  

 Repita este procedimento para todos os sites primários da hierarquia.

