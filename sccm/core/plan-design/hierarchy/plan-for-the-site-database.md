---
title: Planear a base de dados do site
titleSuffix: Configuration Manager
description: Considere a base de dados do site e a função de servidor de base de dados do site quando planear a hierarquia do System Center Configuration Manager.
ms.date: 03/08/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 104fb4cc-6e83-40a3-8e6b-ac909fb9ec7d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0c9134fa0bbabf5425ce17d21b143d71437aea36
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56136386"
---
# <a name="plan-for-the-site-database-for-system-center-configuration-manager"></a>Planear a base de dados do site para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O servidor de base de dados do site é um computador que executa uma versão suportada do Microsoft SQL Server. SQL Server é utilizado para armazenar informações de sites do Configuration Manager. Cada site numa hierarquia do Configuration Manager contém uma base de dados do site e um servidor que está atribuído a função de servidor de base de dados do site.  

-   Para sites de administração central e sites primários, pode instalar o SQL Server no servidor do site ou instalar o SQL Server num computador diferente do servidor do site.  

-   Para sites secundários, pode utilizar a SQL Server Express em vez de uma instalação completa do SQL Server. O servidor de base de dados tem de, no entanto, a ser executado no servidor do site secundário.  

-  Para o grupo de disponibilidade SQL o modelo de recuperação de base de dados de utilização tem de ser definida como FULL  

-  Para não - grupo de disponibilidade SQL o modelo de recuperação de base de dados de utilização tem de ser definida para simples  

Mais informações sobre os modos de recuperação do SQL podem ser encontradas no [modelos de recuperação (SQL Server)](https://docs.microsoft.com/sql/relational-databases/backup-restore/recovery-models-sql-server).

As seguintes configurações do SQL Server podem ser utilizadas para alojar a base de dados do site:  

-   A instância predefinida do SQL Server  

-   Uma instância nomeada num único computador com o SQL Server  

-   Uma instância nomeada numa instância em cluster do SQL Server  

-   Um grupo de Disponibilidade AlwaysOn do SQL Server (desde a versão 1602 do System Center Configuration Manager)


Para alojar a base de dados do site, o SQL Server tem de cumprir os requisitos detalhados em [suporte para versões do SQL Server para o System Center Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md).  



## <a name="remote-database-server-location-considerations"></a>Considerações de local do servidor de base de dados remota  

Se utilizar um computador de servidor de base de dados remota, certifique-se de que a ligação de rede interveniente é uma ligação de rede de elevada disponibilidade, a largura de banda alta. O servidor do site e algumas funções de sistema de sites têm de comunicar constantemente com o servidor remoto que está a alojar a base de dados do site.

-   A quantidade de largura de banda necessária para as comunicações com o servidor de base de dados depende de uma combinação de muitas configurações de site e cliente diferentes. Por conseguinte, a largura de banda real necessária não é possível prever exatamente.  

-   O número de computadores a executar o fornecedor de SMS e a ligar à base de dados do site aumenta os requisitos de largura de banda da rede.  

-   O computador que executa o SQL Server tem de estar localizado num domínio que tenha uma fidedignidade bidirecional com o servidor de site e todos os computadores com o fornecedor de SMS.  

-   Não é possível utilizar um SQL Server agrupado para o servidor de base de dados do site se a base de dados do site estiver localizada conjuntamente com o servidor do site.  


Normalmente, um servidor de sistema de sites suporta funções de sistema de sites de apenas um único site do Configuration Manager. No entanto, pode utilizar várias instâncias do SQL Server, em servidores em cluster ou não agrupados a executar o SQL Server, para alojar uma base de dados de diferentes sites do Configuration Manager. Para suportar bases de dados de diferentes sites, é necessário configurar cada instância do SQL Server para utilizar portas exclusivas para a comunicação.  
