---
title: "Atualizações | Documentos do Microsoft"
description: "Saiba mais sobre um método de serviço na consola denominado **atualizações e a manutenção** que torna mais fácil localizar e instalar as atualizações recomendadas."
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
ms.sourcegitcommit: 90775fcf2549080a43e9c1606caa79d9eb90a89c
ms.openlocfilehash: a33960fb89b71c0f8128e21a5054f5b63cfc6b17
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="updates-for-system-center-configuration-manager"></a>Atualizações para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager utiliza um método de serviço na consola denominado **atualizações e a manutenção** que torna mais fácil para localizar e instalar recomendado atualizações para a sua infraestrutura do Configuration Manager. Este método de manutenção na consola é supplemented pelas atualizações de fora de banda, tais como correções que são direcionadas para os clientes que precisem para resolver problemas que possam ser específicos do respetivo ambiente.  

> [!TIP]
> Ao gerir o site do System Center Configuration Manager e a infraestrutura da hierarquia, os termos *atualizar*, *atualizar*, e *instalar* são utilizados para descrever três conceitos separados. Para saber como cada termo é utilizado, consulte o artigo [sobre a atualização, atualização e instalação](/sccm/core/understand/upgrade-update-install).


 **Os tópicos seguintes podem ajudar a compreender como encontrar e instalar os tipos diferentes de atualização para o System Center Configuration Manager:**  

-   [Instalar as atualizações na consola do System Center Configuration Manager](../../../core/servers/manage/install-in-console-updates.md)  

-   [Utilize a ferramenta de ligação de serviço para o System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md)  

-   [Utilizar a ferramenta de registo de atualização para importar correções para o System Center Configuration Manager](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md)  

-   [Utilize o instalador de correção para instalar atualizações para o System Center Configuration Manager](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md)  


Se utilizar o ramo de pré-visualização técnica, consulte o artigo [pré-visualização técnica do System Center Configuration Manager](/sccm/core/get-started/technical-preview) para obter informações adicionais que é específicas de nessa sucursal.


##  <a name="bkmk_Baselines"></a> Versões de linha de base e de atualização  
 A primeira versão do System Center Configuration Manager atual ramo foi versão 1511, que era uma versão de linha de base. Versões mais recentes do plano base incluem a versão 1606 e 1702:

-   Utilize a versão de linha de base mais recente ao instalar um novo site numa nova hierarquia.  

-   Tem de utilizar uma versão de linha de base para atualizar a partir do System Center 2012 Configuration Manager.  

-   Periodicamente, são lançadas versões adicionais do plano base. Quando utiliza a versão mais recente do plano base para instalar uma nova hierarquia que evitar a instalação de uma versão desatualizada do Configuration Manager, seguido de uma atualização da infraestrutura de colocá-lo atualizado.  

Depois de instalar uma versão de linha de base, ficarão disponíveis versões adicionais do Configuration Manager como atualizações na consola. Nas atualizações da consola, atualize a sua infraestrutura para a versão mais recente do Configuration Manager.  

-   Instale atualizações na consola para atualizar a versão do seu site de nível superior.  

-   As atualizações que instalar no site de administração central serão automaticamente instaladas nos sites primários subordinados, exceto se forem bloqueadas por uma janela de manutenção configurada por si no site primário.  

-   Tem de atualizar manualmente os sites secundários para uma nova versão de atualização a partir da própria consola.  

Ao instalar uma atualização, a atualização armazena os ficheiros de instalação correspondentes a essa versão no servidor do site numa pasta denominada CD.Latest. Consulte o artigo [CD. Pasta mais recente para o System Center Configuration Manager](../../../core/servers/manage/the-cd.latest-folder.md) para obter mais informações sobre estes ficheiros.  

-   Utilize os ficheiros na pasta CD.Latest para a recuperação de sites e para instalar sites adicionais numa hierarquia que já não execute uma versão de linha de base.  

-   Não é possível utilizar ficheiros de instalação da pasta CD.Latest para instalar o primeiro site de uma nova hierarquia nem para atualizar um site a partir do System Center 2012 Configuration Manager.  

Algumas atualizações do Configuration Manager estão disponíveis tanto como versões de atualização na consola para uma infraestrutura existente, como novas versões de linha de base.  

As seguintes versões do Configuration Manager estão disponíveis como linha de base, como atualização, ou ambas:  

|Versão |Data de disponibilidade|[Data de fim de suporte](/sccm/core/servers/manage/current-branch-versions-supported) |Linha de base|Atualização na consola|  
|-------------|-----------|------------|--------------|------------------------|  
|[1702](/sccm/core/plan-design/changes/whats-new-in-version-1702)<br /><br /> 5.00.8498.1000|3/27/2017| 3/27/2018|Sim|Sim|
|[1610](/sccm/core/plan-design/changes/whats-new-in-version-1610)<br /><br /> 5.00.8458.1000|11/18/2016| 11/18/2017|Não|Sim|
|[1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)<br /><br /> 5.00.8412.1000|7/22/2016| 7/22/2017|Não|Sim|
|[1606](/sccm/core/plan-design/changes/whats-new-in-version-1606) com o rollup de correção 1606 (KB3186654) </br></br>5.00.8412.1307 *(tenha em atenção 1)* |10/12/2016| 7/22/2017|Sim|Não|
| 1602<br /><br /> 5.00.8355.1000|3/11/2016| 3/11/2017|Não|Sim|
| 1511 <br /><br /> 5.00.8325.1000|12/8/2015| 12/8/2016|Sim|Não|  


*(Nota 1)*  Deste suporte de dados de linha de base 1606 está disponível como parte do Microsoft System Center 2016 ou versão do System Center Configuration Manager (ramo atual e longo prazo manutenção ramo 1606).

Para verificar a versão do seu site do Configuration Manager, aceda a **Acerca do System Center Configuration Manager** no canto superior esquerdo da consola onde é apresentada a nova versão da consola e do site.  

##  <a name="bkmk_inconsole"></a> Atualizações e manutenção na consola  
 Ao utilizar uma instalação pronto de produção do System Center Configuration Manager, também referido como o ramo atual, a maioria das atualizações a que instalar estão disponível utilizando as atualizações e manutenção canal. Este método identifica, transfere e disponibiliza as atualizações que se apliquem à sua versão e configuração de infraestrutura atuais, incluindo apenas as atualizações recomendadas pela Microsoft a todos os clientes.   
 Estas atualizações incluem:  

-   Novas versões, como versão 1610  

-   Atualizações que incluem novas funcionalidades para a sua versão atual  

-   Correções para a sua versão do Configuration Manager e que todos os clientes devem instalar  

As atualizações na consola garantem uma maior estabilidade e resolvem problemas comuns. Estas atualizações vem substituir os tipos de atualização existentes para versões de produto anteriores para service packs, atualizações cumulativas, correções aplicáveis a todos os clientes e Extensão para o Microsoft Intune. Estas atualizações podem aplicar-se a um ou mais dos seguintes elementos:  

-   Servidores de sites primário e de administração central  

-   Funções de sistema de sites e servidores de sistema de sites  

-   Instâncias do Fornecedor de SMS  

-   Consolas do Configuration Manager  

-   Clientes do Configuration Manager  

O Configuration Manager Deteta novas atualizações por si quando sincronizar a sua função de sistema de sites de ponto de ligação de serviço com o serviço de nuvem da Microsoft e o Centro de transferências:  

-   Quando o seu ponto de ligação de serviço está no modo online, o seu site sincroniza-se com a Microsoft todos os dias para identificar automaticamente novas atualizações que se apliquem à sua infraestrutura.  Para transferir atualizações e redist ficheiros de atualizações, o computador que aloja a função de sistema de sites do ponto de ligação de serviço utiliza a **sistema** contexto para aceder as localizações na Internet seguintes: go.microsoft.com e download.microsoft.com. Para obter informações sobre localizações adicionais liga o ponto de ligação de serviço para, consulte o artigo [requisitos de acesso à Internet](../../../core/servers/deploy/configure/about-the-service-connection-point.md#bkmk_urls) no [sobre a ligação de serviço de ponto no System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  

-   Quando o seu ponto de ligação de serviço está no modo offline, utilize a ferramenta de ligação de serviço para sincronizar manualmente com a Microsoft Cloud. Para obter mais informações,ver [ Utilize a Ferramenta de Ligação de Serviço para o System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md).  

-   As atualizações na consola eliminam a necessidade de localizar e instalar atualizações individuais, service packs e novas funcionalidades de forma independente.  

-   Instale apenas as atualizações na consola da sua preferência. Além disso, quando instala algumas atualizações, pode selecionar as funcionalidades individuais que pretende ativar e utilizar. Para obter mais informações, consulte o artigo [permitem funcionalidades opcionais das atualizações da](../../../core/servers/manage/install-in-console-updates.md#bkmk_options).  

Ao instalar uma atualização na consola:  

-   Esta executa automaticamente uma verificação de pré- requisitos. Também pode executar esta verificação antes de iniciar a instalação.  

-   Esta é instalada no site de administração central (se tiver um) e em sites primários automaticamente. Pode controlar quando cada servidor do site primário é permitida para atualizar a respetiva infraestrutura através de [windows dos servidores do site do serviço](../../../core/servers/manage/service-windows.md).  

-   Após a atualização de um servidor do site, todas as funções do sistema de sites afetadas (incluindo as instâncias do Fornecedor de SMS) são automaticamente atualizadas. Consolas do Configuration Manager também pedirá ao utilizador a consola para atualizar a consola após a instalação do site a atualização.  

-   Se uma atualização incluir o cliente do Configuration Manager, é-lhe oferecida a opção para testar a atualização no pré-produção ou para aplicar a atualização a todos os clientes imediatamente.  

-   Após a atualização de um site primário, os sites secundários não atualizam automaticamente. Em vez disso, tem de iniciar a atualização do site secundário.  

> [!NOTE]  
>  A versão de produção do System Center Configuration Manager (ramo atual), o ramo de manutenção de longo prazo e a pré-visualização técnica do System Center Configuration Manager são diferentes versões. Por conseguinte, as atualizações aplicáveis para um ramo não estão disponíveis como na consola atualizações para as outras ramificações. Para mais informações sobre ramos disponíveis, consulte o artigo [o ramo do Configuration Manager devo utilizar?](/sccm/core/understand/which-branch-should-i-use)

##  <a name="bkmk_outofband"></a> Correções fora de banda  
Algumas correções são lançadas com disponibilidade limitada no sentido de abordar problemas específicos, ou são aplicáveis a todos os clientes, não podendo, contudo, ser instaladas através do método na consola. Estas correções são fornecidas fora da banda e não são detetadas a partir do serviço Microsoft Cloud.  

Normalmente, conheça as correções de fora de banda a partir do suporte técnico da Microsoft, um artigo de Base de dados de conhecimento, ou o [blogue da equipa do System Center Configuration Manager](https://blogs.technet.microsoft.com/configmgrteam) quando procuram corrigir ou resolver um problema com a sua implementação do Configuration Manager.  

Pode instalar estas correções manualmente através de um destes dois métodos:  

-   **Ferramenta de atualização de registo:** Esta ferramenta importa manualmente a correção para a consola do Configuration Manager, onde pode, em seguida, instalar a atualização como que teria no-consola atualizações que são automaticamente detetadas. Este método é atualizado para atualizações que utilizem a seguinte estrutura de nome de ficheiro: **.update.exe**.  O nome de ficheiro completo para este tipo de correção é semelhante: **&lt;Produto\>-&lt;versão do produto\>-&lt;ID do artigo KB\>-ConfigMgr.Update.exe**.  

     Para obter mais informações, consulte o artigo [utilizar a ferramenta de registo de atualização para importar correções para o System Center Configuration Manager](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md).  

-   **Correção do instalador:** Esta ferramenta é utilizada para instalar manualmente uma correção que não pode ser instalada utilizando o método na consola. Este método é utilizado para correções que utilizam a seguinte estrutura de nome de ficheiro: **&lt;Product\>-&lt;product version\>-&lt;KB article ID\>-&lt;platform\>-&lt;language\>.exe**.

     Para obter mais informações, consulte o artigo [utilizar o instalador de correção para instalar atualizações para o System Center Configuration Manager](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md).

