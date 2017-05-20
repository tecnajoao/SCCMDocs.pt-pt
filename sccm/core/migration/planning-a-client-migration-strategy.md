---
title: "Planear a migração de clientes | Documentos do Microsoft"
description: "Saiba mais sobre as tarefas de migração dos clientes a partir de uma hierarquia de origem para uma hierarquia de destino do System Center Configuration Manager."
ms.custom: na
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2e27b0b7-7bd3-45cd-bc99-9c991606c637
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: ac4576035fda943e38d960dd425d44b7a6ef6a01
ms.openlocfilehash: b52ca4059dfeed08cabf1f75319da40d6499622f
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="plan-a-client-migration-strategy-in-system-center-configuration-manager"></a>Planear uma estratégia de migração de clientes no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Para migrar clientes da hierarquia de origem para uma hierarquia de destino do System Center Configuration Manager, tem de realizar duas tarefas. Tem de migrar os objetos que estão associados ao cliente e, em seguida, tem de reinstalar ou reatribuir os clientes da hierarquia de origem à hierarquia de destino. Deve migrar primeiro os objetos para que estejam disponíveis quando os clientes forem migrados. Os objetos associados ao cliente são migrados utilizando tarefas de migração. Para obter informações sobre como migrar os objetos que estão associados ao cliente, consulte o artigo [planear uma estratégia de tarefa de migração no System Center Configuration Manager](../../core/migration/planning-a-migration-job-strategy.md).  

 Utilize as secções seguintes como auxílio para planear a migração dos clientes para a hierarquia de destino.  

-   [Planear a migração dos clientes para a hierarquia de destino](#Planning_for_Client_Agent_Migration)  

-   [Planear o processamento dos dados mantidos nos clientes durante a migração](#Planning_for_Client_Data_Migration)  

-   [Planear a dados de inventário e compatibilidade durante a migração](#Planning_for_Inventory_data_migration)  

##  <a name="Planning_for_Client_Agent_Migration"></a> Planear a migração dos clientes para a hierarquia de destino  
 Quando migra clientes de uma hierarquia de origem, o software de cliente de atualizações de computador cliente para corresponder à versão do produto da hierarquia de destino.  

-   **Uma hierarquia de origem do Configuration Manager 2007:** Quando migra clientes de uma hierarquia de origem que executa uma versão suportada do Configuration Manager, as atualizações de software de cliente para a versão de cliente da hierarquia de destino.  

-   **Um System Center 2012 Configuration Manager ou posterior hierarquia de origem:** Quando migra clientes entre hierarquias com a mesma versão de produto, o software de cliente não alterar ou atualizar. Em vez disso, o cliente é reatribuído a partir da hierarquia de origem a um site na hierarquia de destino.  

    > [!NOTE]  
    >  Quando a versão de produto de uma hierarquia não for suportada para migração para a hierarquia de destino, atualize todos os sites e clientes da hierarquia de origem para uma versão de produto compatível. Depois da atualização da hierarquia de origem para uma versão de produto suportada, pode migrar entre as hierarquias. Para obter mais informações, consulte o artigo [versões do Configuration Manager que são suportadas para migração](../../core/migration/prerequisites-for-migration.md#BKMK_SupportedMigrationVersions) no [os pré-requisitos da migração no System Center Configuration Manager](../../core/migration/prerequisites-for-migration.md).  

Utilize as informações seguintes para planear a migração de clientes:  

-   Para atualizar ou reatribuir clientes de um site de origem a um site de destino, pode utilizar qualquer método de implementação de clientes que seja suportado para implementar clientes na hierarquia de destino. Os métodos de implementação de clientes típicos incluem a instalação push de cliente, a distribuição de software, a Política de Grupo e a instalação de cliente baseada em atualização de software. Para obter mais informações, consulte o artigo [métodos de instalação de cliente no System Center Configuration Manager](../../core/clients/deploy/plan/client-installation-methods.md).  

-   Certifique-se de que o dispositivo que executa o software de cliente na hierarquia de origem satisfaz os requisitos mínimos de hardware e é executado um sistema operativo que é suportado pela versão do Configuration Manager na hierarquia de destino.  

-   Antes de migrar um cliente, execute uma tarefa de migração para migrar as informações que o cliente irá utilizar na hierarquia de destino.  

-   Os clientes que atualizam mantêm o respetivo histórico de execução de implementações. Isto impede que as implementações forem desnecessárias na hierarquia de destino.  

    -   Para clientes do Configuration Manager 2007, execute o histórico de anúncios são mantidos.  

    -   Para clientes do System Center 2012 Configuration Manager ou System Center Configuration Manager, execute o histórico de implementação é mantida.  

-   Pode migrar os clientes de sites da hierarquia de origem por qualquer ordem à escolha. No entanto, considere migrar um número limitado de clientes em fases, em vez de migrar um grande número de clientes de uma só vez. Uma migração faseada reduz os requisitos de largura de banda da rede e o processamento do servidor quando cada cliente recém-atualizado submeter os respetivos dados de inventário e compatibilidade completos iniciais ao site atribuído.  

-   Quando migra clientes do Configuration Manager 2007, o software de cliente existente é desinstalado do computador cliente e o novo software de cliente é instalado.  

-   O Configuration Manager não é possível migrar um cliente de Configuration Manager 2007 que tenha o cliente de App-V instalado, a menos que a versão de cliente de App-V seja a 4.6 SP1 ou posterior.  

Pode monitorizar o processo de migração de clientes no **migração** nó do **administração** área de trabalho na consola do Configuration Manager.  

Depois de migrar o cliente para a hierarquia de destino, já não pode gerir esse dispositivo utilizando a hierarquia de origem e deverá considerar remover o cliente da hierarquia de origem. Embora isto não seja um requisito quando migra hierarquias, pode ajudar a evitar a identificação de um cliente migrado num relatório da hierarquia de origem ou uma contagem incorreta de recursos entre as duas hierarquias durante a migração. Por exemplo, quando um cliente migrado permanece na base de dados do site de origem, poderá executar um relatório de atualizações de software que identifique incorretamente o computador como um recurso não gerido, quando é agora gerido pela hierarquia de destino.  

##  <a name="Planning_for_Client_Data_Migration"></a> Planear o processamento dos dados mantidos nos clientes durante a migração  
Quando migra um cliente da respetiva hierarquia de origem para a hierarquia de destino, algumas informações são mantidas no dispositivo, enquanto outras deixam de estar disponíveis no dispositivo após a migração.  

As informações seguintes são mantidas no dispositivo cliente:  

-   O identificador exclusivo (GUID), que associa um cliente às respetivas informações na base de dados do Configuration Manager.  

-   O histórico de anúncios ou implementações, que impede que os clientes executem de novo implementações ou anúncios desnecessários na hierarquia de destino.  

As informações seguintes não são mantidas no dispositivo cliente:  

-   Os ficheiros da cache do cliente. Se o cliente necessitar destes ficheiros para instalar software, o cliente transfere-os novamente da hierarquia de destino.  

-   Informações da hierarquia de origem sobre quaisquer anúncios ou implementações que ainda não foram executados. Se pretender que o cliente execute as implementações ou os anúncios após a migração, tem de implementá-los de novo no cliente na hierarquia de destino.  

-   Informações sobre o inventário. O cliente reenviar esta informação para o site atribuído na hierarquia de destino após a migração do cliente e os novos dados de cliente foi gerados.  

-   Dados de compatibilidade. O cliente reenviar esta informação para o site atribuído na hierarquia de destino após a migração do cliente e os novos dados de cliente foi gerados.  

Quando um cliente é migrado, as informações que esteja armazenadas no caminho de ficheiros e registo de cliente do Configuration Manager não são mantidas. Após a migração, volte a aplicar estas definições. As definições típicas incluem as seguintes:  

-   Esquemas de energia  

-   Definições de registo  

-   Definições da política local  

Além disso, poderá ter de reinstalar algumas aplicações.  

##  <a name="Planning_for_Inventory_data_migration"></a> Planear os dados de inventário e de compatibilidade durante a migração  
Os dados de inventário e compatibilidade do cliente não são guardados quando migra um cliente para a hierarquia de destino. Em vez disso, esta informações são recriadas na hierarquia de destino quando um cliente envia pela primeira vez as respetivas informações para o site atribuído. Para ajudar a reduzir os requisitos de largura de banda da rede e o processamento do servidor resultantes, considere migrar um pequeno número de clientes em fases, em vez de um grande número de clientes de uma só vez.  

 Além disso, não é possível migrar personalizações do inventário de hardware a partir de uma hierarquia de origem. Tem de as introduzir na hierarquia de destino, em separado da migração. Para obter informações sobre como expandir o inventário de hardware, consulte o artigo [como configurar inventário de hardware no System Center Configuration Manager](../../core/clients/manage/inventory/configure-hardware-inventory.md).  

