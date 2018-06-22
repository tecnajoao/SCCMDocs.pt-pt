---
title: Configurar opções
titleSuffix: Configuration Manager
description: Configurar opções para utilizar o System Center Updates Publisher
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 4e620080-5400-45bb-87c2-fbdbc8aeacac
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: NOINDEX, NOFOLLOW
ms.openlocfilehash: 497ff025dafcdb135e466a18f2f6661ca0f21a00
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32349971"
---
# <a name="configure-options-for-updates-publisher"></a>Configurar opções para o Updates Publisher

*Aplica-se a: O System Center Updates Publisher*

Reveja e configure as opções e definições relacionadas que afetem o funcionamento do Updates Publisher.

Para aceder às opções de Updates Publisher, no canto superior esquerdo da consola, clique em de **Updates Publisher** **propriedades** separador e, em seguida, escolha **opções**.

![Opções](media/properties1.png)   


As opções são divididas no seguinte:

-   Servidor de atualização
-   Servidor do ConfigMgr
-   Definições de proxy
-   Fabricantes fidedignos
-   Avançadas
-   Atualizações
-   Registo

## <a name="update-server"></a>Servidor de atualização
Tem de configurar o Updates Publisher para trabalhar com o servidor de atualização como o Windows Server Update Services (WSUS) para que possa [publicar atualizações](/sccm/sum/tools/manage-updates-with-updates-publisher#publish-updates-and-bundles). Isto inclui a especificação do servidor, métodos para ligar a este servidor quando for remoto a partir da consola e um certificado a utilizar para assinar digitalmente as atualizações publicar.

-   **Configurar um servidor de atualização**. Quando configura um servidor de atualização, selecione o servidor de nível superior de WSUS (servidor de atualização) na sua hierarquia do Configuration Manager para que todos os sites subordinados têm acesso às atualizações de publicar.

  Se o servidor de atualização remoto a partir do seu servidor do Updates Publisher, especifique o nome de domínio completamente qualificado (FQDN) do servidor, e se irá ligar-se por SSL. Quando se liga por SSL, a porta predefinida é alterado de 8530 para 8531. Certifique-se de que a porta que configurou corresponde ao que está em utilização pelo seu servidor de atualização.

    > [!TIP]  
    > Se não configurar um servidor de atualização, pode utilizar o Updates Publisher para criar as atualizações de software.

-   **Configurar o certificado de assinatura**. Tem de configurar e ligar com êxito para um servidor de atualização antes de poder configurar o certificado de assinatura.

    Publicador de atualizações utiliza o certificado de assinatura para assinar as atualizações de software que são publicadas para o servidor de atualização. Publicação falha se o certificado digital não está disponível no arquivo de certificados do servidor de atualização ou o computador que executa o Updates Publisher.

    Para obter mais informações sobre como adicionar o certificado ao arquivo de certificados, consulte [certificados e segurança para o Updates Publisher](/sccm/sum/tools/updates-publisher-security).

    Se um certificado digital não será detetado automaticamente para o servidor de atualização, escolha um dos seguintes:

    -   **Procurar**: Procurar só está disponível quando o servidor de atualização está instalado no servidor onde executa a consola. Depois de selecionar um certificado tem de escolher **criar** para adicionar esse certificado para o arquivo de certificados do WSUS no servidor de atualização. Tem de introduzir o **. pfx** ficheiro palavra-passe de certificados que selecionar através deste método.

    -   **Crie:** Utilize esta opção para criar um novo certificado. Isto também adiciona o certificado para o arquivo de certificados do WSUS no servidor de atualização.

    **Se criar o seu próprio certificado de assinatura**, configure o seguinte:

    -   Ativar o **permitir que a chave privada seja exportada** opção.

    -   Definir **utilização de chave** para assinatura digital.

    -   Definir **tamanho de chave mínimo** para um valor igual ou superior a 2048 bits.

    Utilize o **remover** opção para remover um certificado do arquivo de certificados WSUS. Esta opção está disponível quando o servidor de atualização é local para a consola do Updates Publisher que utiliza, ou quando utilizou **SSL** para ligar a um servidor de atualização remota.

## <a name="configmgr-server"></a>Servidor do ConfigMgr
Utilize estas opções quando utilizar o Configuration Manager com o Updates Publisher.

-   **Especifique o servidor do Configuration Manager:** Depois de ativar o suporte para o Configuration Manager, especifique a localização do servidor do site de nível superior da hierarquia do Configuration Manager. Se esse servidor é remoto relativamente a instalação do Updates Publisher, especifique o FQDN do servidor do site. Escolha **Testar ligação** para garantir que pode ligar ao servidor do site.

-   **Configure limiares:** Os limiares são utilizados quando publicar atualizações com um tipo de publicação de automático. Os valores de limiar ajudam a determinar quando o conteúdo completo para uma atualização for publicado em vez de apenas os metadados. Para saber mais tipos de publicação, consulte [atribuir atualizações para uma publicação](/sccm/sum/tools/manage-updates-with-updates-publisher#assign-updates-and-bundles-to-a-publication)

    É possível um ou ambos dos seguintes limiares:

    -   **Limiar de contagem de clientes de pedido:** Isto define quantos clientes tem de solicitar uma atualização antes do Updates Publisher pode publicar automaticamente o conjunto completo de conteúdo para essa atualização. Até que o número especificado de clientes pedir a atualização, apenas os metadados de atualizações é publicado.

    -   **Limiar de tamanho de origem de pacote (MB):** Isto impede que a publicação automática de atualizações que excedem o tamanho que especificar. Se o tamanho de atualizações excede este valor, apenas os metadados é publicado. Atualizações que estão menores do que o tamanho especificado pode ter o respetivo conteúdo completo publicado.

## <a name="proxy-settings"></a>Definições de proxy
Publicador de atualizações utiliza as definições de proxy quando importar catálogos de software a partir da Internet ou publicar atualizações à Internet.

-   Especifique o FQDN ou endereço IP de um servidor proxy. São suportados IPv4 e IPv6.

-   Se o servidor proxy autentica utilizadores para acesso à Internet, tem de especificar o nome do Windows. Não é suportado um nome de princípio universal (UPN).

## <a name="trusted-publishers"></a>Fabricantes fidedignos
Quando importa um catálogo de atualização, a origem do catálogo de (com base no respetivo certificado), é adicionado como um fabricante fidedigno. Da mesma forma, quando publica uma atualização, a origem do certificado de atualizações é adicionada como um fabricante fidedigno.

Pode ver detalhes do certificado para cada fabricante e remover um fabricante da lista de fabricantes fidedignos.

Conteúdo de fabricantes que não são fidedignas potencialmente pode danificar os computadores cliente quando o cliente verifica a existência de atualizações. Deve aceitar conteúdo só de fabricantes que considera fidedignos.

## <a name="advanced"></a>Avançadas
Opções avançadas incluem o seguinte:

-   **Localização de repositório:** Ver e modificar a localização do ficheiro da base de dados, **scupdb.sdf**. Este ficheiro é o repositório para o Updates Publisher.

-   **Timestamp:** Quando ativada, um timestamp é adicionado à atualizações inicia a sessão que identifica quando estava assinado. Pode ser utilizada uma atualização que foi assinada durante um certificado válido depois desse certificado de assinatura expira. Por predefinição, não não possível implementar atualizações de software depois do respetivo certificado de assinatura expira.

-   **Verificar se existem atualizações para catálogos subscritos:** Sempre que inicia o Updates Publisher,-lo pode procurar automaticamente atualizações para catálogos que tem subscritos. Quando é encontrada uma atualização de catálogo, os detalhes são fornecidos como **alertas recentes** no **descrição geral** janela do **atualiza a área de trabalho**.

-   **Revogação de certificados:** Escolha esta opção para ativar verificações de revogação de certificado.

-   **Publicação de local de origem:** Publicador de atualizações, pode utilizar uma cópia local de uma atualização que está a publicar antes da transferência dessa atualização através da Internet. A localização tem de ser uma pasta no computador que executa o Updates Publisher. Por predefinição, esta localização é **My Documents\LocalSourcePublishing.** Utilize esta opção quando tiver transferido anteriormente uma ou mais atualizações ou foram efetuadas modificações para uma atualização que pretende implementar.

-   **Assistente de limpeza de atualizações de software:** Inicie o Assistente de limpeza de atualizações. O assistente expira as atualizações que estão no servidor de atualização, mas não no repositório de Updates Publisher. Consulte [expirar atualizações não referenciadas](#expire-unreferenced-software-updates) para obter mais detalhes.

## <a name="updates"></a>Atualizações
 Publicador de atualizações automaticamente pode verificar novas atualizações sempre que é aberta. Também pode escolher para receber compilações de pré-visualização do Updates Publisher.

Para manualmente procurar atualizações, na consola do Updates Publisher clique no ![propriedades](media/properties2.png)  
Para abrir o **propriedades do publicador de atualizações**e, em seguida, escolha **Verifique a existência de update**.

Depois do Updates Publisher localiza uma nova atualização, é apresentado o **atualizar disponíveis** janela e, em seguida, pode optar por instalá-lo. Se optar por não instalar a atualização, é-lhe oferecida da próxima vez que abrir a consola.

## <a name="logging"></a>Registo
Publicador de atualizações regista informações básicas sobre o Updates Publisher para  **&lt; *caminho*&gt;\Windows\Temp\UpdatesPublisher.log**.

Bloco de notas de utilização ou **CMTrace** para ver o registo. CMTrace é a ferramenta de ficheiro de registo do Configuration Manager e pode ser encontrado no **\SMSSetup\Tools** pasta do suporte de dados de origem do Configuration Manager.

Pode alterar o tamanho do registo e o respetivo nível de detalhe.

Quando ativar a base de dados de registo, informações sobre as consultas que são executadas na base de dados do Updates Publisher, são incluídos. Utilização do registo da base de dados pode levar a um desempenho do computador Updates Publisher.

Para ver o ficheiro de registo, na consola do clique em ![propriedades](media/properties2.png) para abrir o **propriedades do publicador de atualizações**e, em seguida, escolha **ficheiro de registo de vista**.

## <a name="expire-unreferenced-software-updates"></a>As atualizações de software não referenciadas de expirar
Pode executar o **Assistente de limpeza de atualização de Software** expirar as atualizações que estão no seu servidor de atualização, mas não no repositório de Updates Publisher. Isto notifica o Gestor de configuração que, em seguida, remove as atualizações de todas as implementações futuras.

Não é possível reverter o ato de expirar uma atualização. Só deverá efetue esta tarefa quando tem a certeza de que as atualizações de software que selecionou já não são necessárias pela sua organização.

### <a name="to-remove-expired-software-updates"></a>Para remover as atualizações de software expiradas
1.  Na consola do Updates Publisher, clique em ![propriedades](media/properties2.png) para abrir o **propriedades do publicador de atualizações**e, em seguida, escolha **opções**.

2.  Escolha **avançadas**e, em **assistente limpa de atualização de Software,** escolha **iniciar**.

3.  Selecione as atualizações de software que pretende expire e, em seguida, escolha **seguinte**.

4.  Depois de rever as suas seleções, escolheu **seguinte** aceite as seleções e expirar essas atualizações.

5.  Depois de concluído o assistente, selecione **fechar** para concluir o assistente.
