---
title: Suporte para Windows 10
titleSuffix: Configuration Manager
description: Saiba mais sobre as versões do Windows 10 que são suportadas como clientes ou para o OSD com o System Center Configuration Manager
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 588eeefc8f383a52150dc91e9837e51a718af33c
ms.sourcegitcommit: be8c0182db9ef55a948269fcbad7c0f34fd871eb
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/23/2018
ms.locfileid: "42755865"
---
# <a name="support-for-windows-10-in-configuration-manager"></a>Suporte para Windows 10 no Configuration Manager  

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Saiba mais sobre as versões do Windows 10 que o Configuration Manager suporta, incluindo:
 -  [Windows 10 como um cliente do Configuration Manager](#windows-10-as-a-client)
 -  [A avaliação do Windows e o Deployment Kit (ADK) para Windows 10](#windows-10-adk)



## <a name="windows-10-as-a-client"></a>Windows 10 como um cliente
O Configuration Manager tenta fornecer suporte como um cliente para cada nova versão do Windows 10 logo que possível após torna-se disponível. Como os produtos têm agendas de desenvolvimento e liberação separadas, o suporte técnico que o Configuration Manager fornece depende de quando cada torna-se disponível.

Por exemplo, uma versão do Configuration Manager cai na matriz após [suporte para essa versão](/sccm/core/servers/manage/current-branch-versions-supported) termina. Da mesma forma, suporte para versões do Windows 10, como o LTSB 2015 de Enterprise ou 1511 cai na matriz quando eles são removidos de suporte. Para obter mais informações, consulte [sistemas operativos preteridos](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-client#deprecated-client-operating-systems).

-   Estas informações complementam [sistemas operativos suportados por clientes e dispositivos](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices).  

-   Se usar o Long term servicing branch do Configuration Manager, consulte [configurações suportadas do Long term servicing branch](/sccm/core/understand/supported-configurations-for-ltsb).  

<br/>
A tabela seguinte lista as versões do Windows 10 que pode utilizar como um cliente com versões diferentes do Configuration Manager.

| Versão do Windows 10 | Gestor de configuração 1706 | Gestor de configuração 1710 | Gestor de configuração 1802 | 1806 o Configuration Manager |
|---------------------|-----|-----|-----|-----|
| Enterprise 2015 LTSB            <!--10/14/2025-->   | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) |
| Enterprise 2016 LTSB            <!--10/13/2026-->   | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) |
| 1607   <br />(*veja edições*)   <!--04+6/10/2018-->   | ![Suportado](media/green_check.png) <sup>1</sup> | ![Suportado](media/green_check.png) <sup>1</sup> | ![Suportado](media/green_check.png) <sup>1</sup> | ![Suportado](media/green_check.png) <sup>1</sup> |
| 1703   <br />(*veja edições*)   <!--10+6/09/2018-->   | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) |
| 1709   <br />(*veja edições*)   <!--04+6/09/2019-->   | ![Compatível com versões anteriores](media/blue_compat.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) |
| 1803   <br />(*veja edições*)   <!--11/12/2019-->   | ![Não suportado](media/Red_X.png) | ![Não suportado](media/Red_X.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) |

<!-- lifecycle reference: https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet -->

**Edições**: Enterprise, Pro, Education, Pro Education   

<sup>1</sup> para obter mais informações, consulte [folha de fatos de ciclo de vida do Windows](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet) e a seção sobre "Extensão de serviço para as edições Enterprise e Education".

| Chave |
|--|
| ![Suportado](media/green_check.png) = **suportados**  |
| ![Compatível com versões anteriores](media/blue_compat.png)  = **compatível com versões anteriores** <br/> Funcionalidades de gestão de cliente existentes devem funcionar com a nova versão do Windows 10. Por exemplo, inventário de hardware, inventário de software e atualizações de software. Iremos irá documentar quaisquer problemas conhecidos ou limitações. <br><br>Esta abordagem dá-lhe a capacidade de implementar e gerir novas versões do Windows agora mesmo com o suporte de compatibilidade de aplicativo e sem a necessidade de uma nova versão de atualização do Configuration Manager. |
| ![Não suportado](media/Red_X.png) = **não suportado** |

 > [!NOTE]  
 > A partir da versão 1802, o Configuration Manager suporta o cliente em dispositivos Windows 10 ARM64. Funcionalidades de gestão de cliente existentes devem trabalhar com esses novos dispositivos. Por exemplo, hardware e inventário de software, atualizações de software e gerenciamento de aplicativos. Implementação do SO não é atualmente suportada. <!-- 1353704 --> 



## <a name="windows-10-adk"></a>Windows 10 ADK
Quando implementar sistemas operativos com o Configuration Manager, o [Windows ADK é uma dependência externa](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment) que é necessário.

A tabela seguinte lista as versões do Windows 10 ADK que pode utilizar com diferentes versões do Configuration Manager.

| Versão do Windows 10 ADK  | Gestor de configuração 1706 | Gestor de configuração 1710 | Gestor de configuração 1802 | 1806 o Configuration Manager |
|--------------------|-----|-----|-----|-----|
| 1703  | ![Suportado](media/green_check.png) | ![Compatível com versões anteriores](media/blue_compat.png) | ![Compatível com versões anteriores](media/blue_compat.png) | ![Não suportado](media/Red_X.png)   |
| 1709  | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Compatível com versões anteriores](media/blue_compat.png) |
| 1803  | ![Não suportado](media/Red_X.png)   | ![Não suportado](media/Red_X.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) |

|Chave|
|--|
| ![Suportado](media/green_check.png) = **suportados** <br/> A Microsoft recomenda utilizar o Windows ADK que corresponde à versão do Windows estiver a implementar. Por exemplo, utilizar o Windows ADK para Windows 10 versão 1703 ao implantar o Windows 10 versão 1703. Para obter mais informações sobre a capacidade de suporte do Windows ADK componente, consulte [plataformas suportadas do DISM](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms) e [requisitos USMT](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1). |
| ![Compatível com versões anteriores](media/blue_compat.png)  = **compatíveis com versões anteriores** <br/> Esta combinação não é testada, mas deve funcionar. Iremos irá documentar quaisquer problemas conhecidos ou limitações. |
| ![Não suportado](media/Red_X.png) = **não suportado** |

 > [!Note]  
 > O Configuration Manager só suporta x86 e amd64 componentes do Windows 10 ADK. Ele atualmente não suporta componentes ARM ou ARM64. 

> [!Tip]
> Suporte da versão ADK para implantação de sistema operacional de servidor: Compilações do Windows Server tem o mesmo requisito de ADK como a versão associada do Windows 10. Por exemplo, o Windows Server 2016 é a mesma versão de compilação como o Windows 10 LTSB 2016.
