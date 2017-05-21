---
title: "Lista de verificação para 1602 | Documentos do Microsoft"
description: "Saiba mais sobre as ações a efetuar antes de atualizar a partir do System Center Configuration Manager versão 1511 para versão 1602."
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b63ef197-01f0-4894-b929-5ef8403c5195
caps.latest.revision: 13
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: NOINDEX, NOFOLLOW
ms.translationtype: Machine Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 3e0de56b7a592b105e6a61b3d6654b1d0142584d
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="checklist-for-installing-update-1602-for-system-center-configuration-manager"></a>Lista de verificação para instalar a atualização 1602 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Antes de atualizar a partir do System Center Configuration Manager versão 1511 para versão 1602, reveja as seguintes informações e lista de verificação para ações a efetuar antes de iniciar a atualização.  

 **Sobre a instalação da atualização 1602:**  

 A atualização 1602 só pode ser instalada no site de nível superior da sua hierarquia. Isto significa iniciar a instalação do seu site de administração central, se tiver um, ou a partir do seu site primário autónomo.  

-   Os sites primários subordinados instalam automaticamente a atualização após a conclusão da instalação da atualização do site de administração central. Pode utilizar janelas de manutenção para controlar quando um site instala as atualizações. Iniciar com o lançamento da atualização 1602, janelas de manutenção tem o nome foi mudadas *service windows*. Para obter mais informações, consulte o artigo [windows dos servidores do site do serviço](/sccm/core/servers/manage/service-windows).  

-   Tem de atualizar manualmente os sites secundários a partir da consola do Configuration Manager após a conclusão da instalação da atualização do site primário principal. As atualizações automáticas dos servidores de site secundário não são suportadas.  

Quando o servidor do site instala a atualização, funções de sistema de sites que estão instaladas no servidor do site e os que são instaladas em computadores remotos automaticamente atualizadas. Por conseguinte, antes de instalar a atualização, certifique-se de que cada servidor de sistema de sites cumpre os novos pré-requisitos para as operações com a nova versão de atualização.  

A primeira vez que utiliza uma consola do Configuration Manager após a atualização estiver concluída, será solicitado para atualizar a consola. Para tal, tem de executar a configuração do Configuration Manager no computador que aloja a consola e escolha a opção para atualizar a consola. Recomendamos que não adie a instalação da atualização na consola.  

 **Lista de verificação:**  

 **Certifique-se de que todos os sites executem uma versão suportada do System Center Configuration Manager:**  Cada servidor do site na hierarquia tem de executar o System Center Configuration Manager versão 1511 antes de poder iniciar a instalação da atualização 1602.  

 **Rever instalado versões do Microsoft .NET em servidores do sistema de sites:** Quando instala um site atualização 1602, Configuration Manager instala automaticamente o .NET Framework 4.5.2 em cada computador que aloja uma das seguintes funções do sistema de sites (se o .NET Framework 4.5 ou posterior não está já instalada):  

-   Ponto proxy de registo  

-   Ponto de inscrição  

-   Ponto de gestão  

-   Ponto de ligação de serviço  

Esta instalação pode colocar o servidor de sistema de sites num reinício pendente estado e erros de relatório para o Visualizador de estado do componente do Configuration Manager. Além disso, aplicações de .NET no servidor podem ocorrer falhas aleatórias até que o servidor é reiniciado.  

 Para obter mais informações, veja [Pré-requisitos de site e sistema de sites](../../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

 **Rever o estado de site e da hierarquia e certifique-se de que não existem sem problemas por resolver:** Antes de atualizar um site, resolva todos os problemas operacionais do servidor do site, o servidor de base de dados do site e funções de sistema de sites que estão instaladas em computadores remotos. Uma atualização de site pode falhar devido a problemas operacionais existentes.  

Para obter mais informações, veja [Utilizar alertas e o sistema de estado para o System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

 **Reveja o ficheiro e dados de replicação entre sites:**  Certifique-se esse ficheiro e a replicação de base de dados entre sites é operacional e atual. Atrasos ou os registos de segurança no podem impedir que uma atualização suave, com êxito.    

Para a replicação de base de dados, pode utilizar o Analisador de Ligações de Replicação para ajudar a resolver problemas antes de iniciar a atualização.    

 Para obter mais informações, consulte o artigo [sobre o analisador de ligações de replicação](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_RLA) no [monitorizar a infraestrutura hierarquia e replicação no System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) tópico.  

 **Instale todas as atualizações críticas aplicáveis a sistemas operativos em computadores que alojam o site, o servidor de base de dados de sites e funções do sistema de sites remoto:** Antes de instalar uma atualização para o Configuration Manager, instale as atualizações críticas em cada sistema de sites aplicável. Se uma atualização que instalar necessitar de um reinício, reinicie os computadores aplicáveis antes de iniciar a atualização.  

 **Desative as réplicas de base de dados para pontos de gestão em sites primários:** O Configuration Manager não é possível atualizar com êxito um site primário que tenha uma réplica de base de dados para pontos de gestão ativada. Desative a replicação de base de dados antes de:  

-   Crie uma cópia de segurança da base de dados do site para testar a atualização de base de dados.  

-   Instale uma atualização para o Configuration Manager.  

Para obter mais informações, consulte o artigo [da base de dados réplicas para pontos de gestão do System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

 **Reconfigure os pontos de atualização de software que utilizem NLBs:** O Configuration Manager não é possível atualizar um site que utiliza um cluster de balanceamento de carga na rede (NLB) para alojar pontos de atualização de software.  Se utilizar clusters de NLB para pontos de atualização de software, utilize o Windows PowerShell para remover o cluster NLB.    

 Para obter mais informações, veja [Planear atualizações de software no System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).  

 **Desative todas as tarefas de manutenção do site em cada site durante a instalação da atualização nesse site:** Antes de instalar atualizações, desative as tarefas de manutenção do site que possam ser executadas enquanto o que o processo de atualização estiver ativo. Estas tarefas incluem (mas não se limitando) para o seguinte:  

-   Servidor do Site de Reserva  

-   Eliminar Operações de Cliente Desatualizadas  

-   Eliminar Dados de Deteção Desatualizados  

Quando uma tarefa de manutenção da base de dados do site é executada durante a instalação da atualização, a instalação da atualização pode falhar. Antes de desativar uma tarefa, registe o agendamento da tarefa para que possa restaurar a respetiva configuração uma vez concluída a atualização do site.  

 Para obter mais informações, consulte o artigo [tarefas de manutenção para o System Center Configuration Manager](../../../core/servers/manage/maintenance-tasks.md) e [referência para a manutenção de tarefas para o System Center Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md).  

 **Crie uma cópia de segurança da base de dados do site no site de administração central e sites primários:** Antes de atualizar um site, cópia de segurança da base de dados do site para se certificar de que tem uma cópia de segurança a utilizar para recuperação após desastre.   

Para obter mais informações, consulte o artigo [cópia de segurança e recuperação para o System Center Configuration Manager](../../../protect/understand/backup-and-recovery.md).  

 **Um ficheiro de Configuration.mof personalizado de cópia de segurança:** Se utilizar um ficheiro de Configuration.mof personalizado para definir as classes de dados que utiliza com o inventário de hardware, crie uma cópia de segurança deste ficheiro antes de atualizar o site. Após a atualização, ao restaure este ficheiro para o seu site de 1602 de versão. Ao atualizar um site, o ficheiro atual é substituído com a versão (predefinição) original do ficheiro. Para obter mais informações sobre como utilizar este ficheiro, consulte o artigo [como expandir o inventário de hardware no System Center Configuration Manager](../../../core/clients/manage/inventory/extend-hardware-inventory.md).  

 **Teste a atualização de base de dados numa cópia da cópia de segurança de base de dados site mais recente:** Antes de atualizar um site de administração central do System Center Configuration Manager ou o site primário, teste o processo de atualização de base de dados de site numa cópia da base de dados do site.  

-   Deve testar o processo de atualização de base de dados de site porque, quando atualizar um site, a base de dados do site pode ser modificado.  

-   Embora o teste da atualização da base de dados não seja necessário, poderá identificar potenciais problemas na atualização antes da base de dados de produção é afetada.  

-   Uma atualização de base de dados do site que falhou pode inoperacional a base de dados do site e poderá requerer uma recuperação de site para restaurar a funcionalidade.  

-   Embora a base de dados do site seja partilhada entre os sites numa hierarquia, planeie testar a base de dados em cada site aplicável antes de atualizar esse site.  

-   Se utilizar réplicas de base de dados para pontos de gestão num site primário, desative a replicação antes de criar cópias de segurança da base de dados do site.  

O Configuration Manager não suporta a cópia de segurança de sites secundários nem suporta o teste da atualização de uma base de dados do site secundário.   
Não execute um teste de atualização de base de dados na base de dados de site de produção. Tal procedimento atualiza a base de dados do site e pode fazer com que deixe de funcionar. Para obter mais informações, consulte o artigo [passo 2: Teste a atualização de base de dados antes de instalar uma atualização](/sccm/core/servers/manage/install-in-console-updates#bkmk_step2) de **antes de instalar uma atualização na consola**.  

 **Planear cliente piloting:** Quando instala uma atualização que o cliente de atualizações, pode testar essa nova atualização do cliente no pré-produção antes de implementa e atualiza todos os clientes ativos.   

 Para tirar partido desta opção, tem de configurar o seu site para suportar as atualizações automáticas de pré-produção antes de iniciar a instalação da atualização. Para obter mais informações, veja [Atualização dos clientes no System Center Configuration Manager](../../../core/clients/manage/upgrade/upgrade-clients.md) e   
[Como testar as atualizações de cliente numa coleção de pré-produção no System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

 **Planear a utilização de janelas de manutenção para controlar quando os servidores do site instalam atualizações:** Pode utilizar as janelas de manutenção para definir um período de tempo durante o qual as atualizações ao servidor do site podem ser instaladas. Isto pode ajudar a controlar quando os sites na hierarquia instalam a atualização.   

Iniciar com o lançamento da atualização 1602, janelas de manutenção tem o nome foi mudadas *service windows*. Para obter mais informações, consulte o artigo [windows dos servidores do site do serviço](/sccm/core/servers/manage/service-windows).  

 **Execute Verificador de pré-requisitos do programa de configuração:**  Antes de instalar a atualização 1602, pode executar o Verificador de pré-requisitos independentemente da instalação da atualização. Quando instala a atualização do site, o Verificador de pré-requisitos será novamente executado.  

Para obter mais informações, consulte o artigo **passo 3: Executar o Verificador de pré-requisitos antes de instalar uma atualização** no [atualizações para o System Center Configuration Manager](../../../core/servers/manage/updates.md) tópico.  

> [!IMPORTANT]  
>  Quando o Verificador de pré-requisitos é executada forma independente ou como parte de uma instalação de atualização, o processo atualizará alguns ficheiros de origem do produto que são utilizados para tarefas de manutenção do site. Por conseguinte, depois de executar o Verificador de pré-requisitos, mas antes a instalar a atualização 1602, se precisar de efetuar uma tarefa de manutenção do site, executar **Setupwfe.exe** (programa de configuração do Configuration Manager) a partir do CD. Pasta mais recente no servidor do site.  

 **Atualizar sites:** Agora está pronto para iniciar a instalação da atualização para a sua hierarquia. Recomendamos que planeie instalar a atualização fora do horário comercial normal para cada site, quando o processo de instalação da atualização e as respetivas ações para reinstalar os componentes do site e funções de sistema de sites terão o efeito, pelo menos, nas suas operações de negócio.

Para obter mais informações, veja [Atualizações para o System Center Configuration Manager](../../../core/servers/manage/updates.md).  

## <a name="see-also"></a>Consulte também  
 [Atualizações para o System Center Configuration Manager](../../../core/servers/manage/updates.md)

