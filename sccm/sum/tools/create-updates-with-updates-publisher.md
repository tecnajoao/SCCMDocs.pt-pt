---
title: Criar atualizações
titleSuffix: Configuration Manager
description: Criar e agrupar as atualizações de software com o System Center Updates Publisher
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 46a1a8ac-126c-4ee6-ae09-32dfbdb83368
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4f98e06bac3f396ab9dad29c95861cd225c1d6ec
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/24/2019
ms.locfileid: "54898414"
---
# <a name="create--software-updates-and-update-bundles-with-updates-publisher"></a>Criar atualizações de software e pacotes de atualizações com o Updates Publisher

*Aplica-se a: System Center Updates Publisher*

Com o Updates Publisher pode utilizar o **criar atualizar** Assistente para criar suas próprias atualizações e o **criar pacote** Assistente para criar pacotes de atualizações.

Como esses dois assistentes têm um fluxo de trabalho semelhante, o procedimento para criar um pacote de atualização refere-se para o procedimento para criar atualizações, com apenas as diferenças relevantes detalhadas.

## <a name="use-the-create-update-wizard"></a>Utilize o Assistente de atualização de criar
1. Na consola, aceda a **área de trabalho de atualizações**e, em seguida, no **introdução** painel, escolha **atualização** do **home page** separador do Friso. Esta ação abre o **criar atualizar** assistente.

2. Sobre o **pacote** página, utilize as seguintes informações para ajudar a configurar a atualização:

   -   Escolher **procurar** para localizar o pacote de atualização de software irá utilizar como uma origem de pacote. Incluem origens válidas .MSI. .MSP, ou. Ficheiros .EXE. Publicador de atualizações requer acesso ao ficheiro para criar um hash de ficheiro. O nome de ficheiro e hash, em seguida, são utilizados nos metadados de atualização para a atualização que está a criar.

   -   Especifique a localização de origem do conteúdo para esta atualização. Normalmente, isso é o local onde o binário de atualização será transferido da durante a publicação para um servidor WSUS.  Se o **Use uma fonte de local para publicar conteúdo de atualização de software** opção for selecionada, em seguida, o caminho não é necessário.

       Mais tarde, quando a atualização é publicada para um servidor WSUS, o Updates Publisher transfere os binários da atualização na localização de origem indicado.  Se nenhum caminho for fornecido, em seguida, atualizar o publicador irá procurar o [caminho de origem local de publicação](/sccm/sum/tools/updates-publisher-options#advanced) para o binário de atualização.

   -   Especifique a **linguagem binária** da atualização de software.

   -   Especifique **códigos de retorno de êxito**, e **êxito, pendente de reinício códigos** para a atualização. Separe vários códigos de retorno com uma vírgula. Pode utilizar códigos de retorno para determinar quando a instalação da atualização foi concluída com êxito e, quando reinicializações eram necessárias.

       -   Ficheiros do Windows installer e patches (.MSI e. Ficheiros de .MSP) definido automaticamente estes valores e que não podem ser modificados.

       -   Para. EXE de atualizações, os códigos de padrão definidos pela. Arquivo EXE são utilizados se forem especificados não códigos de retorno.

   -   Especifique os argumentos da linha de comandos que são necessários para instalar a atualização de software.

       -   Ficheiros do Windows installer e patches (.MSI e. Ficheiros de .MSP) são definidas automaticamente estes valores. Para estes tipos de ficheiros os argumentos devem ser especificados como  **\[name\]=\[valor\]**. Além disso, todas as opções que começar a utilizar um **/** (como **/qn**) não são suportadas .MSI ou. Atualizações de software .MSP.

       -   Para. Atualizações do EXE, todos os argumentos são válidos.

3. Sobre o **informações** página, especifique os detalhes sobre a atualização que estão incluídos, quando a atualização é publicada ou exportada. Os detalhes incluem propriedades localizadas, como o nome de atualizações (título) e a descrição. Em seguida, especifique os detalhes mais gerais, como a classificação, fornecedor, produto e onde saber mais sobre a atualização.

    __Propriedades localizadas:__

   - **Idioma**: Selecione um idioma e, em seguida, especifique um título e descrição. Em seguida, pode selecionar idiomas adicionais, um de cada vez, com cada idioma com suporte a seu próprio título e descrição.

   - **Título**: Introduza o nome da atualização. Este nome é exibido na área de trabalho atualizações da consola do Updates Publisher.

   - **Descrição**: Uma descrição amigável da atualização. Pode incluir o que instala a atualização e, por que motivo ou quando deve ser utilizado.

     **Classificação:** Seguem-se descrições comuns para as classificações diferentes.

   - **Atualização**: Uma atualização para uma aplicação ou ficheiro que está atualmente instalado.

   - **Crítico**: Uma atualização amplamente lançada para um problema específico que corrige um erro crítico não relacionado com segurança.

   - **Pacote de funcionalidades**: Novas funcionalidades do produto que são distribuídas fora de uma versão de produto e que normalmente estão incluídas na próxima versão completa do produto.

   - **Segurança**: Uma atualização amplamente lançada para um problema específico do produto que está relacionado à segurança.

   - **Pacote cumulativo de atualizações**: Um conjunto cumulativo de correções que são agrupadas para facilitar a implementação. Estas correções podem incluir atualizações de segurança, atualizações críticas, atualizações e assim sucessivamente. Um pacote cumulativo de atualizações resolve geralmente uma área específica, tal como segurança ou uma funcionalidade do produto.

   - **Service Pack**: Um conjunto cumulativo de correções que são aplicadas a uma aplicação. Estas correções podem incluir atualizações de segurança, atualizações críticas, atualizações de software e assim sucessivamente.

   - **Ferramenta**: Especifica uma ferramenta ou funcionalidade que ajuda a concluir tarefas de um ou mais.

     -   **Driver**: Uma atualização de software de driver.

   **Fornecedor:** Especifique um fornecedor para a atualização. Pode utilizar a lista suspensa para utilizar os valores de atualizações que estão no repositório. Quando especificar um fornecedor, o assistente cria uma pasta com esse nome de fornecedor sob **todas as atualizações de Software** no **área de trabalho atualizações** se nessa pasta ainda não existir. Seguem-se os nomes do Windows Server Update Services (WSUS) reservado que não não possível inserir a existência de atualizações que cria:
   >*   Microsoft Corporation
   >*   Microsoft
   >*   Atualizar
   >*   Atualização de software
   >*   Ferramentas
   >*   Ferramenta
   >*   Crítico
   >*   Atualizações críticas
   >*   Segurança
   >*   Atualizações de segurança
   >*   Pacote de funcionalidades
   >*   Pacote cumulativo de atualizações
   >*   Service Pack
   >*   Controlador
   >*   Atualização do controlador
   >*   Pacote
   >*   Atualização do pacote

**Produto**: Especifique o tipo de produto que se aplica a atualização. Pode utilizar a lista suspensa para utilizar os valores de atualizações que estão no repositório. A mesma lista de WSUS reservado nomes que não podem ser utilizados para **fornecedor**, não pode ser utilizado para **produto**.

 **URL de informações mais**: Especifique o URL em que pode encontrar mais informações sobre esta atualização. Tem de utilizar minúsculas para **https** ou **http** quando introduzir este URL.

4. Sobre o **informações opcionais** página, pode configurar detalhes que fornecem informações adicionais sobre a atualização.

   -   **ID do boletim**: IDs de boletim são, normalmente, mas nem sempre, fornecidos por fornecedores de atualização.

   -   **ID do artigo**: Se estiver disponível um artigo de atualização de software, o ID do artigo podem ser úteis para pessoas que procuram informações adicionais sobre a atualização.

   -   **IDs CVE:** Liste um ou mais vulnerabilidades mais comuns e os identificadores de exposições CVE () que fornecem informações de segurança sobre a atualização ou atualizar o pacote. Quando lista mais do que um, utilize um ponto e vírgula para separar as relacionadas, tal como neste exemplo: *CVE1;CVE2.*

   -   **URL de suporte:** Liste o URL que contém informações de suporte para esta atualização, se disponível. Tem de utilizar minúsculas para **https** ou **http** quando introduzir este URL.

   -   **Gravidade:** Defina o nível de gravidade para esta atualização.

   -   **Impacto:** As seguintes opções podem ser utilizadas para especificar o impacto:
       -   **Normal –** utilizá-lo para indicar a atualização requer procedimentos de instalação típico.
       -   **Pequenas –** utilizá-lo para indicar a atualização requer procedimentos de instalação mínima.
       -   **Requer processamento exclusivo –** utilizá-lo para indicar a atualização tem de ser instalada por si só, exclusivo de todas as atualizações.   <br /><br />

   -   **Comportamento de reinício:** Utilize esta opção para fornecer informações sobre o comportamento de reinício de atualizações. Esta definição não afeta o comportamento real da instalação da atualização.

       -   **Nunca reinicia**: O computador nunca efetua um reinício do sistema depois de instalar a atualização de software.
       -   **Sempre exige reinicialização**: O computador efetua sempre um reinício do sistema depois de instalar a atualização de software.
       -   **Pode pedir a reinicialização**: Depois de instalar a atualização de software, o computador solicita um reinício do sistema apenas se for necessário um reinício. O utilizador tem a opção para adiar o reinício. Este é o valor predefinido. <br /><br />

5. Sobre o **pré-requisitos** , especifique os pré-requisitos que devem ser instalados num computador antes desta atualização pode instalar. Pré-requisitos podem ser **detectoids** ou outras atualizações. Detectoids são regras de alto nível, como um que exija os computadores da CPU para ser um processador de 64 bits. Detectoids também pode especificar as atualizações específicas que devem ser instaladas antes desta atualização pode instalar.

   -   Para um melhor desempenho, utilize detectoids em vez de criar *instalável* e *instalado regras* que executam a mesma verificação ou a ação.

   Utilize a opção de pesquisa **atualizações de software disponíveis e detectoids** para ajudar a encontrar atualizações específicas ou detectoids. Por exemplo, uma procura **CPU** para localizar o detectoids que permitem que limite instalação com base na arquitetura de CPU específica.

   Pode selecionar um ou mais itens em simultâneo para adicionar como um pré-requisito. Ao adicionar a pré-requisitos, os detectoids selecionados são adicionados como um ou mais grupos. Para se qualificar para a instalação, um computador tem de cumprir o requisito pelo menos um membro de cada grupo que configurar:

   -   Quando clica em **adicionar pré-requisitos** todos os itens que selecionou são adicionados a grupos individuais, de separado,. Para se qualificar para esta atualização, um computador tem de cumprir o pré-requisito neste grupo e transmitir os requisitos para todos os grupos adicionais que estão configurados.

   -   Quando clica em **adicionar grupo,** todos os itens que selecionou são adicionados a um único grupo. Para se qualificar para esta atualização, um computador tem de cumprir, pelo menos, um dos pré-requisitos neste grupo e transmitir os requisitos para todos os grupos adicionais que estão configurados.

6. Sobre o **substituição** , especifique as atualizações que são substituídas (substituídas) por esta atualização. Quando esta atualização é publicada, o Configuration Manager irá marcar cada atualização que é substituída como **expirado**. Os clientes, em seguida, irão instalar esta atualização em vez das atualizações substituídas.

7. Sobre o **aplicabilidade** página utilização a **Editor de regras de** para definir um conjunto de regras que determinam se um dispositivo precisa desta atualização. (Esta página é semelhante para o **instalada** página, o que o sucede.)

   Para adicionar uma nova regra, clique em ![Nova regra](media/newrule.png). Esta ação abre a página de regra de aplicabilidade, onde pode configurar regras.

   Os tipos de regras, que pode criar incluem:

   -   **Ficheiro** – utilizar esta regra para exigir que um dispositivo tiver um ficheiro com propriedades corresponderem a uma ou mais critérios que especificar antes desta atualização podem ser aplicados.

   -   **Registo –** usar esse tipo para especificar os detalhes de registo que tem de estar presentes antes de um dispositivo é elegível instalar esta atualização.

   -   **Sistema –** esta regra utiliza detalhes de sistema para determinar a aplicabilidade. Pode escolher entre definir uma versão do Windows, um idioma do Windows, a arquitetura do processador, ou especificar uma consulta WMI para identificar o sistema operativo de dispositivos.

   -   **Windows Installer –** utilizar este tipo de regra para determinar a aplicabilidade com base num instalado. MSI ou do Windows Installer patch (.MSP). Também pode determinar se os componentes específicos ou funcionalidades são instaladas como parte do requisito.

       > [!IMPORTANT]  
       > Em dispositivos geridos, o Windows Update Agent não consegue detetar pacotes de instalação do Windows de mensagens em fila que são instalados por utilizador. Quando utiliza este tipo de regra, configure regras de aplicabilidade adicionais, como versões de ficheiro ou valores de chave de registo, para que o pacote do Windows Installer pode ser detectado corretamente independentemente numa base por usuário ou por sistema.

   -   **Regra – guardada** esta permite opção encontrar e utilizar as regras que *criada na área de trabalho regras*.

       Depois de criar uma regra, pode utilizar os outros ícones para modificar a regra, e se existirem várias regras, definir relações entre essas regras.

   Quando estiver terminando a criação e adicionar regras, clique em **OK** no **criar conjunto de regras de** caixa de diálogo para guardar o conjunto. Em seguida, pode criar uma **New** da regra e adicioná-la para o conjunto também.

   Quando tem várias regras ou define a regra para adicionar a uma atualização, pode utilizar os operadores lógicos no **Editor de regras de** para determinar as condições entre as regras e a ordem pela qual processam.

8. Na **instalada** página utilização a **Editor de regras para** definir um conjunto de regras que determinam se um dispositivo já tem instalada a atualização está a configurar. (Esta página é semelhante para o **aplicabilidade** página, o que continua esta página.)

   Esta página do assistente suporta regras de configuração com as mesmas opções e critérios como o **aplicabilidade** página.

   Quando o assistente terminar, a nova atualização é adicionada a um nó a **atualiza a área de trabalho** que é identificado pela **fornecedor** e **produto** nome que utilizou para essa atualização.

## <a name="use-the-create-bundle-wizard"></a>Utilize o assistente criar pacote
Uma vez que este assistente utiliza o mesmo fluxo de trabalho como o [Assistente de atualização de criar](#use-the-create-update-wizard), utilizar esse fluxo de trabalho, mas tenha em atenção a diferença seguinte para pacotes:

1.  Para iniciar o assistente, na consola do aceda a **área de trabalho de atualizações**e, em seguida, selecione **pacote** partir o **home page** separador do Friso.

2.  Ao contrário do Assistente de atualização de criar, não existe nenhuma página de pacote durante a criação de um pacote.

3.  Sobre o **informações** , especifique os detalhes sobre o pacote de atualização que estão incluídos, quando a atualização é publicada ou exportada.

4.  Sobre o **informações opcionais** página, pode configurar detalhes que fornecem informações adicionais sobre o pacote de atualização. As opções disponíveis são as mesmas usadas para a criação de uma atualização. No entanto, as opções de impacto e o comportamento de reinício não estão disponíveis à medida que eles não são aplicáveis a pacotes.

5.  Sobre o **pré-requisitos** , especifique os pré-requisitos que devem ser instalados num computador antes de pode instalar este pacote. Estas regras são os mesmos conforme se verifica para as atualizações individuais.

6.  Sobre o **substituição** , especifique as atualizações que são substituídas (substituídas) por este pacote de atualização. Estas regras são os mesmos conforme se verifica para as atualizações individuais.

7.  Sobre o **membros** página, selecionar as atualizações para adicionar o pacote de atualização. Estão disponíveis apenas atualizações tiver criado ou importado para o Updates Publisher.

Quando o assistente terminar, o novo pacote de atualização é adicionado a um nó a **atualiza a área de trabalho** que é identificado pela **fornecedor** nome que utilizou para o pacote de atualização.
