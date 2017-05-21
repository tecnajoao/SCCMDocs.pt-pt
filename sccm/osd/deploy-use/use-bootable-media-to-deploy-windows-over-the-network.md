---
title: "Utilize suportes de dados para implementar o Windows através da rede | Documentos do Microsoft"
description: "Utilize implementações de suportes de dados no System Center Configuration Manager para implementar o sistema operativo quando iniciar o computador de destino."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 999b5409-7e72-48d2-8554-4d44427ce383
caps.latest.revision: 5
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 74341fb60bf9ccbc8822e390bd34f9eda58b4bda
ms.openlocfilehash: beb730efbe4d9bae7c4c97f4e587c8919bd79049
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="use-bootable-media-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Utilize suportes de dados para implementar o Windows através da rede com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Implementações de suportes de dados no System Center Configuration Manager permitem-lhe implementar o sistema operativo quando iniciar o computador de destino. Quando o computador de destino é iniciado, obtém a sequência de tarefas, a imagem do sistema operativo e outro conteúdo necessário a partir da rede. Como esse conteúdo não está incluído no suporte de dados, pode atualizar o conteúdo sem ter de recriar o suporte de dados.  

 Pode implementar sistemas operativos na rede através de multicast nos seguintes cenários de implementação de sistema operativo:  

-   [Atualizar um computador existente com uma nova versão do Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Instalar uma nova versão do Windows num novo computador (bare-metal)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Substituir um computador existente e definições de transferência](replace-an-existing-computer-and-transfer-settings.md)  

 Conclua os passos num dos cenários de implementação do sistema operativo e, em seguida, utilize as secções seguintes para utilizar suportes de dados de arranque para implementar o sistema operativo.  

## <a name="configure-deployment-settings"></a>Configurar definições de implementação  
 Quando utilizar suportes de dados de arranque para iniciar o processo de implementação do sistema operativo, tem de configurar a implementação para disponibilizar o sistema operativo nos suportes. Pode configurar esta opção na página **Definições de Implementação** do Assistente de Implementação de Software ou no separador **Definições de Implementação** , nas propriedades da implementação.  Na definição **Tornar disponível para o seguinte** , configure um dos seguintes:  

-   **Clientes do Configuration Manager, suportes de dados e PXE**  

-   **Apenas suportes de dados e PXE**  

-   **Apenas suportes de dados e PXE (oculto)**  

## <a name="create-the-bootable-media"></a>Criar suportes de dados de arranque  
 Pode especificar se os suportes de dados de arranque são uma pen USB ou um conjunto CD/DVD. O computador que vai iniciar o suporte de dados tem de suportar a opção que escolher como unidade de arranque. Para obter mais informações, consulte o artigo [criar suportes de dados](create-bootable-media.md).  

##  <a name="BKMK_Deploy"></a> Instalar o sistema operativo a partir de suportes de dados de arranque  
 Insira o suporte de dados numa unidade de arranque no computador e ligue-o para instalar o sistema operativo.  

