---
title: "Tarefas comuns para linhas de base de configuração - Configuration Manager | Microsoft Docs"
description: "Saiba mais sobre como criar e implementar linhas de base de configuração de System Center Configuration Manager."
ms.custom: na
ms.date: 07/12/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4bb6afeb-d267-4f9b-ade2-26e5400c223b
caps.latest.revision: 6
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: MT
ms.sourcegitcommit: 344b55aecd72479b759b40e8252e64a06c5eaba0
ms.openlocfilehash: 5bf4457af6bedf7bc9cd73c879f1857209c0725d
ms.contentlocale: pt-pt
ms.lasthandoff: 07/13/2017

---
# Tarefas comuns para criar e implementar linhas de base de configuração com o System Center Configuration Manager
<a id="common-tasks-for-creating-and-deploying-configuration-baselines-with-system-center-configuration-manager" class="xliff"></a>

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

Este tópico contém os cenários comuns para o ajudar a saber mais sobre como criar e implementar linhas de base de configuração de System Center Configuration Manager.  

 Se já estiver familiarizado com as definições de compatibilidade, pode encontrar documentação detalhada sobre todas as funcionalidades que utilize o [criar linhas de base de configuração](../../compliance/deploy-use/create-configuration-baselines.md) e [implementar linhas de base de configuração](../../compliance/deploy-use/deploy-configuration-baselines.md) tópicos.  

 Antes de começar, leia [introdução às definições de compatibilidade no System Center Configuration Manager](../../compliance/get-started/get-started-with-compliance-settings.md) para obter algumas noções básicas sobre as definições de compatibilidade e leia também [planear e configurar as definições de compatibilidade](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) para implementar os pré-requisitos necessários.  

## Criar uma linha de base de configuração
<a id="create-a-configuration-baseline" class="xliff"></a>  
 Neste exemplo, criou um item de configuração para apenas PCs Windows 10 que executam o cliente do Configuration Manager.  

 Este item de configuração impõe uma palavra-passe obrigatória de, pelo menos, 6 carateres em PCs Windows 10. O item de configuração tem o nome **Imposição de Palavras-passe do Windows 10**.  

Utilize o procedimento seguinte para saber como adicionar este item de configuração para uma linha de base de configuração para prepará-la para implementação.  

1.  Na consola do Configuration Manager, clique em **ativos e compatibilidade** > **as definições de compatibilidade** > **linhas de base de configuração**.  

3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Linha de Base de Configuração**.  

4.  No **criar linha de base de configuração** diálogo caixa, configure as seguintes definições:  

    -   **Nome** - Introduza **Palavras-passe do Windows 10** (ou outro nome à sua escolha)  

5.  Clique em **Adicionar** > **Itens de Configuração**.  

6.  Na caixa de diálogo **Adicionar Itens de Configuração** , selecione o item de configuração **Imposição de Palavras-passe do Windows 10** anteriormente criado e, em seguida, clique em **Adicionar**.  

7.  Clique em OK para fechar o **adicionar itens de configuração** caixa de diálogo e voltar para o **criar linha de base de configuração** caixa de diálogo.

8.  Clique em **OK** para fechar a caixa de diálogo **Criar Linha de Base de Configuração** .  

 Agora, pode ver a linha de base de configuração no **linhas de base de configuração** nós da consola do Configuration Manager.  

## Implementar a linha de base de configuração
<a id="deploy-the-configuration-baseline" class="xliff"></a>  
 Neste exemplo, implementar a linha de base de configuração que criou no procedimento anterior numa coleção de computadores.  

1.  Na consola do Configuration Manager, clique em **ativos e compatibilidade** > **as definições de compatibilidade** > **linhas de base de configuração**.  

3.  Na lista de linhas de base de configuração, selecione **Palavras-passe do Windows 10**.  

4.  No separador **Home Page** , no grupo **Implementação** , clique em **Implementar**.  

5.  No **implementar linhas de base de configuração** diálogo caixa, configure as seguintes definições:  

    -   **Linhas de base de configuração selecionadas** - Certifique-se de que a linha base de configuração **Palavras-passe do Windows 10** foi adicionada automaticamente a esta lista.  

    -   **Remediar regras incompatíveis quando suportado** - verifique esta caixa para se certificar de que, se as definições corretas não estiverem presentes nos dispositivos visados, em seguida, estes são remediados pelo Configuration Manager.  

    -   **Coleção** -clique em **procurar** para escolher a coleção de computadores em que a linha de base de configuração é avaliada e remediada para compatibilidade. Neste exemplo, a linha de base de configuração foi implementada na coleção **Todos os Clientes de Servidor e de Ambiente de Trabalho** incorporada.  

        > [!TIP]  
        >  Não se preocupe se a coleção que escolheu contiver computadores ou dispositivos que não executam o Windows 10. Desde que tenha configurado plataformas suportadas no item de configuração que criou, apenas a PCs Windows 10 são avaliados para compatibilidade.  

    -   Se necessário, configure o agendamento através do qual a linha de base de configuração é avaliada. Caso contrário, mantenha a predefinição de **7 Dias**.  

7.  Clique em **OK** para fechar a caixa de diálogo **Implementar Linhas de Base de Configuração** e criar a implementação.  

 Se pretender ver rapidamente as estatísticas de compatibilidade para esta implementação, na área de trabalho **Monitorização** , clique em **Implementações**. Na parte inferior do ecrã, verá um **as estatísticas de compatibilidade** gráfico.  

## Passos seguintes
<a id="next-steps" class="xliff"></a> 

Para obter mais informações sobre como monitorizar linhas de base de configuração, consulte [monitorizar as definições de compatibilidade](../../compliance/deploy-use/monitor-compliance-settings.md).  

