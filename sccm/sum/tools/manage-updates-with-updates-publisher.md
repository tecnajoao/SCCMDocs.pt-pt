---
title: Gerir atualizações
titleSuffix: Configuration Manager
description: Gerir o ID={0 implementar e criar com o System Center Updates Publisher
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: cd64994c-b426-4465-96cd-54b0edc2778d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4de365b7df3a18abdfc5a92e9516bad84818ac35
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/24/2019
ms.locfileid: "54896751"
---
# <a name="manage-software-updates-in-updates-publisher"></a>Gerir atualizações de software Updates Publisher

*Aplica-se a: System Center Updates Publisher*     

System Center Updates Publisher, vai utilizar o **espaço de trabalho atualizações** para gerir atualizações de software e os pacotes que tenha importado para o repositório.  

Tarefas de gestão incluem duplicar, editar e prestes a expirar ou reativar as atualizações e pacotes e atribuição de atualizações e tamanho dos pacotes de publicações. Também pode exportar catálogos personalizados para utilização com outras instalações do Updates Publisher.

Para obter atualizações que podem ser geridos:
-  [Adicionar um catálogo de atualização](/sccm/sum/tools/updates-publisher-catalogs#add-software-update-catalogs) à sua instalação do Updates Publisher
-  [Importar](/sccm/sum/tools/updates-publisher-catalogs#import-updates) as atualizações a partir desse catálogo para o seu repositório.

Também pode [criar suas próprias atualizações](/sccm/sum/tools/create-updates-with-updates-publisher).



## <a name="create-a-duplicate-of-an-update"></a>Criar um duplicado de uma atualização
Pode criar duplicados ou cópias, de atualizações que estão no seu repositório. Em seguida, pode modificar a cópia em vez de modificar a atualização original. Não é possível criar cópias de pacotes de atualizações.

Para criar uma cópia, selecione uma atualização no **atualiza a área de trabalho**e, em seguida, escolha **duplicar**. A cópia da atualização é apresentado na mesma localização na área de trabalho de atualizações com *copiar de* adicionado ao nome.

Uma nova cópia criou tem o estado **Unexpired**, mas caso contrário, mantém as definições do original.

## <a name="edit-updates-and-bundles"></a>Atualizações de edição e de pacotes
Pode selecionar as atualizações e pacotes que estão no seu repositório de modificá-las.

Na **área de trabalho de atualizações** Selecione uma atualização ou pacote e, em seguida, selecione **editar** do **home page** separador para abrir o Assistente de edição. Atualizações e pacotes possuem assistentes de separado mas intimamente relacionados que apresentam as mesmas opções que o [criar atualizar](/sccm/sum/tools/create-updates-with-updates-publisher#the-create-update-wizard) ou [criar pacote](/sccm/sum/tools/create-updates-with-updates-publisher#the-create-bundle-wizard) assistentes.

Durante a edição, pode alterar os detalhes disponíveis sobre a atualização ou agrupar para que possa ser utilizado no seu ambiente. Por exemplo, pode editar as regras de aplicabilidade ou precedência ou alterar o idioma. Também pode alterar o produto e o fornecedor para mover a atualização ou agrupar para uma pasta personalizada para atualizações de grupo para sua utilização.

## <a name="assign-updates-and-bundles-to-a-publication"></a>Atribuir as atualizações e pacotes para uma publicação
Pode selecionar as atualizações e pacotes no **área de trabalho de atualizações** e, em seguida, escolha **atribuir** partir o **home page** separador do friso para adicioná-los para uma publicação. Esta ação inicia o **atualizações de Software atribuir** assistente.
-  Ver [publicar atualizações e pacotes](#publish-updates-and-bundles-from-the-updates-workspace) para obter informações sobre como selecionar e publicar as atualizações e pacotes como uma única tarefa.
-  Ver [gerir publicações](/sccm/sum/tools/updates-publisher-publications) para obter informações sobre como gerir grupos de atualizações e pacotes como um único objeto. Depois de atribuir as atualizações para uma publicação, pode gerir essa publicação, que por sua vez inclui todas as atualizações atribuídas.

Se atribuir atualizações para uma publicação:

-   Pode incluir atualizações expiradas e não expirada e pacotes na mesma publicação.

-   Especifique o tipo de publicação:

    -   **Total de conteúdo** – isso publica o conteúdo completo da atualização com o servidor WSUS. Isto inclui metadados e os binários de atualização.

    -   **Apenas os metadados de** – isso publica apenas os metadados; binários de atualização não são publicados. Poderá escolher esta opção quando pretender recolher dados de conformidade.

    -   **Automática** – esse modo está disponível apenas depois de ligar o Updates Publisher para o Configuration Manager (consulte a [servidor do ConfigMgr](/sccm/sum/tools/updates-publisher-options#configmgr-server) opção.)

    Com esse tipo, o Updates Publisher consultas no Configuration Manager para determinar se as atualizações ou pacotes devem ser publicados com o conteúdo completo ou apenas metadados. Conteúdo completas para uma atualização é publicada apenas quando atualizar que cumpre os **limiar de contagem de cliente pedida** e **limiar de tamanho de origem do pacote,** que são especificados no **servidor do ConfigMgr**  página Opções do Updates Publisher.

-   Selecione uma publicação:

    -   Utilizar **atribuir a atualização de software para publicações existentes** quando já tiver criado uma publicação que pretende utilizar. Esta opção não está disponível até que existe pelo menos uma publicação.

    -   Uso **atribuir a atualização de software para uma nova publicação** quando não tiver uma publicação adequada. Isto irá criar uma nova publicação com o nome que especificar.

Depois de atribuir as atualizações para uma publicação, pode utilizar o **área de trabalho de publicação** ao [publicar](/sccm/sum/tools/updates-publisher-publications#publish-pubilcations) ou [exportar](/sccm/sum/tools/updates-publisher-publications#export-a-pubilcation) a publicação como um grupo.

## <a name="publish-updates-and-bundles-from-the-updates-workspace"></a>Publicar atualizações e pacotes a partir da área de trabalho de atualizações
Quando publica atualizações e pacotes, o Updates Publisher adiciona informações sobre essas atualizações e pacotes (metadados) e, possivelmente, os binários para as atualizações (conteúdo completo), para um servidor de atualização para implementação em dispositivos.

Antes de ter a opção de publicar, tem de configurar o [servidor de atualização](/sccm/sum/tools/updates-publisher-options#update-server) opção para o Updates Publisher. Para abrir esta opção de configuração, aceda a **área de trabalho de atualizações** &gt; **descrição geral** e selecione **configurar o WSUS e o certificado de assinatura.** Pode também aceder à página do servidor de atualização nas opções do Updates Publisher.

Existem duas formas de publicar as atualizações e pacotes:
-   Diretamente a partir do espaço de trabalho atualizações. (Consulte o procedimento seguinte, *para publicar as atualizações e pacotes*.)
-   Como um [publicação](/sccm/sum/tools/updates-publisher-publications#publish-pubilcations) da área de trabalho de publicações.  

> [!NOTE]   
> Publicador de atualizações pode publicar somente as atualizações que estão 375 megabytes (MB) ou de tamanho.

### <a name="to-publish-updates-and-bundles"></a>Para publicar as atualizações e pacotes
1.  Aceda a **espaço de trabalho atualizações** e selecione um ou mais atualizações e pacotes que pretende publicar. Em seguida, escolha **Publish** partir **home page** separador do Friso.

2.  Sobre o **selecionar** página do **publicar** assistente, selecione como pretende publicar as atualizações. As opções são os mesmos que para [atribuição de atualizações](#assign-updates-and-bundles-to-a-publication): **Total de conteúdo**, **apenas os metadados**, ou **automática**.

    Também pode optar por inscrever-se a todas as atualizações com um novo certificado de publicação.

3.  Conclua o assistente.

Se falhar a publicação, são apresentados com uma ligação para o ficheiro de UpdatesPublisher.log que pode fornecer mais informações.

## <a name="export-updates"></a>Atualizações de exportação
Pode exportar as atualizações e pacotes do seu repositório do Updates Publisher para criar um catálogo de atualizações personalizadas. Em seguida, pode [adicione](/sccm/sum/tools/updates-publisher-catalogs#add-software-update-catalogs) e, em seguida [importar](/sccm/sum/tools/updates-publisher-catalogs#mport-updates) esse catálogo para outra instância do Updates Publisher. (Também pode [exportar atualizações como uma publicação](/sccm/sum/tools/updates-publisher-publications##export-a-publication).)

Para exportar diretamente, aceda a **área de trabalho de atualizações** > **todas as atualizações de Software** e selecione um ou mais atualizações e pacotes. Não é possível exportar um fornecedor ou a pasta de produto, mas pode selecionar uma pasta e, em seguida, selecione as atualizações nessa pasta para exportação.

Com uma ou mais atualizações selecionadas, escolha **exportar** partir do **home page** separador do Friso e, em seguida, forneça um nome e caminho para a exportação de catálogo.

Terá a opção para exportar (incluir) as atualizações de software dependentes.

## <a name="delete-updates-and-bundles"></a>Elimine as atualizações e pacotes
Pode eliminar as atualizações e pacotes de atualizações para removê-los a partir do repositório do Updates Publisher.

Aceda a **área de trabalho de atualizações** > **todas as atualizações de Software** e selecione uma ou mais atualizações individuais. Em seguida, escolha **elimine** da **home page** separador do Friso.

-   Se a sua seleção contém apenas atualizações ou pacotes não foram publicados ou que estão a expirou, será solicitado a confirmar a eliminação antes dos mesmos serão removidos.

-   Se sua seleção incluir uma atualização ou um pacote que foi publicado e ainda não tenha expirado, tem um aviso. Deve [expirar](/sccm/sum/tools/updates-publisher-pubilcations#expire-or-reactivate-updates-and-bundles) essas atualizações e, em seguida, publicar essa alteração antes de eliminá-los do repositório.  

Se eliminar uma atualização ou de um fornecedor do pacote e, em seguida, importe esse catálogo novamente, essa atualização é restaurada para o seu repositório.

## <a name="manage-vendor-and-product-folders"></a>Gerir o fornecedor e as pastas de produto
Para ver uma lista de fornecedores e produtos para cada fornecedor para o qual tem importados ou criados atualizações, aceda a **área de trabalho de atualizações** > **descrição geral** > **todos os Atualizações de software**.

Pastas de fornecedores e os produtos são criadas automaticamente pelo Updates Publisher quando utiliza um Assistente para importar ou criar uma atualização de software ou o pacote. Também pode criar essas pastas manualmente.

-   Para criar uma pasta de fornecedor, no painel de navegação do **área de trabalho atualizações**, clique com o botão direito no **todas as atualizações de Software**e, em seguida, escolha **criar fornecedor**.

-   Para criar uma pasta de produto numa pasta de fornecedor, clique com o botão direito na pasta de fornecedor e escolha **produto criar**.

Além de criar pastas, pode renomear ou excluir qualquer fornecedor ou a pasta product no seu repositório. Para fazê-lo, clique com o botão direito na pasta e escolha a opção que pretende, **mudar o nome** ou **eliminar**. Eliminar uma pasta remove todas as atualizações e pacotes nessa pasta e respetivos pastas de produto a partir do repositório do Updates Publisher.

Pode mover as atualizações entre fornecedores e pastas de produto, incluindo a pastas que cria. Para mover uma atualização ou para uma nova pasta do pacote, tem de selecionar e, em seguida **editar** a atualização ou pacote. Em seguida, no **informações** página do Assistente de atualização de editar pode reatribuir o fornecedor e o produto. Quando o **editar atualizar** assistente é concluído, a alteração aplica-se e a atualização se move para a nova pasta.

## <a name="view-the-xml-of-an-update-or-bundle"></a>Ver o XML de uma atualização ou pacote
Pode selecionar uma única atualização ou do pacote no **atualiza a área de trabalho** e, em seguida, escolha **vista** XML para apresentar a estrutura do XML da atualização. Não há opções para editar a estrutura XML diretamente.
