---
title: "Definições de software maligno do Endpoint Protection a partir de partilha de rede | Documentos do Microsoft"
description: "Saiba como ativar a transferência de definições de software maligno do Endpoint Protection do Microsoft Updates para o Configuration Manager."
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: ab7626ae-d4bf-4ca6-ab25-c61f96800a02
caps.latest.revision: 21
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 017bd5b899b364fc832c721d63cc7dbad0a11671
ms.openlocfilehash: 58c468fc3d4427cc1f2a8f197ab784a767151203
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---

# <a name="enable-endpoint-protection-malware-definitions-to-download-from-microsoft-updates-for-configuration-manager"></a>Ativar as definições de software maligno do Endpoint Protection transferir a partir do Microsoft Updates para o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


 Quando optar por transferir atualizações de definições do Microsoft Update, os clientes irão verificar o site do Microsoft Update no intervalo definido na secção **Atualizações da definição** da caixa de diálogo da política antimalware.

 Este método pode ser útil quando o cliente não tem conectividade de site do Configuration Manager ou quando pretende que os utilizadores ser capazes de iniciar a atualizações de definições.

> [!IMPORTANT]
>  Os clientes têm de ter acesso ao Microsoft Update na Internet para conseguirem utilizar este método para transferir atualizações de definições.

## <a name="using-the-microsoft-malware-protection-center-to-download-definitions"></a>Utilizar o Centro Microsoft de Proteção Contra Software Maligno para Transferir Definições
 Pode configurar os clientes para transferirem atualizações de definições a partir do Centro Microsoft de Proteção Contra Software Maligno. Esta opção é utilizada pelos clientes do Endpoint Protection para transferir atualizações de definições, se não tiverem sido capazes de transferir atualizações a partir de outra origem. Este método de atualização pode ser útil se existir um problema com a infraestrutura do Configuration Manager que impede a entrega de atualizações.

> [!IMPORTANT]
>  Os clientes têm de ter acesso ao Microsoft Update na Internet para conseguirem utilizar este método para transferir atualizações de definições.


> [!div class="button"]
[Passo seguinte >](endpoint-antimalware-policies.md)

> [!div class="button"]
[Segurança >](endpoint-configure-alerts.md)

