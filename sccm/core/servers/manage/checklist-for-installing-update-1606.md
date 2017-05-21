---
title: "Lista de verificação para 1606 | Documentos do Microsoft"
description: "Saiba mais sobre as ações a efetuar antes de atualizar a partir do System Center Configuration Manager versão 1511 ou 1602 para versão 1606."
ms.custom: na
ms.date: 2/7/2017
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
ms.sourcegitcommit: 30af3326578d39c6d995672071705bcaeb877e4d
ms.openlocfilehash: b0def6eb962d243a7ea5910b8d56bbb448b3a2e4
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="checklist-for-installing-update-1606-for-system-center-configuration-manager"></a>Lista de verificação para instalar a atualização 1606 para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Versão 1606 para ramificação atual do System Center Configuration Manager é uma atualização que pode utilizar para atualizar a partir da versão 1511 ou 1602.

Antes de instalar a versão 1606 como uma atualização, reveja as seguintes informações e lista de verificação para ações a efetuar antes de iniciar a atualização.

Para obter informações sobre as versões do plano base, consulte o artigo [versões de linha de base e atualização](../../../core/servers/manage/updates.md#bkmk_Baselines) no [atualizações para o System Center Configuration Manager](../../../core/servers/manage/updates.md).

 ## <a name="about-installing-update-1606"></a>Sobre a instalação de atualização 1606

Como um *atualizar*, 1606 apenas podem ser instaladas no site de nível superior da hierarquia. Isto significa iniciar a instalação do seu site de administração central, se tiver um, ou a partir do seu site primário autónomo.  

-   Os sites primários subordinados instalam automaticamente a atualização após a conclusão da instalação da atualização do site de administração central. Pode utilizar janelas de serviço para controlar quando um site instala as atualizações. Antes da versão 1606, windows serviço foram chamados janelas de manutenção. Para obter mais informações, consulte o artigo [windows dos servidores do site do serviço](/sccm/core/servers/manage/service-windows).  

-   Tem de atualizar manualmente os sites secundários a partir da consola do Configuration Manager após a conclusão da instalação da atualização do site primário principal. A atualização automática dos servidores de site secundários não é suportada.  

Quando o servidor do site instala a atualização, funções de sistema de sites que estão instaladas no servidor do site e os que são instaladas em computadores remotos atualizadas automaticamente. Por conseguinte, antes de instalar a atualização, certifique-se de que cada servidor de sistema de sites cumpre os novos pré-requisitos para as operações com a nova versão de atualização.  

A primeira vez que utiliza uma consola do Configuration Manager após a atualização foi instalada, será solicitado para atualizar a consola.  Para tal, tem de executar a configuração do Configuration Manager no computador que aloja a consola e, em seguida, escolha a opção para atualizar a consola. Recomendamos que não adie a instalação da atualização na consola.

 **Problemas conhecidos para esta atualização**   
  Os problemas seguintes aplicam-se quando visualiza o estado de instalação do pacote de atualização:
  - Ao atualizar a partir da versão 1602 para 1606, o passo **payload do pacote de atualização de extração** apresenta o estado **não iniciado**, mesmo que a transferência foi concluída.
  - Ao atualizar a partir da versão 1511 para 1606, alguns passos mostram um Estado de **concluído** mas não será apresentado um valor para **hora da última atualização**.


## <a name="checklist"></a>Lista de verificação  

 **Certifique-se de que todos os sites executem uma versão suportada do System Center Configuration Manager:**  Antes de iniciar a instalação da atualização 1606, cada servidor de site na hierarquia tem de executar a mesma versão do System Center Configuration Manager: qualquer uma das versões 1511 ou 1602.

 **Rever instaladas Microsoft.NET versões em servidores de sistema de sites:** Quando instala um site atualização 1606, Configuration Manager instala automaticamente o .NET Framework 4.5.2 em cada computador que aloja uma das seguintes funções do sistema de sites (se o .NET Framework 4.5 ou posterior não está já instalada):  

-   Ponto proxy de registo  

-   Ponto de inscrição  

-   Ponto de gestão  

-   Ponto de ligação de serviço  

Esta instalação pode colocar o servidor de sistema de sites num reinício pendente estado e o relatório de erros para o Visualizador de estado do componente do Configuration Manager. Além disso, as aplicações .NET no servidor podem ter falhas aleatórias até que o servidor seja reiniciado.  

 Para mais informações consulte [Site e os pré-requisitos de sistema de site](../../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

 **Rever o estado de site e da hierarquia e certifique-se de que não existem sem problemas por resolver:** Antes de atualizar um site, resolva todos os problemas operacionais do servidor do site, o servidor de base de dados do site e funções de sistema de sites que estão instaladas em computadores remotos. Uma atualização de site pode falhar devido a problemas operacionais existentes.

 Para obter mais informações, veja [Utilizar alertas e o sistema de estado para o System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

 **Reveja o ficheiro e dados de replicação entre sites:**  Certifique-se esse ficheiro e a replicação de base de dados entre sites é operacional e atual. Atrasos ou os registos de segurança no podem impedir que uma atualização suave, com êxito.    

Para a replicação de base de dados, pode utilizar o Analisador de Ligações de Replicação para ajudar a resolver problemas antes de iniciar a atualização. Para obter mais informações, consulte o artigo [sobre o analisador de ligações de replicação](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_RLA) no tópico [monitorizar a infraestrutura hierarquia e replicação no System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md).  

 **Instale todas as atualizações críticas aplicáveis a sistemas operativos em computadores que alojam o site, o servidor de base de dados de sites e funções do sistema de sites remoto:** Antes de instalar uma atualização para o Configuration Manager, instale as atualizações críticas em cada sistema de sites aplicável. Se uma atualização que instalar necessitar de um reinício, reinicie os computadores aplicáveis antes de iniciar a atualização.  

 **Desative as réplicas de base de dados para pontos de gestão em sites primários:** O Configuration Manager não é possível atualizar com êxito um site primário que tenha uma réplica de base de dados para pontos de gestão ativada. Desative a replicação de base de dados antes de:  

-   Crie uma cópia de segurança da base de dados do site para testar a atualização de base de dados.  

-   Instale uma atualização para o Configuration Manager.  

Para obter mais informações, consulte o artigo [da base de dados réplicas para pontos de gestão do System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

 **Definir grupos de Disponibilidade AlwaysOn do SQL Server para ativação pós-falha manual:**  
 Antes de instalar atualizações, tais como versão 1606, certifique-se de que o grupo de disponibilidade está configurado para ativação pós-falha manual. Após ter sido atualizado o site, pode restaurar a ativação pós-falha para ser automática. Para obter mais informações, consulte o artigo [SQL Server AlwaysOn numa base de dados do site](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

 **Reconfigure os pontos de atualização de software que utilizem NLBs:** O Configuration Manager não é possível atualizar um site que utiliza um cluster de balanceamento de carga na rede (NLB) para alojar pontos de atualização de software.  

Se utilizar clusters de NLB para pontos de atualização de software, utilize o Windows PowerShell para remover o cluster NLB.    

 Para obter mais informações, veja [Planear atualizações de software no System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).  

 **Desative todas as tarefas de manutenção do site em cada site durante a instalação da atualização nesse site:** Antes de instalar a atualização, desative as tarefas de manutenção do site que poderão ser executado durante o tempo que o processo de atualização estiver ativo. Estas incluem as seguintes, entre outras:  

-   Servidor do Site de Reserva  

-   Eliminar Operações de Cliente Desatualizadas  

-   Eliminar Dados de Deteção Desatualizados  

Quando uma tarefa de manutenção da base de dados do site é executada durante a instalação da atualização, a instalação da atualização pode falhar. Antes de desativar uma tarefa, registe a agenda da tarefa para que possa restaurar a respetiva configuração após a atualização foi instalada.  

Para obter mais informações, consulte o artigo [tarefas de manutenção para o System Center Configuration Manager](../../../core/servers/manage/maintenance-tasks.md) e [referência para a manutenção de tarefas para o System Center Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md).  

 **Crie uma cópia de segurança da base de dados do site no site de administração central e sites primários:** Antes de atualizar um site, criar uma cópia de segurança da base de dados do site para se certificar de que tem uma cópia de segurança a utilizar para recuperação após desastre.   

Para obter mais informações, consulte o artigo [cópia de segurança e recuperação para o System Center Configuration Manager](../../../protect/understand/backup-and-recovery.md).  


 **Teste a atualização de base de dados numa cópia da cópia de segurança de base de dados site mais recente:** Antes de atualizar um site de administração central do System Center Configuration Manager ou o site primário, teste o processo de atualização de base de dados de site numa cópia da base de dados do site.  

-   Deve testar o processo de atualização de base de dados de site porque, quando atualizar um site, a base de dados do site pode ser modificado.  

-   Embora o teste da atualização da base de dados não seja necessário, poderá identificar potenciais problemas na atualização antes da base de dados de produção é afetada.  

-   Uma atualização de base de dados do site que falhou pode inoperacional a base de dados do site e poderá requerer uma recuperação de site para restaurar a funcionalidade.  

-   Embora a base de dados do site seja partilhada entre os sites numa hierarquia, planeie testar a base de dados em cada site aplicável antes de atualizar esse site.  

-   Se utilizar réplicas de base de dados para pontos de gestão num site primário, desative a replicação antes de criar cópias de segurança da base de dados do site.  

O Configuration Manager não suporta a cópia de segurança de sites secundários nem suporta o teste da atualização de uma base de dados do site secundário.   

Não execute um teste de atualização de base de dados na base de dados de site de produção. Tal procedimento atualiza a base de dados do site e pode fazer com que deixe de funcionar. Para obter mais informações, para obter mais informações, consulte o artigo [passo 2: Teste a atualização de base de dados antes de instalar uma atualização](/sccm/core/servers/manage/install-in-console-updates#bkmk_step2) de **antes de instalar uma atualização na consola**.

 **Planear cliente piloting:** Quando instala uma atualização que o cliente de atualizações, pode testar essa nova atualização do cliente no pré-produção antes de implementa e atualiza todos os clientes ativos.   

 Para tirar partido desta opção, antes de iniciar a instalação da atualização, tem de configurar o seu site para suportar as atualizações automáticas de pré-produção. Para obter mais informações, veja [Atualização dos clientes no System Center Configuration Manager](../../../core/clients/manage/upgrade/upgrade-clients.md) e   
[Como testar as atualizações de cliente numa coleção de pré-produção no System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

 **Planear a utilização de janelas de serviço para controlar quando os servidores do site instalam atualizações:** Pode utilizar as janelas de serviço para definir um período durante o qual as atualizações para um servidor do site podem ser instaladas.

Isto pode ajudar a controlar quando os sites na hierarquia instalam a atualização.
Antes da versão 1606, windows serviço foram chamados janelas de manutenção. Para obter mais informações, consulte o artigo [windows dos servidores do site do serviço](/sccm/core/servers/manage/service-windows).  

 **Execute Verificador de pré-requisitos do programa de configuração:**  Antes de instalar a atualização 1606, pode executar o Verificador de pré-requisitos independentemente da instalação da atualização. Quando instala a atualização do site, o Verificador de pré-requisitos será novamente executado.  

Para obter mais informações, consulte o artigo **passo 3: Executar o Verificador de pré-requisitos antes de instalar uma atualização** no [atualizações para o System Center Configuration Manager](../../../core/servers/manage/install-in-console-updates.md) tópico.  

> [!IMPORTANT]  
>  Quando o Verificador de pré-requisitos é executada forma independente ou como parte de uma instalação de atualização, o processo atualizará alguns ficheiros de origem do produto que são utilizados para tarefas de manutenção do site. Por conseguinte, depois de executar o Verificador de pré-requisitos, mas antes a instalar a atualização 1606, se precisar de efetuar uma tarefa de manutenção do site, executar **Setupwpf.exe** (programa de configuração do Configuration Manager) a partir do CD. Pasta mais recente no servidor do site.  

 **Atualizar sites:** Agora está pronto para iniciar a instalação da atualização para a sua hierarquia.  
  Recomendamos que planeie instalar a atualização fora do horário comercial normal para cada site, quando o processo de instalação da atualização e as respetivas ações para reinstalar os componentes do site e funções de sistema de sites terão o efeito, pelo menos, nas suas operações de negócio.

Para obter mais informações, veja [Atualizações para o System Center Configuration Manager](../../../core/servers/manage/updates.md).  

