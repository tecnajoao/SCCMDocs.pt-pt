---
title: "Configurar o inventário de hardware | Microsoft Docs"
description: "Configure o inventário de hardware para todos os clientes ou para uma coleção no System Center Configuration Manager."
ms.custom: na
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0e45290e-f8f7-4335-801e-570225d12c2b
caps.latest.revision: "5"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 0baadb95ec8dbb945f1a611ebb95a03cec3199bd
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-configure-hardware-inventory-in-system-center-configuration-manager"></a>Como configurar inventário de hardware no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este procedimento configura as predefinições de cliente para inventário de hardware e aplica-se a todos os clientes na sua hierarquia. Se pretender que estas definições se apliquem apenas a determinados clientes, crie uma definição personalizada do cliente do dispositivo e atribua-a a uma coleção que contenha os dispositivos que pretende que utilizem inventário de hardware. Consulte [como configurar as definições de cliente no System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

> [!NOTE]  
>  Se um dispositivo cliente receber definições de inventário de hardware de vários conjuntos de definições de cliente, as classes de inventário de hardware de cada conjunto de definições serão intercaladas quando o cliente comunicar o inventário de hardware.  

### <a name="to-configure-hardware-inventory"></a>Para configurar o inventário de hardware  

1.  Na consola do Configuration Manager, escolha **administração** > **as definições de cliente** > **predefinições de cliente**.  

4.  No **home page** separador o **propriedades** grupo, escolha **propriedades**.  

5.  No **predefinições** diálogo caixa, escolha **inventário de Hardware**.  

6.  Na lista **Definições do Dispositivo** , configure as seguintes definições:  

    -   **Ativar inventário de hardware nos clientes** - selecione **verdadeiro**.  

    -   **Agenda de inventário de hardware** -clique em **agenda** para especificar o intervalo no qual os clientes recolhem o inventário de hardware.  

7.  Configurar outros [definições de cliente de inventário de hardware](../../../../core/clients/deploy/about-client-settings.md#hardware-inventory) que precisa.  

Os dispositivos cliente serão configurados com estas definições da próxima vez que transferirem a política de cliente. Para iniciar a obtenção da política para um único cliente, veja [Como gerir clientes no System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  
