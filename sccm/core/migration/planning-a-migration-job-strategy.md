---
title: "Planeamento da tarefa de migração"
titleSuffix: Configuration Manager
description: "Utilize tarefas de migração para configurar os dados que pretende migrar para o seu ambiente do System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a70bfbd4-757a-4468-9312-1c3b373ef9fc
caps.latest.revision: "6"
caps.handback.revision: "0"
author: aczechowski
ms.author: aaroncz
manager: angrobe
robots: noindex
ms.openlocfilehash: 96fb65352042c7785dded06251b57cea04b293d7
ms.sourcegitcommit: ca9d15dfb1c9eb47ee27ea9b5b39c9f8cdcc0748
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/04/2018
---
# <a name="plan-a-migration-job-strategy-in-system-center-configuration-manager"></a>Planear uma estratégia de tarefa de migração no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize tarefas de migração para configurar os dados específicos que pretende migrar para o seu ambiente do System Center Configuration Manager. As tarefas de migração identificam os objetos que planeia migrar, e são executadas no site de nível superior na hierarquia de destino. Pode configurar um ou mais tarefas de migração por site de origem. Isto permite-lhe migrar todos os objetos de uma só vez ou subconjuntos limitados de dados com cada tarefa.  

 Pode criar tarefas de migração após o Configuration Manager foi recolhido com êxito os dados de um ou mais sites da hierarquia de origem. É possível migrar dados em qualquer sequência a partir dos sites de origem que recolheram dados. Com um site de origem do Configuration Manager 2007, pode migrar dados apenas a partir do site onde um objeto foi criado. Com sites de origem que executam o System Center 2012 Configuration Manager ou posterior, todos os dados que pode migrar está disponível no site de nível superior da hierarquia de origem.  

 Antes de migrar clientes entre hierarquias, certifique-se de que os objetos que os clientes utilizam foram migrados e de que esses objetos estão disponíveis na hierarquia de destino. Por exemplo, ao migrar a partir de uma hierarquia de origem do Configuration Manager 2007 SP2, pode ter um anúncio para conteúdo que é implementado para uma coleção personalizada que tenha um cliente. Neste cenário, recomendamos que migra a coleção, o anúncio e o conteúdo associado antes de migrar o cliente. Estes dados não podem ser associados ao cliente na hierarquia de destino, se o conteúdo, a recolha e o anúncio não são migrados antes do cliente. Se um cliente não estiver associado aos dados relacionados com o anúncio e conteúdo de uma execução anterior, pode ser oferecido ao cliente o conteúdo para a instalação na hierarquia de destino, o que talvez seja desnecessário. Quando o cliente migra após a migração dos dados, o cliente é associado a este conteúdo e anúncio e, a menos que o anúncio seja recorrente, não lhe é oferecido novamente este conteúdo para o anúncio migrado.  

 Alguns objetos requerem mais do que a migração de dados da hierarquia de origem para a hierarquia de destino. Por exemplo, para migrar com êxito as atualizações de software para os seus clientes para a hierarquia de destino, deve implementar um ponto de atualização de software ativo, configurar o catálogo de produtos e sincronizar o ponto de atualização de software com o Windows Server Update Services (WSUS) na hierarquia de destino.  

 Utilize as secções seguintes para o ajudar a planear as tarefas de migração.  

-   [Tipos de tarefas de migração](#Types_of_Migration)  

-   [Planeamento geral para todas as tarefas de migração](#About_Migration_Jobs)  

-   [Planear as tarefas de migração de coleções](#About_Collection_Migration)  

-   [Planear tarefas de migração de objeto](#About_Object_Migration)  

-   [Planear para migrados anteriormente as tarefas de migração de objeto](#About_Object_Migrations)  

##  <a name="Types_of_Migration"></a>Tipos de tarefas de migração  
 O Configuration Manager suporta os seguintes tipos de tarefas de migração. Cada tipo de tarefa foi concebido para ajudar a definir os objetos que podem ser incluídos nessa tarefa.  

 **Migração de coleção** (apenas suportada ao migrar do Configuration Manager 2007 SP2): Migre objetos que estão relacionados com as coleções selecionadas. Por predefinição, a migração de coleção inclui todos os objetos que estão associados a membros da coleção. Quando utiliza uma tarefa de migração de coleção, pode excluir instâncias de objetos específicas.  

 **Migração de objetos**: Migre objetos individuais selecionados. Selecione apenas os dados específicos que pretende migrar.  

 **Anteriormente migrado de migração de objetos**: Migre objetos migrados anteriormente quando forem atualizados na hierarquia de origem após terem sido migrados pela última vez.  

###  <a name="Objects_that_can_migrate"></a>Objetos que podem ser migrados  
 Nem todos os objetos podem ser migrados através de um tipo específico de tarefa de migração. A lista seguinte identifica o tipo de objetos que é possível migrar com cada tipo de tarefa de migração.  

> [!NOTE]  
>  As tarefas de migração de coleções estão disponíveis apenas quando são migrados objetos a partir de uma hierarquia de origem do Configuration Manager 2007 SP2.  

 **Tipos de tarefa que pode utilizar para migrar cada objeto**  

-   **Anúncios** (disponíveis para migrar a partir de sites de origem suportadas do Configuration Manager 2007)  

    -   Migração de coleção  


-   **Catálogo do Asset Intelligence**  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Requisitos de hardware do Asset Intelligence**  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Lista de software do Asset Intelligence**  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Limites**  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Linhas de base de configuração**  

    -   Migração de coleção  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Itens de configuração**  

    -   Migração de coleção  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Janelas de manutenção**  

    -   Migração de coleção  


-   **Imagens de arranque de implementação do sistema operativo**  

    -   Migração de coleção  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Pacotes de controladores de implementação do sistema operativo**  

    -   Migração de coleção  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Controladores de implementação do sistema operativo**  

    -   Migração de coleção  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Imagens de implementação do sistema operativo**  

    -   Migração de coleção  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Pacotes de implementação do sistema operativo**  

    -   Migração de coleção  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Pacotes de distribuição de software**  

    -   Migração de coleção  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Regras de medição de software**  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Pacotes de implementação de atualização de software**  

    -   Migração de coleção  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Modelos de implementação de atualizações de software**  

    -   Migração de coleção  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Implementações de atualização de software**  

    -   Migração de coleção  


-   **Listas de atualização de software**  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Sequências de tarefas**  

    -   Migração de coleção  

    -   Migração de objeto  

    -   Migração de objetos migrados anteriormente  

-   **Pacotes de aplicações virtuais**  

    -   Migração de coleção  

    -   Migração de objeto  

    > [!IMPORTANT]  
    >  Embora possa migrar um pacote de aplicação virtual através da migração de objetos, os pacotes não podem ser migrados através do tipo de tarefa de migração **Migração de Objetos Migrados Anteriormente**. Em vez disso, é necessário eliminar o pacote de aplicação virtual migrado no site de destino e, em seguida, criar uma nova tarefa de migração para migrar a aplicação virtual.  

##  <a name="About_Migration_Jobs"></a>Planeamento geral para todas as tarefas de migração  
 Utilize o Assistente Criar tarefa de migração para criar uma tarefa de migração para migrar objetos para a hierarquia de destino. O tipo da tarefa de migração criada determina quais os objetos que estão disponíveis para migrar. Pode criar e utilizar várias tarefas de migração para migrar dados a partir do mesmo site de origem ou de vários sites de origem. A utilização de um tipo de tarefa de migração não bloqueia a utilização de um tipo de tarefa de migração diferente.  

 Após a execução bem-sucedida de uma tarefa de migração, o estado desta é apresentado como **Concluída** e não pode ser executada novamente. No entanto, é possível criar uma nova tarefa de migração para criar qualquer um dos objetos migrados pela tarefa original e a nova tarefa de migração pode igualmente incluir outros objetos. Quando criar tarefas de migração adicionais, os objetos que foram migrados anteriormente mostram o estado do **migrado**. Pode selecionar estes objetos para os migrar novamente, mas, a menos que o objeto tiver sido atualizado na hierarquia de origem, migrar estes objetos novamente não é necessário. Se o objeto tiver sido atualizado na hierarquia de origem após a migração original, é possível identificá-lo quando utiliza o tipo de tarefa de migração **Objetos modificados após migração**.  

 É possível eliminar uma tarefa de migração antes da sua execução. No entanto, quando uma tarefa de migração estiver concluído, este permanece visível na consola do Configuration Manager e não pode ser eliminada. Cada tarefa de migração foi concluída ou tiver não executadas permanecem visíveis na consola do Configuration Manager depois de concluir o processo de migração e limpar os dados de migração.  

> [!NOTE]  
>  Depois de Concluir migração utilizando o **limpar dados de migração** ação, pode reconfigurar a mesma hierarquia como a hierarquia de origem atual para restaurar a visibilidade dos objetos migrados anteriormente.  

 Pode ver os objetos contidos numa tarefa de migração na consola do Configuration Manager, selecionando a tarefa de migração e, em seguida, escolha o **objetos na tarefa** separador.  

 Utilize as informações das secções seguintes para o ajudar a planear todas as tarefas de migração.  

### <a name="data-selection"></a>Seleção de dados  
 Ao criar uma tarefa de migração de coleção, é necessário selecionar uma ou mais coleções. Depois de selecionar as coleções, o Assistente Criar tarefa de migração mostra os objetos que estão associados às coleções. Por predefinição, todos os objetos associados as coleções selecionadas são migrados, mas pode desmarcar os objetos que não pretende migrar com essa tarefa. Quando desmarcar um objeto que contém objetos dependentes, esses objetos dependentes também são desmarcados. Todos os objetos desmarcados são adicionados a uma lista de exclusão. Os objetos de uma lista de exclusão são removidos da seleção automática para futuras tarefas de migração. Tem de editar manualmente a lista de exclusão para remover os objetos que pretende que sejam selecionados automaticamente para migração em tarefas de migração que criar no futuro.  

### <a name="site-ownership-for-migrated-content"></a>Propriedade do site para conteúdo migrado  
 Ao migrar conteúdo para implementações,necessita de atribuir o objeto do conteúdo a um site da hierarquia de destino. Em seguida, este site torna-se o proprietário desse conteúdo na hierarquia de destino. Embora o site de nível superior da hierarquia de destino seja o site que efetivamente migra os metadados do conteúdo, será o site atribuído que irá aceder aos ficheiros de origem originais para obter os conteúdos de toda a rede.  

 Para minimizar a largura de banda da rede que é utilizada durante a migração, considere a transferência da propriedade do conteúdo para o site disponível mais próximo. Porque a informação sobre o conteúdo é partilhada globalmente no System Center Configuration Manager, estará disponível em todos os sites.  

 As informações acerca do conteúdo são partilhadas para todos os sites na hierarquia de destino utilizando a replicação de base de dados. No entanto, todos os conteúdos que atribua a um site primário e, em seguida, implementar em pontos de distribuição doutros sites primários será transferido através de replicação baseada em ficheiros. Esta transferência é encaminhada através do site de administração central e, em seguida, para cada site primário adicional. Centralizar os pacotes que pretende distribuir por vários sites primários antes ou durante a migração quando atribui um site como proprietário do conteúdo, pode reduzir as transferências de dados através de redes com pouca largura de banda.  

### <a name="role-based-administration-security-scopes-for-migrated-data"></a>Âmbitos de segurança da administração baseada em funções para dados migrados  
 Quando migra dados para uma hierarquia de destino, tem de atribuir administração baseada em funções de um ou mais âmbitos de segurança aos objetos cujos dados são migrados. Este procedimento assegura que apenas os utilizadores administrativos apropriados têm acesso a estes dados após a sua migração. Os âmbitos de segurança especificados são definidos pela tarefa de migração e aplicados a cada objeto que é migrado por essa tarefa. Se necessitar de âmbitos de segurança diferentes a ser aplicadas a diferentes conjuntos de objetos e pretender atribuir esses âmbitos durante a migração, tem de migrar os diferentes conjuntos de objetos, utilizando as tarefas de migração diferentes.  

 Antes de configurar uma tarefa de migração, reveja como baseada em funções administração funciona no System Center Configuration Manager. Se necessário, configure um ou mais âmbitos de segurança para os dados que serão migrados para controlar quem terá acesso aos objetos migrados na hierarquia de destino.  

 Para mais informações sobre âmbitos de segurança e a administração baseada em funções, consulte [Noções básicas da administração baseada em funções para o System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

### <a name="review-migration-actions"></a>Rever ações de migração  
 Quando configurar uma tarefa de migração, o Assistente Criar tarefa de migração apresenta uma lista de ações que deve tomar para garantir uma migração com êxito e uma lista de ações do Configuration Manager executa durante a migração dos dados selecionados. Reveja estas informações cuidadosamente para verificar o resultado esperado.  

### <a name="schedule-migration-jobs"></a>Agendar tarefas de migração  
 Por predefinição, uma tarefa de migração é executada imediatamente após a sua criação. No entanto, pode especificar quando a tarefa de migração é executada ao criar a tarefa ou editando as propriedades da tarefa. Pode agendar a tarefa de migração para ser executado da seguinte forma:  

-   Executar a tarefa agora  

-   Executar a tarefa a uma hora de início específica  

-   Não executar a tarefa  

### <a name="specify-conflict-resolution-for-migrated-data"></a>Especificar a resolução de conflitos para dados migrados  
 Por predefinição, as tarefas de migração não substituem dados na base de dados de destino, exceto se configurar a tarefa de migração para ignorar ou substituir os dados que tenham sido anteriormente migrados para a base de dados de destino.  

##  <a name="About_Collection_Migration "></a>Planear as tarefas de migração de coleções  
 As tarefas de migração de coleções estão disponíveis apenas quando são migrados dados a partir de uma hierarquia de origem que executa uma versão suportada do Configuration Manager 2007. Tem de especificar uma ou mais coleções para migrar quando migra por coleção. Para cada coleção especificada, a tarefa de migração seleciona automaticamente todos os objetos relacionados para migração. Por exemplo, se selecionar uma coleção específica de utilizadores, são em seguida identificados os membros da coleção e pode migrar as implementações associadas a esta coleção. Opcionalmente, pode selecionar outros objetos de implementação para migrar que estão associados a estes membros. Todos estes itens selecionados são adicionados à lista de objetos que podem ser migrados.  

 Quando migra uma coleção, o System Center Configuration Manager também migra as definições da coleção, incluindo janelas de manutenção e variáveis da coleção, mas não é possível migrar as definições da coleção para aprovisionamento do cliente AMT.  

 Utilize as informações nas secções seguintes para saber mais sobre as configurações adicionais que podem aplicar às tarefas de migração baseada em coleções.  

### <a name="exclude-objects-from-collection-migration-jobs"></a>Excluir objetos de tarefas de migração de coleção  
 Pode excluir objetos específicos de uma tarefa de migração de coleções. Quando exclui um objeto específico de uma tarefa de migração de coleções, esse objeto é adicionado a uma lista de exclusão global que tem todos os objetos excluídos das tarefas de migração criadas para qualquer site de origem na hierarquia de origem atual. Objetos da lista de exclusão ainda estão disponíveis para migração em tarefas futuras, mas não são incluídos automaticamente quando criar uma nova tarefa de migração baseada em coleções.  

 Pode editar a lista de exclusão para remover objetos que excluiu anteriormente. Após a remoção de um objeto da lista de exclusão, este é selecionado automaticamente quando uma coleção associada é especificada durante a criação de uma nova tarefa de migração.  

### <a name="unsupported-collections"></a>Coleções não suportadas  
 O Configuration Manager pode migrar qualquer uma das coleções de utilizador predefinido, a coleções de dispositivos e a maioria das coleções personalizadas a partir de uma hierarquia de origem do Configuration Manager 2007. No entanto, o Configuration Manager não consegue migrar coleções que contêm utilizadores e dispositivos na mesma coleção.  

 Não é possível migrar as seguintes coleções:  

-   Uma coleção que tenha utilizadores e dispositivos.  

-   Uma coleção que contém uma referência a uma coleção de um tipo de recurso diferente. Por exemplo, uma coleção com base no dispositivo que tenha uma subcoleção ou uma ligação para uma coleção baseada no utilizador. Neste exemplo, apenas a coleção de nível superior é migrada.  

-   Uma coleção que tenha uma regra para incluir computadores desconhecidos. A coleção migra, mas a regra para incluir computadores desconhecidos não migra.  

### <a name="empty-collections"></a>Coleções vazias  
 Uma coleção vazia é uma coleção se recursos associados. Quando o Configuration Manager migra uma coleção vazia, converte-numa pasta organizacional que não tem utilizadores ou dispositivos. Esta pasta é criada com o nome da coleção vazia no **coleções de utilizadores** ou **coleções de dispositivos** no nó de **ativos e compatibilidade** área de trabalho na consola do Configuration Manager.  

### <a name="linked-collections-and-subcollections"></a>Coleções ligadas e subcoleções  
 Quando migra coleções ligadas a outras coleções ou que contêm subcoleções, o Configuration Manager cria uma pasta na **coleções de utilizadores** ou **coleções de dispositivos** nó além das coleções ligadas e subcoleções.  

### <a name="collection-dependencies-and-include-objects"></a>Dependências de coleções e inclusão de objetos  
 Quando especificar uma coleção para migrar no Assistente Criar tarefa de migração, todas as coleções dependentes são automaticamente selecionadas para inclusão na tarefa. Este comportamento garante que todos os recursos necessários estão disponíveis após a migração.  

 Por exemplo: Selecione uma coleção para dispositivos que executam o Windows 7 e com o nome **Win_7**. Esta coleção está limitada a uma coleção que tenha todos os sistemas de operativos do cliente e o nome **All_Clients**. A coleção **All_Clients** será selecionada automaticamente para migração.  

### <a name="collection-limiting"></a>Limitação de coleções  
 Com o System Center Configuration Manager, as coleções são dados globais e são avaliadas em cada site na hierarquia. Por conseguinte, planeie a forma de limitar o âmbito de uma coleção após a respetiva migração. Durante a migração, pode identificar uma coleção da hierarquia de destino a utilizar para limitar o âmbito da coleção que está a migrar de modo a que a coleção migrada não contenha membros inesperados.  

 Por exemplo, no Configuration Manager 2007, as coleções são avaliadas no site que as cria e em sites subordinados. Um anúncio pode ser implementado apenas num site subordinado, o que pode limitar o âmbito desse anúncio a esse site subordinado. Em comparação, com o System Center Configuration Manager, as coleções são avaliadas em cada site e anúncios associados são então avaliados para cada site. A limitação da coleção permite-lhe refinar os membros da coleção com base noutra coleção para evitar a adição de membros inesperados da coleção.  

### <a name="site-code-replacement"></a>Substituição do código do site  
 Quando migra uma coleção que tenha os critérios que identificam um site do Configuration Manager 2007, tem de especificar um site específico na hierarquia de destino. Isto garante que a coleção migrada permaneça funcional na sua hierarquia de destino e não aumente o âmbito.  

### <a name="specify-behavior-for-migrated-advertisements"></a>Especificar o comportamento de anúncios migrados  
 Por predefinição, as tarefas de migração baseada em coleções desativam anúncios migrados para a hierarquia de destino. Isto inclui todos os programas que estão associados ao anúncio. Quando cria uma tarefa de migração baseada em coleções que tenha anúncios, verá o **ativar programas para implementação no Configuration Manager após um anúncio ser migrado** opção o **definições** página do Assistente Criar tarefa de migração. Se selecionar esta opção, os programas associados aos anúncios são ativados após terem sido migrados. Como melhor prática, não selecione esta opção. Em vez disso, ative os programas após terem sido migrados quando pretender verificar os clientes que irão recebê-las.  

> [!NOTE]  
>  Pode ver o **ativar programas para implementação no Configuration Manager após um anúncio ser migrado** opção apenas quando estiver a criar uma tarefa de migração baseada em coleções e a tarefa de migração contém anúncios.  

 Para ativar um programa após a migração, desmarque **desativar este programa em computadores onde tenha sido anunciado** no **avançadas** separador de propriedades do programa.  

##  <a name="About_Object_Migration"></a>Plano para tarefas de migração de objeto  
 Ao contrário da migração de coleções, deve selecionar cada objeto e instância do objeto que pretende migrar. Pode selecionar objetos individuais, como (anúncios de uma hierarquia do Configuration Manager 2007) ou uma publicação de uma hierarquia do System Center 2012 Configuration Manager ou System Center Configuration Manager para adicionar à lista de objetos a migrar para uma tarefa de migração específico. Todos os objetos que não forem adicionados à lista de migração não serão migrados para o site de destino pela tarefa de migração de objetos.  

 As tarefas de migração baseada em objetos não têm quaisquer configurações adicionais a planear para além das aplicáveis a todas as tarefas de migração.  

##  <a name="About_Object_Migrations"></a>Planear tarefas de migração de objetos migrados anteriormente  
 Quando um objeto já migrado para a hierarquia de destino é atualizado na hierarquia de origem, pode migrá-lo novamente utilizando o tipo de tarefa **Objetos modificados após migração**. Por exemplo, ao mudar o nome ou atualizar os ficheiros de origem para um pacote na hierarquia de origem, a incrementação da versão de pacote na hierarquia de origem. Após a incrementação da versão do pacote, este pode ser identificado para migração por este tipo de tarefa.  

 Este tipo de tarefa é semelhante ao tipo de migração de objeto, com a exceção de que, quando seleciona objetos para migrar, apenas os objetos atualizados após a migração por uma tarefa de migração anterior poderão ser selecionados.   

 Quando seleciona este tipo de tarefa, o comportamento da resolução de conflito no **definições** página do Assistente Criar tarefa de migração é configurada para substituir os objetos anteriormente migrados. Não é possível alterar esta definição.  

> [!NOTE]  
>  Esta tarefa de migração pode identificar objetos que são atualizados automaticamente pela hierarquia de origem e objetos atualizados por um utilizador administrativo.  
