---
title: "Monitorizar implementações do sistema operativo"
titleSuffix: Configuration Manager
description: "Para ajudar a monitorizar objetos de implementação do sistema operativo, a consola do Configuration Manager fornece alertas, relatórios e vários indicadores de estado."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 08085d94-295c-432f-b5e3-9736bce0193b
caps.latest.revision: "6"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 2e738b0ae9bd16829857edfaae0fb7e398979627
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="monitor-operating-system-deployments-in-system-center-configuration-manager"></a>Monitorizar implementações do sistema operativo no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Consola do Configuration Manager fornece as seguintes opções para o ajudar a monitorizar objetos de implementação do sistema operativo.  


##  <a name="BKMK_OSDAlerts"></a> Alertas para implementações de sistema operativo  
 Pode configurar um alerta nas definições de implementação de sequência de tarefas para notificar os utilizadores administrativos quando os níveis de conformidade da implementação estiverem abaixo da percentagem configurada.  

 Depois de configurar as definições de alerta, se verifiquem as condições especificadas, o Configuration Manager gera um alerta. Pode rever os alertas de implementação da sequência de tarefas nas seguintes localizações:  

1.  Reveja os alertas recentes no nó **Sistemas Operativos** da área de trabalho **Biblioteca de Software** .  

2.  Efetue a gestão dos alertas configurados no nó **Alertas** da área de trabalho **Monitorização** .  

##  <a name="BKMK_TSDeployStatus"></a> Estado de implementação da sequência de tarefas  
 Depois de implementar uma sequência de tarefas, pode monitorizar o estado de implementação. Utilize o procedimento seguinte para monitorizar o estado de implementação de uma sequência de tarefas.  

#### <a name="to-monitor-deployment-status"></a>Para monitorizar o estado da implementação  

1.  Na consola do Configuration Manager, clique em **monitorização**.  

2.  Na área de trabalho Monitorização, clique em **Implementações**.  

3.  Clique na sequência de tarefas para a qual pretende monitorizar o estado de implementação.  

4.  No separador **Home Page** , no grupo **Implementação** , clique em **Ver Estado**.  

##  <a name="BKMK_TSReports"></a> Relatórios de implementação do sistema operativo  
 Existem muitos relatórios de implementação do sistema operativo predefinidos disponíveis. Estes relatórios estão organizados em várias categorias e podem ser utilizados para reportar informações específicas sobre migração de estado e implementações de sequências de tarefas. Além de utilizar os relatórios pré-configurados, também pode criar relatórios de atualização de software personalizados, adequados às necessidades da sua empresa. Para obter mais informações, consulte [operações e manutenção de relatórios](../../core/servers/manage/operations-and-maintenance-for-reporting.md).  

##  <a name="BKMK_MonitorContent"></a> Monitorizar conteúdo  
 Pode monitorizar os conteúdos na consola do Configuration Manager para rever o estado de todos os tipos de pacotes relativamente aos pontos de distribuição associados. Estas informações podem incluir o estado de validação do conteúdo do pacote, o estado dos conteúdos atribuídos a um grupo específico de pontos de distribuição, o estado dos conteúdos atribuídos a um ponto de distribuição e o estado das funcionalidades opcionais de cada ponto de distribuição (validação de conteúdos, PXE e multicast).  

###  <a name="BKMK_ContentStatus"></a> Monitorização do estado do conteúdo  
 O nó **Estado do Conteúdo** da área de trabalho **Monitorização** disponibiliza informações sobre pacotes de conteúdos. Pode rever as informações gerais do pacote, o estado de distribuição do pacote e informações de estado detalhadas do pacote. Utilize o seguinte procedimento para ver o estado do conteúdo.  

#### <a name="to-monitor-content-status"></a>Para monitorizar o estado do conteúdo  

1.  Na consola do Configuration Manager, clique em **monitorização**.  

2.  Na área de trabalho Monitorização, expanda **Estado da Distribuição**e clique em **Estado do Conteúdo**. Os pacotes são apresentados.  

3.  Selecione o pacote cujas informações detalhadas de estado pretende visualizar.  

4.  No separador **Home Page** , clique em **Ver Estado**. São apresentadas informações de estado detalhadas sobre o pacote.  

###  <a name="BKMK_DPGroupStatus"></a> Estado do grupo de pontos de distribuição  
 O nó **Estado do Grupo de Pontos de Distribuição** na área de trabalho **Monitorização** fornece informações acerca dos grupos de pontos de distribuição. Pode rever informações gerais sobre o grupo de pontos de distribuição, tais como o estado e a taxa de compatibilidade do grupo de pontos de distribuição, assim como informações de estado detalhadas sobre o grupo de pontos de distribuição. Utilize o seguinte procedimento para ver o estado do grupo de pontos de distribuição.  

#### <a name="to-monitor-distribution-point-group-status"></a>Para monitorizar o estado do grupo de pontos de distribuição  

1.  Na consola do Configuration Manager, clique em **monitorização**.  

2.  Na área de trabalho de monitorização, expanda **Estado de Distribuição**e, em seguida, clique em **Estado do Grupo de Pontos de Distribuição**. Os grupos de pontos de distribuição são apresentados.  

3.  Selecione o grupo de pontos de distribuição cujas informações detalhadas de estado pretende visualizar.  

4.  No separador **Home Page** , clique em **Ver Estado**. São apresentadas informações detalhadas de estado para o grupo de pontos de distribuição.  

###  <a name="BKMK_DPConfigStatus"></a> Estado da configuração do ponto de distribuição  
 O nó **Estado da Configuração do Ponto de Distribuição** na área de trabalho **Monitorização** fornece informações acerca do ponto de distribuição. Pode consultar quais os atributos que se encontram ativados no ponto de distribuição, incluindo PXE, Multicast e a validação de conteúdo. Também pode ver informações detalhadas de estado para o ponto de distribuição. Utilize o seguinte procedimento para ver o estado da configuração do ponto de distribuição.  

#### <a name="to-monitor-distribution-point-configuration-status"></a>Para monitorizar o estado da configuração do ponto de distribuição  

1.  Na consola do Configuration Manager, clique em **monitorização**.  

2.  Na área de trabalho de monitorização, expanda **Estado de Distribuição**e, em seguida, clique em **Estado da Configuração do Ponto de Distribuição**. Os pontos de distribuição são apresentados.  

3.  Selecione o ponto de distribuição do qual pretende ver informações sobre o estado do ponto de distribuição.  

4.  No painel de resultados, clique no separador **Detalhes** . São apresentadas informações de estado para o ponto de distribuição.  
