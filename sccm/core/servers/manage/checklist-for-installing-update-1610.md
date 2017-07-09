---
title: "Lista de verificação para 1610 | System Center Configuration Manager"
description: "Saiba mais sobre as ações a serem tomadas antes de atualizar para System Center Configuration Manager versão 1610."
ms.custom: na
ms.date: 6/6/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b411cb0-4fd1-41f2-a2f6-33738a5bde96
caps.latest.revision: 7
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 3619a73d3a39659de927e1711a7ec81de9918064
ms.openlocfilehash: 54b243fd33ed13b8ccde48fa5e2525204455d96c
ms.contentlocale: pt-pt
ms.lasthandoff: 06/13/2017

---
# <a name="checklist-for-installing-update-1610-for-system-center-configuration-manager"></a>Lista de verificação para instalar a atualização 1610 para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

Quando você usa o branch atual do System Center Configuration Manager, você pode instalar a atualização no console para a versão 1610 para atualizar sua hierarquia de versão 1606. Se sua hierarquia executa a versão 1511, 1602 ou 1606, você pode atualizar a versão 1610.

Para obter a atualização de versão 1610, você deve usar uma função do sistema de site do ponto de conexão de serviço no site de nível superior da sua hierarquia. Isso pode estar no modo online ou offline. Depois de sua hierarquia baixa o pacote de atualização da Microsoft, você pode encontrá-lo no console em **administração &gt; visão geral &gt; serviços de nuvem &gt; atualizações e manutenção**.

-   Quando a atualização está listada como **disponível**, a atualização está pronta para instalar. Antes de instalar a versão 1610, examine as informações a seguir [sobre como instalar a atualização 1610](#about-installing-update-1610) e [lista de verificação](#checklist) para configurações a serem feitas antes de iniciar a atualização.

-   Se a atualização exibe como **baixando** e não de alteração, examine o **hman.log** e **dmpdownloader.log** para erros.

    -   Normalmente, você também pode reiniciar o **SMS_Executive** serviço no servidor do site para reiniciar o download de arquivos de redistribuição da atualização.

    -   Outro problema de download comum ocorre quando o servidor proxy evitar downloads do <http://silverlight.dlservice.microsoft.com> e <http://download.microsoft.com>.

Para obter mais informações sobre como instalar atualizações, consulte [atualizações e manutenção no console](/sccm/core/servers/manage/updates#a-namebkmkinconsolea-in-console-updates-and-servicing).

Para obter informações sobre as versões da ramificação atual, consulte [versões de linha de base e atualização](/sccm/core/servers/manage/updates#bkmk_Baselines) na [atualizações para o System Center Configuration Manager](/sccm/core/servers/manage/updates).

## <a name="about-installing-update-1610"></a>Sobre a instalação de atualização 1610

**Sites:**  
Atualização 1610 pode ser instalada somente no site de nível superior da sua hierarquia. Isso significa que você inicia a instalação de seu site de administração central se você tiver um, ou de seu site primário autônomo. Depois que a atualização é instalada no site de nível superior, os sites filho tem o seguinte comportamento de atualização:

-   Os sites primários filho instalam a atualização automaticamente depois que o site de administração central conclui a instalação da atualização. Você pode usar as janelas de serviço para controlar quando um site instala atualizações. Antes da versão 1606, janelas de serviço foram chamadas de janelas de manutenção. Para obter mais informações, consulte [serviço windows para servidores do site](/sccm/core/servers/manage/service-windows).

-   Você deve atualizar manualmente os sites secundários de dentro do console do Configuration Manager depois que o site pai primário conclui a instalação da atualização. A atualização automática dos servidores de site secundários não é suportada.

**Funções do sistema de site:**  
Quando o servidor do site instala a atualização, as funções de sistema de site que estão instaladas no servidor do site e aquelas que são instalados automaticamente em computadores remotos são atualizadas. Portanto antes de instalar a atualização, certifique-se de que cada servidor do sistema de sites atende algum dos novos pré-requisitos para operação com a nova versão de atualização.

**Consoles do Configuration Manager:**   
Na primeira vez que você usar um console do Configuration Manager após a atualização, você será solicitado a atualização desse console. Para fazer isso, você deve executar a instalação do Configuration Manager no computador que hospeda o console e, em seguida, escolha a opção para atualizar o console. Recomendamos que não adie a instalação da atualização na consola.



## <a name="checklist"></a>Lista de verificação

**Certifique-se de que todos os sites executem uma versão com suporte do System Center Configuration Manager:** Antes de iniciar a instalação da atualização 1610, cada site na hierarquia deve estar executando a mesma versão do System Center Configuration Manager: a versão 1511, 1602 ou 1606.

**Examine o status do Software Assurance ou direitos de assinatura equivalente:**   
Você deve ter um contrato de Software Assurance (SA) ativo para instalar a atualização 1610. Quando você instala a versão 1610, você terá a opção **licenciamento** tab para confirmar sua **data de expiração do Software Assurance**.

Este é um valor opcional que você pode especificar como um lembrete conveniente de data de expiração de licença, que fica visível quando você instala as atualizações futuras. Se você instalou o Configuration Manager a partir da mídia de linha de base da versão 1606, você pode ter especificado anteriormente esse valor durante a instalação ou no **licenciamento** guia o **configurações da hierarquia** após a instalação do site.

Para obter mais informações, consulte [licenciamento e ramificações para o System Center Configuration Manager](/sccm/core/understand/learn-more-editions).

**Revisão instaladas versões do Microsoft .NET em servidores de sistema de site:** Quando um site instala a atualização 1610, o Configuration Manager instala automaticamente o .NET Framework 4.5.2 em cada computador que hospeda uma das seguintes funções do sistema de site quando o .NET Framework 4.5 ou posterior ainda não foi instalado:

-   Ponto proxy de registo
-   Ponto de inscrição
-   Ponto de gestão
-   Ponto de ligação de serviço

Esta instalação pode colocar o servidor do sistema de site em uma reinicialização pendente estado e o relatório de erros para o Visualizador de status de componente do Configuration Manager. Além disso, aplicativos .NET no servidor podem apresentar falhas aleatórias até que o servidor seja reiniciado.

Para obter mais informações, veja [Pré-requisitos de site e sistema de sites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).

**Examine o status do site e hierarquia e verifique se há problemas não resolvidos:** Antes de atualizar um site, resolva todos os problemas operacionais do servidor do site, o servidor de banco de dados do site e funções do sistema de site que são instaladas em computadores remotos. Uma atualização de site pode falhar devido a problemas operacionais existentes.

Para obter mais informações, veja [Utilizar alertas e o sistema de estado para o System Center Configuration Manager](/sccm/core/servers/manage/use-alerts-and-the-status-system).

**Examine o arquivo e dados de replicação entre sites:**   
Verifique se esse arquivo e replicação de banco de dados entre sites esteja funcionando e atualizada. Atrasos ou listas de pendências em qualquer um podem impedir uma atualização simples e bem-sucedida.
Para a replicação de base de dados, pode utilizar o Analisador de Ligações de Replicação para ajudar a resolver problemas antes de iniciar a atualização.

Para obter mais informações, consulte [sobre o Replication Link Analyzer](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure#BKMK_RLA) no [monitorar replicação de infraestrutura de hierarquia e no System Center Configuration Manager](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure) tópico.

**Instale todas as atualizações críticas aplicáveis para sistemas operacionais em computadores que hospedam o site, o servidor de banco de dados do site e funções do sistema de site remoto:** Antes de instalar uma atualização para o Configuration Manager, instale todas as atualizações críticas para cada sistema de site aplicável. Se uma atualização que você instala exigir uma reinicialização, reinicie os computadores aplicáveis antes de iniciar a atualização do Configuration Manager.

**Desabilite as réplicas de banco de dados para pontos de gerenciamento em sites primários:**   
Do Configuration Manager não pode atualizar um site primário que tenha uma réplica de banco de dados para pontos de gerenciamento habilitado com êxito. Desabilite a replicação de banco de dados antes de instalar uma atualização para o Configuration Manager.

Para obter mais informações, veja [Réplicas de bases de dados para pontos de gestão do System Center Configuration Manager](/sccm/core/servers/deploy/configure/database-replicas-for-management-points).

**Definir grupos de disponibilidade do AlwaysOn do SQL Server para failover manual:**   
Antes de instalar atualizações, como versão 1610, certifique-se de que o grupo de disponibilidade é definido como failover manual. Depois que o site tiver sido atualizado, você pode restaurar o failover para automático. Para obter mais informações, consulte [AlwaysOn do SQL Server para um banco de dados do site](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).

**Reconfigure pontos de atualização de software que usam NLBs:**   
Configuration Manager não pode atualizar um site que usa um cluster (NLB) para hospedar pontos de atualização de software de balanceamento de carga de rede.

Se você usar clusters NLB para pontos de atualização de software, use o Windows PowerShell para remover do cluster NLB.
Para obter mais informações, veja [Planear atualizações de software no System Center Configuration Manager](/sccm/sum/plan-design/plan-for-software-updates).

**Desabilite todas as tarefas de manutenção de site em cada site durante a instalação da atualização do site:**   
Antes de instalar a atualização, desabilite qualquer tarefa de manutenção de site que possam ser executadas durante o tempo que o processo de atualização está ativo. Estas incluem as seguintes, entre outras:

-   Servidor do Site de Reserva
-   Eliminar Operações de Cliente Desatualizadas
-   Eliminar Dados de Deteção Desatualizados

Quando uma tarefa de manutenção da base de dados do site é executada durante a instalação da atualização, a instalação da atualização pode falhar. Antes de desabilitar uma tarefa, registre o agendamento da tarefa para que você possa restaurar sua configuração após a atualização foi instalada.

Para obter mais informações, consulte [tarefas de manutenção para o System Center Configuration Manager](/sccm/core/servers/manage/maintenance-tasks) e [tarefas de referência para a manutenção do System Center Configuration Manager](/sccm/core/servers/manage/reference-for-maintenance-tasks).

**Crie um backup do banco de dados do site no site de administração central e sites primários:** Antes de atualizar um site, faça backup do banco de dados do site para garantir que você tenha um backup bem-sucedido a ser usado para recuperação de desastres.

Para obter mais informações, consulte [Backup e recuperação para o System Center Configuration Manager](/sccm/protect/understand/backup-and-recovery).

<!-- Removed from update guidance 6/6/2017
**Test the database upgrade on a copy of the most recent site database backup:** 
Before you update a System Center Configuration Manager central administration site or primary site, test the site database upgrade process on a copy of the site database.

-   We recommend that you test the site database upgrade process because when you upgrade a site, the site database might be modified.

-   Although a test database upgrade is not required, it can identify problems for the upgrade before your production database is affected.

-   A failed site database upgrade can render your site database inoperable and might require a site recovery to restore functionality.

-   Although the site database is shared between sites in a hierarchy, plan to test the database at each applicable site before you upgrade that site.

-   If you use database replicas for management points at a primary site, disable replication before you create the backup of the site database.

Configuration Manager does not support the backup of secondary sites nor does it support the test upgrade of a secondary site database.

Do not run a test database upgrade on the production site database. Doing so updates the site database and could render your site inoperable. For more information, see [Step 2: Test the database upgrade before installing an update](/sccm/core/servers/manage/install-in-console-updates#bkmk_step2) from **Before you install an in-console update**.
-->

**Plano piloto do cliente:**   
Quando você instala uma atualização que atualiza o cliente, você pode testar essa nova atualização do cliente na pré-produção antes que implanta e atualiza todos os seus clientes ativos.

Para aproveitar essa opção, você deve configurar seu site para dar suporte a atualizações automáticas para pré-produção antes de iniciar a instalação da atualização.

Para obter mais informações, consulte [atualizar clientes no System Center Configuration Manager](/sccm/core/clients/manage/upgrade/upgrade-clients) e [como testar atualizações do cliente em uma coleção de pré-produção no System Center Configuration Manager](/sccm/core/clients/manage/upgrade/test-client-upgrades).

**Planeje usar as janelas de serviço para controlar quando os servidores do site instalam as atualizações:**   
Você pode usar janelas de serviço para definir um período durante o qual as atualizações para um servidor do site podem ser instaladas.

Isto pode ajudar a controlar quando os sites na hierarquia instalam a atualização. Antes da versão 1606, janelas de serviço foram chamadas de janelas de manutenção. Para obter mais informações, consulte [serviço windows para servidores do site](/sccm/core/servers/manage/service-windows).

**Execute o verificador de pré-requisitos de instalação:**   
Quando a atualização está listada no console como **disponível,** independentemente você pode executar o verificador de pré-requisitos antes de instalar a atualização. (Quando você instala a atualização no site, o verificador de pré-requisitos é executado novamente.)

Para executar uma verificação de pré-requisitos do console, vá para **Administração > Visão geral > Serviços de nuvem > atualizações e manutenção.** Em seguida, clique com botão direito **pacote de atualização do Configuration Manager 1610**e, em seguida, escolha **executar verificação de pré-requisitos**.

Para obter mais informações sobre como iniciar e, em seguida, a verificação de pré-requisitos de monitoramento, consulte **etapa 3: Executar o verificador de pré-requisitos antes de instalar uma atualização** no tópico [instalar atualizações no console do System Center Configuration Manager](/sccm/core/servers/manage/install-in-console-updates).

> [!IMPORTANT]  
> Quando o verificador de pré-requisitos é executado independentemente ou como parte de uma instalação de atualização, o processo atualiza alguns arquivos de origem do produto que são usados para tarefas de manutenção do site. Portanto, depois de executar o verificador de pré-requisitos mas antes de instalar a atualização de 1610, se você precisar executar uma tarefa de manutenção do site, execute **Setupwpf.exe** (instalação do Configuration Manager) do CD. Pasta mais recente no servidor do site.

**Sites de atualização:**   
Agora você está pronto para iniciar a instalação da atualização para sua hierarquia. Para obter mais informações sobre como instalar a atualização, consulte [instalar atualizações no console.](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates)

É recomendável que você planeje a instalação da atualização fora do horário comercial normal de cada site, quando o processo de instalação da atualização e suas ações de reinstalação dos componentes de site e funções do sistema de site terão um efeito mínimo sobre as operações de negócios.

Para obter mais informações, veja [Atualizações para o System Center Configuration Manager](/sccm/core/servers/manage/updates).

