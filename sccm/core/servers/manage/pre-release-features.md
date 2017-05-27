---
title: "Pré-lançamento funcionalidades | Documentos do Microsoft"
description: "Funcionalidades de versão de pré-lançamento do System Center Configuration Manager"
ms.custom: na
ms.date: 4/24/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
caps.latest.revision: 36
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 690d03d9c8c49a815bd318df549d7401a855bc5d
ms.openlocfilehash: b12fcb3c372c34ee47306a9b536c3d0c4764b8be
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="pre-release-features-in-system-center-configuration-manager"></a>Funcionalidades de versão de pré-lançamento do System Center Configuration Manager
*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Funcionalidades da versão de pré-lançamento são funcionalidades que estão incluídas no ramo atual para iniciais de teste num ambiente de produção. Estes são totalmente suportadas, mas ainda se encontra na desenvolvimento ativo e poderão receber as alterações até que mudam fora da categoria da versão de pré-lançamento.

 Antes de poder utilizar funcionalidades da versão de pré-lançamento, terá de lhe fornecer consentimento para utilizar funcionalidades de versão de pré-lançamento a partir da consola do Configuration Manager antes de poder selecionar e ativar a utilização.  

Fornecer consentimento é uma ação única por hierarquia não pode ser anulada. Até dar consentimento, não é possível ativar a nova versão de pré-lançamento funcionalidades incluídas com atualizações.

Para dar consentimento, na consola de ir para **administração** > **configuração do Site** > **Sites**e, em seguida, escolha **definições de hierarquia**. No **geral** separador, escolha **consentimento para utilizar funcionalidades da versão de pré-lançamento**.

 > [!NOTE]
 > Se anteriormente tiver ativado as funcionalidades de versão de pré-lançamento do 1602 atualizar, antes de instalar uma versão posterior da atualização, essas funcionalidades permanecem ativadas para utilização, mesmo se não fornecer consentimento para utilizar funcionalidades da versão de pré-lançamento.

Quando instala uma atualização que inclui funcionalidades da versão de pré-lançamento, essas funcionalidades são visíveis no Assistente de manutenção de atualizações e com as funcionalidades regulares incluídas na atualização:
  - **Se lhe tiver fornecido consentimento:** Pode ativar funcionalidades de versão de pré-lançamento do dentro do Assistente de manutenção de atualizações e quando estiver a instalar a atualização. Para fazê-lo, selecione as funcionalidades de pré-lançamento tal como faria com qualquer outra funcionalidade.     

    Opcionalmente, pode aguardar para ativar uma funcionalidade pré-lançamento posteriormente a partir do **administração** > **atualizações e a manutenção** > **funcionalidades** nó da consola. No **funcionalidades** nó escolha a funcionalidade e, em seguida, escolha **ativar**. Esta opção a cinzento até que atribua o consentimento do utilizador. (Antes da versão 1702, atualizações e a manutenção foi em **administração** > **serviços em nuvem**.)
  -   **Se não tiver dado consentimento:** Quando estiver a instalar uma atualização, funcionalidades da versão de pré-lançamento, mas são visíveis no Assistente de manutenção de atualizações e estão a cinzento e não podem ser ativadas. Após a atualização é instalada, pode ver estas funcionalidades, consulte o **funcionalidades** nó, mas não é possível ativá-las até depois de ter-lhe consentimento **definições de hierarquia**.

Se deu consentimento num site primário autónomo e, em seguida, expanda a hierarquia através da instalação de um novo site de administração central, terá de lhe fornecer consentimento novamente no site de administração central.

 Quando ativa uma funcionalidade pré-lançamento, o Gestor da hierarquia do Configuration Manager (HMAN) tem de processar a alteração para que essa funcionalidade fica disponível. Processamento da alteração é frequentemente imediato, mas pode demorar até 30 minutos a concluir, dependendo do ciclo de processamento de HMAN. Após a alteração é processada, é necessário reiniciar a consola antes de poder visualizar a nova IU relacionados com essa funcionalidade.

**As seguintes funcionalidades da versão de pré-lançamento estão disponíveis:**

 |Funcionalidade          |Adicionado como versão de pré-lançamento | Adicionado como uma funcionalidade completa|  
|------------------|---------------------|---------------------|
| Gestão de proteção de dispositivos com o Configuration Manager |  [Versão 1702](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)|![Ainda não](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Verifique a existência de ficheiros executáveis a ser executado antes de instalar uma aplicação  |   [Versão 1702](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application) |![Ainda não](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Ponto de serviço do armazém de dados  |  [Versão 1702](/sccm/core/servers/manage/data-warehouse) |![Ainda não](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Cache ponto a ponto de distribuição de conteúdo para clientes |  [Versão 1610](/sccm/core/plan-design/hierarchy/client-peer-cache) |![Ainda não](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Gateway de gestão da nuvem |  [Versão 1610](/sccm/core/clients/manage/plan-cloud-management-gateway) |![Ainda não](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Dashboard de origens de dados do cliente |  [Versão 1610](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard) |![Ainda não](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Conector de conjunto de aplicações de gestão do Microsoft Operations  | [Versão 1606](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md) |![Ainda não](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Manutenção de uma coleção de conhecimento de cluster (serviço de um grupo de servidor)| [Versão 1602](../../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_ServerGroups)|![Ainda não](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
|Acesso condicional para PCs gerido pelo System Center Configuration Manager | [Versão 1602](../../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md)     | [Versão 1702](/sccm/mdm/deploy-use/manage-access-to-services)                     |

