---
title: Adicionar funções do sistema de sites
titleSuffix: Configuration Manager
description: Compreenda as funções de sistema de sites do Configuration Manager e como adicioná-las para expandir a funcionalidade e a capacidade do seu site.
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: b90de2d9-494e-43ad-b269-c8ed589f37d3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2959d2b97088a2d92b861f0ca4a4d37d0df3e726
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="add-site-system-roles-for-system-center-configuration-manager"></a>Adicionar funções do sistema de sites para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Cada site do System Center Configuration Manager suporta várias funções de sistema de sites. Cada função expande a funcionalidade e a capacidade do seu site para fornecer serviços para o site e para gerir dispositivos e utilizadores. Cada função do sistema de sites num servidor do sistema de sites tem de ser do mesmo site.   

O Configuration Manager não suporta funções do sistema de sites para múltiplos sites num servidor de sistema de site único.  

> [!TIP]  
>  Se não estiver familiarizado com os princípios básicos sobre funções de sistema de sites ou a diferença entre o servidor do site, servidores do sistema de sites e funções de sistema de sites, consulte [Noções básicas do System Center Configuration Manager](../../../../core/understand/fundamentals.md).  

 Os seguintes tópicos indicam em pormenor os procedimentos e detalhes relacionados para instalar funções do sistema do site:  

-   [Instalar funções do sistema de site para o System Center Configuration Manager](../../../../core/servers/deploy/configure/install-site-system-roles.md)  

     Este tópico fornece orientações básicas sobre como utilizar os dois assistentes na consola que pode utilizar para instalar novas funções do sistema de sites.  

-   [Instalar pontos de distribuição baseado na nuvem no Microsoft Azure para o System Center Configuration Manager](../../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)  

    Quando pretender utilizar o Microsoft Azure para alojar conteúdo que implementar em clientes, as informações neste tópico irão ajudar a configurar os ficheiros de certificado necessário para permitir que o Configuration Manager comunicar com e utilizar a sua subscrição do Microsoft Azure. Além disso, terá de configurar a resolução de nome para permitir que os seus clientes para localizar pontos de distribuição baseado na nuvem.  

-   [Instalar funções do sistema de sites para gestão de dispositivos móveis no local no System Center Configuration Manager](../../../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md)  

     Este tópico ajuda-o a configurar com êxito as funções de sistema de sites para suportar a gestão de dispositivos modernos utilizando o MDM do Configuration Manager no local.  

-   [Opções de configuração para funções do sistema de sites para o System Center Configuration Manager](../../../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md)  

     Algumas funções do sistema de site suportam configurações que necessitam de que mais detalhes que a interface de utilizador podem explicar. Este tópico fornece os detalhes.  
