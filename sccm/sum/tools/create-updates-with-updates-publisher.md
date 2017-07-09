---
title: "Criar atualizações | Microsoft Docs"
description: "Criar e incluir atualizações de software com o System Center Updates Publisher"
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
ms.sourcegitcommit: c8717925dba42451b1e241a7c2f59e43896d7d99
ms.openlocfilehash: 98e490d7f5ca17dcf2a0aaa848f14e789f214123
ms.contentlocale: pt-pt
ms.lasthandoff: 06/19/2017

---
# <a name="create--software-updates-and-update-bundles-with-updates-publisher"></a>Criar as atualizações de software e pacotes de atualização com o Updates Publisher

*Aplica-se a: System Center Updates Publisher*

Com o Updates Publisher, você pode usar o **criar atualizar** Assistente para criar suas próprias atualizações e o **criar pacote** Assistente para criar pacotes de atualizações.

Como esses dois assistentes têm um fluxo de trabalho semelhante, o procedimento para criar um pacote de atualização refere-se o procedimento para criar atualizações, com apenas as diferenças relevantes detalhadas.

## <a name="use-the-create-update-wizard"></a>Use o Assistente para criar atualizações
1.  No console, vá para **espaço de trabalho atualizações**e, em seguida, no **Introdução** painel, escolha **atualização** do **início** guia da faixa de opções. Isso abre o **criar atualizar** assistente.

2.  Sobre o **pacote** página, use as informações a seguir para ajudá-lo a configurar a atualização:

    -   Escolha **procurar** para localizar o pacote de atualização de software que você usará como uma origem de pacote. Incluem fontes válidos. MSI. MSP, ou. Arquivos EXE. O Updates Publisher requer acesso ao arquivo para criar um hash de arquivo. O nome de arquivo e de hash são usados nos metadados da atualização para a atualização que você está criando.

    -   Especifique o local de origem do conteúdo desta atualização. Normalmente, esse é o local onde os binários de atualização serão baixados do durante a publicação de um servidor do WSUS.  Se o **usar um local de origem para publicar o conteúdo de atualização de software** opção é selecionada, o caminho não é necessário.

        Posteriormente, quando a atualização for publicada em um servidor WSUS, o Updates Publisher baixa os binários da atualização no local de origem indicado.  Se nenhum caminho for fornecido, então atualizar Publisher pesquisará o [caminho do local de origem de publicação](/sccm/sum/tools/updates-publisher-options#advanced) para os binários de atualização.

    -   Especifique o **idioma binário** da atualização de software.

    -   Especifique **códigos de retorno de êxito**, e **êxito pendentes reinicializar códigos** para a atualização. Separe vários códigos de retorno usando uma vírgula. Você pode usar códigos de retorno para determinar quando a instalação da atualização foi bem-sucedida e quando reinicialização foi necessária.

        -   Patches e arquivos do Windows installer (. MSI e. Arquivos MSP) automaticamente definir esses valores, e eles não podem ser modificados.

        -   Para. EXE atualizações, os códigos padrão definidos pelo. Arquivo EXE são usados se nenhum código de retorno for especificado.

    -   Especifique quaisquer argumentos de linha de comando que são necessárias para instalar a atualização de software.

        -   Patches e arquivos do Windows installer (. MSI e. Arquivos MSP) automaticamente definir esses valores. Para esses tipos de arquivos os argumentos devem ser especificados como  **\[nome\]=\[valor\]**. Além disso, todas as opções que iniciam com uma  **/**  (como **/qn**) não são suportadas. MSI ou. Atualizações de software do MSP.

        -   Para. Atualizações EXE, todos os argumentos são válidos.

3.  Sobre o **informações** página, especifique os detalhes sobre a atualização que são incluídos quando a atualização é publicada ou exportada. Os detalhes incluem propriedades localizadas, como o nome de atualizações (título) e a descrição. Em seguida, você especifica detalhes mais gerais, como a classificação, fornecedor, produto e onde aprender mais sobre a atualização.

     __Propriedades localizadas:__

    -   **Idioma**: Selecione um idioma e, em seguida, especifique um título e uma descrição. Você pode selecionar idiomas adicionais, uma vez, com cada idioma com suporte a seu próprio título e descrição.

    -   **Título**: Digite o nome da atualização. Esse nome é exibido no espaço de trabalho atualizações do console do Updates Publisher.

    -   **Descrição**: Uma descrição amigável da atualização. Você pode incluir a atualização instala e motivo ou quando ele deve ser usado.

     **Classificação:** A seguir estão as descrições comuns para as classificações diferentes.

    -   **Atualização**: Uma atualização para um aplicativo ou arquivo que está atualmente instalado.

    -   **Crítico**: Uma atualização lançada em larga escala para um problema específico que aborda um bug crítico não relacionado à segurança.

    -   **Pacote de recursos**: Novos recursos do produto que são distribuídos fora de uma versão do produto e normalmente são incluídos na próxima versão completa do produto.

    -   **Segurança**: Uma atualização lançada em larga escala para um problema de produto específico que está relacionado à segurança.

    -   **Pacote cumulativo de**: Um conjunto cumulativo de hotfixes que são reunidos para facilitar a implantação. Estas correções podem incluir atualizações de segurança, atualizações críticas, atualizações e assim sucessivamente. Um pacote cumulativo de atualizações geralmente aborda uma área específica, como segurança ou um recurso do produto.

    -   **Service Pack**: Um conjunto cumulativo de hotfixes que são aplicados a um aplicativo. Estas correções podem incluir atualizações de segurança, atualizações críticas, atualizações de software e assim sucessivamente.

    -   **Ferramenta**: Especifica uma ferramenta ou um recurso que ajuda a concluir uma ou mais tarefas.

     -   **Driver**: Uma atualização de software de driver.

    **Fornecedor:** Especifica um fornecedor para a atualização. Você pode usar a lista suspensa para usar valores de atualizações que estão no repositório. Quando você especificar um fornecedor, o assistente cria uma pasta com esse nome de fornecedor em **todas as atualizações de Software** no **espaço de trabalho atualizações** se essa pasta ainda não existir. Estes são os nomes do Windows Server Update Services (WSUS) reservados que não podem ser inseridos para atualizações que você criar:
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
 >*   Feature Pack
 >*   Pacote cumulativo de atualização
 >*   Service Pack
 >*   Controlador
 >*   Atualização do driver
 >*   Pacote
 >*   Atualização do pacote

**Produto**: Especifique o tipo de produto para a atualização. Você pode usar a lista suspensa para usar valores de atualizações que estão no repositório. A mesma lista de WSUS reservado nomes que não podem ser usados para **fornecedor**, não pode ser usado para **produto**.

 **URL para informações mais**: Especifique a URL onde você pode encontrar mais informações sobre essa atualização. Você deve usar letras minúsculas para **https** ou **http** quando você insere esta URL.

4.  Sobre o **informações opcionais** página, você pode configurar detalhes que fornecem informações adicionais sobre a atualização.

    -   **ID do boletim**: Boletim IDs são geralmente, mas não sempre, fornecidos pelos fornecedores de atualização.

    -   **ID do artigo**: Se um artigo de atualização de software está disponível, a ID do artigo pode ser útil para os indivíduos que buscam informações adicionais sobre a atualização.

    -   **IDs CVE:** Lista um ou mais comuns de vulnerabilidades e identificadores de exposições CVE () que fornecem informações sobre a atualização de segurança ou atualizar o pacote. Ao listar mais de uma, use um ponto e vírgula para separar os CVEs como neste exemplo: *CVE1; CVE2.*

    -   **URL de suporte:** Lista a URL que contém informações de suporte para esta atualização, se disponível. Você deve usar letras minúsculas para **https** ou **http** quando você insere esta URL.

    -   **Severidade:** Defina o nível de severidade para esta atualização.

    -   **Impacto:** As opções a seguir podem ser usadas para especificar o impacto:
        -   **Normal –** Use isso para indicar que a atualização requer que os procedimentos de instalação típica.
        -   **Pequenas –** Use isso para indicar que a atualização requer que os procedimentos de instalação mínima.
        -   **Requer manipulação exclusiva –** Use isso para indicar que a atualização deve ser instalada por si só, exclusivos de outras atualizações.   <br /><br />

    -   **Comportamento de reinicialização:** Use isso para fornecer informações sobre o comportamento de reinicialização de atualizações. Essa configuração não afeta o comportamento real de instalação da atualização.

        -   **Nunca reinicia**: O computador nunca realiza uma reinicialização do sistema após a instalação da atualização de software.
        -   **Sempre exige reinicialização**: O computador sempre executa uma reinicialização do sistema após a instalação da atualização de software.
        -   **Pode solicitar reinicialização**: Depois de instalar a atualização de software, o computador solicita uma reinicialização do sistema somente se uma reinicialização é necessária. O usuário tem a opção de adiar a reinicialização. Este é o valor predefinido. <br /><br />

5.  No **pré-requisito** , especifique os pré-requisitos que devem ser instalados em um computador para que possa instalar esta atualização. Pré-requisitos podem ser **detectoids** ou outras atualizações. Detectoids são regras de alto nível como o que exige que os computadores da CPU para ser um processador de 64 bits. Detectoids também pode especificar atualizações específicas que devem ser instaladas antes que possa instalar esta atualização.

    -   Para obter melhor desempenho, use detectoids em vez de criar *instalável* e *instalado regras* que executam a mesma verificação ou a ação.

    Use a opção de pesquisa para **atualizações de software disponíveis e detectoids** para ajudá-lo a localizar atualizações específicas ou detectoids. Por exemplo, pesquise em **CPU** para localizar o detectoids que permitem que você limite a instalação com base na arquitetura de CPU específica.

    Você pode selecionar um ou mais itens em um tempo para adicionar como um pré-requisito. Ao adicionar os pré-requisitos, os detectoids selecionados são adicionados como um ou mais grupos. Para se qualificar para a instalação, um computador deve atender ao requisito de pelo menos um membro de cada grupo que você configurar:

 -   Quando você clica em **adicionar pré-requisito** todos os itens que você selecionou são adicionados aos grupos de individuais, separada. Para se qualificar para essa atualização, um computador deve atender aos pré-requisitos neste grupo e passar nos requisitos de todos os grupos adicionais que são configurados.

 -   Quando você clica em **adicionar grupo** todos os itens que você selecionou são adicionados a um único grupo. Para se qualificar para essa atualização, um computador deve atender a pelo menos um dos pré-requisitos neste grupo e passar nos requisitos de todos os grupos adicionais que são configurados.

6.  Sobre o **substituição** página, especifique as atualizações substituídas (substituídas) por essa atualização. Quando essa atualização é publicada, o Configuration Manager irá marcar cada atualização que é substituída como **expirado**. Os clientes, em seguida, instalar essa atualização em vez de atualizações substituídas.

7.  No **aplicabilidade** página use o **Editor de regras** para definir um conjunto de regras que determinam se um dispositivo precisa desta atualização. (Essa página é semelhante do **instalado** página, que o segue.)

    Para adicionar uma nova regra, clique em ![Nova regra](media/newrule.png). Isso abre a página de regra de aplicabilidade onde você pode configurar regras.

    Tipos de regras que você pode criar:

    -   **Arquivo** – Use essa regra para exigir que um dispositivo tem um arquivo com propriedades que atendam a um ou mais critérios que você especificar antes desta atualização podem ser aplicados.

    -   **Registro –** usar este tipo para especificar detalhes do registro que devem estar presentes antes de um dispositivo se qualifica instalar essa atualização.

    -   **Sistema –** esta regra usa o detalhes do sistema para determinar a aplicabilidade. Você pode escolher entre a definição de uma versão do Windows, uma linguagem do Windows, a arquitetura do processador, ou especificar uma consulta WMI para identificar o sistema operacional de dispositivos.

    -   **Windows Installer –** Use esse tipo de regra para determinar a aplicabilidade com base em um instalado. MSI ou o Windows Installer patch (. MSP). Você também pode determinar se os componentes específicos ou recursos são instalados como parte do requisito.

        > [!IMPORTANT]  
        > Gerenciado por deices, o Windows Update Agent não pode detectar o Windows instale os pacotes que são instalados por usuário. Quando você usa esse tipo de regra, configure regras de aplicabilidade adicionais, como versões de arquivos ou valores de chave do registro, para que o pacote do Windows Installer pode ser detectado corretamente, independentemente de uma base por usuário ou por sistema.

    -   **Salvar regra –** essa opção permite que você localizar e usa regras você *criado no espaço de trabalho regras*.

        Depois de criar uma regra, você pode usar os outros ícones para modificar a regra, e se há várias regras para definir relações entre essas regras.

    Quando você estiver criando concluído e adição de regras, clique em **Okey** no **criar conjunto de regras** caixa de diálogo para salvar esse conjunto. Você pode criar um **novo** regra e o adicione ao conjunto também.

    Quando você tiver várias regras ou conjuntos de regras para adicionar a uma atualização, você pode usar os operadores lógicos no **Editor de regras** para determinar as condições entre as regras e a ordem na qual eles processem.

8.  No **instalado** página use o **Editor de regra para** definir um conjunto de regras que determinam se um dispositivo já tiver instalado a atualização que você está configurando. (Essa página é semelhante do **aplicabilidade** página, que continua a esta página.)

    Esta página do assistente oferece suporte a regras de configuração com as mesmas opções e critérios como o **aplicabilidade** página.

    Quando o assistente for concluído, a nova atualização é adicionada a um nó no **atualiza o espaço de trabalho** que é identificado pelo **fornecedor** e **produto** nome usado para essa atualização.

## <a name="use-the-create-bundle-wizard"></a>Use o assistente Criar pacote
Porque o assistente usa o mesmo fluxo de trabalho como o [assistente criar atualizar](#use-the-create-update-wizard), use o fluxo de trabalho, mas observe a diferença de seguir para pacotes:

1.  Para iniciar o assistente, no console, vá para **espaço de trabalho atualizações**e, em seguida, selecione **pacote** do **início** guia da faixa de opções.

2.  Diferentemente do Assistente de atualização de criar, não há nenhuma página de pacote ao criar um pacote.

3.  Sobre o **informações** página, especifique os detalhes sobre o pacote de atualização que são incluídos quando a atualização é publicada ou exportada.

4.  Sobre o **informações opcionais** página, você pode configurar detalhes que fornecem informações adicionais sobre o pacote de atualização. As opções disponíveis são as mesmas que para a criação de uma atualização. No entanto, opções de impacto e o comportamento de reinicialização não estão disponíveis como eles não são aplicadas aos pacotes.

5.  No **pré-requisito** , especifique os pré-requisitos que devem ser instalados em um computador para que possa instalar este pacote. Essas regras são o mesmo visto para as atualizações individuais.

6.  Sobre o **substituição** página, especifique as atualizações substituídas (substituídas) por este pacote de atualização. Essas regras são o mesmo visto para as atualizações individuais.

7.  Sobre o **membros** página, você seleciona as atualizações para adicionar ao pacote de atualização. Somente as atualizações que você criou ou importados para o Updates Publisher estão disponíveis.

Quando o assistente for concluído, o novo pacote de atualização é adicionado a um nó no **atualiza o espaço de trabalho** que é identificado pelo **fornecedor** nome usado para o pacote de atualização.

