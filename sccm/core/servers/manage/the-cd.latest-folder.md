---
title: A pasta CD.Latest
titleSuffix: Configuration Manager
description: Saiba mais sobre o processo que disponibiliza atualizações do produto a partir da consola do Configuration Manager.
ms.date: 03/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8db92d67-5d9c-4e9c-80d0-ae6fa0dd4817
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 70612d3f60802892aa99bbc4fc006b9385cb8756
ms.sourcegitcommit: af8693048e6706ffda72572374f56e0bc7dfce2c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/11/2019
ms.locfileid: "57737327"
---
# <a name="the-cdlatest-folder-for-configuration-manager"></a>O CD. Pasta mais recente do Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

O Configuration Manager possui um processo para fornecer atualizações para o produto a partir da consola do Configuration Manager. Para suportar este novo método de atualização do Configuration Manager, uma nova pasta é criada com o nome **CD. Mais recente**. Esta pasta contém uma cópia dos ficheiros de instalação do Configuration Manager para a versão atualizada do seu site.  

O CD. Pasta mais recente contém uma pasta denominada **Redist**, que contém os ficheiros redistribuíveis que o programa de configuração transfere e utiliza. Estes ficheiros correspondem à versão dos ficheiros do Configuration Manager localizados na pasta CD.Latest. Ao executar o programa de configuração a partir da pasta CD.Latest, tem de utilizar ficheiros que correspondem a essa versão do programa de configuração. Pode direta configuração para transferir ficheiros novos e atuais da Microsoft, ou configuração direta para utilizar os ficheiros da pasta Redist incluída no CD. Pasta mais recente.

Suporte de dados de linha de base não inclui um **Redist** pasta. O site não cria uma pasta Redist até que instale uma atualização na consola. Entretanto, utilize a pasta Redist que foi utilizado quando instalar sites a partir da mídia de linha de base.  

> [!TIP]  
> Certificar-se de que os ficheiros redistribuíveis que utilizar estão atualizados. Se ainda não acabou de baixar arquivos redistribuíveis, planeie permitir que a configuração para fazê-lo da Microsoft.   

Os seguintes cenários de criar ou atualizar o CD. Pasta mais recente num servidor de site primário ou site de administração central:  

- Quando instala uma atualização ou correção a partir da consola do Configuration Manager, o site cria ou atualiza a pasta na pasta de instalação do Configuration Manager.  

- Quando executar a tarefa de cópia de segurança do Configuration Manager incorporados, o site cria ou atualiza a pasta na localização de pasta designada de cópia de segurança.  

- Quando instala um site novo com o suporte de dados de linha de base, o site cria o CD. Pasta mais recente.


## <a name="supported-scenarios"></a>Cenários suportados

Os ficheiros de origem do CD. Pasta mais recentes são suportados para os seguintes cenários:  

### <a name="backup-and-recovery"></a>Cópia de segurança e recuperação
Para recuperar um site, utilize os ficheiros de origem a partir de um CD. Pasta mais recente que corresponda ao seu site. Quando executa uma cópia de segurança do site utilizando a tarefa de cópia de segurança incorporada do site, o CD. Pasta mais recente é incluída como parte da cópia de segurança.

- Quando reinstala um site como parte de uma recuperação de site, instala o site a partir do CD. Pasta mais recente incluída na sua cópia de segurança. Esta ação instala o site utilizando as versões de ficheiro que correspondem à sua cópia de segurança do site e base de dados do site.  

    - Se não tiver acesso o CD correto. Versão mais recente da pasta, obter o CD. Pasta mais recente com as versões de ficheiro correto, instalando um site num ambiente de laboratório. Em seguida, atualize esse site para corresponder à versão que pretende recuperar.  

    - Se não tiver o CD correto. Pasta mais recente e o respetivo conteúdo disponível, é possível recuperar um site. Nesta circunstância, terá de reinstalar o site.  

- Se não tiver um CD. Pasta mais recente, mas é necessário um site primário do trabalho subordinado ou um site de administração central, pode utilizar esse site como site de referência para uma recuperação de site.  

### <a name="install-a-child-primary-site"></a>Instalar um site primário subordinado
Quando deseja instalar um novo site primário subordinado abaixo de um site de administração central que tem instalado uma ou mais atualizações na consola, utilizar a configuração e os ficheiros de origem a partir do CD. Pasta mais recente a partir do site de administração central. Este processo utiliza ficheiros de origem de instalação que correspondem à versão do site de administração central. Para obter mais informações, consulte [utilizar o Assistente de configuração para instalar sites](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites).  

### <a name="expand-a-stand-alone-primary-site"></a>Expandir um site primário autónomo
Quando expande um site primário autónomo, instalando um novo site de administração central, utilize a configuração e os ficheiros de origem a partir do CD. Pasta mais recente do site primário. Este processo utiliza ficheiros de origem de instalação que correspondem à versão do site primário. Para obter mais informações, consulte [expandir um site primário autónomo](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#bkmk_expand).

### <a name="install-a-secondary-site"></a>Instalar um site secundário
<!-- SCCMDocs-pr issue #3164 --> Quando deseja instalar um novo site secundário abaixo de um site primário que tenha instalado uma ou mais atualizações na consola, utilize os ficheiros de origem a partir do CD. Pasta mais recente do site primário. 

Para obter mais informações, consulte [instala um site secundário](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#bkmk_secondary). 


## <a name="unsupported-scenarios"></a>Cenários não suportados

O CD atualizado. Ficheiros de origem mais recentes não são suportados para:  
   
- Instalar um novo site para uma nova hierarquia  
- Atualizar um site do Microsoft System Center 2012 Configuration Manager para System Center Configuration Manager, ramo atual
- Instalar clientes do Configuration Manager
- Instalar consolas do Configuration Manager

