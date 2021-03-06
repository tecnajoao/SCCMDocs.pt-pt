---
title: Importar dados de configuração
titleSuffix: Configuration Manager
description: Importar dados de configuração se ele tem contidos num formato de ficheiro cab e compatível com o esquema de linguagem de modelagem de serviço suportado.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 309b9a09-a611-4ba2-90ab-dde51582cf87
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 13bf43cb2eb80be6605f6c6a925c641f405732a6
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56131001"
---
# <a name="import-configuration-data-with-system-center-configuration-manager"></a>Importar dados de configuração com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Além de criar linhas de base de configuração e itens de configuração na consola do System Center Configuration Manager, é possível importar a configuração do formato de arquivo de dados se ele está contido num ficheiro CAB (. cab) e em conformidade com a linguagem de modelagem de serviço suportados Esquema de (SML). Pode importar dados de configuração a partir de:  

- Dados de configuração de melhores práticas (Pacotes de Configuração) transferidos da Microsoft ou de outros sites de fornecedores de software.  

- Dados de configuração que tenham sido exportados a partir do System Center 2012 Configuration Manager e mais tarde.  

- Dados de configuração criados externamente e que está em conformidade com o esquema SML.  

  Para obter um exemplo de Pacote de Configuração que ajude a gerir a conformidade para funções de servidor de site do System Center 2012 Configuration Manager, consulte [Pacote de Configuração do System Center 2012 Configuration Manager](http://www.microsoft.com/en-us/download/details.aspx?id=30710&WT.mc_id=rss_alldownloads_all).  

Quando importar uma linha de base de configuração, alguns ou todos os itens de configuração referenciados na linha de base de configuração também podem ser incluídos no ficheiro CAB. Durante o processo de importação, o Configuration Manager verifica todos os itens de configuração referenciados na linha de base de configuração também estão incluídos no ficheiro cab ou já existem no site do Configuration Manager. O processo de importação falha se tentar importar uma linha de base de configuração que referencia os dados de configuração do Configuration Manager não consegue localizar.  

Outros cenários em que o processo de importação poderá falhar incluem os seguintes:  

-   Os dados de configuração referenciam dados de configuração que não é possível localizar o Configuration Manager, na respetiva base de dados ou no próprio ficheiro CAB.  

-   Os dados de configuração já estão presentes na base de dados do Configuration Manager com o mesmo nome e versão de dados de configuração, mas a versão do conteúdo é diferente.  

-   Os dados de configuração já estão presentes na base de dados do Configuration Manager com a mesma versão de conteúdo, mas o cálculo de hash identifica-o como sendo diferente.  

-   Uma versão mais recente dos dados de configuração com o mesmo nome já existe ou foi recentemente eliminada na base de dados do Configuration Manager.  

-   Numa hierarquia do Configuration Manager múltiplos sites, os dados de configuração importados originalmente a partir de um site principal. Tem de atualizá-los a partir do mesmo site e não de um site subordinado.  

### <a name="import-configuration-data"></a>Importar dados de configuração  

1.  Na consola do Configuration Manager, clique em **ativos e compatibilidade** > **itens de configuração** ou **linhas de base de configuração**
2.  Na **home page** separador a **Create** , clique em **importar dados de configuração**.  
3.  Na página **Selecionar Ficheiros** do **Assistente de Importação de Dados de Configuração**, clique em **Adicionar**e, na caixa de diálogo **Abrir** , selecione os ficheiros .cab que pretende importar.  
4.  Selecione o **criar uma nova cópia das linhas de base de configuração importados e itens de configuração** caixa de verificação se pretender que os dados de configuração importados sejam editáveis na consola do Configuration Manager.  
5.  Sobre o **resumo** , reveja as ações que serão executadas e conclua o assistente.  

Os dados de configuração importados são apresentados no **definições de compatibilidade** nó da **ativos e compatibilidade** área de trabalho.  
