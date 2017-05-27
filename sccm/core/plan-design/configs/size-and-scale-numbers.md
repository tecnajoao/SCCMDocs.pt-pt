---
title: Tamanho e a escala | Documentos do Microsoft
description: "Identifique o número de funções do sistema de sites e sites que terá de suportar os dispositivos no seu ambiente do System Center Configuration Manager."
ms.custom: na
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c5a42100-2f60-4952-b495-918025ea6559
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: f9c43e26758d5171a6ef56e827b4b054ebc8a5e5
ms.openlocfilehash: c7ad33339e65e6e00e88f98d6e13baceb98dae77
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="size-and-scale-numbers-for-system-center-configuration-manager"></a>Tamanho e a escala números para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*



Cada implementação do System Center Configuration Manager irá ter um número máximo de sites, funções do sistema de sites e dispositivos que pode suportar. Estes números variam consoante a estrutura de hierarquia (que tipos e o número de sites utiliza) e as funções de sistema de sites que implementar.  As informações nas seguintes áreas podem ajudar a identificar o número de funções do sistema de sites e sites que irá precisar para suportar os dispositivos que pretende gerir com o seu ambiente.

Utilize as informações deste tópico em conjunto com as informações nos seguintes artigos:
-   [Hardware recomendado](../../../core/plan-design/configs/recommended-hardware.md)
-   [Sistemas operativos suportados para servidores do sistema de sites](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  
-   [Sistemas operativos suportados para os clientes e dispositivos](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)
-   [Site e os pré-requisitos de sistema de sites](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)


Os seguintes números de suporte baseiam-se sobre como utilizar o hardware recomendado para o Configuration Manager e as predefinições para todas as funcionalidades disponíveis do Configuration Manager. Quando não utilizar o hardware recomendado, ou utilize definições personalizadas mais intensiva (como executar software de inventário de hardware ou com mais frequência do que as predefinições de uma vez a cada sete dias), o desempenho dos sistemas de sites pode ser degradado e pode não cumprir os níveis declarados de suporte.

##  <a name="bkmk_SiteSystemScale"></a>Tipos de site  
 **Site de administração central:**  

-   Um site de administração central suporta até 25 sites subordinados principais.  

**Site primário:**  

-   Cada site primário suportar até cerca de 250 sites secundários.  

-   O número de sites secundários por site primário baseia-se em ligações de rede (WAN) de área alargada continuamente ligado e fiável. Para localizações que têm menos de 500 clientes, considere um ponto de distribuição em vez de um site secundário.  

 Para obter informações sobre o número de clientes e dispositivos que um site primário pode suportar, consulte o artigo [números do cliente para sites e hierarquias](#bkmk_clientnumbers) neste tópico.  

**Site secundário:**  

-   Os sites secundários não suportam sites subordinados.  

-   Um site de administração central suporta até 25 sites subordinados principais.  

**Ponto de Web site do catálogo de aplicações:**  

-   Pode instalar várias instâncias do ponto de Web site do catálogo de aplicações em sites primários.  

    > [!TIP]  
    >  Como melhor prática, instale o ponto de Web site do catálogo de aplicações e o ponto de serviço web do catálogo de aplicações em conjunto no mesmo sistema do site quando que fornecem serviços a clientes que estão na intranet.  

    -   Para um melhor desempenho, planeie suportar até 50.000 clientes por instância.  

    -   Cada instância desta função de sistema de sites suporta o número máximo de clientes que são suportados pela hierarquia.  

## <a name="bkmk_roles"></a>Funções do sistema de sites    

**Ponto de serviço de web de catálogo de aplicações:**  

-   Pode instalar várias instâncias do ponto de serviço do catálogo de aplicações web em sites primários.  

    > [!TIP]  
    >  Como melhor prática, instale o ponto de Web site do catálogo de aplicações e o ponto de serviço web do catálogo de aplicações em conjunto no mesmo sistema do site quando que fornecem serviços a clientes que estão na intranet.  

    -   Para um melhor desempenho, planeie suportar até 50.000 clientes por instância.  

    -   Cada instância desta função de sistema de sites suporta o número máximo de clientes que são suportados pela hierarquia.  

**Ponto de distribuição:**  

-   Pontos de distribuição por site:  

    -   Cada site primário e secundário suporta até cerca de 250 pontos de distribuição.  

    -   Cada site primário e secundário suporta até 2000 pontos de distribuição adicionais que estão configurados como pontos de distribuição de solicitação. **Por exemplo**, um único site primário suporta 2250 pontos de distribuição quando 2000 desses pontos de distribuição são configurados como pontos de distribuição de solicitação.  

    -   Cada ponto de distribuição suporta ligações a partir de clientes até 4.000.  

    -   Um ponto de distribuição de solicitação é funciona como um cliente quando acede a conteúdo de um ponto de distribuição de origem.  

-   Cada site primário suporta um total combinado de até 5000 pontos de distribuição. Este total inclui todos os pontos de distribuição no site primário e todos os pontos de distribuição que pertencem aos sites secundários subordinados do site primário.  

-   Cada ponto de distribuição suporta um total combinado de até 10.000 pacotes e aplicações.  

> [!WARNING]  
>  O número real de clientes que pode suportar um ponto de distribuição depende da velocidade da rede e a configuração de hardware do computador do ponto de distribuição.  
>   
>  O número de pontos de distribuição de solicitação que pode suportar um ponto de distribuição de origem do mesmo modo depende da velocidade da rede e a configuração de hardware do computador de ponto de distribuição de origem. Mas este número também é afetado pela quantidade de conteúdo que tenha implementado. Isto acontece porque, ao contrário dos clientes que normalmente aceder ao conteúdo em diferentes momentos durante uma implementação, todos os pontos de distribuição de solicitação pedirem de conteúdo ao mesmo tempo — e poderá solicitá todos os conteúdos disponíveis, não apenas o conteúdo que é aplicável aos mesmos, como faria com um cliente. Quando demasiado uma carga de processamento é colocada num ponto de distribuição de origem, poderá haver atrasos inesperados na distribuição de conteúdo aos pontos de distribuição esperado no seu ambiente.  


**Ponto de estado de contingência:**  

-   Cada ponto de estado de contingência pode suportar até 100.000 clientes.  

**Ponto de gestão:**  

-   Cada site primário suportar até 15 pontos de gestão.  

    > [!TIP]  
    >  Não instale pontos de gestão em servidores que são através de uma ligação lenta a partir do servidor do site primário ou do servidor de base de dados do site.  

-   Cada site secundário suporta um único ponto de gestão que tem de estar instalado no servidor do site secundário.  

 Para obter informações sobre o número de clientes e dispositivos que um ponto de gestão pode suportar, consulte o [pontos de gestão](#bkmk_mp) deste tópico.  

**Ponto de atualização de software:**  

-   Um ponto de atualização de software que está instalado no servidor do site pode suportar até 25.000 clientes.  

-   Um ponto de atualização de software que seja remoto relativamente ao servidor do site pode suportar até 150,000 clientes quando o computador remoto cumpre os requisitos do Windows Server Update Services (WSUS) para suportar este número de clientes.  

-   Por predefinição, o Configuration Manager não suporta configurar pontos de atualização de software como clusters de balanceamento de carga na rede (NLB). No entanto, pode utilizar o SDK do Configuration Manager para configurar até quatro pontos de atualização de software num NLB cluster.  

##  <a name="bkmk_clientnumbers"></a>Números de cliente para sites e hierarquias  
 Utilize as seguintes informações para determinar o número de clientes e quais os tipos de clientes pode suportar um site ou de uma hierarquia.  

###  <a name="bkmk_cas"></a>Hierarquia com um site de administração central  
Um site de administração central suporta um número total de dispositivos que inclui até ao número de dispositivos listados para os seguintes três grupos:  

-   700.000 ambientes de trabalho (computadores que executam o Windows, Linux e UNIX)  

-   25.000 dispositivos que executam o Mac e o Windows CE 7.0  

-   Um dos seguintes, dependendo do modo como a implementação suporta a gestão de dispositivos móveis (MDM):  

    -   100000 dispositivos que gere utilizando MDM no local  

    -   300,000 dispositivos baseados em nuvem  

 Por exemplo, numa hierarquia, pode suportar computadores de 700.000 secretária, até 25.000 Mac e o Windows CE 7.0 e no máximo 300,000 dispositivos baseados em nuvem quando integrar o Microsoft Intune — para um total de 1,025,000 dispositivos. Se tiver suporte para dispositivos que são geridos pela MDM no local, o total para a hierarquia é 825,000 dispositivos.  

> [!IMPORTANT]  
>  Numa hierarquia onde o site de administração central utilizará uma edição Standard do SQL Server, a hierarquia suporta um máximo de 50000 computadores de secretária e dispositivos. A edição do SQL Server que está a ser utilizado num site primário autónomo não limita a capacidade desse site para suportar até ao número declarado de clientes.  


###  <a name="bkmk_chipri"></a>Site primário subordinado  
Cada site primário subordinado numa hierarquia com um site de administração central suporta o seguinte:  

-   150,000 total de clientes e dispositivos que não estão limitados a um grupo específico ou o tipo, desde que o suporte não excede o número que é suportado para a hierarquia.  

Por exemplo, um site primário que suporta 25.000 computadores que executem Mac e Windows CE 7.0 (uma vez que é o limite para uma hierarquia), em seguida, pode suportar um computadores de secretária 125,000 adicionais. Isto apresenta o número total de dispositivos suportados até o limite máximo suportado de 150,000 o subordinado do site primário.

###  <a name="bkmk_pri"></a>Site primário autónomo  
Um site primário autónomo suporta o seguinte número de dispositivos:  

-   175,000 total de clientes e dispositivos, não exceder:  

    -   150,000 ambientes de trabalho (computadores que executam o Windows, Linux e UNIX)  

    -   25.000 dispositivos que executam o Mac e o Windows CE 7.0

    -   Um dos seguintes, dependendo do modo como a implementação suporta a gestão de dispositivos móveis:  

        -   50.000 dispositivos que gere utilizando MDM no local  

        -   150,000 dispositivos baseados em nuvem  

Por exemplo, um site primário autónomo que suporte 150,000 computadores de secretária e Mac 10000 ou o Windows CE 7.0 suportam apenas um adicionais 15000 os dispositivos. Os dispositivos podem ser baseado na nuvem ou geridos através da utilização de MDM no local.  

###  <a name="bkmk_sec"></a>Sites secundários  
Os sites secundários suportam o seguinte:  

-   15000 ambientes de trabalho (computadores que executam o Windows, Linux e UNIX)  

###  <a name="bkmk_mp"></a>Pontos de gestão  
Cada ponto de gestão pode suportar o seguinte número de dispositivos:  

-   25.000 total de clientes e dispositivos, não exceder:  

    -   25.000 computadores de secretária (computadores que executam o Windows, Linux e UNIX)  

    -   Um dos seguintes (não ambos):  

        -   10.000 dispositivos que são geridos através da utilização de MDM no local  

        -   10.000 dispositivos que executam os clientes Mac e o Windows CE 7.0

