---
title: "Simular implementações de aplicações | Microsoft Docs"
description: "Avalie o método de deteção, requisitos e dependências para um tipo de implementação sem instalar a aplicação."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 28b240a4-d358-40ce-8006-c697b1622ece
caps.latest.revision: "6"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: b06539ded21eac71dda7da89dae96fda7a801260
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="simulate-application-deployments-with-system-center-configuration-manager"></a>Simular implementações de aplicações com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode utilizar implementações simuladas para testar a implementação de uma aplicação sem instalar ou desinstalar a aplicação. Uma implementação simulada avalia o método de deteção, requisitos e dependências para um tipo de implementação. -Reporta os resultados no **implementações** o nó do **monitorização** área de trabalho. Utilize o procedimento deste tópico para simular uma implementação de aplicações no System Center Configuration Manager (Configuration Manager).  

> [!NOTE]  
> Não é possível utilizar implementações simuladas em coleções de dispositivos móveis.  
>   
> Não é possível implementar uma aplicação com um objetivo de implementação de **Desinstalar** se estiver ativa uma implementação simulada da mesma aplicação.  

## <a name="configure-a-simulated-application-deployment"></a>Configurar uma implementação da aplicação simulada

1.  Na consola do Configuration Manager, selecione um dos seguintes:  
    -   Uma coleção de utilizadores.  
    -   Uma coleção de dispositivos.  
    -   Uma aplicação do Configuration Manager.  

2.  No **home page** separador o **implementação** grupo, escolha **simular implementação**.  

3.  No Assistente de implementação de aplicação simular, defina os seguintes detalhes para a sua implementação simulada:  

    -   **Aplicação**. Escolha **procurar**e, em seguida, selecione a aplicação que pretende criar uma implementação simulada.  

    -   **Coleção**. Escolha **procurar**e, em seguida, selecione a coleção que pretende utilizar na implementação simulada.  

    -   **Ação**. Na lista pendente, selecione se pretende simular a instalação ou a desinstalação da aplicação selecionada.  

    -   **Implementar automaticamente, com ou sem início de sessão do utilizador**. Se esta opção estiver marcada, os clientes avaliar a implementação simulada se ou não a sessão iniciada.  

4.  Clique em **seguinte**, reveja as informações de **resumo** página e, em seguida, conclua o Assistente para criar a implementação da aplicação simulada.  

5.  As aplicações simuladas são apresentadas no **implementações** o nó do **monitorização** área de trabalho, com um objetivo de **simular**. Para obter mais informações sobre como monitorizar implementações de aplicações, consulte [monitorizar aplicações a partir da consola do System Center Configuration Manager](../../apps/deploy-use/monitor-applications-from-the-console.md).  
