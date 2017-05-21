---
title: "Suporte para virtualização | Documentos do Microsoft"
description: "Obter os requisitos para instalar funções de sistema de cliente e o site do System Center Configuration Manager num ambiente de virtualização."
ms.custom: na
ms.date: 1/12/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1098e8c5-9676-4c2b-841b-ec88bd04e495
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 10192da2633555ab3bae60dbb1156d1926f9a4a0
ms.openlocfilehash: b49bd179da850cee35b2487a353bb1788df03d58
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="support-for-virtualization-environments-for-system-center-configuration-manager"></a>Suporte para ambientes de virtualização para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O Configuration Manager suporta a instalação do cliente e funções de sistema de sites no suportados sistemas operativos que são executados como um máquinas virtuais nos ambientes de Virtualização que estão listados neste artigo. Este suporte existe mesmo quando o anfitrião da máquina virtual (ambiente de virtualização) não é suportado como cliente ou servidor do site.  

 Por exemplo, se utilizar o Microsoft Hyper-V Server 2012 para alojar uma máquina virtual que executa o Windows Server 2012, pode instalar as funções do sistema cliente ou um site na máquina virtual (Windows Server 2012), mas não no anfitrião (Microsoft Hyper-V Server 2012).  

|Ambiente de virtualização|  
|--------------------------------|  
|Windows Server 2008 R2|  
|Microsoft Hyper-V Server 2008 R2|  
|Windows Server 2012|  
|Microsoft Hyper-V Server 2012|  
|Windows Server 2012 R2|
|Windows Server 2016 <sup>(consulte *1, tenha em atenção*)</sup>|
|Microsoft Hyper-V Server 2016 <sup>(consulte *1, tenha em atenção*)|
-  *Tenha em atenção 1*: O Configuration Manager não suporta [virtualização aninhada](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/what-s-new-in-hyper-v-on-windows#a-namebkmknestedanested-virtualization-new), que é novo no Windows Server 2016.


 Cada computador virtual que utiliza tem de cumprir ou exceder o mesmo hardware e requisitos de software que pretende utilizar para um computador físico do Configuration Manager.  

 Pode validar que o seu ambiente de Virtualização é suportada para o Configuration Manager utilizando o programa de validação do servidor de Virtualização e o respetivo online Assistente de política de suporte do programa de virtualização. Para obter mais informações sobre o programa de validação de Virtualização de servidor, consulte o artigo [programa de validação de Virtualização do Windows Server](https://www.windowsservercatalog.com/svvp.aspx).  

> [!NOTE]  
>  O Configuration Manager não suporta Virtual PC ou o Virtual Server sistemas de operativos convidados que são executados em computadores Mac.  

O Configuration Manager não consegue gerir máquinas virtuais, a menos que estiverem online. Não é possível atualizar uma imagem de máquina virtual offline, nem pode ser recolhido inventário utilizando o cliente do Configuration Manager no computador anfitrião.  

Não existem considerações especiais para as máquinas virtuais. Por exemplo, o Configuration Manager não poderão determinar se uma atualização tem de ser aplicada novamente a uma imagem de máquina virtual se a máquina virtual foi parada e reiniciada sem a guardar o estado da máquina virtual ao qual foi aplicada a atualização.  

##  <a name="bkmk_Azure"></a> Máquinas virtuais do Microsoft Azure  
 O Configuration Manager pode ser executado em máquinas virtuais no Azure tal como este é executado no local na rede da sua empresa físico. Pode utilizar o Configuration Manager com máquinas virtuais do Azure nos seguintes cenários:  

-   **Cenário 1:** Pode executar o Configuration Manager na máquina virtual do Azure e utilizá-lo a gerir os clientes que estão instalados no outras máquinas virtuais do Azure.  

-   **Cenário 2:** Pode executar o Configuration Manager na máquina virtual do Azure e utilizá-la para gerir clientes que não estão em execução no Azure.  

-   **Cenário 3:** Pode executar diferentes funções de sistema de sites do Configuration Manager em máquinas virtuais do Azure ao executar outras funções na sua rede empresarial física (com conectividade de rede adequada para comunicações).  

Os mesmos requisitos de System Center Configuration Manager para redes, configurações suportadas e requisitos de hardware que se aplicam a instalação do Configuration Manager no local na rede da sua empresa físico também se aplicam a instalação de máquinas virtuais do Azure.  

Para obter mais informações, consulte o artigo [Configuration Manager no Azure - perguntas mais frequentes](/sccm/core/understand/configuration-manager-on-azure).

> [!IMPORTANT]  
>  Sites do Configuration Manager e os clientes executados em máquinas virtuais do Azure estão sujeitos os mesmos requisitos de licença que instalações no local.  

