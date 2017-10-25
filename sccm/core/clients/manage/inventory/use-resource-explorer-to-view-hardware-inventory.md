---
title: "Ver o inventário de hardware | Microsoft Docs | Explorador de recursos"
description: "Utilize o Explorador de recursos para ver o inventário de hardware no System Center Configuration Manager."
ms.custom: na
ms.date: 01/03/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 375912f5-436d-4315-bdbe-d77afee6c9f3
caps.latest.revision: "7"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: e39fa60a5d215fa1b0a98d4463058497e63a4d4f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-use-resource-explorer-to-view-hardware-inventory-in-system-center-configuration-manager"></a>Como utilizar o Explorador de Recursos para ver o inventário de hardware no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize o Explorador de recursos no System Center Configuration Manager para ver informações sobre o inventário de hardware que tenha sido recolhida de clientes na sua hierarquia.  

> [!NOTE]  
>  O Explorador de Recursos não apresentará quaisquer dados de inventário até ser executado um ciclo de inventário de hardware no cliente ao qual está a ligar.  

 Explorador de recursos tem as seguintes secções relacionadas com o inventário de hardware:  

-   **Hardware** -contém o inventário de hardware mais recente recolhido do dispositivo cliente especificado.  **Estado da estação de trabalho** tem a hora e data quando o dispositivo efetuado pela última vez inventário de hardware.  

-   **Histórico de hardware** -contém um histórico dos itens inventariados que foram alterados desde o último inventário de hardware demorou local. Cada item contém um **atual** nós e um ou mais *< data\>*  nós. Pode comparar as informações no nó atual para um de nós do histórico para detetar os itens que foram alterados.  

    > [!NOTE]  
    >  O Configuration Manager mantém o histórico de inventário de hardware para o número de dias que especificar no **eliminar histórico de inventário desatualizado** tarefa de manutenção do site  

> [!NOTE]  
>  Para obter informações sobre como visualizar o inventário de hardware a partir de clientes que executam o Linux e UNIX, veja [Como monitorizar clientes para servidores Linux e UNIX no System Center Configuration Manager](../../../../core/clients/manage/monitor-clients-for-linux-and-unix-servers.md).  

### <a name="how-to-run-resource-explorer-from-the-configuration-manager-console"></a>Como executar o Explorador de Recursos a partir da consola do Configuration Manager  

1.  Na consola do Configuration Manager, escolha **ativos e compatibilidade** > **dispositivos**, ou abra qualquer coleção que apresente dispositivos.  

3.  Escolha o computador que contém o inventário que pretende visualizar e, em seguida, no **home page** separador > **dispositivos** grupo, escolha **iniciar** >  **Explorador de recursos**.   

4.  Clique com o botão direito qualquer item no painel da direita do **Explorador de recursos** janela e escolha **propriedades** para abrir o *< nome do item\>***propriedades** caixa de diálogo para ver as informações de inventário recolhidas num formato mais legível.  

