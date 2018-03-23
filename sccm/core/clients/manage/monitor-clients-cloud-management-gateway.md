---
title: 'Gateway de gestão de nuvem do monitor '
titleSuffix: Configuration Manager
description: ''
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology:
- configmgr-client
ms.assetid: 15f72f80-9850-40ce-9c3a-443ba04b6a03
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: d88749b09dd5e88f29240cc0db2f2ace7a2f06f4
ms.sourcegitcommit: d03e4dee92a31dd214c528e895379f6013b7de82
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/23/2018
---
# <a name="monitor-cloud-management-gateway-in-configuration-manager"></a>Monitorizar o gateway de gestão de nuvem no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

A partir da versão 1610, depois do serviço de gateway de gestão de nuvem está em execução e os clientes se ligam através dele, pode monitorizar os clientes e o tráfego de rede para se certificar de que sabe como o serviço está a efetuar.

## <a name="monitor-clients"></a>Clientes de monitor

Os clientes ligados através do serviço de gateway de gestão de nuvem aparecem na consola do Configuration Manager da mesma forma no local fazem de clientes. Para obter mais informações, consulte [como monitorizar clientes](monitor-clients.md).

## <a name="monitor-traffic-in-the-console"></a>Monitorizar o tráfego na consola do

Pode monitorizar o tráfego no gateway de gestão de nuvem utilizando a consola do Configuration Manager:

1. Aceda a **administração > Serviços em nuvem > Gestão Gateway de nuvem**.

2. Selecione o serviço de gateway de gestão de nuvem no painel de lista.

3. Ver as informações de tráfego no painel de detalhes para a função de ligação de gateway de gestão de nuvem e as funções do sistema de sites liga-se ao.

## <a name="set-up-outbound-traffic-alerts"></a>Configurar alertas de tráfego de saída

Alertas de tráfego de saída irão ajudá-lo informado quando o tráfego se aproxima um nível de limiar (2 semanas) 14 dias. É-lhe dada a opção de configuração de alertas de tráfego, quando criar o serviço de gateway de gestão de nuvem. Se saltou a parte, pode ainda configurar os alertas após o serviço está em execução. E também pode ajustar as definições de alerta em qualquer altura.

1. Aceda a **administração > Serviços em nuvem > Gestão Gateway de nuvem**.

2. O serviço de gateway de gestão de nuvem no painel de lista com o botão direito e selecione **propriedades**.

3. Clique no separador de alertas e optar por ativar (ou desative) o limiar e alertas. Em seguida, especifique o limiar de 14 dias (em GB) e a percentagem de limiar para gerar os diferentes níveis de alerta.

4. Clique em **OK** quando tiver terminado.

## <a name="monitor-logs"></a>Registos de monitor

O serviço de gateway de gestão de nuvem gera entradas num número de ficheiros de registo. Para obter mais informações, consulte [registos do Configuration Manager](/sccm/core/plan-design/hierarchy/log-files).
