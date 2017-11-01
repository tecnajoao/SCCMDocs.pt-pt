---
title: "Operações e manutenção de relatórios "
titleSuffix: Configuration Manager
description: "Saiba os detalhes da gestão de relatórios e subscrições de relatórios no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b89bcfbf-f5b6-4fb1-bb5e-a5cc18ec0c78
caps.latest.revision: "5"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 05a81cdfd46ba2bf0bea17b06bd72f79296b3930
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="operations-and-maintenance-for-reporting-in-system-center-configuration-manager"></a>Operações e manutenção de relatórios no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Depois da infraestrutura no local para relatórios no System Center Configuration Manager, há um número de operações que são geralmente efetuadas para gerir relatórios e subscrições de relatórios.  

##  <a name="BKMK_ManageReports"></a>Gerir relatórios do Configuration Manager  
 Configuration Manager fornece mais de 400 relatórios predefinidos que o ajudam a recolher, organizam e apresentam informações sobre utilizadores, hardware e inventário de software, atualizações de software, aplicações, estado do site e outras operações do Configuration Manager na sua organização. Pode utilizar os relatórios predefinidos tal como estão ou pode modificar um relatório para satisfazer os seus requisitos. Também pode criar o modelo personalizado\-com base e SQL\-com base em relatórios que satisfaçam os requisitos. Utilize as secções seguintes para ajudar a gerir relatórios do Configuration Manager.  

###  <a name="BKMK_RunReport"></a>Executar um relatório do Configuration Manager  
 Relatórios no Configuration Manager são armazenados no SQL Server Reporting Services e os dados compostos no relatório obtidos da base de dados do site do Configuration Manager. Pode aceder a relatórios na consola do Configuration Manager ou utilizando o Gestor de relatórios, que poderá aceder num browser. Pode abrir relatórios em qualquer computador que tenha acesso ao computador que está a executar o SQL Server Reporting Services e tem de ter direitos suficientes para ver os relatórios. Quando executar um relatório, o título do relatório, a descrição e a categoria são apresentados no idioma do sistema operativo local.  

> [!NOTE]  
>  Em algumas não\-inglês idiomas, os carateres poderão não ser corretamente apresentados nos relatórios.  Neste caso, relatórios podem ser visualizados através da web\-com base em Gestor de relatórios ou através da consola do administrador remoto.  

> [!WARNING]  
>  Para executar relatórios, tem de ter **leitura** direitos para o **Site** permissão e o **executar relatório** permissão que está configurado para objetos específicos.  

> [!IMPORTANT]    
> Tem de existir uma confiança bidirecional estabelecida para os utilizadores de um domínio diferente do que a conta de ponto de Reporting Services Servicies com êxito executar relatórios.

> [!NOTE]  
>  Gestor de relatórios é uma web\-com base a ferramenta de gestão e acesso de relatório que utilizar para administrar uma instância de servidor único relatório numa localização remota através de uma ligação HTTP. Pode utilizar Gestor de relatórios para tarefas operacionais, por exemplo, para ver relatórios, modificar propriedades de relatórios e gerir subscrições de relatórios associada. Este tópico fornece os passos para visualizar um relatório e modificar propriedades de relatórios no Gestor de relatórios para mais informações sobre as restantes opções que o Gestor de relatórios fornece, consulte [Gestor de relatórios](http://go.microsoft.com/fwlink/p/?LinkId=224916) no SQL Server 2008 Books Online.  

 Utilize os procedimentos seguintes para executar um relatório do Configuration Manager.  

##### <a name="to-run-a-report-in-the-configuration-manager-console"></a>Para executar um relatório na consola do Configuration Manager  

1.  Na consola do Configuration Manager, clique em **monitorização**.  

2.  No **monitorização** área de trabalho, expanda **relatórios**e, em seguida, clique em **relatórios** para listar os relatórios disponíveis.  

    > [!IMPORTANT]  
    >  Nesta versão do Configuration Manager, o **todo o conteúdo** apresentam apenas pacotes, e não aplicações.  

    > [!TIP]  
    >  Se forem listados quaisquer relatórios, certifique-se de que o ponto do reporting services está instalado e configurado. Para obter mais informações, consulte [configurar relatórios](configuring-reporting.md).  

3.  Selecione o relatório que pretende executar, e, em seguida, no **home page** separador o **grupo de relatórios** secção, clique em **executar** para abrir o relatório.  

4.  Se existirem parâmetros necessários, especifique os parâmetros e, em seguida, clique em **Ver relatório**.  

#### <a name="to-run-a-report-in-a-web-browser"></a>Para executar um relatório num browser  

1.  No seu browser, introduza o URL do Gestor de relatórios, por exemplo, **http:\/\/servidor1\/relatórios**. Pode determinar o URL do Gestor de relatórios no **URL do Gestor de relatórios** página no Reporting Services Configuration Manager.  

2.  No Gestor de relatórios, clique na pasta de relatórios no Configuration Manager, por exemplo, **ConfigMgr\_ACs**.  

    > [!TIP]  
    >  Se forem listados quaisquer relatórios, certifique-se de que o ponto do reporting services está instalado e configurado. Para obter mais informações, consulte [configurar relatórios](configuring-reporting.md).  

3.  Clique na categoria de relatório para o relatório que pretende executar e, em seguida, clique na ligação para o relatório. O relatório é apresentado no Gestor de relatórios.  

4.  Se existirem parâmetros necessários, especifique os parâmetros e, em seguida, clique em **Ver relatório**.  

###  <a name="BKMK_ModifyReportProperties"></a>Modificar as propriedades de um relatório do Configuration Manager  
 Na consola do Configuration Manager, pode ver as propriedades de um relatório, tais como o nome do relatório e a descrição, mas para alterar as propriedades, utilize o Gestor de relatórios. Utilize o procedimento seguinte para modificar as propriedades de um relatório do Configuration Manager.  

#### <a name="to-modify-report-properties-in-report-manager"></a>Para modificar propriedades de relatório no Gestor de relatórios  

1.  No seu browser, introduza o URL do Gestor de relatórios, por exemplo, **http:\/\/servidor1\/relatórios**. Pode determinar o URL do Gestor de relatórios no **URL do Gestor de relatórios** página no Reporting Services Configuration Manager.  

2.  No Gestor de relatórios, clique na pasta de relatórios no Configuration Manager, por exemplo, **ConfigMgr\_ACs**.  

    > [!TIP]  
    >  Se forem listados quaisquer relatórios, certifique-se de que o ponto do Reporting Services está instalado e configurado. Para obter mais informações, consulte [configurar relatórios](configuring-reporting.md)  

3.  Clique na categoria de relatório para o relatório para o qual pretende modificar as propriedades e, em seguida, clique na ligação para o relatório. O relatório é apresentado no Gestor de relatórios.  

4.  Clique em de **propriedades** separador. Pode modificar o nome do relatório e a descrição.  

5.  Quando tiver terminado, clique em **aplicar**. As propriedades de relatório são guardadas no servidor de relatórios e consola do Configuration Manager obtém as propriedades atualizadas para o relatório.  

###  <a name="BKMK_EditReport"></a>Editar um relatório do Configuration Manager  
 Quando um relatório existente do Configuration Manager não obtiver as informações que tem de ter ou não fornecer o esquema ou estrutura pretendidos, pode editar o relatório no Report Builder.  

> [!NOTE]  
>  Também pode optar por clonar um relatório existente, abrindo-o para edição e clicando em **guardar como** para guardá-lo como um novo relatório.  

> [!IMPORTANT]  
>  A conta de utilizador tem de ter **modificar Site** permissão e **modificar relatório** permissões nos objetos específicos associados ao relatório que pretende modificar.  

> [!IMPORTANT]  
>  Quando o Configuration Manager é atualizado para uma versão mais recente, os novos relatórios substituem os relatórios predefinidos. Se modificar um relatório predefinido, tem de copiar o relatório antes de instalar a nova versão e, em seguida, restaure o relatório no Reporting Services. Se estiver a efetuar alterações significativas a um relatório predefinido, considere criar um novo relatório em vez disso. Os novos relatórios que criar antes de atualizar um site não são substituídos.  

 Utilize o procedimento seguinte para editar as propriedades de um relatório do Configuration Manager.  

#### <a name="to-edit-report-properties"></a>Para editar as propriedades de relatório  

1.  Na consola do Configuration Manager, clique em **monitorização**.  

2.  No **monitorização** área de trabalho, expanda **relatórios**e, em seguida, clique em **relatórios** para listar os relatórios disponíveis.  

3.  Selecione o relatório que pretende modificar, e, em seguida, no **home page** separador o **grupo de relatórios** secção, clique em **editar**. Introduza a conta de utilizador e a palavra-passe se for pedido e, em seguida, clique em **OK**. Se o Report Builder não está instalado no computador, lhe for pedido para instalá-lo. Clique em **executar** para instalar o Report Builder, necessário para modificar e criar relatórios.  

4.  No Report Builder, modifique as definições de relatório adequadas e, em seguida, clique em **guardar** para guardar o relatório para o servidor de relatórios.  

###  <a name="BKMK_CreateModelBasedReport"></a>Criar um modelo\-relatório baseado em  
 Um modelo\-com base permite de relatório selecionar interativamente os itens que pretende incluir no relatório. Para obter mais informações sobre como criar modelos de relatórios personalizados, consulte [criar modelos de relatórios personalizados para o System Center Configuration Manager no SQL Server Reporting Services](creating-custom-report-models-in-sql-server-reporting-services.md).  

> [!IMPORTANT]  
>  A conta de utilizador tem de ter **modificar Site** permissão para criar um novo relatório. O utilizador só pode criar um relatório em pastas para a qual o utilizador tem **modificar relatório** permissões.  

 Utilize o procedimento seguinte para criar um modelo\-com base relatório do Configuration Manager.  

#### <a name="to-create-a-model-based-report"></a>Para criar um modelo\-relatório baseado em  

1.  Na consola do Configuration Manager, clique em **monitorização**.  

2.  No **monitorização** área de trabalho, expanda **relatórios** e clique em **relatórios**.  

3.  No **home page** separador o **criar** secção, clique em **criar relatório** para abrir o **Assistente para criar relatório**.  

4.  No **informações** página, configure as seguintes definições:  

    -   **Tipo**: Selecione **modelo\-relatório baseado em** para criar um relatório no Report Builder utilizando um modelo do Reporting Services.  

    -   **Nome**: Especifique um nome para o relatório.  

    -   **Descrição**: Especifique uma descrição para o relatório.  

    -   **Servidor**: Apresenta o nome do servidor de relatórios no qual está a criar este relatório.  

    -   **Caminho**: Clique em **procurar** para especificar uma pasta na qual pretende armazenar o relatório.  

     Clique em **Seguinte**.  

5.  No **seleção do modelo** página, selecione um modelo disponível na lista que é utilizado para criar este relatório. Quando seleciona o modelo de relatório, o **pré-visualização** secção apresenta as vistas do SQL Server e entidades que são disponibilizadas pelo modelo de relatório selecionado.  

6.  Na página **Resumo** , reveja as definições. Clique em **anterior** para alterar as definições ou clique em **seguinte** para criar o relatório no Configuration Manager.  

7.  No **confirmação** página, clique em **fechar** para sair do assistente e reabrir o Report Builder para configurar as definições do relatório. Introduza a conta de utilizador e a palavra-passe se for pedido e, em seguida, clique em **OK**. Se o Report Builder não está instalado no computador, lhe for pedido para instalá-lo. Clique em **executar** para instalar o Report Builder, necessário para modificar e criar relatórios.  

8.  No Microsoft Report Builder, criar o esquema do relatório, selecione os dados nas vistas do SQL Server disponíveis, adicione parâmetros ao relatório e assim sucessivamente. Para obter mais informações sobre como utilizar o Report Builder para criar um novo relatório, consulte a ajuda do Report Builder.  

9. Clique em **executar** para executar o relatório. Certifique-se de que o relatório fornece informações que pretende. Clique em **Design** para regressar à vista estrutura e modificar o relatório, se necessário.  

10. Clique em **guardar** para guardar o relatório para o servidor de relatórios. Pode executar e modificar o novo relatório no **relatórios** no nó de **monitorização** área de trabalho.  

###  <a name="BKMK_CreateSQLBasedReport"></a>Criar um SQL\-relatório baseado em  
 Um SQL\-com base permite relatório obter dados com base na instrução SQL de relatório.  

> [!IMPORTANT]  
>  Quando cria uma instrução SQL para um relatório personalizado, não faça diretamente referência a tabelas do SQL Server. Em alternativa, fazer referência a vistas do SQL Server Reporting Services \(ver os nomes que começam por v\_ \) da base de dados do site. Também pode referenciar procedimentos armazenados públicos \(armazenados nomes que começam por sp\_ \) da base de dados do site.  

> [!IMPORTANT]  
>  A conta de utilizador tem de ter **modificar Site** permissão para criar um novo relatório. O utilizador só pode criar um relatório em pastas para a qual o utilizador tem **modificar relatório** permissões.  

 Utilize o procedimento seguinte para criar um SQL\-com base relatório do Configuration Manager.  

#### <a name="to-create-a-sql-based-report"></a>Para criar um SQL\-relatório baseado em  

1.  Na consola do Configuration Manager, clique em **monitorização**.  

2.  Na área de trabalho **Monitorização** , expanda **Comunicar**e clique em **Relatórios**.  

3.  No **home page** separador o **criar** secção, clique em **criar relatório** para abrir o **Assistente para criar relatório**.  

4.  No **informações** página, configure as seguintes definições:  

    -   **Tipo**: Selecione **SQL\-relatório baseado em** para criar um relatório no Report Builder utilizando uma instrução SQL.  

    -   **Nome**: Especifique um nome para o relatório.  

    -   **Descrição**: Especifique uma descrição para o relatório.  

    -   **Servidor**: Apresenta o nome do servidor de relatórios no qual está a criar este relatório.  

    -   **Caminho**: Clique em **procurar** para especificar uma pasta na qual pretende armazenar o relatório.  

     Clique em **Seguinte**.  

5.  Na página **Resumo** , reveja as definições. Clique em **anterior** para alterar as definições ou clique em **seguinte** para criar o relatório no Configuration Manager.  

6.  No **confirmação** página, clique em **fechar** para sair do assistente e reabrir o Report Builder para configurar as definições de relatório. Introduza a conta de utilizador e a palavra-passe se for pedido e, em seguida, clique em **OK**. Se o Report Builder não está instalado no computador, lhe for pedido para instalá-lo. Clique em **executar** para instalar o Report Builder, necessário para modificar e criar relatórios.  

7.  No Microsoft Report Builder, forneça a instrução SQL para o relatório ou crie-a utilizando colunas nas vistas do SQL Server disponíveis, adicione parâmetros ao relatório e assim sucessivamente.  

8.  Clique em **executar** para executar o relatório. Certifique-se de que o relatório fornece informações que pretende. Clique em **Design** para regressar à vista estrutura e modificar o relatório, se necessário.  

9. Clique em **guardar** para guardar o relatório para o servidor de relatórios. Pode executar o novo relatório no **relatórios** no nó de **monitorização** área de trabalho.  

##  <a name="BKMK_ManageReportSubscriptions"></a>Gerir subscrições de relatórios  
 Subscrições de relatórios no SQL Server Reporting Services permitem configurar a entrega automática de relatórios especificados por correio eletrónico ou uma partilha de ficheiros em intervalos agendados. Utilize o **Assistente para criar subscrição** no System Center 2012 Configuration Manager para configurar subscrições de relatórios.  

###  <a name="BKMK_ReportSubscriptionFileShare"></a>Criar uma subscrição de relatório para entregar um relatório numa partilha de ficheiros  
 Quando cria uma subscrição de relatório para entregar um relatório para uma partilha de ficheiros, o relatório é copiado no formato especificado para a partilha de ficheiros que especificar. Pode subscrever e solicitar a entrega de apenas um relatório a uma hora.  

 Ao contrário dos relatórios alojados e geridos por um servidor de relatórios, relatórios que são entregues a uma pasta partilhada são ficheiros estáticos. As funcionalidades interativas definidas para o relatório não funcionam em relatórios que são armazenados como ficheiros no sistema de ficheiros. As funcionalidades de interação são representadas como elementos estáticos. Se o relatório incluir gráficos, é utilizada a apresentação predefinida. Se o relatório ligar a outro relatório, a ligação é apresentada como texto estático. Se pretender manter as funcionalidades interativas num relatório entregue, utilize em vez disso, entrega de correio eletrónico. Para obter mais informações sobre a entrega de correio eletrónico, consulte o [criar uma subscrição de relatório para entregar um relatório por correio eletrónico](#BKMK_ReportSubscriptionEmail) posterior deste tópico.  

 Quando cria uma subscrição que utiliza a entrega em partilha de ficheiros, tem de especificar uma pasta existente como a pasta de destino. O servidor de relatórios não cria pastas no sistema de ficheiros. A pasta que especificar tem de estar acessível através de uma ligação de rede. Quando especificar a pasta de destino numa subscrição, utilize um caminho UNC e não inclua barras invertidas no caminho da pasta. Por exemplo, é um caminho UNC válido para a pasta de destino: \\ \\ &lt;servername\>\\reportfiles\\operações\\2011.  

 Relatórios podem ser compostos numa variedade de formatos de ficheiro, tais como MHTML ou Excel. Para guardar o relatório no formato de ficheiro específico, selecione esse formato de composição ao criar a sua subscrição. Por exemplo, escolher Excel guarda o relatório como um ficheiro do Microsoft Excel. Embora possa selecionar qualquer formato de composição suportado, alguns formatos funcionam melhor do que outros durante a composição para um ficheiro.  

 Utilize o procedimento seguinte para criar uma subscrição de relatório para entregar um relatório para uma partilha de ficheiros.  

#### <a name="to-create-a-report-subscription-to-deliver-a-report-to-a-file-share"></a>Para criar uma subscrição de relatório para entregar um relatório para uma partilha de ficheiros  

1.  Na consola do Configuration Manager, clique em **monitorização**.  

2.  No **monitorização** área de trabalho, expanda **relatórios** e clique em **relatórios** para listar os relatórios disponíveis. Pode selecionar uma pasta de relatório para listar apenas os relatórios que estão associados essa pasta.  

3.  Selecione o relatório que pretende adicionar à subscrição e, em seguida, no **home page** separador o **grupo de relatórios** secção, clique em **criar subscrição** para abrir o **Assistente para criar subscrição**.  

4.  No **entrega de subscrição** página, configure as seguintes definições:  

    -   Relatório entregue por: Selecione **partilha de ficheiros Windows** para entregar o relatório para uma partilha de ficheiros.  

    -   **Nome de ficheiro**: Especifique o nome de ficheiro para o relatório. Por predefinição, o ficheiro de relatório não inclui uma extensão de nome de ficheiro. Selecione **Adicionar extensão de ficheiro ao criar** para adicionar automaticamente uma extensão de nome de ficheiro a esse relatório com base no formato de composição.  

    -   **Caminho**: Especifique um caminho UNC para uma pasta existente em que pretende enviar o relatório \(por exemplo, \\ \\ &lt;nome do servidor\>\\&lt;partilha de servidor\>\\&lt;à pasta de relatórios\>\).  

        > [!NOTE]  
        >  O nome de utilizador especificado posteriormente nesta página tem de ter acesso a esta partilha de servidor e permissões de escrita na pasta de destino.  

    -   **Formato de composição**: Selecione um dos seguintes formatos para o ficheiro de relatório:  

        -   **Ficheiro XML com dados de relatório**: Guarda o relatório no formato Extensible Markup Language.  

        -   **CSV \(delimitado por vírgulas\)**: Guarda o relatório no vírgulas\-separados\-formato de valores.  

        -   **Ficheiro TIFF**: Guarda o relatório no formato de ficheiro de imagem etiquetados.  

        -   **Acrobat \(PDF\) ficheiro**: Guarda o relatório no formato de documento portátil Acrobat.  

        -   **HTML 4.0**: Guarda o relatório como uma página Web visualizável apenas em browsers que suportam HTML 4.0. O Internet Explorer 5 e versões posteriores suportam HTML 4.0.  

            > [!NOTE]  
            >  Se tiver imagens no relatório, o formato HTML 4.0 não as inclui no ficheiro.  

        -   **MHTML \(arquivo da web\)**: Guarda o relatório no formato MIME HTML \(mhtml\), que é visualizável em muitos browsers.  

        -   **Compositor de RPL**: Guarda o relatório no esquema de página do relatório \(RPL\) formato.  

        -   **Excel**: Guarda o relatório como uma folha de cálculo do Microsoft Excel.  

        -   **Word**: Guarda o relatório como um documento do Microsoft Word.  

    -   **Nome de utilizador**: Especifique uma conta de utilizador do Windows com permissões para aceder a partilha de servidor de destino e a pasta. A conta de utilizador tem de ter acesso a esta partilha de servidor e permissão de escrita na pasta de destino.  

    -   **Palavra-passe**: Especifique a palavra-passe da conta de utilizador do Windows. No **Confirmar palavra-passe**, re\-introduza a palavra-passe.  

    -   Selecione uma das seguintes opções para configurar o comportamento quando existe um ficheiro com o mesmo nome na pasta de destino:  

        -   **Substituir ficheiro existente com uma versão mais recente**: Especifica que quando o ficheiro de relatório já existe, a nova versão substitui-lo.  

        -   **Não substituir um ficheiro existente**: Não especifica que quando o ficheiro de relatório já existe, não existe nenhuma ação.  

        -   **Incrementar nomes de ficheiro são adicionadas novas versões**: Especifica que, quando o ficheiro de relatório já existe, um número é adicionado para o novo relatório para o nome de ficheiro para o distinguir de outras versões.  

    -   **Descrição**: Especifica a descrição para a subscrição do relatório.  

     Clique em **Seguinte**.  

5.  No **agendamento da subscrição** página, selecione uma das seguintes opções de agendamento de entrega para a subscrição de relatório:  

    -   **Utilizar agendamento partilhado**: Um agendamento partilhado é um agendamento definido anteriormente que pode ser utilizado por outras subscrições de relatório. Selecione esta caixa de verificação e, em seguida, selecione um agendamento partilhado na lista se tiver sido especificado algum.  

    -   **Criar novo agendamento**: Configurar a agenda em que executa este relatório, incluindo o intervalo, inicie a hora e data e a data de fim para esta subscrição.  

6.  No **parâmetros de subscrições** página, especifique os parâmetros deste relatório, que são utilizados quando é executado de forma automática. Quando não existem sem parâmetros para o relatório, esta página não é apresentada.  

7.  No **resumo** , reveja as definições de subscrição de relatório. Clique em **anterior** para alterar as definições ou clique em **seguinte** para criar a subscrição de relatório.  

8.  Na página **Conclusão** , clique em **Fechar** para sair do assistente. Certifique-se de que a subscrição do relatório foi criada com êxito. Pode ver e modificar subscrições de relatórios no **subscrições** nó **relatórios** no **monitorização** área de trabalho.  

###  <a name="BKMK_ReportSubscriptionEmail"></a>Criar uma subscrição de relatório para entregar um relatório por correio eletrónico  
 Quando cria uma subscrição de relatório para entregar um relatório por correio eletrónico, é enviado um e-mail para destinatários que configurou e o relatório é incluído como um anexo. O servidor de relatórios não validar endereços de e-mail ou obter endereços de e-mail a partir de um servidor de correio eletrónico. Tem de saber antecipadamente qual e-mail endereços que pretende utilizar. Por predefinição, pode enviar por e-mail relatórios a qualquer conta de e-mail válido dentro ou fora da organização. Pode selecionar uma ou ambas as seguintes opções de entrega de e-mail:  

-   Envie uma notificação e uma hiperligação para o relatório gerado.  

-   Envie um relatório incorporado ou anexado. O formato de composição e o browser determinam se o relatório é incorporado ou anexado. Se o browser suporta HTML 4.0 e MHTML e selecione o MHTML \(arquivo da web\) formato de composição, o relatório é incorporado como parte da mensagem. Todos os outros formatos de composição \(CSV, PDF, Word, e assim sucessivamente\) fornecem relatórios como anexos. O Reporting Services não verifica se o tamanho do anexo ou da mensagem antes de enviar o relatório. Se o anexo ou da mensagem excede o limite máximo permitido pelo servidor de correio, o relatório não for entregue.  

> [!IMPORTANT]  
>  Tem de configurar as definições de correio eletrónico no Reporting Services para o **E-Mail** opção de entrega para estar disponível. Para obter mais informações sobre como configurar as definições de correio eletrónico no Reporting Services, consulte [configurar um servidor de relatórios para entrega de correio eletrónico](http://go.microsoft.com/fwlink/p/?LinkId=226668) no SQL Server Books Online.  

 Utilize o procedimento seguinte para criar uma subscrição de relatório para entregar um relatório por correio eletrónico.  

#### <a name="to-create-a-report-subscription-to-deliver-a-report-by-email"></a>Para criar uma subscrição de relatório para entregar um relatório por correio eletrónico  

-   Na consola do Configuration Manager, clique em **monitorização**.  

-   No **monitorização** área de trabalho, expanda **relatórios** e clique em **relatórios** para listar os relatórios disponíveis. Pode selecionar uma pasta de relatório para listar apenas os relatórios que estão associados essa pasta.  

-   Selecione o relatório que pretende adicionar à subscrição e, em seguida, no **home page** separador o **grupo de relatórios** secção, clique em **criar subscrição** para abrir o **Assistente para criar subscrição**.  

-   No **entrega de subscrição** página, configure as seguintes definições:  

    -   **Relatório entregue por**: Selecione **i\-correio** para entregar o relatório como um anexo numa mensagem de e-mail.  

    -   **Para**: Especifique um endereço de e-mail válido para enviar este relatório.  

        > [!NOTE]  
        >  Pode introduzir vários destinatários de correio eletrónico, separando cada endereço de correio eletrónico com ponto e vírgula.  

    -   **Cc**: Opcionalmente, especifique um endereço de correio eletrónico para copiar este relatório.  

    -   **Bcc**: Opcionalmente, especifique um endereço de correio eletrónico para enviar uma cópia oculta do relatório.  

    -   **Responda a**: Especifique o endereço de resposta a utilizar se o destinatário responder à mensagem de e-mail.  

    -   **Requerente**: Especifique uma linha de assunto para a mensagem de correio eletrónico de subscrição.  

    -   **Prioridade**: Selecione o sinalizador de prioridade desta mensagem de correio eletrónico. Selecione **baixa**, **Normal**, ou **elevada**. A definição de prioridade é utilizada pelo Microsoft Exchange para definir um sinalizador que indica a importância da mensagem de e-mail.  

    -   **Comentário**: Especifique o texto a ser adicionado ao corpo da mensagem de correio eletrónico de subscrição.  

    -   **Descrição**: Especifique a descrição para esta subscrição de relatório.  

    -   **Incluir ligação**: Inclui um URL para o relatório subscrito no corpo da mensagem de correio eletrónico.  

    -   **Incluir relatório**: Especifique que o relatório é anexado ao i\-mensagem de correio. O formato no qual o relatório será anexado é especificado no **formato de composição** lista.  

    -   **Formato de composição**: Selecione um dos seguintes formatos para o relatório anexado:  

        -   **Ficheiro XML com dados de relatório**: Guarda o relatório no formato Extensible Markup Language.  

        -   **CSV \(delimitado por vírgulas\)**: Guarda o relatório no vírgulas\-separados\-formato de valores.  

        -   **Ficheiro TIFF**: Guarda o relatório no formato de ficheiro de imagem etiquetados.  

        -   **Acrobat \(PDF\) ficheiro**: Guarda o relatório no formato de documento portátil Acrobat.  

        -   **MHTML \(arquivo da web\)**: Guarda o relatório no formato MIME HTML \(mhtml\), que é visualizável em muitos browsers.  

        -   **Excel**: Guarda o relatório como uma folha de cálculo do Microsoft Excel.  

        -   **Word**: Guarda o relatório como um documento do Microsoft Word.  

-   No **agendamento da subscrição** página, selecione uma das seguintes opções de agendamento de entrega para a subscrição de relatório:  

    -   **Utilizar agendamento partilhado**: Um agendamento partilhado é um agendamento definido anteriormente que pode ser utilizado por outras subscrições de relatório. Selecione esta caixa de verificação e, em seguida, selecione um agendamento partilhado na lista se tiver sido especificado algum.  

    -   **Criar novo agendamento**: Configure a agenda de execução deste relatório, incluindo o intervalo, a hora de início e a data e a data de fim para esta subscrição.  

-   No **parâmetros de subscrições** página, especifique os parâmetros deste relatório, que são utilizados quando é executado de forma automática. Quando não existem sem parâmetros para o relatório, esta página não é apresentada.  

-   No **resumo** , reveja as definições de subscrição de relatório. Clique em **anterior** para alterar as definições ou clique em **seguinte** para criar a subscrição de relatório.  

-   Na página **Conclusão** , clique em **Fechar** para sair do assistente. Certifique-se de que a subscrição do relatório foi criada com êxito. Pode ver e modificar subscrições de relatórios no **subscrições** nó **relatórios** no **monitorização** área de trabalho.  
