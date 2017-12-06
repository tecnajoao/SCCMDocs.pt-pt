---
title: Importar dados para o Microsoft Intune
titleSuffix: Configuration Manager
description: 
keywords: 
author: dougeby
manager: dougeby
ms.date: 12/05/2017
ms.topic: article
ms.prod: configmgr-hybrid
ms.service: 
ms.technology: 
ms.assetid: b552391d-abc0-48a2-a429-93605a13a66a
ms.openlocfilehash: d42a5fd64b5baead8ef87d8c08a99ec659f94633
ms.sourcegitcommit: 8c6e9355846ff6a73c534c079e3cdae09cf13c45
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/06/2017
---
# <a name="import-configuration-manager-data-to-microsoft-intune"></a>Importar dados do Configuration Manager para o Microsoft Intune 

*Aplica-se a: O System Center Configuration Manager (ramo atual)*    

A primeira fase recomendada no processo de para [migrar utilizadores MDM híbrida e dispositivos ao Intune autónomo](migrate-hybridmdm-to-intunesa.md) na configuração apenas na nuvem está a utilizar a ferramenta do importador de dados do Intune. Se quiser, pode ignorar esta fase e mover para o [preparar o Intune para a migração de utilizador](migrate-prepare-intune.md) fase. No entanto, esta ferramenta efetua as seguintes funções, podem poupar muito tempo na fase de seguinte: 
1.  Recolhe dados sobre os objetos que selecionar na hierarquia do Configuration Manager. 
2.  Fornece detalhes sobre os objetos que pode selecionar para a importação e informações sobre o motivo pelo qual não não possível importar alguns objetos.
3.  Importa objetos selecionados para o inquilino do Microsoft Intune. 

A ferramenta do importador de dados não alterar o seu ambiente do Configuration Manager de qualquer forma e, por conseguinte, pode importar objetos para o Intune e validar que tudo funciona conforme esperado sem o risco de deixar os seus dispositivos MDM híbrida no Estado não gerido. 

## <a name="what-objects-can-this-tool-import"></a>Os objetos que pode importar esta ferramenta?
A ferramenta de importação pode recolher informações sobre os seguintes tipos de objeto no Configuration Manager e fornece informações sobre se os objetos recolhidos podem ser importados: 
- Itens de configuração
- Perfis de certificado
- Perfis de e-mail
- Perfis da VPN
- Perfis de Wi-Fi
- Políticas de conformidade
- Aplicações
- Implementações

> [!Note]    
> Importar implementações só é útil para outros tipos de objeto que está a importar. Por exemplo, se importar perfis VPN e implementações, só poderá importar as implementações para os perfis VPN que selecionar. Implementações no Intune são denominadas atribuições. Se pretender importar uma implementação de um objeto importado anteriormente, terá de importar esse objeto novamente ou criar manualmente a atribuição no Intune no Azure. Por exemplo, se importar perfis VPN e não implementações, terá de executar a ferramenta novamente e selecione perfis VPN e as implementações ou criar manualmente a atribuição no Intune no Azure.  Se voltar a executar a ferramenta, é possível criar objectos duplicados que pode eliminar mais tarde no Intune no Azure.  

> [!Important]    
> Se a coleção para uma implementação baseiam-se um grupo do Active Directory que foram replicado para Azure Active Directory (AAD), a ferramenta automaticamente destina-se a objetos migrados para os grupos se seleciona a implementação adequada quando executar a ferramenta. Quando tiver coleções mais complexas ou coleções de associação direta, tem de recriar manualmente no AAD e atribuições de objeto aos mesmos no Intune no Azure de destino manualmente.


## <a name="things-to-know-before-you-run-the-tool"></a>Coisas que deve saber antes de executar a ferramenta
- Executar a ferramenta não irá alterar o seu ambiente do Configuration Manager de qualquer forma.
- Recomendamos que teste primeiro o processo de importação de dados utilizando um inquilino de avaliação. Em seguida, depois de confirmar que os dados esperados tiver sido importado, pode percorrer o mesmo processo com o seu inquilino do Intune de produção.
- O importador de dados destina-se apenas importar dados do Configuration Manager uma vez. -Não manter controlar dos objetos no Configuration Manager ou o Intune. No entanto, se executar o importador de novo no mesmo computador como anteriormente,-informará os objetos que importou anteriormente. A ferramenta não saberá se o objeto ainda existe no Intune ou se um objeto foi alterada. Se importar dados para o Intune mais do que uma vez, poderá acabar com objetos duplicados.
- Nem todas as definições de perfil podem ser importadas. Por exemplo, não é possível importar o modo de local público ou definições PFX. 
- Se tiver uma política do Gestor de configuração com definições que não são aplicáveis a plataformas selecionadas, a ferramenta poderá ignorar estas definições durante a importação. A ignorar a ajuda de definições para se certificar de que a política pode ser importada e suportada pelo Intune. 
- A ferramenta irá tentar dão-lhe um motivo para o motivo pelo qual um objeto não pode ser importado. Em alguns casos, antes de importar objetos para o Intune, pode aceder novamente à consola do Configuration Manager, corrija o problema, inicie o Gestor de configuração de deteção de objetos novamente procurar e, em seguida, importar os objetos. Por vezes, poderá ter, ou poderá querer, recrie estes objetos manualmente no Intune.
- Existem algumas perfis que dependem de outros objetos. Se pretender importar um perfil que depende de outro objeto, como um perfil de e-mail que depende de um certificado, tem de importar os dois objetos em simultâneo, exceto se tiver importado anteriormente o outro objeto no mesmo computador com o mesmo utilizador.  
- Depois de executar a ferramenta, poderá ter de efetuar passos manuais adicionais. Por exemplo, filtragem de aplicações e políticas a grupos do AAD. 

## <a name="prerequisites"></a>Pré-requisitos
- Configuration Manager versão 1610 ou posterior.-é recomendável que especifica o site de nível superior e execute a ferramenta com um utilizador que tem acesso a todos os objetos na hierarquia do site. A ferramenta só Deteta objetos acessíveis ao utilizador que executa a ferramenta. 
- Um Administrador Global tem de executar a ferramenta do importador de dados pela primeira vez utilizando os seguintes ***intunedataimporter.exe - GlobalConsent*** parâmetro. Em seguida, um Administrador Global ou um administrador do Intune pode executar a ferramenta.  


<!-- ## Objects that cannot be imported
There are some Configuration Manager objects that the importer tool cannot import to Intune. You must manually create these objects in Intune. 
- Collections based on direct membership or that are based on a query. The only collections that are imported are based on a single AD group. For all other collections, you must create the assignment in Intune and add the assignment to the appropriate objects. 
- Profiles <list what we cannot import>
- Policies <??>
- Etc.
-->

## <a name="download-the-data-importer-tool"></a>Transferir a ferramenta do importador de dados
A ferramenta do importador de dados está disponível para transferência do repositório ConfigMgrTools/Intune-Data-importador no GitHub. Utilize o procedimento seguinte para transferir a ferramenta.

1. Vá para o [Intune dados importador GitHub versões](https://github.com/ConfigMgrTools/Intune-Data-Importer/releases) página.
2. Para a versão mais recente, clique em **Microsoft.Intune.Data.Importer.exe**.
3. Guarde e execute (ou basta executar) .exe e, em seguida, escolha uma pasta de destino, a extrair a ferramenta do importador de dados do Intune.

## <a name="run-the-data-importer-tool"></a>Execute a ferramenta do importador de dados
O Assistente para a ferramenta do importador de dados pode ser dividido em três passos principais. Esta secção fornece informações para ajudar a concluir cada secção do assistente e importar dados do Configuration Manager com êxito no Intune. Cada passo continua em que terminou o passo anterior.

### <a name="provide-permission-for-the-data-importer-tool-to-access-resources"></a>Fornecer permissão para a ferramenta de importador de dados para aceder a recursos
Antes de poder executar a ferramenta do importador de dados, tem de utilizar uma conta de Administrador Global para conceder a permissão de ferramenta do importador de dados no Azure para aceder aos recursos. Em seguida, pode executar a ferramenta utilizando uma conta de Administrador Global ou de administrador do Intune.   

1.  Um Administrador Global tem de executar o tempo de ferramenta primeiro utilizar o seguinte parâmetro: ***intunedataimporter.exe - GlobalConsent*** 
2. Quando inicia a ferramenta, um ecrã de início de sessão mostra onde tem de iniciar sessão com uma conta com a função de Administrador Global no Azure. 
3. Clique em **aceitar** para criar uma aplicação no Azure com os direitos adequados no Microsoft Graph. A ferramenta do importador de dados tem estes direitos para importar objetos para o Microsoft Intune.   

   > [!Important]
   > Ao clicar em **aceitar**, atribua a permissão da ferramenta fazer o seguinte:
   > - Ler todos os grupos
   > - A iniciar sessão e leia o perfil de utilizador
   > - Ler e escrever políticas e configuração de dispositivo do Intune
   > - Ler e escrever as aplicações do Intune
   > - Ler e escrever as políticas de controlo de administração baseada em função do Intune
   > - Ler e escrever os dispositivos do Intune
   > - Leitura e escrita de configuração do Intune
1. Depois de aceite consentimento, qualquer outro administrador Global ou o administrador do Intune pode executar a ferramenta para importar dados do Configuration Manager para o Intune no Azure.    
        
    > [!Note]
    > Se o consentimento primeiro não foram aceites por um Administrador Global, a ferramenta poderá apresentar **não é possível aceder a esta aplicação** depois de um administrador do Intune é executado a ferramenta do importador de dados e iniciar sessão para a subscrição do Intune.

### <a name="manually-map-collections-to-azure-ad-groups"></a>Mapear manualmente coleções a grupos do Azure AD
Quando executar a ferramenta do importador de dados, extrai o nome de grupo do AD de coleções com uma única regra destina-se um único grupo do AD. Quando as atribuições são criadas no Intune, o importador de dados de procura para um grupo do Azure AD com o mesmo nome que o grupo do AD e se existir, atribui o objeto importado a esse grupo do Azure AD. Pode substituir o nome de grupo do AD que localiza o importador de dados para uma coleção e fornecer um ou mais grupos do Azure AD a utilizar para essa coleção. Utilizar o ficheiro de mapeamento de coleção fornece uma forma de mapear coleções que não são normalmente importable com o importador de dados a grupos do Azure AD.
#### <a name="find-the-collections-that-cannot-be-imported"></a>Localizar as coleções que não podem ser importadas
Pode obter uma lista de todas as coleções que não são importable para poder adicioná-los para o ficheiro. csv de mapeamento de coleção. 
1. Execute a ferramenta do importador de dados e selecione os objetos a importar. Utilize os procedimentos no [fase 1: Detetar objetos do Configuration Manager e recolher dados](#phase-1:-discover-configuration-manager-objects-and-collect-data) e [fase 2: Resolver problemas e selecione os objetos a importar](#phase-2:-resolve-issues-and-select-the-objects-to-import) para detetar e escolha os objetos. Em seguida, no **resumo** página, escolha **exportar detalhes** para criar um ficheiro. csv com detalhes de tudo selecionados para importação, incluindo os objetos que não podem ser importados e implementações. 
2. Abra o ficheiro. csv no Microsoft Excel e filtre os dados com base no **implementação** para o **tipo** coluna e **não** para o **Importable** coluna. A coluna de nome de coleção mostra todas as coleções que precisem de ser adicionadas a um ficheiro de mapeamento de coleção para que as implementações para ser importable.

#### <a name="create-the-collection-mapping-file"></a>Criar o ficheiro de mapeamento de coleção
O ficheiro de mapeamento de coleção é um ficheiro de valores separados por vírgulas (CSV) em que a primeira coluna é o nome da coleção do Configuration Manager e a segunda coluna é o nome do grupo do Azure AD a utilizar para essa coleção. Para especificar mais do que um grupo do Azure AD para uma única coleção do Configuration Manager, crie várias linhas no ficheiro CSV com esse nome de coleção. O exemplo seguinte é um ficheiro CSV que contém duas coleções. A primeira coleção está mapeada para um único do Azure AD de grupo e a segunda coleção está mapeada para dois grupos do Azure AD.

![Exemplo de ficheiro csv de mapeamento da coleção](..\media\migrate-collectionmapping.png)

#### <a name="start-the-data-importer-tool-using-collection-mapping"></a>Iniciar a ferramenta de importador de dados com o mapeamento de coleção
Para utilizar um ficheiro de mapeamento de coleção, tem de iniciar o importador de dados utilizando a ferramenta de *- CollectionMappingFile* parâmetro da linha de comandos e o caminho completo do ficheiro. csv de coleção mapeamento que cria. Por exemplo:

```IntuneDataImporter.exe -CollectionMappingFile c:\Users\myuser\Documents\collectionmapping.csv```

> [!Note]
> O importador de dados não apresentar tudo em qualquer página do Assistente para indicar que foi carregado o ficheiro de mapeamento de coleção. No entanto, a ferramenta apresenta quaisquer erros encontrados ao ler o ficheiro. csv. Além disso, no **resumo** página do assistente, pode rever **implementação** tipos. A ferramenta apresenta **Sim** na coluna Importable e apresenta uma lista de grupos do Azure AD que irá atribuir aos objetos a **notas** coluna.

### <a name="phase-1-discover-configuration-manager-objects-and-collect-data"></a>Fase 1: Detetar objetos do Configuration Manager e recolher dados
Fase 1, selecione os objetos para detetar e ter a ferramenta de recolher informações sobre os objetos selecionados. 
1. Abrir a ferramenta e clique em **iniciar**.  
2. Ler as informações e, em seguida, clique em **seguinte**. 
3. Escolha se pretende importar um conjunto de dados exportado anteriormente ou selecione os tipos de objeto para importar:
   - **Importar exportado anteriormente o conjunto de dados**: Escolha **exportados do conjunto de dados de importação de uma execução anterior do importador de dados do Intune**e clique em **procurar** para **pasta de dados de Exported** selecionar um dados definir que anteriormente exportado com a ferramenta do importador de dados. O utilizador que importa o conjunto de dados tem de ser o mesmo utilizador que exportou os dados. Depois de importar os dados, um resumo dos objetos listados o **resumo** página do assistente. Se o resumo de procura correto, avance para o [fase 3: Objeto selecionado para importar para o Intune](phase-3:-import-selected-object-to-intune).
 
      > [!Note]
      > Depois de detetar e selecione os objetos do site para importar, pode exportar os objetos para um conjunto de dados no **início de sessão para o Intune** página do assistente. Em seguida, pode importar o conjunto de dados nesta página. O conjunto de dados é encriptado utilizando as credenciais de utilizador do Windows do utilizador com sessão iniciada, por isso, só o utilizador que exportou o conjunto de dados pode importar o conjunto de dados na ferramenta. 
   - **Selecione os tipos de objeto para importar**: Escolha **seleciona os tipos de objeto para importar** para selecionar os tipos de objeto para importar e detete objetos no seu ambiente. Forneça as seguintes informações sobre o seu site e os objetos que pretende importar.
      - **Nome do servidor de site**: Forneça o nome de domínio completamente qualificado do servidor do site para importar objetos. A ferramenta só Deteta objetos acessíveis ao utilizador que executa a ferramenta. Normalmente, irá especificar o site de nível superior e execute a ferramenta com um utilizador que tem acesso a todos os objetos na hierarquia do site.
      - **Código do site**: Forneça o código do site para o servidor do site. Pode encontrar o código de três letras no topo da consola do Configuration Manager.
      - **Para importar os tipos de objeto**: Escolha os objetos que pretende que a ferramenta para recolher. Pode escolher **Selecionar tudo** para escolher todos os objetos ou selecionar tipos de objeto individuais. 
4.  Clique em **seguinte** para iniciar a deteção de objetos no site. A ferramenta mostra o progresso para cada um dos tipos de objeto. 
    - Quando a ferramenta Deteta não existem dados para um tipo de objeto selecionado, o progresso da barra imediatamente apresenta concluída para esse tipo de objeto.
    - Objetos que não selecionou não são apresentados no **recolher** página de dados. 
    - Pode executar a ferramenta novamente para objetos que não foram recolhidos ou cancelou durante o processo de recolha.

### <a name="phase-2-resolve-issues-and-select-the-objects-to-import"></a>Fase 2: Resolver problemas e selecione os objetos a importar  
Na fase 2, reveja os objetos que localizou através da ferramenta, resolva os problemas que impedem que o objeto que está a ser importado para o Intune e selecione os objetos a importar. Se a corrigir problemas, regressar ao **detetar ambiente** página do Assistente para voltar a detetar os objetos. 
5.  Clique em **seguinte** para rever os objetos recolhidos. Página de seleção de um item está disponível para cada tipo de objeto recolhidos. 
 <!--   > [!Tip]     
    > On each item selection page, you can create a filter to help you find the objects that you want to import. However, take note of the following:
    > - When you are on an item selection page and the view is filtered, the Select all checkboxes only apply to the displayed items. Any hidden objects because of a filter are not included when using the checkboxes.
    > - Objects are always grouped under their parent item even when you sort or filter the objects.
-->
6.  Na página de seleção de cada item, ordenar os objetos pela coluna Importable e reveja os objetos que não estão importable. As informações da coluna de notas fornecem detalhes sobre o motivo pelo qual a ferramenta não é possível importar o objeto. 
7.  Agora tem de decidir se pretende corrigir quaisquer problemas de objetos não importable. Se corrigir um ou mais problemas, clique em anterior até obter selecione nos dados de página do Configuration Manager e recolher os dados novamente para ver se resolver o problema. Pode continuar a corrigir problemas até estar satisfeito com os objetos que estão importable. 
8.  Na página de seleção de cada item, selecione os objetos que pretende importar. São apresentadas as seguintes colunas:
    - **Nome**: Nome do objeto do Configuration Manager. 
    - **Importable**: Especifica se um objeto pode ser importado. Só é possível escolher objetos que têm Sim na coluna Importable. 
    - **Plataforma**: Especifica a plataforma suportada pelo objeto.
    - **Já importado**: Especifica se o objeto já foi importado utilizando a ferramenta neste computador. 
    - **Foi substituído** (para aplicações): Especifica se a aplicação é substituída por outra aplicação. Tem de verificar o **Mostrar substituídas aplicações** caixa de verificação na parte superior da página para aplicações substituídas apresentar.
    - **Notas**: Fornece informações sobre o motivo pelo qual um objeto não pode ser importado. O **notas** coluna também apresenta informações sobre as definições que foram ignoradas (para alguns tipos de objeto), mas o objeto é ainda importable sem essas definições.
    - **Linhas de base de configuração** (para itens de configuração): Especifica as linhas de base de configuração que estão associadas um item de configuração.
    - **Certificado necessário** (para as políticas e perfis): Especifica se um certificado é associado o objeto. Quando um certificado é associado o objeto, tem de importar o certificado demasiado.
9.  Após escolher os objetos a importar, estes são apresentados na página de resumo. Tem as seguintes ações disponíveis: 
    - **Exportar detalhes**: Cria um ficheiro. csv que contém as informações apresentadas no ecrã. Também mostra objetos que não são importable e o motivo por que motivo não pode ser importado. Pode manter este ficheiro para os registos. 
    - **Exportar dados de erro**: Exporta um ficheiro comprimido que contém informações sobre os dados que a ferramenta não foi capaz de converter ou importação. 

### <a name="phase-3-import-selected-objects-to-intune"></a>Passo 3: Importar os objetos selecionados ao Intune
Na fase 3, irá iniciar sessão no Intune e importar os objetos selecionados. 
10. Clique em **seguinte**e, em seguida, clique em **iniciar sessão no Intune** para iniciar sessão no inquilino do Intune para os dados de importam ou optar por exportar os dados.

    - **Exportar**: Depois de detetar e selecione os objetos do site para importar, pode exportar os objetos para um conjunto de dados. Isto permite-lhe detetar objetos a partir de um computador que não tem acesso à Internet, exportar os dados e, em seguida, importar os dados a partir de um computador que tenha acesso à Internet. O conjunto de dados é encriptado utilizando as credenciais de utilizador do Windows do utilizador com sessão iniciada, por isso, só o utilizador que exportou o conjunto de dados pode importar o conjunto de dados na ferramenta. Quando seleciona esta opção, escolha o caminho para os dados exportados. 
      1. Clique em **exportar** no **iniciar sessão no Intune** página. 
      2. Clique em **procurar** para selecionar a pasta de destino para a exportação. A pasta deve estar vazia. 
      3. Clique em **iniciar** para exportar os dados e, quando a exportação for concluída, clique em **fechar** para concluir o assistente e feche o importador de dados.
      4. Iniciar o importador de dados a partir de outro computador com acesso à Internet utilizando as mesma credenciais e selecione **importação exportado anteriormente o conjunto de dados** na segunda página do assistente. Depois dos dados são importados, o assistente leva-o para o **iniciar sessão no Intune** página. 
    - **Iniciar sessão no Intune**: Tem de iniciar sessão com uma conta de Administrador Global ou de administrador do Intune. Depois de iniciar sessão, inicia o processo de importação.
    
      > [!Important]
      > Recomendamos que teste primeiro o processo de importação de dados utilizando um inquilino de avaliação. Em seguida, depois de confirmar que os dados esperados tiver sido importado, pode percorrer o mesmo processo com o seu inquilino do Intune de produção.
12. A página do progresso fornece o progresso, como os objetos são importados. Clique em **seguinte** quando a importação estiver concluída. 
13. Na página conclusão, são apresentados os objetos importados. Verifique o estado de quaisquer objetos que encontrou um erro durante o processo de importação. Tem as seguintes ações disponíveis: 
    - **Exportar detalhes**: Cria um ficheiro. csv que contém as informações apresentadas no ecrã. Pode manter este ficheiro para os registos. 
    - **Exportar dados de erro**: Exporta um ficheiro comprimido que contém informações sobre os dados que a ferramenta não foi capaz de converter ou importação.

## <a name="next-steps"></a>Passos seguintes
Depois de importar os dados para o Intune, tem de tomar medidas para [preparar o Intune para a migração de utilizador](migrate-prepare-intune.md). 