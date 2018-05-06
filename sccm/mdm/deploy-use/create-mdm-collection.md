---
title: Criar uma coleção de MDM
titleSuffix: Configuration Manager
description: Crie uma coleção de MDM com o System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: d1b4337f-85e8-45e6-8bbe-9f18b49041c7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d271499baf48364fe24a8961cae767c46d05a332
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="create-an-mdm-collection-with-system-center-configuration-manager-and-microsoft-intune"></a>Criar uma coleção de MDM com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Uma coleção de utilizadores do Gestor de configuração é necessário especificar os utilizadores podem inscrever dispositivos para gestão. Só pode utilizar coleções de utilizadores (em vez de coleções de dispositivos) porque licenças do Intune são atribuídas pelo utilizador.

> [!NOTE]
> Para inscrever dispositivos com o Intune, não terá de atribuir licenças aos utilizadores no portal do Office 365 ou portal do Azure Active Directory. Incluindo os utilizadores numa coleção que obtém associada à subscrição do Intune (num [passo posterior](configure-intune-subscription.md)) é tudo o que é necessário.

Para fins de teste que pode configurar um **regra direta** e adicionar utilizadores específicos que podem inscrever dispositivos. Na consola do Configuration Manager, escolha, **ativos e compatibilidade** > **coleções de utilizadores**, clique em de **home page** separador > **criar** grupo e, em seguida, clique em **criar coleção de utilizador**. Para distribuição mais vasto, deve utilizar **consultar regras** para definir os utilizadores. Para obter mais informações sobre coleções, consulte [como criar coleções](https://technet.microsoft.com/library/mt629371.aspx).

![Criar uma coleção de utilizador da MDM](../media/mdm-create-user-collection.png)

> [!div class="button"]
[Passo seguinte >](confirm-dns.md)
