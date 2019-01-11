---
title: Suporte para virtualização
titleSuffix: Configuration Manager
description: Os requisitos para instalar funções de sistema do cliente e o site do Configuration Manager num ambiente de virtualização.
ms.date: 01/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1098e8c5-9676-4c2b-841b-ec88bd04e495
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 792e9e34f67ad0dc2a12df0905578effaf1f79aa
ms.sourcegitcommit: 3f791918c5dd87d8968ae9977d761dd97909398c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/10/2019
ms.locfileid: "54196319"
---
# <a name="support-for-virtualization-environments-with-configuration-manager"></a>Suporte para ambientes de Virtualização com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O Configuration Manager suporta a instalação do cliente e funções de sistema de sites nos sistemas operativos suportados que executar como uma máquina virtual nos ambientes de Virtualização neste artigo. Este suporte existe mesmo quando o anfitrião de máquina virtual (ambiente de Virtualização) não é suportado como um cliente ou servidor do site.  

Por exemplo, utilizar o Microsoft Hyper-V Server 2012 para alojar uma máquina virtual que executa o Windows Server 2012. Pode instalar as funções de sistema de sites ou de cliente na máquina virtual com o Windows Server 2012. Não é possível instalar o cliente do anfitrião a executar o Microsoft Hyper-V Server 2012.  


## <a name="virtualization-environments"></a>Ambientes de Virtualização

- Windows Server de 2019  
- Windows Server 2016 <sup> [observe 1](#bkmk_note1)</sup>  
- Microsoft Hyper-V Server 2016 <sup> [observe 1](#bkmk_note1)</sup>  
- Windows Server 2012 R2  
- Microsoft Hyper-V Server 2012  
- Windows Server 2012  
- Microsoft Hyper-V Server 2008 R2  
- Windows Server 2008 R2  

#### <a name="bkmk_note1"></a> Nota 1: Virtualização aninhada
O Configuration Manager não suporta [virtualização aninhada](https://docs.microsoft.com/windows-server/virtualization/hyper-v/What-s-new-in-Hyper-V-on-Windows#BKMK_nested), que há de novo no Windows Server 2016.


### <a name="virtualization-environment-support"></a>Suporte de ambiente de Virtualização

Cada computador virtual tem dos requisitos de software que utilizaria para um computador físico do Configuration Manager e hardware igual ou superior.  

Para validar que o seu ambiente de Virtualização é suportado para o Configuration Manager, utilize o Server Virtualization Validation Program. Ele inclui um Virtualization Program Support Policy Wizard online. Para obter mais informações, consulte [Windows Server Virtualization Validation Program](https://www.windowsservercatalog.com/svvp.aspx).  

> [!NOTE]  
> O Configuration Manager não suporta o Virtual PC ou Virtual Server sistemas de operativos convidados que são executados em computadores Mac.  

O Configuration Manager não consegue gerir máquinas virtuais que estejam offline. Não é possível atualizar uma imagem de máquina virtual offline nem inventário pode ser coletado com o cliente de Configuration Manager no computador anfitrião.  

Não existem considerações especiais para as máquinas virtuais. Por exemplo, o Configuration Manager não pode determinar se uma atualização tem de ser reaplicado a uma imagem de máquina virtual se a máquina virtual foi parada e reiniciada sem guardar o estado da máquina virtual para que a atualização foi aplicada.  



##  <a name="bkmk_Azure"></a> Máquinas virtuais do Microsoft Azure  

O Configuration Manager pode ser executado em máquinas virtuais no Azure tal como ele é executado no local no seu centro de dados. Utilize o Gestor de configuração com máquinas virtuais do Azure nos seguintes cenários:  

- **Cenário 1**: Execute o Configuration Manager numa máquina virtual do Azure. Usá-lo para gerir clientes em outras máquinas virtuais do Azure.  

- **Cenário 2**: Execute o Configuration Manager numa máquina virtual do Azure. Utilizá-lo para gerir clientes que não estão em execução no Azure.  

- **Cenário 3**: Execute diferentes funções de sistema de sites do Configuration Manager em máquinas virtuais do Azure. Execute outras funções no seu centro de dados no local, corretamente ligado ao Azure.  

Os mesmos requisitos de Configuration Manager para redes, suportadas configurações e os requisitos de hardware que se aplicam a instalá-lo no local também se aplicam à instalação em máquinas virtuais do Azure.  

Para obter mais informações, consulte [Configuration Manager no Azure](/sccm/core/understand/configuration-manager-on-azure).

> [!IMPORTANT]  
> Sites do Configuration Manager e clientes executados em máquinas virtuais do Azure estão sujeitos aos mesmos requisitos de licença que as instalações no local.  
