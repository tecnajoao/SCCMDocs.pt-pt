---
title: Criar aplicações Windows Phone
titleSuffix: Configuration Manager
description: Como criar e implementar aplicações para dispositivos Windows Phone no Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 68fe11fa-5fb2-4b81-b0f5-b6f2392fb4ad
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 24ce7609a2e3e3ec9cfd9363ebd58cba3ec4dadd
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56120676"
---
# <a name="create-windows-phone-applications-in-configuration-manager"></a>Criar aplicativos do Windows Phone no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Uma aplicação do Configuration Manager tem um ou mais tipos de implementação. O tipo de implementação inclui os ficheiros de instalação e informações necessárias para implementar software num dispositivo. Um tipo de implementação também possui regras que especificam quando e como o software é implementado.  

Ver [criar uma aplicação](/sccm/apps/deploy-use/create-applications#bkmk_create) para obter os passos criar aplicações do Configuration Manager e tipos de implementação. 

Tenha em atenção as seguintes considerações ao criar e implementar aplicações para dispositivos Windows Phone:  


O Configuration Manager suporta a implementação dos seguintes tipos de ficheiro de aplicação:  

|Tipo de Dispositivo|Tipos de ficheiro suportados|  
|-----------------|---------------------|  
|Windows Phone 8|xap|  
|Windows Phone 8.1|xap, appx, appxbundle|
|Windows 10 Mobile|xap, appx, appxbundle|

Implementar o Windows Phone aplicações como **disponíveis** ou **necessário**. Também utilize implementações para desinstalar aplicações.  
