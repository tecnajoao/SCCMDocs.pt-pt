---
title: Criar uma sequência de tarefas personalizado
titleSuffix: Configuration Manager
description: Edite uma sequência de tarefas personalizada no System Center Configuration Manager, para adicionar passos à sequência de tarefas.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b9800a66-7541-47ca-8276-da8ef6cb6d1b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7d71afc9ac8af973d43eac9ee7e1fb4322333d49
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56131698"
---
# <a name="create-a-custom-task-sequence-with-system-center-configuration-manager"></a>Criar uma sequência de tarefas personalizados com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Quando cria uma sequência de tarefas personalizada no System Center Configuration Manager, ele contém passos de sequência de tarefas. Depois de criar a sequência de tarefas, terá de editá-la e adicionar os passos de sequência de tarefas de que precisa.  

##  <a name="BKMK_CustomTS"></a> Criar uma sequência de tarefas personalizada  
 Utilize o procedimento seguinte para criar uma sequência de tarefas personalizada.  

#### <a name="to-create-a-custom-task-sequence"></a>Para criar uma sequência de tarefas personalizada  

1. Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2. Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**e clique em **Sequências de Tarefas**.  

3. No separador **Home Page** , no grupo **Criar** , clique em **Criar Sequência de Tarefas** para iniciar o Assistente de Criação de Sequência de Tarefas.  

4. Na página **Criar uma Nova Sequência de Tarefas** , selecione **Criar uma nova sequência de tarefas personalizada**.  

5. Na página **Informações da Sequência de Tarefas** , especifique um nome para a sequência de tarefas, uma descrição da sequência de tarefas e uma imagem de arranque opcional para a sequência de tarefas utilizar e, em seguida, conclua o assistente.  

   Depois de concluir o Assistente de criação de sequência de tarefas, o Configuration Manager adiciona a sequência de tarefas personalizada para o **sequências de tarefas** nó. Pode agora editar esta sequência de tarefas para lhe adicionar passos de sequência de tarefas.  

   Para obter uma lista dos passos de sequência de tarefas disponíveis, consulte [passos de sequência de tarefas](../understand/task-sequence-steps.md).  

   Para mais informações sobre como editar uma sequência de tarefas, consulte [Edit a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_ModifyTaskSequence).  

   Mais frequentemente irá utilizar as sequências de tarefas para automatizar as tarefas de implementação do sistema operativo, mas pode criar uma sequência de tarefas personalizada para automatizar uma variedade de tarefas. Para obter mais informações, consulte [criar uma sequência de tarefas para implementações do sistema de operativo](create-a-task-sequence-for-non-operating-system-deployments.md).  

   ## <a name="next-steps"></a>Passos seguintes
   [Implementar a sequência de tarefas](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
