---
title: Criar itens de configuração subordinados
titleSuffix: Configuration Manager
description: Crie subordinado itens de configuração no System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 113984fa-6150-41a1-89ed-d2a83b979732
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 42b6bceacf8d8ecd733e4d13b882fe3b5c0500e7
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56135750"
---
# <a name="how-to-create-child-configuration-items-in-system-center-configuration-manager"></a>Como criar subordinado itens de configuração no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Itens de configuração subordinados no System Center Configuration Manager são cópias dos itens de configuração que mantêm uma relação com o item de configuração original em que eles herdam a configuração original do item de configuração principal.  

Ao visualizar as propriedades de um item de configuração subordinado na consola do Configuration Manager, é possível editar os objetos herdados e as definições com seus critérios de validação. No entanto, pode adicionar e, em seguida, editar os critérios de validação adicionais para o item de configuração subordinado e também pode adicionar novos objetos e definições ao item de configuração subordinado.
O objetivo habitual da criação e edição de um item de configuração subordinado é refinar o item de configuração original para cumprir os requisitos comerciais.  

> [!NOTE]  
>  Só pode criar itens de configuração subordinados a partir de itens de configuração do tipo **Windows Desktops and Servers (personalizado)**.  

## <a name="to-create-a-child-configuration-item"></a>Para criar um item de configuração subordinado  

1.  Na consola do Configuration Manager, clique em **ativos e compatibilidade** > **definições de compatibilidade** > **itens de configuração**.  

3.  Na lista **Itens de Configuração** , selecione o item de configuração para o qual pretende criar um item de configuração subordinado e, em seguida, no separador **Início** , no grupo **Item de Configuração** , clique em **Criar Item de Configuração Subordinado**.  

4.  Na página **Geral** página do **Assistente de Criação de Item de Configuração Subordinado**, pode escolher uma revisão específica do item de configuração principal para utilizar para criar o item subordinado. Os outros passos deste assistente são idênticos aos passos que utiliza para criar um item de configuração padrão. Para obter mais informações, consulte [como criar itens de configuração personalizada para computadores de secretária e servidor de Windows](../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md).  

5.  Conclua o assistente. O novo item de configuração subordinado é apresentado na lista **Itens de Configuração** .  
