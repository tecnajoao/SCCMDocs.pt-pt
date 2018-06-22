---
title: Gestão de dispositivos móveis híbridos (MDM) com o Microsoft Intune
titleSuffix: Configuration Manager
description: Saiba mais sobre a gestão de dispositivos móveis híbridos (MDM) com o System Center Configuration Manager e o Microsoft Intune.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c8651b5a82c4e3cb4e39fac53cc5bc3357df6e47
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32346635"
---
# <a name="hybrid-mobile-device-management-mdm-with-system-center-configuration-manager-and-microsoft-intune"></a>Gestão de dispositivos móveis híbridos (MDM) com o System Center Configuration Manager e o Microsoft Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Pode gerir iOS, Windows e dispositivos Android com o Configuration Manager e o Microsoft Intune. Todas as tarefas de gestão são processadas a partir da consola do Configuration Manager onde efetuar o resto das suas tarefas de gestão totalmente integrada com o serviço online do Microsoft Intune através da internet.  Pode utilizar o Configuration Manager para permitir que os utilizadores aceder a recursos da empresa nos respetivos dispositivos de modo seguro e gerido. Ao utilizar a gestão de dispositivos, proteger os dados da empresa, permitindo que os utilizadores inscrevam os respetivos dispositivos pessoais ou da empresa para aceder aos dados da empresa. Capacidades de gestão nos dispositivos:

-   Extinguir e apagar dispositivos
-   Configurar as definições de compatibilidade como palavras-passe, segurança, roaming, encriptação e comunicação wireless
-   Implementar aplicações de linha de negócio (LOB) em dispositivos
-   Implementar aplicações em dispositivos que se liguem à Windows Store, à Loja do Windows Phone, à App Store ou Google Play
-   Recolher inventário de hardware
-   Recolher inventário de software ao utilizar relatórios incorporados

Para ler sobre as novas funcionalidades estão disponíveis para MDM híbrida, consulte [são as novidades na gestão de dispositivos móveis híbridos](../understand/whats-new-in-hybrid-mobile-device-management.md).

Este documento parte do princípio de que está a utilizar o Configuration Manager para gerir computadores e que está interessado em expandir a consola do Configuration Manager com o Intune para gerir dispositivos móveis. Para compreender as diferenças entre a gestão de dispositivos móveis do Intune e híbrido, consulte [escolha entre o Microsoft Intune de autónomo e híbrida de gestão de dispositivos móveis com o System Center Configuration Manager](choose-between-standalone-intune-and-hybrid-mobile-device-management.md).

Após expandir o Configuration Manager com o Intune, pode inscrever e gerir dispositivos pertencentes à empresa ou conceder aos utilizadores permissão para inscreverem os respetivos dispositivos pessoais. Também pode gerir dispositivos pertencentes à empresa com o Intune com o Configuration Manager.

## <a name="hybrid-mdm-enrollment"></a>Inscrição na MDM híbrida
Para trazer dispositivos para gestão híbrida, esses dispositivos têm de estar inscritos com o serviço. Como os dispositivos inscritos dispositivos dependem do tipo de dispositivo, propriedade e o nível de gestão necessário.
- "Bring your own device" inscrição (BYOD) permite aos utilizadores inscrever os respetivos pessoais telemóveis, tablets ou PCs.
- Inscrição de dispositivos pertencentes à empresa (COD) permite cenários de gestão, como eliminação remota, dispositivos partilhados ou afinidade de utilizador para um dispositivo.
- Se utilizar [do Exchange ActiveSync](../plan-design/device-enrollment-methods.md#mobile-device-management-with-exchange-activesync-and-configuration-manager), no local ou alojado na nuvem, pode ativar a gestão do Intune simple sem inscrição. Os PCs Windows também podem ser geridos utilizando [software de cliente Intune](/intune/deploy-use/manage-windows-pcs-with-microsoft-intune).
