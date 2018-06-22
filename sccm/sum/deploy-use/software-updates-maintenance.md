---
title: Manutenção de atualizações de software
titleSuffix: Configuration Manager
description: Para manter as atualizações no Configuration Manager, pode agendar a tarefa de limpeza do WSUS ou pode executá-lo manualmente.
author: aczechowski
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 4b0e2e90-aac7-4d06-a707-512eee6e576c
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 03eabbfcd070bb61b2930fac89a551bbeb111eb4
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32346877"
---
# <a name="software-updates-maintenance"></a>Manutenção de atualizações de software

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode agendar e executar a tarefa de limpeza do WSUS a partir da consola do Configuration Manager ou pode executar manualmente a tarefa de limpeza do WSUS nas propriedades do componente de ponto de atualização de Software. Quando selecionar a opção para executar a tarefa de limpeza do WSUS, será executada na próxima sincronização de atualizações de software. As atualizações do software expirado serão definidas para um estado de recusado no servidor do WSUS e o Agente de Atualizações do Windows em computadores já não irá analisar estas atualizações de software. Por predefinição, a tarefa de limpeza do WSUS é executada a cada 30 dias.  

#### <a name="to-schedule-and-run-the-wsus-cleanup-job"></a>Para agendar e executar a tarefa de limpeza do WSUS  

1.  Na consola do Configuration Manager, navegue até à **administração** > **descrição geral** > **configuração do Site** > **Sites**.  

2.  Clique em **Configurar Componentes do Site** no grupo **Definições** e, em seguida, clique em **Ponto de Atualização de Software** para abrir as Propriedades do Componente do Ponto de Atualização de Software.  

3.  Clique no separador **Regras de Substituição** , selecione **Executar assistente de limpeza de WSUS**e, em seguida, clique em **OK**.
