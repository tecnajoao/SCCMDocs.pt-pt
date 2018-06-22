---
title: Tarefas de gestão de aplicações
titleSuffix: Configuration Manager
description: Gerir aplicações do System Center Configuration Manager e tipos de implementação.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: c4041e21-21ff-4d95-ab05-14007e0047cf
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 4cc6c423880850b40d67d35e990982583c39e54e
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32334145"
---
# <a name="management-tasks-for-system-center-configuration-manager-applications"></a>Tarefas de gestão para aplicações do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize as informações neste artigo para o ajudar a gerir aplicações de System Center Configuration Manager e tipos de implementação.  

Para obter ajuda na criação de aplicações e tipos de implementação, consulte [criar aplicações](../../apps/deploy-use/create-applications.md).  

> [!IMPORTANT]  
>  Dependendo do tipo de aplicação ou tipo de implementação, algumas opções de gestão poderão não estar disponíveis.  

##  <a name="manage-applications"></a>Gerir aplicações  
 No **biblioteca de Software** área de trabalho, expanda **gestão de aplicações** > **aplicações**, escolha a aplicação que pretende gerir e, em seguida, escolha uma tarefa de gestão.  

|Tarefa|Detalhes|  
|----------|-------------|  
|**Gerir Contas de Acesso**|Abre a caixa de diálogo **Gerir Contas de Acesso** que lhe permite especificar o nível de acesso permitido para o conteúdo associado à aplicação selecionada.|  
|**Criar Ficheiro de Conteúdo Pré-configurado**|Abre o **Assistente para Criar Ficheiro de Conteúdo Pré-Configurado** que lhe permite gerir a distribuição do conteúdo por pontos de distribuição remotos. Quando o agendamento e limitação não fornecem uma solução válida para o ponto de distribuição remoto, é possível pré-configurar o conteúdo do ponto de distribuição.<br /><br /> Consulte [gerir a infraestrutura de conteúdo e conteúda](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|**Histórico de Revisão**|Abre o **histórico de revisão da aplicação** caixa de diálogo que lhe permite ver as propriedades das revisões efetuadas nesta aplicação, eliminar revisões antigas da aplicação e restaurar versões antigas desta aplicação.<br /><br /> Consulte [como rever e substituir aplicações](../../apps/deploy-use/revise-and-supersede-applications.md).|  
|**Criar Tipo de Implementação**|Abre o **implementação Assistente para criar tipo** que lhe permite adicionar um novo tipo de implementação à aplicação selecionada.<br /><br /> Consulte [criar aplicações](../../apps/deploy-use/create-applications.md).|  
|**Atualizar Estatísticas**|Atualiza as informações que são apresentadas no nó **Implementações** da área de trabalho **Monitorização** sobre as implementações desta aplicação.<br /><br /> Consulte [monitorizar aplicações a partir da consola do System Center Configuration Manager](../../apps/deploy-use/monitor-applications-from-the-console.md).|  
|**Restabelecer**|Restabelece uma aplicação que foi extinguida utilizando a **extinguir** tarefas de gestão.|  
|**Extinguir**|Quando extinguir uma aplicação, já não está disponível para implementação, mas as aplicações e implementações da aplicação não são eliminadas. As cópias existentes desta aplicação que tenham sido instaladas em computadores cliente não serão removidas. Quaisquer revisões à aplicação serão eliminadas do Configuration Manager após 60 dias. No entanto, as cópias instaladas da aplicação não são removidas.<br /><br /> Para eliminar uma aplicação, tem primeiro extinguir a aplicação, eliminar todas as implementações, remover as referências à aplicação noutras implementações e, em seguida, eliminar todas as revisões da aplicação.<br /><br /> Consulte [rever e substituir aplicações](../../apps/deploy-use/revise-and-supersede-applications.md).|  
|**Exportarar**|Abre o **Assistente para exportar aplicação** que permite exportar as aplicações selecionadas para um ficheiro. zip que pode depois arquivar ou instalar noutro site. Se optar por exportar o conteúdo da aplicação, será criada uma pasta que tem o conteúdo.<br /><br /> Também pode exportar as dependências da aplicação, relações de substituição e condições e os conteúdos para a aplicação e as respetivas dependências.<br /><br /> O cmdlet do Windows PowerShell, **Export-CMApplication**, a mesma função. Para obter mais informações, consulte [Export-CMApplication](http://go.microsoft.com/fwlink/p/?LinkID=258880) na documentação de referência de cmdlet do Microsoft System Center 2012 Configuration Manager SP1.|  
|**Eliminar**|Elimina a aplicação selecionada atualmente.<br /><br /> Não é possível eliminar uma aplicação se outras aplicações dependerem da mesma, se tiver uma implementação ativa ou se tiver sequências de tarefas dependentes.|  
|**Simular Implementação**|Abra o **Assistente de Simulação de Implementação da Aplicação** para testar os resultados da implementação de uma aplicação em computadores sem instalar ou desinstalar a aplicação.<br /><br /> Consulte [simular implementações de aplicações](../../apps/deploy-use/simulate-application-deployments.md).|  
|**Implementar**|Abre o **Assistente de Implementação de Software** para poder implementar a aplicação selecionada em conjuntos de computadores da hierarquia.<br /><br /> Consulte [implementar aplicações](../../apps/deploy-use/deploy-applications.md).|  
|**Distribuir Conteúdo**|Abre o **Assistente para Distribuir Conteúdo** para poder copiar o conteúdo da aplicação selecionada em pontos de distribuição da hierarquia.<br /><br /> Consulte [gerir a infraestrutura de conteúdo e conteúda](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|**Ver Relações**|Mostra um diagrama gráfico de relações das aplicações selecionadas para outras aplicações. Selecione uma das seguintes opções:<br><br><ul><li>**Dependência** – mostra as aplicações que dependem da aplicação selecionada e as aplicações que depende a aplicação selecionada.</li><li>**Substituição** – mostra as aplicações que substitui a aplicação selecionada e as aplicações que a aplicação selecionada foi substituída pelo.</li><li>**As condições globais** – mostra as condições globais que são referenciadas por esta aplicação.</li></ol><br /> Consulte [rever e substituir aplicações](../../apps/deploy-use/revise-and-supersede-applications.md) e [criar condições globais](../../apps/deploy-use/create-global-conditions.md).|  

##  <a name="manage-deployment-types"></a>Gerir tipos de implementação  
 No **biblioteca de Software** área de trabalho, expanda **gestão de aplicações**, escolha **aplicações**e, em seguida, escolha a aplicação que tem o tipo de implementação que pretende gerir. No painel de detalhes, selecione o **tipos de implementação** separador, escolha o tipo de implementação que pretende gerir e, em seguida, escolha uma tarefa de gestão.  

|Tarefa|Detalhes|  
|----------|-------------|  
|**Aumentar Prioridade**|Aumenta a prioridade do tipo de implementação selecionado. Os tipos de implementação são avaliados por ordem. Quando um tipo de implementação cumpre os requisitos especificados, este será executado e, em seguida, não existem mais tipos de implementação na lista de prioridades serão avaliados.|  
|**Diminuir Prioridade**|Diminui a prioridade do tipo de implementação selecionado.|  
|**Eliminar**|Elimina o tipo de implementação selecionado.<br><br>Não é possível eliminar um tipo de implementação se este for referenciado por um tipo de implementação de outra aplicação.<br>Para eliminar um tipo de implementação, tem de remover todas as dependências para o tipo de implementação que estão em outros tipos de implementação.<br>Além disso, também tem de remover as revisões anteriores de todas as aplicações que tenham um tipo de implementação que referencia o tipo de implementação que pretende eliminar.|  
|**Atualizar Conteúdo**|Atualiza o conteúdo do tipo de implementação selecionado.<br /><br /> Quando inicia este assistente para um tipo de implementação que tem uma aplicação virtual, o **Assistente de atualização de conteúdo** é iniciado. Este assistente permite-lhe alterar opções de publicação e regras de requisitos para a aplicação virtual selecionada. Para obter mais informações, consulte [criar aplicações](../../apps/deploy-use/create-applications.md).<br /><br /> Quando atualiza o conteúdo de um tipo de implementação, é criada uma nova revisão da aplicação. Isto pode fazer com que dispositivos cliente sejam atualizados com a nova aplicação.|  
