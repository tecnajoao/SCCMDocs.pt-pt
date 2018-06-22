---
title: Criar uma imagem para um OEM de fábrica ou um depósito local
titleSuffix: Configuration Manager
description: Utilize implementações de suportes de dados para reduzir o tráfego de rede ao implementar um sistema operativo num computador que não esteja totalmente aprovisionado.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: a7d3df90-062d-4d57-9e9d-e137d3e7cd7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0c8cf0af19017f4acfd95bcd01f8226229c05a14
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32353397"
---
# <a name="create-an-image-for-an-oem-in-factory-or-a-local-depot-with-system-center-configuration-manager"></a>Criar uma imagem para um OEM de fábrica ou um depósito local com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Implementações de suportes de dados pré-configurados no System Center Configuration Manager permitem-lhe implementar um sistema operativo num computador que não esteja totalmente aprovisionado. O suporte de dados pré-configurado é um ficheiro de formato WIM (Windows Imaging) que pode ser instalado num computador bare-metal pelo fabricante (OEM) ou num centro de transição empresarial que não está ligado ao ambiente do Configuration Manager. Mais tarde no ambiente do Configuration Manager, é iniciado o computador utilizando a imagem de arranque fornecida pelo suporte de dados, é executada uma verificação de hash no suporte de dados pré-configurado para se certificar de que é válido e, em seguida, o computador liga ao ponto de gestão do site para sequências de tarefas disponíveis que concluam o processo de transferência.


Este método de implementação pode reduzir o tráfego de rede porque a imagem de arranque e a imagem do sistema operativo já estão no computador de destino. Pode especificar aplicações, pacotes e pacotes de controladores para incluir no suporte de dados pré-configurado. Depois de o sistema operativo estar instalado no computador, a cache da sequência de tarefas local é verificada primeiro em relação às aplicações, pacotes ou pacotes de controladores e, se não for possível localizar o conteúdo ou este tiver sido revisto, o conteúdo é transferido a partir de um ponto de distribuição configurado no suporte de dados pré-configurado e, em seguida, instalado.  

 Pode utilizar suportes de dados pré-configurados nos seguintes cenários de implementação do sistema operativo:  

-   [Instalar uma nova versão do Windows num novo computador (bare-metal)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Substituir um computador existente e transferir definições](replace-an-existing-computer-and-transfer-settings.md)  

 Execute os passos num dos cenários de implementação do sistema operativo e utilize as secções seguintes para se preparar e criar o suporte de dados pré-configurado.  

## <a name="configure-deployment-settings"></a>Configurar definições de implementação  
 Quando utilizar suportes de dados pré-configurados para iniciar o processo de implementação do sistema operativo, tem de configurar a implementação para disponibilizar o sistema operativo nos suportes. Pode configurar esta opção na página **Definições de Implementação** do Assistente de Implementação de Software ou no separador **Definições de Implementação** das propriedades da implementação.  Na definição **Tornar disponível para o seguinte** , configure um dos seguintes:  

-   **Clientes do Configuration Manager, suportes de dados e PXE**  

-   **Apenas suportes de dados e PXE**  

-   **Apenas suportes de dados e PXE (oculto)**  

## <a name="create-the-prestaged-media"></a>Criar o suporte de dados pré-configurado  
 Crie o ficheiro de suporte de dados pré-configurado para enviar ao OEM ou depósito local. Para obter mais informações, veja [Criar suportes de dados pré-configurados com o System Center Configuration Manager](create-prestaged-media.md).  

## <a name="send-the-prestaged-media-file-to-the-oem-or-local-depot"></a>Enviar o ficheiro de suporte de dados pré-configurado ao OEM ou depósito local  
 Envie o suporte de dados ao OEM ou depósito local para pré-configurar os computadores. O ficheiro de suporte de dados pré-configurado é aplicado a um disco rígido formatado no computador.  

## <a name="start-the-computer-to-install-the-operating-system"></a>Iniciar o computador para instalar o sistema operativo  
 O ficheiro de suporte de dados pré-configurado é aplicado aos computadores. Quando o computador for iniciado pela primeira vez, é iniciado o processo de instalação do sistema operativo.  
