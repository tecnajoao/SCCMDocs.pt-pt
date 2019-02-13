---
title: Firewalls e domínios
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
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1cc3a1532a326019db3517c70723831f309be76b
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56127138"
---
# <a name="set-up-firewalls-ports-and-domains-for-system-center-configuration-manager"></a>Configurar firewalls, portas e domínios para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Para preparar a sua rede para suportar o System Center Configuration Manager, planeie configurar a infraestrutura como firewalls para passar as comunicações utilizadas pelo Configuration Manager.  

|Consideração|Detalhes|  
|-------------------|-------------|  
|**Portas e protocolos** que usam diferentes capacidades do Configuration Manager. Algumas portas são necessárias, e pode personalizar a outro **domínios e serviços**.|A maioria das comunicações do Configuration Manager utilizam portas comuns, como a porta 80 para HTTP ou 443 para comunicação HTTPS. No entanto, [algumas funções de sistema de sites suportam a utilização de Web sites personalizados](/sccm/core/plan-design/network/websites-for-site-system-servers) e portas personalizadas.<br /><br /> **Antes de implementar o Configuration Manager**, identificar as portas que pretende utilizar e configurar firewalls em conformidade.<br /><br /> **Se precisar de alterar uma porta** depois de instalar o Configuration Manager, não se esqueça de atualizar as firewalls nos dispositivos e a rede e também alterar a configuração da porta do Configuration Manager.<br /><br /> Para obter mais informações, consulte: </br>- [Como configurar portas de comunicação de cliente](../../../core/clients/deploy/configure-client-communication-ports.md) </br>- [Portas utilizadas no Configuration Manager](../../../core/plan-design/hierarchy/ports.md) </br>- [Requisitos de acesso de Internet para o ponto de ligação de serviço](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_urls)|  
|**Domínios e serviços** que clientes e servidores de site, poderão ter de utilizar.|Capacidades do Configuration Manager podem exigir servidores de site e os clientes a terem acesso a serviços específicos e domínios na Internet, como Windowsudpate.microsoft.com ou o serviço Microsoft Intune.<br /><br /> Se pretender utilizar o Microsoft Intune para gerir dispositivos móveis, tem de definir também o acesso a [portas e domínios que o Intune necessita.](https://docs.microsoft.com/intune/get-started/network-infrastructure-requirements-for-microsoft-intune)|  
|**Servidores proxy** para servidores do sistema de sites e para comunicações de cliente. Pode especificar servidores proxy separados para clientes e servidores do sistema de site diferente.|Uma vez que estas configurações são efetuadas no momento, instalar uma função do sistema de sites ou cliente, apenas terá de ter em consideração as configurações de servidor proxy para referência futura quando configurar funções de sistema de sites e clientes.<br /><br /> Se não tiver a certeza de sua implementação terá de utilizar servidores proxy, consulte [suporte de servidor Proxy no System Center Configuration Manager](../../../core/plan-design/network/proxy-server-support.md) para saber mais sobre funções de sistema de sites e as ações de cliente que podem utilizar um servidor proxy.|   
|  
