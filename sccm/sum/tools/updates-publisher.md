---
title: "Publicador de atualizações | Documentos do Microsoft"
description: "Utilizar o System Center Updates Publisher para gerir as atualizações personalizadas"
ms.custom: na
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2200b02b-e76b-4aa7-a77a-6dc5e70f1333
caps.latest.revision: 1
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: NOINDEX, NOFOLLOW
ms.translationtype: Machine Translation
ms.sourcegitcommit: 31819a1df4e63e1114682490a9b3c3b4e5c99cfa
ms.openlocfilehash: f4951c204b32da58174b94a539b380c278fa9756
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="system-center-updates-publisher"></a>System Center Updates Publisher

*Aplica-se a: System Center Updates Publisher*

System Center Updates Publisher (Updates Publisher) é uma ferramenta autónoma que permite fabricantes independentes de software ou programadores da aplicação de linha de negócio para gerir as atualizações personalizadas. Isto inclui atualizações que têm dependências, como controladores e pacotes de atualização.

Utilizar o Updates Publisher, pode:

-   Importar as atualizações de catálogos externos (catálogos de atualização não seja da Microsoft).
-   Modificar definições de atualização, incluindo a aplicabilidade e metadados de implementação.
-   Exporte atualizações para catálogos externos.
-   Publica atualizações para um servidor de atualização.

Depois de publicar as atualizações de um servidor de atualização, em seguida, pode utilizar o System Center Configuration Manager detetar e implementar essas atualizações nos seus dispositivos geridos.

> [!TIP]  
> A versão anterior, [System Center Updates Publisher 2011](http://go.microsoft.com/fwlink/?LinkId=848111), permanece no suporte. Esta versão atualizada mantém a mesma funcionalidade, mas suporta os sistemas operativos adicionais, novas funcionalidades para simplificar algumas tarefas e tem uma interface de utilizador atualizada.

## <a name="workspaces"></a>Áreas de trabalho
Quando abre o Updates Publisher, assume como predefinição para o nó de descrição geral da *área de trabalho atualizações.*

![Consola do publicador de atualizações](media/console1.png)   


Updates Publisher tem quatro áreas de trabalho para ajudar a organizá-lo.


**Área de trabalho de atualizações:** Utilize esta área de trabalho para [criar](/sccm/sum/tools/create-updates-with-updates-publisher) e [gerir](/sccm/sum/tools/manage-updates-with-updates-publisher) atualizações de software e os pacotes de atualização. Isto inclui a atribuição de atualizações e agrupa a uma publicação, publicar e exportar para o outro repositório do Updates Publisher.

**Área de trabalho de publicações:** Este é onde pode [gerir publicações](/sccm/sum/tools/updates-publisher-publications). Uma publicação é o grupo de atualizações que criar para simplificar a exportação e a publicação das atualizações.

Gerir publicações inclui atualizações de publicação a um servidor para que os seus clientes podem encontrar e instalá-las, exportar as atualizações e os pacotes para utilização por outras instalações Updates Publisher, ou modificar o conteúdo de ou detalhes de uma publicação.



**Área de trabalho de regras:** Eis onde pode [gerir regras de aplicabilidade](/sccm/sum/tools/updates-publisher-applicability-rules) que pode ser guardado e, em seguida, utilizada com as atualizações que implementar. Existem dois tipos de regras:

-   As regras instalável – estas regras ajudam a determinar se um cliente deve instalar uma atualização.
-   Instalado regras – estas regras a verificar se uma atualização já está instalada.

**Área de trabalho de catálogos:** Utilize esta área de trabalho para adicionar e [gerir catálogos de atualização de software](/sccm/sum/tools/updates-publisher-catalogs). Isto inclui a importação de atualizações de software a partir desses catálogos para o repositório do Updates Publisher.
## <a name="first-steps"></a>Primeiros passos
Para começar, primeiro [instalar](/sccm/sum/tools/install-updates-publisher)e, em seguida, [configurar opções](/sccm/sum/tools/updates-publisher-options) Updates Publisher.

