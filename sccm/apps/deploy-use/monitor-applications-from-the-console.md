---
title: "Monitorizar aplicações a partir da consola do System Center Configuration Manager | Documentos do Microsoft"
description: "Monitorizar a implementação de software, incluindo aplicações, definições de compatibilidade e atualizações ao utilizar a área de trabalho de monitorização no Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 784c295c-b8b8-4202-ab9f-665908d49d6d
caps.latest.revision: 5
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: fd7ea34b605d70f2ba9bd40384eb566ec3a87430
ms.openlocfilehash: 42d21d10489bffe32b875384f8801686239a0ba4
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="monitor-applications-from-the-system-center-configuration-manager-console"></a>Monitorizar aplicações a partir da consola do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


No System Center Configuration Manager, pode monitorizar a implementação de todo o software, incluindo atualizações de software, definições de compatibilidade, aplicações, sequências de tarefas e pacotes e programas. Pode monitorizar implementações utilizando a **monitorização** área de trabalho na consola do Configuration Manager ou utilizando relatórios.  

 As aplicações no Configuration Manager suportam monitorização baseada no Estado, que lhe permite controlar o último Estado de implementação de aplicações para utilizadores e dispositivos. Estas mensagens de estado apresentam informações sobre dispositivos individuais. Por exemplo, se uma aplicação for implementada para uma coleção de utilizadores, pode ver o estado de compatibilidade da implementação e o objetivo de implementação na consola do Configuration Manager.  

## <a name="learn-about-compliance-states-in-system-center-configuration-manager"></a>Saiba mais sobre os Estados de compatibilidade no System Center Configuration Manager
 O estado de implementação de uma aplicação apresenta um dos seguintes estados de conformidade:  

-   **Bem Sucedido** – A implementação da aplicação foi bem-sucedida ou esta já está instalada.  

-   **Em curso** – A implementação da aplicação está em curso.  

-   **Desconhecido** – Não foi possível determinar o estado de implementação da aplicação. Este estado não é aplicável a implementações com um objetivo de **Disponível**. Este estado é geralmente apresentado quando ainda não tiverem sido recebidas mensagens de estado do cliente.  

-   **Requisitos Não Cumpridos** – A aplicação não foi implementada porque não era compatível com uma dependência ou uma regra de requisito ou porque o sistema operativo em que foi implementada não era aplicável.  

-   **Erro** – Falha na implementação da aplicação devido a um erro.  

Pode ver informações adicionais sobre cada Estado de compatibilidade, incluindo as subcategorias dentro dos Estados de compatibilidade e o número de utilizadores e dispositivos dessa categoria. Por exemplo, o estado de compatibilidade **Erro** inclui as seguintes subcategorias:  

-   Erro na avaliação de requisitos  

-   Erros relacionados com o conteúdo  

-   Erros de instalação  

 Quando se aplica mais de um estado de compatibilidade à implementação de uma aplicação, é possível ver o estado agregado que representa a compatibilidade inferior. Por exemplo:  

    -   Se um utilizador inicia sessão dois dispositivos e a aplicação é instalada com êxito num dispositivo, mas falha no outro, o estado agregado de implementação da aplicação desse utilizador indicará **erro**.  

    -   Se uma aplicação for implementada para todos os utilizadores que inicie sessão no computador, receberá vários resultados de implementação para esse computador. Se uma das implementações falhar, o estado agregado de implementação desse computador indicará **Erro**.  

O estado de implementação para implementações de pacotes e programas não é agregado.  

 Utilize estas subcategorias para o ajudar a identificar rapidamente problemas importantes relacionados com a implementação de uma aplicação. Pode também ver informações adicionais sobre os dispositivos que se enquadram numa subcategoria específica de um estado de compatibilidade.  

 Gestão de aplicações no Configuration Manager inclui um conjunto de relatórios incorporados que permitem monitorizar informações sobre as aplicações e implementações. Estes relatórios possuem a categoria de relatório de **Distribuição de Software - Monitorização de Aplicações**.  

 Para obter mais informações sobre como configurar relatórios no Configuration Manager, consulte o artigo [Reporting no System Center Configuration Manager](../../core/servers/manage/reporting.md).  

## <a name="monitor-the-state-of-an-application-in-the-configuration-manager-console"></a>Monitorizar o estado de uma aplicação na consola do Configuration Manager  

1.  Na consola do Configuration Manager, escolha **monitorização** > **implementações**.  

3.  Para rever detalhes de implementação de cada Estado de compatibilidade e os dispositivos com esse Estado, selecione uma implementação e, em seguida, no **base** separador o **implementação** grupo, selecione **Ver estado** para abrir o **estado da implementação** painel. Neste painel, pode ver os ativos com cada estado de compatibilidade. Escolha qualquer ativo para ver informações mais detalhadas sobre o estado de implementação desse ativo.  

    > [!NOTE]  
    >  O número de itens que podem ser apresentados no painel **Estado da Implementação** está limitado a 20 000. Se precisar de ver mais itens, utilize os relatórios do Configuration Manager para ver os dados de estado da aplicação.  
    >   
    >  O estado dos tipos de implementação é agregado no painel **Estado da Implementação** . Para ver informações mais detalhadas sobre os tipos de implementação, utilize o relatório **Erros da Infraestrutura da Aplicação** na categoria de relatório **Distribuição de Software - Monitorização de Aplicações**.  

4.  Para consultar informações de estado geral sobre uma implementação de aplicações, selecione uma implementação e, em seguida, selecione o **resumo** separador o **implementação selecionada** janela.  

5.  Para consultar informações sobre o tipo de implementação de aplicações, selecione uma implementação e, em seguida, selecione o **tipos de implementação** separador o **implementação selecionada** janela.  

As informações que são mostradas no **estado da implementação** painel depois de escolher **Ver estado** são dados dinâmicos da base de dados do Configuration Manager. As informações que são mostradas no **resumo** separador e **tipos de implementação** separador é dados resumidos.

Se os dados que são mostrados no **resumo** separador e **tipos de implementação** separador não coincide com os dados que são mostrados no **estado da implementação** painel, escolha **executar resumo** para atualizar os dados desses separadores. Pode configurar o intervalo predefinido de resumo da implementação de aplicações da seguinte forma:  

1. Na consola do Configuration Manager, escolha **administração** > **configuração do Site** > **Sites**.

2. A partir do **Sites** lista, selecione o site para o qual pretende configurar o intervalo de resumo e, em seguida, no **base** no separador de **definições** grupo, selecione **Summarizers de estado**.

3. No **Summarizers de estado** diálogo caixa, selecione **Summarizer de implementação de aplicação**e, em seguida, escolha **editar**.  

4. No **propriedades do Summarizer de implementação de aplicação** caixa de diálogo, configure os intervalos de resumo necessários e, em seguida, selecione **OK**.  

