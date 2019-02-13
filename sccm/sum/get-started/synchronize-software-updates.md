---
title: Gerir a sincronização de atualizações de software
titleSuffix: Configuration Manager
description: Utilize estes passos para agendar a sincronização de atualizações de software, manualmente iniciar a sincronização de atualizações de software e monitorizar a sincronização de atualizações de software.
author: aczechowski
ms.date: 12/20/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: ea8698c4-9df5-4cf5-8b62-ab93115b4769
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 543a7867ca40cded389ee3ce875845dd32631274
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56123523"
---
#  <a name="BKMK_SUMSync"></a> Sincronizar atualizações de software

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

 Sincronização de atualizações de software no Configuration Manager é o processo de obtenção dos metadados de atualização de software que cumprem os critérios que configurou. Isto inclui produtos específicos, classificações e idiomas. Normalmente, o ponto de atualização de software no site de administração central ou num site primário autónomo, obtém os metadados do Microsoft Update. Em seguida, o site de nível superior envia um pedido de sincronização para outros sites. Quando um site recebe o pedido de sincronização do site principal, o ponto de atualização de software para o site obtém os metadados de atualizações de software do seu montante [origem de sincronização](../plan-design/plan-for-software-updates.md#BKMK_SyncSource). Para obter mais informações sobre o processo de sincronização de atualizações de software, consulte [sincronização de atualizações de Software](../understand/software-updates-introduction.md#BKMK_Synchronization).

Configurar a sincronização de atualização de software para ser executada com base numa agenda nas propriedades para o ponto de atualização de software no site de nível superior. Depois de configurar a agenda de sincronização, normalmente não alterar o agendamento como parte das operações normais. No entanto, pode iniciar manualmente a sincronização de atualizações de software quando for necessário.

  > [!NOTE]  
  >  Pontos de atualização de software tem de estar ligados à sua origem de sincronização a montante para sincronizar atualizações de software. Se um ponto de atualização de software estiver desligado da respetiva origem de sincronização a montante, poderá utilizar o método de exportação e importação para sincronizar as atualizações de software. Para obter mais informações, veja [Sincronizar atualizações de software a partir de um ponto de atualização de software desligado](synchronize-software-updates-disconnected.md).  

## <a name="schedule-software-updates-synchronization"></a>Agenda de sincronização de atualizações de software
Quando configura uma agenda de sincronização de atualizações de software, o ponto de atualização de software de nível superior inicia a sincronização com o Microsoft Update, a data e hora agendadas. A agenda personalizada permite-lhe sincronizar atualizações de software numa data e hora que os pedidos do servidor Windows Server Update Services (WSUS), servidor de sites e rede são baixos. Por exemplo, pode definir a agenda, para que as atualizações de software são sincronizadas a todas as semanas às 2:00. Durante a sincronização agendada, todas as alterações nos metadados de atualizações de software desde a última sincronização agendada são inseridas na base de dados do site. Isto inclui novos metadados de atualizações de software ou metadados que foram modificados, removidos ou que agora expiraram.

Utilize os procedimentos seguintes no site de nível superior para agendar a sincronização de atualizações de software.  

#### <a name="to-schedule-software-updates-synchronization"></a>Para agendar a sincronização de atualizações de software  

  1.  Na consola do Configuration Manager, clique em **Administração**.  

  2.  Na área de trabalho Administração, expanda **Configuração do Site**e clique em **Sites**.  

  3.  No painel de resultados, clique no site de administração central ou no site autónomo principal.  

  4.  No separador **Home Page** , no grupo **Definições** , expanda **Configurar Componentes do Site**e clique em **Ponto de Atualização de Software**.  

  5.  Na caixa de diálogo Propriedades do Componente do Ponto de Atualização de Software, selecione **Ativar sincronização num agendamento**e, em seguida, especifique o agendamento da sincronização.  

## <a name="manually-start-software-updates-synchronization"></a>Iniciar manualmente a sincronização de atualizações de software
Pode iniciar manualmente a sincronização de atualizações de software no site de nível superior na consola do Configuration Manager a partir do **todas as atualizações de Software** nó no **biblioteca de Software** área de trabalho.  

Utilize os procedimentos seguintes no site de nível superior para iniciar manualmente a sincronização de atualizações de software.  

#### <a name="to-manually-start-software-updates-synchronization"></a>Para iniciar manualmente o software de sincronização de atualizações  

1. Na consola do Configuration Manager que está ligada ao site de administração central ou site primário autónomo, clique em **biblioteca de Software**.  

2. Na área de trabalho Biblioteca de Software, expanda **Atualizações de Software** e clique em **Todas as Atualizações de Software** ou em **Grupos de Atualizações de Software**.  

3. No separador **Home Page** , no grupo **Criar** , clique em **Sincronizar Atualizações de Software**. Clique em **Sim** na caixa de diálogo para confirmar que quer iniciar o processo de sincronização.  

   Após iniciar o processo de sincronização no ponto de atualização de software, pode monitorizar o processo de sincronização a partir da consola do Configuration Manager para todos os pontos de atualização de software na sua hierarquia. Utilize o seguinte procedimento para monitorizar o processo de sincronização de atualizações de software.  


## <a name="monitor-software-updates-synchronization"></a>Monitor de sincronização de atualizações de software
Após iniciar o processo de sincronização, pode utilizar a consola do Configuration Manager para monitorizar o processo para todos os pontos de atualização de software na sua hierarquia. Utilize o seguinte procedimento para monitorizar o processo de sincronização de atualizações de software. Para obter mais informações sobre a monitorização de atualizações de software, incluindo o processo de sincronização, consulte [monitorizar atualizações de software](../deploy-use/monitor-software-updates.md).

#### <a name="to-monitor-the-software-updates-synchronization-process"></a>Para monitorizar o processo de sincronização de atualizações de software  

1. Na consola do Configuration Manager, clique em **monitorização**.  

2. Na área de trabalho **Monitorização** , clique em **Estado de Sincronização do Ponto de Atualização de Software**.  

   Os pontos de atualização de software na sua hierarquia do Configuration Manager são apresentados no painel de resultados. A partir desta vista, poderá monitorizar o estado de sincronização de todos os pontos de atualização de software. Quando quiser obter informações mais detalhadas sobre o processo de sincronização, pode consultar o ficheiro wsyncmgr.log que está localizado em <*ConfigMgrInstallationPath*>\Logs em cada servidor do site.  

## <a name="import-updates-from-the-microsoft-update-catalog"></a>Importar as atualizações do catálogo Microsoft Update

O ponto de atualização de Software de nível superior usarem o WSUS para obter informações sobre atualizações de software da Microsoft para o Configuration Manager. Ocasionalmente, poderá ter uma atualização que não sincronizar automaticamente no WSUS, para os seus produtos selecionados e classificações, mas está disponível na [catálogo Microsoft Update](https://catalog.update.microsoft.com). As atualizações que não sincronizar automaticamente no WSUS, destinam-se, normalmente, para resolver problemas de altamente específicos. Normalmente, se uma atualização está disponível no catálogo, pode importá-lo no WSUS. Pode, em seguida, sincronizá-la para o Configuration Manager e implementá-lo como qualquer outra atualização.

### <a name="to-import-an-update-from-the-microsoft-update-catalog"></a>Para importar uma atualização do catálogo Microsoft Update

1. Abra a consola de administração do WSUS e ligue-o para o servidor WSUS nível superior na sua hierarquia do SCCM. 
   - Se o Internet Explorer não seja o navegador da web padrão do computador, temporariamente defini-lo como predefinição.
2. Clique em **atualizações** ou clique no nome do servidor WSUS. 
3. Na **ações** painel, selecione **atualizações de importação...**  que irá abrir uma janela do browser para o [catálogo Microsoft Update](https://catalog.update.microsoft.com).
   ![Selecione importar atualizações na consola do WSUS](media/wsus-console-import-updates.png)
4. Se lhe for pedido, instale o controle ActiveX de catálogo do Microsoft Update. O controle deve ser instalado para importar as atualizações no WSUS. 
5. Na janela do browser, procure a atualização que pretende. Clique nas **adicionar*** botão para adicioná-lo ao cesto.
6. Clique em **ver cesto**. Certifique-se de que a opção para **importação diretamente para o Windows Server Update Services** está selecionada. Em seguida, clique em **importação**.
    ![Importar atualização a partir do catálogo no WSUS](./media/import-catalog-update-into-wsus.png)
7. Quando a importação estiver concluída, clique em **fechar** na janela do browser.
     - Repor o seu browser predefinido se for necessário.
8. Sincronize o seu ponto de atualização de Software do Configuration Manager.


## <a name="next-steps"></a>Passos seguintes
Depois de sincronizar as atualizações de software pela primeira vez ou depois de existirem novas classificações ou produtos disponíveis, deve [configurar a novas classificações e produtos](configure-classifications-and-products.md) para sincronizar atualizações de software com os critérios de novo .

Depois de sincronizar as atualizações de software com os critérios que necessita, [gerir definições de atualizações de software](manage-settings-for-software-updates.md).  
