---
title: Criar aplicações iOS
titleSuffix: Configuration Manager
description: Como criar e implementar aplicações para dispositivos iOS no Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: ff633013-5313-4cd3-949c-56d45e777280
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e4a2d84fe31c3a524b876e3beb34f0e3d25d0089
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56125447"
---
# <a name="create-ios-applications-in-configuration-manager"></a>Criar aplicações iOS no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Uma aplicação do Configuration Manager tem uma ou mais tipos de implementação que compõem os ficheiros de instalação e informações que são necessários para implementar software num dispositivo. Um tipo de implementação também possui regras que especificam quando e como o software é implementado.  

Ver [criar uma aplicação](/sccm/apps/deploy-use/create-applications#bkmk_create) para obter os passos criar aplicações do Configuration Manager e tipos de implementação. 

Tenha em atenção as seguintes considerações ao criar e implementar aplicações para dispositivos iOS:  

- O Configuration Manager suporta a implementação de pacotes do iOS. IPA. Não precisa de especificar um ficheiro de lista (. plist) de propriedade ao importar uma aplicação iOS. 

- Implementar aplicações iOS como **disponível** ou **necessário**. O utilizador tenha de consentir a instalação e desinstalação.

> [!IMPORTANT]  
>  Atualmente, os utilizadores finais não podem instalar aplicações empresariais a partir da aplicação Portal da empresa do Microsoft Intune para iOS. Esta limitação é porque há restrições sobre aplicações publicadas na iOS App Store. (Consulte App Store Review Guidelines, secção 2). Os utilizadores podem instalar aplicações empresariais ao navegar para o portal do Intune nos respetivos dispositivos. Estas aplicações incluem aplicações geridas da App Store e pacotes de aplicações de linha de negócio. Para obter mais informações sobre as capacidades de gestão de dispositivos móveis que permite a aplicação Portal da empresa do Intune, consulte [funcionalidades de gestão de dispositivos no Microsoft Intune inscritos](https://docs.microsoft.com/intune/device-enrollment).  
