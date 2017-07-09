---
title: "Atualizações | Microsoft Docs"
description: "Saiba mais sobre um método de serviço no console chamado * * atualizações e manutenção * * que torna mais fácil localizar e instalar as atualizações recomendadas."
ms.custom: na
ms.date: 05/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3a832943-580a-4a40-b454-961d0854ac2b
caps.latest.revision: 51
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: f4c46bfab9b40b29654f4e883817a5508ab25b74
ms.openlocfilehash: 4bc076bba4672d0be0032ec785da20e60b11a6c4
ms.contentlocale: pt-pt
ms.lasthandoff: 06/28/2017


---
# <a name="updates-for-system-center-configuration-manager"></a>Atualizações para o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

O System Center Configuration Manager usa um método de serviço no console chamado **atualizações e manutenção** que torna mais fácil para localizar e instalar atualizações recomendadas para sua infraestrutura do Configuration Manager. Esse método de serviço no console é complementado por atualizações fora de banda, como hotfixes que são destinados aos clientes que precisam resolver problemas que podem ser específicos para seus ambientes.  

> [!TIP]  
> Ao gerenciar o site do System Center Configuration Manager e infraestrutura de hierarquia, os termos de *atualização*, *atualizar*, e *instalar* são usados para descrever os três conceitos separados. Para saber como cada termo é usado, consulte [sobre atualização, atualização e instalação](/sccm/core/understand/upgrade-update-install).


 **Os tópicos a seguir podem ajudá-lo a entender como localizar e instalar os diferentes tipos de atualizações para o System Center Configuration Manager:**  

-   [Instalar atualizações no console do System Center Configuration Manager](../../../core/servers/manage/install-in-console-updates.md)  

-   [Usar a ferramenta de Conexão de serviço do System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md)  

-   [Use a ferramenta de registro de atualização para importar hotfixes para o System Center Configuration Manager](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md)  

-   [Usar o instalador do Hotfix para instalar atualizações para o System Center Configuration Manager](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md)  


Se você usar a ramificação de visualização técnica, consulte [visualização técnica do System Center Configuration Manager](/sccm/core/get-started/technical-preview) para obter informações adicionais específicas para a ramificação.


##  <a name="bkmk_Baselines"></a> Versões de linha de base e de atualização  
 A primeira versão da ramificação atual do System Center Configuration Manager foi a versão 1511, que era uma versão de linha de base. Versões mais recentes de linha de base incluem versão 1606 e 1702:

-   Utilize a versão de linha de base mais recente ao instalar um novo site numa nova hierarquia.  

-   Tem de utilizar uma versão de linha de base para atualizar a partir do System Center 2012 Configuration Manager.  

-   Periodicamente, versões adicionais de linha de base são lançadas. Quando você usa a versão de linha de base mais recente para instalar uma nova hierarquia, que você evita a instalação de uma versão desatualizada do Configuration Manager, seguido por uma atualização de sua infraestrutura para colocá-lo atualizado.  

Depois de instalar uma versão de linha de base, ficarão disponíveis versões adicionais do Configuration Manager como atualizações na consola. Nas atualizações da consola, atualize a sua infraestrutura para a versão mais recente do Configuration Manager.  

-   Instale atualizações na consola para atualizar a versão do seu site de nível superior.  

-   As atualizações que instalar no site de administração central serão automaticamente instaladas nos sites primários subordinados, exceto se forem bloqueadas por uma janela de manutenção configurada por si no site primário.  

-   Tem de atualizar manualmente os sites secundários para uma nova versão de atualização a partir da própria consola.  

Ao instalar uma atualização, a atualização armazena os ficheiros de instalação correspondentes a essa versão no servidor do site numa pasta denominada CD.Latest. Consulte [CD. Pasta mais recente para o System Center Configuration Manager](../../../core/servers/manage/the-cd.latest-folder.md) para obter mais informações sobre esses arquivos.  

-   Utilize os ficheiros na pasta CD.Latest para a recuperação de sites e para instalar sites adicionais numa hierarquia que já não execute uma versão de linha de base.  

-   Não é possível utilizar ficheiros de instalação da pasta CD.Latest para instalar o primeiro site de uma nova hierarquia nem para atualizar um site a partir do System Center 2012 Configuration Manager.  

Algumas atualizações do Configuration Manager estão disponíveis tanto como versões de atualização na consola para uma infraestrutura existente, como novas versões de linha de base.  

As seguintes versões do Configuration Manager estão disponíveis como linha de base, como atualização, ou ambas:  

|Versão |Data de disponibilidade|[Data de término do suporte](/sccm/core/servers/manage/current-branch-versions-supported) |Linha de base|Atualização na consola|  
|-------------|-----------|------------|--------------|------------------------|  
|[1702](/sccm/core/plan-design/changes/whats-new-in-version-1702)<br /><br /> 5.00.8498.1000|3/27/2017| 3/27/2018|Sim|Sim|
|[1610](/sccm/core/plan-design/changes/whats-new-in-version-1610)<br /><br /> 5.00.8458.1000|11/18/2016| 11/18/2017|Não|Sim|
|[1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)<br /><br /> 5.00.8412.1000|7/22/2016| 7/22/2017|Não|Sim|
|[1606](/sccm/core/plan-design/changes/whats-new-in-version-1606) com o pacote cumulativo de hotfixes 1606 (KB3186654) </br></br>5.00.8412.1307 *(Observação 1)* |10/12/2016| 7/22/2017|Sim|Não|
| 1602<br /><br /> 5.00.8355.1000|3/11/2016| 3/11/2017|Não|Sim|
| 1511 <br /><br /> 5.00.8325.1000|12/8/2015| 12/8/2016|Sim|Não|  


*(Observação 1)*  a mídia de linha de base 1606 e 1702 está disponível como parte do Microsoft System Center 2016 ou System Center Configuration Manager (ramificação atual e a ramificação de manutenção de longo prazo) versões no [Centro de serviços de licença de Volume](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) (VLSC). Por exemplo, no VLSC você pode procurar *System Center Config Mgr (ramificação atual e LTSB)*, e a mídia de linha de base de versão 1606 e 1702 é retornados e disponível para download.

Para verificar a versão do seu site do Configuration Manager, aceda a **Acerca do System Center Configuration Manager** no canto superior esquerdo da consola onde é apresentada a nova versão da consola e do site.  

##  <a name="bkmk_inconsole"></a> Atualizações e manutenção na consola  
 Quando você usa uma instalação pronta para produção do System Center Configuration Manager, também conhecido como a ramificação atual, a maioria das atualizações que você instalar estão disponíveis usando as atualizações e manutenção de canal. Este método identifica, transfere e disponibiliza as atualizações que se apliquem à sua versão e configuração de infraestrutura atuais, incluindo apenas as atualizações recomendadas pela Microsoft a todos os clientes.   
 Estas atualizações incluem:  

-   Novas versões, como a versão 1610  

-   Atualizações que incluem novas funcionalidades para a sua versão atual  

-   Correções para a sua versão do Configuration Manager e que todos os clientes devem instalar  

As atualizações na consola garantem uma maior estabilidade e resolvem problemas comuns. Estas atualizações vem substituir os tipos de atualização existentes para versões de produto anteriores para service packs, atualizações cumulativas, correções aplicáveis a todos os clientes e Extensão para o Microsoft Intune. Estas atualizações podem aplicar-se a um ou mais dos seguintes elementos:  

-   Servidores de sites primário e de administração central  

-   Funções de sistema de sites e servidores de sistema de sites  

-   Instâncias do Fornecedor de SMS  

-   Consoles do Configuration Manager  

-   Clientes do Configuration Manager  

Configuration Manager descobre novas atualizações para você quando você sincroniza sua função de sistema de site do ponto de conexão de serviço com o serviço de nuvem da Microsoft e o Centro de download:  

-   Quando o seu ponto de ligação de serviço está no modo online, o seu site sincroniza-se com a Microsoft todos os dias para identificar automaticamente novas atualizações que se apliquem à sua infraestrutura.  Para baixar atualizações e arquivos de redistribuição para atualizações, o computador que hospeda a função de sistema de site do ponto de Conexão de serviço usa o **sistema** contexto para acessar os seguintes locais na Internet: go.microsoft.com e download.microsoft.com. Para obter informações sobre outros locais, o ponto de conexão de serviço se conecta ao, consulte [requisitos de acesso à Internet](../../../core/servers/deploy/configure/about-the-service-connection-point.md#bkmk_urls) na [sobre a conexão de serviço do ponto no System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  

-   Quando o seu ponto de ligação de serviço está no modo offline, utilize a ferramenta de ligação de serviço para sincronizar manualmente com a Microsoft Cloud. Para obter mais informações,ver [ Utilize a Ferramenta de Ligação de Serviço para o System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md).  

-   As atualizações na consola eliminam a necessidade de localizar e instalar atualizações individuais, service packs e novas funcionalidades de forma independente.  

-   Instale apenas as atualizações na consola da sua preferência. Além disso, quando instala algumas atualizações, pode selecionar as funcionalidades individuais que pretende ativar e utilizar. Para obter mais informações, consulte [habilitar recursos opcionais de atualizações](../../../core/servers/manage/install-in-console-updates.md#bkmk_options).  

Ao instalar uma atualização na consola:  

-   Esta executa automaticamente uma verificação de pré- requisitos. Também pode executar esta verificação antes de iniciar a instalação.  

-   Esta é instalada no site de administração central (se tiver um) e em sites primários automaticamente. Você pode controlar quando cada servidor do site primário tem permissão para atualizar sua infraestrutura usando [serviço windows para servidores do site](../../../core/servers/manage/service-windows.md).  

-   Após a atualização de um servidor do site, todas as funções do sistema de sites afetadas (incluindo as instâncias do Fornecedor de SMS) são automaticamente atualizadas. Gerenciador de configurações também solicitam que o usuário do console para atualizar o console, depois que o site instala a atualização.  

-   Se uma atualização incluir o cliente do Configuration Manager, você terá a opção de testar a atualização em pré-produção ou aplicar a atualização a todos os clientes imediatamente.  

-   Após a atualização de um site primário, os sites secundários não atualizam automaticamente. Em vez disso, tem de iniciar a atualização do site secundário.  

> [!NOTE]  
>  Versão de produção do System Center Configuration Manager (ramificação atual), a ramificação de manutenção de longo prazo e a visualização técnica do System Center Configuration Manager são versões diferentes. Portanto, as atualizações que se aplicam a uma ramificação não estão disponíveis como atualizações no console para as outras ramificações. Para obter mais informações sobre ramificações disponíveis, consulte [qual ramificação do Configuration Manager devo usar?](/sccm/core/understand/which-branch-should-i-use)

##  <a name="bkmk_outofband"></a> Correções fora de banda  
Algumas correções são lançadas com disponibilidade limitada no sentido de abordar problemas específicos, ou são aplicáveis a todos os clientes, não podendo, contudo, ser instaladas através do método na consola. Estas correções são fornecidas fora da banda e não são detetadas a partir do serviço Microsoft Cloud.  

Normalmente, você fica ciente dos hotfixes fora de banda de suporte técnico da Microsoft, um artigo da Base de dados de conhecimento ou do [blog da equipe do System Center Configuration Manager](https://blogs.technet.microsoft.com/configmgrteam) quando procura corrigir ou solucionar um problema com sua implantação do Configuration Manager.  

Pode instalar estas correções manualmente através de um destes dois métodos:  

-   **Ferramenta de registro de atualização:** Essa ferramenta importa o hotfix manualmente no console do Configuration Manager que você pode, em seguida, instalar a atualização como você faria no console atualizações que são descobertos automaticamente. Este método é atualizado para atualizações que utilizem a seguinte estrutura de nome de ficheiro: **.update.exe**.  O nome de arquivo completo para esse tipo de hotfix é semelhante a: **&lt;Produto\>-&lt;versão do produto\>-&lt;ID do artigo\>-ConfigMgr.Update.exe**.  

     Para obter mais informações, consulte [usar a ferramenta de registro de atualização para importar hotfixes para o System Center Configuration Manager](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md).  

-   **Instalador do hotfix:** Essa ferramenta é usada para instalar manualmente um hotfix que não pode ser instalado usando o método no console. Esse método é usado para correções que usam a seguinte estrutura de nome de arquivo: **&lt;Product\>-&lt;product version\>-&lt;KB article ID\>-&lt;platform\>-&lt;language\>.exe**.

     Para obter mais informações, consulte [usar o instalador do Hotfix para instalar atualizações para o System Center Configuration Manager](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md).

