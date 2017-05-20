---
title: Crie ambientes virtuais App-V | Documentos do Microsoft
description: "Crie ambientes virtuais com o Microsoft Application Virtualization para que aplicações podem partilhar dados entre si."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b6b86078-fcc4-46cf-87d6-4b52b914b712
caps.latest.revision: 6
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: aa9e87830a3a51b01fae29b564c9267ec930a60d
ms.openlocfilehash: 377ed9732fb16b062f53e78504aea394acdb7462
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="create-app-v-virtual-environments-in-system-center-configuration-manager"></a>Crie ambientes virtuais do App-V no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

No Microsoft Application Virtualization (App-V) o ambiente virtual no System Center Configuration Manager (Gestor de configuração), implementada aplicações virtuais podem partilhar o mesmo sistema de ficheiros e registo nos PCs Windows de cliente. Contrariamente às aplicações virtuais padrão, estas aplicações podem partilhar dados entre si. Ambientes virtuais são criados ou modificados em computadores cliente quando a aplicação é instalada ou quando os clientes avaliam as aplicações instaladas. Pode ordenar estas aplicações para que a aplicação com a ordem mais elevada tenha prioridade quando várias aplicações tentarem modificar um sistema de ficheiros ou um valor de registo.  

> [!IMPORTANT]  
>  Não confie em ambientes virtuais do App-V para fornecer proteção de segurança, tal como contra software maligno.  

 Utilize o procedimento seguinte para criar um ambiente virtual de App-V no Configuration Manager.  

## <a name="create-an-app-v-virtual-environment"></a>Criar um ambiente virtual de App-V  

1.  Na consola do Configuration Manager, escolha **biblioteca de Software** > **gestão de aplicações** > **ambientes virtuais App-V**.  

3.  No **base** separador o **criar** grupo, selecione **criar ambiente Virtual**.  

4.  No **criar ambiente Virtual** diálogo caixa, introduza as seguintes informações:  

    -   **Nome**.  Introduza um nome exclusivo para o ambiente virtual (máximo de 128 carateres).  

    -   **Descrição**. (Opcional) Introduza uma descrição para o ambiente virtual.  

5.  Para adicionar um novo tipo de implementação para o ambiente virtual, selecione **adicionar**. Tem de adicionar pelo menos um tipo de implementação.  

6.  No **adicionar aplicações** diálogo caixa, especifique um **nome do grupo** (máximo de 128 carateres). Irá utilizar este nome referir-se para o grupo de aplicações que adicionou ao ambiente virtual.  

7.  Escolher **adicionar**, selecione as aplicações de App-V 5 e tipos de implementação que pretende adicionar ao grupo e, em seguida, selecione **OK**.  

8.  No **adicionar aplicações** caixa de diálogo, pode selecionar **aumentar a ordem** ou **diminuir a ordem** para definir a aplicação que tem prioridade se várias aplicações tentarem modificar as definições de sistema ou do registo do ficheiro do mesmo ambiente virtual.  

9. Para voltar para o **criar ambiente Virtual** diálogo caixa, selecione **OK**.  

10. Quando tiver concluído a adição de grupos, escolha **OK** para criar o ambiente virtual. O novo ambiente virtual é apresentado no **ambientes virtuais App-V** nó da consola do Configuration Manager. Pode monitorizar o estado dos ambientes virtuais utilizando o relatório de estado do ambiente Virtual App-V.  

    > [!NOTE]  
    >  O ambiente virtual é adicionado ou modificado nos computadores cliente quando a aplicação é instalada ou quando o cliente avalia as aplicações instaladas.  

