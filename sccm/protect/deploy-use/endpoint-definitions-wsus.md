---
title: "Definições de software maligno do Endpoint Protection a partir do WSUS | Documentos do Microsoft"
definition: Learn how to configure Windows Server Updates Services to auto-approve definition updates.
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a34d9401-83e4-471d-8e23-b8042fc11c90
caps.latest.revision: 21
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 017bd5b899b364fc832c721d63cc7dbad0a11671
ms.openlocfilehash: 0e606b25065fa25c782d1b5f3fbf164e60733353
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---

# <a name="enable-endpoint-protection-malware-definitions-to-download-from-windows-server-update-services-wsus-for-configuration-manager"></a>Ativar as definições de software maligno do Endpoint Protection transferir a partir do Windows Server Update Services (WSUS) para o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

 Se utilizar o WSUS para manter as definições de antimalware atualizadas, pode configurá-lo para aprovar automaticamente as atualizações de definições. Apesar de utilizar as atualizações de software do Configuration Manager é o método recomendado para manter as definições atualizadas, também pode configurar o WSUS como um método para permitir que os utilizadores iniciar manualmente a definição atualizada. Utilize os procedimentos seguintes para configurar o WSUS como uma origem de atualização de definições.

## <a name="to-synchronize-endpoint-protection-definition-updates-in-configuration-manager-software-updates"></a>Para sincronizar as atualizações de definição do Endpoint Protection em atualizações de software do Configuration Manager

1.  Na consola do Configuration Manager, clique em **Administração**.

2.  Na área de trabalho **Administração** , expanda **Configuração do Site**e clique em **Sites**.

3.  Selecione o site que contém o ponto de atualização de software. No grupo **Definições** , clique em **Configurar Componentes do Site**e, em seguida, clique em **Ponto de Atualização de Software**.

4.  No separador **Classificações** da caixa de diálogo **Propriedades do Componente do Ponto de Atualização de Software** , selecione a caixa de verificação **Atualizações de Definição** .

5.  Especifique os **Produtos** atualizados com o WSUS:

    -   Para o Windows 8.1 e anteriores, no separador **Produtos** da caixa de diálogo **Propriedades do Componente do Ponto de Atualização de Software** , selecione a caixa de verificação **Forefront Endpoint Protection 2010** .

    -   Para o Windows 10 e posterior, no separador **Produtos** da caixa de diálogo **Propriedades do Componente do Ponto de Atualização de Software** , selecione as caixas de verificação **Windows Defender** e **Windows Technical Preview 2** .

6.  Clique em **OK** para fechar a caixa de diálogo **Propriedades do Componente do Ponto de Atualização de Software** .

 Utilize o procedimento seguinte para configurar atualizações do Endpoint Protection quando o servidor dos WSUS não está integrado no ambiente do Configuration Manager.

## <a name="to-synchronize-endpoint-protection-definition-updates-in-standalone-wsus"></a>Para sincronizar atualizações de definições do Endpoint Protection no WSUS autónomo

1.  Na consola de administração do WSUS, expanda **Computadores**, clique em **Opções**e, em seguida, clique em **Produtos e Classificações**.

2.  Especifique os **Produtos** atualizados com o WSUS:

    -   Para o Windows 8.1 e anteriores, no separador **Produtos** da caixa de diálogo **Propriedades do Componente do Ponto de Atualização de Software** , selecione a caixa de verificação **Forefront Endpoint Protection 2010** .

    -   Para o Windows 10 e posterior, no separador **Produtos** da caixa de diálogo **Propriedades do Componente do Ponto de Atualização de Software** , selecione as caixas de verificação **Windows Defender** e **Windows Technical Preview 2** .

3.  No separador **Classificações** da caixa de diálogo **Produtos e Classificações** , selecione as caixas de verificação **Atualizações de Definição** e **Atualizações** .

## <a name="approving-definition-updates"></a>Aprovar Atualizações de Definições
 Atualizações de definições do Endpoint Protection tem de ser aprovadas e transferidas para o servidor WSUS antes de estes são oferecidos aos clientes que solicitam a lista de atualizações disponíveis. Os clientes ligam ao servidor WSUS para verificar se existem atualizações aplicáveis e, em seguida, solicitam as atualizações de definições aprovadas mais recentes.

### <a name="to-approve-definitions-and-updates-in-wsus"></a>Para aprovar definições e atualizações no WSUS

1.  Na consola de administração do WSUS, clique em **Atualizações**e, em seguida, clique em **Todas as Atualizações** ou na classificação das atualizações que pretende aprovar.

2.  Na lista de atualizações, clique com o botão direito do rato na atualização ou atualizações que pretende aprovar para instalação e, em seguida, clique em **Aprovar**.

3.  Na caixa de diálogo **Aprovar Atualizações** , selecione o grupo de computadores para o qual pretende aprovar as atualizações e, em seguida, clique em **Aprovado para Instalação**.

 Para além de aprovação manual, também pode definir uma regra de aprovação automática para atualizações de definições e atualizações do Endpoint Protection. Isto irá configurar o WSUS para aprovar automaticamente atualizações de definições do Endpoint Protection transferidos na íntegra pelo WSUS.

### <a name="to-configure-an-automatic-approval-rule"></a>Para configurar uma regra de aprovação automática

1.  Na consola de administração do WSUS, clique em **Opções**e, em seguida, clique em **Aprovações Automáticas**.

2.  No separador **Regras de Atualização** , clique em **Nova Regra**.

3.  No **Adicionar regra** caixa de diálogo em **passo 1: Selecionar propriedades**, selecione o **quando uma atualização é uma classificação de específico** caixa de verificação.

4.  Em **passo 2: Editar as propriedades**, clique em **qualquer classificação**.

5.  Desmarque todas as caixas de verificação, exceto **Atualizações de Definição**e, em seguida, clique em **OK**.

6.  No **Adicionar regra** caixa de diálogo em **passo 1: Selecionar propriedades**, selecione o **quando uma atualização é um produto específico** caixa de verificação.

7.  Em **passo 2: Editar as propriedades**, clique em **qualquer produto**.

8.  Desmarque todas as caixas de verificação, exceto **Forefront Endpoint Protection** para o Windows 8.1 e versões anteriores ou **Windows Defender** para o Windows 10 e posterior e, em seguida, clique em **OK**.

9. Em **passo 3: Especifique um nome**, introduza um nome para a regra e, em seguida, clique em **OK**.

10. Na caixa de diálogo **Aprovações Automáticas** , selecione a caixa de verificação da regra criada recentemente e, em seguida, clique em **Executar regra**.

> [!NOTE]
>  Para maximizar o desempenho no seu servidor WSUS e computadores cliente, recuse atualizações de definições antigas. Para realizar esta tarefa, pode configurar a aprovação automática de revisões e a recusa automática de atualizações expiradas. Para obter mais informações, veja o [artigo 938947 da Base de Dados de Conhecimento Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=204078).

> [!div class="button"]
[Passo seguinte >](endpoint-antimalware-policies.md)

> [!div class="button"]
[Segurança >](endpoint-configure-alerts.md)

