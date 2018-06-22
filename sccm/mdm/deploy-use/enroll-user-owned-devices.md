---
title: Inscrever dispositivos propriedade do utilizador para implementações híbridas
titleSuffix: Configuration Manager
description: Saiba mais sobre métodos diferentes para inscrever dispositivos propriedade do utilizador para implementações híbridas com o Configuration Manager.
ms.date: 09/08/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 2bdaa8a7-6a64-4b0e-b617-309dcd912c45
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 198e5b65b85e10a1aa64f06361f1ba425e156662
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32345731"
---
# <a name="enroll-user-owned-devices-for-hybrid-deployments-with-configuration-manager"></a>Inscrever dispositivos propriedade do utilizador para implementações híbridas com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Dispositivos detidos podem ser colocados em gestão, inscrevendo-os, muitas vezes um processo chamado "traga a suas própria dispositivos" ou simplesmente "BYOD". Os utilizadores fazê-o ao instalar a aplicação Portal da empresa e iniciar sessão no dispositivo (iOS, macOS e Android) ou ao adicionar uma conta escolar ou profissional para o dispositivo e a associação a um domínio (Windows). Este processo inscreve o dispositivo no Intune, concedendo acesso de utilizador a recursos geridos pelo Intune e permitir que o Intune gerir determinadas definições de dispositivos, como exigir um PIN.

Para trazer dispositivos para gestão, como um administrador deve [configurar a gestão de dispositivos móveis](setup-hybrid-mdm.md) e [ativar a inscrição](enable-platform-enrollment.md). Quando a inscrição estiver ativada, os utilizadores podem inscrever os seus próprios dispositivos. Consulte [como informar os utilizadores finais sobre o Microsoft Intune no](https://docs.microsoft.com/intune/end-user-educate) para considerações e os passos para partilhar com os seus utilizadores.

As empresas ou escolas comprar dispositivos podem tirar partido de programas que permitem-lhe [gerir dispositivos pertencentes à empresa](enroll-company-owned-devices.md).
