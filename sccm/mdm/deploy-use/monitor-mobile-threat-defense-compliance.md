---
title: Monitorizar a conformidade do Mobile Threat Defense
titleSuffix: Configuration Manager
description: Monitorizar o estado de conformidade de parceiros de defesa contra ameaças móveis partir da consola do Configuration manager
ms.date: 03/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 408190da-bea6-4122-9dd6-f90155040e88
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: cc5b38894155df35812d14397fb0d3aaea79c585
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56122496"
---
# <a name="monitor-mobile-threat-defense-compliance"></a>**Monitorizar a conformidade do Mobile Threat Defense**

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

## <a name="to-monitor-the-overall-compliance-status"></a>Para monitorizar o estado de conformidade geral

Para monitorizar o estado de defesa contra ameaças móveis:

1.  Na consola do Configuration Manager, clique em **monitorização** área de trabalho.

2.  Na **monitorização** área de trabalho, clique na **segurança** nó.

Pode ver um resumo do Estado da conformidade com os níveis de ameaça diferentes, que é exibido num formato gráfico visual. Pode clicar nas secções individuais dos gráficos para ver mais informações, como: 

- O número de dispositivos que comunicam como não conforme pela plataforma
- Quaisquer erros relacionados com o estado de conformidade do dispositivo

![](http://i.imgur.com/bmPsiWk.png)

## <a name="to-monitor-the-individual-compliance-status"></a>Para monitorizar o estado de conformidade individual

Também pode ver o estado do dispositivo individuais:

1.  Na consola do Configuration Manager, clique em **ativos e compatibilidade** área de trabalho.

2.  Clique em **dispositivos**.

> [!TIP] 
> Pode adicionar os **conformidade de ameaça do dispositivo** e o **nível de ameaça do dispositivo** colunas para ver o estado. Estas colunas não são apresentadas por predefinição.

## <a name="device-threat-protection-tab"></a>Guia de proteção contra ameaças de dispositivos

Além disso, na **dispositivos** tela, pode selecionar dispositivos específicos, em seguida, clique no **Device Threat Protection** guia que fornece mais detalhes sobre o estado de conformidade do dispositivo. Encontre abaixo as descrições de coluna e os respetivos valores de esperado para o ajudar a que analisar o estado de conformidade do dispositivo.

> [!IMPORTANT] 
> A guia de proteção contra ameaças de dispositivos só aparece se o dispositivo selecionado é um dispositivo móvel.

|Nome da coluna|Visível por padrão|Descrição| 
|-|-|-|
|**Descrição**| Sim | Detalhes sobre a ameaça fornecida pelo parceiro de defesa contra ameaças móveis. |
|**Hora da última atualização**| Sim | A última vez enviado o parceiro de defesa contra ameaças móveis atualizados detalhes sobre a ameaça ao Intune. |
|**Gravidade da ameaça**| Sim | Gravidade da ameaça é a definição para uma ameaça de individual com base na configuração do Centro de administração na consola do parceiro de defesa contra ameaças móveis. Ele tem um dos três valores: **Baixa**, **médio** ou **elevada** |
|**Estado da ameaça**| Sim | O estado atual da ameaça no dispositivo. Estados possíveis: **Active Directory**, **resolvido** ou **ignorados:** Indica que o utilizador ignorou a ameaça no dispositivo, mas a ameaça ainda está presente. |
|**Tipo de ameaça**| Sim | Tipo de parceiro de defesa contra ameaças móveis de ameaça. Valores possíveis: **Aplicação**, **arquivo** ou **SO** |
|**ID de conta do AAD**| Não | O identificador exclusivo do Azure Active Directory. |
|**Classification** (Classificação)| Sim | Parceiro de Mobile Threat Defense fornecido a classificação de ameaça. Valores possíveis: **Ativador de raiz, Riskware, Adware, Chargeware, DataLeak, cavalo de Tróia, worms, vírus, explorar, Backdoor, Bot, AppDropper, ClickFraud, Spam, Spyware, SurveillanceWare, vulnerabilidade, desconhecida, Jailbrake, conectividade, TollFraud, SideloadedApp de raiz** |
|**ID do dispositivo**| Não | O ID de objeto do Azure Active Directory que representa o dispositivo associado à área de trabalho com informações de ameaças. |
|**ID de ameaça**| Não | Parceiro de defesa contra ameaças móveis gerados pelo identificador exclusivo para a ameaça. O ID de ameaça é utilizado para resolução de acompanhamento. |
|**URL da ameaça**| Não | Quando estiver presente, os links de URL da ameaça para regressar à vista de consola de gestão do parceiro de defesa contra ameaças móveis dessa ameaça específica. |

> [!TIP] 
> Certifique-se ativar as colunas que não sejam **visível por padrão** para ver mais detalhes sobre o estado de conformidade Mobile Threat Defense para os seus dispositivos.
