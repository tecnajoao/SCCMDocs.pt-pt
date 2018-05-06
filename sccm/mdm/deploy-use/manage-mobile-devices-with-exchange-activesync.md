---
title: 'Gerir dispositivos móveis '
titleSuffix: Configuration Manager
description: Gerir dispositivos móveis utilizando o conector do Exchange Server no System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: aba688d9-fd5b-4c42-8cb4-f7e1b161ef50
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5bdc881d6d6423aa357cf8916f54f1b5f31120f2
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="manage-mobile-devices-with-system-center-configuration-manager-and-exchange"></a>Gerir dispositivos móveis com o System Center Configuration Manager e o Exchange

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilizar o conector do Exchange Server no System Center Configuration Manager quando pretender gerir dispositivos móveis que liguem ao Exchange Server (no local ou online) utilizando o Microsoft Exchange ActiveSync protocolo e não é possível inscrevê-los utilizando o Gestor de configuração. Pode configurar funcionalidades de gestão de dispositivos móveis do Exchange, como eliminação remota do dispositivo e controlo de definições para vários servidores do Exchange, da consola do Configuration Manager.  

 ![ConfigMgr&#45;com&#45;exchange](../../mdm/deploy-use/media/configmgr-with-exchange.png "do configmgr com o exchange")  

 Quando gerir dispositivos móveis utilizando o conector do Exchange Server, este não instala o cliente do Configuration Manager nos dispositivos móveis. Por conseguinte, algumas funções de gestão são limitadas. Por exemplo, não pode instalar software nestes dispositivos ou utilizar itens de configuração para os configurar. Para obter mais informações sobre as diversas capacidades de gestão que pode utilizar com o Configuration Manager para dispositivos móveis, consulte [escolher uma solução de gestão de dispositivos para o System Center Configuration Manager](../../core/plan-design/choose-a-device-management-solution.md).  

> [!IMPORTANT]  
>  Antes de instalar o conector do Exchange Server, certifique-se de que o Configuration Manager suporta a versão do Microsoft Exchange que está a utilizar. Para obter mais informações, consulte "Conector do Exchange Server" em [sistemas operativos suportados por sites e clientes do System Center Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).  

 Quando utiliza o conector do Exchange Server, os dispositivos móveis podem ser geridos através das definições que configurar no Configuration Manager em vez de a ser gerido através das políticas de caixa de correio predefinidas do Exchange ActiveSync. Configure as definições que pretende utilizar nas definições de grupo seguintes: **Geral**, **palavra-passe**, **a gestão de E-Mail**, **segurança**, e **aplicação**. Por exemplo, no grupo de definições **Palavra-passe** , pode configurar se os dispositivos móveis necessitam de uma palavra-passe, o comprimento mínimo da palavra-passe, a complexidade da palavra-passe e se é permitida a recuperação da palavra-passe.  

 Quando configura pelo menos uma definição no grupo, o Configuration Manager gere todas as definições do grupo para dispositivos móveis. Se não configurar qualquer definição de um grupo, o Exchange continua a gerir os dispositivos móveis para essas definições. Quaisquer políticas de caixa de correio do Exchange ActiveSync que estejam configuradas no Exchange Server e atribuídas a utilizadores continuarão a ser aplicadas.  

 Também pode configurar o conector do Exchange Server para gerir as regras de acesso do Exchange e permitir, bloquear ou colocar dispositivos móveis em quarentena. Podem apagar remotamente dispositivos móveis utilizando a consola do Configuration Manager e os utilizadores podem apagar remotamente os seus dispositivos móveis utilizando o catálogo de aplicações.  

 Dispositivo móvel do utilizador aparece no catálogo de aplicações automaticamente quando o conector do Exchange Server o gere e o Exchange Server for no local. Quando configurar o conector do Exchange Server para o Microsoft Exchange Online, deve configurar manualmente a afinidade de dispositivo / utilizador para o dispositivo móvel do utilizador são apresentadas no catálogo de aplicações. Para obter mais informações sobre como configurar manualmente a afinidade dispositivo / utilizador, consulte [associar utilizadores e dispositivos à afinidade de dispositivo do utilizador no System Center Configuration Manager](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

> [!TIP]  
>  Se gerir um dispositivo móvel utilizando o conector do Exchange Server e o dispositivo móvel for transferido para outro utilizador, elimine o dispositivo móvel da consola do Configuration Manager antes o novo proprietário do dispositivo móvel configura a respetiva conta do Exchange no dispositivo móvel transferido.  

## <a name="required-security-permissions"></a>Permissões de Segurança Necessárias  
 Tem de ter as seguintes permissões de segurança para configurar o conector do Exchange Server:  

-   Para adicionar, modificar e eliminar o conector do Exchange Server: **Modificar** permissão para o **Site** objeto.  

-   Para configurar as definições de dispositivos móveis: **ModifyConnectorPolicy** permissão para o **Site** objeto.  

 A função de segurança **Administrador Global** inclui as permissões necessárias para configurar o conector do Exchange Server.  

 Tem de ter as seguintes permissões de segurança para gerir dispositivos móveis:  

-   Para apagar um dispositivo móvel: **Eliminar recurso** para o **coleção** objeto.  

-   Para cancelar um comando de eliminação: **Modificar recurso** para o **coleção** objeto.  

-   Para permitir e bloquear dispositivos móveis: **Modificar recurso** para o **coleção** objeto.  

 A função de segurança **Administrador de Operações** inclui as permissões necessárias para gerir dispositivos móveis utilizando o conector do Exchange Server.  

 Para obter mais informações sobre como configurar permissões de segurança, consulte [configurar a administração baseada em funções para o System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).  

## <a name="installing-and-configuring-an-exchange-server-connector"></a>Instalar e Configurar um Conector do Exchange Server  
 Utilize o seguinte procedimento para instalar e configurar um conector do Exchange Server para gerir dispositivos móveis. O Configuration Manager suporta apenas um conector numa organização do Exchange. Depois de concluir estes passos, pode monitorizar os dispositivos móveis encontrados e geridos pelo conector quando visualizar as coleções que apresentem dispositivos móveis e utilizando os relatórios de dispositivos móveis.  

> [!NOTE]  
>  O Configuration Manager gera nomes para os dispositivos móveis que encontra utilizando o formato *UserName*_*DeviceType*. Se um utilizador tiver mais do que um dispositivo móvel que tenha o mesmo tipo de dispositivo, o Configuration Manager apresenta o mesmo nome para estes dispositivos móveis na consola e nos relatórios.  

#### <a name="to-install-and-configure-an-exchange-server-connector"></a>Para instalar e configurar um conector do Exchange Server  

1.  Decida qual a conta que irá estabelecer ligação com o servidor de Acesso de Cliente do Exchange para gerir os dispositivos móveis. A conta pode ser a conta de computador do servidor do site ou uma conta de utilizador do Windows. Em seguida, configure esta conta para executar os seguintes cmdlets do Exchange Server:  

    -   **Clear-ActiveSyncDevice**  

    -   **Get-ActiveSyncDevice**  

    -   **Get-ActiveSyncDeviceAccessRule**  

    -   **Get-ActiveSyncDeviceStatistics**  

    -   **Get-ActiveSyncMailboxPolicy**  

    -   **Get-ActiveSyncOrganizationSettings**  

    -   **Get-ExchangeServer**  
    
    -   **Get-Mailbox**
    
    -   **Get-Recipient**  

    -   **Set-ADServerSettings**  

    -   **Set-ActiveSyncDeviceAccessRule**  

    -   **Set-ActiveSyncMailboxPolicy**  

    -   **Set-CASMailbox**  

    -   **New-ActiveSyncDeviceAccessRule**  

    -   **New-ActiveSyncMailboxPolicy**  

    -   **Remove-ActiveSyncDevice**  
    
    -   **Get-CasMailbox**  
    
    -   **Get-utilizador**  
    
    -   **Set-ActiveSyncOrganizationSettings**  

    > [!NOTE]  
    >  As seguintes funções de gestão do Exchange Server incluem estes cmdlets: Gestão de destinatários, gestão da organização apenas de visualização e gestão de servidor. Para mais informações sobre grupos de funções de gestão no Microsoft Exchange Server 2010, consulte [Noções sobre Grupos de Funções de Gestão](http://go.microsoft.com/fwlink/p/?LinkId=212914).  

    > [!TIP]  
    >  Se tentar instalar ou utilizar o conector do Exchange Server sem os cmdlets necessários, será registado um erro com a mensagem `Invoking cmdlet <cmdlet> failed` no ficheiro EasDisc.log no computador servidor do site.  

2.  Na consola do Configuration Manager, clique em **Administração**.  

3.  Na área de trabalho **Administração** , expanda **Configuração da Hierarquia**e clique em **Conectores do Exchange Server**.  

4.  No separador **Home Page** , no grupo **Criar** , clique em **Adicionar Exchange Server**.  

5.  Conclua o Assistente para Adicionar Exchange Server:  

    -   Se utilizar uma instância do Exchange Server no local e especificar um Servidor de Acesso de Cliente, poderá especificar servidor único ou uma matriz de Servidores de Acesso de Cliente para cada site do Active Directory. Se o servidor ou a matriz estiver offline, o Configuration Manager tenta detetar um servidor de acesso de cliente para utilizar. Se não conseguir, o Configuration Manager retrocede para utilizar um servidor de caixa de correio para estabelecer uma ligação a um servidor de acesso de cliente. As novas tentativas são registadas como avisos no ficheiro EasDisc.log no computador servidor do site. Por exemplo, procure `Failed to open runspace for site <site_name>`.  

    -   Para a Conta do Conector do Exchange Server, especifique a conta que configurou no passo 1.  

    -   Se também inscrever dispositivos móveis utilizando o Gestor de configuração, ative a opção **gestão de dispositivos móveis externos** para garantir que estes dispositivos móveis continuam a receber correio eletrónico do Exchange depois do Configuration Manager os inscrever.  

    -   No **conta** página do assistente, pode configurar a conta utilizada para enviar notificações por e-mail para clientes bloqueados pelo acesso condicional do Configuration Manager. A conta que especificar tem de ter uma caixa de correio válida no servidor Exchange.  

         Para obter mais informações, consulte [gerir o acesso a serviços no System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md).  

6.  Pode verificar a instalação do conector do Exchange Server utilizando mensagens de estado e analisando os ficheiros de registo:  

    -   Para confirmar que o Gestor de Componentes do Site instalou com êxito o conector do Exchange Server, procure o ID de estado **1015** para o componente **SMS_EXCHANGE_CONNECTOR** . Se o Configuration Manager não é possível instalar com êxito o conector (por exemplo, porque o computador do servidor de acesso de cliente especificado está offline), a cada 60 minutos, até instalar com êxito ou remover o conector do Exchange Server de instalação de tentativas de Configuration Manager.  

    -   No servidor do site, procure o ficheiro SiteComp.log e, neste, procure `Component SMS_EXCHANGE_CONNECTOR flagged for installation`. Uma instalação com êxito é registada com o seguinte texto: `STATMSG: ID=1015`.  
