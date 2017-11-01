---
title: Monitorizar o estado do Endpoint Protection
titleSuffix: Configuration Manager
description: Saiba como monitorizar o Endpoint Protection na sua hierarquia do System Center Configuration Manager.
ms.custom: na
ms.date: 03/13/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f4a1335c-bb3d-493e-a124-83a32a107dc8
caps.latest.revision: "8"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 9e6356f8b3814ac49c26bfa4d319c3c9926a4382
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="how-to-monitor-endpoint-protection-status"></a>Como monitorizar o estado do Endpoint Protection

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode monitorizar o Endpoint Protection na sua hierarquia do Microsoft System Center Configuration Manager, utilizando o **estado do Endpoint Protection** nó **segurança** no **monitorização** área de trabalho, o **Endpoint Protection** no nó a **ativos e compatibilidade** área de trabalho e utilizando relatórios.  

##  <a name="BKMK_1"></a>Como monitorizar o Endpoint Protection utilizando o nó de estado do Endpoint Protection  

1.  Na consola do Configuration Manager, clique em **monitorização**.  

2.  No **monitorização** área de trabalho, expanda **segurança** e, em seguida, clique em **estado do Endpoint Protection**.  

3.  No **coleção** lista, selecione a coleção para o qual pretende ver informações de estado.  

    > [!IMPORTANT]  
    >  As coleções estão disponíveis para seleção nos seguintes casos:  
    >   
    >  -   Quando seleciona **ver esta coleção no dashboard do Endpoint Protection** no **alertas** separador do *< nome da coleção\>***propriedades** caixa de diálogo.  
    > -   Ao implementar uma política antimalware do Endpoint Protection para a coleção.  
    > -   Quando ativa e implementar definições de cliente do Endpoint Protection na coleção.  

4.  Reveja as informações que são apresentadas no **estado de segurança** e **estado operacional** secções. Pode clicar em qualquer ligação de estado para criar uma coleção temporária no nó **Dispositivos** da área de trabalho **Ativos e Compatibilidade** . A coleção temporária contém os computadores com o estado selecionado.  

    > [!IMPORTANT]  
    >  Informações que são apresentadas no **estado do Endpoint Protection** nós baseia-se nos últimos dados que foram resumidos a partir da base de dados do Configuration Manager e podem não ser atuais. Se pretender obter os dados mais recentes, no separador **Home Page** , clique em **Executar Resumo**ou clique em **Agendar Resumo** para ajustar o intervalo de resumo.  

##  <a name="BKMK_2"></a>Como monitorizar o Endpoint Protection no ativos e compatibilidade área de trabalho  

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  

2.  No **ativos e compatibilidade** área de trabalho, efetue uma das seguintes ações:  

    -   Clique em **dispositivos**. Na lista **Dispositivos** , selecione um computador e, em seguida, clique no separador **Detalhe de Software Maligno** .  

    -   Clique em **coleções de dispositivos**. Na lista **Coleções de Dispositivos** , selecione a coleção que contém o computador que pretende monitorizar e, em seguida, no separador **Home Page** , no grupo **Coleção** , clique em **Mostrar Membros**.  

3.  No *< nome da coleção\>*  lista, selecione um computador e, em seguida, clique o **detalhe de software maligno** separador.  

##  <a name="BKMK_3"></a>Como monitorizar o Endpoint Protection utilizando relatórios  
 Utilize os seguintes relatórios para ver informações sobre o Endpoint Protection na sua hierarquia. Também pode utilizar estes relatórios para ajudar a resolver quaisquer problemas do Endpoint Protection. Para obter mais informações sobre como configurar relatórios no Configuration Manager, consulte [relatórios no System Center Configuration Manager](../../core/servers/manage/reporting.md) e [ficheiros de registo no System Center Configuration Manager](../../core/plan-design/hierarchy/log-files.md). Os relatórios de Endpoint Protection estão na pasta do Endpoint Protection.  

|Nome do Relatório|Descrição|  
|-----------------|-----------------|  
|**Relatório de Atividade Antimalware**|Apresenta uma descrição geral da atividade antimalware de uma coleção específica.|  
|**Computadores Infetados**|Apresenta uma lista de computadores nos quais seja detetada uma ameaça especificada.|  
|**Principais Utilizadores Por Ameaças**|Apresenta uma lista de utilizadores com o maior número de ameaças detetadas.|  
|**Lista de Ameaças**|Apresenta uma lista de ameaças que foram encontradas numa conta de utilizador especificada.|  

## <a name="malware-alert-levels"></a>Níveis de alerta de software maligno  
 Utilize a tabela seguinte para identificar os diferentes níveis de alerta de Endpoint Protection que podem ser apresentados nos relatórios ou na consola do Configuration Manager.  

|Nível de alerta|Descrição|  
|-----------------|-----------------|  
|**Falhou**|Não foi possível remediar o software maligno do Endpoint Protection. Verifique os registos para obter detalhes sobre o erro.<br /><br /> **Nota:** Para obter uma lista de ficheiros de registo de Endpoint Protection e do Configuration Manager, consulte a secção "Endpoint Protection" do [ficheiros de registo no System Center Configuration Manager](../../core/plan-design/hierarchy/log-files.md) tópico.|  
|**Removidas**|Proteção de ponto final removido com êxito o software maligno.|  
|**Em quarentena**|Endpoint Protection moveu o software maligno para uma localização segura e impediu o seu seja executado até removê-lo ou permitir que seja executado.|  
|**Limpo**|O software maligno foi limpo no ficheiro infetado.|  
|**Permitido**|Um utilizador administrativo optou por permitir a execução do software que contém o software maligno.|  
|**Nenhuma ação**|Proteção de ponto final não demorou nenhuma ação no software maligno. Esta situação pode ocorrer se o computador for reiniciado depois de o software maligno ser detetado e o software maligno já não é detetado; por exemplo, se uma unidade de rede mapeada na qual seja detetado software maligno não for religada quando o computador é reiniciado.|  
|**Bloqueado**|Proteção de ponto final bloqueada a execução do software maligno. Esta situação pode ocorrer se for encontrado um processo no computador que contém software maligno.|
