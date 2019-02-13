---
title: Configurar o inventário de hardware
titleSuffix: Configuration Manager
description: Configure o inventário de hardware para todos os clientes ou para uma coleção no System Center Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 0e45290e-f8f7-4335-801e-570225d12c2b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: b96bb7afb370dba2498ed2da886dab254d5eee90
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56131392"
---
# <a name="how-to-configure-hardware-inventory-in-system-center-configuration-manager"></a>Como configurar inventário de hardware no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este procedimento configura as predefinições de cliente para inventário de hardware e aplica-se a todos os clientes na sua hierarquia. Se pretender que estas definições se apliquem apenas a determinados clientes, crie uma definição personalizada do cliente do dispositivo e atribua-a a uma coleção que contenha os dispositivos que pretende que utilizem inventário de hardware. Ver [como configurar as definições de cliente no System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

> [!NOTE]  
>  Se um dispositivo cliente receber definições de inventário de hardware de vários conjuntos de definições de cliente, as classes de inventário de hardware de cada conjunto de definições serão intercaladas quando o cliente comunicar o inventário de hardware. Além disso, não a verificação de uma classe numa definição com uma prioridade mais alta de cliente personalizada não desativar o cliente de inventário dessa classe. 

Para desativar uma classe de inventário de hardware específico em que a maioria dos sistemas, exceto alguns, a classe tem de ser marcada nas predefinições do cliente. Em seguida, crie uma definição para ativar a classe de cliente personalizada e implementá-la para os sistemas de destino.


### <a name="to-configure-hardware-inventory"></a>Para configurar o inventário de hardware  

1.  Na consola do Configuration Manager, escolha **Administration** > **definições de cliente** > **predefinições de cliente**.  

4.  Sobre o **home page** separador a **propriedades** de grupo, escolha **propriedades**.  

5.  Na **predefinições** caixa de diálogo caixa, escolha **inventário de Hardware**.  

6.  Na lista **Definições do Dispositivo** , configure as seguintes definições:  

    -   **Ativar inventário de hardware nos clientes** - selecione **Sim**.  

    -   **Agenda de inventário de hardware** -clique em **agenda** para especificar o intervalo a que os clientes recolhem o inventário de hardware.  

7.  Configurar outro [definições de cliente de inventário de hardware](../../../../core/clients/deploy/about-client-settings.md#hardware-inventory) que necessita.  

Os dispositivos cliente serão configurados com estas definições da próxima vez que transferirem a política de cliente. Para iniciar a obtenção da política para um único cliente, consulte [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  
