---
title: "Planear a interoperabilidade de implementação do sistema operativo de | Documentos do Microsoft"
description: "Quando diversos sites de System Center Configuration Manager de uma única hierarquia utilizam versões diferentes de compreender os problemas de interoperabilidade."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: e327ce38-6c07-4a27-b6eb-7e5bf74ed04b
caps.latest.revision: 10
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 74341fb60bf9ccbc8822e390bd34f9eda58b4bda
ms.openlocfilehash: 50a4b75b8c8c1cb6f7a8e696abad285f99080fcd
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="planning-for-operating-system-deployment-interoperability-in-system-center-configuration-manager"></a>Planear a interoperabilidade da implementação do sistema operativo no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Quando diversos sites de System Center Configuration Manager numa única hierarquia utilizam versões diferentes, algumas funcionalidades do Configuration Manager não está disponível. Normalmente, as funcionalidades da versão mais recente do Configuration Manager não está acessível em sites ou para os clientes que executem uma versão inferior. Para obter mais informações, veja [Interoperabilidade entre diferentes versões do System Center Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  

 Quando atualizar o site de nível superior na sua hierarquia e de outros sites da hierarquia, execute o Gestor de configuração com uma versão inferior, considere o seguinte:  

-   Pacote de instalação do cliente  

    -   A origem para o pacote de instalação de cliente predefinido é automaticamente atualizada e todos os pontos de distribuição na hierarquia são atualizados com o novo pacote de instalação do cliente, mesmo em pontos de distribuição em sites da hierarquia que estão uma versão inferior.  

    -   Os clientes que executem a nova versão não podem ser atribuídos a sites que ainda não foram atualizados para a nova versão. Atribuição é bloqueada no ponto de gestão.  

-   Imagens de arranque  

    -   Quando atualizar o site de nível superior para a versão mais recente do Configuration Manager, imagens de arranque predefinidas (x86 e x64) são automaticamente atualizadas para imagens de arranque baseadas no Windows ADK para Windows 10, que utilizam o Windows PE 10. Os ficheiros que estão associados a imagens de arranque predefinidas são atualizados com a versão mais recente do Configuration Manager dos ficheiros. As imagens de arranque personalizadas não são atualizadas automaticamente. Terá de atualizar manualmente, imagens de arranque personalizadas que inclui as versões mais antigas do Windows PE.  

    -   Evite a utilização de suportes de dados dinâmicos quando a hierarquia de sites contiver sites com diferentes versões do Configuration Manager. Em vez disso, utilize suportes de dados baseados no site para contactar um ponto de gestão específico até que todos os sites tenham sido atualizados para a mesma versão do Configuration Manager.  

    -   Certifique-se de que as imagens de arranque mais recentes do Configuration Manager contêm a personalização que pretende e, em seguida, atualize todos os pontos de distribuição nos sites com a versão mais recente do Configuration Manager com as novas imagens de arranque.  

-   User State Migration Tool (USMT)  

    -   Quando atualizar o site de nível superior para a versão mais recente do Configuration Manager, o pacote do USMT predefinido é atualizado automaticamente para a versão mais recente. Os pacotes USMT personalizados não são atualizados automaticamente. Terá de atualizar manualmente estes pacotes.  

-   Novos passos de sequência de tarefas  

    -   Periodicamente, os novos passos de sequência de tarefas são introduzidos com novas versões do Configuration Manager. Quando implementar uma sequência de tarefas com um novo passo em clientes mais antigos, o passo de sequência de tarefas falhará. Antes de implementar uma sequência de tarefas com um novo passo, certifique-se de que os clientes da coleção de destino são atualizados para a nova versão.  

-   Suporte de dados de implementação do sistema operativo  

    -   Todos os suportes de dados (suportes, captura, autónoma e suportes) têm de ser atualizados com o novo pacote de cliente do Configuration Manager quando o site é atualizado para uma nova versão.  

-   Extensões de terceiros para a implementação do sistema operativo  

    -   Quando tiver de extensões de terceiros para implementação do sistema operativo e têm versões diferentes de sites do Configuration Manager ou clientes do Configuration Manager, numa hierarquia mista, poderão existir problemas com as extensões.  

 Quando atualizar sites na hierarquia de forma ativa, utilize as secções seguintes para o ajudar com as implementações de sistema operativo.  

## <a name="latest-version-of-configuration-manager-sites-in-a-mixed-hierarchy"></a>Versão mais recente de sites do Configuration Manager numa hierarquia mista  
 Ao atualizar um site para a versão mais recente do Configuration Manager, sequências de tarefas que a referência ao pacote de instalação de cliente predefinido começarão automaticamente a implementar a versão mais recente do cliente do Configuration Manager. E sequências de tarefas que fazem referência a um pacote de instalação de cliente personalizado continuarão a implementar a versão do cliente que esteja contida nesse pacote personalizado (provavelmente uma versão de cliente do Configuration Manager anterior), tem de ser atualizadas para evitar falhas de implementação de sequência de tarefas. Quando tiver uma sequência de tarefas que está configurada para utilizar um pacote de instalação de cliente personalizadas, tem de atualizar o passo de sequência de tarefas para utilizar a versão mais recente do Configuration Manager do pacote de instalação de cliente ou atualizar o pacote personalizado para utilizar a origem de instalação de cliente mais recente do Configuration Manager.  

> [!IMPORTANT]  
>  Não implemente uma sequência de tarefas que referencia o pacote de instalação de cliente mais recente do Configuration Manager para os clientes num site do Configuration Manager mais antigo. Quando os clientes atribuídos a um site do Configuration Manager mais antigo sejam atualizados para a versão mais recente do cliente do Configuration Manager, Configuration Manager bloqueia a atribuição ao site do Configuration Manager mais antigo. Por conseguinte, o cliente já não está atribuído a qualquer site e deixará de ser gerido até que manualmente atribuir o cliente ao site do Configuration Manager mais recente ou reinstale a versão mais antiga do Configuration Manager do cliente no computador.  

## <a name="older-versions-of-configuration-manager-in-a-mixed-hierarchy"></a>Versões mais antigas do Configuration Manager numa hierarquia mista  
 Quando tiver atualizado o seu site de administração central para a versão mais recente do Configuration Manager, tem de efetuar o passo seguinte para se certificar de que sequências de tarefas de implementação do sistema operativo que implementar em clientes atribuídos a um site do Configuration Manager mais antigo (ainda não atualizado para a versão mais recente do Configuration Manager) não deixam esses clientes num Estado não gerido.  

-   Crie uma sequência de tarefas que irá utilizar para implementar em clientes apenas num site do Configuration Manager. Provavelmente, irá efetuar uma cópia de uma sequência de tarefas que utilizar para implementar clientes na versão mais recente do site do Configuration Manager e, em seguida, modificar a sequência de tarefas para poder implementar em clientes de um site do Configuration Manager mais antigo. Em seguida, configure a sequência de tarefas para fazer referência a um pacote de instalação de cliente personalizadas que utiliza a origem da instalação de cliente do Configuration Manager mais antiga. Se ainda não tiver um pacote de instalação de cliente personalizado que referencia a origem da instalação de cliente do Configuration Manager anterior, em seguida, tem de criar manualmente um.  

