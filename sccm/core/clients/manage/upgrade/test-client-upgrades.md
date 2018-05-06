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
ms.openlocfilehash: 019b275177e1f264a4bfc2926cfe45ebd0be8eae
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-test-client-upgrades-in-a-pre-production-collection-in-system-center-configuration-manager"></a>Como testar as atualizações de cliente numa coleção de pré-produção no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode testar uma nova versão do cliente do Configuration Manager na coleção de pré-produção antes de atualizar o resto do site com o mesmo.  Ao fazê-lo, apenas os dispositivos que fazem parte da coleção de teste são atualizados. Depois de ter tido oportunidade de testar o cliente pode promover o cliente, que disponibiliza a nova versão do software de cliente para o resto do site.

> [!NOTE]
> Para promover um cliente de teste para produção, deve ter sessão iniciada como um utilizador com função de segurança de **administrador total** e um âmbito de segurança de **todos os**. Para obter mais informações, consulte [Noções básicas da administração baseada em funções](/sccm/core/understand/fundamentals-of-role-based-administration). Também tem de ser registado para um servidor ligado ao site de administração central ou site primário autónomo nível superior.

 Existem 3 passos básicos para testar os clientes em pré-produção.  

1.  Configure atualizações automáticas de cliente para utilizar uma coleção de pré-produção.  

2.  Instale uma atualização do Configuration Manager que inclui uma nova versão do cliente.  

3.  Promova o novo cliente para produção.  

##  <a name="to-configure-automatic-client-upgrades-to-use-a-pre-production-collection"></a>Para configurar atualizações automáticas de cliente para utilizar uma coleção de pré-produção  
> [!IMPORTANT]
> Implementação de cliente de pré-produção não é suportada para computadores de grupo de trabalho. Estes não podem utilizar a autenticação necessária para o ponto de distribuição para aceder ao pacote de cliente de pré-produção.  Estes irão receber o cliente mais recente, quando é promovido para ser o cliente de produção.

1. [Configurar uma coleção](..\collections\create-collections.md) que contenha os computadores que pretende implementar o cliente de pré-produção.   

1.  Na consola do Configuration Manager, abra **administração** > **configuração do Site** > **Sites**e escolha **definições de hierarquia**.  

     No separador **Atualização de Clientes** nas **Propriedades das Definições de Hierarquia**:  

    -   Selecione **Atualizar todos os clientes na coleção de pré-produção automaticamente ao utilizar o cliente de pré-produção**  

    -   Introduza o nome de uma coleção para utilizar como coleção de pré-produção  

![Testar as atualizações de cliente](media/test-client-upgrades.png)

>[!NOTE]
>Para alterar estas definições, a conta tem de ser um membro do **administrador total** função de segurança e o **todos os** âmbito de segurança.


##  <a name="to-install-a-configuration-manager-update-that-includes-a-new-version-of-the-client"></a>Para instalar uma atualização do Configuration Manager que inclua uma nova versão do cliente  

1.  Na consola do Configuration Manager, abra **administração** > **atualizações e manutenção**, selecione um **disponível** atualizar e, em seguida, escolha **Instalar pacote de atualizações**. (Antes da versão 1702, atualizações e manutenção estava **administração** > **serviços em nuvem**.)

     Para obter mais informações sobre como instalar atualizações, veja [Atualizações para o System Center Configuration Manager](../../../../core/servers/manage/updates.md)  

2.  Durante a instalação da atualização, no **opções de clientes** página do assistente, selecione **testar na coleção de pré-produção**.  

3.  Conclua o resto do assistente e instale o pacote de atualizações.  

     Depois de concluído o assistente, os clientes na coleção de pré-produção começarm a implementar o cliente atualizado. Pode monitorizar a implementação de clientes atualizados acedendo a **Monitorização** > **Estado de Cliente** > **Implementação do Cliente de Pré-produção**. Para obter mais informações, veja [Como monitorizar o estado de implementação do cliente no System Center Configuration Manager](../../../../core/clients/deploy/monitor-client-deployment-status.md).

    > [!NOTE]
    > O estado de implementação em computadores que alojam funções do sistema de sites de uma coleção de pré-produção, pode ser comunicado como **não compatíveis** , mesmo quando o cliente foi implementado com êxito. Ao promover o cliente para produção, o estado de implementação é reportado corretamente.

##  <a name="to-promote-the-new-client-to-production"></a>Para promover o novo cliente para produção  

1.  Na consola do Configuration Manager, abra **administração** > **atualizações e manutenção**e escolha **promover o cliente de pré-produção**. (Antes da versão 1702, atualizações e manutenção estava **administração** > **serviços em nuvem**.)

    > [!TIP]
    > Também está disponível o botão **Promover Cliente de Pré-produção** quando está a monitorizar implementações de cliente na consola em **Monitorização** > **Estado de Cliente** > **Implementação do Cliente de Pré-produção**.

2.  Reveja as versões de cliente na produção e de pré-produção, certifique-se de que o correto a coleção de pré-produção é especificada e, em seguida, clique em **promover**, em seguida, **Sim**.  

3.  Depois de fecha a caixa de diálogo, a versão do cliente atualizada irá substituir a versão de cliente em utilização na sua hierarquia. Em seguida, pode atualizar os clientes para todo o site. Para obter mais informações, consulte [Como atualizar clientes para computadores Windows no System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

>[!NOTE]
>Para ativar o cliente de pré-produção, ou para promover um cliente de pré-produção para um cliente de produção, a conta tem de ser um membro de uma função de segurança que tenha **leitura** e **modificar** permissões para o **pacotes de atualização** objeto.
>As atualizações de cliente honrar janelas de manutenção do Configuration Manager, que configurou.
