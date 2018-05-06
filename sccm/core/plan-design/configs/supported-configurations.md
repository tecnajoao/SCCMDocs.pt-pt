---
title: Configurações suportadas
titleSuffix: Configuration Manager
description: Identifica requisitos e configurações de chaves para que possa planear, implementar e manter uma implementação funcional do System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 45a10878-ff48-4318-9c6d-c014b38a4039
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: de769a24b44c5ab5e28035e96fef341aecd78006
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="supported-configurations-for-system-center-configuration-manager"></a>Configurações suportadas do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Como uma solução no local, o System Center Configuration Manager permite utilizar os servidores, clientes, configurações de rede e produtos adicionais, como o Microsoft Intune, o SQL Server e o Azure.

As informações neste e os tópicos seguintes são essenciais para ajudar a identificar configurações chave, os requisitos e limitações, para que pode planear, implementar e manter uma implementação funcional do Configuration Manager.  Esta informação é específica para a infraestrutura de sites do Configuration Manager, hierarquias e dispositivos geridos.

Quando uma funcionalidade do Configuration Manager ou a capacidade necessita de configurações mais específicas, essa informação está incluída com a documentação específica à funcionalidade, não sendo suplementar os detalhes de configuração mais geral.  

 Os produtos e tecnologias que são descritas nos tópicos seguintes são suportadas pelo Configuration Manager. No entanto, a sua inclusão neste conteúdo não implica uma extensão de suporte para qualquer produto além individuais desse produto vida de suporte. Os produtos que estejam fora do respetivo ciclo de vida de suporte não são suportados para utilização com o Configuration Manager. Para mais informações sobre os Ciclos de Vida do Suporte da Microsoft, aceda ao site [Ciclo de Vida do Suporte da Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=208270) .  

> [!NOTE]  
>  Para obter informações sobre a política de ciclo de vida do suporte da Microsoft, aceda ao site Microsoft suporta ciclo de vida suporta política FAQ em [FAQ de política de ciclo de vida de suporte Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=31976).  

 Além disso, os produtos e versões de produto que não estão listadas nos tópicos seguintes não são suportadas com o System Center Configuration Manager, a menos que tenham sido anunciados no [blogue Enterprise Mobility and Security](https://blogs.technet.microsoft.com/enterprisemobility/).  Por vezes, o conteúdo neste blogue precedida de uma atualização para esta corpo de documentação.


-  [Dimensionamento e números da escala](../../../core/plan-design/configs/size-and-scale-numbers.md)  
Saiba mais sobre quantos sites, funções de sistema de sites por site e os clientes ou dispositivos são suportadas em estruturas de outra hierarquia do Configuration Manager.

-  [Pré-requisitos do site e sistema de sites](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)  
Saiba mais sobre as configurações que são necessárias no Windows Server para suportar os diferentes tipos de site e funções de sistema de sites.

-  [Sistemas operativos suportados para servidores do sistema de sites](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  
Saiba mais sobre os sistemas operativos pode utilizar como um servidor do site ou servidor de sistema de sites.

-  [Sistemas operativos suportados por clientes e dispositivos](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)  
Saiba mais sobre os sistemas operativos que pode gerir com o Configuration Manager, incluindo Windows, Windows Embedded, Linux e UNIX, Mac e dispositivos móveis.

-  [Sistemas operativos suportados para a consola do](../../../core/plan-design/configs/supported-operating-systems-consoles.md)  
Saiba mais sobre os quais os sistemas operativos pode alojar a consola do Configuration Manager para fornecer um ponto de acesso para gerir a sua implementação.  

-  [Suporte para versões do SQL Server](../../../core/plan-design/configs/support-for-sql-server-versions.md)  
Saiba mais sobre as versões do SQL Server podem alojar a base de dados do site e base de dados de relatórios, bem como sobre as configurações necessárias e configurações opcionais que pode utilizar.

-  [Opções de elevada disponibilidade](../../../protect/understand/high-availability-options.md)  
Saiba mais sobre as opções que pode implementar ao conceber o seu ambiente para ajudar a manter um elevado nível de serviço disponível para implementação do Configuration Manager.

-  [Hardware recomendado](../../../core/plan-design/configs/recommended-hardware.md)  
Saiba mais sobre as diretrizes que podem ajudar a que identificar o hardware adequado e configurações para alojar os serviços de chaves e sites do Configuration Manager.

-  [Suporte para domínios do Active Directory](../../../core/plan-design/configs/support-for-active-directory-domains.md)  
Saiba mais sobre as configurações suportadas de domínio do Active Directory que o Configuration Manager requer e suporta.

-  [Suporte para funcionalidades e redes do Windows](../../../core/plan-design/configs/support-for-windows-features-and-networks.md)  
Saiba mais sobre tecnologias do Windows (por exemplo, a eliminação de duplicados de dados e do BranchCache) e limitações para utilização com o Gestor de configuração suportados.

-  [Suporte para ambientes de Virtualização](../../../core/plan-design/configs/support-for-virtualization-environments.md)  
Saiba mais sobre como utilizar tecnologias de máquina virtual suportadas.
