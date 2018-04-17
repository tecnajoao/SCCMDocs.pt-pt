---
title: Funcionalidades de pré-lançamento
titleSuffix: Configuration Manager
description: Funcionalidades de pré-lançamento são funcionalidades que estão no ramo atual para um teste antecipado num ambiente de produção.
ms.custom: na
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
caps.latest.revision: 36
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6e3a6a8dd437238a9dd08b07494b51333283f41c
ms.sourcegitcommit: fb84bcb31d825f454785e3d9d8be669e00fe2b27
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/16/2018
---
# <a name="pre-release-features-in-system-center-configuration-manager"></a>As funcionalidades de pré-lançamento no System Center Configuration Manager
*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Funcionalidades de pré-lançamento são funcionalidades que estão no ramo atual para um teste antecipado num ambiente de produção. Estas funcionalidades são totalmente suportadas, mas ainda estão em desenvolvimento Active Directory e poderão receber alterações até que mudam fora da categoria da versão de pré-lançamento.

 Antes de poder utilizar as funcionalidades de pré-lançamento, tem de dar consentimento para utilizar as funcionalidades de pré-lançamento da consola do Configuration Manager para poder selecionar e ativar a sua utilização.  

Dar consentimento é uma ação única por hierarquia não pode ser anulada. Depois de dar consentimento, não é possível ativar novas funcionalidades de pré-lançamento incluídas com atualizações. Depois de ativar uma funcionalidade de pré-lançamento, não pode desativá-la.

Para dar consentimento, na consola do aceda a **administração** > **configuração do Site** > **Sites**e, em seguida, escolha **definições de hierarquia**. No **geral** separador, escolha **consentimento para utilizar as funcionalidades de pré-lançamento**.

Quando instala uma atualização que inclui funcionalidades de pré-lançamento, estas funcionalidades são visíveis nas atualizações e manutenção assistente com as funcionalidades regulares incluídas na atualização:
  - **Se a que atribuiu consentimento:** Pode ativar as funcionalidades de pré-lançamento de atualizações e manutenção assistente quando estiver a instalar a atualização. Para fazê-lo, selecione as funcionalidades de pré-lançamento tal como faria com qualquer outra funcionalidade.     

    Opcionalmente, pode aguardar para ativar uma funcionalidade de pré-lançamento mais tarde a partir de **administração** > **atualizações e manutenção** > **funcionalidades** nó da consola. No **funcionalidades** escolher a funcionalidade de nós e, em seguida, escolha **ativar**. Esta opção fica a cinzento até dar consentimento. (Antes da versão 1702, atualizações e manutenção estava **administração** > **serviços em nuvem**.)
  -   **Se não atribuiu consentimento:** Quando estiver a instalar uma atualização, as funcionalidades de pré-lançamento estão visíveis no Assistente de manutenção e as atualizações, mas estão desativadas e não podem ser ativadas. Após a atualização é instalada, pode ver estas funcionalidades no **funcionalidades** nós. No entanto, não é possível ativá-los até depois de que atribuiu consentimento **definições de hierarquia**.


> [!Important]  
> Numa hierarquia multilocal, só pode ativar funcionalidades opcionais ou a versão de pré-lançamento do site de administração central. Este comportamento garante que existem não existem conflitos entre a hierarquia. <!--507197-->  
> Se forneceu consentimento num site primário autónomo e, em seguida, expanda a hierarquia ao instalar um novo site de administração central, tem de dar consentimento novamente no site de administração central.  

 Quando ativa uma funcionalidade de pré-lançamento, o Gestor da hierarquia do Configuration Manager (HMAN) tem de processar a alteração para que essa funcionalidade fica disponível. O processamento da alteração, muitas vezes, é imediato, mas pode demorar até 30 minutos a concluir, consoante o ciclo de processamento de HMAN. Após a alteração é processada, tem de reiniciar a consola antes de poder visualizar a nova IU relacionados com essa funcionalidade.

**As seguintes funcionalidades de pré-lançamento estão disponíveis:**

 |Funcionalidade          |Adicionado como versão de pré-lançamento | Adicionado como uma funcionalidade completa|  
|------------------|---------------------|---------------------|
|Implementações faseadas<!--1356837-->|[Versão 1802](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence.md)|![Ainda não](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Executar o passo de sequência de tarefas <!-- 1261338 --> |  [Versão 1710](/sccm/osd/understand/task-sequence-steps#child-task-sequence) |[Versão 1802](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#add-child-task-sequences-to-a-task-sequence)|
| Proteção de exploração do Windows Defender <!-- 1355468 --> |  [Versão 1710](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) |[Versão 1802](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy)|
| Avaliação de atestado de estado de funcionamento do dispositivo para as políticas de conformidade de acesso condicional <!-- 1235616 --> |  [Versão 1710](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm) |[Versão 1802](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)|
| Criar e executar scripts do PowerShell a partir da consola do Configuration Manager <!-- 1236459 --> |  [Versão 1706](/sccm/apps/deploy-use/create-deploy-scripts)|[Versão 1802](/sccm/apps/deploy-use/create-deploy-scripts)|
| Gerir atualizações de controladores Microsoft Surface <!-- 1098490 --> |  [Versão 1706](/sccm/sum/get-started/configure-classifications-and-products) | [Versão 1710](/sccm/sum/get-started/configure-classifications-and-products)|
| Gestão de proteção de dispositivos com o Configuration Manager <!-- 1319346 --> |  [Versão 1702](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)|![Ainda não](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Tarefa sequência conteúdo previamente a colocação em cache <!-- 1021244 --> |  [Versão 1702](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content) | [Versão 1710](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content)|
| Verifique a existência de executar ficheiros executáveis antes de instalar uma aplicação <!-- 1284624 --> |   [Versão 1702](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application) |[Versão 1706](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application)|
| Ponto de serviço do armazém de dados <!-- 1277922 --> |  [Versão 1702](/sccm/core/servers/manage/data-warehouse) |[Versão 1706](/sccm/core/servers/manage/data-warehouse)|
| Cache ponto a ponto de distribuição de conteúdo para clientes <!-- 1101436 --> |  [Versão 1610](/sccm/core/plan-design/hierarchy/client-peer-cache) | [Versão 1710](/sccm/core/plan-design/hierarchy/client-peer-cache)|
| Gateway de gestão de nuvem <!-- 1101764 --> |  [Versão 1610](/sccm/core/clients/manage/plan-cloud-management-gateway) |[Versão 1802](/sccm/core/clients/manage/plan-cloud-management-gateway)|
| Conector do Microsoft Operations Management Suite <!-- 1236739 --> | [Versão 1606](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md) |[Versão 1802](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md)|
| Manutenção de uma coleção com suporte para clusters (serviço de um grupo de servidor) <!-- 1081776 --> | [Versão 1602](../../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_ServerGroups)|![Ainda não](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Acesso condicional para PCs geridos pelo System Center Configuration Manager <!--  --> | [Versão 1602](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)     | [Versão 1702](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)                     |
<!--Image used = ![Not yet](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif) -->

> [!Tip]  
> Para obter mais informações sobre as funcionalidades de não-pré-versão que tem de ativar primeiro, consulte [ativar funcionalidades opcionais de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  
> Para obter mais informações sobre as funcionalidades que só estão disponíveis no ramo pré-visualização técnica, consulte [Technical Preview](/sccm/core/get-started/technical-preview).  
