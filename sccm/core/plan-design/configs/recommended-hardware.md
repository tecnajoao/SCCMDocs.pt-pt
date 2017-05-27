---
title: Recomendado hardware | Documentos do Microsoft
description: "Obter recomendações de hardware para o ajudar a dimensionar o ambiente do System Center Configuration Manager para além de uma implementação básica."
ms.custom: na
ms.date: 05/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5267f0af-34d3-47a0-9ab8-986c41276e6c
caps.latest.revision: 26
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 212628639300e9c361f7cee61b3df6b1cb6874ce
ms.openlocfilehash: 8dac6df60b07461d6410d305723b3f03fb09fa16
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="recommended-hardware-for-system-center-configuration-manager"></a>Hardware recomendado para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

As seguintes recomendações-se diretrizes para o ajudar a dimensionar o ambiente do System Center Configuration Manager para suportar mais do que uma implementação muito básica de sites, sistemas de sites e clientes. Estas recomendações não pretendem abranger todas as configurações de sites e hierarquias possíveis.  

 Utilize as informações nas secções seguintes como guia para ajudar a planear o hardware que pode satisfazer as cargas de processamento dos clientes e sites que utilizam as funcionalidades disponíveis do Configuration Manager com as configurações predefinidas.  


##  <a name="bkmk_ScaleSieSystems"></a>Sistemas de sites  
 Esta secção fornece configurações de hardware recomendadas para o Configuration Manager sistemas de sites para implementações que suportem o número máximo de clientes e utilizam a maior parte ou todas as funcionalidades do Configuration Manager. Implementações que suportam menor do que o número máximo de clientes e não utilizam todas as funcionalidades disponíveis poderão necessitar de menos recursos do computador. Em geral, os principais fatores que limitam o desempenho do sistema global incluem o seguinte, por ordem:  

1.  Desempenho da E/S do disco  

2.  Memória disponível  

3.  CPU  

Para melhor desempenho, utilize as configurações do RAID 10 para todas as unidades de dados e uma rede Ethernet de 1 Gbps.  

###  <a name="bkmk_ScaleSiteServer"></a>Servidores do site  

|Site primário autónomo|CPU (núcleos)|Memória (GB)|Alocação de memória para o SQL Server (%)|  
|-------------------------------|---------------|---------------|----------------------------------------|  
|Servidor de site primário autónomo com uma função de base de dados de sites no mesmo servidor<sup>1</sup>|16|96|80|  
|Servidor de site primário autónomo com base de dados de site remoto|8|16|-|  
|Servidor de base de dados remota para um site primário autónomo|16|72|90|  
|Servidor de site de administração central com uma função de base de dados de sites no mesmo servidor<sup>1</sup>|20|128|80|  
|Servidor de site de administração central com base de dados de site remoto|8|16|-|  
|Servidor de base de dados remota de um site de administração central|16|96|90|  
|Site primário subordinado com uma função de base de dados de sites no mesmo servidor|16|96|80|  
|Servidor de site primário subordinado com base de dados de site remoto|8|16|-|  
|Servidor de base de dados remota para um site primário subordinado|16|72|90|  
|Servidor do Site Secundário|8|16|-|  

 <sup>1</sup> quando o servidor do site e o SQL Server estão instalados no mesmo computador, a implementação suporte o máximo [números dimensionamento e a escala](/sccm/core/plan-design/configs/size-and-scale-numbers) dos sites e clientes. Mas, esta configuração pode limitar [opções de elevada disponibilidade para o System Center Configuration Manager](/sccm/protect/understand/high-availability-options), semelhante à utilização de um cluster do SQL Server. Além disso, devido aos requisitos de e/s superior que são necessários para suportar o SQL Server e o servidor do site do Configuration Manager ao executar ambos no mesmo computador, é boa ideia considere utilizar uma configuração com um computador do SQL Server remoto, se tiver uma implementação maior.  

###  <a name="bkmk_RemoteSiteSystem"></a>Servidores do sistema de sites remoto  
 As seguintes orientações for para computadores que possuem uma função de sistema de sites única. Planeie efetuar ajustes quando instalar várias funções de sistema de sites no mesmo computador.  

|Função do sistema de sites|CPU (núcleos)|Memória (GB)|Espaço em disco (GB)|  
|----------------------|---------------|---------------|--------------------|  
|Ponto de gestão|4|8|50|  
|Ponto de distribuição|2|8|Conforme requerido pelo sistema operativo e para armazenar o conteúdo que implementar|  
|Catálogo de Aplicações, com o serviço Web e o Web site no computador do sistema de sites|4|16|50|  
|Ponto de atualização de software<sup>1</sup>|8|16|Conforme requerido pelo sistema operativo e para armazenar as atualizações que implementar|  
|Todas as outras funções do sistema de sites|4|8|50|  

 <sup>1</sup> computador que aloja um ponto de atualização de software requer as seguintes configurações para agrupamentos de aplicações do IIS:  

-   Aumentar o **comprimento da fila WsusPool** para **2000**.  

-   Aumentar o **limite de memória WsusPool privada** por 4 vezes, ou defina-o como **0** (ilimitado).  

###  <a name="bkmk_DiskSpace"></a>Espaço em disco para sistemas de sites  
 Configuração e atribuição do disco contribuem para o desempenho do Configuration Manager. Uma vez que cada ambiente do Configuration Manager for diferente, os valores que implementar podem diferir das seguintes orientações.  

 Para obter o melhor desempenho, coloque cada objeto num volume RAID separado e dedicado. Para todos os volumes de dados (Configuration Manager e os respetivos ficheiros de base de dados), utilize o RAID 10 para obter o melhor desempenho.  

|Utilização de dados|Espaço mínimo em disco|25 000 clientes|50 000 clientes|100 000 clientes|150 000 clientes|700.000 clientes (site de administração central)|  
|----------------|------------------------|--------------------|--------------------|---------------------|---------------------|-----------------------------------------------------|  
|Sistema operativo|Consulte as orientações para o sistema operativo.|Consulte as orientações para o sistema operativo.|Consulte as orientações para o sistema operativo.|Consulte as orientações para o sistema operativo.|Consulte as orientações para o sistema operativo.|Consulte as orientações para o sistema operativo.|  
|Ficheiros de registo de aplicações e do Configuration Manager|25 GB|50 GB|100 GB|200 GB|300 GB|200 GB|  
|Ficheiro .mdf da base de dados do site|75 GB para cada 25.000 clientes|75 GB|150 GB|300 GB|500 GB|2 TB|  
|Ficheiro .ldf da base de dados do site|25 GB para cada 25 000 clientes|25 GB|50 GB|100 GB|150 GB|100 GB|  
|Ficheiros da base de dados temporária (.mdf e .ldf)|Conforme necessário|Conforme necessário|Conforme necessário|Conforme necessário|Conforme necessário|Conforme necessário|  
|Conteúdo (partilhas de ponto de distribuição)|Conforme necessário<sup>1</sup>|Conforme necessário<sup>1</sup>|Conforme necessário<sup>1</sup>|Conforme necessário<sup>1</sup>|Conforme necessário<sup>1</sup>|Conforme necessário<sup>1</sup>|  

 <sup>1</sup> as orientações de espaço em disco não incluem o espaço necessário para o conteúdo que esteja localizado numa biblioteca de conteúdos dos site servidor ou pontos de distribuição. Para obter informações sobre o planeamento da biblioteca de conteúdos, veja [A biblioteca de conteúdos](../../../core/plan-design/hierarchy/the-content-library.md).  

 Além das orientações anteriores, considere as seguintes diretrizes quando planear os requisitos de espaço em disco:  

-   Cada cliente necessita de cerca de 5 MB de espaço.  

-   Ao planear o tamanho da base de dados Temp para um site primário, planear um tamanho combinado que seja 25% a 30% do ficheiro. mdf da base de dados do site. O tamanho real pode ser significativamente inferior ou superior — depende do desempenho do servidor do site e o volume de dados recebidos durante curtos e longos períodos de tempo.  

    > [!NOTE]  
    >  Quando tiver 50.000 ou mais clientes num site, considere a utilização de quatro ou mais ficheiros. mdf da base de dados Temp.  

-   O tamanho da base de dados temporária de um site de administração central é normalmente inferior ao de um site primário.  

-   O tamanho da base de dados do site secundário é limitado ao seguinte:  

    -   SQL Server 2012 Express: 10 GB  

    -   Express do SQL Server 2014: 10 GB  

##  <a name="bkmk_ScaleClient"></a>Clientes  
 Esta secção fornece as configurações de hardware recomendadas para computadores que gere utilizando software de cliente do Configuration Manager.  

### <a name="client-for-windows-computers"></a>Cliente para computadores Windows  
 Seguem-se os requisitos mínimos para computadores baseados em Windows que pode gerir através do Configuration Manager, incluindo os sistemas operativos incorporados:  

-   **O processador e memória:** Consulte os requisitos de RAM para o sistema operativo do computador e processador.  

-   **Espaço em disco:** 500 MB de espaço disponível espaço em disco, com 5 GB recomendados para a cache do cliente do Configuration Manager. Menor espaço em disco é necessário se utilizar as definições personalizadas para instalar o cliente do Configuration Manager:  

    -   Utilize o /skipprereq de propriedade da linha de comandos do CCMSetup para evitar a instalação de ficheiros que o cliente não necessite. Por exemplo, executar **CCMSetup.exe /skipprereq:silverlight.exe** se o cliente não utilizar o catálogo de aplicações.  

    -   Utilize a propriedade SMSCACHESIZE do Client.msi para definir um ficheiro de cache que seja menor do que o predefinido de 5120 MB. O tamanho mínimo é de 1 MB. Por exemplo, o **CCMSetup.exe SMSCachesize=2** cria uma cache com um tamanho de 2 MB.  

    Para obter mais informações sobre estas definições de instalação do cliente, veja [Acerca das propriedades de instalação do cliente no System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

    > [!TIP]  
    >  Instalar o cliente com um espaço em disco mínimo é útil para os dispositivos Windows Embedded que, geralmente, têm um espaço em disco menor do que os computadores Windows padrão.  



 Seguem-se os requisitos mínimos de hardware adicionais para uma funcionalidade opcional no Configuration Manager.  

-   **Implementação do sistema operativo:** 384 MB de RAM  

-   **Centro de Software:** Processador a 500 MHz  

-   **Controlo remoto:** Pentium 4 Hyper-Threaded 3 GHz (único núcleo) ou CPU comparável, pelo menos, 1 GB de RAM para uma experiência ideal  

### <a name="client-for-linux-and-unix"></a>Cliente para Linux e UNIX  
 Seguem-se os requisitos mínimos para servidores Linux e UNIX que gere com o Configuration Manager.  

|Requisito|Detalhes|  
|-----------------|-------------|  
|Processador e memória|Consulte os requisitos de RAM para o sistema operativo do computador e processador.|  
|Espaço em disco|500 MB de espaço disponível espaço em disco, com 5 GB recomendados para a cache do cliente do Configuration Manager.|  
|Conectividade de rede|Computadores de cliente do Configuration Manager tem de ter conectividade de rede para sistemas de sites do Configuration Manager para ativar a gestão.|  

##  <a name="bkmk_ScaleConsole"></a>Consola do Configuration Manager  
 Os requisitos na tabela seguinte aplicam-se em cada computador que executa a consola do Configuration Manager.  

 **Configuração mínima de hardware:**  

-   Intel i3 ou CPU comparável  

-   2 GB de RAM  

-   2 GB de espaço em disco  

|Definição PPP|Resolução mínima|  
|-----------------|------------------------|  
|96/100%|1024 x 768|  
|120/125%|1280 x 960|  
|144/150%|1600 x 1200|  
|196/200%|2500 x 1600|  

 **Suporte para o PowerShell:**  

 Quando instala suporte para o PowerShell num computador que executa a consola do Configuration Manager, pode executar os cmdlets do PowerShell nesse computador para gerir o Configuration Manager.

 - É suportado o PowerShell 3.0 ou posterior

Para além do PowerShell, Windows Management Framework (WMF) versão 3.0 ou posterior é suportada.   


##  <a name="bkmk_ScaleLab"></a>Implementações de laboratório  
 Utilize as seguintes recomendações de hardware mínimo para as implementações de laboratório e teste do Configuration Manager. Estas recomendações aplicam-se a todos os tipos de site, até 100 clientes:  

|Função|CPU (núcleos)|Memória (GB)|Espaço em disco (GB)|  
|----------|---------------|-------------------|-----------------------|  
|Servidor do site e da base de dados|2 - 4|7 - 12|100|  
|Servidor do sistema de sites|1 - 4|2 - 4|50|  
|Cliente|1 - 2|1 - 3|30|  

