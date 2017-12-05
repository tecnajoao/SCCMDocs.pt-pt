---
title: "Lista de verificação para 1610"
titleSuffix: Configuration Manager
description: "Saiba mais sobre as ações a efetuar antes de atualizar o System Center Configuration Manager versão 1610."
ms.custom: na
ms.date: 6/6/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b411cb0-4fd1-41f2-a2f6-33738a5bde96
caps.latest.revision: "7"
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 8099e90fcd16b677b260d1d693c69d0cbe698295
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/04/2017
---
# <a name="checklist-for-installing-update-1610-for-system-center-configuration-manager"></a>Lista de verificação para instalar a atualização 1610 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Quando utiliza o ramo atual do System Center Configuration Manager, pode instalar a atualização na consola para a versão 1610 ao atualizar a sua hierarquia de versão 1606. Se a sua hierarquia executar a versão 1511, versão 1602 ou 1606, pode atualizar para versão 1610.

Para obter a atualização para a versão 1610, tem de utilizar uma função de sistema de sites de ponto de ligação de serviço no site de nível superior da sua hierarquia. Isto pode ser no modo online ou offline. Após a sua hierarquia transfere o pacote de atualização da Microsoft, pode encontrá-lo na consola em **administração &gt; descrição geral &gt; serviços em nuvem &gt; atualizações e manutenção**.

-   Quando a atualização está listada como **disponível**, a atualização está pronta para instalar. Antes de instalar a versão 1610, reveja as seguintes informações [sobre a instalação de atualização 1610](#about-installing-update-1610) e [lista de verificação](#checklist) para configurações para se certificar antes de iniciar a atualização.

-   Se a atualização é apresentado como **transferir** e não alterar, reveja o **hman.log** e **dmpdownloader.log** erros.

    -   Normalmente, também pode reiniciar o **SMS_Executive** serviço no servidor do site para reiniciar a transferência de ficheiros de redistribuição a atualização.

    -   Outro problema comum verificado pela transferência ocorre quando as definições do servidor proxy impediram transferências do <http://silverlight.dlservice.microsoft.com> e <http://download.microsoft.com>.

Para obter mais informações sobre a instalação de atualizações, consulte [na consola atualizações e manutenção](/sccm/core/servers/manage/updates#a-namebkmkinconsolea-in-console-updates-and-servicing).

Para obter informações sobre as versões do ramo atual, consulte [versões de linha de base e atualização](/sccm/core/servers/manage/updates#bkmk_Baselines) no [atualizações para o System Center Configuration Manager](/sccm/core/servers/manage/updates).

## <a name="about-installing-update-1610"></a>Sobre a instalação de atualização 1610

**Sites:**  
Atualização 1610 só pode ser instalada no site de nível superior da hierarquia. Isto significa que inicia a instalação do seu site de administração central, se tiver uma, ou do seu site primário autónomo. Após a atualização obtém instalada no site de nível superior, os sites subordinados têm o seguinte comportamento da atualização:

-   Os sites primários subordinados instalam a atualização automaticamente depois do site de administração central concluir a instalação da atualização. Pode utilizar janelas de serviço para controlar quando um site instala as atualizações. Antes de versão 1606, janelas de serviço foram chamadas janelas de manutenção. Para obter mais informações, consulte [windows para servidores de site do serviço](/sccm/core/servers/manage/service-windows).

-   Tem de atualizar manualmente sites secundários a partir da consola do Configuration Manager depois do site primário principal concluída a instalação da atualização. A atualização automática dos servidores de site secundários não é suportada.

**Funções de sistema de sites:**  
Quando o servidor do site instala a atualização, as funções de sistema de sites que estão instaladas no servidor do site e os que são instaladas automaticamente em computadores remotos for atualizadas. Por isso, antes de instalar a atualização, certifique-se de que cada servidor do sistema de sites cumpre os novos pré-requisitos para a operação com a nova versão de atualização.

**Consolas do Configuration Manager:**   
Na primeira vez que utiliza uma consola do Configuration Manager após a atualização estiver concluída, será solicitado Atualize a consola. Para tal, tem de executar a configuração do Configuration Manager no computador que aloja a consola e, em seguida, escolha a opção para atualizar a consola. Recomendamos que não adie a instalação da atualização na consola.



## <a name="checklist"></a>Lista de verificação

**Certifique-se de que todos os sites executem uma versão suportada do System Center Configuration Manager:** Antes de iniciar a instalação da atualização 1610, cada site na hierarquia tem de executar a mesma versão do System Center Configuration Manager: a versão 1511, versão 1602 ou 1606.

**Rever o estado do seu Software Assurance ou direitos equivalentes de subscrição:**   
Tem de ter um contrato de Software Assurance (SA) de Active Directory ao instalar a atualização 1610. Quando instalar a versão 1610, terá a opção **licenciamento** separador para confirmar a sua **data de expiração do Software Assurance**.

Este é um valor opcional que pode especificar como um lembrete conveniente da sua data de expiração de licença, que é visível quando instalar atualizações futuras. Se instalou o Configuration Manager do suporte de dados de linha de base da versão 1606, pode ter anteriormente especificado este valor durante a configuração, ou no **licenciamento** separador do **definições de hierarquia** após a instalação de site.

Para obter mais informações, consulte [licenciamento e ramos para o System Center Configuration Manager](/sccm/core/understand/learn-more-editions).

**Revisão instaladas as versões do Microsoft .NET em servidores do sistema de sites:** Quando um site instala a atualização 1610, o Configuration Manager instala automaticamente o .NET Framework 4.5.2 em cada computador que aloja uma das seguintes funções do sistema de site quando o .NET Framework 4.5 ou posterior não está já instalada:

-   Ponto proxy de registo
-   Ponto de inscrição
-   Ponto de gestão
-   Ponto de ligação de serviço

Esta instalação pode colocar o servidor de sistema de sites no reinício pendente erros de estado e relatórios para o Visualizador de estado do componente do Configuration Manager. Além disso, as aplicações de .NET no servidor podem ocorrer falhas aleatórias até que o servidor seja reiniciado.

Para obter mais informações, veja [Pré-requisitos de site e sistema de sites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).

**Rever o estado de site e da hierarquia e certifique-se de que existem não existem problemas por resolver:** Antes de atualizar um site, resolva todos os problemas operacionais do servidor do site, o servidor de base de dados do site e funções de sistema de sites que são instaladas em computadores remotos. Uma atualização de site pode falhar devido a problemas operacionais existentes.

Para obter mais informações, veja [Utilizar alertas e o sistema de estado para o System Center Configuration Manager](/sccm/core/servers/manage/use-alerts-and-the-status-system).

**Reveja o ficheiro e dados de replicação entre sites:**   
Certifique-se de que o ficheiro e a replicação de base de dados entre sites está operacional e atual. Os atrasos ou os registos de segurança no podem impedir uma atualização com êxito, uniforme.
Para a replicação de base de dados, pode utilizar o Analisador de Ligações de Replicação para ajudar a resolver problemas antes de iniciar a atualização.

Para obter mais informações, consulte [sobre o analisador do Link de replicação](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure#BKMK_RLA) no [monitorizar a infraestrutura hierarquia e replicação no System Center Configuration Manager](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure) tópico.

**Instale todas as atualizações críticas aplicáveis para sistemas operativos em computadores que alojam o site, o servidor de base de dados do site e as funções do sistema de sites remoto:** Antes de instalar uma atualização para o Configuration Manager, instale quaisquer atualizações críticas para cada sistema de sites aplicáveis. Se uma atualização que instalar necessitar de um reinício, reinicie os computadores aplicáveis antes de iniciar a atualização do Configuration Manager.

**Desative réplicas de base de dados para pontos de gestão em sites primários:**   
O Configuration Manager não é possível atualizar com êxito um site primário que tenha uma réplica de base de dados para pontos de gestão ativada. Desative a replicação de base de dados antes de instalar uma atualização para o Configuration Manager.

Para obter mais informações, veja [Réplicas de bases de dados para pontos de gestão do System Center Configuration Manager](/sccm/core/servers/deploy/configure/database-replicas-for-management-points).

**Definir grupos de Disponibilidade AlwaysOn do SQL Server para ativação pós-falha manual:**   
Antes de instalar atualizações, tais como versão 1610, certifique-se de que o grupo de disponibilidade está definido para ativação pós-falha manual. Depois do site tiver sido atualizado, pode restaurar a ativação pós-falha para ser automática. Para obter mais informações consulte [SQL Server AlwaysOn para uma base de dados do site](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).

**Reconfigure os pontos de atualização de software que utilizem NLB:**   
O Configuration Manager não é possível atualizar um site que utiliza uma cluster (NLB) para alojar pontos de atualização de software de balanceamento de carga na rede.

Se utilizar NLB clusters para pontos de atualização de software, utilize o Windows PowerShell para remover o cluster NLB.
Para obter mais informações, veja [Planear atualizações de software no System Center Configuration Manager](/sccm/sum/plan-design/plan-for-software-updates).

**Desative todas as tarefas de manutenção do site em cada site durante a instalação da atualização desse site:**   
Antes de instalar a atualização, desative as tarefas de manutenção do site que possam ser executadas enquanto o que o processo de atualização estiver ativo. Estas incluem as seguintes, entre outras:

-   Servidor do Site de Reserva
-   Eliminar Operações de Cliente Desatualizadas
-   Eliminar Dados de Deteção Desatualizados

Quando uma tarefa de manutenção da base de dados do site é executada durante a instalação da atualização, a instalação da atualização pode falhar. Antes de desativar uma tarefa, registe o agendamento da tarefa para que possa restaurar a respetiva configuração após a atualização foi instalada.

Para obter mais informações, consulte [tarefas de manutenção do System Center Configuration Manager](/sccm/core/servers/manage/maintenance-tasks) e [tarefas de referência para a manutenção do System Center Configuration Manager](/sccm/core/servers/manage/reference-for-maintenance-tasks).

**Crie uma cópia de segurança da base de dados do site no site de administração central e sites primários:** Antes de atualizar um site, uma cópia de segurança da base de dados do site para se certificar de que tem uma cópia de segurança a utilizar para recuperação após desastre.

Para obter mais informações, consulte [cópia de segurança e recuperação para o System Center Configuration Manager](/sccm/protect/understand/backup-and-recovery).

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

**Planear testes de implementação de cliente:**   
Quando instala uma atualização que atualiza o cliente, pode testar essa nova atualização de cliente em pré-produção antes de implementar e atualiza todos os clientes ativos.

Para tirar partido desta opção, tem de configurar o seu site para suportar as atualizações automáticas para pré-produção antes de iniciar a instalação da atualização.

Para obter mais informações, consulte [atualizar clientes no System Center Configuration Manager](/sccm/core/clients/manage/upgrade/upgrade-clients) e [como testar as atualizações de cliente numa coleção de pré-produção no System Center Configuration Manager](/sccm/core/clients/manage/upgrade/test-client-upgrades).

**Planear a utilização de janelas de serviço para controlar quando os servidores do site instalam atualizações:**   
Pode utilizar janelas de serviço para definir um período durante o qual podem ser instaladas as atualizações de um servidor de site.

Isto pode ajudar a controlar quando os sites na hierarquia instalam a atualização. Antes de versão 1606, janelas de serviço foram chamadas janelas de manutenção. Para obter mais informações, consulte [windows para servidores de site do serviço](/sccm/core/servers/manage/service-windows).

**Execute o Verificador de pré-requisitos do programa de configuração:**   
Quando a atualização está listada na consola do como **disponível,** independentemente pode executar o Verificador de pré-requisitos antes de instalar a atualização. (Quando instalar a atualização no site, o Verificador de pré-requisitos é executado novamente.)

Para executar uma verificação de pré-requisitos a partir da consola, aceda a **administração > Descrição geral > Serviços Cloud > atualizações e manutenção.** Em seguida, clique com botão direito **pacote de atualização do Configuration Manager 1610**e, em seguida, escolha **executar verificação de pré-requisitos**.

Para obter mais informações sobre como iniciar e, em seguida, monitorizar a verificação de pré-requisitos, consulte **passo 3: Executar o Verificador de pré-requisitos antes de instalar uma atualização** no tópico [instalar atualizações na consola do System Center Configuration Manager](/sccm/core/servers/manage/install-in-console-updates).

> [!IMPORTANT]  
> Quando o Verificador de pré-requisitos é executado independentemente ou como parte de uma instalação de atualização, o processo atualiza alguns ficheiros de origem do produto que são utilizados para tarefas de manutenção do site. Por conseguinte, depois de executar o Verificador de pré-requisitos, mas antes a instalar a atualização 1610, se precisar de executar uma tarefa de manutenção do site, execute **Setupwpf.exe** (configuração do Configuration Manager) partir do CD. Pasta mais recente no servidor do site.

**Atualizar sites:**   
Agora está pronto para iniciar a instalação da atualização para a sua hierarquia. Para obter mais informações sobre como instalar a atualização, consulte [instalar atualizações na consola.](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates)

Recomendamos que planeia instalar a atualização fora do horário comercial normal para cada site, quando o processo de instalação da atualização e as respetivas ações para reinstalar os componentes do site e funções de sistema de sites irão ter o mínimo efeito nas suas operações de negócio.

Para obter mais informações, veja [Atualizações para o System Center Configuration Manager](/sccm/core/servers/manage/updates).
