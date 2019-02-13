---
title: Inscrever dispositivos pertencentes ao utilizador para implementações híbridas
titleSuffix: Configuration Manager
description: Saiba mais sobre os diferentes métodos para inscrever dispositivos pertencentes ao utilizador para implementações híbridas com o Configuration Manager.
ms.date: 09/08/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 2bdaa8a7-6a64-4b0e-b617-309dcd912c45
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8b6d56309238acc2889ac39ab39d5982fb8d535c
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56124443"
---
# <a name="enroll-user-owned-devices-for-hybrid-deployments-with-configuration-manager"></a>Inscrever dispositivos pertencentes ao utilizador para implementações híbridas com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Dispositivos propriedade do utilizador podem ser colocados em gestão, inscrevendo-os, muitas vezes um processo chamado "traga seu próprio dispositivos" ou simplesmente "BYOD". Os utilizadores fazê-lo ao instalar a aplicação Portal da empresa e iniciar sessão no dispositivo (iOS, macOS e Android) ou ao adicionar uma conta profissional ou escolar ao dispositivo e a associação a um domínio (Windows). Este processo inscreve o dispositivo com o Intune, dar ao usuário acesso a recursos geridos pelo Intune e permitir que o Intune faça a gestão de determinadas definições do dispositivo, como exigir um PIN.

Para trazer dispositivos para gestão, como um administrador deve primeiro [configurar a gestão de dispositivos móveis](setup-hybrid-mdm.md) e [ativar a inscrição](enable-platform-enrollment.md). Assim que a inscrição é ativada, os utilizadores podem inscrever os seus dispositivos. Ver [como dar formação aos seus utilizadores finais sobre o Microsoft Intune](https://docs.microsoft.com/intune/end-user-educate) para obter considerações e passos para partilhar com os seus utilizadores.

As empresas ou escolas que compram dispositivos podem tirar partido dos programas que permitem-lhe [gerir dispositivos pertencentes à empresa](enroll-company-owned-devices.md).
