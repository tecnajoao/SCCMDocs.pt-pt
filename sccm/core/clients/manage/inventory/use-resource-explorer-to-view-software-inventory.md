---
title: "Ver o inventário de software | Microsoft Docs | Explorador de recursos"
description: "Utilize o Explorador de recursos para ver o inventário de software no System Center Configuration Manager."
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4b7aa5f6-5ebd-49be-b7f3-4206caadc187
caps.latest.revision: "5"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: b76bcf65c61b0a2690a468d375ac95b1334d5298
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-use-resource-explorer-to-view-software-inventory-in-system-center-configuration-manager"></a>Como utilizar o Explorador de recursos para ver o inventário de software no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize o Explorador de recursos no System Center Configuration Manager para ver informações sobre o inventário de software que tenha sido recolhida de computadores na sua hierarquia.  

> [!NOTE]  
>  Explorador de recursos não apresentará quaisquer dados de inventário até ser executado um ciclo de inventário de software no cliente.  

 Explorador de recursos fornece as seguintes informações de inventário de software:  

-   **Software**:  

    -   **Recolher ficheiros** -os ficheiros recolhidos durante o inventário de software.  

    -   **Detalhes de ficheiros** -os ficheiros inventariados durante o inventário de software que não estão associados um produto ou fabricante específico.  

    -   **Última análise de Software** -data e hora da última recolha de ficheiros e inventário de software para o computador cliente.  

    -   **Detalhes do produto** -produtos de Software que foram inventariados pelo inventário de software, agrupados por fabricante.  

## <a name="to-run-resource-explorer-from-the-configuration-manager-console"></a>Para executar o Explorador de Recursos a partir da consola do Configuration Manager  

1.  Na consola do Configuration Manager, escolha **ativos e compatibilidade**

2.  No **ativos e compatibilidade** área de trabalho, escolha **dispositivos** ou abra qualquer coleção que apresente dispositivos.  

3.  Escolha o computador que contém o inventário que pretende visualizar e, em seguida, no **home page** separador > **dispositivos** grupo, escolha **iniciar** > **Explorador de recursos**.

4.  Pode ser qualquer item no painel direito da janela do Explorador de recursos com o botão direito e selecione **propriedades** para ver as informações de inventário recolhidas num formato mais legível.  
 
