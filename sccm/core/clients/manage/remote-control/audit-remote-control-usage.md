---
title: Auditar a utilização do controlo remoto
titleSuffix: Configuration Manager
description: Auditar utilização de controlo remoto no System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 5c975e69-0cc0-4afd-b7fb-b7182162a933
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d7c24692b88571e56c877c8529fe84b7441c6696
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56127648"
---
# <a name="how-to-audit-remote-control-usage-in-system-center-configuration-manager"></a>Como a auditoria da utilização de controlo remoto no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode utilizar relatórios do System Center Configuration Manager para ver informações de auditoria do controlo remoto.  

 Para obter mais informações sobre como configurar relatórios no Configuration Manager, consulte [relatórios no System Center Configuration Manager](../../../../core/servers/manage/reporting.md).  

 Os dois relatórios seguintes estão disponíveis com a categoria **Mensagens de Estado – Auditoria**:  

-   **Controlo remoto - todos os computadores controlados remotamente por um utilizador específico** -apresenta um resumo da atividade de controlo remoto iniciada por um utilizador específico.  

-   **Controlo remoto - todas as informações de controlo remoto** -mostra um resumo das mensagens de estado sobre o controlo remoto dos computadores cliente.  

### <a name="to-run-the-report-remote-control---all-computers-remote-controlled-by-a-specific-user"></a>Para executar o relatório controlo remoto - todos os computadores controlados remotamente por um utilizador específico  

1.  Na consola do Configuration Manager, clique em **monitorização**.  

2.  Na área de trabalho **Monitorização** , expanda **Comunicar**e clique em **Relatórios**.  

3.  No nó **Relatórios** , clique na coluna **Categoria** para ordenar os relatórios de modo a que possa encontrá-los mais facilmente na categoria **Mensagens de Estado – Auditoria**.  

4.  Selecione o relatório **Controlo Remoto - Todos os computadores controlados remotamente por um utilizador específico**e, em seguida, no separador **Início** , em **Grupo de Relatórios**, clique em **Executar**.  

5.  Na lista **Nome de Utilizador** de **Controlo Remoto - Todos os computadores controlados remotamente por um utilizador específico**, especifique o utilizador para o qual pretende reportar as informações de auditoria e, em seguida, clique em **Ver Relatório**.  

6.  Quando terminar de visualizar os dados no relatório, feche a janela do relatório.  

### <a name="to-run-the-report-remote-control---all-remote-control-information"></a>Para executar o relatório controlo remoto - todas as informações de controlo remoto  

1.  Na consola do Configuration Manager, clique em **monitorização**.  

2.  Na área de trabalho **Monitorização** , expanda **Comunicar**e clique em **Relatórios**.  

3.  No nó **Relatórios** , clique na coluna **Categoria** para ordenar os relatórios de modo a que possa encontrá-los mais facilmente na categoria **Mensagens de Estado – Auditoria**.  

4.  Selecione o relatório **Controlo Remoto - Todas as informações de controlo remoto**e, em seguida, no separador **Início** , em **Grupo de Relatórios**, clique em **Executar** para abrir a janela **Controlo Remoto - Todas as informações de controlo remoto** .  

5.  Quando terminar de visualizar os dados no relatório, feche a janela do relatório.  
