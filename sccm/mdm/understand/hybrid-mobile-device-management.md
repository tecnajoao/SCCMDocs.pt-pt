---
title: "Híbrida gestão de dispositivos móveis (MDM) - Configuration Manager e o Microsoft Intune | Documentos do Microsoft"
description: "Saiba mais sobre gestão de dispositivos móveis (MDM) híbrida com o System Center Configuration Manager e o Microsoft Intune."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
caps.latest.revision: 34
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: e54478a03807c939ffa64ff39a21ef6f9ea4ae2d
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="hybrid-mobile-device-management-mdm-with-system-center-configuration-manager-and-microsoft-intune"></a>Gestão de dispositivos móveis híbridos (MDM) com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Pode gerir dispositivos Android com o Configuration Manager e o Microsoft Intune, Windows e iOS. Todas as tarefas de gestão são processadas a partir da consola do Configuration Manager em que executar o resto das suas tarefas de gestão totalmente integrado com o serviço online do Microsoft Intune através da internet.  Pode utilizar o Configuration Manager para permitir que os utilizadores aceder a recursos da empresa nos respetivos dispositivos de forma segura, geridos. Ao utilizar a gestão de dispositivos, é possível proteger dados da empresa, permitindo que os utilizadores inscrevam os respetivos dispositivos pessoais ou da empresa para aceder aos dados da empresa. Funcionalidades de gestão nos dispositivos:

-   Extinguir e apagar dispositivos
-   Configurar as definições de compatibilidade como palavras-passe, segurança, roaming, encriptação e comunicação wireless
-   Implementar aplicações de linha de negócio (LOB) para dispositivos
-   Implementar aplicações em dispositivos que se liguem à Windows Store, à Loja do Windows Phone, à App Store ou Google Play
-   Recolher inventário de hardware
-   Recolher inventário de software ao utilizar relatórios incorporados

Para ler sobre as novas funcionalidades estão disponíveis para uma implementação híbrida MDM, consulte [quais são as novidades na gestão de dispositivos móveis híbrida](../understand/whats-new-in-hybrid-mobile-device-management.md).

Este documento assume que está a utilizar o Configuration Manager para gerir computadores e que está interessado em expandir a consola do Configuration Manager com o Intune para gerir dispositivos móveis. Para compreender as diferenças entre a gestão de dispositivos móveis do Intune e híbrida, consulte o artigo [escolher entre o Microsoft Intune de autónomas e híbrida de gestão de dispositivos móveis com o System Center Configuration Manager](choose-between-standalone-intune-and-hybrid-mobile-device-management.md).

Após expandir do Configuration Manager com o Intune, pode inscrever e gerir os dispositivos da empresa ou dar aos utilizadores permissão para inscreverem os dispositivos pessoais. Também pode gerir dispositivos pertencentes à empresa com o Intune utilizando o Configuration Manager.

## <a name="hybrid-mdm-enrollment"></a>Inscrição na MDM híbrida
Para trazer dispositivos para gestão híbrida, esses dispositivos têm de ser inscritos com o serviço. Como os dispositivos inscritos dispositivos depende do tipo de dispositivo, a propriedade e o nível de gestão necessário.
- "Bring your own device" inscrição (BYOD) permite que os utilizadores inscrevam os respetivos pessoas telemóveis, tablets ou PCs.
- Inscrição de dispositivos de empresa (COD) permite cenários de gestão, tal como a eliminação remota, dispositivos partilhados ou afinidade do utilizador para um dispositivo.
- Se utilizar [do Exchange ActiveSync](../plan-design/device-enrollment-methods.md#mobile-device-management-with-exchange-activesync-and-configuration-manager), ambos no local ou alojado na nuvem, pode ativar a gestão do Intune simple sem inscrição. Windows PCs também podem ser geridos através de [software de cliente Intune](/intune/deploy-use/manage-windows-pcs-with-microsoft-intune).

