---
title: Suportados servidores do sistema de sites | Documentos do Microsoft
description: "Saiba que versões do Windows pode utilizar para alojar um site do System Center Configuration Manager ou a função do sistema de sites."
ms.custom: na
ms.date: 3/9/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 17905b4c-3895-4ad4-a69c-5e0d0fc5a8c3
caps.latest.revision: 44
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 86109f7186422c2b29ee933e827a7d14123e5792
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="supported-operating-systems-for-system-center-configuration-manager-site-system-servers"></a>Sistemas operativos suportados para servidores de sistema de sites do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Este artigo fornece detalhes sobre as versões do Windows que pode utilizar para alojar um site do System Center Configuration Manager ou a função do sistema de sites.


Utilize as informações neste tópico juntamente com as informações dos seguintes artigos:
-   [Hardware recomendados para o Configuration Manager](../../../core/plan-design/configs/recommended-hardware.md)
-   [Site e os pré-requisitos de sistema de sites do Configuration Manager](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)
-   [Tamanho e a escala números para o Configuration Manager](../../../core/plan-design/configs/size-and-scale-numbers.md)



## <a name="windows-server-2016-standard-and-datacenter"></a>Windows Server 2016: Standard e Datacenter
Versão 1606 com o rollup de correção da KB3186654 (ou a versão de linha de base do 1606, que foi lançada em Outubro de 2016) este sistema operativo é suportado para o seguinte:

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

     Pontos de distribuição suportam várias configurações diferentes que têm requisitos diferentes. Em alguns casos, estas configurações suportam a instalação não apenas em servidores, mas em sistemas operativos de cliente. Para obter mais informações sobre as opções que estão disponíveis para os pontos de distribuição, consulte o artigo [gerir a infraestrutura do conteúdo e conteúda para o System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

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

     Pontos de distribuição suportam várias configurações diferentes que têm requisitos diferentes. Em alguns casos, estas configurações suportam a instalação não apenas em servidores, mas em sistemas operativos de cliente. Para obter mais informações sobre as opções que estão disponíveis para os pontos de distribuição, consulte o artigo [gerir a infraestrutura do conteúdo e conteúda para o System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

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

     Pontos de distribuição suportam várias configurações diferentes que têm requisitos diferentes. Em alguns casos, estas configurações suportam a instalação não apenas em servidores, mas em sistemas operativos de cliente. Para obter mais informações sobre as opções que estão disponíveis para os pontos de distribuição, consulte o artigo [gerir a infraestrutura do conteúdo e conteúda para o System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

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
 Windows Server 2008 R2 está agora em suporte alargado e já não em suporte base, conforme especificado nas [ciclo de vida de suporte Microsoft](https://support.microsoft.com/lifecycle). Para obter mais informações sobre o suporte de futuro para estes sistemas operativos como servidores de sistema de sites com o Configuration Manager, consulte o artigo [Removed e funcionalidades preteridas para o System Center Configuration Manager](../../../core/plan-design/changes/removed-and-deprecated-features.md).  

 A partir do Configuration Manager versão 1702, este sistema operativo não é suportado para servidores de site ou a maioria das funções de sistema de sites, mas permanecem suportado para o ponto de migração de estado e pontos de distribuição função do sistema de sites (incluindo os pontos de distribuição de solicitação e para PXE e multicast).
 
 Versões anteriores ao 1702 continuam para suportar a respetiva utilização para o seguinte.


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

     Pontos de distribuição suportam várias configurações diferentes que têm requisitos diferentes. Em alguns casos, estas configurações suportam a instalação não apenas em servidores, mas em sistemas operativos de cliente. Para obter mais informações sobre as opções que estão disponíveis para os pontos de distribuição, consulte o artigo [gerir a infraestrutura do conteúdo e conteúda para o System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

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
 Windows Server 2008 está agora em suporte alargado e já não em suporte base, conforme especificado nas [ciclo de vida de suporte Microsoft](https://support.microsoft.com/lifecycle). Para obter mais informações sobre o suporte de futuro para estes sistemas operativos como servidores de sistema de sites com o Configuration Manager, consulte o artigo [Removed e funcionalidades preteridas para o System Center Configuration Manager](../../../core/plan-design/changes/removed-and-deprecated-features.md).  

Este sistema operativo não é suportado para servidores de site ou funções de sistema de sites com a exceção do ponto de distribuição e ponto de distribuição de solicitação. Pode continuar a utilizar este sistema operativo como um ponto de distribuição até preterição deste suporte é anunciada ou do período de suporte alargado este sistema operativo. Para obter mais informações, consulte o artigo [instalação do System Center Configuration Manager CB e LTSB falha no Windows Server 2008](https://support.microsoft.com/help/4015095).

**Servidores do sistema de sites:**  
-   Ponto de distribuição  

    -   Os pontos de distribuição neste sistema operativo não suportam Multicast.  

    -   Os pontos de distribuição neste sistema operativo têm suporte para PXE, mas não suportam o arranque de rede de computadores cliente no modo EFI. Os computadores cliente com arranque BIOS ou EFI em modo legado são suportados.  

    -   Pontos de distribuição suportam várias configurações diferentes que têm requisitos diferentes. Em alguns casos, estas configurações suportam a instalação não apenas em servidores, mas em sistemas operativos de cliente. Para obter mais informações sobre as opções que estão disponíveis para os pontos de distribuição, consulte o artigo [gerir a infraestrutura do conteúdo e conteúda para o System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  



## <a name="windows-10-x86-x64-pro-and-enterprise"></a>Windows 10 (x86, x64): Pro e Enterprise  
**Servidores do sistema de sites:**  

-   Ponto de distribuição  

    -   Os pontos de distribuição neste sistema operativo não têm suporte para PXE.  

    -   Os pontos de distribuição nesta versão do sistema operativo não suportam Multicast.  

    -   Pontos de distribuição suportam várias configurações diferentes que têm requisitos diferentes. Em alguns casos, estas configurações suportam a instalação não apenas em servidores, mas em sistemas operativos de cliente. Para obter mais informações sobre as opções que estão disponíveis para os pontos de distribuição, consulte o artigo [gerir a infraestrutura do conteúdo e conteúda para o System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

## <a name="windows-81-x86-x64-professional-and-enterprise"></a>Windows 8.1 (x86, x64): Professional e Enterprise  
**Servidores do sistema de sites:**  

-   Ponto de distribuição  

    -   Os pontos de distribuição neste sistema operativo não têm suporte para PXE.  

    -   Os pontos de distribuição nesta versão do sistema operativo não suportam Multicast.  

    -   Pontos de distribuição suportam várias configurações diferentes que têm requisitos diferentes. Em alguns casos, estas configuração suporta a instalação não apenas em servidores, mas em sistemas operativos de cliente. Para obter mais informações sobre as opções que estão disponíveis para os pontos de distribuição, consulte o artigo [gerir a infraestrutura do conteúdo e conteúda para o System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

## <a name="windows-8-x86-x64-professional-and-enterprise"></a>Windows 8 (x86, x64): Professional e Enterprise
**Servidores do sistema de sites:**  

-   Ponto de distribuição  

    -   Os pontos de distribuição neste sistema operativo não têm suporte para PXE.  

    -   Os pontos de distribuição nesta versão do sistema operativo não suportam Multicast.  

    -   Pontos de distribuição suportam várias configurações diferentes que têm requisitos diferentes. Em alguns casos, estas configurações suportam a instalação não apenas em servidores, mas em sistemas operativos de cliente. Para obter mais informações sobre as opções que estão disponíveis para os pontos de distribuição, consulte o artigo [gerir a infraestrutura do conteúdo e conteúda para o System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

## <a name="windows-7-with-sp1-x86-x64-professional-enterprise-and-ultimate"></a>Windows 7 com SP1 (x86, x64): Professional, Enterprise e Ultimate  
**Servidores do sistema de sites:**  

-   Ponto de distribuição  

    -   Os pontos de distribuição neste sistema operativo não têm suporte para PXE.  

    -   Os pontos de distribuição nesta versão do sistema operativo não suportam Multicast.  

    -   Pontos de distribuição suportam várias configurações diferentes que têm requisitos diferentes. Em alguns casos, estas configurações suportam a instalação não apenas em servidores, mas em sistemas operativos de cliente. Para obter mais informações sobre as opções que estão disponíveis para os pontos de distribuição, consulte o artigo [gerir a infraestrutura do conteúdo e conteúda para o System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  


## <a name="the-server-core-installation-of-windows-server-2016"></a>A instalação do núcleo de servidor do Windows Server 2016
Versão 1606 com o rollup de correção de KB3186654 (ou a versão de linha de base do 1606, que foi lançada em Outubro de 2016) a partir deste sistema operativo é suportado para utilização como uma distribuição ponto com as seguintes limitações:  
  -   É suportada apenas a versão de bits x64.
  -   Pontos de distribuição com este sistema operativo não suportam PXE ou Multicast.  


## <a name="the-server-core-installation-of-windows-server-2012-r2"></a>A instalação Server Core do Windows Server 2012 R2  
 Para além de sistemas operativos anteriores listados, a instalação do núcleo de servidor do Windows Server 2012 R2 é suportada para utilização como pontos de distribuição com as seguintes limitações:  

-   É suportada apenas a versão de bits x64.

-   Pontos de distribuição com este sistema operativo não suportam PXE ou Multicast.  

## <a name="the-server-core-installation-of-windows-server-2012"></a>A instalação Server Core do Windows Server 2012  
 Para além de sistemas operativos anteriores listados, a instalação do núcleo de servidor do Windows Server 2012 também é suportada para utilização como uma distribuição ponto com as seguintes limitações:  

-   É suportada apenas a versão de 64 bits.  

-   Pontos de distribuição com este sistema operativo não suportam PXE ou Multicast.

