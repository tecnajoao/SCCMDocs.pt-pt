---
title: "Ver dados de diagnóstico"
titleSuffix: Configuration Manager
description: "Ver dados de diagnóstico e utilização para confirmar que a sua hierarquia do System Center Configuration Manager contém não existem informações confidenciais."
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 594eb284-0d93-4c5d-9ae6-f0f71203682a
caps.latest.revision: "8"
author: aaroncz
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: fb6e5d1e19dbb86d8c2106e0246986734f598853
ms.sourcegitcommit: 7fe45ff75f05f7cc03ad021db8119791abe18049
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/01/2017
---
# <a name="how-to-view-diagnostics-and-usage-data-for-system-center-configuration-manager"></a>Como visualizar diagnósticos e dados de utilização para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode ver os dados de diagnóstico e de utilização da sua hierarquia do System Center Configuration Manager para confirmar que não existem informações confidenciais ou identificáveis incluídas. Dados de telemetria são resumidos e armazenados no **TEL_TelemetryResults** tabela da base de dados do site e são formatados para serem programaticamente utilizáveis e eficientes. Embora as opções seguintes dão-lhe uma vista dos dados exatos enviados à Microsoft, estes não são se destina a ser utilizada para outros fins, tal como uma análise de dados.  

Utilize o seguinte comando SQL para ver os conteúdos desta tabela e mostra exatamente os dados que são enviados. (Também pode exportar estes dados para um ficheiro de texto.):  

-   **SELECIONE \* de TEL_TelemetryResults**  

> [!NOTE]  
>  Antes de instalar a versão 1602, a tabela que armazena dados de telemetria é **TelemetryResults**.  

Quando o ponto de ligação de serviço está no modo offline, pode utilizar a ferramenta de ligação de serviço para exportar os dados de utilização e diagnóstico atual para um ficheiro de valores separados por vírgulas (CSV). Execute a ferramenta de ligação de serviço no ponto de ligação de serviço utilizando o **-exportar** parâmetro.  

##  <a name="bkmk_hashes"></a>Hashes unidirecionais  
Alguns dados incluem cadeias de carateres alfanuméricos aleatórias. O Configuration Manager utiliza o algoritmo SHA-256, que utiliza hashes unidirecionais, para se certificar de que não recolhe dados potencialmente confidenciais. O algoritmo deixa dados num Estado em que ainda podem ser utilizado para correlação e fins de comparação. Por exemplo, em vez de recolher os nomes das tabelas na base de dados do site, é capturado um hash unidirecional para cada nome de tabela. Isto garante que todos os nomes de tabelas personalizados que criou ou suplementos de produtos de terceiros não estão visíveis. Em seguida, podemos fazer o mesmo hash unidirecional dos nomes de tabela do SQL Server que são enviados por predefinição no produto e comparar os resultados das duas consultas para determinar o desvio do seu esquema de base de dados à predefinição do produto. Esta informação é, então, utilizada para melhorar as atualizações que necessitem de alterações no esquema do SQL.  

Ao visualizar os dados não processados, um valor comum com hash irá aparecer em cada linha de dados. Este é o ID de hierarquia. Este valor com hash é utilizado para garantir que os dados estão correlacionados com a mesma hierarquia sem identificar o cliente ou a origem.  

#### <a name="to-see-how-the-one-way-hash-works"></a>Para ver como funciona o hash unidirecional  

1.  Obter o seu ID de hierarquia executando a seguinte instrução SQL no SQL Server Management Studio na base de dados do Configuration Manager: **selecione [dbo]. [ fnGetHierarchyID]\(\)**  

2.  Utilize o seguinte script do Windows PowerShell para efetuar o hash unidirecional do GUID que é obtido a partir da base de dados. Em seguida, pode comparar isto com o ID da hierarquia dos dados não processados para ver como podemos ocultar estes dados.  

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
