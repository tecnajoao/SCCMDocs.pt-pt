---
title: Suporte para virtualização
titleSuffix: Configuration Manager
description: Obter os requisitos para instalar funções de sistema de cliente e o site do System Center Configuration Manager num ambiente de virtualização.
ms.date: 1/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1098e8c5-9676-4c2b-841b-ec88bd04e495
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 374a1643c5ea439a7406bbb1f6b53322caa50871
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="support-for-virtualization-environments-for-system-center-configuration-manager"></a>Suporte para ambientes de Virtualização do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O Configuration Manager suporta a instalação do cliente e funções de sistema de sites nos sistemas operativos suportados que executar como uma máquinas virtuais nos ambientes de Virtualização que são apresentadas neste artigo. Este suporte existe mesmo quando o anfitrião da máquina virtual (ambiente de virtualização) não é suportado como cliente ou servidor do site.  

 Por exemplo, se utilizar o Microsoft Hyper-V Server 2012 para alojar uma máquina virtual que executa o Windows Server 2012, pode instalar as funções do sistema cliente ou um site na máquina virtual (Windows Server 2012), mas não no anfitrião (Microsoft Hyper-V Server 2012).  

|Ambiente de virtualização|  
|--------------------------------|  
|Windows Server 2008 R2|  
|Microsoft Hyper-V Server 2008 R2|  
|Windows Server 2012|  
|Microsoft Hyper-V Server 2012|  
|Windows Server 2012 R2|
|Windows Server 2016 <sup>(consulte *tenha em atenção 1*)</sup>|
|Microsoft Hyper-V Server 2016 <sup>(consulte *tenha em atenção 1*)|
-  *Tenha em atenção 1*: Gestor de configuração não suporta [virtualização aninhada](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/what-s-new-in-hyper-v-on-windows#a-namebkmknestedanested-virtualization-new), que é novo com o Windows Server 2016.


 Cada computador virtual que utiliza tem de cumprir ou exceder os requisitos de software que utilizaria para um computador físico do Configuration Manager e o mesmo hardware.  

 Pode validar que o seu ambiente de Virtualização é suportado para o Configuration Manager, utilizando o Server Virtualization Validation Program e o respetivo Virtualization Program Support Policy Wizard online. Para mais informações sobre o Server Virtualization Validation Program, consulte [Windows Server Virtualization Validation Program](https://www.windowsservercatalog.com/svvp.aspx).  

> [!NOTE]  
>  O Configuration Manager não suporta Virtual PC ou o Virtual Server sistemas de operativos convidados que são executados em computadores Mac.  

O Configuration Manager não consegue gerir máquinas virtuais a menos que estejam online. Não é possível atualizar uma imagem de máquina virtual offline, nem pode ser recolhido inventário, utilizando o cliente do Configuration Manager no computador anfitrião.  

Não existem considerações especiais para as máquinas virtuais. Por exemplo, o Configuration Manager poderá não determinar se uma atualização tem de ser novamente aplicada a uma imagem de máquina virtual se a máquina virtual foi parada e reiniciada sem guardar o estado da máquina virtual para que a atualização foi aplicada.  

##  <a name="bkmk_Azure"></a> Máquinas virtuais do Microsoft Azure  
 O Configuration Manager pode executar em máquinas virtuais no Azure, tal como é executado no local dentro da sua rede empresarial física. Pode utilizar o Gestor de configuração de máquinas virtuais do Azure nos seguintes cenários:  

-   **Cenário 1:** Pode executar o Configuration Manager numa máquina virtual do Azure e utilizá-lo para gerir clientes instalados noutras máquinas virtuais do Azure.  

-   **Cenário 2:** Pode executar o Configuration Manager numa máquina virtual do Azure e utilizá-lo para gerir clientes que não estão em execução no Azure.  

-   **Cenário 3:** Pode executar diferentes funções do sistema de sites do Configuration Manager em máquinas virtuais do Azure enquanto executa outras funções na sua rede empresarial física (com conectividade de rede adequada a comunicações).  

Os mesmos requisitos de System Center Configuration Manager para redes, configurações suportadas e requisitos de hardware aplicáveis à instalação do Configuration Manager no local na sua rede empresarial física também são aplicáveis à instalação em máquinas virtuais do Azure.  

Para obter mais informações, consulte [do Configuration Manager no Azure – perguntas mais frequentes](/sccm/core/understand/configuration-manager-on-azure).

> [!IMPORTANT]  
>  Sites do Configuration Manager e os clientes executados em máquinas virtuais do Azure estão sujeitos aos mesmos requisitos de licença que as instalações no local.  
