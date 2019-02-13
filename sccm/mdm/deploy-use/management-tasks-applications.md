---
title: Gerir aplicações
titleSuffix: Configuration Manager
description: Gerir aplicações no System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 8adbe2e2-de26-4a80-8bbd-a5f34b8bac79
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4ff166d93812b07c37c31228ca395f0cfcf94de6
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56156962"
---
# <a name="manage-applications-in-system-center-configuration-manager"></a>Gerir aplicações no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Quando gerir dispositivos através do Microsoft Intune ou Configuration Manager no local-gestão de dispositivos, pode gerir estes tipos de aplicativo adicional:
- Pacote de aplicação do Windows Phone (ficheiro *.xap)
- Pacote de Aplicações para iOS (ficheiro *.ipa)
- Pacote de Aplicações para Android (ficheiro *.apk)
- Pacote de aplicação para Android no Google Play
- Pacote de aplicação do Windows Phone (na Loja Windows Phone)
- Windows Installer através de MDM
- Aplicação Web

Esta seção fornece informações detalhadas sobre como criar e gerir aplicações com a MDM híbrida MDM ou no local

[Tarefas de gestão para aplicações do System Center Configuration Manager](../../apps/deploy-use/management-tasks-applications.md) fornece mais informações sobre a gestão de aplicações do Microsoft System Center Configuration Manager e tipos de implementação.

## <a name="deploying-and-monitoring-apps"></a>Implementação e monitorização de aplicações

Implementar e monitorizar aplicações no System Center Configuration Manager são os mesmos processos para dispositivos móveis para dispositivos no local, como laptops e desktops. Pode ler os tópicos seguintes para obter informações gerais sobre como implementar e monitorizar aplicações:

- [Implementar aplicações no System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md)
- [Monitorizar aplicações no System Center Configuration Manager](../../apps/deploy-use/monitor-applications-from-the-console.md)

Aqui estão algumas considerações a ter em conta na implementação e monitorização de aplicações, específicas da gestão de dispositivos móveis.

- Dispositivos inscritos na MDM não suportam implementações simuladas, experiência do usuário ou definições de agendamento.

- Pode associar a implementação com uma política de configuração de aplicações iOS, se já tiver congured um. Ver [configurar aplicações iOS com políticas de configuração de aplicação](configure-ios-apps-with-app-configuration-policies.md).

### <a name="next-steps"></a>Passos Seguintes

Eventualmente, poderá querer efetuar alterações a uma aplicação, desinstalar um aplicativo ou substituir uma aplicação já implementada por uma nova aplicação. Leia [atualizar e extinguir aplicações com o System Center Configuration Manager](../../apps/deploy-use/update-and-retire-applications.md) para compreender estas capacidades.
