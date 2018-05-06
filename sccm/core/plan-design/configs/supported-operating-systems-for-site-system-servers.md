---
title: Servidores do sistema de sites suportados
titleSuffix: Configuration Manager
description: Saiba quais as versões do Windows pode utilizar para alojar um site do System Center Configuration Manager ou a função do sistema de sites.
ms.date: 04/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 17905b4c-3895-4ad4-a69c-5e0d0fc5a8c3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: de7f340080111daf3f1b19e26aa838dc6db2e263
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="supported-operating-systems-for-system-center-configuration-manager-site-system-servers"></a>Sistemas operativos suportados para servidores de sistema de sites do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Este artigo fornece detalhes sobre as versões do Windows que pode utilizar para alojar um site do Configuration Manager ou a função do sistema de sites.


Utilize as informações neste artigo com as informações nos seguintes artigos:
-   [Hardware recomendado para o Configuration Manager](../../../core/plan-design/configs/recommended-hardware.md)
-   [Site e os pré-requisitos do sistema de site do Configuration Manager](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)
-   [Tamanho e números da escala do Configuration Manager](../../../core/plan-design/configs/size-and-scale-numbers.md)



## <a name="windows-server-2016-standard-and-datacenter"></a>Windows Server 2016: Standard e Datacenter
Com o rollup de correção de KB3186654 deste SO é suportado para as seguintes funções:

**Servidores do site:**  

-   Site de administração central  

-   Site primário  

-   Site Secundário  

**Servidores do sistema de sites:**  

-   Ponto de serviço Web do Catálogo de Aplicações  

-   Ponto de site do Catálogo de Aplicações  

-   Ponto de sincronização do Asset Intelligence  

-   Ponto de registo de certificados  

-   Ponto de distribuição  

     Os pontos de distribuição suportam várias configurações diferentes em que cada uma tem requisitos diferentes. Em alguns casos, estas configurações suportam a instalação não só em servidores, mas em sistemas operativos cliente. Para obter mais informações sobre as opções disponíveis para os pontos de distribuição, consulte [gerir a infraestrutura de conteúdo e conteúda](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Ponto de Endpoint Protection  

-   Ponto de inscrição  

-   Ponto proxy de registo  

-   Ponto de estado de contingência  

-   Ponto de gestão

-   Ponto do Reporting Services  

-   Ponto de ligação de serviço  

-   Servidor da base de dados do site  

     Os servidores de bases de dados do site não são suportados num controlador de domínio só de leitura (RODC). Para obter mais informações, veja [Pode encontrar problemas ao instalar o SQL Server num controlador de domínio](https://go.microsoft.com/fwlink/p/?LinkId=264856) na Base de Dados de Conhecimento Microsoft. Além disso, os servidores de sites secundários não são suportados em qualquer controlador de domínio.  

-   SMS_Provider  

-   Ponto de atualização de software  

-   Ponto de Migração de Estado



## <a name="windows-storage-server-2016"></a>O Windows Storage Server 2016

**Servidor do sistema de sites:**  

-   Ponto de distribuição  



## <a name="windows-server-2012-r2-x64-standard-and-datacenter"></a>Windows Server 2012 R2 (x64): Standard e Datacenter  
**Servidores do site:**  

-   Site de administração central  

-   Site primário  

-   Site Secundário  

**Servidores do sistema de sites:**  

-   Ponto de serviço Web do Catálogo de Aplicações  

-   Ponto de site do Catálogo de Aplicações  

-   Ponto de sincronização do Asset Intelligence  

-   Ponto de registo de certificados  

-   Ponto de distribuição  

     Os pontos de distribuição suportam várias configurações diferentes em que cada uma tem requisitos diferentes. Em alguns casos, estas configurações suportam a instalação não só em servidores, mas em sistemas operativos cliente. Para obter mais informações sobre as opções disponíveis para os pontos de distribuição, consulte [gerir a infraestrutura de conteúdo e conteúda](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Ponto de Endpoint Protection  

-   Ponto de inscrição  

-   Ponto proxy de registo  

-   Ponto de estado de contingência  

-   Ponto de gestão

-   Ponto do Reporting Services  

-   Ponto de ligação de serviço  

-   Servidor da base de dados do site  

     Os servidores de bases de dados do site não são suportados num controlador de domínio só de leitura (RODC). Para obter mais informações, veja [Pode encontrar problemas ao instalar o SQL Server num controlador de domínio](https://go.microsoft.com/fwlink/p/?LinkId=264856) na Base de Dados de Conhecimento Microsoft. Além disso, os servidores de sites secundários não são suportados em qualquer controlador de domínio.  

-   SMS_Provider  

-   Ponto de atualização de software  

-   Ponto de Migração de Estado  

## <a name="windows-server-2012-x64-standard-and-datacenter"></a>Windows Server 2012 (x64): Standard e Datacenter  
**Servidores do site:**  

-   Site de administração central  

-   Site primário  

-   Site Secundário  

**Servidores do sistema de sites:**  

-   Ponto de serviço Web do Catálogo de Aplicações  

-   Ponto de site do Catálogo de Aplicações  

-   Ponto de sincronização do Asset Intelligence  

-   Ponto de registo de certificados  

-   Ponto de distribuição  

     Os pontos de distribuição suportam várias configurações diferentes em que cada uma tem requisitos diferentes. Em alguns casos, estas configurações suportam a instalação não só em servidores, mas em sistemas operativos cliente. Para obter mais informações sobre as opções disponíveis para os pontos de distribuição, consulte [gerir a infraestrutura de conteúdo e conteúda](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Ponto de Endpoint Protection  

-   Ponto de inscrição  

-   Ponto proxy de registo  

-   Ponto de estado de contingência  

-   Ponto de gestão

-   Ponto do Reporting Services  

-   Ponto de ligação de serviço  

-   Servidor da base de dados do site  

     Os servidores de bases de dados do site não são suportados num controlador de domínio só de leitura (RODC). Para obter mais informações, veja [Pode encontrar problemas ao instalar o SQL Server num controlador de domínio](https://go.microsoft.com/fwlink/p/?LinkId=264856) na Base de Dados de Conhecimento Microsoft. Além disso, os servidores de sites secundários não são suportados em qualquer controlador de domínio.  

-   SMS_Provider  

-   Ponto de atualização de software  

-   Ponto de Migração de Estado  



## <a name="windows-server-2008-r2-with-sp1-x64-standard-enterprise-and-datacenter"></a>Windows Server 2008 R2 com SP1 (x64): Standard, Enterprise e Datacenter  
 Windows Server 2008 R2 tem agora suporte alargado e já não está no suporte base, conforme detalhado em [ciclo de vida de suporte Microsoft](https://support.microsoft.com/lifecycle). Para obter mais informações sobre suporte futuro para estes sistemas operativos como servidores de sistema de sites com o Configuration Manager, consulte [sistemas operativos do servidor preteridos](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems).  

 Este SO não é suportado para servidores do site ou a maioria das funções de sistema de sites. Ainda é suportada para a função de sistema de sites da ponto de distribuição, incluindo pontos de distribuição de solicitação e para PXE e multicast.

**Servidores do sistema de sites:**  
-   Ponto de distribuição  

    -   Os pontos de distribuição deste SO não suportam Multicast.  

    -   Pontos de distribuição neste sistema operativo têm suporte para PXE.

    -   Os pontos de distribuição suportam várias configurações diferentes em que cada uma tem requisitos diferentes. Em alguns casos, estas configurações suportam a instalação não só em servidores, mas em sistemas operativos cliente. Para obter mais informações sobre as opções disponíveis para os pontos de distribuição, consulte [gerir a infraestrutura de conteúdo e conteúda](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  



## <a name="windows-server-2008-with-sp2-x86-x64-standard-enterprise-and-datacenter"></a>Windows Server 2008 com SP2 (x86, x64): Standard, Enterprise e Datacenter  
 Windows Server 2008 tem agora suporte alargado e já não está no suporte base, conforme detalhado em [ciclo de vida de suporte Microsoft](https://support.microsoft.com/lifecycle). Para obter mais informações sobre suporte futuro para estes sistemas operativos como servidores de sistema de sites com o Configuration Manager, consulte [sistemas operativos do servidor preteridos](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems).  

Este SO não é suportado para servidores do site ou funções de sistema de sites, exceto para o ponto de distribuição e o ponto de distribuição de solicitação. Pode continuar a utilizar este SO como um ponto de distribuição, até que a desaprovação deste suporte é anunciada ou o período de suporte alargado deste SO expira. Para obter mais informações, consulte [instalação do System Center Configuration Manager CB e LTSB falha no Windows Server 2008](https://support.microsoft.com/help/4015095).

**Servidores do sistema de sites:**  
-   Ponto de distribuição  

    -   Os pontos de distribuição deste SO não suportam Multicast.  

    -   Pontos de distribuição neste sistema operativo têm suporte para PXE, mas não suportam o arranque de rede de computadores de cliente no modo EFI. Os computadores cliente com arranque BIOS ou EFI em modo legado são suportados.  

    -   Os pontos de distribuição suportam várias configurações diferentes em que cada uma tem requisitos diferentes. Em alguns casos, estas configurações suportam a instalação não só em servidores, mas em sistemas operativos cliente. Para obter mais informações sobre as opções disponíveis para os pontos de distribuição, consulte [gerir a infraestrutura de conteúdo e conteúda](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  



## <a name="windows-10-x86-x64-pro-and-enterprise"></a>Windows 10 (x86, x64): Pro e Enterprise  
**Servidores do sistema de sites:**  

-   Ponto de distribuição  

    -   Os pontos de distribuição deste SO não são suportados para PXE. 

    -   Pontos de distribuição nesta versão do SO não suportam Multicast.  

    -   Os pontos de distribuição suportam várias configurações diferentes em que cada uma tem requisitos diferentes. Em alguns casos, estas configurações suportam a instalação não só em servidores, mas em sistemas operativos cliente. Para obter mais informações sobre as opções disponíveis para os pontos de distribuição, consulte [gerir a infraestrutura de conteúdo e conteúda](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  



## <a name="windows-81-x86-x64-professional-and-enterprise"></a>Windows 8.1 (x86, x64): Professional e Enterprise  
**Servidores do sistema de sites:**  

-   Ponto de distribuição  

    -   Os pontos de distribuição deste SO não são suportados para PXE.  

    -   Pontos de distribuição nesta versão do SO não suportam Multicast.  

    -   Os pontos de distribuição suportam várias configurações diferentes em que cada uma tem requisitos diferentes. Em alguns casos, estas configurações suportam a instalação não só em servidores, mas em sistemas operativos cliente. Para obter mais informações sobre as opções disponíveis para os pontos de distribuição, consulte [gerir a infraestrutura de conteúdo e conteúda](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  



## <a name="windows-7-with-sp1-x86-x64-professional-enterprise-and-ultimate"></a>Windows 7 com SP1 (x86, x64): Professional, Enterprise e Ultimate  
**Servidores do sistema de sites:**  

-   Ponto de distribuição  

    -   Os pontos de distribuição deste SO não são suportados para PXE.  

    -   Pontos de distribuição nesta versão do SO não suportam Multicast.  

    -   Os pontos de distribuição suportam várias configurações diferentes em que cada uma tem requisitos diferentes. Em alguns casos, estas configurações suportam a instalação não só em servidores, mas em sistemas operativos cliente. Para obter mais informações sobre as opções disponíveis para os pontos de distribuição, consulte [gerir a infraestrutura de conteúdo e conteúda](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

## <a name="the-server-core-installation-of-windows-server-version-1709"></a>A instalação do server core do Windows Server, versão 1709
A partir do Configuration Manager 1710, [Windows Server, versão 1709](https://docs.microsoft.com/windows-server/get-started/get-started-with-1709) é suportada para utilização como uma distribuição ponto com as seguintes limitações:  
  -   Apenas a versão de x64 bits é suportada.
  -   Os pontos de distribuição deste SO não suportam PXE ou Multicast.  

## <a name="the-server-core-installation-of-windows-server-2016"></a>A instalação do server core do Windows Server 2016
Com o rollup de correção de KB3186654, este SO é suportado para utilização como uma distribuição ponto com as seguintes limitações:  
  -   Apenas a versão de x64 bits é suportada.
  -   Os pontos de distribuição deste SO não suportam PXE ou Multicast.  



## <a name="the-server-core-installation-of-windows-server-2012-r2"></a>A instalação Server Core do Windows Server 2012 R2  
 A instalação do server core do Windows Server 2012 R2 é suportada para utilização como uma distribuição ponto com as seguintes limitações:  

-   Apenas a versão de x64 bits é suportada.

-   Os pontos de distribuição deste SO não suportam PXE ou Multicast.  



## <a name="the-server-core-installation-of-windows-server-2012"></a>A instalação Server Core do Windows Server 2012  
 A instalação do server core do Windows Server 2012 é suportada para utilização como uma distribuição ponto com as seguintes limitações:  

-   É suportada apenas a versão de 64 bits.  

-   Os pontos de distribuição deste SO não suportam PXE ou Multicast.
