---
title: Suporte para Windows 10
titleSuffix: Configuration Manager
description: "Saiba mais sobre as versões do Windows 10 que são suportadas como clientes ou para OSD com o System Center Configuration Manager."
ms.custom: na
ms.date: 01/25/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
caps.latest.revision: 
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2dfe9b63e9e7c41a4f8457dc5622f386c7cceec2
ms.sourcegitcommit: b13da5ad8ffd58e3b89fa6d7170e1dec3ff130a4
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/01/2018
---
# <a name="support-for-windows-10-for-system-center-configuration-manager"></a>Suporte para Windows 10 para o System Center Configuration Manager  

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


 Este tópico fornece detalhes sobre as versões do Windows 10 que pode utilizar com as diferentes versões do System Center Configuration Manager Current Branch. Este suporte inclui:
 -  Windows 10 como um cliente do Configuration Manager
 -  O Windows Assessment and Deployment Kit (ADK) para Windows 10

## <a name="windows-10-as-a-client"></a>Windows 10 como um cliente
O Configuration Manager tenta fornecer suporte como um cliente para cada nova versão do Windows 10 logo que possível após a ficar disponível. Porque os produtos tem agendas de lançamento e de desenvolvimento separadas, o suporte do Configuration Manager fornece depende da altura em cada fica disponível.

Por exemplo, uma versão do Configuration Manager ignora da matriz após [suporte para essa versão](/sccm/core/servers/manage/current-branch-versions-supported) termina. Da mesma forma, suporte para versões do Windows 10, como o LTSB 2015 de Enterprise ou remoções 1511 da matriz de quando estes são removidos do suporte. Para obter mais informações, consulte [sistemas operativos preteridos](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-client#deprecated-client-operating-systems).


-   Os seguinte suplementos de informações [sistemas operativos suportados para os clientes e dispositivos](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices).
-   Se utilizar a longo prazo manutenção ramo do Configuration Manager, consulte [configurações suportadas para o ramo de manutenção de longo prazo](/sccm/core/understand/supported-configurations-for-ltsb).

|Versão do Windows 10                    |  1702 o Configuration Manager          |    1706 o Configuration Manager |1710 o Configuration Manager          |  
|---------------------|-----|-----|-----|
|Enterprise 2015 LTSB                   |![Suportado](media/green_check.png) |![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) |
|Enterprise LTSB de 2016                   |![Suportado](media/green_check.png) |![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) |
|1607   <br />(Também conhecido como a atualização de aniversário da)<br />(*Consulte edições*)   |![Suportado](media/green_check.png) |![Suportado](media/green_check.png)            |![Suportado](media/green_check.png) |
|1703   <br />(Também conhecido como a atualização criadores)<br />(*Consulte edições*)      |![Retrocompatíveis com o](media/blue_compat.png) |![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) |
|1709   <br />(Também conhecido como a atualização de criadores de reversão)<br />(*Consulte edições*) |![Não suportado](media/Red_X.png)   |![Retrocompatíveis com o](media/blue_compat.png) | ![Suportado](media/green_check.png) |



**Edições:** Enterprise, Pro, Education, Pro Education   

|Chave|
|--|
|![Suportado](media/green_check.png) = **suportados**  |
|![Não suportado](media/blue_compat.png)  = **Backwards compatível** -existente funcionalidades de gestão de cliente (inventário de hardware, inventário de software, atualizações de software, etc.) deverão funcionar com a nova versão do Windows 10. Iremos irá Documente quaisquer problemas conhecidos ou avisos. <br><br>Esta abordagem dá-lhe a capacidade de implementar e gerir o novo Windows baseia-se um dia com suporte de compatibilidade da aplicação sem necessidade de uma nova versão de atualização do Configuration Manager. |
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
|![Suportado](media/green_check.png) = **suportados** - recomenda Windows utilizando o Windows ADK que corresponde à versão do Windows que está a implementar. Por exemplo, utilizar o Windows ADK para Windows 10 versão 1703 quando implementar o Windows 10 versão 1703. Para obter mais informações sobre o suporte de componentes do Windows ADK, consulte [DISM plataformas suportadas](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms) e [requisitos USMT](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1). |
|![Retrocompatível](media/blue_compat.png)  = **retrocompatível** -esta combinação não é testada, mas devem funcionar. Iremos irá Documente quaisquer problemas conhecidos ou avisos. |
|![Suportado](media/Red_X.png) = **não suportado**|
