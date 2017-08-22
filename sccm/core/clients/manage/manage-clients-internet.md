---
title: Gerir clientes na Internet - Configuration Manager | Microsoft Docs
description: "Saiba mais sobre a gestão de clientes com o gateway de gestão de nuvem e gestão de clientes baseados na Internet no Configuration Manager."
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: c667d6af-80c4-485f-910c-896c0171fd00
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 1b6752be448e1062c97a3225db4fa8af9f4832a6
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="manage-clients-on-the-internet-with-configuration-manager"></a>Gerir clientes na Internet com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Normalmente no Configuration Manager, a maioria dos computadores e servidores que estão a ser geridos está fisicamente no mesma privada ou empresarial rede interna que os servidores de sistema de sites que efetuam funções de gestão. No entanto, pode gerir computadores cliente fora da rede empresarial que estão ligados à Internet sem necessidade dos clientes ligar através de redes privadas virtuais a chegar ao site servidores do sistema.

Configuration Manager fornece duas formas de gerir clientes ligadas à Internet:

-   Gateway de gestão de nuvem

-   Gestão de clientes baseada na Internet

## <a name="cloud-management-gateway"></a>Gateway de gestão de nuvem

A partir da versão 1610, o Configuration Manager apresenta gateway de gestão de nuvem. Este novo método fornece uma forma de gerir clientes baseados na Internet utilizando uma combinação de um serviço em nuvem implementada para o Microsoft Azure e uma nova função de sistema de sites que comunica com esse serviço. Os clientes, em seguida, utilizar o serviço para comunicar com o Configuration Manager.

Vantagens:

-   Não existem investimento de infraestrutura adicionais necessário.

-   Não expõe a infraestrutura no local para a Internet.

-   Máquinas virtuais na nuvem que executam o serviço são geridas completamente pelo Azure e não requerem nenhuma manutenção.

-   Facilmente definido e configurado na consola do Configuration Manager.

Desvantagens:

-   Custo de subscrição da nuvem.

-   Dados de gestão enviados através do serviço em nuvem.

Para obter mais informações, consulte [planear para o gateway de gestão de nuvem](plan-cloud-management-gateway.md).

## <a name="internet-based-client-management"></a>Gestão de clientes baseada na Internet

Este método baseia-se em servidores de sistema de site para a Internet para que os clientes comunicam para efeitos de gestão. Este método requer que os clientes e servidores de sistema de sites configurados para gestão baseada na Internet.

Vantagens:

-   Não existem dependência do serviço de nuvem.

-   Sem custos adicionais associados a uma subscrição na nuvem.

-   Controlo total de servidores e funções de fornecer o serviço.

Desvantagens:

-   Requerem um investimento infraestrutura adicionais.

-   Sobrecarga e o custo operacional de infraestrutura adicional.

-   Infraestrutura tem de ser exposta à Internet.

Para obter mais informações, consulte [planear a gestão de clientes baseada na Internet de](plan-internet-based-client-management.md).
