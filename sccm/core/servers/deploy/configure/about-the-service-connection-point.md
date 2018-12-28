---
title: Ponto de ligação de serviço
titleSuffix: Configuration Manager
description: Saiba mais sobre esta função de sistema de sites do Configuration Manager e compreenda e planeie as várias utilizações.
ms.date: 08/01/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bc2282d5-0571-465b-9528-a555855eaacd
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5bf79fa360faecc6d103a2fd209c7f7e5eb9597c
ms.sourcegitcommit: 81e3666c41eb976cc7651854042dafe219e2e467
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/21/2018
ms.locfileid: "53747097"
---
# <a name="about-the-service-connection-point-in-configuration-manager"></a>Acerca do ponto de ligação de serviço no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O ponto de ligação de serviço é uma função de sistema de sites que serve várias funções importantes para a hierarquia. Antes de configurar o ponto de ligação de serviço, compreenda e planeie as várias utilizações. Planear a utilização pode afetar a forma como configura esta função de sistema de sites:  

- **Gerir dispositivos móveis com o Microsoft Intune**: Esta função substitui o conector do Windows Intune que podem ser configuradas com os detalhes de subscrição do Intune e utilizam de versões anteriores do Configuration Manager. Para obter mais informações, consulte [gestão de dispositivos móveis híbridos (MDM)](/sccm/mdm/understand/hybrid-mobile-device-management).  

- **Gerir dispositivos móveis com MDM no local**: Esta função fornece suporte para dispositivos no local que gere e que não se ligar à internet. Para obter mais informações, consulte [gerir dispositivos móveis com a infraestrutura no local](/sccm/mdm/understand/manage-mobile-devices-with-on-premises-infrastructure).  

- **Carregar dados de utilização da sua infraestrutura do Configuration Manager**: Pode controlar o nível ou a quantidade de detalhes que carrega. Os dados carregados ajudam:  

    - Identificar e resolver problemas proativamente  

    - Melhorar os nossos produtos e serviços  

    - Identificar as atualizações do Configuration Manager que se aplicam à versão do Configuration Manager que utilizar  

    Para obter mais informações sobre como alterar o nível de coleção após instala a função e de dados que recolhe de cada nível, consulte [diagnósticos e dados de utilização](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data). Em seguida, siga a ligação para a versão do Configuration Manager que utilizar.  

    Para obter mais informações, consulte [níveis de utilização de dados e definições](/sccm/core/servers/deploy/install/setup-reference#bkmk_usage).  

- **Transferir as atualizações aplicáveis à sua infraestrutura do Configuration Manager**: Apenas as atualizações relevantes para a sua infraestrutura são disponibilizadas com base nos dados de utilização que carrega.  

- **Cada hierarquia suporta uma única instância desta função**:  

    - A função de sistema de sites só pode ser instalada no site de nível superior da hierarquia, que é um site de administração central ou site primário autónomo.  

    - Se expandir um site primário autónomo para uma hierarquia maior, tem de desinstalar esta função do site primário e pode, em seguida, instalá-la no site de administração central.  


##  <a name="bkmk_modes"></a> Modos de operação  
O ponto de ligação de serviço suporta dois modos de funcionamento:  

- Na **modo online**, o ponto de ligação de serviço procura automaticamente a cada 24 horas atualizações. Transfere as novas atualizações disponíveis para a sua infraestrutura atual e versão de produto para que fiquem disponíveis na consola do Configuration Manager.  

- Na **modo offline**, o ponto de ligação do serviço não liga ao serviço de nuvem da Microsoft. Para importar manualmente as atualizações disponíveis, utilize o [ferramenta de ligação de serviço](/sccm/core/servers/manage/use-the-service-connection-tool).  

Se mudar entre os modos online ou offline depois de instalar o ponto de ligação de serviço, tem de reiniciar o thread SMS_DMP_DOWNLOADER do serviço SMS_Executive do Configuration Manager para a alteração entra em vigor. Pode utilizar o Gestor de serviço do Configuration Manager para reiniciar apenas o thread SMS_DMP_DOWNLOADER do serviço SMS_Executive. Também pode reiniciar o serviço SMS_Executive no Configuration Manager, que reinicia a maioria dos componentes do site. Em alternativa, pode aguardar uma tarefa agendada, como uma cópia de segurança do site, que para e, em seguida, mais tarde, reinicia o serviço SMS_Executive para.  

Para utilizar o Gestor de serviço do Configuration Manager, na consola do aceda à **monitorização** > **estado do sistema** > **estado do componente**, escolha **Começar**e, em seguida, escolha **Configuration Manager Service Manager**. No Service Manager:  

- No painel de navegação, expanda o site, expanda **componentes**e, em seguida, selecione o componente que pretende reiniciar.  

- No painel de detalhes, faça duplo clique o componente e, em seguida, escolha **consulta**.  

- Depois do Estado do componente é confirmado, com o botão direito o componente novamente e, em seguida, escolha **parar**.  

- **Consulta** o componente novamente para confirmar que está parada. Faça duplo clique o componente mais uma vez e, em seguida, escolha **iniciar**.  

> [!IMPORTANT]  
> O processo que adiciona automaticamente uma subscrição do Microsoft Intune para o ponto de ligação de serviço define a função de sistema de sites para estar online. O ponto de ligação de serviço não suporta o modo offline quando este está configurado com uma subscrição do Intune.  

**Quando a função é instalada num computador remoto do servidor do site:**  

- A conta de computador do servidor do site tem de ser um administrador local no computador que aloja uma ligação de serviço remoto.

- Tem de configurar o servidor de sistema de sites que aloja a função com uma conta de instalação do sistema de sites.  

- O Gestor de distribuição no servidor do site utiliza a conta de instalação do sistema de sites para transferir atualizações a partir do ponto de ligação de serviço.

##  <a name="bkmk_urls"></a> Requisitos de acesso de Internet  
Para ativar a operação, o computador que aloja o ponto de ligação de serviço e todas as firewalls entre esse computador e a internet tem de passar comunicações através da porta de saída **TCP 443** para HTTPS e a porta de saída  **TCP 80** para HTTP para o abaixo localizações de internet. A serviço do ponto de ligação também suporta a utilização de um proxy web (com ou sem autenticação) para utilizar estas localizações. Se precisar de configurar uma conta de proxy da web, consulte [suporte de servidor de Proxy](/sccm/core/plan-design/network/proxy-server-support).

> [!TIP]  
> O ponto de ligação de serviço utiliza o serviço do Microsoft Intune, quando se liga a go.microsoft.com ou gerir. Microsoft.com. Existe um problema conhecido no qual o conector do Intune apresentar problemas de conectividade se o certificado de raiz Baltimore CyberTrust não estiver instalado, expirou ou está danificado no ponto de ligação de serviço. Para obter mais informações, consulte [ponto de ligação de serviço não transferir as atualizações](https://support.microsoft.com/help/3187516).  

#### <a name="updates-and-servicing"></a>As atualizações e manutenção

- `*.akamaiedge.net`  

- `*.akamaitechnologies.com`  

- `*.manage.microsoft.com`  

- `go.microsoft.com`  

- `blob.core.windows.net`  

- `download.microsoft.com`  

- `download.windowsupdate.com`  

- `sccmconnected-a01.cloudapp.net`  

- `configmgrbits.azureedge.net`  

#### <a name="microsoft-intune"></a>Microsoft Intune

- `*manage.microsoft.com`  

- `https://bspmts.mp.microsoft.com/V`  

- `https://login.microsoftonline.com/{TenantID}`  

#### <a name="windows-10-servicing"></a>Manutenção do Windows 10

- `download.microsoft.com`  

- `https://go.microsoft.com/fwlink/?LinkID=619849`  

#### <a name="azure-services"></a>Serviços do Azure

- `management.azure.com`  

## <a name="install-the-service-connection-point"></a>Instalar o ponto de ligação de serviço
Quando executa **configuração** para instalar o site de nível superior de uma hierarquia, tem a opção para instalar o ponto de ligação de serviço.

Após a execução do programa de configuração ou se estiver a reinstalar a função de sistema de sites, utilize o **adicionar funções de sistema de sites** assistente ou o **criar servidor do sistema de sites** Assistente para instalar o sistema de sites num servidor no site de nível superior da a hierarquia, ou seja, o site de administração central ou um site primário autónomo. Ambos os assistentes são no **home page** separador na consola **administração** > **configuração do Site** > **servidores e sites Funções do sistema**.



## <a name="log-files-used-by-the-service-connection-point"></a>Ficheiros de registo utilizados pelo ponto de ligação de serviço
Para ver informações sobre carregamentos para a Microsoft, veja a **dmpuploader** no computador que executa o ponto de ligação de serviço.  Para transferências, incluindo o progresso do download de atualizações, veja **dmpdownloader. log**. Para obter a lista completa de registos relacionados com o ponto de ligação de serviço, consulte [ponto de ligação de serviço](/sccm/core/plan-design/hierarchy/log-files#BKMK_WITLog) no artigo de ficheiros de registo do Configuration Manager.

Também pode utilizar os fluxogramas seguintes para compreender o fluxo de processo e entradas de chave de registo de downloads de atualização e replicação de atualizações para outros sites:
- [Fluxograma – Transferir atualizações](/sccm/core/servers/manage/download-updates-flowchart)
- [Fluxograma – Atualizar replicação](/sccm/core/servers/manage/update-replication-flowchart)
