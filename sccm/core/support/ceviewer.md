---
title: Visualizador de Avaliação de Coleção
titleSuffix: Configuration Manager
description: Utilize o Visualizador de avaliação de coleção para ver e resolver problemas relacionados com o processo de avaliação de coleção no Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: caad2d93-087c-4dc0-a2a7-6a2fd808b4c8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 054676d5583dbc4468f1d2716d895100f3a5471a
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56134304"
---
# <a name="collection-evaluation-viewer"></a>Visualizador de Avaliação de Coleção

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Visualizador de avaliação de coleção é um da [ferramentas do Configuration Manager](/sccm/core/support/tools). Utilize-o para ver e resolver problemas relacionados com o processo de avaliação de coleção no servidor do site primário.

A ferramenta apresenta as seguintes informações:  

- Informações de históricas e em direto para avaliações de coleção completa e incremental  

- O estado da fila de avaliação  

- O tempo de avaliações de coleção concluir  

- As coleções são atualmente a ser avaliadas  

- O tempo estimado que começará e concluir uma avaliação de coleção  



## <a name="about-collection-evaluation"></a>Sobre a avaliação de coleção

O processo de avaliação de coleção é executada ao avaliar as regras de associação de uma coleção para atualizar seus membros. O site coloca uma coleção que está avaliando em um dos quatro filas diferentes:  

- **Fila manual**: Para coleções que um administrador manualmente selecionada para a avaliação a partir da consola  

- **Nova fila**: Para coleções criadas recentemente  

- **Total de fila**: Para coleções devido para avaliação completa  

- **Fila incremental**: Para coleções com a avaliação incremental  

Existem quatro threads que executam para avaliar as coleções nas filas acima. Cada fila inclui uma série de matrizes e cada matriz inclui as coleções a avaliar. O thread que está em execução para a fila seleciona uma coleção da matriz e executa a avaliação. O comprimento da fila indica o número de matrizes na fila.



## <a name="requirements"></a>Requisitos

- Execute a ferramenta no servidor do site  

- Execute a ferramenta por um utilizador administrativo com, pelo menos, o **analista só de leitura** função  

- O utilizador também requer **leitura** permissão para a base de dados no SQL



## <a name="usage"></a>Utilização

Execute **CEViewer.exe**. Menu principal da ferramenta contém os seguintes separadores: 

- [Ligar](#bkmk_connect): Estabelecer a ligação inicial para o servidor de site primário e o SQL Server  

- [Total de avaliação](#bkmk_full-eval): Lista as informações detalhadas sobre todas as últimas avaliações completas   

- [A avaliação incremental](#bkmk_incremental-eval): Lista as informações detalhadas sobre todas as últimas avaliações incrementais  

- [Todas as filas](#bkmk_all-q): Resume as avaliações de coleção atual para todas as filas de quatro  

- [Fila manual](#bkmk_manual-q): Lista as informações detalhadas sobre a avaliação da coleção atual na fila manual  

- [Nova fila](#bkmk_new-q): Lista as informações detalhadas sobre a avaliação da coleção atual na fila de novo  

- [Total de fila](#bkmk_full-q): Lista as informações detalhadas sobre a avaliação da coleção atual na fila de total  

- [Fila incremental](#bkmk_incremental-q): Lista as informações detalhadas sobre a avaliação da coleção atual na fila de incremental  


### <a name="bkmk_connect"></a> Ligar o separador

Este separador permite-lhe estabelecer a ligação inicial ao servidor do site primário. A ferramenta também estabelece uma ligação para o SQL server que aloja a base de dados do site.

As ligações ao servidor do site principal e servidores SQL utilizam a credencial atual do utilizador com sessão iniciada. As ligações para o site de administração central ou um site secundário não são suportadas. Nenhum processo de avaliação de coleção é executado desses sites.

Assim que a ferramenta com êxito estabelece uma ligação, veem uma notificação na parte inferior do Visualizador de avaliação de coleção que confirma a ligação da ferramenta para o SQL server. 


### <a name="bkmk_full-eval"></a> Guia de avaliação completo

Mostra informações detalhadas sobre as últimas avaliações de coleção completa. Existem oito colunas:  

- **Nome da coleção**: Nome da coleção  

- **ID do site**: ID de site da coleção   

- **Tempo de execução**: O intervalo de tempo da última avaliação de coleção foi executado, em segundos  

- **Hora da última avaliação conclusão**: Quando concluída da última avaliação de coleção  

- **Próxima hora de avaliação**: Quando a próxima avaliação completa é iniciado  

- **Alterações de membro**: As alterações de membro na última avaliação de coleção. Estas alterações são mais (membros adicionados) ou menos (membros removidos).  

- **Última hora de alteração de membro**: O tempo mais recente que ocorreu uma alteração de associação na avaliação de coleção  

- **Por cento**: A percentagem de tempo de avaliação para esta coleção sobre o total (todas as coleções) hora da avaliação  


### <a name="bkmk_incremental-eval"></a> Guia de avaliação incremental

Mostra informações detalhadas sobre as últimas avaliações de coleções incrementais. Existem sete colunas:  

- **Nome da coleção**: Nome da coleção  

- **ID do site**: ID de site da coleção   

- **Tempo de execução**: O intervalo de tempo da última avaliação de coleção foi executado, em segundos  

- **Hora da última avaliação conclusão**: Quando concluída da última avaliação de coleção  

- **Alterações de membro**: As alterações de membro na última avaliação de coleção. Estas alterações são mais (membros adicionados) ou menos (membros removidos).  

- **Última hora de alteração de membro**: O tempo mais recente que ocorreu uma alteração de associação na avaliação de coleção  

- **Por cento**: A percentagem de tempo de avaliação para esta coleção sobre o total (todas as coleções) hora da avaliação  


### <a name="bkmk_all-q"></a> Separador de filas todos

Resume as avaliações de coleção em direto para todas as filas de quatro. Existem seis secções:  

- **Resumo**: Lista o número total de coleção e o comprimento da fila para todas as coleções em todas as filas de quatro  

- **Executar avaliação**: Lista de que coleção está atualmente a ser avaliada em cada fila, e quanto tempo está funcionando  

- **Atualização manual**: Mostra um breve resumo das coleções de que está a ser avaliadas, o tempo de conclusão estimada e a ordem da avaliação na fila manual  

- **Nova coleção**: Mostra um breve resumo das coleções de que está a ser avaliadas, o tempo de conclusão estimada e a ordem da avaliação na fila de nova coleção  

- **Total de avaliação**: Mostra um breve resumo das coleções de que está a ser avaliadas, o tempo de conclusão estimada e a ordem da avaliação na fila de avaliação completa  

- **A avaliação incremental**: Mostra um breve resumo das coleções de que está a ser avaliadas, o tempo de conclusão estimada e a ordem da avaliação na fila de avaliação incremental  


### <a name="bkmk_manual-q"></a> Separador de fila manual

Mostra informações sobre a avaliação de coleção manual atualmente a ser avaliada. A ordem da lista é a ordem em que a coleção será avaliada. Existem quatro colunas:  

- **Nome da coleção**: Nome da coleção  

- **ID do site**: ID de site da coleção   

- **Tempo de conclusão previsto**: Quando a avaliação é estimada para concluir  

- **Tempo de execução estimado**: O tempo que a avaliação é estimada para executar, no formato de dia: horas: minutos: segundo  


### <a name="bkmk_new-q"></a> Novo separador de fila

Mostra as informações em direto sobre a nova avaliação de coleção a ser avaliada. A ordem da lista é a ordem em que a coleção será avaliada. Existem quatro colunas:  

- **Nome da coleção**: Nome da coleção  

- **ID do site**: ID de site da coleção   

- **Tempo de conclusão previsto**: Quando a avaliação é estimada para concluir  

- **Tempo de execução estimado**: O tempo que a avaliação é estimada para executar, no formato de dia: horas: minutos: segundo  


### <a name="bkmk_full-q"></a> Separadores de fila completa

Mostra informações sobre a avaliação de coleção completa atualmente a ser avaliada. A ordem da lista é a ordem em que a coleção será avaliada. Existem quatro colunas:  

- **Nome da coleção**: Nome da coleção  

- **ID do site**: ID de site da coleção   

- **Tempo de conclusão previsto**: Quando a avaliação é estimada para concluir  

- **Tempo de execução estimado**: O tempo que a avaliação é estimada para executar, no formato de dia: horas: minutos: segundo  


### <a name="bkmk_incremental-q"></a> Separador de fila incremental

Mostra informações sobre a avaliação de coleções incrementais atualmente a ser avaliada. A ordem da lista é a ordem em que a coleção será avaliada. Existem quatro colunas:  

- **Nome da coleção**: Nome da coleção  

- **ID do site**: ID de site da coleção   

- **Tempo de conclusão previsto**: Quando a avaliação é estimada para concluir  

- **Tempo de execução estimado**: O tempo que a avaliação é estimada para executar, no formato de dia: horas: minutos: segundo  



