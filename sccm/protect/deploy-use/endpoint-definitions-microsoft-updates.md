---
title: Definições de software maligno do Endpoint Protection da partilha de rede
titleSuffix: Configuration Manager
description: Saiba como permitir a transferência de definições de software maligno do Endpoint Protection do Microsoft Updates do Configuration Manager.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ab7626ae-d4bf-4ca6-ab25-c61f96800a02
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 0d8037f2258f97e2782d475598ca62d2f605e5cd
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32346486"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-microsoft-updates-for-configuration-manager"></a>Ativar as definições de software maligno do Endpoint Protection transferir a partir do Microsoft Updates do Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


 Quando optar por transferir atualizações de definições do Microsoft Update, os clientes irão verificar o site do Microsoft Update no intervalo definido na secção **Atualizações da definição** da caixa de diálogo da política antimalware.

 Este método pode ser útil quando o cliente não tem conectividade para o site do Configuration Manager ou quando pretender que os utilizadores iniciem as atualizações de definições.

> [!IMPORTANT]
>  Os clientes têm de ter acesso ao Microsoft Update na Internet para conseguirem utilizar este método para transferir atualizações de definições.

## <a name="using-the-microsoft-malware-protection-center-to-download-definitions"></a>Utilizar o Centro Microsoft de Proteção Contra Software Maligno para Transferir Definições
 Pode configurar os clientes para transferirem atualizações de definições a partir do Centro Microsoft de Proteção Contra Software Maligno. Esta opção é utilizada pelos clientes do Endpoint Protection para transferir atualizações de definições, se de que não tenham conseguido transferir atualizações a partir de outra origem. Este método de atualização pode ser útil se existir um problema com a sua infraestrutura do Configuration Manager que impeça a entrega de atualizações.

> [!IMPORTANT]
>  Os clientes têm de ter acesso ao Microsoft Update na Internet para conseguirem utilizar este método para transferir atualizações de definições.


> [!div class="button"]
[Passo seguinte >](endpoint-antimalware-policies.md)

> [!div class="button"]
[Volta >](endpoint-configure-alerts.md)
