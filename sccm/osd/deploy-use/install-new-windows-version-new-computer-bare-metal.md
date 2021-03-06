---
title: Instalar o Windows num novo computador
titleSuffix: Configuration Manager
description: Utilize o Gestor de configuração para instalar um sistema operativo num novo computador (bare-metal), utilizando o PXE, OEM ou suportes de dados autónomos.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: f5ad22d5-7df1-49c6-8a0f-db1c3f0cda19
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2e565363bbee5852338d730e39bdead6aa5d8457
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56134270"
---
# <a name="install-a-new-version-of-windows-on-a-new-computer-bare-metal-with-system-center-configuration-manager"></a>Instalar uma nova versão do Windows num novo computador (bare-metal) com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este tópico fornece os passos gerais no System Center Configuration Manager, para instalar um sistema operativo num novo computador. Para este cenário, pode escolher de entre vários métodos de implementação diferentes, como PXE, OEM ou suportes de dados autónomos. Se tiver a certeza de que este é o cenário de implementação do sistema operativo correto para si, veja [cenários para implementar sistemas operativos empresariais](scenarios-to-deploy-enterprise-operating-systems.md).  

Utilize as secções seguintes para atualizar um computador existente com uma nova versão do Windows.  

##  <a name="BKMK_Plan"></a> Planearear  

-   **Planear e implementar requisitos de infraestrutura**  

     Existem vários requisitos de infraestrutura que devem ser cumpridos antes de poder implementar sistemas operativos, como o Windows ADK, serviços de implantação do Windows (WDS), configurações de disco rígido suportadas, etc. Para obter mais informações, consulte [requisitos de infraestrutura para implementação do sistema operativo](../plan-design/infrastructure-requirements-for-operating-system-deployment.md).

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

    > [!NOTE]
    > Novas instalações do Windows também podem ser executadas a partir de ficheiros de origem de instalação por meio de pacotes de atualização do SO, mas utilizar imagens do sistema operacional, como **Install. wim** em vez disso.
    >
    > Implementar novas instalações do Windows por meio de pacotes de atualização de SO ainda é suportado, mas depende de controladores compatíveis com este método. Quando o pacote de atualização do Windows a instalar a partir de um sistema operacional, drivers são instalados ainda no Windows PE versus simplesmente, que é injetado no Windows PE. Alguns drivers não são compatíveis com a ser instalado no Windows PE. Se não forem compatíveis com a ser instalado no Windows PE drivers, em seguida, utilize uma imagem de sistema operacional em vez disso.  

3.  **Criar uma sequência de tarefas para implementar sistemas operativos na rede**  

     Utilize uma sequência de tarefas para automatizar a instalação do sistema operativo na rede. Utilize os passos em [criar uma sequência de tarefas para instalar um sistema operativo](create-a-task-sequence-to-install-an-operating-system.md) para criar a sequência de tarefas para implementar o sistema operativo. Consoante o método de implementação que escolher, poderão existir outras considerações relativamente à sequência de tarefas.  

##  <a name="BKMK_Deploy"></a> Implementar  

-   Utilize um dos seguintes métodos de implementação para implementar o sistema operativo:  

    -   [Utilizar o PXE para implementar o Windows na rede](use-pxe-to-deploy-windows-over-the-network.md)  

    -   [Utilizar multicast para implementar o Windows na rede](use-multicast-to-deploy-windows-over-the-network.md)  

    -   [Criar uma imagem para um OEM de fábrica ou um depósito local](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

    -   [Utilizar um suporte de dados autónomo para implementar o Windows sem utilizar a rede](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

    -   [Utilizar suportes de dados de arranque para implementar o Windows na rede](use-bootable-media-to-deploy-windows-over-the-network.md)  

## <a name="monitor"></a>Monitor  

-   **Monitorizar a implementação da sequência de tarefas**  

     Para monitorizar a implementação de sequência de tarefas para instalar o sistema operativo, consulte [monitorizar implementações do sistema operativo](monitor-operating-system-deployments.md).  
