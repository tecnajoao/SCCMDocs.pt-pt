---
title: Gerir a sincronização de atualizações de software
titleSuffix: Configuration Manager
description: Utilize estes passos para agendar a sincronização de atualizações de software, manualmente iniciar a sincronização de atualizações de software e monitorizar a sincronização de atualizações de software.
author: aczechowski
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: ea8698c4-9df5-4cf5-8b62-ab93115b4769
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 7e2e5493f1aaee448c6573d08a57a69aafb478c7
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
#  <a name="BKMK_SUMSync"></a> Sincronizar atualizações de software

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

 Sincronização de atualizações de software no Configuration Manager é o processo de obtenção de metadados de atualização de software que cumprem os critérios que configurou. Isto inclui idiomas, classificações e produtos específicos. Normalmente, o ponto de atualização de software no site de administração central ou num site primário autónomo, obtém os metadados a partir do Microsoft Update. Em seguida, o site de nível superior envia um pedido de sincronização para outros sites. Quando um site recebe o pedido de sincronização do site principal, o ponto de atualização de software para o site obtém metadados de atualizações de software a montante de [origem de sincronização](../plan-design/plan-for-software-updates.md#BKMK_SyncSource). Para mais informações sobre o processo de sincronização de atualizações de software, consulte [sincronização de atualizações de Software](../understand/software-updates-introduction.md#BKMK_Synchronization).

Configurar a sincronização de atualização de software para ser executada com base numa agenda nas propriedades para o ponto de atualização de software no site de nível superior. Normalmente, após configurar a agenda de sincronização não necessitará de alterar a agenda no contexto das operações normais. No entanto, poderá iniciar manualmente a sincronização de atualizações de software quando for necessário.

  > [!NOTE]  
  >  Pontos de atualização de software devem estar ligados à respetiva origem de sincronização a montante para sincronizar atualizações de software. Se um ponto de atualização de software estiver desligado da respetiva origem de sincronização a montante, poderá utilizar o método de exportação e importação para sincronizar as atualizações de software. Para obter mais informações, veja [Sincronizar atualizações de software a partir de um ponto de atualização de software desligado](synchronize-software-updates-disconnected.md).  

## <a name="schedule-software-updates-synchronization"></a>Agenda de sincronização de atualizações de software
Quando configura uma agenda de sincronização de atualizações de software, o ponto de atualização de software de nível superior inicia a sincronização com o Microsoft Update, a data e hora agendadas. A agenda personalizada permite-lhe sincronizar atualizações de software numa data e hora quando os pedidos do servidor WSUS, servidor de sites e rede são baixos. Por exemplo, pode definir a agenda para que as atualizações de software sejam sincronizadas todas as semanas às 2:00. Durante a sincronização agendada, todas as alterações nos metadados de atualizações de software desde a última sincronização agendada são inseridas na base de dados do site. Isto inclui novos metadados de atualizações de software ou metadados que foram modificados, removidos ou que agora expiraram.

Utilize os procedimentos seguintes no site de nível superior para agendar a sincronização de atualizações de software.  

#### <a name="to-schedule-software-updates-synchronization"></a>Para agendar a sincronização de atualizações de software  

  1.  Na consola do Configuration Manager, clique em **Administração**.  

  2.  Na área de trabalho Administração, expanda **Configuração do Site**e clique em **Sites**.  

  3.  No painel de resultados, clique no site de administração central ou no site autónomo principal.  

  4.  No separador **Home Page** , no grupo **Definições** , expanda **Configurar Componentes do Site**e clique em **Ponto de Atualização de Software**.  

  5.  Na caixa de diálogo Propriedades do Componente do Ponto de Atualização de Software, selecione **Ativar sincronização num agendamento**e, em seguida, especifique o agendamento da sincronização.  

## <a name="manually-start-software-updates-synchronization"></a>Iniciar manualmente a sincronização de atualizações de software
Pode iniciar manualmente a sincronização de atualizações de software no site de nível superior na consola do Configuration Manager a partir de **todas as atualizações de Software** no nó o **biblioteca de Software** área de trabalho.  

Utilize os procedimentos seguintes no site de nível superior para iniciar manualmente a sincronização de atualizações de software.  

#### <a name="to-manually-start-software-updates-synchronization"></a>Para iniciar manualmente o software de sincronização de atualizações  

  1.  Na consola do Configuration Manager que está ligada ao site de administração central ou site primário autónomo, clique em **biblioteca de Software**.  

  2.  Na área de trabalho Biblioteca de Software, expanda **Atualizações de Software** e clique em **Todas as Atualizações de Software** ou em **Grupos de Atualizações de Software**.  

  3.  No separador **Home Page** , no grupo **Criar** , clique em **Sincronizar Atualizações de Software**. Clique em **Sim** na caixa de diálogo para confirmar que quer iniciar o processo de sincronização.  

   Após iniciar o processo de sincronização no ponto de atualização de software, pode monitorizar o processo de sincronização a partir da consola do Configuration Manager para todos os pontos de atualização de software na sua hierarquia. Utilize o seguinte procedimento para monitorizar o processo de sincronização de atualizações de software.  


## <a name="monitor-software-updates-synchronization"></a>Monitor de sincronização de atualizações de software
Após iniciar o processo de sincronização, pode utilizar a consola do Configuration Manager para monitorizar o processo para todos os pontos de atualização de software na sua hierarquia. Utilize o seguinte procedimento para monitorizar o processo de sincronização de atualizações de software. Para obter mais informações sobre a monitorização de atualizações de software, incluindo o processo de sincronização, consulte [monitorizar atualizações de software](../deploy-use/monitor-software-updates.md).

#### <a name="to-monitor-the-software-updates-synchronization-process"></a>Para monitorizar o processo de sincronização de atualizações de software  

  1.  Na consola do Configuration Manager, clique em **monitorização**.  

  2.  Na área de trabalho **Monitorização** , clique em **Estado de Sincronização do Ponto de Atualização de Software**.  

    Os pontos de atualização de software na sua hierarquia do Configuration Manager são apresentados no painel de resultados. A partir desta vista, poderá monitorizar o estado de sincronização de todos os pontos de atualização de software. Quando quiser obter informações mais detalhadas sobre o processo de sincronização, pode consultar o ficheiro wsyncmgr.log que está localizado em <*ConfigMgrInstallationPath*>\Logs em cada servidor do site.  

## <a name="next-steps"></a>Passos seguintes
Depois de sincronizar as atualizações de software pela primeira vez ou depois de existirem novas classificações ou produtos disponíveis, tem [configurar novas classificações e produtos](configure-classifications-and-products.md) para sincronizar atualizações de software com os critérios de novo.

Depois de sincronizar as atualizações de software com os critérios que precisa, [gerir as definições das atualizações de software](manage-settings-for-software-updates.md).  
