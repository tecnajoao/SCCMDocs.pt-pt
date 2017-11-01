---
title: "Criar itens de configuração subordinados"
titleSuffix: Configuration Manager
description: "Crie configuração itens subordinados no System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 113984fa-6150-41a1-89ed-d2a83b979732
caps.latest.revision: "5"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: c1a59bbedbe157c491800064ba54079c4a980b04
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="how-to-create-child-configuration-items-in-system-center-configuration-manager"></a>Como criar subordinados itens de configuração no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Itens de configuração subordinados no System Center Configuration Manager são cópias de itens de configuração que mantêm uma relação com o item de configuração original em que estes herdam a configuração original do item de configuração principal.  

Ao visualizar as propriedades de um item de configuração subordinado na consola do Configuration Manager, não é possível editar os objetos herdados e as definições com os respetivos critérios de validação. No entanto, pode adicionar e, em seguida, editar os critérios de validação adicionais para o item de configuração subordinado e também pode adicionar novos objetos e definições ao item de configuração subordinado.
O objetivo habitual da criação e edição de um item de configuração subordinado é otimizar o item de configuração original para satisfazer os seus requisitos empresariais.  

> [!NOTE]  
>  Só pode criar itens de configuração subordinados a partir de itens de configuração do tipo **Windows Desktops and Servers (personalizado)**.  

## <a name="to-create-a-child-configuration-item"></a>Para criar um item de configuração subordinado  

1.  Na consola do Configuration Manager, clique em **ativos e compatibilidade** > **as definições de compatibilidade** > **itens de configuração**.  

3.  Na lista **Itens de Configuração** , selecione o item de configuração para o qual pretende criar um item de configuração subordinado e, em seguida, no separador **Início** , no grupo **Item de Configuração** , clique em **Criar Item de Configuração Subordinado**.  

4.  Na página **Geral** página do **Assistente de Criação de Item de Configuração Subordinado**, pode escolher uma revisão específica do item de configuração principal para utilizar para criar o item subordinado. Os outros passos deste assistente são idênticos aos passos que utiliza para criar um item de configuração padrão. Para obter mais informações, consulte [como criar itens de configuração personalizados para computadores de secretária e servidor Windows](../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md).  

5.  Conclua o assistente. O novo item de configuração subordinado é apresentado na lista **Itens de Configuração** .  
