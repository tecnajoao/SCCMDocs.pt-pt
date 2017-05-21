---
title: "Atualizar e extinguir aplicações | Documentos do Microsoft"
description: "Rever, substituir ou desinstale as aplicações implementadas utilizando o System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 68ac8a07-8e54-4a3c-91e3-e50dc1cabf5d
caps.latest.revision: 9
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: c9fb0fa46058c773eec6ac23999357d35d9f970f
ms.openlocfilehash: 805e04c447747b4d12350b692880dbc005bd7168
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="update-and-retire-applications-with-system-center-configuration-manager"></a>Atualizar e extinguir aplicações com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


É provável que eventualmente irá pretende efetuar alterações a uma aplicação, desinstalar uma aplicação ou substituir uma aplicação já implementada por uma nova aplicação. System Center Configuration Manager disponibiliza-lhe estas capacidades, para o ajudar a atualizar e retirar aplicações:  

-   **Rever aplicações**. Quando fizer alterações a uma aplicação ou tipo de implementação, o Configuration Manager mantém um histórico das alterações. Pode reverter a aplicação para uma revisão anterior em qualquer altura. Também pode ver as respetivas propriedades, restaurar uma revisão anterior de uma aplicação ou eliminar uma revisão antiga.  

  Para obter mais informações, consulte o artigo [revisões de aplicação](revise-and-supersede-applications.md#application-revisions).  

-   **Substituir aplicações**. Pode atualizar ou substituir as aplicações existentes utilizando uma relação de substituição. Quando uma aplicação é substituída, pode especificar um novo tipo de implementação para substituir o tipo de implementação da aplicação substituída. Além disso, pode definir se a atualizar ou desinstalar a aplicação substituída antes da aplicação substituta está instalado.  

  Para obter mais informações, consulte o artigo [substituição de aplicações](revise-and-supersede-applications.md#application-supersedence).  

-   **Desinstalar aplicações**. O Configuration Manager torna a desinstalação de uma aplicação fácil. Isto pode ser conseguido automaticamente, sem qualquer intervenção da aplicação ou utilizador do dispositivo.  

  Para obter mais informações, consulte o artigo [desinstalar aplicações](uninstall-applications.md).  

