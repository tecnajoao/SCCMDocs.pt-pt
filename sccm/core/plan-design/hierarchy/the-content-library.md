---
title: A biblioteca de conteúdos
titleSuffix: Configuration Manager
description: Saiba mais sobre a biblioteca de conteúdos do Configuration Manager utiliza para reduzir o tamanho geral do conteúdo distribuído.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 65c88e54-3574-48b0-a127-9cc914a89dca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 03c56b9870b145112e8f79932db681022bec7b89
ms.sourcegitcommit: 5875553bd814b7f82c16125f690c4bd2b6dd3a2b
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/11/2018
ms.locfileid: "44385087"
---
# <a name="the-content-library-in-configuration-manager"></a>A biblioteca de conteúdos no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

A biblioteca de conteúdos é um arquivo de instância única de conteúdo no Configuration Manager. O site utiliza para reduzir o tamanho geral do corpo combinado de conteúdo que distribui. A biblioteca de conteúdos armazena todos os ficheiros de conteúdo para implementações de software, por exemplo: atualizações de software, aplicativos e Implantações de SO.  

- O site automaticamente cria e mantém uma cópia da biblioteca de conteúdos de cada servidor do site e cada ponto de distribuição.  

- Antes do Configuration Manager adiciona ficheiros de conteúdo para o servidor do site ou copia os ficheiros para pontos de distribuição, ele verifica se cada ficheiro de conteúdo já se encontra na biblioteca de conteúdos.  

- Se o ficheiro de conteúdo estiver disponível, o Configuration Manager não copia o ficheiro. -Lo em vez disso, associa o ficheiro de conteúdo existente à aplicação ou pacote.  

Nos servidores de ponto de distribuição, configure as seguintes opções:

- Um ou mais unidades de disco no qual pretende criar a biblioteca de conteúdos.  

- Uma prioridade para cada unidade que utilizar.  

Gestor de configuração copia ficheiros de conteúdo para a unidade com a prioridade mais alta até essa unidade conter menos do que uma quantidade mínima de espaço livre que especificar.  

- Configurar as definições de unidade durante a instalação do ponto de distribuição.  

- Não é possível configurar as definições de unidade nas propriedades do ponto de distribuição após concluir a instalação.  


Para obter mais informações sobre como configurar as definições de unidade para o ponto de distribuição, consulte [gerir a infraestrutura de conteúdo e conteúda](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure).  


>  [!IMPORTANT]  
>  Para mover a biblioteca de conteúdos para uma localização diferente num ponto de distribuição após a instalação, utilize o **transferência da biblioteca de conteúdos** ferramenta nas ferramentas do Configuration Manager. Para obter mais informações, consulte a [ferramenta de transferência da biblioteca de conteúdos](/sccm/core/support/content-library-transfer).  



## <a name="about-the-content-library-on-the-central-administration-site"></a>Sobre a biblioteca de conteúdos no site de administração central  
Por predefinição, o Configuration Manager cria uma biblioteca de conteúdos no site de administração central, quando a instalação do site. A biblioteca de conteúdos é colocada na unidade do servidor do site que tenha mais disco espaço livre. Uma vez que não é possível instalar um ponto de distribuição no site de administração central, não é possível priorizar as unidades para utilização da biblioteca de conteúdos. Semelhante à biblioteca de conteúdos noutros servidores de site e nos pontos de distribuição, quando a unidade que contém a biblioteca de conteúdos fica sem espaço em disco disponível, a biblioteca de conteúdos aplica-se automaticamente à seguinte unidade disponível.  

O Configuration Manager utiliza a biblioteca de conteúdos no site de administração central nos seguintes cenários:  

- Criar conteúdo no site de administração central  

- Migrar o conteúdo a partir de outro site do Configuration Manager e atribui o site de administração central como o site que gere esse conteúdo  

> [!NOTE]  
>  Quando cria conteúdo num site primário e, em seguida, distribuí-la para outro site primário ou um site secundário abaixo de um site primário diferente, o site de administração central armazena temporariamente esse conteúdo da caixa de entrada do scheduler no site de administração central mas não adiciona esse conteúdo à respetiva biblioteca de conteúdos.  

Utilize as seguintes opções para gerir a biblioteca de conteúdos no site de administração central:  

- Para impedir que a biblioteca de conteúdos que está a ser instalado numa unidade específica, crie um ficheiro vazio designado **no_sms_on_drive**. Copie-o para a raiz da unidade antes da biblioteca de conteúdos é criada.  

- Depois da biblioteca de conteúdos tiver sido criada, utilize o **transferência da biblioteca de conteúdos** ferramenta a partir as ferramentas do Configuration Manager para gerir a localização da biblioteca de conteúdos. Para obter mais informações, consulte a [ferramenta de transferência da biblioteca de conteúdos](/sccm/core/support/content-library-transfer).  

> [!Note]  
> Pontos de distribuição de cloud não utilizam o armazenamento de instância única. O site encripta pacotes antes de enviar para o Azure, e cada pacote tem uma chave encriptada exclusiva. Mesmo se dois arquivos idênticos, as versões criptografadas seria o mesmo.  



## <a name="bkmk_remote"></a> Configurar uma biblioteca de conteúdos remota para o servidor do site  
<!--1357525--> A partir da versão 1806, para configurar [elevada disponibilidade do servidor do site](/sccm/core/servers/deploy/configure/site-server-high-availability) ou para libertar espaço no disco rígido no seu administração central ou servidores de site primário, reposicionar a biblioteca de conteúdos para outra localização de armazenamento. Mova a biblioteca de conteúdos para outra unidade no servidor do site, um servidor separado ou discos tolerante a falhas na rede de armazenamento (SAN). Uma SAN é recomendada, porque está altamente disponível e fornece armazenamento elástico que aumenta ou diminui ao longo do tempo para atender às suas necessidades em constante mudança conteúdas. Para obter mais informações, consulte [opções de elevada disponibilidade](/sccm/protect/understand/high-availability-options).

Uma biblioteca de conteúdos remota é um pré-requisito para [elevada disponibilidade do servidor do site](/sccm/core/servers/deploy/configure/site-server-high-availability). 

> [!Note]  
> Esta ação só mova a biblioteca de conteúdos no servidor do site. Não afetar a localização da biblioteca de conteúdos em pontos de distribuição. 

> [!Tip]  
> Também planear para gerenciar o conteúdo de origem do pacote, que é externo à biblioteca de conteúdos. Todos os objetos de software no Configuration Manager tem uma origem de pacote num compartilhamento de rede. Considere a centralização todas as origens para uma única partilha, mas certifique-se de que esta localização é redundante e de elevada disponibilidade. 
> 
> Se mover a biblioteca de conteúdos para o mesmo volume de armazenamento que as origens do pacote, não é possível marcar este volume para a eliminação de duplicados de dados. Enquanto a biblioteca de conteúdos suporta a eliminação de duplicados de dados, o volume de origens do pacote não suporta a ele. Para obter mais informações, consulte [a eliminação de duplicados de dados](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#bkmmk_datadedup).<!--SCCMDOcs issue #831-->  


### <a name="prerequisites"></a>Pré-requisitos  

- A conta de computador do servidor de site precisa **ler** e **escrever** permissões para o caminho de rede à qual esteja a mover a biblioteca de conteúdos. Não estão instalados componentes no sistema remoto.  

- O servidor do site não pode ter a função de ponto de distribuição. O ponto de distribuição também utiliza a biblioteca de conteúdos e esta função não suporta uma biblioteca de conteúdos remota. Depois de mover a biblioteca de conteúdos, não é possível adicionar a função de ponto de distribuição para o servidor do site.  

> [!Important]  
> Não reutilize os ficheiros numa localização de rede partilhada entre vários sites. Por exemplo, não utilize o mesmo caminho para um site de administração central e um site primário subordinado. Esta configuração tem o potencial para corromper a biblioteca de conteúdos e requerem que reconstrua ele.<!--SCCMDocs-pr issue 2764-->  


### <a name="process-to-manage-the-content-library"></a>Processo para gerir a biblioteca de conteúdos

1. Crie uma pasta numa partilha de rede como destino para a biblioteca de conteúdos. Por exemplo, `\\server\share\folder`.  

2. Na consola do Configuration Manager, mude para o **administração** área de trabalho. Expanda **configuração do Site**, selecione a **Sites** nó e selecione o site. Sobre o **resumo** separador na parte inferior do painel de detalhes, observe que uma nova coluna para o **biblioteca de conteúdos**.  

3. Clique em **biblioteca de conteúdos gerir** da faixa de opções.   

4. Na janela de gerir a biblioteca de conteúdos, o **localização atual** campo mostra o disco local e o caminho. Introduza um caminho de rede válido para o **nova localização**. Este caminho é a localização a que o site move a biblioteca de conteúdos. Tem de incluir um nome de pasta que já existe na partilha, por exemplo, `\\server\share\folder`. Clique em **OK**.  

5. Tenha em atenção a **estado** valor da coluna de biblioteca de conteúdos no separador Resumo do painel de detalhes. Atualiza para mostrar o progresso do site em mover a biblioteca de conteúdos.  

    - Embora **em curso**, o **mover progresso (%)** valor apresenta a percentagem concluída.  

    - Se houver um Estado de erro, o estado é apresentado o erro. Erros comuns incluem **acesso negado** ou **disco cheio**.  

    - Quando terminar apresenta **Complete**.  
    
    Consulte a **distmgr** para obter detalhes. Para obter mais informações, consulte [registos do servidor de sistema de site e o servidor do Site](/sccm/core/plan-design/hierarchy/log-files#BKMK_SiteSiteServerLog).  

Para obter mais informações sobre este processo, consulte [fluxograma - gerir a biblioteca de conteúdos](/sccm/core/plan-design/hierarchy/manage-content-library-flowchart).

O site realmente *cópias* os ficheiros de biblioteca de conteúdos para o local remoto. Este processo não elimina os ficheiros de biblioteca de conteúdos disponíveis na localização original do servidor do site. Para libertar espaço, um administrador tem de eliminar manualmente esses arquivos originais.

Se precisar de mover a biblioteca de conteúdos de volta ao servidor do site, repita este processo, mas que introduza uma unidade local e o caminho para o **nova localização**. Tem de incluir um nome de pasta que já existe na unidade, por exemplo, `D:\SCCMContentLib`. Quando o conteúdo original continua a existir, o processo move rapidamente a configuração para a localização local no servidor do site. 

> [!Tip]  
> Para mover o conteúdo para outra unidade no servidor do site, utilize o **transferência da biblioteca de conteúdos** ferramenta. Para obter mais informações, consulte a [ferramenta de transferência da biblioteca de conteúdos](/sccm/core/support/content-library-transfer).  



## <a name="inside-the-content-library"></a>Por dentro da biblioteca de conteúdos

> [!Warning]  
> A seção a seguir é fornecida apenas para fins informativos. Não alterar, adicionar ou remover quaisquer ficheiros ou pastas na biblioteca de conteúdos. Se o fizer, pode corromper os pacotes, conteúdo ou a biblioteca de conteúdos como um todo. Se suspeitar de quaisquer dados inválidos em falta, danificados ou, caso contrário, utilize a funcionalidade de validação na consola do Configuration Manager para detectar esses problemas. Em seguida, redistribuir os conteúdos afetados para corrigir os problemas. 

Por predefinição, a biblioteca de conteúdos é armazenada na raiz de uma unidade numa pasta denominada **SCCMContentLib**. Esta pasta é partilhada por predefinição como **SCCMContentLib$**. A pasta e partilha de ter permissões para evitar danos acidentais restritas. Todas as alterações devem ser feitas a partir da consola do Configuration Manager. Dentro dessa pasta são os seguintes objetos:  

- A biblioteca de pacote (**PkgLib** pasta): Informações sobre os pacotes estão presentes no ponto de distribuição.  

- A biblioteca de dados (**DataLib** pasta): Informações sobre a estrutura original dos pacotes.  

- A biblioteca de ficheiro (**FileLib** pasta): Os arquivos originais no pacote. Esta pasta é, normalmente, o que utiliza a maior parte do armazenamento.  

![Descrição geral de diagrama da biblioteca de conteúdos do Configuration Manager](media/content-library-overview.png)

> [!Tip]  
> Utilize o **Explorador de biblioteca de conteúdos** ferramenta a partir as ferramentas do Configuration Manager para procurar o conteúdo da biblioteca de conteúdos. Não é possível utilizar esta ferramenta para modificar o conteúdo. Ele fornece informações sobre o que está presente, bem como que permite de validação e de redistribuição. Para obter mais informações, consulte a [Explorador de biblioteca de conteúdos](/sccm/core/support/content-library-explorer).  


### <a name="package-library"></a>Biblioteca de pacote
A pasta de biblioteca do pacote **PkgLib**, inclui um ficheiro para cada pacote distribuído ao ponto de distribuição. O nome de ficheiro é o ID do pacote, por exemplo, `ABC00001.INI`. Neste ficheiro, sob o `[Packages]` secção é uma lista de IDs de conteúdo que fazem parte do pacote, bem como outras informações como a versão. Por exemplo, **ABC00001** é um pacote de legado na versão **1**. O ID de conteúdo neste ficheiro é `ABC00001.1`.


### <a name="data-library"></a>Biblioteca de dados
A pasta de biblioteca de dados **DataLib**, inclui um arquivo e uma pasta para cada um dos conteúdos em cada pacote. Por exemplo, este ficheiro e pasta são nomeados `ABC00001.1.INI` e `ABC00001.1`, respectivamente. O arquivo inclui informações para a validação. A pasta recria a estrutura de pasta do pacote original. 

Os ficheiros na biblioteca de dados são substituídos pelos ficheiros INI com o nome do ficheiro original no pacote. Por exemplo, `MyFile.exe.INI`. Esses arquivos incluem informações sobre o ficheiro original, como o tamanho, tempo modificado e o hash. Utilize os primeiros quatro carateres do hash para localizar o ficheiro original na biblioteca do ficheiro. Por exemplo, é o hash no MyFile.exe.INI **DEF98765**, e os quatro primeiros carateres são **DEF9**.


### <a name="file-library"></a>Biblioteca de ficheiro
Se a biblioteca de conteúdos se expande entre várias unidades, os ficheiros do pacote podem ser na pasta de biblioteca do ficheiro, **FileLib**, em qualquer uma destas unidades.

Localize um ficheiro específico com os quatro primeiros carateres do hash foi encontrado na biblioteca de dados. Dentro da pasta de biblioteca de ficheiro são muitas pastas, cada um com um nome de quatro carateres. Localize a pasta que corresponde aos primeiros quatro carateres de hash. Depois de localizar essa pasta, ele inclui um ou mais conjuntos de três arquivos. Estes ficheiros partilham o mesmo nome, mas um tem a extensão INI, um tem a extensão SIG e um tem nenhuma extensão de ficheiro. O ficheiro original é o sem extensão cujo nome é igual do hash da biblioteca de dados.

Por exemplo, a pasta **DEF9** inclui `DEF98765.INI`, `DEF98765.SIG`, e `DEF98765`. `DEF98765` é o original `MyFile.exe`. O ficheiro INI inclui uma lista de "utilizadores" ou IDs de conteúdo que partilham o mesmo arquivo. O site não remove um ficheiro, a menos que todos estes conteúdos também são removidos.


### <a name="drive-spanning"></a>Unidade de expansão

A biblioteca de conteúdos pode ser distribuída por várias unidades. Estas unidades é escolher ao criar o ponto de distribuição. Por predefinição, o Configuration Manager escolhe automaticamente as unidades na biblioteca de conteúdos de distribuição.

Ao escolher as unidades, selecione uma unidade primária e secundária. O site armazena todos os metadados sobre a unidade principal. Ele abrange apenas a biblioteca de ficheiro em toda a unidade do secundária. Nome da partilha da pasta para as unidades de secundárias inclui a letra de unidade. Por exemplo, se d: e e: unidades secundárias para a biblioteca de conteúdos, os nomes de partilha são **SCCMContentLibD$** e **SCCMContentLibE$**.

Se tiver escolhido o **automática** opção, o Configuration Manager seleciona a unidade com o espaço livre disponível mais como sua unidade principal. Ele armazena todos os metadados nesta unidade. O site abrange apenas a biblioteca de ficheiros em unidades de secundário. 

Especifique uma quantidade de espaço de reserva durante a configuração. O Configuration Manager tenta utilizar um disco secundário depois que o disco melhor tiver apenas a quantidade de espaço para esta reserva deixado gratuita. Sempre que uma nova unidade está selecionada para uso, a unidade com o mais espaço livre está selecionada.

Não é possível especificar que um ponto de distribuição deve usar todas as unidades, exceto um conjunto específico. Impedir que esse comportamento através da criação de um ficheiro vazio na raiz da unidade, chamada `NO_SMS_ON_DRIVE.SMS`. Coloque este ficheiro antes do Configuration Manager seleciona a unidade para utilização. Se o Configuration Manager detetar este ficheiro na raiz da unidade, ele não usa a unidade da biblioteca de conteúdos. 



## <a name="troubleshooting"></a>Resolução de Problemas

As sugestões seguintes podem ajudá-lo a resolver problemas com a biblioteca de conteúdos:  

- Reveja os registos no servidor do site (**distmgr** e **Pkgxfermgr**) e o ponto de distribuição (**smsdpprov.log**) para qualquer ponteiros para as falhas.  

- Utilize o [Explorador de biblioteca de conteúdos](/sccm/core/support/content-library-explorer) ferramenta.  

- Verifique a existência de bloqueios de arquivos por outros processos, como o software antivírus. Excluir a biblioteca de conteúdos em todas as unidades de análise automática de antivírus, bem como no diretório de testes temporário **SMS_DP$**, em cada unidade.  

- Para ver se existem erros de correspondência hash, valide o pacote a partir da consola do Configuration Manager.  

- Como uma última opção, redistribuir os conteúdos. Esta ação deve resolver a maioria dos problemas.  

