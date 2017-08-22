---
title: Gerir a compatibilidade em dispositivos geridos com o Intune | Microsoft Docs
description: "Saiba mais sobre as definições de compatibilidade do System Center Configuration Manager ao trabalhar com alguns cenários comuns."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9e83007f-e81c-4b7e-b47e-b01d7b19cfbc
caps.latest.revision: "5"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: b3a63f6c55c317c9c84d4394dfdcb9f1cbbbc90b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="managing-compliance-on-devices-managed-with-intune"></a>Gerir a compatibilidade em dispositivos geridos com o Intune

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Estes cenários dão-lhe uma introdução à utilização de definições de compatibilidade do System Center Configuration Manager ao trabalhar com alguns cenários comuns que poderá encontrar.  

 Se já estiver familiarizado com as definições de compatibilidade, pode encontrar documentação detalhada sobre todas as funcionalidades que utiliza no [itens de configuração para dispositivos geridos com o Intune](#configuration-items-for-devices-managed-with-intune) secção.  

 [Introdução às definições de compatibilidade](../../compliance/get-started/get-started-with-compliance-settings.md) fornece as noções básicas sobre as definições de compatibilidade e [planear e configurar as definições de compatibilidade](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) ajuda-o a implementar os pré-requisitos necessários.  

## <a name="general-information-for-each-scenario"></a>Informações gerais para cada cenário  
 Em cada cenário, irá criar um item de configuração que realiza uma tarefa específica. Para abrir o Assistente de Criação de Item de Configuração, utilize os seguintes passos:  

1.  Na consola do Configuration Manager, clique em **ativos e compatibilidade** > **as definições de compatibilidade** > **itens de configuração**.  

3.  No separador **Início** , no grupo **Criar** , clique em **Criar Item de Configuração**.  

4.  No separador **Geral** do Assistente de Criação de Item de Configuração, conforme apresentado abaixo, especifique um nome e uma descrição para o item de configuração e escolha o tipo de item de configuração adequado para cada cenário deste tópico.  

     ![Mostra a página geral do Assistente de item de configuração de criar.](media/Compliance-Settings-Wizard---1.png)  

## <a name="scenarios-for-windows-81-and-windows-10-devices-managed-with-intune"></a>Cenários para dispositivos Windows 8.1 e Windows 10 geridos com o Intune  

### <a name="scenario-restrict-access-to-the-app-store-on-all-windows-pcs"></a>Cenário: Restringir o acesso à loja de aplicações em todos os PCs Windows  
 Neste cenário, o utilizador é o administrador de TI de uma empresa que lida com informações extremamente confidenciais. Por este motivo, quer restringir as aplicações que os utilizadores podem instalar. Pretende impedir que os utilizadores de todos os PCs Windows 10 transfiram aplicações da Loja Windows e, por isso, executa as ações seguintes.  

1.  Na página **Geral** do Assistente de Criação de Item de Configuração, selecione o tipo de item de configuração **Windows 8.1 e Windows 10** e clique em **Seguinte**.  

2.  No **plataformas suportadas** página, selecione todas as plataformas Windows 10.  

3.  Na página **Definições do Dispositivo** , selecione **Loja**e clique em **Seguinte**.  

4.  Na página **Loja** , selecione **Proibido** como o valor de **Loja de aplicações**.  

5.  Selecione **Remediar definições incompatíveis** para garantir que a alteração é aplicada a todos os PCs.  

6.  Conclua o assistente para criar o item de configuração.  

 Agora, pode utilizar as informações de [tarefas comuns para criar e implementar linhas de base de configuração](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) tópico para o ajudar a implementar a configuração que criou em dispositivos.  

## <a name="scenarios-for-windows-phone-devices-managed-with-intune"></a>Cenários para dispositivos Windows Phone geridos com o Intune  

### <a name="scenario-disable-the-use-of-screen-capture-on-a-windows-phone"></a>Cenário: Desativar a utilização de captura de ecrã num Windows Phone  
 Neste cenário, utiliza os dispositivos Windows Phone 8.1 na sua empresa. Estes dispositivos executam uma aplicação de vendas que contém informações confidenciais. Para proteger a sua empresa, pretende desativar a utilização de captura de ecrã no dispositivo que, potencialmente, poderia ser utilizado para transmitir informações confidenciais fora da sua empresa.  

1.  Na página **Geral** do Assistente de Criação de Item de Configuração, selecione o tipo de item de configuração **Windows Phone** e clique em **Seguinte**.  

2.  No **plataformas suportadas** página, selecione **todos os Windows Phone 8.1** plataformas.  

3.  Na página **Definições do Dispositivo** , selecione **Dispositivo**e clique em **Seguinte**.  

4.  Na página **Dispositivo** , selecione **Desativado** como o valor de **Captura de ecrã**.  

5.  Selecione **Remediar definições incompatíveis** para garantir que a alteração é aplicada a todos os dispositivos Windows Phone 8.1.  

6.  Conclua o assistente para criar o item de configuração.  

 Agora, pode utilizar as informações de [tarefas comuns para criar e implementar linhas de base de configuração com o System Center Configuration Manager](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) tópico para o ajudar a implementar a configuração que criou em dispositivos.  

## <a name="scenarios-for-ios-and-mac-os-x-devices-managed-with-intune"></a>Cenários para dispositivos iOS e Mac OS X geridos com o Intune  

### <a name="scenario-disable-the-camera-on-ios-devices"></a>Cenário: Desativar a câmara em dispositivos iOS  
 Neste cenário, a sua empresa produz esquemas para novos designs de produto. Estes contêm informações confidenciais que não podem ser divulgadas. Como a empresa lança iPhones ou iPads para todos os funcionários, pretende desativar a utilização da câmara nestes dispositivos para impedi-los de serem utilizados para fotografar os esquemas.  

1.  Na página **Geral** do Assistente de Criação de Item de Configuração, selecione o tipo de item de configuração **iOS e Mac OS X** e clique em **Seguinte**.  

2.  No **plataformas suportadas** página, selecione todos os iPhone e todas as plataformas de dispositivos iPad.  

3.  Na página **Definições do Dispositivo** , selecione **Segurança**e clique em **Seguinte**.  

4.  Na página **Segurança** , selecione **Proibido** como o valor de **Câmara**.  

5.  Selecione **Remediar definições incompatíveis** para garantir que a alteração é aplicada a todos os dispositivos iOS.  

6.  Conclua o assistente para criar o item de configuração.  

 Agora, pode utilizar as informações de [tarefas comuns para criar e implementar linhas de base de configuração com o System Center Configuration Manager](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) tópico para o ajudar a implementar a configuração que criou em dispositivos.  

## <a name="scenarios-for-android-and-samsung-knox-standard-devices-managed-with-intune"></a>Cenários para dispositivos Android e Samsung KNOX Standard geridos com o Intune  

### <a name="scenario-require-a-password-on-all-android-5-devices"></a>Cenário: Exigir uma palavra-passe em todos os dispositivos Android 5  
 Neste cenário, irá criar um item de configuração apenas para dispositivos Android 5 que exige que os utilizadores configurem uma palavra-passe com, pelo menos, 6 carateres nos respetivos dispositivos. Além disso, se um utilizador introduzir uma palavra-passe incorreta 5 vezes, o dispositivo será apagado.  

1.  Na página **Geral** do Assistente de Criação de Item de Configuração, selecione o tipo de item de configuração **Android e Samsung KNOX** e clique em **Seguinte**.  

2.  No **plataformas suportadas** página, selecione apenas **Android 5** (para garantir que as definições são aplicadas apenas nessa plataforma).  

3.  Na página **Definições do Dispositivo** , selecione **Palavra-passe**e clique em **Seguinte**.  

4.  Na página **Palavra-passe** , configure as seguintes definições:  

    -   **Exigir definições de palavra-passe em dispositivos** > **Necessário**  

    -   **Comprimento mínimo de palavra-passe (carateres)** > **6**  

    -   **Número de tentativas de início de sessão falhadas antes de o dispositivo ser apagado** > **5**  

5.  Conclua o assistente para criar o item de configuração.  

 Agora, pode utilizar as informações de [tarefas comuns para criar e implementar linhas de base de configuração](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) tópico para o ajudar a implementar a configuração que criou em dispositivos.  

## <a name="configuration-items-for-devices-managed-with-intune"></a>Itens de configuração para dispositivos geridos com o Intune

Os seguintes tipos de item de configuração do System Center Configuration Manager estão disponíveis para dispositivos que não são geridos pelo cliente do Configuration Manager, por exemplo, os dispositivos inscritos com o Microsoft Intune.  

 -   [Como criar itens de configuração para dispositivos Windows 8.1 e Windows 10 geridos com o Intune](create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)  

 -   [Como criar itens de configuração para dispositivos Windows Phone geridos com o Intune](create-configuration-items-for-windows-phone-devices-managed-without-the-client.md)  

 -   [Como criar itens de configuração para dispositivos iOS e Mac OS X geridos com o Intune](create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client.md)  

 -   [Como criar itens de configuração para dispositivos Android e Samsung KNOX Standard geridos com o Intune](create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md)  
