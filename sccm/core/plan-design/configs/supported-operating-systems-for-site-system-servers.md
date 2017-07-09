---
title: Suporte para servidores de sistema de site | Microsoft Docs
description: "Saiba quais versões do Windows que você pode usar para hospedar um site do System Center Configuration Manager ou a função do sistema de site."
ms.custom: na
ms.date: 06/27/2017
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
ms.sourcegitcommit: 0ec241d07f51b80b84d65676ef1207b31a9a9983
ms.openlocfilehash: be635e4df79b57b6f650287fa3774d2c10613cee
ms.contentlocale: pt-pt
ms.lasthandoff: 06/28/2017


---
# <a name="supported-operating-systems-for-system-center-configuration-manager-site-system-servers"></a>Sistemas operacionais com suporte para servidores de sistema de site do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramificação atual)*


Este artigo fornece detalhes sobre as versões do Windows que você pode usar para hospedar um site do System Center Configuration Manager ou a função do sistema de site.


Utilize as informações neste tópico juntamente com as informações dos seguintes artigos:
-   [Hardware recomendado para o Configuration Manager](../../../core/plan-design/configs/recommended-hardware.md)
-   [Site e pré-requisitos do sistema de site do Configuration Manager](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)
-   [Números de tamanho e a escala para o Configuration Manager](../../../core/plan-design/configs/size-and-scale-numbers.md)



## <a name="windows-server-2016-standard-and-datacenter"></a>Windows Server 2016: Standard e Datacenter
Começando com a versão 1606 com o pacote cumulativo de hotfix do KB3186654 (ou a versão de linha de base do 1606, que foi lançada em outubro de 2016) neste sistema operacional é suporte para o seguinte:

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

     Pontos de distribuição dão suporte a várias configurações diferentes que possuem requisitos diferentes. Em alguns casos, essas configurações dão suporte à instalação não somente em servidores, mas em sistemas operacionais cliente. Para obter mais informações sobre as opções que estão disponíveis para pontos de distribuição, consulte [gerenciar conteúda e infraestrutura de conteúdo para o System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

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

     Pontos de distribuição dão suporte a várias configurações diferentes que possuem requisitos diferentes. Em alguns casos, essas configurações dão suporte à instalação não somente em servidores, mas em sistemas operacionais cliente. Para obter mais informações sobre as opções que estão disponíveis para pontos de distribuição, consulte [gerenciar conteúda e infraestrutura de conteúdo para o System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

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

     Pontos de distribuição dão suporte a várias configurações diferentes que possuem requisitos diferentes. Em alguns casos, essas configurações dão suporte à instalação não somente em servidores, mas em sistemas operacionais cliente. Para obter mais informações sobre as opções que estão disponíveis para pontos de distribuição, consulte [gerenciar conteúda e infraestrutura de conteúdo para o System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

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
 Windows Server 2008 R2 agora está em suporte estendido e não têm suporte, conforme detalhado no [ciclo de vida do suporte Microsoft](https://support.microsoft.com/lifecycle). Para obter mais informações sobre suporte futuro para esses sistemas operacionais como servidores do sistema de site com o Configuration Manager, consulte [recursos removidos e preteridos do System Center Configuration Manager](../../../core/plan-design/changes/removed-and-deprecated-features.md).  

 Começando com o Configuration Manager versão 1702, este sistema operacional não tem suporte para servidores do site ou a maioria das funções de sistema de site, mas permanecem com suporte para a função de sistema de site do ponto de distribuição (incluindo pontos de distribuição de recepção e para PXE e multicast).

 Versões anteriores 1702 continuam dar suporte ao seu uso para o seguinte.


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

     Pontos de distribuição dão suporte a várias configurações diferentes que possuem requisitos diferentes. Em alguns casos, essas configurações dão suporte à instalação não somente em servidores, mas em sistemas operacionais cliente. Para obter mais informações sobre as opções que estão disponíveis para pontos de distribuição, consulte [gerenciar conteúda e infraestrutura de conteúdo para o System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

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
 Windows Server 2008 agora está em suporte estendido e não têm suporte, conforme detalhado no [ciclo de vida do suporte Microsoft](https://support.microsoft.com/lifecycle). Para obter mais informações sobre suporte futuro para esses sistemas operacionais como servidores do sistema de site com o Configuration Manager, consulte [recursos removidos e preteridos do System Center Configuration Manager](../../../core/plan-design/changes/removed-and-deprecated-features.md).  

Não há suporte para este sistema operacional para servidores do site ou funções de sistema de site com a exceção do ponto de distribuição e ponto de distribuição de recepção. Você pode continuar a usar este sistema operacional como um ponto de distribuição até que a desaprovação desse suporte seja anunciada ou o período de suporte estendido deste sistema operacional expire. Para obter mais informações, consulte [LTSB e instalação do System Center Configuration Manager CB falhar no Windows Server 2008](https://support.microsoft.com/help/4015095).

**Servidores do sistema de sites:**  
-   Ponto de distribuição  

    -   Os pontos de distribuição neste sistema operativo não suportam Multicast.  

    -   Os pontos de distribuição neste sistema operativo têm suporte para PXE, mas não suportam o arranque de rede de computadores cliente no modo EFI. Os computadores cliente com arranque BIOS ou EFI em modo legado são suportados.  

    -   Pontos de distribuição dão suporte a várias configurações diferentes que possuem requisitos diferentes. Em alguns casos, essas configurações dão suporte à instalação não somente em servidores, mas em sistemas operacionais cliente. Para obter mais informações sobre as opções que estão disponíveis para pontos de distribuição, consulte [gerenciar conteúda e infraestrutura de conteúdo para o System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  



## <a name="windows-10-x86-x64-pro-and-enterprise"></a>Windows 10 (x86, x64): Pro e Enterprise  
**Servidores do sistema de sites:**  

-   Ponto de distribuição  

    -   Os pontos de distribuição neste sistema operativo não têm suporte para PXE.  

    -   Os pontos de distribuição nesta versão do sistema operativo não suportam Multicast.  

    -   Pontos de distribuição dão suporte a várias configurações diferentes que possuem requisitos diferentes. Em alguns casos, essas configurações dão suporte à instalação não somente em servidores, mas em sistemas operacionais cliente. Para obter mais informações sobre as opções que estão disponíveis para pontos de distribuição, consulte [gerenciar conteúda e infraestrutura de conteúdo para o System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

## <a name="windows-81-x86-x64-professional-and-enterprise"></a>Windows 8.1 (x86, x64): Professional e Enterprise  
**Servidores do sistema de sites:**  

-   Ponto de distribuição  

    -   Os pontos de distribuição neste sistema operativo não têm suporte para PXE.  

    -   Os pontos de distribuição nesta versão do sistema operativo não suportam Multicast.  

    -   Pontos de distribuição dão suporte a várias configurações diferentes que possuem requisitos diferentes. Em alguns casos, esses oferece suporte à instalação configuração não apenas em servidores, mas em sistemas operacionais cliente. Para obter mais informações sobre as opções que estão disponíveis para pontos de distribuição, consulte [gerenciar conteúda e infraestrutura de conteúdo para o System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

## <a name="windows-8-x86-x64-professional-and-enterprise"></a>Windows 8 (x86, x64): Professional e Enterprise
**Servidores do sistema de sites:**  

-   Ponto de distribuição  

    -   Os pontos de distribuição neste sistema operativo não têm suporte para PXE.  

    -   Os pontos de distribuição nesta versão do sistema operativo não suportam Multicast.  

    -   Pontos de distribuição dão suporte a várias configurações diferentes que possuem requisitos diferentes. Em alguns casos, essas configurações dão suporte à instalação não somente em servidores, mas em sistemas operacionais cliente. Para obter mais informações sobre as opções que estão disponíveis para pontos de distribuição, consulte [gerenciar conteúda e infraestrutura de conteúdo para o System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

## <a name="windows-7-with-sp1-x86-x64-professional-enterprise-and-ultimate"></a>Windows 7 com SP1 (x86, x64): Professional, Enterprise e Ultimate  
**Servidores do sistema de sites:**  

-   Ponto de distribuição  

    -   Os pontos de distribuição neste sistema operativo não têm suporte para PXE.  

    -   Os pontos de distribuição nesta versão do sistema operativo não suportam Multicast.  

    -   Pontos de distribuição dão suporte a várias configurações diferentes que possuem requisitos diferentes. Em alguns casos, essas configurações dão suporte à instalação não somente em servidores, mas em sistemas operacionais cliente. Para obter mais informações sobre as opções que estão disponíveis para pontos de distribuição, consulte [gerenciar conteúda e infraestrutura de conteúdo para o System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  


## <a name="the-server-core-installation-of-windows-server-2016"></a>A instalação do server core do Windows Server 2016
Começando com a versão 1606 com o pacote cumulativo de hotfix do KB3186654 (ou a versão de linha de base do 1606, que foi lançada em outubro de 2016) neste sistema operacional tem suporte para uso como uma distribuição ponto com as seguintes limitações:  
  -   Somente a versão de x64 bits tem suporte.
  -   Pontos de distribuição neste sistema operacional não dão suporte a PXE ou Multicast.  


## <a name="the-server-core-installation-of-windows-server-2012-r2"></a>A instalação Server Core do Windows Server 2012 R2  
 Além dos sistemas operacionais anteriores listadas, a instalação do server core do Windows Server 2012 R2 é suportada para uso como pontos de distribuição com as seguintes limitações:  

-   Somente a versão de x64 bits tem suporte.

-   Pontos de distribuição neste sistema operacional não dão suporte a PXE ou Multicast.  

## <a name="the-server-core-installation-of-windows-server-2012"></a>A instalação Server Core do Windows Server 2012  
 Além dos sistemas operacionais anteriores listadas, a instalação do server core do Windows Server 2012 também é suportada para uso como uma distribuição ponto com as seguintes limitações:  

-   Somente a versão de 64 bits tem suporte.  

-   Pontos de distribuição neste sistema operacional não dão suporte a PXE ou Multicast.

