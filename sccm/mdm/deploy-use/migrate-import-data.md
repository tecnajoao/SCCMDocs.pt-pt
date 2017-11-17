---
title: Importar dados para o Microsoft Intune
titleSuffix: Configuration Manager
description: 
keywords: 
author: dougeby
manager: dougeby
ms.date: 09/12/2017
ms.topic: article
ms.prod: configmgr-hybrid
ms.service: 
ms.technology: 
ms.assetid: b552391d-abc0-48a2-a429-93605a13a66a
ms.openlocfilehash: 4b5f788a611b9df7c12f788099d82fadbf1e4af9
ms.sourcegitcommit: 986fc2d54f7c5fa965fd4df42f4db4ecce6b79cb
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 11/17/2017
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
> Importar implementações só é útil para outros tipos de objeto que está a importar. Por exemplo, se importar perfis VPN e implementações, só poderá importar as implementações para os perfis VPN que selecionar. Implementações no Intune são denominadas atribuições. Se pretender importar uma implementação de um objeto importado anteriormente, terá de importar esse objeto againor criar manualmente a atribuição no Intune no Azure. Por exemplo, se importar perfis VPN e não implementações, terá de executar a ferramenta novamente e selecione perfis VPN e as implementações ou criar manualmente a atribuição no Intune no Azure.  Se voltar a executar a ferramenta, é possível criar objectos duplicados que pode eliminar mais tarde no Intune no Azure.  

> [!Important]    
> Se a coleção para uma implementação baseiam-se um grupo do Active Directory que foram replicado para Azure Active Directory (AAD), a ferramenta automaticamente destina-se a objetos migrados para os grupos se seleciona a implementação adequada quando executar a ferramenta. Quando tiver coleções mais complexas ou coleções de associação direta, tem de recriar manualmente no AAD e atribuições de objeto aos mesmos no Intune no Azure de destino manualmente.


## <a name="things-to-know-before-you-run-the-tool"></a>Coisas que deve saber antes de executar a ferramenta
- Executar a ferramenta não irá alterar o seu ambiente do Configuration Manager de qualquer forma.
- Recomendamos que teste primeiro o processo de importação de dados utilizando um inquilino de avaliação. Em seguida, depois de confirmar que os dados esperados tiver sido importado, pode percorrer o mesmo processo com o seu inquilino do Intune de produção.
- O importador de dados destina-se apenas importar dados do Configuration Manager uma vez. -Não manter controlar dos objetos no Configuration Manager ou o Intune. No entanto, se executar o importador de novo no mesmo computador como anteriormente,-informará os objetos que importou anteriormente. A ferramenta não saberá se o objeto ainda existe no Intune ou se um objeto foi alterada. Se importar dados para o Intune mais do que uma vez, poderá acabar com objetos duplicados.
- Nem todas as definições de perfil podem ser importadas. Por exemplo, não é possível importar o modo de local público ou definições PFX. 
- Se tiver uma política do Gestor de configuração com definições que não são aplicáveis a plataformas selecionadas, a ferramenta poderá ignorar estas definições durante a importação. A ignorar a ajuda de definições para se certificar de que a política pode ser importada e suportada pelo Intune. 
- A ferramenta irá tentar dão-lhe um motivo para o motivo pelo qual um objeto não pode ser importado. Em alguns casos, antes de importar objetos para o Intune, pode aceder novamente à consola do Configuration Manager, corrija o problema, inicie o Gestor de configuração de deteção de objetos novamente procurar e, em seguida, importar os objetos. Por vezes, poderá ter, ou poderá querer, recrie estes objetos manualmente no Intune.
- Existem algumas perfis que dependem de outros objetos. Se pretender importar um perfil que depende de outro objeto, como um perfil de e-mail que depende de um certificado, tem de importar os dois objetos ao mesmo tempo.
- Depois de executar a ferramenta, poderá ter de efetuar passos manuais adicionais. Por exemplo, filtragem de aplicações e políticas a grupos do AAD. 

## <a name="prerequisites"></a>Pré-requisitos
- Configuration Manager versão 1610 ou posterior.-é recomendável que especifica o site de nível superior e execute a ferramenta com um utilizador que tem acesso a todos os objetos na hierarquia do site. A ferramenta só Deteta objetos acessíveis ao utilizador que executa a ferramenta. 
- Tem de executar a ferramenta de um computador que tenha acesso ao fornecedor de SMS (para recolher dados do Configuration Manager) e a Internet (para importar objetos para o Intune).
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

1. Vá para o [Intune dados importador GitHub](https://go.microsoft.com/fwlink/?linkid=858194) página.
2. Clique em **clonar ou transferir**, clique em **transferir ZIP**e guarde o ficheiro ZIP comprimido. 
3. Extraia os conteúdos do ficheiro ZIP.

## <a name="run-the-data-importer-tool"></a>Execute a ferramenta do importador de dados
Antes de poder executar a ferramenta do importador de dados, tem de utilizar uma conta de Administrador Global para conceder a permissão de ferramenta do importador de dados no Azure para aceder aos recursos. Em seguida, pode executar a ferramenta utilizando uma conta de Administrador Global ou de administrador do Intune.     

O Assistente para a ferramenta do importador de dados pode ser dividido em três passos principais. Esta secção fornece informações para ajudar a concluir cada secção do assistente e importar dados do Configuration Manager com êxito no Intune. Cada passo continua em que terminou o passo anterior.

### <a name="provide-permission-for-the-data-importer-tool-to-access-resources"></a>Fornecer permissão para a ferramenta de importador de dados para aceder a recursos
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

### <a name="phase-1-discover-configuration-manager-objects-and-collect-data"></a>Fase 1: Detetar objetos do Configuration Manager e recolher dados
Fase 1, selecione os objetos para detetar e ter a ferramenta de recolher informações sobre os objetos selecionados. 
1. Abrir a ferramenta e clique em **iniciar**.  
2. Ler as informações e, em seguida, clique em **seguinte**. 
3. Forneça as seguintes informações sobre o seu site e os objetos no site que pretende importar. 
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

    > [!Tip]     
    > Na página de seleção de cada item, pode criar um filtro para o ajudar a localizar os objetos que pretende importar. No entanto, tome nota dos seguintes procedimentos:
    > - Quando estão na página de seleção de um item e a vista é filtrada, selecionar todas as caixas de verificação só se aplicam aos itens apresentados. Quaisquer objetos ocultos devido a um filtro não estão incluídos ao utilizar as caixas de verificação.
    > - Objetos sempre são agrupados no respetivo item principal, mesmo quando a ordenação ou os objetos de filtro.


6.  Na página de seleção de cada item, ordenar os objetos pela coluna Importable e reveja os objetos que não estão importable. As informações da coluna de notas fornecem detalhes sobre o motivo pelo qual a ferramenta não é possível importar o objeto. 
7.  Agora tem de decidir se pretende corrigir quaisquer problemas de objetos não importable. Se corrigir um ou mais problemas, clique em anterior até obter selecione nos dados de página do Configuration Manager e recolher os dados novamente para ver se resolver o problema. Pode continuar a corrigir problemas até estar satisfeito com os objetos que estão importable. 
8.  Na página de seleção de cada item, selecione os objetos que pretende importar. São apresentadas as seguintes colunas:
    - **Nome**: Nome do objeto do Configuration Manager. 
    - **Importable**: Especifica se um objeto pode ser importado. Só é possível escolher objetos que têm Sim na coluna Importable. 
    - **Plataforma**: Especifica a plataforma suportada pelo objeto.
    - **Já importado**: Especifica se o objeto já foi importado utilizando a ferramenta neste computador. 
    - **Notas**: Fornece informações sobre o motivo pelo qual um objeto não pode ser importado.
    - **Linhas de base de configuração** (para itens de configuração): Especifica as linhas de base de configuração que estão associadas um item de configuração.
    - **Certificado necessário** (para as políticas e perfis): Especifica se um certificado é associado o objeto. Quando um certificado é associado o objeto, tem de importar o certificado demasiado.
9.  Após escolher os objetos a importar, estes são apresentados na página de resumo. Tem as seguintes ações disponíveis: 
    - **Exportar detalhes**: Cria um ficheiro. csv que contém as informações apresentadas no ecrã. Pode manter este ficheiro para os registos. 
    - **Exportar dados de erro**: Exporta um ficheiro comprimido que contém informações sobre os dados que a ferramenta não foi capaz de converter ou importação. 

### <a name="phase-3-import-selected-object-to-intune"></a>Passo 3: Importar o objeto selecionado para o Intune
Na fase 3, irá iniciar sessão no Intune e importar os objetos selecionados. 
10. Clique em **seguinte**e, em seguida, clique em **iniciar sessão no Intune** para iniciar sessão no inquilino do Intune para que a importação de dados. Tem de iniciar sessão com uma conta de Administrador Global ou de administrador do Intune. Depois de iniciar sessão, inicia o processo de importação.

    > [!Important]
    > Recomendamos que teste primeiro o processo de importação de dados utilizando um inquilino de avaliação. Em seguida, depois de confirmar que os dados esperados tiver sido importado, pode percorrer o mesmo processo com o seu inquilino do Intune de produção.

12. A página do progresso fornece o progresso, como os objetos são importados. Clique em **seguinte** quando a importação estiver concluída. 
13. Na página conclusão, são apresentados os objetos importados. Verifique o estado de quaisquer objetos que encontrou um erro durante o processo de importação. Tem as seguintes ações disponíveis: 
    - **Exportar detalhes**: Cria um ficheiro. csv que contém as informações apresentadas no ecrã. Pode manter este ficheiro para os registos. 
    - **Exportar dados de erro**: Exporta um ficheiro comprimido que contém informações sobre os dados que a ferramenta não foi capaz de converter ou importação.

## <a name="next-steps"></a>Passos seguintes
Depois de importar os dados para o Intune, tem de tomar medidas para [preparar o Intune para a migração de utilizador](migrate-prepare-intune.md). 