---
title: Gateway de gestão de nuvem do monitor
titleSuffix: Configuration Manager
description: Monitorizar os clientes e o tráfego de rede através do gateway de gestão de nuvem (CMG).
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology:
- configmgr-client
ms.assetid: 15f72f80-9850-40ce-9c3a-443ba04b6a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 18a98ae924b985b08aed911797b07ef0a1974420
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/23/2018
---
# <a name="monitor-cloud-management-gateway-in-configuration-manager"></a>Monitorizar o gateway de gestão de nuvem no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Depois do gateway de gestão de nuvem está em execução e os clientes se ligam através dele, pode monitorizar os clientes e o tráfego de rede para se certificar de que sabe como o serviço está a efetuar.



## <a name="monitor-clients"></a>Clientes de monitor

Os clientes ligados através do gateway de gestão de nuvem aparecem na consola do Configuration Manager da mesma forma no local fazem de clientes. Para obter mais informações, consulte [como monitorizar clientes](/sccm/core/clients/manage/monitor-clients).



## <a name="monitor-traffic-in-the-console"></a>Monitorizar o tráfego na consola do

Monitorizar o tráfego no gateway de gestão de nuvem utilizando a consola do Configuration Manager:

1. Aceda a **administração > Serviços em nuvem > Gestão Gateway de nuvem**.

2. Selecione o gateway de gestão de nuvem no painel de lista.

3. Ver as informações de tráfego no painel de detalhes para o ponto de ligação de gateway de gestão de nuvem e as funções do sistema de sites liga-se ao.



## <a name="set-up-outbound-traffic-alerts"></a>Configurar alertas de tráfego de saída

Alertas de tráfego de saída ajudam a saber quando o tráfego de rede se aproxima um nível de limiar de 14 dias. Ao criar o gateway de gestão de nuvem, pode configurar alertas de tráfego. Se saltou a parte, pode ainda configurar os alertas após o serviço está em execução. Ajuste as definições de alerta em qualquer altura.

1. Aceda a **administração > Serviços em nuvem > Gestão Gateway de nuvem**.

2. Clique com o botão direito do gateway de gestão de nuvem no painel de lista e escolha **propriedades**.

3. Clique em de **alertas** separador. Ative o limiar e alertas. Especifique o limiar de dados de 14 dias em gigabytes (GB). Especifique também a percentagem de limiar para elevar os níveis de alerta diferentes.

4. Clique em **OK** quando tiver terminado.



## <a name="monitor-logs"></a>Registos de monitor

O gateway de gestão de nuvem gera entradas num número de ficheiros de registo. Para obter mais informações, consulte [registos do Configuration Manager](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway).
