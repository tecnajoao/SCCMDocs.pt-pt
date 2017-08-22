---
title: "Gerir as publicações | Microsoft Docs"
description: "Gerir grupos de atualizações de software como uma publicação com o System Center Updates Publisher"
ms.custom: na
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e6c1df1d-7728-4980-9199-bc32cde5439e
caps.latest.revision: "1"
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: NOINDEX, NOFOLLOW
ms.openlocfilehash: ddea7af935d5be880b96e383401061f8aa11e6da
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="manage-publications-in-updates-publisher"></a>Gerir as publicações no publicador de atualizações

*Aplica-se a: O System Center Updates Publisher*

Pode utilizar publicações para gerir grupos de atualizações e os pacotes de como um único objeto. Isto inclui publicar as atualizações para um servidor de gestão e exportar a publicação como grupo para utilização com outra instalação do Updates Publisher.

## <a name="create-publications"></a>Criar publicações
As publicações são criadas duas formas:

-   Quando gere as atualizações e pacotes no **área de trabalho atualizações**, pode [atribuir](/sccm/sum/tools/manage-updates-with-updates-publisher#assign-updates-and-bundles-to-a-publication) -las para uma publicação novo criado nessa altura.

-   No **publicações área de trabalho** pode utilizar o **criar** botão no **publicação** separador do Friso. Este método permite-lhe criar uma publicação para utilização futura. Mais tarde, quando atribui atualizações, pode utilizar esta publicação.

## <a name="rename-a-publication"></a>Mudar o nome de uma publicação
Para mudar o nome de uma publicação, selecione a publicação a partir do **publicações área de trabalho**e, em seguida, no **publicação** separador do Friso, selecione **editar**.

## <a name="change-the-publication-type-of-updates-in-a-publication"></a>Alterar o tipo de publicação de atualizações numa publicação
Do **área de trabalho de publicação**, pode modificar o **tipo publicação** das atualizações e os pacotes que são atribuídos a uma publicação.

1. Selecione a publicação que contenha as atualizações que pretende modificar e, em seguida, selecione um ou mais atualizações ou pacotes do **todos os &lt;nome da publicação > Membro atualizações** lista.

2. Em seguida, no **home page** separador, escolha uma das seguintes opções. As opções disponíveis dependem do tipo de publicação de atualizações que selecionou.

  -   **Automática**
  -   **Conteúdo completo**
  -   **Metadados apenas**

Depois de efetuar uma alteração, poderá ter de atualizar a vista de publicação para ver os novos valores.

Para obter informações sobre os tipos de publicação diferentes, consulte [atribuir as atualizações e os pacotes para uma publicação](/sccm/sum/tools/manage-updates-with-updates-publisher#assign-updates-and-bundles-to-a-publication).

> [!TIP]    
> Quando definir o tipo de publicação de um pacote, todas as atualizações de software nesse grupo são publicadas com o tipo de publicação desse pacote.

## <a name="remove-updates-from-a-publication"></a>Remover as atualizações de uma publicação
Remover as atualizações ou pacotes de uma publicação, o **publicações área de trabalho** selecione a publicação que pretende modificar e, em seguida, selecione as atualizações e pacotes que pretende remover. Em seguida, no **home page** separador do Friso, selecione **remover**.

Depois das atualizações são removidas da publicação, permanecem disponíveis no repositório de Updates Publisher.

## <a name="publish-publications"></a>Publicar publicações
Ao publicar as atualizações e pacotes, Updates Publisher adiciona informações sobre as atualizações de pacotes (metadados) e, possivelmente, os binários das atualizações (conteúdo completo), de um servidor de atualização para implementação em dispositivos.

Antes de ter a opção de publicar, tem de configurar o [servidor de atualização](/sccm/sum/tools/updates-publisher-options#update-server) opção para o Updates Publisher. Para abrir esta opção de configuração, aceda a **área de trabalho atualizações** &gt; **descrição geral** e selecione **configurar o WSUS e o certificado de assinatura.** Pode também aceder à página servidor de atualização nas opções do Updates Publisher.

> [!NOTE]   
> Publicador de atualizações só pode publicar as atualizações que estão 375 megabytes (MB) ou tamanho.

### <a name="to-publish-a-publication"></a>Para publicar uma publicação

1.  Vá para o **publicações área de trabalho**e, em seguida, selecione uma publicação que contém o grupo de atualizações e os pacotes que pretende publicar ou exportar. Em seguida, escolha **publicar** de **home page** separador do Friso.

2.  No **selecione** página do **publicar** assistente, pode optar por assinar todas as atualizações com um novo certificado de publicação, mas não é possível alterar o tipo de publicação.

3.  Conclua o assistente.

  Se falhar a publicação, são apresentadas com uma ligação para o ficheiro de UpdatesPublisher.log que pode fornecer mais informações.

## <a name="export-a-publication"></a>Exportar uma publicação
Pode exportar uma publicação do seu repositório do Updates Publisher. Se o fizer, exporta as atualizações e os pacotes são atribuídos a esse publicação, que cria um catálogo de atualização. Pode, em seguida, [adicionar](/sccm/sum/tools/updates-publisher-catalogs#add-software-update-catalogs) e, em seguida, [importar](/sccm/sum/tools/updates-publisher-catalogs#mport-updates) esse catálogo noutra instância do Updates Publisher. Também pode [exportar atualizações](/sccm/sum/tools/manage-updates-with-updates-publisher#export-updates) que não fazem parte de uma publicação.

Para exportar uma publicação, vá para o **publicações área de trabalho** e selecione a publicação que contém as atualizações que pretende exportar. Só pode selecionar uma publicação de cada vez.

Com a publicação selecionada, escolher **exportar** do **home page** separador do Friso e, em seguida, forneça um caminho e nome de ficheiro para a exportação de catálogo.

Também tem a opção para exportar (incluem) atualizações de software dependentes como parte da exportação.

## <a name="rename-a-publication"></a>Mudar o nome de uma publicação
Para mudar o nome de uma publicação, selecione a publicação de **publicações área de trabalho**e, em seguida, escolha **editar** do **publicação** separador do Friso.

## <a name="delete-a-publication"></a>Eliminar uma publicação
Para eliminar uma publicação, selecione a publicação de **publicações área de trabalho**e, em seguida, escolha **eliminar** do **publicação** separador do Friso.

Após a publicação é removida do Updates Publisher, as atualizações que foram na publicação permanecem disponíveis no repositório de Updates Publisher.

## <a name="expire-or-reactivate-updates-and-bundles"></a>Expirar ou reativar atualizações e pacotes
Pode utilizar o **área de trabalho atualizações** para selecionar e, em seguida, expirar ou reativar atualizações e pacotes. Pode expirar e reativar as atualizações e os pacotes tantas vezes quanto que escolher.

-   **Expirar atualizações ou pacotes**, na, selecione a área de trabalho de atualizações uma ou mais atualizações ou bundles que não expiraram e, em seguida, escolha **expirar** do **home page** separador. Depois de publicar a atualização ou pacote como expirados para o Configuration Manager, pode reativá-lo.

    Antes de poder remover (eliminar) personalizadas atualização ou pacote do Configuration Manager, tem de expirá-lo e, em seguida, publicar esse estado expirado para o Configuration Manager. Depois das atualizações ou pacotes expiraram no Configuration Manager, já não pode implementar ou reativar a atualização ou pacote.

-   **Para reativar atualizações ou pacotes**, na área de trabalho de atualizações, selecione uma ou mais atualizações que expiraram em, em seguida, escolha **reativar** do **home page** separador do Friso. Se a atualização expirada anteriormente foi publicada como expirados para o Configuration Manager, não pode reativá-lo.
