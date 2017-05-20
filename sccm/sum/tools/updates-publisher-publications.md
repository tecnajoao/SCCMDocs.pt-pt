---
title: "Gerir publicações | Documentos do Microsoft"
description: "Gerir grupos de atualizações de software como uma publicação com o System Center Updates Publisher"
ms.custom: na
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e6c1df1d-7728-4980-9199-bc32cde5439e
caps.latest.revision: 1
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: NOINDEX, NOFOLLOW
ms.translationtype: Machine Translation
ms.sourcegitcommit: 31819a1df4e63e1114682490a9b3c3b4e5c99cfa
ms.openlocfilehash: ddea7af935d5be880b96e383401061f8aa11e6da
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="manage-publications-in-updates-publisher"></a>Gerir publicações no Updates Publisher

*Aplica-se a: System Center Updates Publisher*

Pode utilizar publicações para gerir grupos de atualizações e os pacotes de como um único objeto. Isto inclui publicar as atualizações de um servidor de gestão e exportar a publicação como grupo para utilização com outra instalação do Updates Publisher.

## <a name="create-publications"></a>Criar publicações
Publicações são criadas duas formas:

-   Quando gerir atualizações e os pacotes de no **área de trabalho atualizações**, pode [atribuir](/sccm/sum/tools/manage-updates-with-updates-publisher#assign-updates-and-bundles-to-a-publication) -los para uma nova publicação que é criada nesse momento.

-   No **área de trabalho de publicações,** pode utilizar o **criar** botão a **publicação** separador do Friso. Este método permite-lhe criar uma publicação para utilização futura. Mais tarde, quando atribui atualizações, pode utilizar esta publicação.

## <a name="rename-a-publication"></a>Mudar o nome de uma publicação
Para mudar o nome de uma publicação, selecione a publicação a partir do **publicações área de trabalho**e, em seguida, no **publicação** separador do Friso, selecione **editar**.

## <a name="change-the-publication-type-of-updates-in-a-publication"></a>Alterar o tipo de publicação de atualizações de uma publicação
A partir de **área de trabalho de publicação**, pode modificar o **tipo de publicação** das atualizações e os pacotes que são atribuídos a uma publicação.

1. Selecione a publicação que contenha as atualizações que pretende modificar e, em seguida, selecione um ou mais atualizações ou pacotes a partir de **todos os &lt;nome da publicação > as atualizações de membros** lista.

2. Em seguida, no **base** separador, escolha uma das seguintes opções. As opções que estão disponíveis dependem do tipo de publicação de atualizações que selecionou.

  -   **Automática**
  -   **Conteúdo completo**
  -   **Metadados apenas**

Depois de efetuar uma alteração, poderá ter de actualizar a vista de publicação para ver os novos valores.

Para obter informações sobre os tipos de publicação diferente, consulte o artigo [atribuir atualizações e os pacotes para uma publicação](/sccm/sum/tools/manage-updates-with-updates-publisher#assign-updates-and-bundles-to-a-publication).

> [!TIP]    
> Quando definir o tipo de publicação de um pacote, todas as atualizações de software esse pacote são publicadas com o tipo de publicação desse agrupamento.

## <a name="remove-updates-from-a-publication"></a>Remover as atualizações de uma publicação
Remover as atualizações ou pacotes a partir de uma publicação, a **publicações área de trabalho** selecione a publicação que pretende modificar e, em seguida, selecione as atualizações e os pacotes que pretende remover. Em seguida, no **base** separador do Friso, selecione **remover**.

Após as atualizações são removidas de uma publicação, estes permanecem disponíveis no repositório de Updates Publisher.

## <a name="publish-publications"></a>Publicar publicações
Quando publica atualizações e os pacotes, o Updates Publisher adiciona informações sobre as atualizações de pacotes (metadados) e possivelmente os binários para as atualizações (conteúdo completo), para um servidor de atualização para a implementação nos dispositivos.

Antes de ter a opção de publicação, tem de configurar o [servidor de atualização](/sccm/sum/tools/updates-publisher-options#update-server) opção Updates Publisher. Para abrir esta opção de configuração, aceda a **área de trabalho atualizações** &gt; **descrição geral** e selecione **configurar o WSUS e o certificado de assinatura.** Pode também aceder à página de servidor de atualização nas opções do Updates Publisher.

> [!NOTE]   
> Updates Publisher só pode publicar as atualizações que sejam 375 megabytes (MB) ou menos em tamanho.

### <a name="to-publish-a-publication"></a>Para publicar uma publicação

1.  Aceda ao **publicações área de trabalho**e, em seguida, selecione uma publicação que contém o grupo de atualizações e os pacotes que pretende publicar ou exportar. Em seguida, escolha **publicar** de **base** separador do Friso.

2.  No **selecione** página do **publicar** assistente pode escolher assinar todas as atualizações com um novo certificado de publicação, mas não é possível alterar o tipo de publicação.

3.  Conclua o assistente.

  Se falhar a publicação, são apresentadas com uma ligação para o ficheiro de UpdatesPublisher.log que pode fornecer mais informações.

## <a name="export-a-publication"></a>Exportar uma publicação
Pode exportar uma publicação do seu repositório do Updates Publisher. Se o fizer, as exportações as atualizações e os pacotes que são atribuídos a essa publicação e cria um catálogo de atualização. Em seguida, pode [adicionar](/sccm/sum/tools/updates-publisher-catalogs#add-software-update-catalogs) e, em seguida, [importar](/sccm/sum/tools/updates-publisher-catalogs#mport-updates) esse catálogo para outra instância do Updates Publisher. Também pode [exportar atualizações](/sccm/sum/tools/manage-updates-with-updates-publisher#export-updates) que não fazem parte de uma publicação.

Para exportar uma publicação, vá para o **publicações área de trabalho** e selecione a publicação que contém as atualizações que pretende exportar. Só pode selecionar uma publicação de cada vez.

Com a publicação selecionada, escolher **exportar** a partir de **base** separador do Friso e, em seguida, forneça um caminho e nome de ficheiro para a exportação de catálogo.

Tem também a opção de exportação (incluir) atualizações de software dependentes como parte da exportação.

## <a name="rename-a-publication"></a>Mudar o nome de uma publicação
Para mudar o nome de uma publicação, selecione a publicação de **publicações área de trabalho**e, em seguida, escolha **editar** a partir do **publicação** separador do Friso.

## <a name="delete-a-publication"></a>Eliminar uma publicação
Para eliminar uma publicação, selecione a publicação de **publicações área de trabalho**e, em seguida, escolha **eliminar** a partir do **publicação** separador do Friso.

Após a publicação é removida do Updates Publisher, as atualizações que foram na publicação permanecem disponíveis no repositório de Updates Publisher.

## <a name="expire-or-reactivate-updates-and-bundles"></a>Expirar ou reativar atualizações e os pacotes
Pode utilizar o **área de trabalho atualizações** para selecionar e, em seguida, expirar ou reativar atualizações e os pacotes. Pode expirar e reativar as atualizações e os pacotes de tantas vezes quanto que escolher.

-   **Para expirar atualizações ou pacotes**, na selecionar área de trabalho atualizações um ou mais atualizações ou agrupa que não são expirou e, em seguida, selecione **expirar** a partir do **base** separador. Quando a publicar o pacote como expirada ao Configuration Manager ou a atualização, pode reativá-lo.

    Antes de poder remover atualização (delete) um personalizado ou pacote do Configuration Manager, tem de expirá-lo e, em seguida, publicar estado expirado para o Configuration Manager. Depois de atualizações ou pacotes expirem no Configuration Manager, que já não pode implementar ou reativar o pacote ou atualização.

-   **Para reativar as atualizações ou pacotes**, na área de trabalho de atualizações, selecione uma ou mais atualizações que são expiradas e, em seguida, escolha **reativar** a partir do **base** separador do Friso. Se a atualização expirada anteriormente foi publicada como expirada ao Configuration Manager, não pode reativá-la.

