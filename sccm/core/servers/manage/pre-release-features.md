---
title: "Recursos de pré-lançamento | Microsoft Docs"
description: "Recursos de pré-lançamento no System Center Configuration Manager"
ms.custom: na
ms.date: 6/13/2017
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
ms.sourcegitcommit: 3619a73d3a39659de927e1711a7ec81de9918064
ms.openlocfilehash: 988f8da0b221f8c0b470e7a0a8ed995356193f98
ms.contentlocale: pt-pt
ms.lasthandoff: 06/13/2017


---
# <a name="pre-release-features-in-system-center-configuration-manager"></a>Recursos de pré-lançamento no System Center Configuration Manager
*Aplica-se a: System Center Configuration Manager (ramificação atual)*

Recursos de pré-lançamento são recursos que estão na ramificação atual para testes iniciais em um ambiente de produção. Esses recursos são totalmente suportados, mas ainda estão em desenvolvimento ativo e poderão receber alterações até que eles mover para fora a categoria de pré-lançamento.

 Antes de usar recursos de pré-lançamento, você deverá dar consentimento para usar recursos de pré-lançamento no console do Configuration Manager antes de selecionar e habilitar seu uso.  

Dar o consentimento é uma ação única por hierarquia não pode ser desfeita. Até você dê consentimento, você não pode habilitar novos recursos de pré-lançamento incluídos com as atualizações. Após ativar o recurso de pré-lançamento, não é possível desativá-lo.

Para dar consentimento, no console, vá para **administração** > **configuração do Site** > **Sites**e, em seguida, escolha **configurações da hierarquia**. Sobre o **geral** guia, escolha **consentir o uso de recursos de pré-lançamento**.

 > [!NOTE]
 > Se você tiver habilitado os recursos de pré-lançamento da atualização 1602 antes de instalar uma versão mais recente de atualização, esses recursos estão habilitados para uso mesmo se você não tenha permissão para usar recursos de pré-lançamento.

Quando você instala uma atualização que inclui recursos de pré-lançamento, esses recursos são visíveis no Assistente de atualizações e manutenção com os recursos regulares incluídos na atualização:
  - **Se você tiver consentido:** Quando você estiver instalando a atualização, você pode habilitar recursos de pré-lançamento no Assistente de atualizações e manutenção. Para fazê-lo, selecione as funcionalidades de pré-lançamento tal como faria com qualquer outra funcionalidade.     

    Opcionalmente, você pode esperar para habilitar um recurso de pré-lançamento mais tarde o **administração** > **atualizações e manutenção** > **recursos** nó do console. No **recursos** nó escolha o recurso e, em seguida, escolha **ativar**. Essa opção está esmaecida até você dê consentimento. (Antes da versão 1702, atualizações e manutenção estava sob **administração** > **serviços de nuvem**.)
  -   **Se você não tiver consentido:** Quando você estiver instalando uma atualização, recursos de pré-lançamento, mas são visíveis no Assistente de atualizações e manutenção ficarão esmaecidos e não podem ser habilitados. Após a atualização é instalada, você pode exibir esses recursos no **recursos** nó. No entanto, você não pode habilitá-las até depois que você tiver consentido **configurações da hierarquia**.

Se você forneceu o consentimento a um site primário autônomo e, em seguida, expanda a hierarquia instalando um novo site de administração central, você deverá dar consentimento novamente no site de administração central.

 Quando você habilita o recurso de pré-lançamento, o Gerenciador de hierarquia do Configuration Manager (HMAN) deve processar a alteração antes que esse recurso se torne disponível. Processamento da alteração geralmente é imediato, mas pode levar até 30 minutos para ser concluída, dependendo do ciclo de processamento HMAN. Depois que a alteração é processada, você deve reiniciar o console antes de exibir a nova interface do usuário relacionado a esse recurso.

**Os seguintes recursos de pré-lançamento estão disponíveis:**

 |Funcionalidade          |Adicionado como pré-lançamento | Adicionado como um recurso completo|  
|------------------|---------------------|---------------------|
| Gerenciamento de proteção de dispositivos com o Configuration Manager |  [Versão 1702](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)|![Ainda não](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Verificar para executar arquivos executáveis antes de instalar um aplicativo  |   [Versão 1702](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application) |![Ainda não](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Ponto de serviço do Data Warehouse  |  [Versão 1702](/sccm/core/servers/manage/data-warehouse) |![Ainda não](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Cache de sistemas pares para distribuição de conteúdo para clientes |  [Versão 1610](/sccm/core/plan-design/hierarchy/client-peer-cache) |![Ainda não](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Gateway de gerenciamento de nuvem |  [Versão 1610](/sccm/core/clients/manage/plan-cloud-management-gateway) |![Ainda não](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Painel de fontes de dados do cliente |  [Versão 1610](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard) |![Ainda não](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Conector do Microsoft Operations Management Suite  | [Versão 1606](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md) |![Ainda não](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Manutenção de uma coleção com reconhecimento de cluster (serviço de um grupo de servidores)| [Versão 1602](../../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_ServerGroups)|![Ainda não](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
|Acesso condicional para PCs gerenciados pelo System Center Configuration Manager | [Versão 1602](../../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md)     | [Versão 1702](/sccm/mdm/deploy-use/manage-access-to-services)                     |

