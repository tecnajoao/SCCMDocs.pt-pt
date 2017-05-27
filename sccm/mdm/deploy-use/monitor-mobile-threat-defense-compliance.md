---
title: "Monitorizar a compatibilidade de Mobile ameaça defesa | O System Center Configuration Manager"
description: "Monitorizar o estado de compatibilidade de parceiro Mobile ameaça defesa da consola do Configuration manager"
ms.custom: na
ms.date: 03/21/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 408190da-bea6-4122-9dd6-f90155040e88
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 212628639300e9c361f7cee61b3df6b1cb6874ce
ms.openlocfilehash: 8edf83a0f761dfc16274ce49c3aa2b878c7fe6cd
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---

# <a name="monitor-mobile-threat-defense-compliance"></a>**Monitorizar a compatibilidade de defesa de ameaça Mobile**

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

## <a name="to-monitor-the-overall-compliance-status"></a>Para monitorizar o estado de conformidade geral

Para monitorizar o estado de defesa ameaça móveis:

1.  Na consola do Configuration Manager, clique nos **monitorização** área de trabalho.

2.  No **monitorização** área de trabalho, clique na **segurança** nó.

Pode ver um resumo do Estado de compatibilidade com níveis de ameaça diferentes, que é apresentado num formato gráfico visual. Pode clicar nas secções individuais dos gráficos para obter mais informações, como: 

- O número de relatórios não conformes como pela plataforma de dispositivos
- Quaisquer erros relacionados com o estado de compatibilidade do dispositivo

![](http://i.imgur.com/bmPsiWk.png)

## <a name="to-monitor-the-individual-compliance-status"></a>Para monitorizar o estado de compatibilidade individuais

Também pode ver o estado dos dispositivos individuais:

1.  Na consola do Configuration Manager, clique nos **ativos e compatibilidade** área de trabalho.

2.  Clique no **dispositivos**.

> [!TIP] 
> Pode adicionar o **conformidade do dispositivo ameaça** e **nível de ameaças de dispositivo** colunas para ver o estado. Estas colunas não são apresentadas por predefinição.

## <a name="device-threat-protection-tab"></a>Separador de proteção de ameaça de dispositivo

Além disso, no **dispositivos** ecrã, pode selecionar dispositivos específicos, em seguida, clique no **dispositivo ameaça proteção** separador que fornece mais detalhes sobre o estado de conformidade do dispositivo. Localize abaixo as descrições de colunas e os respetivos valores esperados para o ajudar a analisa o estado de compatibilidade do dispositivo.

> [!IMPORTANT] 
> No separador dispositivos ameaça proteção só aparece se o dispositivo selecionado é um dispositivo móvel.

|Nome da coluna|Visível por predefinição|Descrição| 
|-|-|-|
|**Descrição**| Sim | Detalhes sobre a ameaça fornecidas pelo parceiro de defesa de ameaça Mobile. |
|**Hora da última atualização**| Sim | A última vez que o parceiro de Mobile ameaça defesa enviado atualizado com detalhes sobre a ameaça ao Intune. |
|**Gravidade de ameaça**| Sim | Gravidade de ameaça é a definição para uma ameaça individual consoante a configuração de administração na consola de parceiro do Mobile ameaça defesa. Tem um dos três valores: **Low**, **Medium** or **High** |
|**Estado de ameaça**| Sim | O estado atual da ameaça no dispositivo. Estados possíveis: **Active Directory**, **resolvido** ou **ignoradas:** Indica que o utilizador ignorada a ameaça nos respetivos dispositivos, mas a ameaça ainda está presente. |
|**Tipo de ameaça**| Sim | Tipo de parceiro Mobile ameaça defesa de ameaça. Valores possíveis: **App**, **File** or **OS** |
|**ID de conta do AAD**| Não | O identificador exclusivo do Azure Active Directory. |
|**Classificação**| Sim | Parceiro de Mobile ameaça defesa fornecido classificação de ameaça. Valores possíveis: **Ativador de raiz, Riskware, Adware, Chargeware, DataLeak, Trojan, Worm, vírus, explorar, Backdoor, Bot, AppDropper, ClickFraud, Spam, Spyware, SurveillanceWare, vulnerabilidade, desconhecida, raiz Jailbrake, conectividade, TollFraud, SideloadedApp** |
|**ID do dispositivo**| Não | O ID de objeto do Azure Active Directory que representa o dispositivo associado à área de trabalho com as informações de ameaças. |
|**ID de ameaça**| Não | Parceiro de Mobile ameaça defesa gerado um identificador exclusivo para a ameaça. O ID de ameaça é utilizado para controlar a resolução. |
|**URL de ameaça**| Não | Quando presente, as ligações de ameaça URL novamente para a vista da consola de gestão do parceiro Mobile ameaça defesa desta ameaça específica. |

> [!TIP] 
> Certifique-se ativar as colunas que não são **visível por predefinição** para ver mais detalhes sobre o estado de compatibilidade Mobile ameaça defesa para os seus dispositivos.

