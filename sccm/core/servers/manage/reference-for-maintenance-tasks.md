---
title: Referência para tarefas de manutenção
titleSuffix: Configuration Manager
description: Leia os detalhes para cada uma das tarefas de manutenção do site do System Center Configuration Manager e se essas tarefas estão ativadas por predefinição.
ms.date: 3/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 68dc6acd-5848-47a4-b4c1-ffa40e47890b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7b395cc8a19a3aab86f3ad40302673d41afe4885
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56123370"
---
# <a name="reference-for-maintenance-tasks-for-system-center-configuration-manager"></a>Referência das tarefas de manutenção para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este tópico lista os detalhes para cada uma das tarefas de manutenção do site do System Center Configuration Manager e especifica os tipos de site em que a tarefa está disponível. Cada entrada também indica se a tarefa está ativada ou não ativada por predefinição. Para obter informações sobre como planear e configurar sites para executar tarefas de manutenção, consulte [tarefas de manutenção para o System Center Configuration Manager](../../../core/servers/manage/maintenance-tasks.md).  

**Servidor do Site de reserva**: Utilize esta tarefa para preparar a recuperação de dados críticos. Pode criar uma cópia de segurança das suas informações críticas para restaurar um site e a base de dados do Configuration Manager. Para obter mais informações, consulte [cópia de segurança e recuperação para o System Center Configuration Manager](../../../protect/understand/backup-and-recovery.md).  

-   **Site de administração central**: Ativado    
-   **Site primário**: Não ativado    
-   Site secundário: Não disponível  

**Verificar o título da aplicação nas informações de inventário**: Utilize esta tarefa para manter a consistência entre os títulos de software comunicados no inventário de software e os títulos de software no catálogo do Asset Intelligence. Para obter mais informações, veja [Introdução ao Asset Intelligence no System Center Configuration Manager](../../../core/clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

-   **Site de administração central**: Ativado    
-   **Site primário**: Ativado    
-   Site secundário: Não disponível  

**Limpar sinalizador de instalação**: Utilize esta tarefa para remover o sinalizador instalado para clientes que não submeterem um registo de deteção de Heartbeat durante os **Redeteção do cliente** período. O sinalizador instalado impede a instalação de push de cliente automática num computador que pode ter um cliente ativo do Configuration Manager.  

-   Site de administração central: Não disponível    
-   **Site primário**: Não ativado    
-   Site secundário: Não disponível  

**Eliminar dados de pedido de aplicação desatualizados**: Utilize esta tarefa para eliminar pedidos de aplicações desatualizados da base de dados. Para obter mais informações sobre pedidos de aplicação, consulte [criar e implementar uma aplicação com o System Center Configuration Manager](/sccm/apps/get-started/create-and-deploy-an-application).  

-   Site de administração central: Não disponível
-   **Site primário**: Ativado    
-   Site secundário: Não disponível  

**Eliminiar histórico de transferências do cliente**: Utilize esta tarefa para eliminar dados históricos sobre a origem de download usado pelos clientes. Transferir informações de origem são usadas para preencher os [dashboard de origens de dados do cliente](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard).  
-  Site de administração central – não está disponível
-    **Site primário** - ativado
-  Site secundário - não disponível

**Eliminar operações de cliente Desatualizadas**: Utilize esta tarefa para eliminar todos os dados desatualizados de operações de cliente da base de dados do site. Por exemplo, isto inclui dados de notificações de cliente desatualizados ou expirados (tal como pedidos de transferência de política de computador ou utilizador) e do Endpoint Protection (como pedidos feitos por um utilizador administrativo para os clientes executarem uma análise ou transferirem definições atualizadas).

-   **Site de administração central**: Ativado    
-   **Site primário**: Ativado    
-   Site secundário: Não disponível  

**Eliminiar histórico de presença de cliente**: Utilize esta tarefa para eliminar informações de histórico sobre o estado online dos clientes (registado por notificação de cliente) que é anteriores à hora especificada. Para obter mais informações sobre a notificação de clientes, veja [Como monitorizar clientes no System Center Configuration Manager](../../../core/clients/manage/monitor-clients.md).  

-   **Site de administração central**: Ativado   
-   **Site primário**: Ativado    
-   Site secundário: Não disponível  

**Eliminar dados de tráfego do Gateway de gestão de nuvem de antiguidade**: Utilize esta tarefa para eliminar todos os dados desatualizados sobre o tráfego que passa através da [gateway de gestão da nuvem](/sccm/core/clients/manage/plan-cloud-management-gateway) da base de dados do site. Por exemplo, isto inclui dados sobre o número de pedidos, bytes de pedidos total, bytes de resposta total, número de pedidos falhados e o número máximo de pedidos simultâneos.  
- **Site de administração central** - ativado
- **Site primário** - ativado
- Site secundário - não disponível


**Eliminar ficheiros recolhidos desatualizados**: Utilize esta tarefa para eliminar informações Desatualizadas sobre ficheiros recolhidos da base de dados. Esta tarefa também elimina os ficheiros recolhidos da estrutura de pastas do servidor de site no site selecionado. Por predefinição, as cinco cópias mais recentes dos ficheiros recolhidos são armazenadas no servidor do site no **Inboxes\sinv.box\FileCol** diretório. Para obter mais informações, consulte [introdução ao inventário de software no System Center Configuration Manager](/sccm/core/clients/manage/inventory/introduction-to-software-inventory).  

-   Site de administração central: Não disponível    
-   **Site primário**: Ativado    
-   Site secundário: Não disponível  

**Eliminar dados de associação de computadores desatualizados**: Utilize esta tarefa para eliminar dados de associação de computador de implementação de sistemas operativos desatualizados da base de dados. Estas informações são utilizadas como parte da conclusão de restauros do estado de utilizador. Para obter mais informações sobre associações de computadores, veja [Gerir o estado do utilizador no System Center Configuration Manager](../../../osd/get-started/manage-user-state.md).  

-   Site de administração central: Não disponível    
-   **Site primário**: Ativado    
-   Site secundário: Não disponível  

**Eliminar dados de deteção de eliminações desatualizados**: Utilize esta tarefa para eliminar dados desatualizados da base de dados que foram criado pelas vistas de extração. Por predefinição, as vistas de extração estão desativadas. Apenas permite-lhes com o SDK do Configuration Manager. Exceto se as vistas de extração estiverem ativadas, não há dados para esta tarefa eliminar.  

-   **Site de administração central**: Ativado    
-   **Site primário**: Ativado    
-   Site secundário: Não disponível  

**Eliminar registo de eliminação de dispositivo dados desatualizados**: Utilize esta tarefa para eliminar dados desatualizados sobre as ações de apagamento de dispositivo móvel da base de dados. Para obter informações sobre a eliminação de dispositivos móveis, consulte [proteger dados através de eliminação remota, bloqueio ou com o System Center Configuration Manager de reposição do código de acesso](/sccm/mdm/deploy-use/wipe-lock-reset-devices).  

-   Site de administração central: Não disponível    
-   **Site primário**: Ativado    
-   Site secundário: Não disponível  

**Eliminar dispositivos desatualizados geridos pelo conector do Exchange Server**: Utilize esta tarefa para eliminar dados desatualizados sobre dispositivos móveis que são geridos com o conector do Exchange Server. Estes dados são eliminados de acordo com o intervalo configurado para o **ignorar os dispositivos móveis que estejam Inativos durante mais de (dias)** opção a **deteção** separador do conector do Exchange Server Propriedades. Para obter mais informações, veja [Gerir dispositivos móveis com o System Center Configuration Manager e o Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

-   Site de administração central: Não disponível   
-   **Site primário**: Ativado    
-   Site secundário: Não disponível  

**Eliminar dados de deteção desatualizados**: Utilize esta tarefa para eliminar dados de deteção desatualizados da base de dados. Estes dados podem incluir registos resultantes de deteção de heartbeat, deteção de rede e os métodos de deteção de serviços de domínio do Active Directory (sistema, utilizador e grupo). Esta tarefa também irá remover dispositivos desatualizados marcados como desativados. Quando esta tarefa é executada num site, os dados associados a esse site são eliminados e essas alterações são replicadas para outros sites. Para obter informações sobre a Deteção, veja [Executar a deteção no System Center Configuration Manager](../../../core/servers/deploy/configure/run-discovery.md).  

-   Site de administração central: Não disponível    
-   **Site primário**: Ativado    
-   Site secundário: Não disponível  

**Eliminar dados de utilização do ponto de distribuição desatualizados**: Utilize esta tarefa para eliminar da base de dados dados desatualizados de pontos de distribuição que tenham sido armazenados há mais do que um tempo especificado.  

-   **Site de administração central**: Ativado    
-   **Site primário**: Ativado    
-   Site secundário: Não disponível  

**Eliminiar dados de histórico do Estado de funcionamento do Endpoint Protection**: Utilize esta tarefa para eliminar informações de estado Desatualizadas para o Endpoint Protection da base de dados. Para obter mais informações sobre informações de estado do Endpoint Protection, veja [Como monitorizar o Endpoint Protection no System Center Configuration Manager](../../../protect/deploy-use/monitor-endpoint-protection.md).  

-   Site de administração central: Não disponível    
-   **Site primário**: Ativado    
-   Site secundário: Não disponível  

**Eliminar dispositivos inscritos desatualizados**: A partir da atualização para 1602, esta tarefa está desativada por predefinição. Pode utilizar esta tarefa para eliminar da base de dados do site os dados desatualizados sobre dispositivos móveis que ainda não comunicam quaisquer informações ao site há um período de tempo especificado.

Esta tarefa é aplicável a dispositivos inscritos com o Microsoft Intune (híbrido) ou do Configuration Manager no local-gestão de dispositivos móveis. Para obter mais informações, consulte [sistemas operativos suportados por clientes e dispositivos](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices#bkmk_OnpremOS).

-   Site de administração central: Não disponível    
-   **Site primário**: Não ativado    
-   Site secundário: Não disponível  

**Eliminar histórico de inventário desatualizado**: Utilize esta tarefa para eliminar dados de inventário que tenham sido armazenados há mais do que um tempo especificado da base de dados. Para obter informações sobre o histórico de inventário, veja [Como utilizar o Explorador de Recursos para ver o inventário de hardware no System Center Configuration Manager](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).  

-   Site de administração central: Não disponível    
-   **Site primário**: Ativado    
-   Site secundário: Não disponível  

**Eliminar dados de registo desatualizados**: Utilize esta tarefa para eliminar dados de registo desatualizados que são utilizados para resolução de problemas da base de dados. Estes dados não estão relacionado com operações de componente do Configuration Manager.  

> [!IMPORTANT]  
> Por predefinição, esta tarefa é executada diariamente em cada site. Num site de administração central e em sites primários, a tarefa elimina dados com mais de 30 dias. Quando utiliza o SQL Server Express num site secundário, certifique-se de que esta tarefa é executada diariamente e elimina os dados que tenham estado Inativos durante sete dias.  

-   **Site de administração central**: Ativado    
-   **Site primário**: Ativado    
-   **Site secundário**: Ativado  

**Eliminiar histórico de tarefas de notificação**: Utilize esta tarefa para eliminar informações sobre tarefas de notificação de cliente da base de dados do site quando este não tenha sido atualizado por um período de tempo especificado. Para obter mais informações sobre a notificação de cliente, consulte [tarefas de implementação do cliente do System Center Configuration Manager](../../../core/clients/manage/monitor-clients.md).  

-   Site de administração central: Não disponível    
-   **Site primário**: Ativado    
-   Site secundário: Não disponível  

**Eliminar dados de resumo de replicação desatualizados**: Utilize esta tarefa para eliminar dados de resumo de replicação desatualizados da base de dados do site quando este não tenha sido atualizado por um período de tempo especificado. Para obter mais informações, veja a secção [Como monitorizar ligações de replicação de base de dados e o estado de replicação](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) do tópico [Monitorizar a infraestrutura de hierarquia e replicação no System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md).  

-   **Site de administração central**: Ativado    
-   **Site primário**: Ativado    
-   **Site secundário**: Ativado  

**Eliminar código de acesso antigo**: Utilize esta tarefa no site de nível superior da hierarquia para eliminar dados desatualizados de reposição do código de acesso para dispositivos Android e Windows Phone. Repor código de acesso de dados são encriptados, mas incluem o PIN para dispositivos. Por predefinição, esta tarefa está ativada e elimina os dados que é mais antigos que um dia.  

-   **Site de administração central**: Ativado    
-   **Site primário**: Ativado    
-   Site secundário: Não disponível  

**Eliminar dados de controlo de replicação desatualizados**: Utilize esta tarefa para eliminar dados desatualizados sobre a replicação de base de dados entre sites do Configuration Manager da base de dados. Quando alterar a configuração desta tarefa de manutenção, a configuração é aplicada a cada site aplicável da hierarquia. Para obter mais informações, veja a secção [Como monitorizar ligações de replicação de base de dados e o estado de replicação](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) do tópico [Monitorizar a infraestrutura de hierarquia e replicação no System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md).  

-   **Site de administração central**: Ativado    
-   **Site primário**: Ativado    
-   **Site secundário**: Ativado  

**Eliminar dados de medição de Software desatualizados**: Utilize esta tarefa para eliminar dados desatualizados de medição de software que tenham sido armazenados há mais do que um tempo especificado da base de dados. Para obter mais informações, veja [Medição de software no System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

-   Site de administração central: Não disponível    
-   **Site primário**: Ativado    
-   Site secundário: Não disponível  

**Eliminar dados de resumo de medição de Software desatualizados**: Utilize esta tarefa para eliminar dados desatualizados de resumos de medição de software que tenham sido armazenados há mais do que um tempo especificado da base de dados. Para obter mais informações, veja [Medição de software no System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

-   Site de administração central: Não disponível    
-   **Site primário**: Ativado    
-   Site secundário: Não disponível  

**Eliminar mensagens de estado Desatualizadas**: Utilize esta tarefa para eliminar dados de mensagem de estado Desatualizadas de acordo com o configurado nas regras de filtro de estado da base de dados. Para informações, consulte a secção "Monitorizar o estado do sistema do Configuration Manager" no tópico [utilizar alertas e o estado do sistema do System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

-   **Site de administração central**: Ativado    
-   **Site primário**: Ativado    
-   Site secundário: Não disponível  

**Eliminar dados de ameaças desatualizados**: Utilize esta tarefa para eliminar dados de ameaças de Endpoint Protection desatualizados que estejam armazenados há mais do que um tempo especificado da base de dados. Para obter informações sobre o Endpoint Protection, veja [Endpoint Protection no System Center Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).  

-   Site de administração central: Não disponível    
-   **Site primário**: Ativado    
-   Site secundário: Não disponível  

**Eliminar computadores antigos desconhecidos**: Utilize esta tarefa para eliminar informações sobre computadores desconhecidos da base de dados do site quando este não tenha sido atualizado por um período de tempo especificado. Para obter mais informações, veja [Preparar implementações de computadores desconhecidos no System Center Configuration Manager](../../../osd/get-started/prepare-for-unknown-computer-deployments.md).  

-   Site de administração central: Não disponível    
-   **Site primário**: Ativado    
-   Site secundário: Não disponível  

**Eliminar dados de afinidade de dispositivo do utilizador desatualizados**: Utilize esta tarefa para eliminar dados de afinidade dispositivo / utilizador desatualizados da base de dados. Para obter mais informações, veja [Associar utilizadores e dispositivos à afinidade de dispositivo do utilizador no System Center Configuration Manager](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

-   Site de administração central: Não disponível    
-   **Site primário**: Ativado    
-   Site secundário: Não disponível  

**Eliminar expirados MDM registos de pacote de inscrição em massa**: Utilize esta tarefa para eliminar os antigos certificados de inscrição em massa e perfis correspondentes depois do certificado de inscrição expirou. Para obter mais informações, consulte [perfis de certificado](/sccm/protect/deploy-use/create-certificate-profiles).
-   **Site de administrações centrais**: Ativado
-   **Site primário**: Ativado
-   Site secundário: Não disponível

**Eliminar dados de deteção de clientes Inativos**: Utilize esta tarefa para eliminar dados de deteção de clientes Inativos da base de dados. Os clientes são marcados como Inativos quando o cliente está assinalado como obsoleto e por configurações que são efetuadas para o estado do cliente.

Esta tarefa apenas opera em recursos que são clientes do Configuration Manager. É diferente da **eliminar dados de deteção desatualizados** desatualizados de tarefa, o que elimina todos os registos de dados de deteção. Quando esta tarefa é executada num site, remove os dados da base de dados em todos os sites numa hierarquia. Para obter mais informações, veja [Como configurar o estado do cliente no System Center Configuration Manager](../../../core/clients/deploy/configure-client-status.md).  

> [!IMPORTANT]  
> Quando estiver ativada, configure esta tarefa para ser executado num intervalo maior do que o **deteção de Heartbeat** agenda. Isto permite que os clientes ativos enviem um registo de deteção de Heartbeat para marcar o respetivo registo de cliente como ativa para que esta tarefa não eliminá-los.  

-   Site de administração central: Não disponível    
-   **Site primário**: Não ativado    
-   Site secundário: Não disponível  

**Eliminar alertas obsoletos**: Utilize esta tarefa para eliminar alertas expirados que estejam armazenadas há mais do que um tempo especificado da base de dados. Para obter mais informações, veja [Utilizar alertas e o sistema de estado para o System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

-   **Site de administração central**: Ativado    
-   **Site primário**: Ativado    
-   Site secundário: Não disponível  

**Eliminar dados de deteção de cliente obsoletos**: Utilize esta tarefa para eliminar registos de cliente obsoletos da base de dados. Normalmente, um registo que está marcado como obsoleto foi substituído por um registo mais recente para o mesmo cliente. O registo mais recente torna-se o registo atual do cliente. Para obter informações sobre a Deteção, veja [Executar a deteção no System Center Configuration Manager](../../../core/servers/deploy/configure/run-discovery.md).  

> [!IMPORTANT]  
> Quando estiver ativada, configure esta tarefa para ser executado num intervalo maior do que a agenda da deteção de Heartbeat. Isto permite que o cliente envie um registo de Deteção de Heartbeat que define corretamente o estado de obsoleto.  

-   Site de administração central: Não disponível    
-   **Site primário**: Não ativado    
-   Site secundário: Não disponível  

**Eliminar subredes e Sites de deteção de florestas obsoletos**: Utilize esta tarefa para eliminar dados sobre sites, sub-redes e domínios que ainda não foram detetados pelo método de deteção de floresta do Active Directory nos últimos 30 dias do Active Directory. Isto remove os dados de deteção, mas não afeta os limites que são criados a partir destes dados de deteção. Para obter mais informações, veja [Executar a deteção no System Center Configuration Manager](../../../core/servers/deploy/configure/run-discovery.md).  

-   **Site de administração central**: Ativado    
-   **Site primário**: Ativado    
-   Site secundário: Não disponível  

**Eliminar registos de estado de implementação de cliente órfão**: Utilize esta tarefa para limpar periodicamente a tabela que contém informações de estado de implementação do cliente. Esta tarefa irá limpar registos associados a dispositivos obsoletos ou desativados.  
-   **Site de administração central**: Ativado    
-   **Site primário**: Ativado    
-   Site secundário: Não disponível

**Eliminar revisões de aplicações não utilizadas**: Utilize esta tarefa para eliminar revisões de aplicações que não são mais referenciados. Para obter mais informações, veja [Como rever e substituir aplicações no System Center Configuration Manager](../../../apps/deploy-use/revise-and-supersede-applications.md).  

-   Site de administração central: Não disponível    
-   **Site primário**: Ativado    
-   Site secundário: Não disponível  

**Avaliar membros da coleção**: Configurar a avaliação da associação da coleção como um componente do site. Para obter informações sobre componentes do site, veja [Componentes do site para o System Center Configuration Manager](../../../core/servers/deploy/configure/site-components.md).  

-   Site de administração central: Não disponível    
-   **Site primário**: Ativado    
-   Site secundário: Não disponível  

**Monitorizar chaves**: Utilize esta tarefa para monitorizar a integridade das chaves de principal de base de dados do Configuration Manager. Uma chave primária é uma coluna (ou uma combinação de colunas) que identifica uma linha com exclusividade e distingue-lo de qualquer outra linha de uma tabela de base de dados do Microsoft SQL Server.  

-   **Site de administração central**: Ativado    
-   **Site primário**: Ativado    
-   Site secundário: Não disponível  

**Reconstruir índices**: Utilize esta tarefa para reconstruir os índices de base de dados do Configuration Manager. Um índice é uma estrutura de base de dados criada numa tabela de base de dados para acelerar a obtenção de dados. Por exemplo, pesquisar uma coluna indexada é muito mais rapidamente do que a procura de uma coluna que não está indexada.

Para melhorar o desempenho, os índices de base de dados do Configuration Manager com frequência são atualizados para permanecer sincronizado com os dados em constante mudança armazenados na base de dados. Esta tarefa cria índices das colunas da base de dados que sejam pelo menos 50% exclusivas, ignora os índices de colunas com menos de 50% de exclusividade e reconstrói todos os índices existentes que satisfaçam os critérios de exclusividade de dados.  

-   **Site de administração central**: Não ativado    
-   **Site primário**: Não ativado    
-   **Site secundário**: Não ativado  

**Resumir dados de Software instalado**: Utilize esta tarefa para resumir os dados do software instalado a partir de vários registos num único registo geral. Resumo de dados pode comprimir a quantidade de dados que são armazenados na base de dados do Configuration Manager. Para obter mais informações, consulte [introdução ao inventário de software no System Center Configuration Manager](../../clients/manage/inventory/introduction-to-software-inventory.md).  

-   Site de administração central: Não disponível    
-   **Site primário**: Ativado    
-   Site secundário: Não disponível  

**Resumir os dados de utilização do ficheiro de medição de Software**: Utilize esta tarefa para resumir os dados de vários registos de software de medição de utilização de ficheiros num único registo geral. Resumo de dados pode comprimir a quantidade de dados que são armazenados na base de dados do Configuration Manager.

Pode utilizar esta tarefa com o **resumir Software de medição de dados de utilização mensais** tarefa para resumir os dados de medição de software e poupar espaço em disco na base de dados do Configuration Manager. Para obter mais informações, veja [Medição de software no System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

-   Site de administração central: Não disponível    
-   **Site primário**: Ativado    
-   Site secundário: Não disponível  

**Resumir dados de utilização mensais de medição de Software**: Utilize esta tarefa para resumir os dados de vários registos de utilização mensal da medição num único registo geral do software. Resumo de dados pode comprimir a quantidade de dados que são armazenados na base de dados do Configuration Manager.

Pode utilizar esta tarefa com o **resumir o Software de medição os dados de utilização do ficheiro** tarefa para resumir os dados de medição de software e poupar espaço na base de dados do Configuration Manager. Para obter mais informações, veja [Medição de software no System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

-   Site de administração central: Não disponível    
-   **Site primário**: Ativado    
-   Site secundário: Não disponível  

**Atualizar filtragem disponível de aplicações**: Utilize esta tarefa para que o Configuration Manager recalcule o mapeamento de implementações de políticas e de aplicações para recursos em coleções. Ao implementar políticas ou aplicações para uma coleção, o Configuration Manager cria um mapeamento inicial entre os objetos que implementa e os membros da coleção.

Estes mapeamentos são armazenados numa tabela para referência rápida. Quando uma associação de coleções é alterada, estes mapeamentos armazenados são atualizados para refletir essas alterações. No entanto, é possível que estes mapeamentos falhem a sincronização. Por exemplo, se o site não conseguir processar corretamente um ficheiro de notificação, essa alteração poderá não refletir-se numa alteração aos mapeamentos. Esta tarefa atualiza esse mapeamento com base na associação da coleção atual.  

-   Site de administração central: Não disponível    
-   **Site primário**: Ativado    
-   Site secundário: Não disponível  

**Atualizar tabelas de catálogo de aplicações**: Utilize esta tarefa para sincronizar a cache de base de dados de site do catálogo de aplicações com as informações mais recentes do aplicativo. Quando alterar a configuração desta tarefa de manutenção, a configuração é aplicada a todos os sites primários da hierarquia.  

-   Site de administração central: Não disponível    
-   **Site primário**: Ativado    
-   Site secundário: Não disponível  
