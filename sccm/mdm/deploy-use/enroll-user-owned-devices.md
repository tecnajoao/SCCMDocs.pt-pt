---
title: "Inscrever dispositivos propriedade do utilizador para implementações híbridas com o Configuration Manager | Microsoft Docs"
description: "Saiba mais sobre métodos diferentes para inscrever dispositivos propriedade do utilizador para implementações híbridas com o Configuration Manager."
ms.custom: na
ms.date: 09/08/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bdaa8a7-6a64-4b0e-b617-309dcd912c45
caps.latest.revision: "13"
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 56bd6bfd900a8ecbb149392de62889970ddedb60
ms.sourcegitcommit: 40f2a4e3cc546e6bfd10f195a8e87af2b0780928
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/08/2017
---
# <a name="enroll-user-owned-devices-for-hybrid-deployments-with-configuration-manager"></a>Inscrever dispositivos propriedade do utilizador para implementações híbridas com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Dispositivos detidos podem ser colocados em gestão, inscrevendo-os, muitas vezes um processo chamado "traga a suas própria dispositivos" ou simplesmente "BYOD". Os utilizadores fazê-o ao instalar a aplicação Portal da empresa e iniciar sessão no dispositivo (iOS, macOS e Android) ou ao adicionar uma conta escolar ou profissional para o dispositivo e a associação a um domínio (Windows). Este processo inscreve o dispositivo no Intune, concedendo acesso de utilizador a recursos geridos pelo Intune e permitir que o Intune gerir determinadas definições de dispositivos, como exigir um PIN.

Para trazer dispositivos para gestão, como um administrador deve [configurar a gestão de dispositivos móveis](setup-hybrid-mdm.md) e [ativar a inscrição](enable-platform-enrollment.md). Quando a inscrição estiver ativada, os utilizadores podem inscrever os seus próprios dispositivos. Consulte [como informar os utilizadores finais sobre o Microsoft Intune no](https://docs.microsoft.com/intune/end-user-educate) para considerações e os passos para partilhar com os seus utilizadores.

As empresas ou escolas comprar dispositivos podem tirar partido de programas que permitem-lhe [gerir dispositivos pertencentes à empresa](enroll-company-owned-devices.md).
