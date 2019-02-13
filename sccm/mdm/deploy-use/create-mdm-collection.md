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
ms.collection: M365-identity-device-management
ms.openlocfilehash: f0288b88187ead39f1cf584ebf88e3943549b01f
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56124017"
---
# <a name="create-an-mdm-collection-with-system-center-configuration-manager-and-microsoft-intune"></a>Criar uma coleção de MDM com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Uma coleção de utilizadores do Gestor de configuração é necessária para especificar os utilizadores que podem inscrever dispositivos para gestão. Só pode utilizar coleções de utilizadores (em vez de coleções de dispositivos), porque as licenças do Intune são atribuídas pelo utilizador.

> [!NOTE]
> Para inscrever dispositivos com o Intune, não é necessário atribuir licenças aos utilizadores no portal do Office 365 ou do portal do Azure Active Directory. Incluindo os utilizadores numa coleção que é associada com a subscrição do Intune (num [mais tarde passo](configure-intune-subscription.md)) é tudo o que é necessário.

Para fins de teste pode configurar uma **regra direta** e adicione utilizadores específicos que podem inscrever dispositivos. Na consola do Configuration Manager, escolha, **ativos e compatibilidade** > **coleções de utilizadores**, clique no **base** separador > **Create**  agrupar e, em seguida, clique em **criar coleção de utilizadores**. Para mais ampla distribuição deve usar **consultar regras** definir que os utilizadores. Para obter mais informações sobre as coleções, consulte [como criar coleções](https://technet.microsoft.com/library/mt629371.aspx).

![Criar uma coleção de utilizadores para MDM](../media/mdm-create-user-collection.png)

> [!div class="button"]
> [Passo seguinte >](confirm-dns.md)
