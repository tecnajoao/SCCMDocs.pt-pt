---
title: "Estratégia de hierarquia de origem"
titleSuffix: Configuration Manager
description: "Configurar uma hierarquia de origem e recolher dados de um site de origem antes de configurar uma tarefa de migração do System Center Configuration Manager."
ms.custom: na
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4800a800-66c8-4c35-aebe-e413a23790c1
caps.latest.revision: "6"
caps.handback.revision: "0"
author: aaroncz
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: f56d21095e4a781c0a490ff0a6f3a4e05007755f
ms.sourcegitcommit: 7fe45ff75f05f7cc03ad021db8119791abe18049
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/01/2017
---
# <a name="plan-a-source-hierarchy-strategy-in-system-center-configuration-manager"></a>Planear uma estratégia de hierarquia de origem no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Antes de configurar uma tarefa de migração no seu ambiente do System Center Configuration Manager, tem de configurar uma hierarquia de origem e recolher dados de, pelo menos, um site de origem nessa hierarquia. Utilize as secções seguintes para ajudar a planear configurar hierarquias de origem, configurar sites de origem e determinar a forma como o Configuration Manager recolhe informações dos sites de origem na hierarquia de origem. 

##  <a name="BKMK_Source_Hierarchies"></a> Hierarquias de origem  
Uma hierarquia de origem é uma hierarquia do Configuration Manager que tem dados que pretende migrar. Quando configurar a migração e especificar uma hierarquia de origem, especifique o site de nível superior da hierarquia de origem. Este site é também designado por site de origem. Sites adicionais que pode migrar dados a partir da hierarquia de origem são também denominados sites de origem.  

-   Quando configurar uma tarefa de migração para migrar dados de uma hierarquia de origem do Configuration Manager 2007, configurar para migrar dados a partir de um ou mais sites de origem específicos na hierarquia de origem.  

-   Quando configurar uma tarefa de migração para migrar dados de uma hierarquia de origem que executa o System Center 2012 Configuration Manager ou posterior, só tem de especificar o site de nível superior.  

Pode configurar apenas uma hierarquia de origem num momento.  

-   Se configurar uma nova hierarquia de origem, essa hierarquia torna-se automaticamente a hierarquia de origem atual, substituindo a hierarquia de origem de anterior.  

-   Quando configurar uma hierarquia de origem, tem de especificar o site de nível superior da hierarquia de origem e especifique as credenciais para o Configuration Manager para utilizar para estabelecer ligação com o fornecedor de SMS e a base de dados do site desse site de origem.  

-   O Configuration Manager utiliza estas credenciais para executar a recolha para obter informações sobre os objetos e pontos de distribuição do site de origem de dados.  

-   Como parte do processo de recolha dados, são identificados os sites subordinados na hierarquia de origem.  

-   Se a hierarquia de origem for uma hierarquia do Configuration Manager 2007, pode configurar esses sites adicionais como sites de origem com credenciais separadas para cada site de origem.  

Apesar de poder configurar várias hierarquias de origem sucessivamente, a migração está ativa para apenas uma hierarquia de origem num momento.  

-   Se configurar uma hierarquia de origem adicional antes de concluir a migração da hierarquia de origem atual, o Configuration Manager cancela quaisquer tarefas de migração ativos e postpones as tarefas de migração agendada para a hierarquia de origem atual.  

-   A hierarquia de origem recém configurada torna-se então na hierarquia de origem atual e a hierarquia de origem original agora está inativa.  

-   Pode, em seguida, definir as credenciais de ligação, sites de origem adicionais e tarefas de migração da nova hierarquia de origem.  

Se restaurar uma hierarquia de origem inativa e não tiver utilizado anteriormente **limpar dados de migração**, pode ver as tarefas de migração anteriormente configuradas para essa hierarquia de origem. No entanto, para poder prosseguir a migração a partir dessa hierarquia terá de reconfigurar as credenciais para estabelecer ligação aos sites de origem aplicáveis na hierarquia e, em seguida, reagendar as tarefas de migração que não tenham sido concluídas.  

> [!CAUTION]  
>  Se migrar dados de mais do que uma hierarquia de origem, cada hierarquia de origem adicional terá de conter um conjunto exclusivo de códigos de site.  

Para obter mais informações sobre como configurar uma hierarquia de origem, consulte [configurar hierarquias de origem e sites de origem para migração para o System Center Configuration Manager](../../core/migration/configuring-source-hierarchies-and-source-sites-for-migration.md)  

##  <a name="BKMK_Source_Sites"></a> Sites de origem  
 Os sites de origem são os sites da hierarquia de origem que contêm os dados que pretende migrar. O site de nível superior da hierarquia de origem é sempre o primeiro site de origem. Quando a migração recolhe dados do primeiro site de origem de uma nova hierarquia de origem, deteta informações sobre os sites adicionais dessa hierarquia.  

 Após a conclusão da recolha de dados do site de origem inicial, as ações seguintes a efetuar dependem da versão de produto da hierarquia de origem.  

### <a name="source-sites-that-run-configuration-manager-2007-sp2"></a>Sites de origem com o Configuration Manager 2007 SP2  
 Após a recolha de dados do site de origem inicial da hierarquia do Configuration Manager 2007 SP2, não dispõe de configurar sites de origem adicionais para que poder criar tarefas de migração. No entanto, para poder migrar dados de sites adicionais, tem de configurar sites adicionais como sites de origem e o System Center Configuration Manager com êxito tem recolher dados a partir desses sites.  

 Para recolher dados de sites adicionais, individualmente configurar cada site como site de origem. Isto requer que especifique as credenciais para o System Center Configuration Manager, para estabelecer ligação com o fornecedor de SMS e a base de dados do site de cada site de origem. Depois de configurar as credenciais para um site de origem, inicia os processo recolha de dados para esse site.  

 Quando configurar sites de origem adicionais numa hierarquia de origem do Configuration Manager 2007 SP2, tem de configurar sites de origem do nível superior, o que significa que configura os sites da camada inferior serão pela última vez. Pode configurar sites de origem num ramo da hierarquia em qualquer altura, mas tem de configurar um site como site de origem antes de configurar qualquer um dos respetivos sites subordinados como sites de origem.  

> [!NOTE]  
>  Apenas os sites primários numa hierarquia do Configuration Manager 2007 SP2 são suportados para migração.  

### <a name="source-sites-that-run-system-center-2012-configuration-manager-or-later"></a>Sites de origem com o System Center 2012 Configuration Manager ou posterior  
 Após a recolha de dados do site de origem inicial do System Center 2012 Configuration Manager ou hierarquia posterior, não dispõe de configurar sites de origem adicionais nessa hierarquia de origem. Isto acontece porque ao contrário do Configuration Manager 2007, estas versões do Configuration Manager utilizarem uma base de dados partilhado e a base de dados partilhada permite-lhe identificar e migrar todos os objetos disponíveis a partir do site de origem inicial.  

 Quando configurar as contas de acesso para recolha de dados, poderá ter de conceder a **conta do fornecedor de SMS de Site de origem** acesso a vários computadores na hierarquia de origem. Isto pode ser necessário quando o site de origem suporta múltiplas instâncias do Fornecedor de SMS, cada uma num computador diferente. Quando a recolha de dados é iniciada, o site de nível superior da hierarquia de destino contacta o site de nível superior da hierarquia de origem para identificar as localizações do Fornecedor de SMS desse site. Só é identificada a primeira instância do Fornecedor de SMS. Se o processo de recolha de dados não conseguir aceder ao Fornecedor de SMS na localização identificada, o processo falhará, não tentando estabelecer ligação a computadores adicionais que executem uma instância do Fornecedor de SMS desse site.  

##  <a name="BKMK_Data_Gathering"></a> Recolha de dados  
 Imediatamente após especificar uma hierarquia de origem, configurar as credenciais de cada site de origem adicionais numa hierarquia de origem ou partilhar os pontos de distribuição de um site de origem, o Configuration Manager começa a recolher dados do site de origem.  

 Em seguida, o processo de recolha de dados repete-se numa agenda simples, para manter a sincronização com eventuais alterações dos dados do site de origem. Por predefinição, o processo é repetido a cada quatro horas. Pode alterar a agenda deste ciclo editando o **propriedades** do site de origem. O processo de recolha inicial de dados tem de consultar todos os objetos na base de dados do Configuration Manager e pode demorar muito tempo a concluir. Os processos de recolha de dados subsequentes identificam apenas as alterações dos dados, demorando menos tempo.  

 Para recolher os dados, o site de nível superior da hierarquia de destino estabelece ligação ao Fornecedor de SMS e à base de dados do site de origem para obter uma lista de objetos e pontos de distribuição. Estas ligações utilizam as contas de acesso do site de origem. Para obter informações sobre as configurações necessárias para a recolha de dados, consulte [pré-requisitos para migração no System Center Configuration Manager](../../core/migration/prerequisites-for-migration.md).  

 Pode iniciar e parar os processo recolha de dados utilizando **recolher dados agora** e **parar a recolha de dados** na consola do Configuration Manager.  

 Depois de utilizar **parar a recolha de dados** para um site de origem por qualquer motivo, terá de reconfigurar o credenciais para o site para poder voltar a recolher dados desse site. Até reconfigurar o site de origem, o Configuration Manager não consegue identificar novos objetos ou alterações a objetos anteriormente migrados nesse site.  

> [!NOTE]  
>  Antes de expandir um site primário autónomo numa hierarquia com um site de administração central, tem de parar a recolha de todos os dados. Pode reconfigurar depois de concluída a expansão do site de recolha de dados.  

### <a name="gather-data-now"></a>Recolher Dados Agora  
 Após a execução do processo inicial de recolha de dados de um site, o processo é repetido para identificar os objetos que tenham sido atualizados desde o último ciclo de recolha de dados. Também pode utilizar o **recolher dados agora** ação na consola do Configuration Manager para iniciar imediatamente o processo e para repor a hora de início do ciclo seguinte.  

 Após a conclusão com êxito do processo de recolha de dados de um site de origem, poderá partilhar os pontos de distribuição do site de origem e configurar as tarefas de migração de dados do site. Recolha de dados é um processo de migração recorrente e continua até que altere a hierarquia de origem ou utilize **parar a recolha de dados** para terminar os processo recolha de dados para esse site.  

### <a name="stop-gathering-data"></a>Parar a Recolha de Dados  
 Pode utilizar **parar a recolha de dados** para terminar os processo recolha de dados para um site de origem quando pretender que deixem o Configuration Manager para identificar objetos novos ou alterados a partir desse site. Esta ação também impede que o Configuration Manager oferta quaisquer pontos de distribuição partilhados da origem como localizações de conteúdo para o conteúdo migrado a clientes da hierarquia de destino.  

 Para parar a recolha de dados de cada site de origem, tem de executar **parar a recolha de dados** em sites de origem da camada inferior e, em seguida, repita o processo em cada site principal. O site de nível superior da hierarquia de origem terá de ser o último em que a recolha de dados é interrompida. Terá de interromper a recolha de dados em cada site subordinado antes de efetuar essa ação num site principal. Normalmente, apenas interromperá a recolha de dados quando estiver pronto para concluir o processo de migração.  

 Depois de interromper a recolha de dados de um site de origem, as informações anteriormente recolhidas sobre objetos e coleções desse site continuarão disponíveis para utilização quando configurar novas tarefas de migração. No entanto, não verá os novos objetos ou coleções nem verá as alterações efetuadas em objetos existentes. Se reconfigurar o site de origem e recomeçar a recolher dados, verá o estado e informações sobre os objetos anteriormente migrados.  
