---
title: Tamanho e escala
titleSuffix: Configuration Manager
description: Determine o número de funções do sistema de sites e sites que precisará para suportar os dispositivos no seu ambiente.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c5a42100-2f60-4952-b495-918025ea6559
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4e1ee76acca06534605e58fff27d2e7ec5e464dd
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53424719"
---
# <a name="size-and-scale-numbers-for-system-center-configuration-manager"></a>Tamanho e números da escala para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*



Cada implementação no Configuration Manager tem um número máximo de sites, funções de sistema de sites e dispositivos que pode suportar. Esses números variam consoante a estrutura de hierarquia, que tipos e números de sites, utilização e as funções de sistema de sites que implementar. As informações neste artigo podem ajudá-lo a determinar o número de funções do sistema de sites e sites que precisa para suportar os dispositivos que pretende gerir.

Utilize as informações neste tópico juntamente com as informações nos seguintes artigos:
-   [Hardware recomendado](../../../core/plan-design/configs/recommended-hardware.md)
-   [Sistemas operativos suportados para servidores do sistema de sites](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  
-   [Sistemas operativos suportados por clientes e dispositivos](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)
-   [Pré-requisitos do site e sistema de sites](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)


Esses números baseiam-se sobre como utilizar o hardware recomendado para o Configuration Manager de suporte. Também são baseadas nas predefinições para todas as funcionalidades disponíveis do Configuration Manager. Quando não utiliza o hardware recomendado ou utilizar definições personalizadas mais agressivas, pode degradar o desempenho dos sistemas de sites. Os sistemas de site poderão não cumprir os níveis declarados de suporte. (Um exemplo de definições de cliente mais agressivos está em execução inventário de hardware ou software com mais frequência do que os padrões de uma vez a cada sete dias.)

##  <a name="bkmk_SiteSystemScale"></a> Tipos de site  

### <a name="central-administration-site"></a>Site de administração central  

-   Um site de administração central suporta até 25 sites primários subordinados.  


### <a name="primary-site"></a>Site primário  

- Cada site primário suporta até 250 sites secundários.  

- O número de sites secundários por site primário é baseado em ligações de rede (WAN) continuamente estabelecidas e fiáveis alargada. Para localizações com menos de 500 clientes, considere um ponto de distribuição em vez de um site secundário.  

  Para obter informações sobre o número de clientes e dispositivos que um site primário pode suportar, consulte [números de clientes para sites e hierarquias](#bkmk_clientnumbers).  


### <a name="secondary-site"></a>Site Secundário  

-   Os sites secundários não suportam sites subordinados.  



## <a name="bkmk_roles"></a> Site system roles    


### <a name="application-catalog-web-service-point"></a>Ponto de serviço Web do Catálogo de Aplicações  

-   Pode instalar várias instâncias do ponto de serviço do catálogo de aplicações web em sites primários.  

    > [!TIP]  
    >  Como melhor prática, instale o ponto de Web sites do catálogo de aplicações e ponto de serviço web do catálogo de aplicações em conjunto no mesmo sistema de sites quando fornecerem serviço aos clientes que estão na intranet.  

    -   Para um melhor desempenho, planeie oferecer suporte a até 50 000 clientes por instância.  

    -   Cada instância desta função de sistema de sites suporta o número máximo de clientes que são suportados pela hierarquia.  


### <a name="application-catalog-website-point"></a>Ponto de site do Catálogo de Aplicações  

-   Pode instalar várias instâncias do ponto de Web sites do catálogo de aplicações nos sites primários.  

    > [!TIP]  
    >  Como melhor prática, instale o ponto de Web sites do catálogo de aplicações e ponto de serviço web do catálogo de aplicações em conjunto no mesmo sistema de sites quando fornecerem serviço aos clientes que estão na intranet.  

    -   Para um melhor desempenho, planeie oferecer suporte a até 50 000 clientes por instância.  

    -   Cada instância desta função de sistema de sites suporta o número máximo de clientes que são suportados pela hierarquia.  


### <a name="bkmk_cmg"></a> Gateway de gestão na cloud

- Pode instalar várias instâncias do gateway de gestão na cloud (CMG) em sites primários ou o site de administração central.  

    > [!Tip]  
    > Numa hierarquia, crie CMG no site de administração central.  

    - Um CMG suporta instâncias de máquina virtual (VM) de um-para-16 no serviço cloud do Azure.  

    - Cada instância de VM de CMG suporta 6.000 conexões de cliente. Quando o CMG está sob carga elevada devido a mais do que o número suportado de clientes, processa pedidos ainda, mas poderá haver atraso.  

Para obter mais informações, consulte CMG [desempenho e dimensionamento](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#performance-and-scale)


### <a name="cloud-management-gateway-connection-point"></a>Ponto de ligação de gateway de gestão na cloud

- Pode instalar várias instâncias do ponto de ligação CMG em sites primários.  

- Um ponto de ligação do CMG pode suportar um CMG com até quatro instâncias de VM. Se o CMG tiver mais de quatro instâncias VM, adicione um segundo ponto de ligação CMG para balanceamento de carga. Um CMG com 16 instâncias de VM deve ser ligado com quatro pontos de ligação do CMG.

Para obter mais informações, consulte CMG [desempenho e dimensionamento](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#performance-and-scale)


### <a name="distribution-point"></a>Ponto de distribuição  

-   Pontos de distribuição por site:  

    -   Cada site primário e secundário suporta até 250 pontos de distribuição.  

    -   Cada site primário e secundário suporta até 2000 pontos de distribuição adicionais configurados como pontos de distribuição de extração. **Por exemplo**, um único site primário suporta 2250 pontos de distribuição quando 2000 desses pontos de distribuição são configurados como pontos de distribuição de extração.  

    -   Cada ponto de distribuição suporta ligações de até 4 000 clientes.  

    -   Um ponto de distribuição de extração funciona como um cliente quando acede a conteúdo de um ponto de distribuição de origem.  

-   Cada site primário suporta um total combinado de até 5 000 pontos de distribuição. Este total inclui todos os pontos de distribuição no site primário e todos os pontos de distribuição que pertencem a sites secundários subordinados do site primário.  

-   Cada ponto de distribuição suporta um total combinado de até 10 000 pacotes e aplicações.  

> [!WARNING]  
>  O número real de clientes que um ponto de distribuição consegue suportar depende da velocidade da rede e a configuração de hardware do servidor.  
>   
>  O número de pontos de distribuição de extração que um ponto de distribuição de origem consegue suportar depende da mesma forma a velocidade da rede e a configuração de hardware do ponto de distribuição de origem. Mas este número também é afetado pela quantidade de conteúdo que tenha implementado. Esse efeito é porque, ao contrário dos clientes que geralmente acedem ao conteúdo em momentos diferentes durante uma implantação, todos os pontos de distribuição de extração pedem conteúdo, ao mesmo tempo. Pontos de distribuição de extração podem solicitar todos os conteúdos disponíveis, não apenas o conteúdo que se aplicam aos mesmos. Quando coloca uma elevada carga de processamento num ponto de distribuição de origem, poderá haver atrasos inesperados na distribuição de conteúdos para os pontos de distribuição de destino.  


### <a name="fallback-status-point"></a>Ponto de estado de contingência  

-   Cada ponto de estado de contingência pode suportar até 100.000 clientes.  


### <a name="management-point"></a>Ponto de gestão  

- Cada site primário suporta até 15 pontos de gestão.  

  > [!TIP]  
  >  Não instale pontos de gestão em servidores que estão numa ligação lenta do servidor do site primário ou servidor de base de dados do site.  

- Cada site secundário suporta um único ponto de gestão que tem de estar instalado no servidor do site secundário.  

  Para obter informações sobre o número de clientes e dispositivos que um ponto de gestão pode suportar, consulte a [pontos de gestão](#bkmk_mp) secção.  


### <a name="software-update-point"></a>Ponto de atualização de software  

-   Um ponto de atualização de software que está instalado no servidor do site pode suportar até 25.000 clientes.   

-   Um ponto de atualização de software que seja remoto do servidor do site consegue suportar até 150.000 clientes, quando o computador remoto cumpre os requisitos do Windows Server Update Services (WSUS) para suportar este número de clientes.  



##  <a name="bkmk_clientnumbers"></a> Números de clientes para sites e hierarquias  
 Utilize as seguintes informações para determinar o número de clientes e os tipos de clientes pode suportar num site ou hierarquia.  


###  <a name="bkmk_cas"></a> Hierarquia com um site de administração central  
Um site de administração central suporta um número total de dispositivos que inclui até ao número de dispositivos listados para os seguintes três grupos:  

- 700.000 ambientes de trabalho (computadores que executam o Windows, Linux e UNIX). Consulte também, suporte para [dispositivos embedded](#embedded).

- 25 000 dispositivos que executam o Mac e Windows CE 7.0  

- Um dos seguintes, dependendo de como a implementação suporta a gestão de dispositivos móveis (MDM):  

  -   100 000 dispositivos que gere com MDM no local  

  -   300.000 dispositivos baseados na nuvem  

  Por exemplo, numa hierarquia pode suportar 700.000 ambientes de trabalho, até 25 000 dispositivos Mac e Windows CE 7.0 e até 300.000 dispositivos baseados na nuvem quando integra o Microsoft Intune. Esta hierarquia suporta um número total de 1.025.000 dispositivos. Se tiver suporte para dispositivos geridos por MDM no local, o total para esta hierarquia é 825.000 dispositivos.  

> [!IMPORTANT]  
>  Numa hierarquia onde o site de administração central utiliza uma edição Standard do SQL Server, a hierarquia suporta um máximo de 50 000 computadores de secretária e dispositivos. Para suportar mais de 50 000 computadores de secretária e dispositivos, tem de utilizar uma edição Enterprise do SQL Server. Este requisito aplica-se apenas a um site de administração central. Não se aplica a um site primário autónomo ou um site primário subordinado. A edição do SQL Server que utiliza para um site primário não limita a capacidade para oferecer suporte ao número declarado de clientes.   


 A edição do SQL Server que está a ser utilizado num site primário autónomo não limita a capacidade desse site para suportar até ao número declarado de clientes.  


###  <a name="bkmk_chipri"></a> Site primário subordinado  
Cada site primário subordinado numa hierarquia com um site de administração central suporta o seguinte número de clientes:  

-   150.000 total de clientes e dispositivos que não estão limitados a um grupo específico ou tipo, desde que o suporte não excede o número que é suportado para a hierarquia. Consulte também, suporte para [dispositivos embedded](#embedded).

Por exemplo, um site primário suporta 25 000 dispositivos Mac e Windows CE 7.0. Se o número é o limite para uma hierarquia. Este site primário, em seguida, pode suportar um computadores de secretária 125,000 adicionais. O número total de dispositivos suportados para o site primário subordinado é o limite máximo suportado de 150 000.


###  <a name="bkmk_pri"></a> Site primário autónomo  
Um site primário autónomo suporta o seguinte número de dispositivos:  

-   175.000 total de clientes e dispositivos, não deve exceder:  

    -   150.000 ambientes de trabalho (computadores que executam o Windows, Linux e UNIX). Consulte também, suporte para [dispositivos embedded](#embedded).

    -   25 000 dispositivos que executam o Mac e Windows CE 7.0

    -   Um dos seguintes, dependendo de como a implementação suporta a gestão de dispositivos móveis:  

        -   50 000 dispositivos que gere com MDM no local  

        -   150.000 dispositivos baseados na nuvem  


Por exemplo, um site primário autónomo que suporte 150,000 ambientes de trabalho e 10.000 Mac ou Windows CE 7.0 pode suportar apenas 15.000 dispositivos adicionais. Esses dispositivos podem ser baseados na nuvem ou geridos através de MDM no local.  


### <a name="embedded"></a> Sites primários e de dispositivos Windows Embedded
Os sites primários suportam dispositivos Windows Embedded que tenham baseados em ficheiros filtros de escrita (FBWF) ativados. Quando os dispositivos embedded não têm filtros de escrita ativados, um site primário pode suportar um número de dispositivos incorporados até o número permitido de dispositivos para esse site. O número total de dispositivos que um site primário suporta, um máximo de 10 000 destes dispositivos pode ser Windows Embedded. Estes dispositivos devem ser configurados para as exceções listadas na nota importante encontrada no [planejar a implantação de cliente em dispositivos Windows Embedded](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices). Um site primário suporta apenas 3 000 dispositivos Windows Embedded que tenham o EWF ativado e que não estejam configurados para as exceções.


###  <a name="bkmk_sec"></a> Sites secundários  
Os sites secundários suportam o seguinte número de dispositivos:  

-   15.000 ambientes de trabalho (computadores que executam o Windows, Linux e UNIX)  


###  <a name="bkmk_mp"></a> Pontos de gestão  
Cada ponto de gestão pode suportar o seguinte número de dispositivos:  

-   25.000 total de clientes e dispositivos, não deve exceder:  

    -   25.000 ambientes de trabalho (computadores que executam o Windows, Linux e UNIX)  

    -   Um dos seguintes (não ambos):  

        -   10 000 dispositivos que são geridos com MDM no local  

        -   10.000 dispositivos que executam os clientes Mac e Windows CE 7.0
