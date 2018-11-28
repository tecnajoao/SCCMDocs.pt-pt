---
title: Gerir pacotes de atualização do SO
titleSuffix: Configuration Manager
description: Saiba como gerir pacotes de atualização do sistema operacional no Configuration Manager.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b9b22655-b8c1-461f-8047-3a7e906f647a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f7b8b18cbec5a3b5972a448e8a70339533dc11fb
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52456014"
---
# <a name="manage-os-upgrade-packages-with-configuration-manager"></a>Gerir pacotes de atualização de SO com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Um pacote de atualização do sistema operacional no Configuration Manager contém os arquivos de origem de instalação do Windows para atualizar um sistema operacional existente num computador. Este artigo descreve como adicionar, distribuir e um pacote de atualização do sistema operacional de serviço.



##  <a name="BKMK_AddOSUpgradePkgs"></a> Adicionar um pacote de atualização de SO  

Antes de poder utilizar um pacote de atualização de SO, primeiro adicioná-lo para o seu site do Configuration Manager. 

1.  Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho, expanda **sistemas operativos**e, em seguida, selecione o **pacotes de atualização do sistema operativo** nó .  

2.  Sobre o **home page** separador do Friso, no **criar** grupo, selecione **Adicionar pacote de atualização do sistema operativo**. Esta ação inicia o sistema operativo atualizar o Assistente para adicionar.  

3.  Sobre o **origem de dados** página, especifique as seguintes definições: 

    - A rede **caminho** à instalação do pacote de atualização de ficheiros de origem do sistema operacional. Por exemplo, `\\server\share\path`.  

        > [!NOTE]  
        >  Os ficheiros de origem de instalação contêm setup.exe e outros ficheiros e pastas para instalar o sistema operacional.  

        > [!IMPORTANT]  
        >  Limitar o acesso a estes ficheiros de origem de instalação para impedir a adulteração indesejável.  

    - Se quiser pré-colocar em cache conteúdo num cliente, especifique a **arquitetura** e **linguagem** da imagem. Para obter mais informações, consulte [configurar pré-armazenar conteúdo em cache](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content).  

4.  Sobre o **gerais** , especifique as seguintes informações. Estas informações são úteis para fins de identificação quando tem mais do que um sistema operacional de pacote de atualização.  

    -   **Nome**: Pacote de atualização de um nome exclusivo para o sistema operacional.  

    -   **Versão**: Um identificador de versão opcional. Esta propriedade não precisa ser a versão do pacote de atualização do SO. É, muitas vezes, versão da sua organização para o pacote.  

    -   **Comentário**: Uma breve descrição opcional.  

5.  Conclua o assistente.  


Em seguida, distribua o pacote de atualização de SO para pontos de distribuição.  



##  <a name="BKMK_Distribute"></a> Distribuir conteúdo para um ponto de distribuição  

Pacotes de atualização do SO para pontos de distribuição distribua o mesmo que outro conteúdo. Antes de implementar a sequência de tarefas, distribua o pacote de atualização de SO para, pelo menos, um ponto de distribuição. Para mais informações, consulte [Distribute content](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute).  



[!INCLUDE [Apply software updates to an image](includes/wim-apply-updates.md)]



## <a name="next-steps"></a>Passos seguintes

[Criar uma sequência de tarefas para atualizar um SO](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system)