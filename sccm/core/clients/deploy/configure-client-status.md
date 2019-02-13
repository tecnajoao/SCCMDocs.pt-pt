---
title: Configurar o estado do cliente
titleSuffix: Configuration Manager
description: Selecione as definições de estado do cliente no System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a2275ba2-c83d-43e7-90ed-418963a707fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 70c213a628c72d415a912f99ae5efd6f07150ebf
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56140750"
---
# <a name="how-to-configure-client-status-in-system-center-configuration-manager"></a>Como configurar o estado do cliente no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Antes de poder monitorizar o estado de cliente do System Center Configuration Manager e remediar problemas detetados, tem de configurar o seu site para especificar os parâmetros que são utilizados para marcar clientes como inativos e configurar opções para o alertar caso atividade do cliente cai abaixo de um limiar especificado. Também pode desativar a computadores a partir de remediar automaticamente quaisquer problemas que localiza o estado do cliente.  

##  <a name="BKMK_1"></a> Configurar o estado do cliente  

1.  Na consola do Configuration Manager, clique em **monitorização**.  

2.  Na **monitorização** área de trabalho, clique em **estado do cliente**, em seguida, no **home page** separador o **estado do cliente** , clique em **As definições de estado do cliente**.  

3.  Na **propriedades de definições de estado do cliente** diálogo caixa, especifique os valores seguintes para determinar a atividade do cliente:  

    > [!NOTE]  
    >  Se nenhuma das definições forem cumpridas, o cliente será marcado como inativo.  

    -   **Pedidos de política de cliente durante os dias seguintes:** Especifique o número de dias desde que um cliente solicitou a política. O valor predefinido é **7** dias.  

    -   **Deteção de heartbeat durante os dias seguintes:** Especifique o número de dias desde que o computador cliente enviada um registo de deteção de heartbeat à base de dados do site. O valor predefinido é **7** dias.  

    -   **Inventário de hardware durante os dias seguintes:** Especifique o número de dias desde que o computador cliente enviou um registo de inventário de hardware para a base de dados do site. O valor predefinido é **7** dias.  

    -   **Inventário de software durante os dias seguintes:** Especifique o número de dias desde que o computador cliente enviou um registo de inventário de software para a base de dados do site. O valor predefinido é **7** dias.  

    -   **Mensagens de estado durante os dias seguintes:** Especifique o número de dias desde que o computador cliente enviou mensagens de estado na base de dados do site. O valor predefinido é **7** dias.  

4.  Na **propriedades de definições de estado do cliente** diálogo caixa, especifique o seguinte valor para determinar como período de retenção de dados do histórico de estado de cliente:  

    -   **Manter histórico do Estado de cliente para o número de dias seguinte:** Especifique o tempo que pretende que o histórico de estado do cliente permaneça na base de dados do site. O valor predefinido é **31** dias.  

5.  Clique em **OK** para guardar as propriedades e fechar o **propriedades de definições de estado do cliente** caixa de diálogo.  

##  <a name="BKMK_Schedule"></a> Para configurar a agenda para o estado do cliente  

1.  Na consola do Configuration Manager, clique em **monitorização**.  

2.  Na **monitorização** área de trabalho, clique em **estado do cliente**, em seguida, no **home page** separador o **estado do cliente** , clique em **Agendar atualização do Estado do cliente**.  

3.  Na **agenda de atualização do Estado do cliente** diálogo caixa, configure o intervalo no qual pretende que o estado do cliente para atualizar e, em seguida, clique em OK.  

    > [!NOTE]  
    >  Quando alterar a agenda de atualizações de estado do cliente, a atualização não surtir efeito até que o estado do cliente agendada seguinte atualizar (para o agendamento configurado anteriormente).  

##  <a name="BKMK_2"></a> Para configurar alertas para o estado do cliente  

1. Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.  

2. Na área de trabalho **Ativos e Compatibilidade** , clique em **Coleções de Dispositivos**.  

3. Na lista **Coleções de Dispositivos** , selecione a coleção para a qual pretende configurar alertas e, no separador **Home Page** , no grupo **Propriedades** , clique em **Propriedades**.  

   > [!NOTE]  
   >  Não é possível configurar alertas de coleções de utilizadores.  

4. Sobre o **alertas** separador da  <em>&lt;coleção nome\></em>**propriedades** caixa de diálogo, clique em **adicionar**.  

   > [!NOTE]  
   >  O separador **Alertas** só está visível se a função de segurança a que o utilizador está associado tiver permissões para alertas.  

5. Na caixa de diálogo **Adicionar Novos Alertas da Coleção** , escolha os alertas que pretende que sejam gerados quando os limites do estado do cliente são inferiores a um valor específico e, em seguida, clique em **OK**.  

6. Na lista **Condições** do separador **Alertas** , selecione cada um dos alertas do estado do cliente e especifique as informações seguintes.  

   -   **Nome do alerta** – aceite o nome predefinido ou introduza um novo nome para o alerta.  

   -   **Gravidade do alerta** – na lista pendente, escolha o nível de alerta que será apresentado na consola do Configuration Manager.  

   -   **Emitir alerta** -especifique a percentagem de limiar do alerta.  

7. Clique em **OK** para fechar a  <em>&lt;coleção nome\></em>**propriedades** caixa de diálogo.  

##  <a name="BKMK_3"></a> Para excluir computadores da remediação automática  

1. Abra o editor de registo no computador cliente para o qual pretende desativar a remediação automática.  

   > [!WARNING]  
   >  A utilização incorreta do Editor de registo poderá causar problemas graves que poderão exigir a reinstalação do sistema operacional. A Microsoft não garante que consiga resolver os problemas resultantes da utilização incorreta do Editor de Registo. A utilização do Editor de Registo é da exclusiva responsabilidade do utilizador.  

2. Navegue para **HKEY_LOCAL_MACHINE\Software\Microsoft\CCM\CcmEval\NotifyOnly**.  

3. Introduza um dos seguintes valores para esta chave de registo:  

   -   **Verdadeiro** -o computador cliente não irá remediar automaticamente quaisquer problemas detetados. No entanto, ainda será alertado na **monitorização** área de trabalho sobre problemas com este cliente.  

   -   **FALSE** -o cliente irá remediar automaticamente problemas quando estes forem detetados e será alertado na **monitorização** área de trabalho. Esta é a predefinição.  

4. Feche o editor de registo.  

   Também pode instalar clientes utilizando o CCMSetup **NotifyOnly** propriedade de instalação para os excluir da remediação automática. Para obter mais informações sobre esta propriedade de instalação do cliente, consulte [acerca das propriedades de instalação de cliente no System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  
