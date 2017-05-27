---
title: "Gateway de gestão da nuvem monitor - Configuration Manager | Documentos do Microsoft"
description: 
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology:
- configmgr-client
ms.assetid: 15f72f80-9850-40ce-9c3a-443ba04b6a03
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 690d03d9c8c49a815bd318df549d7401a855bc5d
ms.openlocfilehash: daa0790995dc13ec2c78ae2d98a9eb38c0bcf8ae
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---

# <a name="monitor-cloud-management-gateway-in-configuration-manager"></a>Monitorizar o gateway de gestão de nuvem no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

A partir na versão 1610, depois do serviço em nuvem management gateway está em execução e os clientes estão a ligar através dele, pode monitorizar os clientes e o tráfego de rede para se certificar de que sabe como o serviço está a efetuar.

## <a name="monitor-clients"></a>Clientes de monitor

Clientes ligados através do serviço de gateway de gestão de nuvem aparecem na consola do Configuration Manager da mesma forma no local os clientes fazem. Para obter mais informações, consulte o artigo [como monitorizar clientes](monitor-clients.md).

## <a name="monitor-traffic-in-the-console"></a>Monitor de tráfego na consola do

Pode monitorizar o tráfego na nuvem management gateway utilizando a consola do Configuration Manager:

1. Aceda a **administração > Serviços em nuvem > Gestão Gateway de nuvem**.

2. Selecione o serviço em nuvem management gateway no painel de lista.

3. Visualizar as informações de tráfego no painel de detalhes para a função de ligação de gateway de gestão de nuvem e as funções de sistema de sites que liga-se a.

## <a name="set-up-outbound-traffic-alerts"></a>Configurar alertas de tráfego de saída

Alertas de tráfego de saída ajudará a saber quando tráfego estiver prestes a atingir um nível de limiar (2 semanas) 14 dias. É-lhe dada a opção de configuração de alertas de tráfego ao criar o serviço de gateway de gestão de nuvem. Se ignorada essa parte, pode ainda configurar os alertas após o serviço está em execução. E também pode ajustar as definições de alerta em qualquer altura.

1. Aceda a **administração > Serviços em nuvem > Gestão Gateway de nuvem**.

2. O serviço em nuvem management gateway no painel de lista com o botão direito e selecione **propriedades**.

3. Clique no separador de alertas e optar por ativar (ou desative) o limiar e os alertas. Em seguida, especifique o limiar de 14 dias (em GB) e percentagens do limiar para elevar os diferentes níveis de alerta.

4. Clique em **OK** quando terminar.

## <a name="monitor-logs"></a>Registos de monitor

O serviço de gateway de gestão de nuvem gera entradas num número de ficheiros de registo. Para obter mais informações, consulte o artigo [registos do Configuration Manager](/sccm/core/plan-design/hierarchy/log-files).

