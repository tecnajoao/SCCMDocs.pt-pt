---
title: "Configurar a administração baseada em funções | Documentos do Microsoft"
ms.custom: na
ms.date: 2/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 57413dd3-b2f8-4a5f-b27f-8464d357caff
caps.latest.revision: 7
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 1defe96163f1bb70f586619ad89098c6f0e6c665
ms.openlocfilehash: 3eea3a6e5f23808570ded4be3bd7412954518b96
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---

# <a name="configure-role-based-administration-for-system-center-configuration-manager"></a>Configurar a administração baseada em funções para o System Center Configuration Manager   

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

No System Center Configuration Manager, a administração baseada em funções combina funções de segurança, âmbitos de segurança e coleções atribuídas para definir o âmbito administrativo para cada utilizador administrativo. Um âmbito administrativo inclui os objetos que um utilizador administrativo pode ver na consola do Configuration Manager e as tarefas relacionadas com esses objetos que o utilizador administrativo tem permissão para executar. As configurações de administração baseadas em funções são aplicadas em cada site de uma hierarquia.  

 Se não estiver familiarizado com conceitos para a administração baseada em funções, consulte o artigo [Noções básicas da administração baseada em funções para o System Center Configuration Manager](../../../../core/understand/fundamentals-of-role-based-administration.md).  

 As informações dos procedimentos seguintes podem ajudar a criar e configurar a administração baseada em funções e as definições de segurança associadas:  

-   [Criar funções de segurança personalizadas](#BKMK_CreateSecRole)  

-   [Configurar funções de segurança](#BKMK_ConfigSecRole)  

-   [Configurar âmbitos de segurança para um objeto](#BKMK_ConfigSecScope)  

-   [Configurar coleções para gerir a segurança](#BKMK_ConfigColl)  

-   [Criar um novo utilizador administrativo](#BKMK_Create_AdminUser)  

-   [Modificar o âmbito administrativo de um utilizador administrativo](#BKMK_ModAdminUser)  

##  <a name="BKMK_CreateSecRole"></a> Criar funções de segurança personalizadas  
 O Configuration Manager oferece várias funções de segurança incorporadas. Se precisar de funções de segurança adicionais, poderá criar uma função de segurança personalizada fazendo uma cópia de uma função existente e modificando-a em seguida. Poderá criar uma função de segurança personalizada para conceder aos utilizadores administrativos as permissões de segurança adicional que necessitem e que não estão incluídas na função de segurança atualmente atribuída. Ao utilizar uma função de segurança personalizada, poderá conceder-lhes apenas as permissões de que necessitam, sem ter de atribuir uma função de segurança que conceda permissões adicionais.  

 Utilize o procedimento seguinte para criar uma nova função de segurança utilizando uma função de segurança existente como modelo.  

#### <a name="to-create-custom-security-roles"></a>Para criar funções de segurança personalizadas  

1.  Na consola do Configuration Manager, aceda a **administração**.  

2.  No **administração** área de trabalho, expanda **segurança**e, em seguida, escolha **funções de segurança**.  

     Utilize um dos seguintes processos para criar a nova função de segurança:  

    -   Para criar uma nova função de segurança personalizada, execute as seguintes ações:  

        1.  Selecione uma função de segurança existente para utilizar como origem da nova função de segurança.  

        2.  No **base** separador o **função de segurança** grupo, selecione **cópia**. Será criada uma cópia da função de segurança de origem.  

        3.  No assistente Copiar Função de Segurança, especifique um **Nome** para a nova função de segurança personalizada.  

        4.  Em **Atribuições de operações de segurança**, expanda cada nó **Operações de Segurança** para apresentar as ações disponíveis.  

        5.  Para alterar a definição de uma operação de segurança, selecione a seta para baixo no **valor** coluna e selecione **Sim** ou **não**.  

            > [!CAUTION]  
            >  Quando configura uma função de segurança personalizada, certifique-se de que não conceda permissões que não são necessários para os utilizadores administrativos que estão associados a nova função de segurança. Por exemplo, o **modificar** o valor para o **funções de segurança** operação de segurança concede a utilizadores administrativos a permissão para editar qualquer função de segurança acessível – mesmo que não estão associados essa função de segurança.  

        6.  Depois de configurar as permissões, escolher **OK** para guardar a nova função de segurança.  

    -   Para importar uma função de segurança que tenha sido exportada de outra hierarquia do Configuration Manager, execute as seguintes ações:  

        1.  No **base** separador o **criar** grupo, selecione **importar função de segurança**.  

        2.  Especifique o ficheiro. XML que contém a configuração da função de segurança que pretende importar. Escolher **abrir** para concluir o procedimento e guardar a função de segurança.  

            > [!NOTE]  
            >  Após importar uma função de segurança, poderá editar as propriedades da mesma para alterar as permissões de objetos associadas à função.  

##  <a name="BKMK_ConfigSecRole"></a> Configurar funções de segurança  
 Os grupos de permissões de segurança definidos para uma função de segurança são designados atribuições de operações de segurança. As atribuições de operações de segurança representam uma combinação de tipos de objetos e ações disponíveis para cada tipo de objeto. Pode modificar as operações de segurança estão disponíveis para qualquer função de segurança personalizada, mas não é possível modificar as funções de segurança incorporadas que o Configuration Manager oferece.  

 Utilize o procedimento seguinte para modificar as operações de segurança de uma função de segurança.  

#### <a name="to-modify-security-roles"></a>Para modificar funções de segurança  

1.  Na consola do Configuration Manager, escolha **administração**.  

2.  No **administração** área de trabalho, expanda **segurança**e, em seguida, escolha **funções de segurança**.  

3.  Selecione a função de segurança personalizada que pretende modificar.  

4.  No **base** separador o **propriedades** grupo, selecione **propriedades**.  

5.  Escolha o **permissões** separador.  

6.  Em **Atribuições de operações de segurança**, expanda cada nó **Operações de Segurança** para apresentar as ações disponíveis.  

7.  Para alterar a definição de uma operação de segurança, selecione a seta para baixo no **valor** coluna e, em seguida, selecione a **Sim** ou **não**.  

    > [!CAUTION]  
    >  Quando configura uma função de segurança personalizada, certifique-se de que não conceda permissões que não são necessários para os utilizadores administrativos que estão associados a nova função de segurança. Por exemplo, o **modificar** o valor para o **funções de segurança** operação de segurança concede a utilizadores administrativos a permissão para editar qualquer função de segurança acessível – mesmo que não estão associados essa função de segurança.  

8.  Quando tiver concluído a configuração de atribuições de operações de segurança, escolha **OK** para guardar a nova função de segurança.  

##  <a name="BKMK_ConfigSecScope"></a> Configurar âmbitos de segurança para um objeto  
 Gerir a associação de um âmbito de segurança para um objeto do objeto – não a partir do âmbito de segurança. As únicas configurações diretas suportadas pelos âmbitos de segurança são as alterações ao respetivo nome e descrição. Para alterar o nome e descrição de um âmbito de segurança ao visualizar as propriedades do âmbito, terá de possuir a permissão **Modificar** no objeto com capacidade de segurança **Âmbitos de Segurança** .  

 Quando criar um novo objeto no Configuration Manager, o novo objeto é associado a cada âmbito de segurança que está associado a funções de segurança da conta utilizada para criar o objeto – quando esses âmbitos de segurança fornecem a **criar** permissão ou **definir âmbito de segurança** permissão. Só pode alterar os âmbitos de segurança que o objeto se encontra associado depois de criado.  

 Por exemplo, lhe é atribuída uma função de segurança que concede a permissão para criar um novo grupo de limites. Quando cria um novo grupo de limites, não tem nenhuma opção que possa atribuir âmbitos de segurança específicas para. Em vez disso, os âmbitos de segurança que estão disponíveis a partir de funções de segurança que o utilizador está associado são automaticamente atribuídos ao novo grupo de limites. Depois de guardar o novo grupo de limites, pode editar os âmbitos de segurança que estão associados ao novo grupo de limites.  

 Utilize o procedimento seguinte para configurar os âmbitos de segurança que são atribuídos a um objeto.  

#### <a name="to-configure-security-scopes-for-an-object"></a>Para configurar âmbitos de segurança para um objeto  

1.  Na consola do Configuration Manager, selecione um objeto que suporte a ser atribuído a um âmbito de segurança.  

2.  No **base** separador o **classificar** grupo, selecione **definir âmbitos de segurança**.  

3.  Na caixa de diálogo **Definir Âmbitos de Segurança** , selecione ou desmarque os âmbitos de segurança a que este objeto se encontra associado. Cada objeto que suporte âmbitos de segurança tem de ser atribuído a pelo menos um âmbito de segurança.  

4.  Escolher **OK** para guardar os âmbitos de segurança atribuídas.  

    > [!NOTE]  
    >  Ao criar um novo objeto, poderá atribuir o objeto a vários âmbitos de segurança. Para modificar o número de âmbitos de segurança que estão associados ao objeto, terá de alterar esta atribuição após a criação do objeto.  

##  <a name="BKMK_ConfigColl"></a> Configurar coleções para gerir a segurança  
 Não existem procedimentos para configurar coleções para administração baseada em funções. Coleções não têm uma configuração de administração baseada em funções. Em vez disso, é atribuir coleções para um utilizador administrativo quando configurou o utilizador administrativo. As operações de segurança de coleção ativadas nas funções de segurança atribuída determinam as permissões que um utilizador administrativo possui para as coleções e recursos de coleção (membros da coleção).  

 Quando um utilizador administrativo tem permissões para uma coleção, também tem permissões para coleções que estejam limitadas a essa coleção. Por exemplo, a sua organização utiliza uma coleção designada todos os computadores de secretária e, existe uma coleção designada ambientes de trabalho da América do Norte todas as que está limitado a coleção de todos os computadores de secretária. Se um utilizador administrativo tiver permissões para Todos os Ambientes de Trabalho, também terá as mesmas permissões para a coleção Todos os Ambientes de Trabalho da América do Norte.

 Além disso, um utilizador administrativo não é possível utilizar o **eliminar** ou **modificar** permissão numa coleção que lhe esteja diretamente atribuída. No entanto, podem utilizar estas permissões nas coleções que estejam limitadas a essa coleção. No exemplo anterior, o utilizador administrativo pode eliminar ou modificar a coleção todos os ambientes de trabalho da América do Norte, mas não é possível eliminar ou modificar a coleção todos os computadores de secretária.  

##  <a name="BKMK_Create_AdminUser"></a> Criar um novo utilizador administrativo  
 Para conceder a indivíduos ou membros de um grupo de segurança acesso para gerir o Configuration Manager, criar um utilizador administrativo no Configuration Manager e especificar a conta do Windows do utilizador ou grupo de utilizadores. Cada utilizador administrativo no Configuration Manager deve ser atribuído pelo menos uma função de segurança e um âmbito de segurança. Também é possível atribuir coleções para limitar o âmbito administrativo do utilizador administrativo.  

 Utilize os procedimentos seguintes para criar novos utilizadores administrativos.  

#### <a name="to-create-a-new-administrative-user"></a>Para criar um novo utilizador administrativo  

1.  Na consola do Configuration Manager, escolha **administração**.  

2.  No **administração** área de trabalho, expanda **segurança**e, em seguida, escolha **os utilizadores administrativos**.  

3.  No **base** separador o **criar** grupo, selecione **adicionar utilizador ou grupo**.  

4.  Escolher **procurar**e, em seguida, selecione a conta de utilizador ou grupo a utilizar para este novo utilizador administrativo.  

    > [!NOTE]  
    >  Para a administração baseada em consolas, apenas podem ser especificados utilizadores de domínio ou grupos de segurança como utilizadores administrativos.  

5.  Para **associados a funções de segurança**, escolha **adicionar** para abrir uma lista das funções de segurança disponíveis, selecione a caixa para uma ou mais funções de segurança e, em seguida, escolha **OK**.  

6.  Escolha uma das duas opções seguintes para definir o comportamento do objeto com capacidade de segurança para o novo utilizador:  

    -   **Todos os objetos com capacidade de segurança que são relevantes para as respetivas funções de segurança associadas**: Esta opção associa o utilizador administrativo a **todos os** âmbito de segurança e o nível de raiz, as coleções incorporadas para **todos os sistemas** e **todos os utilizadores e grupos de utilizadores**. As funções de segurança atribuídas ao utilizador definem o acesso aos objetos. Os novos objetos criados por este utilizador administrativo são atribuídos ao âmbito de segurança **Predefinido** .  

    -   **Apenas os objetos com capacidade de segurança em coleções ou âmbitos de segurança especificados**: Por predefinição, esta opção associa o utilizador administrativo a **predefinido** âmbito de segurança e o **todos os sistemas** e **todos os utilizadores e grupos de utilizadores** coleções. No entanto, os âmbitos de segurança e coleções reais estão limitados aos que estão associados à conta utilizada para criar o novo utilizador administrativo. Esta opção suporta a adição ou remoção de âmbitos de segurança e de coleções para personalizar o âmbito administrativo do utilizador administrativo.  

    > [!IMPORTANT]  
    >  As opções anteriores associam cada âmbito de segurança atribuído e a coleção para cada função de segurança que é atribuída ao utilizador administrativo. Pode utilizar uma terceira opção, **objetos apenas com capacidade de segurança conforme determinado pelas funções de segurança do utilizador administrativo**, para associar funções de segurança individuais a coleções e âmbitos de segurança específicos. Esta terceira opção está disponível após a criação do novo utilizador administrativo, quando este é modificado.  

7.  Dependendo da seleção no passo 6, execute a ação seguinte:  

    -   Se tiver selecionado **todos os objetos com capacidade de segurança que são relevantes para as respetivas funções de segurança associadas**, escolha **OK** para concluir este procedimento.  

    -   Se tiver selecionado **objetos com capacidade de segurança apenas em coleções ou âmbitos de segurança especificados**, pode escolher **adicionar** para selecionar coleções e âmbitos de segurança adicionais. Ou selecione um ou mais objetos na lista e, em seguida, escolha **remover** para removê-los. Escolher **OK** para concluir este procedimento.  

##  <a name="BKMK_ModAdminUser"></a> Modificar o âmbito administrativo de um utilizador administrativo  
 Para modificar o âmbito administrativo de um utilizador administrativo, adicione ou remova funções de segurança, âmbitos de segurança e coleções que estejam associados ao utilizador. Cada utilizador administrativo tem de estar associado, pelo menos, a uma função de segurança e a um âmbito de segurança. Poderá ser necessário atribuir uma ou mais coleções ao âmbito administrativo do utilizador. A maioria das funções de segurança interagem com coleções e não função corretamente sem uma coleção atribuída.  

 Quando modifica um utilizador administrativo, pode alterar o comportamento para a forma como os objetos com capacidade de segurança são associados às funções de segurança atribuídas. Os três comportamentos que pode selecionar são os seguintes:  

-   **Todos os objetos com capacidade de segurança que são relevantes para as respetivas funções de segurança associadas**: Esta opção associa o utilizador administrativo a **todos os** âmbito e a nível de raiz coleções incorporadas para **todos os sistemas** e **todos os utilizadores e grupos de utilizadores**. As funções de segurança atribuídas ao utilizador definem o acesso aos objetos.  

-   **Apenas os objetos com capacidade de segurança em coleções ou âmbitos de segurança especificados**: Esta opção associa o utilizador administrativo aos mesmos âmbitos de segurança e coleções que estejam associadas à conta que utiliza para configurar o utilizador administrativo. Esta opção suporta a adição ou remoção de funções de segurança e de coleções para personalizar o âmbito administrativo do utilizador administrativo.  

-   **Objetos apenas com capacidade de segurança conforme determinado pelas funções de segurança do utilizador administrativo**: Esta opção permite-lhe criar associações específicas entre funções de segurança individuais e coleções para o utilizador e âmbitos de segurança específicos.  

    > [!NOTE]  
    >  Esta opção está disponível apenas quando modificar as propriedades de um utilizador administrativo.  

A configuração atual do comportamento do objeto com capacidade de segurança altera o processo utilizado para atribuir funções de segurança adicionais. Utilize os procedimentos seguintes que são baseados nas diferentes opções para objetos com capacidade de segurança para o ajudar a gerir um utilizador administrativo.  

Utilize o procedimento seguinte para ver e gerir a configuração dos objetos com capacidade de segurança para um utilizador administrativo.  

#### <a name="to-view-and-manage-the-securable-object-behavior-for-an-administrative-user"></a>Para ver e gerir o comportamento de objetos com capacidade de segurança de um utilizador administrativo  

1.  Na consola do Configuration Manager, escolha **administração**.  

2.  No **administração** área de trabalho, expanda **segurança**e, em seguida, escolha **os utilizadores administrativos**.  

3.  Selecione o utilizador administrativo que pretende modificar.  

4.  No **base** separador o **propriedades** grupo, selecione **propriedades**.  

5.  Escolha o **âmbitos de segurança** separador para ver a configuração atual dos objetos com capacidade de segurança para este utilizador administrativo.  

6.  Para modificar o comportamento do objeto com capacidade de segurança, selecione uma nova opção para o comportamento do objeto com capacidade de segurança. Depois de alterar esta configuração, consulte o procedimento adequado para obter orientações adicionais para configurar âmbitos de segurança e coleções e funções de segurança para este utilizador administrativo.  

7.  Escolher **OK** para concluir o procedimento.  

Utilize o procedimento seguinte para modificar um utilizador administrativo que tem o comportamento de objeto com capacidade de segurança definido **todos os objetos com capacidade de segurança que são relevantes para as respetivas funções de segurança associadas**.  

#### <a name="for-option-all-securable-objects-that-are-relevant-to-their-associated-security-roles"></a>Opção: Todos os objetos com capacidade de segurança que são relevantes para as respetivas funções de segurança associadas  

1.  Na consola do Configuration Manager, escolha **administração**.  

2.  No **administração** área de trabalho, expanda **segurança**e, em seguida, escolha **os utilizadores administrativos**.  

3.  Selecione o utilizador administrativo que pretende modificar.  

4.  No **base** separador o **propriedades** grupo, selecione **propriedades**.  

5.  Escolha o **âmbitos de segurança** tecla de tabulação para confirmar que o utilizador administrativo está configurado para **todos os objetos com capacidade de segurança que são relevantes para as respetivas funções de segurança associadas**.  

6.  Para modificar as funções de segurança atribuídas, escolha o **funções de segurança** separador.  

    -   Para atribuir funções de segurança adicionais a este utilizador administrativo, escolha **adicionar**, marque a caixa para cada função de segurança adicional que pretende atribuir e, em seguida, escolha **OK**.  

    -   Para remover funções de segurança, selecione uma ou mais funções de segurança a partir da lista e, em seguida, escolha **remover**.  

7.  Para modificar o comportamento do objeto com capacidade de segurança, escolha o **âmbitos de segurança** separador e escolha uma nova opção para o comportamento do objeto com capacidade de segurança. Depois de alterar esta configuração, consulte o procedimento adequado para obter orientações adicionais para configurar âmbitos de segurança e coleções e funções de segurança para este utilizador administrativo.  

    > [!NOTE]  
    >  Quando o comportamento do objeto com capacidade de segurança está definido como **todos os objetos com capacidade de segurança que são relevantes para as respetivas funções de segurança associadas**, é possível adicionar ou remover coleções e âmbitos de segurança específicos.  

8.  Escolher **OK** para concluir este procedimento.  

Utilize o procedimento seguinte para modificar um utilizador administrativo que tem o comportamento de objeto com capacidade de segurança definido para **Apenas objetos com capacidade de segurança em coleções ou âmbitos de segurança especificados**.  

#### <a name="for-option-only-securable-objects-in-specified-security-scopes-or-collections"></a>Opção: Apenas os objetos com capacidade de segurança em coleções ou âmbitos de segurança especificados  

1.  Na consola do Configuration Manager, escolha **administração**.  

2.  No **administração** área de trabalho, expanda **segurança**e, em seguida, escolha **os utilizadores administrativos**.  

3.  Selecione o utilizador administrativo que pretende modificar.  

4.  No **base** separador o **propriedades** grupo, selecione **propriedades**.  

5.  Escolha o **âmbitos de segurança** tecla de tabulação para confirmar que o utilizador está configurado para **objetos com capacidade de segurança apenas em coleções ou âmbitos de segurança especificados**.  

6.  Para modificar as funções de segurança atribuídas, escolha o **funções de segurança** separador.  

    -   Para atribuir funções de segurança adicionais a este utilizador, selecione **adicionar**, marque a caixa para cada função de segurança adicional que pretende atribuir e, em seguida, escolha **OK**.  

    -   Para remover funções de segurança, selecione uma ou mais funções de segurança a partir da lista e, em seguida, escolha **remover**.  

7.  Para modificar as coleções que estão associadas a funções de segurança e âmbitos de segurança, escolha o **âmbitos de segurança** separador.  

    -   Para associar novos âmbitos de segurança ou coleções a todas as funções de segurança que são atribuídas a este utilizador administrativo, escolha **adicionar** e selecione uma das quatro opções. Se selecionar **âmbito de segurança** ou **coleção**, marque a caixa para um ou mais objetos concluir a seleção e, em seguida, selecione **OK**.  

    -   Para remover um âmbito de segurança ou uma coleção, selecione o objeto e, em seguida, selecione **remover**.  

8.  Escolher **OK** para concluir este procedimento.  

Utilize o procedimento seguinte para modificar um utilizador administrativo que tem o comportamento de objeto com capacidade de segurança definido para **Apenas objetos com capacidade de segurança conforme determinado pelas funções de segurança do utilizador administrativo**.  

#### <a name="for-option-only-securable-objects-as-determined-by-the-security-roles-of-the-administrative-user"></a>Opção: Apenas os objetos com capacidade de segurança conforme determinado pelas funções de segurança do utilizador administrativo  

1.  Na consola do Configuration Manager, escolha **administração**.  

2.  No **administração** área de trabalho, expanda **segurança**e, em seguida, escolha **os utilizadores administrativos**.  

3.  Selecione o utilizador administrativo que pretende modificar.  

4.  No **base** separador o **propriedades** grupo, selecione **propriedades**.  

5.  Escolha o **âmbitos de segurança** tecla de tabulação para confirmar que o utilizador administrativo está configurado para **objetos com capacidade de segurança apenas em coleções ou âmbitos de segurança especificados**.  

6.  Para modificar as funções de segurança atribuídas, escolha o **funções de segurança** separador.  

    -   Para atribuir funções de segurança adicionais a este utilizador administrativo, escolha **adicionar**. No **Adicionar função de segurança** caixa de diálogo, selecione um ou mais disponíveis funções de segurança, escolha **adicionar**e selecione um tipo de objeto para associar às funções de segurança selecionadas. Se selecionar **âmbito de segurança** ou **coleção**, marque a caixa para um ou mais objetos concluir a seleção e, em seguida, selecione **OK**.  

        > [!NOTE]  
        >  Tem de configurar, pelo menos, um âmbito de segurança para que as funções de segurança selecionadas possam ser atribuídas ao utilizador administrativo. Quando seleciona várias funções de segurança, cada coleção e âmbito de segurança que configura são associados a cada um dos perfis de segurança selecionados.  

    -   Para remover funções de segurança, selecione uma ou mais funções de segurança a partir da lista e, em seguida, escolha **remover**.  

7.  Para modificar as coleções que estão associadas uma função de segurança específicos e os âmbitos de segurança, escolha o **âmbitos de segurança** separador, selecione a função de segurança e, em seguida, selecione **editar**.  

    -   Para associar novos objetos a esta função de segurança, escolha **adicionar**e selecione um tipo de objeto para associar às funções de segurança selecionadas. Se selecionar **âmbito de segurança** ou **coleção**, marque a caixa para um ou mais objetos concluir a seleção e, em seguida, selecione **OK**.  

        > [!NOTE]  
        >  Tem de configurar pelo menos um âmbito de segurança.  

    -   Para remover um âmbito de segurança ou uma coleção que está associada esta função de segurança, selecione o objeto e, em seguida, escolha **remover**.  

    -   Quando tiver terminado a modificação dos objetos associados, escolher **OK**.  

8.  Escolher **OK** para concluir este procedimento.  

    > [!CAUTION]  
    >  Quando uma função de segurança concede a utilizadores administrativos a permissão de implementação de coleção, esses utilizadores administrativos podem distribuir objetos de qualquer âmbito de segurança para o qual possuam permissões de **leitura** de objetos, mesmo que esse âmbito de segurança esteja associado a outra função de segurança.  

