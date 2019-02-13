---
title: Ferramenta de Envio de Agendamento
titleSuffix: Configuration Manager
description: Utilize a ferramenta de agendamento enviar para acionar um agendamento num cliente do Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d5ce547d-3b3b-47d3-bcd7-6ff94692c046
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 38829a249ca87ca87f9c5005ed7ae73e1500e2ab
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56131205"
---
# <a name="send-schedule-tool"></a>Ferramenta de Envio de Agendamento

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

A ferramenta de agendamento de envio é um da [ferramentas do Configuration Manager](/sccm/core/support/tools). Usá-lo para acionar uma agenda num cliente ou a acionar a avaliação de uma linha de base de configuração especificado. Funciona para o computador local ou alvo de um cliente remoto.  

Por exemplo, utilize a ferramenta para acionar uma avaliação de compatibilidade ou agenda de inventário. Se um número de clientes do Configuration Manager recentemente ainda não comunicou o estado de compatibilidade ou de inventário, execute a ferramenta para iniciar o agendamento de necessário em cada cliente.



## <a name="usage"></a>Utilização

Execute **SendSchedule.exe** como administrador. 

`SendSchedule /L [Computer Name]`
`SendSchedule "<Message GUID | DCM UID>" [Computer Name]` 

Depois de acionar uma mensagem (GUID), consulte **SMSClientMethodProvider.log**. Para obter mais informações sobre os GUIDs de mensagem disponíveis, consulte [IDs de mensagem](#bkmk_sendschedule-guids).

Depois de acionar a avaliação de uma linha de base de configuração (DCM UID), consulte **DCMAgent.log**.



## <a name="command-line-options"></a>Opções da linha de comandos


### <a name="option-l"></a>Opção: `/L` 
Liste todos os GUID de mensagem ou UID de DCM disponíveis para o envio. Exiba o nome significativo de mensagens na tabela de dados para cada um deles. Se o nome do computador estiver ausente, ele usa o computador local. Se especificar uma mensagem sem um nome de máquina, em seguida, envia a mensagem para o computador local. 



## <a name="examples"></a>Exemplos

#### <a name="list-the-available-messages-on-the-local-machine"></a>As mensagens disponíveis na máquina local 
`SendSchedule /L` 

#### <a name="list-the-available-messages-on-the-client-mypc"></a>Liste as mensagens disponíveis no cliente MyPC: 
`SendSchedule /L MyPC`

#### <a name="trigger-hardware-inventory-on-the-local-machine"></a>Inventário de hardware de Acionador na máquina local
`SendSchedule {00000000-0000-0000-0000-000000000001}`

#### <a name="trigger-hardware-inventory-on-mypc"></a>Inventário de hardware de Acionador em MyPC: 
`SendSchedule {00000000-0000-0000-0000-000000000001} MyPC` 

#### <a name="trigger-the-evaluation-of-a-specific-configuration-baseline-on-mypc"></a>Acione a avaliação de uma linha de base de configuração específica no MyPC: 
`SendSchedule ScopeId_611E8382-C064-4B62-B0DE-EFFB52AE8994/Baseline_36722778-69dd-4423-9632-b61148b2b67e MyPC` 



## <a name="bkmk_sendschedule-guids"></a> IDs de mensagem

|ID da mensagem  |Nome a Apresentar  |
|---------|---------|
|{00000000-0000-0000-0000-000000000001}|Inventário de hardware|
|{00000000-0000-0000-0000-000000000002}|Inventário de software|
|{00000000-0000-0000-0000-000000000003}|Inventário de deteção|
|{00000000-0000-0000-0000-000000000010}|Recolha de ficheiros|
|{00000000-0000-0000-0000-000000000011}|Recolha IDMIF|
|{00000000-0000-0000-0000-000000000021}|Atribuições de máquina de pedido|
|{00000000-0000-0000-0000-000000000022}|Avaliar as políticas de máquina|
|{00000000-0000-0000-0000-000000000023}|Atualizar a tarefa predefinida de MP|
|{00000000-0000-0000-0000-000000000024}|Tarefa de localizações de atualização de LS (serviço de localização)|
|{00000000-0000-0000-0000-000000000025}|Tarefa de atualização de tempo limite de LS|
|{00000000-0000-0000-0000-000000000026}|Atribuição de pedido de agente de política (utilizador)|
|{00000000-0000-0000-0000-000000000027}|Agente de política avaliar atribuição (utilizador)|
|{00000000-0000-0000-0000-000000000031}|Gerar relatório de utilização de medição de software|
|{00000000-0000-0000-0000-000000000032}|Mensagem de actualização de origem|
|{00000000-0000-0000-0000-000000000037}|Limpar a cache de definições de proxy|
|{00000000-0000-0000-0000-000000000040}|Limpeza de agente de política de computador|
|{00000000-0000-0000-0000-000000000041}|Limpeza de agente de política de utilizador|
|{00000000-0000-0000-0000-000000000042}|Agente de política validar a política de computador / atribuição|
|{00000000-0000-0000-0000-000000000043}|Agente de política validar a política de utilizador / atribuição|
|{00000000-0000-0000-0000-000000000051}|Repetir/atualização certificados no AD no pacote de gestão|
|{00000000-0000-0000-0000-000000000061}|Configurar o peering em relatórios de estado do ponto de distribuição|
|{00000000-0000-0000-0000-000000000062}|Agendamento da verificação de pacote pendente de ponto de distribuição ponto a ponto|
|{00000000-0000-0000-0000-000000000063}|Agenda de instalação de atualizações de soma|
|{00000000-0000-0000-0000-000000000071}|Ação de NAP|
|{00000000-0000-0000-0000-000000000101}|Ciclo de recolha de inventário de hardware|
|{00000000-0000-0000-0000-000000000102}|Ciclo de recolha de inventário de software|
|{00000000-0000-0000-0000-000000000103}|Ciclo de recolha de dados de deteção|
|{00000000-0000-0000-0000-000000000104}|Ciclo de recolha de ficheiros|
|{00000000-0000-0000-0000-000000000105}|Ciclo de recolha IDMIF|
|{00000000-0000-0000-0000-000000000106}|Ciclo de relatório de utilização medição do software|
|{00000000-0000-0000-0000-000000000107}|Ciclo de atualização do lista de origem do Windows Installer|
|{00000000-0000-0000-0000-000000000108}|Software atualizações política ação Software atualizações atribuições ciclo de avaliação|
|{00000000-0000-0000-0000-000000000109}|Tarefa de manutenção de ponto de distribuição de ramificação política manutenção PDP|
|{00000000-0000-0000-0000-000000000110}|Política do DCM|
|{00000000-0000-0000-0000-000000000111}|Enviar mensagem de estado não enviada|
|{00000000-0000-0000-0000-000000000112}|Cleanout de cache de política de sistema de estado|
|{00000000-0000-0000-0000-000000000113}|Atualizar a política de origem|
|{00000000-0000-0000-0000-000000000114}|Política de atualização Store|
|{00000000-0000-0000-0000-000000000115}|Em massa de política de sistema de estado enviar elevada|
|{00000000-0000-0000-0000-000000000116}|Em massa de política de sistema de estado enviar baixa|
|{00000000-0000-0000-0000-000000000120}|Política de verificação de estado AMT|
|{00000000-0000-0000-0000-000000000121}|Ação de política do Gestor de aplicação|
|{00000000-0000-0000-0000-000000000122}|Ação de política de utilizador de Gestor de aplicação|
|{00000000-0000-0000-0000-000000000123}|Ação de avaliação global do Gestor de aplicação|
|{00000000-0000-0000-0000-000000000131}|Summarizer de início de gestão de energia|
|{00000000-0000-0000-0000-000000000221}|Reavaliar de implementação de ponto final|
|{00000000-0000-0000-0000-000000000222}|Reavaliar de política de ponto de extremidade AM|
|{00000000-0000-0000-0000-000000000223}|Deteção de evento externo|



