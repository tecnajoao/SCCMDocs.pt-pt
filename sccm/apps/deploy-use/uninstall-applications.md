---
title: "Desinstalar aplicações"
titleSuffix: Configuration Manager
description: "Desinstalar uma aplicação utilizando o System Center Configuration Manager"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0ea3edaa-27c6-4391-9896-cd97d9c5d06d
caps.latest.revision: "4"
caps.handback.revision: "0"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: 11b6f7ad65296131622b707fcb68d77183e3a288
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="uninstall-applications-with-system-center-configuration-manager"></a>Desinstalar aplicações com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Execute as ações seguintes para desinstalar uma aplicação que implementou anteriormente.

-   Especifique a linha de comandos para desinstalar o conteúdo do tipo de implementação do **conteúdo** página do Assistente para criar tipo de implementação.  

-   Implemente a aplicação utilizando uma ação de implementação de **Desinstalar**.  

> [!IMPORTANT]  
> Alguns tipos de aplicações não suportam a desinstalação.  

 Esta lista dá-lhe obter mais informações sobre como funciona a desinstalação da aplicação:  

-   Quando desinstala uma aplicação do System Center Configuration Manager (Gestor de configuração), quaisquer aplicações dependentes não são automaticamente desinstaladas.  

-   Se implementar uma aplicação que utiliza uma ação de **desinstalação** para um utilizador e a aplicação foi instalada para todos os utilizadores do computador, a desinstalação pode falhar se a conta de utilizador não tem permissões para desinstalar a aplicação.  

-   Se remover um utilizador ou um dispositivo de uma coleção que tenha uma aplicação implementada, a aplicação não é removida automaticamente do dispositivo.  

-   Uma implementação com o objetivo de implementação de **Desinstalar** não verifica as regras de requisitos. Se a aplicação estiver instalada no computador em que é executada a implementação, será desinstalada.  

> [!IMPORTANT]  
> Tem de eliminar todas as implementações ou implementações simuladas existentes de uma aplicação numa coleção para poder implementar a aplicação com uma ação de implementação de **Desinstalar**.  

 Para obter mais informações sobre como criar um tipo de implementação, consulte [criar aplicações](../../apps/deploy-use/create-applications.md).  

 Para obter mais informações sobre como implementar uma aplicação, consulte [implementar aplicações](../../apps/deploy-use/deploy-applications.md).  

## <a name="uninstall-an-application"></a>Desinstalar uma aplicação  

1.  Configure o tipo de implementação da aplicação com a linha de comandos de desinstalação utilizando um dos seguintes métodos:  

    -   No **geral** página do Assistente de implementação de criação, selecione a opção **identificar automaticamente informações sobre este tipo de implementação nos ficheiros de instalação**. Se as informações estiverem disponíveis nos ficheiros de instalação, a linha de comandos de desinstalação é automaticamente adicionada às propriedades do tipo de implementação.  

    -   No **conteúdo** página do Assistente para criar tipo de implementação, no **programa de desinstalação** campo, especifique a linha de comandos para desinstalar a aplicação.  

        > [!NOTE]  
        >  O **conteúdo** página só é apresentada se selecionar a opção **especificar manualmente as informações de tipo de implementação** no **geral** página do Assistente para criar tipo de implementação.  

    -   No **programas** separador do  **<* nome do tipo de implementação*> propriedades * * a caixa de diálogo caixa, especifique a linha de comandos para desinstalar a aplicação no **programa de desinstalação** campo.  

2.  Implemente a aplicação e, em seguida, selecione a ação de implementação **desinstalação** no **definições de implementação** página do Assistente de implementação de Software.  

    > [!NOTE]  
    >  Quando selecionar uma ação de implementação de **Desinstalar**, o objetivo de implementação é automaticamente configurado como **Necessário**.  
