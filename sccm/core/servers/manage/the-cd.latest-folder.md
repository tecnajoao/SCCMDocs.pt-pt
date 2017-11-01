---
title: A pasta CD.Latest
titleSuffix: Configuration Manager
description: "Saiba mais sobre o novo processo de atualização que disponibiliza atualizações do produto a partir do consola do Configuration Manager."
ms.custom: na
ms.date: 05/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8db92d67-5d9c-4e9c-80d0-ae6fa0dd4817
caps.latest.revision: "6"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 51120ecb681da4ac82fd98ef68405db8d462c5ec
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="the-cdlatest-folder-for-system-center-configuration-manager"></a>A pasta CD.Latest do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

System Center Configuration Manager apresenta um novo processo de atualização que disponibiliza atualizações do produto a partir do consola do Configuration Manager. Para suportar este novo método de atualização do Configuration Manager, é criada uma nova pasta com nome **CD. Mais recente** que contém uma cópia dos ficheiros de instalação do Configuration Manager para a versão atualizada do seu site.  

A partir da atualização 1606, a pasta CD.Latest contém uma pasta denominada **Redist** com os ficheiros redistribuíveis que o programa de configuração transfere e utiliza. Estes ficheiros correspondem à versão dos ficheiros do Configuration Manager localizados na pasta CD.Latest. Ao executar o programa de configuração a partir da pasta CD.Latest, tem de utilizar ficheiros que correspondem a essa versão do programa de configuração. Para tal, pode indicar ao programa de configuração para transferir ficheiros novos e atuais da Microsoft, ou indicar ao programa de configuração para utilizar os ficheiros da pasta Redist incluída na pasta CD.Latest.

No entanto, o suporte de dados de linha de base, incluindo a linha de base versão 1606 lançadas em Outubro de 2016, não inclui uma pasta de Redist. Não será possível criar a pasta de Redist até que instale uma atualização na consola. Entretanto, utilize a pasta de Redist que utilizou quando instalar sites a partir do suporte de dados de linha de base.  

> [!TIP]
> Se ainda não instalou a versão 1606, certifique-se de que os ficheiros redist utilizados são atuais. Se não tiver transferido ficheiros redist recentemente, planeie permitir que o programa de configuração o faça a partir da Microsoft.   

 Seguem-se alguns cenários que criam ou atualizam a pasta CD.Latest num site de administração central ou servidor de site primário:  

-   Instalar uma atualização ou correção a partir da consola do Configuration Manager: A pasta é criada ou atualizada na pasta de instalação do Configuration Manager.  

-   Execute a tarefa de cópia de segurança do Configuration Manager incorporados: A pasta é criada ou atualizada na localização de pasta designada de cópia de segurança.  

-  A partir da versão 1606, CD. Pasta mais recente é criada quando instala um novo site utilizar suportes de dados de linha de base (como a versão 1606 ou 1702).

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
