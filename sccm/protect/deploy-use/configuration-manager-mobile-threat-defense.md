---
title: "Defesa ameaça móveis"
titleSuffix: Configuration Manager
description: "Restringir o acesso aos recursos da empresa com base em risco de dispositivo, rede e de aplicação utilizando o Configuration Manager e o Intune Mobile ameaça defesa parceiros"
ms.custom: na
ms.date: 03/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4c0e6824-2dfe-4700-b817-d5631e0eb872
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 83911f35dbe8fc7bc24a4885929fbdf5660e7285
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="intune-mobile-threat-defense-connectors-in-configuration-manager"></a>Conectores do Intune Mobile ameaça defesa no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O [(SCCM com o Intune) de implementação de MDM híbrida](https://docs.microsoft.com/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management) e a integração entre o Intune e os parceiros de defesa de ameaça móveis dão-lhe a capacidade de controlar o acesso a recursos da empresa e dados com base na avaliação de riscos de dispositivo.

Conectores do Intune Mobile ameaça defesa permitem-lhe tirar partido do seu fornecedor de defesa de ameaça Mobile escolhido como uma origem de informações para as políticas de conformidade e as regras de acesso condicional. Isto permite aos administradores de TI adicionar uma camada de proteção para os respetivos recursos da empresa como o Exchange e Sharepoint, especificamente a partir com dispositivos móveis comprometidos.

## <a name="what-problem-does-this-solve"></a>Que problemas isto resolve?

Empresas necessitem para proteger os dados confidenciais contra ameaças emergentes, incluindo ameaças físicas, com base na aplicação e baseados na rede, bem como vulnerabilidades de sistema operativo.
Historicamente, as empresas têm sido proativa ao proteger os PCs de ataque, enquanto aceda de dispositivos móveis não monitorizado e não protegido. Plataformas móveis têm proteção incorporada, como o isolamento de aplicações e de lojas de aplicações de consumidor vetted, mas estas plataformas permanecem vulneráveis a ataques sofisticadas. Atualmente, os funcionários mais utilizarem dispositivos de trabalho e necessitam de aceder a informações confidenciais. Dispositivos têm de ser protegida contra ataques de cada vez mais sofisticadas.

## <a name="how-the-intune-mobile-threat-defense-connectors-work"></a>Como funcionam os conectores do Intune Mobile ameaça defesa?

O conector protege os recursos da empresa através da criação de um canal de comunicação entre o Intune e o fornecedor de defesa de ameaça Mobile escolhido. Parceiros de defesa de ameaça do Intune Mobile oferecem intuitiva, fácil de implementar aplicações para dispositivos móveis que ativamente analisar e analisam as informações de ameaças para partilhar com o Intune, para fins de relatórios ou a imposição. Por exemplo, se uma aplicação de Mobile ameaça defesa ligada relatórios para o fornecedor de defesa de ameaça Mobile um telefone na sua rede está actualmente ligado a uma rede que é vulnerável a ataques Man nos ataques de meio, esta informação é partilhada com e categorizada para um nível de risco adequado (baixa/Média/alta) – que, em seguida, pode ser comparado ao seu allowances de nível de risco configurado no Intune para determinar se deve ser revogado acesso para certos recursos da sua preferência enquanto o dispositivo fica comprometido.

## <a name="sample-scenarios"></a>Cenários de exemplo

Quando um dispositivo é considerado infetados pela solução de Mobile ameaça defesa:

![](http://i.imgur.com/Li1WUOU.png)

Quando o dispositivo está sujeito a remediação, é concedido acesso:

![](http://i.imgur.com/VCIwpdz.png)

## <a name="mobile-threat-defense-partners"></a>Parceiros de defesa de ameaça Mobile

Saiba como proteger o acesso aos recursos da empresa com base no dispositivo, rede e o risco de aplicação com:

- [Lookout](https://docs.microsoft.com/sccm/protect/deploy-use/lookout-mobile-threat-defense-in-configuration-manager)
