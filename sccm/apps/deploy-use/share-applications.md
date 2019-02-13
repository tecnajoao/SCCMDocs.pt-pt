---
title: Partilhar aplicações no Centro de Software
titleSuffix: Configuration Manager
description: Partilhe uma ligação a uma aplicação no Centro de Software no System Center Configuration Manager.
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e7a700482dad9f1ab2e41456596423fa23c15434
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56131052"
---
# <a name="share-an-application-from-software-center"></a>Partilhar uma aplicação do Centro de Software

*Aplica-se a: O System Center Configuration Manager (ramo atual)* <!-- 1706 -->

Pode copiar uma hiperligação a uma aplicação no Centro de Software com o ![partilha](media/share15.png)**partilha** botão na vista de detalhes da aplicação. Apenas pode partilhar as hiperligações para aplicações. Se a aplicação ficar indisponível, a hiperligação abre uma janela com uma mensagem de indisponível do aplicativo.

1. Escolher **aplicativos**e, em seguida, escolha a aplicação.
2. Clique nas ![partilha](media/share15.png) **partilha** botão.
3. Clique em **cópia** na janela.
4. Cole o URL de uma mensagem de e-mail para partilhar a aplicação.  

> [!TIP]  
>  Para criar uma hiperligação numa mensagem de e-mail do Outlook, prima **CTRL** + **K** e, em seguida, cole o URL.  
>  
> Por predefinição, o Outlook mostra um alerta de segurança para o protocolo de centro de Software quando o destinatário clica na ligação. Evitar esta situação no seu ambiente, adicionando uma chave de protocolo fidedigno para o registo. Por exemplo, `HKCU\Software\Policies\Microsoft\Office\16.0\Common\Security\Trusted Protocols\All Applications\softwarecenter:`  
