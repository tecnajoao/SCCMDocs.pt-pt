---
title: Servidores do sistema de sites suportados
titleSuffix: Configuration Manager
description: "Saiba quais as versões do Windows pode utilizar para alojar um site do System Center Configuration Manager ou a função do sistema de sites."
ms.custom: na
ms.date: 06/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 17905b4c-3895-4ad4-a69c-5e0d0fc5a8c3
caps.latest.revision: "44"
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: e7606e087e2540b49e8aa23c09d09831651ee48b
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/04/2017
---
# <a name="supported-operating-systems-for-system-center-configuration-manager-site-system-servers"></a>Sistemas operativos suportados para servidores de sistema de sites do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Este artigo fornece detalhes sobre as versões do Windows que pode utilizar para alojar um site do System Center Configuration Manager ou a função do sistema de sites.


Utilize as informações neste tópico juntamente com as informações dos seguintes artigos:
-   [Hardware recomendado para o Configuration Manager](../../../core/plan-design/configs/recommended-hardware.md)
-   [Site e os pré-requisitos do sistema de site do Configuration Manager](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)
-   [Tamanho e números da escala do Configuration Manager](../../../core/plan-design/configs/size-and-scale-numbers.md)



## <a name="windows-server-2016-standard-and-datacenter"></a>Windows Server 2016: Standard e Datacenter
Este sistema operativo a partir da versão 1606 com o rollup de correção de KB3186654 (ou a versão de linha de base do 1606, que foi lançada em Outubro de 2016) é suportado para o seguinte:

**Servidores do site:**  

-   Site de administração central  

-   Site primário  

-   Site Secundário  

**Servidores do sistema de sites:**  

-   Ponto de serviço Web do Catálogo de Aplicações  

-   Ponto de Web site do Catálogo de Aplicações  

-   Ponto de sincronização do Asset Intelligence  

-   Ponto de registo de certificados  

-   Ponto de distribuição  

     Os pontos de distribuição suportam várias configurações diferentes em que cada uma tem requisitos diferentes. Em alguns casos, estas configurações suportam a instalação não só em servidores, mas em sistemas operativos cliente. Para mais informações sobre as opções disponíveis para os pontos de distribuição, consulte [gerir a infraestrutura de conteúdo e o conteúdo para o System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Ponto de Endpoint Protection  

-   Ponto de inscrição  

-   Ponto proxy de registo  

-   Ponto de estado de contingência  

-   Ponto de gestão

-   Ponto do Reporting Services  

-   Ponto de ligação de serviço  

-   Servidor da base de dados do site  

     Os servidores de bases de dados do site não são suportados num controlador de domínio só de leitura (RODC). Para obter mais informações, veja [Pode encontrar problemas ao instalar o SQL Server num controlador de domínio](http://go.microsoft.com/fwlink/p/?LinkId=264856) na Base de Dados de Conhecimento Microsoft. Além disso, os servidores de sites secundários não são suportados em qualquer controlador de domínio.  

-   SMS_Provider  

-   Ponto de atualização de Software  

-   Ponto de migração de estado

## <a name="windows-server-2012-r2-x64-standard-and-datacenter"></a>Windows Server 2012 R2 (x64): Standard e Datacenter  
**Servidores do site:**  

-   Site de administração central  

-   Site primário  

-   Site Secundário  

**Servidores do sistema de sites:**  

-   Ponto de serviço Web do Catálogo de Aplicações  

-   Ponto de Web site do Catálogo de Aplicações  

-   Ponto de sincronização do Asset Intelligence  

-   Ponto de registo de certificados  

-   Ponto de distribuição  

     Os pontos de distribuição suportam várias configurações diferentes em que cada uma tem requisitos diferentes. Em alguns casos, estas configurações suportam a instalação não só em servidores, mas em sistemas operativos cliente. Para mais informações sobre as opções disponíveis para os pontos de distribuição, consulte [gerir a infraestrutura de conteúdo e o conteúdo para o System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Ponto de Endpoint Protection  

-   Ponto de inscrição  

-   Ponto proxy de registo  

-   Ponto de estado de contingência  

-   Ponto de gestão

-   Ponto do Reporting Services  

-   Ponto de ligação de serviço  

-   Servidor da base de dados do site  

     Os servidores de bases de dados do site não são suportados num controlador de domínio só de leitura (RODC). Para obter mais informações, veja [Pode encontrar problemas ao instalar o SQL Server num controlador de domínio](http://go.microsoft.com/fwlink/p/?LinkId=264856) na Base de Dados de Conhecimento Microsoft. Além disso, os servidores de sites secundários não são suportados em qualquer controlador de domínio.  

-   SMS_Provider  

-   Ponto de atualização de Software  

-   Ponto de migração de estado  

## <a name="windows-server-2012-x64-standard-and-datacenter"></a>Windows Server 2012 (x64): Standard e Datacenter  
**Servidores do site:**  

-   Site de administração central  

-   Site primário  

-   Site Secundário  

**Servidores do sistema de sites:**  

-   Ponto de serviço Web do Catálogo de Aplicações  

-   Ponto de Web site do Catálogo de Aplicações  

-   Ponto de sincronização do Asset Intelligence  

-   Ponto de registo de certificados  

-   Ponto de distribuição  

     Os pontos de distribuição suportam várias configurações diferentes em que cada uma tem requisitos diferentes. Em alguns casos, estas configurações suportam a instalação não só em servidores, mas em sistemas operativos cliente. Para mais informações sobre as opções disponíveis para os pontos de distribuição, consulte [gerir a infraestrutura de conteúdo e o conteúdo para o System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Ponto de Endpoint Protection  

-   Ponto de inscrição  

-   Ponto proxy de registo  

-   Ponto de estado de contingência  

-   Ponto de gestão

-   Ponto do Reporting Services  

-   Ponto de ligação de serviço  

-   Servidor da base de dados do site  

     Os servidores de bases de dados do site não são suportados num controlador de domínio só de leitura (RODC). Para obter mais informações, veja [Pode encontrar problemas ao instalar o SQL Server num controlador de domínio](http://go.microsoft.com/fwlink/p/?LinkId=264856) na Base de Dados de Conhecimento Microsoft. Além disso, os servidores de sites secundários não são suportados em qualquer controlador de domínio.  

-   SMS_Provider  

-   Ponto de atualização de Software  

-   Ponto de migração de estado  

## <a name="windows-server-2008-r2-with-sp1-x64-standard-enterprise-and-datacenter"></a>Windows Server 2008 R2 com SP1 (x64): Standard, Enterprise e Datacenter  
 Windows Server 2008 R2 tem agora suporte alargado e já não está no suporte base, conforme detalhado em [ciclo de vida de suporte Microsoft](https://support.microsoft.com/lifecycle). Para obter mais informações sobre suporte futuro para estes sistemas operativos como servidores de sistema de sites com o Configuration Manager, consulte [removidas e funcionalidades preteridas para o System Center Configuration Manager](../../../core/plan-design/changes/removed-and-deprecated-features.md).  

 A partir do Configuration Manager versão 1702, este sistema operativo não é suportado para servidores do site ou a maioria das funções de sistema de sites, mas permanecem suportado para a função de sistema de sites de ponto de distribuição (incluindo pontos de distribuição de extração e para PXE e multicast).

 As versões anteriores 1702 continuam a suportar a sua utilização para o seguinte.


**Servidores do site:**  

-   Site de administração central  

-   Site primário  

-   Site Secundário  

**Servidores do sistema de sites:**  

-   Ponto de serviço Web do Catálogo de Aplicações  

-   Ponto de Web site do Catálogo de Aplicações  

-   Ponto de sincronização do Asset Intelligence  

-   Ponto de registo de certificados  

-   Ponto de distribuição  

     Os pontos de distribuição suportam várias configurações diferentes em que cada uma tem requisitos diferentes. Em alguns casos, estas configurações suportam a instalação não só em servidores, mas em sistemas operativos cliente. Para mais informações sobre as opções disponíveis para os pontos de distribuição, consulte [gerir a infraestrutura de conteúdo e o conteúdo para o System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Ponto de Endpoint Protection  

-   Ponto de inscrição  

-   Ponto proxy de registo  

-   Ponto de estado de contingência  

-   Ponto de gestão

-   Ponto do Reporting Services  

-   Ponto de ligação de serviço  

-   Servidor da base de dados do site  

     Os servidores de bases de dados do site não são suportados num controlador de domínio só de leitura (RODC). Para obter mais informações, veja [Pode encontrar problemas ao instalar o SQL Server num controlador de domínio](http://go.microsoft.com/fwlink/p/?LinkId=264856) na Base de Dados de Conhecimento Microsoft. Além disso, os servidores de sites secundários não são suportados em qualquer controlador de domínio.  

-   SMS_Provider  

-   Ponto de atualização de Software  

-   Ponto de migração de estado  

## <a name="windows-server-2008-with-sp2-x86-x64-standard-enterprise-and-datacenter"></a>Windows Server 2008 com SP2 (x86, x64): Standard, Enterprise e Datacenter  
 Windows Server 2008 tem agora suporte alargado e já não está no suporte base, conforme detalhado em [ciclo de vida de suporte Microsoft](https://support.microsoft.com/lifecycle). Para obter mais informações sobre suporte futuro para estes sistemas operativos como servidores de sistema de sites com o Configuration Manager, consulte [removidas e funcionalidades preteridas para o System Center Configuration Manager](../../../core/plan-design/changes/removed-and-deprecated-features.md).  

Este sistema operativo não é suportado para servidores de site ou funções de sistema de sites com a exceção do ponto de distribuição e ponto de distribuição de solicitação. Pode continuar a utilizar este sistema operativo como um ponto de distribuição, até que a desaprovação deste suporte é anunciada ou o período de suporte expandido deste sistema operativo expira. Para obter mais informações, consulte [instalação do System Center Configuration Manager CB e LTSB falha no Windows Server 2008](https://support.microsoft.com/help/4015095).

**Servidores do sistema de sites:**  
-   Ponto de distribuição  

    -   Os pontos de distribuição neste sistema operativo não suportam Multicast.  

    -   Os pontos de distribuição neste sistema operativo têm suporte para PXE, mas não suportam o arranque de rede de computadores cliente no modo EFI. Os computadores cliente com arranque BIOS ou EFI em modo legado são suportados.  

    -   Os pontos de distribuição suportam várias configurações diferentes em que cada uma tem requisitos diferentes. Em alguns casos, estas configurações suportam a instalação não só em servidores, mas em sistemas operativos cliente. Para mais informações sobre as opções disponíveis para os pontos de distribuição, consulte [gerir a infraestrutura de conteúdo e o conteúdo para o System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  



## <a name="windows-10-x86-x64-pro-and-enterprise"></a>Windows 10 (x86, x64): Pro e Enterprise  
**Servidores do sistema de sites:**  

-   Ponto de distribuição  

    -   Os pontos de distribuição neste sistema operativo não têm suporte para PXE.  

    -   Os pontos de distribuição nesta versão do sistema operativo não suportam Multicast.  

    -   Os pontos de distribuição suportam várias configurações diferentes em que cada uma tem requisitos diferentes. Em alguns casos, estas configurações suportam a instalação não só em servidores, mas em sistemas operativos cliente. Para mais informações sobre as opções disponíveis para os pontos de distribuição, consulte [gerir a infraestrutura de conteúdo e o conteúdo para o System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

## <a name="windows-81-x86-x64-professional-and-enterprise"></a>Windows 8.1 (x86, x64): Professional e Enterprise  
**Servidores do sistema de sites:**  

-   Ponto de distribuição  

    -   Os pontos de distribuição neste sistema operativo não têm suporte para PXE.  

    -   Os pontos de distribuição nesta versão do sistema operativo não suportam Multicast.  

    -   Os pontos de distribuição suportam várias configurações diferentes em que cada uma tem requisitos diferentes. Em alguns casos, estas configuração suporta a instalação não só em servidores, mas em sistemas operativos cliente. Para mais informações sobre as opções disponíveis para os pontos de distribuição, consulte [gerir a infraestrutura de conteúdo e o conteúdo para o System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

## <a name="windows-8-x86-x64-professional-and-enterprise"></a>Windows 8 (x86, x64): Professional e Enterprise
**Servidores do sistema de sites:**  

-   Ponto de distribuição  

    -   Os pontos de distribuição neste sistema operativo não têm suporte para PXE.  

    -   Os pontos de distribuição nesta versão do sistema operativo não suportam Multicast.  

    -   Os pontos de distribuição suportam várias configurações diferentes em que cada uma tem requisitos diferentes. Em alguns casos, estas configurações suportam a instalação não só em servidores, mas em sistemas operativos cliente. Para mais informações sobre as opções disponíveis para os pontos de distribuição, consulte [gerir a infraestrutura de conteúdo e o conteúdo para o System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

## <a name="windows-7-with-sp1-x86-x64-professional-enterprise-and-ultimate"></a>Windows 7 com SP1 (x86, x64): Professional, Enterprise e Ultimate  
**Servidores do sistema de sites:**  

-   Ponto de distribuição  

    -   Os pontos de distribuição neste sistema operativo não têm suporte para PXE.  

    -   Os pontos de distribuição nesta versão do sistema operativo não suportam Multicast.  

    -   Os pontos de distribuição suportam várias configurações diferentes em que cada uma tem requisitos diferentes. Em alguns casos, estas configurações suportam a instalação não só em servidores, mas em sistemas operativos cliente. Para mais informações sobre as opções disponíveis para os pontos de distribuição, consulte [gerir a infraestrutura de conteúdo e o conteúdo para o System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  


## <a name="the-server-core-installation-of-windows-server-2016"></a>A instalação do server core do Windows Server 2016
Este sistema operativo a partir da versão 1606 com o rollup de correção de KB3186654 (ou a versão de linha de base do 1606, que foi lançada em Outubro de 2016) é suportado para utilização como uma distribuição ponto com as seguintes limitações:  
  -   Apenas a versão de x64 bits é suportada.
  -   Pontos de distribuição neste sistema operativo não suportam PXE ou Multicast.  


## <a name="the-server-core-installation-of-windows-server-2012-r2"></a>A instalação Server Core do Windows Server 2012 R2  
 Para além de sistemas operativos anteriores listados, a instalação do server core do Windows Server 2012 R2 é suportada para utilização como pontos de distribuição com as seguintes limitações:  

-   Apenas a versão de x64 bits é suportada.

-   Pontos de distribuição neste sistema operativo não suportam PXE ou Multicast.  

## <a name="the-server-core-installation-of-windows-server-2012"></a>A instalação Server Core do Windows Server 2012  
 Para além de sistemas operativos anteriores listados, a instalação do server core do Windows Server 2012 também é suportada para utilização como uma distribuição ponto com as seguintes limitações:  

-   É suportada apenas a versão de 64 bits.  

-   Pontos de distribuição neste sistema operativo não suportam PXE ou Multicast.
