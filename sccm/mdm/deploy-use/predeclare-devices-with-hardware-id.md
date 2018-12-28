---
title: Pré-declarar dispositivos com números de série IMEI ou iOS
titleSuffix: Configuration Manager
description: Pré-declarar dispositivos pertencentes à empresa com o respetivo número de série IMEI ou iOS.
ms.date: 09/01/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: ddb4c68e-e7f7-475a-89e2-7379a86e44c4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 118e9b32d691c228857fc31b2da1e9d9b72b7b58
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53415930"
---
# <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>Pré-declarar dispositivos com números de série IMEI ou iOS

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

É possível identificar os dispositivos pertencentes ao importar os números do internacional do equipamento móvel (IMEI) de identidade ou números de série iOS. Pode carregar um ficheiro de valores separados por vírgulas (. csv) que contenha números IMEI de dispositivos ou pode introduzir manualmente as informações do dispositivo.  Informação importada definirá **propriedade** dos dispositivos que são inscritos como **Corporate** nas listas de dispositivos. Uma licença do Intune ainda é necessária para cada utilizador que acede ao serviço.  

Ao carregar números de série para dispositivos iOS pertencentes à empresa, devem ser associadas um perfil de inscrição empresarial. Dispositivos têm de estar inscritos com o programa de inscrição de dispositivos (DEP) da Apple ou do Apple Configurator para que sejam apresentados como propriedade da empresa.

>[!NOTE]
>Dispositivos Android, excluindo os dispositivos Samsung Knox Standard, tem de ter um número de telefone atribuído a eles pré-declarar e inscrevê-lo como um dispositivo pertencentes à empresa com um número IMEI.

## <a name="how-to-predeclare-corporate-owned-devices"></a>Como pré-declarar dispositivos pertencentes à empresa

1. Na consola do Configuration Manager, aceda a **ativos e compatibilidade** > **descrição geral** > **todos os dispositivos da empresa**  >  **Pré-declarados pretencentes dispositivos**.

2. Clique em **criar dispositivos pré-declarados**. É aberto o Assistente para criar dispositivos pré-declarados.

3. Escolha como pretende adicionar informações do dispositivo:

    -  **Carregar um ficheiro CSV que contenha o IMEI ou números de série e detalhes**

       Para esta opção, clique em **procurar** para especificar o ficheiro. csv que contém informações de pré-declarar dispositivos pertencentes à empresa. O ficheiro. csv tem de ser formatado corretamente. Para obter mais informações, consulte [formato para o carregamento de ficheiros. csv](#format-for-uploading-csv-files).

    -  **Adicionar manualmente o IMEI ou números de série e detalhes**

       Para introduzir manualmente as informações, escreva o número de série de número ou iOS do IMEI e os detalhes para os dispositivos. Corrigir quaisquer erros ou avisos antes de continuar.

   Clique em **Seguinte**.

4. Se tiver carregado um ficheiro. csv, reveja os resultados da importação de ficheiros. Se um número de dispositivos foi importado anteriormente, o Configuration Manager apresenta esses dispositivos e a substituição **detalhes**. Selecione os dispositivos cujos detalhes que pretende substituir. Detalhes do dispositivo só podem ser modificados por voltar a importar a identificação do dispositivo ou o número de série.

   Se optar por introduzir manualmente o número, preencha o formulário para os dispositivos que pretende pré-declarar.

   Clique em **Seguinte** para continuar.

5. Se a lista inclui os números de série iOS, selecione o **perfil de inscrição a atribuir** na lista de perfis disponíveis e clique em **próxima**.

6. Clique em **próxima** para rever os detalhes e, em seguida, clique em **próxima** novamente para carregar os dados.

7. Clique em **fechar** para concluir.

## <a name="format-for-uploading-csv-files"></a>Formato para o carregamento de ficheiros. csv

O ficheiro. csv utilizado para identificar os dispositivos por número de série IMEI ou iOS tem de ter o seguinte formato, excluindo a linha superior, que é fornecida para obter orientações apenas. Cada linha tem de conter um número de identificação, um número IMEI ou um número de série do iOS. Para dispositivos iOS, pode incluir ambos. Os números IMEI podem ser utilizados para dispositivos Android, iOS e Windows. Esta tabela contém dados de exemplo:

| IMEI N. º  | Série n. º de iOS  | SO | Detalhes |
|------------ |---------------|-----|-----|
| 123456789012345    |   | WINDOWS | Dispositivo de Windows pertencentes à empresa|
|   | A1B2C3D4E5C6 | IOS |  Dispositivos iOS pertencentes à empresa|
| 223456789012345 | E6D5C4B3A210 |   IOS |  Noutro dispositivo iOS|
| 323456789012345 |        |   IOS |    Um dispositivo iOS terceiro|
| 123456789012346 |         |   ANDROID |   Dispositivo Android pertencentes à empresa|

Não inclua uma linha de cabeçalho no ficheiro. csv. O exemplo seguinte mostra os mesmos dados de exemplo no formato CSV:

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
|Número IMEI sem espaços | número de série iOS | IOS, WINDOWS ou ANDROID | Detalhes do dispositivo opcional (limite de carateres de 1024) |
