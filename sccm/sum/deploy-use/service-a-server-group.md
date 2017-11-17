---
title: "Fazer manutenção a um grupo de servidores"
titleSuffix: Configuration Manager
description: "A consola do System Center Configuration Manager disponibiliza alertas e Estados para monitorizar as atualizações e conformidade."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 12/07/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: 304a83ea-0f72-437d-9688-2e6e0c7526dd
ms.openlocfilehash: 12382015f2b673103c3c0d8fc9c0cbf29511a434
ms.sourcegitcommit: 986fc2d54f7c5fa965fd4df42f4db4ecce6b79cb
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 11/17/2017
---
# <a name="service-a-server-group"></a>Fazer manutenção a um grupo de servidores

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

>[!IMPORTANT]
>Funcionalidades de pré-lançamento são funcionalidades que estão no ramo atual para um teste antecipado num ambiente de produção. Estas funcionalidades são totalmente suportadas, mas ainda estão em desenvolvimento Active Directory e poderão receber alterações até que mudam fora da categoria da versão de pré-lançamento. Tem de ativar esta funcionalidade para que fique disponível. Para obter mais informações, veja [Utilizar as funcionalidades da versão de pré-lançamento de atualizações](https://docs.microsoft.com/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease).

Começando no System Center Configuration Manager versão 1606, pode configurar definições de grupo do servidor para uma coleção para definir quantos, que percentagem ou a ordem pela qual os computadores na coleção irão instalar atualizações de software. Também pode configurar scripts do PowerShell de pré-implementação e pós-implementação para executar ações personalizadas.

Quando implementa atualizações de software para uma coleção que tenha as definições de grupo do servidor configuradas, o Configuration Manager determina quantos computadores na coleção pode instalar as atualizações de software em qualquer momento e disponibiliza o mesmo número de bloqueios de implementação. Apenas os computadores que obter um bloqueio de implementação irão iniciar a instalação da atualização de software. Quando estiver disponível um bloqueio de implementação, um computador obtém o bloqueio de implementação, instala as atualizações de software e, em seguida, liberta o bloqueio de implementação quando a instalação de atualizações de software estiver concluída com êxito. Em seguida, o bloqueio de implementação fica disponível para outros computadores. Se um computador não é possível libertar um bloqueio de implementação, pode de versão manualmente todos os bloqueios de implementação de grupo de servidor para a coleção.

>[!IMPORTANT]
>Todos os computadores na coleção devem ser atribuídos ao mesmo site.

#### <a name="to-create-a-collection-for-a-server-group"></a>Para criar uma coleção para um grupo de servidores  
As definições do grupo de servidor são configuradas nas propriedades de uma coleção de dispositivos. Um grupo de servidores de serviço, todos os membros da coleção devem ser atribuídos ao mesmo site. Utilize os seguintes passos para criar uma coleção e configurar as definições de grupo do servidor:
1.  [Criar uma coleção de dispositivos](../../core/clients/manage/collections/create-collections.md) que contenha os computadores no grupo de servidor.  

2.  No **ativos e compatibilidade** área de trabalho, clique em **coleções de dispositivos**, faça duplo clique na coleção que contém os computadores no grupo de servidor e, em seguida, clique em **propriedades**.  

3.  No **geral** separador, selecione **todos os dispositivos fazem parte do mesmo grupo de servidor**e, em seguida, clique em **definições**.  

4.  No **as definições do grupo de servidor** página, especifique uma das seguintes definições:  

    -   **Permitir que uma percentagem das máquinas seja atualizada ao mesmo tempo**: Especifica que apenas determinada percentagem de clientes são atualizadas ao mesmo tempo. Se, por exemplo, a coleção tem 10 clientes, e a coleção é configurada para atualização 30% de clientes ao mesmo tempo, em seguida, apenas 3 clientes irão instalar atualizações de software em qualquer momento.  

    -   **Permitir que um número de máquinas seja atualizada ao mesmo tempo**: Especifica que apenas um determinado número de clientes é atualizado ao mesmo tempo.  

    -   **Especifique a sequência de manutenção**: Especifica que os clientes na coleção será atualizado um de cada vez na sequência que configurar. Um cliente apenas irá instalar atualizações de software depois do cliente que está à frente das-la na lista concluiu a instalação respetivas atualizações de software.  

5.  Especifique se pretende utilizar um script de pré-implementação (drenagem do nó) ou um script de pós-implementação (retoma do nó).  

    > [!WARNING]
    > Scripts personalizados não são assinados pela Microsoft. É da responsabilidade do cliente para manter a integridade destes scripts.

    > [!TIP]  
    > Seguem-se exemplos que pode utilizar no teste de pré-implementação e pós-implementação scripts que escrevem a hora atual para um ficheiro de texto:  
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

## <a name="deploy-software-updates-to-the-server-group-and-monitor-status"></a>Implementar atualizações de software para o estado do monitor e o grupo de servidor  
Implementar atualizações de software para a coleção de grupo de servidor utilizando o processo de implementação típica. Depois de implementar as atualizações de software, pode monitorizar a implementação de atualização de software na consola do Configuration Manager.
1.  [Implementar atualizações de software](manually-deploy-software-updates.md) na coleção de grupo do servidor.   

2.  [Monitorizar a implementação de atualização de software](monitor-software-updates.md). Para além do padrão para a implementação de atualizações de software, as vistas de monitorização de **à espera de bloqueio** estado é apresentado quando um cliente está a aguardar a ativar instalar as atualizações de software. Pode rever o ficheiro UpdatesDeployment.log para mais informações.


## <a name="clear-the-deployment-locks-for-computers-in-a-server-group"></a>Limpar os bloqueios de implementação para computadores num grupo de servidor  
Quando um computador falhar ao libertar um bloqueio de implementação, pode de versão manualmente todos os bloqueios de implementação de grupo de servidor para a coleção. Limpar bloqueios apenas quando uma implementação é bloqueada a atualizar os computadores na coleção e não existirem computadores continuam não compatíveis.  
1.  No **ativos e compatibilidade** área de trabalho, clique em **coleções de dispositivos**e clique na coleção para limpar os bloqueios de implementação.  

2.  No **home page** separador o **implementação** , clique em **bloqueia de implementação de grupo de servidor limpar**. Quando os clientes não tem conseguido instalar as atualizações de software e estão a impedir outros clientes instalar as atualizações de software, os bloqueios de implementação podem ser eliminados manualmente.  
