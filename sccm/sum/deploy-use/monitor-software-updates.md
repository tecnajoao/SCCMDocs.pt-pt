---
title: Monitorizar atualizações de software
titleSuffix: Configuration Manager
description: A consola do System Center Configuration Manager fornece alertas e os Estados para monitorizar as atualizações e a conformidade.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 9afd7b0f-5c8e-48bc-9a65-1f7d74103688
ms.openlocfilehash: e51e2c8236b014063efe9734baf338ebe70d1eb3
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39384488"
---
# <a name="monitor-software-updates-in-system-center-configuration-manager"></a>Monitorizar atualizações de software no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager fornece várias formas de ajudá-lo a monitorizar objetos de atualizações de software, processos e informações de compatibilidade. Utilize as secções seguintes para monitorizar atualizações de software.

## <a name="software-updates-dashboard"></a>Dashboard de atualizações de software
A partir do Configuration Manager versão 1610, pode utilizar o Dashboard de atualizações de Software para ver o atual estado de conformidade de dispositivos na sua organização e analisar rapidamente os dados para ver os dispositivos que estão em risco. Para ver o dashboard, navegue até **monitorização** > **descrição geral** > **segurança** > **atualizações de Software Dashboard**.   

##  <a name="BKMK_SUAlerts"></a> Alertas de atualizações de software  
 Pode configurar alertas para que as atualizações de software notifiquem os utilizadores administrativos sempre que os níveis de conformidade das implementações de atualizações de software se encontrem abaixo da percentagem configurada. Pode configurar alertas de implementações de atualizações de software nas seguintes localizações:  

-   Definição de ADR: Pode configurar as definições de alertas no Assistente de regra de implementação automática e nas propriedades para a ADR.  

-   Definição de implementação: Pode configurar as definições de alertas no Assistente de implementação de atualizações de Software e nas propriedades de implementação.  

Depois de configurar as definições de alerta, se verifiquem as condições especificadas, o Configuration Manager gera um alerta. Poderá consultar os alertas de atualização de software nas seguintes localizações:  

1.  Consulte os alertas recentes no nó **Atualizações de Software** da área de trabalho **Biblioteca de Software** .  

2.  Efetue a gestão dos alertas configurados no nó **Alertas** da área de trabalho **Monitorização** .  

##  <a name="BKMK_SUSyncStatus"></a> Estado de sincronização de atualizações de software  
 Após iniciar o processo de sincronização, pode monitorizar o processo de sincronização a partir da consola do Configuration Manager para todos os pontos de atualização de software na sua hierarquia. Utilize o seguinte procedimento para monitorizar o processo de sincronização de atualizações de software.  

#### <a name="to-monitor-the-software-updates-synchronization-process"></a>Para monitorizar o processo de sincronização de atualizações de software  

- Na consola do Configuration Manager, navegue até **monitorização** > **descrição geral** > **estado de sincronização do ponto de atualização de Software**.  

    Os pontos de atualização de software na sua hierarquia do Configuration Manager são apresentados no painel de resultados. A partir desta vista, poderá monitorizar o estado de sincronização de todos os pontos de atualização de software. Para ver informações mais detalhadas sobre o processo de sincronização, pode rever o ficheiro Wsyncmgr log que está localizado em <*ConfigMgrInstallationPath*> \Logs em cada servidor do site.  

##  <a name="BKMK_SUDeployStatus"></a> Estado de implementação da atualização de software  
 Após implementar as atualizações de software de um grupo de atualização de software ou implementar uma atualização de software individual, poderá monitorizar o estado da implementação. Utilize o seguinte procedimento para monitorizar o estado de implementação de um grupo de atualização de software ou de uma atualização de software.  

#### <a name="to-monitor-deployment-status"></a>Para monitorizar o estado da implementação  

1.  Na consola do Configuration Manager, navegue até **monitorização** > **descrição geral** > **implementações**.  

2.  Clique no grupo de atualização de software ou na atualização de software cujo estado da implementação pretende monitorizar.  

3.  No separador **Home Page** , no grupo **Implementação** , clique em **Ver Estado**.  

##  <a name="BKMK_SUReports"></a> Relatórios de atualizações do software  
 As mensagens de estado relativas a atualizações de software disponibilizam informações sobre a conformidade das atualizações de software e sobre o estado de avaliação e de imposição das implementações de atualizações de software. Pode executar relatórios de atualizações de software para ver estas mensagens de estado. Estão disponíveis mais de 30 relatórios de atualização de software predefinidos. Estes relatórios estão organizados em várias categorias e podem ser utilizados para o envio de informações específicas sobre atualizações de software e implementações. Além de utilizar os relatórios pré-configurados, também pode criar relatórios de atualização de software personalizados, adequados às necessidades da sua empresa. Para obter mais informações, consulte [operações e manutenção de relatórios](../../core/servers/manage/operations-and-maintenance-for-reporting.md).  

### <a name="recommended-software-updates-reports"></a>Recomendado relatórios de atualizações de software
Seguem-se alguns dos relatórios que são úteis na identificação de problemas potenciais: 

#### <a name="compliance-9---overall-health-and-compliance-starting-in-version-1806"></a>Conformidade 9 - estado de funcionamento geral e conformidade (a partir da versão 1806)
O relatório inclui as seguintes partes:

- **Bom estado de funcionamento clientes vs Total de clientes**: Este gráfico de barras compara os clientes de "integridade" que comunicaram com o site no período de tempo especificado com o número total de clientes na coleção especificada.
- **Descrição geral de conformidade**: Este gráfico circular mostra o estado de conformidade geral para o grupo de atualização de software específico em clientes ativos na coleção especificada.
- **5 principais em não conformidades por ID de artigo**: Este gráfico de barras mostra as atualizações de software de cinco principais no grupo especificado que estão em não conformidades em clientes ativos na coleção especificada.
- A parte inferior do relatório é uma tabela com mais detalhes, que lista as atualizações de software no grupo especificado.

#### <a name="management-2---updates-required-but-not-deployed"></a>Gestão 2 - atualizações obrigatórias mas não implementadas

Este relatório mostra as atualizações de software específicos do fornecedor numa classificação de atualizações específicas que foram detetados como obrigatório nos clientes, mas que não foram implementadas numa coleção específica. 

#### <a name="troubleshooting-2---deployment-errors"></a>Resolução de problemas 2 - erros de implementação

Este relatório devolve os erros de implementação no site e uma contagem de computadores com cada erro. 


##  <a name="BKMK_MonitorContent"></a> Monitorizar conteúdo  
 Pode monitorizar o conteúdo na consola do Configuration Manager para rever o estado de todos os tipos de pacotes relativamente aos pontos de distribuição associados. Estas informações podem incluir o estado de validação do conteúdo do pacote, o estado dos conteúdos atribuídos a um grupo específico de pontos de distribuição, o estado dos conteúdos atribuídos a um ponto de distribuição e o estado das funcionalidades opcionais de cada ponto de distribuição (validação de conteúdos, PXE e multicast).  

###  <a name="BKMK_ContentStatus"></a> Monitorização do estado do conteúdo  
 O nó **Estado do Conteúdo** da área de trabalho **Monitorização** disponibiliza informações sobre pacotes de conteúdos. Pode rever as informações gerais do pacote, o estado de distribuição do pacote e informações de estado detalhadas do pacote. Utilize o seguinte procedimento para ver o estado do conteúdo.  

#### <a name="to-monitor-content-status"></a>Para monitorizar o estado do conteúdo  

1.  Na consola do Configuration Manager, navegue até **monitorização** > **descrição geral** > **estado da distribuição**  >   **Estado do conteúdo**. Os pacotes são apresentados.  

2.  Selecione o pacote cujas informações detalhadas de estado pretende visualizar.  

3.  No separador **Home Page** , clique em **Ver Estado**. São apresentadas informações de estado detalhadas sobre o pacote.  

###  <a name="BKMK_DPGroupStatus"></a> Estado do grupo de pontos de distribuição  
 O nó **Estado do Grupo de Pontos de Distribuição** na área de trabalho **Monitorização** fornece informações acerca dos grupos de pontos de distribuição. Pode rever informações gerais sobre o grupo de pontos de distribuição, tais como o estado e a taxa de compatibilidade do grupo de pontos de distribuição, assim como informações de estado detalhadas sobre o grupo de pontos de distribuição. Utilize o seguinte procedimento para ver o estado do grupo de pontos de distribuição.  

#### <a name="to-monitor-distribution-point-group-status"></a>Para monitorizar o estado do grupo de pontos de distribuição  

1.  Na consola do Configuration Manager, navegue até **monitorização** > **descrição geral** > **estado da distribuição**  >   **Estado do grupo de ponto de distribuição**. Os grupos de pontos de distribuição são apresentados.  

2.  Selecione o grupo de pontos de distribuição cujas informações detalhadas de estado pretende visualizar.  

3.  No separador **Home Page** , clique em **Ver Estado**. São apresentadas informações detalhadas de estado para o grupo de pontos de distribuição.  

###  <a name="BKMK_DPConfigStatus"></a> Estado da configuração do ponto de distribuição  
 O nó **Estado da Configuração do Ponto de Distribuição** na área de trabalho **Monitorização** fornece informações acerca do ponto de distribuição. Pode consultar quais os atributos que se encontram ativados no ponto de distribuição, incluindo PXE, Multicast e a validação de conteúdo. Também pode ver informações detalhadas de estado para o ponto de distribuição. Utilize o seguinte procedimento para ver o estado da configuração do ponto de distribuição.  

#### <a name="to-monitor-distribution-point-configuration-status"></a>Para monitorizar o estado da configuração do ponto de distribuição  

1.  Na consola do Configuration Manager, navegue até **monitorização** > **descrição geral** > **estado da distribuição**  >   **Estado da configuração do ponto de distribuição**. Os pontos de distribuição são apresentados.  

2.  Selecione o ponto de distribuição do qual pretende ver informações sobre o estado do ponto de distribuição.  

3.  No painel de resultados, clique no separador **Detalhes** . São apresentadas informações de estado para o ponto de distribuição.  
