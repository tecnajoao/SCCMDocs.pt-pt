---
title: Atualizações
titleSuffix: Configuration Manager
description: Saiba mais sobre um método de manutenção na consola denominado **atualizações e manutenção** que torna mais fácil localizar e instalar atualizações recomendadas.
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3a832943-580a-4a40-b454-961d0854ac2b
caps.latest.revision: ''
caps.handback.revision: ''
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 8be32aa07819239820711079e4ff3637e96367db
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/23/2018
---
# <a name="updates-for-system-center-configuration-manager"></a>Atualizações para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O System Center Configuration Manager utiliza um método de manutenção na consola denominado **atualizações e manutenção**. Este método na consola torna mais fácil para localizar e instalar as atualizações para a sua infraestrutura do Configuration Manager recomendadas. Manutenção na consola é complementado por atualizações fora de banda, tais como correções que foram concebidas para os clientes que precisem de resolver problemas específicos ao seu respetivo ambiente.  

> [!TIP]  
> Ao gerir o site do System Center Configuration Manager e a infraestrutura de hierarquia, os termos de licenciamento *atualizar*, *atualizar*, e *instalar* são utilizados para descrever três conceitos diferentes. Para saber como cada termo é utilizado, consulte [sobre a atualização, atualização e instalação](/sccm/core/understand/upgrade-update-install).


 **Os tópicos seguintes podem ajudá-lo a compreender como encontrar e instalar os diferentes tipos de atualização para o System Center Configuration Manager:**  

-   [Instalar atualizações na consola do System Center Configuration Manager](../../../core/servers/manage/install-in-console-updates.md)  

-   [Utilizar a ferramenta de ligação de serviço do System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md)  

-   [Utilize a ferramenta de registo de atualização para importar correções para o System Center Configuration Manager](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md)  

-   [Utilizar o instalador de correções para instalar atualizações para o System Center Configuration Manager](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md)  


Se utilizar o ramo do Technical Preview, consulte [pré-visualização técnica do System Center Configuration Manager](/sccm/core/get-started/technical-preview) para obter informações adicionais que são específicas para nessa sucursal.


##  <a name="bkmk_Baselines"></a> Versões de linha de base e de atualização  
 A primeira versão do ramo atual do System Center Configuration Manager tinha a versão 1511, que era uma versão de linha de base. Versões de linha de base mais recentes incluem versão 1702 e 1802:

-   Utilize a versão de linha de base mais recente ao instalar um novo site numa nova hierarquia.  

-   Utilizar uma versão de linha de base a atualização do System Center 2012 Configuration Manager. Depois de atualizar para o System Center Configuration Manager, pode deixar de utilizar versões de linha de base para se manter atual em vez disso, apenas [atualizações na consola](/sccm/core/servers/manage/install-in-console-updates) para atualizar para a versão mais recente.  

-   Periodicamente, são lançadas versões de linha de base adicionais. Quando utilizar a versão de linha de base mais recente para instalar uma nova hierarquia, evite instalar uma versão desatualizada do Configuration Manager seguido por uma atualização adicional da sua infraestrutura para colocá-lo atualizados.  

Depois de instalar uma versão de linha de base, ficarão disponíveis versões adicionais do Configuration Manager como atualizações na consola. Nas atualizações da consola, atualize a sua infraestrutura para a versão mais recente do Configuration Manager.  

-   Instale atualizações na consola para atualizar a versão do seu site de nível superior.  

-   Instalação de atualizações que instalar num site de administração central automaticamente em sites primários subordinados, exceto se forem bloqueadas por uma janela de manutenção configuradas no site primário.  

-   Atualizar manualmente os sites secundários para uma nova versão de atualização da consola do.  

Ao instalar uma atualização, a atualização armazena os ficheiros de instalação correspondentes a essa versão no servidor do site numa pasta denominada CD.Latest. Para obter mais informações sobre estes ficheiros, consulte [o CD. Pasta mais recente para o System Center Configuration Manager](../../../core/servers/manage/the-cd.latest-folder.md).  

-   Utilize os ficheiros no CD. Pasta mais recente durante a recuperação de Site e para instalar sites adicionais numa hierarquia que já não executa uma versão de linha de base.  

-   Não é possível utilizar ficheiros de instalação da pasta CD.Latest para instalar o primeiro site de uma nova hierarquia nem para atualizar um site a partir do System Center 2012 Configuration Manager.  

Algumas atualizações do Configuration Manager estão disponíveis tanto como versões de atualização na consola para uma infraestrutura existente, como novas versões de linha de base.  

As seguintes versões do Configuration Manager estão disponíveis como linha de base, como atualização, ou ambas:  

|Versão |Data de disponibilidade|[Data de fim de suporte](/sccm/core/servers/manage/current-branch-versions-supported) |Linha de base|Atualização na consola|  
|-------------|-----------|------------|--------------|------------------------|  
|[1802](/sccm/core/plan-design/changes/whats-new-in-version-1802)<br /><br /> 5.00.8634.1000|22 de Março de 2018|22 de Setembro de 2019|Sim|Sim|
|[1710](/sccm/core/plan-design/changes/whats-new-in-version-1710)<br /><br /> 5.00.8577.1000|20 de Novembro de 2017|20 de Maio de 2019|Não|Sim|
|[1706](/sccm/core/plan-design/changes/whats-new-in-version-1706)<br /><br /> 5.00.8540.1000|31 de Julho de 2017|31 de Julho de 2018|Não|Sim|
|[1702](/sccm/core/plan-design/changes/whats-new-in-version-1702)<br /><br /> 5.00.8498.1000|27 de Março de 2017| 27 de Março de 2018|Sim|Sim|
|[1610](/sccm/core/plan-design/changes/whats-new-in-version-1610)<br /><br /> 5.00.8458.1000|18 de Novembro de 2016| 18 de Novembro de 2017|Não|Sim|
|[1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)<br /><br /> 5.00.8412.1000|22 de Julho de 2016| 22 de Julho de 2017|Não|Sim|
|[1606](/sccm/core/plan-design/changes/whats-new-in-version-1606) com o rollup de correção 1606 (KB3186654) </br></br>5.00.8412.1307 *(tenha em atenção 1)* |12 de Outubro de 2016| 12 de Outubro de 2017|Sim|Não|
| 1602<br /><br /> 5.00.8355.1000|11 de Março de 2016| 11 de Março de 2017|Não|Sim|
| 1511 <br /><br /> 5.00.8325.1000|8 de Dezembro de 2015| 8 de Dezembro de 2016|Sim|Não|  


*(Nota 1)*  o suporte de dados de linha de base 1802 e 1702 está disponíveis como parte do Microsoft System Center 2016 ou o System Center Configuration Manager (ramo atual e ramo de manutenção de longo prazo) versões no [Centro de serviços de licenciamento de Volume](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) (VLSC). Por exemplo, no VLSC pode procurar *System Center Config Mgr (ramo atual e LTSB)*, e 1802 e 1702 versão da linha de base suporte de dados é devolvidos e disponível para transferência.

Para verificar a versão do seu site do Configuration Manager, aceda a **Acerca do System Center Configuration Manager** no canto superior esquerdo da consola onde é apresentada a nova versão da consola e do site.  

##  <a name="bkmk_inconsole"></a> Atualizações e manutenção na consola  
 Ao utilizar uma instalação pronta para produção do System Center Configuration Manager, também referida como ramo atual, a maioria das atualizações que instalar estão disponíveis utilizando as atualizações e manutenção de canal. Este método identifica, transfere e disponibiliza as atualizações que se apliquem à sua versão e configuração de infraestrutura atuais, incluindo apenas as atualizações recomendadas pela Microsoft a todos os clientes.   
 Estas atualizações incluem:  

-   Novas versões, como versão 1702, 1706, 1710 ou 1802.  

-   Atualizações, que incluem novas funcionalidades para a sua versão atual.

-   Correções, para a sua versão do Configuration Manager e que todos os clientes devem instalar.

As atualizações na consola garantem uma maior estabilidade e resolvem problemas comuns. Estas atualizações vem substituir os tipos de atualização existentes para versões de produto anteriores para service packs, atualizações cumulativas, correções aplicáveis a todos os clientes e Extensão para o Microsoft Intune. Estas atualizações podem aplicar-se a um ou mais dos seguintes elementos:  

-   Servidores de sites primário e de administração central  

-   Funções de sistema de sites e servidores de sistema de sites  

-   Instâncias do Fornecedor de SMS  

-   Consolas do Configuration Manager  

-   Clientes do Configuration Manager  

O Configuration Manager Deteta novas atualizações para si quando sincronizar a sua função de sistema de sites de ponto de ligação de serviço com o serviço de nuvem da Microsoft e Centro de transferências:  

-   Quando o seu ponto de ligação de serviço está no modo online, o seu site sincroniza-se com a Microsoft todos os dias para identificar automaticamente novas atualizações que se apliquem à sua infraestrutura.  Para transferir atualizações e ficheiros de redist para atualizações, o computador que aloja a função de sistema de sites do ponto de ligação de serviço utiliza o **sistema** contexto para aceder a localizações de Internet seguintes: go.microsoft.com e download.microsoft.com. Para obter informações sobre localizações adicionais que o ponto de ligação de serviço liga ao, consulte [requisitos de acesso à Internet](../../../core/servers/deploy/configure/about-the-service-connection-point.md#bkmk_urls) no [sobre a ligação de serviço do ponto no System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md) .  

-   Quando o seu ponto de ligação de serviço está no modo offline, utilize a ferramenta de ligação de serviço para sincronizar manualmente com a Microsoft Cloud. Para obter mais informações,ver [ Utilize a Ferramenta de Ligação de Serviço para o System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md).  

-   As atualizações na consola eliminam a necessidade de localizar e instalar atualizações individuais, service packs e novas funcionalidades de forma independente.  

-   Instale apenas as atualizações na consola da sua preferência. Além disso, quando instala algumas atualizações, pode selecionar as funcionalidades individuais que pretende ativar e utilizar. Para obter mais informações, consulte [ativar funcionalidades opcionais de atualizações](../../../core/servers/manage/install-in-console-updates.md#bkmk_options).  

Ao instalar uma atualização na consola:  

-   Esta executa automaticamente uma verificação de pré- requisitos. Também pode executar esta verificação antes de iniciar a instalação.  

-   Esta é instalada no site de administração central (se tiver um) e em sites primários automaticamente. Pode controlar quando cada servidor do site primário tem permissão para atualizar a respetiva infraestrutura utilizando [windows para servidores de site do serviço](../../../core/servers/manage/service-windows.md).  

-   Após a atualização de um servidor do site, todas as funções do sistema de sites afetadas (incluindo as instâncias do Fornecedor de SMS) são automaticamente atualizadas. Consolas do Configuration Manager também pedirá ao utilizador a consola para atualizar a consola após a instalação do site a atualização.  

-   Se uma atualização incluir o cliente do Configuration Manager, é-lhe dada a opção para testar a atualização em pré-produção ou por aplicar a atualização para todos os clientes imediatamente.  

-   Após a atualização de um site primário, os sites secundários não atualizam automaticamente. Em vez disso, tem de iniciar a atualização do site secundário.  

> [!NOTE]  
>  A versão de produção do System Center Configuration Manager (ramo atual), o ramo de manutenção de longo prazo e o Technical Preview do System Center Configuration Manager são versões diferentes. Por conseguinte, as atualizações aplicáveis para um ramo não estão disponíveis como atualizações na consola para os outros ramos. Para mais informações sobre ramos disponíveis, consulte [o ramo do Configuration Manager devo utilizar?](/sccm/core/understand/which-branch-should-i-use)

##  <a name="bkmk_outofband"></a> Correções fora de banda  
Algumas correções de versão com disponibilidade limitada para resolver problemas específicos, ou são aplicáveis a todos os clientes, mas não é possível instalar utilizando o método na consola. Estas correções são fornecidas fora da banda e não são detetadas a partir do serviço Microsoft Cloud.  

Normalmente, pode obter informações sobre correções fora de banda do cliente suporte técnico da Microsoft, num artigo da Base de dados de conhecimento, ou a partir de [blogue da equipa do System Center Configuration Manager](https://blogs.technet.microsoft.com/configmgrteam) quando necessita de corrigir ou abordar um problema com a sua implementação do Configuration Manager.  

Pode instalar estas correções manualmente através de um destes dois métodos:  

-   **Ferramenta de registo de atualização:** Esta ferramenta importa manualmente a correção para a consola do Configuration Manager, onde pode, em seguida, instalar a atualização como que seria atualizações na consola que são detetadas automaticamente. Este método é atualizado para atualizações que utilizem a seguinte estrutura de nome de ficheiro: **.update.exe**.  O nome de ficheiro completo para este tipo de correção assemelha-se: **&lt;Produto\>-&lt;versão do produto\>-&lt;ID do artigo KB\>-ConfigMgr.Update.exe**.  

     Para obter mais informações, consulte [utilizar a ferramenta de registo de atualização para importar correções para o System Center Configuration Manager](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md).  

-   **Instalador de correções:** Esta ferramenta é utilizada para instalar manualmente uma correção que não pode ser instalada através do método na consola. Este método é utilizado para correções que utilizem a seguinte estrutura de nome de ficheiro: **&lt;Produto\>-&lt;versão do produto\>-&lt;ID do artigo KB\>-&lt;plataforma\> - &lt;idioma\>.exe**.

     Para obter mais informações, consulte [utilizar o instalador de correções para instalar atualizações para o System Center Configuration Manager](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md).
