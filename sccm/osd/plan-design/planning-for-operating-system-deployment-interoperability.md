---
title: Planear a interoperabilidade da implementação do sistema operativo
titleSuffix: Configuration Manager
description: Compreenda os problemas de interoperabilidade quando diversos sites do System Center Configuration Manager numa única hierarquia utilizam versões diferentes.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: e327ce38-6c07-4a27-b6eb-7e5bf74ed04b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: aceb5f032cd0a4a5c12672db625b540465e37800
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53418480"
---
# <a name="planning-for-operating-system-deployment-interoperability-in-system-center-configuration-manager"></a>Planear a interoperabilidade da implementação do sistema operativo no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Quando diversos sites do System Center Configuration Manager numa única hierarquia utilizam versões diferentes, algumas funcionalidades do Configuration Manager não estão disponível. Normalmente, as funcionalidades da versão mais recente do Configuration Manager não estão acessível em sites ou para clientes que tenham uma versão inferior. Para obter mais informações, veja [Interoperabilidade entre diferentes versões do System Center Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  

 Quando atualizar o site de nível superior na sua hierarquia e outros sites na sua hierarquia executar o Configuration Manager com uma versão inferior, considere o seguinte:  

- Pacote de instalação de cliente  

  -   A origem para o pacote de instalação de cliente predefinido é atualizada automaticamente e todos os pontos de distribuição na hierarquia são atualizados com o novo pacote de instalação do cliente, mesmo em pontos de distribuição em sites da hierarquia que tenham uma versão inferior.  

  -   Os clientes que executem a nova versão não podem ser atribuídos a sites que ainda não tenham sido atualizados para a nova versão. Atribuição é bloqueada no ponto de gestão.  

- Imagens de arranque  

  -   Ao atualizar o site de nível superior para a versão mais recente do Configuration Manager, as imagens de arranque predefinidas (x86 e x64) são automaticamente atualizadas para imagens de arranque baseadas no Windows ADK para Windows 10, que utilizam o Windows PE 10. Os ficheiros que estão associados a imagens de arranque predefinidas são atualizados com a versão mais recente do Configuration Manager dos ficheiros. As imagens de arranque personalizadas não são atualizadas automaticamente. Precisará atualizar imagens de arranque personalizadas manualmente, que inclui as versões mais antigas do Windows PE.  

  -   Evite a utilização de suportes de dados dinâmicos quando a hierarquia de sites contiver sites com diferentes versões do Configuration Manager. Em vez disso, utilize o suporte de dados baseado no site para contactar um ponto de gestão específico até que todos os sites são atualizados para a mesma versão do Configuration Manager.  

  -   Certifique-se de que as imagens de arranque mais recente do Configuration Manager contêm a personalização desejada e, em seguida, atualize todos os pontos de distribuição nos sites com a versão mais recente do Configuration Manager com as novas imagens de arranque.  

- User State Migration Tool (USMT)  

  -   Ao atualizar o site de nível superior para a versão mais recente do Configuration Manager, o pacote do USMT predefinido é atualizado automaticamente para a versão mais recente. Os pacotes USMT personalizados não são atualizados automaticamente. Terá de atualizar manualmente estes pacotes.  

- Novos passos de sequência de tarefas  

  -   Periodicamente, são introduzidos novos passos de sequência de tarefas com novas versões do Configuration Manager. Quando implementar uma sequência de tarefas com um novo passo em clientes mais antigos, o passo de sequência de tarefas falhará. Antes de implementar uma sequência de tarefas com um novo passo, certifique-se de que os clientes da coleção de destino são atualizados para a nova versão.  

- Suporte de dados de implementação do sistema operativo  

  -   Todos os suportes de dados (de arranque, captura, pré-configurados e autónoma) têm de ser atualizados com o novo pacote de cliente do Configuration Manager quando o site é atualizado para uma nova versão.  

- Extensões de terceiros para a implementação do sistema operativo  

  -   Quando tiver extensões de terceiros para implementação do sistema operativo e tiver versões diferentes de sites do Configuration Manager ou de clientes do Configuration Manager, de uma hierarquia mista, poderão existir problemas com as extensões.  

  Quando atualizar sites na hierarquia de forma ativa, utilize as secções seguintes para o ajudar com as implementações de sistema operativo.  

## <a name="latest-version-of-configuration-manager-sites-in-a-mixed-hierarchy"></a>Versão mais recente dos sites do Configuration Manager numa hierarquia mista  
 Ao atualizar um site para a versão mais recente do Configuration Manager, sequências de tarefas que a referência ao pacote de instalação de cliente predefinido começarão automaticamente para implementar a versão mais recente do cliente do Configuration Manager. Sequências de tarefas que façam referência a um pacote de instalação de cliente personalizado continuarão a implementar a versão do cliente que está contida nesse pacote personalizado (provavelmente uma versão de cliente do Configuration Manager anterior) e tem de ser atualizadas para evitar a sequência de tarefas falhas de implementação. Quando tiver uma sequência de tarefas que está configurada para utilizar um pacote de instalação de cliente personalizado, terá de atualizar o passo de sequência de tarefas para utilizar a versão mais recente do Configuration Manager do pacote de instalação do cliente ou atualizar o pacote personalizado para utilizar a versão mais recente Origem de instalação de cliente do Configuration Manager.  

> [!IMPORTANT]  
>  Não implemente uma sequência de tarefas que referencia o pacote de instalação de cliente mais recente do Configuration Manager para os clientes num site mais antigo do Configuration Manager. Quando os clientes atribuídos a um site do Configuration Manager mais antigo são atualizados para a versão mais recente do cliente do Configuration Manager, o Configuration Manager bloqueia a atribuição ao site do Configuration Manager mais antigo. Por conseguinte, o cliente já não está atribuído a qualquer site e deixará de ser gerido até que atribuir o cliente ao site mais recente do Configuration Manager manualmente ou reinstale a versão mais antiga do Configuration Manager do cliente no computador.  

## <a name="older-versions-of-configuration-manager-in-a-mixed-hierarchy"></a>Versões mais antigas do Configuration Manager numa hierarquia mista  
 Quando tiver atualizado o seu site de administração central para a versão mais recente do Configuration Manager, tem de executar os seguintes passos para garantir que essa implementação do sistema operativo sequências de tarefas que implementa em clientes atribuídos a um mais antigas do Configuration Manager site (ainda não atualizado para a versão mais recente do Configuration Manager) não deixam esses clientes num Estado não gerido.  

-   Crie uma sequência de tarefas que irá utilizar para implementar em clientes apenas num site do Configuration Manager. Provavelmente, fará uma cópia de uma sequência de tarefas que utiliza para implementar em clientes na versão mais recente do site do Configuration Manager e, em seguida, modificar a sequência de tarefas de modo a poder implementá-lo para os clientes num site mais antigo do Configuration Manager. Em seguida, configure a sequência de tarefas para fazer referência a um pacote de instalação de cliente personalizado que utiliza a origem de instalação de cliente mais antiga do Configuration Manager. Se ainda não tiver um pacote de instalação de cliente personalizado que faça referência a origem de instalação de cliente mais antiga do Configuration Manager, em seguida, deve criá-lo manualmente.  
