---
title: "Definições de software maligno do Endpoint Protection"
titleSuffix: Configuration Manager
description: "Saiba como configurar atualizações de software do Configuration Manager para fornecer atualizações de definições para os computadores cliente."
ms.custom: na
ms.date: 10/06/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3b9c4027-a98b-406b-935c-ccabcfe713df
caps.latest.revision: "21"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: cf488babe28267c2438e03fa94c514c872f960c7
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
#  <a name="using-configuration-manager-software-updates-to-deliver-definition-updates"></a>Utilizar atualizações de Software do Configuration Manager para fornecer atualizações de definições

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


 Pode configurar as atualizações de software do Configuration Manager para fornecer atualizações de definições para os computadores cliente. Isto é feito através da configuração de regras de implementação automática. Antes de começar a criar regras de implementação automática, certifique-se de que tem configuradas atualizações de software do Configuration Manager. Para obter mais informações, consulte [introdução ao software atualizações no System Center Configuration Manager](/sccm/sum/understand/software-updates-introduction).

> [!NOTE]
>  Este procedimento é apenas para os itens que devem ser especificamente configurados para o Endpoint Protection. Para obter mais informações sobre como criar regra de Assistente de implementação automática, consulte [implementar automaticamente atualizações de software](/sccm/sum/deploy-use/automatically-deploy-software-updates).

## <a name="to-configure-an-automatic-deployment-rule-to-deliver-definition-updates"></a>Para configurar uma regra de implementação automática para disponibilizar atualizações de definições

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.

2.  Na área de trabalho **Biblioteca de Software** , expanda **Atualizações de Software**e clique em **Regras de Implementação Automática**.

3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Regra de Implementação Automática**.

4.  Na página **General** do **Assistente de Criação de Regra de Implementação Automática**, especifique as seguintes informações:

    -   **Nome**: Introduza um nome exclusivo para a regra de implementação automática.

    -   **Coleção**: Selecione a coleção de computadores cliente nos quais pretende implementar atualizações de definições.

        > [!NOTE]
        >  Não é possível implementar atualizações de definições para uma coleção de utilizadores.

5.  Clique em **Adicionar a um Grupo de Atualização de Software existente**.

6.  Certifique-se de que a caixa de verificação  **Ativar a implementação após a execução desta regra** está selecionada e, em seguida, clique em **Seguinte**.

7.  Na página **Definições de Implementação** do assistente, na lista **Nível de detalhe** , selecione **Mínimo**e clique em **Seguinte**.

    > [!NOTE]
    >  Do **nível de detalhe** lista, selecione **mínima** (Configuration Manager sem Service Pack) ou **apenas mensagens de erro** (Configuration Manager). Isto irá reduzir o número de mensagens de estado devolvidas pela implementação da definição. Esta configuração ajuda a reduzir a utilização de processamento da CPU nos servidores do Configuration Manager.

8.  Na lista **Filtros de propriedades** , selecione a caixa de verificação **Classificação da Atualização** .

9. No **os critérios de pesquisa** lista, clique em **< itens para localizar\>**. Em seguida, na caixa de diálogo **Critérios de Procura** , na lista **Especifique o valor para procurar** , selecione **Atualizações de Definição**.

10. Clique em **OK** para fechar a caixa de diálogo **Critérios de Procura** .

11. Na lista **Filtros de propriedades** , selecione a caixa de verificação **Produto** .

12. No **os critérios de pesquisa** lista, clique em **< itens para localizar\>**. Em seguida, na caixa de diálogo **Critérios de Procura** , na lista **Especifique o valor para procurar** , selecione **Forefront Endpoint Protection 2010** para o Windows 8.1 e versões anteriores ou **Windows Defender** para o Windows 10 e posterior.

13. Clique em **OK** para fechar a caixa de diálogo **Critérios de Procura** e, em seguida, clique em **Seguinte**.

14. Opcionalmente, pode filtrar as atualizações substituídas.   Para fazê-lo:
  1.  Na lista **Filtros de propriedades** , selecione a caixa de verificação **Ultrapassado** .
  2.  No **os critérios de pesquisa** lista, clique em **< itens para localizar\>**. Em seguida, na caixa de diálogo **Critérios de Procura** , na lista **Especifique o valor para procurar** , selecione **Não**.  <br><br>

15. Clique em **OK** para fechar a caixa de diálogo **Critérios de Procura** e, em seguida, clique em **Seguinte**.

16. Na página **Agenda de Avaliação** do assistente, selecione **Ativar regra para executar conforme agendado**e, em seguida, configure o agendamento através do qual pretende transferir atualizações de definições. No mínimo, defina a regra para ser executada duas horas após cada sincronização de ponto de atualização de software. Clique em **Seguinte**.

17. Na página **Agenda de Implementação** do assistente, configure as seguintes definições:

    -   **Hora baseada na**: Selecione **UTC** se pretender que todos os clientes na hierarquia instalem as definições mais recentes ao mesmo tempo. O tempo de instalação real irá variar num período de duas horas. Esta definição é uma melhor prática recomendada.

    -   **Hora de disponibilização do software**: Especifique o tempo disponível para a implementação que foi criada por esta regra. A hora especificada tem de ser, pelo menos, uma hora após a execução da regra de implementação automática. Isto ajuda a garantir que o conteúdo tem tempo suficiente para ser replicado nos pontos de distribuição na hierarquia. Algumas atualizações de definições também podem incluir atualizações de motores antimalware, que podem demorar mais tempo a chegar aos pontos de distribuição.

    -   **Prazo de instalação**: Selecione **logo que possível**.

        > [!NOTE]
        >  Os prazos de atualização de software são diversificados durante um período de duas horas para impedir que todos os clientes solicitem uma atualização ao mesmo tempo.

18. Clique em **Seguinte**.

19. Na página **Experiência do Utilizador** do assistente, na lista **Notificações do utilizador** , selecione **Ocultar no Centro de Software e em todas as notificações**.   Isto garante que as atualizações de definições são instaladas automaticamente. Clique em **Seguinte**.

20. Na página **Alertas** do assistente, não é necessário configurar alertas. Endpoint Protection no Configuration Manager gera todos os alertas que poderão ser necessários. Clique em **Seguinte**.

21. Na página **Definições de Transferência** do assistente, selecione o comportamento de transferência de atualizações de software necessário e, em seguida, clique em **Seguinte**.

22. Na página **Pacote de Implementação** do assistente, selecione um pacote de implementação existente ou crie um novo pacote de implementação para incluir os ficheiros de atualização de software associados à regra.

    > [!NOTE]
    >  Considere colocar as atualizações de definições num pacote que não contenha outras atualizações de software. Esta estratégia mantém o tamanho do pacote de atualizações de definições mais pequeno, o que lhe permite replicar para pontos de distribuição mais rapidamente.

23. Na página **Pontos de Distribuição** do assistente, selecione um ou mais pontos de distribuição para os quais o conteúdo deste pacote será copiado e, em seguida, clique em **Seguinte**.

24. Na página **Localização de Transferência** do assistente, selecione **Transferir as atualizações de software a partir da Internet**e clique em **Seguinte**.

25. Na página **Seleção de Idioma** do assistente, selecione cada versão de idioma das atualizações a transferir e clique em **Seguinte**.

26. Conclua o Assistente de Criação de Regra de Implementação Automática.

27. Certifique-se de que a nova regra é apresentada no **regras de implementação automática** nós da consola do Configuration Manager.


> [!div class="button"]
[Passo seguinte >](endpoint-antimalware-policies.md)

> [!div class="button"]
[Volta >](endpoint-configure-alerts.md)
