---
title: Pré-requisitos para atualizações de software
titleSuffix: Configuration Manager
description: Saiba mais sobre a pré-requisitos para atualizações de software no System Center Configuration Manager.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 02/02/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: fdf05118-162a-411e-b72e-386b9dc9a5e1
ms.openlocfilehash: 5ec545fd2ae6c775fbbd0d984dcdd487359ab043
ms.sourcegitcommit: f7b2fe522134cf102a3447505841cee315d3680c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/01/2019
ms.locfileid: "55570171"
---
# <a name="prerequisites-for-software-updates-in-system-center-configuration-manager"></a>Pré-requisitos para atualizações de software no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo lista os pré-requisitos para atualizações de software no System Center Configuration Manager. Para cada um destes procedimentos, as dependências externas e as dependências internas são listadas em tabelas separadas.  

## <a name="software-update-dependencies-that-are-external-to-configuration-manager"></a>Dependências de atualização de software que são externas ao Configuration Manager  
 As secções seguintes listam as dependências externas para atualizações de software.  

### <a name="internet-information-services"></a>Serviços de informação Internet  
 Serviços de informação Internet (IIS) tem de ser instalado em servidores de sistema de sites para executar o ponto de atualização de software, o ponto de gestão e o ponto de distribuição. Para obter mais informações, veja [Pré-requisitos das funções do sistema de sites](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

### <a name="windows-server-update-services"></a>Windows Server Update Services  
 Windows Server Update Services (WSUS) é necessário para a sincronização de atualizações de software e da verificação de aplicabilidade de atualizações de software nos clientes. O servidor WSUS tem de ser instalado antes de criar a função de ponto de atualização de software. As seguintes versões do WSUS são suportadas para um ponto de atualização de software:  

-   WSUS 10.0.14393 (função no Windows Server 2016)
-   WSUS 10.0.17763 (função no Windows Server 2019) (requer o Configuration Manager 1810 ou posterior)
-   WSUS 6.2 e 6.3 (função no Windows Server 2012 e Windows Server 2012 R2)

>[!NOTE]
>-   Windows Server 2008 R2 a partir da versão 1702, não é suportada para a função de ponto de atualização de software. Para obter mais informações, consulte [sistemas operativos suportados para servidores do sistema de sites](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers#bkmk_2008r2sp1).  

Quando tiver vários pontos de atualização de software num site, certifique-se de que eles estão todos a utilizar a mesma versão do WSUS.  

> [!WARNING]  
>  O **atualizações** classificação de atualizações de software só é suportada a partir do WSUS 4.0. Antes de sincronizar esta nova classificação e ter a capacidade de avaliar computadores Windows 10 num plano de manutenção do Windows 10, é fundamental que instale [correção 3095113](https://support.microsoft.com/kb/3095113) para WSUS no seu software de atualização de pontos e site servidores. Esta correção ativa o WSUS num servidor baseado no Windows Server 2012 ou um servidor baseado no Windows Server 2012 R2 para sincronizar e distribuir atualizações de funcionalidades para o Windows 10. Para obter mais informações, consulte [gerir o Windows como um serviço](../../osd/deploy-use/manage-windows-as-a-service.md).  
>   
>  Se sincronizar atualizações de software com a classificação **Atualizações** antes de instalar a [correção 3095113](https://support.microsoft.com/kb/3095113), veja [Recuperar a partir da sincronização da categoria Atualizações antes de instalar o KB 3095113](#BKMK_RecoverUpgrades).  

### <a name="wsus-administration-console"></a>Consola de Administração do WSUS  
 A consola de administração do WSUS é necessária no servidor do site do Configuration Manager, quando o ponto de atualização de software é num servidor de sistema de sites remoto e o WSUS ainda não está instalado no servidor do site.  

> [!IMPORTANT]  
> A versão do WSUS no servidor do site tem de ser o mesmo que a versão do WSUS que está em execução nos pontos de atualização de software.
>
> Não utilize a consola de administração do WSUS para configurar as definições de WSUS. Configuration Manager estabelece ligação à instância do WSUS que está em execução no ponto de atualização de software e configura as definições apropriadas.  



### <a name="windows-update-agent"></a>Windows Update Agent  
 O cliente do Windows Update Agent (WUA) é necessário nos clientes para que se podem ligar ao servidor WSUS. WUA obtém a lista de atualizações de software que deve ser analisada a compatibilidade.  

 Ao instalar o Configuration Manager, é transferida a versão mais recente do WUA. Em seguida, quando instala o cliente do Configuration Manager, o WUA é atualizado se for necessário. No entanto, se a instalação falhar, tem de utilizar um método diferente para atualizar o WUA.  

## <a name="software-update-dependencies-that-are-internal-to-configuration-manager"></a>Dependências de atualização de software que são internas do Configuration Manager  
 As secções seguintes listam as dependências internas para atualizações de software no Configuration Manager.  

### <a name="management-points"></a>Pontos de gestão  
 Pontos de gestão transferem informações entre computadores cliente e o site do Configuration Manager. Os pontos de gestão são necessários para atualizações de software.  

### <a name="software-update-points"></a>Pontos de atualização de software  
 Tem de instalar um ponto de atualização de software no servidor WSUS para poder implementar atualizações de software no Configuration Manager. Para obter mais informações, consulte [instalar e configurar um ponto de atualização de software](../get-started/install-a-software-update-point.md).

### <a name="distribution-points"></a>Pontos de distribuição  
 Pontos de distribuição são necessários para armazenar o conteúdo para atualizações de software. Para obter mais informações sobre como instalar pontos de distribuição e gerir conteúdo, consulte [gerir a infraestrutura de conteúdo e conteúda](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

### <a name="client-settings-for-software-updates"></a>Definições de cliente para atualizações de software  
 Por predefinição, as atualizações de software são ativadas para os clientes. No entanto, existem outras definições disponíveis que controlam como e quando os clientes avaliam a compatibilidade das atualizações de software e controlam a forma como as atualizações de software são instaladas.  

 Para obter mais informações, veja os artigos seguintes:  

-   [Definições de cliente para atualizações de software](../get-started/manage-settings-for-software-updates.md#BKMK_ClientSettings)   

-   [Definições de cliente de atualizações de software](../../core/clients/deploy/about-client-settings.md#software-updates)  

### <a name="reporting-services-points"></a>Pontos do Reporting Services  
 A função do sistema de sites do ponto do Reporting Services pode apresentar relatórios de atualizações de software. Esta função é opcional mas recomendado. Para obter mais informações sobre como criar um relatório de ponto de serviços, consulte [Configuring reporting](../../core/servers/manage/configuring-reporting.md).  

##  <a name="BKMK_RecoverUpgrades"></a> Recuperar a partir da sincronização da categoria Atualizações antes de instalar o KB 3095113  
 Tem de instalar a [correção 3095113](https://support.microsoft.com/kb/3095113) para o WSUS nos seus pontos de atualização de software e servidores do site antes de sincronizar a classificação **Atualizações** . Se a correção não estiver instalada quando o **atualizações** classificação estiver ativada, vê do WSUS do Windows 10 1511 de compilação atualização da funcionalidades, mesmo que não é possível corretamente baixar e implantar os pacotes associados. 
 
 Se sincronizar atualizações sem ter instalado primeiro [correção 3095113](https://support.microsoft.com/kb/3095113), preenche a base de dados WSUS (SUSDB) com dados não utilizáveis. Que dados têm de ser limpos antes das atualizações podem ser implementadas corretamente. Utilize o procedimento seguinte para resolver este problema.  

#### <a name="to-recover-from-synchronizing-the-upgrades-classification-before-you-install-kb-3095113"></a>Para recuperar da sincronização a classificação atualizações antes de instalar o KB 3095113  

1.  Elimine as atualizações de software com o **atualizações** classificação. Pode usar um script do PowerShell semelhante para o seguinte script de exemplo:  

    ```  
    $Server = Get-WSUSServer  
    $Config = $Server.GetConfiguration()  
    $Update10563 = “df4e45a3-946d-4467-b3fd-8621174bb666”  
    $UpdateGUID = New-Object Guid($Update10563)  
    $Server.DeleteUpdate($UpdateGUID)  
    ```  

    > [!IMPORTANT]  
    >  Tem de executar o script em todos os pontos de atualização de software na sua hierarquia do Configuration Manager antes de ir para o passo seguinte.  

     Para atualizações de software de eliminação em massa com o **atualizações** classificação, pode modificar o script do PowerShell para ler GUIDs a partir de um ficheiro de texto.  

2.  Desmarque os **atualizações** classificação nas propriedades do componente de ponto de atualização de Software. (Para obter mais informações, consulte [configurar classificações e produtos](../get-started/configure-classifications-and-products.md).) Em seguida, inicie a sincronização de atualizações de software. (Para obter mais informações, consulte [sincronizar as atualizações de software](../get-started/synchronize-software-updates.md).)  

3.  Instale a [correção 3095113](https://support.microsoft.com/kb/3095113) para o WSUS nos pontos de atualização de software e nos servidores do site.  

4.  Selecione o **atualizações** classificação nas propriedades do componente de ponto de atualização de Software. (Para obter mais informações, consulte [configurar classificações e produtos](../get-started/configure-classifications-and-products.md).) Em seguida, inicie a sincronização de atualizações de software. (Para obter mais informações, consulte [sincronizar as atualizações de software](../get-started/synchronize-software-updates.md).)  

## <a name="next-steps"></a>Passos seguintes
[Preparar a gestão de atualizações de software](../get-started/prepare-for-software-updates-management.md)
