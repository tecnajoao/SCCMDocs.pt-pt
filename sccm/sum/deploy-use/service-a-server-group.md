---
title: "Um grupo de servidores de serviço | Documentos do Microsoft"
description: "A consola do System Center Configuration Manager fornece alertas e os Estados para monitorizar as atualizações e conformidade."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 12/07/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: 304a83ea-0f72-437d-9688-2e6e0c7526dd
ms.translationtype: Machine Translation
ms.sourcegitcommit: af5f58dd5fe1f19d7a70cb9516af159c6682d194
ms.openlocfilehash: ae09a02dd5d67113b9a7e2ce146c844efa4caf55
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
>[!IMPORTANT]
>Esta é uma funcionalidade pré-lançamento disponível no Configuration Manager versão 1606 e versão 1610. As funcionalidades de pré-lançamento estão incluídas no produto para um teste antecipado num ambiente de produção, mas devem não ser consideradas prontas para produção. Tem de ativar esta funcionalidade para este ficar disponível. Para obter mais informações, veja [Utilizar as funcionalidades da versão de pré-lançamento de atualizações](https://docs.microsoft.com/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease).


# <a name="service-a-server-group"></a>Fazer manutenção a um grupo de servidores

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

A partir do System Center Configuration Manager versão 1606, pode configurar definições de grupo do servidor para uma coleção para definir quantos, que percentagem ou em que ordem os computadores na coleção serão instaladas as atualizações de software. Também pode configurar implementação pré e pós-implementação de scripts do PowerShell para executar as ações personalizadas.

Ao implementar atualizações de software para uma coleção que tenha definições de grupo do servidor configuradas, Configuration Manager determina como quantos computadores na coleção pode instalar as atualizações de software num determinado momento e disponibiliza o mesmo número de bloqueios de implementação. Apenas os computadores que obter um bloqueio de implementação irão iniciar a instalação da atualização de software. Quando estiver disponível um bloqueio de implementação, um computador obtém o bloqueio de implementação, instala as atualizações de software e, em seguida, liberta o bloqueio de implementação quando concluir a instalação de atualizações de software com êxito. Em seguida, o bloqueio de implementação torna-se disponível para outros computadores. Se um computador for não é possível libertar um bloqueio de implementação, pode libertar manualmente todos os bloqueios de implementação de grupo de servidor para a coleção.

>[!IMPORTANT]
>Todos os computadores na coleção devem ser atribuídos ao mesmo site.

#### <a name="to-create-a-collection-for-a-server-group"></a>Para criar uma coleção para um grupo de servidores  
As definições de grupo do servidor são configuradas nas propriedades de uma coleção de dispositivos. Para um grupo de servidores de serviço, todos os membros da coleção devem ser atribuídos ao mesmo site. Utilize os seguintes passos para criar uma coleção e configurar as definições de grupo do servidor:
1.  [Criar uma coleção de dispositivos](../../core/clients/manage/collections/create-collections.md) que contém os computadores no grupo de servidor.  

2.  No **ativos e compatibilidade** área de trabalho, clique em **coleções de dispositivos**, faça duplo clique na coleção que contém os computadores no grupo de servidor e, em seguida, clique em **propriedades**.  

3.  No **geral** separador, selecione **todos os dispositivos fazem parte do mesmo grupo de servidor**e, em seguida, clique em **definições**.  

4.  No **definições de grupo do servidor** página, especifique uma das seguintes definições:  

    -   **Permitir que uma percentagem das máquinas para sejam atualizadas ao mesmo tempo**: Especifica que são atualizados apenas numa determinada percentagem de clientes em qualquer momento. Se, por exemplo, a coleção tem 10 clientes e a coleção é configurada para atualização 30% do clientes ao mesmo tempo, em seguida, apenas 3 clientes irão instalar atualizações de software num determinado momento.  

    -   **Permitir que um número de máquinas para sejam atualizadas ao mesmo tempo**: Especifica que apenas um determinado número de clientes é atualizado ao mesmo tempo.  

    -   **Especifique a sequência de manutenção**: Especifica que os clientes na coleção serão atualizado um de cada vez na sequência que configurar. Um cliente apenas irá instalar atualizações de software após o cliente que está adiantada-lo na lista terminar a atualizações de software.  

5.  Especifique se pretende utilizar um script de pré-implementação (drenagem de nó) ou scripts pós-implementação (currículo de nó).  

    > [!WARNING]
    > Scripts personalizados não são assinados pela Microsoft. É sua responsabilidade em relação a manter a integridade destes scripts.

    > [!TIP]  
    > Seguem-se exemplos que pode utilizar testes de pré-implementação e scripts pós-implementação que escreverem a hora atual para um ficheiro de texto:  
    >   
    >  **Pré-implementação**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\start.txt`  
    >   
    >  **Pós-implementação**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\end.txt`  

## <a name="deploy-software-updates-to-the-server-group-and-monitor-status"></a>Implementar atualizações de software para o estado de grupo e o monitor de servidor  
Implementar atualizações de software para a coleção de grupo do servidor utilizando o processo de implementação típica. Depois de implementar as atualizações de software, pode monitorizar a implementação de atualizações de software na consola do Configuration Manager.
1.  [Implementar atualizações de software](manually-deploy-software-updates.md) na coleção de grupo do servidor.   

2.  [Monitorizar a implementação de atualização de software](monitor-software-updates.md). Para além de padrão de vistas para implementação de atualizações de software, de monitorização de **aguardar pelo bloqueio** estado é apresentado quando um cliente está a aguardar o desativar instalar as atualizações de software. Pode rever o ficheiro de UpdatesDeployment.log para obter mais informações.


## <a name="clear-the-deployment-locks-for-computers-in-a-server-group"></a>Desmarque os bloqueios de implementação para computadores de um grupo de servidores  
Quando um computador falhar ao libertar um bloqueio de implementação, pode libertar manualmente todos os bloqueios de implementação de grupo de servidor para a coleção. Desmarque bloqueios apenas quando uma implementação está bloqueada de atualização de computadores na coleção e não existirem computadores que ainda não estar em conformidade.  
1.  No **ativos e compatibilidade** área de trabalho, clique em **coleções de dispositivos**e clique na coleção para limpar os bloqueios de implementação.  

2.  No **base** separador o **implementação** grupo, clique em **bloqueia de implementação de grupo de servidor limpar**. Quando os clientes falharam ao instalar as atualizações de software e estão a impedir a outros clientes de instalar as atualizações de software, os bloqueios de implementação podem ser desmarcados manualmente.  

