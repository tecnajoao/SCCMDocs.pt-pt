---
title: Planear a base de dados do site | Microsoft Docs
description: "Considere a base de dados do site e a função de servidor de base de dados do site quando planear a hierarquia do System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 104fb4cc-6e83-40a3-8e6b-ac909fb9ec7d
caps.latest.revision: "5"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: d4efe1f013dbb74efca79cd27f7248fc085c7424
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="plan-for-the-site-database-for-system-center-configuration-manager"></a>Planear a base de dados do site para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O servidor de base de dados do site é um computador que executa uma versão suportada do Microsoft SQL Server. SQL Server é utilizada para armazenar informações de sites do Configuration Manager. Cada site numa hierarquia do Configuration Manager contém uma base de dados do site e um servidor que está atribuído a função de servidor de base de dados do site.  

-   Para sites de administração central e sites primários, pode instalar o SQL Server no servidor do site ou pode instalar o SQL Server num computador diferente do servidor do site.  

-   Para sites secundários, pode utilizar o SQL Server Express em vez de uma instalação completa do SQL Server. O servidor de base de dados tem de, no entanto, a ser executado no servidor do site secundário.  

As seguintes configurações do SQL Server podem ser utilizadas para alojar a base de dados do site:  

-   A instância predefinida do SQL Server  

-   Uma instância nomeada num único computador com o SQL Server  

-   Uma instância nomeada numa instância em cluster do SQL Server  

-   Um grupo de Disponibilidade AlwaysOn do SQL Server (início com a versão 1602 do System Center Configuration Manager)


Para alojar a base de dados do site, o SQL Server tem de cumprir os requisitos detalhados em [suporte para versões do SQL Server para o System Center Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md).  



## <a name="remote-database-server-location-considerations"></a>Considerações de localização do servidor de base de dados remota  

Se utilizar um computador de servidor de base de dados remota, certifique-se de que a ligação de rede intervenientes é uma ligação de rede de elevada disponibilidade, a largura de banda alta. O servidor do site e algumas funções de sistema de sites têm de comunicar constantemente com o servidor remoto que está a alojar a base de dados do site.

-   A quantidade de largura de banda necessária para as comunicações com o servidor de base de dados depende de uma combinação de muitas configurações de site e cliente diferentes. Por conseguinte, a largura de banda realmente necessária não é possível prever exatamente.  

-   O número de computadores a executar o fornecedor de SMS e a ligar à base de dados do site aumenta os requisitos de largura de banda da rede.  

-   O computador que executa o SQL Server tem de estar localizado num domínio que tenha uma fidedignidade bidirecional com o servidor de site e todos os computadores com o fornecedor de SMS.  

-   Não é possível utilizar um SQL Server agrupado para o servidor de base de dados do site se a base de dados do site estiver localizada conjuntamente com o servidor do site.  


Normalmente, um servidor de sistema de sites suporta funções de sistema de sites de apenas um único site do Configuration Manager. No entanto, pode utilizar várias instâncias do SQL Server, em servidores agrupados ou não em cluster, com o SQL Server para alojar uma base de dados de diferentes sites do Configuration Manager. Para suportar bases de dados de diferentes sites, é necessário configurar cada instância do SQL Server para utilizar portas exclusivas para a comunicação.  
