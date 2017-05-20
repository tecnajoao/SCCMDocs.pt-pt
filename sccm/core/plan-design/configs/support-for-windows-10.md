---
title: Suporte para Windows 10 | Documentos do Microsoft
description: "Saiba mais sobre as versões do Windows 10 que são suportadas como clientes ou para OSD com o System Center Configuration Manager."
ms.custom: na
ms.date: 05/09/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
caps.latest.revision: 5
author: brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: f809c9327db9f298168674add2d09820fdecd1b8
ms.openlocfilehash: ed5efcf7b305f8bee6e99e00c5285f6ae7033d82
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="support-for-windows-10-for-system-center-configuration-manager"></a>Suporte para Windows 10 para o System Center Configuration Manager  

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


 Este tópico fornece detalhes sobre as versões do Windows 10 que pode utilizar com as versões diferentes do ramo atual do System Center Configuration Manager. Isto inclui:
 -  Windows 10, como o cliente do Configuration Manager.
 -  O Windows 10 Windows Assessment and Deployment Kit (ADK).

## <a name="windows-10-as-a-client"></a>Windows 10 como um cliente
O Configuration Manager tenta fornecer suporte como um cliente para cada nova versão do Windows 10 com a brevidade possível após disponibilizar e que versão do Windows. Uma vez que os produtos que têm agendas de desenvolvimento e versão separadas, o suporte de que o Configuration Manager oferece depende da altura em versões e ramos de cada produto de versão.

Por exemplo, uma versão do Configuration Manager irá remover da matriz após [suporte para essa versão](/sccm/core/servers/manage/current-branch-versions-supported) termina. Da mesma forma, o suporte das versões do Windows 10, tal como o LTSB de 2015 Enterprise ou 1607 (CBB) irá remover da matriz quando os mesmos serão removidos da lista de configurações suportadas do Configuration Manager. Consulte o artigo [preterido sistemas operativos](/sccm/core/plan-design/changes/removed-and-deprecated-features#deprecated-operating-systems) para obter mais informações.

-   Os suplementos de informações seguintes [sistemas operativos suportados para os clientes e dispositivos](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices).
-   Se utilizar a longo prazo manutenção secundário do Configuration Manager, consulte o artigo [configurações suportadas para o ramo de manutenção de longo prazo](/sccm/core/understand/supported-configurations-for-ltsb).

|Versões do Windows 10                    |O Configuration Manager 1606          |O Configuration Manager 1610          |    O Configuration Manager 1702 |
|---------------------|-----|-----|-----|
|Enterprise LTSB de 2015                   |![Suportado](media/green_check.png) |![Suportado](media/green_check.png) |![Suportado](media/green_check.png) |
|1507 <br />(*ver edições*)            |![Suportado](media/green_check.png) |![Suportado](media/green_check.png) |![Suportado](media/green_check.png) |
|1511 (CB), (CBB)<br />(*ver edições*) |![Suportado](media/green_check.png) |![Suportado](media/green_check.png) |![Suportado](media/green_check.png) |
|Enterprise 2016 LTSB                   |![Suportado](media/green_check.png) |![Suportado](media/green_check.png) |![Suportado](media/green_check.png) |
|1607 (CB)    <br />Atualização de aniversário<br />(*ver edições*)      |![Compatível com versões anteriores](media/blue_compat.png) |![Suportado](media/green_check.png) |![Suportado](media/green_check.png) |
|1607 (CBB)    <br />Atualização de aniversário<br />(*ver edições*)      |![Não suportado](media/Red_X.png)   |![Suportado](media/green_check.png) |![Suportado](media/green_check.png) |
|1703 (CB)    <br />Criadores de atualização<br />(*ver edições*)      |![Não suportado](media/Red_X.png)   |![Não suportado](media/Red_X.png) |![Compatível com versões anteriores](media/blue_compat.png) |


**Edições:** Enterprise, educação Pro Pro, educação,   

|Chave|
|--|
|![Suportado](media/green_check.png) = **suportados**  |
|![Não suportado](media/blue_compat.png)  = **compatíveis com o Backwards** -Isto significa que existente funcionalidades de gestão de cliente (inventário de hardware, inventário de software, atualizações de software, etc.) deverá trabalhar com a nova compilação de ramo atual do Windows 10. Todos os problemas conhecidos e advertências serão documentadas. <br><br>Esta abordagem dá-lhe a capacidade de implementar e gerir novos Windows 10 CB baseia-se num dia com suporte de compatibilidade de aplicações sem necessidade de uma nova versão de atualização do Configuration Manager. |
|![Suportado](media/Red_X.png) = **não suportado**|


## <a name="windows-10-adk"></a>Windows 10 ADK
Quando implementar sistemas operativos com o Configuration Manager, o [Windows ADK é uma dependências externas](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment) que é necessário.

A tabela seguinte lista as versões do Windows 10 ADK que pode utilizar com diversas versões do Configuration Manager.

|Versões do Windows 10 ADK |O Configuration Manager 1606 |O Configuration Manager 1610  |O Configuration Manager 1702 |
|--------------------|-----|-----|-----|
|1507  |![Não suportado](media/Red_X.png)         |![Não suportado](media/Red_X.png)  |![Não suportado](media/Red_X.png)|
|1511  |![Compatível com versões anteriores](media/blue_compat.png)|![Não suportado](media/Red_X.png)  |![Não suportado](media/Red_X.png)|
|1607  |![Suportado](media/green_check.png)       |![Suportado](media/green_check.png)|![Compatível com versões anteriores](media/blue_compat.png) |
|1703  |![Não suportado](media/Red_X.png)         |![Não suportado](media/Red_X.png)  |![Suportado](media/green_check.png) |  

|Chave|
|--|
|![Suportados](media/green_check.png) = **suportados** - recomenda Windows utilizando o Windows ADK, que corresponde à versão do Windows estiver a implementar. Por exemplo, utilize o Windows ADK para Windows 10 versão 1703 ao implementar o Windows 10 versão 1703.  |
|![Compatível com versões anteriores](media/blue_compat.png)  = **compatíveis com versões anteriores** -esta combinação não é testada, mas deverá trabalhar. Todos os problemas conhecidos e advertências serão documentadas. |
|![Suportado](media/Red_X.png) = **não suportado**|

