---
title: Lista de verificação para a versão 1602
titleSuffix: Configuration Manager
description: Saiba mais sobre as ações a efetuar antes de atualizar do System Center Configuration Manager versão 1511 para a versão 1602.
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: b63ef197-01f0-4894-b929-5ef8403c5195
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: ecefbaa7de198992ad68c3942fd25311515e4118
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/24/2019
ms.locfileid: "54897760"
---
# <a name="checklist-for-installing-update-1602-for-system-center-configuration-manager"></a>Lista de verificação para instalar a atualização 1602 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Antes de atualizar do System Center Configuration Manager versão 1511 para a versão 1602, reveja as seguintes informações e lista de verificação para ações a efetuar antes de iniciar a atualização.  

 **Sobre a instalação da atualização 1602:**  

 A atualização 1602 só pode ser instalada no site de nível superior da sua hierarquia. Isto significa que inicia a instalação do seu site de administração central, se tiver uma, ou a partir de seu site primário autónomo.  

-   Os sites primários subordinados instalam a atualização automaticamente após a conclusão do site de administração central instalar a atualização. Pode utilizar janelas de manutenção para controlar quando um site instala as atualizações. A partir da versão da atualização 1602, janelas de manutenção foram renomeadas *janelas de manutenção*. Para obter mais informações, consulte [manutenção do windows para servidores de site](/sccm/core/servers/manage/service-windows).  

-   Tem de atualizar manualmente sites secundários a partir da consola do Configuration Manager após a conclusão do site principal primário instalar a atualização. As atualizações automáticas dos servidores de site secundário não são suportadas.  

Quando o servidor do site instala a atualização, as funções de sistema de sites que estão instaladas no servidor do site e os que são instaladas automaticamente em computadores remotos for atualizadas. Por conseguinte, antes de instalar a atualização, certifique-se de que cada servidor de sistema de sites cumpre os novos pré-requisitos para operações com a nova versão de atualização.  

Na primeira vez que utiliza uma consola do Configuration Manager após a atualização foi concluída, será solicitado que Atualize a consola. Para tal, tem de executar a configuração do Configuration Manager no computador que aloja a consola e escolha a opção para atualizar a consola. Recomendamos que não adie a instalação da atualização na consola.  

 **Lista de verificação:**  

 **Certifique-se de que todos os sites executam uma versão suportada do System Center Configuration Manager:**  Cada servidor do site na hierarquia tem de executar o System Center Configuration Manager versão 1511, antes de poder iniciar a instalação da atualização 1602.  

 **Rever instaladas as versões de Microsoft .NET nos servidores do sistema de sites:** Quando um site instala a atualização 1602, o Configuration Manager instala automaticamente o .NET Framework 4.5.2 em cada computador que aloja uma das seguintes funções do sistema de site (se o .NET Framework 4.5 ou posterior não estiver já instalado):  

-   Ponto proxy de registo  

-   Ponto de inscrição  

-   Ponto de gestão  

-   Ponto de ligação de serviço  

Esta instalação pode colocar o servidor de sistema de sites num reinício pendente estado e relatório de erros para o Visualizador de estado do componente do Configuration Manager. Além disso, as aplicações de .NET no servidor de podem ocorrer falhas aleatórias até que o servidor seja reiniciado.  

 Para obter mais informações, veja [Pré-requisitos de site e sistema de sites](../../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

 **Analise o estado do site e da hierarquia e certifique-se de que não existem não existem problemas por resolver:** Antes de atualizar um site, resolva todos os problemas operacionais do servidor do site, o servidor de base de dados do site e funções de sistema de sites que são instaladas em computadores remotos. Uma atualização de site pode falhar devido a problemas operacionais existentes.  

Para obter mais informações, veja [Utilizar alertas e o sistema de estado para o System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

 **Reveja os replicação de ficheiros e dados entre sites:**  Certifique-se esse ficheiro e a replicação de base de dados entre sites está operacional e atualizada. Atrasos ou registos de segurança em qualquer um podem impedir que uma atualização uniforme e bem-sucedida.    

Para a replicação de base de dados, pode utilizar o Analisador de Ligações de Replicação para ajudar a resolver problemas antes de iniciar a atualização.    

 Para obter mais informações, consulte [sobre o analisador de ligações de replicação](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_RLA) no [monitorizar a infraestrutura hierarquia e replicação no System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) tópico.  

 **Instale todas as atualizações críticas aplicáveis para sistemas operativos em computadores que alojam o site, o servidor de base de dados do site e funções de sistema de sites remoto:** Antes de instalar uma atualização para o Configuration Manager, instale quaisquer atualizações críticas para cada sistema de sites aplicável. Se uma atualização que instalar necessitar de um reinício, reinicie os computadores aplicáveis antes de iniciar a atualização.  

 **Desative réplicas de base de dados para pontos de gestão em sites primários:** O Configuration Manager não é possível atualizar com êxito um site primário que tenha uma réplica de base de dados para pontos de gestão ativada. Desative a replicação de base de dados antes de:  

-   Crie uma cópia de segurança da base de dados do site para testar a atualização da base de dados.  

-   Instale uma atualização para o Configuration Manager.  

Para obter mais informações, consulte [Database replicas para pontos de gestão do System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

 **Reconfigure os pontos de atualização de software que utilizem NLB:** O Configuration Manager não é possível atualizar um site que utiliza um cluster de balanceamento de carga na rede (NLB) para alojar pontos de atualização de software.  Se utilizar NLB clusters para pontos de atualização de software, utilize o Windows PowerShell para remover o cluster NLB.    

 Para obter mais informações, veja [Planear atualizações de software no System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).  

 **Desative todas as tarefas de manutenção do site em cada site durante a instalação da atualização nesse site:** Antes de instalar atualizações, desative as tarefas de manutenção do site que possam ser executadas durante o tempo que o processo de atualização estiver ativo. Estas tarefas incluem (mas não se limitam) para o seguinte:  

-   Servidor do Site de Reserva  

-   Eliminar Operações de Cliente Desatualizadas  

-   Eliminar Dados de Deteção Desatualizados  

Quando uma tarefa de manutenção da base de dados do site é executada durante a instalação da atualização, a instalação da atualização pode falhar. Antes de desativar uma tarefa, registe o agendamento da tarefa para que possa restaurar a respetiva configuração uma vez concluída a atualização do site.  

 Para obter mais informações, consulte [tarefas de manutenção para o System Center Configuration Manager](../../../core/servers/manage/maintenance-tasks.md) e [tarefas de manutenção para o System Center Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md). 

**Pare temporariamente a qualquer software antivírus em servidores do System Center Configuration Manager:** Antes de atualizar um site, certifique-se de que parou o software antivírus em servidores do Configuration Manager. <!--SMS.503481--> 

 **Crie uma cópia de segurança da base de dados do site no site de administração central e sites primários:** Antes de atualizar um site, cópia de segurança da base de dados do site para se certificar de que tem uma cópia de segurança para recuperação após desastre.   

Para obter mais informações, consulte [cópia de segurança e recuperação para o System Center Configuration Manager](../../../protect/understand/backup-and-recovery.md).  

 **Cópia de segurança um ficheiro Configuration MOF personalizado:** Se utilizar um ficheiro Configuration MOF personalizado para definir as classes de dados que utiliza com o inventário de hardware, crie uma cópia de segurança deste ficheiro antes de atualizar o site. Após a atualização, restaure este ficheiro para o seu site do versão 1602. Quando atualizar um site, o ficheiro atual é substituído com a versão (predefinição) original do ficheiro. Para obter mais informações sobre como utilizar este ficheiro, consulte [como expandir o inventário de hardware no System Center Configuration Manager](../../../core/clients/manage/inventory/extend-hardware-inventory.md).  

 **Teste a atualização de base de dados numa cópia da cópia de segurança de base de dados site mais recente:** Antes de atualizar um site de administração central do System Center Configuration Manager ou o site primário, teste o processo de atualização de base de dados de site numa cópia da base de dados do site.  

-   Deve testar o processo de atualização de base de dados de site porque, quando atualizar um site, a base de dados pode ser modificado.  

-   Embora não seja necessária uma atualização da base de dados de teste, poderá identificar potenciais problemas na atualização antes de sua base de dados de produção é afetado.  

-   Uma atualização de base de dados do site em falha pode processar o seu banco de dados do site inoperável e pode exigir uma recuperação de site para restaurar a funcionalidade.  

-   Embora a base de dados do site seja partilhada entre sites numa hierarquia, planeie o teste da base de dados em cada site aplicável antes de atualizar esse site.  

-   Se utilizar réplicas de base de dados para pontos de gestão num site primário, desative a replicação antes de criar a cópia de segurança da base de dados do site.  

O Configuration Manager não suporta a cópia de segurança de sites secundários nem suporta o teste de atualização de uma base de dados do site secundário.   
Não execute um teste de atualização da base de dados na base de dados de site de produção. Tal procedimento atualiza a base de dados do site e pode fazer com que deixe de funcionar. Para obter mais informações, consulte [passo 2: Testar a atualização da base de dados antes de instalar uma atualização](/sccm/core/servers/manage/install-in-console-updates#bkmk_step2) partir **antes de instalar uma atualização na consola**.  

 **Planear a criação de pilotos de cliente:** Quando instala uma atualização que atualiza o cliente, pode testar essa nova atualização de cliente em pré-produção antes de implementar e atualizar todos os clientes ativos.   

 Para tirar partido desta opção, tem de configurar o seu site para suportar as atualizações automáticas para pré-produção antes de iniciar a instalação da atualização. Para obter mais informações, veja [Atualização dos clientes no System Center Configuration Manager](../../../core/clients/manage/upgrade/upgrade-clients.md) e   
[Como testar as atualizações de cliente numa coleção de pré-produção no System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

 **Plano para utilizar janelas de manutenção para controlar quando os servidores do site instalam atualizações:** Pode utilizar as janelas de manutenção para definir um período de tempo durante o qual as atualizações ao servidor do site podem ser instaladas. Isto pode ajudar a controlar quando os sites na hierarquia instalam a atualização.   

A partir da versão da atualização 1602, janelas de manutenção foram renomeadas *janelas de manutenção*. Para obter mais informações, consulte [manutenção do windows para servidores de site](/sccm/core/servers/manage/service-windows).  

 **Execute o Verificador de pré-requisitos de configuração:**  Antes de instalar a atualização 1602, pode executar o Verificador de pré-requisitos independentemente da instalação da atualização. Quando instalar a atualização no site, o Verificador de pré-requisitos é executado novamente.  

Para obter mais informações, consulte **passo 3: Executar o Verificador de pré-requisitos antes de instalar uma atualização** no [atualiza para o System Center Configuration Manager](../../../core/servers/manage/updates.md) tópico.  

> [!IMPORTANT]  
>  Quando o Verificador de pré-requisitos é executado independentemente ou como parte de uma instalação de atualização, o processo atualiza alguns ficheiros de origem do produto que são utilizados para tarefas de manutenção do site. Por conseguinte, depois de executar o Verificador de pré-requisitos, mas antes a instalar a atualização 1602, se tiver de realizar uma tarefa de manutenção do site, execute **Setupwfe.exe** (configuração do Configuration Manager) partir do CD. Pasta mais recente no servidor do site.  

 **Atualizar sites:** Agora está pronto para iniciar a instalação de atualização para a sua hierarquia. Recomendamos que planeie instalar a atualização fora do horário comercial normal para cada site, quando o processo de instalação da atualização e respetivas ações para reinstalar os componentes do site e as funções de sistema de sites irão ter o mínimo efeito nas operações comerciais.

Para obter mais informações, veja [Atualizações para o System Center Configuration Manager](../../../core/servers/manage/updates.md).  

## <a name="see-also"></a>Consulte também  
 [Atualizações para o System Center Configuration Manager](../../../core/servers/manage/updates.md)
