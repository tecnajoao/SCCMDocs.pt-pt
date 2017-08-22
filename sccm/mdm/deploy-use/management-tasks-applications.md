---
title: "Gerir aplicações no System Center Configuration Manager | Microsoft Docs"
description: "Gerir aplicações no System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8adbe2e2-de26-4a80-8bbd-a5f34b8bac79
caps.latest.revision: "18"
caps.handback.revision: "0"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: bc7bb99bc526ed0bbaaad15fc9af39fa8b7c3893
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="manage-applications-in-system-center-configuration-manager"></a>Gerir aplicações no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Quando gerir dispositivos através do Microsoft Intune do Configuration Manager local ou na gestão de dispositivos, pode gerir estes tipos de aplicação adicional:
- Pacote de aplicação do Windows Phone (ficheiro *.xap)
- Pacote de Aplicações para iOS (ficheiro *.ipa)
- Pacote de Aplicações para Android (ficheiro *.apk)
- Pacote de aplicação para Android no Google Play
- Pacote de aplicação do Windows Phone (na Loja Windows Phone)
- Windows Installer através de MDM
- Aplicação Web

Esta secção fornece informações detalhadas sobre como criar e gerir aplicações através de MDM híbrida MDM ou no local

[Tarefas de gestão do System Center Configuration Manager aplicações](../../apps/deploy-use/management-tasks-applications.md) fornece informações mais gerais sobre a gestão de aplicações do System Center Configuration Manager e tipos de implementação.

## <a name="deploying-and-monitoring-apps"></a>Implementação e monitorização de aplicações

Implementar e monitorizar aplicações no System Center Configuration Manager são os processos para dispositivos móveis de dispositivos no local, como computadores portáteis e ambientes de trabalho. Pode leia os tópicos seguintes para obter informações gerais sobre a implementação e monitorização de aplicações:

- [Implementar aplicações no System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md)
- [Monitorizar aplicações no System Center Configuration Manager](../../apps/deploy-use/monitor-applications-from-the-console.md)

Seguem-se algumas considerações a lembrar quando implementar e monitorizar aplicações, específico para gestão de dispositivos móveis.

- Dispositivos inscritos de MDM não suportam implementações simuladas, experiência de utilizador ou as definições de agendamento.

- Pode associar a implementação com uma política de configuração de aplicação iOS, se já tiver congured um. Consulte [configurar aplicações iOS com políticas de configuração de aplicação](configure-ios-apps-with-app-configuration-policies.md).

### <a name="next-steps"></a>Passos Seguintes

Que poderão, eventualmente, pretende efetuar alterações a uma aplicação, desinstalar uma aplicação ou substituir uma aplicação já implementada por uma nova aplicação. Leia [atualizar e extinguir aplicações com o System Center Configuration Manager](../../apps/deploy-use/update-and-retire-applications.md) para compreender estas capacidades.
