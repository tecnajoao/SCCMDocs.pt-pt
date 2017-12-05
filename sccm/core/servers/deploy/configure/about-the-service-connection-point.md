---
title: "Ponto de ligação de serviço"
titleSuffix: Configuration Manager
description: "Saiba mais sobre esta função de sistema de sites do Configuration Manager e compreenda e planeie as várias utilizações."
ms.custom: na
ms.date: 6/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bc2282d5-0571-465b-9528-a555855eaacd
caps.latest.revision: "18"
caps.handback.revision: "0"
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 145fe172665310caa48d8f152ad46d72df4168dd
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/04/2017
---
# <a name="about-the-service-connection-point-in-system-center-configuration-manager"></a>Acerca do ponto de ligação de serviço no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O ponto de ligação de serviço do System Center Configuration Manager é uma função de sistema de sites que serve várias funções importantes para a hierarquia. Antes de configurar o ponto de ligação de serviço, compreenda e planeie as várias utilizações, que podem afetar a forma como configura esta função de sistema de sites:  

-   **Gerir dispositivos móveis com o Microsoft Intune** -esta função substitui o conector do Windows Intune que versões anteriores do Configuration Manager utilizado e podem ser configurados com os detalhes da subscrição do Intune. Consulte [gestão híbrida de dispositivos móveis (MDM) com o System Center Configuration Manager e o Microsoft Intune](../../../../mdm/understand/hybrid-mobile-device-management.md).  

-   **Gerir dispositivos móveis com MDM no local** -esta função fornece suporte para dispositivos no local que gere e que não ligam à Internet. Consulte [gerir dispositivos móveis com a infraestrutura no local no System Center Configuration Manager](../../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

-   **Carregar dados de utilização da sua infraestrutura do Configuration Manager** -pode controlar o nível ou a quantidade de detalhes que carrega. Os dados carregados ajudam-nos a:  

    -   Identificar e resolver problemas proativamente  

    -   Melhorar os nossos produtos e serviços  

    -   Identificar as atualizações para o Configuration Manager que se aplicam à versão do Configuration Manager que utilizar  

  Para informações sobre como alterar o nível da coleção depois da função é instalada e dados que recolhe de cada nível, consulte [diagnósticos e dados de utilização](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data)e, em seguida, siga a ligação para a versão do Configuration Manager que utilizar.  

  Para obter mais informações, consulte [níveis de dados de utilização e definições](../../../../core/servers/deploy/install/setup-reference.md#bkmk_usage).  

-   **Transferir as atualizações que se aplicam à sua infraestrutura do Configuration Manager** - só relevantes para a sua infraestrutura são disponibilizadas atualizações com base nos dados de utilização que carrega.  

- **Cada hierarquia suporta uma única instância desta função:**  

 -   A função de sistema de sites só pode ser instalada no site de nível superior da sua hierarquia, o que é um site de administração central ou site primário autónomo.  

  -   Se expandir um site primário autónomo para uma hierarquia maior, tem de desinstalar esta função do site primário e pode, em seguida, instalá-la no site de administração central.  


##  <a name="bkmk_modes"></a>Modos de operação  
 O ponto de ligação de serviço suporta dois modos de funcionamento:  

-   No **modo online**, o ponto de ligação de serviço verifica automaticamente, a cada 24 horas atualizações e, em seguida, transfere as novas atualizações que estão disponíveis para a sua versão de produto e a infraestrutura atual para que fiquem disponíveis na consola do Configuration Manager.  

-   No **modo offline**, o ponto de ligação de serviço não liga ao serviço de nuvem da Microsoft e tem manualmente [utilizar a ferramenta de ligação de serviço do System Center Configuration Manager](../../../../core/servers/manage/use-the-service-connection-tool.md) para importar as atualizações disponíveis.  

Quando altera entre os modos online ou offline depois de instalar o ponto de ligação de serviço, em seguida, tem de reiniciar o thread SMS_DMP_DOWNLOADER do serviço do SMS_Executive do Configuration Manager antes desta alteração entrar em vigor. Para tal, utilize o Gestor do serviço do Configuration Manager para reiniciar apenas o thread SMS_DMP_DOWNLOADER do serviço SMS_Executive. Também pode reiniciar o serviço SMS_Executive no Configuration Manager, que reinicia a maior parte dos componentes do site, ou pode aguardar uma tarefa agendada, como uma cópia de segurança do site que para e, em seguida, mais tarde, reinicia o serviço SMS_Executive por si.  

Para utilizar o Configuration Manager Service Manager, na consola de ir para **monitorização** > **estado do sistema** > **estado do componente**, escolha **iniciar**e, em seguida, escolha **do serviço do Configuration Manager**. No Service Manager:  

-   No painel de navegação, expanda o site, expanda **componentes**e, em seguida, escolha o componente que pretende reiniciar.  

-   No painel de detalhes, faça duplo clique o componente e, em seguida, escolha **consulta**.  

-   Depois do Estado do componente é confirmado, clique com botão direito o componente novamente e, em seguida, escolha **parar**.  

-   **Consulta** o componente novamente para confirmar se está parado, faça duplo clique o componente mais uma vez e, em seguida, escolha **iniciar**.  

> [!IMPORTANT]  
>  O processo que adiciona automaticamente uma subscrição do Microsoft Intune para o ponto de ligação de serviço define a função de sistema de sites para estar online. O ponto de ligação de serviço não suporta o modo offline quando é configurada com uma subscrição do Intune.  

**Quando a função é instalada num computador que esteja remoto a partir do servidor do site:**  

-   A conta de computador do servidor do site tem de ser um administrador local no computador que aloja uma ligação de serviço remoto.

-   Tem de configurar o servidor de sistema de sites que aloja a função com uma conta de instalação do sistema de sites.  

-   O Gestor de distribuição no servidor do site utiliza a conta de instalação do sistema de sites para transferir atualizações a partir do ponto de ligação de serviço.

##  <a name="bkmk_urls"></a>Requisitos de acesso à Internet  
Para ativar a operação, o computador que aloja o ponto de ligação de serviço e quaisquer firewalls entre esse computador e da Internet tem de passar as comunicações através de **porta TCP 443** e **porta TCP 443** para as localizações de Internet seguintes. A serviço do ponto de ligação também suporta a utilização de um proxy web (com ou sem autenticação) para utilizar estas localizações.  Se precisar de configurar uma conta de proxy web consulte: [Suporte para servidor proxy no System Center Configuration Manager](/sccm/core/plan-design/network/proxy-server-support).

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
-   https://login.microsoftonline.com/{TenantID}


**Manutenção do Windows 10**  

-   download.microsoft.com  

-   https://go.microsoft.com/fwlink/?LinkID=619849  

## <a name="install-the-service-connection-point"></a>Instalar o ponto de ligação de serviço
Quando executa **configuração** para instalar o site de nível superior de uma hierarquia, tem a opção para instalar o ponto de ligação de serviço.

Após a execução do programa de configuração, ou se estiver a reinstalar a função de sistema de sites, utilize o **adicionar funções do sistema de sites** assistente ou no **criar servidor do sistema de sites** Assistente para instalar o sistema de sites num servidor no site de nível superior da hierarquia, ou seja, o site de administração central ou um site primário autónomo. Ambos os assistentes são no **home page** separador na consola em **administração** > **configuração do Site** > **servidores e funções de sistema de sites**.

## <a name="log-files-used-by-the-service-connection-point"></a>Ficheiros de registo utilizados pelo ponto de ligação de serviço
Para ver informações sobre carregamentos para a Microsoft, consulte o **Dmpuploader.log** no computador que executa o ponto de ligação de serviço.  Para as transferências, incluindo o progresso da transferência das atualizações, ver **Dmpdownloader.log**. Para obter a lista completa de registos relacionadas com o ponto de ligação de serviço, consulte [ponto de ligação de serviço](/sccm/core/plan-design/hierarchy/log-files#BKMK_WITLog) no tópico de ficheiros de registo do Configuration Manager.

Também pode utilizar as seguintes fluxogramas para compreender o fluxo de processo e entradas de chave de registo para transferências de atualização e para replicação de atualizações para outros sites:
 - [Fluxograma – Transferir atualizações](/sccm/core/servers/manage/download-updates-flowchart)
 - [Fluxograma – Atualizar replicação](/sccm/core/servers/manage/update-replication-flowchart)
