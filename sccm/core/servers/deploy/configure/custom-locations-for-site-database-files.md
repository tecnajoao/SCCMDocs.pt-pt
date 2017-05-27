---
title: "Localizações de ficheiros de base de dados personalizado | Documentos do Microsoft"
description: "Saiba como especificar localizações personalizadas para ficheiros de base de dados do SQL Server."
ms.custom: na
ms.date: 10/06/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 500a9aa6-68aa-44eb-bf49-350c1314a697
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 5e5155aa8c03b7e0c200d083024c8fa386f97aa7
ms.openlocfilehash: cfac2c03c1b71b40c68d8acd5fbd96c5e98caaa9
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="custom-locations-for-system-center-configuration-manager-site-database-files"></a>Ficheiros de base de dados do site localizações personalizadas para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

 System Center Configuration Manager suporta localizações personalizadas para ficheiros de base de dados do SQL Server.  

> [!NOTE]  
>  A opção para especificar localizações de ficheiros não predefinidas não está disponível quando utiliza um cluster do SQL Server.  

 **Durante a configuração** de um novo site primário ou site de administração central, pode:  

-   **Especificar localizações de ficheiros não predefinidas para a base de dados do site**: Configuração do Configuration Manager, em seguida, cria a base de dados do site utilizando essas localizações.  

-   **Especifique a utilização de uma base de dados previamente criada do SQL Server que utilize localizações de ficheiros personalizadas**:  Em seguida, a configuração do Configuration Manager utiliza essa base de dados previamente criada e respetivas localizações de ficheiros pré-configurada.  

**Após a configuração**, pode alterar a localização dos ficheiros de base de dados do site. Isto requer que parar o site e editar a localização do ficheiro no SQL Server:  

-   No servidor do site do Configuration Manager, parar a **SMS_Executive** serviço.  

-   Utilize a documentação para a sua versão do SQL Server para ajudá-lo sobre como mover uma base de dados do utilizador. Por exemplo, se utilizar o SQL Server 2014, consulte o artigo [mover bases de dados de utilizador](https://technet.microsoft.com/library/ms345483\(v=sql.120\).aspx) na TechNet.  

-   Depois de concluir a mudança do ficheiro da base de dados, reinicie o **SMS_Executive** serviço no servidor do site do Configuration Manager.  

