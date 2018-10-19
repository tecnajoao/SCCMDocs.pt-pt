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
ms.openlocfilehash: 655d7663a6597ce1b13fb26a5340d482be1ba7ed
ms.sourcegitcommit: 8827ffaea108678da968a3623f072876990c830c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/18/2018
ms.locfileid: "49411315"
---
# <a name="import-configuration-manager-data-to-microsoft-intune"></a>Importar os dados do Configuration Manager para o Microsoft Intune 

*Aplica-se a: O System Center Configuration Manager (ramo atual)*    

A primeira fase recomendada do processo para [migrar dispositivos e utilizadores MDM híbrida para o Intune autónomo](migrate-hybridmdm-to-intunesa.md) na configuração apenas na cloud é usar a ferramenta importador de dados do Intune. Se desejar, pode ignorar esta fase e passarei para o [preparar o Intune para a migração de utilizador](migrate-prepare-intune.md) fase. No entanto, essa ferramenta executa as seguintes funções que podem economizar muito tempo na fase seguinte: 
1.  Recolhe dados sobre os objetos que selecionar na hierarquia do Configuration Manager. 
2.  Fornece detalhes sobre os objetos que pode selecionar para a importação e informações sobre por que alguns objetos não podem ser importados.
3.  Importa objetos selecionados para o inquilino do Microsoft Intune. 

A ferramenta importador de dados não altera o ambiente do Configuration Manager de qualquer forma e, portanto, pode importar objetos para o Intune e validar que tudo funciona conforme esperado sem risco de mantendo os seus dispositivos MDM híbrida num Estado não gerido. 

## <a name="what-objects-can-this-tool-import"></a>Os objetos que pode importar esta ferramenta?
A ferramenta de importação pode recolher informações sobre os seguintes tipos de objeto no Configuration Manager e fornece informações sobre se a objetos recolhidos podem ser importados: 
- Itens de configuração
- Perfis de certificado
- Perfis de e-mail
- Perfis VPN
- Perfis de Wi-Fi
- Políticas de conformidade
- Aplicações
- Implementações

> [!Note]    
> A importação de implementações só é útil para outros tipos de objeto que está a importar. Por exemplo, se importar perfis VPN e implementações, apenas poderá importar as implementações para os perfis VPN que selecionar. As implementações no Intune são chamadas de atribuições. Se pretender importar uma implementação para um objeto importado anteriormente, terá de importar novamente esse objeto ou a atribuição de criar manualmente no Intune no Azure. Por exemplo, se importar perfis VPN e implementações não, terá executá-la novamente e selecione os perfis VPN e implementações ou a atribuição de criar manualmente no Intune no Azure.  Se voltar a executar a ferramenta, podem ser criados objetos duplicados que pode eliminar posteriormente no Intune no Azure.  

> [!Important]    
> Se a coleção para uma implementação baseia-se um grupo do Active Directory que foram replicado para Azure Active Directory (AAD), a ferramenta automaticamente destina-se a objetos migrados para os grupos se seleciona a implementação apropriada ao executar a ferramenta. Quando tiver coleções mais complexas ou coleções de associação direta, tem de recriar manualmente no AAD e manualmente as atribuições de objeto aos mesmos no Intune no Azure de destino.


## <a name="things-to-know-before-you-run-the-tool"></a>Que precisa saber antes de executar a ferramenta
- Executar a ferramenta não será alterado ao ambiente do Configuration Manager de forma alguma.
- Recomendamos que teste primeiro o processo de importação de dados a utilizar um inquilino de avaliação. Em seguida, depois de confirmar que os dados esperados foi importado, pode avançar para o mesmo processo com o seu inquilino do Intune de produção.
- O importador de dados destina-se apenas de importar dados do Configuration Manager uma vez. Ele não manter um registo de objetos no Configuration Manager ou o Intune. No entanto, se executar o importador novamente no mesmo computador como antes, ele informará quais os objetos que importou anteriormente. A ferramenta não saberá se o objeto ainda existe no Intune ou se um objeto tiver sido alterado. Se importar dados para o Intune mais de uma vez, pode acabar com objetos duplicados.
- Nem todas as definições de perfil podem ser importadas. Por exemplo, não é possível importar o modo de local público ou definições PFX. 
- Se tiver uma política do Gestor de configuração com definições que não são aplicáveis às plataformas selecionadas, a ferramenta poderá ignorar estas definições durante a importação. Ignorar a ajuda de definições para se certificar de que a política pode ser importado e suportada pelo Intune. 
- A ferramenta irá tentar para que tenha um motivo por que um objeto não pode ser importado. Em alguns casos, antes de importar objetos para o Intune, pode ir para o console do Configuration Manager, corrigir o problema, inicie o Gestor de configuração de deteção de objetos procurar novamente e, em seguida, importar os objetos. Por vezes, poderá ter ou, talvez queira, recrie esses objetos manualmente no Intune.
- Existem alguns perfis que dependem de outros objetos. Se quiser importar um perfil que depende de outro objeto, como um perfil de e-mail que depende de um certificado, tem de importar os dois objetos ao mesmo tempo, a menos que tiver importado anteriormente o outro objeto no mesmo computador com o mesmo utilizador.  
- Depois de executar a ferramenta, poderá ter de efetuar passos manuais adicionais. Filtragem por exemplo, aplicações e políticas a grupos do AAD. 
- Se todas as aplicações web (por vezes denominadas webclips) foram atribuídas aos utilizadores, deve remover essas aplicações web antes de migrar os seus utilizadores, então reatribuir as aplicações web, assim que a migração estiver concluída. Se isso não for feito, os clips web tornará impossível de gerenciar após a migração.

## <a name="prerequisites"></a>Pré-requisitos
- Configuration Manager versão 1610 ou posterior.-é recomendável que especificar o site de nível superior e execute a ferramenta com um utilizador que tem acesso a todos os objetos na hierarquia do site. A ferramenta Deteta apenas objetos acessíveis pelo utilizador que executa a ferramenta. 
- Um Administrador Global tem de executar a ferramenta importador de dados na primeira vez utilizando os seguintes ***intunedataimporter.exe - GlobalConsent*** parâmetro. Em seguida, um Administrador Global ou administrador do Intune pode executar a ferramenta.  


<!-- ## Objects that cannot be imported
There are some Configuration Manager objects that the importer tool cannot import to Intune. You must manually create these objects in Intune. 
- Collections based on direct membership or that are based on a query. The only collections that are imported are based on a single AD group. For all other collections, you must create the assignment in Intune and add the assignment to the appropriate objects. 
- Profiles <list what we cannot import>
- Policies <??>
- Etc.
-->

## <a name="download-the-data-importer-tool"></a>Transferir a ferramenta importador de dados
A ferramenta importador de dados está disponível para transferência a partir do repositório de ConfigMgrTools/Intune-Data-Importer no GitHub. Utilize o procedimento seguinte para transferir a ferramenta.

1. Vá para o [versões do GitHub de importador de dados do Intune](https://github.com/ConfigMgrTools/Intune-Data-Importer/releases) página.
2. Para a versão mais recente, clique em **Microsoft.Intune.Data.Importer.exe**.
3. Guardar e executar (ou basta executar) .exe e, em seguida, escolha uma pasta de destino para extrair a ferramenta importador de dados do Intune.

## <a name="run-the-data-importer-tool"></a>Execute a ferramenta importador de dados
O Assistente para a ferramenta importador de dados pode ser dividido em três etapas principais. Esta seção fornece informações para ajudar a concluir cada seção do assistente e importar com êxito os dados do Configuration Manager para o Intune. Cada passo continua em que terminou o passo anterior.

### <a name="provide-permission-for-the-data-importer-tool-to-access-resources"></a>Fornecer permissão para a ferramenta importador de dados para aceder aos recursos
Antes de poder executar a ferramenta importador de dados, tem de utilizar uma conta de Administrador Global para conceder a permissão de ferramenta importador de dados no Azure para aceder aos recursos. Em seguida, pode executar a ferramenta com uma conta de Administrador Global ou administrador do Intune.   

1.  Um Administrador Global tem de executar o tempo de ferramenta o primeiro com o seguinte parâmetro: ***intunedataimporter.exe - GlobalConsent*** 
2. Quando a ferramenta é iniciada, um ecrã de início de sessão mostra onde tem de iniciar sessão com uma conta com a função de Administrador Global no Azure. 
3. Clique em **Accept** para criar uma aplicação no Azure com os direitos adequados no Microsoft Graph. A ferramenta importador de dados precisa estes direitos para importar objetos para o Microsoft Intune.   

   > [!Important]
   > Quando clica em **Accept**, conceder a permissão de ferramenta para fazer o seguinte:
   > - Ler todos os grupos
   > - Iniciar sessão e ler o perfil de utilizador
   > - Leitura e escrita da configuração de dispositivo do Intune e políticas
   > - Ler e escrever aplicações do Intune
   > - Ler e escrever as políticas de controlo de administração baseada em funções do Intune
   > - Leitura e escrita de dispositivos do Intune
   > - Leitura e escrita da configuração do Intune
1. Depois de aceitar o consentimento, qualquer outro administrador Global ou administrador do Intune pode executar a ferramenta para importar dados do Configuration Manager para o Intune no Azure.    
        
    > [!Note]
    > Se o consentimento primeiro não foi aceite por um Administrador Global, a ferramenta pode exibir **não é possível aceder a esta aplicação** depois de um administrador do Intune é executado a ferramenta importador de dados e inicia sessão na subscrição do Intune.

### <a name="manually-map-collections-to-azure-ad-groups"></a>Mapear manualmente coleções a grupos do Azure AD
Quando executar a ferramenta importador de dados, extrai o nome de grupo do AD a partir de coleções com uma única regra direcionada para um único grupo do AD. Quando as atribuições são criadas no Intune, o importador de dados procura um grupo do Azure AD com o mesmo nome que o grupo do AD e, se existir, atribui o objeto importado a esse grupo do Azure AD. Pode substituir o nome de grupo do AD que o importador de dados localiza-se para uma coleção e fornecer um ou mais grupos do Azure AD para utilizar para essa coleção. Utilizar o ficheiro de mapeamento de coleção fornece uma forma para que possa mapear coleções que não são normalmente importável com o importador de dados para os grupos do Azure AD.
#### <a name="find-the-collections-that-cannot-be-imported"></a>Encontre as coleções que não não possível importar
Pode obter uma lista de todas as coleções que não são importável para que pode adicioná-los para o ficheiro. csv de mapeamento de coleção. 
1. Execute a ferramenta importador de dados e selecione os objetos a importar. Utilize os procedimentos no [fase 1: Detetar objetos do Configuration Manager e recolher dados](#phase-1:-discover-configuration-manager-objects-and-collect-data) e [fase 2: Resolver problemas e selecione os objetos a importar](#phase-2:-resolve-issues-and-select-the-objects-to-import) para detetar e escolha os objetos. Em seguida, no **resumo** página, selecione **exportar detalhes** para criar um ficheiro. csv com os detalhes de tudo o que selecionou para importação, incluindo os objetos que não podem ser importados e as Implantações. 
2. Abra o ficheiro. csv no Microsoft Excel e filtrar os dados com base na **implantação** para o **tipo** coluna e **não** para o **Importable** coluna. A coluna de nome de coleção mostra todas as coleções que têm de ser adicionadas a um ficheiro de mapeamento de coleção para que a ser importável dessas implementações.

#### <a name="create-the-collection-mapping-file"></a>Criar o ficheiro de mapeamento de coleção
O ficheiro de mapeamento de coleção é um ficheiro de valores separados por vírgulas (CSV) em que a primeira coluna é o nome da coleção do Configuration Manager e a segunda coluna é o nome do grupo do Azure AD para utilizar para essa coleção. Para especificar mais do que um grupo do Azure AD para uma única coleção do Configuration Manager, crie várias linhas no ficheiro CSV com esse nome de coleção. O exemplo seguinte é um ficheiro CSV que contém duas coleções. A primeira coleção é mapeada para um único Azure AD de grupo e a segunda coleção é mapeada para dois grupos do Azure AD.

![Exemplo de ficheiro csv de mapeamento da coleção](..\media\migrate-collectionmapping.png)

#### <a name="start-the-data-importer-tool-using-collection-mapping"></a>Inicie a ferramenta importador de dados com o mapeamento de coleção
Para utilizar um ficheiro de mapeamento de coleção, tem de iniciar a ferramenta importador de dados usando o *- CollectionMappingFile* parâmetro da linha de comandos e o caminho completo para o ficheiro. csv do mapeamento de coleção que cria. Por exemplo:

```IntuneDataImporter.exe -CollectionMappingFile c:\Users\myuser\Documents\collectionmapping.csv```

> [!Note]
> O importador de dados não apresenta nada em qualquer página do Assistente para indicar que o ficheiro de mapeamento de coleção foi carregado. No entanto, a ferramenta apresenta quaisquer erros encontrados ao ler o ficheiro. csv. Além disso, no **resumo** página do assistente, pode rever **implementação** tipos. A ferramenta exibe **Sim** na coluna importável e listas de grupos do Azure AD que irá atribuir aos objetos na **notas** coluna.

### <a name="phase-1-discover-configuration-manager-objects-and-collect-data"></a>Fase 1: Detetar objetos do Configuration Manager e recolher dados
Na fase 1, selecione os objetos para detetar e tiver a ferramenta recolher informações sobre os objetos selecionados. 
1. Abra a ferramenta e clique em **iniciar**.  
2. Leia as informações e, em seguida, clique em **seguinte**. 
3. Escolha se pretende importar um conjunto de dados anteriormente exportado ou selecione os tipos de objeto para importar:
   - **Importar exportado anteriormente o conjunto de dados**: Escolher **conjunto de dados de importação exportado a partir de uma execução anterior de importador de dados do Intune**e clique em **procurar** para **pasta de dados exportados** selecionar uma data definida que anteriormente exportado com a ferramenta importador de dados. O utilizador que importa o conjunto de dados tem de ser o mesmo utilizador que os dados exportados. Depois de importar os dados, um resumo dos objetos são listados os **resumo** página do assistente. Se o resumo parecer correto, avance para o [fase 3: Objeto selecionado de importação para o Intune](phase-3:-import-selected-object-to-intune).
 
      > [!Note]
      > Depois de detetar e selecione os objetos no seu site para importar, pode exportar os objetos a um conjunto de dados sobre o **iniciar sessão no Intune** página do assistente. Em seguida, pode importar o conjunto de dados nesta página. O conjunto de dados é encriptado utilizando as credenciais de utilizador do Windows do utilizador com sessão iniciada por isso, só o utilizador que exportou o conjunto de dados pode importar o conjunto de dados na ferramenta. 
   - **Selecione os tipos de objeto para importar**: Escolher **seleciona os tipos de objeto para importar** para selecionar os tipos de objeto para importar e detete objetos no seu ambiente. Forneça as seguintes informações sobre o seu site e os objetos que pretende importar.
      - **Nome do servidor de site**: Forneça o nome de domínio completamente qualificado do servidor do site para importar objetos. A ferramenta Deteta apenas objetos acessíveis pelo utilizador que executa a ferramenta. Normalmente, irá especificar o site de nível superior e execute a ferramenta com um utilizador que tenha acesso a todos os objetos na hierarquia do site.
      - **Código do site**: Fornece o código de site para o servidor do site. Pode encontrar o código de três letras na parte superior da consola do Configuration Manager.
      - **Objeto de tipos para importar**: Escolha os objetos que pretende que a ferramenta para recolher. Pode escolher **Selecionar tudo** para escolher todos os objetos ou selecionar os tipos de objeto individuais. 
4.  Clique em **seguinte** para começar a detetar os objetos no site. A ferramenta exibe o progresso de cada um dos tipos de objeto. 
    - Quando a ferramenta Deteta não existem dados para um tipo de objeto selecionado, o barra imediatamente apresenta foi concluída para esse tipo de objeto de progresso.
    - Objetos que não selecionou não são apresentadas na **recolher** página de dados. 
    - Pode executar a ferramenta novamente para objetos que não foram recolhidos ou se tiver cancelado durante o processo de coleta.

### <a name="phase-2-resolve-issues-and-select-the-objects-to-import"></a>Fase 2: Resolver problemas e selecione os objetos a importar  
Fase 2, reveja os objetos encontrados pela ferramenta, resolver problemas que impedem que o objeto a ser importado para o Intune e selecione os objetos a importar. Se corrigir problemas, regresse à **detetar ambiente** página do Assistente para voltar a detetar os objetos. 
5.  Clique em **seguinte** para rever os objetos recolhidos. Uma página de seleção de item está disponível para cada tipo de objeto recolhido. 
 <!--   > [!Tip]     
    > On each item selection page, you can create a filter to help you find the objects that you want to import. However, take note of the following:
    > - When you are on an item selection page and the view is filtered, the Select all checkboxes only apply to the displayed items. Any hidden objects because of a filter are not included when using the checkboxes.
    > - Objects are always grouped under their parent item even when you sort or filter the objects.
-->
6.  Em cada página de seleção de item, ordenar os objetos pela coluna importável e analise os objetos que não são importável. As informações da coluna de notas fornecem detalhes sobre por que a ferramenta não é possível importar o objeto. 
7.  Agora deve decidir se pretende corrigir qualquer um dos problemas para objetos não importável. Se corrigir um ou mais problemas, clique em anterior até que obtenha a selecionar os dados da página do Configuration Manager e recolher os dados novamente para ver se resolveu o problema. Pode continuar a corrigir problemas até estar satisfeito com os objetos que estão importável. 
8.  Em cada página de seleção de item, selecione os objetos que pretende importar. São listadas as seguintes colunas:
    - **Nome**: Nome do objeto do Configuration Manager. 
    - **Importável**: Especifica se um objeto pode ser importado. Só é possível escolher objetos que têm Sim na coluna importável. 
    - **Plataforma**: Especifica a plataforma suportada pelo objeto.
    - **Já importado**: Especifica se o objeto já foi importado utilizando a ferramenta neste computador. 
    - **Foi substituído** (para aplicações): Especifica se a aplicação é substituída por outra aplicação. Tem de verificar a **Show substituídas aplicações** caixa de verificação na parte superior da página para aplicações substituídas apresentar.
    - **Notas de**: Fornece informações sobre por que um objeto não pode ser importado. O **notas** coluna também apresenta informações sobre as definições que foram ignoradas (para alguns tipos de objeto), mas o objeto é ainda importável sem essas definições.
    - **Linhas de base de configuração** (para itens de configuração): Especifica as linhas de base de configuração que estão associadas um item de configuração.
    - **Certificado necessário** (para políticas e perfis): Especifica se um certificado é associado com o objeto. Quando um certificado está associado com o objeto, tem de importar o certificado também.
9.  Depois de escolher os objetos a importar, estes são apresentados na página de resumo. Tem as seguintes ações disponíveis: 
    - **Exportar detalhes**: Cria um ficheiro. csv que contém as informações apresentadas no ecrã. Ela também mostra objetos que não são importável e o motivo por que não é possível importar. Pode manter este ficheiro para seus registros. 
    - **Exportar dados de erro**: Exporta um ficheiro comprimido que contém informações sobre os dados que a ferramenta não foi capaz de converter ou importação. 

### <a name="phase-3-import-selected-objects-to-intune"></a>Fase 3: Importar objetos selecionados para o Intune
Fase 3, irá iniciar sessão no Intune e importar os objetos selecionados. 
10. Clique em **próxima**e, em seguida, clique em **iniciar sessão no Intune** para iniciar sessão no inquilino do Intune para os dados de importam ou optar por exportar os dados.

    - **Exportar**: Depois de detetar e selecione os objetos no seu site para importar, é possível exportar os objetos para um conjunto de dados. Isto permite-lhe detetar objetos a partir de um computador que não tem acesso à Internet, exportar os dados e, em seguida, importar os dados a partir de um computador com acesso à Internet. O conjunto de dados é encriptado utilizando as credenciais de utilizador do Windows do utilizador com sessão iniciada por isso, só o utilizador que exportou o conjunto de dados pode importar o conjunto de dados na ferramenta. Ao escolher esta opção, escolha o caminho para os dados exportados. 
      1. Clique em **exportar** sobre o **iniciar sessão no Intune** página. 
      2. Clique em **procurar** para selecionar a pasta de destino para a exportação. A pasta pode estar vazia. 
      3. Clique em **começar** para exportar os dados e, quando a exportação for concluída, clique em **fechar** para concluir o assistente e feche o importador de dados.
      4. Iniciar o importador de dados a partir de outro computador com acesso à Internet usando as mesmas credenciais e selecione **importação exportado anteriormente o conjunto de dados** na segunda página do assistente. Depois dos dados são importados, o assistente leva-o para o **iniciar sessão no Intune** página. 
    - **Iniciar sessão no Intune**: Tem de iniciar sessão com uma conta de Administrador Global ou administrador do Intune. Depois de iniciar sessão, o processo de importação é iniciado.
    
      > [!Important]
      > Recomendamos que teste primeiro o processo de importação de dados a utilizar um inquilino de avaliação. Em seguida, depois de confirmar que os dados esperados foi importado, pode avançar para o mesmo processo com o seu inquilino do Intune de produção.
12. A página de progresso fornece o progresso, como os objetos são importados. Clique em **seguinte** quando a importação estiver concluída. 
13. Na página conclusão, os objetos importados são listados. Verifique o estado de todos os objetos que encontrou um erro durante o processo de importação. Tem as seguintes ações disponíveis: 
    - **Exportar detalhes**: Cria um ficheiro. csv que contém as informações apresentadas no ecrã. Pode manter este ficheiro para seus registros. 
    - **Exportar dados de erro**: Exporta um ficheiro comprimido que contém informações sobre os dados que a ferramenta não foi capaz de converter ou importação.

## <a name="next-steps"></a>Passos seguintes
Depois de importar os dados para o Intune, tem de tomar medidas para [preparar o Intune para a migração de utilizador](migrate-prepare-intune.md). 
