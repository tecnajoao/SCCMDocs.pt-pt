---
title: Criar ambientes virtuais App-V
titleSuffix: Configuration Manager
description: Crie ambientes virtuais com o Microsoft Application Virtualization para que as aplicações podem partilhar dados entre si.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: b6b86078-fcc4-46cf-87d6-4b52b914b712
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e04b1d5662bb67ddb14310cd136abd6fdf29855d
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32331833"
---
# <a name="create-app-v-virtual-environments-in-system-center-configuration-manager"></a>Criar ambientes virtuais App-V no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

No Microsoft Application Virtualization (App-V) aplicações virtuais do ambiente virtual no System Center Configuration Manager (Gestor de configuração) implementada podem partilhar o mesmo sistema de ficheiros e registo em PCs com o cliente Windows. Ao contrário de aplicações virtuais padrão, estas aplicações podem partilhar dados entre si. Ambientes virtuais são criados ou modificados em computadores cliente quando a aplicação está instalada ou quando os clientes avaliam as aplicações instaladas. Pode ordenar estas aplicações para que a aplicação com a ordem mais elevada tenha prioridade quando várias aplicações tentarem modificar um sistema de ficheiros ou um valor de registo.  

> [!IMPORTANT]  
>  Não confie em ambientes virtuais do App-V para fornecer proteção de segurança, tal como contra software maligno.  

 Utilize o procedimento seguinte para criar um ambiente virtual App-V no Configuration Manager.  

## <a name="create-an-app-v-virtual-environment"></a>Criar um ambiente virtual App-V  

1.  Na consola do Configuration Manager, escolha **biblioteca de Software** > **gestão de aplicações** > **ambientes virtuais App-V**.  

3.  No **home page** separador o **criar** grupo, escolha **criar ambiente Virtual**.  

4.  No **criar ambiente Virtual** caixa de diálogo, introduza as seguintes informações:  

    -   **Nome**.  Introduza um nome exclusivo para o ambiente virtual (máximo de 128 carateres).  

    -   **Descrição**. (Opcional) Introduza uma descrição para o ambiente virtual.  

5.  Para adicionar um novo tipo de implementação para o ambiente virtual, escolha **adicionar**. Tem de adicionar pelo menos um tipo de implementação.  

6.  No **adicionar aplicações** diálogo caixa, especifique um **nome do grupo** (máximo de 128 carateres). Irá utilizar este nome para designar o grupo de aplicações que adicionou ao ambiente virtual.  

7.  Escolha **adicionar**, selecione as aplicações de App-V 5 e tipos de implementação que pretende adicionar ao grupo e, em seguida, escolha **OK**.  

8.  No **adicionar aplicações** caixa de diálogo, pode selecionar **aumentar a ordem** ou **diminuir a ordem** de definir a aplicação que utiliza a prioridade se várias aplicações tentarem modificar as definições de sistema ou o registo do ficheiro no mesmo ambiente virtual.  

9. Para voltar para o **criar ambiente Virtual** diálogo caixa, escolha **OK**.  

10. Quando tiver terminado de adicionar grupos, escolha **OK** para criar o ambiente virtual. O novo ambiente virtual é apresentado no **ambientes virtuais App-V** nós da consola do Configuration Manager. Pode monitorizar o estado dos ambientes virtuais utilizando o relatório de estado do ambiente Virtual App-V.  

    > [!NOTE]  
    >  O ambiente virtual é adicionado ou modificado em computadores cliente quando a aplicação está instalada ou quando o cliente avalia as aplicações instaladas.  
