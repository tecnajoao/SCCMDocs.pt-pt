---
title: Remover um ponto de atualização de software
titleSuffix: Configuration Manager
description: Siga este procedimento para remover a função de sistema de sites de ponto de atualização do software num site da consola do Configuration Manager.
author: aczechowski
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 2486375c-d4a2-4cf2-9124-9bee02bbf173
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: c7ab7e28d576bb543fa47f86ad4363e9cffd53e0
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56138012"
---
#  <a name="BKMK_RemoveSUP"></a> Remover a função de sistema de sites do ponto de atualização de software  

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode remover a função de sistema de sites de ponto de atualização do software num site a partir da consola do Configuration Manager. A política de cliente é atualizada para remover o ponto de atualização de software da lista. Ao remover o último ponto de atualização de software no site, a lista de pontos de atualização de software não conterá pontos de atualização de software e as atualizações de software serão essencialmente desativadas no site. Quando tem mais do que um ponto de atualização de software num site primário e remove o ponto de atualização de software que está configurado como origem de sincronização, tem de escolher outro ponto de atualização de software no site para ser a nova origem de sincronização.  

> [!NOTE]  
>  Quando remover a função de site de ponto de atualização de software de um sistema de sites, aguarde pelo menos 15 minutos antes de a reinstalar.  

 Utilize o procedimento seguinte para remover um ponto de atualização de software.  

#### <a name="to-remove-the-software-update-point"></a>Para remover o ponto de atualização de software  

1.  Na consola do **Configuration Manager** , clique em **Administração**.  

2.  Na área de trabalho Administração, expanda **Configuração do Site**e clique em **Servidores e Funções de Sistema de Sites**.  

3.  Selecione o servidor do sistema de sites com o ponto de atualização de software a remover e, em **Funções do Sistema de Sites**, selecione **Ponto de atualização de software**.  

4.  No separador **Função do Site** , no grupo **Função do Site** , clique em **Remover Função**. Confirme que pretende remover o ponto de atualização de software ou selecione uma nova origem de sincronização para os outros pontos de atualização de software no site.  
