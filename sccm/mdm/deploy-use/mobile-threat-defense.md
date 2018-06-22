---
title: Restringir o acesso baseado em risco
titleSuffix: Configuration Manager
description: Restringir o acesso aos recursos da empresa com base em risco de dispositivo, rede e de aplicação.
ms.date: 04/25/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 9083c571-f4fc-4a78-adc5-8aec84dabcbd
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e921e6ab90eb57caf031b49d375d0017ea9a2930
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32346464"
---
# <a name="manage-access-to-company-resource-based-on-device-network-and-application-risk"></a>Gerir o acesso aos recursos da empresa com base no dispositivo, rede e o risco de aplicação

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Conectores de defesa de ameaça móveis permitem-lhe tirar partido do seu fornecedor de defesa de ameaça Mobile escolhido como uma origem de informações para as políticas de conformidade e as regras de acesso condicional. Isto permite aos administradores de TI adicionar uma camada de proteção para os respetivos recursos da empresa como o Exchange e Sharepoint, especificamente a partir com dispositivos móveis comprometidos.

## <a name="what-problem-does-this-solve"></a>Que problemas isto resolve?

Empresas necessitem para proteger os dados confidenciais contra ameaças emergentes, incluindo ameaças físicas, com base na aplicação e baseados na rede, bem como vulnerabilidades de sistema operativo.
Historicamente, as empresas têm sido proativa ao proteger os PCs de ataque, enquanto aceda de dispositivos móveis não monitorizado e não protegido. Plataformas móveis têm proteção incorporada, como o isolamento de aplicações e de lojas de aplicações de consumidor vetted, mas estas plataformas permanecem vulneráveis a ataques sofisticadas. Atualmente, os funcionários mais utilizarem dispositivos de trabalho e necessitam de aceder a informações confidenciais. Dispositivos têm de ser protegida contra ataques de cada vez mais sofisticadas.

O [(SCCM com o Intune) de implementação de MDM híbrida](https://docs.microsoft.com/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management) dá-lhe a capacidade de controlar o acesso a recursos da empresa e dados com base na avaliação de risco que fornecem soluções de proteção de ameaças de dispositivo, como Mobile ameaça defesa parceiros.

## <a name="how-the-intune-mobile-threat-defense-connectors-work"></a>Como funcionam os conectores do Intune Mobile ameaça defesa?

O conector protege os recursos da empresa através da criação de um canal de comunicação entre o Intune e o fornecedor de defesa de ameaça Mobile escolhido. Parceiros de defesa de ameaça do Intune Mobile oferecem intuitiva, fácil de implementar aplicações para dispositivos móveis que ativamente analisar e analisam as informações de ameaças para partilhar com o Intune, para fins de relatórios ou a imposição. Por exemplo, se uma aplicação de Mobile ameaça defesa ligada relatórios para o fornecedor de defesa de ameaça Mobile um telefone na sua rede está actualmente ligado a uma rede que é vulnerável a ataques Man nos ataques de meio, esta informação é partilhada com e categorizada para um nível de risco adequado (baixa/Média/alta) – que, em seguida, pode ser comparado ao seu allowances de nível de risco configurado no Intune para determinar se deve ser revogado acesso para certos recursos da sua preferência enquanto o dispositivo fica comprometido.

## <a name="sample-scenarios"></a>Cenários de exemplo

Quando um dispositivo é considerado infetados pela solução de Mobile ameaça defesa:

![Dispositivo móvel ameaça defesa infetados](../media/mtp/MTD-image-1.png)

Quando o dispositivo está sujeito a remediação, é concedido acesso:

![Mobile ameaça defesa acesso concedido](../media/mtp/MTD-image-2.png)

## <a name="next-steps"></a>Passos seguintes

Saiba como proteger o acesso aos recursos da empresa com base no dispositivo, rede e o risco de aplicação com:

- [Lookout](https://docs.microsoft.com/intune/deploy-use/lookout-mobile-threat-defense-connector)