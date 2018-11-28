---
title: As atualizações e manutenção
titleSuffix: Configuration Manager
description: Saiba mais sobre o método de manutenção na consola denominado atualizações e manutenção que torna mais fácil de localizar e instalar atualizações recomendadas.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3a832943-580a-4a40-b454-961d0854ac2b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1acc1bd6a6ccbd010308d026933a371f9e8227d8
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52456554"
---
# <a name="updates-and-servicing-for-configuration-manager"></a>As atualizações e manutenção do Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O Configuration Manager utiliza um método de manutenção na consola denominado **atualizações e manutenção**. Esse método na consola torna mais fácil para localizar e instalar as atualizações para a sua infraestrutura do Configuration Manager recomendadas. A manutenção na consola é complementado por atualizações fora de banda, como correções. As atualizações fora de banda destinam-se para os clientes que precisem de resolver problemas específicos ao seu respetivo ambiente.  

> [!TIP]  
> Os termos *atualizar*, *atualizar*, e *instalar* são utilizados para descrever três conceitos diferentes no Configuration Manager. Para obter mais informações sobre como cada termo é usado, consulte [sobre a atualização, atualização e instalação](/sccm/core/understand/upgrade-update-install).  



##  <a name="bkmk_Baselines"></a> Versões de linha de base e de atualização  

Utilize a versão de linha de base mais recente ao instalar um novo site numa nova hierarquia. 
- Também utiliza uma versão de linha de base para atualizar a partir do System Center 2012 Configuration Manager.  

- Depois de atualizar para o Configuration Manager current branch, não utilize versões de linha de base para manter-se atualizado. Em alternativa, utilize apenas [atualizações na consola](/sccm/core/servers/manage/install-in-console-updates) para atualizar para a versão mais recente.  

- Periodicamente, são lançadas as versões de linha de base adicionais. Quando utiliza a versão de linha de base mais recente para instalar uma nova hierarquia, evitar a instalação de uma versão ultrapassada ou sem suporte do Configuration Manager, seguida por uma atualização adicional da sua infraestrutura para colocá-lo atualizado.  

Depois de instalar uma versão de linha de base, ficarão disponíveis versões adicionais do Configuration Manager como atualizações na consola. Nas atualizações da consola, atualize a sua infraestrutura para a versão mais recente do Configuration Manager.  

-   Instale atualizações na consola para atualizar a versão do seu site de nível superior.  

-   Instalar as atualizações que instalar automaticamente no site de administração central em sites primários subordinados. Controle este tempo com uma janela de manutenção no site primário.  

-   Atualize manualmente os sites secundários para uma nova versão de atualização de dentro da consola.  

Quando instala uma atualização, a atualização armazena os ficheiros de instalação para essa versão no servidor do site numa pasta chamada **CD. Mais recente**. Para obter mais informações sobre estes ficheiros, consulte [The CD. Pasta mais recente](/sccm/core/servers/manage/the-cd.latest-folder).  

-   Use os arquivos do CD. Pasta mais recente durante a recuperação de site. Além disso, quando a hierarquia já não é executada uma versão de linha de base, utilize estes ficheiros para instalar sites adicionais.  

-   Não é possível utilizar ficheiros de instalação a partir do CD. Versão mais recente para instalar o primeiro site numa nova hierarquia ou para atualizar um site do System Center 2012 Configuration Manager.  


### <a name="version-details"></a>Detalhes da versão

Algumas atualizações do Configuration Manager estão disponíveis tanto como versões de atualização na consola para uma infraestrutura existente, como novas versões de linha de base.  

#### <a name="supported-versions"></a>Versões suportadas
As seguintes versões suportadas do Configuration Manager estão atualmente disponíveis como uma linha de base, uma atualização ou ambas:  

| Versão | Data de disponibilidade | [Data de fim do suporte](/sccm/core/servers/manage/current-branch-versions-supported) | Linha de base | Atualização na consola |  
|-------------|-----------|------------|--------------|------------------------|  
| [1810](/sccm/core/plan-design/changes/whats-new-in-version-1810)<br /><br /> 5.00.8740.1000 | 27 de Novembro de 2018 | 27 de Maio de 2020 | Não | Sim |
| [1806](/sccm/core/plan-design/changes/whats-new-in-version-1806)<br /><br /> 5.00.8692.1000 | 31 de Julho de 2018 | 31 de Janeiro de 2020 | Não | Sim |
| [1802](/sccm/core/plan-design/changes/whats-new-in-version-1802)<br /><br /> 5.00.8634.1000 | 22 de Março de 2018 | 22 de Setembro de 2019 | Sim<sup>[observe 1](#bkmk_note1)</sup> | Sim |
| [1710](/sccm/core/plan-design/changes/whats-new-in-version-1710)<br /><br /> 5.00.8577.1000 | 20 de Novembro de 2017 | 20 de Maio de 2019 | Não | Sim |

<a name="bkmk_note1"></a> 

> [!Note]  
> <sup>**Nota 1:**</sup> O suporte de dados de linha de base de 1802 está disponível como parte das seguintes versões no [Centro de atendimento de licenciamento de Volume](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) (VLSC):
> - Gestor de configuração do System Center (ramo atual)
> - O Centro de dados do System Center 2016
> - Padrão do System Center 2016  
> 
> Por exemplo, procure o VLSC para `System Center Config Mgr (current branch)`. Localize o suporte de dados de linha de base de 1802 na lista de ficheiros e transferir para aquela versão.  

#### <a name="historical-versions"></a>Versões históricas
A tabela seguinte lista as versões do Configuration Manager current branch históricas que estão fora de suporte:

| Versão | Data de disponibilidade | Data de fim do suporte | Linha de base | Atualização na consola |  
|-------------|-----------|------------|--------------|------------------------|  
| 1706 <br /><br /> 5.00.8540.1000 | 31 de Julho de 2017 | 31 de Julho de 2018 | Não | Sim |
| 1702 <br /><br /> 5.00.8498.1000 | 27 de Março de 2017 | 27 de Março de 2018 | Sim | Sim |
| 1610 <br /><br /> 5.00.8458.1000 | 18 de Novembro de 2016 | 18 de Novembro de 2017 | Não | Sim |
| 1606 <br /><br /> 5.00.8412.1000 | 22 de Julho de 2016 | 22 de Julho de 2017 | Não | Sim |
| 1606 com o versão 1606 hotfix rollup (KB3186654) <br><br>5.00.8412.1307 | 12 de Outubro de 2016 | 12 de Outubro de 2017 | Sim | Não |
| 1602<br /><br /> 5.00.8355.1000 | 11 de Março de 2016 | 11 de Março de 2017 | Não | Sim |
| 1511 <br /><br /> 5.00.8325.1000 | 8 de Dezembro de 2015 | 8 de Dezembro de 2016 | Sim | Não |  

#### <a name="how-to-check-the-version"></a>Como verificar a versão
Para verificar a versão do seu site do Configuration Manager, além da consola, aceda a **sobre o System Center Configuration Manager** no canto superior esquerdo da consola. Esta caixa de diálogo mostra as versões de consola e do site.  

 > [!Note]  
 > A partir da versão 1802, a versão da consola agora é um pouco diferente da versão de site. A versão secundária da consola agora corresponde à versão de lançamento do Configuration Manager. Por exemplo, no Configuration Manager versão 1802 a versão do site inicial é 5.0.8634.1000 e a versão da consola inicial é 5. **1802**.1082.1700. A compilação (1082) e números de revisão (1700) podem ser alteradas com correções futuras, para a versão 1802.



##  <a name="bkmk_inconsole"></a> Atualizações e manutenção na consola  

Quando utiliza uma instalação de prontos para produção do Configuration Manager current branch, a maior parte das atualizações estão disponíveis através da **atualizações e manutenção** canal. Este método identifica, transfere e disponibiliza-se de que as atualizações que se aplicam à sua versão atual da infraestrutura e a configuração. Ele inclui apenas as atualizações que a Microsoft recomenda para todos os clientes.   

Estas atualizações incluem:  

-   Novas versões, como a versão 1802, 1806 ou 1810.  

-   Atualizações que incluem novas funcionalidades para a sua versão atual.

-   Correções para a sua versão do Configuration Manager e que todos os clientes devem instalar.

As atualizações na consola garantem uma maior estabilidade e resolvem problemas comuns. Estas atualizações vem substituir os tipos de atualização existentes para versões anteriores do produto, como pacotes de serviço, as atualizações cumulativas, correções que são aplicáveis a todos os clientes e a extensão do Microsoft Intune. 

As atualizações na consola, podem aplicar a um ou mais dos seguintes sistemas:  

-   Servidores de sites primário e de administração central  

-   Funções de sistema de sites e servidores de sistema de sites  

-   Instâncias do Fornecedor de SMS  

-   Consolas do Configuration Manager  

-   Clientes do Configuration Manager  

O Configuration Manager Deteta novas atualizações. Sincronize o ponto de ligação de serviço do Configuration Manager com o serviço de nuvem da Microsoft, observar os comportamentos seguintes:  

-   Quando o ponto de ligação de serviço está no modo online, o seu site sincroniza com a Microsoft todos os dias. Ele identifica automaticamente novas atualizações que se aplicam à sua infraestrutura. Para transferir as atualizações e os ficheiros redistribuíveis, o computador que aloja a função de sistema de sites de ponto de ligação de serviço utiliza a **sistema** contexto para aceder a localizações de internet seguintes: go.microsoft.com e download.microsoft.com. Para obter mais informações sobre localizações adicionais utilizado pelo ponto de ligação de serviço, consulte [requisitos de acesso de Internet](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_urls).  

-   Quando o ponto de ligação de serviço está no modo offline, utilize a ferramenta de ligação de serviço para sincronizar manualmente com a cloud da Microsoft. Para obter mais informações, consulte [utilizar a ferramenta de ligação de serviço](/sccm/core/servers/manage/use-the-service-connection-tool).  

-   As atualizações na consola eliminam a necessidade de localizar e instalar atualizações individuais, service packs e novas funcionalidades de forma independente.  

-   Instale apenas as atualizações na consola que escolher. Quando instala algumas atualizações, pode selecionar as funcionalidades individuais para ativar e utilizar. Para mais informações, consulte [Enable optional features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  

Quando instala uma atualização na consola, ocorre o seguinte processo:  

-   Esta executa automaticamente uma verificação de pré- requisitos. Pode executar também manualmente esta verificação antes de iniciar a instalação.  

-   Ele é instalado no site de nível superior no seu ambiente. Este site é o site de administração central, se tiver uma. Numa hierarquia, a atualização instala automaticamente em sites primários. Controlar quando cada servidor de site primário é permitida para atualizar usando [manutenção do windows para servidores de site](/sccm/core/servers/manage/service-windows).  

-   Após a atualização de um servidor de site, todas as funções de sistema de sites afetados são atualizados automaticamente. Estas funções incluem instâncias do fornecedor de SMS. Depois do site instala a atualização, consolas do Configuration Manager também pedir-lhe a consola para atualizar a consola.  

-   Se uma atualização inclui o cliente do Configuration Manager, são oferecidos a opção para testar a atualização em pré-produção ou para aplicar a atualização para todos os clientes imediatamente.  

-   Depois de um site primário é atualizado, os sites secundários não atualizam automaticamente. Em vez disso, tem de iniciar manualmente a atualização do site secundário.  

> [!NOTE]  
>  O Configuration Manager current branch, Long term servicing branch e o ramo de pré-visualização técnica são versões diferentes. Por conseguinte, as atualizações aplicáveis para um ramo não estão disponíveis como atualizações na consola para os outros ramos. Para obter mais informações sobre ramos disponíveis, consulte [o ramo do Configuration Manager devo utilizar?](/sccm/core/understand/which-branch-should-i-use)



##  <a name="bkmk_outofband"></a> Correções fora de banda  

Algumas correções lançados com disponibilidade limitada para resolver problemas específicos. Outras correções são aplicáveis a todos os clientes, mas não é possível instalar usando o método na consola. Estas correções são fornecidas fora da banda e não são detetadas a partir do serviço Microsoft Cloud.  

Normalmente, quando está procurando corrigir ou abordar um problema com a sua implementação do Configuration Manager, pode obter informações sobre correções fora de banda dos serviços de suporte de cliente do Microsoft, um artigo da base de dados de conhecimento de suporte do Microsoft, ou [mensagens da a equipe do System Center Configuration Manager](https://cloudblogs.microsoft.com/enterprisemobility/?product=system-center-configuration-manager) sobre o Enterprise Mobility + Security blog. 

Instale estas correções manualmente, utilizando um dos seguintes dois métodos:  

#### <a name="update-registration-tool"></a>Ferramenta de registo de atualização
Esta ferramenta importa manualmente a correção para a consola do Configuration Manager. Em seguida, instale a atualização, como faria atualizações na consola detetadas automaticamente.  

Este método é utilizado para correções que utilizem a seguinte estrutura de nome de ficheiro:  
  `<Product>-<product version>-<KB article ID>-ConfigMgr.Update.exe`    

Para obter mais informações, consulte [utilizar a ferramenta de registo de atualização para importar correções](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes).  

#### <a name="hotfix-installer"></a>Instalador de correções
Utilize esta ferramenta para instalar manualmente uma correção que não pode ser instalada através do método na consola.  

Este método é utilizado para correções que utilizem a seguinte estrutura de nome de ficheiro:   
   `<Product>-<product version>-<KB article ID>-<platform>-<language>.exe`  

Para obter mais informações, consulte [utilizar o instalador de correções para instalar atualizações](/sccm/core/servers/manage/use-the-hotfix-installer-to-install-updates).  



## <a name="next-steps"></a>Passos seguintes

Os artigos seguintes podem ajudá-lo a compreender como encontrar e instalar os diferentes tipos de atualização para o Configuration Manager:  

-   [Instalar atualizações na consola](/sccm/core/servers/manage/install-in-console-updates)  

-   [Utilizar a ferramenta de ligação de serviço](/sccm/core/servers/manage/use-the-service-connection-tool)  

-   [Utilizar a ferramenta de registo de atualização para importar correções](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes)  

-   [Utilizar o instalador de correções para instalar atualizações](/sccm/core/servers/manage/use-the-hotfix-installer-to-install-updates)  


Para obter mais informações sobre o ramo de pré-visualização técnica, veja [pré-visualização técnica](/sccm/core/get-started/technical-preview).
