---
title: "Criar relatórios personalizados | Microsoft Docs"
description: "Definir modelos de relatórios para satisfazer os seus requisitos empresariais e, em seguida, implementar modelos de relatórios no Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f2df88b4-c348-4dcf-854a-54fd6eedf485
caps.latest.revision: "5"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 9951dd9333ebef00c7acd5d72b20a02382e3206c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="creating-custom-report-models-for-system-center-configuration-manager-in-sql-server-reporting-services"></a>Criar modelos de relatórios personalizados para o System Center Configuration Manager no SQL Server Reporting Services

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Modelos de relatórios de exemplo estão incluídos no System Center Configuration Manager, mas pode também definir modelos de relatórios que satisfaçam os seus requisitos de negócio e, em seguida, implementar o modelo de relatório para o Configuration Manager para utilizar quando criar novos relatórios baseados em modelos. A tabela seguinte fornece os passos para criar e implementar um modelo de relatório básico.  

> [!NOTE]  
>  Consulte os passos de criação de um modelo de relatório mais avançado na secção [Steps for Creating an Advanced Report Model in SQL Server Reporting Services](#AdvancedReportModel) deste tópico.  

|Passo|Descrição|Mais informações|  
|----------|-----------------|----------------------|  
|Verificar se o SQL Server Business Intelligence Development Studio está instalado|Os modelos de relatórios são concebidos e criados utilizando o SQL Server Business Intelligence Development Studio. Certifique-se de que o SQL Server Business Intelligence Development Studio se encontra instalado no computador em que estiver a criar o modelo de relatório personalizado.|Para mais informações sobre o SQL Server Business Intelligence Development Studio, consulte a documentação do SQL Server 2008.|  
|Criar um projeto de modelo de relatório|Um projeto de modelo de relatório contém a definição da origem de dados (um ficheiro .ds), a definição de uma vista de origem de dados (um ficheiro .dsv) e o modelo de relatório (um ficheiro .smdl).|Para obter mais informações, consulte a secção [To create the report model project](#BKMK_CreateReportModelProject) neste tópico.|  
|Definir uma origem de dados para um modelo de relatório|Depois de criar um projeto de modelo de relatório, terá de definir uma origem de dados a partir da qual extrair os dados de negócio. Normalmente, esta é a base de dados do site do Configuration Manager.|Para obter mais informações, consulte a secção [To define the data source for the report model](#BKMK_DefineReportModelDataSource) neste tópico.|  
|Definir uma vista de origem de dados para um modelo de relatório|Após definir as origens de dados que utiliza no seu projeto de modelo de relatório, o passo seguinte será definir uma vista de origem de dados para o projeto. Uma vista de origem de dados é um modelo de dados lógico baseado numa ou mais origens de dados. As vistas de origem de dados encapsulam o acesso aos objetos físicos, tais como tabelas e vistas, contidos nas origens de dados subjacentes. O SQL Server Reporting Services gera o modelo de relatório a partir da vista de origem de dados.<br /><br /> As vistas de origem de dados facilitam o processo de criação do modelo, fornecendo uma representação útil dos dados que especificou. Sem alterar a origem de dados subjacente, poderá mudar o nome de tabelas e campos e adicionar campos agregados e tabelas derivadas numa vista de origem de dados. Para um modelo eficiente, adicione apenas à vista de origem de dados as tabelas que pretender utilizar.|Para obter mais informações, consulte a secção [Para definir a vista de origem de dados para o modelo de relatório](#BKMK_DefineReportModelDataSourceView) neste tópico.|  
|Criar um modelo de relatório|Um modelo de relatório é uma camada sobreposta a uma base de dados que identifica as entidades de negócio, campos e funções. Quando publicado utilizando estes modelos, os utilizadores do Report Builder poderão desenvolver relatórios sem terem de se familiarizar com as estruturas de bases de dados nem compreender e escrever consultas. Os modelos são compostos por conjuntos de itens de relatório relacionados, agrupados sob um nome amigável, com relações predefinidas entre estes itens de negócio e com cálculos predefinidos. Os modelos são definidos utilizando uma linguagem XML denominada SMDL (Semantic Model Definition Language). A extensão do nome de ficheiro dos modelos de relatório é .smdl.|Para obter mais informações, consulte a secção [To create the report model](#BKMK_CreateReportModel) neste tópico.|  
|Publicar um modelo de relatório|Para criar um relatório utilizando o modelo que acabou de criar, terá de o publicar num servidor de relatórios. A origem de dados e a vista de origem de dados serão incluídas no modelo, quando este for publicado.|Para obter mais informações, consulte a secção [To publish the report model for use in SQL Server Reporting Services](#BKMK_PublishReportModel) neste tópico.|  
|Implementar o modelo de relatório do Configuration Manager|Antes de poder utilizar um modelo de relatório personalizado no **Assistente para criar relatório** para criar um relatório baseado num modelo, terá de implementar o modelo de relatório do Configuration Manager.|Para obter mais informações, consulte a secção [To deploy the custom report model to Configuration Manager](#BKMK_DeployReportModel) neste tópico.|  

## <a name="steps-for-creating-a-basic-report-model-in-sql-server-reporting-services"></a>Passos para criar um modelo de relatório básico no SQL Server Reporting Services  
 Pode utilizar os procedimentos seguintes para criar um modelo de relatório básico que os utilizadores do seu site poderão usar para criar relatórios baseados em modelos específicos com base nos dados de uma única vista da base de dados do Configuration Manager. Crie um modelo de relatório que apresente as informações sobre os computadores cliente do site ao autor do relatório. Estas informações são obtidas a partir de **v_R_System** vista na base de dados do Configuration Manager.  

 No computador em que executar estes procedimentos, certifique-se de que instalou o SQL Server Business Intelligence Development Studio e de que o computador possui conectividade de rede para o servidor do ponto do Reporting Services. Para obter informações detalhadas sobre o SQL Server Business Intelligence Development Studio, consulte a documentação do SQL Server 2008.  

###  <a name="BKMK_CreateReportModelProject"></a> To create the report model project  

1.  No ambiente de trabalho, clique em **Iniciar**, clique em **Microsoft SQL Server 2008**e clique em **SQL Server Business Intelligence Development Studio**.  

2.  Após o **SQL Server Business Intelligence Development Studio** ser apresentado no Microsoft Visual Studio, clique em **Ficheiro**, clique em **Novo**e clique em **Projeto**.  

3.  Na caixa de diálogo **Novo Projeto** , selecione **Projeto de Modelo de Relatório** na lista **Modelos** .  

4.  Na caixa **Nome** , especifique um nome para este modelo de relatório. Para este exemplo, digite **Simple_Model**.  

5.  Para criar o projeto de modelo de relatório, clique em **OK**.  

6.  A solução **Simple_Model** é apresentada no **Solution Explorer**.  

    > [!NOTE]  
    >  Se o painel do **Solution Explorer** não for apresentado, clique em **Ver**e clique em **Solution Explorer**.  

###  <a name="BKMK_DefineReportModelDataSource"></a>Para definir a origem de dados para o modelo de relatório  

1.  No painel **Solution Explorer** do **SQL Server Business Intelligence Development Studio**, clique com o botão direito do rato em **Origens de Dados** e selecione **Adicionar Nova Origem de Dados**.  

2.  Na página **Bem-vindo ao Assistente de Origem de Dados** , clique em **Seguinte**.  

3.  Na página **Selecione como definir a ligação** , certifique-se de que a opção **Criar uma origem de dados com base numa ligação nova ou existente** se encontra selecionada e clique em **Novo**.  

4.  Na caixa de diálogo **Gestor de Ligações** , especifique as seguintes propriedades de ligação para a origem de dados:  

    -   **Nome do servidor**: Escreva o nome do seu servidor de base de dados do site do Configuration Manager ou selecione-o na lista. Se estiver a trabalhar com uma instância nomeada em vez da instância predefinida, escreva &lt; *servidor de base de dados*>\\&lt;*nome da instância*>.  

    -   Selecione **Utilizar Autenticação do Windows**.  

    -   No **selecione ou introduza um nome de base de dados** lista, selecione o nome da sua base de dados do site do Configuration Manager.  

5.  Para verificar a ligação à base de dados, clique em **Testar Ligação**.  

6.  Se a ligação tiver êxito, clique em **OK** para fechar a caixa de diálogo **Gestor de Ligações** . Se a ligação não tiver êxito, verifique se as informações que introduziu estão corretas e clique novamente em **Testar Ligação** .  

7.  Na página **Selecione como definir a ligação** , certifique-se de que a opção **Criar uma origem de dados com base numa ligação nova ou existente** se encontra selecionada, verifique se a origem de dados que acabou de especificar se encontra selecionada em **Ligações de dados**e clique em **Seguinte**.  

8.  Em **Nome da origem de dados**, especifique um nome para a origem de dados e clique em **Concluir**. Para este exemplo, digite **Simple_Model**.  

9. A origem de dados **Simple_Model.ds** é apresentada no **Solution Explorer** , sob o nó **Origens de Dados** .  

    > [!NOTE]  
    >  Para editar as propriedades de uma origem de dados existente, faça duplo clique na origem de dados na pasta **Origens de Dados** do painel do **Solution Explorer** para apresentar as propriedades da origem de dados no Estruturador de Origens de Dados.  

###  <a name="BKMK_DefineReportModelDataSourceView"></a>Para definir a vista de origem de dados para o modelo de relatório  

1.  No **Solution Explorer**, clique com o botão direito do rato em **Vistas de Origem de Dados** e selecione **Adicionar Nova Vista de Origem de Dados**.  

2.  Na página **Bem-vindo ao Assistente de Vista de Origem de Dados** , clique em **Seguinte**. É apresentada a página **Selecionar uma Origem de Dados** .  

3.  Na janela **Origens de dados relacionais** , certifique-se de que a origem de dados **Simple_Model** se encontra selecionada e clique em **Seguinte**.  

4.  Na página **Selecionar Tabelas e Vistas** , selecione a vista seguinte na lista **Objetos disponíveis** para utilizar no modelo de relatório: **v_R_System (dbo)**.  

    > [!TIP]  
    >  Para ajudar a localizar as vistas na lista **Objetos disponíveis** , clique no cabeçalho **Nome** na parte superior da lista para ordenar os objetos por ordem alfabética.  

5.  Após selecionar a vista, clique em **>** para transferir o objeto para a lista **Objetos incluídos** .  

6.  Se a página **Correspondência de Nomes** for apresentada, aceite as seleções predefinidas e clique em **Seguinte**.  

7.  Quando tiver selecionado os objetos de que necessitar, clique em **Seguinte**e especifique um nome para a vista de origem de dados. Para este exemplo, digite **Simple_Model**.  

8.  Clique em **Concluir**. A vista de origem de dados **Simple_Model.dsv** é apresentada na pasta **Vistas de Origem de Dados** do **Solution Explorer**.  

###  <a name="BKMK_CreateReportModel"></a> To create the report model  

1.  No **Solution Explorer**, clique com o botão direito do rato em **Modelos de Relatório** e selecione **Adicionar Novo Modelo de Relatório**.  

2.  Na página **Bem-vindo ao Assistente de Modelos de Relatório** , clique em **Seguinte**.  

3.  Na página **Selecionar Vistas de Origem de Dados** , selecione a vista de origem de dados na lista **Vistas de origem de dados disponíveis** e clique em **Seguinte**. Para este exemplo, selecione **Simple_Model.dsv**.  

4.  Na página **Selecionar regras de geração de modelos de relatório** , aceite os valores predefinidos e clique em **Seguinte**.  

5.  Na página **Recolher Estatísticas de Modelo** , certifique-se de que a opção **Atualizar estatísticas de modelo antes de gerar** se encontra selecionada e clique em **Seguinte**.  

6.  Na página **A Concluir o Assistente** , especifique um nome para o modelo de relatório. Para este exemplo, verifique se é apresentado **Simple_Model** .  

7.  Para concluir o assistente e criar o modelo de relatório, clique em **Executar**.  

8.  Para sair do assistente, clique em **Concluir**. O modelo de relatório é apresentado na janela Estrutura.  

###  <a name="BKMK_PublishReportModel"></a>Para publicar o modelo de relatório para utilização no SQL Server Reporting Services  

1.  No **Solution Explorer**, clique com o botão direito do rato no modelo de relatório e selecione **Implementar**. Neste exemplo, o modelo de relatório é **Simple_Model.smdl**.  

2.  Examine o estado da implementação no canto inferior esquerdo da janela **SQL Server Business Intelligence Development Studio** . Quando a implementação estiver concluída, será apresentado **Implementação com Êxito** . Se a implementação falhar, o motivo da falha será apresentado na janela **Saída** . O novo modelo de relatório está agora disponível no Web site do SQL Server Reporting Services.  

3.  Clique em **Ficheiro**, clique em **Guardar Tudo**e feche o **SQL Server Business Intelligence Development Studio**.  

###  <a name="BKMK_DeployReportModel"></a> To deploy the custom report model to Configuration Manager  

1.  Localize a pasta em que criou o projeto de modelo de relatório. Por exemplo, %*USERPROFILE*%\Documents\Visual Studio 2008\Projects\\*&lt;nome do projeto\>.*  

2.  Copie os ficheiros seguintes da pasta do projeto de modelo de relatório para uma pasta temporária no seu computador:  

    -   *&lt;Nome de modelo\>*  **. DSV**  

    -   *&lt;Nome de modelo\>*  **. smdl**  

3.  Abra os ficheiros acima referidos utilizando um editor de texto, como o Bloco de Notas.  

4.  No ficheiro  *&lt;nome do modelo\>***. DSV**, localize a primeira linha do ficheiro, que lê da seguinte forma:  

     **&lt;DataSourceView xmlns = "http://schemas.microsoft.com/analysisservices/2003/engine"\>**  

     Edite esta linha para:  

     **&lt;DataSourceView xmlns = "http://schemas.microsoft.com/analysisservices/2003/engine" xmlns:xsi = "RelationalDataSourceView"\>**  

5.  Copie todo o conteúdo do ficheiro para a Área de Transferência do Windows.  

6.  Feche o ficheiro  *&lt;nome do modelo\>***. DSV**.  

7.  No ficheiro  *&lt;nome do modelo\>***. smdl**, localize as últimas três linhas do ficheiro, que são apresentados da seguinte forma:  

     `</Entity>`  

     `</Entities>`  

     `</SemanticModel>`  

8.  Colar o conteúdo do ficheiro  *&lt;nome do modelo\>***. DSV** imediatamente antes da última linha do ficheiro (**&lt;SemanticModel\>**).  

9. Guarde e feche o ficheiro  *&lt;nome do modelo\>***. smdl**.  

10. Copie o ficheiro  *&lt;nome do modelo\>***. smdl** para a pasta *% programfiles %*\Microsoft do Configuration Manager \AdminConsole\XmlStorage\Other no servidor de site do Configuration Manager.  

    > [!IMPORTANT]  
    >  Depois de copiar o ficheiro de modelo de relatório para o servidor de site do Configuration Manager, tem de sair e reiniciar a consola do Configuration Manager antes de poder utilizar o modelo de relatório a **Assistente para criar relatório**.  

##  <a name="AdvancedReportModel"></a>Passos para criar um modelo de relatório avançado no SQL Server Reporting Services  
 Pode utilizar os procedimentos seguintes para criar um modelo de relatório avançado que os utilizadores do seu site poderão usar para criar relatórios baseados em modelos específicos com base nos dados de várias vistas da base de dados do Configuration Manager. Crie um modelo de relatório que apresente as informações sobre os computadores cliente e sobre o sistema operativo instalado nesses computadores ao autor do relatório. Estas informações são obtidas a partir das seguintes vistas na base de dados do Configuration Manager:  

-   **V_R_System**: Contém informações sobre computadores detetados e o cliente do Configuration Manager.  

-   **V_GS_OPERATING_SYSTEM**: Contém informações sobre o sistema operativo instalado no computador cliente.  

 Os itens selecionados nas vistas anteriores são consolidados numa lista, recebem nomes amigáveis e são apresentados ao autor do relatório no Report Builder para inclusão em determinados relatórios.  

 No computador em que executar estes procedimentos, certifique-se de que instalou o SQL Server Business Intelligence Development Studio e de que o computador possui conectividade de rede para o servidor do ponto do Reporting Services. Para obter informações detalhadas sobre o SQL Server Business Intelligence Development Studio, consulte a documentação do SQL Server.  

#### <a name="to-create-the-report-model-project"></a>To create the report model project  

1.  No ambiente de trabalho, clique em **Iniciar**, clique em **Microsoft SQL Server 2008**e clique em **SQL Server Business Intelligence Development Studio**.  

2.  Após o **SQL Server Business Intelligence Development Studio** ser apresentado no Microsoft Visual Studio, clique em **Ficheiro**, clique em **Novo**e clique em **Projeto**.  

3.  Na caixa de diálogo **Novo Projeto** , selecione **Projeto de Modelo de Relatório** na lista **Modelos** .  

4.  Na caixa **Nome** , especifique um nome para este modelo de relatório. Para este exemplo, digite **Advanced_Model**.  

5.  Para criar o projeto de modelo de relatório, clique em **OK**.  

6.  A solução **Advanced_Model** é apresentada no **Solution Explorer**.  

    > [!NOTE]  
    >  Se o painel do **Solution Explorer** não for apresentado, clique em **Ver**e clique em **Solution Explorer**.  

#### <a name="to-define-the-data-source-for-the-report-model"></a>Para definir a origem de dados para o modelo de relatório  

1.  No painel **Solution Explorer** do **SQL Server Business Intelligence Development Studio**, clique com o botão direito do rato em **Origens de Dados** e selecione **Adicionar Nova Origem de Dados**.  

2.  Na página **Bem-vindo ao Assistente de Origem de Dados** , clique em **Seguinte**.  

3.  Na página **Selecione como definir a ligação** , certifique-se de que a opção **Criar uma origem de dados com base numa ligação nova ou existente** se encontra selecionada e clique em **Novo**.  

4.  Na caixa de diálogo **Gestor de Ligações** , especifique as seguintes propriedades de ligação para a origem de dados:  

    -   **Nome do servidor**: Escreva o nome do seu servidor de base de dados do site do Configuration Manager ou selecione-o na lista. Se estiver a trabalhar com uma instância nomeada em vez da instância predefinida, escreva &lt; *servidor de base de dados*>\\&lt;*nome da instância*>.  

    -   Selecione **Utilizar Autenticação do Windows**.  

    -   No **selecione ou introduza um nome de base de dados** lista, selecione o nome da sua base de dados do site do Configuration Manager.  

5.  Para verificar a ligação à base de dados, clique em **Testar Ligação**.  

6.  Se a ligação tiver êxito, clique em **OK** para fechar a caixa de diálogo **Gestor de Ligações** . Se a ligação não tiver êxito, verifique se as informações que introduziu estão corretas e clique novamente em **Testar Ligação** .  

7.  Na página **Selecione como definir a ligação** , certifique-se de que a opção **Criar uma origem de dados com base numa ligação nova ou existente** se encontra selecionada, verifique se a origem de dados que acabou de especificar se encontra selecionada na caixa de listagem **Ligações de dados** e clique em **Seguinte**.  

8.  Em **Nome da origem de dados**, especifique um nome para a origem de dados e clique em **Concluir**. Para este exemplo, digite **Advanced_Model**.  

9. A origem de dados **Advanced_Model.ds** é apresentada no **Solution Explorer** , sob o nó **Origens de Dados** .  

    > [!NOTE]  
    >  Para editar as propriedades de uma origem de dados existente, faça duplo clique na origem de dados na pasta **Origens de Dados** do painel do **Solution Explorer** para apresentar as propriedades da origem de dados no Estruturador de Origens de Dados.  

#### <a name="to-define-the-data-source-view-for-the-report-model"></a>Para definir a vista de origem de dados para o modelo de relatório  

1.  No **Solution Explorer**, clique com o botão direito do rato em **Vistas de Origem de Dados** e selecione **Adicionar Nova Vista de Origem de Dados**.  

2.  Na página **Bem-vindo ao Assistente de Vista de Origem de Dados** , clique em **Seguinte**. É apresentada a página **Selecionar uma Origem de Dados** .  

3.  Na janela **Origens de dados relacionais** , certifique-se de que a origem de dados **Advanced_Model** se encontra selecionada e clique em **Seguinte**.  

4.  Na página **Selecionar Tabelas e Vistas** , na lista **Objetos disponíveis** , selecione as vistas seguintes a utilizar no modelo de relatório:  

    -   **v_R_System (dbo)**  

    -   **v_GS_OPERATING_SYSTEM (dbo)**  

     Após selecionar cada vista, clique em **>** para transferir o objeto para a lista **Objetos incluídos** .  

    > [!TIP]  
    >  Para ajudar a localizar as vistas na lista **Objetos disponíveis** , clique no cabeçalho **Nome** na parte superior da lista para ordenar os objetos por ordem alfabética.  

5.  Se a caixa de diálogo **Correspondência de Nomes** for apresentada, aceite as seleções predefinidas e clique em **Seguinte**.  

6.  Quando tiver selecionado os objetos de que necessita, clique em **Seguinte**e especifique um nome para a vista de origem de dados. Para este exemplo, digite **Advanced_Model**.  

7.  Clique em **Concluir**. A vista de origem de dados **Advanced_Model.dsv** é apresentada na pasta **Vistas de Origem de Dados** do **Solution Explorer**.  

#### <a name="to-define-relationships-in-the-data-source-view"></a>Para definir relações na vista de origem de dados  

1.  No **Solution Explorer**, faça duplo clique em **Advanced_Model.dsv** para abrir a janela Estrutura.  

2.  Clique com o botão direito do rato na barra de título da janela **v_R_System** , selecione **Substituir Tabela**e clique em **Com Nova Consulta Nomeada**.  

3.  Na caixa de diálogo **Criar Consulta Nomeada** , clique no ícone **Adicionar Tabela** (normalmente o último ícone na fita).  

4.  Na caixa de diálogo **Adicionar Tabela** , clique no separador **Vistas** , selecione **V_GS_OPERATING_SYSTEM** na lista e clique em **Adicionar**.  

5.  Clique em **Fechar** para fechar a caixa de diálogo **Adicionar Tabela** .  

6.  Na caixa de diálogo **Criar Consulta Nomeada** , especifique as seguintes informações:  

    -   **Nome:** Especifique o nome para a consulta. Para este exemplo, digite **Advanced_Model**.  

    -   **Descrição:** Especifique uma descrição para a consulta. Para este exemplo, escreva **Exemplo de modelo de relatório do Reporting Services**.  

7.  Na janela **v_R_System** , selecione os seguintes itens na lista de objetos para apresentar no modelo de relatório:  

    -   **ResourceID**  

    -   **ResourceType**  

    -   **Active0**  

    -   **AD_Domain_Name0**  

    -   **AD_SiteName0**  

    -   **Client0**  

    -   **Client_Type0**  

    -   **Client_Version0**  

    -   **CPUType0**  

    -   **Hardware_ID0**  

    -   **User_Domain0**  

    -   **User_Name0**  

    -   **Netbios_Name0**  

    -   **Operating_System_Name_and0**  

8.  Na caixa **v_GS_OPERATING_SYSTEM** , selecione os seguintes itens na lista de objetos para apresentar no modelo de relatório:  

    -   **ResourceID**  

    -   **Caption0**  

    -   **CountryCode0**  

    -   **CSDVersion0**  

    -   **Description0**  

    -   **InstallDate0**  

    -   **LastBootUpTime0**  

    -   **Locale0**  

    -   **Manufacturer0**  

    -   **Version0**  

    -   **WindowsDirectory0**  

9. Para apresentar os objetos destas vistas como uma lista ao autor do relatório, tem de especificar uma relação entre as duas tabelas ou vistas, utilizando uma associação. Para associar as duas vistas, utilize o objeto **ResourceID**que é apresentado em ambas as vistas.  

10. Na janela **v_R_System** , clique e mantenha premido o objeto **ResourceID** e arraste-o para o objeto **ResourceID** na janela **v_GS_OPERATING_SYSTEM** .  

11. Clique em **OK.**  

12. A janela **Advanced_Model** substitui a janela **v_R_System** e contém todos os objetos necessários para o modelo de relatório das vistas **v_R_System** e **v_GS_OPERATING_SYSTEM** . Pode agora eliminar a janela **v_GS_OPERATING_SYSTEM** a partir do Estruturador de Vistas de Origem de Dados. Clique com o botão direito do rato na janela **v_GS_OPERATING_SYSTEM** e selecione **Eliminar Tabela da DSV**. Na caixa de diálogo **Eliminar Objetos** , clique em **OK** para confirmar a eliminação.  

13. Clique em **Ficheiro**e, em seguida, clique em **Guardar Tudo**.  

#### <a name="to-create-the-report-model"></a>To create the report model  

1.  No **Solution Explorer**, clique com o botão direito do rato em **Modelos de Relatório** e selecione **Adicionar Novo Modelo de Relatório**.  

2.  Na página **Bem-vindo ao Assistente de Modelos de Relatório** , clique em **Seguinte**.  

3.  Na página **Selecionar Vista de Origem de Dados** , selecione a vista de origem de dados na lista **Vistas de origem de dados disponíveis** e clique em **Seguinte**. Para este exemplo, selecione **Simple_Model.dsv**.  

4.  Na página **Selecionar regras de geração de modelos de relatório** , não altere os valores predefinidos e clique em **Seguinte**.  

5.  Na página **Recolher Estatísticas de Modelo** , certifique-se de que a opção **Atualizar estatísticas de modelo antes de gerar** se encontra selecionada e clique em **Seguinte**.  

6.  Na página **A Concluir o Assistente** , especifique um nome para o modelo de relatório. Para este exemplo, verifique se é apresentado **Advanced_Model** .  

7.  Para concluir o assistente e criar o modelo de relatório, clique em **Executar**.  

8.  Para sair do assistente, clique em **Concluir**.  

9. O modelo de relatório é apresentado na janela Estrutura.  

#### <a name="to-modify-object-names-in-the-report-model"></a>Para modificar os nomes dos objetos no modelo de relatório  

1.  No **Solution Explorer**, clique com o botão direito do rato no modelo de relatório e selecione **Estruturador de Vistas**. Para este exemplo, selecione **Advanced_Model.dsv**.  

2.  Na vista Estrutura do modelo de relatório, clique com o botão direito do rato num nome de objeto e selecione **Mudar o Nome**.  

3.  Escreva um novo nome para o objeto selecionado e prima Enter. Por exemplo, poderia mudar o nome do objeto **CSD_Version_0** para **Versão de Service Pack do Windows**.  

4.  Quando tiver concluído a mudança do nome de objetos, clique em **Ficheiro**e, em seguida, clique em **Guardar Tudo**.  

#### <a name="to-publish-the-report-model-for-use-in-sql-server-reporting-services"></a>Para publicar o modelo de relatório para utilização no SQL Server Reporting Services  

1.  No **Solution Explorer**, clique com o botão direito do rato em **Advanced_Model.smdl** e selecione **Implementar**.  

2.  Examine o estado da implementação no canto inferior esquerdo da janela **SQL Server Business Intelligence Development Studio** . Quando a implementação estiver concluída, será apresentado **Implementação com Êxito** . Se a implementação falhar, o motivo da falha será apresentado na janela **Saída** . O novo modelo de relatório está agora disponível no Web site do SQL Server Reporting Services.  

3.  Clique em **Ficheiro**, clique em **Guardar Tudo**e feche o **SQL Server Business Intelligence Development Studio**.  

#### <a name="to-deploy-the-custom-report-model-to-configuration-manager"></a>To deploy the custom report model to Configuration Manager  

1.  Localize a pasta em que criou o projeto de modelo de relatório. Por exemplo, %*USERPROFILE*%\Documents\Visual Studio 2008\Projects\\*&lt;nome do projeto\>.*  

2.  Copie os ficheiros seguintes da pasta do projeto de modelo de relatório para uma pasta temporária no seu computador:  

    -   *&lt;Nome de modelo\>*  **. DSV**  

    -   *&lt;Nome de modelo\>*  **. smdl**  

3.  Abra os ficheiros acima referidos utilizando um editor de texto, como o Bloco de Notas.  

4.  No ficheiro  *&lt;nome do modelo\>***. DSV**, localize a primeira linha do ficheiro, que lê da seguinte forma:  

     **&lt;DataSourceView xmlns = "http://schemas.microsoft.com/analysisservices/2003/engine"\>**  

     Edite esta linha para:  

     **&lt;DataSourceView xmlns = "http://schemas.microsoft.com/analysisservices/2003/engine" xmlns:xsi = "RelationalDataSourceView"\>**  

5.  Copie todo o conteúdo do ficheiro para a Área de Transferência do Windows.  

6.  Feche o ficheiro  *&lt;nome do modelo\>***. DSV**.  

7.  No ficheiro  *&lt;nome do modelo\>***. smdl**, localize as últimas três linhas do ficheiro, que são apresentados da seguinte forma:  

     `</Entity>`  

     `</Entities>`  

     `</SemanticModel>`  

8.  Colar o conteúdo do ficheiro  *&lt;nome do modelo\>***. DSV** imediatamente antes da última linha do ficheiro (**&lt;SemanticModel\>**).  

9. Guarde e feche o ficheiro  *&lt;nome do modelo\>***. smdl**.  

10. Copie o ficheiro  *&lt;nome do modelo\>***. smdl** para a pasta *% programfiles %*\Microsoft Configuration Manager\AdminConsole\XmlStorage\Other no servidor do site do Configuration Manager.  

    > [!IMPORTANT]  
    >  Depois de copiar o ficheiro de modelo de relatório para o servidor de site do Configuration Manager, tem de sair e reiniciar a consola do Configuration Manager antes de poder utilizar o modelo de relatório a **Assistente para criar relatório**.  
