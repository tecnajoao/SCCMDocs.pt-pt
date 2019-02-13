---
title: Utilizar limites e grupos de limites
titleSuffix: Configuration Manager
description: Utilizar limites e grupos de limites para definir localizações de rede e de sistemas de sites acessível para dispositivos que gere.
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 54aa20d5-791e-4416-9db4-5aaea472c0b7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f519762e7ba4dcc90083bc43149e18b8a444df25
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56136716"
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
-   **Localize determinadas funções de sistema de sites que podem utilizar:** Quando associa um grupo de limites a determinadas funções de sistema de sites, o grupo de limites fornece aos clientes essa lista de sistemas de sites para utilização durante a localização de conteúdo e como pontos de gestão preferenciais.  

Os clientes que estão na Internet ou configurados como clientes apenas da Internet não utilizam informações de limites. Estes clientes não podem utilizar a atribuição automática de sites e podem sempre transferir conteúdo de qualquer ponto de distribuição do seu site atribuído, quando o ponto de distribuição está configurado para permitir ligações de cliente a partir da Internet.  

**Para começar a utilizar:**
- Primeiro, [definem as localizações de rede como limites](/sccm/core/servers/deploy/configure/boundaries).
- Em seguida, continue ao [configurar grupos de limites](/sccm/core/servers/deploy/configure/boundary-groups) para associar os clientes nesses limites para os servidores do sistema de sites que podem utilizar.



##  <a name="BKMK_BoundaryBestPractices"></a> Melhores práticas para limites e grupos de limites  

- **Utilize uma combinação dos limites de menor que satisfaça as suas necessidades:**  
  No passado, recomendamos a utilização de alguns tipos de limites sobre os outros. Com as alterações para melhorar o desempenho, agora, recomendamos que usar qualquer tipo de limite ou tipos que escolher, que funcionam para seu ambiente e que permitem utilizam o menor número de limites, pode para simplificar as tarefas de gestão.      

- **Evite limites de sobreposição na atribuição automática de sites:**  
   Embora cada grupo de limites suporte configurações de atribuição de site e de localização de conteúdo, é uma melhor prática criar um conjunto de grupos de limites separado a utilizar apenas na atribuição de sites. Significado: certifique-se de que cada limite num grupo de limites não é um membro de outro grupo de limites com uma atribuição de site diferente. Isto acontece porque:  

  - Um único limite pode ser incluído em vários grupos de limites  

  - Cada grupo de limites pode ser associado a outro site primário para atribuição de sites  

  - Um cliente num limite que seja membro de dois grupos de limites diferentes com atribuições de sites diferentes selecionará aleatoriamente um site para associação, que pode não ser o site ao qual pretende que o cliente seja associado.  Esta configuração denomina-se limites de sobreposição.  

    Os limites de sobreposição não são um problema para a localização de conteúdo. Pelo contrário, trata-se frequentemente de uma configuração desejada que fornece aos clientes recursos adicionais ou localizações de conteúdo que podem utilizar.  
