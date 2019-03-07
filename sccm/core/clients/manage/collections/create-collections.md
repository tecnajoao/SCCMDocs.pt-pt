---
title: Criar coleções
titleSuffix: Configuration Manager
description: Crie coleções no Configuration Manager para gerir mais facilmente os grupos de utilizadores e dispositivos.
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1401a35e-4312-4d3b-8ceb-0abbb10d4f05
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8e79ec4b19ad45c49438ef273bcaf031754cf7e7
ms.sourcegitcommit: f3dd8405018fe1043434386be15c16752c1a4a3c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/07/2019
ms.locfileid: "57558138"
---
# <a name="how-to-create-collections-in-configuration-manager"></a>Como criar coleções no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

As coleções são grupos de utilizadores ou dispositivos. Coleções de utilização para tarefas como a gestão de aplicações, implementar as definições de compatibilidade ou instalação de atualizações de software. Também pode utilizar coleções para gerir grupos de definições de cliente ou utilizá-las com a administração baseada em funções para especificar os recursos aos quais um utilizador administrativo pode aceder. O Configuration Manager contém várias coleções incorporadas. Para obter mais informações, consulte [introdução às coleções](/sccm/core/clients/manage/collections/introduction-to-collections).  

> [!NOTE]  
> Uma coleção pode conter utilizadores ou dispositivos, mas não ambos.  


Utilize este artigo para ajudar a criar coleções no Configuration Manager. Também pode importar coleções criadas este ou para outro site do Configuration Manager. Para obter mais informações sobre como exportar e importar coleções, consulte [como gerir coleções](/sccm/core/clients/manage/collections/manage-collections).  



## <a name="collection-rules"></a>Regras de recolha

Existem regras diferentes que pode utilizar para configurar os membros de uma coleção no Configuration Manager.  


### <a name="direct-rule"></a>Regra direta

Utilize para escolher os utilizadores ou computadores que pretende adicionar a uma coleção. Esta associação não é alterado, a menos que remove um recurso do Configuration Manager. Antes de poder adicionar os recursos numa coleção de regra direta, deve ter detetado do Configuration Managê-los ou terá de ter importado-los. As coleções de regra direta têm um overhead administrativo mais elevado que as coleções de regra de consulta de pois requerem alterações manuais.


### <a name="query-rule"></a>Regra de consulta

Atualize dinamicamente a associação de uma coleção com base numa consulta com o Configuration Manager com base numa agenda. Por exemplo, pode criar uma coleção de utilizadores que são membros da unidade organizacional Recursos Humanos nos Serviços de Domínio do Active Directory. Esta coleção é atualizada automaticamente quando novos utilizadores são adicionados ou removidos da unidade organizacional recursos humanos.

Por exemplo consultas que pode utilizar para criar coleções, consulte [como criar consultas](/sccm/core/servers/manage/create-queries).


### <a name="device-category-rule"></a>Regra de categoria de dispositivo

Pode facilitar a gestão dos seus dispositivos ao associar categorias de dispositivos com as coleções de dispositivos. 

Para obter mais informações, consulte [automaticamente categorizar dispositivos em coleções](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections).<!-- SCCMDocs issue 552 -->


### <a name="include-collection-rule"></a>Regra de inclusão de coleção

Inclua os membros de outra coleção numa coleção do Configuration Manager. Se a coleção incluída for alterada, o Configuration Manager atualiza a associação da coleção atual num agendamento.

Pode adicionar várias regras de inclusão de coleção a uma coleção.


### <a name="exclude-collection-rule"></a>Regra de exclusão de coleção

A regra de exclusão de coleção permitem-lhe excluir os membros de outra coleção a partir de uma coleção do Configuration Manager. Se a coleção excluída for alterada, o Configuration Manager atualiza a associação da coleção atual num agendamento.

Pode adicionar várias regras de exclusão de coleção a uma coleção. Se uma coleção inclui ambos incluem a coleção e excluir regras de recolha e existe um conflito, a regra de exclusão de coleção tem prioridade.

#### <a name="example"></a>Exemplo
Criar uma coleção que tem uma regra de recolha e uma coleção regra de exclusão de inclusão. A regra de inclusão de coleção destina-se a uma coleção de computadores de secretária Dell. A exclusão de coleção destina-se uma coleção de computadores que têm menos de 4 GB de RAM. A nova coleção contém os computadores de secretária Dell que tenham, pelo menos, 4 GB de RAM.



## <a name="bkmk_create"></a> Criar uma coleção  

1. Na consola do Configuration Manager, vá para o **ativos e compatibilidade** área de trabalho.  

    - Para criar uma *coleção de dispositivos*, selecione a **coleções de dispositivos** nó. Em seguida, no **home page** separador do Friso, no **Create** de grupo, selecione **criar coleção de dispositivos**.  

    - Para criar uma *coleção de utilizadores*, selecione a **coleções de utilizadores** nó. Em seguida, no **home page** separador do Friso, na **Create** de grupo, escolha **criar coleção de utilizadores**.  

2. Sobre o **gerais** página do assistente, forneça um **nome** e um **comentário**. Na **coleção restritiva** secção, escolha **procurar**e selecione uma coleção restritiva. A coleção que está a criar irá conter apenas membros da coleção restritiva.  

4. No **regras de associação** página, além do **Adicionar regra** , selecione o tipo de regra de associação que pretende utilizar para esta coleção. Pode configurar várias regras para cada coleção. A configuração para cada regra varia. Para obter mais informações sobre como configurar cada regra, consulte as secções seguintes:  
    - [Regra direta](#bkmk-direct)
    - [Regra de consulta](#bkmk-query)
    - [Regra de categoria de dispositivo](#bkmk-category)
    - [Coleção de regra de inclusão](#bkmk-include)
    - [Regra de coleção de exclusão](#bkmk-exclude)

5. Além disso, no **regras de associação** , reveja as seguintes definições:

    - **Utilizar atualizações incrementais para esta coleção**: Selecione esta opção para procurar e atualizar recursos apenas novos ou alterados a partir da avaliação de coleção anterior de periodicamente. Este processo é independente de uma avaliação de coleção completa. Por predefinição, as atualizações incrementais ocorrem em intervalos de 5 minutos.  

        > [!IMPORTANT]  
        >  Coleções com regras de consulta que utilizem as classes seguintes não suportam atualizações incrementais:  
        >   
        > -   SMS_G_System_CollectedFile  
        > -   SMS_G_System_LastSoftwareScan  
        > -   SMS_G_System_AppClientState  
        > -   SMS_G_System_DCMDeploymentState  
        > -   SMS_G_System_DCMDeploymentErrorAssetDetails  
        > -   SMS_G_System_DCMDeploymentCompliantAssetDetails  
        > -   SMS_G_System_DCMDeploymentNonCompliantAssetDetails  
        > -   SMS_G_User_DCMDeploymentCompliantAssetDetails (apenas para coleções de utilizadores)  
        > -   SMS_G_User_DCMDeploymentNonCompliantAssetDetails (apenas para coleções de utilizadores)  
        > -   SMS_G_System_SoftwareUsageData  
        > -   SMS_G_System_CI_ComplianceState  
        > -   SMS_G_System_EndpointProtectionStatus  
        > -   SMS_GH_System_*  
        > -   SMS_GEH_System_*  

    - **Agendar uma atualização completa para esta coleção**: Agende uma avaliação completa regular da associação à coleção.  

        A partir da versão 1810, as seguintes alterações no comportamento de avaliação de coleção podem melhorar o desempenho do site:<!--3607726-->  

        - Anteriormente, quando tiver configurado uma agenda numa coleção com base na consulta, o site continuaria a avaliar a consulta quer ou não tiver ativado a definição de coleção para **agendar uma atualização completa para esta coleção**. Para desabilitar totalmente a agenda, era necessário que alterar a agenda para **None**. 

            Agora o site limpa a agenda quando desativar esta definição. Para especificar uma agenda para avaliação de coleção, ative a opção para **agendar uma atualização completa para esta coleção**.  

            Quando atualiza o seu site, para uma coleção existente em que especificou uma agenda, o site ativa a opção para **agendar uma atualização completa para esta coleção**. Embora esta configuração não pode ser sua intenção, foi o comportamento real. Para parar o site avaliar uma coleção com base numa agenda, desative esta opção.  

        - Não é possível desativar a avaliação de coleções incorporadas, como **todos os sistemas**, mas agora pode configurar a agenda. Este comportamento permite-lhe personalizar esta ação ao mesmo tempo que cumpre os seus requisitos. 

            > [!Tip]  
            > Alterar apenas a **tempo** da agenda personalizada em coleções incorporadas. Não altere os **padrão de periodicidade**. Iterações futuras podem impor um padrão de periodicidade específico.  

6. Conclua o assistente para criar a nova coleção. A nova coleção é apresentada no nó **Coleções de Dispositivos** da área de trabalho **Ativos e Compatibilidade** .  

> [!NOTE]  
> É necessário atualizar ou recarregar a consola do Configuration Manager para ver os membros da coleção. Não são apresentados na coleção após a primeira atualização agendada. Pode selecionar manualmente **associação de atualização** para a coleção. Pode demorar alguns minutos para concluir uma atualização da coleção.  

        
### <a name="bkmk-direct"></a> Configurar uma regra direta  

1. Na página **Procurar Recursos** do **Assistente para Criar Regra de Associação Direta**, especifique as seguintes informações:  

    - **Classe de recursos**: Selecione o tipo de recurso que pretende procurar e adicionar à coleção. Por exemplo, 
        - **Recursos de sistema**: Procurar dados de inventário devolvidos de computadores cliente
        - **Computadores desconhecidos**: Selecione entre os valores devolvidos por computadores desconhecidos
        - **Recurso de utilizador**: Pesquisar informações de utilizador recolhidas pelo Configuration Manager
        - **Recursos do grupo de utilizadores**: Procurar informações de grupo de utilizador recolhidas pelo Configuration Manager

    - **Nome de atributo**: Selecione o atributo associado à classe de recursos selecionada que pretende procurar. Por exemplo,  

        - Se pretender selecionar computadores pelo respetivo nome NetBIOS, selecione **recurso do sistema** no **classe de recursos** lista e **nome NetBIOS** no **nome de atributo**  lista.  

        - Se pretender selecionar utilizadores pelo respetivo nome de unidade organizacional (UO), selecione **recurso de utilizador** no **classe de recursos** lista e **nome da UO de utilizador** no  **Nome de atributo** lista.  

    - **Excluir recursos marcados como obsoletos**: Se um computador cliente estiver marcado como obsoleto, não inclua este valor nos resultados da pesquisa.  

    - **Excluir recursos que não têm o cliente do Configuration Manager instalado**: Estes recursos não ser apresentados nos resultados da pesquisa.  

    - **Valor**: Introduza um valor para procurar o nome de atributo selecionado. Utilizar o caráter de percentagem `%` como caráter universal. Por exemplo,  
        - Para procurar computadores que tenham um nome NetBIOS que começa com "M", introduza `M%` neste campo.  
        - Para procurar utilizadores na UO Contoso, introduza `Contoso` neste campo.

2. Sobre o **selecionar recursos** página, selecione os recursos que pretende adicionar à coleção na **recursos** lista e, em seguida, escolha **seguinte**.  


### <a name="bkmk-query"></a> Configurar uma regra de consulta  

Na caixa de diálogo **Propriedades da Regra de Consulta** , especifique as seguintes informações:  

- **Nome**: Especifique um nome exclusivo para a consulta.  

- **Importar instrução de consulta**: Abre o **procurar consulta** caixa de diálogo. Selecione um [Configuration Manager consulta](/sccm/core/servers/manage/create-queries) para utilizar como regra de consulta para a coleção.   

- **Classe de recursos**: Selecione o tipo de recurso que pretende procurar e adicionar à coleção. Selecione um valor entre os valores de **Recurso do Sistema** para procurar dados de inventário devolvidos de computadores cliente ou **Computador Desconhecido** para selecionar entre os valores devolvidos por computadores desconhecidos.  

- **Editar instrução de consulta**: Abre o **propriedades da instrução de consulta** caixa de diálogo onde pode criar uma consulta para utilizar como regra para a coleção. Para obter mais informações sobre consultas, consulte [referência técnica consultas](/sccm/core/servers/manage/queries-technical-reference).  


### <a name="bkmk-category"></a> Regra de categoria de dispositivo

As ações seguintes estão disponíveis no **selecionar categorias de dispositivos** janela:

- **Criar**: Especifique um nome para criar uma nova categoria
- **Mudar o nome**: Mudar o nome da categoria selecionada
- **Delete**: Selecione uma ou mais categorias e utilize esta ação para removê-los a partir da lista

Para obter mais informações, consulte [automaticamente categorizar dispositivos em coleções](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections).<!-- SCCMDocs issue 552 -->


### <a name="bkmk-include"></a> Configurar uma regra de inclusão de coleção  

Na **selecionar coleções** caixa de diálogo caixa, selecione as coleções que pretende incluir na nova coleção, em seguida, escolha **OK**.  


### <a name="bkmk-exclude"></a> Configurar uma regra de exclusão de coleção  

Na **selecionar coleções** caixa de diálogo caixa, selecione as coleções que pretende excluir da nova coleção, em seguida, escolha **OK**.  



## <a name="bkmk_import"></a> Importar uma coleção  

Quando exportar uma coleção a partir de um site, o Configuration Manager guarda-lo como um ficheiro de formato (MOF) do objeto gerido. Utilize este procedimento para importar esse ficheiro para a base de dados do site. Precisa **criar** permissões na classe de coleções. 

> [!Important]  
> - Certifique-se de que o ficheiro só contém dados de coleção, é de uma origem fidedigna e ainda não adulterado.  
> 
> - Certifique-se de que o ficheiro foi exportado a partir de um site com a mesma versão do Configuration Manager.  

Para obter mais informações sobre a exportação de coleções, consulte [como gerir coleções](/sccm/core/clients/manage/collections/manage-collections).


1. Na consola do Configuration Manager, vá para o **ativos e compatibilidade** área de trabalho. Selecione o **coleções de utilizadores** ou **coleções de dispositivos** nó.  

2. No **home page** separador do Friso, no **Create** de grupo, escolha **importar coleções**.  

3. Na **gerais** página do **Assistente Importar coleções**, escolha **seguinte**.  

4. Sobre o **nome do ficheiro MOF** página, selecione **procurar**. Navegue para o ficheiro MOF que contém as informações da coleção que pretende importar.  

5. Conclua o assistente para importar a coleção. A nova coleção é apresentada no nó **Coleções de Utilizadores** ou **Coleções de Dispositivos** da área de trabalho **Ativos e Compatibilidade** . Atualizar ou recarregar a consola do Configuration Manager para ver os membros da coleção para a coleção recentemente importada.  

