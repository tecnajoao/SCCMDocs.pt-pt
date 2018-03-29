---
title: A pasta CD.Latest
titleSuffix: Configuration Manager
description: Saiba mais sobre o novo processo de atualização que disponibiliza atualizações do produto a partir do consola do Configuration Manager.
ms.custom: na
ms.date: 03/28/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8db92d67-5d9c-4e9c-80d0-ae6fa0dd4817
caps.latest.revision: ''
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 86b6393a6719895357d34fe8e562f3d0c967ad06
ms.sourcegitcommit: 27da4be015f1496b7b89ebddb517a2685f1ecf74
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/28/2018
---
# <a name="the-cdlatest-folder-for-system-center-configuration-manager"></a>A pasta CD.Latest do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager apresenta um novo processo de atualização que disponibiliza atualizações do produto a partir do consola do Configuration Manager. Para suportar este novo método de atualização do Configuration Manager, é criada uma nova pasta com nome **CD. Mais recente** que contém uma cópia dos ficheiros de instalação do Configuration Manager para a versão atualizada do seu site.  

CD. Pasta mais recente contém uma pasta denominada **Redist** que contém os ficheiros que transfere e utiliza o programa de configuração. Estes ficheiros correspondem à versão dos ficheiros do Configuration Manager localizados na pasta CD.Latest. Ao executar o programa de configuração a partir da pasta CD.Latest, tem de utilizar ficheiros que correspondem a essa versão do programa de configuração. Para tal, pode indicar ao programa de configuração para transferir ficheiros novos e atuais da Microsoft, ou indicar ao programa de configuração para utilizar os ficheiros da pasta Redist incluída na pasta CD.Latest.

No entanto, o suporte de dados de linha de base, incluindo a versão de linha de base 1802 que lançada em Março de 2018, não inclui uma pasta de Redist. Não será possível criar a pasta de Redist até que instale uma atualização na consola. Entretanto, utilize a pasta de Redist que utilizou quando instalar sites a partir do suporte de dados de linha de base.  

> [!TIP]
> Certifique-se os ficheiros redistribuíveis que utilizar atuais. Se não tiver transferido os ficheiros redistribuíveis recentemente, planeie permitir que o programa de configuração para fazê-lo da Microsoft.   

 Seguem-se alguns cenários que criam ou atualizam a pasta CD.Latest num site de administração central ou servidor de site primário:  

-   Instalar uma atualização ou correção a partir da consola do Configuration Manager: A pasta é criada ou atualizada na pasta de instalação do Configuration Manager.  

-   Execute a tarefa de cópia de segurança do Configuration Manager incorporados: A pasta é criada ou atualizada na localização de pasta designada de cópia de segurança.  

-  CD. Pasta mais recente é criada quando instala um novo site utilizar suportes de dados de linha de base (como a versão 1802).

Os ficheiros de origem da pasta CD.Latest são suportadas para o seguinte:  

1.  **Cópia de segurança e recuperação:** Para recuperar um site, tem de utilizar os ficheiros de origem a partir de um CD. Pasta mais recente que corresponde ao seu site. Quando executa uma cópia de segurança do site utilizando a tarefa de cópia de segurança incorporada do site, CD. Pasta mais recente é incluída como parte da cópia de segurança.

    -   **Quando reinstala um site como parte de uma recuperação de site,** instala o site a partir da pasta CD.Latest incluída na sua cópia de segurança. Esta ação instala o site utilizando as versões de ficheiro que correspondem à sua cópia de segurança do site e à base de dados do site.  Se não tiver acesso CD correto. Versão mais recente da pasta, pode obter um CD. Pasta mais recente com as versões de ficheiro corretos ao instalar um site num ambiente de laboratório e, em seguida, atualizar esse site para corresponderem à versão que pretende recuperar.

        > [!IMPORTANT]  
        >  Se não tiver a pasta CD.Latest correta e o respetivo conteúdo disponível, não é possível recuperar um site e tem de ser reinstalado.  

    -   Se não tiver uma pasta CD.Latest, mas tiver um site primário subordinado ou um site de administração central em funcionamento, pode utilizar esse site como referência para uma recuperação do site.  

2.  **Para instalar um site primário subordinado:** Quando pretende instalar um novo site primário subordinado abaixo de um site de administração central que tem instalado uma ou mais atualizações na consola, tem de utilizar o programa de configuração e os ficheiros de origem a partir do CD. Pasta mais recente do site de administração central. Quando a Configuração é executada a partir de uma cópia da pasta CD.Latest a partir do site de administração central, utiliza ficheiros de origem de instalação que correspondem à versão do site de administração central. Para mais informações consulte [Utilizar o Assistente de Configuração para instalar sites](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md).  

3.  **Para expandir um site primário autónomo:** Quando está a expandir um site primário autónomo, instalando um novo site de administração central, tem de utilizar o programa de configuração e os ficheiros de origem a partir do CD. Pasta mais recente do site primário para instalar o novo site de administração central. Quando executa a partir de uma cópia da pasta CD.Latest a partir do site primário, utiliza ficheiros de origem de instalação que correspondem à versão do site primário. Para obter mais informações, consulte [Expandir um site primário autónomo](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand)) no tópico [Utilizar o Assistente de Configuração para instalar sites](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md)

> [!IMPORTANT]  
>  Os ficheiros de origem CD.Latest atualizados não são suportados para:  
>   
>  -   Instalar um novo site para uma nova hierarquia  
>  -   Atualizar um site do Microsoft System Center 2012 Configuration Manager para o System Center Configuration Manager
>  -   Instalar o cliente do Configuration Manager
>  -   Instalar a consola de administração do Configuration Manager

