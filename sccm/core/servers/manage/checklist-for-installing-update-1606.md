---
title: Lista de verificação da versão 1606
titleSuffix: Configuration Manager
description: Saiba mais sobre as ações a efetuar antes de atualizar do System Center Configuration Manager versão 1511 ou 1602 para a versão 1606.
ms.date: 6/6/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 75652cd2-a95a-46c5-91c1-6d43fc8e787e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3ad9d054f39e5d5a607b0116b438c784950c7ebd
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56138114"
---
# <a name="checklist-for-installing-update-1606-for-system-center-configuration-manager"></a>Lista de verificação para instalar a atualização 1606 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

A versão 1606 para o ramo atual do System Center Configuration Manager é uma atualização que pode utilizar para atualizar a partir da versão 1511 ou 1602.

Antes de instalar a versão 1606 como uma atualização, reveja as seguintes informações e lista de verificação para ações a efetuar antes de iniciar a atualização.

Para obter informações sobre as versões de linha de base, consulte [versões de linha de base e de atualização](../../../core/servers/manage/updates.md#bkmk_Baselines) na [atualiza para o System Center Configuration Manager](../../../core/servers/manage/updates.md).

 ## <a name="about-installing-update-1606"></a>Sobre como instalar a atualização 1606

Como um *atualizar*, 1606 só pode ser instalada no site de nível superior da sua hierarquia. Isto significa que inicia a instalação do seu site de administração central, se tiver uma, ou a partir de seu site primário autónomo.  

-   Os sites primários subordinados instalam a atualização automaticamente após a conclusão do site de administração central instalar a atualização. Pode utilizar janelas de serviço para controlar quando um site instala as atualizações. Antes da versão 1606, janelas de serviço foram janelas de manutenção. Para obter mais informações, consulte [manutenção do windows para servidores de site](/sccm/core/servers/manage/service-windows).  

-   Tem de atualizar manualmente sites secundários a partir da consola do Configuration Manager após a conclusão do site principal primário instalar a atualização. A atualização automática dos servidores de site secundários não é suportada.  

Quando o servidor do site instala a atualização, as funções de sistema de sites que estão instaladas no servidor do site e que estão instalados em computadores remotos atualizadas automaticamente. Por conseguinte, antes de instalar a atualização, certifique-se de que cada servidor de sistema de sites cumpre os novos pré-requisitos para operações com a nova versão de atualização.  

Na primeira vez que utiliza uma consola do Configuration Manager após a atualização foi instalada, será solicitado que Atualize a consola.  Para fazer isso, tem de executar a configuração do Configuration Manager no computador que aloja a consola e, em seguida, escolha a opção para atualizar a consola. Recomendamos que não adie a instalação da atualização na consola.

 **Problemas conhecidos para esta atualização**   
  Os problemas seguintes aplicam-se ao visualizar o estado de instalação do pacote de atualização:
  - Ao atualizar a partir da versão 1602 para 1606, a etapa **payload do pacote de atualização de extração** apresenta o estado **não iniciado**, apesar do download for concluído.
  - Ao atualizar a partir da versão 1511 a versão 1606, alguns passos irão mostrar estado **concluído** mas não apresentará um valor para **hora da última atualização**.


## <a name="checklist"></a>Lista de verificação  

 **Certifique-se de que todos os sites executam uma versão suportada do System Center Configuration Manager:**  Antes de iniciar a instalação da atualização 1606, cada servidor do site na hierarquia tem de executar a mesma versão do System Center Configuration Manager: a versão 1511 ou 1602.

 **Rever instaladas versões Microsoft.NET nos servidores do sistema de sites:** Quando um site instala a atualização 1606, Configuration Manager instala automaticamente o .NET Framework 4.5.2 em cada computador que aloja uma das seguintes funções do sistema de site (se o .NET Framework 4.5 ou posterior não estiver já instalado):  

-   Ponto proxy de registo  

-   Ponto de inscrição  

-   Ponto de gestão  

-   Ponto de ligação de serviço  

Esta instalação pode colocar o servidor de sistema de sites num reinício pendente estado e o relatório de erros para o Visualizador de estado do componente do Configuration Manager. Além disso, as aplicações .NET no servidor podem ter falhas aleatórias até que o servidor seja reiniciado.  

 Para obter mais informações, consulte [Site e pré-requisitos de sistema de sites](../../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

 **Analise o estado do site e da hierarquia e certifique-se de que não existem não existem problemas por resolver:** Antes de atualizar um site, resolva todos os problemas operacionais do servidor do site, o servidor de base de dados do site e funções de sistema de sites que são instaladas em computadores remotos. Uma atualização de site pode falhar devido a problemas operacionais existentes.

 Para obter mais informações, veja [Utilizar alertas e o sistema de estado para o System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

 **Reveja os replicação de ficheiros e dados entre sites:**  Certifique-se esse ficheiro e a replicação de base de dados entre sites está operacional e atualizada. Atrasos ou registos de segurança em qualquer um podem impedir que uma atualização uniforme e bem-sucedida.    

Para a replicação de base de dados, pode utilizar o Analisador de Ligações de Replicação para ajudar a resolver problemas antes de iniciar a atualização. Para obter mais informações, consulte [sobre o analisador de ligações de replicação](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_RLA) no tópico [monitorizar a infraestrutura hierarquia e replicação no System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md).  

 **Instale todas as atualizações críticas aplicáveis para sistemas operativos em computadores que alojam o site, o servidor de base de dados do site e funções de sistema de sites remoto:** Antes de instalar uma atualização para o Configuration Manager, instale quaisquer atualizações críticas para cada sistema de sites aplicável. Se uma atualização que instalar necessitar de um reinício, reinicie os computadores aplicáveis antes de iniciar a atualização.  

 **Desative réplicas de base de dados para pontos de gestão em sites primários:** O Configuration Manager não é possível atualizar com êxito um site primário que tenha uma réplica de base de dados para pontos de gestão ativada. Desative a replicação de base de dados antes de instalar uma atualização para o Configuration Manager.  

Para obter mais informações, consulte [Database replicas para pontos de gestão do System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

 **Definir grupos de Disponibilidade AlwaysOn do SQL Server para ativação pós-falha manual:**  
 Antes de instalar atualizações, como a versão 1606, certifique-se de que o grupo de disponibilidade está definido para ativação pós-falha manual. Depois do site tenha sido atualizado, pode restaurar a ativação pós-falha para ser automática. Para obter mais informações, consulte [SQL Server AlwaysOn para uma base de dados do site](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

 **Reconfigure os pontos de atualização de software que utilizem NLB:** O Configuration Manager não é possível atualizar um site que utiliza um cluster de balanceamento de carga na rede (NLB) para alojar pontos de atualização de software.  

Se utilizar NLB clusters para pontos de atualização de software, utilize o Windows PowerShell para remover o cluster NLB.    

 Para obter mais informações, veja [Planear atualizações de software no System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).  

 **Desative todas as tarefas de manutenção do site em cada site durante a instalação da atualização nesse site:** Antes de instalar a atualização, desative as tarefas de manutenção do site que possam ser executadas durante a hora em que o processo de atualização estiver ativo. Estas incluem as seguintes, entre outras:  

-   Servidor do Site de Reserva  

-   Eliminar Operações de Cliente Desatualizadas  

-   Eliminar Dados de Deteção Desatualizados  

Quando uma tarefa de manutenção da base de dados do site é executada durante a instalação da atualização, a instalação da atualização pode falhar. Antes de desativar uma tarefa, registe o agendamento da tarefa para que possa restaurar a respetiva configuração após a atualização foi instalada.  

Para obter mais informações, consulte [tarefas de manutenção para o System Center Configuration Manager](../../../core/servers/manage/maintenance-tasks.md) e [tarefas de manutenção para o System Center Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md). 

**Pare temporariamente a qualquer software antivírus em servidores do System Center Configuration Manager:** Antes de atualizar um site, certifique-se de que parou o software antivírus em servidores do Configuration Manager. <!--SMS.503481--> 

 **Crie uma cópia de segurança da base de dados do site no site de administração central e sites primários:** Antes de atualizar um site, criar cópias de segurança da base de dados do site para se certificar de que tem uma cópia de segurança para recuperação após desastre.   

Para obter mais informações, consulte [cópia de segurança e recuperação para o System Center Configuration Manager](../../../protect/understand/backup-and-recovery.md).  

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

 **Planear a criação de pilotos de cliente:** Quando instala uma atualização que atualiza o cliente, pode testar essa nova atualização de cliente em pré-produção antes de implementar e atualizar todos os clientes ativos.   

 Para tirar partido desta opção, antes de iniciar a instalação da atualização, tem de configurar o seu site para suportar as atualizações automáticas para pré-produção. Para obter mais informações, veja [Atualização dos clientes no System Center Configuration Manager](../../../core/clients/manage/upgrade/upgrade-clients.md) e   
[Como testar as atualizações de cliente numa coleção de pré-produção no System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

 **Planear a utilização de janelas de serviço para controlar quando os servidores do site instalam atualizações:** Pode utilizar janelas de serviço para definir um período durante o qual podem ser instaladas atualizações a um servidor de site.

Isto pode ajudar a controlar quando os sites na hierarquia instalam a atualização.
Antes da versão 1606, janelas de serviço foram janelas de manutenção. Para obter mais informações, consulte [manutenção do windows para servidores de site](/sccm/core/servers/manage/service-windows).  

 **Execute o Verificador de pré-requisitos de configuração:**  Antes de instalar a atualização 1606, pode executar o Verificador de pré-requisitos independentemente da instalação da atualização. Quando instalar a atualização no site, o Verificador de pré-requisitos é executado novamente.  

Para obter mais informações, consulte **passo 3: Executar o Verificador de pré-requisitos antes de instalar uma atualização** no [atualiza para o System Center Configuration Manager](../../../core/servers/manage/install-in-console-updates.md) tópico.  

> [!IMPORTANT]  
>  Quando o Verificador de pré-requisitos é executado independentemente ou como parte de uma instalação de atualização, o processo atualiza alguns ficheiros de origem do produto que são utilizados para tarefas de manutenção do site. Por conseguinte, depois de executar o Verificador de pré-requisitos, mas antes a instalar a atualização 1606, se tiver de realizar uma tarefa de manutenção do site, execute **Setupwpf.exe** (configuração do Configuration Manager) partir do CD. Pasta mais recente no servidor do site.  

 **Atualizar sites:** Agora está pronto para iniciar a instalação de atualização para a sua hierarquia.  
  Recomendamos que planeie instalar a atualização fora do horário comercial normal para cada site, quando o processo de instalação da atualização e respetivas ações para reinstalar os componentes do site e as funções de sistema de sites irão ter o mínimo efeito nas operações comerciais.

Para obter mais informações, veja [Atualizações para o System Center Configuration Manager](../../../core/servers/manage/updates.md).  
