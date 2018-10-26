---
title: 'Gestão de clientes de infraestrutura de ambiente de trabalho virtual (VDI) '
titleSuffix: Configuration Manager
description: Gerir clientes do System Center Configuration Manager numa infraestrutura de ambiente de trabalho virtual (VDI).
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: abd45393-d84e-4583-bc80-74bbb3709577
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a17bb43d91d26cf10da0e1d3da5d8f6e4a2af2a7
ms.sourcegitcommit: 5b3ff56018cfc6bda9643c9f1bebc575173f61bc
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/25/2018
ms.locfileid: "50083790"
---
# <a name="considerations-for-managing-system-center-configuration-manager-clients--in-a-virtual-desktop-infrastructure-vdi"></a>Considerações sobre a gestão de clientes do System Center Configuration Manager numa infraestrutura de ambiente de Trabalho Virtual (VDI)

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager suporta a instalação do cliente do Configuration Manager nos seguintes cenários de infraestrutura de ambiente de trabalho virtual (VDI):  

-   **Máquinas virtuais pessoais** -máquinas virtuais pessoais geralmente são utilizadas quando deseja certificar-se de que esses dados de utilizador e as definições são mantidas na máquina virtual entre sessões.  

-   **Sessões de serviços de ambiente de trabalho remotos** -serviços de ambiente de trabalho remoto permite que um servidor alojar várias sessões de cliente simultâneas. Os utilizadores podem ligar a uma sessão e, em seguida, executar aplicações nesse servidor.  

-   **Máquinas virtuais agrupadas** -máquinas virtuais agrupadas não são mantidas entre sessões. Quando uma sessão é fechada, todos os dados e definições são eliminadas. Máquinas virtuais agrupadas são úteis quando os serviços de ambiente de trabalho remoto não pode ser utilizados uma vez que uma aplicação empresarial necessária não é possível executar no Windows Server que aloja as sessões de cliente.  

 A tabela seguinte lista as considerações para gerir o cliente do Configuration Manager numa infraestrutura de ambiente de trabalho virtual.  

|Tipo de máquina virtual|Considerações|  
|--------------------------|--------------------|  
|Máquinas virtuais pessoais|O Configuration Manager trata máquinas virtuais pessoais idêntico a um computador físico. O cliente do Configuration Manager pode ser pré-instalado na imagem de máquina virtual ou implementado depois de aprovisionar a máquina virtual.|  
|Serviços de Ambiente de Trabalho Remoto|O cliente do Configuration Manager não está instalado para sessões de ambiente de trabalho remoto individuais. Em vez disso, o cliente só é instalado uma vez no servidor dos serviços de ambiente de trabalho remoto. Todas as funcionalidades do Configuration Manager podem ser utilizadas no servidor dos serviços de ambiente de trabalho remoto.|  
|Máquinas virtuais agrupadas|Quando uma máquina virtual agrupada ser desativada, quaisquer alterações efetuadas utilizando o Gestor de configuração serão perdidas.<br /><br /> Dados retornados de recursos do Configuration Manager, como o inventário de hardware, inventário de software e medição de software podem não ser relevantes para as suas necessidades, a máquina virtual poderá estar operacional apenas por um curto período de tempo. Considere excluir máquinas virtuais agrupadas das tarefas de inventário.|  

 Uma vez que a virtualização suporta a execução de vários clientes do Configuration Manager no mesmo computador físico, muitas operações de cliente tem um atraso aleatório incorporado para ações agendadas, como o hardware e de inventário de software, rastreios antimalware, software as instalações e atualização de software verificações. Este atraso ajuda a distribuir a transferência de dados e processamento de CPU para um computador que tenha várias máquinas virtuais que executam o cliente do Configuration Manager.  

> [!NOTE]  
>  Com exceção dos clientes Windows Embedded que estão no modo de manutenção, os clientes do Configuration Manager que não estão em execução em ambientes virtualizados também utilizam este atraso aleatório. Quando tiver muitos clientes implementados, este comportamento ajuda a evitar picos na largura de banda de rede e reduz os requisitos de processamento da CPU nos sistemas de sites do Configuration Manager, como o servidor de site e ponto de gestão. O intervalo de atraso varia de acordo com a capacidade do Configuration Manager.  
>   
>  O atraso de aleatoriedade é desativado por predefinição para atualizações de software necessárias, utilizando a seguinte definição de cliente: **Agente do computador**: **Desativar a aleatoriedade**.
