---
title: Monitorizar clientes - Configuration Manager | Microsoft Docs
description: "Obter orientações detalhadas sobre como monitorizar clientes no System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2c8f57cf-1968-48de-87fb-4897432ed6e0
caps.latest.revision: "23"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: ec912dc60492ad3879a576970f93ff2fa016099d
ms.sourcegitcommit: b438515490e04fb09c82a8af642d38e9a0605178
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/15/2017
---
# <a name="how-to-monitor-clients-in-system-center-configuration-manager"></a>Como monitorizar clientes no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


 Assim que a aplicação de cliente do System Center Configuration Manager foi instalada nos computadores com o Windows e dispositivos no seu site, pode monitorizar o respetivo estado de funcionamento e a atividade na consola do Configuration Manager.  

##  <a name="bkmk_about"></a> Sobre o estado do cliente  
 O Configuration Manager fornece os seguintes tipos de informações como o estado do cliente:  

-   **Estado online do cliente** -a partir da versão 1602 do Configuration Manager, este estado indica se o computador está online ou não. Um computador é considerado online se estiver ligado ao respetivo ponto de gestão atribuído.  Para indicar que o cliente está online, envia mensagens do tipo ping ao ponto de gestão. Se o ponto de gestão não receber uma mensagem após cerca de 5 minutos, o cliente é considerado offline.  

-   **Atividade do cliente** -este estado indica se o cliente tem estado a interagir ativamente com o Configuration Manager nos últimos 7 dias. Se o cliente não solicitou uma atualização de política, enviou uma mensagem heartbeat ou enviou um inventário de hardware nos últimos 7 dias, o cliente é considerado inativo.  

-   **Verificação de cliente** -este estado indica o êxito da avaliação periódica que executa o cliente do Configuration Manager no computador.  A avaliação verifica o computador e pode retificar alguns dos problemas que encontra. Para obter mais informações, veja [Verificações e remediações efetuadas pela verificação do cliente](#BKMK_ClientHealth).  

     Nos computadores que executam o Windows 7, a verificação de cliente é executada como uma tarefa agendada. Em sistemas operativos posteriores, a verificação de cliente é executada automaticamente durante o período de manutenção do Windows.  

     É possível configurar a remediação para não funcionar em computadores específicos, por exemplo, um servidor crítico para a empresa. Além disso, se existirem itens adicionais que pretenda avaliar, pode utilizar as definições de compatibilidade do Configuration Manager para fornecer uma solução abrangente para monitorizar o estado de funcionamento, atividade e compatibilidade dos computadores na sua organização geral. Para obter mais informações sobre as definições de compatibilidade, veja [Planear e configurar definições de compatibilidade no Configuration Manager](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md).  

##  <a name="bkmk_indStatus"></a> Monitorizar o estado de clientes individuais  

1.  Na consola do Configuration Manager, clique em **ativos e compatibilidade** > **dispositivos** ou escolha uma coleção em **coleções de dispositivos**.  

     A partir da versão 1602 do Configuration Manager, os ícones no início de cada linha indicam o estado online do dispositivo:  

    |||  
    |-|-|  
    |![ícone de estado online dos clientes](../../../core/clients/manage/media/online-status-icon.png)|O dispositivo está online.|  
    |![ícone de estado offline dos clientes](../../../core/clients/manage/media/offline-status-icon.png)|O dispositivo está offline.|  
    |![ícone de estado desconhecido dos clientes](../../../core/clients/manage/media/unknown-status-icon.png)|O estado online é desconhecido.|  
    |![cliente não instalado](../../../core/clients/manage/media/client-not-installed.png)|O cliente não está instalado no dispositivo.|  

2.  Para o estado online mais detalhado, adicione as informações de estado online do cliente para a vista do dispositivo clicando no cabeçalho da coluna e clicando nos campos de estado online que pretende adicionar. As colunas que pode adicionar são:  

    -   **Estado Online do Dispositivo** indica se o cliente está atualmente online ou offline. (Esta é a mesma informação dada pelos ícones).  

    -   **Última Vez Online** indica se o estado online do cliente mudou para online.  

    -   **Última Vez Offline** indica se o estado mudou para offline.  

3.  Clique num cliente individual no painel de lista para ver mais estados no painel de detalhes, incluindo informações sobre a atividade do cliente e as verificações do cliente.  

##  <a name="bkmk_allStatus"></a> Monitorizar o estado de todos os clientes  

1.  Na consola do Configuration Manager, clique em **monitorização** > **estado do cliente**. Nesta página da consola, pode rever as estatísticas gerais da atividade do cliente e as verificações do cliente em todo o site.  Também pode alterar o âmbito das informações, selecionando uma coleção diferente.  

2.  Para obter detalhes sobre as estatísticas comunicadas, clique no nome das informações comunicadas (tais como **clientes ativos que passaram a verificação de cliente ou que não obtiveram resultados**) e reveja as informações sobre os clientes individuais.  

3.  Clique em **atividade do cliente** para ver gráficos que mostram a atividade do cliente no site do Configuration Manager.  

4.  Clique em **verificação de cliente** para ver gráficos que mostram o estado do cliente verifica no seu site do Configuration Manager.  

 Pode configurar alertas para receber notificações quando os resultados da verificação de cliente ou a atividade do cliente descerem abaixo de uma percentagem especificada de clientes numa coleção ou quando a remediação falhar numa percentagem especificada de clientes. Para obter informações sobre como configurar o estado de cliente, veja [Como configurar o estado de cliente no Configuration Manager](../../../core/clients/deploy/configure-client-status.md).  

##  <a name="BKMK_ClientHealth"></a> Verificações e remediações efetuadas pela verificação do cliente  
 As verificações e remediações seguintes podem ser efetuadas pela verificação do cliente.  

|Verificação do Cliente|Ação de remediação|Mais informações|  
|------------------|------------------------|----------------------|  
|Verificar se a verificação do cliente foi executada recentemente|Executar verificação do cliente|Verifica se a verificação do cliente foi executada pelo menos uma vez nos últimos três dias.|  
|Verificar se os pré-requisitos de cliente estão instalados|Instalar os pré-requisitos de cliente|Verifica se os pré-requisitos de cliente estão instalados. Lê o ficheiro ccmsetup.xml na pasta de instalação do cliente para detetar os pré-requisitos.|  
|Teste de integridade do repositório de WMI|Reinstalar o cliente do Configuration Manager|Verifica se as entradas de cliente do Configuration Manager estão presentes no WMI.|  
|Verificar se o serviço de cliente está em execução|Iniciar o serviço de cliente (Anfitrião de Agente do SMS)|Não existem informações adicionais|  
|Teste do Event Sink de WMI.|Reiniciar o serviço de cliente|Verifique se o Gestor de configuração relacionados com o sink de evento do WMI foi perdida|  
|Verificar se o serviço Windows Management Instrumentation (WMI) existe|Sem remediação|Não existem informações adicionais|  
|Verificar se o cliente foi instalado corretamente|Reinstalar o cliente|Não existem informações adicionais|  
|Teste de leitura e escrita do repositório de WMI|Repor o repositório WMI e reinstalar o cliente do Configuration Manager|A remediação desta verificação de cliente só é executada em computadores com o Windows Server 2003, o Windows XP (64 bits) ou versões anteriores.|  
|Verificar se o tipo de arranque do serviço antimalware é automático|Repor o tipo de arranque do serviço em automático|Não existem informações adicionais|  
|Verificar se o serviço antimalware está em execução|Iniciar o serviço antimalware|Não existem informações adicionais|  
|Verificar se o tipo de arranque do serviço Windows Update é automático ou manual|Repor o tipo de arranque do serviço em automático|Não existem informações adicionais|  
|Verificar se o tipo de arranque do serviço de cliente (Anfitrião de Agente do SMS) é automático|Repor o tipo de arranque do serviço em automático|Não existem informações adicionais|  
|Verificar se o serviço Windows Management Instrumentation (WMI) está em execução.|Iniciar o serviço Windows Management Instrumentation|Não existem informações adicionais|  
|Verificar se a base de dados do Microsoft SQL CE está em bom estado de funcionamento|Reinstalar o cliente do Configuration Manager|Não existem informações adicionais|  
|Teste de Integridade do WMI do Microsoft Policy Platform|Reparar o Microsoft Policy Platform|Não existem informações adicionais|  
|Verificar que o Microsoft Policy Platform Service existe|Reparar o Microsoft Policy Platform|Não existem informações adicionais|  
|Verificar que o tipo de arranque do Microsoft Policy Platform Service é manual|Repor o tipo de arranque do serviço em manual|Não existem informações adicionais|  
|Verificar se o Serviço de Transferência Inteligente em Segundo Plano existe|Sem remediação|Não existem informações adicionais|  
|Verificar se o tipo de arranque do Serviço de Transferência Inteligente em Segundo Plano é automático ou manual|Repor o tipo de arranque do serviço em automático|Não existem informações adicionais|  
|Verificar se o tipo de arranque do Serviço de Inspeção de Rede é manual|Repor o tipo de arranque do serviço em manual se estiver instalado|Não existem informações adicionais|  
|Verificar se o tipo de arranque do serviço Windows Management Instrumentation (WMI) é automático|Repor o tipo de arranque do serviço em automático|Não existem informações adicionais|  
|Verificar se o tipo de arranque do serviço Windows Update em computadores com o Windows 8 é automático ou manual|Repor o tipo de arranque do serviço em manual|Não existem informações adicionais|  
|Verificar se o serviço de cliente (Anfitrião de Agente do SMS) existe.|Sem remediação|Não existem informações adicionais|  
|Verificar se o tipo de arranque do serviço Controlo Remoto do Configuration Manager é automático ou manual|Repor o tipo de arranque do serviço em automático|Não existem informações adicionais|  
|Verificar se o serviço Controlo Remoto do Configuration Manager está em execução|Iniciar o serviço de controlo remoto|Não existem informações adicionais|  
|Verificar se o fornecedor WMI cliente está em bom estado de funcionamento|Reiniciar o serviço Windows Management Instrumentation|A remediação desta verificação de cliente só é executada em computadores com o Windows Server 2003, o Windows XP (64 bits) ou versões anteriores.|  
|Verificar se o serviço proxy de reativação (Proxy de Reativação do ConfigMgr) está em execução|Iniciar o serviço Proxy de Reativação do ConfigMgr|Esta verificação de cliente é executada apenas se o **gestão de energia**: **Ativar o proxy de reativação** definição de cliente está definido como **Sim** em sistemas operativos cliente suportados.|  
|Verificar se o tipo de arranque do serviço proxy de reativação (Proxy de Reativação do ConfigMgr) é automático|Repor o tipo de arranque do serviço Proxy de Reativação do ConfigMgr em automático|Esta verificação de cliente é executada apenas se o **gestão de energia**: **Ativar o proxy de reativação** definição de cliente está definido como **Sim** em sistemas operativos cliente suportados.|  

## <a name="client-deployment-log-files"></a>Ficheiros de registo de implementação do cliente
Para obter informações sobre os ficheiros de registo utilizado pela implementação do cliente e operações de gestão, consulte [ficheiros de registo no System Center Configuration Manager](/sccm/core/plan-design/hierarchy/log-files#BKMK_ClientLogs).
