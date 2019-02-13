---
title: Coleção de pré-produção de atualizações de cliente de teste
titleSuffix: Configuration Manager
description: Testar as atualizações de cliente numa coleção de pré-produção no System Center Configuration Manager.
ms.date: 05/04/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 49ef2ed2-2e15-4637-8b63-1d5b7f9c17e1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5a8e7cbfefcb97506ac83231bcb7c24fc54f919e
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56129668"
---
# <a name="how-to-test-client-upgrades-in-a-pre-production-collection-in-system-center-configuration-manager"></a>Como testar as atualizações de cliente numa coleção de pré-produção no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode testar uma nova versão de cliente do Configuration Manager numa coleção de pré-produção antes de atualizar o resto do site com o mesmo.  Ao fazê-lo, apenas os dispositivos que fazem parte da coleção de teste são atualizados. Depois de ter tido oportunidade de testar o cliente pode promover o cliente, o que torna a nova versão do software de cliente disponível para o resto do site.

> [!NOTE]
> Para promover um cliente de teste para produção, deve fazer logon como um utilizador com função de segurança do **administrador total** e um âmbito de segurança de **todos os**. Para obter mais informações, consulte [Noções básicas da administração baseada em funções](/sccm/core/understand/fundamentals-of-role-based-administration). Também deve estar conectado a um servidor ligado para o site de administração central ou um site primário autónomo de nível superior.

 Existem 3 passos básicos para testar os clientes em pré-produção.  

1.  Configure atualizações automáticas de clientes para utilizar uma coleção de pré-produção.  

2.  Instale uma atualização do Configuration Manager que inclua uma nova versão do cliente.  

3.  Promova o novo cliente para produção.  

##  <a name="to-configure-automatic-client-upgrades-to-use-a-pre-production-collection"></a>Para configurar atualizações automáticas de clientes para utilizar uma coleção de pré-produção  
> [!IMPORTANT]
> Implementação do cliente de pré-produção não é suportada para computadores de grupo de trabalho. Estes não podem utilizar a autenticação necessária para o ponto de distribuição para aceder ao pacote de cliente de pré-produção.  Eles irão receber o cliente mais recente, quando ele é promovido para ser o cliente de produção.

1. [Configurar uma coleção](../collections/create-collections.md) que contém os computadores que pretende implementar o cliente de pré-produção.   

2. Na consola do Configuration Manager, abra **Administration** > **configuração do Site** > **Sites**e escolha  **Definições de hierarquia**.  

    No separador **Atualização de Clientes** nas **Propriedades das Definições de Hierarquia**:  

   -   Selecione **Atualizar todos os clientes na coleção de pré-produção automaticamente ao utilizar o cliente de pré-produção**  

   -   Introduza o nome de uma coleção para utilizar como coleção de pré-produção  

![Testar as atualizações de cliente](media/test-client-upgrades.png)

>[!NOTE]
>Para alterar estas definições, sua conta tem de ser um membro do **administrador total** função de segurança e o **todos os** âmbito de segurança.


##  <a name="to-install-a-configuration-manager-update-that-includes-a-new-version-of-the-client"></a>Para instalar uma atualização do Configuration Manager que inclua uma nova versão do cliente  

1.  Na consola do Configuration Manager, abra **Administration** > **atualizações e manutenção**, selecione um **disponível** atualizar e, em seguida, escolha **Instalar pacote de atualização**. (Antes da versão 1702, atualizações e manutenção foi sob **Administration** > **serviços Cloud**.)

     Para obter mais informações sobre como instalar atualizações, veja [Atualizações para o System Center Configuration Manager](../../../../core/servers/manage/updates.md)  

2.  Durante a instalação da atualização, sobre o **opções de clientes** página do assistente, selecione **testar na coleção de pré-produção**.  

3.  Conclua o resto do assistente e instale o pacote de atualizações.  

     Depois de concluído o assistente, os clientes na coleção de pré-produção começarm a implementar o cliente atualizado. Pode monitorizar a implementação de clientes atualizados acedendo a **Monitorização** > **Estado de Cliente** > **Implementação do Cliente de Pré-produção**. Para obter mais informações, veja [Como monitorizar o estado de implementação do cliente no System Center Configuration Manager](../../../../core/clients/deploy/monitor-client-deployment-status.md).

    > [!NOTE]
    > O estado de implementação em computadores que alojam funções do sistema de sites de uma coleção de pré-produção possam ser relatado como **não conformes** até mesmo quando o cliente foi implementado com êxito. Ao promover o cliente para produção, o estado de implementação é reportado corretamente.

##  <a name="to-promote-the-new-client-to-production"></a>Para promover o novo cliente para produção  

1.  Na consola do Configuration Manager, abra **Administration** > **atualizações e manutenção**e escolha **promover cliente de pré-produção**. (Antes da versão 1702, atualizações e manutenção foi sob **Administration** > **serviços Cloud**.)

    > [!TIP]
    > Também está disponível o botão **Promover Cliente de Pré-produção** quando está a monitorizar implementações de cliente na consola em **Monitorização** > **Estado de Cliente** > **Implementação do Cliente de Pré-produção**.

2.  Rever as versões de cliente em produção e pré-produção, certifique-se de que o correto a coleção de pré-produção uvedena e, em seguida, clique em **promover**, em seguida, **Sim**.  

3.  Depois de fecha a caixa de diálogo, a versão do cliente atualizada irá substituir a versão do cliente em utilização na sua hierarquia. Em seguida, pode atualizar os clientes para todo o site. Para obter mais informações, consulte [Como atualizar clientes para computadores Windows no System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md) .  

>[!NOTE]
>Para ativar o cliente de pré-produção ou para promover um cliente de pré-produção para um cliente de produção, sua conta tem de ser membro de uma função de segurança que tenha **leitura** e **modificar** permissões para o **Pacotes de atualização de** objeto.
>As atualizações de cliente honrar quaisquer janelas de manutenção do Configuration Manager que configurou.
