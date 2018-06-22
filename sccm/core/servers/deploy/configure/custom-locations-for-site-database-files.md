---
title: Localizações de ficheiros de base de dados personalizada
titleSuffix: Configuration Manager
description: Saiba como especificar localizações personalizadas para ficheiros de base de dados do SQL Server.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 500a9aa6-68aa-44eb-bf49-350c1314a697
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 597ce060dc1fb37f1cc827da3e1c059958a91163
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32332734"
---
# <a name="custom-locations-for-system-center-configuration-manager-site-database-files"></a>Ficheiros de base de dados do site localizações personalizadas para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

 System Center Configuration Manager suporta localizações personalizadas para ficheiros de base de dados do SQL Server.  

> [!NOTE]  
>  A opção para especificar localizações de ficheiros não predefinidas não está disponível quando utiliza um cluster do SQL Server.  

 **Durante a configuração** de um novo site primário ou site de administração central, pode:  

-   **Especifique localizações de ficheiros não predefinidas para a base de dados do site**: Configuração do Configuration Manager, em seguida, cria a base de dados do site utilizando essas localizações.  

-   **Especifique a utilização de uma base de dados do SQL Server previamente criada que utilize localizações de ficheiros personalizadas**:  Configuração do Configuration Manager, em seguida, utiliza essa base de dados previamente criada e respetivas localizações de ficheiros pré-configurada.  

**Após a configuração**, pode alterar a localização dos ficheiros de base de dados do site. Isto requer que pare o site e edite a localização do ficheiro no SQL Server:  

-   No servidor do site do Configuration Manager, pare o **SMS_Executive** serviço.  

-   Utilize a documentação para a sua versão do SQL Server para ajudá-lo sobre como mover uma base de dados do utilizador. Por exemplo, se utilizar o SQL Server 2014, consulte o artigo [mover bases de dados de utilizador](https://technet.microsoft.com/library/ms345483\(v=sql.120\).aspx) no TechNet.  

-   Depois de concluir a mudança do ficheiro de base de dados, reinicie o **SMS_Executive** serviço no servidor do site do Configuration Manager.  
