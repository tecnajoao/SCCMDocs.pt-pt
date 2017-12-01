---
title: Updates Publisher
titleSuffix: Configuration Manager
description: "Utilizar o System Center Updates Publisher para gerir as atualizações personalizadas"
ms.custom: na
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2200b02b-e76b-4aa7-a77a-6dc5e70f1333
caps.latest.revision: "1"
author: mstewart
ms.author: mstewart
manager: angrobe
robots: NOINDEX, NOFOLLOW
ms.openlocfilehash: ecd8811db25ea179fcdfb26f71f475710119803b
ms.sourcegitcommit: 7fe45ff75f05f7cc03ad021db8119791abe18049
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/01/2017
---
# <a name="system-center-updates-publisher"></a>O System Center Updates Publisher

*Aplica-se a: O System Center Updates Publisher*

System Center Updates Publisher (Updates Publisher) é uma ferramenta autónoma que permite que os fabricantes independentes de software ou programadores de aplicações de linha de negócio gerir as atualizações personalizadas. Isto inclui atualizações que têm dependências, como controladores e pacotes de atualização.

Utilizar o Updates Publisher, pode:

-   Importar as atualizações de catálogos externos (catálogos de atualização de terceiros).
-   Modificar definições de atualização, incluindo a aplicabilidade e metadados de implementação.
-   Exporte as atualizações para catálogos externos.
-   Publica atualizações para um servidor de atualização.

Depois de publicar as atualizações para um servidor de atualização, em seguida, pode utilizar o System Center Configuration Manager para detetar e implementar essas atualizações nos seus dispositivos geridos.

> [!TIP]  
> A versão anterior, [System Center Updates Publisher 2011](http://go.microsoft.com/fwlink/?LinkId=848111), permanece no suporte. Esta versão atualizada mantém a mesma funcionalidade, mas suporta sistemas operativos adicionais, novas funcionalidades para simplificar algumas tarefas e tem uma interface de utilizador atualizado.

## <a name="workspaces"></a>Áreas de trabalho
Quando abrir o Updates Publisher, assume como nó de descrição geral do *área de trabalho de atualizações.*

![Consola do publicador de atualizações](media/console1.png)   


Publicador de atualizações tem quatro áreas de trabalho para ajudar a organizá-lo.


**Área de trabalho de atualizações:** Utilize esta área de trabalho para [criar](/sccm/sum/tools/create-updates-with-updates-publisher) e [gerir](/sccm/sum/tools/manage-updates-with-updates-publisher) atualizações de software e os pacotes de atualizações. Isto inclui a atribuição de atualizações e os pacotes para uma publicação, publicar e exportar para o repositório do Updates Publisher outro a pedido.

**Área de trabalho publicações:** Este é onde pode [gerir publicações](/sccm/sum/tools/updates-publisher-publications). Uma publicação é o grupo de atualizações cria para simplificar a exportação e a publicação de atualizações.

Gerir publicações inclui a publicação de atualizações para um servidor para que os seus clientes podem encontrar e instalá-los, exportar as atualizações e os pacotes para utilização por outras instalações do Updates Publisher ou modificar o conteúdo ou detalhes de uma publicação.



**Área de trabalho de regras:** Segue-se onde [gerir as regras de aplicabilidade](/sccm/sum/tools/updates-publisher-applicability-rules) que pode ser guardado e, em seguida, utilizado com as atualizações que implementar. Existem dois tipos de regras:

-   As regras de instaláveis – estas regras ajudar a determinar se um cliente deve instalar uma atualização.
-   Instalado regras – estas regras, verifique se uma atualização já está instalada.

**Área de trabalho de catálogos:** Utilize esta área de trabalho para adicionar e [gerir catálogos de atualização de software](/sccm/sum/tools/updates-publisher-catalogs). Isto inclui a importação de atualizações de software desses catálogos para o repositório do Updates Publisher.
## <a name="first-steps"></a>Passos primeiro
Para começar a utilizar, primeiro [instalar](/sccm/sum/tools/install-updates-publisher)e, em seguida, [configurar opções](/sccm/sum/tools/updates-publisher-options) para o Updates Publisher.
