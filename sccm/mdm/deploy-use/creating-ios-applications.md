---
title: Criar aplicações iOS
titleSuffix: Configuration Manager
description: Consulte as considerações deve ter em conta quando criar e implementar aplicações em dispositivos iOS.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: ff633013-5313-4cd3-949c-56d45e777280
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 985a8177602bd32da0b6134eeddb564a44749d65
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="create-ios-applications-with-system-center-configuration-manager"></a>Criar aplicações iOS com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Uma aplicação do System Center Configuration Manager tem um ou mais tipos de implementação que compõem os ficheiros de instalação e informações que são necessários para implementar software num dispositivo. Um tipo de implementação tem também as regras que especificam quando e como o software é implementado.  

 Pode criar aplicações utilizando os seguintes métodos:  

-   Crie automaticamente os tipos de aplicação e implementação ao ler os ficheiros de instalação da aplicação.  

-   Criar manualmente a aplicação e adicionar posteriormente os tipos de implementação.  

-   Importe uma aplicação de um ficheiro.  

Consulte [iniciar o Assistente para criar aplicação](../../apps/deploy-use/create-applications.md#start-the-create-application-wizard) para os passos necessários para criar aplicações de Configuration Manager e tipos de implementação. Além disso, mantenha as seguintes considerações em mente quando criar e implementar aplicações em dispositivos iOS.  

## <a name="general-considerations"></a>Considerações gerais  
 O Configuration Manager suporta a implementação dos seguintes tipos de aplicação:  

|Tipo de Dispositivo|Ficheiros suportados|  
|-----------------|---------------------|  
|iOS|*.ipa<br /><br /> No System Center Configuration Manager, não terá de especificar um ficheiro de lista (. plist) de propriedades quando importar uma aplicação iOS.|  

 As seguintes ações de implementação são suportadas:  

|Tipo de Dispositivo|Ações suportadas|  
|-----------------|-----------------------|  
|iOS|**Disponível**, **necessário**. O utilizador tenha de consentir a instalação e desinstalação.

> [!IMPORTANT]  
>  Atualmente, os utilizadores finais não podem instalar aplicações empresariais a partir da aplicação Portal da Empresa do Microsoft Intune para iOS. Isto acontece porque existem restrições que são colocadas nas aplicações que são publicadas na iOS App Store (consulte App Store Review Guidelines, secção 2). Os utilizadores podem instalar aplicações empresariais (incluindo aplicações geridas da App Store e pacotes de aplicações de linha de negócio) ao navegar para o Portal Web do Intune nos respetivos dispositivos (portal.manage.microsoft.com). Para obter mais informações sobre as capacidades de gestão de dispositivos móveis que são ativadas pela aplicação do Portal da empresa do Intune, consulte [inscritos capacidades de gestão de dispositivos no Microsoft Intune](https://technet.microsoft.com/library/dn600287.aspx).  
