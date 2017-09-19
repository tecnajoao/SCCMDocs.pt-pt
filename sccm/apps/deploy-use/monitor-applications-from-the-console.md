---
title: "Monitorizar aplicações a partir da consola do System Center Configuration Manager | Microsoft Docs"
description: "Monitorizar a implementação de software, incluindo atualizações, definições de compatibilidade e aplicações utilizando a área de trabalho de monitorização no Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 784c295c-b8b8-4202-ab9f-665908d49d6d
caps.latest.revision: "5"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: ded2a085510def60d388d9754da9c2c41de565d4
ms.sourcegitcommit: b438515490e04fb09c82a8af642d38e9a0605178
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/15/2017
---
# <a name="monitor-applications-from-the-system-center-configuration-manager-console"></a>Monitorizar aplicações a partir da consola do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


No System Center Configuration Manager, pode monitorizar a implementação de todo o software, incluindo atualizações de software, definições de compatibilidade, aplicações, sequências de tarefas e pacotes e programas. Pode monitorizar implementações utilizando a **monitorização** área de trabalho na consola do Configuration Manager ou utilizando relatórios.  

 As aplicações no Configuration Manager suportam a monitorização baseada no Estado, que lhe permite controlar o último Estado de implementação de aplicação para utilizadores e dispositivos. Estas mensagens de estado apresentam informações sobre dispositivos individuais. Por exemplo, se uma aplicação for implementada para uma coleção de utilizadores, pode ver o estado de compatibilidade da implementação e o objetivo da implementação na consola do Configuration Manager.  

## <a name="learn-about-compliance-states-in-system-center-configuration-manager"></a>Saiba mais sobre os Estados de compatibilidade no System Center Configuration Manager
 O estado de implementação de uma aplicação apresenta um dos seguintes estados de conformidade:  

-   **Bem Sucedido** – A implementação da aplicação foi bem-sucedida ou esta já está instalada.  

-   **Em curso** – A implementação da aplicação está em curso.  

-   **Desconhecido** – Não foi possível determinar o estado de implementação da aplicação. Este estado não é aplicável a implementações com um objetivo de **Disponível**. Este estado é geralmente apresentado quando ainda não tiverem sido recebidas mensagens de estado do cliente.  

-   **Requisitos Não Cumpridos** – A aplicação não foi implementada porque não era compatível com uma dependência ou uma regra de requisito ou porque o sistema operativo em que foi implementada não era aplicável.  

-   **Erro** – Falha na implementação da aplicação devido a um erro.  

Pode ver informações adicionais para cada Estado de compatibilidade, incluindo as subcategorias dentro do Estado de compatibilidade e o número de utilizadores e dispositivos desta categoria. Por exemplo, o estado de compatibilidade **Erro** inclui as seguintes subcategorias:  

-   Erro na avaliação de requisitos  

-   Erros relacionados com o conteúdo  

-   Erros de instalação  

 Quando se aplica mais de um estado de compatibilidade à implementação de uma aplicação, é possível ver o estado agregado que representa a compatibilidade inferior. Por exemplo:  

    -   Se um utilizador inicia sessão dois dispositivos e a aplicação é instalada com êxito num dispositivo, mas falha no outro, o estado agregado de implementação da aplicação desse utilizador indicará **erro**.  

    -   Se uma aplicação for implementada para todos os utilizadores que iniciam sessão computador, receberá vários resultados de implementação para esse computador. Se uma das implementações falhar, o estado agregado de implementação desse computador indicará **Erro**.  

O estado de implementação para implementações de pacotes e programas não é agregado.  

 Utilize estas subcategorias para o ajudar a identificar rapidamente problemas importantes relacionados com a implementação de uma aplicação. Pode também ver informações adicionais sobre os dispositivos que se enquadram numa subcategoria específica de um estado de compatibilidade.  

 Gestão de aplicações no Configuration Manager inclui um número de relatórios incorporados que permitem monitorizar informações sobre as aplicações e implementações. Estes relatórios possuem a categoria de relatório de **Distribuição de Software - Monitorização de Aplicações**.  

 Para obter mais informações sobre como configurar relatórios no Configuration Manager, consulte [relatórios no System Center Configuration Manager](../../core/servers/manage/reporting.md).  

## <a name="monitor-the-state-of-an-application-in-the-configuration-manager-console"></a>Monitorizar o estado de uma aplicação na consola do Configuration Manager  

1.  Na consola do Configuration Manager, escolha **monitorização** > **implementações**.  

3.  Para rever os detalhes de implementação para cada Estado de compatibilidade e os dispositivos com esse Estado, selecione uma implementação e, em seguida, no **home page** separador o **implementação** grupo, escolha **Ver estado** para abrir o **estado da implementação** painel. Neste painel, pode ver os ativos com cada estado de compatibilidade. Escolha a qualquer recurso para ver informações mais detalhadas sobre o estado de implementação para esse recurso.  

    > [!NOTE]  
    >  O número de itens que podem ser apresentados no painel **Estado da Implementação** está limitado a 20 000. Se precisar de ver mais itens, utilize os relatórios do Configuration Manager para ver os dados de estado da aplicação.  
    >   
    >  O estado dos tipos de implementação é agregado no painel **Estado da Implementação** . Para ver informações mais detalhadas sobre os tipos de implementação, utilize o relatório **Erros da Infraestrutura da Aplicação** na categoria de relatório **Distribuição de Software - Monitorização de Aplicações**.  

4.  Para rever informações de estado geral sobre uma implementação de aplicação, selecione uma implementação e, em seguida, escolha o **resumo** separador o **implementação selecionada** janela.  

5.  Para rever informações sobre o tipo de implementação de aplicações, selecione uma implementação e, em seguida, escolha o **tipos de implementação** separador o **implementação selecionada** janela.  

As informações mostradas no **estado da implementação** painel após escolher **Ver estado** são dados dinâmicos da base de dados do Configuration Manager. As informações mostradas no **resumo** separador e **tipos de implementação** separador é dados resumidos.

Se os dados que são apresentados no **resumo** separador e **tipos de implementação** separador não correspondem aos dados mostrados no **estado da implementação** painel, escolha **executar resumo** para atualizar os dados desses separadores. Pode configurar o intervalo predefinido de resumo da implementação de aplicações da seguinte forma:  

1. Na consola do Configuration Manager, escolha **administração** > **configuração do Site** > **Sites**.

2. Do **Sites** lista, selecione o site para o qual pretende configurar o intervalo de resumo e, em seguida, no **home page** separador o **definições** grupo, escolha **Summarizers de estado**.

3. No **Summarizers de estado** diálogo caixa, escolha **Summarizer de implementação de aplicação**e, em seguida, escolha **editar**.  

4. No **propriedades do Summarizer de implementação de aplicação** caixa de diálogo, configure os intervalos de resumo necessários e, em seguida, escolha **OK**.  
