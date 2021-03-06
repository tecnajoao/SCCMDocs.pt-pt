---
title: Funcionalidades de pré-lançamento
titleSuffix: Configuration Manager
description: Funcionalidades de pré-lançamento são recursos que estão no ramo atual para um teste antecipado num ambiente de produção.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e31e56948d30b95c6de4d9640985c4387bbe7058
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56124971"
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
| API do fornecedor de SMS <!--1359052--> | Versão 1810 | ![Ainda não](media/red_x.png) |
| [Sistema de sites HTTP avançado](/sccm/core/plan-design/hierarchy/enhanced-http) <!--1356889,1358228--> | Versão 1806 | Versão 1810 |
| [Aplicações de cliente para dispositivos cogeridos](/sccm/comanage/workloads#client-apps) <!--1357892--> | Versão 1806 | ![Ainda não](media/red_x.png) |
| [Extensões SCAP](/sccm/compliance/plan-design/scap/about-scap) <!--3607889--> | Versão 1806 | ![Ainda não](media/red_x.png) |
| [Gestor de conversão de pacotes](/sccm/apps/pcm/package-conversion-manager) <!--1357861--> | Versão 1806 | Versão 1810 |
| [Suporte para Cisco AnyConnect 4.0.07x e posteriores para iOS](/sccm/mdm/deploy-use/create-vpn-profiles) <!--1357393--> | Versão 1802 | Versão 1802 <br>com a atualização 4163547 |
| [Implementações faseadas](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence) <!--1356837--> | Versão 1802 | Versão 1806 |
| [Executar o passo de sequência de tarefas](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#add-child-task-sequences-to-a-task-sequence) <!--1261338--> |  Versão 1710 | Versão 1802 |
| [O Windows Defender Exploit Guard](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) <!--1355468--> | Versão 1710 | Versão 1802 |
| [Avaliação de atestado de estado de funcionamento de dispositivo para políticas de conformidade de acesso condicional](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm) <!--1235616--> | Versão 1710 | Versão 1802 |
| [Criar e executar scripts do Windows PowerShell](/sccm/apps/deploy-use/create-deploy-scripts) <!--1236459--> | Versão 1706 | Versão 1802 |
| [Gerir atualizações de controladores do Microsoft Surface](/sccm/sum/get-started/configure-classifications-and-products) <!--1098490--> | Versão 1706 | Versão 1710 |
| [Gestão de proteção de dispositivos](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager) <!--1355092 (1319346)--> | Versão 1702 | ![Ainda não](media/red_x.png) |
| [Tarefa sequência conteúdo pré-colocação em cache](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content) <!--1021244--> | Versão 1702 | Versão 1710 |
| [Verifique a existência de executar ficheiros executáveis antes de instalar uma aplicação](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application) <!--1284624--> | Versão 1702 | Versão 1706 |
| [Ponto de serviço do armazém de dados](/sccm/core/servers/manage/data-warehouse) <!--1277922--> | Versão 1702 | Versão 1706 |
| [Cache ponto a ponto de distribuição de conteúdo para clientes](/sccm/core/plan-design/hierarchy/client-peer-cache) <!--1101436--> | Versão 1610 | Versão 1710 |
| [Gateway de gestão na cloud](/sccm/core/clients/manage/plan-cloud-management-gateway) <!--1101764--> | Versão 1610 | Versão 1802 |
| [Conector do Log Analytics do Azure](/sccm/core/clients/manage/sync-data-log-analytics) <!--1236739--> | Versão 1606 | Versão 1802 |
| [Manutenção de uma coleção com reconhecimento de cluster (serviço de um grupo de servidor)](/sccm/core/get-started/capabilities-in-technical-preview-1605#BKMK_ServerGroups) <!--1081776--> | Versão 1602 | ![Ainda não](media/red_x.png) |
| [Acesso condicional para PCs geridos pelo Configuration Manager](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm) <!--  --> | Versão 1602 | Versão 1702 |

<!--Image used = ![Not yet](media/red_x.png) -->

> [!Tip]  
> Para obter mais informações sobre as funcionalidades da versão não pré que tem de ativar primeiro, consulte [ativar funcionalidades opcionais de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  
> 
> Para obter mais informações sobre as funcionalidades que só estão disponíveis no ramo de pré-visualização técnica, veja [Technical Preview](/sccm/core/get-started/technical-preview).  
