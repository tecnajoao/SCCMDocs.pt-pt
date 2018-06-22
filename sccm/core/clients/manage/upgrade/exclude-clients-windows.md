---
title: Excluir as atualizações de cliente para o Windows
titleSuffix: Configuration Manager
description: Saiba como excluir os clientes do Windows da introdução atualizado no System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4cd6031f-8844-4d0b-8166-b24d6528a94e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 164fe811c44306e01e372aa380c2422ec8bd0be7
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32332972"
---
# <a name="how-to-exclude-upgrading-clients-for-windows-computers-in-system-center-configuration-manager"></a>Como excluir atualizar clientes em computadores Windows no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

A partir da versão 1610, pode excluir uma coleção de clientes de instalar automaticamente as versões de cliente atualizado. Isto aplica-se a atualização automática, bem como outros métodos, tais como a atualização baseada em atualização de software, scripts de início de sessão e política de grupo. Pode utilizar esta opção para uma coleção de computadores que têm maior cuidado ao atualizar o cliente. Um cliente que está a ser uma coleção excluída ignora os pedidos para instalar o software de cliente atualizado.

## <a name="configure-exclusion-for-automatic-upgrades"></a>Configurar exclusões de atualizações automáticas

1. Na consola do Configuration Manager, vá para **administração** > **configuração do Site** > **Sites**e, em seguida, clique em **definições de hierarquia**.

2. Clique em de **atualização de cliente** separador.

3. Clique na caixa de verificação para **excluir especificado de clientes de atualização**e, em seguida, para a coleção de exclusão, selecione a coleção que pretende excluir. Só pode selecionar uma única coleção para exclusão.

4.  Clique em **OK** para fechar e guardar a configuração. Em seguida, depois de política de atualização de clientes, os clientes na coleção excluída automaticamente já não irão instalar atualizações para o software de cliente. Para obter mais informações, consulte [como atualizar clientes em computadores Windows](upgrade-clients-for-windows-computers.md).

![Definições de exclusão de atualização automática](media/automatic_upgrade_exclusion.png)



>[!NOTE]
>Embora a interface de utilizador de Estados de que os clientes não serão atualizados através de qualquer método, existem dois métodos que pode utilizar para substituir estas definições. Instalação push do cliente e uma instalação de cliente manual podem ser utilizadas para substituir esta configuração. Para obter mais detalhes, consulte a secção seguinte.

## <a name="how-to-upgrade-a-client-that-is-in-an-excluded-collection"></a>Como atualizar um cliente que está a ser uma coleção excluída

Uma coleção é configurada a serem excluídos, desde que os membros dessa coleção só podem ter atualizado por um dos dois métodos que substituem a exclusão do respetivo software de cliente:
 - **Instalação Push do cliente** – pode utilizar a instalação push do cliente para atualizar um cliente que está a ser uma coleção excluída. Isto é permitido como é considerada a intenção do administrador e permite-lhe atualizar os clientes sem remover o conjunto completo de exclusão.       

 - **Instalação de cliente manual** – pode atualizar manualmente os clientes que estejam numa coleção excluída quando utilizar o seguinte parâmetro de linha de comandos com ccmsetup: ***/ignoreskipupgrade***

  Se tentar atualizar manualmente um cliente que é um membro da coleção excluída e não utilize este parâmetro, o cliente não irá instalar o software de cliente novo. Para obter mais informações consulte [como instalar o Configuration Manager clientes manualmente](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual).

Para obter mais informações sobre métodos de instalação de cliente, consulte [como implementar clientes em computadores Windows no System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).
