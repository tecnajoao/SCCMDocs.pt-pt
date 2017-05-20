---
title: "Tarefas comuns para linhas de base de configuração - Configuration Manager | Documentos do Microsoft"
description: "Saiba mais sobre como criar e implementar linhas base de configuração do System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
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
ms.translationtype: Machine Translation
ms.sourcegitcommit: 991eff171dce95590a7f050e0d3b07f98c0224b3
ms.openlocfilehash: 5682cacb43af5bf9248446f1c35b08f137bdae9d
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="common-tasks-for-creating-and-deploying-configuration-baselines-with-system-center-configuration-manager"></a>Tarefas comuns para criar e implementar linhas de base de configuração com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este tópico contém cenários comuns para ajudar a saber mais sobre como criar e implementar linhas base de configuração do System Center Configuration Manager.  

 Se já estiver familiarizado com as definições de compatibilidade, documentação detalhada sobre todas as funcionalidades que utiliza pode ser encontrada no [criar linhas de base de configuração](../../compliance/deploy-use/create-configuration-baselines.md) e [implementar linhas de base de configuração](../../compliance/deploy-use/deploy-configuration-baselines.md) tópicos.  

 Antes de começar, leia [começar com as definições de compatibilidade no System Center Configuration Manager](../../compliance/get-started/get-started-with-compliance-settings.md) para algumas noções básicas sobre as definições de conformidade e consulte também [planear e configurar as definições de compatibilidade](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) para implementar os pré-requisitos necessários.  

## <a name="create-a-configuration-baseline"></a>Criar uma linha de base de configuração  
 Neste exemplo, criou um item de configuração para apenas Windows 10 PCs que executam o cliente do Configuration Manager.  

 Este item de configuração impõe uma palavra-passe obrigatória de, pelo menos, 6 carateres em PCs Windows 10. O item de configuração tem o nome **Imposição de Palavras-passe do Windows 10**.  

No procedimento seguinte, aprenderá a adicionar este item de configuração a uma linha de base de configuração para prepará-lo para implementação.  

1.  Na consola do Configuration Manager, clique em **ativos e compatibilidade** > **definições de compatibilidade** > **linhas de base de configuração**.  

3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Linha de Base de Configuração**.  

4.  Na caixa de diálogo **Criar Linha de Base de Configuração** , configure o seguinte:  

    -   **Nome** - Introduza **Palavras-passe do Windows 10** (ou outro nome à sua escolha)  

5.  Clique em **Adicionar** > **Itens de Configuração**.  

6.  Na caixa de diálogo **Adicionar Itens de Configuração** , selecione o item de configuração **Imposição de Palavras-passe do Windows 10** anteriormente criado e, em seguida, clique em **Adicionar**.  

7.  Clique em OK para fechar a caixa de diálogo **Adicionar Itens de Configuração** e regressar à caixa de diálogo **Criar Linha de Base de Configuração** que deve ser semelhante a esta captura de ecrã:  

     ![Criar a caixa de diálogo da linha base de configuração](/sccm/compliance/plan-design/media/Create-Configuration-Baseline.png)  

8.  Clique em **OK** para fechar a caixa de diálogo **Criar Linha de Base de Configuração** .  

 Agora pode ver a linha de base de configuração que acabou de criar no **linhas de base de configuração** nó da consola do Configuration Manager.  

## <a name="deploy-the-configuration-baseline"></a>Implementar a linha de base de configuração  
 Neste exemplo, irá implementar a linha de base de configuração que criou no procedimento anterior numa coleção de computadores.  

1.  Na consola do Configuration Manager, clique em **ativos e compatibilidade** > **definições de compatibilidade** > **linhas de base de configuração**.  

3.  Na lista de linhas de base de configuração, selecione **Palavras-passe do Windows 10**.  

4.  No separador **Home Page** , no grupo **Implementação** , clique em **Implementar**.  

5.  Na caixa de diálogo **Implementar Linhas de Base de Configuração** , configure o seguinte:  

    -   **Linhas de base de configuração selecionadas** - Certifique-se de que a linha base de configuração **Palavras-passe do Windows 10** foi adicionada automaticamente a esta lista.  

    -   **Remediar regras incompatíveis quando suportado** - verifique esta caixa para se certificar de que, se as definições corretas não estão presentes nos dispositivos visados, em seguida, irá ser resolvidos pelo Configuration Manager.  

    -   **Coleção** - Clique em **Procurar** para escolher a coleção de computadores em que a linha de base de configuração será avaliada e remediada para compatibilidade. Neste exemplo, a linha de base de configuração foi implementada na coleção **Todos os Clientes de Servidor e de Ambiente de Trabalho** incorporada.  

        > [!TIP]  
        >  Não se preocupe se a coleção que escolheu contiver computadores ou dispositivos que não executam o Windows 10. Desde que tenha configurado plataformas suportadas no item de configuração que criou, apenas os PCs Windows 10 serão avaliados para compatibilidade.  

    -   Se necessário, configure o agendamento através do qual a linha de base de configuração será avaliada. Caso contrário, mantenha a predefinição de **7 Dias**.  

6.  A caixa de diálogo terá agora o seguinte aspeto:  

     ![Implementar a caixa de diálogo de linhas de base de configuração](/sccm/compliance/plan-design/media/Deploy-configuration-baselines.png)  

7.  Clique em **OK** para fechar a caixa de diálogo **Implementar Linhas de Base de Configuração** e criar a implementação.  

 Se pretender ver rapidamente as estatísticas de compatibilidade para esta implementação, na área de trabalho **Monitorização** , clique em **Implementações**. Na parte inferior do ecrã, verá um gráfico **Estatísticas de Compatibilidade** .  

 Para obter mais informações sobre como monitorizar linhas de base de configuração, consulte o artigo [monitorizar as definições de compatibilidade](../../compliance/deploy-use/monitor-compliance-settings.md)  

