---
title: "Gerir as atualizações"
titleSuffix: Configuration Manager
description: "Gerir as atualizações que implementar e criar com o System Center Updates Publisher"
ms.custom: na
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cd64994c-b426-4465-96cd-54b0edc2778d
caps.latest.revision: "1"
author: mestew
ms.author: mstewart
manager: angrobe
robots: NOINDEX, NOFOLLOW
ms.openlocfilehash: b6e2f2a117613087cd3ef561391cdcf665f0db6a
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/04/2017
---
# <a name="manage-software-updates-in-updates-publisher"></a>Gerir atualizações de software Updates Publisher

*Aplica-se a: O System Center Updates Publisher*     

No System Center Updates Publisher, utilize o **área de trabalho atualizações** para gerir atualizações de software e os pacotes que importou para o repositório.  

Tarefas de gestão incluem duplicar, editar e prestes a expirar ou reativar atualizações e pacotes e atribuição de atualizações e os pacotes para publicações. Também pode exportar catálogos personalizados para utilização com outras instalações do Updates Publisher.

Para obter as atualizações que pode gerir:
-  [Adicionar um catálogo de atualização](/sccm/sum/tools/updates-publisher-catalogs#add-software-update-catalogs) à sua instalação do Updates Publisher
-  [Importar](/sccm/sum/tools/updates-publisher-catalogs#import-updates) as atualizações de que o catálogo para o seu repositório.

Também pode [criar as suas próprias atualizações](/sccm/sum/tools/create-updates-with-updates-publisher).



## <a name="create-a-duplicate-of-an-update"></a>Criar um duplicado de uma atualização
Pode criar os duplicados ou cópias, de atualizações que estão no seu repositório. Em seguida, pode modificar a cópia em vez de modificar a atualização original. Não é possível criar cópias de pacotes de atualização.

Para criar uma cópia, selecione uma atualização no **atualiza a área de trabalho**e, em seguida, escolha **duplicado**. A cópia da atualização é apresentado na mesma localização na área de trabalho de atualizações com *copiar de* adicionadas para o seu nome.

Uma nova cópia cria tem um Estado de **Unexpired**, mas mantém caso contrário, as definições do original.

## <a name="edit-updates-and-bundles"></a>Editar as atualizações e pacotes
Pode selecionar as atualizações e os pacotes que estão no seu repositório modificá-las.

No **área de trabalho atualizações** Selecione uma atualização ou pacote e, em seguida, selecione **editar** do **home page** separador para abrir o Assistente de edição. Atualizações e os pacotes têm separados mas estritamente relacionadas com assistentes que apresentam as mesmas opções como o [criar atualizar](/sccm/sum/tools/create-updates-with-updates-publisher#the-create-update-wizard) ou [criar pacote](/sccm/sum/tools/create-updates-with-updates-publisher#the-create-bundle-wizard) assistentes.

Ao editar, pode alterar qualquer detalhes disponíveis sobre a atualização ou agrupar para que possa ser utilizado no seu ambiente. Por exemplo, pode editar as regras de aplicabilidade ou precedência ou alterar o idioma. Também pode alterar o produto e fabricante para mover a atualização ou agrupar para uma pasta personalizada para as atualizações de grupo para utilização própria.

## <a name="assign-updates-and-bundles-to-a-publication"></a>Atribuir as atualizações e os pacotes para uma publicação
Pode selecionar as atualizações e pacotes no **área de trabalho atualizações** e, em seguida, escolha **atribuir** do **home page** separador do friso para adicioná-los para uma publicação. Esta ação inicia o **atribuir as atualizações de Software** assistente.
-  Consulte [publicar as atualizações e os pacotes](#publish-updates-and-bundles-from-the-updates-workspace) para obter informações sobre como selecionar e publicar atualizações e os pacotes de como uma única tarefa.
-  Consulte [gerir publicações](/sccm/sum/tools/updates-publisher-publications) para obter informações sobre como gerir grupos de atualizações e os pacotes de como um único objeto. Depois de atribuir as atualizações para uma publicação, pode gerir essa publicação, que por sua vez inclui todas as atualizações atribuídas.

Se atribuir atualizações para uma publicação:

-   Pode incluir atualizações expiradas e não expirou e os pacotes na mesma publicação.

-   Especifique o tipo de publicação:

    -   **Total de conteúdo** – isto publica o conteúdo completo da atualização com o servidor WSUS. Isto inclui os metadados e os binários da atualização.

    -   **Apenas metadados** – isto publica apenas os metadados; os binários de atualização não são publicados. Poderá escolher esta opção quando pretender recolher dados de conformidade.

    -   **Automática** – este modo estará disponível apenas quando tiver estabelecido ligação Updates Publisher para o Configuration Manager (consulte o [servidor do ConfigMgr](/sccm/sum/tools/updates-publisher-options#configmgr-server) opção.)

    Com este tipo, o Updates Publisher consulta do Configuration Manager para determinar se as atualizações ou pacotes devem ser publicados com conteúdo completo ou apenas de metadados. Conteúdo completas para uma atualização é publicada apenas quando atualizar que cumpre os o **limiar de contagem de cliente pedida** e **limiar de tamanho de origem do pacote,** que são especificados no **servidor do ConfigMgr** página Opções do Updates Publisher.

-   Selecione uma publicação:

    -   Utilizar **atribuir a atualização de software para publicações existentes** quando que já criou uma publicação que pretende utilizar. Esta opção não está disponível até que existe pelo menos uma publicação.

    -   Utilize **atribuir a atualização de software para uma publicação novo** quando não tiver uma publicação adequada. Esta ação irá criar uma nova publicação com o nome que especificar.

Depois de atribuir as atualizações para uma publicação, pode utilizar o **área de trabalho de publicação** para [publicar](/sccm/sum/tools/updates-publisher-publications#publish-pubilcations) ou [exportar](/sccm/sum/tools/updates-publisher-publications#export-a-pubilcation) a publicação como um grupo.

## <a name="publish-updates-and-bundles-from-the-updates-workspace"></a>Publicar as atualizações e pacotes a partir da área de trabalho de atualizações
Ao publicar as atualizações e pacotes, Updates Publisher adiciona informações sobre as atualizações de pacotes (metadados) e, possivelmente, os binários das atualizações (conteúdo completo), de um servidor de atualização para implementação em dispositivos.

Antes de ter a opção de publicar, tem de configurar o [servidor de atualização](/sccm/sum/tools/updates-publisher-options#update-server) opção para o Updates Publisher. Para abrir esta opção de configuração, aceda a **área de trabalho atualizações** &gt; **descrição geral** e selecione **configurar o WSUS e o certificado de assinatura.** Pode também aceder à página servidor de atualização nas opções do Updates Publisher.

Existem duas formas de publicar as atualizações e os pacotes:
-   Diretamente a partir da área de trabalho de atualizações. (Consulte o procedimento seguinte, *para publicar as atualizações e os pacotes*.)
-   Como um [publicação](/sccm/sum/tools/updates-publisher-publications#publish-pubilcations) da área de trabalho de publicações.  

> [!NOTE]   
> Publicador de atualizações só pode publicar as atualizações que estão 375 megabytes (MB) ou tamanho.

### <a name="to-publish-updates-and-bundles"></a>Para publicar as atualizações e pacotes
1.  Aceda a **área de trabalho atualizações** e selecione um ou mais atualizações e os pacotes que pretende publicar. Em seguida, escolha **publicar** de **home page** separador do Friso.

2.  No **selecione** página do **publicar** assistente, selecione como pretende publicar as atualizações. As opções são os mesmos que para [atribuir atualizações](#assign-updates-and-bundles-to-a-publication): **Total de conteúdo**, **apenas metadados**, ou **automática**.

    Também pode optar por assinar todas as atualizações com um novo certificado de publicação.

3.  Conclua o assistente.

Se falhar a publicação, são apresentadas com uma ligação para o ficheiro de UpdatesPublisher.log que pode fornecer mais informações.

## <a name="export-updates"></a>Atualizações de exportação
Pode exportar as atualizações e os pacotes do seu repositório do Updates Publisher para criar um catálogo de atualizações personalizadas. Em seguida, pode [adicionar](/sccm/sum/tools/updates-publisher-catalogs#add-software-update-catalogs) e, em seguida, [importar](/sccm/sum/tools/updates-publisher-catalogs#mport-updates) esse catálogo noutra instância do Updates Publisher. (Também pode [exportar atualizações como uma publicação](/sccm/sum/tools/updates-publisher-publications##export-a-publication).)

Para exportar diretamente, aceda a **área de trabalho atualizações** > **todas as atualizações de Software** e selecione um ou mais atualizações e pacotes. Não é possível exportar um fornecedor ou a pasta de produto, mas pode selecionar uma pasta e, em seguida, selecione as atualizações nessa pasta para exportação.

Um ou mais das atualizações selecionadas, escolha **exportar** do **home page** separador do Friso e, em seguida, forneça um caminho e nome de ficheiro para a exportação de catálogo.

Terá a opção para exportar (incluem) atualizações de software dependentes.

## <a name="delete-updates-and-bundles"></a>Elimine as atualizações e pacotes
Pode eliminar as atualizações e os pacotes de atualizações a removê-los a partir do repositório Updates Publisher.

Aceda a **área de trabalho atualizações** > **todas as atualizações de Software** e selecione uma ou mais atualizações individuais. Em seguida, escolha **eliminar** do **home page** separador do Friso.

-   Se a sua seleção contém apenas atualizações ou pacotes não foram publicados ou que são expirado, é-lhe pedido para confirmar a eliminação antes dos mesmos serão removidos.

-   Se a seleção incluir uma atualização ou o pacote que foi publicado e ainda não expirou, recebem um aviso. Deve [expirar](/sccm/sum/tools/updates-publisher-pubilcations#expire-or-reactivate-updates-and-bundles) essas atualizações e, em seguida, publicar essa alteração antes de eliminá-los do repositório.  

Se eliminar uma atualização ou de um fornecedor do pacote e, em seguida, importar esse catálogo novamente, essa atualização está restaurada para o seu repositório.

## <a name="manage-vendor-and-product-folders"></a>Gerir pastas de produto e fabricante
Para ver uma lista de fornecedores e produtos para cada fornecedor para o qual tem importados ou criados atualizações, aceda a **área de trabalho atualizações** > **descrição geral** > **todas as atualizações de Software**.

Pastas para os fornecedores e produtos são criadas automaticamente pelo publicador de atualizações quando utiliza um Assistente para importar ou criar uma atualização de software ou pacote. Também pode criar estas pastas manualmente.

-   Para criar uma pasta de fornecedor, no painel de navegação do **área de trabalho atualizações**, faça duplo clique no **todas as atualizações de Software**e, em seguida, escolha **criar fornecedor**.

-   Para criar uma pasta do produto na pasta fornecedor, clique com o botão direito na pasta de fornecedor e escolha **criar produto**.

Para além de criar pastas, pode mudar o nome ou eliminar qualquer fornecedor ou a pasta de produto no seu repositório. Para fazê-lo, clique com o botão direito na pasta e escolha a opção que pretende, **mudar o nome** ou **eliminar**. Eliminar uma pasta remove todas as atualizações e os pacotes na pasta e respetivas pastas de produto do repositório Updates Publisher.

Pode mover atualizações entre o fornecedor e pastas de produto, incluindo a pastas que cria. Para mover uma atualização ou para uma nova pasta do pacote, tem de selecionar e, em seguida, **editar** a atualização ou pacote. Em seguida, no **informações** página do Assistente de atualização de editar pode reatribuir o fabricante e produto. Quando o **editar atualizar** assistente estiver concluído, a alteração aplica-se e a atualização é movido para a nova pasta.

## <a name="view-the-xml-of-an-update-or-bundle"></a>Ver o XML de uma atualização ou pacote
Pode selecionar uma única atualização ou agrupar no **atualiza a área de trabalho** e, em seguida, escolha **vista** XML para apresentar a estrutura XML de que a atualização. Não existem não existem opções para editar diretamente a estrutura XML.
