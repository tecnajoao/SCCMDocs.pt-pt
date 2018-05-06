---
title: Atualizações e Manutenção
titleSuffix: Configuration Manager
description: Saiba mais sobre um método de manutenção na consola denominado atualizações e manutenção que torna mais fácil localizar e instalar atualizações recomendadas.
ms.date: 05/01/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3a832943-580a-4a40-b454-961d0854ac2b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9c2a9d7c754e7a1a02527c4c985d1b9db6bc7d14
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="updates-for-system-center-configuration-manager"></a>Atualizações para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O Configuration Manager utiliza um método de manutenção na consola denominado **atualizações e manutenção**. Este método na consola torna mais fácil para localizar e instalar as atualizações para a sua infraestrutura do Configuration Manager recomendadas. Manutenção na consola é complementado por atualizações fora de banda, tais como correções que foram concebidas para os clientes que precisem de resolver problemas específicos ao seu respetivo ambiente.  

> [!TIP]  
> Os termos de licenciamento *atualizar*, *atualizar*, e *instalar* são utilizados para descrever três conceitos diferentes no Configuration Manager. Para obter mais informações sobre como cada termo é utilizado, consulte [sobre a atualização, atualização e instalação](/sccm/core/understand/upgrade-update-install).


 **Os tópicos seguintes podem ajudá-lo a compreender como encontrar e instalar os diferentes tipos de atualização para o Configuration Manager:**  

-   [Instalar atualizações na consola](../../../core/servers/manage/install-in-console-updates.md)  

-   [Utilizar a ferramenta de ligação de serviço](../../../core/servers/manage/use-the-service-connection-tool.md)  

-   [Utilize a ferramenta de registo de atualização para importar correções](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md)  

-   [Utilizar o instalador de correções para instalar atualizações](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md)  


Para obter mais informações sobre o ramo de pré-visualização técnica, consulte [pré-visualização técnica do System Center Configuration Manager](/sccm/core/get-started/technical-preview).



##  <a name="bkmk_Baselines"></a> Versões de linha de base e de atualização  

Utilize a versão de linha de base mais recente ao instalar um novo site numa nova hierarquia. 
- Também utilize uma versão de linha de base a atualização do System Center 2012 Configuration Manager.  

- Após atualizar para o ramo atual do Configuration Manager, não utilize versões de linha de base para se manter atual. Em vez disso, utilize apenas [atualizações na consola](/sccm/core/servers/manage/install-in-console-updates) para atualizar para a versão mais recente.  

- Periodicamente, são lançadas versões de linha de base adicionais. Quando utilizar a versão de linha de base mais recente para instalar uma nova hierarquia, evite instalar uma versão desatualizada ou não suportada do Configuration Manager, seguido de uma atualização adicional da sua infraestrutura para colocá-lo atualizado.  

Depois de instalar uma versão de linha de base, ficarão disponíveis versões adicionais do Configuration Manager como atualizações na consola. Nas atualizações da consola, atualize a sua infraestrutura para a versão mais recente do Configuration Manager.  

-   Instale atualizações na consola para atualizar a versão do seu site de nível superior.  

-   A instalação de atualizações a que instalar automaticamente o site de administração central em sites primários subordinados. Controla este temporização utilizando uma janela de manutenção no site primário.  

-   Atualize manualmente os sites secundários para uma nova versão de atualização da consola do.  

Quando instala uma atualização, a atualização armazena os ficheiros de instalação para essa versão no servidor do site numa pasta denominada **CD. Mais recente**. Para obter mais informações sobre estes ficheiros, consulte [o CD. Pasta mais recente](../../../core/servers/manage/the-cd.latest-folder.md).  

-   Utilize os ficheiros no CD. Pasta mais recente durante a recuperação de site. Além disso, quando a hierarquia já não executa uma versão de linha de base, utilize estes ficheiros para instalar sites adicionais.  

-   Não é possível utilizar os ficheiros de instalação a partir do CD. Mais recente para instalar o primeiro site numa nova hierarquia ou para atualizar um site do System Center 2012 Configuration Manager.  

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


*(Nota 1)*  o suporte de dados de linha de base de 1802 está disponível como parte das seguintes versões no [Centro de serviços de licenciamento de Volume](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) (VLSC):
- Gestor de configuração do System Center (ramo atual)
- O Centro de dados do System Center 2016
- System Center 2016 padrão por exemplo, pesquisar VLSC para `System Center Config Mgr (current branch)`. Determinar o suporte de dados de linha de base de 1802 na lista de ficheiros e transferir para essa versão.

Para verificar a versão do seu site do Configuration Manager, na consola, aceda a **sobre o System Center Configuration Manager** no canto superior esquerdo da consola. Esta caixa de diálogo apresenta as versões de consola e do site.  

 > [!Note]  
 > A partir de versão 1802, a versão da consola agora é ligeiramente diferente da versão do site. A versão secundária da consola agora corresponde à versão de lançamento do Configuration Manager. Por exemplo, no Configuration Manager versão 1802 a versão do site inicial é 5.0.8634.1000 e a versão da consola inicial é 5. **1802**.1082.1700. A compilação (1082) e números de revisão (1700) podem ser alteradas com correções futuras para a versão de 1802.



##  <a name="bkmk_inconsole"></a> Atualizações e manutenção na consola  
 Ao utilizar uma instalação de prontos para produção do ramo atual do Configuration Manager, a maioria das atualizações estão disponíveis utilizando o **atualizações e manutenção** canal. Este método identifica, transfere e disponibiliza-se de que as atualizações que se aplicam à sua versão de infraestrutura atual e a configuração. Inclui apenas as atualizações de que a Microsoft recomenda para todos os clientes.   

 Estas atualizações incluem:  

-   Novas versões, como versão 1702, 1706, 1710 ou 1802.  

-   Atualizações que incluem novas funcionalidades para a sua versão atual.

-   Correções para a sua versão do Configuration Manager e que todos os clientes devem instalar.

As atualizações na consola garantem uma maior estabilidade e resolvem problemas comuns. Estas atualizações vem substituir os tipos de atualização existentes para versões anteriores do produto, como os service packs, atualizações cumulativas, correções aplicáveis a todos os clientes e a extensão para Microsoft Intune. 

Podem aplicar as atualizações na consola para um ou mais dos seguintes sistemas:  

-   Servidores de sites primário e de administração central  

-   Funções de sistema de sites e servidores de sistema de sites  

-   Instâncias do Fornecedor de SMS  

-   Consolas do Configuration Manager  

-   Clientes do Configuration Manager  

O Configuration Manager Deteta novas atualizações. Sincronize o seu ponto de ligação de serviço do Configuration Manager com o serviço de nuvem da Microsoft, salientar comportamentos seguintes:  

-   Quando o ponto de ligação de serviço está no modo online, o seu site sincroniza com a Microsoft todos os dias. Identifica automaticamente novas atualizações que se aplicam à sua infraestrutura. Para transferir as atualizações e os ficheiros redistribuíveis, o computador que aloja a função de sistema de sites de ponto de ligação de serviço utiliza o **sistema** contexto para aceder a localizações de internet seguintes: go.microsoft.com e download.microsoft.com. Para obter mais informações sobre localizações adicionais utilizado pelo ponto de ligação de serviço, consulte [requisitos de acesso à Internet](../../../core/servers/deploy/configure/about-the-service-connection-point.md#bkmk_urls).  

-   Quando o ponto de ligação de serviço está no modo offline, utilize a ferramenta de ligação de serviço para sincronizar manualmente com a nuvem da Microsoft. Para obter mais informações, consulte [utilizar a ferramenta de ligação de serviço](../../../core/servers/manage/use-the-service-connection-tool.md).  

-   As atualizações na consola eliminam a necessidade de localizar e instalar atualizações individuais, service packs e novas funcionalidades de forma independente.  

-   Instale apenas as atualizações na consola que escolher. Quando instala algumas atualizações, pode selecionar as funcionalidades individuais para ativar e utilizar. Para obter mais informações, consulte [ativar funcionalidades opcionais de atualizações](../../../core/servers/manage/install-in-console-updates.md#bkmk_options).  

Quando instala uma atualização na consola, ocorre o seguinte processo:  

-   Esta executa automaticamente uma verificação de pré- requisitos. Pode executar também manualmente esta verificação antes de iniciar a instalação.  

-   Instala o site de nível superior no seu ambiente. Este site é o site de administração central, se tiver uma. Numa hierarquia, a atualização instala automaticamente em sites primários. Controlar quando cada servidor do site primário é permitido atualizar utilizando [windows para servidores de site do serviço](../../../core/servers/manage/service-windows.md).  

-   Depois de atualizações de um servidor de site, todas as funções de sistema de sites afetadas atualizar automaticamente. Estas funções incluem as instâncias do fornecedor de SMS. Depois do site instala a atualização, consolas do Configuration Manager também pedem ao utilizador da consola para atualizar a consola.  

-   Se uma atualização incluir o cliente do Configuration Manager, é-lhe dada a opção para testar a atualização em pré-produção ou por aplicar a atualização para todos os clientes imediatamente.  

-   Após a atualização de um site primário, os sites secundários não atualizam automaticamente. Em vez disso, tem de iniciar manualmente a atualização do site secundário.  

> [!NOTE]  
>  O ramo atual do Configuration Manager, o ramo de manutenção longo prazo e o ramo de pré-visualização técnica são versões diferentes. Por conseguinte, as atualizações aplicáveis para um ramo não estão disponíveis como atualizações na consola para os outros ramos. Para mais informações sobre ramos disponíveis, consulte [o ramo do Configuration Manager devo utilizar?](/sccm/core/understand/which-branch-should-i-use)



##  <a name="bkmk_outofband"></a> Correções fora de banda  
Algumas correções de versão com disponibilidade limitada para resolver problemas específicos. Outras correções são aplicáveis a todos os clientes, mas não é possível instalar utilizando o método na consola. Estas correções são fornecidas fora da banda e não são detetadas a partir do serviço Microsoft Cloud.  

Normalmente, quando necessita de corrigir ou abordar um problema com a sua implementação do Configuration Manager, pode saber sobre correções fora de banda do cliente suporte técnico da Microsoft, um suporte de dados de conhecimento base artigo da Microsoft, ou a partir de [ System Center Configuration Manager Team blog](https://blogs.technet.microsoft.com/configmgrteam). 

Instale estas correções manualmente, utilizando um dos seguintes dois métodos:  

-   **Atualizar a ferramenta de registo**: Esta ferramenta importa manualmente a correção para a consola do Configuration Manager. Em seguida, instale a atualização seria atualizações na consola que são detetadas automaticamente.  

    - Este método é utilizado para correções que utilizem a seguinte estrutura de nome de ficheiro:  
         `<Product>-<product version>-<KB article ID>-ConfigMgr.Update.exe`    

    - Para obter mais informações, consulte [utilizar a ferramenta de registo de atualização para importar correções](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md).  

-   **Instalador de correções**: Utilize esta ferramenta para instalar manualmente uma correção que não pode ser instalada através do método na consola.  

    - Este método é utilizado para correções que utilizem a seguinte estrutura de nome de ficheiro:   
         `<Product>-<product version>-<KB article ID>-<platform>-<language>.exe`  

    - Para obter mais informações, consulte [utilizar o instalador de correções para instalar atualizações](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md).  
