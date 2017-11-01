---
title: Utilizar limites e grupos de limites
titleSuffix: Configuration Manager
description: "Utilizar limites e grupos de limites para definir as localizações de rede e sistemas de sites acessível para dispositivos que gere."
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 54aa20d5-791e-4416-9db4-5aaea472c0b7
caps.latest.revision: "10"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 5980b33cef6e7711e09c3199150bf60008d1a73b
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="define-site-boundaries-and-boundary-groups-for-system-center-configuration-manager"></a>Definir limites de site e grupos de limites para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Limites para o System Center Configuration Manager definem localizações de rede na sua intranet que pode conter dispositivos que pretende gerir. Grupos de limites são grupos lógicos de limites que configurar.

 Uma hierarquia pode incluir qualquer número de grupos de limites e cada grupo de limites pode conter qualquer combinação dos seguintes tipos de limites:  

-   Sub-rede IP  
-   Nome do site do Active Directory  
-   Prefixo IPv6  
-   Intervalo de endereços IP  

Os clientes na intranet avaliam a respetiva localização de rede atual e, em seguida, utilizam essa informação para identificar os grupos de limites a que pertencem.  

 Os clientes utilizam grupos de limites para:  
-   **Localize um site atribuído:** Grupos de limites permitem aos clientes localizar um site primário para atribuição de cliente (atribuição automática de site).  
-   **Localize determinadas funções de sistema de sites podem utilizar:** Quando associa um grupo de limites a determinadas funções de sistema de sites, o grupo de limites fornece aos clientes essa lista dos sistemas de sites para utilização durante a localização de conteúdo e como pontos de gestão preferenciais.  

Os clientes que estão na Internet ou configurados como clientes apenas da Internet não utilizam informações de limites. Estes clientes não podem utilizar a atribuição automática de sites e podem sempre transferir conteúdo de qualquer ponto de distribuição do seu site atribuído, quando o ponto de distribuição está configurado para permitir ligações de cliente a partir da Internet.  

**Para começar a utilizar:**
- Primeiro, [definem localizações de rede como limites](/sccm/core/servers/deploy/configure/boundaries).
- Em seguida, continue a [configurar grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups) para associar clientes nesses limites para os servidores do sistema de sites podem utilizar.



##  <a name="BKMK_BoundaryBestPractices"></a>Melhores práticas de limites e grupos de limites  

-   **Utilize uma combinação de limites a menos que as suas necessidades:**  
   No passado, recomendamos a utilização de alguns tipos de limites através de outros utilizadores. Com as alterações para melhorar o desempenho, iremos agora Recomendamos que utilize qualquer tipo de limite ou tipos escolher que funcionam para o seu ambiente e que lhe permitem utilizam o menor número de limites, pode para simplificar as tarefas de gestão.      

-   **Evite limites de sobreposição na atribuição automática de sites:**  
     Embora cada grupo de limites suporte configurações de atribuição de site e de localização de conteúdo, é uma melhor prática criar um conjunto de grupos de limites separado a utilizar apenas na atribuição de sites. Significado: certifique-se de que cada limite num grupo de limites não é um membro de outro grupo de limites com uma atribuição de site diferente. Isto acontece porque:  

    -   Um único limite pode ser incluído em vários grupos de limites  

    -   Cada grupo de limites pode ser associado a outro site primário para atribuição de sites  

    -   Um cliente num limite que seja membro de dois grupos de limites diferentes com atribuições de sites diferentes selecionará aleatoriamente um site para associação, que pode não ser o site ao qual pretende que o cliente seja associado.  Esta configuração denomina-se limites de sobreposição.  

     Os limites de sobreposição não são um problema para a localização de conteúdo. Pelo contrário, trata-se frequentemente de uma configuração desejada que fornece aos clientes recursos adicionais ou localizações de conteúdo que podem utilizar.  
