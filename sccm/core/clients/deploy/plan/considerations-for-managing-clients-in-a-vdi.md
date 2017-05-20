---
title: "Gestão de cliente de infraestrutura de ambiente de trabalho virtual (VDI) | Documentos do Microsoft "
description: Gerir clientes do System Center Configuration Manager numa infraestrutura de ambiente de trabalho virtual (VDI).
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: abd45393-d84e-4583-bc80-74bbb3709577
caps.latest.revision: 7
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 690d03d9c8c49a815bd318df549d7401a855bc5d
ms.openlocfilehash: d73daf6427b8c58d21d579f3b41df513cc3e3b0b
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="considerations-for-managing-system-center-configuration-manager-clients--in-a-virtual-desktop-infrastructure-vdi"></a>Considerações sobre a gestão de clientes do System Center Configuration Manager num Virtual Desktop Infrastructure (VDI)

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager suporta a instalação de cliente do Configuration Manager nos seguintes cenários de infraestrutura de ambiente de trabalho virtual (VDI):  

-   **As máquinas virtuais pessoais** -as máquinas virtuais pessoais são utilizadas geralmente quando pretende certificar-se de que os dados de utilizador e as definições são mantidas na máquina virtual entre sessões.  

-   **Sessões de serviços de ambiente de trabalho remoto** -serviços de ambiente de trabalho remoto permitem a um servidor alojar várias sessões de cliente simultâneas. Os utilizadores podem estabelecer ligação a uma sessão e, em seguida, executar aplicações nesse servidor.  

-   **Máquinas virtuais agrupadas** -máquinas virtuais agrupadas não são mantidas entre sessões. Quando uma sessão é fechada, são eliminadas todos os dados e definições. As máquinas virtuais agrupadas são úteis quando não é possível utilizar os serviços de ambiente de trabalho remoto porque uma aplicação empresarial necessária não funciona no Windows Server que aloja as sessões de cliente.  

 A tabela seguinte lista as considerações para gerir o cliente do Configuration Manager numa infraestrutura de ambiente de trabalho virtual.  

|Tipo de máquina virtual|Considerações|  
|--------------------------|--------------------|  
|Máquinas virtuais pessoais|O Configuration Manager trata as máquinas virtuais pessoais coincidir como um computador físico. O cliente do Configuration Manager pode ser pré-instalado na imagem de máquina virtual ou implementado depois da máquina virtual estar aprovisionada.|  
|Serviços de Ambiente de Trabalho Remoto|O cliente do Configuration Manager não está instalado para sessões individuais de ambiente de trabalho remoto. Em vez disso, o cliente só é instalado uma vez no servidor de serviços de ambiente de trabalho remoto. Todas as funcionalidades do Configuration Manager podem ser utilizadas no servidor de serviços de ambiente de trabalho remoto.|  
|Máquinas virtuais agrupadas|Quando uma máquina virtual agrupada é encerrada, quaisquer alterações que fizer utilizando o Gestor de configuração são perdidas.<br /><br /> Dados devolvidos a partir de funcionalidades do Configuration Manager, tais como inventário de hardware, inventário de software e medição de software podem não ser relevantes para as suas necessidades que a máquina virtual poderá estar operacional apenas por um curto período de tempo. Considere excluir máquinas virtuais agrupadas das tarefas de inventário.|  

 Porque a virtualização suporta a execução de múltiplos clientes do Configuration Manager no mesmo computador físico, muitas operações de cliente têm um atraso aleatório incorporado para ações agendadas, tais como o hardware e análises de inventário de software, antimalware, instalações de software e atualizações de software análises. Este atraso ajuda a distribuir a transferência de dados e de processamento de CPU para um computador que tenha várias máquinas virtuais que executam o cliente do Configuration Manager.  

> [!NOTE]  
>  Com exceção dos clientes Windows Embedded que estão no modo de manutenção, os clientes do Configuration Manager que não estão a ser executados em ambientes virtualizados também utilizam este atraso aleatório. Quando tiver muitos clientes implementados, este comportamento ajuda a evitar picos na largura de banda de rede e reduz os requisitos de processamento de CPU nos sistemas de sites do Configuration Manager, tais como o servidor de site e ponto de gestão. O intervalo de atraso varia de acordo com a capacidade do Configuration Manager.  
>   
>  O atraso de aleatoriedade é desativado por predefinição para atualizações de software necessárias e implementações de aplicações necessárias utilizando a seguinte definição de cliente: **Agente do computador**: **Desativar a aleatoriedade de prazos**.

