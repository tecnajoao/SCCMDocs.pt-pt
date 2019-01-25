---
title: Configurar opções
titleSuffix: Configuration Manager
description: Configurar opções para usar o System Center Updates Publisher
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 4e620080-5400-45bb-87c2-fbdbc8aeacac
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7f86a871355a48774a25ae8759065b6a02d0feac
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/24/2019
ms.locfileid: "54898261"
---
# <a name="configure-options-for-updates-publisher"></a>Configurar opções para o Updates Publisher

*Aplica-se a: System Center Updates Publisher*

Reveja e configure as opções e definições relacionadas que afetam o funcionamento do Updates Publisher.

Para aceder às opções Updates Publisher, no canto superior esquerdo da consola, clique nas **Updates Publisher** **propriedades** separador e, em seguida, escolha **opções**.

![Opções](media/properties1.png)   


As opções são divididas no seguinte:

-   Servidor de atualização
-   Servidor do ConfigMgr
-   Definições de proxy
-   Fublicadores fidedignos
-   Avançadas
-   Atualizações
-   Registo

## <a name="update-server"></a>Servidor de atualização
Tem de configurar o Updates Publisher para trabalhar com o servidor de atualização, como o Windows Server Update Services (WSUS) antes de poder [publicar atualizações](/sccm/sum/tools/manage-updates-with-updates-publisher#publish-updates-and-bundles). Isto inclui a especificação do servidor, publicar de métodos para ligar a esse servidor quando for remoto a partir da consola e atualizações de um certificado a utilizar para assinar digitalmente.

- **Configurar um servidor de atualização**. Quando configurar um servidor de atualização, selecione o servidor de nível superior de WSUS (servidor de atualização) na sua hierarquia do Configuration Manager para que todos os sites subordinados têm acesso para as atualizações que publicar.

  Se o seu servidor de atualização é remoto a partir do seu servidor do Updates Publisher, especifique o nome de domínio completamente qualificado (FQDN) do servidor, e se irá se conectar por SSL. Quando se conectar por SSL, a porta predefinida é alterado de 8530 para 8531. Certifique-se de que a porta que definiu corresponde ao que está em utilização pelo seu servidor de atualização.

  > [!TIP]  
  > Se não configurar um servidor de atualização, pode utilizar o Updates Publisher para criar atualizações de software.

- **Configurar o certificado de assinatura**. Tem de configurar e ligar com êxito para um servidor de atualização antes de poder configurar o certificado de assinatura.

  Publicador de atualizações utiliza o certificado de assinatura para assinar as atualizações de software que são publicadas para o servidor de atualização. Publicação falha se o certificado digital não está disponível no arquivo de certificados de servidor de atualização ou o computador que executa o Updates Publisher.

  Para obter mais informações sobre como adicionar o certificado ao arquivo de certificados, consulte [certificados e segurança para o Updates Publisher](/sccm/sum/tools/updates-publisher-security).

  Se um certificado digital não é detetado automaticamente para o servidor de atualização, escolha um dos seguintes:

  -   **Procurar**: Procurar só está disponível quando o servidor de atualização está instalado no servidor onde executa a consola. Depois de selecionar um certificado tem de escolher **criar** para adicionar esse certificado para o arquivo de certificados do WSUS no servidor de atualização. Tem de introduzir o **. pfx** palavra-passe de ficheiros de certificados que selecionar através deste método.

  -   **Crie:** Utilize esta opção para criar um novo certificado. Isso também adiciona o certificado para o arquivo de certificados do WSUS no servidor de atualização.

  **Se criar seu próprio certificado de assinatura**, configure o seguinte:

  -   Ativar a **permitir que a chave privada seja exportada** opção.

  -   Definir **utilização de chave** para assinatura digital.

  -   Definir **tamanho mínimo da chave** para um valor igual ou superior a 2048 bits.

  Utilize o **remover** opção para remover um certificado do arquivo de certificados WSUS. Esta opção está disponível quando o servidor de atualização é local para a consola do Updates Publisher que utilizar, ou quando utilizou **SSL** para ligar a um servidor de atualização remota.

## <a name="configmgr-server"></a>Servidor do ConfigMgr
Utilize estas opções quando utilizar o Configuration Manager com o Updates Publisher.

-   **Especifique o servidor do Configuration Manager:** Depois de ativar o suporte para o Configuration Manager, especifique a localização do servidor do site de nível superior da hierarquia do Configuration Manager. Se esse servidor remoto a partir da instalação do Updates Publisher, especifique o FQDN do servidor do site. Escolher **Testar ligação** para garantir que pode ligar ao servidor do site.

-   **Configure limiares:** Limiares são utilizados quando publica atualizações com um tipo de publicação de automático. Os valores de limiar ajudam a determinar quando o conteúdo completo para uma atualização é publicado em vez de apenas os metadados. Para saber mais tipos de publicação, veja [atribuir atualizações para uma publicação](/sccm/sum/tools/manage-updates-with-updates-publisher#assign-updates-and-bundles-to-a-publication)

    É possível um ou ambos dos seguintes limiares:

    -   **Pediu o limiar de contagem de cliente:** Isso define o número de clientes tem de solicitar uma atualização antes do Updates Publisher, pode publicar automaticamente o conjunto completo de conteúdo para essa atualização. Até que o número especificado de clientes pedir a atualização, apenas os metadados de atualizações é publicado.

    -   **Limite de tamanho de origem de pacote (MB):** Isto impede que a publicação automática de atualizações que excedem o tamanho especificado. Se o tamanho de atualizações excede este valor, apenas os metadados é publicado. Atualizações que estão a menores do que o tamanho especificado pode ter seu conteúdo completo publicado.

## <a name="proxy-settings"></a>Definições de proxy
Publicador de atualizações utiliza as definições de proxy quando importar catálogos de software a partir da Internet ou publicar atualizações à Internet.

-   Especifique o FQDN ou endereço IP de um servidor proxy. São suportados IPv4 e IPv6.

-   Se o servidor proxy autentica utilizadores para acesso à Internet, tem de especificar o nome do Windows. Um nome de principal (UPN) não é suportado.

## <a name="trusted-publishers"></a>Fublicadores fidedignos
Quando importa um catálogo de atualização, a origem desse catálogo (com base no seu certificado), é adicionado como um fabricante fidedigno. Da mesma forma, quando publica uma atualização, a origem do certificado de atualizações é adicionada como um fabricante fidedigno.

Pode ver os detalhes do certificado para cada editor e remover um publicador da lista de publicadores fidedignos.

Conteúdos de editores que não são fidedignos podem danificar computadores cliente quando o cliente verifica a existência de atualizações. Deve aceitar conteúdo apenas a partir de editores que confia.

## <a name="advanced"></a>Avançadas
Opções avançadas incluem o seguinte:

-   **Localização do repositório:** Ver e modificar a localização do ficheiro da base de dados, **scupdb**. Este ficheiro é o repositório para o Updates Publisher.

-   **Timestamp:** Quando ativada, um carimbo é adicionado às atualizações de que o início de sessão que identifica quando ele foi assinado. Pode ser utilizada uma atualização que foi assinada enquanto um certificado era válido após esse certificado de assinatura expira. Por predefinição, as atualizações de software não não possível implementar depois do certificado de assinatura expira.

-   **Verifique se existem atualizações para catálogos subscritos:** Sempre que for iniciado o Updates Publisher, ele pode automaticamente procurar atualizações para catálogos qual se inscreveu. Quando é encontrada uma atualização de catálogo, os detalhes são fornecidos como **alertas recentes** no **descrição geral** janela do **atualiza a área de trabalho**.

-   **Revogação de certificados:** Escolha esta opção para ativar as verificações de revogação de certificado.

-   **Publicação de local de origem:** Publicador de atualizações pode usar uma cópia local de uma atualização que está a publicar antes de transferir a atualização a partir da Internet. A localização tem de ser uma pasta no computador que executa o Updates Publisher. Por predefinição, esta localização é **My Documents\LocalSourcePublishing.** Utilize esta opção quando tenha transferido uma ou mais atualizações ou efetuadas modificações para uma atualização que pretende implementar.

-   **Assistente de limpeza de atualizações de software:** Inicie o Assistente de limpeza de atualizações. O assistente expira as atualizações que estão no servidor de atualização, mas não no repositório do Updates Publisher. Ver [expirar atualizações não referenciadas](#expire-unreferenced-software-updates) para obter mais detalhes.

## <a name="updates"></a>Atualizações
 Publicador de atualizações automaticamente pode verificar novas atualizações sempre que é aberto. Pode também optam por receber compilações de pré-visualização do Updates Publisher.

Para procurar atualizações, na consola do Updates Publisher clicar manualmente no ![propriedades](media/properties2.png)  
Para abrir o **atualiza as propriedades de publicador**e, em seguida, escolha **verificar a existência de update**.

Depois do Updates Publisher encontra uma nova atualização, ele exibe a **Update Available** janela e, em seguida, pode optar por instalá-lo. Se optar por não instalar a atualização, é oferecido na próxima vez que abrir a consola.

## <a name="logging"></a>Registo
Informações básicas sobre o Updates Publisher para registos do Updates Publisher  **&lt; *caminho*&gt;\Windows\Temp\UpdatesPublisher.log**.

Bloco de notas de utilização ou **CMTrace** para ver o registo. CMTrace é a ferramenta de ficheiro de registo do Configuration Manager e pode ser encontrado na **\SMSSetup\Tools** pasta do suporte de dados de origem do Configuration Manager.

Pode alterar o tamanho do registo e seu nível de detalhe.

Quando ativar o registo de base de dados, informações sobre as consultas que são executadas para a base de dados do Updates Publisher, são incluídos. Utilização do registo de base de dados pode levar a queda de desempenho do computador Updates Publisher.

Para ver o ficheiro de registo, na consola do clique em ![propriedades](media/properties2.png) para abrir o **atualiza as propriedades de publicador**e, em seguida, escolha **ficheiro de registo do modo de exibição**.

## <a name="expire-unreferenced-software-updates"></a>Atualizações de software sem referência de expirar
Pode executar o **Assistente de limpeza de atualização de Software** para expirar as atualizações que estão no seu servidor de atualização, mas não no repositório do Updates Publisher. Isso notifica o Gestor de configuração que, em seguida, remove as atualizações de todas as implementações futuras.

O ato de prestes a expirar uma atualização não pode ser revertido. Execute esta tarefa apenas quando tiver a certeza de que as atualizações de software que selecionou já não são exigidas pela sua organização.

### <a name="to-remove-expired-software-updates"></a>Para remover as atualizações de software expiradas
1.  Na consola do Updates Publisher, clique em ![propriedades](media/properties2.png) para abrir o **atualiza as propriedades de publicador**e, em seguida, escolha **opções**.

2.  Escolher **avançadas**e, em **assistente limpa de atualização de Software,** escolher **iniciar**.

3.  Selecione as atualizações de software que pretende expire e, em seguida, escolha **seguinte**.

4.  Depois de rever as suas seleções, escolheu **seguinte** aceite as seleções e expirar essas atualizações.

5.  Depois de concluído o assistente, escolha **fechar** para concluir o assistente.
