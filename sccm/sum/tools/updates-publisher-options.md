---
title: "Configurar opções | Documentos do Microsoft"
description: "Configurar opções para utilizar o System Center Updates Publisher"
ms.custom: na
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4e620080-5400-45bb-87c2-fbdbc8aeacac
caps.latest.revision: 1
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: NOINDEX, NOFOLLOW
ms.translationtype: Machine Translation
ms.sourcegitcommit: 31819a1df4e63e1114682490a9b3c3b4e5c99cfa
ms.openlocfilehash: b66ed0a5e1c87d8c82853da86e3d55b0e2c043bb
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="configure-options-for-updates-publisher"></a>Configurar opções para o Updates Publisher

*Aplica-se a: System Center Updates Publisher*

Reveja e configure as opções e definições relacionadas que afetam o funcionamento do Updates Publisher.

Para aceder às opções de Updates Publisher, no canto superior esquerdo da consola, clique no **Updates Publisher** **propriedades** separador e, em seguida, selecione **opções**.

![Opções](media/properties1.png)   


As opções são divididas em da seguinte forma:

-   Servidor de atualização
-   Servidor do ConfigMgr
-   Definições de proxy
-   Fabricantes fidedignos
-   Avançadas
-   Atualizações
-   Registo

## <a name="update-server"></a>Servidor de atualização
Tem de configurar o Updates Publisher para funcionar com o servidor de atualização como Windows Server Update Services (WSUS) antes de a pode [publicar atualizações](/sccm/sum/tools/manage-updates-with-updates-publisher#publish-updates-and-bundles). Isto inclui a especificação do servidor, métodos para ligar a este servidor quando for remoto a partir da consola e um certificado a utilizar para assinar digitalmente as atualizações publicar.

-   **Configurar um servidor de atualização**. Quando configurar um servidor de atualização, selecione o servidor WSUS (servidor de atualização) nível superior na sua hierarquia do Configuration Manager para que todos os sites subordinados têm acesso para as atualizações que publicar.

  Se o servidor de atualização estiver remoto a partir do seu servidor do publicador de atualizações, especifique o nome de domínio completamente qualificado (FQDN) do servidor, e se ligarão por SSL. Quando se liga ao SSL, a porta predefinida é muda de 8530 para 8531. Certifique-se de que a porta definiu corresponde ao que está em utilização pelo seu servidor de atualização.

    > [!TIP]  
    > Se não configurar um servidor de atualização, pode utilizar o Updates Publisher para a criação de atualizações de software.

-   **Configurar o certificado de assinatura**. Tem de configurar e ligar com êxito para um servidor de atualização antes de poder configurar o certificado de assinatura.

    Updates Publisher utiliza o certificado de assinatura para assinar as atualizações de software que são publicadas no servidor de atualização. Publicação falha se o certificado digital não está disponível no arquivo de certificados do servidor de atualização ou o computador que executa o publicador de atualizações.

    Para obter mais informações sobre como adicionar o certificado ao arquivo de certificados, consulte o artigo [certificados e segurança para o Updates Publisher](/sccm/sum/tools/updates-publisher-security).

    Se um certificado digital não é detetado automaticamente para o servidor de atualização, escolha um dos seguintes procedimentos:

    -   **Procurar**: Procurar apenas está disponível quando o servidor de atualização está instalado no servidor onde é executada a consola. Depois de selecionar um certificado, tem de escolher **criar** para adicionar esse certificado ao arquivo de certificados do WSUS no servidor de atualização. Tem de introduzir o **. pfx** ficheiro palavra-passe de certificados que selecionar através deste método.

    -   **Crie:** Utilize esta opção para criar um novo certificado. Esta ação adiciona também o certificado do arquivo de certificados do WSUS no servidor de atualização.

    **Se criar o seu próprio certificado de assinatura**, configure as seguintes opções:

    -   Ativar o **permitir que a chave privada seja exportada** opção.

    -   Definir **utilização de chave** para assinatura digital.

    -   Definir **tamanho de chave mínimo** para um valor igual ou superior a 2048 bits.

    Utilize o **remover** opção para remover um certificado a partir do arquivo de certificados do WSUS. Esta opção está disponível quando o servidor de atualização é local na consola do publicador de atualizações de que utiliza, ou quando utilizou **SSL** para ligar a um servidor de atualização remoto.

## <a name="configmgr-server"></a>Servidor do ConfigMgr
Utilize estas opções ao utilizar o Configuration Manager com o Updates Publisher.

-   **Especifique o servidor do Configuration Manager:** Depois de ativar o suporte do Configuration Manager, especifique a localização do servidor do site de nível superior da hierarquia do Configuration Manager. Se esse servidor for remoto relativamente a instalação do Updates Publisher, especifique o FQDN do servidor do site. Escolher **Testar ligação** para se certificar de que pode ligar ao servidor do site.

-   **Configure limiares:** Limiares são utilizados durante a publicação de atualizações com um tipo de publicação de automático. Os valores de limiar ajudam a determinar quando o conteúdo completo para uma atualização é publicado em vez de apenas os metadados. Para saber mais tipos de publicação, consulte o artigo [atribuir atualizações a uma publicação](/sccm/sum/tools/manage-updates-with-updates-publisher#assign-updates-and-bundles-to-a-publication)

    É possível um ou ambos os limiares do seguinte:

    -   **Pediu o limiar de contagem de cliente:** Isto define o número de clientes tem de solicitar uma atualização antes de publicador de atualizações automaticamente pode publicar o conjunto completo de conteúdo para que o update. Até que o número especificado de clientes pedir a atualização, são publicado apenas os metadados de atualizações.

    -   **Limiar de tamanho de origem de pacote (MB):** Isto impede a publicação automática das atualizações que excedem o tamanho que especificar. Se o tamanho de atualizações excede este valor, apenas os metadados são publicado. Atualizações que são menores do que o tamanho especificado pode ter o respetivo conteúdo completo publicado.

## <a name="proxy-settings"></a>Definições de proxy
Updates Publisher utiliza as definições de proxy quando importa catálogos de software a partir da Internet ou publicar atualizações à Internet.

-   Especifique o FQDN ou endereço IP de um servidor proxy. São suportados IPv4 e IPv6.

-   Se o servidor proxy autentica utilizadores para acesso à Internet, tem de especificar o nome do Windows. Um nome de princípio universal (UPN) não é suportado.

## <a name="trusted-publishers"></a>Fabricantes fidedignos
Quando importa um catálogo de atualização, a origem de que o catálogo (com base no respetivo certificado), é adicionado como um fabricante fidedigno. Da mesma forma, quando publica uma atualização, a origem do certificado atualizações é adicionada como um fabricante fidedigno.

Pode ver detalhes do certificado para cada publicador e remover um fabricante da lista de fabricantes fidedignos.

Conteúdo a partir de fabricantes que não são fidedignos potencialmente pode danificar computadores cliente quando o cliente analisa a existência de atualizações. Deve aceitar conteúdo apenas a partir de fabricantes que confia.

## <a name="advanced"></a>Avançadas
Opções avançadas incluem o seguinte:

-   **Localização de repositório:** Ver e modificar a localização do ficheiro da base de dados, **scupdb**. Este ficheiro é o repositório para o Updates Publisher.

-   **Carimbo:** Quando ativada, uma timestamp é adicionado à atualizações que terminar a sessão que identifique quando estava assinado. Uma atualização que foi assinada enquanto estava um certificado válido pode ser utilizada depois de expira esse certificado de assinatura. Por predefinição, as atualizações de software não podem ser implementadas depois de expira o respetivo certificado de assinatura.

-   **Verifique se existem atualizações para catálogos subscritos:** Sempre que inicia o Updates Publisher,-possa procurar automaticamente atualizações para catálogos subscreveu. Quando é encontrada uma atualização do catálogo, detalhes são fornecidos como **alertas recentes** no **descrição geral** janela do **área de trabalho atualiza**.

-   **Revogação de certificados:** Escolha esta opção para ativar verificações de revogação de certificado.

-   **Publicação de origem local:** Updates Publisher pode utilizar uma cópia local de uma atualização a publicar antes da transferência essa atualização a partir da Internet. A localização tem de ser uma pasta no computador que executa o Updates Publisher. Por predefinição, esta localização é **Documents\LocalSourcePublishing meu.** Utilize esta opção quando tiverem sido transferidas anteriormente uma ou mais atualizações ou efetuadas modificações para uma atualização que pretende implementar.

-   **Assistente de limpeza de atualizações de software:** Inicie o Assistente de limpeza de atualizações. O assistente expira atualizações que estão no servidor de atualização, mas não no repositório Updates Publisher. Consulte o artigo [expirar as atualizações não referenciadas](#expire-unreferenced-software-updates) para obter mais detalhes.

## <a name="updates"></a>Atualizações
 Publicador de atualizações automaticamente pode verificar novas atualizações sempre que é aberta. Também pode optar por para receber compilações de pré-visualização do Updates Publisher.

Para manualmente Verifique se existem atualizações, na consola do Updates Publisher clique na ![propriedades](media/properties2.png)  
Para abrir o **atualizações Publisher propriedades**e, em seguida, escolha **verificar a existência de update**.

Depois do Updates Publisher localiza uma nova atualização, é apresentado o **atualizar disponíveis** janela e, em seguida, pode escolher para instalá-lo. Se optar por não instalar a atualização, é-lhe dada a próxima vez que abrir a consola.

## <a name="logging"></a>Registo
Informações básicas sobre o Updates Publisher para os registos de Updates Publisher  **&lt;* caminho*&gt;\Windows\Temp\UpdatesPublisher.log**.

Bloco de notas de utilização ou **CMTrace** para ver o registo. CMTrace é a ferramenta de ficheiro de registo do Configuration Manager e pode ser encontrado no **\SMSSetup\Tools** pasta do suporte de dados de origem do Configuration Manager.

Pode alterar o tamanho do registo e respetivo nível de detalhe.

Quando ativar o registo da base de dados, são incluídas informações sobre as consultas que são executadas na base de dados do Updates Publisher. Utilização do registo da base de dados pode levar a redução de desempenho do computador Updates Publisher.

Para ver o ficheiro de registo, na consola do clique em ![propriedades](media/properties2.png) para abrir o **atualizações Publisher propriedades**e, em seguida, escolha **ficheiro de registo de vista**.

## <a name="expire-unreferenced-software-updates"></a>Expirar atualizações de software não referenciadas
Pode executar o **Assistente de limpeza de atualização de Software** para expirar as atualizações que estão no seu servidor de atualização, mas não no repositório Updates Publisher. Isto notifica o Gestor de configuração que, em seguida, remove as atualizações de todas as implementações futuras.

Não é possível reverter o ato de expirar uma atualização. Execute esta tarefa apenas quando tiver a certeza de que as atualizações de software que selecionou já não são exigidas pela sua organização.

### <a name="to-remove-expired-software-updates"></a>Para remover as atualizações de software expiradas
1.  Na consola do Updates Publisher, clique no ![propriedades](media/properties2.png) para abrir o **atualizações Publisher propriedades**e, em seguida, escolha **opções**.

2.  Escolher **avançadas**e, em seguida, em **assistente limpar de atualização de Software,** escolher **iniciar**.

3.  Selecione as atualizações de software que pretende expire e, em seguida, escolha **seguinte**.

4.  Depois de rever as suas seleções, escolheu **seguinte** para aceite as seleções e expirar essas atualizações.

5.  Depois de concluído o assistente, escolher **fechar** para concluir o assistente.

