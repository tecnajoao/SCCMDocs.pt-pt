---
title: Gateway de gestão de cloud de monitor
titleSuffix: Configuration Manager
description: Monitorize os clientes e tráfego de rede através do gateway de gestão da cloud (CMG).
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 15f72f80-9850-40ce-9c3a-443ba04b6a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 820d8a4241a6d250ce652f95ea47abe015600d4a
ms.sourcegitcommit: 316899b08f2ef372993909e08e069f7edfed1d33
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/07/2018
ms.locfileid: "44111132"
---
# <a name="monitor-cloud-management-gateway-in-configuration-manager"></a>Monitorizar gateway de gestão da nuvem no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Depois do gateway de gestão da nuvem está em execução e os clientes estão a ligar através do mesmo, pode monitorizar os clientes e tráfego de rede para se certificar de que sabe como o serviço está sendo executada.



## <a name="monitor-clients"></a>Monitorar clientes

Clientes ligados através do gateway de gestão de cloud aparecem na consola do Configuration Manager da mesma forma no local os clientes fazem. Para obter mais informações, consulte [como monitorizar clientes](/sccm/core/clients/manage/monitor-clients).



## <a name="monitor-traffic-in-the-console"></a>Tráfego de monitor na consola do

Monitorizar o tráfego no gateway de gestão na cloud utilizando a consola do Configuration Manager:

1. Aceda a **administração > Serviços Cloud > Gateway de gestão da Cloud**.

2. Selecione o gateway de gestão na cloud, no painel de lista.

3. Ver as informações de tráfego no painel de detalhes para o ponto de ligação do gateway de gestão na cloud e as funções do sistema de sites liga-se ao.



## <a name="set-up-outbound-traffic-alerts"></a>Configurar alertas de tráfego de saída

Alertas de tráfego de saída ajudá-lo a saber quando o tráfego de rede se aproxima de um nível de limiar de 14 dias. Ao criar o gateway de gestão na cloud, pode configurar alertas de tráfego. Se saltou a essa parte, pode ainda configurar os alertas depois do serviço está em execução. Ajuste as definições de alerta em qualquer altura.

1. Aceda a **administração > Serviços Cloud > Gateway de gestão da Cloud**.

2. O gateway de gestão de nuvem no painel de lista com o botão direito e escolher **propriedades**.

3. Clique nas **alertas** separador. Ative o limiar e alertas. Especifique o limiar de 14 dias de dados em gigabytes (GB). Especifique também a percentagem de limiar para aumentar os diferentes níveis de alerta.

4. Clique em **OK** quando terminar.



## <a name="monitor-logs"></a>Registos de monitor

O gateway de gestão da nuvem gera entradas num número de ficheiros de registo. Para obter mais informações, consulte [registos do Configuration Manager](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway).
