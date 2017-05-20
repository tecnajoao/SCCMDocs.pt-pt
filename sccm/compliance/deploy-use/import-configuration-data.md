---
title: "Importar dados de configuração | Documentos do Microsoft"
description: "Importar dados de configuração se tenha tido num formato de ficheiro cab e paradigmas o esquema de serviço Modeling Language suportado."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 309b9a09-a611-4ba2-90ab-dde51582cf87
caps.latest.revision: 6
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: f9e939d871e95a3248d8e5d96cb73063a81fd5cf
ms.openlocfilehash: 60d0642618a3074fc50a848f1189f4d6559ca916
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="import-configuration-data-with-system-center-configuration-manager"></a>Importar dados de configuração com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Para além de criar linhas de base de configuração e itens de configuração na consola do System Center Configuration Manager, pode importar a configuração dados se um ficheiro CAB (. cab) está contida formato de ficheiro e os paradigmas o esquema de idioma de modelação de serviço (SML) suportados. Pode importar dados de configuração a partir de:  

-   Dados de configuração de melhores práticas (Pacotes de Configuração) transferidos da Microsoft ou de outros sites de fornecedores de software.  

-   Dados de configuração que tenham sido exportados a partir do System Center 2012 Configuration Manager e mais tarde.  

-   Dados de configuração que foi criada externamente e que está em conformidade para o esquema SML.  

 Para obter um exemplo de Pacote de Configuração que ajude a gerir a conformidade para funções de servidor de site do System Center 2012 Configuration Manager, consulte [Pacote de Configuração do System Center 2012 Configuration Manager](http://www.microsoft.com/en-us/download/details.aspx?id=30710&WT.mc_id=rss_alldownloads_all).  

Quando importar uma linha de base de configuração, alguns ou todos os itens de configuração referenciados na linha de base de configuração também podem ser incluídos no ficheiro CAB. Durante o processo de importação, o Configuration Manager verifica se todos os itens de configuração que são referenciados na linha de base de configuração também estão incluídos no ficheiro cab ou já existem no site do Configuration Manager. O processo de importação falhará se tentar importar uma linha de base de configuração que faça referência a dados de configuração do Configuration Manager não é possível localizar.  

Outros cenários em que o processo de importação poderá falhar incluem os seguintes:  

-   Os dados de configuração referencia os dados de configuração do Configuration Manager não conseguir localizar, na sua base de dados ou no ficheiro cab em si.  

-   Os dados de configuração já se encontra presentes na base de dados do Configuration Manager com o mesmo nome e versão de dados de configuração, mas a versão do conteúdo é diferente.  

-   Os dados de configuração já se encontra presentes na base de dados do Configuration Manager com a mesma versão de conteúdo, mas o cálculo de hash identifica-o como sendo diferentes.  

-   Uma versão mais recente dos dados de configuração com o mesmo nome já se encontra presente ou foi recentemente eliminada na base de dados do Configuration Manager.  

-   Numa hierarquia do Configuration Manager multilocal, os dados de configuração foi originalmente importados de um site principal. Tem de atualizá-los a partir do mesmo site e não de um site subordinado.  

### <a name="import-configuration-data"></a>Importar dados de configuração  

1.  Na consola do Configuration Manager, clique em **ativos e compatibilidade** > **itens de configuração** ou **linhas de base de configuração**
2.  No **base** separador o **criar** grupo, clique em **importar dados de configuração**.  
3.  Na página **Selecionar Ficheiros** do **Assistente de Importação de Dados de Configuração**, clique em **Adicionar**e, na caixa de diálogo **Abrir** , selecione os ficheiros .cab que pretende importar.  
4.  Selecione o **criar uma nova cópia dos itens de configuração e linhas de base de configuração importados** caixa de verificação se pretender que os dados de configuração importados a ser editável na consola do Configuration Manager.  
5.  No **resumo** página, reveja as ações que serão efetuadas e, em seguida, conclua o assistente.  

Apresenta os dados de configuração importados a **definições de compatibilidade** nó do **ativos e compatibilidade** área de trabalho.  

