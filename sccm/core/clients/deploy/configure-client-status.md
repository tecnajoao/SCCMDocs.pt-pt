---
title: Configurar o estado do cliente | Microsoft Docs
description: "Selecione as definições de estado do cliente no System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a2275ba2-c83d-43e7-90ed-418963a707fe
caps.latest.revision: "6"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: fc898bf2433ab99eb0da9c60bd0e890bba97a415
ms.sourcegitcommit: b438515490e04fb09c82a8af642d38e9a0605178
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/15/2017
---
# <a name="how-to-configure-client-status-in-system-center-configuration-manager"></a>Como configurar o estado do cliente no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Antes de poder monitorizar o estado de cliente do System Center Configuration Manager e remediar problemas detetados, tem de configurar o seu site para especificar os parâmetros que são utilizados para marcar clientes como inativos e configurar opções para o alertar caso a atividade do cliente seja inferior a um limiar especificado. Também pode desativar computadores a partir de remediação automaticamente quaisquer problemas que encontre de estado do cliente.  

##  <a name="BKMK_1"></a>Para configurar o estado do cliente  

1.  Na consola do Configuration Manager, clique em **monitorização**.  

2.  No **monitorização** área de trabalho, clique em **estado do cliente**, em seguida, no **home page** separador o **estado do cliente** , clique em **as definições de estado do cliente**.  

3.  No **propriedades de definições de estado do cliente** diálogo caixa, especifique os valores seguintes para determinar a atividade do cliente:  

    > [!NOTE]  
    >  Se nenhuma das definições forem cumpridas, o cliente será marcado como inativo.  

    -   **Pedidos de política de cliente durante os dias seguintes:** Especifique o número de dias desde que um cliente solicitou a política. O valor predefinido é **7** dias.  

    -   **Deteção de heartbeat durante os dias seguintes:** Especifique o número de dias desde o computador cliente enviada um registo de deteção de heartbeat à base de dados do site. O valor predefinido é **7** dias.  

    -   **Inventário de hardware durante os dias seguintes:** Especifique o número de dias desde que o computador cliente enviou um registo de inventário de hardware na base de dados do site. O valor predefinido é **7** dias.  

    -   **Inventário de software durante os dias seguintes:** Especifique o número de dias desde que o computador cliente enviou um registo de inventário de software para a base de dados do site. O valor predefinido é **7** dias.  

    -   **Mensagens de estado durante os dias seguintes:** Especifique o número de dias desde que o computador cliente enviou mensagens de estado na base de dados do site. O valor predefinido é **7** dias.  

4.  No **propriedades de definições de estado do cliente** diálogo caixa, especifique o seguinte valor para determinar durante quanto os dados de histórico de estado do cliente são mantidos:  

    -   **Manter histórico do Estado de cliente para o número de dias seguinte:** Especifique quanto pretende que o histórico de estado do cliente permaneça na base de dados do site. O valor predefinido é **31** dias.  

5.  Clique em **OK** para guardar as propriedades e fechar o **propriedades de definições de estado do cliente** caixa de diálogo.  

##  <a name="BKMK_Schedule"></a>Para configurar a agenda para o estado do cliente  

1.  Na consola do Configuration Manager, clique em **monitorização**.  

2.  No **monitorização** área de trabalho, clique em **estado do cliente**, em seguida, no **home page** separador o **estado do cliente** , clique em **agendar atualização do Estado de cliente**.  

3.  No **agenda de atualização do Estado do cliente** diálogo caixa, configure o intervalo no qual pretende que o estado do cliente para atualizar e, em seguida, clique em OK.  

    > [!NOTE]  
    >  Quando alterar o agendamento para atualizações de estado do cliente, a atualização não terão efeito até que Atualize o estado do cliente agendada seguinte (para o agendamento configurado anteriormente).  

##  <a name="BKMK_2"></a>Para configurar alertas para o estado do cliente  

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  

2.  Na área de trabalho **Ativos e Compatibilidade** , clique em **Coleções de Dispositivos**.  

3.  Na lista **Coleções de Dispositivos** , selecione a coleção para a qual pretende configurar alertas e, no separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.  

    > [!NOTE]  
    >  Não é possível configurar alertas de coleções de utilizadores.  

4.  No **alertas** separador do * &lt;coleção nome\>***propriedades** caixa de diálogo, clique em **adicionar**.  

    > [!NOTE]  
    >  O separador **Alertas** só está visível se a função de segurança a que o utilizador está associado tiver permissões para alertas.  

5.  Na caixa de diálogo **Adicionar Novos Alertas da Coleção** , escolha os alertas que pretende que sejam gerados quando os limites do estado do cliente são inferiores a um valor específico e, em seguida, clique em **OK**.  

6.  Na lista **Condições** do separador **Alertas** , selecione cada um dos alertas do estado do cliente e especifique as informações seguintes.  

    -   **Nome do alerta** - aceite o nome predefinido ou introduza um novo nome para o alerta.  

    -   **Gravidade do alerta** – na lista pendente, escolha o nível de alerta que será apresentado na consola do Configuration Manager.  

    -   **Emitir um alerta** -especifique a percentagem de limiar do alerta.  

7.  Clique em **OK** para fechar o * &lt;coleção nome\>***propriedades** caixa de diálogo.  

##  <a name="BKMK_3"></a>Para excluir computadores da remediação automática  

1.  Abra o editor de registo no computador cliente para o qual pretende desativar a remediação automática.  

    > [!WARNING]  
    >  A utilização incorreta do Editor de registo poderá causar problemas graves que poderão exigir a reinstalação do sistema operativo. A Microsoft não garante que consiga resolver os problemas resultantes da utilização incorreta do Editor de Registo. A utilização do Editor de Registo é da exclusiva responsabilidade do utilizador.  

2.  Navegue para **HKEY_LOCAL_MACHINE\Software\Microsoft\CCM\CcmEval\NotifyOnly**.  

3.  Introduza um dos seguintes valores para esta chave de registo:  

    -   **Verdadeiro** -o computador cliente não irá remediar automaticamente quaisquer problemas detetados. No entanto, pode ainda será alertado no **monitorização** área de trabalho sobre quaisquer problemas com este cliente.  

    -   **FALSO** -o computador cliente irá remediar automaticamente problemas quando estes forem detetados e o utilizador será alertado no **monitorização** área de trabalho. Esta é a predefinição.  

4.  Feche o editor de registo.  

 Também pode instalar clientes utilizando o CCMSetup **NotifyOnly** propriedade de instalação para os excluir da remediação automática. Para obter mais informações sobre esta propriedade de instalação de cliente, consulte [acerca das propriedades de instalação de cliente no System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  
