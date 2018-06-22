---
title: Configure a publicação de DNS de pontos de gestão de encontrar clientes
titleSuffix: Configuration Manager
description: Definir os computadores cliente para localizar pontos de gestão utilizando a publicação de DNS no System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 03cec407-0f9f-454f-a360-b005af738d29
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3735e2cc8ac2f7e4a5c05b49783cad3981a04930
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32333839"
---
# <a name="how-to-configure-client-computers-to-find-management-points-by-using-dns-publishing-in-system-center-configuration-manager"></a>Como configurar computadores cliente para localizar pontos de gestão utilizando a publicação de DNS no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Os clientes no System Center Configuration Manager tem de localizar um ponto de gestão para concluir a atribuição de site e como processo contínuo para continuam a ser geridos. Os Serviços de Domínio do Active Directory fornecem o método mais seguro para que os clientes da intranet consigam localizar pontos de gestão. Porém, se os clientes não puderem utilizar este método de localização do serviço (por exemplo, não expandiu o esquema do Active Directory ou os clientes pertencem a um grupo de trabalho), utilize a publicação de DNS como método de localização do serviço alternativo preferido.  

> [!NOTE]  
>  Quando instala o cliente no Linux e UNIX, tem de especificar um ponto de gestão para utilizar como um ponto inicial de contacto. Para obter informações sobre como instalar o cliente para Linux e UNIX, consulte [como implementar clientes em servidores UNIX e Linux no System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

 Antes de utilizar a publicação de DNS em pontos de gestão, certifique-se de que os servidores DNS da intranet possuem registos de recursos de localização do serviço (SRV RR) e registos de recursos de anfitrião correspondente (A ou AAA) para os pontos de gestão do site. Os registos de recursos de localização de serviço podem ser criados automaticamente pelo Configuration Manager ou manualmente pelo administrador de DNS responsável pela criação de registos no DNS.  

 Para obter mais informações sobre a publicação de DNS como método de localização de serviço para clientes do Configuration Manager, consulte [compreender a forma como os clientes localizam os recursos de site e os serviços do System Center Configuration Manager](../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

 Por predefinição, os clientes procuram o DNS para pontos de gestão no respetivo domínio de DNS. No entanto, se existirem pontos de gestão publicados no domínio dos clientes, tem de configurar manualmente os clientes com o sufixo DNS de ponto de gestão. Pode configurar este sufixo DNS nos clientes durante ou após a instalação do cliente:  

-   Para configurar os clientes com um sufixo de ponto de gestão durante a instalação do cliente, configure as propriedades do CCMSetup Client.msi.  

-   Para configurar os clientes com um sufixo de ponto de gestão após a instalação do cliente, no Painel de Controlo, configure as **Propriedades do Configuration Manager**.  

#### <a name="to-configure-clients-for-a-management-point-suffix-during-client-installation"></a>Para configurar os clientes com um sufixo de ponto de gestão durante a instalação do cliente  

-   Instale o cliente com a seguinte propriedade do CCMSetup Client.msi:  

    -   **DNSSUFFIX =**  *&lt;domínio de ponto de gestão\>*  

         Se o site tiver mais que um ponto de gestão e estes estiverem em mais de um domínio, especifique apenas um domínio. Quando os clientes estabelecem ligação a um ponto de gestão deste domínio, transferem uma lista de pontos de gestão disponíveis que inclui os pontos de gestão de outros domínios.  

     Para obter mais informações sobre as propriedades de linha de comandos do CCMSetup, consulte [acerca das propriedades de instalação de cliente no System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

#### <a name="to-configure-clients-for-a-management-point-suffix-after-client-installation"></a>Para configurar os clientes com um sufixo de ponto de gestão após a instalação do cliente  

1.  No Painel de Controlo do computador cliente, aceda a **Configuration Manager**e faça duplo clique em **Propriedades**.  

2.  No separador **Site** , especifique o sufixo DNS de um ponto de gestão e clique em **OK**.  

     Se o site tiver mais que um ponto de gestão e estes estiverem em mais de um domínio, especifique apenas um domínio. Quando os clientes estabelecem ligação a um ponto de gestão deste domínio, transferem uma lista de pontos de gestão disponíveis que inclui os pontos de gestão de outros domínios.
