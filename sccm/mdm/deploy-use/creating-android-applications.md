---
title: "Criar aplicações Android | Documentos do Microsoft"
description: "Consulte as considerações tem de efetuar para conta quando criar e implementar aplicações para dispositivos Android."
ms.custom: na
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e025c48c-1514-4ab7-836c-e0635aaa993a
caps.latest.revision: 6
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 27a92dc1c3710ff55f0b145386319dda371533d9
ms.openlocfilehash: d3b20a59a9147e09e58f04f83f97fd72ebfef5a1
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="create-android-applications-with-system-center-configuration-manager"></a>Criar aplicações Android com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Uma aplicação do System Center Configuration Manager tem um ou mais tipos de implementação que compõem os ficheiros de instalação e informações que são necessários para implementar software num dispositivo. Um tipo de implementação também contém as regras que especificam quando e como o software é implementado.  

 Pode criar aplicações utilizando os seguintes métodos:  

-   Crie automaticamente os tipos de aplicação e implementação ao ler os ficheiros de instalação da aplicação.  
-   Criar manualmente a aplicação e adicionar posteriormente os tipos de implementação.  
-   Importe uma aplicação a partir de um ficheiro.  

Consulte o artigo [iniciar o Assistente para criar aplicação](../../apps/deploy-use/create-applications.md#start-the-create-application-wizard) para os passos necessários para criar do Configuration Manager aplicações e tipos de implementação. Além disso, mantenha as seguintes considerações em consideração quando criar e implementar aplicações para dispositivos Android.  

## <a name="general-considerations-for-android-apps"></a>Considerações gerais para aplicações para Android

O Configuration Manager suporta a implementação dos seguintes tipos de aplicação para Android:

|Tipo de Dispositivo|Ficheiros suportados|
|-|-|
|Android|. apk|

As seguintes ações de implementação são suportadas:

|Tipo de Dispositivo|Ações suportadas|
|-|-|
|Android|**Disponível**, **necessário**. O utilizador terá de consentir a instalação e desinstalação.

## <a name="approve-and-deploy-android-for-work-apps"></a>Aprovar e implementar Android para aplicações de trabalho
Como administrador do Configuration Manager, também pode aprovar e implementar aplicações no [reproduzir para o Web site de trabalho](https://play.google.com/work)e implementar estas aplicações para Android gerido para dispositivos de trabalho.

Siga estes passos para aprovar aplicações na Play para o arquivo de trabalho, sincronizá-los para a consola do Configuration Manager e implementá-las Android gerido para dispositivos de trabalho. Para implementar aplicações para perfis de utilizador de trabalho, terá de aprovar aplicações da Play para o trabalho e, em seguida, sincronizar as aplicações com a consola do Configuration Manager.

1. Abra um browser e aceda a: https://play.google.com/work.
2. Inicie sessão utilizando a conta de administrador de Google vinculada ao seu inquilino do Intune.
3. Procurar aplicações que pretende implementar no seu ambiente e escolha **aprovar** para cada um deles para disponibilizar a aplicação para Android para trabalhar.
4. Na consola do Configuration Manager, aceda a **administrador** > **descrição geral** > **serviços em nuvem** > **Android para trabalhar** e escolha **sincronização**.
5. Aguarde até 10 minutos para as aplicações sincronizar e, em seguida, aceda a **biblioteca de Software** > **descrição geral** > **gestão de aplicações** > **informações de licença de aplicações da loja**.
6. Selecione uma aplicação sincronizada a partir da Play para o trabalho e, em seguida, selecione **Criar aplicação**.
7. Concluir o assistente e escolher **fechar**.
8. Aceda a **biblioteca de Software** > **descrição geral** > **gestão de aplicações** > **aplicações**, escolha um Android para a aplicação de trabalho e implementar como habitualmente.

Para sincronizar Play para aplicações de trabalho com o Configuration Manager, terá de aprovar pela primeira vez, pelo menos, uma aplicação no Play para o Web site de trabalho.

