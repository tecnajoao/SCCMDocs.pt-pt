---
title: Criar aplicações Android
titleSuffix: Configuration Manager
description: Como criar e implementar aplicações para dispositivos Android no Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: e025c48c-1514-4ab7-836c-e0635aaa993a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ef070186112642d204aade24039da87c0e3a22f0
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56139675"
---
# <a name="create-android-applications-in-configuration-manager"></a>Criar aplicações Android no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Uma aplicação do Configuration Manager tem um ou mais tipos de implementação. Tipos de implementação compreendem os ficheiros de instalação e informações necessários para implementar software num dispositivo. Um tipo de implementação também possui regras que especificam quando e como o software é implementado.  

Ver [criar uma aplicação](/sccm/apps/deploy-use/create-applications#bkmk_create) para obter os passos criar aplicações do Configuration Manager e tipos de implementação. 

Tenha em atenção as seguintes considerações ao criar e implementar aplicações em dispositivos Android:  



## <a name="general-considerations-for-android-apps"></a>Considerações gerais para aplicações Android

O Configuration Manager suporta a implementação de pacotes. apk Android. 

Suporta as seguintes ações de implementação:

|Tipo de Dispositivo|Ações suportadas|
|-|-|
|Android|**Disponível**, **necessário**: O utilizador tenha de consentir a instalação e desinstalação.|
|Android for Work |**Disponível**, **necessário** |



## <a name="approve-and-deploy-android-for-work-apps"></a>Aprovar e implementar o Android for Work

Enquanto administrador do Configuration Manager, também pode aprovar aplicações no [reproduzir para o Web site de trabalho](https://play.google.com/work). Em seguida, implemente essas aplicações para gerido dispositivos Android for Work.

Siga estes passos para aprovar as aplicações na Play Store de trabalho, sincronizá-las para a consola do Configuration Manager e implementá-las em gerenciado dispositivos Android for Work. Para implementar aplicações para perfis de trabalho dos utilizadores, tem de aprovar as aplicações na Play for Work. Em seguida, sincronize as aplicações com a consola do Configuration Manager.

1. Abra um browser e aceda a: https://play.google.com/work.  

2. Inicie sessão com a conta de administrador do Google que vinculado ao seu inquilino do Microsoft Intune.  

3. Procure aplicações que pretende implementar no seu ambiente. Escolher **aprovar** para cada uma delas para disponibilizar a aplicação para Android for Work.  

4. Na consola do Configuration Manager, vá para o **administração** área de trabalho, expanda **serviços Cloud**e selecione o **Android for Work** nó.  

5. Clique em **sincronização** na faixa de opções.  

6. Aguarde até 10 minutos para as aplicações sincronizar. Em seguida, vá para o **biblioteca de Software** área de trabalho, expanda **gestão de aplicações**e selecione o **informações de licença para aplicações de Store** nó.  

7. Selecione uma aplicação sincronizada do Play for Work e, em seguida, clique em **Criar aplicação**.  

8. Conclua o assistente.  

9. Vá para o **biblioteca de Software** área de trabalho, expanda **gestão de aplicações**e selecione o **aplicativos** nó. Selecione uma aplicação Android for Work e implemente como de costume.  

Sincronizar Play para aplicações de trabalho com o Configuration Manager, aprove pela primeira vez pelo menos uma aplicação na Play para o Web site de trabalho.

Como as aplicações implementadas **disponível** apresentar na aplicação do Google Play com distintivo de trabalho em vez do Portal da empresa. Isto permite-lhe implementar aplicações de uma origem fidedigna. A aplicação do Google Play com distintivo de trabalho é uma origem fidedigna. Não tem de permitir que as aplicações de origens não confiáveis.
