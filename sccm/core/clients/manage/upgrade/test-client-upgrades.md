---
title: "Cliente de teste atualiza a coleção de pré-produção | Documentos do Microsoft"
description: "Testar as atualizações de cliente numa coleção de pré-produção no System Center Configuration Manager."
ms.custom: na
ms.date: 05/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 49ef2ed2-2e15-4637-8b63-1d5b7f9c17e1
caps.latest.revision: 10
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 212628639300e9c361f7cee61b3df6b1cb6874ce
ms.openlocfilehash: 572ef13883f7930e69ec1f1f53c9bfe029898c81
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="how-to-test-client-upgrades-in-a-pre-production-collection-in-system-center-configuration-manager"></a>Como testar as atualizações de cliente numa coleção de pré-produção no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode testar uma nova versão do cliente do Configuration Manager de uma coleção de pré-produção antes de atualizar o resto do site com o mesmo.  Ao fazê-lo, são atualizados apenas os dispositivos que fazem parte da coleção de teste. Uma vez que tenha tido a oportunidade de testar o cliente pode promover o cliente, que disponibiliza a nova versão do software de cliente para o resto do site.

> [!NOTE]
> Para promover um cliente de teste para produção, deve ter sessão iniciada como um utilizador com função de segurança de **administrador total** e um âmbito de segurança de **todos os**. Para obter mais informações, consulte o artigo [Noções básicas da administração baseada em funções](/sccm/core/understand/fundamentals-of-role-based-administration). Tem também de ter iniciado para um servidor ligado para o site de administração central ou um site primário autónomo de nível superior.

 Existem 3 passos básicos para testar os clientes num pré-produção.  

1.  Configure atualizações automáticas de cliente para utilizar uma coleção de pré-produção.  

2.  Instale uma atualização do Configuration Manager que inclui uma nova versão do cliente.  

3.  Promova o novo cliente de produção.  

##  <a name="to-configure-automatic-client-upgrades-to-use-a-pre-production-collection"></a>Para configurar atualizações automáticas de cliente para utilizar uma coleção de pré-produção  

1. [Configurar uma coleção](..\collections\create-collections.md) que contém os computadores que pretende implementar o cliente de pré-produção. Não inclua computadores de grupo de trabalho em coleções de pré-produção. Estes não podem utilizar a autenticação necessária para o ponto de distribuição ao aceder ao pacote de cliente de pré-produção.   

1.  Na consola do Configuration Manager abrir **administração** > **configuração do Site** > **Sites**e escolha **definições de hierarquia**.  

     No separador **Atualização de Clientes** nas **Propriedades das Definições de Hierarquia**:  

    -   Selecione **Atualizar todos os clientes na coleção de pré-produção automaticamente ao utilizar o cliente de pré-produção**  

    -   Introduza o nome de uma coleção para utilizar como coleção de pré-produção  

![Atualizações de cliente de teste](media/test-client-upgrades.png)

>[!NOTE]
>Para alterar estas definições, a conta tem de ser um membro do **administrador total** função de segurança e o **todos os** âmbito de segurança.


##  <a name="to-install-a-configuration-manager-update-that-includes-a-new-version-of-the-client"></a>Para instalar uma atualização do Configuration Manager que inclua uma nova versão do cliente  

1.  Na consola do Configuration Manager, abra **administração** > **atualizações e a manutenção**, selecione um **disponível** atualizar e, em seguida, escolha **instalar o pacote de atualização**. (Antes da versão 1702, atualizações e a manutenção foi em **administração** > **serviços em nuvem**.)

     Para obter mais informações sobre como instalar atualizações, veja [Atualizações para o System Center Configuration Manager](../../../../core/servers/manage/updates.md)  

2.  Durante a instalação da atualização, no **cliente opções** página do assistente, selecione **teste na coleção de pré-produção**.  

3.  Conclua o resto do assistente e instale o pacote de atualizações.  

     Depois de concluído o assistente, os clientes na coleção de pré-produção começarm a implementar o cliente atualizado. Pode monitorizar a implementação de clientes atualizados acedendo a **Monitorização** > **Estado de Cliente** > **Implementação do Cliente de Pré-produção**. Para obter mais informações, veja [Como monitorizar o estado de implementação do cliente no System Center Configuration Manager](../../../../core/clients/deploy/monitor-client-deployment-status.md).

    > [!NOTE]
    > Será possível reportar o estado de implementação em computadores que alojam funções de sistema de sites numa coleção de pré-produção como **não compatíveis** mesmo quando o cliente foi implementado com êxito. Ao promover o cliente para produção, o estado de implementação é reportado corretamente.

##  <a name="to-promote-the-new-client-to-production"></a>Para promover o novo cliente para produção  

1.  Na consola do Configuration Manager, abra **administração** > **atualizações e a manutenção**e escolha **promover cliente de pré-produção**. (Antes da versão 1702, atualizações e a manutenção foi em **administração** > **serviços em nuvem**.)

    > [!TIP]
    > Também está disponível o botão **Promover Cliente de Pré-produção** quando está a monitorizar implementações de cliente na consola em **Monitorização** > **Estado de Cliente** > **Implementação do Cliente de Pré-produção**.

2.  Reveja as versões de cliente na produção e de pré-produção, certifique-se corretos a coleção de pré-produção é especificado e, em seguida, clique em **promover**, em seguida, **Sim**.  

3.  Depois da caixa de diálogo é fechada, a versão de cliente atualizado irá substituir a versão do cliente em utilização na sua hierarquia. Em seguida, pode atualizar os clientes para todo o site. Para obter mais informações, consulte [Como atualizar clientes para computadores Windows no System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

>[!NOTE]
>Para ativar o cliente de pré-produção ou promover um cliente de pré-produção para um cliente de produção, a conta tem de ser um membro de uma função de segurança que tenha **leitura** e **modificar** permissões para o **pacotes de atualização** objeto.
>As atualizações de cliente honrar das janelas de manutenção do Configuration Manager configurou.

