---
title: "Ver o inventário de hardware | Documentos do Microsoft | Explorador de recursos"
description: "Utilize o Explorador de recursos para ver o inventário de hardware no System Center Configuration Manager."
ms.custom: na
ms.date: 01/03/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 375912f5-436d-4315-bdbe-d77afee6c9f3
caps.latest.revision: 7
author: andredm7
ms.author: andredm
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 9c5d1e48b76392beaf54b5377c69b648537e86f8
ms.openlocfilehash: e39fa60a5d215fa1b0a98d4463058497e63a4d4f
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="how-to-use-resource-explorer-to-view-hardware-inventory-in-system-center-configuration-manager"></a>Como utilizar o Explorador de Recursos para ver o inventário de hardware no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize o Explorador de recursos no System Center Configuration Manager para ver informações sobre o inventário de hardware que tenha sido recolhida a partir de clientes na sua hierarquia.  

> [!NOTE]  
>  O Explorador de Recursos não apresentará quaisquer dados de inventário até ser executado um ciclo de inventário de hardware no cliente ao qual está a ligar.  

 Explorador de recursos tem as seguintes secções relacionadas com o inventário de hardware:  

-   **Hardware** -contém o mais recente inventário de hardware recolhido do dispositivo cliente especificado.  **Estado de estação de trabalho** tem a hora e data quando o dispositivo última efetuar um inventário de hardware.  

-   **Histórico de hardware** -contém um histórico das inventariados itens que foram alterados desde o último inventário de hardware demorou local. Cada item contém uma **atual** nó e um ou mais *< data\>*  nós. Pode comparar as informações no nó atual para um de nós do histórico para detetar os itens que tenham sido alterados.  

    > [!NOTE]  
    >  Do Configuration Manager mantém o histórico de inventário de hardware para o número de dias que especificou no **eliminar histórico de inventário desatualizados** tarefa de manutenção do site  

> [!NOTE]  
>  Para obter informações sobre como visualizar o inventário de hardware a partir de clientes que executam o Linux e UNIX, veja [Como monitorizar clientes para servidores Linux e UNIX no System Center Configuration Manager](../../../../core/clients/manage/monitor-clients-for-linux-and-unix-servers.md).  

### <a name="how-to-run-resource-explorer-from-the-configuration-manager-console"></a>Como executar o Explorador de Recursos a partir da consola do Configuration Manager  

1.  Na consola do Configuration Manager, escolha **ativos e compatibilidade** > **dispositivos**, ou abra qualquer coleção que apresente dispositivos.  

3.  Selecione o computador que contém o inventário que pretende ver e, em seguida, no **base** separador > **dispositivos** grupo, selecione **iniciar** >  **Explorador de recursos**.   

4.  Com o botão direito num item no painel da direita do **Explorador de recursos** janela e selecione **propriedades** para abrir o *< nome do item\>***propriedades** caixa de diálogo para ver as informações de inventário recolhidos num formato mais legível.  


