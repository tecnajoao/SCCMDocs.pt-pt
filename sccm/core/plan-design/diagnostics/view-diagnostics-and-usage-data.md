---
title: Ver dados do diagnostics | Documentos do Microsoft
description: "Ver dados de utilização e de diagnóstico para confirmar que a hierarquia do System Center Configuration Manager contém sem informações confidenciais."
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 594eb284-0d93-4c5d-9ae6-f0f71203682a
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 199096db7a23fb14db98b95e75246ed254848ab7
ms.openlocfilehash: 0932e2b2a4f3e13c35d6b7b0446083f1c233ce03
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="how-to-view-diagnostics-and-usage-data-for-system-center-configuration-manager"></a>Como visualizar diagnósticos e dados de utilização para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode visualizar os dados de diagnóstico e a utilização da sua hierarquia do System Center Configuration Manager para confirmar que não existem informações confidenciais ou identificáveis estão incluídas. Dados de telemetria são resumidos e armazenados no **TEL_TelemetryResults** tabela da base de dados do site e é formatado para ser programaticamente utilizável e eficiente. Embora as seguintes opções dão-lhe uma vista de exatamente os dados enviados para a Microsoft, estes não se destinam a ser utilizada para outros fins, tal como análise de dados.  

Utilize o seguinte comando do SQL Server para ver os conteúdos desta tabela e apresentar exatamente os dados que são enviados. (Pode também exportar estes dados para um ficheiro de texto.):  

-   **SELECIONE \* de TEL_TelemetryResults**  

> [!NOTE]  
>  Antes de instalar a versão 1602, a tabela que armazena dados de telemetria está **TelemetryResults**.  

Quando o ponto de ligação de serviço está no modo offline, pode utilizar a ferramenta de ligação de serviço para exportar a diagnostics atual e os dados de utilização para um ficheiro de valores separados por vírgulas (CSV). Execute a ferramenta de ligação de serviço no ponto de ligação de serviço, utilizando o **-exportar** parâmetro.  

##  <a name="bkmk_hashes"></a>Hashes unidirecionais  
Alguns dados consistem em cadeias de carateres alfanuméricos aleatórios. O Configuration Manager utiliza o algoritmo SHA-256, que utiliza hashes unidirecionais, para se certificar de que não recolhemos dados potencialmente confidenciais. O algoritmo deixa dados num Estado em que ainda pode ser utilizada para correlação e fins de comparação. Por exemplo, em vez de recolher os nomes das tabelas na base de dados do site, um hash unidirecional é capturado para cada nome de tabela. Isto garante que os nomes de tabelas personalizados que criou ou suplementos de produto a partir de outras pessoas não estão visíveis. Em seguida, podemos pode fazer o mesmo hash unidirecional dos nomes de tabela do SQL Server que são enviados por predefinição no produto e comparar os resultados das duas consultas para determinar o desvio do seu esquema de base de dados a predefinição de produto. Esta informação é, então, utilizada para melhorar as atualizações que necessitem de alterações no esquema do SQL.  

Ao visualizar os dados não processados, um valor comum com hash irá aparecer em cada linha de dados. Este é o ID de hierarquia. Este valor com hash é utilizado para garantir que os dados estão correlacionados com a mesma hierarquia sem identificar o cliente ou origem.  

#### <a name="to-see-how-the-one-way-hash-works"></a>Para ver como funciona o hash unidirecional  

1.  Obter o seu ID de hierarquia executando a seguinte instrução SQL no SQL Server Management Studio a base de dados do Configuration Manager: **selecione [dbo]. [ fnGetHierarchyID]\(\)**  

2.  Utilize o seguinte script do Windows PowerShell para o hash do GUID que é obtido a partir da base de dados unidirecional. Em seguida, pode comparar isto com o ID da hierarquia dos dados não processados para ver como podemos ocultar estes dados.  

    ```  
    Param( [Parameter(Mandatory=$True)] [string]$value )  
      $guid = [System.Guid]::NewGuid()  
      if( [System.Guid]::TryParse($value,[ref] $guid) -eq $true ) {  
      #many of the values we hash are Guids  
      $bytesToHash = $guid.ToByteArray()  
    } else {  
      #otherwise hash as string (unicode)  
      $ue = New-Object System.Text.UnicodeEncoding  
      $bytesToHash = $ue.GetBytes($value)   
    }  
      # Load Hash Provider (https://en.wikipedia.org/wiki/SHA-2)   
    $hashAlgorithm = [System.Security.Cryptography.SHA256Cng]::Create()    
    # Hash the input   
    $hashedBytes = $hashAlgorithm.ComputeHash($bytesToHash)              
    # Base64 encode the result for transport   
    $result = [Convert]::ToBase64String($hashedBytes)    
    return $result   
    ```  

