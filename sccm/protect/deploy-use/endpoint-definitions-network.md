---
title: "Definições de software maligno do Endpoint Protection da partilha de rede | Microsoft Docs"
description: "Saiba como transferir manualmente as atualizações de definições mais recentes da Microsoft e, em seguida, configure clientes para transferirem estas definições."
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: ddef4d2a-f481-4020-9ddd-9cca5f9795cb
caps.latest.revision: "21"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 110bd9a9d04b27ef6794145fae66dbd910308bdc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-a-network-share-for-configuration-manager"></a>Ativar as definições de software maligno do Endpoint Protection transferir a partir de uma partilha de rede para o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

 Pode transferir manualmente as atualizações de definições mais recentes da Microsoft e, em seguida, configurar os clientes para transferirem estas definições a partir de uma pasta partilhada na rede. Os utilizadores também podem iniciar atualizações de definições quando utiliza esta origem de atualização.

> [!NOTE]
>  Os clientes têm de ter acesso de leitura à pasta partilhada para conseguirem transferir as atualizações de definições.

 Para obter mais informações sobre como transferir as atualizações de definições e de motor para armazenar na partilha de ficheiros, consulte [instalar o software mais recente do antimalware e antisspyware Microsoft](http://www.microsoft.com/security/portal/Definitions/HowToForeFront.aspx).

## <a name="to-configure-definition-downloads-from-a-file-share"></a>Para configurar transferências de definições a partir de uma partilha de ficheiros

1.  Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.

2.  Na área de trabalho **Ativos e Compatibilidade** , expanda **Endpoint Protection**e clique em **Políticas Antimalware**.

3.  Abra a página de propriedades da **Política Antimalware Predefinida** ou crie uma nova política antimalware. Para obter mais informações sobre como criar políticas antimalware, consulte [como criar e implementar políticas antimalware do Endpoint Protection no System Center Configuration Manager](endpoint-antimalware-policies.md).

4.  Na secção **Atualizações da definição** da caixa de diálogo de propriedades de antimalware, clique em **Definir Origem**.

5.  Na caixa de diálogo **Configurar Origens de Atualização da Definição** , selecione **Atualizações a partir de partilhas de ficheiros UNC**.

6.  Clique em **OK** para fechar a caixa de diálogo **Configurar Origens de Atualização da Definição** .

7.  Clique em **Definir Caminhos**. Em seguida, na caixa de diálogo **Configurar Caminhos UNC de Atualização da Definição** , adicione um ou mais caminhos UNC para a localização dos ficheiros de atualizações de definições numa partilha de rede.

8.  Clique em **OK** para fechar a caixa de diálogo **Configurar Caminhos UNC de Atualização da Definição** .


> [!div class="button"]
[Passo seguinte >](endpoint-antimalware-policies.md)

> [!div class="button"]
[Volta >](endpoint-configure-alerts.md)
