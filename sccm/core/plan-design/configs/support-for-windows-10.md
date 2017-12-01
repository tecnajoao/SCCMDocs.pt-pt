---
title: Suporte para Windows 10
titleSuffix: Configuration Manager
description: "Saiba mais sobre as versões do Windows 10 que são suportadas como clientes ou para OSD com o System Center Configuration Manager."
ms.custom: na
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
caps.latest.revision: "5"
author: mstewart
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: b3a11357f068416bfa4d4c9faf20aa154618306d
ms.sourcegitcommit: 7fe45ff75f05f7cc03ad021db8119791abe18049
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/01/2017
---
# <a name="support-for-windows-10-for-system-center-configuration-manager"></a>Suporte para Windows 10 para o System Center Configuration Manager  

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


 Este tópico fornece detalhes sobre as versões do Windows 10 que pode utilizar com as diferentes versões do System Center Configuration Manager Current Branch. Isto inclui:
 -  Windows 10 como cliente do Configuration Manager.
 -  O Windows 10 Windows Assessment and Deployment Kit (ADK).

## <a name="windows-10-as-a-client"></a>Windows 10 como um cliente
O Configuration Manager tenta fornecer suporte como um cliente para cada nova versão do Windows 10 logo que possível após a ficar disponível. Porque os produtos tem agendas de lançamento e de desenvolvimento separadas, o suporte do Configuration Manager fornece depende da altura em cada fica disponível.

Por exemplo, uma versão do Configuration Manager irá remover da matriz após [suporte para essa versão](/sccm/core/servers/manage/current-branch-versions-supported) termina. Da mesma forma, suporte para versões do Windows 10 LTSB de 2015 Enterprise ou 1511 irá remover da matriz quando estes são removidos do suporte. Consulte [sistemas operativos preteridos](/sccm/core/plan-design/changes/removed-and-deprecated-features#deprecated-operating-systems) para obter mais informações.

-   Os seguinte suplementos de informações [sistemas operativos suportados para os clientes e dispositivos](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices).
-   Se utilizar a longo prazo manutenção ramo do Configuration Manager, consulte [configurações suportadas para o ramo de manutenção de longo prazo](/sccm/core/understand/supported-configurations-for-ltsb).

|Versão do Windows 10                    |  1702 o Configuration Manager          |    1706 o Configuration Manager |1710 o Configuration Manager          |  
|---------------------|-----|-----|-----|
|LTSB 2015 de Enterprise                   |![Suportado](media/green_check.png) |![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) |
|Enterprise LTSB de 2016                   |![Suportado](media/green_check.png) |![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) |
|1607   <br />(Também conhecido como a atualização de aniversário da)<br />(*Consulte edições*)   |![Suportado](media/green_check.png) |![Suportado](media/green_check.png)            |![Suportado](media/green_check.png) |
|1703   <br />(Também conhecido como a atualização criadores)<br />(*Consulte edições*)      |![Retrocompatíveis com o](media/blue_compat.png) |![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) |
|1709   <br />(Também conhecido como a atualização de criadores de reversão)<br />(*Consulte edições*) |![Não suportado](media/Red_X.png)   |![Retrocompatíveis com o](media/blue_compat.png) | ![Suportado](media/green_check.png) |



**Edições:** Enterprise, educação Pro Pro, Education,   

|Chave|
|--|
|![Suportado](media/green_check.png) = **suportados**  |
|![Não suportado](media/blue_compat.png)  = **Backwards compatível** -Isto significa que os existentes funcionalidades de gestão de cliente (inventário de hardware, inventário de software, atualizações de software, etc.) deverão funcionar com a nova versão do Windows 10. Serão documentados quaisquer problemas conhecidos ou avisos. <br><br>Esta abordagem dá-lhe a capacidade de implementar e gerir o novo Windows baseia-se um dia com suporte de compatibilidade da aplicação sem necessidade de uma nova versão de atualização do Configuration Manager. |
|![Suportado](media/Red_X.png) = **não suportado**|


## <a name="windows-10-adk"></a>Windows 10 ADK
Quando implementar sistemas operativos com o Configuration Manager, o [Windows ADK é uma dependências externas](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment) que é necessário.

A tabela seguinte lista as versões do Windows 10 ADK que pode utilizar com diferentes versões do Configuration Manager.

|Versão do Windows 10 ADK  |1702 o Configuration Manager   |1706 o Configuration Manager |1710 o Configuration Manager |
|--------------------|-----|-----|-----|
|1607  |![Retrocompatíveis com o](media/blue_compat.png) |![Não suportado](media/Red_X.png)| ![Não suportado](media/Red_X.png) |
|1703  |![Suportado](media/green_check.png)            |![Suportado](media/green_check.png) | ![Retrocompatíveis com o](media/blue_compat.png)|
|1709  |![Não suportado](media/Red_X.png)              |![Suportado](media/green_check.png) | ![Suportado](media/green_check.png)|

|Chave|
|--|
|![Suportado](media/green_check.png) = **suportados** - recomenda Windows utilizando o Windows ADK que corresponde à versão do Windows que está a implementar. Por exemplo, utilizar o Windows ADK para Windows 10 versão 1703 quando implementar o Windows 10 versão 1703.  |
|![Retrocompatível](media/blue_compat.png)  = **retrocompatível** -esta combinação não é testada, mas devem funcionar. Serão documentados quaisquer problemas conhecidos ou avisos. |
|![Suportado](media/Red_X.png) = **não suportado**|
