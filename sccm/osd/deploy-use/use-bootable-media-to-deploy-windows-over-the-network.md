---
title: Utilizar suportes de dados para implementar o Windows através da rede
titleSuffix: Configuration Manager
description: Utilize implementações de suportes de dados no System Center Configuration Manager para implementar o sistema operativo quando iniciar o computador de destino.
ms.date: 6/16/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 999b5409-7e72-48d2-8554-4d44427ce383
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4f7ec06d5bd5f23ac2b8afa2a288dfb8c971f950
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="use-bootable-media-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Utilizar suportes de dados para implementar o Windows através da rede com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode implementar o sistema operativo quando o computador de destino é iniciado com uma implementação de suportes de dados. O suporte de dados contém um ponteiro para a sequência de tarefas, a imagem do sistema operativo e outro conteúdo necessário a partir da rede. Quando o computador de destino é iniciado, o computador obtém os itens referenciados do ponteiro. Com os suportes de dados livres de conteúdo, pode atualizar o destino sem ter de substituí-lo no suporte de dados.

Pode implementar sistemas operativos através da rede através de multicast nos seguintes cenários de implementação do sistema operativo:

-   [Atualizar um computador existente com uma nova versão do Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

-   [Instalar uma nova versão do Windows num novo computador (bare-metal)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Substituir um computador existente e transferir definições](replace-an-existing-computer-and-transfer-settings.md)  

Conclua os passos num dos cenários de implementação do sistema operativo e, em seguida, utilize as secções seguintes para utilizar suportes de dados de arranque para implementar o sistema operativo.  

## <a name="configure-deployment-settings"></a>Configurar definições de implementação  
Quando utilizar suportes de dados para iniciar o processo de implementação do sistema operativo, configure a implementação para disponibilizar o sistema operativo para o suporte de dados. Pode configurar esta opção no **definições de implementação** página do Assistente de implementação de Software ou no **definições de implementação** separador nas propriedades para a implementação. Na definição **Tornar disponível para o seguinte** , configure um dos seguintes:

-   Clientes do Configuration Manager, suportes de dados e PXE

-   Apenas suportes de dados e PXE

-   Apenas suportes de dados e PXE (oculto)

## <a name="create-the-bootable-media"></a>Criar suportes de dados de arranque
Pode especificar se os suportes de dados é uma unidade flash USB ou conjunto CD/DVD. O computador é iniciado o suporte de dados tem de suportar a opção que escolher como unidade de arranque. Para obter mais informações, consulte [criar suportes de dados](create-bootable-media.md).  

##  <a name="BKMK_Deploy"></a> Instalar o sistema operativo a partir de suportes de dados de arranque  
Insira o suporte de dados numa unidade de arranque no computador e ligue-o para instalar o sistema operativo.
