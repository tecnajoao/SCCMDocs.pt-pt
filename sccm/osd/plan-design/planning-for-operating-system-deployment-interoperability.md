---
title: "Planear a interoperabilidade da implementação do sistema operativo"
titleSuffix: Configuration Manager
description: "Compreenda os problemas de interoperabilidade quando diversos sites do System Center Configuration Manager numa única hierarquia utilizam versões diferentes."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: e327ce38-6c07-4a27-b6eb-7e5bf74ed04b
caps.latest.revision: "10"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 41c7c83602f965cd4a225d38a00b90501206de45
ms.sourcegitcommit: 08f9854fb6c6d21e1e923b13e38a64d0bc2bc9a4
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/12/2017
---
# <a name="planning-for-operating-system-deployment-interoperability-in-system-center-configuration-manager"></a>Planear a interoperabilidade da implementação do sistema operativo no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Quando diversos sites do System Center Configuration Manager numa única hierarquia utilizam versões diferentes, algumas funcionalidades do Configuration Manager não estão disponível. Normalmente, as funcionalidades da versão mais recente do Configuration Manager não está acessível em sites ou para clientes que possuam uma versão anterior. Para obter mais informações, veja [Interoperabilidade entre diferentes versões do System Center Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  

 Quando atualizar o site de nível superior na sua hierarquia e a outros sites na sua hierarquia executar o Configuration Manager com uma versão inferior, considere o seguinte:  

-   Pacote de instalação de cliente  

    -   A origem para o pacote de instalação de cliente predefinido é atualizada automaticamente e todos os pontos de distribuição na hierarquia são atualizados com o novo pacote de instalação do cliente, mesmo em pontos de distribuição em sites da hierarquia que tenham uma versão inferior.  

    -   Clientes que executam a nova versão não podem ser atribuídos a sites que ainda não tenham sido atualizados para a nova versão. Atribuição é bloqueada no ponto de gestão.  

-   Imagens de arranque  

    -   Quando atualizar o site de nível superior para a versão mais recente do Configuration Manager, as imagens de arranque predefinidas (x86 e x64) são automaticamente atualizadas para imagens de arranque baseadas no Windows ADK para Windows 10, que utilizam o Windows PE 10. Os ficheiros que estão associados a imagens de arranque predefinidas são atualizados com a versão mais recente do Configuration Manager dos ficheiros. As imagens de arranque personalizadas não são atualizadas automaticamente. Terá de atualizar imagens de arranque personalizadas manualmente, que inclui as versões mais antigas do Windows PE.  

    -   Evite a utilização de suportes de dados dinâmicos quando a hierarquia de sites contiver sites com diversas versões do Configuration Manager. Em alternativa, utilize suportes de dados baseados no site para contactar um ponto de gestão específico até que todos os sites tenham sido atualizados para a mesma versão do Configuration Manager.  

    -   Certifique-se de que as imagens de arranque mais recentes do Configuration Manager contêm a personalização desejada e, em seguida, atualize todos os pontos de distribuição dos sites com a versão mais recente do Configuration Manager com as novas imagens de arranque.  

-   User State Migration Tool (USMT)  

    -   Quando atualizar o site de nível superior para a versão mais recente do Configuration Manager, o pacote USMT predefinido é atualizado automaticamente para a versão mais recente. Os pacotes USMT personalizados não são atualizados automaticamente. Terá de atualizar manualmente estes pacotes.  

-   Novos passos de sequência de tarefas  

    -   Periodicamente, são introduzidos novos passos de sequência de tarefas com novas versões do Configuration Manager. Quando implementar uma sequência de tarefas com um novo passo em clientes mais antigos, o passo de sequência de tarefas falhará. Antes de implementar uma sequência de tarefas com um novo passo, certifique-se de que os clientes da coleção de destino são atualizados para a nova versão.  

-   Suporte de dados de implementação do sistema operativo  

    -   Todos os suportes de dados (arranque, captura, pré-configurados e autónoma) têm de ser atualizados com o novo pacote de cliente do Configuration Manager quando o site é atualizado para uma nova versão.  

-   Extensões de terceiros para a implementação do sistema operativo  

    -   Quando tiver extensões de terceiros para implementação do sistema operativo e tiver versões diferentes dos sites do Configuration Manager ou clientes do Configuration Manager, uma hierarquia mista, poderão existir problemas com as extensões.  

 Quando atualizar sites na hierarquia de forma ativa, utilize as secções seguintes para o ajudar com as implementações de sistema operativo.  

## <a name="latest-version-of-configuration-manager-sites-in-a-mixed-hierarchy"></a>Versão mais recente dos sites do Configuration Manager numa hierarquia mista  
 Quando atualizar um site para a versão mais recente do Configuration Manager, sequências de tarefas que a referência ao pacote de instalação de cliente predefinido começarão automaticamente a implementar a versão mais recente do cliente do Configuration Manager. E sequências de tarefas que façam referência a um pacote de instalação de cliente personalizado continuarão a implementar a versão do cliente que esteja contida nesse pacote personalizado (provavelmente uma versão de cliente do Configuration Manager anterior), tem de ser atualizadas para evitar falhas de implementação de sequência de tarefas. Quando tiver uma sequência de tarefas que está configurada para utilizar um pacote de instalação de cliente personalizado, tem de atualizar o passo de sequência de tarefas para utilizar a versão mais recente do Configuration Manager do pacote de instalação de cliente ou atualizar o pacote personalizado para utilizar a origem de instalação de cliente mais recente do Configuration Manager.  

> [!IMPORTANT]  
>  Não implemente uma sequência de tarefas referencia o pacote de instalação de cliente mais recente do Configuration Manager para clientes de um site do Configuration Manager mais antigos. Quando os clientes atribuídos a um site do Configuration Manager mais antigo sejam atualizados para a versão mais recente do cliente do Configuration Manager, o Configuration Manager bloqueia a atribuição ao site do Configuration Manager mais antigo. Por conseguinte, o cliente já não está atribuído a qualquer site e deixará de ser gerido até que atribuir o cliente ao site mais recente do Configuration Manager manualmente ou reinstale a versão mais antiga do Configuration Manager do cliente no computador.  

## <a name="older-versions-of-configuration-manager-in-a-mixed-hierarchy"></a>Versões mais antigas do Configuration Manager numa hierarquia mista  
 Quando tiver atualizado o seu site de administração central para a versão mais recente do Configuration Manager, tem de executar os seguintes passos para se certificar de que as sequências de tarefas de implementação do sistema operativo que implementar em clientes atribuídos a um site do Configuration Manager mais antigo (ainda não atualizado para a versão mais recente do Configuration Manager) não deixam esses clientes num Estado não gerido.  

-   Crie uma sequência de tarefas que irá utilizar para implementar em clientes apenas num site do Configuration Manager. Provavelmente, fará uma cópia da sequência de tarefas que utilizar para implementar em clientes na versão mais recente do site do Configuration Manager e, em seguida, modificar a sequência de tarefas de modo a poder implementá-la em clientes de um site do Configuration Manager mais antigo. Em seguida, configure a sequência de tarefas para fazer referência a um pacote de instalação de cliente personalizado que utiliza a origem de instalação de cliente mais antiga do Configuration Manager. Se ainda não tiver um pacote de instalação de cliente personalizado que faça referência a origem de instalação de cliente mais antiga do Configuration Manager, em seguida, tem de criar manualmente um.  
