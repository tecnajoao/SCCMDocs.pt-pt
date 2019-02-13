---
title: Configurar a administração baseada em funções
titleSuffix: Configuration Manager
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 57413dd3-b2f8-4a5f-b27f-8464d357caff
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 554e67e171fe5b800d231d257105531dcd633baf
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56131579"
---
# <a name="configure-role-based-administration-for-configuration-manager"></a>Configurar a administração baseada em funções para o Configuration Manager   

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

No Configuration Manager, a administração baseada em funções combina funções de segurança, âmbitos de segurança e coleções atribuídas para definir o âmbito administrativo de cada utilizador administrativo. Um âmbito administrativo inclui os objetos que um utilizador administrativo pode ver na consola do Configuration Manager e as tarefas relacionadas com esses objetos que o utilizador administrativo tem permissão para executar. As configurações de administração baseadas em funções são aplicadas em cada site de uma hierarquia.  

 Se não estiver familiarizado com conceitos para a administração baseada em funções, veja [Noções básicas da administração baseada em funções](/sccm/core/understand/fundamentals-of-role-based-administration).  

 As informações nos procedimentos seguintes podem ajudá-lo a criar e configurar a administração baseada em funções e as definições de segurança relacionadas:  

-   [Criar funções de segurança personalizadas](#BKMK_CreateSecRole)  

-   [Configurar funções de segurança](#BKMK_ConfigSecRole)  

-   [Configurar âmbitos de segurança para um objeto](#BKMK_ConfigSecScope)  

-   [Configurar coleções para gerir a segurança](#BKMK_ConfigColl)  

-   [Criar um novo utilizador administrativo](#BKMK_Create_AdminUser)  

-   [Modificar o âmbito administrativo de um utilizador administrativo](#BKMK_ModAdminUser)  

##  <a name="BKMK_CreateSecRole"></a> Criar funções de segurança personalizadas  
 O Configuration Manager fornece várias funções de segurança incorporadas. Se precisar de funções de segurança adicionais, poderá criar uma função de segurança personalizada fazendo uma cópia de uma função existente e modificando-a em seguida. Pode criar uma função de segurança personalizada para conceder aos utilizadores administrativos as permissões de segurança adicionais que necessitam que não estão incluídos numa função de segurança atualmente atribuída. Ao utilizar uma função de segurança personalizada, poderá conceder-lhes apenas as permissões de que necessitam, sem ter de atribuir uma função de segurança que conceda permissões adicionais.  

 Utilize o procedimento seguinte para criar uma nova função de segurança utilizando uma função de segurança existente como modelo.  

#### <a name="to-create-custom-security-roles"></a>Para criar funções de segurança personalizadas  

1.  Na consola do Configuration Manager, aceda a **administração**.  

2.  Na **Administration** área de trabalho, expanda **segurança**e, em seguida, escolha **funções de segurança**.  

     Utilize um dos seguintes processos para criar a nova função de segurança:  

    -   Para criar uma nova função de segurança personalizada, execute as seguintes ações:  

        1.  Selecione uma função de segurança existente para utilizar como origem da nova função de segurança.  

        2.  Sobre o **home page** separador a **função de segurança** de grupo, escolha **cópia**. Esta ação cria uma cópia da função de segurança de origem.  

        3.  No assistente Copiar Função de Segurança, especifique um **Nome** para a nova função de segurança personalizada.  

        4.  Em **Atribuições de operações de segurança**, expanda cada nó **Operações de Segurança** para apresentar as ações disponíveis.  

        5.  Para alterar a definição de uma operação de segurança, selecione a seta para baixo na **valor** coluna e escolha o **Sim** ou **não**.  

            > [!CAUTION]  
            >  Ao configurar uma função de segurança personalizada, certifique-se de que não conceda permissões que não são necessárias por utilizadores administrativos que estão associados a nova função de segurança. Por exemplo, o **Modify** valor para o **funções de segurança** operação de segurança concede a utilizadores administrativos a permissão para editar qualquer função de segurança acessível – mesmo que eles não estão associados a que função de segurança.  

        6.  Depois de configurar as permissões, escolha **OK** para guardar a nova função de segurança.  

    -   Para importar uma função de segurança que tenha sido exportada de outra hierarquia do Configuration Manager, execute as seguintes ações:  

        1.  Sobre o **home page** separador a **criar** de grupo, escolha **importar função de segurança**.  

        2.  Especifique o ficheiro. XML que contém a configuração de função de segurança que pretende importar. Escolher **aberto** para concluir o procedimento e guardar a função de segurança.  

            > [!NOTE]  
            >  Após importar uma função de segurança, poderá editar as propriedades da mesma para alterar as permissões de objetos associadas à função.  

##  <a name="BKMK_ConfigSecRole"></a> Configurar funções de segurança  
 Os grupos de permissões de segurança definidos para uma função de segurança são designados atribuições de operações de segurança. As atribuições de operações de segurança representam uma combinação de tipos de objetos e ações disponíveis para cada tipo de objeto. Pode modificar as operações de segurança estão disponíveis para qualquer função de segurança personalizada, mas não é possível modificar as funções de segurança incorporadas que o Configuration Manager fornece.  

 Utilize o procedimento seguinte para modificar as operações de segurança de uma função de segurança.  

#### <a name="to-modify-security-roles"></a>Para modificar funções de segurança  

1.  Na consola do Configuration Manager, escolha **administração**.  

2.  Na **Administration** área de trabalho, expanda **segurança**e, em seguida, escolha **funções de segurança**.  

3.  Selecione a função de segurança personalizada que pretende modificar.  

4.  Sobre o **home page** separador a **propriedades** de grupo, escolha **propriedades**.  

5.  Escolha o **permissões** separador.  

6.  Em **Atribuições de operações de segurança**, expanda cada nó **Operações de Segurança** para apresentar as ações disponíveis.  

7.  Para alterar a definição de uma operação de segurança, selecione a seta para baixo na **valor** coluna e, em seguida, escolhem **Sim** ou **não**.  

    > [!CAUTION]  
    >  Ao configurar uma função de segurança personalizada, certifique-se de que não conceda permissões que não são necessárias por utilizadores administrativos que estão associados a nova função de segurança. Por exemplo, o **Modify** valor para o **funções de segurança** operação de segurança concede a utilizadores administrativos a permissão para editar qualquer função de segurança acessível – mesmo que eles não estão associados a que função de segurança.  

8.  Quando tiver terminado de configurar atribuições de operações de segurança, escolha **OK** para guardar a nova função de segurança.  

##  <a name="BKMK_ConfigSecScope"></a> Configurar âmbitos de segurança para um objeto  
 Gerir a associação de um âmbito de segurança para um objeto do objeto – não do âmbito de segurança. As únicas configurações diretas suportadas pelos âmbitos de segurança são as alterações ao respetivo nome e descrição. Para alterar o nome e descrição de um âmbito de segurança ao visualizar as propriedades do âmbito, terá de possuir a permissão **Modificar** no objeto com capacidade de segurança **Âmbitos de Segurança** .  

 Quando cria um novo objeto no Configuration Manager, está associado a cada âmbito de segurança que está associada às funções de segurança da conta utilizada para criar o objeto. Este comportamento ocorre quando esses âmbitos de segurança fornecem a **Create** permissão ou **definir âmbito de segurança** permissão. Pode alterar os âmbitos de segurança para o objeto depois de o criar.  

 Por exemplo, estiver atribuído uma função de segurança que lhe concede permissão para criar um novo grupo de limites. Quando cria um novo grupo de limites, não terá nenhuma opção que pode atribuir âmbitos de segurança específicos para. Em vez disso, os âmbitos de segurança que estão disponíveis a partir de funções de segurança que o utilizador está associado são automaticamente atribuídos ao novo grupo de limites. Depois de guardar o novo grupo de limites, é possível editar os âmbitos de segurança que estão associados ao novo grupo de limites.  

 Utilize o procedimento seguinte para configurar os âmbitos de segurança que são atribuídos a um objeto.  

#### <a name="to-configure-security-scopes-for-an-object"></a>Para configurar âmbitos de segurança para um objeto  

1.  Na consola do Configuration Manager, selecione um objeto que suporte a serem atribuídas a um âmbito de segurança.  

2.  Sobre o **home page** separador a **classificar** de grupo, escolha **definir âmbitos de segurança**.  

3.  Na caixa de diálogo **Definir Âmbitos de Segurança** , selecione ou desmarque os âmbitos de segurança a que este objeto se encontra associado. Cada objeto que suporte âmbitos de segurança tem de ser atribuído a pelo menos um âmbito de segurança.  

4.  Escolher **OK** para guardar os âmbitos de segurança atribuídas.  

    > [!NOTE]  
    >  Ao criar um novo objeto, poderá atribuir o objeto a vários âmbitos de segurança. Para modificar o número de âmbitos de segurança que estão associados com o objeto, tem de alterar esta atribuição após a criação do objeto.  

##  <a name="BKMK_ConfigColl"></a> Configurar coleções para gerir a segurança  
 Não existem procedimentos para configurar coleções para administração baseada em funções. As coleções não têm uma configuração de administração baseada em funções. Em vez disso, são atribuídas a um utilizador administrativo quando configurar o utilizador administrativo. As operações de segurança de coleção ativadas nas funções de segurança atribuído ao utilizador determinam as permissões que um utilizador administrativo possui para coleções e recursos de coleção (membros da coleção).  

 Quando um utilizador administrativo tem permissões para uma coleção, também tem permissões para coleções que estejam limitadas a essa coleção. Por exemplo, a sua organização utiliza uma coleção designada todas as áreas de trabalho. Também há uma coleção denominada todas áreas de trabalho da América do Norte é limitado à coleção de todos os ambientes de trabalho. Se um utilizador administrativo tiver permissões para Todos os Ambientes de Trabalho, também terá as mesmas permissões para a coleção Todos os Ambientes de Trabalho da América do Norte.

 Além disso, um utilizador administrativo não é possível utilizar o **elimine** ou **modificar** permissão numa coleção que lhe esteja diretamente atribuída aos mesmos. No entanto, eles podem utilizar essas permissões nas coleções que estejam limitadas a essa coleção. No exemplo anterior, o utilizador administrativo pode eliminar ou modificar a coleção de todas as áreas de trabalho América do Norte, mas eles não é possível eliminar ou modificar a coleção de todas as áreas de trabalho.  

##  <a name="BKMK_Create_AdminUser"></a> Criar um novo utilizador administrativo  
 Para conceder a utilizadores individuais ou membros de um grupo de segurança de acesso para gerir o Gestor de configuração, crie um utilizador administrativo no Configuration Manager e especificar a conta do Windows do utilizador ou grupo de utilizadores. Cada utilizador administrativo no Configuration Manager tem de ser atribuído pelo menos uma função de segurança e um âmbito de segurança. Também é possível atribuir coleções para limitar o âmbito administrativo do utilizador administrativo.  

 Utilize os procedimentos seguintes para criar novos utilizadores administrativos.  

#### <a name="to-create-a-new-administrative-user"></a>Para criar um novo utilizador administrativo  

1.  Na consola do Configuration Manager, escolha **administração**.  

2.  Na **Administration** área de trabalho, expanda **segurança**e, em seguida, escolha **utilizadores administrativos**.  

3.  Na **home page** separador a **Create** de grupo, escolha **adicionar utilizador ou grupo**.  

4.  Escolher **procurar**e, em seguida, selecione a conta de utilizador ou grupo a utilizar para este novo utilizador administrativo.  

    > [!NOTE]  
    >  Para a administração baseada em consolas, apenas podem ser especificados utilizadores de domínio ou grupos de segurança como utilizadores administrativos.  

5.  Para **funções de segurança associadas**, escolha **Add** para abrir uma lista de funções de segurança disponíveis, selecione a caixa para uma ou mais funções de segurança e, em seguida, escolha **OK**.  

6.  Escolha uma das duas opções seguintes para definir o comportamento de objeto com capacidade de segurança para o novo utilizador:  

    -   **Todas as instâncias dos objetos que estão relacionados com as funções de segurança atribuídas**: Esta opção associa o utilizador administrativo com o **todos os** âmbito de segurança e o **todos os sistemas** e **todos os utilizadores e grupos de utilizadores** coleções. As funções de segurança atribuídas ao utilizador definem o acesso aos objetos. Os novos objetos criados por este utilizador administrativo são atribuídos ao âmbito de segurança **Predefinido** .  

    -   **Apenas as instâncias de objetos que estão atribuídos a coleções e âmbitos de segurança especificados**: Por predefinição, esta opção associa o utilizador administrativo com o **predefinição** âmbito de segurança e o **todos os sistemas** e **todos os utilizadores e grupos de utilizadores** coleções. No entanto, os âmbitos de segurança e coleções reais estão limitados aos que estão associados à conta utilizada para criar o novo utilizador administrativo. Esta opção suporta a adição ou remoção de âmbitos de segurança e de coleções para personalizar o âmbito administrativo do utilizador administrativo.  

    > [!IMPORTANT]  
    >  As opções anteriores associam cada âmbito de segurança atribuído e a coleção para cada função de segurança que é atribuída ao utilizador administrativo. Pode utilizar uma terceira opção, **associar atribuídos a coleções e âmbitos de segurança específicos**, para associar funções de segurança individuais a coleções e âmbitos de segurança específicos. Esta terceira opção está disponível após a criação do novo utilizador administrativo, quando este é modificado.  

7.  Dependendo da seleção no passo 6, execute a ação seguinte:  

    -   Se tiver selecionado **todas as instâncias dos objetos que estão relacionados com as funções de segurança atribuídas**, escolha **OK** para concluir este procedimento.  

    -   Se tiver selecionado **apenas as instâncias de objetos que estão atribuídos a coleções e âmbitos de segurança especificados**, pode escolher **Add** para selecionar coleções e âmbitos de segurança adicionais. Ou selecione um ou mais objetos na lista e, em seguida, escolha **remover** para removê-los. Escolher **OK** para concluir este procedimento.  

##  <a name="BKMK_ModAdminUser"></a> Modificar o âmbito administrativo de um utilizador administrativo  
 Para modificar o âmbito administrativo de um utilizador administrativo, adicione ou remova funções de segurança, âmbitos de segurança e coleções que estejam associados ao utilizador. Cada utilizador administrativo tem de estar associado, pelo menos, a uma função de segurança e a um âmbito de segurança. Poderá ser necessário atribuir uma ou mais coleções ao âmbito administrativo do utilizador. A maioria das funções de segurança interagem com coleções e não a função corretamente sem uma coleção atribuída.  

 Quando modifica um utilizador administrativo, pode alterar o comportamento para a forma como os objetos com capacidade de segurança são associados às funções de segurança atribuídas. Os três comportamentos que pode selecionar são os seguintes:  

-   **Todas as instâncias dos objetos que estão relacionados com as funções de segurança atribuídas**: Esta opção associa o utilizador administrativo com o **todos os** escopo e o **todos os sistemas** e **todos os utilizadores e grupos de utilizadores** coleções. As funções de segurança atribuídas ao utilizador definem o acesso aos objetos.  

-   **Apenas as instâncias de objetos que estão atribuídos a coleções e âmbitos de segurança especificados**: Esta opção associa o utilizador administrativo aos mesmos âmbitos de segurança e coleções que estão associadas à conta que utilizar para configurar o utilizador administrativo. Esta opção suporta a adição ou remoção de funções de segurança e de coleções para personalizar o âmbito administrativo do utilizador administrativo.  

-   **Associar funções de segurança atribuídas a coleções e âmbitos de segurança específicos**: Esta opção permite criar associações específicas entre funções de segurança individuais e coleções para o utilizador e âmbitos de segurança específicos.  

    > [!NOTE]  
    >  Esta opção está disponível apenas quando modificar as propriedades de um utilizador administrativo.  

A configuração atual do comportamento do objeto com capacidade de segurança altera o processo utilizado para atribuir funções de segurança adicionais. Utilize os procedimentos seguintes que são baseados nas diferentes opções para objetos com capacidade de segurança para o ajudar a gerir um utilizador administrativo.  

Utilize o procedimento seguinte para ver e gerir a configuração dos objetos com capacidade de segurança para um utilizador administrativo.  

#### <a name="to-view-and-manage-the-securable-object-behavior-for-an-administrative-user"></a>Para ver e gerir o comportamento de objetos com capacidade de segurança de um utilizador administrativo  

1.  Na consola do Configuration Manager, escolha **administração**.  

2.  Na **Administration** área de trabalho, expanda **segurança**e, em seguida, escolha **utilizadores administrativos**.  

3.  Selecione o utilizador administrativo que pretende modificar.  

4.  Sobre o **home page** separador a **propriedades** de grupo, escolha **propriedades**.  

5.  Escolha o **âmbitos de segurança** separador para ver a configuração atual dos objetos com capacidade para este utilizador administrativo.  

6.  Para modificar o comportamento do objeto com capacidade de segurança, selecione uma nova opção para o comportamento do objeto com capacidade de segurança. Depois de alterar esta configuração, consulte o procedimento adequado para obter orientações adicionais para configurar âmbitos de segurança e coleções e funções de segurança para este utilizador administrativo.  

7.  Escolher **OK** para concluir o procedimento.  

Utilize o procedimento seguinte para modificar um utilizador administrativo que tem o comportamento de objeto com capacidade de segurança definido **todas as instâncias dos objetos que estão relacionados com as funções de segurança atribuídas**.  

#### <a name="for-option-all-instances-of-the-objects-that-are-related-to-the-assigned-security-roles"></a>Para a opção: Todas as instâncias dos objetos que estão relacionados com as funções de segurança atribuídas  

1.  Na consola do Configuration Manager, escolha **administração**.  

2.  Na **Administration** área de trabalho, expanda **segurança**e, em seguida, escolha **utilizadores administrativos**.  

3.  Selecione o utilizador administrativo que pretende modificar.  

4.  Sobre o **home page** separador a **propriedades** de grupo, escolha **propriedades**.  

5.  Escolha o **âmbitos de segurança** separador para confirmar que o utilizador administrativo está configurado para **todas as instâncias dos objetos que estão relacionados com as funções de segurança atribuídas**.  

6.  Para modificar as funções de segurança atribuídas, escolha o **funções de segurança** separador.  

    -   Para atribuir funções de segurança adicionais a este utilizador administrativo, escolha **Add**, selecione a caixa para cada função de segurança adicional que pretende atribuir e, em seguida, escolha **OK**.  

    -   Para remover funções de segurança, selecione uma ou mais funções de segurança a partir da lista e, em seguida, escolha **remover**.  

7.  Para modificar o comportamento de objeto com capacidade de segurança, escolha o **âmbitos de segurança** separador e escolha uma nova opção para o comportamento do objeto com capacidade de segurança. Depois de alterar esta configuração, consulte o procedimento adequado para obter orientações adicionais para configurar âmbitos de segurança e coleções e funções de segurança para este utilizador administrativo.  

    > [!NOTE]  
    >  Quando o comportamento do objeto com capacidade de segurança está definido como **todas as instâncias dos objetos que estão relacionados com as funções de segurança atribuídas**, é possível adicionar ou remover coleções e âmbitos de segurança específicos.  

8.  Escolher **OK** para concluir este procedimento.  

Utilize o procedimento seguinte para modificar um utilizador administrativo que tem o comportamento de objeto com capacidade de segurança definido **apenas as instâncias de objetos que estão atribuídos a coleções e âmbitos de segurança especificados**.  

#### <a name="for-option-only-the-instances-of-objects-that-are-assigned-to-the-specified-security-scopes-and-collections"></a>Para a opção: Apenas as instâncias de objetos que estão atribuídos a coleções e âmbitos de segurança especificados  

1.  Na consola do Configuration Manager, escolha **administração**.  

2.  Na **Administration** área de trabalho, expanda **segurança**e, em seguida, escolha **utilizadores administrativos**.  

3.  Selecione o utilizador administrativo que pretende modificar.  

4.  Sobre o **home page** separador a **propriedades** de grupo, escolha **propriedades**.  

5.  Escolha o **âmbitos de segurança** separador para confirmar que o utilizador está configurado para **apenas as instâncias de objetos que estão atribuídos a coleções e âmbitos de segurança especificados**.  

6.  Para modificar as funções de segurança atribuídas, escolha o **funções de segurança** separador.  

    -   Para atribuir funções de segurança adicionais a este utilizador, escolha **Add**, selecione a caixa para cada função de segurança adicional que pretende atribuir e, em seguida, escolha **OK**.  

    -   Para remover funções de segurança, selecione uma ou mais funções de segurança a partir da lista e, em seguida, escolha **remover**.  

7.  Para modificar as coleções que estão associadas a funções de segurança e âmbitos de segurança, escolha o **âmbitos de segurança** separador.  

    -   Para associar novos âmbitos de segurança ou coleções a todas as funções de segurança que são atribuídas a este utilizador administrativo, escolha **adicionar** e selecione uma das quatro opções. Se selecionou **âmbito de segurança** ou **coleção**, selecione a caixa para um ou mais objetos concluir a seleção e, em seguida, escolha **OK**.  

    -   Para remover um âmbito de segurança ou uma coleção, escolha o objeto e, em seguida, escolha **remover**.  

8.  Escolher **OK** para concluir este procedimento.  

Utilize o procedimento seguinte para modificar um utilizador administrativo que tem o comportamento de objeto com capacidade de segurança definido **associar atribuídos a coleções e âmbitos de segurança específicos**.  

#### <a name="for-option-associate-assigned-security-roles-with-specific-security-scopes-and-collections"></a>Para a opção: Associar funções de segurança atribuídas a coleções e âmbitos de segurança específicos  

1.  Na consola do Configuration Manager, escolha **administração**.  

2.  Na **Administration** área de trabalho, expanda **segurança**e, em seguida, escolha **utilizadores administrativos**.  

3.  Selecione o utilizador administrativo que pretende modificar.  

4.  Sobre o **home page** separador a **propriedades** de grupo, escolha **propriedades**.  

5.  Escolha o **âmbitos de segurança** separador para confirmar que o utilizador administrativo está configurado para **associar atribuídos a coleções e âmbitos de segurança específicos**.  

6.  Para modificar as funções de segurança atribuídas, escolha o **funções de segurança** separador.  

    -   Para atribuir funções de segurança adicionais a este utilizador administrativo, escolha **adicionar**. Sobre o **Adicionar função de segurança** caixa de diálogo, selecione um ou mais disponíveis funções de segurança, escolha **adicionar**e selecione um tipo de objeto para associar às funções de segurança selecionado. Se selecionou **âmbito de segurança** ou **coleção**, selecione a caixa para um ou mais objetos concluir a seleção e, em seguida, escolha **OK**.  

        > [!NOTE]  
        >  Tem de configurar, pelo menos, um âmbito de segurança para que as funções de segurança selecionadas possam ser atribuídas ao utilizador administrativo. Quando seleciona várias funções de segurança, cada coleção e âmbito de segurança que configura são associados a cada um dos perfis de segurança selecionados.  

    -   Para remover funções de segurança, selecione uma ou mais funções de segurança a partir da lista e, em seguida, escolha **remover**.  

7.  Para modificar as coleções que estão associadas uma função de segurança específicas e os âmbitos de segurança, escolha o **âmbitos de segurança** separador, selecione a função de segurança e, em seguida, escolha **editar**.  

    -   Para associar novos objetos esta função de segurança, escolha **adicionar**e selecione um tipo de objeto para associar às funções de segurança selecionado. Se selecionou **âmbito de segurança** ou **coleção**, selecione a caixa para um ou mais objetos concluir a seleção e, em seguida, escolha **OK**.  

        > [!NOTE]  
        >  Tem de configurar, pelo menos, um âmbito de segurança.  

    -   Para remover um âmbito de segurança ou uma coleção que está associada esta função de segurança, selecione o objeto e, em seguida, escolha **remover**.  

    -   Quando tiver terminado a modificação dos objetos associados, escolha **OK**.  

8.  Escolher **OK** para concluir este procedimento.  

    > [!CAUTION]  
    >  Quando uma função de segurança concede a utilizadores administrativos a permissão de implementação de coleção, esses utilizadores administrativos podem distribuir objetos de qualquer âmbito de segurança para o qual possuam permissões de **leitura** de objetos, mesmo que esse âmbito de segurança esteja associado a outra função de segurança.  
