---
title: Monitorizar o estado do Endpoint Protection | Documentos do Microsoft
description: Saiba como monitorizar o Endpoint Protection na sua hierarquia do System Center Configuration Manager.
ms.custom: na
ms.date: 03/13/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f4a1335c-bb3d-493e-a124-83a32a107dc8
caps.latest.revision: 8
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: af0aafb4b7209d840676d16723509f399c662aad
ms.openlocfilehash: b5771f4faebc06076bdbf84727848c881fc1dfb4
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="how-to-monitor-endpoint-protection-status"></a>Como monitorizar o estado do Endpoint Protection

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode monitorizar o Endpoint Protection na sua hierarquia do Microsoft System Center Configuration Manager utilizando a **Estado Endpoint Protection** nó em **segurança** no **monitorização** área de trabalho, o **Endpoint Protection** nó o **ativos e compatibilidade** área de trabalho e utilizando os relatórios.  

##  <a name="BKMK_1"></a>Como monitorizar o Endpoint Protection utilizando o nó de estado do Endpoint Protection  

1.  Na consola do Configuration Manager, clique em **monitorização**.  

2.  No **monitorização** área de trabalho, expanda **segurança** e, em seguida, clique em **Estado Endpoint Protection**.  

3.  No **coleção** lista, selecione a coleção para o qual pretende ver informações de estado.  

    > [!IMPORTANT]  
    >  Coleções estão disponíveis para seleção nos seguintes casos:  
    >   
    >  -   Quando seleciona **ver esta coleção no dashboard do Endpoint Protection** no **alertas** separador do *< nome da coleção\>***propriedades** caixa de diálogo.  
    > -   Ao implementar uma política de proteção contra software maligno do Endpoint Protection para a coleção.  
    > -   Quando ativar e implementar definições de cliente do Endpoint Protection na coleção.  

4.  Reveja as informações que são apresentadas no **estado de segurança** e **estado operacional** secções. Pode clicar em qualquer ligação de estado para criar uma coleção temporária no nó **Dispositivos** da área de trabalho **Ativos e Compatibilidade** . Na coleção temporária contém os computadores com o estado selecionado.  

    > [!IMPORTANT]  
    >  Informações que são apresentadas no **Estado Endpoint Protection** nó baseia-se os últimos dados que foi resumidos da base de dados do Configuration Manager e poderão não ser atuais. Se pretender obter os dados mais recentes, no separador **Home Page** , clique em **Executar Resumo**ou clique em **Agendar Resumo** para ajustar o intervalo de resumo.  

##  <a name="BKMK_2"></a>Como monitorizar o Endpoint Protection no ativos e compatibilidade área de trabalho  

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  

2.  No **ativos e compatibilidade** área de trabalho, efetue uma das seguintes ações:  

    -   Clique em **dispositivos**. Na lista **Dispositivos** , selecione um computador e, em seguida, clique no separador **Detalhe de Software Maligno** .  

    -   Clique em **coleções de dispositivos**. Na lista **Coleções de Dispositivos** , selecione a coleção que contém o computador que pretende monitorizar e, em seguida, no separador **Home Page** , no grupo **Coleção** , clique em **Mostrar Membros**.  

3.  No *< nome da coleção\>*  lista, selecione um computador e, em seguida, clique a **detalhe de software maligno** separador.  

##  <a name="BKMK_3"></a>Como monitorizar o Endpoint Protection utilizando os relatórios  
 Utilize os seguintes relatórios para o ajudar a ver informações sobre o Endpoint Protection na hierarquia. Também pode utilizar estes relatórios para ajudar a resolver problemas do Endpoint Protection. Para obter mais informações sobre como configurar relatórios no Configuration Manager, consulte o artigo [Reporting no System Center Configuration Manager](../../core/servers/manage/reporting.md) e [ficheiros de registo no System Center Configuration Manager](../../core/plan-design/hierarchy/log-files.md). Os relatórios de Endpoint Protection estão na pasta do Endpoint Protection.  

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
|**Falhou**|Não foi possível remediar o software maligno do Endpoint Protection. Verifique os registos para obter detalhes sobre o erro.<br /><br /> **Nota:** Para obter uma lista do Configuration Manager e ficheiros de registo do Endpoint Protection, consulte a secção "Endpoint Protection" o [ficheiros de registo no System Center Configuration Manager](../../core/plan-design/hierarchy/log-files.md) tópico.|  
|**Removidas**|Endpoint Protection removeu com êxito o software maligno.|  
|**Em quarentena**|Endpoint Protection movido o software maligno para uma localização segura e impediu a ser executado até removê-lo ou permitir que seja executado.|  
|**Limpo**|O software maligno foi limpo no ficheiro infetado.|  
|**Permitido**|Um utilizador administrativo optou por permitir a execução do software que contém o software maligno.|  
|**Nenhuma ação**|Endpoint Protection não demorou nenhuma ação no software maligno. Esta situação pode ocorrer se o computador for reiniciado depois de o software maligno ser detetado e o software maligno já não é detetado; por exemplo, se uma unidade de rede mapeada na qual seja detetado software maligno não for religada quando o computador é reiniciado.|  
|**Bloqueado**|Endpoint Protection bloqueada o software maligno a execução. Esta situação pode ocorrer se for encontrado um processo no computador que contém software maligno.|

