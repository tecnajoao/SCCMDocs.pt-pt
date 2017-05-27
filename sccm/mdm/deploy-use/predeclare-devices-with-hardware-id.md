---
title: "Predeclare dispositivos com números de série IMEI ou iOS | Documentos do Microsoft"
description: "Predeclare dispositivos pertencentes à empresa com o respetivo número de série IMEI ou iOS."
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
ms.sourcegitcommit: e6833951db27b227a3ca22925e9d9f4c3fc443fc
ms.openlocfilehash: e8606b8a9268a0a0668b75070cf35894f4794123
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>Predeclare dispositivos com números de série IMEI ou iOS

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode identificar dispositivos pertencentes ao importar os seus números de identidade (IMEI) estação internacional do equipamento móvel ou números de série iOS. Pode carregar um ficheiro de valores separados por vírgulas (. csv) que contenha números IMEI do dispositivo ou pode introduzir manualmente as informações de dispositivo.  Informação importada definirá **propriedade** dos dispositivos inscritos como **empresa** nas listas de dispositivos. Uma licença do Intune é ainda necessária para cada utilizador que aceda ao serviço.  

Ao carregar os números de série para dispositivos iOS pertencentes à empresa, têm de fazer par com um perfil de inscrição na empresa. Dispositivos, em seguida, devem ser inscritos utilizando o programa de inscrição de dispositivos (DEP) ou do Apple Configurator ambos Apple para os aparecem como pertencendo à empresa.

## <a name="how-to-predeclare-corporate-owned-devices"></a>Como predeclare dispositivos pertencentes à empresa

1.    Na consola do Configuration Manager, aceda a **ativos e compatibilidade** > **descrição geral** > **todos os dispositivos pertencentes** > **Predeclared dispositivos**.

2.  Clique em **criar dispositivos Predeclared**. O Assistente para criar Predeclared dispositivos é aberta.

3.    Escolha como pretende adicionar informações do dispositivo:

     -    **Carregar um ficheiro CSV contendo IMEI ou números de série e detalhes**

        Para esta opção, clique em **procurar** para especificar o ficheiro. csv que contém informações para predeclare os dispositivos da empresa. O ficheiro. csv tem de ser formatado corretamente. Para obter mais informações, consulte o artigo [formato para carregamento de ficheiros. csv](#format-for-uploading-csv-files).

     -    **Adicionar manualmente IMEI ou números de série e detalhes**

        Para introduzir manualmente as informações, escreva o número de série de número ou iOS IMEI e os detalhes para os dispositivos. Corrigir quaisquer erros ou avisos antes de continuar.

    Clique em **Seguinte**.

4. Se carregar um ficheiro. csv, reveja os resultados da importação de ficheiro. Se um número de dispositivo foi importado anteriormente, o Configuration Manager apresenta desses dispositivos e a substituição **detalhes**. Selecione os dispositivos cujos detalhes que pretende substituir. Os detalhes de dispositivos apenas podem ser modificados por voltar a importar a identificação de dispositivo ou o número de série.

  Se optar por introduzir manualmente o número, preencha o formulário para os dispositivos que pretende predeclare.

  Clique em **Seguinte** para continuar.

4. Se a sua lista inclui números de série iOS, selecione o **perfil de inscrição para atribuir** da lista de perfis disponíveis e, em seguida, clique em **seguinte**.

5. Clique em **seguinte** para rever os detalhes e, em seguida, clique em **seguinte** novamente para carregar os dados.

6. Clique em **fechar** para concluir.

## <a name="format-for-uploading-csv-files"></a>Formato do carregamento de ficheiros. csv

O ficheiro. csv que utiliza para identificar os dispositivos por IMEI ou número de série tem de ter o seguinte formato, excluindo a linha de cima fornecido para obter orientações sobre apenas. Cada linha tem de conter um número de ID, é um número de série IMEI número ou iOS. Pode incluir ambos. Números IMEI podem ser utilizados para dispositivos Android, iOS e Windows. números de série iOS também são suportados.  Esta tabela contém dados de exemplo:

| IMEI #  | iOS # série  | SO | Detalhes |
|------------ |---------------|-----|-----|
| 123456789012345    |   | WINDOWS | Dispositivo de Windows pertencentes à empresa|
|   | A1B2C3D4E5C6 | IOS |     Dispositivos iOS pertencentes à empresa|
| 223456789012345 | E6D5C4B3A210 |   IOS |     Outro dispositivo iOS|
| 323456789012345 |        |   IOS |     Um dispositivo iOS terceiro|
| 123456789012346 |         |   ANDROID |     Dispositivo Android pertencentes à empresa|

Não inclua uma linha de cabeçalho do ficheiro. csv. O exemplo seguinte mostra os mesmos dados de exemplo no formato CSV:

```
123456789012345,,WINDOWS,Company-owned Windows device
,A1B2C3D4E5C6,IOS,Company-owned iOS device
223456789012345,E6D5C4B3A210,IOS,Another iOS device
323456789012345,,IOS,A third iOS device
123456789012346,,ANDROID,Company-owned Android device
```

As colunas do ficheiro. csv aceitam os seguintes valores:

| Coluna 1 | Coluna 2 | Coluna 3 | Coluna 4 |
|---|---|---|---|
|Número IMEI sem espaços | número de série iOS | IOS, WINDOWS ou ANDROID | Detalhes do dispositivo opcional (limite de carateres de 1024) |

