---
title: "Criar linhas de base de configuração | Documentos do Microsoft"
description: "Crie linhas de base de configuração no System Center Configuration Manager que pode implementar para uma coleção."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 678c9622-c61b-47d1-ba25-690616e431c7
caps.latest.revision: 5
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: f9e939d871e95a3248d8e5d96cb73063a81fd5cf
ms.openlocfilehash: 649942d3d468ec35c7246e08f741cdebd22fb3ac
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="create-configuration-baselines-in-system-center-configuration-manager"></a>Criar linhas de base de configuração no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Linhas de base de configuração no System Center Configuration Manager contêm itens de configuração predefinidas e, opcionalmente, outras linhas de base de configuração. Depois de criar uma linha de base de configuração, pode implementá-la numa coleção, para que os dispositivos nessa coleção a transfiram e avaliem a compatibilidade com a mesma.  

 Linhas de base de configuração no Configuration Manager podem conter revisões específicas de itens de configuração ou podem ser configuradas para utilizar sempre a versão mais recente de um item de configuração. Para mais informações sobre revisões do item de configuração, consulte o artigo [tarefas de gestão para dados de configuração](../../compliance/deploy-use/management-tasks-for-configuration-data.md).  

 Existem dois métodos que pode utilizar para criar linhas de base de configuração:  

-   Importar dados de configuração de um ficheiro. Para iniciar o **Assistente de Importação de Dados de Configuração**, no nó **Itens de Configuração** ou **Linhas de Base de Configuração** , na área de trabalho **Recursos e Compatibilidade** , clique em **Importar Dados de Configuração**.  

-   Utilize a caixa de diálogo **Criar Linha de Base de Configuração** para criar uma nova linha de base de configuração.  

 Utilize o procedimento seguinte para criar uma linha de base de configuração com a caixa de diálogo **Criar Linha de Base de Configuração** .  

1.  Na consola do Configuration Manager, clique em **ativos e compatibilidade** > **definições de compatibilidade** > **linhas de base de configuração**.  

3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Linha de Base de Configuração**.  

4.  Na caixa de diálogo **Criar Linha de Base de Configuração** , introduza um nome único e uma descrição para a linha de base de configuração. Pode utilizar um máximo de 255 carateres para o nome e 512 carateres para a descrição.  

5.  A lista **Dados de configuração** apresenta todos os itens de configuração ou linhas de base de configuração que estão incluídos nesta linha de base de configuração. Clique em **Adicionar** para adicionar um novo item de configuração ou linha base de configuração à lista. Pode selecionar de entre o seguinte:  

    -   **Itens de Configuração**  

    -   **Atualizações de Software**  

    -   **Linhas de Base de Configuração**  
      > [!IMPORTANT]
      > Tem de limitar cada linha de base de configuração para não mais de 1000 atualizações de software.
6.  Utilize a lista **Alterar Objetivo** para especificar o comportamento de um item de configuração que selecionou na lista **Dados de configuração** . Pode selecionar as seguintes opções:  

    -   **Necessário** A linha de base de configuração é avaliada como não conforme se o item de configuração não for detetado num dispositivo cliente. Se for detetado, é avaliado para fins de compatibilidade  

    -   **Opcional** A compatibilidade do item de configuração é avaliada apenas se a aplicação a que faz referência for encontrada nos computadores cliente. Se a aplicação não for encontrada, a linha de base de configuração não é marcada como não compatível (apenas aplicável a itens de configuração de aplicação).  

    -   **Proibido** A linha de base de configuração é avaliada como não compatível se o item de configuração for detetado em computadores cliente (apenas aplicável a itens de configuração de aplicação).  

    > [!NOTE]
    >  A lista **Alterar Objetivo** só está disponível se tiver clicado na opção **Este item de configuração contém as definições da aplicação** na página **Geral** do **Assistente de Criação de Item de Configuração**.  

7.  Utilize a lista **Alterar Revisão** para selecionar uma revisão específica ou a revisão mais recente do item de configuração para avaliar a compatibilidade nos dispositivos cliente ou selecione **Utilizar Sempre Mais Recente** para utilizar sempre a revisão mais recente. Para mais informações sobre revisões do item de configuração, consulte o artigo [tarefas de gestão para dados de configuração](../../compliance/deploy-use/management-tasks-for-configuration-data.md).  

8.  Para remover um item de configuração de linha de base de configuração, selecione um item de configuração e, em seguida, clique em **remover**.  

9. Clique em **OK** para fechar a caixa de diálogo **Criar Linha de Base de Configuração** e para criar a linha de base de configuração.  

