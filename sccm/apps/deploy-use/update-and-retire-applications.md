---
title: Atualizar e extinguir aplicações
titleSuffix: Configuration Manager
description: Revisar, substituir ou desinstalar aplicações implementadas com o System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 68ac8a07-8e54-4a3c-91e3-e50dc1cabf5d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8a58e16819a9f207bea98ed799e709268c3b5d37
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53423359"
---
# <a name="update-and-retire-applications-with-system-center-configuration-manager"></a>Atualizar e extinguir aplicações com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


É provável que, eventualmente, vai querer fazer alterações a uma aplicação, desinstalar um aplicativo ou substituir uma aplicação já implementada por uma nova aplicação. System Center Configuration Manager-lhe essas capacidades, para o ajudar a atualizar e extinguir aplicações:  

- **Rever aplicações**. Quando fizer alterações a uma aplicação ou tipo de implementação, o Configuration Manager mantém um histórico das alterações. Pode reverter a aplicação para uma revisão anterior em qualquer altura. Também pode ver as respetivas propriedades, restaurar uma revisão anterior de uma aplicação ou eliminar uma revisão antiga.  

  Para obter mais informações, consulte [revisões de aplicações](revise-and-supersede-applications.md#application-revisions).  

- **Substituir aplicações**. Pode atualizar ou substituir as aplicações existentes utilizando uma relação de substituição. Quando uma aplicação é substituída, pode especificar um novo tipo de implementação para substituir o tipo de implementação da aplicação substituída. Além disso, pode definir se atualizar ou desinstalar a aplicação substituída antes da aplicação substituta está instalado.  

  Para obter mais informações, consulte [substituição de aplicações](revise-and-supersede-applications.md#application-supersedence).  

- **Desinstalar aplicações**. O Configuration Manager torna a desinstalação de uma aplicação. Pode fazê-lo silenciosamente, sem qualquer intervenção do utilizador do dispositivo ou aplicação.  

  Para obter mais informações, consulte [desinstalar aplicações](uninstall-applications.md).  
