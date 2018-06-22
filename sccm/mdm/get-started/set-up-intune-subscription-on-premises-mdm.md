---
title: 'Configurar a subscrição do Intune '
titleSuffix: Configuration Manager
description: Configure uma subscrição do Intune para controlar o licenciamento para a gestão de dispositivos móveis no local no System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 1e42b1c1-3d58-481f-8647-5c7ae640c5f5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: aa931c848bc3a25df452f8034530b6c740659e12
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32347421"
---
# <a name="set-up-a-microsoft-intune-subscription-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Configurar uma subscrição do Microsoft Intune para gestão de dispositivos móveis no local no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager no\-local gestão de dispositivos móveis requer uma subscrição do Microsoft Intune para controlar o licenciamento. O serviço do Intune não é utilizado para gerir os dispositivos ou armazenar informações de gestão. Nos\-local gestão de dispositivos móveis, toda a gestão de dispositivos é processado pela infraestrutura do Configuration Manager.  

> [!NOTE]  
> A partir da versão 1610, Configuration Manager suporta a utilização de ambos os Microsoft Intune e no local infraestrutura do Configuration Manager para gerir dispositivos móveis ao mesmo tempo.   

> [!TIP]  
>  Recomendamos que configure a subscrição do Intune no\-no local a gestão de dispositivos móveis antes de instalar as funções do sistema de sites necessárias para minimizar o tempo necessário para as funções do sistema de sites recentemente instaladas se tornarem funcionais.  

##  <a name="sign-up-for-microsoft-intune"></a>Inscrever-se no Microsoft Intune  
 Intune é necessário efetuar no\-no local a gestão de dispositivos móveis funcional. Basta [inscrever](http://www.microsoft.com/en-us/server-cloud/products/microsoft-intune/) para uma subscrição de avaliação ou paga e avançar para o passo seguinte para adicionar a subscrição para o Configuration Manager.  

##  <a name="add-the-intune-subscription-to-configuration-manager"></a>Adicionar a subscrição do Intune ao Configuration Manager  
 Para adicionar a subscrição para o Configuration Manager, siga os mesmos passos básicos, tal como faria para adicionar a subscrição para gestão de dispositivos móveis com o Intune. Leia as notas abaixo para conhecer as diferenças específicas e, em seguida, utilize as instruções no [configurar a sua subscrição do Intune](../deploy-use/configure-intune-subscription.md).  

> [!NOTE]  
>  Ao adicionar a subscrição do Intune, tenha em atenção o seguinte:  
>   
>  -   A coleção especificada no Microsoft Intune Assistente para adicionar subscrição não é utilizada para\-no local a delegação de direitos de utilizador de gestão de dispositivos móveis. Só é utilizada para gestão de dispositivos móveis com o Intune. No entanto, tem de especificar uma coleção para que o assistente continue.  
> -   A definição de código do site especificada no assistente é ignorada no\-no local a gestão de dispositivos móveis. O código do site utilizado é aquele que especificar no perfil de inscrição que concede aos utilizadores permissão para inscreverem dispositivos.  
> -   Não ative a autenticação multifator. Não é suportada no\-no local a gestão de dispositivos móveis.  

##  <a name="configure-the-intune-subscription-for-on-premises-mobile-device-management"></a>Configurar a subscrição do Intune para gestão de dispositivos móveis no local  

1.  Na consola do Configuration Manager, clique com botão direito do **subscrição do Microsoft Intune**e clique em **propriedades**.  

2.  Na caixa de gestão de dispositivos no móveis no local, escolha um dos seguintes:

  - Se planear ter apenas a dispositivos geridos no local, clique na caixa de verificação junto a **apenas gerir dispositivos no local**e clique em **OK**.  

      > [!NOTE]  
      >  Ao clicar nesta caixa de verificação, configurar a subscrição do Intune para manter todos os gestão informações no local e não replicar dados para a nuvem.  

    - Se planear ter dispositivos geridos pelo Intune e Configuration Manager no local, deixe a caixa desmarcada.

3.  Se pretender gerir dispositivos Windows 10 Mobile, clique com o botão direito do rato em **Subscrição do Windows Intune**, clique em **Configurar Plataformas**e, em seguida, clique em  **Windows Phone**.  

4.  Clique na caixa de verificação junto a **Windows Phone 8.1 e Windows 10 Mobile**e, em seguida, clique em **OK**.  

5.  Se pretender gerir computadores de secretária Windows 10, clique com o botão direito do rato em **Subscrição do Windows Intune**, clique em **Configurar Plataformas**e, em seguida, clique em **Ativar Inscrição Windows**.  

6.  Clique na caixa de verificação junto a **Ativar inscrição Windows**e, em seguida, clique em **OK**.  
