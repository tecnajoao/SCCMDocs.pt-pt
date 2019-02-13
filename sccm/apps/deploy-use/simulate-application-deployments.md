---
title: Simular implementações de aplicações
titleSuffix: Configuration Manager
description: Avalie o método de deteção, requisitos e dependências para um tipo de implementação sem instalar a aplicação.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 28b240a4-d358-40ce-8006-c697b1622ece
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 89283226a067ff3e0bd232c33ab1cfe5d9240fb5
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56130025"
---
# <a name="simulate-application-deployments-with-system-center-configuration-manager"></a>Simular implementações de aplicações com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode utilizar implementações simuladas para testar a implementação de uma aplicação sem instalar ou desinstalar a aplicação. Uma implementação simulada avalia o método de deteção, requisitos e dependências para um tipo de implementação. Reporta os resultados na **implementações** nó da **monitorização** área de trabalho. Utilize o procedimento neste tópico para simular uma implementação de aplicações no System Center Configuration Manager (Gestor de configuração).  

> [!NOTE]  
> Não é possível utilizar implementações simuladas em coleções de dispositivos móveis.  
>   
> Não é possível implementar uma aplicação com um objetivo de implementação de **Desinstalar** se estiver ativa uma implementação simulada da mesma aplicação.  

## <a name="configure-a-simulated-application-deployment"></a>Configurar uma implementação simulada de aplicativos

1.  Na consola do Configuration Manager, selecione um dos seguintes:  
    -   Uma coleção de utilizadores.  
    -   Uma coleção de dispositivos.  
    -   Uma aplicação do Configuration Manager.  

2.  Sobre o **home page** separador a **implementação** de grupo, escolha **simular implementação**.  

3.  No Assistente de implementação de aplicação simular, defina os seguintes detalhes para a sua implementação simulado:  

    -   **Aplicação**. Escolher **procurar**e, em seguida, selecione a aplicação que pretende criar uma implementação simulada para.  

    -   **Coleção**. Escolher **procurar**e, em seguida, selecione a coleção que pretende utilizar na implementação simulada.  

    -   **Ação**. Na lista pendente, selecione se pretende simular a instalação ou a desinstalação da aplicação selecionada.  

    -   **Implementar automaticamente, com ou sem início de sessão do utilizador**. Se esta opção estiver marcada, os clientes avaliam na implementação simulada se ou não a sessão iniciada.  

4.  Clique em **próxima**, reveja as informações sobre o **resumo** página e, em seguida, concluir o Assistente para criar a implementação da aplicação simulada.  

5.  Aplicações simuladas são apresentadas na **implementações** nó da **monitorização** área de trabalho, com um objetivo de **simular**. Para obter mais informações sobre como monitorizar implementações de aplicações, consulte [monitorizar aplicações a partir da consola do System Center Configuration Manager](../../apps/deploy-use/monitor-applications-from-the-console.md).  
