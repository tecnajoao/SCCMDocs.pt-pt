---
title: "Pré-declarar dispositivos com números de série do iOS ou IMEI | Microsoft Docs"
description: "Pré-declarar dispositivos corporativos com o número de série do iOS ou IMEI."
ms.custom: na
ms.date: 03/24/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ddb4c68e-e7f7-475a-89e2-7379a86e44c4
caps.latest.revision: 3
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 5eed004bd38a567dfdd4e392300be656a7abe3f7
ms.openlocfilehash: c692fad43807e54cecbd7ab60284ea740d60617d
ms.contentlocale: pt-pt
ms.lasthandoff: 05/25/2017

---
# <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>Pré-declarar dispositivos com números de série do iOS ou IMEI

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

Você pode identificar dispositivos de propriedade corporativa importando seus números IMEI (identidade) estação internacional de equipamentos móveis ou números de série do iOS. Você pode carregar um arquivo de valores separados por vírgula (. csv) contendo números IMEI do dispositivo, ou você pode inserir manualmente as informações do dispositivo.  Informações importadas definirá **propriedade** dos dispositivos que registram como **corporativo** em listas de dispositivos. Uma licença do Intune ainda é necessária para cada usuário que acessa o serviço.  

Quando você carrega os números de série para dispositivos iOS da empresa, eles devem ser combinados com um perfil de registro corporativo. Dispositivos devem ser registrados usando o programa de registro de dispositivo (DEP) ou o Apple Configurator ou Apple que eles aparecem como propriedade da empresa.

## <a name="how-to-predeclare-corporate-owned-devices"></a>Como pré-declarar dispositivos corporativos

1.    No console do Configuration Manager, vá para **ativos e conformidade** > **visão geral** > **todos os dispositivos corporativos** > **declaradas previamente dispositivos**.

2.  Clique em **criar dispositivos pré-declarada**. Abre o Assistente para criar dispositivos declaradas previamente.

3.    Escolha como você deseja adicionar informações de dispositivo:

     -    **Carregar um arquivo CSV contendo o IMEI ou os números de série e detalhes**

        Para essa opção, clique em **procurar** para especificar o arquivo. csv que contém informações para pré-declarar dispositivos corporativos. O arquivo. csv deve ser formatado corretamente. Para obter mais informações, consulte [formato para carregar arquivos. csv](#format-for-uploading-csv-files).

     -    **Adicionar manualmente o IMEI ou os números de série e detalhes**

        Para inserir manualmente as informações, digite o número de série do iOS ou de número IMEI e detalhes para os dispositivos. Corrija qualquer erro ou avisos antes de continuar.

    Clique em **Seguinte**.

4. Se você carregou um arquivo. csv, analise os resultados da importação de arquivo. Se um número de dispositivo foi importado anteriormente, o Configuration Manager exibe os dispositivos e a substituição **detalhes**. Selecione os dispositivos cujos detalhes você deseja substituir. Detalhes do dispositivo só podem ser modificados por reimportação a identificação do dispositivo ou o número de série.

  Se você optar por inserir manualmente o número, preencha o formulário para os dispositivos que você deseja pré-declarar.

  Clique em **Seguinte** para continuar.

4. Se a lista inclui os números de série do iOS, selecione o **perfil de registro para atribuir** da lista de perfis disponíveis e depois clique em **próximo**.

5. Clique em **próximo** para examinar os detalhes e, em seguida, clique em **próximo** novamente para carregar os dados.

6. Clique em **fechar** para concluir.

## <a name="format-for-uploading-csv-files"></a>Formato para carregar arquivos. csv

O arquivo. csv que você usa para identificar dispositivos pelo número de série do iOS ou IMEI deve ter o seguinte formato, exceto a linha superior, que é fornecida para obter orientação somente. Cada linha deve conter um número de identificação, um número IMEI ou um número de série do iOS. Para dispositivos iOS, você pode incluir ambos. Números IMEI podem ser usados para dispositivos iOS, Android e Windows. Esta tabela contém dados de exemplo:

| IMEI #  | número de série do iOS  | SISTEMA OPERACIONAL | Detalhes |
|------------ |---------------|-----|-----|
| 123456789012345    |   | WINDOWS | Dispositivo de propriedade da empresa do Windows|
|   | A1B2C3D4E5C6 | IOS |     Dispositivos iOS da empresa|
| 223456789012345 | E6D5C4B3A210 |   IOS |     Outro dispositivo iOS|
| 323456789012345 |        |   IOS |     Um terceiro dispositivo iOS|
| 123456789012346 |         |   ANDROID |     Dispositivo Android da empresa|

Não inclua uma linha de cabeçalho no seu arquivo. csv. O exemplo a seguir mostra os mesmos dados de exemplo no formato CSV:

```
123456789012345,,WINDOWS,Company-owned Windows device
,A1B2C3D4E5C6,IOS,Company-owned iOS device
223456789012345,E6D5C4B3A210,IOS,Another iOS device
323456789012345,,IOS,A third iOS device
123456789012346,,ANDROID,Company-owned Android device
```

As colunas no arquivo. csv aceitam os seguintes valores:

| Coluna 1 | Coluna 2 | Coluna 3 | Coluna 4 |
|---|---|---|---|
|Número IMEI sem espaços | número de série do iOS | IOS, WINDOWS ou ANDROID | Detalhes do dispositivo opcional (máximo de 1024 caracteres) |

