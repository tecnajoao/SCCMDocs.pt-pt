---
title: "Defesa ameaça móveis | O System Center Configuration Manager"
description: "Restringir o acesso aos recursos da empresa com base em risco de dispositivo, rede e de aplicações utilizando o Configuration Manager e do Intune Mobile ameaça defesa parceiros"
ms.custom: na
ms.date: 03/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4c0e6824-2dfe-4700-b817-d5631e0eb872
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 266897b7ac674a369931e8ed63ff464edc10c9d8
ms.openlocfilehash: 298d879638a2d20d421b19752cb5f20f6725df14
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="intune-mobile-threat-defense-connectors-in-configuration-manager"></a>Conectores do Intune Mobile ameaça defesa no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O [MDM implementação (SCCM com o Intune) híbrida](https://docs.microsoft.com/en-us/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management) e a integração entre o Intune e os parceiros de Mobile ameaça defesa dão-lhe a capacidade de controlar o acesso a recursos da empresa e os dados com base na avaliação de riscos de dispositivo.

Os conectores do Intune Mobile ameaça defesa permitem-lhe tirar partido do seu fornecedor de Mobile ameaça defesa escolhido como fonte de informações do seu políticas de conformidade e as regras de acesso condicional. Isto permite aos administradores de TI adicionar uma camada de proteção para os respetivos recursos da empresa como o Exchange e Sharepoint, especificamente a partir de comprometida dispositivos móveis.

## <a name="what-problem-does-this-solve"></a>O problema isto resolver?

Empresas necessitem para proteger dados confidenciais contra ameaças emergentes, incluindo ameaças físicas, com base na aplicação e baseada na rede, bem como vulnerabilidades de sistema operativo.
Historically, empresas foram proativa quando PCs a proteger contra ataques, enquanto dispositivos móveis aceda não monitorizados e não protegidas. Plataformas móveis têm proteção incorporada, tais como o isolamento de aplicações e de consumidor vetted lojas de aplicações, mas estes plataformas permanecem vulneráveis a ataques de sofisticadas. Hoje em dia, os funcionários mais utilizarem dispositivos para o trabalho e necessitam de aceder a informações confidenciais. Dispositivos precisam de ser possível proteger contra ataques de dar sofisticadas.

## <a name="how-the-intune-mobile-threat-defense-connectors-work"></a>Como funcionam os conectores do Intune Mobile ameaça defesa?

O conector protege os recursos da empresa através da criação de um canal de comunicação entre o Intune e o fornecedor do Mobile ameaça defesa escolhido. Parceiros do Intune Mobile ameaça defesa oferecem intuitivos, fácil de implementar aplicações para dispositivos móveis que ativamente analisar e analisar informações de ameaças para partilhar com o Intune, para fins de relatórios ou imposição. Por exemplo, se uma aplicação móvel ameaça defesa ligada de relatórios para o fornecedor Mobile ameaça defesa que um telefone na sua rede está atualmente ligado a uma rede que é vulnerável a Man na ataques de Middle, esta informação é partilhada com e categorizada para um nível de risco adequado (baixa/médio/alto) – que, em seguida, pode ser comparado com as permissões de nível de risco configurado no Intune para determinar se deve ser revogado acesso a determinados recursos da sua preferência enquanto o dispositivo for comprometido.

## <a name="sample-scenarios"></a>Cenários de exemplo

Quando um dispositivo é considerado infetados pela solução de defesa de ameaça Mobile:

![](http://i.imgur.com/Li1WUOU.png)

É concedido acesso quando o dispositivo for remediado:

![](http://i.imgur.com/VCIwpdz.png)

## <a name="mobile-threat-defense-partners"></a>Parceiros de defesa de ameaça Mobile

Saiba como proteger o acesso a recursos da empresa com base no dispositivo, rede e o risco de aplicação com:

- [Atento](https://docs.microsoft.com/sccm/protect/deploy-use/lookout-mobile-threat-defense-in-configuration-manager)
