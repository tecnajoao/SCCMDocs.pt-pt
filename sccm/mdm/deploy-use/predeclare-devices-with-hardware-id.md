---
title: "Pré-declarar dispositivos com números de série iOS ou IMEI | Microsoft Docs"
description: "Pré-declarar dispositivos pertencentes à empresa com o respetivo número de série iOS ou IMEI."
ms.custom: na
ms.date: 09/01/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ddb4c68e-e7f7-475a-89e2-7379a86e44c4
caps.latest.revision: "3"
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 424f04b2b3ad4c7ef91f884bbf5bae3580ea6b85
ms.sourcegitcommit: cd1f9c58e55f1c9a19acd743ec6a8824c39fd3a1
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/05/2017
---
# <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>Pré-declarar dispositivos com números de série iOS ou IMEI

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode identificar dispositivos pertencentes ao importar os números de identidade (IMEI) estação internacional do equipamento móvel ou números de série iOS. Pode carregar um ficheiro de valores separados por vírgulas (. csv) contendo os números IMEI de dispositivo ou pode introduzir manualmente as informações do dispositivo.  Informação importada definirá **propriedade** dos dispositivos que inscrever como **empresa** nas listas de dispositivos. Uma licença do Intune é ainda necessária para cada utilizador que acede ao serviço.  

Ao carregar os números de série para dispositivos iOS pertencentes à empresa, tem de ser emparelhados com um perfil de inscrição empresarial. Dispositivos, em seguida, têm de ser inscritos utilizando o programa de inscrição de dispositivos (DEP) da Apple ou ou do Apple Configurator para os aparecer como pertencentes à empresa.

>[!NOTE]
>Dispositivos Android, excluindo os dispositivos Samsung Knox Standard, tem de ter um número de telefone atribuído aos mesmos pré-declarar e inscrevê-lo como um dispositivo propriedade da empresa com um número IMEI.

## <a name="how-to-predeclare-corporate-owned-devices"></a>Como pré-declarar dispositivos pertencentes à empresa

1.  Na consola do Configuration Manager, vá para **ativos e compatibilidade** > **descrição geral** > **todos os dispositivos pertencentes** > **Predeclared dispositivos**.

2.  Clique em **criar dispositivos Predeclared**. O assistente criar dispositivos Predeclared abre.

3.  Escolha como pretende adicionar informações do dispositivo:

     -  **Carregar um ficheiro CSV que contenha o IMEI ou os números de série e os detalhes**

        Para esta opção, clique em **procurar** para especificar o ficheiro. csv que contém informações de pré-declarar dispositivos pertencentes à empresa. O ficheiro. csv tem de ser formatado corretamente. Para obter mais informações, consulte [formato do carregamento de ficheiros. csv](#format-for-uploading-csv-files).

     -  **Adicionar manualmente o IMEI ou os números de série e os detalhes**

        Para introduzir manualmente as informações, escreva o número de série IMEI número ou iOS e os detalhes para os dispositivos. Corrija quaisquer erros ou avisos antes de continuar.

    Clique em **Seguinte**.

4. Se carregado um ficheiro. csv, reveja os resultados da importação de ficheiro. Se um número de dispositivos foi importado anteriormente, o Configuration Manager apresenta desses dispositivos e a substituição **detalhes**. Selecione os dispositivos cujos detalhes que pretende substituir. Detalhes do dispositivo só podem ser modificados por voltar a importar a identificação do dispositivo ou o número de série.

  Se optar por introduzir manualmente o número, preencha o formulário para os dispositivos que pretende pré-declarar.

  Clique em **Seguinte** para continuar.

4. Se a lista inclui os números de série iOS, selecione o **perfil de inscrição a atribuir** da lista de perfis disponíveis e, em seguida, clique em **seguinte**.

5. Clique em **seguinte** para rever os detalhes e, em seguida, clique em **seguinte** novamente para carregar os dados.

6. Clique em **fechar** para concluir.

## <a name="format-for-uploading-csv-files"></a>Formato do carregamento de ficheiros. csv

O ficheiro. csv utilizado para identificar dispositivos por número de série iOS ou IMEI tem de ter o seguinte formato, excluindo a linha superior, que é fornecida para obter orientações sobre apenas. Cada linha tem de conter um número de ID, um número IMEI ou um número de série iOS. Para dispositivos iOS, pode incluir ambos. Os números IMEI podem ser utilizados para dispositivos Android, iOS e Windows. Esta tabela contém dados de exemplo:

| IMEI N. º  | Série n. º de iOS  | SO | Detalhes |
|------------ |---------------|-----|-----|
| 123456789012345    |   | WINDOWS | Dispositivo de Windows pertencentes à empresa|
|   | A1B2C3D4E5C6 | IOS |  Dispositivos iOS pertencentes à empresa|
| 223456789012345 | E6D5C4B3A210 |   IOS |  Noutro dispositivo iOS|
| 323456789012345 |        |   IOS |    Um dispositivo iOS terceiro|
| 123456789012346 |         |   ANDROID |   Dispositivo Android da empresa|

Não inclua a linha de cabeçalho no seu ficheiro. csv. O exemplo seguinte mostra os mesmos dados de exemplo num formato CSV:

```
123456789012345,,WINDOWS,Company-owned Windows device
,A1B2C3D4E5C6,IOS,Company-owned iOS device
223456789012345,E6D5C4B3A210,IOS,Another iOS device
323456789012345,,IOS,A third iOS device
123456789012346,,ANDROID,Company-owned Android device
```

As colunas do ficheiro. csv aceitam os valores seguintes:

| Coluna 1 | Coluna 2 | Coluna 3 | Coluna 4 |
|---|---|---|---|
|Número IMEI sem espaços | número de série iOS | IOS, WINDOWS ou ANDROID | Detalhes do dispositivo opcional (limite de caracteres de 1024) |
