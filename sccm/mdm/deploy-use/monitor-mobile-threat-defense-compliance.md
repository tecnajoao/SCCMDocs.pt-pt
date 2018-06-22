---
title: Monitorizar a conformidade de defesa de ameaça Mobile
titleSuffix: Configuration Manager
description: Monitorizar o estado de conformidade de parceiro Mobile ameaça defesa partir da consola do Configuration Manager
ms.date: 03/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 408190da-bea6-4122-9dd6-f90155040e88
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 24a066b30d6c220ecb5be8455a3150bd27936da7
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32347540"
---
# <a name="monitor-mobile-threat-defense-compliance"></a>**Monitorizar a conformidade de defesa de ameaça Mobile**

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

## <a name="to-monitor-the-overall-compliance-status"></a>Para monitorizar o estado de conformidade geral

Para monitorizar o estado de defesa de ameaça móveis:

1.  Na consola do Configuration Manager, clique em **monitorização** área de trabalho.

2.  No **monitorização** área de trabalho, clique em de **segurança** nós.

Pode ver um resumo do Estado de compatibilidade com níveis de ameaça diferentes, que é apresentado num formato gráfico visual. Pode clicar nas secções individuais dos gráficos para obter mais informações, como: 

- O número de relatórios não conformes como pela plataforma de dispositivos
- Quaisquer erros relacionados com o estado de conformidade do dispositivo

![](http://i.imgur.com/bmPsiWk.png)

## <a name="to-monitor-the-individual-compliance-status"></a>Para monitorizar o estado de conformidade individuais

Também pode ver o estado do dispositivo individual:

1.  Na consola do Configuration Manager, clique em **ativos e compatibilidade** área de trabalho.

2.  Clique em **dispositivos**.

> [!TIP] 
> Pode adicionar o **conformidade do dispositivo ameaça** e **nível de ameaças de dispositivo** colunas para ver o estado. Estas colunas não são apresentadas por predefinição.

## <a name="device-threat-protection-tab"></a>Separador de proteção contra ameaças do dispositivo

Além disso, no **dispositivos** ecrã, pode selecionar dispositivos específicos, em seguida, clique em de **proteção contra ameaças do dispositivo** separador fornece mais detalhes sobre o estado de conformidade do dispositivo. Localize abaixo as descrições das colunas e os respetivos valores esperados para ajudar a que analisar o estado de conformidade do dispositivo.

> [!IMPORTANT] 
> O separador proteção contra ameaças de dispositivo só aparece se o dispositivo selecionado é um dispositivo móvel.

|Nome da coluna|Visíveis por predefinição|Descrição| 
|-|-|-|
|**Descrição**| Sim | Detalhes sobre a ameaça fornecido pelo parceiro de defesa de ameaça Mobile. |
|**Hora da última atualização**| Sim | A última enviado do parceiro de defesa de ameaça Mobile atualizados detalhes sobre a ameaça para o Intune. |
|**Gravidade de ameaça**| Sim | Gravidade de ameaça é a definição de uma ameaça individuais com base na configuração de administração na consola do parceiro de defesa de ameaça Mobile. Tem um dos três valores seguintes: **Baixa**, **média** ou **elevada** |
|**Estado de ameaça**| Sim | O estado atual da ameaça no dispositivo. Estados possíveis: **Active Directory**, **resolvido** ou **ignoradas:** Indica que o utilizador ignorado a ameaça nos respetivos dispositivos, mas a ameaça ainda está presente. |
|**Tipo de ameaça**| Sim | Tipo de parceiro de Mobile ameaça defesa de ameaça. Valores possíveis: **Aplicação**, **ficheiro** ou **SO** |
|**ID de conta do AAD**| Não | O identificador exclusivo do Azure Active Directory. |
|**Classificação**| Sim | Parceiro de defesa de ameaça Mobile fornecido a classificação de ameaça. Valores possíveis: **Ativador de raiz, Riskware, Adware, Chargeware, DataLeak, Trojan, Worm, vírus, exploram, Backdoor, Bot, AppDropper, ClickFraud, Spam, Spyware, SurveillanceWare, vulnerabilidade, desconhecida, raiz Jailbrake, Conetividade, TollFraud, SideloadedApp** |
|**ID de dispositivo**| Não | O ID de objeto do Azure Active Directory que representa o dispositivo associado à área de trabalho com informações de ameaças. |
|**ID de ameaça**| Não | Parceiro de defesa de ameaça Mobile gerado um identificador exclusivo para a ameaça. O ID de ameaça é utilizado para resolução de controlo. |
|**URL de ameaça**| Não | Quando presente, as ligações de URL de ameaças de volta para a vista de consola de gestão do parceiro Mobile ameaça defesa desta ameaça específica. |

> [!TIP] 
> Certifique-se de ativar as colunas que não são **visíveis por predefinição** para ver mais detalhes sobre o estado de conformidade para os seus dispositivos móveis defesa de ameaça.
