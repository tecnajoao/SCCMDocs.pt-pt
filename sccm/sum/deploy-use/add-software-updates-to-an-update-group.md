---
title: "Adicionar as atualizações a um grupo de atualização - Configuration Manager | Documentos do Microsoft"
description: "Adiciona as atualizações de software a um grupo de atualização de software no seu ambiente, manualmente ou automaticamente."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 01/23/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: a0767664-fd60-46a8-9da5-86cc431ce53c
ms.translationtype: Machine Translation
ms.sourcegitcommit: 4e44e2b8f6baf020c3b7742bafd607082ffacaa4
ms.openlocfilehash: 02e30ba48f3564fa8a31f21793c145054e02e002
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---

# <a name="add-software-updates-to-an-update-group"></a>Adicionar atualizações de software a um grupo de atualizações  

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

 Os grupos de atualizações de software proporcionam-lhe um método eficaz para organizar as atualizações de software no seu ambiente. Pode adicionar manualmente atualizações de software a um grupo de atualizações de software ou adicionar as atualizações de software automaticamente a um grupo de atualizações de software utilizando uma ADR. Também pode implementar um grupo de atualizações de software manualmente ou implementar o grupo automaticamente, utilizando uma ADR. Depois de implementar um grupo de atualização de software, pode adicionar novas atualizações de software ao grupo e do Configuration Manager automaticamente implementá-las. Utilize os seguintes procedimentos para adicionar atualizações de software a um grupo de atualizações de software novo ou existente.  

#### <a name="to-add-software-updates-to-a-new-software-update-group"></a>Para adicionar atualizações de software a um novo grupo de atualizações de software  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho Biblioteca de Software, expanda **Atualizações de Software**e, em seguida, clique em **Todas as Atualizações de Software**.  

3.  Selecione as atualizações de software a serem adicionadas ao novo grupo de atualizações de software.  

4.  No separador **Home Page** , no grupo **Atualizar** , clique em **Criar Grupo de Atualização de Software**.  

5.  Especifique o nome para o grupo de atualizações de software e, opcionalmente, forneça uma descrição. Utilize um nome e uma descrição que forneçam informações suficientes para determinar qual o tipo de atualizações de software que fazem parte do grupo de atualizações de software. Para continuar, clique em **Criar**.  

6.  Clique em **Grupos de Atualização de Software** para apresentar o novo grupo de atualização de software.  

7.  Selecione o grupo de atualização de software e, no separador **Home Page** , no grupo **Atualizar** , clique em **Mostrar Membros** para apresentar uma lista das atualizações de software que estão incluídas no grupo.  

#### <a name="to-add-software-updates-to-an-existing-software-update-group"></a>Para adicionar atualizações de software a um grupo de atualização de software existente  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho Biblioteca de Software, expanda **Atualizações de Software**e, em seguida, clique em **Todas as Atualizações de Software**.  

3.  Selecione as atualizações de software que pretende adicionar ao novo grupo de atualizações de software.  

    > [!NOTE]  
    >  No **todas as atualizações de Software** nó, por predefinição, o Configuration Manager apresenta apenas atualizações de software com uma **crítico** e **segurança** classificação e que foram lançadas nos 30 últimos dias.  

4.  No separador **Home Page** , no grupo **Atualizar** , clique em **Editar Associação**.  

5.  Selecione o grupo de atualizações de software ao qual pretende adicionar as atualizações de software.  

6.  Clique no nó **Grupos de Atualização de Software** para apresentar o grupo de atualização de software.  

7.  Selecione o grupo de atualizações de software e, no separador **Home Page** , no grupo **Atualizar** , clique em **Mostrar Membros** para apresentar uma lista das atualizações de software que estão incluídas no grupo de atualizações de software.  

