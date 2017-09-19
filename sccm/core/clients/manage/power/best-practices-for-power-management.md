---
title: "Melhores práticas para gestão de energia | Microsoft Docs"
description: "Obter as melhores práticas para gestão de energia no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9f7142e1-c972-4384-853b-2da1568cb3e3
caps.latest.revision: "5"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 68b8be80152da52be427a3d2fdbf5c466029add6
ms.sourcegitcommit: f6a428a8db7145affa388f59e0ad880bdfcf17b5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/14/2017
---
# <a name="best-practices-for-power-management-in-system-center-configuration-manager"></a>Melhores práticas para gestão de energia no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize as seguintes melhores práticas para gestão de energia no System Center Configuration Manager.  

## <a name="perform-the-monitoring-phase-at-a-representative-time"></a>Efetuar a fase de monitorização num período representativo  
 A fase de monitorização da gestão de energia fornece-lhe informações sobre o consumo de energia, atividade, capacidades de gestão de energia e o  impacto ambiental de computadores na sua organização. Certifique-se de que escolhe um período representativo para efetuar a fase de monitorização. Por exemplo, efetuar a fase de monitorização durante um feriado público não fornece um relatório realista sobre a utilização de energia do computador.  

## <a name="create-a-control-collection-of-computers-with-no-power-plans-applied"></a>Criar uma coleção de controlo dos computadores sem esquemas de energia aplicados  
 Crie duas coleções de computadores para o ajudar a monitorizar os efeitos de aplicação de esquemas de energia em computadores. A primeira coleção deve conter a maioria dos computadores em relação aos quais pretende aplicar as definições de energia e a outra coleção (a coleção de controlo) deve conter os restantes computadores. Aplique a gestão de energia necessária para a coleção que contém a maioria dos computadores. Em seguida, pode executar relatórios para comparar o custo da energia, a utilização de energia e o impacto ambiental dos computadores nos quais aplicou definições de controlo com a coleção de controlo às quais não aplicou definições de energia.  

## <a name="run-the-power-settings-report-before-you-apply-a-power-management-plan"></a>Executar o relatório de Definições de Energia antes de aplicar um esquema de gestão de energia  
 Antes de aplicar um esquema de gestão de energia a uma coleção de computadores, execute o relatório **Definições de Energia** para o ajudar a compreender as definições de gestão de energia já configuradas em computadores na coleção. Se aplicar novas definições de gestão de energia a computadores sem examinar primeiro as definições existentes, isto pode representar um aumento do consumo de energia.  

## <a name="exclude-servers-from-power-management"></a>Excluir os servidores da gestão de energia  
 A gestão de energia para os computadores que executam o Windows Server não é suportada (embora os dados de utilização de energia são recolhidos). Certifique-se de que adiciona servidores a uma coleção e a remove da gestão de energia.  

## <a name="exclude-computers-that-you-do-not-want-to-manage"></a>Excluir computadores que não pretende gerir  
 Se tiver computadores que não pretenda gerir com a gestão de energia, adicione-as a uma coleção e certifique-se de que a coleção é excluída da gestão de energia.  

 Seguem-se alguns exemplos de computadores que pode querer excluir da gestão de energia:  

-   Computadores que têm de permanecer ligados.  

-   Computadores que os utilizadores necessitam para ligar utilizando a Ligação ao Ambiente de Trabalho Remoto .  

-   Computadores que não podem utilizar a gestão de energia.  

-   Computadores que tenham a função de sistema de sites de ponto de distribuição.  

-   Computadores públicos, como computadores de quiosque, ecrãs de informações ou consolas de monitorização onde o computador e o monitor devem estar sempre ativados.  

 Para obter mais informações, consulte [configurar gestão de energia no System Center Configuration Manager](../../../../core/clients/manage/power/configuring-power-management.md).  

## <a name="first-apply-power-plans-to-a-test-collection-of-computers"></a>Em primeiro lugar, aplique os esquemas de energia a uma coleção de teste de computadores  
 Teste sempre o efeito de aplicar um esquema de gestão de energia a uma coleção de teste de computadores antes de aplicar o esquema de energia a uma coleção maior de computadores.  

 As definições de energia aplicadas a computadores que executam o Windows XP ou o Windows Server 2003 não são revertidas para os valores originais, mesmo que exclua o computador da gestão de energia. Em versões posteriores do Windows, excluir um computador da gestão de energia faz com que todas as definições de energia sejam revertidas para os valores originais. Não é possível reverter as definições de energia individuais para os valores originais.  

## <a name="apply-power-plan-settings-individually"></a>Aplicar as definições do plano de energia individualmente  
 Monitorize o efeito de aplicação de cada definição de energia antes de aplicar o seguinte para garantir que cada definição tem o efeito necessário. Para mais informações sobre as definições do plano de energia, consulte [definições do plano de gestão de energia disponíveis](../../../../core/clients/manage/power/create-and-apply-power-plans.md#BKMK_Plans) no tópico [como criar e aplicar esquemas de energia no System Center Configuration Manager](../../../../core/clients/manage/power/create-and-apply-power-plans.md).  

## <a name="regularly-monitor-computers-to-see-if-they-have-multiple-power-plans-applied"></a>Monitorize regularmente os computadores para verificar se têm vários esquemas de energia aplicados  
 A gestão de energia inclui um relatório que apresenta os computadores que têm mais do que um esquema de energia aplicado.  

 Se um computador for membro de várias coleções, em que cada aplica esquemas de energia diferentes, serão executadas as seguintes ações:  

-   Esquema de energia: Se forem aplicados vários valores para definições de energia para um computador, é utilizado o valor menos restritivo.  

-   Hora de reativação: Se forem aplicadas várias horas de reativação a um computador de secretária, será utilizada a hora mais próxima da meia-noite.  

     Para obter mais informações, consulte [computadores com vários esquemas de energia](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Multiple) no tópico [como monitorizar e planear a gestão de energia no System Center Configuration Manager](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md). Para obter mais informações sobre como a gestão de energia resolve conflitos, consulte [como criar e aplicar esquemas de energia no System Center Configuration Manager](../../../../core/clients/manage/power/create-and-apply-power-plans.md).  

## <a name="save-or-export-power-management-information-during-the-monitoring-and-planning-phase-of-power-management"></a>Guardar ou exportar informações de gestão de energia durante a fase de monitorização e planeamento da gestão de energia  
 Informações de gestão de energia utilizadas pelos relatórios diários são mantidas na base de dados do site do Configuration Manager 31 dias.  

 Informações de gestão de energia utilizadas pelos relatórios diários são mantidas na base de dados do site do Configuration Manager durante 13 meses.  

 Quando executa relatórios durante as fases de monitorização, planeamento e compatibilidade de gestão de energia, guarde ou exporte os resultados de quaisquer relatórios para o qual pretende manter os dados para comparação posterior caso sejam posteriores removido pelo Configuration Manager.  
