---
title: 'Tarefas comuns para linhas de base de configuração '
titleSuffix: Configuration Manager
description: Saiba mais sobre como criar e implementar linhas de base de configuração de System Center Configuration Manager.
ms.date: 07/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 4bb6afeb-d267-4f9b-ade2-26e5400c223b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a12d2e40007a351d3718247803d8be7856e12273
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53423342"
---
# <a name="common-tasks-for-creating-and-deploying-configuration-baselines-with-system-center-configuration-manager"></a>Tarefas comuns para criar e implementar linhas de base de configuração com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este tópico contém cenários comuns para o ajudar a saber mais sobre como criar e implementar linhas de base de configuração de System Center Configuration Manager.  

 Se já estiver familiarizado com as definições de conformidade, pode encontrar documentação detalhada sobre todas as funcionalidades que utilize o [criar linhas de base de configuração](../../compliance/deploy-use/create-configuration-baselines.md) e [implementar linhas de base de configuração](../../compliance/deploy-use/deploy-configuration-baselines.md) tópicos.  

 Antes de começar, leia [introdução às definições de conformidade no System Center Configuration Manager](../../compliance/get-started/get-started-with-compliance-settings.md) para obter algumas noções básicas sobre definições de conformidade e consulte também [planear e configurar as definições de compatibilidade](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)para implementar os pré-requisitos necessários.  

## <a name="create-a-configuration-baseline"></a>Criar uma linha de base de configuração  
 Neste exemplo, criou um item de configuração para apenas PCs Windows 10 que executam o cliente do Configuration Manager.  

 Este item de configuração impõe uma palavra-passe obrigatória de, pelo menos, 6 carateres em PCs Windows 10. O item de configuração tem o nome **Imposição de Palavras-passe do Windows 10**.  

Utilize o procedimento seguinte para aprender a adicionar este item de configuração a uma linha de base de configuração para o preparar para implantação.  

1. Na consola do Configuration Manager, clique em **ativos e compatibilidade** > **definições de compatibilidade** > **linhas de base de configuração**.  

2. No separador **Home Page** , no grupo **Criar** , clique em **Criar Linha de Base de Configuração**.  

3. Na **criar linha de base de configuração** diálogo caixa, configure as seguintes definições:  

   -   **Nome** - Introduza **Palavras-passe do Windows 10** (ou outro nome à sua escolha)  

4. Clique em **Adicionar** > **Itens de Configuração**.  

5. Na caixa de diálogo **Adicionar Itens de Configuração** , selecione o item de configuração **Imposição de Palavras-passe do Windows 10** anteriormente criado e, em seguida, clique em **Adicionar**.  

6. Clique em OK para fechar a **adicionar itens de configuração** caixa de diálogo e retornar para o **criar linha de base de configuração** caixa de diálogo.

7. Clique em **OK** para fechar a caixa de diálogo **Criar Linha de Base de Configuração** .  

   Agora, pode ver a linha de base de configuração no **linhas de base de configuração** nó da consola do Configuration Manager.  

## <a name="deploy-the-configuration-baseline"></a>Implementar a linha de base de configuração  
 Neste exemplo, vai implementar a linha de base de configuração que criou no procedimento anterior para uma coleção de computadores.  

1. Na consola do Configuration Manager, clique em **ativos e compatibilidade** > **definições de compatibilidade** > **linhas de base de configuração**.  

2. Na lista de linhas de base de configuração, selecione **Palavras-passe do Windows 10**.  

3. No separador **Home Page** , no grupo **Implementação** , clique em **Implementar**.  

4. Na **implementar linhas de base de configuração** diálogo caixa, configure as seguintes definições:  

   -   **Linhas de base de configuração selecionadas** - Certifique-se de que a linha base de configuração **Palavras-passe do Windows 10** foi adicionada automaticamente a esta lista.  

   -   **Remediar regras incompatíveis quando suportado** – Marque esta caixa para se certificar de que, se as definições corretas não estiverem presentes nos dispositivos visados, em seguida, estes são remediados pelo Configuration Manager.  

   -   **Recolha** -clique em **procurar** para escolher a coleção de computadores em que a linha de base de configuração é avaliada e remediada para compatibilidade. Neste exemplo, a linha de base de configuração foi implementada na coleção **Todos os Clientes de Servidor e de Ambiente de Trabalho** incorporada.  

       > [!TIP]  
       >  Não se preocupe se a coleção que escolheu contiver computadores ou dispositivos que não executam o Windows 10. Desde que tenha configurado plataformas suportadas no item de configuração que criou, apenas a PCs Windows 10 são avaliados quanto à conformidade.  

   -   Se for necessário, configure o agendamento através do qual a linha de base de configuração é avaliada. Caso contrário, mantenha a predefinição de **7 Dias**.  

5. Clique em **OK** para fechar a caixa de diálogo **Implementar Linhas de Base de Configuração** e criar a implementação.  

   Se pretender ver rapidamente as estatísticas de compatibilidade para esta implementação, na área de trabalho **Monitorização** , clique em **Implementações**. Na parte inferior do ecrã, verá uma **estatísticas de compatibilidade** gráfico.  

## <a name="next-steps"></a>Passos seguintes 

Para obter mais informações sobre como monitorizar linhas de base de configuração, consulte [monitorizar as definições de conformidade](../../compliance/deploy-use/monitor-compliance-settings.md).  
