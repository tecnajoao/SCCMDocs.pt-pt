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
ms.openlocfilehash: ec8989a2e7b71d09198e03f2e263364bebc6b169
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32344165"
---
# <a name="considerations-for-managing-system-center-configuration-manager-clients--in-a-virtual-desktop-infrastructure-vdi"></a>Considerações para gerir clientes do System Center Configuration Manager numa infraestrutura de ambiente de Trabalho Virtual (VDI)

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager suporta a instalação do cliente do Configuration Manager nos seguintes cenários de infraestrutura de ambiente de trabalho virtual (VDI):  

-   **Máquinas virtuais pessoais** -as máquinas virtuais pessoais são utilizadas geralmente quando pretender certificar-se de que os dados de utilizador e as definições são mantidas na máquina virtual entre sessões.  

-   **Sessões de serviços de ambiente de trabalho remoto** -serviços de ambiente de trabalho remoto permite que um servidor alojar várias sessões de cliente simultâneas. Os utilizadores podem ligar a uma sessão e, em seguida, executar aplicações nesse servidor.  

-   **Máquinas virtuais agrupadas** -máquinas virtuais agrupadas não são mantidas entre sessões. Quando uma sessão é fechada, todos os dados e definições são eliminadas. Máquinas virtuais agrupadas são úteis quando os serviços de ambiente de trabalho remoto não é possível utilizar uma aplicação empresarial necessária não é possível executar no Windows Server que aloja as sessões de cliente.  

 A tabela seguinte lista as considerações para gerir o cliente do Configuration Manager numa infraestrutura de ambiente de trabalho virtual.  

|Tipo de máquina virtual|Considerações|  
|--------------------------|--------------------|  
|Máquinas virtuais pessoais|O Configuration Manager trata as máquinas virtuais pessoais de forma idêntica para um computador físico. O cliente do Configuration Manager pode ser pré-instalado na imagem de máquina virtual ou implementado depois da máquina virtual estar aprovisionada.|  
|Serviços de Ambiente de Trabalho Remoto|O cliente do Configuration Manager não está instalado para sessões individuais de ambiente de trabalho remoto. Em vez disso, o cliente só é instalado uma vez no servidor de serviços de ambiente de trabalho remoto. Todas as funcionalidades do Configuration Manager podem ser utilizadas no servidor de serviços de ambiente de trabalho remoto.|  
|Máquinas virtuais agrupadas|Quando uma máquina virtual agrupada é encerrada, quaisquer alterações efetuadas utilizando o Gestor de configuração serão perdidas.<br /><br /> Dados devolvidos pelo funcionalidades do Configuration Manager, tais como inventário de hardware, inventário de software e medição de software podem não ser relevantes para as suas necessidades que a máquina virtual poderá estar operacional apenas por um curto período de tempo. Considere excluir máquinas virtuais agrupadas das tarefas de inventário.|  

 Porque a virtualização suporta vários clientes do Configuration Manager a ser executado no mesmo computador físico, muitas operações de cliente têm um atraso aleatório incorporado para ações agendadas, tais como o hardware e análises de inventário de software, antimalware, instalações de software e atualização de software análises. Este atraso ajuda a distribuir a transferência de dados e processamento de CPU para um computador que disponha de várias máquinas virtuais que executam o cliente do Configuration Manager.  

> [!NOTE]  
>  Com exceção dos clientes Windows Embedded que estão no modo de manutenção, os clientes do Configuration Manager que não estão em execução em ambientes virtualizados também utilizam este atraso aleatório. Quando tiver muitos clientes implementados, este comportamento ajuda a evitar picos na largura de banda de rede e reduz os requisitos de processamento de CPU nos sistemas de sites do Configuration Manager, tais como o servidor de ponto e o site de gestão. O intervalo de atraso varia de acordo com a capacidade do Configuration Manager.  
>   
>  O atraso de aleatoriedade é desativado por predefinição para atualizações de software necessárias e implementações de aplicações necessárias utilizando a seguinte definição de cliente: **Agente do computador**: **Desativar a aleatoriedade de prazos**.
