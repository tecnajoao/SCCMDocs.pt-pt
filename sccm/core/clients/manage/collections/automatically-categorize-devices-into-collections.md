---
title: "Categorizar automaticamente dispositivos para coleções | Documentos do Microsoft"
description: "Categorize dispositivos em coleções automaticamente com o System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 98b038b4-1a13-4228-bdb8-a12194e32b0e
caps.latest.revision: 5
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 690d03d9c8c49a815bd318df549d7401a855bc5d
ms.openlocfilehash: d1b79fb091a6ae4b967d63843ae7b45a0cbeb555
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="automatically-categorize-devices-into-collections-with-system-center-configuration-manager"></a>Categorizar automaticamente dispositivos para coleções com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode criar categorias de dispositivo, o que podem ser utilizadas para colocar automaticamente os dispositivos em coleções de dispositivos quando está a utilizar o Configuration Manager com o Microsoft Intune. Em seguida, os utilizadores têm a escolher uma categoria de dispositivo quando o possam inscreverem um dispositivo no Intune. Pode alterar uma categoria de dispositivo a partir da consola do Configuration Manager.

> [!IMPORTANT]  
    >  Esta capacidade é funciona com o **Junho de 2016** de versão do Microsoft Intune e mais tarde. Certifique-se de que lhe foram atualizadas para esta versão antes de experimentar estes procedimentos.

## <a name="create-device-categories"></a>Criar categorias de dispositivo

1.  Aceda a **ativos e compatibilidade** > **descrição geral** > **coleções de dispositivos**.
2.  No **base** separador o **coleções de dispositivos** grupo, selecione **gerir categorias de dispositivo**.
3.  Criar, editar ou remover categorias.

## <a name="associate-a-collection-with-a-device-category"></a>Associar uma coleção com uma categoria de dispositivo

Quando associar uma coleção com uma categoria de dispositivo, serão adicionados à coleção todos os dispositivos dessa categoria. Não é possível adicionar uma regra de categoria de dispositivo para uma coleção incorporada, como **todos os sistemas**.

1.  No **regras de associação** separador do **propriedades** caixa de diálogo para uma coleção de dispositivos, escolha **Adicionar regra** > **dispositivo categoria de regra**.
2.  No **selecionar dispositivo categorias** caixa de diálogo, selecione um ou mais categorias de dispositivos que serão aplicadas a todos os dispositivos da coleção.

## <a name="change-the-category-of-a-device"></a>Alterar a categoria de um dispositivo

1.  No **ativos e compatibilidade** > **descrição geral** > **dispositivos**, selecione um dispositivo a partir de **dispositivos** lista.
2.  No **base** separador o **dispositivo** grupo, selecione **alterar uma categoria**.
3.  Selecione uma categoria, em seguida, escolha **OK**.

## <a name="view-which-category-a-device-belongs-to"></a>Ver a categoria de um dispositivo pertence à

No **ativos e compatibilidade** > **descrição geral** > **dispositivos**, no **dispositivos** lista, a categoria é apresentada no **dispositivo categoria** coluna.

Se o **dispositivo categoria** coluna não é apresentada, faça duplo clique no cabeçalho de uma das colunas a **dispositivos** lista (como **nome**), em seguida, selecione **categoria de dispositivo**.

Se atribuir um dispositivo a uma categoria e posteriormente eliminar a categoria, o relatório **lista de dispositivos inscritos por utilizador no Microsoft Intune** apresentará um GUID no **dispositivo categoria** coluna, em vez de um nome de categoria.

