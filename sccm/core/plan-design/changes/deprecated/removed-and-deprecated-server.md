---
title: Preterido para servidores de site do Configuration Manager
titleSuffix: Configuration Manager
description: Saiba mais sobre os produtos e sistemas operativos que já não suporta System Center Configuration Manager para os servidores de site.
ms.date: 01/25/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d53ac075-438b-41da-ab85-42f33982da0c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b92eb8083ce886fcab4d9957b2a79999d72a1a5a
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="removed-and-deprecated-for-system-center-configuration-manager-site-servers"></a>Removidas e preteridas para servidores de site do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo descreve os produtos e sistemas operativos que são removidos do suporte para servidores de site do System Center Configuration Manager ou serão removidos numa futura atualização (preterida). Este artigo fornece aviso antecipado sobre futuras alterações que podem afetar a utilização do Configuration Manager.  

Esta informação está sujeita a alterações em versões futuras e não pode incluir cada funcionalidades preteridas, produtos ou sistema operativo.  


## <a name="deprecated-server-operating-systems"></a>Sistemas operativos de servidor preterido  

|**Sistemas operativos**|**Preterição anunciada pela primeira vez**|**Suporte removido** |  
|-|-|-| 
|Windows Server 2008 R2|10 de Julho de 2015| Versão 1702 (ver nota 1)| 
|Windows Server 2008|10 de Julho de 2015|Versão 1511 </br></br>Suporta como um sistema de sites é removido. (Ver nota 2).|  

>[!NOTE]
>-   A partir da versão 1702, Windows Server 2008 R2 não é suportado para servidores de site ou a maioria das funções de sistema de sites. No entanto, as versões anteriores 1702 continuam suportar a sua utilização. Este sistema operativo continua a ser suportado para a função de sistema de sites de ponto de distribuição (incluindo pontos de distribuição de extração e para PXE e multicast), até que a desaprovação de suporte é anunciada ou o sistema operativo expandido período de suporte expira. A partir da versão 1602, pode direta atualizar o sistema operativo de um servidor de site do Windows Server 2008 R2 para o Windows Server 2012 R2.  
>- Para obter mais informações sobre a atualização no local de um sistema de operativo de servidores de site, consulte o [direta atualizar o sistema operativo de servidores de sites que executam o Windows Server 2008 R2](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#bkmk_from2008r2) secção [atualizar no local infraestrutura que suporta o System Center Configuration Manager](/sccm/core/servers/manage/upgrade-on-premises-infrastructure).

>[!NOTE]
>-   Windows Server 2008 não é suportado para servidores de site ou funções de sistema de sites, exceto para o ponto de distribuição e ponto de distribuição de solicitação. Pode continuar a utilizar este sistema operativo como um ponto de distribuição, até que a desaprovação de suporte é anunciada ou o período de suporte alargado do sistema operativo expira. Para obter mais informações, consulte [instalação do System Center Configuration Manager CB e LTSB falha no Windows Server 2008](https://support.microsoft.com/help/4015095).

## <a name="deprecated-support-for-sql-server-versions-as-a-site-database"></a>Suporte preterido para versões do SQL Server como uma base de dados do site  

|**Versões do SQL Server**|**Preterição anunciada pela primeira vez**|**Suporte removido**|   
|-|-|-| 
|SQL Server 2008 R2|10 de Julho de 2015|Versão 1702| 
|SQL Server 2008|10 de Julho de 2015|Versão 1511|  


Se precisar de atualizar a sua versão do SQL Server, recomendamos os seguintes métodos, de fácil mais complexas.
1. [Atualizar o SQL Server no local](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#a-namebkmksupconfigupgradedbsrva-upgrade-sql-server-on-the-site-database-server) (recomendado).
2. Instale uma nova versão do SQL Server num novo computador. Em seguida, [utilizar a opção de mover a base de dados](/sccm/core/servers/manage/modify-your-infrastructure#a-namebkmkdbconfiga-modify-the-site-database-configuration) de configuração do Configuration Manager para apontar o servidor do site para o novo SQL Server.
3. Utilize [cópia de segurança e recuperação](/sccm/protect/understand/backup-and-recovery).


## <a name="more-information"></a>Mais informações
Para obter mais informações, consulte:
 - [Removidas e preteridas](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated)
 - O [ciclo de vida de suporte de Microsoft](https://support.microsoft.com/lifecycle) Web site.
 - [Suporte para versões de ramo atual do Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported).