---
title: Criar linhas de base de configuração
titleSuffix: Configuration Manager
description: Crie linhas de base de configuração no System Center Configuration Manager que pode implementar numa coleção.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 678c9622-c61b-47d1-ba25-690616e431c7
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 665f5720486164cc4c728d579f1a700c4fb16245
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39384676"
---
# <a name="create-configuration-baselines-in-system-center-configuration-manager"></a>Criar linhas de base de configuração no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Linhas de base de configuração no System Center Configuration Manager contêm itens de configuração predefinidos e, opcionalmente, outras linhas de base de configuração. Depois de criar uma linha de base de configuração, pode implementá-la numa coleção, para que os dispositivos nessa coleção a transfiram e avaliem a compatibilidade com a mesma.  

 Linhas de base de configuração no Configuration Manager podem conter revisões específicas de itens de configuração ou podem ser configuradas para utilizar sempre a versão mais recente de um item de configuração. Para obter mais informações sobre revisões de item de configuração, consulte [tarefas de gestão para dados de configuração](../../compliance/deploy-use/management-tasks-for-configuration-data.md).  

 Existem dois métodos que pode utilizar para criar linhas de base de configuração:  

-   Importar dados de configuração de um ficheiro. Para iniciar o **Assistente de Importação de Dados de Configuração**, no nó **Itens de Configuração** ou **Linhas de Base de Configuração** , na área de trabalho **Recursos e Compatibilidade** , clique em **Importar Dados de Configuração**.  

-   Utilize a caixa de diálogo **Criar Linha de Base de Configuração** para criar uma nova linha de base de configuração.  

Para criar uma linha de base de configuração com o **criar linha de base de configuração** diálogo caixa, utilize o seguinte procedimento:  

1.  Na consola do Configuration Manager, clique em **ativos e compatibilidade** > **definições de compatibilidade** > **linhas de base de configuração**.  

2.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Linha de Base de Configuração**.  

3.  Na caixa de diálogo **Criar Linha de Base de Configuração** , introduza um nome único e uma descrição para a linha de base de configuração. Pode utilizar um máximo de 255 carateres para o nome e 512 carateres para a descrição.  

4.  A lista **Dados de configuração** apresenta todos os itens de configuração ou linhas de base de configuração que estão incluídos nesta linha de base de configuração. Clique em **Adicionar** para adicionar um novo item de configuração ou linha base de configuração à lista. Pode escolher entre os seguintes itens:  

    -   **Itens de Configuração**  

    -   **Atualizações de Software**  

    -   **Linhas de Base de Configuração**  
      > [!IMPORTANT]
      > Deve limitar cada linha de base de configuração para não mais de 1000 atualizações de software.
5.  Utilize o **alterar objetivo** lista para especificar o comportamento de um item de configuração que selecionou na **dados de configuração** lista. Pode selecionar os seguintes itens:  

    -   **Necessário**: A linha de base de configuração é avaliada como não conforme se o item de configuração não é detetado num dispositivo cliente. Se for detetado, é avaliado relativamente à conformidade  

    -   **Opcional**: O item de configuração é avaliado apenas de conformidade se a aplicação faz referência for encontrada nos computadores cliente. Se o aplicativo não for encontrado, a linha de base de configuração não está marcada como não conformes (apenas aplicável a itens de configuração de aplicação).  

    -   **Proibido**: A linha de base de configuração é avaliada como não conforme se o item de configuração for detetado nos computadores de cliente (apenas aplicáveis a itens de configuração de aplicação).  

    > [!NOTE]
    >  A lista **Alterar Objetivo** só está disponível se tiver clicado na opção **Este item de configuração contém as definições da aplicação** na página **Geral** do **Assistente de Criação de Item de Configuração**.  

6.  Utilize a lista **Alterar Revisão** para selecionar uma revisão específica ou a revisão mais recente do item de configuração para avaliar a compatibilidade nos dispositivos cliente ou selecione **Utilizar Sempre Mais Recente** para utilizar sempre a revisão mais recente. Para obter mais informações sobre revisões de item de configuração, consulte [tarefas de gestão para dados de configuração](../../compliance/deploy-use/management-tasks-for-configuration-data.md).  

7.  Para remover um item de configuração de linha de base de configuração, selecione um item de configuração e, em seguida, clique em **remover**.  

8. A partir da versão 1806, selecione se pretende **aplique sempre esta linha de base para clientes cogeridos**. Quando selecionado, esta linha de base será aplicada, mesmo em clientes que são geridos pelo Intune.  Essa exceção pode ser utilizada para configurar as definições que são necessárias pela sua organização, mas ainda não está disponível no Intune. 

9. Opcionalmente, clique em **categorias** para atribuir categorias para a linha de base de pesquisa e filtragem. 

10. Clique em **OK** para fechar a caixa de diálogo **Criar Linha de Base de Configuração** e para criar a linha de base de configuração.  

>[!NOTE]
> Modificar uma linha de base existente, como a definição **aplique sempre esta linha de base para clientes cogeridos**, aumentará a versão do conteúdo da linha de base. Os clientes terão a avaliar a nova versão para atualizar os relatórios de linha de base. 