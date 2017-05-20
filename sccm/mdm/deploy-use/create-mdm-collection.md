---
title: "Criar uma coleção de MDM com o System Center Configuration Manager | Documentos do Microsoft"
description: "Crie uma coleção de MDM com o System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d1b4337f-85e8-45e6-8bbe-9f18b49041c7
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: fabbcfd2d5656d4fa8cb87feffe87e17998df145
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="create-an-mdm-collection-with-system-center-configuration-manager-and-microsoft-intune"></a>Criar uma coleção de MDM com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Uma coleção de utilizador do Configuration Manager é necessário para especificar os utilizadores que podem inscrever dispositivos para gestão. Só pode utilizar coleções de utilizadores (em vez de coleções de dispositivos) porque licenças do Intune são atribuídas pelo utilizador.

> [!NOTE]
> Para inscrever dispositivos com o Intune, não é necessário atribuir licenças aos utilizadores no portal do Office 365 ou no portal do Azure Active Directory. Incluindo os utilizadores numa coleção que obtém associada com a subscrição do Intune (num [mais tarde passo](configure-intune-subscription.md)) é tudo o que seja necessário.

Para fins de teste, pode configurar um **regra direta** e adicionar utilizadores específicos que podem inscrever dispositivos. Na consola do Configuration Manager athe, escolha, **ativos e compatibilidade** > **coleções de utilizadores**, clique na **base** separador > **criar** grupo e, em seguida, clique em **criar coleção de utilizadores**. Para mais abrangente sobre distribuição deverá utilizar **regras de consulta** para definir os utilizadores. Para obter mais informações sobre coleções, consulte o artigo [como criar coleções](https://technet.microsoft.com/library/mt629371.aspx).

![Criar uma coleção de utilizadores por MDM](../media/mdm-create-user-collection.png)

> [!div class="button"]
[Passo seguinte >](confirm-dns.md)

