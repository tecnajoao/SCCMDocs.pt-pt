---
title: As firewalls e os domínios
titleSuffix: Configuration Manager
description: Configure firewalls, portas e domínios para se preparar para as comunicações do System Center Configuration Manager.
ms.date: 2/6/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d6993bba-f6bd-4639-adbf-efc1c638b2f3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ee7494b582828014114d41eb6bb721a7e1fd5c16
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="set-up-firewalls-ports-and-domains-for-system-center-configuration-manager"></a>Configurar firewalls, portas e domínios para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Para preparar a sua rede para suportar o System Center Configuration Manager, planeie configurar infraestrutura como firewalls para passar as comunicações utilizadas pelo Configuration Manager.  

|Consideração|Detalhes|  
|-------------------|-------------|  
|**Portas e protocolos** que utilizam diferentes capacidades do Configuration Manager. Algumas portas são necessárias e pode personalizar outros **domínios e serviços**.|A maioria das comunicações do Configuration Manager utilizam portas comuns, como a porta 80 para HTTP ou 443 para comunicação por HTTPS. No entanto, [algumas funções de sistema de sites suportam a utilização de Web sites personalizados](/sccm/core/plan-design/network/websites-for-site-system-servers) e portas personalizadas.<br /><br /> **Antes de implementar o Configuration Manager**, identifique as portas que pretende utilizar e configurar as firewalls em conformidade.<br /><br /> **Se precisar de alterar uma porta** depois de instalar o Configuration Manager, não se esqueça de atualizar as firewalls em dispositivos e da rede e também alterar a configuração da porta do Configuration Manager.<br /><br /> Para obter mais informações, consulte: </br>- [Como configurar portas de comunicação de cliente](../../../core/clients/deploy/configure-client-communication-ports.md) </br>- [Portas utilizadas no Configuration Manager](../../../core/plan-design/hierarchy/ports.md) </br>- [Requisitos de acesso à Internet para o ponto de ligação de serviço](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_urls)|  
|**Domínios e serviços** que os clientes e servidores de site poderão ter de utilizar.|Capacidades do Configuration Manager podem exigir a servidores de sites e clientes tenham acesso a serviços específicos e domínios na Internet, como Windowsudpate.microsoft.com ou o serviço Microsoft Intune.<br /><br /> Se for utilizar o Microsoft Intune para gerir dispositivos móveis, também tem de definir configurar o acesso ao [portas e domínios que requer o Intune.](https://docs.microsoft.com/en-us/intune/get-started/network-infrastructure-requirements-for-microsoft-intune)|  
|**Servidores proxy** para servidores do sistema de sites e para as comunicações do cliente. Pode especificar servidores proxy separados para clientes e servidores de sistema de site diferente.|Porque estas configurações são efetuadas no momento que instalar uma função do sistema de sites ou o cliente, apenas terá de ter em consideração as configurações de servidor proxy para futura referência quando configurar funções de sistema de sites e clientes.<br /><br /> Se não tiver a certeza a sua implementação terá de utilizar servidores proxy, consulte [suporte para servidor Proxy no System Center Configuration Manager](../../../core/plan-design/network/proxy-server-support.md) para saber mais sobre as funções do sistema de sites e as ações de cliente que podem utilizar um servidor proxy.|   
|  
