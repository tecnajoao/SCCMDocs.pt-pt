---
title: Suporte internacional
titleSuffix: Configuration Manager
description: Configure o System Center Configuration Manager para estar em conformidade com requisitos internacionais específicos.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 46dd9cb2-a812-4b6a-a747-b840f92fef8b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bce6abd57cd50ff19339c29b97bda165109b79b1
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="international-support-in-system-center-configuration-manager"></a>Suporte internacional no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

As secções seguintes fornecem detalhes técnicos para ajudar a tornar o System Center Configuration Manager em conformidade com requisitos internacionais específicos.  

## <a name="gb18030-requirements"></a>Requisitos da GB18030  
 O Configuration Manager cumprem as normas definidas na GB18030 para que possa utilizar o Configuration Manager na China. Uma implementação do Configuration Manager tem de ter as seguintes configurações para satisfazer os requisitos da GB18030:  

-   Cada computador do servidor do site e o computador SQL Server que utiliza com o Configuration Manager tem de utilizar um sistema operativo chinês.  

-   Cada base de dados do site e cada instância do SQL Server da hierarquia deve utilizar o mesmo agrupamento, e tem de ser um dos seguintes:  

    -   Chinese_Simplified_Pinyin_100_CI_AI  

    -   Chinese_Simplified_Stroke_Order_100_CI_AI  

    > [!NOTE]  
    >  Estes agrupamentos de base de dados são uma exceção aos requisitos que são apresentados nos [suporte para versões do SQL Server para o System Center Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md).  

-   Tem de colocar um ficheiro com o nome **GB18030.SMS** na pasta raiz do volume do sistema de cada computador do servidor do site da hierarquia. Este ficheiro não contém quaisquer dados e pode ser um ficheiro de texto vazio com um nome que satisfaça este requisito.  
