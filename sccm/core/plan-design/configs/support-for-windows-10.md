---
title: Suporte para Windows 10
titleSuffix: Configuration Manager
description: Saiba mais sobre as versões do Windows 10 que são suportadas como clientes ou para OSD com o System Center Configuration Manager
ms.date: 04/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 947392d4c11b419e0e373fbe83db42522d3c5f25
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="support-for-windows-10-in-system-center-configuration-manager"></a>Suporte para Windows 10 no System Center Configuration Manager  

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Saiba mais sobre as versões do Windows 10 que suporta o Configuration Manager, incluindo:
 -  [Windows 10 como um cliente do Configuration Manager](#windows-10-as-a-client)
 -  [O Windows Assessment and Deployment Kit (ADK) para Windows 10](#windows-10-adk)



## <a name="windows-10-as-a-client"></a>Windows 10 como um cliente
O Configuration Manager tenta fornecer suporte como um cliente para cada nova versão do Windows 10 logo que possível após a ficar disponível. Porque os produtos tem agendas de lançamento e de desenvolvimento separadas, o suporte do Configuration Manager fornece depende da altura em cada fica disponível.

Por exemplo, uma versão do Configuration Manager ignora da matriz após [suporte para essa versão](/sccm/core/servers/manage/current-branch-versions-supported) termina. Da mesma forma, suporte para versões do Windows 10, como o LTSB 2015 de Enterprise ou remoções 1511 da matriz de quando estes são removidos do suporte. Para obter mais informações, consulte [sistemas operativos preteridos](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-client#deprecated-client-operating-systems).

-   Estas informações complementam [sistemas operativos suportados para os clientes e dispositivos](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices).  

-   Se utilizar o ramo de manutenção longo prazo do Configuration Manager, consulte [as configurações suportadas para o ramo de manutenção longo prazo](/sccm/core/understand/supported-configurations-for-ltsb).  

<br/>
A tabela seguinte lista as versões do Windows 10 que pode utilizar como um cliente com versões diferentes do Configuration Manager.

| Versão do Windows 10 | 1706 o Configuration Manager | 1710 o Configuration Manager | 1802 o Configuration Manager |
|---------------------|-----|-----|-----|
| LTSB 2015 de Enterprise            <!--10/14/2025-->   | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) |
| Enterprise LTSB de 2016            <!--10/13/2026-->   | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) |
| 1607   <br />(*Consulte edições*)   <!--04+6/10/2018-->   | ![Suportado](media/green_check.png) <sup>1</sup> | ![Suportado](media/green_check.png) <sup>1</sup> | ![Suportado](media/green_check.png) <sup>1</sup> |
| 1703   <br />(*Consulte edições*)   <!--10+6/09/2018-->   | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) |
| 1709   <br />(*Consulte edições*)   <!--04+6/09/2019-->   | ![Retrocompatíveis com o](media/blue_compat.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) |
| 1803   <br />(*Consulte edições*)   <!--11/12/2019-->   | ![Não suportado](media/Red_X.png) | ![Não suportado](media/Red_X.png) | ![Suportado](media/green_check.png) |

<!-- lifecycle reference: https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet -->

**Edições**: Enterprise, educação Pro Pro, Education,   

<sup>1</sup> para obter mais informações, consulte [folha do facto de ciclo de vida de Windows](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet) e a secção em "Extensão de serviço para edições Enterprise e Education".

| Chave |
|--|
| ![Suportado](media/green_check.png) = **suportados**  |
| ![Compatível com a Backwards](media/blue_compat.png)  = **Backwards compatível** <br/> As funcionalidades de gestão existentes do cliente deverá trabalhar com a nova versão do Windows 10. Por exemplo, inventário de hardware, inventário de software e atualizações de software. Iremos irá Documente quaisquer problemas conhecidos ou avisos. <br><br>Esta abordagem dá-lhe a capacidade de implementar e gerir as novas versões do Windows imediato com suporte de compatibilidade da aplicação e, sem necessidade de uma nova versão de atualização do Configuration Manager. |
| ![Não suportado](media/Red_X.png) = **não suportado** |

 > [!NOTE]  
 > A partir de versão 1802, o Configuration Manager suporta o cliente em dispositivos Windows 10 ARM64. As funcionalidades de gestão existentes do cliente deverá trabalhar com estes novos dispositivos. Por exemplo, hardware e inventário de software, atualizações de software e gestão de aplicações. Implementação do SO não é atualmente suportada. <!-- 1353704 --> 



## <a name="windows-10-adk"></a>Windows 10 ADK
Quando implementar sistemas operativos com o Configuration Manager, o [Windows ADK é uma dependências externas](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment) que é necessário.

A tabela seguinte lista as versões do Windows 10 ADK que pode utilizar com diferentes versões do Configuration Manager.

| Versão do Windows 10 ADK  | 1706 o Configuration Manager | 1710 o Configuration Manager | 1802 o Configuration Manager   |
|--------------------|-----|-----|-----|
| 1703  | ![Suportado](media/green_check.png) | ![Retrocompatíveis com o](media/blue_compat.png) | ![Retrocompatíveis com o](media/blue_compat.png) |
| 1709  | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) |
| 1803  | ![Não suportado](media/Red_X.png)   | ![Não suportado](media/Red_X.png) | ![Suportado](media/green_check.png) |

|Chave|
|--|
| ![Suportado](media/green_check.png) = **suportados** <br/> Windows recomenda utilizar o Windows ADK que corresponde à versão do Windows estiver a implementar. Por exemplo, utilizar o Windows ADK para Windows 10 versão 1703 quando implementar o Windows 10 versão 1703. Para obter mais informações sobre o suporte de componentes do Windows ADK, consulte [DISM plataformas suportadas](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms) e [requisitos USMT](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1). |
| ![Retrocompatível](media/blue_compat.png)  = **retrocompatível** <br/> Esta combinação não é testada, mas deve funcionar. Iremos irá Documente quaisquer problemas conhecidos ou avisos. |
| ![Não suportado](media/Red_X.png) = **não suportado** |

 > [!Note]  
 > O Configuration Manager só suporta x86 e amd64 componentes do Windows 10 ADK. Não suporta atualmente ARM ou ARM64 componentes. 