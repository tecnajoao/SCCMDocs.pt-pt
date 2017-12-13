---
title: "Gerir pacotes de atualização do sistema operativo"
titleSuffix: Configuration Manager
description: "Saiba como gerir pacotes de atualização do sistema operativo no System Center Configuration Manager."
ms.custom: na
ms.date: 12/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b9b22655-b8c1-461f-8047-3a7e906f647a
caps.latest.revision: "12"
caps.handback.revision: "0"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: b70e8ecd32957f19b9738d14c94c7e54b0312ea5
ms.sourcegitcommit: 08f9854fb6c6d21e1e923b13e38a64d0bc2bc9a4
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/12/2017
---
# <a name="manage-operating-system-upgrade-packages-with-system-center-configuration-manager"></a>Gerir pacotes de atualização do sistema operativo com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Um pacote de atualização no System Center Configuration Manager contém os ficheiros de origem de configuração do Windows que são utilizados para atualizar um sistema operativo existente num computador. Utilize as seguintes secções para gerir pacotes de atualização do sistema operativo no Configuration Manager.

##  <a name="BKMK_AddOSUpgradePkgs"></a> Adicionar pacotes de atualização do sistema operativo no Configuration Manager  
 Antes de poder utilizar um pacote de atualização do sistema operativo, tem de adicionar o pacote para um site do Configuration Manager. Utilize o procedimento seguinte para adicionar um pacote de atualização do sistema operativo a um site.  

#### <a name="to-add-an-operating-system-upgrade-package"></a>Para adicionar um pacote de atualização do sistema operativo  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**e clique em **Pacotes de atualização de Sistema Operativo**.  

3.  No separador **Home Page** , no grupo **Criar** , clique em **Adicionar Atualização de Sistema Operativo** para iniciar o Assistente para Adicionar Atualização de Sistema Operativo.  

4.  Na página **Origem de Dados** , especifique o caminho de rede para os ficheiros de origem de instalação do pacote de atualização do sistema operativo. Por exemplo, especifique o UNC **\\\server\path** onde estão instalados os ficheiros de origem de instalação.  

    > [!NOTE]  
    >  Os ficheiros de origem de instalação contêm Setup.exe e outros ficheiros e pastas para instalar o sistema operativo.  

    > [!IMPORTANT]  
    >  Limite o acesso aos ficheiros de origem de instalação para impedir a adulteração indesejável.  

5.  Na página **Geral** , especifique as seguintes informações e clique em **Seguinte**. Estas informações são úteis para fins de identificação quando tem vários programas de instalação do sistema operativo.  

    -   **Nome**: Especifique o nome do programa de instalação de sistema operativo.  

    -   **Versão**: Especifique a versão da instalação do sistema operativo.  

    -   **Comentário**: Especifique uma breve descrição da instalação do sistema operativo.  

6.  Conclua o assistente.  

 É agora possível distribuir o programa de instalação do sistema operativo pelos pontos de distribuição a que se acede através das sequências de tarefas de implementação.  

##  <a name="BKMK_DistributeBootImages"></a> Distribuir imagens do sistema operativo por pontos de distribuição  
 As imagens do sistema operativo são distribuídas por pontos de distribuição da mesma forma que são distribuídos outros conteúdos. Na maioria dos casos, terá de distribuir a imagem do sistema operativo por, pelo menos, um ponto de distribuição antes de implementar o sistema operativo. Para obter os passos para distribuir uma imagem do sistema operativo, veja [Distribuir conteúdo](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

##  <a name="BKMK_OSUpgradePkgApplyUpdates"></a> Aplicar atualizações de software num pacote de atualização do sistema operativo  
 A partir do Configuration Manager versão 1602, pode aplicar novas atualizações de software à imagem do sistema operativo no seu pacote de atualização do sistema operativo. Antes de poder aplicar as atualizações de software a um pacote de atualização que tem de ter o software de atualizações de infraestrutura no local e com êxito atualizações de software sincronizadas, transferir as atualizações de software para a biblioteca de conteúdos no servidor do site. Para obter mais informações, consulte [implementar atualizações de software](../../sum/deploy-use/deploy-software-updates.md).  

 Pode aplicar atualizações de software aplicáveis a um pacote de atualização numa agenda especificada. Na agenda que especificar, o Configuration Manager aplica as atualizações de software que selecionar para o pacote de atualização do sistema operativo e, em seguida, distribui opcionalmente o pacote de atualização atualizado a pontos de distribuição. As informações sobre o pacote de atualização do sistema operativo são armazenadas na base de dados do site, incluindo as atualizações de software que foram aplicadas no momento da importação. As atualizações de software aplicadas ao pacote de atualização desde que foi adicionado inicialmente também são armazenadas na base de dados do site. Ao iniciar o assistente para aplicar as atualizações de software ao pacote de atualização do sistema operativo, o assistente obtém uma lista de atualizações de software aplicáveis que ainda não foram aplicadas ao pacote de atualização para que possa selecioná-las. Configuration Manager copia as atualizações de software da biblioteca de conteúdos no servidor do site e aplica as atualizações de software para o pacote de atualização do sistema operativo.  

 Utilize o procedimento seguinte para aplicar atualizações de software a um pacote de atualização do sistema operativo.  

#### <a name="to-apply-software-updates-to-an-operating-system-upgrade-package"></a>Aplicar atualizações de software a um pacote de atualização do sistema operativo  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**e clique em **Pacotes de atualização de Sistema Operativo**.  

3.  Selecione o pacote de atualização do sistema operativo em relação ao qual pretende aplicar atualizações de software.  

4.  No separador **Home Page** , no grupo **Pacotes de Atualização do Sistema Operativo** , clique em **Agendar Atualizações** para iniciar o assistente.  

5.  Na página **Escolher as Atualizações** , selecione as atualizações de software para aplicar à imagem do sistema operativo e clique em **Seguinte**.  

6.  Na página **Definir Agendamento** , especifique as seguintes definições e clique em **Seguinte**.  

    1.  **Agenda**: Especifique o agendamento para quando as atualizações de software são aplicadas à imagem do sistema operativo.  

    2.  **Continuar com o erro**:  Selecione esta opção para continuar a aplicar atualizações de software à imagem, mesmo se ocorrer um erro.  

    3.  **Distribuir a imagem por pontos de distribuição**: Selecione esta opção para atualizar a imagem do sistema operativo em pontos de distribuição após as atualizações de software são aplicadas.  

7.  Na página **Resumo** , verifique as informações e clique em **Seguinte**.  

8.  Na página **Conclusão** , confirme que as atualizações de software foram aplicadas com êxito na imagem do sistema operativo.  
