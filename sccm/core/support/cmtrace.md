---
title: CMTrace
titleSuffix: Configuration Manager
description: Saiba mais sobre como utilizar a ferramenta CMTrace para ver ficheiros de registo para o Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6a4a3290-5228-4871-918a-554aa1c20834
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3ad96cedf1170f8563fdafe3922f6ad2e7c67b5a
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39386872"
---
# <a name="cmtrace"></a>CMTrace

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

CMTrace é um da [ferramentas do Configuration Manager](/sccm/core/support/tools). Permite-lhe ver e monitorizar ficheiros de registo, incluindo os seguintes tipos:  

- Ficheiros de registo no formato do Configuration Manager ou o Gestor de componentes de cliente (CCM)  

- Sem formatação ASCII ou Unicode ficheiros de texto, por exemplo, registos do instalador do Windows  

A ferramenta ajuda a analisar ficheiros de registo, realce, filtragem e pesquisa de erros.

A partir da versão 1806, o ferramenta de visualização de registos de CMTrace é instalado automaticamente, juntamente com o cliente do Configuration Manager. Este é adicionado ao diretório de instalação do cliente, que, por predefinição, é `%WinDir%\CCM\CMTrace.exe`.<!--1357971-->

> [!Note]  
> CMTrace automaticamente não estiver registado com o Windows para abrir a extensão de ficheiro. log. Para obter mais informações, consulte [associações de arquivo](#file-associations).  



## <a name="usage"></a>Utilização

Execute **CMTrace.exe**. Na primeira vez que executar a ferramenta, verá uma linha de comandos para a associação de ficheiro. Para obter mais informações, consulte [associações de arquivo](#file-associations).

Dê a maioria das ações a na CMTrace partir os seguintes menus:
- [Ficheiro](#file-menu)
- [Ferramentas](#tools-menu)


### <a name="file-menu"></a>Menu ficheiro

As ações seguintes estão disponíveis no **ficheiro** menu:  
- [abrir](#open)
- [Aberta no servidor](#open-on-server)
- [Impressão](#print)
- [Preferências](#preferences)

O menu Arquivo também lista os últimos oito ficheiros recentes. Reabra rapidamente uma destes registos, selecionando-a partir do menu ficheiro. 

#### <a name="open"></a>Abrir
Apresenta a caixa de diálogo de abertura para navegar para um ficheiro de registo. 

Filtre a vista para os ficheiros dos seguintes tipos: 
- Ficheiros de registo (\*. log)  
- Ficheiros de registo antigos (\*. lo _) 
- Todos os ficheiros (\*.\*)

As duas opções seguintes não são selecionadas por predefinição:  

- **Ignorar linhas existentes**: Quando selecionada, a CMTrace ignora o conteúdo existente do ficheiro de registo selecionada e apresenta novas linhas apenas como estes serão adicionados. Utilize esta opção para monitorizar apenas novas ações quando não precisar do histórico completo do ficheiro de registo.  

- **Intercalar os ficheiros selecionados**: Se ativar esta opção e selecione mais de um ficheiro de registo, CMTrace mescla os registos selecionados na vista. Apresenta-os como se fossem um único ficheiro de registo. O registo intercalado atualiza o mesmo e oferece suporte a todos os outros recursos de CMTrace como se fosse um único ficheiro de registo.  


#### <a name="open-on-server"></a>Aberta no servidor
Procure a pasta de registos do Configuration Manager no computador do sistema de sites com a caixa de diálogo de procura padrão. Também pode navegar da rede para um computador remoto.   

Quando seleciona um computador remoto para procurar, CMTrace verifica-se para a partilha do Configuration Manager. Se não for possível encontrar uma partilha com ficheiros de registo do Configuration Manager, ele exibe uma mensagem de erro.  

Para ligar diretamente a um computador conhecido sem navegar, utilize o [aberto](#open) ação. Em seguida, introduza um nome de servidor e partilhar com o formato UNC.

#### <a name="print"></a>Impressão
Exiba a caixa de diálogo de impressão do Windows padrão. Esta ação envia o arquivo de log atual para uma impressora. Formata o resultado, de acordo com as definições no separador de impressão de preferências de CMTrace.

#### <a name="preferences"></a>Preferências
Configure definições para a ferramenta CMTrace. Estão disponíveis as seguintes opções:  

- **Geral** separador  

     - **Atualizar intervalo**: Controla a frequência CMTrace verifica a existência de alterações em arquivos de log e carrega novas linhas. Por predefinição, este valor é de 500 milissegundos.  

     - **Realçar**: Define a cor que CMTrace utiliza ao realçar linhas de registo que escolher. Por predefinição, esta cor é amarelo básico (vermelho: 255, verde: 255, azul: 0).  

     - **Colunas**: Configura as colunas que estão visíveis na vista de registo e a ordem em que aparecem. Por padrão, ele exibe o texto de registo, o componente, Thread e data/hora.  

- **Impressão** separador  

     - **Colunas**: Configure as colunas que utiliza durante a impressão de ficheiros de registo e a ordem em que aparecem. Por predefinição, imprime as mesmas colunas como ele exibe.  

     - **Orientação**: Define a orientação de impressão padrão durante a impressão de ficheiros de registo. Substitua esta definição na caixa de diálogo de impressão. Por predefinição, utiliza orientação retrato.  
 
- **Advanced** separador  

     - **Intervalo de atualização**: Força a ferramenta CMTrace para atualizar a vista de registo num intervalo especificado ao carregar um grande número de linhas. Por predefinição, esta opção está desativada por um valor igual a zero.  

        > [!Note]  
        > Em geral, não modifique os **atualizar intervalo**. Pode aumentar significativamente a quantidade de tempo que demora a abrir os ficheiros de registo grandes. 


### <a name="tools-menu"></a>Menu Ferramentas
As ações seguintes estão disponíveis no **ferramentas** menu:  
- [Localizar](#find)
- [Localizar seguinte](#find-next)
- [Copiar para área de transferência](#copy-to-clipboard)
- [Realçar](#highlight)
- [Filtro](#filter)
- [Pesquisa de erros](#error-lookup)
- [Colocar em pausa](#pause)
- [Mostrar/ocultar detalhes](#show-hide-details)
- [Mostrar/Ocultar painel de informações](#show-hide-info-pane)

#### <a name="find"></a>Localizar
Procure no ficheiro de registo abertos para uma cadeia de texto especificado.  

#### <a name="find-next"></a>Localizar seguinte
Localiza a seguinte seqüência de caracteres, anteriormente especificados na caixa de diálogo Localizar.  

#### <a name="copy-to-clipboard"></a>Copiar para área de transferência
Copia as linhas selecionadas como texto simples para a área de transferência do Windows. Se estiver analisando o Configuration Manager e os ficheiros de registo CCM, copia as colunas na mesma ordem como o modo de exibição. Ela separa cada coluna por um caractere de tabulação. Utilize esta ação ao copiar os registos em mensagens de e-mail ou outros documentos.  

#### <a name="highlight"></a>Realçar
Introduza uma cadeia de caracteres que CMTrace utiliza para pesquisar o texto de cada entrada de registo. Ele destaca, em seguida, qualquer texto de registo que corresponda ao introduzir a cadeia de caracteres.  

- O destaque utiliza a cor que especificou nas preferências das.  

- Desativar realce, limpar a cadeia a partir deste campo.  

- Se introduzir um número decimal ou hexadecimal, CMTrace tenta corresponder o valor para a coluna de Thread. Utilize este comportamento para realçar o processamento de um único thread, sem filtrar outros threads que podem interagir com ele.  

- Para comparar cadeias de caracteres por caso, ative a opção para **maiúsculas de minúsculas**.  
 
#### <a name="filter"></a>Filtro
Mostrar ou ocultar as linhas de registo com base nos critérios especificados. Aplica filtros a qualquer uma das quatro colunas, independentemente se estão visíveis. Estas definições aplicam-se cada ficheiro de registo abertos. 

Exemplos: <!--SCCMDocs issue #603-->
- Filtro **smsts** no texto de entrada que contenham "a ação" ou "o grupo". 
- Filtro **Inventoryagent** em que o texto de entrada contém "destino".


#### <a name="error-lookup"></a>Pesquisa de erros
Escreva ou cole um código de erro no formato decimal ou hexadecimal para exibir uma descrição. Origens de erro possíveis incluem: Windows, WMI ou Winhttp.

#### <a name="pause"></a>Colocar em pausa
Suspender ou reiniciar a monitorização do registo. Os seguintes casos de utilização são algumas das razões possíveis para utilizar esta ação:  

- Quando CMTrace está exibindo informações de ficheiro de registo demasiado rapidamente  

- Quando pausar a monitorização do registo, as informações apresentadas CMTrace não perdidas se o ficheiro atual passa para um novo registo  

- Quando quiser parar CMTrace de apresentar novos dados enquanto examinar o ficheiro de registo  

#### <a name="showhide-details"></a>Mostrar/ocultar detalhes
Mostrar ou ocultar todas as colunas que não seja o texto de registo. Também se expande a coluna de texto de registo para a largura da janela. Utilize esta ação quando estiver a ver registos num computador com a exibição de baixa resolução. Ele apresenta mais o texto de registo.  

> [!Note]   
> Ao visualizar os ficheiros de texto sem formatação, CMTrace automaticamente oculta detalhes porque eles sempre vazios.  
 
#### <a name="showhide-info-pane"></a>Mostrar/Ocultar painel de informações
Mostrar ou ocultar o painel de informações. Utilize esta ação quando estiver a ver registos num computador com a exibição de baixa resolução. Ele apresenta mais detalhes de registo.  



## <a name="log-pane"></a>Painel de registo

O painel de log é na parte superior da janela CMTrace. Ele exibe linhas dos ficheiros de registo. 

Quando seleciona uma linha, está temporariamente realçada usando o esquema de cores de seleção do Windows. 

Linhas realçadas correspondem os critérios definidos por si com o **realce** opção a **ferramentas** menu. O destaque utiliza a cor que especificou no **preferências**.

CMTrace Exibe linhas com erros através de um plano de fundo vermelho e a cor do texto amarelo. Nos registos do formato de CCM, entradas de registo tem um valor de tipo explícito que indica a entrada como um erro. Para outros formatos de log, CMTrace faz uma pesquisa de maiúsculas e minúsculas em cada entrada para qualquer texto cadeia de caracteres "erro de correspondência".

Ele exibe linhas com avisos com um plano de fundo amarelo. Nos registos do formato de CCM, entradas de registo tem um valor de tipo explícito que indica a entrada como um aviso. Para outros formatos de log, CMTrace faz uma pesquisa de maiúsculas e minúsculas em cada entrada para qualquer cadeia de caracteres de texto que "Avisar".



## <a name="info-pane"></a>Painel de informações

O painel de informações é na parte inferior da janela CMTrace. Ele inclui as seguintes funcionalidades:   

- Detalhes sobre a entrada de registo atualmente selecionado  

- Uma caixa de texto que apresenta o texto de registo  

- Ele exibe os retornos de carro, para que o texto formatado é mais fácil de ler  

- Mais fácil de ler entradas longas que não são totalmente visíveis no painel de registo  

Mostrar ou ocultar o painel de informações com o **Mostrar/Ocultar painel de informações** opção a **ferramentas** menu. Se o painel de informações ocupa-se mais da metade da janela do log, CMTrace automaticamente oculta-lo.


### <a name="progress-bar"></a>Barra de progresso

Primeira vez que abrir um ficheiro de registo, CMTrace substitui o painel de informações por uma barra de progresso. Este curso indica a quantidade do ficheiro existente de conteúdo que é carregado. O progresso atinge 100 por cento, CMTrace remove a barra de progresso e substitui-o com o painel de informações. Quando carrega ficheiros grandes, esse comportamento fornece uma indicação de quanto tempo a carga pode demorar.


### <a name="status-bar"></a>Barra de status

Para o formato do Configuration Manager e os ficheiros de registo de formato de CCM, na barra de estado apresenta o tempo decorrido para as entradas de registo selecionado. Se selecionar uma única entrada, a ferramenta exibe a hora da primeira entrada de log para a entrada selecionada. Se selecionar várias entradas, ele calcula o tempo da entrada selecionada mais para a entrada selecionada na extremidade inferior. CMTrace formatos essas informações da seguinte forma:

`Elapsed time is <hours>h <minutes>m <seconds>s <milliseconds>ms (<seconds+milliseconds> seconds)`



## <a name="windows-shell-integration"></a>Integração de shell do Windows

Oferece suporte a ferramenta CMTrace [associações de arquivo](#file-associations) e [arrastar-e-soltar](#drag-and-drop).


### <a name="file-associations"></a>Associações de arquivo 

CMTrace pode associar-se em si, com extensões de nome de ficheiro. log e. lo _. Quando o programa é iniciado, ele verifica o registo para determinar se já está associado com estas extensões de nome de ficheiro. Se não estiver associado a nenhuma extensão de nome de ficheiro CMTrace, lhe for pedido para associar as extensões de nome de ficheiro com a ferramenta CMTrace. Se selecionou **não a perguntar**, CMTrace ignora esta verificação, sempre que for executada neste computador.


### <a name="drag-and-drop"></a>Arrastar e largar

CMTrace suporta a funcionalidade básica de arrastar e soltar. Arraste um ficheiro de registo a partir do Explorador do Windows para CMTrace para abri-lo.



## <a name="other-tips"></a>Outras dicas

### <a name="last-directory-registry-key"></a>Última chave de registo de diretório
<!--511280--> Por predefinição, a CMTrace guarda a localização do registo última que abriu. Este comportamento é útil no servidor do site, como predefinições para o caminho dos registos de cada vez. 

Na primeira vez que iniciá-lo num cliente, é assumida como predefinição para o diretório de trabalho atual. Esta localização pode ser o caminho onde o guardou CMTrace, ou um caminho como `%userprofile%\Desktop`. 

O **Directory último** valor na chave do registo `HKEY_CURRENT_USER\Software\Microsoft\Trace32` controla esta localização predefinida. Se definir este valor como `%windir%\CCM\Logs` em seus clientes, em seguida, CMTrace abre os arquivos o tempo de localização a primeira de registo de cliente executá-lo.


## <a name="see-also"></a>Consulte também

[Ficheiros de registo](/sccm/core/plan-design/hierarchy/log-files)
