---
title: "Configurar a subscrição do Intune | Documentos do Microsoft"
description: "Configure uma subscrição do Intune para controlar de licenciamento para gestão de dispositivos móveis no local no System Center Configuration Manager."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 1e42b1c1-3d58-481f-8647-5c7ae640c5f5
caps.latest.revision: 8
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 6424fb07802b62820b4dc78a58ab30d3b956abef
ms.openlocfilehash: 5a81ec06e16992ae1c41b0fc98ebcd07386c5381
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="set-up-a-microsoft-intune-subscription-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Configurar uma subscrição do Microsoft Intune para gestão de dispositivos móveis no local no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager no\-local gestão de dispositivos móveis requer uma subscrição do Microsoft Intune para controlar de licenciamento. O serviço Intune não é utilizado para gerir os dispositivos ou para armazenar informações de gestão. No\-local gestão de dispositivos móveis, toda a gestão de dispositivos é processada pela infraestrutura do Configuration Manager.  

> [!NOTE]  
> A partir na versão 1610, Configuration Manager suporta a utilização de ambos os Microsoft Intune e no local da infraestrutura do Configuration Manager para gerir dispositivos móveis ao mesmo tempo.   

> [!TIP]  
>  Recomendamos que configure a subscrição do Intune no\-local gestão de dispositivos móveis antes de instalar as funções do sistema de sites necessários para minimizar o tempo necessário para as funções do sistema de site recentemente instalado para se tornarem funcional.  

##  <a name="sign-up-for-microsoft-intune"></a>Inscrever-se para o Microsoft Intune  
 Intune é necessário para efetuar\-local funcionais de gestão de dispositivos móveis. Basta [inscrever-se](http://www.microsoft.com/en-us/server-cloud/products/microsoft-intune/) para uma subscrição paga ou de avaliação e vá para o passo seguinte para adicionar a subscrição para o Configuration Manager.  

##  <a name="add-the-intune-subscription-to-configuration-manager"></a>Adicionar a subscrição do Intune ao Configuration Manager  
 Para adicionar a subscrição para o Configuration Manager, siga os mesmos passos básicos como o faria ao adicionar a subscrição de gestão de dispositivos móveis com o Intune. Leia as notas abaixo para diferenças específicas e, em seguida, utilize as instruções em [configurar a sua subscrição do Intune](../deploy-use/configure-intune-subscription.md).  

> [!NOTE]  
>  Ao adicionar a subscrição do Intune, tenha em atenção o seguinte:  
>   
>  -   A coleção especificada no adicionar Microsoft Intune Assistente de subscrição não é utilizada para no\-local delegação de direita de utilizador de gestão de dispositivos móveis. Só é utilizado para gestão de dispositivos móveis com o Intune. No entanto, tem de especificar uma coleção para que o assistente continue.  
> -   A definição do código de site especificada no Assistente de é ignorada no\-local gestão de dispositivos móveis. O código do site utilizado é aquele que especificar no perfil de inscrição que concede aos utilizadores permissão para inscreverem dispositivos.  
> -   Não ative a autenticação multifator. Não é suportada no\-local gestão de dispositivos móveis.  

##  <a name="configure-the-intune-subscription-for-on-premises-mobile-device-management"></a>Configurar a subscrição do Intune para gestão de dispositivos móveis no local  

1.  Na consola do Configuration Manager, faça duplo clique a **subscrição do Windows Intune**e clique em **propriedades**.  

2.  Na caixa de gestão de dispositivos no móveis no local, escolha um dos seguintes procedimentos:

  - Se planear ter apenas os dispositivos geridos no local, clique na caixa de verificação junto a **apenas gerir dispositivos no local**e clique em **OK**.  

      > [!NOTE]  
      >  Ao clicar nesta caixa de verificação, é configurar a subscrição do Intune para manter todos os gestão informações no local e não são replicados dados para a nuvem.  

    - Se planear ter dispositivos geridos pelo Intune e Configuration Manager no local, deixe a caixa desmarcada.

3.  Se pretender gerir dispositivos Windows 10 Mobile, clique com o botão direito do rato em **Subscrição do Windows Intune**, clique em **Configurar Plataformas**e, em seguida, clique em  **Windows Phone**.  

4.  Clique na caixa de verificação junto a **Windows Phone 8.1 e Windows 10 Mobile**e, em seguida, clique em **OK**.  

5.  Se pretender gerir computadores de secretária Windows 10, clique com o botão direito do rato em **Subscrição do Windows Intune**, clique em **Configurar Plataformas**e, em seguida, clique em **Ativar Inscrição Windows**.  

6.  Clique na caixa de verificação junto a **Ativar inscrição Windows**e, em seguida, clique em **OK**.  

