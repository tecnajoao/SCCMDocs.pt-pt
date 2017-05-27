---
title: "Ponto de ligação de serviço | Documentos do Microsoft"
description: "Saiba mais sobre esta função de sistema de sites do Configuration Manager e compreender e planear para o intervalo de recomendadas."
ms.custom: na
ms.date: 3/30/2017
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
ms.sourcegitcommit: 6accec2d356861b273b25ba2b6338d9684a46ff6
ms.openlocfilehash: ad6df047beff670411d203220576b87f7d56d50c
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="about-the-service-connection-point-in-system-center-configuration-manager"></a>Acerca do ponto de ligação de serviço no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O ponto de ligação de serviço do System Center Configuration Manager é uma função de sistema de sites que funciona várias funções importantes para a hierarquia. Antes de configurar o ponto de ligação de serviço, compreender e planear para o intervalo de utilizações, que podem afetar como configurar esta função do sistema de sites:  

-   **Gerir dispositivos móveis com o Microsoft Intune** -esta função substitui o conector do Windows Intune que versões anteriores do Configuration Manager utilizado e podem ser configuradas com os detalhes da subscrição do Intune. Consulte o artigo [gestão de dispositivos móveis (MDM) híbrida com o System Center Configuration Manager e o Microsoft Intune](../../../../mdm/understand/hybrid-mobile-device-management.md).  

-   **Gerir dispositivos móveis com MDM no local** -esta função fornece suporte para dispositivos no local que está a gerir e que não estabelecer ligação à Internet. Consulte o artigo [gerir dispositivos móveis com a infraestrutura no local no System Center Configuration Manager](../../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

-   **Carregar dados de utilização a partir da sua infraestrutura do Configuration Manager** -pode controlar o nível ou a quantidade de detalhes que será carregado. Os dados carregados ajudam-nos a:  

    -   Identificar e resolver problemas proativamente  

    -   Melhorar os nossos produtos e serviços  

    -   Identificar as atualizações para o Configuration Manager que se aplicam a versão do Configuration Manager que utiliza  

  Para obter informações sobre os dados que recolhe de cada nível e como alterar o nível da coleção após a instalação da função, consulte o artigo [diagnósticos e dados de utilização](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data)e, em seguida, seguir a ligação para a versão do Configuration Manager que utilizar.  

  Para obter informações adicionais, consulte o artigo [níveis de dados de utilização e definições](../../../../core/servers/deploy/install/setup-reference.md#bkmk_usage).  

-   **Transferir as atualizações aplicáveis a sua infraestrutura do Configuration Manager** - apenas atualizações relevantes para a sua infraestrutura ficam disponíveis com base em dados de utilização que carrega.  

- **Cada hierarquia suporta uma única instância desta função:**  

 -   A função de sistema de sites apenas pode ser instalada no site de nível superior da hierarquia, que é um site de administração central ou site primário autónomo.  

  -   Se expandir um site primário autónomo para uma hierarquia maior, tem de desinstalar esta função do site primário e pode, em seguida, instalá-lo no site de administração central.  


##  <a name="bkmk_modes"></a>Modos de funcionamento  
 O ponto de ligação de serviço suporta dois modos de funcionamento:  

-   No **modo online**, o ponto de ligação de serviço verifica automaticamente a cada 24 horas para as atualizações e, em seguida, transfere novas atualizações que estão disponíveis para a sua versão atual, infraestrutura e os produtos, para que fiquem disponíveis na consola do Configuration Manager.  

-   No **modo offline**, o ponto de ligação de serviço não estabelecer ligação ao serviço de nuvem Microsoft, e tem manualmente [utilizar a ferramenta de ligação de serviço para o System Center Configuration Manager](../../../../core/servers/manage/use-the-service-connection-tool.md) para importar as atualizações disponíveis.  

Quando alterar entre modos online ou offline depois de instalar o ponto de ligação de serviço, em seguida, tem de reiniciar o thread SMS_DMP_DOWNLOADER do serviço SMS_Executive do Configuration Manager antes desta alteração entra em vigor. Para tal, utilize o Gestor de serviço do Configuration Manager para reiniciar o thread SMS_DMP_DOWNLOADER do serviço SMS_Executive. Também pode reiniciar o serviço SMS_Executive no Configuration Manager, que reinicia a maior parte dos componentes do site, ou pode aguardar que uma tarefa agendada, como uma cópia de segurança do site que deixa e, em seguida, mais tarde reinicia o serviço SMS_Executive por si.  

Para utilizar o Gestor de serviço do Configuration Manager, na consola de ir para **monitorização** > **estado do sistema** > **estado do componente**, escolha **iniciar**e, em seguida, escolha **do serviço do Configuration Manager**. No Service Manager:  

-   No painel de navegação, expanda o site, expanda **componentes**e, em seguida, selecione o componente que pretende reiniciar.  

-   No painel de detalhes, o componente com o botão direito e, em seguida, selecione **consulta**.  

-   Depois do Estado do componente for confirmado, faça duplo clique o componente novamente e, em seguida, escolha **parar**.  

-   **Consulta** o componente novamente para confirmar que é parada, o componente de contexto mais uma vez e, em seguida, escolha **iniciar**.  

> [!IMPORTANT]  
>  O processo que adiciona automaticamente uma subscrição do Microsoft Intune para o ponto de ligação de serviço define a função de sistema de sites para estar online. O ponto de ligação de serviço não suporta o modo offline quando estiver configurado com uma subscrição do Intune.  

**Quando a função é instalada num computador que seja remoto relativamente ao servidor do site:**  

-   A conta de computador do servidor do site tem de ser um administrador local no computador que aloja uma ligação de serviço remoto.

-   Tem de configurar o servidor de sistema de sites que aloja a função com uma conta de instalação do sistema de sites.  

-   O Gestor de distribuição no servidor do site utiliza a conta de instalação do sistema de sites para transferir atualizações a partir do ponto de ligação de serviço.

##  <a name="bkmk_urls"></a>Requisitos de acesso à Internet  
Para ativar a operação, o computador que aloja o ponto de ligação de serviço e todas as firewalls entre nesse computador e a Internet tem de passar comunicações que faz através de **porta TCP 443** e **porta TCP 443** para as localizações de Internet seguinte. A ligação de serviço do ponto também suporta a utilizar um web proxy (com ou sem autenticação) para utilizar estas localizações.  Se precisar de configurar uma conta de proxy web consulte o artigo: [Suporte de servidor proxy no System Center Configuration Manager](/sccm/core/plan-design/network/proxy-server-support).

**As atualizações e manutenção**  

-   *.akamaiedge.net  

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


**Manutenção do Windows 10**  

-   download.microsoft.com  

-   https://go.microsoft.com/fwlink/?LinkID=619849  

## <a name="install-the-service-connection-point"></a>Instalar o ponto de ligação de serviço
Quando executa **configuração** para instalar o site de nível superior de uma hierarquia, tem a opção para instalar o ponto de ligação de serviço.

Após a execução do programa de configuração ou se estiver a reinstalar a função de sistema de sites, utilize o **adicionar funções do sistema de sites** assistente ou no **criar servidor do sistema de sites** Assistente para instalar o sistema de sites num servidor do site de nível superior da hierarquia, ou seja, o site de administração central ou um site primário autónomo. Ambos os assistentes estão no **base** separador na consola em **administração** > **configuração do Site** > **servidores e funções de sistema de sites**.

## <a name="log-files-used-by-the-service-connection-point"></a>Ficheiros de registo utilizados pelo ponto de ligação de serviço
Para ver informações sobre os carregamentos para a Microsoft, consulte o **dmpuploader** no computador que executa o ponto de ligação de serviço.  Para as transferências, incluindo o progresso da transferência das atualizações, ver **dmpdownloader**. Para a lista completa de registos relacionados com o ponto de ligação de serviço, consulte o artigo [ponto de ligação de serviço](/sccm/core/plan-design/hierarchy/log-files#BKMK_WITLog) no tópico de ficheiros de registo do Configuration Manager.

Também pode utilizar as fluxogramas seguinte para compreender o fluxo de processo e entradas de chave de registo de atualização transferências e a replicação das atualizações para outros sites:
 - [Fluxograma - transfiram as atualizações](/sccm/core/servers/manage/download-updates-flowchart)
 - [Fluxograma - replicação de atualização](/sccm/core/servers/manage/update-replication-flowchart)

