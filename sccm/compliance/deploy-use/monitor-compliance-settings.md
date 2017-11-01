---
title: "Definições de compatibilidade do monitor"
titleSuffix: Configuration Manager
description: "Utilize um ou mais dos procedimentos neste tópico para apresentar o estado de compatibilidade da linha de base de configuração."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 92c1ccca-a748-44cd-a52e-e41d34bf981d
caps.latest.revision: "6"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 1da8bf6ab83be7c72cc95ec5e07cb9b1a17526d5
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="monitor-compliance-settings-in-system-center-configuration-manager"></a>Monitorizar as definições de compatibilidade no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Depois de implementar linhas de base de configuração de System Center Configuration Manager para dispositivos na sua hierarquia, pode utilizar um ou mais dos procedimentos neste tópico para apresentar o estado de compatibilidade da linha de base de configuração:

> [!NOTE]  
>  Os campos de critérios de validação nos relatórios de definições de compatibilidade (o equivalente no relatório do lado do cliente **Restrições**) apresentam o Service Modeling Language (SML). Isto pode dificultar para administradores que tenham criado o item de configuração na consola do Configuration Manager para compreender quais são os critérios de validação se não tiverem conhecimento do SML. Neste caso, utilize o **monitorização** área de trabalho na consola do Configuration Manager para ver as propriedades do item de configuração e os respetivos critérios de validação.  

##  <a name="view-compliance-results-in-the-configuration-manager-console"></a>Ver os resultados de compatibilidade na consola do Configuration Manager  
 Utilize este procedimento para ver detalhes sobre a compatibilidade das linhas de base de configuração implementadas na consola do Configuration Manager.  

### <a name="view-compliance-results-in-the-configuration-manager-console"></a>Ver os resultados de compatibilidade na consola do Configuration Manager  

1.  Na consola do Configuration Manager, clique em **monitorização** > **implementações**.  

3.  Na lista **Implementações** , selecione a implementação de linha de base de configuração cujas informações de compatibilidade pretende rever.  

4.  Poderá rever as informações de resumo sobre a compatibilidade da implementação da linha de base de configuração na página principal. Para ver informações mais detalhadas, selecione a implementação de linha de base de configuração e, no separador **Home Page** , no grupo **Implementação** , clique em **Ver Estado** para abrir a página **Estado da Implementação** .  

     A página **Estado da Implementação** contém os seguintes separadores:  

    -   **Em conformidade**: Apresenta a compatibilidade da linha de base de configuração com base no número de ativos afetados. Pode clicar numa regra para criar um nó temporário sob o nó **Utilizadores** ou **Dispositivos** na área de trabalho **Ativos e Conformidade** , que contém todos os utilizadores ou dispositivos em conformidade com esta regra. O painel **Detalhes do Ativo** apresenta os utilizadores ou os dispositivos conformes com a linha de base de configuração. Faça duplo clique num utilizador ou num dispositivo na lista para visualizar informações adicionais.  

        > [!IMPORTANT]  
        >  Uma regra de item de configuração não é avaliada se não for detetada ou não é aplicável num dispositivo cliente; No entanto, a regra será devolvida como compatível.  

    -   **Erro**: Mostra uma lista de todos os erros para a implementação de linha de base de configuração selecionada com base no número de ativos afetados. Pode fazer duplo clique numa regra para criar um nó temporário sob o nó **Utilizadores** ou **Dispositivos** na área de trabalho **Ativos e Compatibilidade** que contém todos os utilizadores ou dispositivos que geraram erros com esta regra. Quando seleciona um utilizador ou dispositivo, o painel **Detalhes do Ativo** apresenta os utilizadores ou os dispositivos que são afetados pelo problema selecionado. Faça duplo clique num utilizador ou num dispositivo na lista para visualizar informações adicionais sobre o problema.  

    -   **Não conformes**: Mostra uma lista de todas as regras não compatíveis na linha de base de configuração com base no número de ativos afetados. Pode clicar numa regra para criar um nó temporário sob o nó **Utilizadores** ou **Dispositivos** na área de trabalho **Ativos e Conformidade** que contém todos os utilizadores ou dispositivos não conformes com esta regra. Quando seleciona um utilizador ou dispositivo, o painel **Detalhes do Ativo** apresenta os utilizadores ou os dispositivos que são afetados pelo problema selecionado. Faça duplo clique num utilizador ou num dispositivo na lista para visualizar mais informações sobre o problema.  

    -   **Desconhecido**: Mostra uma lista de todos os utilizadores e dispositivos que não comunicaram compatibilidade para a implementação de linha de base de configuração selecionado, juntamente com o estado atual do cliente dos dispositivos.  

5.  Na página **Estado da Implementação** , poderá rever informações detalhadas sobre a compatibilidade da linha de base de configuração implementada. É criado um nó temporário no nó **Implementações** que o ajuda a localizar novamente estas informações de forma rápida.  

##  <a name="view-compliance-results-by-using-reports"></a>Ver resultados de compatibilidade através de relatórios  
 As definições de compatibilidade no Configuration Manager inclui um número de relatórios incorporados que permitem monitorizar informações sobre itens de configuração, linhas de base de configuração e implementações. Estes relatórios têm a categoria de relatório de **Gestão de Compatibilidade e Definições**.  

> [!IMPORTANT]  
>  Deverá utilizar um caráter universal (**%**) ao utilizar os parâmetros **Filtro do dispositivo** e Filtro do utilizador nos relatórios de definições de compatibilidade.  

 Para obter mais informações sobre como configurar relatórios no Configuration Manager, consulte [relatórios no System Center Configuration Manager](../../core/servers/manage/reporting.md)  

##  <a name="view-compliance-results-on-a-configuration-manager-windows-client-computer"></a>Ver resultados de compatibilidade num computador cliente Windows do Configuration Manager

> [!NOTE]  
>  Não é possível ver informações no cliente Windows do Configuration Manager, se tiver iniciado sessão com uma conta de convidado de domínio.    

1.  Navegue para **Configuration Manager** no Painel de Controlo do computador cliente e faça duplo clique no mesmo para abrir as respetivas propriedades.  

2.  Clique no separador **Configurações** e veja a lista de linhas de base de configuração implementadas.  

3.  Veja o **Estado de Conformidade** para cada linha de base da configuração:  

    > [!IMPORTANT]  
    >  Os resultados da avaliação são colocados em cache no cliente por 15 minutos. Se iniciar uma reavaliação dentro do período de 15 minutos, os resultados de compatibilidade desta cache são devolvidos, em vez de ser efetuada uma nova avaliação. Por conseguinte, se fizer uma alteração ao cliente que possa afetar os resultados da avaliação de compatibilidade, aguarde até que os 15 minutos tenham decorrido antes de iniciar uma reavaliação.  

    -   **Em conformidade**: O computador cliente está em conformidade com a linha de base de configuração avaliada.  

    -   **Não conformes**: O computador cliente não está em conformidade com a linha de base de configuração avaliada.  

    -   **Desconhecido**: O computador cliente ainda não avaliou a linha de base de configuração. Se pretender iniciar a avaliação fora da agenda de avaliação de compatibilidade, selecione as linhas de base de configuração a avaliar e, em seguida, clique em **Avaliar**.  

        > [!NOTE]  
        >  Se tiver credenciais de administrador local no computador cliente, pode ver detalhes de cada linha de base de configuração avaliada para determinar qual o item de configuração que está a comunicar um estado não compatível. Para tal, selecione a linha de base de configuração e, em seguida, clique em **Ver Relatório**.  

4.  Clique em **OK**.  

##  <a name="create-collections-based-on-configuration-baseline-compliance"></a>Criar coleções baseadas em compatibilidade da linha de base de configuração  
 Utilize o procedimento seguinte para criar uma coleção do Configuration Manager baseada em dispositivos com uma compatibilidade especificada. Pode criar coleções baseadas nos seguintes estados de conformidade:  

-   **Compatibilidade:**  

-   **Erro**  

-   **Non-compliant**  

-   **Desconhecido**  

1.  Na consola do Configuration Manager, clique em **ativos e compatibilidade** > **as definições de compatibilidade** > **linhas de base de configuração**.  

3.  Na lista **Linhas de Base de Configuração** , selecione a linha de base de configuração a partir da qual pretende criar uma coleção.  

4.  No separador **Implementação** , no **Grupo de Implementação**, clique em **Criar Nova Coleção** e, em seguida, na lista pendente, selecione o nível de compatibilidade para o qual pretende criar uma coleção.  

5.  É aberta opção **Assistente de Criação de Coleção de Utilizadores** ou **Assistente de Criação de Coleção de Dispositivos** , dependendo de o item de configuração ser implementado em utilizadores ou em dispositivos. O assistente é preenchido automaticamente com os valores corretos para criar a coleção; no entanto, pode editar esses valores.  

6.  Após concluir o assistente, a coleção é apresentada no nó **Coleções de Utilizadores** ou **Coleções de Dispositivos** , na área de trabalho **Recursos e Compatibilidade** .  
