---
title: Utilizar o Asset Intelligence | Microsoft Docs
description: Realizar tarefas comuns de Asset Intelligence no System Center Configuration Manager.
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e8159bd9-5c2b-4d25-82f9-78fcfd732ba9
caps.latest.revision: "6"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 17168e26f13340847928f6e3623115cd4b55997b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-use-asset-intelligence-in-system-center-configuration-manager"></a>Como utilizar o Asset Intelligence no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este tópico contém informações para ajudar a gerir as tarefas comuns do Asset Intelligence na sua hierarquia do System Center Configuration Manager:  

##  <a name="BKMK_ViewInformation"></a> Ver informações do Asset Intelligence  
 Pode ver informações do Asset Intelligence na home page do **Asset Intelligence** e nos relatórios do Asset Intelligence.  

###  <a name="BKMK_AssetIntelligenceHomePage"></a> Home page do Asset Intelligence  
 A home page do **Asset Intelligence** apresenta um dashboard de resumo de informações do catálogo do Asset Intelligence. Na home page, pode ver informações sobre a sincronização do catálogo e o estado do software inventariado. A home page do **Asset Intelligence** está dividida nas secções seguintes:  

-   **Sincronização do catálogo**: Fornece informações sobre se o Asset Intelligence está ativado, o estado atual do ponto de sincronização do Asset Intelligence, a agenda de sincronização, se a declaração de licença de cliente é importada, quando o estado da última foi atualizado e a hora para a próxima atualização agendada e o número de alterações que ocorreram após o sistema de sites do ponto de sincronização do Asset Intelligence foi instalado.  

    > [!NOTE]  
    >  A secção de sincronização do catálogo do Asset Intelligence da home page do **Asset Intelligence** só é apresentada se tiver sido instalada uma função de sistema de sites do ponto de sincronização do Asset Intelligence.  

-   **Estado de Software inventariado**: Fornece a contagem e a percentagem de software inventariado, categorias de software e famílias de software que são identificadas pela Microsoft, identificada por um utilizador administrativo, com identificação online pendente ou não identificadas e não pendentes. As informações apresentadas em formato de tabela mostram a contagem de cada uma, enquanto as informações apresentadas no gráfico mostram a percentagem de cada uma.  

 Utilize o procedimento seguinte para ver informações do Asset Intelligence na home page do **Asset Intelligence** .  

##### <a name="to-view-asset-intelligence-information-on-the-asset-intelligence-home-page"></a>Para ver informações do Asset Intelligence na home page do Asset Intelligence  

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  

2.  Na área de trabalho **Ativos e Compatibilidade** , clique em **Asset Intelligence**. Os relatórios do Asset Intelligence são apresentados.  

###  <a name="BKMK_AssetIntelligenceReports"></a> Relatórios do Asset Intelligence  
 Existem mais de 60 relatórios do Asset Intelligence que apresentam as informações recolhidas pelo Asset Intelligence. Muitos destes relatórios incluem uma ligação para relatórios mais específicos nos quais pode consultar informações gerais e desagregar para obter informações mais detalhadas. Relatórios do Asset Intelligence estão localizados na consola do Configuration Manager, no **monitorização** área de trabalho, sob o **relatórios** nó. Os relatórios fornecem informações sobre hardware, gestão de licenças e software. Para obter mais informações sobre os relatórios no Configuration Manager, consulte [relatórios no System Center Configuration Manager](../../../../core/servers/manage/reporting.md).  

> [!NOTE]  
>  A precisão das quantidades de títulos de software instalado e das informações de licença apresentadas nos relatórios do Asset Intelligence podem variar em relação ao número real de títulos de software instalados ou de licenças em utilização no ambiente devido às complexas dependências e limitações envolvidas no inventário de informações de licença de software para títulos de software instalado em ambientes empresariais. Os relatórios do Asset Intelligence não devem ser utilizados como única fonte para determinar o cumprimento das licenças de software adquiridas.  

 Utilize o procedimento seguinte para ver informações do Asset Intelligence, utilizando relatórios do Asset Intelligence.  

##### <a name="to-view-collected-asset-intelligence-information-by-using-asset-intelligence-reports"></a>Para ver informações do Asset Intelligence recolhidas através de relatórios do Asset Intelligence  

1.  Na consola do Configuration Manager, clique em **monitorização**.  

2.  Na área de trabalho **Monitorização** , expanda **A relatar**, expanda **Relatórios**e clique em **Asset Intelligence**. Os relatórios do Asset Intelligence são apresentados.  

    > [!WARNING]  
    >  Se não existirem pastas de relatórios no nó **Relatórios** , verifique se configurou os relatórios. Para obter mais informações, consulte [configurar relatórios no System Center Configuration Manager](../../../../core/servers/manage/configuring-reporting.md).  

3.  Selecione o relatório do Asset Intelligence que pretende executar e, em seguida, no separador **Home Page** , no grupo **Grupo de Relatórios** , clique em **Executar**.  

##  <a name="BKMK_SynchronizeTheCatalog"></a> Sincronizar o catálogo do Asset Intelligence  
 Pode sincronizar o catálogo do Asset Intelligence local com o System Center Online para obter a categorização mais recente de títulos de software. Quando solicitar manualmente a sincronização do catálogo com o System Center Online, pode demorar 15 minutos ou mais a concluir o processo de sincronização com o System Center Online. Atualizações do Configuration Manager a **última atualização bem sucedida** definição o **do Asset Intelligence** home page com a hora atual para quando sincronização for concluída com êxito.  

> [!NOTE]  
>  Uma função de sistema de sites do ponto de sincronização do Asset Intelligence tem de ser instalada primeiro através dos procedimentos. Para obter informações sobre como instalar um ponto de sincronização do Asset Intelligence, consulte [configurar do Asset Intelligence no System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

 Utilize o procedimento seguinte para criar um agendamento de sincronização para o catálogo do Asset Intelligence.  

#### <a name="to-create-a-synchronization-schedule-for-the-asset-intelligence-catalog"></a>Para criar um agendamento de sincronização para o catálogo do Asset Intelligence  

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  

2.  Na área de trabalho **Ativos e Compatibilidade** , clique em **Asset Intelligence**.  

3.  No separador **Home Page** , no grupo **Criar** , clique em **Sincronizar**e, em seguida, clique em **Agendar Sincronização**.  

4.  Na caixa de diálogo **Agendamento do Ponto de Sincronização do Asset Intelligence** , selecione **Ativar sincronização num agendamento**e configure um agendamento simples ou personalizado.  

5.  Clique em **OK** para guardar as alterações.  

    > [!NOTE]  
    >  Para obter informações sobre o agendamento da sincronização, incluindo a próxima sincronização agendada, consulte o nó **Asset Intelligence** na área de trabalho **Ativos e Compatibilidade** , no site de nível superior da hierarquia.  

 Utilize o procedimento seguinte para sincronizar manualmente o catálogo do Asset Intelligence.  

> [!WARNING]  
>  O System Center Online só aceita um pedido de sincronização manual num período de 12 horas.  

###  <a name="BKMK_ManuallySynchronizeCatalog"></a> Para sincronizar manualmente o catálogo do Asset Intelligence  

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  

2.  Na área de trabalho **Ativos e Compatibilidade** , clique em **Asset Intelligence**.  

3.  No separador **Home Page** , no grupo **Criar** , clique em **Sincronizar**, clique em **Sincronizar Catálogo do Asset Intelligence**e, em seguida, clique em **OK**.  

##  <a name="BKMK_CustomizeCatalog"></a> Personalizar o catálogo do Asset Intelligence  
 As informações de categorização do catálogo do Asset Intelligence recebidas do System Center Online são armazenadas na base de dados do site com permissões só de leitura e não podem ser modificadas nem eliminadas. No entanto, pode criar, modificar e eliminar categorias de software personalizadas, famílias de software, etiquetas de software e informações do catálogo de requisitos de hardware. Em seguida, pode utilizar os dados de categorização personalizada em vez das informações fornecidas pelo System Center Online para informações sobre títulos de software existentes ou definidas pelo utilizador. Quando alterar ou adicionar informações de categorização, as informações do catálogo são consideradas definidas pelo utilizador. As informações de categorização definidas pelo utilizador são armazenadas em tabelas de base de dados diferentes do que as informações do catálogo validadas.  

###  <a name="BKMK_SoftwareCategories"></a> Categorias de software  
 As categorias de software do Asset Intelligence são utilizadas para categorizar amplamente títulos de software inventariado e são também utilizadas como agrupamentos de alto nível de famílias de software mais específicas. Por exemplo, uma categoria de software poderá ser empresas de energia e uma família de software dentro dessa categoria de software poderá ser petróleo e gás ou hidroelétrica. Muitas categorias de software estão predefinidas no catálogo do Asset Intelligence e outras categorias definidas pelo utilizador podem ser criadas para definir mais pormenorizadamente o software inventariado. O estado de validação para todas as categorias predefinidas de software é sempre **Validado**, enquanto as informações de categorias personalizadas de software adicionadas ao catálogo do Asset Intelligence são **Definidas pelo Utilizador**.  

 Utilize o procedimento seguinte para criar uma categoria de software definida pelo utilizador.  

##### <a name="to-create-a-user-defined-software-category"></a>Para criar uma categoria de software definida pelo utilizador  

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  

2.  Na área de trabalho **Ativos e Compatibilidade** , clique em **Asset Intelligence**e, em seguida, clique em **Catálogo**.  

3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Categoria de Software**.  

4.  Na página **Geral** , introduza um nome para a nova categoria de software e, opcionalmente, uma descrição.  

    > [!NOTE]  
    >  O estado de validação para todas as novas categorias personalizadas de software está sempre definido como **Definido pelo Utilizador**.  

     Clique em **Seguinte**.  

5.  Na página **Resumo** , reveja as definições e clique em **Seguinte**.  

6.  Na página **Conclusão** , clique em **Fechar** para sair do assistente.  

###  <a name="BKMK_SoftwareFamilies"></a> Famílias de software  
 As famílias de software do Asset Intelligence são utilizadas para definir mais pormenorizadamente os títulos de software inventariado dentro de categorias de software. Por exemplo, uma categoria de software poderá ser empresas de energia e uma família de software dentro dessa categoria de software poderá ser petróleo e gás ou hidroelétrica. Muitas famílias de software estão predefinidas no catálogo do Asset Intelligence e outras famílias definidas pelo utilizador podem ser criadas para definir mais pormenorizadamente o software inventariado. O estado de validação para todas as famílias predefinidas de software é sempre **Validado**, enquanto o estado das informações de famílias personalizadas de software adicionadas ao catálogo do Asset Intelligence é **Definido pelo Utilizador**.  

 Utilize o procedimento seguinte para criar uma família de software definida pelo utilizador.  

##### <a name="to-create-a-user-defined-software-family"></a>Para criar uma família de software definida pelo utilizador  

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  

2.  Na área de trabalho **Ativos e Compatibilidade** , clique em **Asset Intelligence**e, em seguida, clique em **Catálogo**.  

3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Família de Software**.  

4.  Na página **Geral** , introduza um nome para a nova família de software e, opcionalmente, uma descrição.  

    > [!NOTE]  
    >  O estado de validação para todas as novas famílias personalizadas de software está sempre definido como **Definido pelo Utilizador**.  

5.  Na página **Resumo** , reveja as definições e clique em **Seguinte**.  

6.  Na página **Conclusão** , clique em **Fechar** para sair do assistente.  

###  <a name="BKMK_SoftwareLabels"></a> Etiquetas de software  
 As etiquetas personalizadas de software do Asset Intelligence permitem criar filtros que poderá utilizar para agrupar títulos de software e visualizá-los através de relatórios do Asset Intelligence. Por exemplo, pode criar uma etiqueta de software denominada shareware, associá-la a um número de aplicações e, em seguida, executar um relatório que mostre todos os títulos com a etiqueta de software «shareware». O estado de validação é **Definido pelo Utilizador** para todas as etiquetas personalizadas de software que adiciona ao catálogo do Asset Intelligence.  

 Utilize o procedimento seguinte para criar uma etiqueta personalizada definida pelo utilizador.  

##### <a name="to-create-a-user-defined-software-label"></a>Para criar uma etiqueta de software definida pelo utilizador  

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  

2.  Na área de trabalho **Ativos e Compatibilidade** , clique em **Asset Intelligence**e, em seguida, clique em **Catálogo**.  

3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Etiqueta de Software**.  

4.  Na página **Geral** , introduza um nome para a nova família de software e, opcionalmente, uma descrição.  

    > [!NOTE]  
    >  O estado de validação para todas as novas etiquetas personalizadas de software está sempre definido como **Definido pelo Utilizador**.  

5.  Na página **Resumo** , reveja as definições e clique em **Seguinte**.  

6.  Na página **Conclusão** , clique em **Fechar** para sair do assistente.  

###  <a name="BKMK_HardwareRequirements"></a> Requisitos de hardware  
 As informações de requisitos de hardware podem ajudar a verificar se os computadores cumprem os requisitos de hardware para títulos de software antes de terem como destino implementações de software. Muitos requisitos de hardware estão predefinidos no catálogo do Asset Intelligence e poderá criar novas informações de requisitos de hardware definidos pelo utilizador para satisfazer requisitos personalizados. O estado de validação para todos os requisitos de hardware predefinidos é sempre **Validado**, enquanto o estado das informações de requisitos de hardware definidos pelo utilizador adicionados ao catálogo do Asset Intelligence é **Definido pelo Utilizador**.  

> [!IMPORTANT]  
>  Os requisitos de hardware apresentados na consola do Configuration Manager são obtidos a partir do catálogo do Asset Intelligence no computador local e não se baseiam em informações de títulos de software inventariado de clientes do System Center 2012 Configuration Manager. As informações de requisitos de hardware não são atualizadas como parte do processo de sincronização com o System Center Online. Pode criar requisitos de hardware definidos pelo utilizador para software inventariado, que não tenham requisitos de hardware associados.  

 Utilize o procedimento seguinte para criar um requisito de hardware definido pelo utilizador.  

##### <a name="to-create-a-user-defined-hardware-requirements"></a>Para criar um requisito de hardware definido pelo utilizador  

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  

2.  Na área de trabalho **Ativos e Compatibilidade** , clique em **Asset Intelligence**e, em seguida, clique em **Requisitos de Hardware**.  

3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Requisitos de Hardware**.  

4.  Na página **Geral** , introduza as seguintes informações:  

    1.  **Título de software**: Especifica o título de software para os quais os requisitos de hardware estão associados. O título de software não pode existir já no catálogo do Asset Intelligence.  

    2.  **Estado de validação**: Apresenta o estado de validação como **definido pelo utilizador** para os requisitos de hardware. Não é possível modificar esta definição.  

    3.  **Mínima da CPU (MHz)**: Especifica a velocidade mínima do processador, em megahertz (MHz), necessária para o título de software.  

    4.  **RAM mínima (KB)**: Especifica a RAM mínima, em quilobytes (KB), necessárias para o título de software.  

    5.  **Espaço mínimo em disco (KB)**: Especifica o espaço mínimo livre em disco, em KB, necessário ao título de software.  

    6.  **Tamanho mínimo do disco (KB)**: Especifica o tamanho de mínima de disco rígido, em KB, necessário ao título de software.  

     Clique em **Seguinte**.  

5.  Na página **Resumo** , reveja as definições e clique em **Seguinte**.  

6.  Na página **Conclusão** , clique em **Fechar** para sair do assistente.  

###  <a name="BKMK_ModifyCategorization"></a> Modificar informações de categorização para software inventariado  
 O software predefinido no catálogo do Asset Intelligence está configurado com informações de categorização específicas, tais como o nome do produto, fornecedor, categoria de software e família de software. Quando as informações de categorização predefinidas não cumprem os requisitos, pode modificar as informações nas propriedades para o título de software. Quando modificar as informações de categorização para software predefinido, o estado de validação do software é alterado de **Validado** para **Definido pelo Utilizador**.  

> [!IMPORTANT]  
>  As informações de categorização só podem ser modificadas no site de nível superior.  

 Utilize o procedimento seguinte para modificar informações de categorização para software inventariado.  

##### <a name="to-modify-the-categorizations-for-software-titles"></a>Para modificar as categorizações para títulos de software  

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  

2.  Na área de trabalho **Ativos e Compatibilidade** , clique em **Asset Intelligence**e, em seguida, clique em **Software inventariado**.  

3.  Selecione um título de software ou vários títulos de software para os quais pretenda modificar as categorizações.  

4.  No separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.  

5.  No separador **Geral** , pode modificar as seguintes informações de categorização:  

    -   **Nome do produto**: Especifica o nome do título de software inventariado.  

    -   **Fornecedor**: Especifica o nome do fornecedor que desenvolveu o título de software inventariado.  

    -   **Categoria**: Especifica a categoria de software que está atualmente atribuída ao título de software inventariado.  

    -   **Família**: Especifica a família de software que está atualmente atribuída ao título de software inventariado.  

6.  Clique em **OK** para guardar as alterações.  

 Utilize o procedimento seguinte para reverter o software para as informações de categorização originais.  

### <a name="revert-categorization-information-to-original-settings-for-software"></a>Reverter informações de categorização para as definições originais do software  
 O Configuration Manager armazena informações de categorização obtidas a partir do System Center Online na base de dados. Não é possível eliminar as informações. Depois de as informações terem sido modificadas, pode reverter as informações de categorização novamente para a categorização do System Center Online. Também é possível reverter o software inventariado que não se encontra no catálogo do Asset Intelligence para as definições originais.  

 Utilize o procedimento seguinte para reverter informações de categorização para as definições originais.  

##### <a name="to-revert-categorization-information-to-original-settings"></a>Para reverter informações de categorização para as definições originais  

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  

2.  Na área de trabalho **Ativos e Compatibilidade** , clique em **Asset Intelligence**e, em seguida, clique em **Software inventariado**.  

3.  Selecione um título de software ou vários títulos de software que pretenda reverter para as definições originais. Só é possível reverter software com o estado **Definido pelo Utilizador** .  

    > [!TIP]  
    >  Clique na coluna **Estado** para ordenar pelo estado de validação. A ordenação permite-lhe ver todo o software por estado de validação e selecionar rapidamente vários itens para reverter para as definições originais.  

4.  No separador **Home Page** , no grupo **Produto** , clique em **Reverter**.  

5.  Clique em **Sim** para reverter o software para as informações de categorização originais.  

6.  Ao reverter as informações de categorização de software que se encontra no catálogo do Asset Intelligence, o estado de validação é alterado de **Definido pelo Utilizador** para **Validado**. Ao reverter software que não se encontra no catálogo, o estado de validação é alterado de **Definido pelo Utilizador** para **Não Categorizado**.  

##  <a name="BKMK_RequestCatalogUpdate"></a> Pedir uma atualização de catálogo para títulos de software não categorizados  
 As informações de títulos de software não categorizados podem ser submetidas para o System Center Online para investigação e categorização. Depois de um título de software não categorizado ser submetido, e caso existam, pelo menos, 4 pedidos de categorização de clientes para o mesmo título de software, os investigadores identificam, categorizam e disponibilizam as informações de categorização do título de software para todos os clientes que estejam a utilizar o serviço System Center Online. A Microsoft dá máxima prioridade aos títulos de software que tenham o maior número de pedidos de categorização. É improvável que as aplicações personalizadas de linha de negócio e de software recebam uma categoria e, como melhor prática, o utilizador não deve enviar estes títulos de software à Microsoft para categorização.  

 Quando as informações de título de software são submetidas ao System Center Online para categorização, aplicam-se as seguintes condições:  

-   Apenas as informações básicas de títulos de software são transmitidas ao System Center Online e as informações de títulos de software a categorizar podem ser revistas antes do envio.  

-   As informações de licença de software nunca são transmitidas.  

-   Qualquer título de software que seja carregado fica publicamente disponível como parte do catálogo do System Center Online e pode ser transferido por outros clientes.  

-   A origem do título de software não é armazenada no catálogo do System Center Online. No entanto, os títulos de aplicações que contenham informações confidenciais ou de propriedade não devem ser submetidos para categorização pelo System Center Online.  

> [!NOTE]  
>  Para obter mais informações sobre as informações de privacidade do Asset Intelligence, consulte [segurança e privacidade do Asset Intelligence no System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/security-and-privacy-for-asset-intelligence.md).  

 Utilize o procedimento seguinte para pedir a categorização de títulos de software do catálogo do Asset Intelligence a partir do System Center Online.  

#### <a name="to-request-a-catalog-update-for-uncategorized-software-titles"></a>Para pedir uma atualização de catálogo para títulos de software não categorizados  

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  

2.  Na área de trabalho **Ativos e Compatibilidade** , clique em **Asset Intelligence**e, em seguida, clique em **Software inventariado**.  

3.  Selecione o nome de um produto ou vários nomes de produtos para submeter para o System Center Online para categorização. Apenas os títulos de software inventariado não categorizados podem ser submetidos para o System Center Online for categorização. Se um título de software inventariado tiver sido categorizado por um administrador, resultando num estado definido pelo utilizador, terá de clicar com o botão direito do rato no título de software inventariado e, em seguida, clicar em **Reverter** para reverter o título de software para o estado **Não Categorizado** , para que possa ser submetido para o System Center Online para categorização.  

    > [!NOTE]  
    >  Gestor de configuração pode processar até 100 títulos de software para categorização de cada vez. Se selecionar mais do que 100 títulos de software, apenas são processados os primeiros 100 títulos de software. Tem de selecionar os restantes títulos de software para categorização em lotes de menos de 100.  

    > [!TIP]  
    >  Clique na coluna **Estado** para ordenar pelo estado de validação. Isto permite-lhe ver todos os nomes de produto não categorizados e selecionar rapidamente vários itens para submeter para categorização.  

4.  No separador **Home Page** , no grupo **Produto** , clique em **Pedir Atualização de Catálogo**.  

5.  Reveja a mensagem de privacidade de submissão de categorização do System Center Online. Clique em **Detalhes** para ver as informações que serão enviadas para o System Center Online.  

6.  Selecione **Li e compreendi esta mensagem**e, em seguida, clique em **OK** para permitir que os títulos de software selecionados sejam submetidos para categorização.  

7.  Verifique se o estado dos nomes de produtos de software inventariado submetidos para o System Center Online para categorização mudou de **Não Categorizado** para **Pendente**.  

    > [!NOTE]  
    >  O software submetido para o System Center Online para categorização com o estado de validação **Pendente** num site de administração central ainda é apresentado com o estado de validação **Não Categorizado** em sites primários subordinados.  

##  <a name="BKMK_ResolveSoftwareDetails"></a> Resolver conflitos de detalhes de software  
 Depois de os detalhes de categorização de software recentemente atualizados serem recebidos do System Center Online, que estão em conflito com os detalhes de software existentes, pode escolher como resolver o conflito. O software que tem um conflito atual tem o estado de validação **Atualizável**. Depois de um conflito de detalhes de software ser resolvido, as informações de categorização de software são mantidas no catálogo do Asset Intelligence, de acordo com a definição que especificar. Um conflito de detalhes de software não ocorrerá novamente para o mesmo valor de categorização de software, a menos que o valor do System Center Online seja alterado após a resolução do conflito.  

 Utilize o procedimento seguinte para resolver um conflito de detalhes de software.  

#### <a name="to-resolve-a-software-details-conflict"></a>Para resolver um conflito de detalhes de software  

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  

2.  Na área de trabalho **Ativos e Compatibilidade** , clique em **Asset Intelligence**e, em seguida, clique em **Software inventariado**.  

3.  Reveja a coluna **Estado** para ver os títulos de software no estado **Atualizável** .  

4.  Selecione o título de software para o qual tenha de resolver um conflito e, em seguida, no separador **Home Page** , no grupo **Produto** , clique em **Resolver Conflito**.  

5.  Reveja as seguintes informações:  

    -   **Valor local**: Especifica as informações de categorização de software existentes no catálogo do Asset Intelligence que entram em conflito com detalhes de categorização de software do System Center Online mais recentes.  

    -   **Valor transferido**: Especifica as novas informações de categorização de software System Center Online para em conflito informações de categorização do software de catálogo do Asset Intelligence.  

6.  Selecione uma das seguintes definições para resolver o conflito de detalhes de software:  

    -   **Não altere o valor de informações de catálogo localmente editado**: Resolve o conflito de detalhes de software ao manter as existentes informações de categorização de software do catálogo do Asset Intelligence. Quando seleciona esta definição, o estado do título de software é alterado de **Atualizável** para **Definido pelo Utilizador**.  

    -   **Substituir o valor de informações de catálogo localmente editado com o valor de System Center Online transferido**: Resolve o conflito de detalhes de software ao substituir as existentes informações de categorização de software do catálogo do Asset Intelligence pelas novas informações obtidas do System Center Online. Quando seleciona esta definição, o estado do título de software é alterado de **Atualizável** para **Validado**.  

     Clique em **OK** para guardar a resolução de conflito.  
