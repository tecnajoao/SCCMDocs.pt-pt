---
title: Desinstalar aplicações
titleSuffix: Configuration Manager
description: Desinstalar um aplicativo com o System Center Configuration Manager
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 0ea3edaa-27c6-4391-9896-cd97d9c5d06d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c0626b94d4ffe97b34a6c8376d6ebaa621d91d44
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56142073"
---
# <a name="uninstall-applications-with-system-center-configuration-manager"></a>Desinstalar aplicações com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Execute as ações seguintes para desinstalar uma aplicação que implementou anteriormente.

-   Especifique a linha de comando para desinstalar o conteúdo do tipo de implementação na **conteúdo** página do Assistente para criar tipo de implementação.  

-   Implemente a aplicação utilizando uma ação de implementação de **Desinstalar**.  

> [!IMPORTANT]  
> Alguns tipos de aplicações não suportam a desinstalação.  

 Esta lista dá-lhe obter mais informações sobre como funciona a desinstalação da aplicação:  

-   Quando desinstala uma aplicação do System Center Configuration Manager (Gestor de configuração), as aplicações dependentes não são automaticamente desinstaladas.  

-   Se implementar uma aplicação que utiliza uma ação de **desinstalação** para um utilizador e o aplicativo foi instalado para todos os utilizadores do computador, a desinstalação pode falhar se a conta de utilizador não tem permissões para desinstalar o aplicação.  

-   Se remover um utilizador ou um dispositivo de uma coleção que tenha uma aplicação implementada, a aplicação não é removida automaticamente do dispositivo.  

-   Uma implementação com o objetivo de implementação de **Desinstalar** não verifica as regras de requisitos. Se a aplicação estiver instalada no computador em que é executada a implementação, será desinstalada.  

> [!IMPORTANT]  
> Para implementar a aplicação com a ação de desinstalação, tem primeiro de eliminar quaisquer implementações de aplicações existentes, implementações simuladas ou implementações de sequência de tarefas que incluem esta aplicação. 

 Para obter mais informações sobre como criar um tipo de implementação, consulte [criem aplicativos](../../apps/deploy-use/create-applications.md).  

 Para obter mais informações sobre como implementar uma aplicação, consulte [implementar aplicações](../../apps/deploy-use/deploy-applications.md).  

## <a name="uninstall-an-application"></a>Desinstalar um aplicativo  

1.  Configure o tipo de implementação da aplicação com a linha de comandos de desinstalação utilizando um dos seguintes métodos:  

    -   Sobre o **gerais** página do Assistente para criar implementação, selecione a opção **identificar automaticamente informações sobre este tipo de implementação nos ficheiros de instalação**. Se as informações estiverem disponíveis nos ficheiros de instalação, a linha de comandos de desinstalação é automaticamente adicionada às propriedades do tipo de implementação.  

    -   Sobre o **conteúdo** página do Assistente para criar tipo de implementação, na **programa de desinstalação** campo, especifique a linha de comandos para desinstalar a aplicação.  

        > [!NOTE]  
        >  O **conteúdo** página só é apresentada se selecionar a opção **especificar manualmente as informações de tipo de implementação** sobre o **geral** página de criar tipo de implementação Assistente.  

    -   Sobre o **programas** separador da  **< *nome do tipo de implementação*> propriedades** caixa de diálogo caixa, especifique a linha de comandos para desinstalar a aplicação no  **Desinstalar programa** campo.  

2.  Implementar a aplicação e, em seguida, selecione a ação de implementação **desinstalação** sobre o **definições de implementação** página do Assistente de implementação de Software.  

    > [!NOTE]  
    >  Quando selecionar uma ação de implementação de **Desinstalar**, o objetivo de implementação é automaticamente configurado como **Necessário**.  
