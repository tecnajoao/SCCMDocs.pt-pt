---
title: Restringir o acesso com base no risco
titleSuffix: Configuration Manager
description: Restringir o acesso aos recursos da empresa com base em riscos de aplicações, redes e dispositivos.
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 9083c571-f4fc-4a78-adc5-8aec84dabcbd
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a00a4e8140548c4f503e3467626b8d6cbab69ee3
ms.sourcegitcommit: 98c3f7848dc9014de05541aefa09f36d49174784
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/14/2018
ms.locfileid: "42586210"
---
# <a name="manage-access-to-company-resource-based-on-device-network-and-application-risk"></a>Gerir o acesso a recursos da empresa com base em riscos de aplicações, redes e dispositivos

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Conectores de defesa contra ameaças móveis permitem-lhe tirar partido do seu fornecedor de defesa contra ameaças móveis escolhido como uma fonte de informações para as suas políticas de conformidade e regras de acesso condicional. Isto permite-lhe adicionar uma camada de proteção para recursos da sua organização como o Exchange e Sharepoint, especificamente de dispositivos móveis comprometidos.

> [!Important]  
> A partir de 14 de Agosto de 2018, gestão de dispositivos móveis híbrida é um [funcionalidade preterida](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Para obter mais informações, consulte [o que é a MDM híbrida](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  



## <a name="what-problem-does-this-solve"></a>Que problema é que isto resolve?

As organizações precisam de proteger dados confidenciais de ameaças emergentes que incluem ameaças com base na aplicação e físicas baseados na rede, bem como vulnerabilidades do SO.

Historicamente, as organizações foram proativas ao proteger os PCs contra ataques, enquanto os dispositivos móveis permaneciam não monitorizados e desprotegidos. Plataformas móveis terem proteção incorporada, como o isolamento de aplicações e lojas de aplicações de clientes avaliadas, mas estas plataformas permanecem vulneráveis a ataques sofisticados. Hoje em dia, mais funcionários utilizem os dispositivos para o trabalho e precisam de acesso a informações confidenciais. Dispositivos têm de ser protegidos contra ataques cada vez mais sofisticados.



## <a name="how-the-intune-mobile-threat-defense-connectors-work"></a>Como funcionam os conectores de defesa contra ameaças do Intune Mobile?

O conector protege os recursos da organização através da criação de um canal de comunicação entre o Intune e o seu fornecedor de defesa contra ameaças móveis escolhido. Parceiros de defesa contra ameaças do Intune Mobile oferecem intuitivas e fáceis de implementar aplicações para dispositivos móveis que detetam e analisam as informações de ameaças para partilhar com o Intune ativamente. Utilize estas informações para fins de relatórios ou imposição. 

Por exemplo, uma aplicação de Mobile Threat Defense ligada comunica ao fornecedor de defesa contra ameaças móveis que um dispositivo estiver presentemente conectado a uma rede que são vulnerável a ataques man-in-the-middle. Esta informação é partilhada com e categorizada para um nível de risco adequado: baixa, média ou alta. Compare esse risco com sua concessões de nível de risco configurados no Intune para determinar se deve ser revogado acesso a determinados recursos da sua preferência, enquanto o dispositivo estiver comprometido.



## <a name="sample-scenarios"></a>Cenários de exemplo

Quando um dispositivo é considerado infetado pela solução de defesa contra ameaças móveis:

![Dispositivo Mobile Threat Defense infetados](../media/mtp/MTD-image-1.png)

Acesso será concedido quando o dispositivo for remediado:

![Mobile Threat Defense acesso concedido](../media/mtp/MTD-image-2.png)



## <a name="next-steps"></a>Passos seguintes

Saiba como proteger o acesso a recursos da empresa com base no risco da aplicação com, redes e dispositivos:

- [Lookout](https://docs.microsoft.com/intune/deploy-use/lookout-mobile-threat-defense-connector)