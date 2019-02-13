---
title: Atualizar um computador existente com uma nova versão do Windows
titleSuffix: Configuration Manager
description: Pode utilizar vários métodos no Configuration Manager para particionar e formatar (apagar) um computador existente e instalar um novo sistema operativo no computador.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b189a346-8c0d-4870-a876-0719fbb0ab04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8481b0934998a44b6142131d2cff3dbbd0821720
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56124249"
---
# <a name="refresh-an-existing-computer-with-a-new-version-of-windows-using-system-center-configuration-manager"></a>Atualizar um computador existente com uma nova versão do Windows com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este tópico fornece os passos gerais no System Center Configuration Manager para particionar e formatar (apagar) um computador existente e instalar um novo sistema operativo no computador. Para este cenário, pode escolher de entre vários métodos de implementação diferentes, como PXE, suporte de dados de arranque ou Centro de Software. Também pode optar por instalar um ponto de migração de estado para armazenar definições e, em seguida, restaurá-lo para o novo sistema operativo após a respetiva instalação. Se tiver a certeza de que este é o cenário de implementação do sistema operativo correto para si, veja [cenários para implementar sistemas operativos empresariais](scenarios-to-deploy-enterprise-operating-systems.md).  

 Utilize as secções seguintes para atualizar um computador existente com uma nova versão do Windows.  

##  <a name="BKMK_Plan"></a> Planearear  

-   **Planear e implementar requisitos de infraestrutura**  

     Existem vários requisitos de infraestrutura que devem ser cumpridos antes de poder implementar sistemas operativos, como o Windows ADK, a ferramenta de migração de perfil do usuário (USMT), serviços de implementação do Windows (WDS), suporte a configurações de disco rígido, etc. Para obter mais informações, consulte [requisitos de infraestrutura para implementação do sistema operativo](../plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

-   **Instalar um ponto de migração de estado (necessário apenas se transferir definições)**  

     Quando pretender capturar definições do computador existente e, em seguida, restaurá-las para o novo sistema operativo, tem de instalar um ponto de migração de estado. Para mais informações, consulte [State migration point](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

##  <a name="BKMK_Configure"></a> Configurar  

1.  **Preparar uma imagem de arranque**  

     As imagens de arranque iniciam um computador com ambiente Windows PE (um sistema operativo mínimo com componentes e serviços limitados) que, em seguida, pode instalar o sistema operativo Windows completo no computador.   Quando implementar sistemas operativos, tem de selecionar uma imagem de arranque para utilizar e distribuir a imagem por um ponto de distribuição. Utilize o seguinte procedimento para preparar a imagem de arranque:  

    -   Para obter mais informações sobre imagens de arranque, consulte [gerir imagens de arranque](../get-started/manage-boot-images.md).  

    -   Para obter mais informações sobre como personalizar uma imagem de arranque, consulte [personalizar imagens de arranque](../get-started/customize-boot-images.md).  

    -   Distribua a imagem de arranque por pontos de distribuição. Para mais informações, consulte [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

2.  **Preparar uma imagem do sistema operativo**  

     A imagem do sistema operativo contém os ficheiros necessários para instalar o sistema operativo no computador de destino. Utilize o seguinte procedimento para preparar a imagem do sistema operativo:  

    -   Para saber mais sobre como criar uma imagem do sistema operativo, consulte [gerir imagens de sistema operativo](../get-started/manage-operating-system-images.md).  

    -   Distribua a imagem do sistema operativo por pontos de distribuição. Para mais informações, consulte [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

3.  **Criar uma sequência de tarefas para implementar sistemas operativos na rede**  

     Utilize uma sequência de tarefas para automatizar a instalação do sistema operativo na rede. Utilize os passos em [criar uma sequência de tarefas para instalar um sistema operativo](create-a-task-sequence-to-install-an-operating-system.md) para criar a sequência de tarefas para implementar o sistema operativo. Consoante o método de implementação que escolher, poderão existir outras considerações relativamente à sequência de tarefas.  

    > [!NOTE]  
    >  Neste cenário, a sequência de tarefas formata e particiona os discos rígidos no computador. Para capturar as definições do utilizador, tem de utilizar o ponto de migração de estado e selecionar **Gravar ficheiros e definições do utilizador num Ponto de Migração de Estado** na página **Migração de Estado** do assistente Criar Sequência de Tarefas. Se guardar as definições de utilizador e os ficheiros localmente, eles serão perdidos quando o disco rígido é formatado e do Configuration Manager que não poderá restaurar as definições. Para obter mais informações, consulte [gerir o estado do utilizador](../get-started/manage-user-state.md).  

##  <a name="BKMK_Deploy"></a> Implementar  

-   Utilize um dos seguintes métodos de implementação para implementar o sistema operativo:  

    -   [Utilizar o PXE para implementar o Windows na rede](use-pxe-to-deploy-windows-over-the-network.md)  

    -   [Utilizar multicast para implementar o Windows na rede](use-multicast-to-deploy-windows-over-the-network.md)  

    -   [Criar uma imagem para um OEM de fábrica ou um depósito local](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

    -   [Utilizar um suporte de dados autónomo para implementar o Windows sem utilizar a rede](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

    -   [Utilizar suportes de dados de arranque para implementar o Windows na rede](use-bootable-media-to-deploy-windows-over-the-network.md)  

    -   [Utilizar o Centro de Software para implementar o Windows através da rede](use-software-center-to-deploy-windows-over-the-network.md)  

## <a name="monitor"></a>Monitor  

-   **Monitorizar a implementação da sequência de tarefas**  

     Para monitorizar a implementação de sequência de tarefas para instalar o sistema operativo, consulte [monitorizar implementações do sistema operativo](monitor-operating-system-deployments.md).  
