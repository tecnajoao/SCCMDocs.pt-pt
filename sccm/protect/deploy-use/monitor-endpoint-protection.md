---
title: Monitorizar o estado do Endpoint Protection
titleSuffix: Configuration Manager
description: Saiba como monitorizar o Endpoint Protection na sua hierarquia do System Center Configuration Manager.
ms.date: 03/13/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f4a1335c-bb3d-493e-a124-83a32a107dc8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5de0ab2eb56ad671a43a6a40fab4e1f4dcc051a4
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53424399"
---
# <a name="how-to-monitor-endpoint-protection-status"></a>Como monitorizar o estado do Endpoint Protection

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode monitorizar o Endpoint Protection na sua hierarquia do Microsoft System Center Configuration Manager utilizando a **estado do Endpoint Protection** no nó **Security** no **monitorização**  área de trabalho, o **Endpoint Protection** nó a **ativos e compatibilidade** área de trabalho e utilizando relatórios.  

##  <a name="BKMK_1"></a> Como monitorizar o Endpoint Protection utilizando o nó de estado de proteção de ponto final  

1. Na consola do Configuration Manager, clique em **monitorização**.  

2. Na **monitorização** área de trabalho, expanda **Security** e, em seguida, clique em **estado do Endpoint Protection**.  

3. Na **coleção** , selecione a coleção para o qual pretende ver informações de estado.  

   > [!IMPORTANT]
   >  As coleções estão disponíveis para seleção nos seguintes casos:  
   > 
   > - Quando seleciona **ver esta coleção no dashboard do Endpoint Protection** sobre o **alertas** separador do <em>< nome da coleção\></em>   **Propriedades** caixa de diálogo.  
   >   -   Ao implementar uma política antimalware do Endpoint Protection para a coleção.  
   >   -   Quando ativa e implementa definições de cliente do Endpoint Protection para a coleção.  

4. Reveja as informações que são apresentadas no **estado de segurança** e **estado operacional** secções. Pode clicar em qualquer ligação de estado para criar uma coleção temporária no nó **Dispositivos** da área de trabalho **Ativos e Compatibilidade** . A coleção temporária contém os computadores com o estado selecionado.  

   > [!IMPORTANT]  
   >  Informações que são apresentadas na **estado do Endpoint Protection** nó baseia-se nos últimos dados que foram resumidos a partir da base de dados do Configuration Manager e poderão não ser atuais. Se pretender obter os dados mais recentes, no separador **Home Page** , clique em **Executar Resumo**ou clique em **Agendar Resumo** para ajustar o intervalo de resumo.  

##  <a name="BKMK_2"></a> Como monitorizar o Endpoint Protection na ativos e conformidade área de trabalho  

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  

2.  Na **ativos e compatibilidade** área de trabalho, execute uma das seguintes ações:  

    -   Clique em **dispositivos**. Na lista **Dispositivos** , selecione um computador e, em seguida, clique no separador **Detalhe de Software Maligno** .  

    -   Clique em **coleções de dispositivos**. Na lista **Coleções de Dispositivos** , selecione a coleção que contém o computador que pretende monitorizar e, em seguida, no separador **Home Page** , no grupo **Coleção** , clique em **Mostrar Membros**.  

3.  Na *< nome da coleção\>*  lista, selecione um computador e, em seguida, clique nas **detalhe de software maligno** separador.  

##  <a name="BKMK_3"></a> Como monitorizar o Endpoint Protection através de relatórios  
 Utilize os seguintes relatórios para ver informações sobre o Endpoint Protection na sua hierarquia. Também pode utilizar estes relatórios para ajudar a resolver quaisquer problemas do Endpoint Protection. Para obter mais informações sobre como configurar relatórios no Configuration Manager, consulte [relatórios no System Center Configuration Manager](../../core/servers/manage/reporting.md) e [ficheiros de registo no System Center Configuration Manager](../../core/plan-design/hierarchy/log-files.md). Os relatórios de proteção de ponto final estão na pasta do Endpoint Protection.  

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
|**Falhou**|Falha na proteção de ponto final remediar o software maligno. Verifique os registos para obter detalhes do erro.<br /><br /> **Nota:** Para obter uma lista do Configuration Manager e os ficheiros de registo do Endpoint Protection, consulte a secção "Endpoint Protection" a [ficheiros de registo no System Center Configuration Manager](../../core/plan-design/hierarchy/log-files.md) tópico.|  
|**Removidas**|Endpoint Protection removido com êxito o software maligno.|  
|**Em quarentena**|Endpoint Protection moveu o software maligno para uma localização segura e impediu que fosse executado até removê-lo ou permitir que seja executado.|  
|**Limpo**|O software maligno foi limpo no ficheiro infetado.|  
|**Permitido**|Um utilizador administrativo optou por permitir a execução do software que contém o software maligno.|  
|**Nenhuma ação**|Proteção de ponto final não executou qualquer ação no software maligno. Esta situação pode ocorrer se o computador for reiniciado depois de o software maligno ser detetado e o software maligno já não é detetado; por exemplo, se uma unidade de rede mapeada na qual seja detetado software maligno não for religada quando o computador é reiniciado.|  
|**Bloqueado**|Proteção de ponto final bloqueado a execução do software maligno. Esta situação pode ocorrer se for encontrado um processo no computador que contém software maligno.|
