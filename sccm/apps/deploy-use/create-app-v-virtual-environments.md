---
title: Criar ambientes virtuais App-V
titleSuffix: Configuration Manager
description: Crie ambientes virtuais com o Microsoft Application Virtualization, para que as aplicações podem partilhar dados entre si.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: b6b86078-fcc4-46cf-87d6-4b52b914b712
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2becf31d807f0854bf6ab9d4eb58adf84d8ab7e6
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56135767"
---
# <a name="create-app-v-virtual-environments-in-system-center-configuration-manager"></a>Criar ambientes virtuais App-V no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

No Microsoft Application Virtualization (App-V), aplicações virtuais de ambiente virtual no System Center Configuration Manager (Gestor de configuração), implementada podem partilhar o mesmo sistema de ficheiros e registo nos PCs do cliente Windows. Ao contrário de aplicações virtuais padrão, estas aplicações podem partilhar dados entre si. Ambientes virtuais são criados ou modificados em PCs cliente quando a aplicação está instalada ou quando os clientes avaliam as aplicações instaladas. Pode ordenar estas aplicações para que a aplicação com a ordem mais elevada tenha prioridade quando várias aplicações tentarem modificar um sistema de ficheiros ou um valor de registo.  

> [!IMPORTANT]  
>  Não confie em ambientes virtuais do App-V para fornecer proteção de segurança, por exemplo, contra software maligno.  

 Utilize o procedimento seguinte para criar um ambiente virtual de App-V no Configuration Manager.  

## <a name="create-an-app-v-virtual-environment"></a>Criar um ambiente virtual de App-V  

1.  Na consola do Configuration Manager, escolha **biblioteca de Software** > **gestão de aplicações** > **ambientes virtuais App-V**.  

3.  Sobre o **home page** separador a **criar** de grupo, escolha **criar ambiente Virtual**.  

4.  Na **criar ambiente Virtual** caixa de diálogo, introduza as seguintes informações:  

    -   **Nome**.  Introduza um nome exclusivo para o ambiente virtual (máximo de 128 carateres).  

    -   **Descrição**. (Opcional) Introduza uma descrição para o ambiente virtual.  

5.  Para adicionar um novo tipo de implementação para o ambiente virtual, escolha **adicionar**. Tem de adicionar pelo menos um tipo de implementação.  

6.  Na **adicionar aplicações** caixa de diálogo caixa, especifique um **nome do grupo** (máximo de 128 carateres). Irá utilizar este nome para designar o grupo de aplicações que adicionou ao ambiente virtual.  

7.  Escolher **Add**, selecione as aplicações de App-V 5 e tipos de implementação que pretende adicionar ao grupo e, em seguida, escolha **OK**.  

8.  Na **adicionar aplicações** caixa de diálogo, pode selecionar **aumentar a ordem** ou **diminuir a ordem** para definir a aplicação que tem prioridade se várias aplicações tentarem modifica definições de sistema ou registo de ficheiros no mesmo ambiente virtual.  

9. Para voltar para o **criar ambiente Virtual** caixa de diálogo caixa, escolha **OK**.  

10. Quando tiver terminado a adição de grupos, escolha **OK** para criar o ambiente virtual. O novo ambiente virtual é apresentado na **ambientes virtuais App-V** nó da consola do Configuration Manager. Pode monitorizar o estado dos ambientes virtuais utilizando o relatório de estado do ambiente Virtual App-V.  

    > [!NOTE]  
    >  O ambiente virtual é adicionado ou modificado nos PCs cliente quando a aplicação está instalada ou quando o cliente avalia as aplicações instaladas.  
