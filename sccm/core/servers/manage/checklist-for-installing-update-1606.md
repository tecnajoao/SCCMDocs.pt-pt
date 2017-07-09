---
title: "Lista de verificação para 1606 | Microsoft Docs"
description: "Saiba mais sobre as ações a serem tomadas antes da atualização do System Center Configuration Manager versão 1511 ou 1602 para a versão 1606."
ms.custom: na
ms.date: 6/6/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 75652cd2-a95a-46c5-91c1-6d43fc8e787e
caps.latest.revision: 7
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 3619a73d3a39659de927e1711a7ec81de9918064
ms.openlocfilehash: a6bda116499845fedff0126e2890755931de85bb
ms.contentlocale: pt-pt
ms.lasthandoff: 06/13/2017

---
# <a name="checklist-for-installing-update-1606-for-system-center-configuration-manager"></a>Lista de verificação para instalar a atualização 1606 para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

A versão 1606 de ramificação atual do System Center Configuration Manager é uma atualização que você pode usar para atualizar da versão 1511 ou da 1602.

Antes de instalar a versão 1606 como uma atualização, revise as seguintes informações e lista de verificação de ações a serem tomadas antes de iniciar a atualização.

Para obter informações sobre as versões de linha de base, consulte [versões de linha de base e atualização](../../../core/servers/manage/updates.md#bkmk_Baselines) na [atualizações para o System Center Configuration Manager](../../../core/servers/manage/updates.md).

 ## <a name="about-installing-update-1606"></a>Sobre como instalar a atualização 1606

Como um *atualizar*, 1606 só pode ser instalado no site de nível superior da sua hierarquia. Isso significa que você inicia a instalação de seu site de administração central se você tiver um, ou de seu site primário autônomo.  

-   Os sites primários filho instalam a atualização automaticamente após a conclusão da instalação da atualização do site de administração central. Você pode usar as janelas de serviço para controlar quando um site instala atualizações. Antes da versão 1606, janelas de serviço foram chamadas de janelas de manutenção. Para obter mais informações, consulte [serviço windows para servidores do site](/sccm/core/servers/manage/service-windows).  

-   Você deve atualizar manualmente os sites secundários de dentro do console do Configuration Manager após a conclusão da instalação da atualização do site pai primário. A atualização automática dos servidores de site secundários não é suportada.  

Quando o servidor do site instala a atualização, as funções de sistema de site que estão instaladas no servidor do site e aquelas que são instalados em computadores remotos são atualizadas automaticamente. Portanto, antes de instalar a atualização, verifique se cada servidor do sistema de sites atende algum dos novos pré-requisitos para operações com a nova versão de atualização.  

Na primeira vez que você usar um console do Configuration Manager após a atualização foi instalada, você será solicitado a atualização desse console.  Para fazer isso, você deve executar a instalação do Configuration Manager no computador que hospeda o console e, em seguida, escolha a opção para atualizar o console. Recomendamos que não adie a instalação da atualização na consola.

 **Problemas conhecidos desta atualização**   
  Os problemas a seguir se aplicam quando você exibir o status de instalação do pacote de atualização:
  - Ao atualizar da versão 1602 a 1606, a etapa **carga do pacote de atualização de extração** exibe um Status de **não iniciado**, mesmo que o download estiver concluído.
  - Ao atualizar da versão 1511 para 1606, algumas etapas mostrará um status de **concluído** , mas não exibirá um valor para **hora da última atualização**.


## <a name="checklist"></a>Lista de verificação  

 **Certifique-se de que todos os sites executem uma versão com suporte do System Center Configuration Manager:**  Antes de iniciar a instalação da atualização 1606, cada servidor do site na hierarquia deve executar a mesma versão do System Center Configuration Manager: a versão 1511 ou da 1602.

 **Revisão instalou versões do Microsoft.NET nos servidores de sistema de site:** Quando um site instala a atualização 1606, Configuration Manager instala automaticamente o .NET Framework 4.5.2 em cada computador que hospeda uma das seguintes funções do sistema de site (se o .NET Framework 4.5 ou posterior já não estiver instalado):  

-   Ponto proxy de registo  

-   Ponto de inscrição  

-   Ponto de gestão  

-   Ponto de ligação de serviço  

Esta instalação pode colocar o servidor do sistema de site em uma reinicialização pendente estado e o relatório de erros para o Visualizador de status de componente do Configuration Manager. Além disso, as aplicações .NET no servidor podem ter falhas aleatórias até que o servidor seja reiniciado.  

 Para obter mais informações, consulte [Site e pré-requisitos de sistema de site](../../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

 **Examine o status do site e hierarquia e verifique se há problemas não resolvidos:** Antes de atualizar um site, resolva todos os problemas operacionais do servidor do site, o servidor de banco de dados do site e funções do sistema de site que são instaladas em computadores remotos. Uma atualização de site pode falhar devido a problemas operacionais existentes.

 Para obter mais informações, veja [Utilizar alertas e o sistema de estado para o System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

 **Examine o arquivo e dados de replicação entre sites:**  Verifique se esse arquivo e replicação de banco de dados entre sites esteja funcionando e atualizada. Atrasos ou listas de pendências em qualquer um podem impedir uma atualização simples e bem-sucedida.    

Para a replicação de base de dados, pode utilizar o Analisador de Ligações de Replicação para ajudar a resolver problemas antes de iniciar a atualização. Para obter mais informações, consulte [sobre o Replication Link Analyzer](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_RLA) no tópico [monitorar replicação de infraestrutura de hierarquia e no System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md).  

 **Instale todas as atualizações críticas aplicáveis para sistemas operacionais em computadores que hospedam o site, o servidor de banco de dados do site e funções do sistema de site remoto:** Antes de instalar uma atualização para o Configuration Manager, instale todas as atualizações críticas para cada sistema de site aplicável. Se uma atualização que instalar necessitar de um reinício, reinicie os computadores aplicáveis antes de iniciar a atualização.  

 **Desabilite as réplicas de banco de dados para pontos de gerenciamento em sites primários:** Do Configuration Manager não pode atualizar um site primário que tenha uma réplica de banco de dados para pontos de gerenciamento habilitado com êxito. Desabilite a replicação de banco de dados antes de instalar uma atualização para o Configuration Manager.  

Para obter mais informações, consulte [Database replicas para pontos de gerenciamento do System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

 **Definir grupos de disponibilidade do AlwaysOn do SQL Server para failover manual:**  
 Antes de instalar atualizações, como versão 1606, certifique-se de que o grupo de disponibilidade é definido como failover manual. Depois que o site tiver sido atualizado, você pode restaurar o failover para automático. Para obter mais informações, consulte [AlwaysOn do SQL Server para um banco de dados do site](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

 **Reconfigure pontos de atualização de software que usam NLBs:** Configuration Manager não pode atualizar um site que usa um cluster de balanceamento de carga de rede (NLB) para hospedar pontos de atualização de software.  

Se você usar clusters NLB para pontos de atualização de software, use o Windows PowerShell para remover do cluster NLB.    

 Para obter mais informações, veja [Planear atualizações de software no System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).  

 **Desabilite todas as tarefas de manutenção de site em cada site durante a instalação da atualização do site:** Antes de instalar a atualização, desabilite as tarefas de manutenção de site que possam ser executadas durante o tempo que o processo de atualização está ativo. Estas incluem as seguintes, entre outras:  

-   Servidor do Site de Reserva  

-   Eliminar Operações de Cliente Desatualizadas  

-   Eliminar Dados de Deteção Desatualizados  

Quando uma tarefa de manutenção da base de dados do site é executada durante a instalação da atualização, a instalação da atualização pode falhar. Antes de desabilitar uma tarefa, registre o agendamento da tarefa para que você possa restaurar sua configuração após a atualização foi instalada.  

Para obter mais informações, consulte [tarefas de manutenção para o System Center Configuration Manager](../../../core/servers/manage/maintenance-tasks.md) e [tarefas de referência para a manutenção do System Center Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md).  

 **Crie um backup do banco de dados do site no site de administração central e sites primários:** Antes de atualizar um site, faça backup do banco de dados do site para garantir que você tenha um backup bem-sucedido a ser usado para recuperação de desastres.   

Para obter mais informações, consulte [Backup e recuperação para o System Center Configuration Manager](../../../protect/understand/backup-and-recovery.md).  

<!-- Removed from update guidance 6/6/2017
 **Test the database upgrade on a copy of the most recent site database backup:** Before you update a System Center Configuration Manager central administration site or primary site, test the site database upgrade process on a copy of the site database.  

-   You should test the site database upgrade process because when you upgrade a site, the site database might be modified.  

-   Although a test database upgrade is not required, it can identify problems for the upgrade before your production database is affected.  

-   A failed site database upgrade can render your site database inoperable and might require a site recovery to restore functionality.  

-   Although the site database is shared between sites in a hierarchy, plan to test the database at each applicable site before you upgrade that site.  

-   If you use database replicas for management points at a primary site, disable replication before you create the backup of the site database.  

Configuration Manager does not support the backup of secondary sites nor does it support the test upgrade of a secondary site database.   

Do not run a test database upgrade on the production site database. Doing so updates the site database and could render your site inoperable. For more information, For more information, see [Step 2: Test the database upgrade before installing an update](/sccm/core/servers/manage/install-in-console-updates#bkmk_step2) from **Before you install an in-console update**.
-->

 **Plano piloto do cliente:** Quando você instala uma atualização que atualiza o cliente, você pode testar essa nova atualização do cliente na pré-produção antes que implanta e atualiza todos os seus clientes ativos.   

 Para aproveitar essa opção, antes de iniciar a instalação da atualização, você deve configurar seu site para dar suporte a atualizações automáticas para pré-produção. Para obter mais informações, veja [Atualização dos clientes no System Center Configuration Manager](../../../core/clients/manage/upgrade/upgrade-clients.md) e   
[Como testar atualizações do cliente em uma coleção de pré-produção no System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

 **Planeje usar as janelas de serviço para controlar quando os servidores do site instalam as atualizações:** Você pode usar janelas de serviço para definir um período durante o qual as atualizações para um servidor do site podem ser instaladas.

Isto pode ajudar a controlar quando os sites na hierarquia instalam a atualização.
Antes da versão 1606, janelas de serviço foram chamadas de janelas de manutenção. Para obter mais informações, consulte [serviço windows para servidores do site](/sccm/core/servers/manage/service-windows).  

 **Execute o verificador de pré-requisitos de instalação:**  Antes de instalar a atualização 1606, você pode executar o verificador de pré-requisitos independentemente da instalação de atualização. Quando você instala a atualização no site, o verificador de pré-requisitos é executado novamente.  

Para obter mais informações, consulte **etapa 3: Executar o verificador de pré-requisitos antes de instalar uma atualização** no [atualizações para o System Center Configuration Manager](../../../core/servers/manage/install-in-console-updates.md) tópico.  

> [!IMPORTANT]  
>  Quando o verificador de pré-requisitos é executado independentemente ou como parte de uma instalação de atualização, o processo atualiza alguns arquivos de origem do produto que são usados para tarefas de manutenção do site. Portanto, depois de executar o verificador de pré-requisitos mas antes de instalar a atualização 1606, se você precisar executar uma tarefa de manutenção do site, execute **Setupwpf.exe** (instalação do Configuration Manager) do CD. Pasta mais recente no servidor do site.  

 **Sites de atualização:** Agora você está pronto para iniciar a instalação da atualização para sua hierarquia.  
  É recomendável que você planeje a instalação da atualização fora do horário comercial normal de cada site, quando o processo de instalação da atualização e suas ações de reinstalação dos componentes de site e funções do sistema de site terão um efeito mínimo sobre as operações de negócios.

Para obter mais informações, veja [Atualizações para o System Center Configuration Manager](../../../core/servers/manage/updates.md).  

