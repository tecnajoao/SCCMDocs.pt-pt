---
title: Gerir coleções
titleSuffix: Configuration Manager
description: Efetue tarefas no Configuration Manager de coleções comuns.
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e102fd1a-76df-4d8e-b1b0-10ee18318f67
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5d7c967ce02c009cd9659c7956f7ca79f4a34faf
ms.sourcegitcommit: be8c0182db9ef55a948269fcbad7c0f34fd871eb
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/23/2018
ms.locfileid: "42755977"
---
# <a name="how-to-manage-collections-in-configuration-manager"></a>Como gerir coleções no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize as informações de descrição geral neste artigo para ajudar a realizar tarefas de gestão para coleções no Configuration Manager.  

> [!NOTE]  
>  Para obter informações sobre como criar coleções do Configuration Manager, consulte [como criar coleções](/sccm/core/clients/manage/collections/create-collections).  



## <a name="bkmk_device"></a> Como gerir coleções de dispositivos  

 Na área de trabalho **Ativos e Compatibilidade** , selecione **Coleções de Dispositivos**, selecione a coleção que pretende gerir e, em seguida, selecione uma tarefa de gestão.  


#### <a name="show-members"></a>Mostrar membros
 Apresenta todos os recursos que são membros da coleção selecionada num nó temporário sob o nó **Dispositivos** .


#### <a name="add-selected-items"></a>Adicionar itens selecionados
 Fornece as seguintes opções: 

 - **Adicionar itens selecionados à coleção de dispositivos existente**: Abre o **selecionar coleção** caixa de diálogo. Selecione a coleção à qual pretende adicionar os membros da coleção selecionada. A coleção selecionada está incluída nesta coleção, utilizando uma regra de associação **Incluir Coleções** .  

 - **Adicionar itens selecionados à coleção de novos dispositivos**: Abre o **criar Assistente de coleção de dispositivos** onde pode criar uma nova coleção. A coleção selecionada está incluída nesta coleção, utilizando uma regra de associação **Incluir Coleções** .  


 Para obter mais informações, consulte [como criar coleções](/sccm/core/clients/manage/collections/create-collections).


#### <a name="install-client"></a>Instalar cliente
 Abre o **instalar o cliente assistente**. Este assistente utiliza a instalação push do cliente para instalar o cliente do Configuration Manager em todos os computadores na coleção selecionada. Para obter mais informações, consulte [instalação push do cliente](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush).


#### <a name="run-script"></a>Executar Script
 Abre o **executar Script** Assistente para executar um script do PowerShell em todos os clientes na coleção. Para obter mais informações, consulte [criar e executar scripts do PowerShell](/sccm/apps/deploy-use/create-deploy-scripts).


#### <a name="manage-affinity-requests"></a>Gerir pedidos de afinidade
 Abre o **gerir pedidos de afinidade de dispositivo do utilizador** caixa de diálogo. Aprovar ou rejeitar pedidos pendentes para estabelecer afinidades de dispositivo do utilizador para dispositivos na coleção selecionada. Para obter mais informações, consulte [associar utilizadores e dispositivos à afinidade de dispositivo do utilizador](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity)


#### <a name="clear-required-pxe-deployments"></a>Limpar as implementações de PXE necessárias
 Limpa quaisquer implementações de arranque PXE necessárias de todos os membros da coleção selecionada. Para obter mais informações, consulte [utilizar o PXE para implementar o Windows na rede](/sccm/osd/deploy-use/use-pxe-to-deploy-windows-over-the-network).


#### <a name="update-membership"></a>Atualizar associação
 Avalia a associação da coleção selecionada. Para coleções com muitos membros, esta atualização pode demorar algum tempo a concluir. Utilize a ação **Atualizar** para atualizar a apresentação com os novos membros de coleções após a atualização estar concluída.


#### <a name="add-resources"></a>Adicionar recursos
 Abre o **adicionar recursos à coleção** caixa de diálogo. Procurar novos recursos adicionar a coleção selecionada. O ícone para a coleção selecionada mostra um símbolo de ampulheta enquanto a atualização está em curso.


#### <a name="client-notification"></a>Notificação de cliente
 Instrui a todos os clientes na coleção de dispositivos selecionada imediatamente a fazer uma das seguintes ações:

 - **Transferir política do computador**: Atualize a política de dispositivo. Para obter mais informações, consulte [iniciar a obtenção de política para um cliente do Configuration Manager](/sccm/core/clients/manage/manage-clients#BKMK_PolicyRetrieval).  

 - **Transferir política do utilizador**: Atualize a política de utilizador.  

 - **Recolher dados de deteção**: Clientes de Acionador para enviar um registo de dados de deteção (DDR). Para obter mais informações, consulte [deteção de Heartbeat](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutHeartbeat).  

 - **Recolher inventário de Software**: Ciclo de clientes de Acionador a executar um inventário de software. Para obter mais informações, consulte [introdução ao inventário de software](/sccm/core/clients/manage/inventory/introduction-to-software-inventory).  

 - **Recolher inventário de Hardware**: Ciclo de clientes de Acionador a executar um inventário de hardware. Para obter mais informações, consulte [introdução ao inventário de hardware](/sccm/core/clients/manage/inventory/introduction-to-hardware-inventory).  

 - **Avaliar implementações de aplicações**: Ciclo de clientes de Acionador a executar uma edição de avaliação de implementação de aplicação. Para obter mais informações, consulte [agendar reavaliação para implementações](/sccm/core/clients/deploy/about-client-settings#schedule-re-evaluation-for-deployments).  

 - **Avaliar implementações de atualizações de Software**: Ciclo de clientes de Acionador a executar uma avaliação de implementação de atualizações de software. Para obter mais informações, consulte [introdução às atualizações de software](/sccm/sum/understand/software-updates-introduction).  

 - **Mude para o ponto de atualização de Software seguinte**: Ponto de atualização de clientes de Acionador para mudar para o seguinte software disponível. Para obter mais informações, consulte [mudança de ponto de atualização de Software](/sccm/sum/plan-design/plan-for-software-updates#BKMK_SUPSwitching).  

 - **Avaliar atestado de estado de funcionamento do dispositivo**: Acione os clientes do Windows 10 para verificar e enviar o respetivo estado de funcionamento do dispositivo mais recente. Para obter mais informações, consulte [atestado de estado de funcionamento](/sccm/core/servers/manage/health-attestation).  

 - **Verificação de conformidade de acesso condicional**: Clientes de Acionador para verificar a compatibilidade com o acesso condicional. Para obter mais informações, consulte [gerir o acesso aos serviços do O365 para PCs](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm).  


#### <a name="endpoint-protection"></a>Endpoint Protection
 Instrui a todos os clientes na coleção de dispositivos selecionada imediatamente a fazer uma das seguintes ações:

 - **Análise completa**: Acionar o Endpoint Protection ou o Windows Defender para executar uma *completo* análise de antimalware  

 - **Análise rápida**: Acionar o Endpoint Protection ou o Windows Defender para executar uma *Rápido* análise de antimalware  

 - **Transferir definição**: Acionar o Windows Defender ou Endpoint Protection para transferir as definições de antimalware mais recentes  


 Para obter mais informações, consulte [Endpoint Protection no Configuration Manager](/sccm/protect/deploy-use/endpoint-protection).


#### <a name="export"></a>Exportar
 Abre o **Assistente de exportação de coleção** que ajuda a exportar esta coleção para um ficheiro de formato MOF (Managed Object). Este ficheiro, em seguida, pode ser arquivado ou importado noutro site do Configuration Manager. Ao exportar uma coleção, as coleções referenciadas não são exportadas. Uma coleção referenciada é referenciada pela coleção selecionada através da utilização de um **inclusão** ou **excluir** regra.


#### <a name="copy"></a>cópia
 Cria uma cópia da coleção selecionada. A nova coleção utiliza a coleção selecionada como uma coleção restritiva.


#### <a name="refresh"></a>Atualizar
 Atualize a vista.


#### <a name="delete"></a>Eliminar
 Elimina a coleção selecionada. Também pode eliminar todos os recursos na coleção da base de dados do site. 

 Não é possível eliminar as coleções que estão incorporadas no Configuration Manager. Para obter uma lista das coleções incorporadas, consulte [introdução às coleções](/sccm/core/clients/manage/collections/introduction-to-collections#built-in-collections).


#### <a name="simulate-deployment"></a>Simular implementação
 Abre o **simular Assistente de implementação de aplicação**. Este assistente permite-lhe testar os resultados da implementação de uma aplicação sem instalar ou desinstalar a aplicação. Para obter mais informações, consulte [como simular implementações de aplicações](/sccm/apps/deploy-use/simulate-application-deployments).


#### <a name="deploy"></a>Implementar
 Apresenta as seguintes opções:  

 - **Aplicação**: Abre o **Assistente de implementação Software**. Selecione e configure a implementação de uma aplicação para a coleção selecionada. Para obter mais informações, consulte [como implementar aplicações](/sccm/apps/deploy-use/deploy-applications).  

 - **Programa**: Abre o **Assistente de implementação Software**. Selecionar e configurar uma implementação de pacote e programa para a coleção selecionada. Para obter mais informações, consulte [pacotes e programas](/sccm/apps/deploy-use/packages-and-programs).  

 - **Linha de base de configuração**: Abre o **implementar linhas de base de configuração** caixa de diálogo. Configure a implementação de um ou mais linhas base de configuração para a coleção selecionada. Para obter mais informações, consulte [como implementar linhas de base de configuração](/sccm/compliance/deploy-use/deploy-configuration-baselines).  

 - **Sequência de tarefas**: Abre o **Assistente de implementação Software**. Selecionar e configurar uma implementação de sequência de tarefas para a coleção selecionada. Para obter mais informações, consulte [gerir sequências de tarefas para automatizar tarefas](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS).  

 - **Atualizações de software**: Abre o **assistente Deploy Software Updates**. Configure a implementação de atualizações de software para recursos na coleção selecionada. Para obter mais informações, consulte [gerir atualizações de software](/sccm/sum/understand/software-updates-introduction).  


#### <a name="clear-server-group-deployment-locks"></a>Bloqueios de implementação do grupo de servidores de Clear
 Versão manualmente todos os bloqueios de implementação de grupo de servidores para a coleção. Para obter mais informações, consulte [manutenção a um grupo de servidor](/sccm/sum/deploy-use/service-a-server-group).


#### <a name="move"></a>Mover
 Mover a coleção selecionada para outra pasta na **coleções de dispositivos** nó. 


#### <a name="properties"></a>Propriedades
 Para obter mais informações, consulte [propriedades de coleção](#BKMK_CollProp).  



## <a name="bkmk_user"></a> Como gerir coleções de utilizadores  

 Na área de trabalho **Ativos e Compatibilidade** , selecione **Coleções de Utilizadores**, selecione a coleção que pretende gerir e, em seguida, selecione uma tarefa de gestão.  

 > [!Note]  
 > As ações seguintes estão disponíveis em coleções de utilizadores, mas os comportamentos são os mesmos que com coleções de dispositivos. Que eles se aplicam para coleções de utilizadores e os usuários. Para obter mais informações, consulte a ação correspondente sob [como gerir coleções de dispositivos](#bkmk_device).  

 - **Mostrar Membros**  
 - **Adicionar Itens Selecionados**  
     - **Adicionar itens selecionados à coleção de utilizador existente**  
     - **Adicionar itens selecionados à coleção de novos utilizadores**  
 - **Gerir Pedidos de Afinidade**  
 - **Atualizar Associação**  
 - **Adicionar Recursos**  
 - **Exportarar**  
 - **Copiar**  
 - **Atualização**  
 - **Eliminar**  
 - **Simular Implementação**  
 - **Implementar**  
     - **Aplicação**  
     - **Programa**  
     - **Linha de base de configuração**   
 - **Moverr**  
 - **Propriedades**



##  <a name="BKMK_CollProp"></a> Propriedades da coleção  

 Quando abre o **propriedades** caixa de diálogo para uma coleção, ver e configurar as seguintes opções:  

#### <a name="general"></a>Geral
 Ver e configurar informações gerais sobre a coleção selecionada, incluindo o nome da coleção e a coleção restritiva.

#### <a name="membership-rules"></a>Regras de associação
 Configure as regras de associação que definem a associação desta coleção. Para obter mais informações, consulte [como criar coleções](/sccm/core/clients/manage/collections/create-collections).  

#### <a name="power-management"></a>Gestão de Energia
 Configure planos de gestão de energia que atribuir aos computadores na coleção selecionada. Para obter mais informações, consulte [introdução à gestão de energia](/sccm/core/clients/manage/power/introduction-to-power-management).  

#### <a name="deployments"></a>Implementações
 Apresenta qualquer software que implementou a membros da coleção selecionada.  

#### <a name="maintenance-windows"></a>Janelas de manutenção
 Ver e configurar janelas de manutenção que são aplicadas aos membros da coleção selecionada. Para obter mais informações, consulte [como utilizar janelas de manutenção](/sccm/core/clients/manage/collections/use-maintenance-windows).

#### <a name="collection-variables"></a>Variáveis da coleção
 Configure variáveis que se aplicam a esta coleção e podem ser utilizadas por sequências de tarefas. Para obter mais informações, consulte [como definir variáveis de sequência de tarefas](/sccm/osd/understand/using-task-sequence-variables#bkmk_set).  

#### <a name="distribution-point-groups"></a>Ponto de distribuição de grupos
 Associe uma ou mais grupos de pontos de distribuição a membros da coleção selecionada. Para obter mais informações, consulte [gerir a infraestrutura de conteúdo e conteúda](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure).

#### <a name="security"></a>Segurança
 Apresenta os utilizadores administrativos que têm permissões para a coleção selecionada a partir de funções e âmbitos de segurança associados. Para obter mais informações, consulte [Noções básicas da administração baseada em funções](/sccm/core/understand/fundamentals-of-role-based-administration).  

#### <a name="alerts"></a>Alertas 
 Configure quando são gerados alertas para o estado do cliente e o Endpoint Protection. Para obter mais informações, consulte [como configurar o estado do cliente](/sccm/core/clients/deploy/configure-client-status) e [como monitorizar o Endpoint Protection](/sccm/protect/deploy-use/monitor-endpoint-protection).  
