---
title: "Importar dados de configuração | Microsoft Docs"
description: "Importar dados de configuração se tem contidas num formato de ficheiro cab e respeita o esquema de Service Modeling Language suportado."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 309b9a09-a611-4ba2-90ab-dde51582cf87
caps.latest.revision: "6"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 60d0642618a3074fc50a848f1189f4d6559ca916
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="import-configuration-data-with-system-center-configuration-manager"></a>Importar dados de configuração com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Para além de criar linhas de base de configuração e itens de configuração na consola do System Center Configuration Manager, pode importar a configuração de dados se faz é um ficheiro CAB (. cab) formato de ficheiro e em conformidade com o esquema de Service Modeling Language (SML) suportado. Pode importar dados de configuração a partir de:  

-   Dados de configuração de melhores práticas (Pacotes de Configuração) transferidos da Microsoft ou de outros sites de fornecedores de software.  

-   Dados de configuração que foi exportados a partir do System Center 2012 Configuration Manager e mais tarde.  

-   Dados de configuração criados externamente e em conformidade com o esquema SML.  

 Para obter um exemplo de Pacote de Configuração que ajude a gerir a conformidade para funções de servidor de site do System Center 2012 Configuration Manager, consulte [Pacote de Configuração do System Center 2012 Configuration Manager](http://www.microsoft.com/en-us/download/details.aspx?id=30710&WT.mc_id=rss_alldownloads_all).  

Quando importar uma linha de base de configuração, alguns ou todos os itens de configuração referenciados na linha de base de configuração também podem ser incluídos no ficheiro CAB. Durante o processo de importação, o Configuration Manager verifica se todos os itens de configuração que são referenciados na linha de base de configuração também estão incluídos no ficheiro cab ou já existem no site do Configuration Manager. O processo de importação falha se tentar importar uma linha de base de configuração que referencia dados de configuração do Configuration Manager não é possível localizar.  

Outros cenários em que o processo de importação poderá falhar incluem os seguintes:  

-   Os dados de configuração referenciam dados de configuração que não é possível localizar o Configuration Manager, na base de dados ou no próprio ficheiro CAB.  

-   Os dados de configuração já estão presentes na base de dados do Configuration Manager com o mesmo nome e versão de dados de configuração, mas a versão do conteúdo é diferente.  

-   Os dados de configuração já estão presentes na base de dados do Configuration Manager com a mesma versão de conteúdo, mas o cálculo de hash identifica-o como sendo diferente.  

-   Uma versão mais recente dos dados de configuração com o mesmo nome já está presente ou foi recentemente eliminada na base de dados do Configuration Manager.  

-   Numa hierarquia do Configuration Manager vários sites, os dados de configuração importados originalmente de um site principal. Tem de atualizá-los a partir do mesmo site e não de um site subordinado.  

### <a name="import-configuration-data"></a>Importar dados de configuração  

1.  Na consola do Configuration Manager, clique em **ativos e compatibilidade** > **itens de configuração** ou **linhas de base de configuração**
2.  No **home page** separador o **criar** , clique em **importar dados de configuração**.  
3.  Na página **Selecionar Ficheiros** do **Assistente de Importação de Dados de Configuração**, clique em **Adicionar**e, na caixa de diálogo **Abrir** , selecione os ficheiros .cab que pretende importar.  
4.  Selecione o **criar uma nova cópia das linhas de base de configuração importados e itens de configuração** caixa de verificação se pretender que os dados de configuração importados sejam editáveis na consola do Configuration Manager.  
5.  No **resumo** , reveja as ações que serão tomadas e, em seguida, conclua o assistente.  

Os dados de configuração importados apresenta na **as definições de compatibilidade** nó do **ativos e compatibilidade** área de trabalho.  
