---
title: "Ponto de conexão de serviço | Microsoft Docs"
description: "Saiba mais sobre essa função do sistema de site do Configuration Manager, entenda e planeje seus usos."
ms.custom: na
ms.date: 6/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bc2282d5-0571-465b-9528-a555855eaacd
caps.latest.revision: 18
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0ec241d07f51b80b84d65676ef1207b31a9a9983
ms.openlocfilehash: e3d41dc1bb732e887d722f39ee86deaf0aae3240
ms.contentlocale: pt-pt
ms.lasthandoff: 06/28/2017


---
# <a name="about-the-service-connection-point-in-system-center-configuration-manager"></a>Acerca do ponto de ligação de serviço no System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

O ponto de conexão de serviço do System Center Configuration Manager é uma função de sistema de site que atende a várias funções importantes para a hierarquia. Antes de configurar o ponto de conexão de serviço, entenda e planeje seus usos, que podem afetar a maneira como você configurar essa função do sistema de site:  

-   **Gerenciar dispositivos móveis com o Microsoft Intune** -esta função substitui o conector do Windows Intune que versões anteriores do Configuration Manager usado e podem ser configuradas com os detalhes de assinatura do Intune. Consulte [gerenciamento de dispositivo móvel (MDM) híbrido com o System Center Configuration Manager e o Microsoft Intune](../../../../mdm/understand/hybrid-mobile-device-management.md).  

-   **Gerenciar dispositivos móveis com o MDM local** -esta função oferece suporte para dispositivos de locais que você gerencia e que não se conectam à Internet. Consulte [gerenciar dispositivos móveis com infraestrutura local no System Center Configuration Manager](../../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

-   **Carregar dados de uso da infra-estrutura do Configuration Manager** -você pode controlar a quantidade de detalhe que você carregue ou nível. Os dados carregados ajudam-nos a:  

    -   Identificar e resolver problemas proativamente  

    -   Melhorar os nossos produtos e serviços  

    -   Identificar atualizações para o Configuration Manager que se aplicam à versão do Configuration Manager que você usar  

  Para obter informações sobre como alterar o nível de coleção depois de instala a função e dados que coleta de cada nível, consulte [dados de diagnóstico e uso](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data)e, em seguida, siga o link para a versão do Configuration Manager que você usa.  

  Para obter mais informações, consulte [níveis de uso de dados e configurações](../../../../core/servers/deploy/install/setup-reference.md#bkmk_usage).  

-   **Baixar as atualizações que se aplicam à sua infraestrutura do Configuration Manager** - somente atualizações relevantes para sua infraestrutura ficam disponíveis com base em dados de uso carregados.  

- **Cada hierarquia oferece suporte a uma única instância dessa função:**  

 -   A função do sistema de site só pode ser instalada no site de nível superior da hierarquia, que é um site de administração central ou site primário autônomo.  

  -   Se você expandir um site primário autônomo para uma hierarquia maior, você deve desinstalar essa função do site primário e, em seguida, pode instalá-lo no site de administração central.  


##  <a name="bkmk_modes"></a>Modos de operação  
 O ponto de ligação de serviço suporta dois modos de funcionamento:  

-   Em **modo online**, o ponto de conexão de serviço verifica automaticamente a cada 24 horas para atualizações e, em seguida, baixa novas atualizações que estão disponíveis para sua atual infraestrutura e versão do produto para torná-los disponíveis no console do Configuration Manager.  

-   Em **modo offline**, o ponto de conexão de serviço não se conecta ao serviço de nuvem da Microsoft e você deve manualmente [usar a ferramenta de Conexão de serviço para o System Center Configuration Manager](../../../../core/servers/manage/use-the-service-connection-tool.md) para importar as atualizações disponíveis.  

Quando você alterar entre os modos online ou offline depois de instalar o ponto de conexão de serviço, você deve reiniciar o thread SMS_DMP_DOWNLOADER do serviço SMS_Executive do Configuration Manager antes que essa alteração entre em vigor. Para fazer isso, use o Configuration Manager Service Manager para reiniciar apenas o thread SMS_DMP_DOWNLOADER do serviço SMS_Executive. Também é possível reiniciar o serviço SMS_Executive do Configuration Manager, que reinicia a maioria dos componentes do site, ou você pode esperar para uma tarefa agendada, como um backup do site, interrompa e posteriormente reinicie o serviço SMS_Executive para você.  

Para usar o Configuration Manager Service Manager, no console, vá para **monitoramento** > **Status do sistema** > **Status do componente**, escolha **iniciar**e, em seguida, escolha **Configuration Manager Service Manager**. No Service Manager:  

-   No painel de navegação, expanda o site, expanda **componentes**e, em seguida, escolha o componente que você deseja reiniciar.  

-   No painel de detalhes, clique com botão direito do componente e, em seguida, escolha **consulta**.  

-   Depois que o status do componente for confirmado, clique o componente novamente e, em seguida, escolha **parar**.  

-   **Consulta** o componente novamente para confirmar que ele seja interrompido, clique o componente mais uma vez e, em seguida, escolha **iniciar**.  

> [!IMPORTANT]  
>  O processo que adiciona automaticamente a uma assinatura Microsoft Intune para o ponto de conexão de serviço define a função do sistema de site estar online. O ponto de conexão de serviço não dá suporte para o modo offline quando ele é configurado com uma assinatura do Intune.  

**Quando a função é instalada em um computador remoto do servidor do site:**  

-   A conta de computador do servidor do site deve ser um administrador local no computador que hospeda uma conexão de serviço remoto.

-   Você deve configurar o servidor de sistema de site que hospeda a função com uma conta de instalação do sistema de Site.  

-   O Gerenciador de distribuição no servidor do site usa a conta de instalação do sistema de Site para transferir atualizações do ponto de conexão de serviço.

##  <a name="bkmk_urls"></a>Requisitos de acesso à Internet  
Para habilitar a operação, o computador que hospeda o ponto de conexão de serviço e quaisquer firewalls entre o computador e a Internet deve passar as comunicações por meio de **porta TCP 443** e **porta TCP 443** nos seguintes locais da Internet. A conexão de serviço do ponto também dá suporte ao uso um proxy da web (com ou sem autenticação) para usar esses locais.  Se você precisa configurar uma conta de proxy da web consulte: [Suporte do servidor proxy no System Center Configuration Manager](/sccm/core/plan-design/network/proxy-server-support).

**Atualizações e manutenção**  

-   *.akamaiedge.net  

-   *. akamaitechnologies.com 

-   *.manage.microsoft.com

-   go.microsoft.com

-   blob.core.windows.net  

-   download.microsoft.com  

-   download.windowsupdate.com

-   sccmconnected-a01.cloudapp.net  

**Microsoft Intune**  

-   *manage.microsoft.com  
-   https://bspmts.MP.microsoft.com/V
-   https://login.microsoftonline.com/ {TenantID}


**Serviço do Windows 10**  

-   download.microsoft.com  

-   https://go.microsoft.com/fwlink/?LinkID=619849  

## <a name="install-the-service-connection-point"></a>Instalar o ponto de conexão de serviço
Quando você executa **instalação** para instalar o site de nível superior de uma hierarquia, você tem a opção de instalar o ponto de conexão de serviço.

Depois que a instalação é executada, ou se você estiver reinstalando a função do sistema de site, use o **adicionar funções do sistema de Site** assistente ou o **criar servidor do sistema de Site** Assistente para instalar o sistema de site em um servidor no site de nível superior da sua hierarquia, ou seja, o site de administração central ou um site primário autônomo. Os dois assistentes são no **início** guia no console em **administração** > **configuração do Site** > **servidores e funções de sistema de Site**.

## <a name="log-files-used-by-the-service-connection-point"></a>Arquivos de log usados pelo ponto de conexão de serviço
Para exibir informações sobre carregamentos à Microsoft, consulte o **Dmpuploader.log** no computador que executa o ponto de conexão de serviço.  Para obter downloads, incluindo o andamento do download de atualizações, exibir **Dmpdownloader.log**. Para obter uma lista de logs relacionados ao ponto de conexão de serviço, consulte [ponto de conexão de serviço](/sccm/core/plan-design/hierarchy/log-files#BKMK_WITLog) no tópico de arquivos de log do Configuration Manager.

Você também pode usar os seguintes fluxogramas para entender o fluxo de processo e entradas de log principais para downloads de atualização e replicação de atualizações para outros sites:
 - [Fluxograma – Transferir atualizações](/sccm/core/servers/manage/download-updates-flowchart)
 - [Fluxograma – Atualizar replicação](/sccm/core/servers/manage/update-replication-flowchart)

