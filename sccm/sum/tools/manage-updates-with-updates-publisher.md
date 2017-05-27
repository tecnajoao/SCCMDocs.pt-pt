---
title: "Gerir atualizações | Documentos do Microsoft"
description: "Gerir as atualizações que implementar e criar com o System Center Updates Publisher"
ms.custom: na
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cd64994c-b426-4465-96cd-54b0edc2778d
caps.latest.revision: 1
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: NOINDEX, NOFOLLOW
ms.translationtype: Machine Translation
ms.sourcegitcommit: 90775fcf2549080a43e9c1606caa79d9eb90a89c
ms.openlocfilehash: 1d6c3b1db14867bdbc5cae8ded099d9024a79549
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="manage-software-updates-in-updates-publisher"></a>Gerir atualizações de software Updates Publisher

*Aplica-se a: System Center Updates Publisher*     

No System Center Updates Publisher, utiliza o **área de trabalho atualizações** para gerir atualizações de software e os pacotes que tenha importado para o repositório.  

Tarefas de gestão incluem duplicar, editar e prestes a expirar ou reativar atualizações e os pacotes e atribuir as atualizações e tamanho dos pacotes de publicações. Também pode exportar catálogos personalizados para utilização com outras instalações Updates Publisher.

Para obter atualizações que pode gerir:
-  [Adicionar um catálogo de atualização](/sccm/sum/tools/updates-publisher-catalogs#add-software-update-catalogs) à sua instalação do publicador de atualizações
-  [Importar](/sccm/sum/tools/updates-publisher-catalogs#import-updates) as atualizações a partir do que catálogo para o seu repositório.

Também pode [criar as suas próprias atualizações](/sccm/sum/tools/create-updates-with-updates-publisher).



## <a name="create-a-duplicate-of-an-update"></a>Criar um duplicado de uma atualização
Pode criar duplicados ou cópias das atualizações que estão no seu repositório. Em seguida, pode modificar a cópia em vez de modificar a atualização original. Não é possível criar cópias de pacotes de atualização.

Para criar uma cópia, selecione uma atualização no **área de trabalho atualiza**e, em seguida, escolha **duplicar**. A cópia da atualização é apresentado na mesma localização na área de trabalho de atualizações com *copiar de* adicionada para o seu nome.

Uma nova cópia que cria tem o estado **Unexpired**, mas caso contrário, mantém as definições do original.

## <a name="edit-updates-and-bundles"></a>Editar as atualizações e os pacotes
Pode selecionar as atualizações e os pacotes que estão no seu repositório para modificá-las.

No **área de trabalho atualizações** selecionar uma atualização ou agrupamento e, em seguida, selecione **editar** a partir de **base** separador para abrir o Assistente de edição. As atualizações e os pacotes têm separados, mas conteúdo intimamente relacionados assistentes que apresentar as mesmas opções que o [criar atualizar](/sccm/sum/tools/create-updates-with-updates-publisher#the-create-update-wizard) ou [criar pacote](/sccm/sum/tools/create-updates-with-updates-publisher#the-create-bundle-wizard) assistentes.

Ao editar, pode alterar qualquer detalhes disponíveis sobre a atualização ou agrupar para que possa ser utilizado no seu ambiente. Por exemplo, pode editar as regras de aplicabilidade ou precedência ou alterar o idioma. Também pode alterar o produto e o fornecedor para mover a atualização ou agrupar para uma pasta personalizada para as atualizações de grupo para utilização própria.

## <a name="assign-updates-and-bundles-to-a-publication"></a>Atribuir as atualizações e os pacotes para uma publicação
Pode selecionar as atualizações e os pacotes de no **área de trabalho atualizações** e, em seguida, escolha **atribuir** a partir do **base** separador do friso para adicioná-los para uma publicação. Esta ação inicia o **atribuir as atualizações de Software** assistente.
-  Consulte o artigo [publicar as atualizações e os pacotes de](#publish-updates-and-bundles-from-the-updates-workspace) para obter informações sobre como selecionar e publicar as atualizações e os pacotes de como uma única tarefa.
-  Consulte o artigo [gerir publicações](/sccm/sum/tools/updates-publisher-publications) para obter informações sobre como gerir grupos de atualizações e os pacotes de como um único objeto. Após as atualizações são atribuídos a uma publicação, pode gerir essa publicação, que por sua vez inclui todas as atualizações atribuídas.

Quando atribui atualizações a uma publicação:

-   Pode incluir atualizações expiradas e não expirou e os pacotes na mesma publicação.

-   Especifique o tipo de publicação:

    -   **Conteúdo completo** – isto publica o conteúdo completo da atualização para o seu servidor de WSUS. Isto inclui metadados e os binários da atualização.

    -   **Apenas metadados** – isto publica apenas os metadados; binários de atualização não são publicados. Pode escolher esta opção quando pretender recolher dados de conformidade.

    -   **Automática** – este modo está apenas disponível quando se ligou ao Configuration Manager Updates Publisher (consulte a [servidor do ConfigMgr](/sccm/sum/tools/updates-publisher-options#configmgr-server) opção.)

    Com este tipo, o Updates Publisher consulta do Configuration Manager para determinar se as atualizações ou pacotes devem ser publicados com conteúdo completo ou apenas metadados. Conteúdo completas para uma atualização é publicada apenas quando atualizar que cumpre o **limiar de contagem de cliente pedida** e **limiar de tamanho de origem do pacote,** que são especificadas no **servidor do ConfigMgr** página de opções de publicador de atualizações.

-   Selecione uma publicação:

    -   Utilizar **atribuir a atualização de software para publicações existentes** quando já tiver criado uma publicação que pretende utilizar. Esta opção não está disponível até que existe pelo menos uma publicação.

    -   Utilize **atribuir a atualização de software para uma nova publicação** quando não tiver uma publicação adequada. Esta ação cria uma nova publicação com o nome que especificar.

Depois de atribuir atualizações a uma publicação, pode utilizar o **área de trabalho de publicação** para [publicar](/sccm/sum/tools/updates-publisher-publications#publish-pubilcations) ou [exportar](/sccm/sum/tools/updates-publisher-publications#export-a-pubilcation) a publicação como um grupo.

## <a name="publish-updates-and-bundles-from-the-updates-workspace"></a>Publicar as atualizações e os pacotes a partir da área de trabalho atualizações
Quando publica atualizações e os pacotes, o Updates Publisher adiciona informações sobre as atualizações de pacotes (metadados) e possivelmente os binários para as atualizações (conteúdo completo), para um servidor de atualização para a implementação nos dispositivos.

Antes de ter a opção de publicação, tem de configurar o [servidor de atualização](/sccm/sum/tools/updates-publisher-options#update-server) opção Updates Publisher. Para abrir esta opção de configuração, aceda a **área de trabalho atualizações** &gt; **descrição geral** e selecione **configurar o WSUS e o certificado de assinatura.** Pode também aceder à página de servidor de atualização nas opções do Updates Publisher.

Existem duas formas de publicar as atualizações e os pacotes:
-   Diretamente a partir da área de trabalho atualizações. (Consulte o procedimento seguinte, *para publicar as atualizações e os pacotes de*.)
-   Como um [publicação](/sccm/sum/tools/updates-publisher-publications#publish-pubilcations) a partir da área de trabalho de publicações.  

> [!NOTE]   
> Updates Publisher só pode publicar as atualizações que sejam 375 megabytes (MB) ou menos em tamanho.

### <a name="to-publish-updates-and-bundles"></a>Para publicar as atualizações e os pacotes
1.  Aceda a **área de trabalho atualizações** e selecione um ou mais atualizações e os pacotes que pretende publicar. Em seguida, escolha **publicar** de **base** separador do Friso.

2.  No **selecione** página do **publicar** assistente, selecione como pretende publicar as atualizações. As opções são os mesmos que para [atribuir atualizações](#assign-updates-and-bundles-to-a-publication): **Conteúdo completo**, **apenas metadados**, ou **automática**.

    Também pode optar por assinar todas as atualizações com um novo certificado de publicação.

3.  Conclua o assistente.

Se falhar a publicação, são apresentadas com uma ligação para o ficheiro de UpdatesPublisher.log que pode fornecer mais informações.

## <a name="export-updates"></a>Atualizações de exportação
Pode exportar as atualizações e os pacotes a partir do seu repositório do Updates Publisher para criar um catálogo de atualização personalizado. Em seguida, pode [adicionar](/sccm/sum/tools/updates-publisher-catalogs#add-software-update-catalogs) e, em seguida, [importar](/sccm/sum/tools/updates-publisher-catalogs#mport-updates) esse catálogo para outra instância do Updates Publisher. (Também pode [exportar atualizações como uma publicação](/sccm/sum/tools/updates-publisher-publications##export-a-publication).)

Para exportar diretamente, aceda a **área de trabalho atualizações** > **todas as atualizações de Software** e selecione um ou mais atualizações e os pacotes. Não é possível exportar um fornecedor ou a pasta de produto, mas pode selecionar uma pasta e, em seguida, selecione as atualizações de nessa pasta para exportação.

Com uma ou mais atualizações selecionadas, escolher **exportar** a partir de **base** separador do Friso e, em seguida, forneça um caminho e nome de ficheiro para a exportação de catálogo.

Terá a opção de exportação (incluir) atualizações de software dependentes.

## <a name="delete-updates-and-bundles"></a>Eliminar as atualizações e os pacotes
Pode eliminar as atualizações e os pacotes de atualizações de removê-los do repositório Updates Publisher.

Aceda a **área de trabalho atualizações** > **todas as atualizações de Software** e selecione uma ou mais atualizações individuais. Em seguida, escolha **eliminar** a partir de **base** separador do Friso.

-   Se a sua seleção contém apenas as atualizações ou pacotes de que não foram publicados ou que expirem, é-lhe pedido para confirmar a eliminação antes dos mesmos serão removidos.

-   Se a sua seleção inclui uma atualização ou o pacote que foi publicado e ainda não está expirado, recebem um aviso. Deve [expirar](/sccm/sum/tools/updates-publisher-pubilcations#expire-or-reactivate-updates-and-bundles) essas atualizações e, em seguida, publicar essa alteração antes de as eliminar do repositório.  

Se eliminar uma atualização ou a partir de um fornecedor de agrupar e, em seguida, importe esse catálogo novamente, essa atualização está restaurada para o seu repositório.

## <a name="manage-vendor-and-product-folders"></a>Gerir o fornecedor e pastas de produto
Para ver uma lista de fornecedores e produtos para cada fornecedor para o qual tenha importado ou criado atualizações, aceda ao **área de trabalho atualizações** > **descrição geral** > **todas as atualizações de Software**.

Pastas para produtos e fornecedores são criadas automaticamente pelo Updates Publisher quando utilizar um Assistente para importar ou criar um pacote ou atualização de software. Também pode criar estas pastas manualmente.

-   Para criar uma pasta de fornecedor, no painel de navegação do **área de trabalho atualizações**, com o botão direito no **todas as atualizações de Software**e, em seguida, escolha **criar fornecedor**.

-   Para criar uma pasta de produto numa pasta de fornecedor, faça duplo clique na pasta de fornecedor e escolher **criar produto**.

Para além de criar pastas, pode mudar o nome ou eliminar qualquer fornecedor ou a pasta de produto no seu repositório. Para fazê-lo, com o botão direito na pasta e escolha a opção que pretende, **mudar o nome** ou **eliminar**. Eliminar uma pasta remove todas as atualizações e os pacotes de na pasta e as pastas de produto do repositório Updates Publisher.

Pode mover atualizações entre o fornecedor e pastas de produto, incluindo para pastas que criar. Para mover uma atualização ou agrupar para uma nova pasta, tem de selecionar e, em seguida, **editar** o pacote ou atualização. Em seguida, no **informações** página do Assistente de atualização de editar pode reatribuir o fornecedor e o produto. Quando o **editar atualizar** assistente ser concluído, a alteração se aplica e a atualização move o cursor para a nova pasta.

## <a name="view-the-xml-of-an-update-or-bundle"></a>Ver o XML de um pacote ou atualização
Pode selecionar uma única atualização ou agrupar no **área de trabalho atualiza** e, em seguida, escolha **vista** XML para apresentar a estrutura XML que a atualização. Não existem sem opções para editar a estrutura XML diretamente.

