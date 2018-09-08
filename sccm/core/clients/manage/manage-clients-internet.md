---
title: Gerir clientes na internet
titleSuffix: Configuration Manager
description: Saiba mais sobre a gestão de clientes com o gateway de gestão da nuvem e gestão de clientes baseados na internet no Configuration Manager.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.topic: conceptual
ms.technology: configmgr-client
ms.assetid: c667d6af-80c4-485f-910c-896c0171fd00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 198b044a66bf81ea846d5e4febe655b78c04dd13
ms.sourcegitcommit: 316899b08f2ef372993909e08e069f7edfed1d33
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/07/2018
ms.locfileid: "44111081"
---
# <a name="manage-clients-on-the-internet-with-configuration-manager"></a>Gerir clientes na internet com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Normalmente, no Gestor de configuração, a maioria dos computadores geridos e servidores está fisicamente na mesma rede interna como os servidores do sistema de sites que executam funções de gestão. No entanto, pode gerir os clientes fora da sua rede interna quando estiverem ligados à internet. Esta capacidade não requer os clientes ligar através de VPN para chegar ao site servidores do sistema.

O Configuration Manager fornece duas formas de gerir clientes ligados à internet:

-   Gateway de gestão na cloud

-   Gestão de clientes baseada na Internet


## <a name="cloud-management-gateway"></a>Gateway de gestão na cloud

O gateway de gestão da nuvem fornece gestão de clientes baseados na internet. Ele usa uma combinação de um serviço em nuvem do Microsoft Azure e uma nova função de sistema de sites que comunica com o serviço. Clientes baseados na Internet utilizam o serviço em nuvem para comunicar com o Gestor de configuração no local.

#### <a name="advantages"></a>Vantagens  

-   Sem investimento em infra-estrutura adicionais necessárias.  

-   Não expõem a infraestrutura no local para a internet.  

-   Máquinas de virtuais de nuvem que executam o serviço são totalmente geridas pelo Azure e não exigem nenhuma manutenção.  

-   Facilmente configurar e configurado na consola do Configuration Manager.  

#### <a name="disadvantages"></a>Desvantagens  

-   Custo de subscrição da cloud.  

-   Dados de gestão enviados através do serviço em nuvem.  

Para obter mais informações, consulte [planear para o gateway de gestão da cloud](plan-cloud-management-gateway.md).  



## <a name="internet-based-client-management"></a>Gestão de clientes baseada na Internet

Este método se baseia em servidores de sistema de sites com acesso à internet para que os clientes comunicam para fins de gestão. Ele requer clientes e servidores de sistema de sites para ser configurado para gestão baseada na internet.

#### <a name="advantages"></a>Vantagens  

-   Nenhuma dependência de serviço cloud.  

-   Sem custos adicionais associados a uma subscrição na nuvem.  

-   Controlo total de servidores e funções de fornecimento do serviço.  

#### <a name="disadvantages"></a>Desvantagens  

-   Exigir o investimento em infra-estrutura adicionais.  

-   Sobrecarga e os custos operacionais de infraestrutura adicional.  

-   Infraestrutura tem de ser exposta à internet.  

Para obter mais informações, consulte [planear a gestão de clientes baseada na internet de](plan-internet-based-client-management.md).  
