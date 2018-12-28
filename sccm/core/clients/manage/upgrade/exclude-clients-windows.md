---
title: Excluir as atualizações de cliente para Windows
titleSuffix: Configuration Manager
description: Saiba como impedir que os clientes do Windows a ser atualizados no System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4cd6031f-8844-4d0b-8166-b24d6528a94e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b14ff463d6f39e74ad757d992fda1042f534a2cd
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53414672"
---
# <a name="how-to-exclude-upgrading-clients-for-windows-computers-in-system-center-configuration-manager"></a>Como excluir atualizar clientes para computadores do Windows no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Partir da versão 1610, pode excluir uma coleção de clientes instalem automaticamente as versões de cliente atualizado. Isto aplica-se a atualização automática, bem como outros métodos, como a atualização baseada em atualização de software, scripts de logon e a política de grupo. Pode utilizá-lo para uma coleção de computadores que necessitam de maior cuidado ao atualizar o cliente. Um cliente que está numa coleção excluída ignora os pedidos para instalar o software de cliente atualizado.

## <a name="configure-exclusion-for-automatic-upgrades"></a>Configurar a exclusão pelas atualizações automáticas

1. Na consola do Configuration Manager, aceda a **Administration** > **configuração do Site** > **Sites**e, em seguida, clique em  **Definições de hierarquia**.

2. Clique nas **atualização do cliente** separador.

3. Clique a caixa de verificação **excluir os clientes especificados da atualização**e, em seguida, para a coleção de exclusão, selecione a coleção que pretende excluir. Só pode selecionar uma única coleção de exclusão.

4.  Clique em **OK** para fechar e guardar a configuração. Em seguida, depois de clientes de atualização de política, os clientes na coleção excluída já não instalará automaticamente atualizações para o software de cliente. Para obter mais informações, consulte [como atualizar clientes para computadores Windows](upgrade-clients-for-windows-computers.md).

![Definições de atualização automática de exclusão](media/automatic_upgrade_exclusion.png)



>[!NOTE]
>Embora a interface do usuário indica que os clientes não serão atualizados através de qualquer método, existem dois métodos que pode utilizar para substituir estas definições. Instalação push do cliente e uma instalação de cliente manual podem ser utilizados para substituir esta configuração. Para obter mais detalhes, consulte a secção seguinte.

## <a name="how-to-upgrade-a-client-that-is-in-an-excluded-collection"></a>Como atualizar um cliente que está numa coleção excluída

Uma coleção é configurada para ser excluído, desde que os membros dessa coleção só podem ter seu software de cliente atualizado por um dos dois métodos, substituem a exclusão:
- **Instalação Push do cliente** – pode utilizar a instalação de push de cliente para atualizar um cliente que está numa coleção excluída. Isso é permitido uma vez que ele é considerado como estando a intenção do administrador e permite-lhe atualizar os clientes sem remover toda a coleção de exclusão.       

- **Instalação de cliente manual** – pode atualizar manualmente os clientes que estão numa coleção excluída ao utilizar o seguinte comutador de linha de comandos com o ccmsetup: ***/ignoreskipupgrade***

  Se tenta atualizar manualmente um cliente que seja membro da coleção excluída e não utilize este parâmetro, o cliente não será instalado o novo software de cliente. Para obter mais informações, consulte [como instalar clientes manualmente do Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual).

Para obter mais informações sobre métodos de instalação de cliente, consulte [como implementar clientes em computadores do Windows no System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).
