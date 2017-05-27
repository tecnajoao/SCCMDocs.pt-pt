---
title: "Referência de configuração | Documentos do Microsoft"
description: "Reveja esta referência para o ajudar a preparar para instalar um site do Configuration Manager ou a hierarquia."
ms.custom: na
ms.date: 4/18/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cdb9fb0c-0912-41e4-b427-f40620971763
caps.latest.revision: 22
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 761c3f58f7c57d8f87ee802da37821895062546d
ms.openlocfilehash: 739461a6cca0fd67431093524c1e8158afd80d0f
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="reference-for-system-center-configuration-manager-setup"></a>Referência para o Programa de Configuração do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O programa de configuração do System Center Configuration Manager fornece hiperligações para vários tópicos que estão descritos nas secções seguintes. As informações apresentadas aqui podem ajudar a preparar para instalar um site do Configuration Manager ou uma hierarquia e ajudam a preparar para algumas das decisões que deve tomar durante a instalação.  


##  <a name="bkmk_start"></a> Antes de começar  
Antes de instalar novos sites do Configuration Manager, certifique-se de que rever as informações seguintes, que podem ajudar a definir o palco para uma estrutura de implementação efetuada com êxito:  

-   [Noções básicas do System Center Configuration Manager](../../../../core/understand/fundamentals.md)  
-   [Planear a infraestrutura do System Center Configuration Manager](../../../plan-design/network/configure-firewalls-ports-domains.md)  
-   [Preparar a instalação de sites do Configuration Manager do System Center](prepare-to-install-sites.md)  

##  <a name="bkmk_assess"></a> Avaliar a preparação do servidor  
Antes de iniciar a instalação de um novo site, certifique-se de que o servidor do site e os servidores de sistema de sites remotos que pretende utilizar para o site (por exemplo, o servidor que aloja a base de dados do site) cumprem todas as configurações de pré-requisitos. Estes tópicos na biblioteca de documentação podem ajudar:  

-   [Configurações suportadas para o System Center Configuration Manager](../../../../core/plan-design/configs/supported-configurations.md)  
-   [Verificador de pré-requisitos](prerequisite-checker.md)  

##  <a name="bkmk_Addclients"></a> Clientes de sistemas operativos adicionais  
Pode transferir o software de cliente do Configuration Manager a partir de Center Download Microsoft para os seguintes sistemas operativos:  

-   Mac (Apple)  
-   UNIX  
-   Linux  

Utilize as seguintes ligações para transferir clientes para a versão do Configuration Manager utiliza:  

-   Consulte o artigo [do Microsoft System Center Configuration Manager - os clientes para sistemas operativos adicionais](http://www.microsoft.com/download/details.aspx?id=47719)  

##  <a name="bkmk_usage"></a> Níveis e definições de dados de utilização  
Ao instalar o primeiro site do System Center Configuration Manager, Configuration Manager instala e automaticamente configura uma nova função de sistema de sites, o **ponto de ligação de serviço**, no servidor do site. O ponto de ligação de serviço tem estas predefinições:  

-   **Online** modo (modo offline também está disponível)  
-   **Avançada** nível da coleção de dados (dois outros dados coleção níveis, Basic e completo, também estão disponíveis)  

Quando a função de sistema de sites de ponto de ligação de serviço está online, a Microsoft automaticamente pode recolher informações de diagnóstico e de utilização através da Internet. As informações recolhidas ajudam-nos a:  

-   Identificar e resolver problemas  
-   Melhorar os nossos produtos e serviços  
-   Identificar as atualizações para o Configuration Manager que se aplicam à versão do Configuration Manager utilizada  

### <a name="levels-of-data-collection"></a>Níveis de recolha de dados  
Recolha de dados incluem estas três níveis:

-   **Básicas** inclui dados sobre a configuração e atualização, como o número de sites e que funcionalidades do Configuration Manager estão ativadas. Não é transmitida nenhuma informação identificativa.  

-   **Avançada** inclui os dados na definição de nível básica, plus transmite dados sobre a hierarquia, como cada funcionalidade é utilizada (frequência e duração) e melhorada informações de diagnóstico, como o estado da memória do servidor quando um sistema ou ocorrer falhas de aplicação. Não existem dados pessoalmente identificáveis são transmitidos.  

-   **Completo** inclui os dados as definições de nível básico e avançado e se também informações de diagnóstico envia avançada, como ficheiros de sistema e instantâneos de memória. Esta opção poderá incluir informação identificativa, mas não usaremos essa informação para o identificar ou contactar o utilizador, ou publicidade de destino para si.  

Para mais informações, incluindo divulgação dos detalhes da recolhidos por cada nível, consulte o artigo [diagnósticos e dados de utilização para o System Center Configuration Manager](../../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).  

Para ver o System Center Configuration Manager declaração de privacidade online, aceda ao [http://go.microsoft.com/fwlink/?LinkID=626527](http://go.microsoft.com/fwlink/?LinkID=626527).

