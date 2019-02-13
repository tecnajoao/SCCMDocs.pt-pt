---
title: Ver o inventário de software com o Explorador de recursos
titleSuffix: Configuration Manager
description: Utilize o Explorador de recursos para ver o inventário de software no System Center Configuration Manager.
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4b7aa5f6-5ebd-49be-b7f3-4206caadc187
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 341f1530e0b5bc9486cf062b5f16ede2154439ed
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56129651"
---
# <a name="how-to-use-resource-explorer-to-view-software-inventory-in-system-center-configuration-manager"></a>Como utilizar o Explorador de recursos para ver o inventário de software no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize o Explorador de recursos no System Center Configuration Manager para ver informações sobre o inventário de software que tenha sido recolhida de computadores na sua hierarquia.  

> [!NOTE]  
>  Explorador de recursos não apresentará quaisquer dados de inventário até ser executado um ciclo de inventário de software no cliente.  

 Explorador de recursos fornece as seguintes informações de inventário de software:  

-   **Software**:  

    -   **Ficheiros recolhidos** -ficheiros recolhidos durante o inventário de software.  

    -   **Detalhes do ficheiro** -ficheiros inventariados durante o inventário de software que não estão associados um produto ou fabricante específico.  

    -   **Última análise de Software** -data e hora da última recolha de ficheiros e inventário de software para o computador cliente.  

    -   **Detalhes do produto** -produtos de Software inventariados pelo inventário de software, agrupados por fabricante.  

## <a name="to-run-resource-explorer-from-the-configuration-manager-console"></a>Para executar o Explorador de Recursos a partir da consola do Configuration Manager  

1.  Na consola do Configuration Manager, escolha **ativos e compatibilidade**

2.  Na **ativos e compatibilidade** área de trabalho, escolha **dispositivos** ou abra qualquer coleção que apresente dispositivos.  

3.  Escolha o computador que contém o inventário que pretende ver e, em seguida, no **home page** separador > **dispositivos** de grupo, escolha **iniciar**  >   **Explorador de recursos**.

4.  Pode ser qualquer item no painel direito da janela do Explorador de recursos com o botão direito e escolher **propriedades** para ver as informações de inventário recolhidas num formato mais legível.  
 
