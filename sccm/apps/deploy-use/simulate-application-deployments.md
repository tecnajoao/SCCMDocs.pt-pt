---
title: "Simular implementações de aplicações | Documentos do Microsoft"
description: "Avalie o método de deteção, requisitos e as dependências de um tipo de implementação sem instalar a aplicação."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 28b240a4-d358-40ce-8006-c697b1622ece
caps.latest.revision: 6
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0ad42d07d260581099046f11255ee312046b2595
ms.openlocfilehash: b06539ded21eac71dda7da89dae96fda7a801260
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="simulate-application-deployments-with-system-center-configuration-manager"></a>Simular implementações de aplicações com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode utilizar implementações simuladas para testar a implementação de uma aplicação sem instalar ou desinstalar a aplicação. Uma implementação simulada avalia o método de deteção, requisitos e as dependências de um tipo de implementação. -Reporta os resultados no **implementações** nó do **monitorização** área de trabalho. Utilize o procedimento neste tópico para simular uma implementação de aplicações no System Center Configuration Manager (Configuration Manager).  

> [!NOTE]  
> Não é possível utilizar implementações simuladas em coleções de dispositivos móveis.  
>   
> Não é possível implementar uma aplicação com um objetivo de implementação de **Desinstalar** se estiver ativa uma implementação simulada da mesma aplicação.  

## <a name="configure-a-simulated-application-deployment"></a>Configurar uma implementação de aplicações simulada

1.  Na consola do Configuration Manager, selecione um dos seguintes procedimentos:  
    -   Uma coleção de utilizadores.  
    -   Uma coleção de dispositivos.  
    -   Uma aplicação do Configuration Manager.  

2.  No **base** separador o **implementação** grupo, selecione **simular implementação**.  

3.  No Assistente de implementação de aplicação simular, defina os seguintes detalhes para a implementação simulada:  

    -   **Aplicação**. Escolher **procurar**e, em seguida, selecione a aplicação que pretende criar uma implementação simulada.  

    -   **Recolha**. Escolher **procurar**e, em seguida, selecione a coleção que pretende utilizar na implementação simulada.  

    -   **Ação**. Na lista pendente, selecione se pretende simular a instalação ou a desinstalação da aplicação selecionada.  

    -   **Implementar automaticamente, com ou sem início de sessão do utilizador**. Se esta opção for selecionada, os clientes avaliar na implementação simulada se ou não a sessão iniciada.  

4.  Clique em **seguinte**, reveja as informações no **resumo** página e, em seguida, conclua o Assistente para criar a implementação da aplicação simulada.  

5.  Aplicações simuladas são apresentadas no **implementações** nó do **monitorização** área de trabalho, com um objetivo de **simular**. Para obter mais informações sobre como monitorizar implementações de aplicações, consulte o artigo [monitorizar aplicações a partir da consola do System Center Configuration Manager](../../apps/deploy-use/monitor-applications-from-the-console.md).  

