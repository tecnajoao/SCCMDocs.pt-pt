---
title: "Pré-requisitos para atualizações de software"
titleSuffix: Configuration Manager
description: "Saiba mais sobre os pré-requisitos para atualizações de software no System Center Configuration Manager."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: fdf05118-162a-411e-b72e-386b9dc9a5e1
ms.openlocfilehash: 905ecc023dd181a8d4801860898b05aff5e4e07f
ms.sourcegitcommit: 986fc2d54f7c5fa965fd4df42f4db4ecce6b79cb
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 11/17/2017
---
# <a name="prerequisites-for-software-updates-in-system-center-configuration-manager"></a>Pré-requisitos para atualizações de software no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este tópico lista os pré-requisitos para atualizações de software no System Center Configuration Manager. Para cada um destes procedimentos, as dependências externas e as dependências internas são listadas em tabelas separadas.  

## <a name="software-update-dependencies-external-to-configuration-manager"></a>Dependências de atualização de software externas ao Configuration Manager  
 As secções seguintes listam as dependências externas para atualizações de software.  

### <a name="internet-information-services-iis"></a>Serviços de Informação de Internet (IIS)  
 Serviços de informação Internet (IIS) tem de ser em servidores de sistema de sites para executar o ponto de atualização de software, o ponto de gestão e o ponto de distribuição. Para obter mais informações, consulte [pré-requisitos para funções do sistema de sites](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

### <a name="windows-server-update-services-wsus"></a>Windows Server Update Services (WSUS)  
 O WSUS é necessário para a sincronização de atualizações de software e para a análise da avaliação de conformidade de atualizações de software em clientes. O servidor WSUS tem de ser instalado antes de ser criada a função do sistema de sites do ponto de atualização de software. As seguintes versões do WSUS são suportadas para um ponto de atualização de software:  

-   WSUS 4 (função no Windows Server 2012 e Windows Server 2012 R2)  

-   WSUS 3.2 (função no Windows Server 2008 R2)  

 Quando tiver vários pontos de atualização de software num site, certifique-se de que todos executam a mesma versão do WSUS.  

> [!WARNING]  
>  O **atualizações** atualizações de software classificação só é suportada no WSUS 4.0 início. Antes de sincronizar esta nova classificação e ter a capacidade de avaliar computadores Windows 10 num plano de manutenção do Windows 10, é fundamental que instale a [correção 3095113](https://support.microsoft.com/kb/3095113) para o WSUS nos pontos de atualização de software e nos servidores do site. Esta correção ativa o WSUS em com base no Windows Server 2012 ou um servidor baseado no Windows Server 2012 R2 para sincronizar e distribuir atualizações de funcionalidades para o Windows 10. Para obter mais informações, consulte [gerir o Windows como um serviço](../../osd/deploy-use/manage-windows-as-a-service.md).  
>   
>  Se sincronizar atualizações de software com a classificação **Atualizações** antes de instalar a [correção 3095113](https://support.microsoft.com/kb/3095113), veja [Recover from synchronizing the Atualizações category before you install KB 3095113](#BKMK_RecoverUpgrades).  

### <a name="wsus-administration-console"></a>Consola de Administração do WSUS  
 A consola de administração do WSUS é necessário no servidor do site do Configuration Manager quando o ponto de atualização de software está num servidor de sistema de sites remoto e WSUS ainda não está instalado no servidor do site.  

> [!IMPORTANT]  
>  A versão do WSUS no servidor do site tem de ser o mesmo que a versão do WSUS em execução nos pontos de atualização de software.  

> [!IMPORTANT]  
>  Não utilize a consola de administração do WSUS para configurar as definições de WSUS. O Configuration Manager liga-se ao WSUS que está em execução no ponto de atualização de software e configura as definições apropriadas.  

### <a name="windows-update-agent-wua"></a>Windows Update Agent (WUA)  
 O cliente do WUA é necessário nos clientes para que estes possam ligar ao servidor WSUS e obter a lista de atualizações de software cuja compatibilidade deve ser analisada.  

 Ao instalar o Configuration Manager, é transferida a versão mais recente do WUA. Em seguida, quando o cliente do Configuration Manager está instalado, o WUA é atualizado se for necessário. No entanto, se a instalação falhar, é necessário utilizar um método diferente para atualizar o WUA.  

## <a name="software-update-dependencies-internal-to-configuration-manager"></a>Dependências de atualização de software internas do Configuration Manager  
 As secções seguintes listam as dependências internas para atualizações de software no Configuration Manager.  

### <a name="management-points"></a>Pontos de gestão  
 Pontos de gestão transferem informações entre computadores cliente e o site do Configuration Manager. São necessários para atualizações de software.  

### <a name="software-update-point"></a>Ponto de atualização de Software  
 Tem de instalar um ponto de atualização de software no servidor WSUS para poder implementar atualizações de software no Configuration Manager. Para obter mais informações, consulte [instalar e configurar um ponto de atualização de software](../get-started/install-a-software-update-point.md).

### <a name="distribution-points"></a>Pontos de distribuição  
 São necessários pontos de distribuição para armazenar o conteúdo para atualizações de software. Para obter mais informações sobre como instalar pontos de distribuição e gerir conteúdo, consulte [gerir a infraestrutura de conteúdo e conteúda](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

### <a name="client-settings-for-software-updates"></a>Definições de cliente para atualizações de software  
 Por predefinição, as atualizações de software estão ativadas para os clientes. No entanto, existem outras definições disponíveis que controlam como e quando os clientes avaliam a compatibilidade para o software, atualizações e controla a forma como as atualizações de software são instaladas.  

 Para obter mais informações, consulte o seguinte:  

-   [Definições de cliente para atualizações de software](../get-started/manage-settings-for-software-updates.md#BKMK_ClientSettings).   

-   [Definições de cliente de atualizações de software](../../core/clients/deploy/about-client-settings.md#software-updates) tópico.  

### <a name="reporting-services-point"></a>Ponto do Reporting Services  
 A função do sistema de sites do ponto do Reporting Services pode apresentar relatórios de atualizações de software. Esta função é opcional, mas recomendada. Para obter mais informações sobre como criar um relatório do ponto, consulte [configurar relatórios](../../core/servers/manage/configuring-reporting.md) .  

##  <a name="BKMK_RecoverUpgrades"></a> Recuperar a partir da sincronização da categoria Atualizações antes de instalar o KB 3095113  
 Tem de instalar a [correção 3095113](https://support.microsoft.com/kb/3095113) para o WSUS nos seus pontos de atualização de software e servidores do site antes de sincronizar a classificação **Atualizações** . Se a correção não estiver instalada quando a classificação **Atualizações** estiver ativada, o WSUS verá a atualização da funcionalidades da compilação do Windows 10 1511, mesmo que não seja possível transferir e implementar corretamente os pacotes associados. Se sincronizar atualizações sem ter instalado primeiro a [correção 3095113](https://support.microsoft.com/kb/3095113), irá preencher a base de dados do WSUS (SUSDB) com dados não utilizáveis que têm de ser limpos antes das atualizações poderem ser implementadas corretamente.  Utilize o procedimento seguinte para resolver este problema.  

#### <a name="to-recover-from-synchronizing-the-upgrades-classification-before-you-install-kb-3095113"></a>Para recuperar de sincronizar a classificação atualizações antes de instalar o KB 3095113  

1.  Elimine as atualizações de software com a classificação atualizações. Pode utilizar um script do PowerShell semelhante para o script de exemplo seguinte:  

    ```  
    $Server = Get-WSUSServer  
    $Config = $Server.GetConfiguration()  
    $Update10563 = “df4e45a3-946d-4467-b3fd-8621174bb666”  
    $UpdateGUID = New-Object Guid($Update10563)  
    $Server.DeleteUpdate($UpdateGUID)  
    ```  

    > [!IMPORTANT]  
    >  Tem de executar o script em todos os pontos de atualização de software na sua hierarquia do Configuration Manager antes de ir para o passo seguinte.  

     Para efetuar uma eliminação em massa com a classificação Atualizações, pode modificar o script do PowerShell para ler GUIDs a partir de um ficheiro txt.  

2.  Desmarque a **atualizações** classificação nas propriedades do componente de ponto de atualização de Software (para obter mais informações, consulte [configurar classificações e produtos](../get-started/configure-classifications-and-products.md)) e, em seguida, iniciar a sincronização de atualizações de software (para obter mais informações, consulte [sincronizar atualizações de software](../get-started/synchronize-software-updates.md).  

3.  Instale a [correção 3095113](https://support.microsoft.com/kb/3095113) para o WSUS nos pontos de atualização de software e nos servidores do site.  

4.  Selecione o **atualizações** classificação nas propriedades do componente de ponto de atualização de Software (para obter mais informações, consulte [configurar classificações e produtos](../get-started/configure-classifications-and-products.md)) e, em seguida, iniciar a sincronização de atualizações de software (para obter mais informações, consulte [sincronizar atualizações de software](../get-started/synchronize-software-updates.md).  

## <a name="next-steps"></a>Passos seguintes
[Preparar a gestão de atualizações de software](../get-started/prepare-for-software-updates-management.md)
