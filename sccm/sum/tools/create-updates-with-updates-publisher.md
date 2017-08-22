---
title: "Criar atualizações | Microsoft Docs"
description: "Criar e agrupar as atualizações de software com o System Center Updates Publisher"
ms.custom: na
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 46a1a8ac-126c-4ee6-ae09-32dfbdb83368
caps.latest.revision: "1"
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: NOINDEX, NOFOLLOW
ms.openlocfilehash: 98e490d7f5ca17dcf2a0aaa848f14e789f214123
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="create--software-updates-and-update-bundles-with-updates-publisher"></a>Criar as atualizações de software e atualizar os pacotes com o Updates Publisher

*Aplica-se a: O System Center Updates Publisher*

Com o Updates Publisher pode utilizar o **criar atualizar** Assistente para criar as suas próprias atualizações e a **criar pacote** Assistente para criar pacotes de atualizações.

Como estes dois assistentes têm um fluxo de trabalho semelhante, o procedimento para criar um pacote de atualização refere-se para o procedimento para criar atualizações, com apenas as diferenças relevantes detalhadas.

## <a name="use-the-create-update-wizard"></a>Utilize o Assistente de atualização de criar
1.  Na consola, aceda a **área de trabalho atualizações**e, em seguida, no **introdução** painel, escolha **atualização** do **home page** separador do Friso. Esta ação abre o **criar atualizar** assistente.

2.  No **pacote** página, utilize as seguintes informações para ajudar a configurar a atualização:

    -   Escolha **procurar** para localizar o pacote de atualização de software que irá utilizar como uma origem de pacote. Incluem origens válidas. MSI. \\&Lt;ServerName>\SMS_<SITECODE>\HOTFIX\<KB, ou. Ficheiros. EXE. Publicador de atualizações requer acesso ao ficheiro para criar um hash de ficheiro. O nome de ficheiro e hash, em seguida, são utilizados nos metadados da atualização para a atualização que está a criar.

    -   Especifique a localização de origem do conteúdo para esta atualização. Normalmente, esta é a localização onde o binário de atualização será transferido da durante a publicação para um servidor WSUS.  Se o **utilizar uma origem local para publicar conteúdo de atualização de software** opção está selecionada, em seguida, o caminho não é necessário.

        Mais tarde, quando a atualização é publicada para um servidor WSUS, o Updates Publisher transfere os binários da atualização na localização de origem indicado.  Se nenhum caminho for fornecido, em seguida, irá procurar Update Publisher o [caminho de publicação de origem local](/sccm/sum/tools/updates-publisher-options#advanced) para o binário de atualização.

    -   Especifique o **idioma binário** da atualização de software.

    -   Especifique **códigos de retorno de êxito**, e **êxito pendente de reinício códigos** para a atualização. Separe os vários códigos de retorno com uma vírgula. Pode utilizar códigos de retorno para determinar quando a instalação da atualização foi concluída com êxito e, quando reinícios eram necessários.

        -   Ficheiros do Windows installer e patches (. MSI e. Ficheiros de \\<ServerName>\SMS_<SITECODE>\HOTFIX\<KB) definido automaticamente estes valores e que não podem ser modificados.

        -   Para. EXE de atualizações, os códigos de predefinição definidos pelo. O ficheiro EXE são utilizados se forem especificados códigos de retorno.

    -   Especifique os argumentos da linha de comandos que são necessários para instalar a atualização de software.

        -   Ficheiros do Windows installer e patches (. MSI e. Ficheiros de \\<ServerName>\SMS_<SITECODE>\HOTFIX\<KB) são definidas automaticamente estes valores. Para estes tipos de ficheiros de argumentos tem de ser especificados como  **\[nome\]=\[valor\]**. Além disso, todas as opções que começar a utilizar um  **/**  (como **/qn**) não são suportadas. MSI ou. Atualizações de software \\<ServerName>\SMS_<SITECODE>\HOTFIX\<KB.

        -   Para. Atualizações EXE, todos os argumentos são válidos.

3.  No **informações** página, especifique os detalhes sobre a atualização, que estão incluídos quando a atualização é publicada ou exportada. Detalhes incluem propriedades localizadas, como o nome de atualizações (título) e a descrição. Em seguida, especifique os detalhes mais gerais, tais como a classificação, fabricante, produto e onde saber mais sobre a atualização.

     __Propriedades localizadas:__

    -   **Idioma**: Selecione um idioma e, em seguida, especifique um título e descrição. Em seguida, pode selecionar idiomas adicionais, um de cada vez, com cada idioma que suporta a sua própria título e descrição.

    -   **Título**: Introduza o nome da atualização. Este nome apresenta na área de trabalho de atualizações da consola do Updates Publisher.

    -   **Descrição**: Uma descrição amigável da atualização. Pode incluir o que a instalação da atualização e por que motivo ou quando deve ser utilizada.

     **Classificação:** Seguem-se descrições comuns para as classificações diferentes.

    -   **Atualização**: Uma atualização para uma aplicação ou o ficheiro que está atualmente instalado.

    -   **Crítico**: Uma atualização amplamente lançada para um problema específico que corrige um crítico não relacionado com segurança.

    -   **Pacote de funcionalidades**: Novas funcionalidades do produto que são distribuídas fora de uma versão de produto e que normalmente estão incluídas na próxima versão completa do produto.

    -   **Segurança**: Uma atualização amplamente lançada para um problema específico do produto que está relacionado com segurança.

    -   **Update Rollup**: Um conjunto cumulativo de correções que são agrupadas para facilitar a implementação. Estas correções podem incluir atualizações de segurança, atualizações críticas, atualizações e assim sucessivamente. Um update rollup resolve geralmente uma área específica, tal como segurança ou uma funcionalidade do produto.

    -   **Pacote de serviço**: Um conjunto cumulativo de correções que são aplicadas a uma aplicação. Estas correções podem incluir atualizações de segurança, atualizações críticas, atualizações de software e assim sucessivamente.

    -   **Ferramenta**: Especifica uma ferramenta ou funcionalidade que ajuda a concluir as tarefas de um ou mais.

     -   **Controlador**: Uma atualização de software do controlador.

    **Fornecedor:** Especifique um fornecedor para a atualização. Pode utilizar na lista pendente para utilizar valores de atualizações que estão no repositório. Quando especificar um fornecedor, o assistente cria uma pasta com esse nome de fornecedor em **todas as atualizações de Software** no **área de trabalho atualizações** se nessa pasta não existe. Seguem-se os nomes do Windows Server Update Services (WSUS) reservado que não podem ser introduzidos para atualizações de que criar:
 >*   Microsoft Corporation
 >*   Microsoft
 >*   Atualização
 >*   Atualização de software
 >*   Ferramentas
 >*   Ferramenta
 >*   Crítico
 >*   Atualizações críticas
 >*   Segurança
 >*   Atualizações de segurança
 >*   Pacote de funcionalidades
 >*   Rollup de atualização
 >*   Service Pack
 >*   Controlador
 >*   Atualização do controlador
 >*   Pacote
 >*   Atualização do pacote

**Produto**: Especifique o tipo de produto que se aplica a atualização. Pode utilizar na lista pendente para utilizar valores de atualizações que estão no repositório. A mesma lista de WSUS reservado nomes que não podem ser utilizados para **fornecedor**, não pode ser utilizado para **produto**.

 **Mais informações URL**: Especifique o URL onde pode encontrar mais informações sobre esta atualização. Tem de utilizar letras minúsculas para **https** ou **http** quando introduzir este URL.

4.  No **informações opcionais** página, pode configurar detalhes que fornecem informações adicionais sobre a atualização.

    -   **ID do boletim**: ID do boletim é, normalmente, mas nem sempre, fornecidos pelos fornecedores de atualização.

    -   **ID de artigo**: Se estiver disponível um artigo de atualização de software, o ID do artigo podem ser úteis para indivíduos para procurar informações adicionais sobre a atualização.

    -   **IDs de Exposures:** Liste um ou mais comuns de vulnerabilidades e identificadores de CVE (Exposures) que fornecem informações de segurança sobre a atualização ou atualizar o pacote. Quando a listagem mais do que um, utilize um ponto e vírgula para separar CVEs tal como neste exemplo: *CVE1; CVE2.*

    -   **URL de suporte:** Liste o URL que contém as informações de suporte para esta atualização, se disponível. Tem de utilizar letras minúsculas para **https** ou **http** quando introduzir este URL.

    -   **Gravidade:** Defina o nível de gravidade para esta atualização.

    -   **Impacto:** As seguintes opções podem ser utilizadas para especificar o impacto:
        -   **Normal –** utilizá-lo para indicar a atualização requer procedimentos de instalação típicas.
        -   **Secundárias –** utilizá-lo para indicar a atualização requer procedimentos de instalação mínima.
        -   **Requer processamento exclusivo –** utilizá-lo para indicar a atualização tem de ser instalada por si só, exclusivo de quaisquer outras atualizações.   <br /><br />

    -   **Comportamento de reinício:** Utilize esta opção para fornecer informações sobre o comportamento de reinício de atualizações. Esta definição não afeta o comportamento da instalação da atualização real.

        -   **Nunca reinicia**: O computador nunca efetua um reinício do sistema depois de instalar a atualização de software.
        -   **Requer sempre reinício**: O computador efetua sempre um reinício do sistema depois de instalar a atualização de software.
        -   **Pode pedir reinício**: Depois de instalar a atualização de software, o computador pede um reinício do sistema apenas se for necessário um reinício. O utilizador tem a opção para adiar o reinício. Este é o valor predefinido. <br /><br />

5.  No **pré-requisitos** página, especifique os pré-requisitos que devem ser instalados num computador antes de instalar esta atualização. Pré-requisitos podem ser **detectoids** ou outras atualizações. Detectoids são regras de alto nível, como um que requer que os computadores da CPU para um processador de 64 bits. Detectoids também pode especificar atualizações específicas que tem de estar instaladas antes de instalar esta atualização.

    -   Para um melhor desempenho, utilize detectoids em vez de criar *instalável* e *instalado regras* que executam a mesma verificação ou a ação.

    Utilize a opção de pesquisa para **atualizações de software disponíveis e detectoids** para ajudar a encontrar atualizações específicas ou detectoids. Por exemplo, uma procura **CPU** para localizar o detectoids que lhe permitem limitar a instalação com base na arquitetura de CPU específica.

    Pode selecionar um ou mais itens em simultâneo para adicionar como um pré-requisito. Ao adicionar pré-requisitos, os detectoids selecionados são adicionados como um ou mais grupos. Para se qualificar para a instalação, um computador tem de cumprir o requisito de pelo menos um membro de cada grupo que configurou:

 -   Ao clicar em **adicionar pré-requisitos** todos os itens que selecionou são adicionados a grupos individuais, separados,. Para se qualificar para esta atualização, um computador tem de cumprir os pré-requisitos neste grupo e passar os requisitos de todos os grupos adicionais que estão configurados.

 -   Ao clicar em **adicionar grupo,** todos os itens que selecionou são adicionados a um único grupo. Para se qualificar para esta atualização, um computador tem de cumprir, pelo menos, um dos pré-requisitos neste grupo e passar os requisitos de todos os grupos adicionais que estão configurados.

6.  No **substituição** página, especifique as atualizações que são substituídas (substituídas) por esta atualização. Quando esta atualização for publicada, o Configuration Manager irá marcar cada atualização que é substituída como **expirado**. Os clientes, em seguida, irão instalar esta atualização em vez das atualizações substituídas.

7.  No **aplicabilidade** página utilize o **Editor de regras** para definir um conjunto de regras que determinam se um dispositivo tem desta atualização. (Esta página é semelhante a **instalada** página, o seguinte.)

    Para adicionar uma nova regra, clique em ![Nova regra](media/newrule.png). Esta ação abre a página de regra de aplicabilidade onde pode configurar as regras.

    Os tipos de regras, que pode criar incluem:

    -   **Ficheiro** – utilizar esta regra para exigir que um dispositivo tem um ficheiro com propriedades que cumprem um ou mais critérios que especificar antes desta atualização podem ser aplicados.

    -   **Registo –** utilizar este tipo para especificar detalhes de registo que tem de existir antes de um dispositivo se qualificam instalar esta atualização.

    -   **Sistema –** esta regra utiliza detalhes de sistema para determinar a aplicabilidade. Pode escolher entre definir uma versão do Windows, um idioma do Windows, a arquitetura de processador ou especificar uma consulta WMI para identificar o sistema operativo de dispositivos.

    -   **Windows Installer –** utilizar este tipo de regra para determinar a aplicabilidade com base num instalado. MSI ou do Windows Installer patch (. \\&LT;SERVERNAME&GT;\SMS_&LT;SITECODE&GT;\HOTFIX\&LT;KB). Também pode determinar se os componentes específicos ou funcionalidades são instaladas como parte do requisito.

        > [!IMPORTANT]  
        > No geridos deices, o Windows Update Agent não conseguiu detetar o Windows instalar pacotes que são instaladas por utilizador. Quando utilizar este tipo de regra, configure as regras de aplicabilidade adicionais, como as versões de ficheiro ou valores de chave de registo, para que o pacote Windows Installer pode ser detetado corretamente independentemente numa base por utilizador ou por sistema.

    -   **Guardar a regra –** esta permite opção Localizar e utilizar as regras *criada na área de trabalho de regras*.

        Depois de criar uma regra, pode utilizar os ícones de outros para modificar a regra, e se existem várias regras, para definir relações entre essas regras.

    Quando já está a criar e adicionar regras, clique em **OK** no **criar conjunto de regras de** caixa de diálogo para guardar o conjunto. Em seguida, pode criar um **novo** regra e adicione que, bem como ao conjunto.

    Quando tiver várias regras ou define a regra para adicionar a uma atualização, pode utilizar os operadores lógicos no **Editor de regras** para determinar as condições entre as regras e a ordem pela qual processam.

8.  No **instalada** página utilize o **Editor de regras para** definir um conjunto de regras que determinam se um dispositivo já tem instalada a atualização está a configurar. (Esta página é semelhante a **aplicabilidade** página, que as prossegue nesta página.)

    Esta página do assistente suporta configurar regras com as mesmas opções e critérios de como o **aplicabilidade** página.

    Quando concluir o assistente, a nova atualização é adicionada a um nó no **atualiza a área de trabalho** que é identificado pelo **fornecedor** e **produto** nome utilizado para essa atualização.

## <a name="use-the-create-bundle-wizard"></a>Utilize o assistente criar pacote
Uma vez que este assistente utiliza o mesmo fluxo de trabalho como o [assistente criar atualizar](#use-the-create-update-wizard), utilizar esse fluxo de trabalho, mas tenha em atenção a seguinte diferença para pacotes:

1.  Para iniciar o assistente, na consola do aceda a **área de trabalho atualizações**e, em seguida, selecione **pacote** do **home page** separador do Friso.

2.  Ao contrário do assistente criar atualizar, não há nenhuma página de pacote ao criar um pacote.

3.  No **informações** página, especifique os detalhes sobre o pacote de atualização que estão incluídos quando a atualização é publicada ou exportada.

4.  No **informações opcionais** página, pode configurar detalhes que fornecem informações adicionais sobre o pacote de atualização. As opções disponíveis são iguais para criação de uma atualização. No entanto, as opções de impacto e o comportamento de reinício não estão disponíveis como estas não são aplicadas a pacotes.

5.  No **pré-requisitos** página, especifique os pré-requisitos que devem ser instalados num computador antes de pode instalar este pacote. Estas regras são os mesmos visto para as atualizações individuais.

6.  No **substituição** página, especifique as atualizações que são substituídas (substituídas) por este pacote de atualização. Estas regras são os mesmos visto para as atualizações individuais.

7.  No **membros** página, selecione atualizações para adicionar o pacote de atualização. Estão disponíveis apenas as atualizações de ter criado ou importado para o Updates Publisher.

Quando concluir o assistente, o novo pacote de atualização é adicionado a um nó a **atualiza a área de trabalho** que é identificado pelo **fornecedor** nome utilizado para o pacote de atualização.
