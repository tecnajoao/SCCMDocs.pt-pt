---
title: Gerir clientes na internet
titleSuffix: Configuration Manager
description: Saiba mais sobre a gestão de clientes com o gateway de gestão de nuvem e gestão de clientes baseados na internet no Configuration Manager.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: c667d6af-80c4-485f-910c-896c0171fd00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6296a171f2ef225dbbf647eb5e53103650d60c11
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32332265"
---
# <a name="manage-clients-on-the-internet-with-configuration-manager"></a>Gerir clientes na internet com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Normalmente, no Gestor de configuração, a maioria dos computadores geridos e servidores está fisicamente na rede interna mesma que os servidores de sistema de sites que efetuam funções de gestão. No entanto, pode gerir os clientes fora da rede interna quando estão ligados à internet. Esta capacidade não requer que os clientes ligar através de VPN a chegar ao site servidores do sistema.

Configuration Manager fornece duas formas de gerir clientes ligados à internet:

-   Gateway de gestão de nuvem

-   Gestão de clientes baseada na Internet


## <a name="cloud-management-gateway"></a>Gateway de gestão de nuvem

O gateway de gestão de nuvem fornece gestão de clientes baseados na internet. Utiliza uma combinação de um serviço em nuvem do Microsoft Azure e uma nova função de sistema de sites que comunica com esse serviço. Os clientes baseados na Internet utilizar o serviço em nuvem para comunicar com o Gestor de configuração no local.

#### <a name="advantages"></a>Vantagens  

-   Não existem investimento de infraestrutura adicionais necessário.  

-   Não expõe a infraestrutura no local para a internet.  

-   Máquinas virtuais na nuvem que executam o serviço são geridas completamente pelo Azure e não requerem nenhuma manutenção.  

-   Facilmente definido e configurado na consola do Configuration Manager.  

#### <a name="disadvantages"></a>Desvantagens  

-   Custo de subscrição da nuvem.  

-   Dados de gestão enviados através do serviço em nuvem.  

Para obter mais informações, consulte [planear para o gateway de gestão de nuvem](plan-cloud-management-gateway.md).  



## <a name="internet-based-client-management"></a>Gestão de clientes baseada na Internet

Este método baseia-se em servidores de sistema de site para a internet para que os clientes comunicam para efeitos de gestão. Requer clientes e servidores de sistema de sites configurados para gestão baseada na internet.

#### <a name="advantages"></a>Vantagens  

-   Não existem dependência do serviço de nuvem.  

-   Sem custos adicionais associados a uma subscrição na nuvem.  

-   Controlo total de servidores e funções de fornecer o serviço.  

#### <a name="disadvantages"></a>Desvantagens  

-   Requerem um investimento infraestrutura adicionais.  

-   Sobrecarga e o custo operacional de infraestrutura adicional.  

-   Infraestrutura tem de ser exposta à internet.  

Para obter mais informações, consulte [planear a gestão de clientes baseada na internet de](plan-internet-based-client-management.md).  
