---
title: Suporte internacional | Documentos do Microsoft
description: "Configure o System Center Configuration Manager para estar em conformidade com requisitos internacionais específicos."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 46dd9cb2-a812-4b6a-a747-b840f92fef8b
caps.latest.revision: 6
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 40e018084dd2703327ff653f962f488432b1ec98
ms.openlocfilehash: 3bab51be96445f766e8f5bbf54eee854e5d09cee
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="international-support-in-system-center-configuration-manager"></a>Suporte internacional no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

As secções seguintes fornecem detalhes técnicos para ajudar a que o System Center Configuration Manager fique em conformidade com requisitos internacionais específicos.  

## <a name="gb18030-requirements"></a>Requisitos da GB18030  
 O Configuration Manager cumpre as normas definidas na GB18030 para que possa utilizar o Configuration Manager na China. Uma implementação do Configuration Manager tem de ter as seguintes configurações para satisfazer os requisitos da GB18030:  

-   Cada computador do servidor de site e o computador do SQL Server que utiliza com o Configuration Manager tem de utilizar um sistema operativo chinês.  

-   Cada base de dados do site e cada instância do SQL Server da hierarquia deve utilizar o mesmo agrupamento, e tem de ser um dos seguintes:  

    -   Chinese_Simplified_Pinyin_100_CI_AI  

    -   Chinese_Simplified_Stroke_Order_100_CI_AI  

    > [!NOTE]  
    >  Estes agrupamentos de base de dados são uma exceção aos requisitos que são descritas na [suporte para versões do SQL Server para o System Center Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md).  

-   Tem de colocar um ficheiro com o nome **GB18030.SMS** na pasta raiz do volume do sistema de cada computador do servidor do site da hierarquia. Este ficheiro não contém quaisquer dados e pode ser um ficheiro de texto vazio com um nome que satisfaça este requisito.  

