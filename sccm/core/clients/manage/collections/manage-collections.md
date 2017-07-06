---
title: "Gerir coleções de | Documentos do Microsoft"
description: "Realizar coleções comuns tarefas de gestão no System Center Configuration Manager."
ms.custom: na
ms.date: 4/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e102fd1a-76df-4d8e-b1b0-10ee18318f67
caps.latest.revision: 8
caps.handback.revision: 0
author: andredm7
ms.author: andredm
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: d94acac84f052a01de9d9c9f65f237c0006c45b8
ms.openlocfilehash: 4d44f98eb0755619cdd2101203a13725186b835b
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="how-to-manage-collections-in-system-center-configuration-manager"></a>Como gerir coleções no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize as informações de descrição geral deste tópico para o ajudar a efetuar tarefas de gestão para coleções no System Center Configuration Manager.  

> [!NOTE]  
>  Para obter informações sobre como criar coleções do Configuration Manager, consulte o artigo [como criar coleções no System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md).  

## <a name="how-to-manage-device-collections"></a>Como gerir coleções de dispositivos  
 Na área de trabalho **Ativos e Compatibilidade** , selecione **Coleções de Dispositivos**, selecione a coleção que pretende gerir e, em seguida, selecione uma tarefa de gestão.  

 Utilize a tabela seguinte para obter mais informações sobre as tarefas de gestão que podem necessitar de algumas informações antes de as selecionar.  

|Tarefa de gestão|Detalhes|Mais informações|  
|---------------------|-------------|----------------------|  
|**Mostrar Membros**|Apresenta todos os recursos que são membros da coleção selecionada num nó temporário sob o nó **Dispositivos** .|Não existem informações adicionais.|  
|**Adicionar Itens Selecionados**|Fornece as seguintes opções para efetuar uma das seguintes ações:<br /><br /> - <br />                    **Adicionar itens selecionados à coleção de dispositivos existente** -abre a **selecionar coleção** caixa de diálogo onde pode selecionar a coleção à qual pretende adicionar os membros da coleção selecionada. A coleção selecionada está incluída nesta coleção, utilizando uma regra de associação **Incluir Coleções** .<br /><br /> - **Adicionar itens selecionados à coleção de dispositivos novo** -abre a **criar Assistente de coleção de dispositivos** onde pode criar uma nova coleção. A coleção selecionada está incluída nesta coleção, utilizando uma regra de associação **Incluir Coleções** .|[Como criar coleções no System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md)|  
|**Instalar Cliente**|Abre o **Assistente de instalação do cliente** que utiliza a instalação push do cliente para instalar o cliente do Configuration Manager em todos os computadores na coleção selecionada.|[Como implementar clientes em computadores com o Windows](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md)|  
|**Gerir Pedidos de Afinidade**|Abre a caixa de diálogo **Gerir Pedidos de Afinidade Dispositivo/Utilizador** , onde pode aprovar ou rejeitar pedidos pendentes para estabelecer afinidades dispositivo/utilizador para dispositivos na coleção selecionada.|[Associar utilizadores e dispositivos com a afinidade de dispositivo / utilizador no System Center Configuration Manager](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)|  
|**Limpar as Implementações de PXE Necessárias**|Limpa quaisquer implementações de arranque PXE necessárias de todos os membros da coleção selecionada.|[Introdução à implementação do sistema operativo](../../../../osd/understand/introduction-to-operating-system-deployment.md)|  
|**Atualizar Associação**|Avalia a associação da coleção selecionada. Para coleções com muitos membros, esta atualização pode demorar algum tempo a concluir. Utilize a ação **Atualizar** para atualizar a apresentação com os novos membros de coleções após a atualização estar concluída.|Não existem informações adicionais.|  
|**Adicionar Recursos**|Abre a caixa de diálogo **Adicionar Recursos à Coleção** , onde pode procurar novos recursos para adicionar à coleção selecionada.<br /><br /> O ícone para a coleção selecionada irá apresentar um símbolo ampulheta enquanto a atualização está em curso.|Não existem informações adicionais.|  
|**Notificação de cliente**|Indica a todos os clientes na coleção de dispositivos selecionada para transferirem a política de computador ou utilizador.|Não existem informações adicionais.|  
|**Endpoint Protection**|Efetua uma análise antimalware completa ou rápida ou transfere as definições antimalware mais recentes para computadores na coleção selecionada.|[Endpoint Protection no System Center Configuration Manager](../../../../protect/deploy-use/endpoint-protection.md)|  
|**Exportarar**|Abre o **Assistente para exportar coleção** que ajuda a exportar para um formato de objeto gerido (MOF) nesta coleção de ficheiros que podem, em seguida, ser arquivados ou utilizados noutro site do Configuration Manager.<br /><br /> Ao exportar uma coleção, as coleções que são referenciados pela coleção selecionada através da utilização de uma regra **Incluir** ou **Excluir** não são exportadas.|Não existem informações adicionais.|  
|**Copiar**|Cria uma cópia da coleção selecionada. A nova coleção utiliza a coleção selecionada como uma coleção restritiva.|Não existem informações adicionais.|  
|**Eliminar**|Elimina a coleção selecionada. Também pode eliminar todos os recursos na coleção da base de dados do site.<br /><br /> Não é possível eliminar as coleções que vêm com o Configuration Manager.|Para obter uma lista das coleções incorporadas, consulte o artigo [introdução às coleções no System Center Configuration Manager](../../../../core/clients/manage/collections/introduction-to-collections.md).|  
|**Simular Implementação**|Abra o **Assistente de Simulação de Implementação de Aplicação** , que permite testar os resultados da implementação de uma aplicação sem instalar ou desinstalar a aplicação.|[Como simular implementações de aplicações com o System Center Configuration Manager](../../../../apps/deploy-use/simulate-application-deployments.md)|  
|**Implementar**|Apresenta as seguintes opções:<br /><br /> - <br />                    **Aplicação** -abre a **Assistente de implementação de Software** onde pode selecionar e configurar uma implementação de aplicação para a coleção selecionada.<br /><br /> - <br />                    **Programa** - abre o **Assistente de Implementação de Software** , onde pode selecionar e configurar a implementação de um pacote e programa para a coleção selecionada.<br /><br /> - **Linha base de configuração** -abre a **implementar linhas de base de configuração** caixa de diálogo onde pode configurar a implementação de um ou mais linhas base de configuração para a coleção selecionada.<br /><br /> - <br />                    **Sequência de Tarefas** - abre o **Assistente de Implementação de Software** , onde pode selecionar e configurar a implementação de uma sequência de tarefas para a coleção selecionada.<br /><br /> - <br />                    **As atualizações de software** -abre a **implementar Assistente de atualização de Software** onde pode configurar a implementação de atualizações de software aos recursos na coleção selecionada.|[Como implementar aplicações com o System Center Configuration Manager](../../../../apps/deploy-use/deploy-applications.md)<br /><br /> [Pacotes e programas no System Center Configuration Manager](../../../../apps/deploy-use/packages-and-programs.md)<br /><br /> [Como implementar linhas de base de configuração no System Center Configuration Manager](../../../../compliance/deploy-use/deploy-configuration-baselines.md)<br /><br /> [Gerir sequências de tarefas para automatizar tarefas no System Center Configuration Manager](../../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md)<br /><br /> [Gerir atualizações de software no System Center Configuration Manager](/sccm/sum/understand/software-updates-introduction)|  

## <a name="how-to-manage-user-collections"></a>Como gerir coleções de utilizadores  
 Na área de trabalho **Ativos e Compatibilidade** , selecione **Coleções de Utilizadores**, selecione a coleção que pretende gerir e, em seguida, selecione uma tarefa de gestão.  

 Utilize a tabela seguinte para obter mais informações sobre as tarefas de gestão que podem necessitar de algumas informações antes de as selecionar.  

|Tarefa de gestão|Detalhes|Mais informações|  
|---------------------|-------------|----------------------|  
|**Mostrar Membros**|Apresenta todos os recursos que são membros da coleção selecionada num nó temporário sob o nó **Utilizadores** .|Não existem informações adicionais.|  
|**Adicionar Itens Selecionados**|Esta opção permite efetuar uma das seguintes ações:<br /><br /> - <br />                    **Adicionar itens selecionados à coleção de utilizador existente** -abre a **selecionar coleção** caixa de diálogo onde pode selecionar a coleção à qual pretende adicionar os membros da coleção selecionada. A coleção selecionada está incluída nesta coleção, utilizando uma regra de associação **Incluir Coleções** .<br /><br /> - **Adicionar itens selecionados à coleção de novos utilizadores** -abre a **Assistente para criar utilizador coleção** onde pode criar uma nova coleção. A coleção selecionada está incluída nesta coleção, utilizando uma regra de associação **Incluir Coleções** .|[Como criar coleções no System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md)|  
|**Gerir Pedidos de Afinidade**|Abre a caixa de diálogo **Gerir Pedidos de Afinidade Dispositivo/Utilizador** , onde pode aprovar ou rejeitar pedidos pendentes para estabelecer afinidades dispositivo/utilizador para utilizadores na coleção selecionada.|[Associar utilizadores e dispositivos com a afinidade de dispositivo / utilizador no System Center Configuration Manager](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)|  
|**Atualizar Associação**|Avalia a associação da coleção selecionada. Para coleções com muitos membros, esta atualização pode demorar algum tempo a concluir. Utilize a ação **Atualizar** para atualizar a apresentação com os novos membros de coleções após a atualização estar concluída.<br /><br /> O ícone para a coleção selecionada irá apresentar um símbolo ampulheta enquanto a atualização está em curso.|Não existem informações adicionais.|  
|**Adicionar Recursos**|Abre a caixa de diálogo **Adicionar Recursos à Coleção** , onde pode procurar novos recursos para adicionar à coleção selecionada.|Não existem informações adicionais.|  
|**Exportarar**|Abre o **Assistente para exportar coleção** que lhe permite exportar esta coleção para um ficheiro de formato de objeto gerido (MOF) que, em seguida, pode ser arquivado ou utilizado noutro site do Configuration Manager.<br /><br /> Ao exportar uma coleção, as coleções que são referenciados pela coleção selecionada através da utilização de uma regra **Incluir** ou **Excluir** não são exportadas.|Não existem informações adicionais.|  
|**Copiar**|Cria uma cópia da coleção selecionada. A nova coleção utiliza a coleção selecionada como uma coleção restritiva.|Não existem informações adicionais.|  
|**Eliminar**|Elimina a coleção selecionada. Também pode eliminar todos os recursos na coleção da base de dados do site.<br /><br /> Não é possível eliminar as coleções que vêm com o Configuration Manager.|Para obter uma lista das coleções incorporadas, consulte o artigo [introdução às coleções no System Center Configuration Manager](../../../../core/clients/manage/collections/introduction-to-collections.md).|  
|**Simular Implementação**|Abra o **Assistente de Simulação de Implementação de Aplicação** , que permite testar os resultados da implementação de uma aplicação sem instalar ou desinstalar a aplicação.|[Como simular implementações de aplicações com o System Center Configuration Manager](../../../../apps/deploy-use/simulate-application-deployments.md)|  
|**Implementar**|Apresenta as seguintes opções:<br /><br /> - **Aplicação** -abre a **Assistente de implementação de Software** onde pode selecionar e configurar uma implementação de aplicação para a coleção selecionada.<br /><br /> - <br />                    **Programa** - abre o **Assistente de Implementação de Software** , onde pode selecionar e configurar a implementação de um pacote e programa para a coleção selecionada.<br /><br /> - **Linha base de configuração** -abre a **implementar linhas de base de configuração** caixa de diálogo onde pode configurar a implementação de um ou mais linhas base de configuração para a coleção selecionada.|[Como implementar aplicações com o System Center Configuration Manager](../../../../apps/deploy-use/deploy-applications.md)<br /><br /> [Pacotes e programas no System Center Configuration Manager](../../../../apps/deploy-use/packages-and-programs.md)<br /><br /> [Como implementar linhas de base de configuração no System Center Configuration Manager](../../../../compliance/deploy-use/deploy-configuration-baselines.md)|  

##  <a name="BKMK_CollProp"></a> Propriedades da coleção  
 Quando abre a caixa de diálogo **Propriedades** para uma coleção, pode ver e configurar as seguintes propriedades de uma coleção.  

|Nome do separador|Mais informações|  
|--------------|----------------------|  
|**Geral**|Permite ver e configurar informações gerais sobre a coleção selecionada, incluindo o nome da coleção e a coleção restritiva.|  
|**Regras de Associação**|Permite configurar as regras de associação que definem a associação desta coleção. Para obter mais informações, consulte o artigo [como criar coleções no System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md).|  
|**Gestão de Energia**|Permite configurar planos de gestão de energia que são atribuídos aos computadores na coleção selecionada. Para obter mais informações, consulte o artigo [introdução à gestão de energia](../../../../core/clients/manage/power/introduction-to-power-management.md).|  
|**Implementações**|Apresenta qualquer software que tenha sido implementado para os membros da coleção selecionada.|  
|**Janelas de manutenção**|Permite ver e configurar janelas de manutenção que são aplicadas aos membros da coleção selecionada. Para obter mais informações, consulte o artigo [como utilizar as janelas de manutenção no System Center Configuration Manager](../../../../core/clients/manage/collections/use-maintenance-windows.md).|  
|**Variáveis da Coleção**|Permite configurar variáveis que se aplicam a esta coleção e podem ser utilizadas por sequências de tarefas. Para obter mais informações, consulte o artigo [variáveis incorporadas de sequência de tarefas](../../../../osd/understand/task-sequence-built-in-variables.md).|  
|**Grupos de Pontos de Distribuição**|Permite associar um ou mais grupos de pontos de distribuição a membros da coleção selecionada. Para obter mais informações, consulte o artigo [gerir a infraestrutura do conteúdo e conteúda para o System Center Configuration Manager](../../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|**Segurança**|Apresenta os utilizadores administrativos que têm permissões para a coleção selecionada a partir de funções e âmbitos de segurança associados.|  
|**Monitor**|Permite configurar quando são gerados alertas para o estado do cliente e do Endpoint Protection. Para obter mais informações, consulte o artigo [como configurar o estado do cliente no System Center Configuration Manager](../../../../core/clients/deploy/configure-client-status.md) e [como monitorizar o Endpoint Protection no System Center Configuration Manager](../../../../protect/deploy-use/monitor-endpoint-protection.md).|  
