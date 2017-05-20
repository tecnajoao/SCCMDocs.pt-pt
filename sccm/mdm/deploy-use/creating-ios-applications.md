---
title: "Criar aplicações iOS | Documentos do Microsoft"
description: "Consulte as considerações tem de efetuar para conta quando criar e implementar aplicações para dispositivos iOS."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ff633013-5313-4cd3-949c-56d45e777280
caps.latest.revision: 10
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 6424fb07802b62820b4dc78a58ab30d3b956abef
ms.openlocfilehash: 349fcf335e7faddbcbd2ffe0ece7e711465f28df
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="create-ios-applications-with-system-center-configuration-manager"></a>Criar aplicações iOS com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Uma aplicação do System Center Configuration Manager tem um ou mais tipos de implementação que compõem os ficheiros de instalação e informações que são necessários para implementar software num dispositivo. Um tipo de implementação também contém as regras que especificam quando e como o software é implementado.  

 Pode criar aplicações utilizando os seguintes métodos:  

-   Crie automaticamente os tipos de aplicação e implementação ao ler os ficheiros de instalação da aplicação.  

-   Criar manualmente a aplicação e adicionar posteriormente os tipos de implementação.  

-   Importe uma aplicação a partir de um ficheiro.  

Consulte o artigo [iniciar o Assistente para criar aplicação](../../apps/deploy-use/create-applications.md#start-the-create-application-wizard) para os passos necessários para criar do Configuration Manager aplicações e tipos de implementação. Além disso, mantenha as seguintes considerações em consideração quando criar e implementar aplicações para dispositivos iOS.  

## <a name="general-considerations"></a>Considerações gerais  
 O Configuration Manager suporta a implementação dos seguintes tipos de aplicação:  

|Tipo de Dispositivo|Ficheiros suportados|  
|-----------------|---------------------|  
|iOS|*.ipa<br /><br /> No System Center Configuration Manager, não tem de especificar um ficheiro de lista (. plist) propriedade ao importar uma aplicação iOS.|  

 As seguintes ações de implementação são suportadas:  

|Tipo de Dispositivo|Ações suportadas|  
|-----------------|-----------------------|  
|iOS|**Disponível**, **necessário**. O utilizador terá de consentir a instalação e desinstalação.

> [!IMPORTANT]  
>  Atualmente, os utilizadores finais não podem instalar aplicações empresariais a partir da aplicação Portal da Empresa do Microsoft Intune para iOS. Isto acontece porque existem restrições são colocadas nas aplicações que são publicadas na iOS App Store (consulte orientações de revisão da loja de aplicações, secção 2). Os utilizadores podem instalar aplicações empresariais (incluindo aplicações geridas da App Store e pacotes de aplicações de linha de negócio) ao navegar para o Portal Web do Intune nos respetivos dispositivos (portal.manage.microsoft.com). Para obter mais informações sobre as capacidades de gestão de dispositivos móveis que são ativadas pela aplicação do Portal da empresa do Intune, consulte o artigo [inscritos funcionalidades de gestão de dispositivos no Microsoft Intune](https://technet.microsoft.com/library/dn600287.aspx).  

