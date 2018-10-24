---
title: Categorizar automaticamente os dispositivos em coleções
titleSuffix: Configuration Manager
description: Categorize dispositivos em coleções automaticamente com o System Center Configuration Manager.
ms.date: 04/23/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 98b038b4-1a13-4228-bdb8-a12194e32b0e
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 2730464afe21705d020943d3e1566b3130c9c780
ms.sourcegitcommit: ee434c53b3695a039b56298082b6f61f1006d9dd
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/23/2018
ms.locfileid: "49943262"
---
# <a name="automatically-categorize-devices-into-collections-with-system-center-configuration-manager"></a>Categorizar automaticamente os dispositivos em coleções com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode criar categorias de dispositivos, que podem ser utilizadas para colocar automaticamente os dispositivos em coleções de dispositivos quando estiver a utilizar o Configuration Manager com o Microsoft Intune. Os usuários precisam, em seguida, escolha uma categoria de dispositivo quando estes inscrevem um dispositivo no Intune. É possível alterar uma categoria de dispositivo a partir da consola do Configuration Manager.

> [!IMPORTANT]  
    >  Esse recurso funciona com o **Junho de 2016** de versão do Microsoft Intune e mais tarde. Certifique-se de que tiver sido atualizado para esta versão antes de experimentar estes procedimentos.

## <a name="create-device-categories"></a>Criar categorias de dispositivos

1.  Aceda a **ativos e compatibilidade** > **descrição geral** > **coleções de dispositivos**.
2.  Sobre o **home page** separador a **coleções de dispositivos** de grupo, escolha **gerir categorias de dispositivos**.
3.  Criar, editar ou remover as categorias.

## <a name="associate-a-collection-with-a-device-category"></a>Associar uma coleção com uma categoria de dispositivo

Quando associa uma coleção com uma categoria de dispositivo, serão adicionados à coleção todos os dispositivos dessa categoria. Não é possível adicionar uma regra de categoria de dispositivo a uma coleção incorporada, como **todos os sistemas**.

1.  Na **regras de associação** separador do **propriedades** caixa de diálogo para uma coleção de dispositivo, escolha **Adicionar regra** > **deregradecategoriadodispositivo**.
2.  Na **selecionar categorias de dispositivos** caixa de diálogo, selecione um ou mais categorias de dispositivos que serão aplicadas a todos os dispositivos na coleção.

## <a name="change-the-category-of-a-device"></a>Alterar a categoria de um dispositivo

1.  Na **ativos e compatibilidade** > **descrição geral** > **dispositivos**, selecione um dispositivo a partir do **dispositivos** lista.
2.  Sobre o **home page** separador o **dispositivo** de grupo, escolha **alterar categoria**.
3.  Escolher uma categoria, em seguida, escolha **OK**.

## <a name="view-which-category-a-device-belongs-to"></a>Ver qual categoria um dispositivo pertence a

Na **ativos e compatibilidade** > **descrição geral** > **dispositivos**, na **dispositivos** lista, a categoria é apresentado no **categoria de dispositivo** coluna.

Se o **categoria de dispositivos** coluna não for apresentada, clique no título de uma das colunas na **dispositivos** lista (como **nome**), em seguida, selecione **dispositivo Categoria**.

Se atribuir um dispositivo a uma categoria e, em seguida, eliminar a categoria, o relatório **lista de dispositivos inscritos por utilizador no Microsoft Intune** apresentará um GUID no **categoria de dispositivo** coluna, em vez de um nome da categoria.
