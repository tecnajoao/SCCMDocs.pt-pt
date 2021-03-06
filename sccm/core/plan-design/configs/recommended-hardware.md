---
title: Hardware recomendado
titleSuffix: Configuration Manager
description: Obtenha recomendações de hardware para o ajudar a dimensionar o seu ambiente do System Center Configuration Manager para além de uma implementação básica.
ms.date: 05/23/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5267f0af-34d3-47a0-9ab8-986c41276e6c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b773696d5967d9ed1779ee822168d7177f10f585
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56130450"
---
# <a name="recommended-hardware-for-system-center-configuration-manager"></a>Hardware recomendado para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

As seguintes recomendações são diretrizes para o ajudar a dimensionar o seu ambiente do System Center Configuration Manager para suportar mais do que uma implementação muito básica de sites, sistemas de sites e clientes. Estas recomendações não pretendem abranger todas as configurações de sites e hierarquias possíveis.  

 Utilize as informações nas secções seguintes como guia para ajudar a planear de hardware que pode satisfazer as cargas de processamento dos clientes e sites que utilizam as funcionalidades disponíveis do Configuration Manager com as configurações predefinidas.  



##  <a name="bkmk_ScaleSieSystems"></a> Sistemas de sites  
 Esta seção fornece configurações de hardware recomendadas para o Configuration Manager sistemas de sites para implementações que suportam o número máximo de clientes e utilizam a maioria ou todos os recursos do Configuration Manager. Implementações que suportam menos do que o número máximo de clientes e não utilizem todas as funcionalidades disponíveis podem requerer menos recursos informáticos. Em geral, os principais fatores que limitam o desempenho do sistema global incluem o seguinte, por ordem:  

1.  Desempenho da E/S do disco  

2.  Memória disponível  

3.  CPU  

Para obter melhor desempenho, utilize as configurações do RAID 10 para todas as unidades de dados e uma rede de Ethernet de 1 Gbps.  

###  <a name="bkmk_ScaleSiteServer"></a> Servidores de site  

|Configuração do site|CPU (núcleos)|Memória (GB)|Alocação de memória para o SQL Server (%)|  
|-------------------------------|---------------|---------------|----------------------------------------|  
|Servidor de site primário autónomo com uma função de site de base de dados no mesmo servidor<sup>1</sup>|16|96|80|  
|Servidor de site primário autónomo com base de dados de site remoto|8|16|-|  
|Servidor de base de dados remota para um site primário autónomo|16|72|90|  
|Servidor de site de administração central com uma função de site de base de dados no mesmo servidor<sup>1</sup>|20|128|80|  
|Servidor de site de administração central com base de dados de site remoto|8|16|-|  
|Servidor de base de dados remota de um site de administração central|16|96|90|  
|Site primário subordinado com uma função de site de base de dados no mesmo servidor|16|96|80|  
|Servidor de site primário subordinado com base de dados de site remoto|8|16|-|  
|Servidor de base de dados remota para um site primário subordinado|16|72|90|  
|Servidor do Site Secundário|8|16|-|  

 <sup>1</sup> quando o servidor do site e o SQL Server estão instalados no mesmo computador, a implementação suporta o máximo [dimensionamento e números da escala](/sccm/core/plan-design/configs/size-and-scale-numbers) por sites e clientes. No entanto, esta configuração pode limitar [opções de elevada disponibilidade para o System Center Configuration Manager](/sccm/protect/understand/high-availability-options), semelhante à utilização de um cluster do SQL Server. Além disso, devido os requisitos de e/s superior que são necessários para suportar o SQL Server e o servidor de site do Configuration Manager ao executar ambos no mesmo computador, ele é uma boa idéia considerar o uso de uma configuração com uma máquina remota do SQL Server, se ter uma implantação maior.  

###  <a name="bkmk_RemoteSiteSystem"></a> Servidores de sistema de sites remoto  
 As seguintes orientações destina-se a computadores que possuem uma função de sistema de site único. Planeie efetuar ajustes quando instalar várias funções de sistema de sites no mesmo computador.  

|Função do sistema de sites|CPU (núcleos)|Memória (GB)|Espaço em disco (GB)|  
|----------------------|---------------|---------------|--------------------|  
|Ponto de gestão|4|8|50|  
|Ponto de distribuição|2|8|Conforme requerido pelo sistema operativo e para armazenar o conteúdo que implementar|  
|Catálogo de Aplicações, com o serviço Web e o Web site no computador do sistema de sites|4|16|50|  
|Ponto de atualização de software<sup>1</sup>|8|16|Conforme requerido pelo sistema operativo e para armazenar as atualizações que implementar|  
|Todas as outras funções do sistema de sites|4|8|50|  

 <sup>1</sup> o computador que aloja um ponto de atualização de software requer as seguintes configurações para conjuntos aplicacionais do IIS:  

-   Aumentar a **comprimento da fila WsusPool** ao **2000**.  

-   Aumentar a **limite de memória privada WsusPool** por quatro vezes, ou defina-o como **0** (ilimitado).  

###  <a name="bkmk_DiskSpace"></a> Espaço em disco para sistemas de sites  
 Configuração e atribuição do disco contribuem para o desempenho do Configuration Manager. Uma vez que cada ambiente do Configuration Manager é diferente, os valores que implementar podem variar das seguintes orientações.  

 Para obter o melhor desempenho, coloque cada objeto num volume RAID separado e dedicado. Para todos os volumes de dados (Configuration Manager e respetivos ficheiros de base de dados), utilize o RAID 10 para obter o melhor desempenho.  

|Utilização de dados|Espaço mínimo em disco|25 000 clientes|50 000 clientes|100 000 clientes|150 000 clientes|700 000 clientes (site de administração central)|  
|----------------|------------------------|--------------------|--------------------|---------------------|---------------------|-----------------------------------------------------|  
|Sistema Operativo|Consulte as orientações para o sistema operativo.|Consulte as orientações para o sistema operativo.|Consulte as orientações para o sistema operativo.|Consulte as orientações para o sistema operativo.|Consulte as orientações para o sistema operativo.|Consulte as orientações para o sistema operativo.|  
|Ficheiros de registo e de aplicação do Configuration Manager|25 GB|50 GB|100 GB|200 GB|300 GB|200 GB|  
|Ficheiro .mdf da base de dados do site|75 GB para cada 25.000 clientes|75 GB|150 GB|300 GB|500 GB|2 TB|  
|Ficheiro .ldf da base de dados do site|25 GB para cada 25 000 clientes|25 GB|50 GB|100 GB|150 GB|100 GB|  
|Ficheiros da base de dados temporária (.mdf e .ldf)|Conforme necessário|Conforme necessário|Conforme necessário|Conforme necessário|Conforme necessário|Conforme necessário|  
|Conteúdo (partilhas de ponto de distribuição)|Conforme necessário<sup>1</sup>|Conforme necessário<sup>1</sup>|Conforme necessário<sup>1</sup>|Conforme necessário<sup>1</sup>|Conforme necessário<sup>1</sup>|Conforme necessário<sup>1</sup>|  

 <sup>1</sup> as orientações de espaço em disco não incluem o espaço necessário para conteúdo localizado na biblioteca de conteúdos nos pontos de servidor ou a distribuição de site. Para obter informações sobre o planeamento da biblioteca de conteúdos, veja [A biblioteca de conteúdos](../../../core/plan-design/hierarchy/the-content-library.md).  

 Além das orientações anteriores, considere as seguintes diretrizes quando planear os requisitos de espaço em disco:  

-   Cada cliente necessita de cerca de 5 MB de espaço.  

-   Quando planear o tamanho da base de dados Temp para um site primário, o plano para um tamanho combinado que seja 25% a 30% do ficheiro. mdf da base de dados do site. O tamanho real pode ser significativamente menor ou maior — depende do desempenho do servidor do site e o volume de dados de entrada durante curtos e longos períodos de tempo.  

    > [!NOTE]  
    >  Quando tiver 50 000 ou mais clientes num site, recomendamos que utilize quatro ou mais ficheiros. mdf da base de dados Temp.  

-   O tamanho da base de dados Temp para um site de administração central é normalmente muito menor do que para um site primário.  

-   A base de dados do site secundário tem as seguintes limitações de tamanho:  

    -   SQL Server 2012 Express: 10 GB  

    -   SQL Server 2014 Express: 10 GB  

##  <a name="bkmk_ScaleClient"></a> Clientes  
 Esta seção fornece configurações de hardware recomendadas para computadores que gere com software de cliente do Configuration Manager.  

### <a name="client-for-windows-computers"></a>Cliente para computadores Windows  
 Seguem-se os requisitos mínimos para computadores baseados em Windows que gere com o Configuration Manager, incluindo sistemas de operativos incorporados:  

-   **Processador e memória:** Consulte os requisitos de RAM para o sistema operativo do computador e processador.  

-   **Espaço em disco:** 500 MB espaço em disco disponível, com 5 GB recomendados para a cache do cliente do Configuration Manager. Menos espaço em disco é necessário se utilizar definições personalizadas para instalar o cliente do Configuration Manager:  

    -   Utilize o /skipprereq de propriedade da linha de comandos do CCMSetup para evitar a instalação de ficheiros que não exige que o cliente. Por exemplo, executar `CCMSetup.exe /skipprereq:silverlight.exe` se o cliente não utilizar o catálogo de aplicações. A partir do Configuration Manager 1802, Silverlight automaticamente já não está instalado.  

    -   Utilize a propriedade SMSCACHESIZE do Client.msi para definir um ficheiro de cache que seja menor do que o predefinido de 5120 MB. O tamanho mínimo é de 1 MB. Por exemplo, `CCMSetup.exe SMSCachesize=2` cria uma cache com 2 MB de tamanho.  

    Para obter mais informações sobre estas definições de instalação do cliente, consulte [acerca das propriedades de instalação de cliente](../../../core/clients/deploy/about-client-installation-properties.md).  

    > [!TIP]  
    >  Instalar o cliente com um espaço em disco mínimo é útil para os dispositivos Windows Embedded que, geralmente, têm um espaço em disco menor do que os computadores Windows padrão.  



 Seguem-se requisitos de hardware adicionais mínimos para funcionalidades opcionais no Configuration Manager.  

-   **Implementação do sistema operativo:** 384 MB de RAM  

-   **Centro de Software:** Processador a 500 MHz  

-   **Controlo remoto:** Pentium 4 Hyper-Threaded 3 GHz (um núcleo) ou CPU comparável, com, pelo menos, 1 GB de RAM para uma experiência ideal  

### <a name="client-for-linux-and-unix"></a>Cliente para Linux e UNIX  
 Seguem-se os requisitos mínimos para servidores Linux e UNIX que gere com o Configuration Manager.  

|Requisito|Detalhes|  
|-----------------|-------------|  
|Processador e memória|Consulte os requisitos de RAM para o sistema operativo do computador e processador.|  
|Espaço em disco|500 MB espaço em disco disponível, com 5 GB recomendados para a cache do cliente do Configuration Manager.|  
|Conectividade de rede|Computadores de cliente do Configuration Manager tem de ter conectividade de rede para sistemas de sites do Configuration Manager para ativar a gestão.|  

##  <a name="bkmk_ScaleConsole"></a> Consola do Configuration Manager  
 Os requisitos na tabela a seguir se aplicam a cada computador que executa a consola do Configuration Manager.  

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

 Quando instala suporte para o PowerShell num computador que executa a consola do Configuration Manager, pode executar cmdlets do PowerShell nesse computador para gerir o Gestor de configuração.

 - PowerShell 3.0 ou posterior é suportado

Além do PowerShell, Windows Management Framework (WMF) versão 3.0 ou posterior é suportado.   


##  <a name="bkmk_ScaleLab"></a> Implementações de laboratório  
 Utilize as seguintes recomendações mínimas de hardware para implementações de laboratório e teste do Configuration Manager. Estas recomendações aplicam-se a todos os tipos de site, até 100 clientes:  

|Função|CPU (núcleos)|Memória (GB)|Espaço em disco (GB)|  
|----------|---------------|-------------------|-----------------------|  
|Servidor do site e da base de dados|2 - 4|8 - 12|100|  
|Servidor do sistema de sites|1 - 4|2 - 4|50|  
|Cliente|1 - 2|1 - 3|30|  
