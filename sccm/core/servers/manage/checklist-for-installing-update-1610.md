---
title: Lista de verificação da versão 1610
titleSuffix: Configuration Manager
description: Saiba mais sobre as ações a efetuar antes de atualizar para o System Center Configuration Manager versão 1610.
ms.date: 6/6/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7b411cb0-4fd1-41f2-a2f6-33738a5bde96
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: dc06edc9bea3f86187604e9b94ca0e2216df391a
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/24/2019
ms.locfileid: "54897598"
---
# <a name="checklist-for-installing-update-1610-for-system-center-configuration-manager"></a>Lista de verificação para instalar a atualização 1610 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Quando utiliza o ramo atual do System Center Configuration Manager, pode instalar a atualização na consola para a versão 1610 para atualizar a sua hierarquia da versão 1606. Se a sua hierarquia executa a versão 1511, versão 1602 ou 1606, pode atualizar para versão 1610.

Para obter a atualização de versão 1610, tem de utilizar uma função de sistema de sites de ponto de ligação de serviço no site de nível superior da sua hierarquia. Isso pode ser no modo online ou offline. Depois da hierarquia transfere o pacote de atualização da Microsoft, pode encontrá-lo na consola em **Administration &gt; descrição geral &gt; serviços Cloud &gt; atualizações e manutenção**.

-   Quando a atualização é listada como **disponível**, está pronta para instalar a atualização. Antes de instalar a versão 1610, reveja as seguintes informações [sobre a instalação da atualização 1610](#about-installing-update-1610) e o [lista de verificação](#checklist) para configurações de fazer antes de iniciar a atualização.

-   Se a atualização indicará **transferir** e não alterar, reveja o **hman. log** e **dmpdownloader. log** erros.

    -   Normalmente, também pode reiniciar o **SMS_Executive** serviço no servidor do site para reiniciar o download dos arquivos de redistribuição da atualização.

    -   Outro problema comum de download ocorre quando transferências a partir de impedir que as definições do servidor proxy <http://silverlight.dlservice.microsoft.com> e <http://download.microsoft.com>.

Para obter mais informações sobre como instalar atualizações, consulte [atualizações e manutenção na consola](/sccm/core/servers/manage/updates#a-namebkmkinconsolea-in-console-updates-and-servicing).

Para obter informações sobre as versões do ramo atual, consulte [versões de linha de base e de atualização](/sccm/core/servers/manage/updates#bkmk_Baselines) na [atualiza para o System Center Configuration Manager](/sccm/core/servers/manage/updates).

## <a name="about-installing-update-1610"></a>Sobre como instalar a atualização 1610

**Sites:**  
Atualização 1610 só pode ser instalada no site de nível superior da sua hierarquia. Isto significa que inicia a instalação do seu site de administração central, se tiver uma, ou a partir de seu site primário autónomo. Após a atualização é instalada no site de nível superior, os sites subordinados têm o seguinte comportamento de atualização:

-   Os sites primários subordinados instalam a atualização automaticamente após o site de administração central concluir a instalação da atualização. Pode utilizar janelas de serviço para controlar quando um site instala as atualizações. Antes da versão 1606, janelas de serviço foram janelas de manutenção. Para obter mais informações, consulte [manutenção do windows para servidores de site](/sccm/core/servers/manage/service-windows).

-   Tem de atualizar manualmente sites secundários a partir da consola do Configuration Manager depois do site principal primário concluir a instalação da atualização. A atualização automática dos servidores de site secundários não é suportada.

**Funções de sistema de sites:**  
Quando o servidor do site instala a atualização, as funções de sistema de sites que estão instaladas no servidor do site e os que são instaladas automaticamente em computadores remotos for atualizadas. Portanto, antes de instalar a atualização, certifique-se de que cada servidor de sistema de sites cumpre os novos pré-requisitos para a operação com a nova versão de atualização.

**Consolas do Configuration Manager:**   
Na primeira vez que utiliza uma consola do Configuration Manager após a atualização foi concluída, será solicitado que Atualize a consola. Para fazer isso, tem de executar a configuração do Configuration Manager no computador que aloja a consola e, em seguida, escolha a opção para atualizar a consola. Recomendamos que não adie a instalação da atualização na consola.



## <a name="checklist"></a>Lista de verificação

**Certifique-se de que todos os sites executam uma versão suportada do System Center Configuration Manager:**  Antes de iniciar a instalação de atualização 1610, cada site na hierarquia tem de executar a mesma versão do System Center Configuration Manager: a versão 1511, versão 1602 ou 1606.

**Rever o estado do seu Software Assurance ou ter direitos equivalentes de subscrição:**   
Tem de ter um contrato de Software Assurance (SA) ativo para instalar a atualização 1610. Quando instalar a versão 1610, terá a opção **Licensing** separador para confirmar sua **data de expiração do Software Assurance**.

Este é um valor opcional que pode ser especificado como um lembrete conveniente da sua data de expiração de licença, que é visível quando instalar atualizações futuras. Se tiver instalado o Configuration Manager a partir do suporte de dados de linha de base da versão 1606, pode ter anteriormente especificado neste valor durante a configuração ou no **Licensing** separador da **definições de hierarquia** depois de site instalação.

Para obter mais informações, consulte [ramificações para o System Center Configuration Manager e de licenciamento](/sccm/core/understand/learn-more-editions).

**Rever instaladas as versões de Microsoft .NET nos servidores do sistema de sites:**  Quando um site instala a atualização 1610, o Configuration Manager instala automaticamente o .NET Framework 4.5.2 em cada computador que aloja uma das seguintes funções do sistema de site quando o .NET Framework 4.5 ou posterior ainda não estiver instalado:

-   Ponto proxy de registo
-   Ponto de inscrição
-   Ponto de gestão
-   Ponto de ligação de serviço

Esta instalação pode colocar o servidor de sistema de sites num reinício pendente estado e o relatório de erros para o Visualizador de estado do componente do Configuration Manager. Além disso, as aplicações de .NET no servidor de podem ocorrer falhas aleatórias até que o servidor seja reiniciado.

Para obter mais informações, consulte [Site e pré-requisitos de sistema de sites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).

**Analise o estado do site e da hierarquia e certifique-se de que não existem não existem problemas por resolver:**  Antes de atualizar um site, resolva todos os problemas operacionais do servidor do site, o servidor de base de dados do site e funções de sistema de sites que são instaladas em computadores remotos. Uma atualização de site pode falhar devido a problemas operacionais existentes.

Para obter mais informações, consulte [utilizar alertas e o estado do sistema do System Center Configuration Manager](/sccm/core/servers/manage/use-alerts-and-the-status-system).

**Reveja os replicação de ficheiros e dados entre sites:**   
Certifique-se esse ficheiro e a replicação de base de dados entre sites está operacional e atualizada. Atrasos ou registos de segurança em qualquer um podem impedir que uma atualização uniforme e bem-sucedida.
Para a replicação de base de dados, pode utilizar o Analisador de Ligações de Replicação para ajudar a resolver problemas antes de iniciar a atualização.

Para obter mais informações, consulte [sobre o analisador de ligações de replicação](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure#BKMK_RLA) no [monitorizar a infraestrutura hierarquia e replicação no System Center Configuration Manager](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure)   tópico.

**Instale todas as atualizações críticas aplicáveis para sistemas operativos em computadores que alojam o site, o servidor de base de dados do site e funções de sistema de sites remoto:**  Antes de instalar uma atualização para o Configuration Manager, instale quaisquer atualizações críticas para cada sistema de sites aplicável. Se uma atualização que instalar necessitar de um reinício, reinicie os computadores aplicáveis antes de iniciar a atualização do Configuration Manager.

**Desative réplicas de base de dados para pontos de gestão em sites primários:**   
O Configuration Manager não é possível atualizar com êxito um site primário que tenha uma réplica de base de dados para pontos de gestão ativada. Desative a replicação de base de dados antes de instalar uma atualização para o Configuration Manager.

Para obter mais informações, veja [Réplicas de bases de dados para pontos de gestão do System Center Configuration Manager](/sccm/core/servers/deploy/configure/database-replicas-for-management-points).

**Definir grupos de Disponibilidade AlwaysOn do SQL Server para ativação pós-falha manual:**   
Antes de instalar atualizações, como versão 1610, certifique-se de que o grupo de disponibilidade está definido para ativação pós-falha manual. Depois do site tenha sido atualizado, pode restaurar a ativação pós-falha para ser automática. Para obter mais informações, consulte [SQL Server AlwaysOn para uma base de dados do site](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).

**Reconfigure os pontos de atualização de software que utilizem NLB:**   
O Configuration Manager não é possível atualizar um site que utiliza uma cluster (NLB) para alojar pontos de atualização de software de balanceamento de carga de rede.

Se utilizar NLB clusters para pontos de atualização de software, utilize o Windows PowerShell para remover o cluster NLB.
Para obter mais informações, consulte [planear atualizações de software no System Center Configuration Manager](/sccm/sum/plan-design/plan-for-software-updates).

**Desative todas as tarefas de manutenção do site em cada site durante a instalação da atualização nesse site:**   
Antes de instalar a atualização, desative as tarefas de manutenção do site que possam ser executadas durante o tempo que o processo de atualização estiver ativo. Estas incluem as seguintes, entre outras:

-   Servidor do Site de Reserva
-   Eliminar Operações de Cliente Desatualizadas
-   Eliminar Dados de Deteção Desatualizados

Quando uma tarefa de manutenção da base de dados do site é executada durante a instalação da atualização, a instalação da atualização pode falhar. Antes de desativar uma tarefa, registe o agendamento da tarefa para que possa restaurar a respetiva configuração após a atualização foi instalada.

Para obter mais informações, consulte [tarefas de manutenção para o System Center Configuration Manager](/sccm/core/servers/manage/maintenance-tasks) e [tarefas de manutenção para o System Center Configuration Manager](/sccm/core/servers/manage/reference-for-maintenance-tasks).

**Pare temporariamente a qualquer software antivírus em servidores do System Center Configuration Manager:** Antes de atualizar um site, certifique-se de que parou o software antivírus em servidores do Configuration Manager. <!--SMS.503481-->

**Crie uma cópia de segurança da base de dados do site no site de administração central e sites primários:**  Antes de atualizar um site, criar cópias de segurança da base de dados do site para se certificar de que tem uma cópia de segurança para recuperação após desastre.

Para obter mais informações, consulte [cópia de segurança e recuperação para o System Center Configuration Manager](/sccm/protect/understand/backup-and-recovery).

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

**Planear a criação de pilotos de cliente:**   
Quando instala uma atualização que atualiza o cliente, pode testar essa nova atualização de cliente em pré-produção antes de implementar e atualizar todos os clientes ativos.

Para tirar partido desta opção, tem de configurar o seu site para suportar as atualizações automáticas para pré-produção antes de iniciar a instalação da atualização.

Para obter mais informações, consulte [atualizar os clientes no System Center Configuration Manager](/sccm/core/clients/manage/upgrade/upgrade-clients) e [como testar as atualizações de cliente numa coleção de pré-produção no System Center Configuration Manager](/sccm/core/clients/manage/upgrade/test-client-upgrades).

**Planear a utilização de janelas de serviço para controlar quando os servidores do site instalam atualizações:**   
Pode utilizar janelas de serviço para definir um período durante o qual podem ser instaladas atualizações a um servidor de site.

Isto pode ajudar a controlar quando os sites na hierarquia instalam a atualização. Antes da versão 1606, janelas de serviço foram janelas de manutenção. Para obter mais informações, consulte [manutenção do windows para servidores de site](/sccm/core/servers/manage/service-windows).

**Execute o Verificador de pré-requisitos de configuração:**   
Quando a atualização é listada na consola do como **disponível,** independente pode executar o Verificador de pré-requisitos antes de instalar a atualização. (Quando instalar a atualização no site, verificador de pré-requisitos é executado novamente.)

Para executar uma verificação de pré-requisitos a partir da consola, aceda a **administração > Descrição geral > Serviços Cloud > atualizações e manutenção.** Em seguida, clique com botão direito **pacote de atualização de versão 1610 do Configuration Manager**e, em seguida, escolha **executar verificação de pré-requisitos**.

Para obter mais informações sobre como iniciar e, em seguida, monitorizar a verificação de pré-requisitos, consulte **passo 3: Executar o Verificador de pré-requisitos antes de instalar uma atualização** no tópico [instalar atualizações na consola do System Center Configuration Manager](/sccm/core/servers/manage/install-in-console-updates).

> [!IMPORTANT]  
> Quando o Verificador de pré-requisitos é executado independentemente ou como parte de uma instalação de atualização, o processo atualiza alguns ficheiros de origem do produto que são utilizados para tarefas de manutenção do site. Portanto, depois de executar o Verificador de pré-requisitos, mas antes a instalar a atualização 1610, se tiver de realizar uma tarefa de manutenção do site, execute **Setupwpf.exe** (configuração do Configuration Manager) partir do CD. Pasta mais recente no servidor do site.

**Atualizar sites:**   
Agora está pronto para iniciar a instalação de atualização para a sua hierarquia. Para obter mais informações sobre como instalar a atualização, consulte [instalar atualizações na consola.](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates)

Recomendamos que planeie instalar a atualização fora do horário comercial normal para cada site, quando o processo de instalação da atualização e respetivas ações para reinstalar os componentes do site e as funções de sistema de sites irão ter o mínimo efeito nas operações comerciais.

Para obter mais informações, consulte [atualizações para o System Center Configuration Manager](/sccm/core/servers/manage/updates).
