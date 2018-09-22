---
title: Fazer manutenção a um grupo de servidores
titleSuffix: Configuration Manager
description: A consola do System Center Configuration Manager fornece alertas e os Estados para monitorizar as atualizações e a conformidade.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 12/07/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 304a83ea-0f72-437d-9688-2e6e0c7526dd
ms.openlocfilehash: 7c775df2446dbd0da1d9317982fc752dbfe5120a
ms.sourcegitcommit: 4e4b71227309bee7e9f1285971f8235c67a9c502
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/21/2018
ms.locfileid: "46533818"
---
# <a name="service-a-server-group"></a>Fazer manutenção a um grupo de servidores

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

>[!IMPORTANT]
>Funcionalidades de pré-lançamento são recursos que estão no ramo atual para um teste antecipado num ambiente de produção. Estas funcionalidades são totalmente suportadas, mas ainda estão em desenvolvimento Active Directory e podem receber as alterações até que eles mover para fora da categoria da versão de pré-lançamento. Tem de ativar esta funcionalidade para que fique disponível. Para obter mais informações, veja [Utilizar as funcionalidades da versão de pré-lançamento de atualizações](https://docs.microsoft.com/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease).

Começando no System Center Configuration Manager versão 1606, pode configurar definições de grupo do servidor para uma coleção para definir quantos, o que percentagem ou a ordem pela qual os computadores na coleção irão instalar as atualizações de software. Também pode configurar scripts do PowerShell de pré e pós-implementação para executar ações personalizadas.

Quando implementa atualizações de software numa coleção que tem definições de grupo do servidor configuradas, o Configuration Manager determina quantos computadores na coleção pode instalar as atualizações de software em qualquer momento e faz com que o mesmo número de bloqueios de implementação está disponível. Apenas os computadores que obtém um bloqueio de implementação irão iniciar a instalação da atualização de software. Quando um bloqueio de implementação estiver disponível, um computador obtém o bloqueio de implementação, instala as atualizações de software e, em seguida, libera o bloqueio de implementação quando a instalação de atualizações de software estiver concluída com êxito. Em seguida, o bloqueio de implementação fica disponível para outros computadores. Se um computador não é possível libertar um bloqueio de implementação, pode libertar manualmente todos os bloqueios de implementação de grupo de servidores para a coleção.

>[!IMPORTANT]
>Todos os computadores na coleção devem ser atribuídos ao mesmo site.

#### <a name="to-create-a-collection-for-a-server-group"></a>Para criar uma coleção para um grupo de servidores  
As definições de grupo do servidor são configuradas nas propriedades de uma coleção de dispositivos. Para atender a um grupo de servidores, todos os membros da coleção devem ser atribuídos ao mesmo site. Utilize os seguintes passos para criar uma coleção e configurar as definições de grupo do servidor:
1.  [Criar uma coleção de dispositivos](../../core/clients/manage/collections/create-collections.md) que contenha os computadores no grupo de servidor.  

2.  Na **ativos e compatibilidade** área de trabalho, clique em **coleções de dispositivos**, clique com o botão direito na coleção que contém os computadores no grupo de servidor e, em seguida, clique em **propriedades**.  

3.  Sobre o **gerais** separador, selecione **todos os dispositivos fazem parte do mesmo grupo de servidor**e, em seguida, clique em **definições**.  

4.  Sobre o **definições do grupo de servidor** , especifique uma das seguintes definições:  

    -   **Permitir que uma porcentagem de computadores seja atualizada ao mesmo tempo**: Especifica que apenas uma determinada percentagem de clientes são atualizados num dado momento. Se, por exemplo, a coleção tem 10 clientes, e a coleção é configurada para atualização 30% de clientes ao mesmo tempo, os clientes apenas 3 irão instalar as atualizações de software em qualquer momento.  

    -   **Permitir um número de computadores seja atualizada ao mesmo tempo**: Especifica que apenas um determinado número de clientes é atualizado num dado momento.  

    -   **Especifique a sequência de manutenção**: Especifica que os clientes na coleção será atualizado um de cada vez na sequência que configurar. Um cliente apenas irá instalar as atualizações de software depois do cliente que é um passo à frente-lo na lista concluiu a instalação suas atualizações de software.  

5.  Especifique se pretende utilizar um script de pré-implementação (drenagem do nó) ou o script de pós-implementação (retoma do nó).  

    > [!WARNING]
    > Scripts personalizados não são assinados pela Microsoft. É da responsabilidade do cliente para manter a integridade desses scripts.

    > [!TIP]  
    > Seguem-se exemplos que pode utilizar em testes de pré-implantação e os scripts de pós-implementação escrevem a hora atual num arquivo de texto:  
    >   
    >  **Pré-implementação**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\Windows\Temp\start.txt`  
    >   
    >  **Pós-implementação**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\Windows\Temp\end.txt`  

## <a name="deploy-software-updates-to-the-server-group-and-monitor-status"></a>Implementar atualizações de software para o estado do monitor e o grupo de servidor  
Implementar atualizações de software para a coleção de grupo de servidor utilizando o processo de implementação típica. Depois de implementar as atualizações de software, pode monitorizar a implementação de atualização de software na consola do Configuration Manager.
1.  [Implementar atualizações de software](manually-deploy-software-updates.md) para a coleção de grupo do servidor.   

2.  [Monitorizar a implementação de atualização de software](monitor-software-updates.md). Para além do padrão de monitorização as vistas de implementação de atualizações de software, o **aguardar o bloqueio** estado é apresentado quando um cliente está a aguardar por sua vez para instalar as atualizações de software. Pode rever o ficheiro Updatesdeployment log para obter mais informações.


## <a name="clear-the-deployment-locks-for-computers-in-a-server-group"></a>Limpar os bloqueios de implementação para computadores num grupo de servidor  
Quando um computador falhar a liberar um bloqueio de implementação, pode libertar manualmente todos os bloqueios de implementação de grupo de servidores para a coleção. Limpar bloqueios apenas quando uma implementação fica preso a atualizar computadores na coleção e existem computadores ainda não compatíveis.  
1.  Na **ativos e compatibilidade** área de trabalho, clique em **coleções de dispositivos**e clique na coleção para limpar os bloqueios de implementação.  

2.  Sobre o **home page** separador a **implementação** , clique em **bloqueios de implementação de grupo de servidor clara**. Quando os clientes tiverem falhado instalar as atualizações de software e estão a impedir que outros clientes de instalar as atualizações de software, os bloqueios de implementação podem ser removidos manualmente.  
