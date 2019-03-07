---
title: Configurar a subscrição do Intune
titleSuffix: Configuration Manager
description: Configurar uma subscrição do Intune para controlar o licenciamento para a gestão de dispositivos móveis no local no Configuration Manager
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 1e42b1c1-3d58-481f-8647-5c7ae640c5f5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: aff4fcc67325645387aea1e57354321769a515ca
ms.sourcegitcommit: f3dd8405018fe1043434386be15c16752c1a4a3c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/07/2019
ms.locfileid: "57558070"
---
# <a name="set-up-a-microsoft-intune-subscription-for-on-premises-mdm-in-configuration-manager"></a>Configurar uma subscrição do Microsoft Intune para MDM no local no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O Configuration Manager no local a gestão de dispositivos móveis (MDM) requer uma subscrição do Microsoft Intune para controlar o licenciamento. O serviço do Intune não é utilizado para gerir os dispositivos ou armazenar informações de gestão. Para a MDM no local, toda a gestão de dispositivos é manipulada pela infraestrutura do Configuration Manager.  

Antes de instalar as funções do sistema de sites necessárias para a MDM no local, configure a subscrição do Intune. Esta ação minimiza o tempo necessário para as funções do sistema de sites recentemente instaladas se tornarem funcionais.  

> [!Note]  
> A partir da versão 1810, uma ligação do Intune já não é necessária para novas implementações de MDM no local.<!--3607730, fka 1359124--> Sua organização ainda requer licenças do Intune para utilizar esta funcionalidade. Atualmente não é possível remover a ligação do Intune a partir de implementações de MDM no local existentes. Para obter mais informações, consulte a [mensagem de blogue de suporte do Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).  



##  <a name="sign-up-for-microsoft-intune"></a>Inscreva-se para o Microsoft Intune  

Intune é necessário para tornar funcional a MDM no local. [Inscreva-se](https://docs.microsoft.com/intune/free-trial-sign-up) para uma subscrição de avaliação ou paga. Em seguida, avance para o passo seguinte para adicionar a subscrição para o Configuration Manager.  



##  <a name="add-the-intune-subscription-to-configuration-manager"></a>Adicionar a subscrição do Intune ao Configuration Manager  

Para adicionar a subscrição para o Configuration Manager, siga as mesmas etapas básicas de como faria ao adicionar a subscrição para MDM híbrida com o Intune. Leia as notas abaixo para diferenças específicas e, em seguida, utilize as instruções em [configurar a sua subscrição do Intune](/sccm/mdm/deploy-use/configure-intune-subscription).  

> [!NOTE]
>  Ao adicionar a subscrição do Intune, considere as seguintes notas de:  
> 
> - A coleção especificada no Microsoft Intune Assistente para adicionar subscrição não é utilizada para delegação de direitos de utilizador MDM no local. Só é utilizado para gestão de dispositivos móveis com o Intune. No entanto, tem de especificar uma coleção para que o assistente continuar.  
> 
> - O código do site que especificar no assistente é ignorado para MDM no local. Ele usa o código do site que especificou na inscrição do perfil que concede aos utilizadores permissão para inscrever dispositivos.  
> 
> - Não ative a autenticação multifator. Não é suportada no MDM no local.  



##  <a name="configure-the-intune-subscription-for-on-premises-mdm"></a>Configurar a subscrição do Intune para MDM no local  

1. Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **serviços Cloud**e selecione o **subscrições do Microsoft Intune** nó. Selecione a sua subscrição e, em seguida, escolha **propriedades** na faixa de opções.   

    1. Na secção Gestão de dispositivos no Mobile local na parte inferior a **gerais** página, escolha uma das seguintes opções:

        - Se planear ter apenas a dispositivos geridos no local, selecione a opção para **apenas gerir dispositivos no local**.  

            > [!NOTE]  
            > Quando ativa esta opção, configurar a subscrição do Intune para manter todos os gestão informações no local. Não existem dados de gestão de dispositivos são replicados para a cloud.  

        - Se planear ter dispositivos geridos pelo Intune e Configuration Manager no local, não configure esta opção.  

    Selecione **OK** para fechar as propriedades de subscrição.

2. Se pretender gerir dispositivos Windows 10 Mobile, selecione a sua subscrição na lista, selecione **configurar plataformas** no Friso e, em seguida, selecione **Windows Phone**.  

    1. Selecione a opção para **Windows Phone 8.1 e Windows 10 Mobile**e, em seguida, selecione **OK**.  

3. Se pretender gerir computadores com Windows 10, selecione a sua subscrição na lista, selecione **configurar plataformas** no Friso e, em seguida, selecione **Windows**.  

    1. Selecione a opção para **inscrição do Windows permitem**e, em seguida, selecione **OK**.  

