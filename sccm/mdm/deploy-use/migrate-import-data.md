---
title: Importar dados para o Microsoft Intune
titleSuffix: Configuration Manager
description: Importar os dados do Configuration Manager para o Microsoft Intune
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 12/05/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: b552391d-abc0-48a2-a429-93605a13a66a
ms.collection: M365-identity-device-management
ms.openlocfilehash: 46b5034cb95193a07421fe79a445dac0f5b28503
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56124266"
---
# <a name="import-configuration-manager-data-to-microsoft-intune"></a>Importar os dados do Configuration Manager para o Microsoft Intune 

*Aplica-se a: O System Center Configuration Manager (ramo atual)*    

A primeira fase recomendada do processo para [migrar dispositivos e utilizadores MDM híbrida para o Intune autónomo](migrate-hybridmdm-to-intunesa.md) na configuração apenas na cloud é usar a ferramenta importador de dados do Intune. Se desejar, pode ignorar esta fase e passarei para o [preparar o Intune para a migração de utilizador](migrate-prepare-intune.md) fase. No entanto, essa ferramenta executa as seguintes funções que podem economizar muito tempo na fase seguinte:  

1.  Recolhe dados sobre os objetos que selecionar na hierarquia do Configuration Manager.  

2.  Fornece detalhes sobre os objetos que pode selecionar para a importação e informações sobre por que alguns objetos não podem ser importados.  

3.  Importa objetos selecionados para o inquilino do Microsoft Intune.  

A ferramenta importador de dados não altera o ambiente do Configuration Manager de forma alguma. Pode importar objetos para o Intune e validar que tudo funciona conforme esperado sem risco de mantendo os seus dispositivos MDM híbrida num Estado não gerido. 


## <a name="what-objects-can-this-tool-import"></a>Os objetos que pode importar esta ferramenta?

A ferramenta de importação pode recolher informações sobre os seguintes tipos de objeto no Configuration Manager e fornece informações sobre se a objetos recolhidos podem ser importados:  

- Itens de configuração  
- Perfis de certificados  
- Perfis de e-mail  
- Perfis VPN  
- Perfis de Wi-Fi  
- Políticas de conformidade  
- Aplicações  
- Implementações  

> [!Note]  
> A importação de implementações só é útil para outros tipos de objeto que está a importar. Por exemplo, se importar perfis VPN e implementações, apenas poderá importar as implementações para os perfis VPN que selecionar. As implementações no Intune são chamadas de atribuições. Se pretender importar uma implementação para um objeto importado anteriormente, terá de importar novamente esse objeto ou a atribuição de criar manualmente no Intune no Azure. Por exemplo, se importar perfis VPN e implementações não, terá executá-la novamente e selecione os perfis VPN e implementações ou a atribuição de criar manualmente no Intune no Azure. Se voltar a executar a ferramenta, podem ser criados objetos duplicados que pode eliminar posteriormente no Intune no Azure.  

> [!Important]  
> Se a coleção para uma implementação baseia-se um grupo do Active Directory que foram replicado para o Azure Active Directory (Azure AD), a ferramenta automaticamente destina-se os objetos migrados para os grupos se seleciona a implementação apropriada ao executar a ferramenta. Quando tiver coleções mais complexas ou coleções de associação direta, tem de recriar manualmente no Azure AD e manualmente as atribuições de objeto aos mesmos no Intune no Azure de destino.  


## <a name="things-to-know-before-you-run-the-tool"></a>Que precisa saber antes de executar a ferramenta

- Executar a ferramenta não será alterado o ambiente do Configuration Manager de forma alguma.  

- Em primeiro lugar, teste o processo de importação de dados a utilizar um inquilino de avaliação. Depois de confirmar que os dados esperados foi importado, pode avançar para o mesmo processo com o seu inquilino do Intune de produção.  

- O importador de dados destina-se apenas de importar dados do Configuration Manager uma vez. Ele não manter o controle de objetos no Configuration Manager ou o Intune. No entanto, se executar o importador novamente no mesmo computador como antes, ele indica quais os objetos que importou anteriormente. A ferramenta não sabe se o objeto ainda existe no Intune ou se um objeto tiver sido alterado. Se importar dados para o Intune mais de uma vez, pode acabar com objetos duplicados.  

- Nem todas as definições de perfil podem ser importadas. Por exemplo, não é possível importar o modo de local público ou definições PFX.  

- Se tiver uma política do Configuration Manager com as definições que não são aplicáveis às plataformas selecionadas, a ferramenta poderá ignorar estas definições durante a importação. Ignorar a ajuda de definições para se certificar de que a política pode ser importado e suportada pelo Intune.  

- A ferramenta tenta para que tenha um motivo por que um objeto não pode ser importado. Em alguns casos, antes de importar objetos para o Intune, pode ir para o console do Configuration Manager, corrigir o problema, inicie o Gestor de configuração de deteção de objetos procurar novamente e, em seguida, importar os objetos. Por vezes, poderá ter ou, talvez queira, recrie esses objetos manualmente no Intune.  

- Existem alguns perfis que dependem de outros objetos. Se quiser importar um perfil que depende de outro objeto, como um perfil de e-mail que depende de um certificado, tem de importar os dois objetos ao mesmo tempo, a menos que tiver importado anteriormente o outro objeto no mesmo computador com o mesmo utilizador.  

- Depois de executar a ferramenta, poderá ter de efetuar passos manuais adicionais. Filtragem por exemplo, aplicações e políticas de grupos do Azure AD.  

- Se todas as aplicações web (por vezes denominadas webclips) foram atribuídas aos utilizadores, deverá remover essas aplicações web antes de migrar os seus utilizadores. Em seguida, reatribua as aplicações web depois de concluída a migração. Se não fizer esta ação, os clips web tornará impossível de gerenciar após a migração.  


## <a name="prerequisites"></a>Pré-requisitos

- Especifique o site de nível superior e execute a ferramenta com um utilizador que tenha acesso a todos os objetos na hierarquia do site. A ferramenta Deteta apenas objetos acessíveis pelo utilizador que executa a ferramenta.  

- Um Administrador Global tem de executar a ferramenta importador de dados na primeira vez utilizando o parâmetro - GlobalConsent. Em seguida, um Administrador Global ou administrador do Intune pode executar a ferramenta. 

- Execute a ferramenta importador de dados no Windows 10 ou Windows Server 2016.


<!-- ## Objects that cannot be imported
There are some Configuration Manager objects that the importer tool cannot import to Intune. You must manually create these objects in Intune. 
- Collections based on direct membership or that are based on a query. The only collections that are imported are based on a single AD group. For all other collections, you must create the assignment in Intune and add the assignment to the appropriate objects. 
- Profiles <list what we cannot import>
- Policies <??>
- Etc.
-->



## <a name="download-the-data-importer-tool"></a>Transferir a ferramenta importador de dados

Transferir a ferramenta importador de dados a partir da **ConfigMgrTools/Intune-Data-Importer** repositório no GitHub. Utilize o procedimento seguinte para transferir a ferramenta.

1. Vá para o [versões do GitHub de importador de dados do Intune](https://github.com/ConfigMgrTools/Intune-Data-Importer/releases) página.  

2. Para a versão mais recente, clique em **Microsoft.Intune.Data.Importer.exe**.  

3. Salve e execute o ficheiro executável. Em seguida, escolha uma pasta de destino para extrair a ferramenta importador de dados do Intune.  



## <a name="run-the-data-importer-tool"></a>Execute a ferramenta importador de dados

O Assistente para a ferramenta importador de dados pode ser dividido em três etapas principais. Esta seção fornece informações para ajudar a concluir cada seção do assistente e importar com êxito os dados do Configuration Manager para o Intune. Cada passo continua em que terminou o passo anterior.


### <a name="provide-permission-for-the-data-importer-tool-to-access-resources"></a>Fornecer permissão para a ferramenta importador de dados para aceder aos recursos

Antes de poder executar a ferramenta importador de dados, tem de utilizar uma conta de Administrador Global para conceder a permissão de ferramenta importador de dados no Azure para aceder aos recursos. Em seguida, pode executar a ferramenta com uma conta de Administrador Global ou administrador do Intune.   

1.  Um Administrador Global tem de executar a ferramenta a primeira vez utilizando o seguinte parâmetro: `IntuneDataImporter.exe -GlobalConsent`  

2. Quando a ferramenta é iniciada, inicie sessão com uma conta com a função de Administrador Global no Azure.  

3. Selecione **Accept** para criar uma aplicação no Azure com os direitos adequados no Microsoft Graph. A ferramenta importador de dados precisa estes direitos para importar objetos para o Microsoft Intune.  

    > [!Important]  
    > Quando aceitar esta linha de comandos, conceder a permissão de ferramenta para executar as seguintes ações:  
    > - Ler todos os grupos  
    > - Iniciar sessão e ler o perfil de utilizador  
    > - Leitura e escrita da configuração de dispositivo do Intune e políticas  
    > - Ler e escrever aplicações do Intune  
    > - Ler e escrever as políticas de controlo de administração baseada em funções do Intune  
    > - Leitura e escrita de dispositivos do Intune  
    > - Leitura e escrita da configuração do Intune  

4. Depois de aceitar o consentimento, qualquer outro administrador Global ou administrador do Intune pode executar a ferramenta para importar dados do Configuration Manager para o Intune no Azure.  

> [!Note]  
> Se um Administrador Global primeiro ainda não aceitou o consentimento, a ferramenta pode apresentar o seguinte erro para um administrador do Intune: **Não é possível aceder a esta aplicação**.  


### <a name="manually-map-collections-to-azure-ad-groups"></a>Mapear manualmente coleções a grupos do Azure AD

Quando executar a ferramenta importador de dados, extrai o nome do grupo do Active Directory a partir de coleções com uma única regra direcionada para um único grupo do Active Directory. Quando as atribuições são criadas no Intune, o importador de dados de procura de um grupo do Azure AD com o mesmo nome de grupo do Active Directory. Se existir, a ferramenta atribui o objeto importado a esse grupo do Azure AD. 

Pode substituir o nome do grupo do Active Directory que o importador de dados encontra-se para uma coleção e fornecer um ou mais grupos do Azure AD para utilizar para essa coleção. Utilizar o ficheiro de mapeamento de coleção fornece uma forma para que possa mapear coleções que não são normalmente importável com o importador de dados para os grupos do Azure AD. 

#### <a name="find-the-collections-that-cant-be-imported"></a>Encontre as coleções que não não possível importar
Pode obter uma lista de todas as coleções que não são importável para que pode adicioná-los para o ficheiro. csv de mapeamento de coleção. 

1. Execute a ferramenta importador de dados e selecione os objetos a importar. Utilize os procedimentos no [fase 1: Detetar objetos do Configuration Manager e recolher dados](#phase-1:-discover-configuration-manager-objects-and-collect-data) e [fase 2: Resolver problemas e selecione os objetos a importar](#phase-2:-resolve-issues-and-select-the-objects-to-import) para detetar e escolha os objetos. Em seguida, no **resumo** página, selecione **exportar detalhes** para criar um ficheiro. csv com os detalhes de tudo o que selecionou para importação, incluindo os objetos que não podem ser importados e as Implantações.  

2. Abra o ficheiro. csv no Microsoft Excel e filtrar os dados com base na **implantação** para o **tipo** coluna e **não** para o **Importable** coluna. A coluna de nome de coleção mostra todas as coleções que têm de ser adicionadas a um ficheiro de mapeamento de coleção para que a ser importável dessas implementações.  

#### <a name="create-the-collection-mapping-file"></a>Criar o ficheiro de mapeamento de coleção
O ficheiro de mapeamento de coleção é um ficheiro de valores separados por vírgulas (CSV) em que a primeira coluna é o nome da coleção do Configuration Manager e a segunda coluna é o nome do grupo do Azure AD para utilizar para essa coleção. Para especificar mais do que um grupo do Azure AD para uma única coleção do Configuration Manager, crie várias linhas no ficheiro CSV com esse nome de coleção. O exemplo seguinte é um ficheiro CSV que contém duas coleções. A primeira coleção é mapeada para um único Azure AD de grupo e a segunda coleção é mapeada para dois grupos do Azure AD.

![Exemplo de ficheiro csv de mapeamento da coleção](../media/migrate-collectionmapping.png)

#### <a name="start-the-data-importer-tool-using-collection-mapping"></a>Inicie a ferramenta importador de dados com o mapeamento de coleção
Para utilizar um ficheiro de mapeamento de coleção, tem de iniciar a ferramenta importador de dados usando o **- CollectionMappingFile** parâmetro da linha de comandos e o caminho completo para o ficheiro. csv do mapeamento de coleção que cria. Por exemplo:

```IntuneDataImporter.exe -CollectionMappingFile c:\Users\myuser\Documents\collectionmapping.csv```

> [!Note]  
> O importador de dados não apresenta nada em qualquer página do Assistente para indicar que o ficheiro de mapeamento de coleção foi carregado. No entanto, a ferramenta apresenta quaisquer erros encontrados ao ler o ficheiro. csv. 
> 
> Além disso, no **resumo** página do assistente, pode rever **implementação** tipos. A ferramenta exibe **Sim** na coluna importável e listas de grupos do Azure AD que irá atribuir aos objetos na **notas** coluna.  


### <a name="phase-1-discover-configuration-manager-objects-and-collect-data"></a>Fase 1: Detetar objetos do Configuration Manager e recolher dados

Na fase 1, selecione os objetos para detetar e tiver a ferramenta recolher informações sobre os objetos selecionados. 

1. Abra a ferramenta e selecione **iniciar**.  

2. Leia as informações e, em seguida, selecione **seguinte**.  

3. Escolha se pretende importar um conjunto de dados anteriormente exportado ou selecione os tipos de objeto para importar:  

    - **Conjunto de dados de importação exportado a partir de uma execução anterior de importador de dados do Intune**: Selecione **navegue** para **pasta de dados exportados**. Selecione um conjunto de dados que exportou anteriormente com a ferramenta importador de dados. O utilizador que importa o conjunto de dados tem de ser o mesmo utilizador que os dados exportados. Depois de importar os dados, um resumo dos objetos são listados os **resumo** página do assistente. Se o resumo parecer correto, avance para o [fase 3: Objeto selecionado de importação para o Intune](#phase-3-import-selected-objects-to-intune).  

        > [!Note]  
        > Depois de detetar e selecione os objetos no seu site para importar, pode exportar os objetos a um conjunto de dados sobre o **iniciar sessão no Intune** página do assistente. Em seguida, pode importar o conjunto de dados nesta página. O conjunto de dados é encriptado utilizando as credenciais de utilizador do Windows do utilizador com sessão iniciada por isso, só o utilizador que exportou o conjunto de dados pode importar o conjunto de dados na ferramenta.  

    - **Selecione os tipos de objeto para importar**: Forneça as seguintes informações sobre o seu site e os objetos que pretende importar:  

        - **Nome do servidor de site**: Forneça o nome de domínio completamente qualificado do servidor do site para importar objetos. A ferramenta Deteta apenas objetos acessíveis pelo utilizador que executa a ferramenta. Normalmente, irá especificar o site de nível superior e execute a ferramenta com um utilizador que tenha acesso a todos os objetos na hierarquia do site.  

        - **Código do site**: Fornece o código de site para o servidor do site. Pode encontrar o código de três letras na parte superior da consola do Configuration Manager.  

        - **Objeto de tipos para importar**: Escolha os objetos que pretende que a ferramenta para recolher. Pode escolher **Selecionar tudo** para escolher todos os objetos ou selecionar os tipos de objeto individuais.  

4.  Selecione **seguinte** para começar a detetar os objetos no site. A ferramenta exibe o progresso de cada um dos tipos de objeto.  

    - Quando a ferramenta Deteta não existem dados para um tipo de objeto selecionado, o barra imediatamente apresenta foi concluída para esse tipo de objeto de progresso.  

    - Objetos que não selecionou não exibir na **recolher** página de dados.  

    - Pode executar a ferramenta novamente para objetos que não foram recolhidos ou se tiver cancelado durante o processo de coleta.  


### <a name="phase-2-resolve-issues-and-select-the-objects-to-import"></a>Fase 2: Resolver problemas e selecione os objetos a importar  

Fase 2, reveja os objetos encontrados pela ferramenta, resolver problemas que impedem que o objeto a ser importado para o Intune e selecione os objetos a importar. Se corrigir problemas, regresse à **detetar ambiente** página do Assistente para voltar a detetar os objetos. 

1. Clique em **seguinte** para rever os objetos recolhidos. Uma página de seleção de item está disponível para cada tipo de objeto recolhido.  
   <!--   > [!Tip]     
   > On each item selection page, you can create a filter to help you find the objects that you want to import. However, take note of the following:
   > - When you are on an item selection page and the view is filtered, the Select all checkboxes only apply to the displayed items. Any hidden objects because of a filter are not included when using the checkboxes.
   > - Objects are always grouped under their parent item even when you sort or filter the objects.
   -->
2. Em cada página de seleção de item, ordenar os objetos pela **Importable** coluna e analise os objetos que não são importável. As informações a **notas** coluna fornece detalhes sobre por que a ferramenta não é possível importar o objeto.  

3. Decida se pretende corrigir qualquer um dos problemas para objetos não importável. Se corrigir um ou mais problemas, selecione **Previous** até chegar ao selecionar os dados da página do Configuration Manager. Em seguida, coletar os dados novamente para ver se resolveu o problema. Pode continuar a corrigir problemas até estar satisfeito com os objetos que estão importável.  

4. Em cada página de seleção de item, selecione os objetos que pretende importar. São listadas as seguintes colunas:  

    - **Nome**: Nome do objeto do Configuration Manager.  

    - **Importável**: Especifica se um objeto pode ser importado. Só é possível escolher objetos que têm Sim na coluna importável.  

    - **Plataforma**: Especifica a plataforma suportada pelo objeto.  

    - **Já importado**: Especifica se o objeto já foi importado utilizando a ferramenta neste computador.  

    - **Foi substituído** (para aplicações): Especifica se a aplicação é substituída por outra aplicação. Selecione o **Show substituídas aplicações** opção na parte superior da página para aplicações substituídas apresentar.  

    - **Notas de**: Fornece informações sobre por que um objeto não pode ser importado. O **notas** coluna também apresenta informações sobre as definições que foram ignoradas (para alguns tipos de objeto), mas o objeto é ainda importável sem essas definições.  

    - **Linhas de base de configuração** (para itens de configuração): Especifica as linhas de base de configuração que estão associadas um item de configuração.  

    - **Certificado necessário** (para políticas e perfis): Especifica se um certificado é associado com o objeto. Quando um certificado está associado com o objeto, tem de importar o certificado também.  

5. Depois de escolher os objetos a importar, estes estão listados na página de resumo. Tem as seguintes ações disponíveis:  

    - **Exportar detalhes**: Cria um ficheiro. csv que contém as informações apresentadas no ecrã. Ela também mostra objetos que não são importável e o motivo por que não é possível importar. Pode manter este ficheiro para seus registros.  

    - **Exportar dados de erro**: Exporta um ficheiro comprimido que contém informações sobre os dados que a ferramenta não foi capaz de converter ou importação.  


### <a name="phase-3-import-selected-objects-to-intune"></a>Fase 3: Importar objetos selecionados para o Intune

Fase 3, inicie sessão no Intune e importar os objetos selecionados. 

1. Selecione **seguinte**e, em seguida, selecione uma das seguintes opções:  

    - **Exportar**: Depois de detetar e selecione os objetos no seu site para importar, é possível exportar os objetos para um conjunto de dados. Isto permite-lhe detetar objetos a partir de um computador que não tem acesso à internet, exportar os dados e, em seguida, importar os dados a partir de um computador com acesso à internet. O conjunto de dados é encriptado utilizando as credenciais de utilizador do Windows do utilizador com sessão iniciada por isso, só o utilizador que exportou o conjunto de dados pode importar o conjunto de dados na ferramenta. Ao escolher esta opção, escolha o caminho para os dados exportados.  

        1. Selecione **exportar** sobre o **iniciar sessão no Intune** página.  

        2. Selecione **procurar** para selecionar a pasta de destino para a exportação. A pasta pode estar vazia.  

        3. Selecione **iniciar** para exportar os dados. Quando a exportação for concluída, selecione **fechar** para concluir o assistente e feche o importador de dados.  

        4. Inicie o importador de dados a partir de outro computador com acesso à internet com as mesmas credenciais. Selecione **importação exportado anteriormente o conjunto de dados** na segunda página do assistente. Depois dos dados são importados, o assistente leva-o para o **iniciar sessão no Intune** página.  

    - **Iniciar sessão no Intune**: Inicie sessão com uma conta de Administrador Global ou administrador do Intune. Depois de iniciar sessão, o processo de importação é iniciado.  

        > [!Important]  
        > Em primeiro lugar, teste o processo de importação de dados a utilizar um inquilino de avaliação. Depois de confirmar que os dados esperados foi importado, pode avançar para o mesmo processo com o seu inquilino do Intune de produção.  

2. A página de progresso fornece o progresso, como os objetos são importados. Clique em **seguinte** quando a importação estiver concluída.  

3. Na página conclusão, os objetos importados são listados. Verifique o estado de todos os objetos que encontrou um erro durante o processo de importação. Tem as seguintes ações disponíveis:  

    - **Exportar detalhes**: Cria um ficheiro. csv que contém as informações apresentadas no ecrã. Pode manter este ficheiro para seus registros.  

    - **Exportar dados de erro**: Exporta um ficheiro comprimido que contém informações sobre os dados que a ferramenta não foi capaz de converter ou importação.  



## <a name="next-steps"></a>Passos seguintes

Depois de importar os dados para o Intune, [preparar o Intune para a migração de utilizador](migrate-prepare-intune.md). 
