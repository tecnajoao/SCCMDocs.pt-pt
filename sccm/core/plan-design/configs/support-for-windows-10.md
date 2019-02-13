---
title: Suporte para Windows 10
titleSuffix: Configuration Manager
description: Saiba mais sobre as versões do Windows 10 que são suportadas como clientes ou para o OSD com o System Center Configuration Manager
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7e09453086d2ce8ff02e566188e5ae4a20228820
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56135944"
---
# <a name="support-for-windows-10-in-configuration-manager"></a>Suporte para Windows 10 no Configuration Manager  

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Saiba mais sobre as versões do Windows 10 que o Configuration Manager suporta, incluindo:
 -  [Windows 10 como um cliente do Configuration Manager](#windows-10-as-a-client)
 -  [A avaliação do Windows e o Deployment Kit (ADK) para Windows 10](#windows-10-adk)

> [!Tip]
> Compilações do Windows Server como um cliente são suportadas o mesmo que a versão associada do Windows 10. Por exemplo, o Windows Server 2016 é a mesma versão de compilação como o Windows 10 LTSB 2016 e Windows Server versão 1803 é a mesma versão de compilação como o Windows 10 versão 1803.
> 
> Para obter mais informações sobre o Windows Server como um sistema de sites, consulte [sistemas operativos suportados para servidores de sistema de sites do Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers#the-server-core-installation-of-windows-server-version-1803).



## <a name="windows-10-as-a-client"></a>Windows 10 como um cliente

O Configuration Manager tenta fornecer suporte como um cliente para cada nova versão do Windows 10 logo que possível após torna-se disponível. Como os produtos têm agendas de desenvolvimento e liberação separadas, o suporte técnico que o Configuration Manager fornece depende de quando cada torna-se disponível.

Uma versão do Configuration Manager cai na matriz após [suporte para essa versão](/sccm/core/servers/manage/current-branch-versions-supported) termina. Da mesma forma, suporte para versões do Windows 10, como o LTSB 2015 de Enterprise ou 1511 cai na matriz quando que foram removidos do suporte.

-   A versão mais recente do current branch do Configuration Manager recebe a segurança e atualizações críticas, o que podem incluir correções para problemas com versões do Windows 10. Quando a Microsoft lança uma nova versão do Configuration Manager current branch, versões anteriores recebem apenas atualizações de segurança. Para obter mais informações, consulte [suporte para versões de ramo atual do Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported).  

    > [!Note]  
    > A melhor forma de manter-se atualizado com o Windows 10 é manter-se atualizado com o Configuration Manager. Para obter mais informações, consulte [Configuration Manager e o Windows como um serviço](/sccm/core/understand/configuration-manager-and-windows-as-service).  

-   Estas informações complementam [sistemas operativos suportados por clientes e dispositivos](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices).  

-   Se usar o Long term servicing branch do Configuration Manager, consulte [configurações suportadas do Long term servicing branch](/sccm/core/understand/supported-configurations-for-ltsb).  

<br/>
A tabela seguinte lista as versões do Windows 10 que pode utilizar como um cliente com versões diferentes do Configuration Manager.

| Versão do Windows 10 | Configuration Manager 1710 | Configuration Manager 1802 | 1806 o Configuration Manager | Configuration Manager 1810 |
|---------------------|-----|-----|-----|-----|
| Enterprise 2015 LTSB <!--10/14/2025-->   | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) |
| Enterprise 2016 LTSB <!--10/13/2026-->   | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) |
| Enterprise LTSC 2019 <!--10/10/2028-->   | ![Não suportado](media/Red_X.png)   | ![Não suportado](media/Red_X.png)   | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) |
| 1607   <!--04/09/2019-->   | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) |
| 1703   <!--10/08/2019-->   | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) |
| 1709   <!--04/14/2020-->   | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) |
| 1803   <!--11/10/2020-->   | ![Não suportado](media/Red_X.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) |
| 1809   <!--04/12/2021?-->   | ![Não suportado](media/Red_X.png) | ![Não suportado](media/Red_X.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) |

<!-- lifecycle reference: https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet -->

> [!Note]  
> Suporte para versões de canal semianual do Windows 10 inclui as seguintes edições: Enterprise, Pro, Education e Pro Education.   

| Chave |
|--|
| ![Suportado](media/green_check.png) = **suportados**  |
| ![Não suportado](media/Red_X.png) = **não suportado** |

 > [!NOTE]  
 > A partir da versão 1802, o Configuration Manager suporta o cliente em dispositivos Windows 10 ARM64. Funcionalidades de gestão de cliente existentes devem trabalhar com esses novos dispositivos. Por exemplo, hardware e inventário de software, atualizações de software e gerenciamento de aplicativos. Implementação do SO não é atualmente suportada. <!-- 1353704 --> 

Para obter mais informações sobre o ciclo de vida do Windows, consulte o [folha de fatos de ciclo de vida do Windows](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)



## <a name="windows-10-adk"></a>Windows 10 ADK

Ao implementar sistemas operativos com o Configuration Manager, o Windows ADK é uma dependência externa necessária. Para obter mais informações, consulte [requisitos de infraestrutura para implementação do SO](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment#windows-adk-for-windows-10).

A tabela seguinte lista as versões do Windows 10 ADK que pode utilizar com diferentes versões do Configuration Manager.

| Versão do Windows 10 ADK  | Configuration Manager 1710 | Configuration Manager 1802 | 1806 o Configuration Manager | Configuration Manager 1810 |
|--------------------|-----|-----|-----|-----|
| 1703  | ![Compatível com versões anteriores](media/blue_compat.png) | ![Compatível com versões anteriores](media/blue_compat.png) | ![Não suportado](media/Red_X.png) | ![Não suportado](media/Red_X.png) |
| 1709  | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Compatível com versões anteriores](media/blue_compat.png) | ![Não suportado](media/Red_X.png)   |
| 1803  | ![Não suportado](media/Red_X.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) | ![Compatível com versões anteriores](media/blue_compat.png) |
| 1809  | ![Não suportado](media/Red_X.png) | ![Não suportado](media/Red_X.png) | ![Suportado](media/green_check.png) | ![Suportado](media/green_check.png) |

|Chave|
|--|
| ![Suportado](media/green_check.png) = **suportados** <br/> A Microsoft recomenda utilizar o Windows ADK que corresponde à versão do Windows estiver a implementar. Por exemplo, utilizar o Windows ADK para Windows 10 versão 1703 ao implantar o Windows 10 versão 1703. Para obter mais informações sobre a capacidade de suporte do Windows ADK componente, consulte [plataformas suportadas do DISM](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms) e [requisitos USMT](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1). |
| ![Compatível com versões anteriores](media/blue_compat.png)  = **compatíveis com versões anteriores** <br/> Esta combinação não é testada, mas deve funcionar. Iremos irá documentar quaisquer problemas conhecidos ou limitações. |
| ![Não suportado](media/Red_X.png) = **não suportado** |

 > [!Note]  
 > O Configuration Manager só suporta x86 e amd64 componentes do Windows 10 ADK. Ele atualmente não suporta componentes ARM ou ARM64. 

> [!Tip]
> Compilações do Windows Server tem o mesmo requisito do Windows ADK que a versão do Windows 10 associado. Por exemplo, o Windows Server 2016 é a mesma versão de compilação como o Windows 10 LTSB 2016.
