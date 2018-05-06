---
title: Criar aplicações Android
titleSuffix: Configuration Manager
description: Consulte as considerações deve ter em conta quando criar e implementar aplicações em dispositivos Android.
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: e025c48c-1514-4ab7-836c-e0635aaa993a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4c09216744b33412bf1840c20aad659c59b0f52b
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="create-android-applications-with-system-center-configuration-manager"></a>Criar aplicações Android com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Uma aplicação do System Center Configuration Manager tem um ou mais tipos de implementação. Tipos de implementação incluem os ficheiros de instalação e informações necessários para implementar software num dispositivo. Um tipo de implementação tem também as regras que especificam quando e como o software é implementado.  

 Pode criar aplicações utilizando os seguintes métodos:  

-   Crie automaticamente os tipos de aplicação e implementação ao ler os ficheiros de instalação da aplicação.  
-   Criar manualmente a aplicação e adicionar posteriormente os tipos de implementação.  
-   Importe uma aplicação de um ficheiro.  

Consulte [iniciar o Assistente para criar aplicação](../../apps/deploy-use/create-applications.md#start-the-create-application-wizard) para os passos necessários para criar aplicações de Configuration Manager e tipos de implementação. Além disso, mantenha as seguintes considerações em mente quando criar e implementar aplicações em dispositivos Android.  

## <a name="general-considerations-for-android-apps"></a>Considerações gerais para aplicações Android

O Configuration Manager suporta a implementação dos seguintes tipos de aplicação para Android:

|Tipo de Dispositivo|Ficheiros suportados|
|-|-|
|Android|. apk|

As seguintes ações de implementação são suportadas:

|Tipo de Dispositivo|Ações suportadas|
|-|-|
|Android|**Disponível**, **necessário** o utilizador tenha de consentir a instalação e desinstalação.|
|Android for Work |**Disponível**, **necessário** |

## <a name="approve-and-deploy-android-for-work-apps"></a>Aprovar e implementar Android para aplicações de trabalho
Como administrador do Configuration Manager, também pode aprovar aplicações no [Play para o Web site de trabalho](https://play.google.com/work)e implementar essas aplicações para Android gerida para dispositivos de trabalho.

Siga estes passos para aprovar aplicações na Play para o arquivo de trabalho, sincronizá-los para a consola do Configuration Manager e implementá-las para o Android gerida para dispositivos de trabalho. Para implementar aplicações para perfis de utilizador de trabalho, terá de aprovar as aplicações na Play para o trabalho e, em seguida, sincronizar as aplicações com a consola do Configuration Manager.

1. Abra um browser e aceda a: https://play.google.com/work.
2. Inicie sessão com a conta de administrador do Google vinculado ao seu inquilino do Intune.
3. Procurar as aplicações que pretende implementar no seu ambiente e escolha **aprovar** para cada um deles para disponibilizar a aplicação para Android para o trabalho.
4. Na consola do Configuration Manager, vá para **administrador** > **descrição geral** > **serviços em nuvem** > **Android para trabalho** e escolha **sincronização**.
5. Aguarde até 10 minutos para as aplicações sincronizar e, em seguida, aceda a **biblioteca de Software** > **descrição geral** > **gestão de aplicações** > **informações de licença para aplicações da loja**.
6. Escolha uma aplicação sincronizada a partir da Play para o trabalho e, em seguida, escolha **Criar aplicação**.
7. Concluir o assistente e escolha **fechar**.
8. Aceda a **biblioteca de Software** > **descrição geral** > **gestão de aplicações** > **aplicações**, escolha um Android para a aplicação de trabalho e implementar como habitualmente.

Para sincronizar Play para aplicações de trabalho com o Configuration Manager, necessitará de aprovar pela primeira vez, pelo menos, uma aplicação na Play para o Web site de trabalho.

As aplicações implementadas como **disponível** apresentar na aplicação do Google Play badged de trabalho em vez do Portal da empresa. Isto permite-lhe implementar aplicações de uma origem fidedigna (a aplicação do Google Play badged de trabalho é uma origem fidedigna) e têm de permitir que as aplicações de fontes não fidedignas.