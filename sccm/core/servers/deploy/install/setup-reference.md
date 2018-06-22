---
title: Referência da configuração
titleSuffix: Configuration Manager
description: Reveja esta referência para ajudar a preparar para instalar um site do Configuration Manager ou a hierarquia.
ms.date: 4/18/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: cdb9fb0c-0912-41e4-b427-f40620971763
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f9f857a2045f67690579955236c082ff29721a5f
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32339575"
---
# <a name="reference-for-system-center-configuration-manager-setup"></a>Referência para o Programa de Configuração do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Configuração do System Center Configuration Manager fornece ligações para vários tópicos descritos detalhadamente nas secções seguintes. As informações aqui apresentadas podem ajudar a preparar para instalar um site do Configuration Manager ou a hierarquia e ajudar a preparar-se para algumas das decisões que deve tomar durante a instalação.  


##  <a name="bkmk_start"></a> Antes de começar  
Antes de instalar novos sites do Configuration Manager, certifique-se de que reviu as informações seguintes, que podem ajudar a definir o palco para uma estrutura de implementação efetuada com êxito:  

-   [Noções básicas do System Center Configuration Manager](../../../../core/understand/fundamentals.md)  
-   [Planear a infraestrutura do System Center Configuration Manager](../../../plan-design/network/configure-firewalls-ports-domains.md)  
-   [Preparar a instalação de sites do System Center Configuration Manager](prepare-to-install-sites.md)  

##  <a name="bkmk_assess"></a> Avaliar a preparação do servidor  
Antes de iniciar a instalação de um novo site, certifique-se de que o servidor do site e os servidores de sistema de sites remotos que pretende utilizar para o site (por exemplo, o servidor que aloja a base de dados do site) satisfazem todas as configurações de pré-requisitos. Estes tópicos na biblioteca de documentação podem ajudar:  

-   [Configurações suportadas para o System Center Configuration Manager](../../../../core/plan-design/configs/supported-configurations.md)  
-   [Verificador de pré-requisitos](prerequisite-checker.md)  

##  <a name="bkmk_Addclients"></a> Clientes de sistemas operativos adicionais  
Pode transferir o software de cliente do Configuration Manager do Microsoft Download Center para os seguintes sistemas operativos:  

-   Mac (Apple)  
-   UNIX  
-   Linux  

Utilize as seguintes ligações para transferir clientes para a versão do Configuration Manager utiliza:  

-   Consulte [do Microsoft System Center Configuration Manager - clientes para sistemas operativos adicionais](http://www.microsoft.com/download/details.aspx?id=47719)  

##  <a name="bkmk_usage"></a> Níveis e definições de dados de utilização  
Quando instalar o primeiro site do System Center Configuration Manager, Configuration Manager instala e automaticamente configura uma nova função de sistema de sites, o **ponto de ligação de serviço**, no servidor do site. O ponto de ligação de serviço tem estas predefinições:  

-   **Online** modo (modo offline também está disponível)  
-   **Melhorado** nível de recolha de dados (dois outros dados níveis de recolha, Basic e completo, também estão disponíveis)  

Quando a função de sistema de sites de ponto de ligação de serviço está online, a Microsoft pode recolher automaticamente informações de diagnóstico e utilização através da Internet. As informações recolhidas ajudam-nos a:  

-   Identificar e resolver problemas  
-   Melhorar os nossos produtos e serviços  
-   Identificar as atualizações para o Configuration Manager que se aplicam à versão do Configuration Manager utilizada  

### <a name="levels-of-data-collection"></a>Níveis de recolha de dados  
Recolha de dados incluem estas três níveis:

-   **Básico** inclui dados sobre configuração e atualização, como o número de sites e que funcionalidades do Configuration Manager estão ativadas. Não existem informações de identificação pessoal são transmitidas.  

-   **Melhorado** inclui os dados da definição de nível básico, e transmite dados sobre a hierarquia, a forma como cada funcionalidade é utilizada (frequência e duração) e modulação de informações de diagnóstico, como o estado de memória do seu servidor quando uma falha de sistema ou aplicação ocorre. Não existem dados de identificação pessoal são transmitidos.  

-   **Completo** inclui os dados as definições de nível básico e avançado e também informações de diagnóstico envia avançadas como instantâneos de memória e de ficheiros de sistema. Esta opção pode incluir informações identificativas, mas não as utilizaremos essas informações para identificar ou contactar o utilizador, ou para anúncios de destino para o utilizador.  

Para obter mais informações, incluindo divulgação dos detalhes recolhidos por cada nível, consulte [diagnósticos e dados de utilização para o System Center Configuration Manager](../../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).  

Para ver o System Center Configuration Manager declaração de privacidade online, aceda a [ http://go.microsoft.com/fwlink/?LinkID=626527 ](http://go.microsoft.com/fwlink/?LinkID=626527).
