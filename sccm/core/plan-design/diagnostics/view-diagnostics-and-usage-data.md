---
title: Zobrazit diagnostická data
titleSuffix: Configuration Manager
description: Ver dados de diagnóstico e utilização para confirmar que a hierarquia do System Center Configuration Manager contém não existem informações confidenciais.
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 594eb284-0d93-4c5d-9ae6-f0f71203682a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 64ad8cf66266bd13195925e3de48fc5179714ad0
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56125634"
---
# <a name="how-to-view-diagnostics-and-usage-data-for-system-center-configuration-manager"></a>Como visualizar diagnósticos e dados de utilização para o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode ver os dados de diagnóstico e utilização da sua hierarquia do System Center Configuration Manager para confirmar que não existem informações confidenciais ou identificáveis incluídas. Dados de telemetria são resumidos e armazenados no **TEL_TelemetryResults** tabela da base de dados do site e são formatados para serem programaticamente utilizáveis e eficientes. Embora as opções seguintes dão-lhe uma vista dos dados exatos enviados à Microsoft, eles não se destinam a ser utilizada para outros fins, tal como análise de dados.  

Utilize o seguinte comando SQL para ver os conteúdos desta tabela e mostra exatamente os dados que são enviados. (Também pode exportar estes dados para um arquivo de texto.):  

-   **SELECT \* FROM TEL_TelemetryResults**  

> [!NOTE]  
>  Antes de instalar a versão 1602, a tabela que armazena dados de telemetria é **TelemetryResults**.  

Quando o ponto de ligação de serviço está no modo offline, pode utilizar a ferramenta de ligação de serviço para exportar os dados de utilização e diagnóstico atual para um ficheiro de valores separados por vírgulas (CSV). Execute a ferramenta de ligação de serviço no ponto de ligação de serviço utilizando o **-exportar** parâmetro.  

##  <a name="bkmk_hashes"></a> Hashes unidirecionais  
Alguns dados consiste em cadeias de caracteres de alfanuméricos aleatórias. O Configuration Manager utiliza o algoritmo SHA-256, que utiliza hashes unidirecionais, para garantir que que não recolhe dados potencialmente confidenciais. O algoritmo mantém os dados num Estado em que ainda podem ser utilizado para fins de comparação e de correlação. Por exemplo, em vez de recolher os nomes das tabelas do banco de dados do site, é capturado um hash unidirecional para cada nome de tabela. Isto garante que todos os nomes de tabela personalizado que criou ou suplementos de produtos de terceiros não estão visíveis. Em seguida, podemos fazer o mesmo hash unidirecional dos nomes de tabela SQL que são enviados por predefinição no produto e comparar os resultados das duas consultas para determinar o desvio do seu esquema de base de dados à predefinição do produto. Esta informação é, então, utilizada para melhorar as atualizações que necessitem de alterações no esquema do SQL.  

Ao visualizar os dados não processados, um valor comum com hash irá aparecer em cada linha de dados. Este é o ID de hierarquia. Este valor de hash é utilizado para garantir que os dados estão correlacionados com a mesma hierarquia sem identificar o cliente ou a origem.  

#### <a name="to-see-how-the-one-way-hash-works"></a>Para ver como funciona o hash unidirecional  

1.  Obtenha o seu ID de hierarquia executando a seguinte instrução SQL no SQL Management Studio na base de dados do Configuration Manager: **selecione [dbo]. [ fnGetHierarchyID]\(\)**  

2.  Utilize o seguinte script do Windows PowerShell para fazer o hash unidirecional do GUID que é obtido a partir da base de dados. Em seguida, pode comparar isto com o ID da hierarquia dos dados não processados para ver como podemos ocultar estes dados.  

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
