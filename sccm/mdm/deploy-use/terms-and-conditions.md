---
title: "Termos e condições no System Center Configuration Manager | Microsoft Docs"
description: "Implemente termos e condições para grupos de utilizadores no System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4d3f9e6b-4d71-4fc4-9b91-47f1bfbd8c70
caps.latest.revision: "9"
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 20be68496099a67ad2d475067f073da2cef16c86
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="add-terms-and-conditions-with-system-center-configuration-manager"></a>Adicionar os termos e condições com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode implementar o System Center Configuration Manager termos e condições para grupos de utilizadores para explicar como a inscrição, o acesso a recursos de trabalho e a utilização do Portal da empresa afetam os dispositivos e utilizadores. Os utilizadores têm de aceitar os termos e condições antes de poderem utilizar o Portal da Empresa para inscrever e aceder ao seu trabalho.  

 ## <a name="working-with-terms-and-conditions-policies-in-system-center-configuration-manager"></a>Trabalhar com políticas de termos e condições no System Center Configuration Manager  
 Pode criar e implementar vários conjuntos de termos e condições. Pode também produzir versões dos mesmos termos e condições em idiomas diferentes e, em seguida, implementá-los nos grupos adequados.  

## <a name="to-create-a-terms-and-conditions"></a>Para criar termos e condições  

1.  Na consola do Configuration Manager, aceda a **Recursos e Compatibilidade** > **Descrição Geral** > **Definições de Compatibilidade** > **Termos e Condições**.  

2.  Clique em **Criar Termos e Condições** para criar novos termos e condições.  

3.  Na página **Geral** , especifique as seguintes informações:  

    -   **Nome** -um nome exclusivo apresentado na consola do Configuration Manager  

    -   **Descrição** - detalhes que o ajudam a identificar os termos e condições na consola do Configuration Manager  

     Em seguida, clique em **Seguinte**.  

4.  Na página **Termos** , especifique as seguintes informações:  

    -   **Título** - O título apresentado aos utilizadores no Portal da Empresa  

    -   **Texto para os termos** - os termos e condições apresentados aos utilizadores no Portal da Empresa  

    -   **Texto a explicar o que significa se o utilizador aceita** - marca os utilizadores que veem a aceitação. **Exemplo**: "Concordo com os termos e condições."  

     Em seguida, clique em **Seguinte**.  

5.  Conclua o assistente para criar os novos termos e condições. Os novos termos e condições são apresentados no nó Termos e Condições da área de trabalho Recursos e Compatibilidade.  

## <a name="to-deploy-a-terms-and-conditions"></a>Para implementar termos e condições  

1.  Na consola do Configuration Manager, aceda a **Recursos e Compatibilidade** > **Descrição Geral** > **Definições de Compatibilidade** > **Termos e Condições**.  

2.  Na lista **Termos e Condições** , selecione o item que pretende implementar e, em seguida, clique em **Implementar**.  

3.  **Navegue** para a **Coleção** na qual quer implementar os termos e condições e, em seguida, clique em **OK**.  

     Quando os dispositivos abrangidos acederem à aplicação Portal da Empresa, são apresentados os termos e condições implementados. Os utilizadores têm de aceitar estes termos antes de terem acesso aos recursos da empresa.  

    > [!NOTE]  
    >  Se implementar um conjunto de termos em várias coleções de utilizadores ao qual pertence um utilizador, esse utilizador verá várias cópias de termos idênticos quando abrir o Portal da Empresa. Uma vez que os utilizadores só podem aceitar ou recusar todos os termos, não existe perigo de cair num estado de aceitação ambígua, em que o utilizador aceitou e rejeitou os termos. O relatório de aceitação dos Termos e Condições incluirá apenas uma linha para cada conjunto de termos para cada utilizador, pelo que não existe nenhum erro no relatório.  

## <a name="to-monitor-terms-and-conditions"></a>Monitorizar termos e condições  

1.  Pode monitorizar implementações de termos e condições na consola do Configuration Manager. Na consola do Configuration Manager, vá para **Monitorização** > **Descrição Geral** > **Implementações**.  

2.  Selecione a implementação de termos e condições na lista de implementações.  

     A área de resumo irá apresentar as estatísticas seguintes:  

    -   **Compatível** - os utilizadores aceitaram a versão mais recente dos termos e condições  

    -   **Erro**  

    -   **Não compatível** - os utilizadores aceitaram uma versão dos termos e condições, mas não a versão mais recente  

    -   **Desconhecido** - os utilizadores nunca aceitaram os termos e condições, incluindo as pessoas sem um dispositivo inscrito  

3.  Selecione uma implementação de termos e condições e, em seguida, selecione **Executar Resumo** para ver o estado de implementação de utilizadores individuais.  

     No ecrã Estado de Implementação pode selecionar os separadores de estado para ver os utilizadores com esse estado. Pode clicar em **Executar Resumo** para atualizar os dados em toda a hierarquia. Clique em **Atualizar** para atualizar os dados na consola  

## <a name="to-view--a-terms-and-conditions-report"></a>Visualizar um relatório de termos e condições  

1.  Na consola do Configuration Manager, vá para **Monitorização** > **Descrição Geral** > **Relatórios** > **Relatório**.  

2.  Selecione **Aceitação dos Termos e Condições** e, em seguida, clique em **Executar**. É aberto o relatório de aceitação dos termos e condições. O relatório apresenta cada utilizador a quem os termos e condições foram implementados. Os campos incluem:  

    -   Nome dos termos e condições  

    -   Nome de utilizador  

    -   Versão aceite  

    -   Data aceite  

    -   Aceite mais recente  

## <a name="updates-and-version-control-for-terms-and-conditions"></a>Atualizações e controlo de versão para termos e condições  
 Quando editar termos e condições existentes, pode escolher o comportamento quando implementar os termos e condições. Utilize o procedimento seguinte para ajudar a atualizar os termos e condições existentes.  

### <a name="how-to-work-with-multiple-versions-of-terms-and-conditions"></a>Como trabalhar com várias versões de termos e condições  

1.  Na consola do Configuration Manager, aceda a **Recursos e Compatibilidade** > **Descrição Geral** > **Definições de Compatibilidade** > **Termos e Condições**.  

2.  Selecione a instância de termos e condições que pretende editar e, em seguida, faça duplo clique para abri-la.  

3.  Pode modificar o conteúdo na página **Geral** ou **Termos** para fazer edições necessárias.  

4.  Na página **Termos** , pode especificar se esta nova versão necessita que todos os utilizadores aceitem os termos e condições ou apenas os novos utilizadores irão ver a nova versão.  

     Recomendamos que aumente o número da versão e solicite a aceitação sempre que efetuar alterações significativas aos termos e condições. Mantenha o número da versão atual se, por exemplo, estiver a corrigir erros de digitação ou a alterar a formatação.

> [!div class="button"]
[< Anterior passo](configure-intune-subscription.md)[passo seguinte >  ](create-service-connection-point.md)
