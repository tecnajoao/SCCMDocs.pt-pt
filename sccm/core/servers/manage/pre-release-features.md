---
title: Funcionalidades de pré-lançamento
titleSuffix: Configuration Manager
description: Funcionalidades de pré-lançamento são recursos que estão no ramo atual para um teste antecipado num ambiente de produção.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e72cdf667f96828fb6730cf3294c8d20ec553130
ms.sourcegitcommit: 759098de944b8f7d5eedfc2bae2cb9a6ba15276f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/30/2018
ms.locfileid: "43289259"
---
# <a name="pre-release-features-in-configuration-manager"></a>Funcionalidades de pré-lançamento no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Funcionalidades de pré-lançamento são recursos que estão no ramo atual para um teste antecipado num ambiente de produção. Estas funcionalidades são totalmente suportadas, mas ainda em fase de desenvolvimento. Eles podem receber alterações até que eles mover para fora da categoria da versão de pré-lançamento.



## <a name="give-consent"></a>Dar consentimento  

Antes de utilizar as funcionalidades de pré-lançamento, dar consentimento para utilizar as funcionalidades de pré-lançamento. Dar consentimento é uma ação única por hierarquia que não pode anular. Até dar consentimento, não é possível ativar novas funcionalidades de pré-lançamento incluídas com atualizações. Depois de ativar uma funcionalidade de pré-lançamento, não pode desativá-la.

1. Na consola do Configuration Manager, vá para o **Administration** área de trabalho, expanda **configuração do Site**e selecione o **Sites** nó.  

2. Clique em **definições de hierarquia** na faixa de opções.  

3. Sobre o **gerais** separador das propriedades de definições de hierarquia, ative a opção de **consentimento para utilizar as funcionalidades de pré-lançamento**. Clique em **OK**.  



## <a name="enabling-pre-release-features"></a>Ativar funcionalidades de pré-lançamento

Quando instala uma atualização que inclui funcionalidades de pré-lançamento, essas funcionalidades estão visíveis no Assistente de manutenção de atualizações e com as funcionalidades normais incluídas na atualização.

#### <a name="if-you-have-given-consent"></a>Se tiver dado consentimento
No Assistente de atualizações e manutenção, ative funcionalidades de pré-lançamento. Selecione as funcionalidades de pré-lançamento tal como faria com qualquer outra funcionalidade.     

Opcionalmente, aguardar para ativar funcionalidades de pré-lançamento mais tarde a partir da **funcionalidades** no nó **atualizações e manutenção** no **administração** área de trabalho. Selecione um recurso e, em seguida, clique em **ativar o** na faixa de opções. Até dar consentimento, esta opção não está disponível para utilização.

#### <a name="if-you-havent-given-consent"></a>Se ainda não tiver dado consentimento
No Assistente de atualizações e manutenção, funcionalidades de pré-lançamento estão visíveis, mas não é possível ativá-las. Após a atualização é instalada, estas funcionalidades são visíveis no **funcionalidades** nó. No entanto, não é possível ativá-las até dar consentimento.


> [!Important]  
> Numa hierarquia multilocal, apenas pode ativar funcionalidades opcionais ou de pré-lançamento do site de administração central. Esse comportamento garante que não existam conflitos entre a hierarquia. <!--507197-->  
> 
> Se deu consentimento num site primário autónomo e, em seguida, expanda a hierarquia ao instalar um novo site de administração central, tem de dar consentimento novamente no site de administração central.  

Quando ativa a funcionalidade de pré-lançamento, o Gestor da hierarquia do Configuration Manager (HMAN) têm de processar a alteração para que esse recurso fica disponível. Processamento da alteração, muitas vezes, é imediato. Consoante o HMAN ciclo de processamento, pode demorar até 30 minutos a concluir. Após a alteração é processada, reinicie a consola antes de utilizar a funcionalidade.



## <a name="pre-release-features"></a>Funcionalidades de pré-lançamento

<!--Note/tip for target article

> [!Note]  
> In this version of Configuration Manager, <feature name> is a pre-release feature. To enable it, see [Pre-release features](/sccm/core/servers/manage/pre-release-features).  


> [!Tip]  
> This feature was first introduced in version 1702 as a [pre-release feature](/sccm/core/servers/manage/pre-release-features). Beginning with version 1706, this feature is no longer a pre-release feature.  

-->


| Funcionalidade          | Adicionado como versão de pré-lançamento | Adicionado como todas as funcionalidades |  
|------------------|----------------------|-------------------------|
| Sistema de sites HTTP avançado<!--1356889,1358228-->|Versão 1806|![Ainda não](media/red_x.png)|
| Aplicações móveis para dispositivos cogeridos<!--1357892-->|[Versão 1806](/sccm/core/clients/manage/co-management-switch-workloads#workloads-able-to-be-transitioned-to-intune)|![Ainda não](media/red_x.png)|
| Gestor de conversão de pacotes<!--1357861-->|[Versão 1806](/sccm/apps/pcm/package-conversion-manager)|![Ainda não](media/red_x.png)|
| Suporte para Cisco AnyConnect 4.0.07x e posteriores para iOS<!--1357393-->|[Versão 1802](/sccm/mdm/deploy-use/create-vpn-profiles)| [Versão 1802 com atualização 4163547](/sccm/mdm/deploy-use/create-vpn-profiles) |
| Implementações faseadas<!--1356837-->|[Versão 1802](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)|[Versão 1806](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)|
| Executar o passo de sequência de tarefas <!-- 1261338 --> |  [Versão 1710](/sccm/osd/understand/task-sequence-steps#child-task-sequence) |[Versão 1802](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#add-child-task-sequences-to-a-task-sequence)|
| O Windows Defender Exploit Guard <!-- 1355468 --> |  [Versão 1710](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) |[Versão 1802](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy)|
| Avaliação de atestado de estado de funcionamento do dispositivo para políticas de conformidade de acesso condicional <!-- 1235616 --> |  [Versão 1710](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm) |[Versão 1802](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)|
| Criar e executar scripts do PowerShell a partir da consola do Configuration Manager <!-- 1236459 --> |  [Versão 1706](/sccm/apps/deploy-use/create-deploy-scripts)|[Versão 1802](/sccm/apps/deploy-use/create-deploy-scripts)|
| Gerir atualizações de controladores do Microsoft Surface <!-- 1098490 --> |  [Versão 1706](/sccm/sum/get-started/configure-classifications-and-products) | [Versão 1710](/sccm/sum/get-started/configure-classifications-and-products)|
| Gestão de proteção de dispositivos com o Configuration Manager <!-- 1319346 --> |  [Versão 1702](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)|![Ainda não](media/red_x.png)|
| Tarefa sequência conteúdo pré-colocação em cache <!-- 1021244 --> |  [Versão 1702](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content) | [Versão 1710](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content)|
| Verifique a existência de executar ficheiros executáveis antes de instalar uma aplicação <!-- 1284624 --> |   [Versão 1702](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application) |[Versão 1706](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application)|
| Ponto de serviço do armazém de dados <!-- 1277922 --> |  [Versão 1702](/sccm/core/servers/manage/data-warehouse) |[Versão 1706](/sccm/core/servers/manage/data-warehouse)|
| Cache ponto a ponto de distribuição de conteúdo para clientes <!-- 1101436 --> |  [Versão 1610](/sccm/core/plan-design/hierarchy/client-peer-cache) | [Versão 1710](/sccm/core/plan-design/hierarchy/client-peer-cache)|
| Gateway de gestão na cloud <!-- 1101764 --> |  [Versão 1610](/sccm/core/clients/manage/plan-cloud-management-gateway) |[Versão 1802](/sccm/core/clients/manage/plan-cloud-management-gateway)|
| Conector do Microsoft Operations Management Suite <!-- 1236739 --> | [Versão 1606](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) |[Versão 1802](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite)|
| Manutenção de uma coleção de deteção de cluster (serviço de um grupo de servidor) <!-- 1081776 --> | [Versão 1602](/sccm/core/get-started/capabilities-in-technical-preview-1605#BKMK_ServerGroups)|![Ainda não](media/red_x.png)|
| Acesso condicional para PCs geridos pelo System Center Configuration Manager <!--  --> | [Versão 1602](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)     | [Versão 1702](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)                     |
<!--Image used = ![Not yet](media/red_x.png) -->

> [!Tip]  
> Para obter mais informações sobre as funcionalidades da versão não pré que tem de ativar primeiro, consulte [ativar funcionalidades opcionais de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  
> 
> Para obter mais informações sobre as funcionalidades que só estão disponíveis no ramo de pré-visualização técnica, veja [Technical Preview](/sccm/core/get-started/technical-preview).  
