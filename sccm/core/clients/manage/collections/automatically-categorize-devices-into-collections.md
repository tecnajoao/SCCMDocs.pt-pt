---
title: "Categorizar automaticamente os dispositivos para coleções | Microsoft Docs"
description: "Categorize os dispositivos para coleções automaticamente com o System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 98b038b4-1a13-4228-bdb8-a12194e32b0e
caps.latest.revision: "5"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: d1b79fb091a6ae4b967d63843ae7b45a0cbeb555
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="automatically-categorize-devices-into-collections-with-system-center-configuration-manager"></a>Categorizar automaticamente os dispositivos em coleções com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode criar categorias de dispositivo, que podem ser utilizadas para colocar automaticamente os dispositivos em coleções de dispositivos quando estiver a utilizar o Configuration Manager com o Microsoft Intune. Em seguida, os utilizadores têm para escolher uma categoria de dispositivo quando inscreverem um dispositivo no Intune. Pode alterar uma categoria de dispositivo a partir da consola do Configuration Manager.

> [!IMPORTANT]  
    >  Esta capacidade funciona com o **Junho de 2016** de versão do Microsoft Intune e mais tarde. Certifique-se de que lhe foram atualizadas para esta versão antes de experimentar estes procedimentos.

## <a name="create-device-categories"></a>Criar as categorias de dispositivos

1.  Aceda a **ativos e compatibilidade** > **descrição geral** > **coleções de dispositivos**.
2.  No **home page** separador o **coleções de dispositivos** grupo, escolha **gerir categorias de dispositivo**.
3.  Criar, editar ou remover categorias.

## <a name="associate-a-collection-with-a-device-category"></a>Associar uma coleção uma categoria de dispositivo

Quando associa uma coleção com uma categoria de dispositivo, serão adicionados à coleção todos os dispositivos dessa categoria. Não é possível adicionar uma regra de categoria do dispositivo para uma coleção incorporada como **todos os sistemas**.

1.  No **regras de associação** separador do **propriedades** caixa de diálogo para uma coleção de dispositivos, escolha **Adicionar regra** > **regra de categoria do dispositivo**.
2.  No **Selecione as categorias de dispositivos** caixa de diálogo, selecione um ou mais categorias de dispositivos que serão aplicadas a todos os dispositivos na coleção.

## <a name="change-the-category-of-a-device"></a>Alterar a categoria de um dispositivo

1.  No **ativos e compatibilidade** > **descrição geral** > **dispositivos**, selecione um dispositivo do **dispositivos** lista.
2.  No **home page** separador o **dispositivo** grupo, escolha **alterar categoria**.
3.  Escolher uma categoria de, em seguida, escolha **OK**.

## <a name="view-which-category-a-device-belongs-to"></a>Ver qual um dispositivo pertence de categoria

No **ativos e compatibilidade** > **descrição geral** > **dispositivos**, no **dispositivos** lista, a categoria é apresentada no **categoria de dispositivo** coluna.

Se o **categoria de dispositivo** coluna não for apresentada, faça duplo clique no cabeçalho de uma das colunas do **dispositivos** lista (como **nome**), em seguida, selecione **categoria de dispositivo**.

Se atribuir um dispositivo a uma categoria e, subsequentemente, elimine a categoria de relatório **lista de dispositivos inscritos por utilizador no Microsoft Intune** apresentará um GUID no **categoria de dispositivo** coluna, em vez de um nome de categoria.
