---
title: Updates Publisher
titleSuffix: Configuration Manager
description: Utilizar o System Center Updates Publisher para gerir as atualizações personalizadas
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 2200b02b-e76b-4aa7-a77a-6dc5e70f1333
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2047874bb44c89e510abd52a387277e749cf65db
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/24/2019
ms.locfileid: "54896452"
---
# <a name="system-center-updates-publisher"></a>System Center Updates Publisher

*Aplica-se a: System Center Updates Publisher*

System Center Updates Publisher (Editor de atualizações) é uma ferramenta autónoma que permite que fornecedores independentes de software ou desenvolvedores de aplicativos de linha de negócio gerir as atualizações personalizadas. Isto inclui atualizações que têm dependências, como drivers e pacotes de atualizações.

Utilizar o Updates Publisher, pode:

-   Importar as atualizações de catálogos externos (catálogos de atualizações de terceiros).
-   Modificar definições de atualização, incluindo a aplicabilidade e metadados de implementação.
-   Exporte as atualizações para catálogos externos.
-   Publicar atualizações para um servidor de atualização.

Depois de publicar as atualizações para um servidor de atualização, em seguida, pode utilizar o System Center Configuration Manager para detetar e implementá-las nos dispositivos geridos.

> [!TIP]  
> A versão anterior, [System Center Updates Publisher 2011](http://go.microsoft.com/fwlink/?LinkId=848111), permanece em suporte. Essa versão atualizada mantém a mesma funcionalidade, mas oferece suporte a sistemas operativos adicionais, novos recursos para simplificar algumas tarefas e tem uma interface do usuário atualizada.

## <a name="workspaces"></a>Áreas de trabalho
Quando abre o Updates Publisher, é assumida como predefinição para o nó de descrição geral da *área de trabalho de atualizações.*

![Consola do Editor de atualizações](media/console1.png)   


Updates Publisher tem quatro áreas de trabalho para ajudar a organizá-lo.


**Área de trabalho de atualizações:** Utilize esta área de trabalho para [crie](/sccm/sum/tools/create-updates-with-updates-publisher) e [gerir](/sccm/sum/tools/manage-updates-with-updates-publisher) atualizações de software e os pacotes de atualizações. Isto inclui a atribuição de atualizações e agrupa para uma publicação, publicação e exportar para o outro repositório do Updates Publisher.

**Área de trabalho de publicações:** É aqui que [gerir publicações](/sccm/sum/tools/updates-publisher-publications). Uma publicação é o grupo de atualizações que criar para simplificar a exportação e a publicação de atualizações.

Gerir publicações inclui a publicação de atualizações para um servidor para que os clientes podem encontrar e instalá-los, exportar as atualizações e pacotes para utilização por outras instalações do Updates Publisher ou ao modificar o conteúdo do ou detalhes de uma publicação.



**Área de trabalho de regras:** É aqui que [gerir regras de aplicabilidade](/sccm/sum/tools/updates-publisher-applicability-rules) que pode ser salvo e, em seguida, utilizado com as atualizações que implementar. Existem dois tipos de regras:

-   Regras de instaláveis – estas regras ajudam a determinar se um cliente deve instalar uma atualização.
-   Instalado regras – estas regras verificar se uma atualização já está instalada.

**Área de trabalho de catálogos:** Utilize esta área de trabalho para adicionar e [gerir catálogos de atualizações de software](/sccm/sum/tools/updates-publisher-catalogs). Isto inclui a importação de atualizações de software desses catálogos para o repositório do Updates Publisher.
## <a name="first-steps"></a>Primeiras etapas
Para começar, primeiro [instale](/sccm/sum/tools/install-updates-publisher)e, em seguida [configurar opções](/sccm/sum/tools/updates-publisher-options) para o Updates Publisher.
