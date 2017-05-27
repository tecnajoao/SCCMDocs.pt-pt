---
title: Gerir clientes na Internet - Configuration Manager | Documentos do Microsoft
description: "Saiba mais sobre gestão de clientes com o gateway de gestão de nuvem e gestão de clientes baseados na Internet no Configuration Manager."
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology:
- configmgr-client
ms.assetid: c667d6af-80c4-485f-910c-896c0171fd00
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 690d03d9c8c49a815bd318df549d7401a855bc5d
ms.openlocfilehash: 1b6752be448e1062c97a3225db4fa8af9f4832a6
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---

# <a name="manage-clients-on-the-internet-with-configuration-manager"></a>Gerir clientes na Internet com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Normalmente, no Gestor de configuração, a maioria dos computadores e servidores que estão a ser geridos é fisicamente na mesma interna privada ou empresarial rede como as servidores de sistema de sites que executam funções de gestão. No entanto, pode gerir computadores cliente fora da sua rede empresarial, se estiverem ligados à Internet sem necessidade dos clientes para se ligar através de redes privadas virtuais a chegar ao site servidores do sistema.

O Configuration Manager oferece duas formas de gerir os clientes ligadas à Internet:

-   Gateway de gestão da nuvem

-   Gestão de clientes baseada na Internet

## <a name="cloud-management-gateway"></a>Gateway de gestão da nuvem

Iniciar na versão 1610, o Configuration Manager apresenta gateway de gestão da nuvem. Este método novo fornece uma forma de gerir os clientes baseados na Internet utilizando uma combinação de um serviço de nuvem implementada para Microsoft Azure e uma nova função de sistema de sites que comunica com esse serviço. Os clientes, em seguida, utilizar o serviço para comunicar com o Configuration Manager.

Vantagens:

-   Nenhum investimento de infraestrutura adicionais necessário.

-   Não expõe infraestrutura no local para a Internet.

-   Máquinas virtuais na nuvem que executam o serviço completamente são geridas pelo Azure e não requerem nenhuma manutenção.

-   Fácil de configurar e configurados na consola do Configuration Manager.

Desvantagens:

-   Custo da subscrição da nuvem.

-   Dados de gestão enviados através do serviço em nuvem.

Para obter mais informações, consulte o artigo [planear de gateway de gestão da nuvem](plan-cloud-management-gateway.md).

## <a name="internet-based-client-management"></a>Gestão de clientes baseada na Internet

Este método depende de servidores de sistema de sites com acesso à Internet para o qual os clientes comunicam para fins de gestão. Este método necessita de clientes e servidores de sistema de sites para ser configurados para gestão baseados na Internet.

Vantagens:

-   Nenhum dependência do serviço de nuvem.

-   Sem custos adicionais associados a uma subscrição de nuvem.

-   Controlo total de servidores e funções de fornecer o serviço.

Desvantagens:

-   Necessitam de investimento de infraestrutura adicionais.

-   Sobrecarga e o custo operacional de infraestrutura adicional.

-   Infraestrutura têm de ficar exposta à Internet.

Para obter mais informações, consulte o artigo [planear a gestão de clientes baseados na Internet](plan-internet-based-client-management.md).

