---
title: Gerir publicações
titleSuffix: Configuration Manager
description: Gerir grupos de atualizações de software como uma publicação com o System Center Updates Publisher
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: e6c1df1d-7728-4980-9199-bc32cde5439e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f626d07d1fe25d8277ab2189f136862079dc503c
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/24/2019
ms.locfileid: "54896629"
---
# <a name="manage-publications-in-updates-publisher"></a>Gerir publicações no Updates Publisher

*Aplica-se a: System Center Updates Publisher*

Pode utilizar publicações para gerir grupos de atualizações e pacotes como um único objeto. Isto inclui as atualizações de publicação para um servidor de gestão e a exportação de publicação como grupo para utilização com outra instalação do Updates Publisher.

## <a name="create-publications"></a>Crie publicações
Publicações são criadas duas formas:

-   Quando gerir atualizações e pacotes no **área de trabalho de atualizações**, pode [atribuir](/sccm/sum/tools/manage-updates-with-updates-publisher#assign-updates-and-bundles-to-a-publication) -os para uma nova publicação que é criada nessa altura.

-   Na **publicações de área de trabalho** pode utilizar o **criar** botão o **publicação** separador do Friso. Este método permite-lhe criar uma publicação para utilização futura. Mais tarde, quando atribuir as atualizações, pode utilizar esta publicação.

## <a name="rename-a-publication"></a>Mudar o nome de uma publicação
Para mudar o nome de uma publicação, selecione a publicação de dentro do **publicações de área de trabalho**e, em seguida, no **publicação** separador do Friso, selecione **editar**.

## <a name="change-the-publication-type-of-updates-in-a-publication"></a>Alterar o tipo de publicação de atualizações numa publicação
Do **área de trabalho de publicação**, pode modificar o **tipo de publicação** de atualizações e pacotes que estão atribuídos a uma publicação.

1. Selecione a publicação que contenha as atualizações que pretende modificar e, em seguida, selecione um ou mais atualizações ou pacotes do **todos os &lt;nome da publicação > atualizações do membro** lista.

2. Em seguida, na **home page** separador, selecione uma das seguintes opções. As opções disponíveis dependem do tipo de publicação de atualizações que selecionou.

   -   **automática**
   -   **Conteúdo completo**
   -   **Apenas os metadados**

Depois de fazer uma alteração, poderá ter de atualizar a vista de publicação para ver os novos valores.

Para obter informações sobre os tipos diferentes de publicação, consulte [atribuir atualizações e pacotes para uma publicação](/sccm/sum/tools/manage-updates-with-updates-publisher#assign-updates-and-bundles-to-a-publication).

> [!TIP]    
> Ao definir o tipo de publicação de um pacote, todas as atualizações de software no pacote são publicadas com o tipo de publicação do pacote.

## <a name="remove-updates-from-a-publication"></a>Remover as atualizações de uma publicação
Para remover as atualizações ou pacotes de uma publicação no **publicações de área de trabalho** selecione a publicação que pretende modificar e, em seguida, selecione as atualizações e pacotes que pretende remover. Em seguida, na **home page** separador do Friso, selecione **remover**.

Depois das atualizações são removidas de uma publicação, estas permaneçam disponíveis no repositório do Updates Publisher.

## <a name="publish-publications"></a>Publicar publicações
Quando publica atualizações e pacotes, o Updates Publisher adiciona informações sobre essas atualizações e pacotes (metadados) e, possivelmente, os binários para as atualizações (conteúdo completo), para um servidor de atualização para implementação em dispositivos.

Antes de ter a opção de publicar, tem de configurar o [servidor de atualização](/sccm/sum/tools/updates-publisher-options#update-server) opção para o Updates Publisher. Para abrir esta opção de configuração, aceda a **área de trabalho de atualizações** &gt; **descrição geral** e selecione **configurar o WSUS e o certificado de assinatura.** Pode também aceder à página do servidor de atualização nas opções do Updates Publisher.

> [!NOTE]   
> Publicador de atualizações pode publicar somente as atualizações que estão 375 megabytes (MB) ou de tamanho.

### <a name="to-publish-a-publication"></a>Para publicar uma publicação

1. Vá para o **publicações de área de trabalho**e, em seguida, selecione uma publicação que contém o grupo de atualizações e pacotes que pretende publicar ou exportar. Em seguida, escolha **Publish** partir **home page** separador do Friso.

2. Sobre o **selecione** página do **publicar** assistente, pode optar por inscrever-se a todas as atualizações com um novo certificado de publicação, mas não é possível alterar o tipo de publicação.

3. Conclua o assistente.

   Se falhar a publicação, são apresentados com uma ligação para o ficheiro de UpdatesPublisher.log que pode fornecer mais informações.

## <a name="export-a-publication"></a>Exportar uma publicação
Pode exportar uma publicação a partir do seu repositório do Updates Publisher. Se o fizer, exporta as atualizações e pacotes que são atribuídos a essa publicação e cria um catálogo de atualização. Pode então [adicione](/sccm/sum/tools/updates-publisher-catalogs#add-software-update-catalogs) e, em seguida [importar](/sccm/sum/tools/updates-publisher-catalogs#mport-updates) esse catálogo para outra instância do Updates Publisher. Também pode [exportar atualizações](/sccm/sum/tools/manage-updates-with-updates-publisher#export-updates) que não fazem parte de uma publicação.

Para exportar uma publicação, vá para o **publicações de área de trabalho** e selecione a publicação que contém as atualizações que pretende exportar. Só pode selecionar uma publicação, ao mesmo tempo.

Com a publicação selecionada, escolha **exportar** partir do **home page** separador do Friso e, em seguida, forneça um nome e caminho para a exportação de catálogo.

Também tem a opção para exportar (incluir) as atualizações de software dependentes como parte da exportação.

## <a name="rename-a-publication"></a>Mudar o nome de uma publicação
Para mudar o nome de uma publicação, selecione a publicação da **publicações de área de trabalho**e, em seguida, escolha **editar** do **publicação** separador do Friso.

## <a name="delete-a-publication"></a>Eliminar uma publicação
Para eliminar uma publicação, selecione a publicação da **publicações de área de trabalho**e, em seguida, escolha **eliminar** do **publicação** separador do Friso.

Após a publicação é removida do Updates Publisher, as atualizações que foram na publicação permanecem disponíveis no repositório do Updates Publisher.

## <a name="expire-or-reactivate-updates-and-bundles"></a>Expirar ou reativar as atualizações e pacotes
Pode utilizar o **espaço de trabalho atualizações** para selecionar e, em seguida, expirar ou reativar as atualizações e pacotes. Pode expirar e reativar as atualizações e os pacotes de quantas vezes escolher.

-   **Para expirar atualizações ou pacotes**, no, selecione a área de trabalho atualizações um ou mais atualizações ou agrupa que não são expirado e, em seguida, escolha **Expire** da **home page** separador. Até a publicar a atualização ou pacote como expirada para o Configuration Manager, pode reativá-la.

    Antes de poder remover (eliminar) personalizada update ou o pacote do Configuration Manager, tem de expiração e, em seguida, publicar esse Estado expiradas para o Configuration Manager. Depois de atualizações ou pacotes são a expirou no Configuration Manager, já não pode implementar ou reativar a atualização ou pacote.

-   **Para reativar a atualizações ou pacotes**, na área de trabalho atualizações, selecione uma ou mais atualizações que são a expirou em, em seguida, escolha **reativar** da **home page** separador do Friso. Se a atualização expirada tiver sido publicada anteriormente como a expirou ao Configuration Manager, não pode reativá-la.
