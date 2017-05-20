---
title: "Criar atualizações | Documentos do Microsoft"
description: "Criar e do pacote de atualizações de software com o System Center Updates Publisher"
ms.custom: na
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 46a1a8ac-126c-4ee6-ae09-32dfbdb83368
caps.latest.revision: 1
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: NOINDEX, NOFOLLOW
ms.translationtype: Machine Translation
ms.sourcegitcommit: 31819a1df4e63e1114682490a9b3c3b4e5c99cfa
ms.openlocfilehash: 33b188f4a9c14091429d1f49e07f1f17fbf98516
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="create--software-updates-and-update-bundles-with-updates-publisher"></a>Criar atualizações de software e atualizar os pacotes com o Updates Publisher

*Aplica-se a: System Center Updates Publisher*

Com o Updates Publisher pode utilizar o **criar atualizar** Assistente para criar as suas próprias atualizações e **criar pacote** Assistente para criar pacotes de atualizações.

Uma vez que estes dois assistentes tem um fluxo de trabalho semelhante, o procedimento para criar um pacote de atualização refere-se para o procedimento para criar atualizações, com apenas as relevantes diferenças detalhadas.

## <a name="use-the-create-update-wizard"></a>Utilize o Assistente de atualização de criar
1.  Na consola de ir para **área de trabalho atualizações**e, em seguida, no **introdução** painel, escolha **atualização** a partir do **base** separador do Friso. Esta ação abre o **criar atualizar** assistente.

2.  No **pacote** página, utilize as seguintes informações para ajudar a configurar a atualização:

    -   Escolher **procurar** para localizar o pacote de atualização de software que irá utilizar como uma origem de pacote. Origens de dados válidas incluem. MSI. MSP, ou. Ficheiros. EXE. Updates Publisher cria um hash do ficheiro. O hash e nome de ficheiro são então utilizadas nos metadados de atualização para a atualização que está a criar.

    -   Especifique a localização de origem do conteúdo para esta atualização. Quando tiver uma cópia local do conteúdo, pode selecionar a caixa de verificação **utilizar uma origem local para publicar conteúdos de atualização de software** para utilizar o [caminho de publicação de origem local](/sccm/sum/tools/updates-publisher-options#advanced) (e opção avançada). Se esta opção não estiver selecionada, tem de especificar um URL onde a atualização pode ser encontrada na web. Este caminho ou URL é adicionado aos metadados de atualização.

        Mais tarde, quando a atualização é publicada para um servidor WSUS, o Publisher atualizações obtém os binários da atualização na localização de origem indicado.

    -   Especifique o **idioma binário** da atualização de software.

    -   Especifique **códigos de retorno de êxito**, e **êxito pendente de reinício códigos** para a atualização. Com uma vírgula para separar vários códigos de retorno. Pode utilizar códigos de retorno para determinar quando a instalação da atualização foi efetuada com êxito e, quando foram necessários reinícios.

        -   Ficheiros de programa de instalação do Windows e patches (. MSI e. Os ficheiros MSP) definidos automaticamente estes valores e não podem ser modificadas.

        -   Para. EXE códigos de atualizações, os predefinição definidos pelo. Ficheiro. EXE são utilizados se forem especificados não códigos de retorno.

    -   Especifique os argumentos da linha de comandos que são necessários para instalar a atualização de software.

        -   Ficheiros de programa de instalação do Windows e patches (. MSI e. Ficheiros MSP) defina automaticamente estes valores. Para estes tipos de ficheiro os argumentos devem ser especificados como  **\[nome\]=\[valor\]**. Além disso, todas as opções que comece com um  **/**  (como **/qn**) não são suportadas. MSI ou. MSP atualizações de software.

        -   Para. As atualizações. EXE, todos os argumentos são válidos.

3.  No **informações** página, especifique os detalhes sobre a atualização que estão incluídos quando a atualização é publicada ou exportada. Detalhes incluem propriedades localizadas como o nome de atualizações (o título) e a descrição. Em seguida, especifique os detalhes mais gerais, tais como a classificação, fornecedor, produto e onde pode saber mais sobre a atualização.

    * * Propriedades localizadas: * *

    -   **Idioma**: Selecione um idioma e, em seguida, especifique um título e descrição. Em seguida, pode selecionar idiomas adicionais, um de cada vez, com cada idioma que suporte o seu próprio título e descrição.

    -   **Título**: Introduza o nome da atualização. Apresenta este nome na área de trabalho atualizações da consola do Updates Publisher.

    -   **Descrição**: Uma descrição amigável da atualização. Podem incluir a atualização instala e por que razão e quando deve ser utilizada.

  **Classificação:** Seguem-se comuns descrições para as classificações de diferentes.

  -   **Atualização**: Uma atualização para uma aplicação ou um ficheiro que está atualmente instalado.

  -   **Crítico**: Uma atualização amplamente lançada para um problema específico que corrige um erro crítico não relacionado com segurança.

  -   **Pacote de funcionalidades**: Novas funcionalidades do produto que são distribuídas fora de uma versão de produto e que normalmente estão incluídas na próxima versão completa do produto.

  -   **Segurança**: Uma atualização amplamente lançada para um problema específico do produto que está relacionado com segurança.

  -   **Coletânea de atualizações**: Um conjunto cumulativo de correções que são agrupadas para facilitar a implementação. Estas correções podem incluir atualizações de segurança, atualizações críticas, atualizações e assim sucessivamente. Um rollup de atualizações resolve geralmente uma área específica, tal como segurança ou uma funcionalidade do produto.

  -   **Service Packs**: Um conjunto cumulativo de correções que são aplicadas a uma aplicação. Estas correções podem incluir atualizações de segurança, atualizações críticas, atualizações de software e assim sucessivamente.

  -   **Ferramenta**: Especifica uma ferramenta ou funcionalidade que ajuda uma ou mais tarefas concluídas.

  -   **Controlador**: Uma atualização de software de controladores.

 **Fornecedor**: Especifique um fornecedor para a atualização. Pode utilizar na lista pendente para utilizar valores de atualizações que estão no repositório. Quando especificar um fornecedor, o assistente cria uma pasta com esse nome de fornecedor em **todas as atualizações de Software** no **área de trabalho atualizações** se nessa pasta já não existe. Seguem-se os nomes de Windows Server Update Services (WSUS) reservada que não podem ser introduzidos para atualizações de que criar:
 -   Microsoft Corporation
 -   Microsoft
 -   Atualização
 -   Atualização de software
 -   Ferramentas
 -   Ferramenta
 -   Crítico
 -   Atualizações críticas
 -   Segurança
 -   Atualizações de segurança
 -   Pacote de funcionalidades
 -   Coletânea de atualizações
 -   Service Pack
 -   Controlador
 -   Atualização do controlador
 -   Pacote de
 -   Atualização do pacote  <br /><br />

 **Produto**: Especifique o tipo de produto que se aplica a atualização. Pode utilizar na lista pendente para utilizar valores de atualizações que estão no repositório. A mesma lista de WSUS reservados nomes que não podem ser utilizados para **fornecedor**, não pode ser utilizado para **produto**.

 **Mais informações URL**: Especifique o URL onde pode encontrar mais informações sobre esta atualização. Tem de utilizar letras minúsculas para **https** ou **http** ao introduzir este URL.

1.  No **informações opcionais** página, pode configurar detalhes que fornecem informações adicionais sobre a atualização.

    -   **ID do boletim**: ID do boletim por norma, mas nem sempre, fornecidas por fornecedores de atualização.

    -   **ID de artigo**: Se um artigo de atualização de software estiver disponível, o ID do artigo pode ser útil para os indivíduos para procurar informações adicionais sobre a atualização.

    -   **IDs de CVE:** Apresentam um ou mais vulnerabilidades comuns e os identificadores de Exposures (CVE) que fornecem informações de segurança sobre a atualização ou atualizar o pacote. Quando uma lista mais do que um, utilize um ponto e vírgula para separar os CVEs tal como neste exemplo: *CVE1; CVE2.*

    -   **URL de suporte:** Lista de URL que contém informações de suporte para esta atualização, se disponível. Tem de utilizar letras minúsculas para **https** ou **http** ao introduzir este URL.

    -   **Gravidade:** Defina o nível de gravidade para esta atualização.

    -   **Impacto:** As seguintes opções podem ser utilizadas para especificar o impacto:
        -   **Normal –** Utilize esta opção para indicar a atualização necessita de procedimentos de instalação típicas.
        -   **Secundárias –** Utilize esta opção para indicar a atualização necessita de procedimentos de instalação de um mínimo de informações.
        -   **Requer processamento exclusivo –** Utilize esta opção para indicar a atualização tem de estar instalada por si só, exclusivo a partir de quaisquer outras atualizações.   <br /><br />

    -   **Comportamento de reinício:** Utilize esta opção para fornecer informações sobre o comportamento de reinício de atualizações. Esta definição não afeta o comportamento real da instalação de atualização.

        -   **Nunca é reiniciada**: O computador nunca efetua um reinício do sistema depois de instalar a atualização de software.
        -   **Sempre requer o reinício**: O computador efetua sempre um reinício do sistema depois de instalar a atualização de software.
        -   **Pode pedir reinício**: Depois de instalar a atualização de software, o computador de pedidos de um reinício do sistema apenas se for necessário um reinício. O utilizador tem a opção de adiar o reinício. Este é o valor predefinido. <br /><br />

2.  No **pré-requisitos** página, especifique os pré-requisitos que tem de estar instalados num computador antes de pode instalar esta atualização. As regras são denominadas **detectoids**. Detectoids são regras de alto nível, como uma que requer que os computadores da CPU para um processador de 64 bits. Detectoids pode também especificar atualizações específicas que tem de estar instaladas antes de pode instalar esta atualização.

    -   Para um melhor desempenho, utilize detectoids em vez de criar *instalável* e *instalado regras* que efetuar a verificação mesma ou ação.

 Utilize a opção de pesquisa para **atualizações de software disponíveis e detectoids** para o ajudar a localizar detectoids específico. Por exemplo, uma procura **CPU** para localizar o detectoids que lhe permitem limitar a instalação com base na arquitetura de CPU específica.

 Pode selecionar um ou mais detectoids em simultâneo para adicionar como um pré-requisito. Ao adicionar pré-requisitos, os detectoids selecionados são adicionados como um ou mais grupos. Para se qualificar para a instalação, um computador tem de satisfazer o requisito de pelo menos um membro de cada grupo que configurar:

 -   Quando clica em **adicionar pré-requisitos** detectoids todos os que selecionou são adicionados a grupos de individuais, separado,. Para se qualificar para esta atualização, um computador tem de satisfazer os pré-requisitos neste grupo e passar requisitos para todos os grupos adicionais que estão configurados.

 -   Quando clica em **adicionar grupo,** detectoids todos os que selecionou são adicionados a um único grupo. Para se qualificar para esta atualização, um computador tem de cumprir, pelo menos, um dos pré-requisitos neste grupo e passar requisitos para todos os grupos adicionais que estão configurados.

1.  No **substituição** página, especifique as atualizações que são substituídas (substituídas) por esta atualização. Quando esta atualização é publicada, Configuration Manager irá marcar a cada atualização quais foi substituída como **expiradas**. Os clientes, em seguida, irão instalar esta atualização em vez das atualizações substituídas.

2.  No **aplicabilidade** página utilizar os **Editor de regra** para definir um conjunto de regras que determinam se um dispositivo tem desta atualização. (Esta página é semelhante a **instalada** página, que se segue-la.)

    Para adicionar uma nova regra, clique em ![Nova regra](media/newrule.png). Este procedimento abre a página de regra de aplicabilidade onde poderá configurar regras.

    Os tipos de regras que pode criar incluem:

    -   **Ficheiro** – Utilize esta regra para realizar um dispositivo tem de ter um ficheiro com propriedades que correspondam a um ou mais critérios especificados por si antes desta atualização podem ser aplicados.

    -   **Registo –** Utilize este tipo para especificar os detalhes de registo que tem de existir antes de um dispositivo está qualificada para instalar esta atualização.

    -   **Sistema –** esta regra utiliza detalhes de sistema para determinar a aplicabilidade. Pode escolher entre definir uma versão do Windows, um idioma do Windows, a arquitetura do processador ou especificar uma consulta WMI para identificar o sistema operativo de dispositivos.

    -   **Windows Installer –** utilizar este tipo de regra para determinar a aplicabilidade com base num instalado. MSI ou do Windows Installer patch (. MSP). Pode também determinar se específico componentes ou funcionalidades são instaladas como parte do requisito.

        > [!IMPORTANT]  
        > No geridos deices, o Windows Update Agent não consegue detetar Windows instalar pacotes que são instalados por utilizador. Quando utiliza este tipo de regra, configure as regras de aplicabilidade adicionais, como versões de ficheiro ou valores de chave de registo, para que o pacote Windows Installer pode ser detetado corretamente independentemente numa base por utilizador ou por sistema.

    -   **Regra – guardada** esta opção permite-lhe encontrar e utiliza as regras *criado na área de trabalho de regras*.

        Depois de criar uma regra, pode utilizar os outros ícones para modificar a regra, e se existirem várias regras, para definir relações entre essas regras.

 Quando tiver concluído a criar e adicionar regras, clique em **OK** no **criar regra definir** caixa de diálogo para guardar o conjunto. Em seguida, pode criar um **novo** e adicionar também o conjunto de regra.

 Quando tiver várias regras ou define a regra para adicionar a uma atualização, pode utilizar os operadores lógicos no **Editor regra** para determinar as condições entre as regras e ordem pela qual serem processados.

1.  No **instalada** página utilizar os **Editor de regra para** definir um conjunto de regras que determinam se um dispositivo já instalou a atualização estiver a configurar. (Esta página é semelhante a **aplicabilidade** página, que continua esta página.)

    Esta página do assistente suporta regras de configuração com as mesmas opções e critérios como o **aplicabilidade** página.

Quando o assistente ser concluído, a nova atualização é adicionada a um nó no **área de trabalho atualiza** que é identificada pelo **fornecedor** nome utilizado para essa atualização.

## <a name="use-the-create-bundle-wizard"></a>Utilize o assistente criar pacote
Uma vez que este assistente utiliza o mesmo fluxo de trabalho como o [assistente criar atualizar](#use-the-create-update-wizard), utilizar esse fluxo de trabalho, mas tenha em atenção a diferença seguinte para os pacotes:

1.  Para iniciar o assistente, na consola do aceda a **área de trabalho atualizações**e, em seguida, selecione **pacote** a partir de **base** separador do Friso.

2.  Ao contrário do Assistente de atualização de criar, não existe nenhuma página do pacote ao criar um pacote.

3.  No **informações** página, especifique os detalhes sobre o pacote de atualização que estão incluídos quando a atualização é publicada ou exportada.

4.  No **informações opcionais** página, pode configurar detalhes que fornecem informações adicionais sobre o pacote de atualização. As opções disponíveis são os mesmos idêntica à criação de uma atualização. No entanto, as opções para o impacto e reinicie o comportamento não estão disponíveis à medida que não se aplicam ao tamanho dos pacotes.

5.  No **pré-requisitos** página, especifique os pré-requisitos que tem de estar instalados num computador antes de pode instalar este pacote. Estas regras são os mesmos conforme se verificava para atualizações individuais.

6.  No **substituição** página, especifique as atualizações que são substituídas (substituídas) por este pacote de atualização. Estas regras são os mesmos conforme se verificava para atualizações individuais.

7.  No **membros** página, selecionar as atualizações para adicionar para o pacote de atualização. Estão disponíveis apenas atualizações que tiver criado ou importados para o Updates Publisher.

Quando o assistente ser concluído, é adicionado o novo pacote de atualização para um nó no **área de trabalho atualiza** que é identificada pelo **fornecedor** nome utilizado para o pacote de atualização.

