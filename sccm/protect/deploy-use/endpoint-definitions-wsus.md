---
title: Definições de software maligno do Endpoint Protection do WSUS
titleSuffix: Configuration Manager
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a34d9401-83e4-471d-8e23-b8042fc11c90
author: aczechowski
description: Saiba como configurar os serviços de atualizações do Windows Server para aprovar automaticamente atualizações de definições.
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: b66c55da65f65c219b5c961949244f105885ba8f
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53424291"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-windows-server-update-services-wsus-for-configuration-manager"></a>Ativar as definições de software maligno do Endpoint Protection transferir a partir do Windows Server Update Services (WSUS) para o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

 Se utilizar o WSUS para manter as definições de antimalware atualizadas, pode configurá-lo para aprovar automaticamente as atualizações de definições. Apesar de utilizar atualizações de software do Configuration Manager é o método recomendado para manter as definições atualizadas, também pode configurar o WSUS como um método para permitir que os utilizadores iniciem manualmente a definição atualizada. Utilize os procedimentos seguintes para configurar o WSUS como uma origem de atualização de definições.

## <a name="to-synchronize-endpoint-protection-definition-updates-in-configuration-manager-software-updates"></a>Para sincronizar atualizações de definições do Endpoint Protection em atualizações de software do Configuration Manager

1. Na consola do Configuration Manager, clique em **Administração**.

2. Na área de trabalho **Administração** , expanda **Configuração do Site**e clique em **Sites**.

3. Selecione o site que contém o ponto de atualização de software. No grupo **Definições** , clique em **Configurar Componentes do Site**e, em seguida, clique em **Ponto de Atualização de Software**.

4. No separador **Classificações** da caixa de diálogo **Propriedades do Componente do Ponto de Atualização de Software** , selecione a caixa de verificação **Atualizações de Definição** .

5. Especifique os **Produtos** atualizados com o WSUS:

   -   Para o Windows 8.1 e anteriores, no separador **Produtos** da caixa de diálogo **Propriedades do Componente do Ponto de Atualização de Software** , selecione a caixa de verificação **Forefront Endpoint Protection 2010** .

   -   Para o Windows 10 e posterior, no **produtos** separador da **propriedades do componente de ponto de atualização de Software** caixa de diálogo, selecione o **Windows Defender** caixas de verificação.

6. Clique em **OK** para fechar a caixa de diálogo **Propriedades do Componente do Ponto de Atualização de Software** .

   Utilize o procedimento seguinte para configurar atualizações de Endpoint Protection ao seu servidor do WSUS não está integrado no ambiente do Configuration Manager.

## <a name="to-synchronize-endpoint-protection-definition-updates-in-standalone-wsus"></a>Para sincronizar atualizações de definições do Endpoint Protection no WSUS autónomo

1.  Na consola de administração do WSUS, expanda **Computadores**, clique em **Opções**e, em seguida, clique em **Produtos e Classificações**.

2.  Especifique os **Produtos** atualizados com o WSUS:

    -   Para o Windows 8.1 e anteriores, no separador **Produtos** da caixa de diálogo **Propriedades do Componente do Ponto de Atualização de Software** , selecione a caixa de verificação **Forefront Endpoint Protection 2010** .

    -   Para o Windows 10 e posterior, no **produtos** separador da **propriedades do componente de ponto de atualização de Software** caixa de diálogo, selecione o **Windows Defender** caixas de verificação.

3.  No separador **Classificações** da caixa de diálogo **Produtos e Classificações** , selecione as caixas de verificação **Atualizações de Definição** e **Atualizações** .

## <a name="approving-definition-updates"></a>Aprovar Atualizações de Definições
 Atualizações de definições de proteção de ponto final tem de ser aprovadas e transferidas para o servidor WSUS antes de serem disponibilizadas aos clientes que solicitam a lista das atualizações disponíveis. Os clientes ligam ao servidor WSUS para verificar se existem atualizações aplicáveis e, em seguida, solicitam as atualizações de definições aprovadas mais recentes.

### <a name="to-approve-definitions-and-updates-in-wsus"></a>Para aprovar definições e atualizações no WSUS

1. Na consola de administração do WSUS, clique em **Atualizações**e, em seguida, clique em **Todas as Atualizações** ou na classificação das atualizações que pretende aprovar.

2. Na lista de atualizações, clique com o botão direito do rato na atualização ou atualizações que pretende aprovar para instalação e, em seguida, clique em **Aprovar**.

3. Na caixa de diálogo **Aprovar Atualizações** , selecione o grupo de computadores para o qual pretende aprovar as atualizações e, em seguida, clique em **Aprovado para Instalação**.

   Para além da aprovação manual, também pode definir uma regra de aprovação automática para atualizações de definições e atualizações do Endpoint Protection. Isto irá configurar o WSUS para aprovar automaticamente atualizações de definições de Endpoint Protection transferidas pelo WSUS.

### <a name="to-configure-an-automatic-approval-rule"></a>Para configurar uma regra de aprovação automática

1.  Na consola de administração do WSUS, clique em **Opções**e, em seguida, clique em **Aprovações Automáticas**.

2.  No separador **Regras de Atualização** , clique em **Nova Regra**.

3.  Na **Adicionar regra** caixa de diálogo em **passo 1: Selecionar propriedades**, selecione o **quando uma atualização está numa classificação específica** caixa de verificação.

4.  Em **passo 2: Editar as propriedades**, clique em **qualquer classificação**.

5.  Desmarque todas as caixas de verificação, exceto **Atualizações de Definição**e, em seguida, clique em **OK**.

6.  Na **Adicionar regra** caixa de diálogo em **passo 1: Selecionar propriedades**, selecione o **quando uma atualização está num produto específico** caixa de verificação.

7.  Em **passo 2: Editar as propriedades**, clique em **qualquer produto**.

8.  Desmarque todas as caixas de verificação, exceto **Forefront Endpoint Protection** para o Windows 8.1 e versões anteriores ou **Windows Defender** para o Windows 10 e posterior e, em seguida, clique em **OK**.

9. Em **passo 3: Especifique um nome**, introduza um nome para a regra e, em seguida, clique em **OK**.

10. Na caixa de diálogo **Aprovações Automáticas** , selecione a caixa de verificação da regra criada recentemente e, em seguida, clique em **Executar regra**.

> [!NOTE]
>  Para maximizar o desempenho no seu servidor WSUS e computadores cliente, recuse atualizações de definições antigas. Para realizar esta tarefa, pode configurar a aprovação automática de revisões e a recusa automática de atualizações expiradas. Para obter mais informações, veja o [artigo 938947 da Base de Dados de Conhecimento Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=204078).
> 
> [!div class="button"]
> [Passo seguinte >](endpoint-antimalware-policies.md)
> 
> [!div class="button"]
> [Volta >](endpoint-configure-alerts.md)
