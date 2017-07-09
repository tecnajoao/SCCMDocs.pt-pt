---
title: "Operações e manutenção para relatórios | Microsoft Docs"
description: "Obter os detalhes de gerenciamento de relatórios e assinaturas de relatório no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b89bcfbf-f5b6-4fb1-bb5e-a5cc18ec0c78
caps.latest.revision: 5
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: f62d969dd49fb00b688602128df74b28ff551135
ms.openlocfilehash: df572cd0c64c82e25164430a53e1b893b3ba3cf5
ms.contentlocale: pt-pt
ms.lasthandoff: 06/07/2017


---
# <a name="operations-and-maintenance-for-reporting-in-system-center-configuration-manager"></a>Operações e manutenção para relatórios no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

Após implantar a infraestrutura em vigor para a emissão de relatórios no System Center Configuration Manager, há um número de operações que você poderá realizar para gerenciar relatórios e assinaturas de relatório.  

##  <a name="BKMK_ManageReports"></a>Gerenciar relatórios do Configuration Manager  
 Configuration Manager fornece mais de 400 relatórios predefinidos que ajudarão a coletam, organizam e apresentam informações sobre usuários, hardware e inventário de software, atualizações de software, aplicativos, status do site e outras operações do Configuration Manager na sua organização. Você pode usar os relatórios predefinidos como estão, ou você pode modificar um relatório para atender às suas necessidades. Também é possível criar um modelo personalizado\-com base em SQL e\-com base em relatórios para atender às suas necessidades. Use as seções a seguir para ajudá-lo a gerenciar relatórios do Configuration Manager.  

###  <a name="BKMK_RunReport"></a>Executar um relatório do Configuration Manager  
 Relatórios no Configuration Manager são armazenados no SQL Server Reporting Services e os dados renderizados no relatório são recuperados do banco de dados de site do Configuration Manager. Você pode acessar relatórios no console do Configuration Manager ou usando o Gerenciador de relatórios, acessar em um navegador da web. Você pode abrir relatórios em qualquer computador que tenha acesso ao computador que está executando o SQL Server Reporting Services, e você deve ter direitos suficientes para exibir os relatórios. Quando você executa um relatório, o título do relatório, a descrição e categoria são exibidos no idioma do sistema operacional local.  

> [!NOTE]  
>  Em alguns não\-inglês idiomas, caracteres podem não aparecer corretamente nos relatórios.  Nesse caso, relatórios podem ser exibidos usando a web\-com base em Gerenciador de relatórios ou pelo Console do administrador remoto.  

> [!WARNING]  
>  Para executar relatórios, você deve ter **leitura** direitos para o **Site** permissão e o **executar relatório** permissão que está configurado para objetos específicos.  

> [!IMPORTANT]    
> Deve haver uma relação de confiança bidirecional estabelecida para usuários de um domínio diferente do que a conta do ponto de Reporting Servicies a execução de relatórios com êxito.

> [!NOTE]  
>  Gerenciador de relatórios é uma web\-com base em ferramenta de acesso e gerenciamento de relatórios que você pode usar para administrar uma instância de servidor de relatório único em um local remoto por meio de uma conexão HTTP. Você pode usar o Gerenciador de relatórios para tarefas operacionais como, por exemplo, para exibir relatórios, modificar propriedades de relatórios e gerenciar assinaturas de relatório associado. Este tópico fornece as etapas para exibir um relatório e modificar propriedades de relatório no Gerenciador de relatórios, mas para obter mais informações sobre as outras opções que fornece o Gerenciador de relatórios, consulte [Gerenciador de relatórios](http://go.microsoft.com/fwlink/p/?LinkId=224916) nos Manuais Online do SQL Server 2008.  

 Use os procedimentos a seguir para executar um relatório do Configuration Manager.  

##### <a name="to-run-a-report-in-the-configuration-manager-console"></a>Para executar um relatório no console do Configuration Manager  

1.  No console do Configuration Manager, clique em **monitoramento**.  

2.  No **monitoramento** espaço de trabalho, expanda **relatórios**e, em seguida, clique em **relatórios** para listar os relatórios disponíveis.  

    > [!IMPORTANT]  
    >  Nesta versão do Configuration Manager, o **todo o conteúdo** relatórios exibem somente pacotes e não aplicativos.  

    > [!TIP]  
    >  Se não houver relatórios listados, verifique se que o ponto do reporting services está instalado e configurado. Para obter mais informações, consulte [Configurando reporting](configuring-reporting.md).  

3.  Selecione o relatório que você deseja executar, e, em seguida, no **início** guia o **grupo relatório** seção, clique em **executar** para abrir o relatório.  

4.  Quando houver parâmetros obrigatórios, especifique os parâmetros e, em seguida, clique em **Exibir relatório**.  

#### <a name="to-run-a-report-in-a-web-browser"></a>Para executar um relatório em um navegador da web  

1.  No navegador da web, digite a URL do Gerenciador de relatórios, por exemplo, **http:\/\/Server1\/relatórios**. Você pode determinar a URL do Gerenciador de relatórios no **URL do Report Manager** página no Reporting Services Configuration Manager.  

2.  No Gerenciador de relatórios, clique em pasta de relatórios do Configuration Manager, por exemplo, **ConfigMgr\_CAS**.  

    > [!TIP]  
    >  Se não houver relatórios listados, verifique se que o ponto do reporting services está instalado e configurado. Para obter mais informações, consulte [Configurando reporting](configuring-reporting.md).  

3.  Clique na categoria do relatório que você deseja executar e, em seguida, clique no link para o relatório. O relatório é aberto no Gerenciador de relatórios.  

4.  Quando houver parâmetros obrigatórios, especifique os parâmetros e, em seguida, clique em **Exibir relatório**.  

###  <a name="BKMK_ModifyReportProperties"></a>Modificar as propriedades de um relatório do Configuration Manager  
 No console do Configuration Manager, você pode exibir as propriedades de um relatório, como o nome do relatório e a descrição, mas para alterar as propriedades, use o Gerenciador de relatórios. Use o procedimento a seguir para modificar as propriedades de um relatório do Configuration Manager.  

#### <a name="to-modify-report-properties-in-report-manager"></a>Para modificar propriedades de relatório no Gerenciador de relatórios  

1.  No navegador da web, digite a URL do Gerenciador de relatórios, por exemplo, **http:\/\/Server1\/relatórios**. Você pode determinar a URL do Gerenciador de relatórios no **URL do Report Manager** página no Reporting Services Configuration Manager.  

2.  No Gerenciador de relatórios, clique em pasta de relatórios do Configuration Manager, por exemplo, **ConfigMgr\_CAS**.  

    > [!TIP]  
    >  Se não houver relatórios listados, verifique se que o ponto do Reporting Services está instalado e configurado. Para obter mais informações, consulte [Configurando relatórios](configuring-reporting.md)  

3.  Clique na categoria de relatório para o relatório para o qual você deseja modificar as propriedades e, em seguida, clique no link para o relatório. O relatório é aberto no Gerenciador de relatórios.  

4.  Clique o **propriedades** guia. Você pode modificar o nome do relatório e a descrição.  

5.  Quando tiver terminado, clique em **aplicar**. As propriedades do relatório são salvos no servidor de relatório e o console do Configuration Manager recupera as propriedades do relatório atualizado para o relatório.  

###  <a name="BKMK_EditReport"></a>Editar um relatório do Configuration Manager  
 Quando um relatório existente do Configuration Manager não recuperar as informações que você precisa ter ou não fornece o layout ou o design desejado, você pode editar o relatório no construtor de relatórios.  

> [!NOTE]  
>  Você também pode optar por clonar um relatório existente ao abri-lo para edição ou clicar em **Salvar como** salvá-lo como um novo relatório.  

> [!IMPORTANT]  
>  A conta de usuário deve ter **modificar do Site** permissão e **modificar relatório** permissões em objetos específicos associados com o relatório que você deseja modificar.  

> [!IMPORTANT]  
>  Quando o Configuration Manager é atualizado para uma versão mais recente, substituídos por novos relatórios os relatórios predefinidos. Se você modificar um relatório predefinido, você deve fazer backup do relatório antes de instalar a nova versão e, em seguida, restaure o relatório no Reporting Services. Se você estiver fazendo alterações significativas em um relatório predefinido, considere criar um novo relatório em vez disso. Novos relatórios criados antes de atualizar um site não serão substituídos.  

 Use o procedimento a seguir para editar as propriedades de um relatório do Configuration Manager.  

#### <a name="to-edit-report-properties"></a>Para editar as propriedades de relatório  

1.  No console do Configuration Manager, clique em **monitoramento**.  

2.  No **monitoramento** espaço de trabalho, expanda **relatórios**e, em seguida, clique em **relatórios** para listar os relatórios disponíveis.  

3.  Selecione o relatório que você deseja modificar, e, em seguida, no **início** guia o **grupo relatório** seção, clique em **editar**. Insira sua conta de usuário e senha, se você for solicitado e, em seguida, clique em **Okey**. Se o construtor de relatórios não estiver instalado no computador, você precisará instalá-lo. Clique em **executar** para instalar o construtor de relatórios, que é necessário para modificar e criar relatórios.  

4.  No construtor de relatórios, modifique as configurações apropriadas do relatório e, em seguida, clique em **salvar** para salvar o relatório para o servidor de relatório.  

###  <a name="BKMK_CreateModelBasedReport"></a>Criar um modelo de\-com base em relatórios  
 Um modelo de\-com base permite que o relatório você interativamente seleciona os itens que você deseja incluir em seu relatório. Para obter mais informações sobre como criar modelos de relatório personalizado, consulte [criando modelos de relatório personalizado para o System Center Configuration Manager no SQL Server Reporting Services](creating-custom-report-models-in-sql-server-reporting-services.md).  

> [!IMPORTANT]  
>  A conta de usuário deve ter **modificar do Site** permissão para criar um novo relatório. O usuário só pode criar um relatório em pastas para os quais o usuário tem **modificar relatório** permissões.  

 Use o procedimento a seguir para criar um modelo de\-com base em relatórios do Configuration Manager.  

#### <a name="to-create-a-model-based-report"></a>Para criar um modelo\-com base em relatórios  

1.  No console do Configuration Manager, clique em **monitoramento**.  

2.  No **monitoramento** espaço de trabalho, expanda **relatórios** e clique em **relatórios**.  

3.  No **início** guia o **criar** seção, clique em **criar relatório** para abrir o **Assistente para criar relatório**.  

4.  Sobre o **informações** página, defina as seguintes configurações:  

    -   **Tipo**: Selecione **modelo\-relatório baseado em** para criar um relatório no construtor de relatórios usando um modelo do Reporting Services.  

    -   **Nome**: Especifique um nome para o relatório.  

    -   **Descrição**: Especifique uma descrição para o relatório.  

    -   **Servidor**: Exibe o nome do servidor de relatório no qual você está criando o relatório.  

    -   **Caminho**: Clique em **procurar** para especificar uma pasta na qual você deseja armazenar o relatório.  

     Clique em **Seguinte**.  

5.  Sobre o **seleção de modelo** , selecione um modelo disponível na lista que você pode usar para criar o relatório. Quando você seleciona o modelo de relatório, o **visualização** seção exibe os modos de exibição do SQL Server e entidades que estão disponíveis pelo modelo de relatório selecionado.  

6.  Na página **Resumo** , reveja as definições. Clique em **anterior** para alterar as configurações ou clique em **próximo** para criar o relatório no Configuration Manager.  

7.  Sobre o **confirmação** , clique em **fechar** para sair do assistente e, em seguida, abra o construtor de relatórios para definir as configurações de relatório. Insira sua conta de usuário e senha, se você for solicitado e, em seguida, clique em **Okey**. Se o construtor de relatórios não estiver instalado no computador, você precisará instalá-lo. Clique em **executar** para instalar o construtor de relatórios, que é necessário para modificar e criar relatórios.  

8.  No construtor de relatórios da Microsoft, crie o layout do relatório, selecione dados nos modos de exibição disponíveis do SQL Server, adicionar parâmetros ao relatório e assim por diante. Para obter mais informações sobre como usar o construtor de relatórios para criar um novo relatório, consulte a Ajuda do construtor de relatórios.  

9. Clique em **executar** para executar o relatório. Verifique se o relatório contém as informações que você espera. Clique em **Design** para retornar para a exibição de Design para modificar o relatório, se necessário.  

10. Clique em **salvar** para salvar o relatório para o servidor de relatório. Você pode executar e modificar o novo relatório no **relatórios** nó o **monitoramento** espaço de trabalho.  

###  <a name="BKMK_CreateSQLBasedReport"></a>Criar um SQL\-com base em relatórios  
 Um SQL\-com base permite que o relatório recuperar dados com base em um instrução SQL do relatório.  

> [!IMPORTANT]  
>  Quando você cria uma instrução SQL para um relatório personalizado, não faça referência diretamente tabelas do SQL Server. Em vez disso, a referência de visualizações de relatórios do SQL Server \(exibir nomes que comecem com v\_ \) do banco de dados do site. Você também pode fazer referência a procedimentos armazenados públicos \(os nomes de procedimento que iniciam com sp armazenado\_ \) do banco de dados do site.  

> [!IMPORTANT]  
>  A conta de usuário deve ter **modificar do Site** permissão para criar um novo relatório. O usuário só pode criar um relatório em pastas para os quais o usuário tem **modificar relatório** permissões.  

 Use o procedimento a seguir para criar um SQL\-com base em relatórios do Configuration Manager.  

#### <a name="to-create-a-sql-based-report"></a>Para criar um SQL\-com base em relatórios  

1.  No console do Configuration Manager, clique em **monitoramento**.  

2.  Na área de trabalho **Monitorização** , expanda **Comunicar**e clique em **Relatórios**.  

3.  No **início** guia o **criar** seção, clique em **criar relatório** para abrir o **Assistente para criar relatório**.  

4.  Sobre o **informações** página, defina as seguintes configurações:  

    -   **Tipo**: Selecione **SQL\-relatório baseado em** para criar um relatório no construtor de relatórios usando uma instrução SQL.  

    -   **Nome**: Especifique um nome para o relatório.  

    -   **Descrição**: Especifique uma descrição para o relatório.  

    -   **Servidor**: Exibe o nome do servidor de relatório no qual você está criando o relatório.  

    -   **Caminho**: Clique em **procurar** para especificar uma pasta na qual você deseja armazenar o relatório.  

     Clique em **Seguinte**.  

5.  Na página **Resumo** , reveja as definições. Clique em **anterior** para alterar as configurações ou clique em **próximo** para criar o relatório no Configuration Manager.  

6.  Sobre o **confirmação** , clique em **fechar** para sair do assistente e abrir o construtor de relatórios para definir as configurações de relatório. Insira sua conta de usuário e senha, se você for solicitado e, em seguida, clique em **Okey**. Se o construtor de relatórios não estiver instalado no computador, você precisará instalá-lo. Clique em **executar** para instalar o construtor de relatórios, que é necessário para modificar e criar relatórios.  

7.  No construtor de relatórios, forneça a instrução SQL para o relatório ou crie a instrução SQL usando colunas nas exibições disponíveis do SQL Server, adicionar parâmetros ao relatório e assim por diante.  

8.  Clique em **executar** para executar o relatório. Verifique se o relatório contém as informações que você espera. Clique em **Design** para retornar para a exibição de Design para modificar o relatório, se necessário.  

9. Clique em **salvar** para salvar o relatório para o servidor de relatório. Você pode executar o novo relatório **relatórios** nó o **monitoramento** espaço de trabalho.  

##  <a name="BKMK_ManageReportSubscriptions"></a>Gerenciar assinaturas de relatório  
 Assinaturas de relatório no SQL Server Reporting Services permitem configurar a entrega automática de relatórios especificados por email ou para um compartilhamento de arquivos em intervalos agendados. Use o **Assistente para criar assinatura** no System Center 2012 Configuration Manager para configurar assinaturas de relatório.  

###  <a name="BKMK_ReportSubscriptionFileShare"></a>Criar uma assinatura de relatório para entregar um relatório em um compartilhamento de arquivos  
 Quando você cria uma assinatura de relatório para entregar um relatório para um compartilhamento de arquivos, o relatório é copiado no formato especificado para o compartilhamento de arquivo que você especificar. Você pode assinar e solicitar entrega de apenas um relatório por vez.  

 Diferentemente dos relatórios hospedados e gerenciados por um servidor de relatório, relatórios que são entregues em uma pasta compartilhada são arquivos estáticos. Recursos interativos definidos para o relatório não funcionam para relatórios que são armazenados como arquivos no sistema de arquivos. Recursos de interação são representados como elementos estáticos. Se o relatório incluir gráficos, a apresentação padrão será usada. Se o relatório estiver vinculado a outro relatório, o link é processado como texto estático. Se você quiser reter recursos interativos em um relatório entregue, use a entrega de email. Para obter mais informações sobre a entrega de email, consulte o [criar uma assinatura de relatório para entregar um relatório por email](#BKMK_ReportSubscriptionEmail) seção mais adiante neste tópico.  

 Quando você cria uma assinatura que usa a entrega de compartilhamento de arquivos, você deve especificar uma pasta existente como a pasta de destino. O servidor de relatório não cria pastas no sistema de arquivos. A pasta que você especificar deve ser acessível por uma conexão de rede. Quando você especificar a pasta de destino em uma assinatura, use um caminho UNC e não inclua barras invertidas no caminho da pasta. Por exemplo, um caminho UNC válido para a pasta de destino é: \\ \\ &lt;servername\>\\reportfiles\\operações\\2011.  

 Os relatórios podem ser renderizados em uma variedade de formatos de arquivo, como MHTML ou Excel. Para salvar o relatório em um formato de arquivo específico, selecione o formato de renderização ao criar sua assinatura. Por exemplo, escolher o Excel salva o relatório como um arquivo do Microsoft Excel. Embora você possa selecionar qualquer formato de renderização com suporte, alguns formatos funcionam melhor do que outros na renderização de um arquivo.  

 Use o procedimento a seguir para criar uma assinatura de relatório para entregar um relatório em um compartilhamento de arquivos.  

#### <a name="to-create-a-report-subscription-to-deliver-a-report-to-a-file-share"></a>Para criar uma assinatura de relatório para entregar um relatório para um compartilhamento de arquivos  

1.  No console do Configuration Manager, clique em **monitoramento**.  

2.  No **monitoramento** espaço de trabalho, expanda **relatórios** e clique em **relatórios** para listar os relatórios disponíveis. Você pode selecionar uma pasta de relatório para listar somente os relatórios que estão associados com a pasta.  

3.  Selecione o relatório que você deseja adicionar à assinatura, e, em seguida, no **início** guia o **grupo relatório** seção, clique em **Criar assinatura** para abrir o **Assistente para criar assinatura**.  

4.  Sobre o **entrega da assinatura** página, defina as seguintes configurações:  

    -   Relatório entregue por: Selecione **compartilhamento de arquivos do Windows** para entregar o relatório para um compartilhamento de arquivos.  

    -   **Nome do arquivo**: Especifique o nome de arquivo para o relatório. Por padrão, o arquivo de relatório não inclui uma extensão de nome de arquivo. Selecione **Adicionar extensão de arquivo quando criada** para adicionar automaticamente uma extensão de nome de arquivo para esse relatório com base no formato de renderização.  

    -   **Caminho**: Especifique um caminho UNC para uma pasta existente onde você deseja enviar esse relatório \(por exemplo, \\ \\ &lt;nome do servidor\>\\&lt;compartilhamento de servidor\>\\&lt;pasta relatório\>\).  

        > [!NOTE]  
        >  O nome de usuário especificado posteriormente nesta página deve ter acesso a esse compartilhamento de servidor e ter permissões de gravação na pasta de destino.  

    -   **Renderizar formato**: Selecione um dos seguintes formatos de arquivo de relatório:  

        -   **Arquivo XML com dados de relatório**: Salva o relatório no formato de linguagem de marcação.  

        -   **CSV \(delimitada por vírgula\)**: Salva o relatório no vírgula\-separados\-formato de valor.  

        -   **Arquivo TIFF**: Salva o relatório no formato TIFF.  

        -   **Acrobat \(PDF\) arquivo**: Salva o relatório no formato PDF do Acrobat.  

        -   **O HTML 4.0**: Salva o relatório como uma página da Web visível apenas em navegadores que oferecem suporte a HTML 4.0. O Internet Explorer 5 e versões posteriores oferecem suporte a HTML 4.0.  

            > [!NOTE]  
            >  Se houver imagens em seu relatório, no formato HTML 4.0 não irá incluí-las no arquivo.  

        -   **MHTML \(arquivo da web\)**: Salva o relatório no formato MIME HTML \(mhtml\), que é visível em muitos navegadores da web.  

        -   **Processador RPL**: Salva o relatório no Layout de página de relatório \(RPL\) formato.  

        -   **Excel**: Salva o relatório como uma planilha do Microsoft Excel.  

        -   **Word**: Salva o relatório como um documento do Word.  

    -   **Nome de usuário**: Especifique uma conta de usuário do Windows com permissões para acessar o compartilhamento do servidor de destino e a pasta. A conta de usuário deve ter acesso a esse compartilhamento de servidor e ter permissão de gravação na pasta de destino.  

    -   **Senha**: Especifique a senha da conta de usuário do Windows. Em **Confirmar senha**, re\-digite a senha.  

    -   Selecione uma das opções a seguir para configurar o comportamento quando um arquivo de mesmo nome existe na pasta de destino:  

        -   **Substituir um arquivo existente com uma versão mais recente**: Especifica que quando o arquivo de relatório já existe, a nova versão o substitui.  

        -   **Não substituir um arquivo existente**: Especifica que, quando o arquivo de relatório já existe, não há nenhuma ação.  

        -   **Incrementar nomes de arquivos quando versões mais recentes são adicionadas**: Especifica que, quando o arquivo de relatório já existe, um número é adicionado ao novo relatório para o nome do arquivo para diferenciá-la de outras versões.  

    -   **Descrição**: Especifica a descrição para a assinatura de relatório.  

     Clique em **Seguinte**.  

5.  Sobre o **agendamento da assinatura** página, selecione uma das seguintes opções de agendamento de entrega para a assinatura de relatório:  

    -   **Usar agendamento compartilhado**: Uma agenda compartilhada é um agendamento previamente definido que pode ser usado por outras assinaturas de relatório. Marque esta caixa de seleção e, em seguida, selecione uma agenda compartilhada na lista se algum tiver sido especificado.  

    -   **Criar novo agendamento**: Configure o agendamento no qual este relatório é executado, incluindo o intervalo, hora de início e data e a data de término para essa assinatura.  

6.  Sobre o **parâmetros de assinatura** , especifique os parâmetros para este relatório que são usados quando ele é executado de forma autônomo. Quando não existem parâmetros para o relatório, essa página não é exibida.  

7.  Sobre o **resumo** , examine as configurações de assinatura de relatório. Clique em **anterior** para alterar as configurações ou clique em **próximo** para criar a assinatura de relatório.  

8.  Na página **Conclusão** , clique em **Fechar** para sair do assistente. Verifique se a assinatura do relatório foi criada com êxito. Você pode exibir e modificar as assinaturas de relatório no **assinaturas** nó **relatórios** no **monitoramento** espaço de trabalho.  

###  <a name="BKMK_ReportSubscriptionEmail"></a>Criar uma assinatura de relatório para entregar um relatório por email  
 Quando você cria uma assinatura de relatório para entregar um relatório por email, um email é enviado aos destinatários que você configurar, e o relatório é incluído como um anexo. O servidor de relatório não valida endereços de email ou obter endereços de email de um servidor de email. Você deve saber com antecedência quais endereços que deseja usar. Por padrão, você pode enviar por email relatórios a qualquer conta de email válida dentro ou fora de sua organização. Você pode selecionar uma ou ambas das seguintes opções de entrega de email:  

-   Envie uma notificação e um hiperlink para o relatório gerado.  

-   Envie um relatório anexado ou inserido. O formato de renderização e o navegador determinam se o relatório é inserido ou anexado. Se seu navegador dá suporte a HTML 4.0 e MHTML, e selecione o MHTML \(arquivo da web\) formato de renderização, o relatório será inserido como parte da mensagem. Todos os outros formatos de renderização \(CSV, PDF, Word, e assim por diante\) entregar relatórios como anexos. O Reporting Services não verifica o tamanho do anexo ou mensagem antes de enviar o relatório. Se o anexo ou a mensagem exceder o limite máximo permitido pelo servidor de email, o relatório não será entregue.  

> [!IMPORTANT]  
>  Você deve configurar as configurações de email no Reporting Services para o **Email** opção de entrega para estar disponível. Para obter mais informações sobre como configurar as configurações de email no Reporting Services, consulte [Configurando um servidor de relatório para entrega de Email](http://go.microsoft.com/fwlink/p/?LinkId=226668) no SQL Server Books Online.  

 Use o procedimento a seguir para criar uma assinatura de relatório para entregar um relatório por email.  

#### <a name="to-create-a-report-subscription-to-deliver-a-report-by-email"></a>Para criar uma assinatura de relatório para entregar um relatório por email  

-   No console do Configuration Manager, clique em **monitoramento**.  

-   No **monitoramento** espaço de trabalho, expanda **relatórios** e clique em **relatórios** para listar os relatórios disponíveis. Você pode selecionar uma pasta de relatório para listar somente os relatórios que estão associados com a pasta.  

-   Selecione o relatório que você deseja adicionar à assinatura, e, em seguida, no **início** guia o **grupo relatório** seção, clique em **Criar assinatura** para abrir o **Assistente para criar assinatura**.  

-   Sobre o **entrega da assinatura** página, defina as seguintes configurações:  

    -   **Relatório entregue por**: Selecione **E\-mail** para entregar o relatório como um anexo em uma mensagem de email.  

    -   **To**: Especifique um endereço de email válido para enviar esse relatório.  

        > [!NOTE]  
        >  Você pode inserir vários destinatários de email, separando cada endereço de email com um ponto e vírgula.  

    -   **Cc**: Opcionalmente, especifique um endereço de email para copiar esse relatório.  

    -   **Bcc**: Opcionalmente, especifique um endereço de email para enviar uma cópia oculta desse relatório.  

    -   **Responder a**: Especifique o endereço de resposta a ser usado se o destinatário responder à mensagem de email.  

    -   **Entidade**: Especifique uma linha de assunto da mensagem de email de assinatura.  

    -   **Prioridade**: Selecione o sinalizador de prioridade para essa mensagem de email. Select **Low**, **Normal**, or **High**. A configuração de prioridade é usada pelo Microsoft Exchange para definir um sinalizador que indica a importância da mensagem de email.  

    -   **Comentário**: Especifique o texto a ser adicionado ao corpo da mensagem de email de assinatura.  

    -   **Descrição**: Especifique a descrição para essa assinatura de relatório.  

    -   **Incluir Link**: Inclui uma URL ao relatório inscrito no corpo da mensagem de email.  

    -   **Incluir relatório**: Especifique que o relatório é anexado à e\-mensagem de email. O formato no qual o relatório será anexado é especificado no **formato de renderização** lista.  

    -   **Renderizar formato**: Selecione um dos seguintes formatos para o relatório anexado:  

        -   **Arquivo XML com dados de relatório**: Salva o relatório no formato de linguagem de marcação.  

        -   **CSV \(delimitada por vírgula\)**: Salva o relatório no vírgula\-separados\-formato de valor.  

        -   **Arquivo TIFF**: Salva o relatório no formato TIFF.  

        -   **Acrobat \(PDF\) arquivo**: Salva o relatório no formato PDF do Acrobat.  

        -   **MHTML \(arquivo da web\)**: Salva o relatório no formato MIME HTML \(mhtml\), que é visível em muitos navegadores da web.  

        -   **Excel**: Salva o relatório como uma planilha do Microsoft Excel.  

        -   **Word**: Salva o relatório como um documento do Word.  

-   Sobre o **agendamento da assinatura** página, selecione uma das seguintes opções de agendamento de entrega para a assinatura de relatório:  

    -   **Usar agendamento compartilhado**: Uma agenda compartilhada é um agendamento previamente definido que pode ser usado por outras assinaturas de relatório. Marque esta caixa de seleção e, em seguida, selecione uma agenda compartilhada na lista se algum tiver sido especificado.  

    -   **Criar novo agendamento**: Configure o agendamento no qual este relatório será executado, incluindo o intervalo, a hora de início e a data e a data de término para essa assinatura.  

-   Sobre o **parâmetros de assinatura** , especifique os parâmetros para este relatório que são usados quando ele é executado de forma autônomo. Quando não existem parâmetros para o relatório, essa página não é exibida.  

-   Sobre o **resumo** , examine as configurações de assinatura de relatório. Clique em **anterior** para alterar as configurações ou clique em **próximo** para criar a assinatura de relatório.  

-   Na página **Conclusão** , clique em **Fechar** para sair do assistente. Verifique se a assinatura do relatório foi criada com êxito. Você pode exibir e modificar as assinaturas de relatório no **assinaturas** nó **relatórios** no **monitoramento** espaço de trabalho.  

