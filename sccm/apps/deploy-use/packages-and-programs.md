---
title: Pacotes e programas | Documentos do Microsoft
description: "Suporta implementações que utilizem pacotes e programas ou aplicações com o System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: caad0507-9913-415a-b13d-d36f8f0a1b80
caps.latest.revision: 8
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 6c5b23270501c11ed5aba9a6045734c73095d1bf
ms.openlocfilehash: 6146bcf4e5aa9df6fe0b8cf71898e488ecf217cc
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="packages-and-programs-in-system-center-configuration-manager"></a>Pacotes e programas no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager continua a suportar pacotes e programas que foram utilizados no Configuration Manager 2007. Uma implementação que utiliza pacotes e programas pode ser mais adequada do que uma implementação que utiliza uma aplicação quando implementa qualquer um dos seguintes procedimentos:  

- Aplicações em servidores Linux e UNIX
- Scripts que não instalam uma aplicação num computador, tal como um script para desfragmentar a unidade de disco do computador
- Scripts "pontuais" que não têm de ser monitorizados continuamente  
- Scripts que são executados num agendamento periódico e não podem utilizar a avaliação global

Ao migrar pacotes a partir de uma versão anterior do Configuration Manager, pode implementá-los na sua hierarquia do Configuration Manager. Quando a migração é concluída, os pacotes são apresentados no nó **Pacotes** na área de trabalho**Biblioteca de Software**.

Pode modificar e implementar estes pacotes da mesma forma que efetuou através da utilização de distribuição de software. O **importar pacote no Assistente de definição** permanece no Configuration Manager para importar pacotes de legado. Anúncios são convertidas em implementações quando são migrados a partir do Configuration Manager 2007 para uma hierarquia do Configuration Manager.  

> [!NOTE]  
>  Pode utilizar o Microsoft System Center Configuration Manager Package Conversion Manager para converter pacotes e programas em aplicações do Configuration Manager.  
>   
>  Para obter mais informações, veja [Gestor de Conversão de Pacotes do Configuration Manager](https://technet.microsoft.com/library/hh531519.aspx).  

Pacotes podem utilizar algumas novas funcionalidades do Configuration Manager, incluindo os grupos de pontos de distribuição e a monitorização. Aplicações do Microsoft Application Virtualization (App-V) não podem ser distribuídas através da utilização de pacotes e programas no Configuration Manager. Para distribuir aplicações virtuais, tem de criá-los como aplicações do Configuration Manager.  

##  <a name="create-a-package-and-program"></a>Criar um pacote e programa  
 Utilize um dos seguintes procedimentos para ajudar a criar ou importar pacotes e programas.  

### <a name="create-a-package-and-program-using-the-create-package-and-program-wizard"></a>Criar um pacote e um programa utilizando o Assistente para Criar Pacote e Programa  

1.  Na consola do Configuration Manager, escolha **biblioteca de Software** > **gestão de aplicações** > **pacotes**.  

3.  No **base** separador o **criar** grupo, selecione **criar pacote**.  

4.  No **pacote** página do **assistente criar pacote e programa**, especifique as seguintes informações:  

    -   **Nome**: Especifique um nome para o pacote com um máximo de 50 carateres.  

    -   **Descrição**: Especifique uma descrição para este pacote com um máximo de 128 carateres.  

    -   **Fabricante** (opcional): Especifique um nome de fabricante para o ajudar a identificar o pacote na consola do Configuration Manager. Este nome pode ter um máximo de 32 carateres.

    -   **Idioma** (opcional): Especifique a versão de idioma do pacote com um máximo de 32 carateres.  

    -   **Versão** (opcional):  Especifique um número de versão para o pacote com um máximo de 32 carateres.

    -   **Este pacote contém ficheiros de origem**: Esta definição indica se o pacote necessita que os ficheiros de origem esteja presente nos dispositivos cliente. Por predefinição, esta caixa de verificação estiver desmarcada e do Configuration Manager não utilizar pontos de distribuição para o pacote. Quando esta caixa de verificação está selecionada, são utilizados pontos de distribuição.  

    -   **Pasta de origem**: Se o pacote contém ficheiros de origem, escolher **procurar** para abrir o **definir a pasta de origem** diálogo caixa e, em seguida, especifique a localização dos ficheiros de origem para o pacote.  

        > [!NOTE]  
        >  A conta de computador do servidor do site deve ter permissões de acesso de leitura para a pasta de origem que especificar.  

5.  No **tipo de programa** página do **assistente criar pacote e programa**, selecione o tipo de programa para criar e, em seguida, escolha **seguinte**. Pode criar um programa para um computador ou dispositivo, ou pode ignorar este passo e criar um programa mais tarde.  

    > [!TIP]  
    >  Para criar um novo programa para um pacote existente, selecione primeiro o pacote. Em seguida, no **base** no separador de **pacote** grupo, selecione **criar programa** para abrir o **Assistente de criação de programa**.  

6.  Utilize um dos seguintes procedimentos para criar um programa padrão ou um programa de dispositivo.  

    #### <a name="create-a-standard-program"></a>Criar um programa padrão  

  1.  No **tipo de programa** página do **assistente criar pacote e programa**, escolha **programa padrão**e, em seguida, escolha **seguinte**.     

    2.  No **programa padrão** página, especifique as seguintes informações:  

        -   **Nome:** Especifique um nome para o programa com um máximo de 50 carateres.  

            > [!NOTE]  
            >  O nome do programa deve ser exclusivo num pacote. Depois de criar um programa, não é possível modificar o respetivo nome.  

        -   **Linha de comandos**: Introduza a linha de comandos a utilizar para iniciar este programa, ou escolha **procurar** para navegar para a localização do ficheiro.  

            Se um nome de ficheiro não tiver uma extensão especificada, o Configuration Manager tenta utilizar. com, .exe e. bat como extensões possíveis.  

             Quando o programa é executado num cliente, o Configuration Manager procura pela primeira vez o nome do ficheiro da linha de comandos no pacote, pesquisas junto numa pasta local do Windows e, em seguida, procura locais *% caminho %*. Se o ficheiro não for encontrado, o programa irá falhar.  

        -   **Pasta de arranque** (opcional): Especifique a pasta a partir do qual o programa é executado, até 127 carateres. Esta pasta pode ser um caminho absoluto no cliente ou um caminho relativo para a pasta de ponto de distribuição que contém o pacote.

        -   **Executar**: Especifique o modo no qual o programa é executado em computadores cliente. Selecione um dos seguintes procedimentos:  

            -   **Normal**: O programa é executado no modo normal com base nas predefinições do sistema e do programa. Este é o modo predefinido.  

            -   **Minimizado**: O programa é executado minimizado nos dispositivos cliente. Os utilizadores poderão ver a atividade de instalação na área de notificação ou na barra de tarefas.  

            -   **Maximizado**: O programa é executado maximizado em dispositivos cliente. Os utilizadores veem todas as atividades de instalação.  

            -   **Oculta**: O programa é executado ocultado nos dispositivos cliente. Os utilizadores não veem qualquer atividade de instalação.  

        -   **Programa pode ser executado**: Especifique se o programa é executado apenas quando um utilizador tem sessão iniciado, só quando nenhum utilizador está inscrita no, ou, independentemente de um utilizador tiver sessão iniciado no computador cliente.  

        -   **Modo de execução**: Especifique se o programa é executado com permissões administrativas ou com as permissões do utilizador que tem atualmente sessão iniciada.  

        -   **Permitir que os utilizadores visualizem e interajam com a instalação do programa**: Utilize esta definição, se estiver disponível, para especificar se pretende permitir que os utilizadores interajam com a instalação do programa. Esta caixa de verificação só estará disponível se **só quando nenhum utilizador tiver sessão iniciado** ou **se deve ou não um utilizador tiver sessão iniciado** está selecionada para **programa pode ser executado** e quando **executar com direitos administrativos** está selecionada para **modo de execução**.  

        -   **Modo de unidade**: Especifica informações sobre como executar este programa na rede. Escolha uma das seguintes opções:  

            -   **Executa com nome UNC**: Especifique que o programa é executado com um nome de convenção de Nomenclatura Universal (UNC). Esta é a predefinição.  

            -   **Requer letra de unidade**: Especifique que o programa requer uma letra de unidade para qualificar completamente a respetiva localização. Para esta definição, o Configuration Manager pode utilizar qualquer letra de unidade disponível no cliente.  

            -   **Requer letra de unidade específica** : Especifique que o programa requer uma letra de unidade específica que especificou para qualificar completamente a respetiva localização (por exemplo, **z:)**). Se a letra de unidade especificada já estiver a ser utilizada num cliente, o programa não é executado.  

        -   **Restabelecer a ligação ao ponto de distribuição no registo em**: Utilize esta caixa de verificação para indicar se o computador cliente volta a ligar ao ponto de distribuição quando o utilizador inicia sessão. Por predefinição, esta caixa de verificação está desmarcada.  

  3.  No **requisitos** página do **criar pacote e programa assistente,** especifique as seguintes informações:  

        -   **Executar outro programa primeiro**: Utilize esta definição para identificar um pacote e programa que é executado antes deste pacote e programa está a ser executado.  

        -   **Requisitos de plataforma**: Selecione **pode executar este programa em qualquer plataforma** ou **este programa pode ser executado apenas nas plataformas especificadas**e, em seguida, selecione os sistemas operativos que os clientes devem ser executadas para ser possível instalar o pacote e programa.  

        -   **Espaço em disco estimado**: Especifique a quantidade de espaço em disco que o programa de software necessita para ser executada no computador. Pode especificá-lo como **Desconhecido** (a predefinição) ou como um número inteiro igual ou superior a zero. Se for especificado um valor, é necessário especificar também as unidades para o valor.  

        -   **Máximo tempo de execução permitido (minutos)**: Especifique o tempo máximo que o programa poderá demorar a ser executado num computador cliente. Pode especificá-lo como **Desconhecido** (a predefinição) ou como um número inteiro superior a zero.  

             Por predefinição, este valor é definido para 120 minutos.  

            > [!IMPORTANT]  
            >  Se estiver a utilizar janelas de manutenção para a coleção onde este programa é executado, poderá ocorrer um conflito se o **tempo de execução máximo permitido** é maior do que a janela de manutenção agendada. No entanto, se o número máximo de tempo de execução estiver definido como **desconhecido**, o programa começa a ser executada durante a janela de manutenção e continua a ser executada conforme necessário depois de fechar a janela de manutenção. Se o utilizador define o tempo de execução máximo para um período específico que excede o comprimento de qualquer janela de manutenção disponível, em seguida, o programa não é executado.  

             Se o valor é definido como **desconhecido**, tempo de execução Configuration Manager conjuntos o máximo permitido como 12 horas (720 minutos).  

            > [!NOTE]  
            >  Se o tempo máximo de execução (definido pelo utilizador ou como o valor predefinido) for excedido, o Configuration Manager deixa o programa se **executar com direitos administrativos** está selecionada e **permitir que os utilizadores visualizem e interajam com a instalação do programa** não estiver selecionada.  

  4.  Escolher **seguinte**.  

    #### <a name="create-a-device-program"></a>Criar um programa de dispositivo  

  1.  No **tipo de programa** página do **assistente criar pacote e programa**, selecione **programa para dispositivo**e, em seguida, escolha **seguinte**.  

  2.  No **programa para dispositivo** página, especifique o seguinte:  

        -   **Nome**: Especifique um nome para o programa com um máximo de 50 carateres.  

            > [!NOTE]  
            >  O nome do programa deve ser exclusivo num pacote. Depois de criar um programa, não é possível modificar o respetivo nome.  

        -   **Comentário** (opcional): Especifique um comentário para este programa de dispositivo com um máximo de 127 carateres.  

        -   **Transferir pasta**: Especifique o nome da pasta no dispositivo Windows CE onde serão armazenados os ficheiros de origem do pacote. O valor predefinido é **\Temp\\**.  

        -   **Linha de comandos**: Introduza a linha de comandos a utilizar para iniciar este programa, ou escolha **procurar** para navegar para a localização do ficheiro.  

        -   **Executar linha de comandos na pasta de transferência**: Selecione esta opção para executar o programa a partir da pasta de transferência especificado anteriormente.  

        -   **Executar linha de comandos a partir desta pasta**: Selecione esta opção para especificar uma pasta diferente a partir do qual executar o programa.  

    3.  No **requisitos** página, especifique o seguinte:  

        -   **Espaço em disco estimado**: Especifique a quantidade de espaço em disco necessário para o software. Esta informação é apresentada aos utilizadores de dispositivos móveis antes de instalarem o programa.  

        -   **Transferir o programa**: Especifique informações sobre quando este programa pode ser transferido para dispositivos móveis. Pode especificar **Assim que possível**, **Apenas sobre uma rede rápida** ou **Apenas quando o dispositivo estiver ancorado**.  

        -   **Requisitos adicionais**: Especifique quaisquer requisitos suplementares para este programa. Estes são apresentados aos utilizadores antes de instalarem o software. Por exemplo, pode indicar os utilizadores que necessitam de fechar todas as outras aplicações antes de executar o programa.  

  4.  Escolher **seguinte**.  

  7.  No **resumo** página, reveja as ações que serão efetuadas e, em seguida, conclua o assistente.  

 Certifique-se de que o novo pacote e programa são apresentados no **pacotes** nó do **biblioteca de Software** área de trabalho.  

## <a name="create-a-package-and-program-from-a-package-definition-file"></a>Criar um pacote e um programa a partir de um ficheiro de definição de pacote  

1.  Na consola do Configuration Manager, escolha **biblioteca de Software** > **gestão de aplicações** > **pacotes**.  

3.  No **base** separador o **criar** grupo, selecione **criar pacote a partir da definição**.  

4.  No **definição de pacote** página do **criar pacote a partir do Assistente de definição**, escolha um ficheiro de definição de pacote existente, ou escolha **procurar** para abrir um novo ficheiro de definição de pacote. Depois de especificar um novo ficheiro de definição de pacote, selecione-o partir de **definição do pacote** lista e, em seguida, selecione **seguinte**.  

5.  No **ficheiros de origem** página, especifique informações sobre ficheiros de origem necessários para o pacote e programa e, em seguida, selecione **seguinte**.  

6.  Se o pacote requer ficheiros de origem no **pasta de origem** página, especifique a localização a partir da qual os ficheiros de origem estão a ser obtidos e, em seguida, escolha **seguinte**.  

7.  No **resumo** página, reveja as ações que serão efetuadas e, em seguida, conclua o assistente. O novo pacote e programa são apresentados no **pacotes** nó do **biblioteca de Software** área de trabalho.  

 Para mais informações sobre ficheiros de definição de pacote, consulte o artigo [sobre o formato de ficheiro de definição de pacote](/sccm/apps/deploy-use/packages-and-programs#about-the-package-definition-file-format) neste tópico.  

##  <a name="deploy-packages-and-programs"></a>Implementar pacotes e programas  

1.  Na consola do Configuration Manager, escolha **biblioteca de Software** > **gestão de aplicações** > **pacotes**.  

2.  Selecione o pacote que pretende implementar, e, em seguida, no **base** separador o **implementação** grupo, selecione **implementar**.  

3.  No **geral** página do **Assistente de implementação de Software**, especifique o nome do pacote e programa que pretende implementar, a coleção à qual pretende implementar o pacote e programa e comentários opcionais para a implementação.  

     Selecione **Utilizar grupos de pontos de distribuição predefinidos associados a esta coleção** se quiser armazenar o conteúdo do pacote no grupo de pontos de distribuição predefinido da coleção. Se não foi possível associar a coleção selecionada a um grupo de pontos de distribuição, esta opção está disponível.  

4.  No **conteúdo** página, selecione **adicionar**e, em seguida, selecione os pontos de distribuição ou grupos de pontos de distribuição ao qual pretende implementar o conteúdo que está associado este pacote e programa.  

5.  No **definições de implementação** página, selecione um objetivo para esta implementação e especifique as opções para dos pacotes de reativação e ligações com tráfego limitado:  

    -   **Objetivo**: Escolha entre:  

        -   **Disponível**: Se a aplicação for implementada para um utilizador, o utilizador vê o pacote publicado e o programa no catálogo de aplicações e poderá solicitá-la a pedido. Se o pacote e programa for implementado num dispositivo, o utilizador vê-lo no Centro de Software e pode instalá-la a pedido.  

        -   **Obrigatório**: O pacote e programa é implementada automaticamente, de acordo com a agenda configurada. No entanto, um utilizador poderá controlar o estado de implementação do pacote e programa e instalá-los antes do prazo, utilizando o Centro de Software.   

    -   **Enviar pacotes de reativação**: Se o objetivo da implementação estiver definido como **obrigatório** e esta opção estiver selecionada, é enviado um pacote de reativação aos computadores antes da instalação da implementação para reativar o computador da suspensão quando for atingido o prazo de instalação. Para poder utilizar esta opção, os computadores devem ser configurados para Wake On LAN.  

    -  **Permitir que os clientes numa ligação de Internet limitada transfiram conteúdo após o prazo de instalação, o que pode implicar custos adicionais**: Selecione esta opção se é obrigatório.  

    > [!NOTE]  
    >  A opção **Pré-implementar software no dispositivo primário do utilizador** não está disponível ao implementar um pacote e um programa.  

6.  No **agendamento** página, configure quando este pacote e programa serão implementadas ou disponibilizadas aos dispositivos cliente.  

     As opções nesta página variam consoante a ação de implementação esteja definida **disponível** ou **necessário**.  

7.  Se o objetivo da implementação estiver definido como **necessário**, configurar o comportamento de executar novamente o programa a partir de **comportamento da nova execução** menu pendente. Pode escolher uma das seguintes opções:  

    |Comportamento da nova execução|Mais informações|  
    |--------------------|----------------------|  
    |Nunca voltar a executar o programa implementado|O programa não possível executar de novo no cliente, mesmo que o programa falhado ou se forem alterados, os ficheiros de programa.|  
    |Executar sempre novamente o programa|O programa será sempre novamente executado no cliente quando a implementação estiver agendada, mesmo que o programa foi executada já com êxito. Isto pode ser útil quando utilizar implementações periódicas no qual o programa é atualizado, por exemplo, com software antivírus.|  
    |Executar novamente se a tentativa anterior falhar|O programa será novamente executado quando a implementação estiver agendada apenas se a falha da tentativa de execução anterior.|  
    |Executar novamente se a tentativa anterior tiver êxito|O programa será novamente executado apenas se anteriormente foi executado com êxito no cliente. Isto é útil se utilizar anúncios periódicos nos quais o programa é atualizado regularmente, e em que cada atualização necessitar que a atualização anterior tenha sido instalada com êxito.|  

8. Na página **Experiência de Utilizador** , especifique as seguintes informações:  

    -   **Permitir que os utilizadores executem o programa independentemente das atribuições**: Se estiver ativada, os utilizadores podem instalar este software a partir do Centro de Software, independentemente de qualquer hora de instalação agendada.  

    -   **Instalação de software**: Permite que o software seja instalado fora das janelas de manutenção configurada.  

    -   **Reinício do sistema (se for necessário para concluir a instalação)**: Se a instalação de software exigir um reinício de dispositivo para concluir, permitir esta ação ocorrer fora de quaisquer janelas de manutenção configurada.  

    -   **Dispositivos Embedded**: Ao implementar pacotes e programas em dispositivos Windows Embedded que com filtro escrita ativado, pode especificar que pacotes e programas ser instalado em temporária sobreposição e confirmar as alterações mais tarde. Em alternativa, consolidar as alterações no prazo de instalação ou durante uma janela de manutenção. Ao consolidar alterações no prazo de instalação ou durante uma janela de manutenção, é necessário um reinício e as alterações sejam mantidas no dispositivo.  

        > [!NOTE]  
        >  Quando implementa um pacote ou programa num dispositivo Windows Embedded, certifique-se de que o dispositivo é membro de uma coleção que tenha uma janela de manutenção configurada. Para mais informações sobre como as janelas de manutenção são utilizadas quando implementar pacotes e programas em dispositivos Windows Embedded, consulte o artigo [aplicações criar Windows Embedded](../../apps/get-started/creating-windows-embedded-applications.md).  

9. Na página **Pontos de Distribuição** , especifique as seguintes informações:  

    -   **Opções de implementação**: Especifique as ações que um cliente deverá ser necessário para executar o conteúdo do programa. Pode especificar o comportamento quando o cliente está numa zona de rede rápida ou numa zona de rede lenta ou pouco fiável.  

    -   **Permitir que os clientes partilhem conteúdos com outros clientes na mesma sub-rede**: Selecione esta opção para reduzir a carga de rede ao permitir que os clientes transfiram conteúdos a partir de outros clientes na rede que já transferido e colocado em cache o conteúdo. Esta opção utiliza o Windows BranchCache e pode ser utilizada em computadores que executam o Windows Vista SP2 e posterior.  

    -   **Permitir que os clientes utilizem uma localização de origem de contingência para conteúdo**:  

        -  **Versões anteriores ao 1610**: Pode selecionar o **permitir a localização de origem de contingência para conteúdo de caixa de verificação** para permitir que os clientes fora destes limites grupos recorram à contingência e utilize a distribuição ponto como uma localização de origem de conteúdo quando não houver outros pontos de distribuição disponíveis.

        - **Versão 1610 e posterior**: Já não pode configurar **permitir a localização de origem de contingência para conteúdo**.  Em vez disso, pode configurar relações entre grupos de limites que determinam quando um cliente pode começar a procurar grupos de limites adicionais para uma localização de origem de conteúdo válida.

10. No **resumo** página, reveja as ações que serão efetuadas e, em seguida, conclua o assistente.  

     Pode ver a implementação no nó **Implementações** da área de trabalho **Monitorização** e no painel de detalhes no separador de implementação do pacote quando seleciona a implementação. Para obter mais informações, consulte o artigo [monitorizar pacotes e programas](/sccm/apps/deploy-use/packages-and-programs#monitor-packages-and-programs) neste tópico.  

> [!IMPORTANT]  
>  Se tiver configurado a opção **executar programa a partir do ponto de distribuição** no **pontos de distribuição** página do **Assistente de implementação de Software**, não desmarque a opção **copiar o conteúdo deste pacote para uma partilha de pacote em pontos de distribuição** porque isto faz com que o pacote disponível para execução a partir de pontos de distribuição.  

##  <a name="monitor-packages-and-programs"></a>Monitor de pacotes e programas  
 Para monitorizar implementações de pacote e programa, utilize os mesmos procedimentos que utilizar para monitorizar aplicações conforme especificado nas [monitorizar aplicações](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

 Pacotes e programas também inclui um número de relatórios incorporados que permitem monitorizar informações sobre o estado de implementação de pacotes e programas. Estes relatórios têm a categoria de relatório de **Distribuição de Software – Pacotes e Programas** e **Distribuição de Software - Estado de Implementação do Pacote e do Programa**.  

 Para obter mais informações sobre como configurar relatórios no Configuration Manager, consulte o artigo [Reporting no System Center Configuration Manager](../../core/servers/manage/reporting.md).  

##  <a name="manage-packages-and-programs"></a>Gerir pacotes e programas  
 No **biblioteca de Software** área de trabalho, expanda **gestão de aplicações**, escolha **pacotes**, selecione o pacote que pretende gerir e, em seguida, selecione uma tarefa de gestão da tabela seguinte:  

|Tarefa|Mais informações|  
|----------|----------------------|  
|**Criar Ficheiro de Conteúdo Pré-configurado**|Abre o **criar Assistente de ficheiro de conteúdo pré-configurado**, que lhe permite criar um ficheiro que contém o conteúdo do pacote que pode ser importado manualmente a outro site. Isto é útil em situações onde a largura de banda de rede seja fraca entre o servidor do site e o ponto de distribuição.|  
|**Criar programa**|Abre o **Assistente de criação de programa**, que lhe permite criar um novo programa para este pacote.|  
|**Exportarar**|Abre o **Assistente para Exportar pacote**, que lhe permite exportar o pacote selecionado e o respetivo conteúdo para um ficheiro.<br /><br /> Para obter informações sobre como importar pacotes e programas, consulte o artigo [criar pacotes e programas](/sccm/apps/deploy-use/packages-and-programs#create-packages-and-programs) neste tópico.|  
|**Implementar**|Abre o **Assistente de implementação de Software**, que lhe permite implementar o pacote selecionado e o programa numa coleção. Para obter mais informações, consulte o artigo [implementar pacotes e programas](/sccm/apps/deploy-use/packages-and-programs#deploy-packages-and-programs) neste tópico.|  
|**Distribuir Conteúdo**|Abre o **Assistente para distribuir conteúdo**, que lhe permite enviar o conteúdo que está associado ao pacote e programa para pontos de distribuição selecionados ou grupos de pontos de distribuição.|  
|**Atualizar Pontos de Distribuição**|Atualiza pontos de distribuição com o conteúdo mais recente para o pacote e o programa selecionados.|  

##  <a name="about-the-package-definition-file-format"></a>Sobre o formato de ficheiro de definição de pacote  
 Ficheiros de definição do pacote estão scripts que podem ser utilizados para ajudar a automatizar a criação do pacote e programa com o Configuration Manager. Fornecem todas as informações que necessita de criar um pacote e programa, excepto para a localização dos ficheiros de origem do pacote do Configuration Manager. Cada ficheiro de definição de pacote é um ficheiro de texto ASCII ou UTF-8 que utiliza o formato de ficheiro. ini e que contém as seguintes secções:  

###  <a name="pdf"></a>[PDF]  
 Esta secção identifica o ficheiro como um ficheiro de definição de pacote. Contém as seguintes informações:  

-   **Versão**: Especifique a versão do formato de ficheiro de definição de pacote que é utilizado pelo ficheiro. Isto corresponde à versão do System Management Server (SMS) ou o Configuration Manager para o qual foi escrito. Esta entrada é necessária.  

###  <a name="package-definition"></a>[Definição de Pacote]  
 Especifica as propriedades do pacote e programa. Fornece as seguintes informações:  

-   **Nome**: O nome do pacote, até 50 carateres.  

-   **Versão** (opcional): A versão do pacote, até 32 carateres.  

-   **Ícone** (opcional): O ficheiro que contém o ícone a utilizar para este pacote. Se for especificado, este ícone substitui o ícone de pacote de predefinição na consola do Configuration Manager.

-   **Publisher**: O publicador do pacote, até 32 carateres.

-   **Idioma**: A versão de idioma do pacote, até 32 carateres.

-   **Comentário** (opcional): Um comentário sobre o pacote, até 127 carateres.

-   **ContainsNoFiles**: Esta entrada indica se é ou não uma origem associada ao pacote.  

-   **Programas**: Os programas que estão definidos para este pacote. Cada nome do programa corresponde a uma secção **[Programa]** neste ficheiro de definição de pacote.  

     Exemplo:  

     `Programs=Typical, Custom, Uninstall`  

-   **MIFFileName**: O nome do ficheiro de formato MIF (Management Information) que contém o estado de pacote, até 50 carateres.  

-   **MIFName**: O nome do pacote (para correspondência MIF de), até 50 carateres.  

-   **MIFVersion**: O número de versão do pacote (para correspondência MIF de), até 32 carateres.  

-   **MIFPublisher**: O fabricante de software do pacote (para correspondência MIF de), até 32 carateres.  

###  <a name="program"></a>[Programa]  
 Para cada programa que está especificado no **programas** entrada no **[definição de pacote]** secção, o ficheiro de definição do pacote tem de incluir uma secção [programa] que define desse programa. Cada secção Programa fornece as seguintes informações:  

-   **Nome**: O nome do programa, até 50 carateres. Esta entrada deve ser exclusiva num pacote. Este nome é utilizado quando se definem anúncios. Em computadores cliente, o nome do programa é mostrado em **Executar Programas Anunciados**, no Painel de Controlo.  

-   **Ícone** (opcional): Especifique o ficheiro que contém o ícone a utilizar para este programa. Se for especificado, este ícone substitui o ícone de programa predefinido na consola do Configuration Manager e é apresentado nos computadores cliente quando o programa tenha sido anunciado.

-   **Comentário** (opcional): Um comentário sobre o programa, até 127 carateres.

-   **Uma linha de comando**: Especifique a linha de comandos do programa, até 127 carateres. O comando é relativo à pasta de origem do pacote.

-   **StartIn**: Especifique a pasta de trabalho para o programa, até 127 carateres. Esta entrada pode ser um caminho absoluto no computador cliente ou um caminho relativo para a pasta de origem do pacote.

-   **Executar**: Especifique o modo de programa no qual o programa é executado. Pode especificar **Minimizado**, **Maximizado** ou **Oculto**. Se esta entrada não é incluída, o programa é executado no modo normal.  

-   **AfterRunning**: Especifique qualquer acção especial que ocorre após o programa é concluído com êxito. As opções disponíveis são **SMSRestart**, **ProgramRestart** ou **SMSLogoff**. Se esta entrada não é incluída, o programa não executa uma acção especial.  

-   **EstimatedDiskSpace**: Especifique a quantidade de espaço em disco que o programa de software necessita para ser executada no computador. Pode especificá-lo como **Desconhecido** (a predefinição) ou como um número inteiro igual ou superior a zero. Se for especificado um valor, é necessário especificar também as unidades para o valor.  

     Exemplo:  

     `EstimatedDiskSpace=38MB`  

-   **EstimatedRunTime**: Especifique a duração estimada (em minutos) que o programa poderá demorar a ser executado num computador cliente. Pode especificá-lo como **Desconhecido** (a predefinição) ou como um número inteiro superior a zero.  

     Exemplo:  

     `EstimatedRunTime=25`  

-   **SupportedClients**: Especifica os processadores e sistemas operativos onde este programa é executado. As plataformas especificadas devem ser separadas por vírgulas. Se esta entrada não é incluída, a verificação de plataforma suportada está desativada para este programa.  

-   **SupportedClientMinVersionX**, **SupportedClientMaxVersionX**: Especifique o intervalo de início para terminar para números de versão para os sistemas operativos que são especificados no **SupportedClients** entrada.  

     Exemplo:  

    ```  
    SupportedClients=Win NT (I386),Win NT (IA64),Win NT (x64)  
    Win NT (I386) MinVersion1=5.00.2195.4  
    Win NT (I386) MaxVersion1=5.00.2195.4  
    Win NT (I386) MinVersion2=5.10.2600.2  
    Win NT (I386) MaxVersion2=5.10.2600.2  
    Win NT (I386) MinVersion3=5.20.0000.0  
    Win NT (I386) MaxVersion3=5.20.9999.9999  
    Win NT (I386) MinVersion4=5.20.3790.0  
    Win NT (I386) MaxVersion4=5.20.3790.2  
    Win NT (I386) MinVersion5=6.00.0000.0  
    Win NT (I386) MaxVersion5=6.00.9999.9999  
    Win NT (IA64) MinVersion1=5.20.0000.0  
    Win NT (IA64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion1=5.20.0000.0  
    Win NT (x64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion2=5.20.3790.0  
    Win NT (x64) MaxVersion2=5.20.9999.9999  
    Win NT (x64) MinVersion3=5.20.3790.0  
    Win NT (x64) MaxVersion3=5.20.3790.2  
    Win NT (x64) MinVersion4=6.00.0000.0  
    Win NT (x64) MaxVersion4=6.00.9999.9999   
    ```  

-   **AdditionalProgramRequirements** (opcional): Forneça quaisquer informações ou outros requisitos para computadores cliente, até 127 carateres.

-   **CanRunWhen**: Especifique o estado de utilizador que o programa necessita para ser executada no computador cliente. Os valores disponíveis são **UserLoggedOn**, **NoUserLoggedOn** ou **AnyUserStatus**. O valor predefinido é **UserLoggedOn**.  

-   **UserInputRequired**: Especifique se o programa necessite de interação com o utilizador. Os valores disponíveis são **Verdadeiro** ou **Falso**. O valor predefinido é **Verdadeiro**. Esta entrada é definida como **Falso** se **CanRunWhen** não estiver definido como **UserLoggedOn**.  

-   **AdminRightsRequired**: Especifique se o programa necessita de credenciais administrativas no computador para ser executada. Os valores disponíveis são **Verdadeiro** ou **Falso**. O valor predefinido é **Falso**. Esta entrada é definida como **Verdadeiro** se **CanRunWhen** não estiver definido como **UserLoggedOn**.  

-   **UseInstallAccount**: Especifique se o programa utiliza a conta de instalação do Software de cliente quando este é executado em computadores cliente. Por predefinição, este valor é **Falso**. Este valor é também **Falso** se **CanRunWhen** estiver definido como **UserLoggedOn**.  

-   **DriveLetterConnection**: Especifique se o programa requer uma ligação de letra de unidade para os ficheiros do pacote que se encontram no ponto de distribuição. Pode especificar **Verdadeiro** ou **Falso**. O valor predefinido é **falso**, que permite que o programa utilizar uma ligação de convenção de Nomenclatura Universal (UNC). Quando este valor está definido como **verdadeiro**, a seguinte letra de unidade disponível é utilizada (começando z:) e prosseguir para trás).  

-   **SpecifyDrive** (opcional): Especifique uma letra de unidade que o programa necessário para estabelecer ligação para os ficheiros do pacote no ponto de distribuição. Esta especificação força a utilização da letra de unidade especificada para ligações de cliente para pontos de distribuição.

-   **ReconnectDriveAtLogon**: Especifique se o computador voltar a ligar ao ponto de distribuição quando o utilizador inicia sessão. Os valores disponíveis são **Verdadeiro** ou **Falso**. O valor predefinido é **Falso**.  

-   **DependentProgram**: Especifique um programa deste pacote que tem de executar antes do programa atual. Esta entrada utiliza o formato **DependentProgram**=<**NomedoPrograma>**, em que **<NomedoPrograma\>** é a entrada **Nome** do programa no ficheiro de definição do pacote. Se não houver programas dependentes, deixe esta entrada em branco.  

     Exemplo:  

     DependentProgram=Admin  
    DependentProgram=  

-   **Atribuição**: Especifique como o programa é atribuído aos utilizadores. Este valor pode ser: **FirstUser** (apenas o primeiro utilizador que inicia a sessão para o cliente executa o programa) ou **EveryUser** (todos os utilizadores que inicia sessão executarem o programa). Quando **CanRunWhen** não está definido como **UserLoggedOn**, esta entrada é definida como **FirstUser**.  

-   **Desativado**: Especifique se este programa pode ser publicitado aos clientes. Os valores disponíveis são **Verdadeiro** ou **Falso**. O valor predefinido é **Falso**.  

