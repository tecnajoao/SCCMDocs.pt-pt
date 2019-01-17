---
title: Preteridos para servidores do site
titleSuffix: Configuration Manager
description: Saiba mais sobre os produtos e sistemas operativos que o Configuration Manager já não suporta servidores de sites.
ms.date: 01/15/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d53ac075-438b-41da-ab85-42f33982da0c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c8ea24e141d0e01512ed81ca96e88f2f0f2d07bc
ms.sourcegitcommit: d5c013a29f53b975fe3a6cb0a41f1e817bd7b235
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/16/2019
ms.locfileid: "54342725"
---
# <a name="removed-and-deprecated-for-configuration-manager-site-servers"></a>Removidos e preteridos para servidores de site do Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo descreve os produtos e sistemas operativos que são removidos do suporte para servidores de site do Configuration Manager ou serão removidos numa futura atualização (preterida). Ele fornece um aviso antecipado sobre futuras alterações que pode afetar a utilização do Configuration Manager.  

Estas informações podem ser alterados no futuro. Não pode incluir cada funcionalidade despromovida, produto ou sistema operativo.  



## <a name="server-os"></a>SO do servidor  

|**Sistemas operativos**|**Preterição anunciada pela primeira vez**|**Suporte removido** |  
|-|-|-| 
|Windows Server 2008 R2 com SP1|10 de Julho de 2015| Versão 1702 <sup> [observe 1](#bkmk_note1)</sup>| 
|Windows Server 2008 com SP2|10 de Julho de 2015|Versão 1511 <sup> [observe 2](#bkmk_note2)</sup>|  

#### <a name="bkmk_note1"></a> Nota 1: Windows Server 2008 R2 com SP1
Windows Server 2008 R2 com Service Pack 1 não é suportado para servidores do site ou a maioria das funções de sistema de sites. Esse SO ainda é suportado para a função de ponto de distribuição. Este suporte inclui pontos de distribuição de extração, PXE e multicast. 

> [!Important]  
> A data de fim do suporte alargado para o Windows Server 2008 R2 com SP1 é a 14 de Janeiro de 2020. Após esta data, Configuration Manager não suporta este sistema operacional como qualquer função de sistema de sites. 

Pode atualizar o SO do servidor do site do Windows Server 2008 R2 para Windows Server 2012 R2. Para obter mais informações, consulte [in-loco atualizar o sistema operativo de servidores de sites que executam o Windows Server 2008 R2](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#bkmk_from2008r2).  


#### <a name="bkmk_note2"></a> Nota 2: Windows Server 2008 com SP2
Windows Server 2008 com Service Pack 2 não é suportado para servidores do site ou a maioria das funções de sistema de sites. Esse SO ainda é suportado para a função de ponto de distribuição. Este suporte inclui pontos de distribuição de extração, PXE e multicast. 

> [!Important]  
> A data de fim do suporte alargado para o Windows Server 2008 com SP2 é 14 de Janeiro de 2020. Após esta data, Configuration Manager não suporta este sistema operacional como qualquer função de sistema de sites.  



## <a name="sql-server"></a>SQL Server   

|**Versões do SQL Server**|**Preterição anunciada pela primeira vez**|**Suporte removido**|   
|-|-|-| 
|SQL Server 2008 R2|10 de Julho de 2015|Versão 1702| 
|SQL Server 2008|10 de Julho de 2015|Versão 1511|  


Se precisar de atualizar a sua versão do SQL Server, recomendamos os seguintes métodos, de fácil mais complexas:

1. [Atualizar o SQL Server no local](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#a-namebkmksupconfigupgradedbsrva-upgrade-sql-server-on-the-site-database-server) (recomendado).  

2. Instale uma nova versão do SQL Server num novo computador. Em seguida, para apontar o seu servidor do site para o novo SQL Server [utilize a opção de mover base de dados](/sccm/core/servers/manage/modify-your-infrastructure#a-namebkmkdbconfiga-modify-the-site-database-configuration) de configuração do Configuration Manager.  

3. Uso [cópia de segurança e recuperação](/sccm/protect/understand/backup-and-recovery).  



## <a name="more-information"></a>Mais informações

Para obter mais informações, veja os artigos seguintes: 

- [Removidas e preteridas](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated)  

- [Ciclo de vida do suporte da Microsoft](https://support.microsoft.com/lifecycle)  

- [Suporte para versões de ramo atual do Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported)  

