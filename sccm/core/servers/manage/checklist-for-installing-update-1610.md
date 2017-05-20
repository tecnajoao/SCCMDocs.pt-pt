---
title: "Lista de verificação para 1610 | O System Center Configuration Manager"
description: "Saiba mais sobre as ações a efetuar antes de atualizar para o System Center Configuration Manager versão 1610."
ms.custom: na
ms.date: 2/7/2017
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
ms.sourcegitcommit: 30af3326578d39c6d995672071705bcaeb877e4d
ms.openlocfilehash: 640fc5ddb4e0a6828901b7f406ca72fc210b2970
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="checklist-for-installing-update-1610-for-system-center-configuration-manager"></a>Lista de verificação para instalar a atualização 1610 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Quando utiliza o ramo atual do System Center Configuration Manager, pode instalar a atualização na consola para a versão 1610 para atualizar a hierarquia a partir da versão 1606. Se a hierarquia executa versão 1511, 1602 ou 1606, pode atualizar para versão 1610.

Para obter a atualização da versão 1610, tem de utilizar uma função de sistema de sites de ponto de ligação de serviço no site de nível superior da hierarquia. Isto pode ser no modo online ou offline. Depois da hierarquia transfere o pacote de atualização da Microsoft, pode encontrá-lo na consola em **administração &gt; descrição geral &gt; serviços em nuvem &gt; atualizações e a manutenção**.

-   Se a atualização estiver listada como **disponível**, está pronta para instalar a atualização. Antes de instalar a versão 1610, reveja as seguintes informações [sobre a instalação de atualização 1610](#about-installing-update-1610) e [lista de verificação](#checklist) configurações efetuar antes de iniciar a atualização.

-   Se a atualização apresenta como **transferir** e não altere, reveja o **hman** e **dmpdownloader** erros.

    -   Normalmente, também pode reiniciar o **SMS_Executive** serviço no servidor do site para reiniciar a transferência de ficheiros de redistribuição a atualização.

    -   Outro problema de transferência comuns ocorre quando as definições do servidor proxy impedem transferências do <http://silverlight.dlservice.microsoft.com> e <http://download.microsoft.com>.

Para obter mais informações sobre a instalação de atualizações, consulte o artigo [em-consola atualizações e a servir](/sccm/core/servers/manage/updates#a-namebkmkinconsolea-in-console-updates-and-servicing).

Para obter informações sobre as versões do mesmo atual, consulte o artigo [versões de linha de base e atualização](/sccm/core/servers/manage/updates#bkmk_Baselines) no [atualizações para o System Center Configuration Manager](/sccm/core/servers/manage/updates).

## <a name="about-installing-update-1610"></a>Sobre a instalação de atualização 1610

**Sites:**  
Atualização 1610 apenas pode ser instalada no site de nível superior da hierarquia. Isto significa iniciar a instalação do seu site de administração central, se tiver um, ou a partir do seu site primário autónomo. Após a atualização obtém instalada no site de nível superior, os sites subordinados têm o seguinte comportamento de atualização:

-   Os sites primários subordinados instalam automaticamente a atualização depois do site de administração central conclui a instalação da atualização. Pode utilizar janelas de serviço para controlar quando um site instala as atualizações. Antes da versão 1606, windows serviço foram chamados janelas de manutenção. Para obter mais informações, consulte o artigo [windows dos servidores do site do serviço](/sccm/core/servers/manage/service-windows).

-   Tem de atualizar manualmente os sites secundários a partir da consola do Configuration Manager depois do site primário principal concluída a instalação da atualização. A atualização automática dos servidores de site secundários não é suportada.

**Funções de sistema de sites:**  
Quando o servidor do site instala a atualização, as funções de sistema de sites que estão instaladas no servidor do site e os que são instaladas automaticamente em computadores remotos atualizadas. Por isso, antes de instalar a atualização, certifique-se de que cada servidor de sistema de sites cumpre os novos pré-requisitos para a operação com a nova versão de atualização.

**Consolas do Configuration Manager:**   
A primeira vez que utiliza uma consola do Configuration Manager após a atualização estiver concluída, será solicitado para atualizar a consola. Para tal, tem de executar a configuração do Configuration Manager no computador que aloja a consola e, em seguida, escolha a opção para atualizar a consola. Recomendamos que não adie a instalação da atualização na consola.



## <a name="checklist"></a>Lista de verificação

**Certifique-se de que todos os sites executem uma versão suportada do System Center Configuration Manager:** Antes de iniciar a instalação da atualização 1610, cada site na hierarquia têm de ter a mesma versão do System Center Configuration Manager: qualquer uma das versões 1511, 1602 ou 1606.

**Rever o estado do seu Software Assurance ou direitos equivalentes de subscrição:**   
Tem de ter um contrato de Software Assurance (SA) de Active Directory para instalar a atualização 1610. Quando instala a versão 1610, terá a opção **licenciamento** separador para confirmar o **data de expiração de Software Assurance**.

Este é um valor opcional que pode ser especificado como um lembrete conveniente de sua data de expiração de licença, que está visível quando a instalação de atualizações futuras. Se tiver instalado o Configuration Manager a partir do suporte de dados de linha de base da versão 1606, poderá ter anteriormente especificado este valor durante a configuração, ou no **licenciamento** separador do **definições de hierarquia** após a instalação de site.

Para obter mais informações, consulte o artigo [licenciamento e ramos para o System Center Configuration Manager](/sccm/core/understand/learn-more-editions).

**Rever instaladas versões do Microsoft .NET em servidores de sistema de sites:** Quando instala um site atualização 1610, o Configuration Manager instala automaticamente o .NET Framework 4.5.2 em cada computador que aloje um dos seguintes funções do sistema de site quando o .NET Framework 4.5 ou posterior não está já instalada:

-   Ponto proxy de registo
-   Ponto de inscrição
-   Ponto de gestão
-   Ponto de ligação de serviço

Esta instalação pode colocar o servidor de sistema de sites num reinício pendente estado e o relatório de erros para o Visualizador de estado do componente do Configuration Manager. Além disso, aplicações de .NET no servidor podem ocorrer falhas aleatórias até que o servidor seja reiniciado.

Para obter mais informações, veja [Pré-requisitos de site e sistema de sites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).

**Rever o estado de site e da hierarquia e certifique-se de que não existem sem problemas por resolver:** Antes de atualizar um site, resolva todos os problemas operacionais do servidor do site, o servidor de base de dados do site e funções de sistema de sites que estão instaladas em computadores remotos. Uma atualização de site pode falhar devido a problemas operacionais existentes.

Para obter mais informações, veja [Utilizar alertas e o sistema de estado para o System Center Configuration Manager](/sccm/core/servers/manage/use-alerts-and-the-status-system).

**Reveja o ficheiro e dados de replicação entre sites:**   
Certifique-se esse ficheiro e a replicação de base de dados entre sites é operacional e atual. Atrasos ou os registos de segurança no podem impedir que uma atualização suave, com êxito.
Para a replicação de base de dados, pode utilizar o Analisador de Ligações de Replicação para ajudar a resolver problemas antes de iniciar a atualização.

Para obter mais informações, consulte o artigo [sobre o analisador de ligações de replicação](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure#BKMK_RLA) no [monitorizar a infraestrutura hierarquia e replicação no System Center Configuration Manager](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure) tópico.

**Instale todas as atualizações críticas aplicáveis a sistemas operativos em computadores que alojam o site, o servidor de base de dados de sites e funções do sistema de sites remoto:** Antes de instalar uma atualização para o Configuration Manager, instale as atualizações críticas em cada sistema de sites aplicável. Se uma atualização que instalar necessitar de um reinício, reinicie os computadores aplicáveis antes de iniciar a atualização do Configuration Manager.

**Desative as réplicas de base de dados para pontos de gestão em sites primários:**   
O Configuration Manager não é possível atualizar com êxito um site primário que tenha uma réplica de base de dados para pontos de gestão ativada. Desative a replicação de base de dados antes de:

-   Crie uma cópia de segurança da base de dados do site para testar a atualização de base de dados.
-   Instale uma atualização para o Configuration Manager.

Para obter mais informações, veja [Réplicas de bases de dados para pontos de gestão do System Center Configuration Manager](/sccm/core/servers/deploy/configure/database-replicas-for-management-points).

**Definir grupos de Disponibilidade AlwaysOn do SQL Server para ativação pós-falha manual:**   
Antes de instalar atualizações, tais como versão 1610, certifique-se de que o grupo de disponibilidade está configurado para ativação pós-falha manual. Após ter sido atualizado o site, pode restaurar a ativação pós-falha para ser automática. Para mais informações consulte [SQL Server AlwaysOn numa base de dados do site](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).

**Reconfigure os pontos de atualização de software que utilizem NLBs:**   
O Configuration Manager não é possível atualizar um site que utiliza uma cluster de (NLB) para alojar pontos de atualização de software de balanceamento de carga na rede.

Se utilizar clusters de NLB para pontos de atualização de software, utilize o Windows PowerShell para remover o cluster NLB.
Para obter mais informações, veja [Planear atualizações de software no System Center Configuration Manager](/sccm/sum/plan-design/plan-for-software-updates).

**Desative todas as tarefas de manutenção do site em cada site durante a instalação da atualização nesse site:**   
Antes de instalar a atualização, desative as tarefas de manutenção do site que possam ser executadas enquanto o que o processo de atualização estiver ativo. Estas incluem as seguintes, entre outras:

-   Servidor do Site de Reserva
-   Eliminar Operações de Cliente Desatualizadas
-   Eliminar Dados de Deteção Desatualizados

Quando uma tarefa de manutenção da base de dados do site é executada durante a instalação da atualização, a instalação da atualização pode falhar. Antes de desativar uma tarefa, registe a agenda da tarefa para que possa restaurar a respetiva configuração após a atualização foi instalada.

Para obter mais informações, consulte o artigo [tarefas de manutenção para o System Center Configuration Manager](/sccm/core/servers/manage/maintenance-tasks) e [referência para a manutenção de tarefas para o System Center Configuration Manager](/sccm/core/servers/manage/reference-for-maintenance-tasks).

**Crie uma cópia de segurança da base de dados do site no site de administração central e sites primários:** Antes de atualizar um site, criar uma cópia de segurança da base de dados do site para se certificar de que tem uma cópia de segurança a utilizar para recuperação após desastre.

Para obter mais informações, consulte o artigo [cópia de segurança e recuperação para o System Center Configuration Manager](/sccm/protect/understand/backup-and-recovery).

**Teste a atualização de base de dados numa cópia da cópia de segurança de base de dados site mais recente:** Antes de atualizar um site de administração central do System Center Configuration Manager ou o site primário, teste o processo de atualização de base de dados de site numa cópia da base de dados do site.

-   Recomendamos que teste o processo de atualização de base de dados de site porque, quando atualizar um site, a base de dados do site pode ser modificado.

-   Embora o teste da atualização da base de dados não seja necessário, poderá identificar potenciais problemas na atualização antes da base de dados de produção é afetada.

-   Uma atualização de base de dados do site que falhou pode inoperacional a base de dados do site e poderá requerer uma recuperação de site para restaurar a funcionalidade.

-   Embora a base de dados do site seja partilhada entre os sites numa hierarquia, planeie testar a base de dados em cada site aplicável antes de atualizar esse site.

-   Se utilizar réplicas de base de dados para pontos de gestão num site primário, desative a replicação antes de criar cópias de segurança da base de dados do site.

O Configuration Manager não suporta a cópia de segurança de sites secundários nem suporta o teste da atualização de uma base de dados do site secundário.

Não execute um teste de atualização de base de dados na base de dados de site de produção. Tal procedimento atualiza a base de dados do site e pode fazer com que deixe de funcionar. Para obter mais informações, consulte o artigo [passo 2: Teste a atualização de base de dados antes de instalar uma atualização](/sccm/core/servers/manage/install-in-console-updates#bkmk_step2) de **antes de instalar uma atualização na consola**.

**Planear cliente piloting:**   
Quando instala uma atualização que o cliente de atualizações, pode testar essa nova atualização do cliente no pré-produção antes de implementa e atualiza todos os clientes ativos.

Para tirar partido desta opção, tem de configurar o seu site para suportar as atualizações automáticas de pré-produção antes de iniciar a instalação da atualização.

Para obter mais informações, consulte o artigo [atualizar os clientes no System Center Configuration Manager](/sccm/core/clients/manage/upgrade/upgrade-clients) e [como testar as atualizações de cliente numa coleção de pré-produção no System Center Configuration Manager](/sccm/core/clients/manage/upgrade/test-client-upgrades).

**Planear a utilização de janelas de serviço para controlar quando os servidores do site instalam atualizações:**   
Pode utilizar as janelas de serviço para definir um período durante o qual as atualizações para um servidor do site podem ser instaladas.

Isto pode ajudar a controlar quando os sites na hierarquia instalam a atualização. Antes da versão 1606, windows serviço foram chamados janelas de manutenção. Para obter mais informações, consulte o artigo [windows dos servidores do site do serviço](/sccm/core/servers/manage/service-windows).

**Execute o Verificador de pré-requisitos do programa de configuração:**   
Se a atualização estiver listada na consola do como **disponível,** independentemente pode executar o Verificador de pré-requisitos antes de instalar a atualização. (Quando instala a atualização do site, o Verificador de pré-requisitos será novamente executado.)

Para executar uma verificação de pré-requisitos a partir da consola, aceda a **administração > Descrição geral > Serviços em nuvem > atualizações e a manutenção.** Em seguida, faça duplo clique **pacote de atualização do Configuration Manager 1610**e, em seguida, escolha **executar verificação de pré-requisitos**.

Para obter mais informações sobre como iniciar e, em seguida, monitorizar a verificação dos pré-requisitos, consulte o artigo **passo 3: Executar o Verificador de pré-requisitos antes de instalar uma atualização** no tópico [instalar as atualizações na consola do System Center Configuration Manager](/sccm/core/servers/manage/install-in-console-updates).

> [!IMPORTANT]  
> Quando o Verificador de pré-requisitos é executada forma independente ou como parte de uma instalação de atualização, o processo atualizará alguns ficheiros de origem do produto que são utilizados para tarefas de manutenção do site. Por conseguinte, depois de executar o Verificador de pré-requisitos, mas antes a instalar a atualização 1610, se precisar de efetuar uma tarefa de manutenção do site, executar **Setupwpf.exe** (programa de configuração do Configuration Manager) a partir do CD. Pasta mais recente no servidor do site.

**Atualizar sites:**   
Agora está pronto para iniciar a instalação da atualização para a sua hierarquia. Para obter mais informações sobre como instalar a atualização, consulte o artigo [instalar atualizações na consola.](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates)

Recomendamos que planeie instalar a atualização fora do horário comercial normal para cada site, quando o processo de instalação da atualização e as respetivas ações para reinstalar os componentes do site e funções de sistema de sites terão o efeito, pelo menos, nas suas operações de negócio.

Para obter mais informações, veja [Atualizações para o System Center Configuration Manager](/sccm/core/servers/manage/updates).

