---
title: Definições de software maligno do Endpoint Protection de compartilhamento de rede
titleSuffix: Configuration Manager
description: Saiba como ativar a transferência de definições de software maligno do Endpoint Protection do Microsoft Updates para o Configuration Manager.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ab7626ae-d4bf-4ca6-ab25-c61f96800a02
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: ee1734178e3225aaf25a8105d83d9c0315866283
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56122190"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-microsoft-updates-for-configuration-manager"></a>Ativar as definições de software maligno do Endpoint Protection transferir a partir do Microsoft Updates para o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


 Quando optar por transferir atualizações de definições do Microsoft Update, os clientes irão verificar o site do Microsoft Update no intervalo definido na secção **Atualizações da definição** da caixa de diálogo da política antimalware.

 Este método pode ser útil quando o cliente não tem conectividade de site do Configuration Manager ou quando pretender que os utilizadores iniciem as atualizações de definições.

> [!IMPORTANT]
>  Os clientes têm de ter acesso ao Microsoft Update na Internet para conseguirem utilizar este método para transferir atualizações de definições.

## <a name="using-the-microsoft-malware-protection-center-to-download-definitions"></a>Utilizar o Centro Microsoft de Proteção Contra Software Maligno para Transferir Definições
 Pode configurar os clientes para transferirem atualizações de definições a partir do Centro Microsoft de Proteção Contra Software Maligno. Esta opção é utilizada pelos clientes do Endpoint Protection para transferir atualizações de definições, se não tiverem sido capazes de transferir as atualizações a partir de outra origem. Este método de atualização pode ser útil se houver um problema com a sua infraestrutura do Configuration Manager que impeça a entrega de atualizações.

> [!IMPORTANT]
>  Os clientes têm de ter acesso ao Microsoft Update na Internet para conseguirem utilizar este método para transferir atualizações de definições.
> 
> 
> [!div class="button"]
> [Passo seguinte >](endpoint-antimalware-policies.md)
> 
> [!div class="button"]
> [Volta >](endpoint-configure-alerts.md)
