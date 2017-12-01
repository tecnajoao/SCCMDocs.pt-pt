---
title: "Noções básicas de sites e hierarquias"
titleSuffix: Configuration Manager
description: "Obter informações básicas sobre o System Center Configuration Manager sites e hierarquias."
ms.custom: na
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4db1e15f-e832-4cf9-be33-d3971e635a55
caps.latest.revision: "6"
author: aaroncz
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 3e1cd18a3791b6ad009ca21851bb7173f8510f71
ms.sourcegitcommit: 7fe45ff75f05f7cc03ad021db8119791abe18049
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/01/2017
---
# <a name="fundamentals-of-sites-and-hierarchies-for-system-center-configuration-manager"></a>Noções básicas sobre sites e hierarquias do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Uma implementação do System Center Configuration Manager tem de ser instalada num domínio do Active Directory. A base desta implementação inclui um ou mais sites do Configuration Manager que formam uma hierarquia de sites. Desde um único site a uma hierarquia de vários sites, o tipo e a localização dos sites que instala proporcionam a capacidade de aumentar verticalmente a implementação quando necessário, bem como fornecer serviços principais a utilizadores e dispositivos geridos.

## <a name="hierarchies-of-sites"></a>Hierarquias de sites
Quando instalar o System Center Configuration Manager pela primeira vez, o primeiro site do Configuration Manager que instalar determina o âmbito da sua hierarquia. O primeiro site do Configuration Manager é o alicerce partir do qual irá gerir dispositivos e utilizadores na sua empresa. Este primeiro site tem de ser um site de administração central ou um site primário autónomo.  

 A *site de administração central* é adequado para implementações em larga escala, fornece um ponto central de administração e fornece a flexibilidade para suportar dispositivos que estão distribuídos numa infraestrutura de rede global. Depois de instalar um site de administração central, terá de instalar um ou mais sites primários como sites subordinados. Esta configuração é necessária porque o site de administração central não suporta diretamente a gestão de dispositivos, que é a função de um site primário. Um site de administração central suporta vários sites primários subordinados. Os sites primários subordinados são utilizados para gerir dispositivos diretamente e controlar a largura de banda de rede quando os dispositivos geridos se encontram em localizações geográficas diferentes.  

 A *site primário autónomo* é adequado para implementações mais pequenas e pode ser utilizado para gerir dispositivos sem ter de instalar sites adicionais. Embora um site primário autónomo pode limitar o tamanho da sua implementação, suporta um cenário para expandir a hierarquia mais tarde instalando um novo site de administração central. Com este cenário de expansão do site, o site primário autónomo passa a ser um site primário subordinado e, em seguida, pode instalar sites primários subordinados adicionais abaixo do novo site de administração central. Em seguida, pode expandir a implementação inicial para o crescimento futuro da sua empresa.  

> [!TIP]  
>  Um site primário autónomo e um site primário subordinado são, de facto o mesmo tipo de site: um site primário. A diferença no nome baseia-se na relação hierárquica que é criada quando utiliza também um site de administração central. Esta relação hierárquica também pode limitar a instalação de determinadas funções de sistema de sites que expandem a funcionalidade do Configuration Manager. Esta limitação das funções ocorre porque determinadas funções de sistema de sites apenas podem ser instaladas num site de nível superior da hierarquia, um site de administração central ou um site primário autónomo.  

 Depois de instalar o primeiro site, pode instalar sites adicionais. Se o primeiro site era um site de administração central, em seguida, pode instalar um ou mais sites primários subordinados. Depois de instalar um site primário (autónomo ou principal subordinado), em seguida, pode instalar um ou mais sites secundários.  

 Um *site secundário* só pode ser instalado como site subordinado abaixo de um site primário. Este tipo de sites aumentam o alcance de um site primário para gerir dispositivos em locais com ligação de rede lenta ao site primário. Apesar de um site secundário expande o site primário, o site primário gere todos os clientes. O site secundário fornece suporte para dispositivos na localização remota. Fornece suporte através da compressão e, em seguida, gerir a transferência de informações através da rede que envia (implementa) para clientes, e que os clientes enviam para o site.  

 Os diagramas seguintes mostram alguns exemplos de estruturas de sites.  

 ![Exemplos de hierarquia](media/Hierarchy_examples.png)  

 Para obter mais informações, consulte os tópicos seguintes:  

-   [Introdução ao System Center Configuration Manager](../../core/understand/introduction.md)  

-   [Estruturar uma hierarquia de sites para o System Center Configuration Manager](../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md)  

-   [Instalar sites do System Center Configuration Manager](/sccm/core/servers/deploy/install/installing-sites)  

## <a name="site-system-servers-and-site-system-roles"></a>Servidores do sistema de sites e funções do sistema de sites  
 Cada site do Configuration Manager instala *funções do sistema de sites* que suporte operações de gestão. As seguintes funções são instaladas por predefinição quando instala um site:

-   A função de servidor do site é atribuída ao computador onde instalou o site.

-   A função de servidor de base de dados do site é atribuída ao SQL Server que aloja a base de dados do site.

Outras funções de sistema de sites são opcionais e são apenas utilizadas quando pretende utilizar as funcionalidades que estão ativa na função de sistema de sites. Qualquer computador que aloje uma função de sistema de sites é referido como um servidor de sistema de sites.  

 Para uma implementação mais pequena do Configuration Manager, poderá executar inicialmente todas do seu site as funções do sistema diretamente no computador do servidor do site. Em seguida, como o ambiente gerido e as necessidades aumentam, pode instalar servidores do sistema de sites adicionais para alojar funções do sistema de sites adicionais para melhorar a eficiência do site no fornecimento de serviços para mais dispositivos.  

 Para obter informações sobre as funções de sistema de sites diferentes, consulte [funções do sistema de sites](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles) no [planear servidores de sistema de sites e funções de sistema de sites para o System Center Configuration Manager](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).

## <a name="publishing-site-information-to-active-directory-domain-services"></a>Publicação de informações de sites nos Serviços de Domínio do Active Directory  
 Para simplificar a gestão do Configuration Manager, pode expandir o esquema do Active Directory para suportar os detalhes que são utilizados pelo Configuration Manager e, em seguida, tiver sites publiquem as respetivas informações chaves nos serviços de domínio do Active Directory (AD DS). Em seguida, os computadores que pretende gerir podem obter de forma segura informações relacionadas com o site de origem fidedigna dos AD DS. As informações que os clientes podem obter identificam sites disponíveis, servidores do sistema de sites e os serviços que esses servidores de sistema de sites fornecem.  

 *Expandir o esquema do Active Directory* é efetuado apenas uma vez para cada floresta e pode ser efetuado antes ou depois de instalar o Configuration Manager.   Quando expande o esquema, tem de criar um novo contentor do Active Directory com o nome de gestão do sistema em cada domínio. O contentor contém um site do Configuration Manager que irá publicar dados para os clientes localizarem. Para obter mais informações, consulte [preparar um Active Directory para publicação de site](../../core/plan-design/network/extend-the-active-directory-schema.md).  

 *Publicar dados do site* melhora a segurança da sua hierarquia do Configuration Manager e reduz a sobrecarga administrativa, mas não é necessário para funcionalidades básicas do Configuration Manager.  
