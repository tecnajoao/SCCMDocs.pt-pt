---
title: "Excluir as atualizações de cliente | Windows | O System Center Configuration Manager"
description: "Aprenda a excluir clientes Windows da introdução atualizado no System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4cd6031f-8844-4d0b-8166-b24d6528a94e
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 690d03d9c8c49a815bd318df549d7401a855bc5d
ms.openlocfilehash: de5602179f3ac55b51133b8280a0143f1b0ff30e
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="how-to-exclude-upgrading-clients-for-windows-computers-in-system-center-configuration-manager"></a>Como excluir atualizar clientes para computadores com Windows no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

A partir na versão 1610, pode excluir uma coleção de clientes de instalar automaticamente o cliente atualizado de versões. Isto aplica-se a atualização automática, bem como outros métodos, tais como a atualização baseada em atualização de software, scripts de início de sessão e política de grupo. Pode utilizar este para uma coleção de computadores que necessitam de maior cuidado quando atualizar o cliente. Um cliente que está a ser uma coleção de excluídos ignora os pedidos para instalar o software de cliente atualizado.

## <a name="configure-exclusion-for-automatic-upgrades"></a>Configurar a exclusão para atualizações automáticas

1. Na consola do Configuration Manager, aceda a **administração** > **configuração do Site** > **Sites**e, em seguida, clique em **definições de hierarquia**.

2. Clique na **atualização de cliente** separador.

3. Clique na caixa de verificação para **excluir especificada de clientes a partir da atualização**e, em seguida, para a coleção de exclusão, selecione a coleção que pretende excluir. Só pode selecionar uma única coleção para exclusão.

4.  Clique em **OK** fechar e guardar a configuração. Em seguida, após política de atualização de clientes, clientes da coleção de excluídos instalará não ajustarão automaticamente atualizações de software de cliente. Para obter mais informações, consulte o artigo [como atualizar clientes para computadores Windows](upgrade-clients-for-windows-computers.md).

![Definições de exclusão de atualização automática](media/automatic_upgrade_exclusion.png)



>[!NOTE]
>Embora a interface de utilizador indica que os clientes não serão atualizados através de qualquer método, existem dois métodos que pode utilizar para substituir estas definições. Instalação de push de cliente e uma instalação manual de cliente podem ser utilizados para esta configuração de substituição. Para obter mais detalhes, consulte a secção seguinte.

## <a name="how-to-upgrade-a-client-that-is-in-an-excluded-collection"></a>Como atualizar um cliente que está a ser uma coleção de excluídos

Uma coleção é configurada para ser excluídos, desde que os membros da coleção de que só podem ter o software de cliente atualizado por um de dois métodos, que substituem a exclusão:
 - **Instalação Push do cliente** – pode utilizar a instalação push do cliente para atualizar um cliente que está a ser uma coleção de excluídos. Isto é permitido como é considerada a intenção do administrador e permite que a atualização dos clientes sem remover o conjunto completo de exclusão.       

 - **Instalação manual de cliente** – pode atualizar manualmente os clientes que estejam numa coleção de excluídos, ao utilizar o seguinte parâmetro de linha de comandos com o ccmsetup: ***/ignoreskipupgrade***

  Se tentar atualizar manualmente um cliente que seja um membro da coleção de excluídos e não utilize este parâmetro, o cliente não irá instalar o novo software de cliente. Para mais informações consulte [como instalar clientes do Configuration Manager manualmente](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual).

Para obter mais informações sobre os métodos de instalação de cliente, consulte o artigo [como implementar clientes em computadores com Windows no System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).

