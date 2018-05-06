---
title: Preparar implementações de computadores desconhecidos
titleSuffix: Configuration Manager
description: Saiba como implementar sistemas operativos em computadores que não são geridos pelo Configuration Manager no seu ambiente do System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 9e447e34-0943-49ed-b6ba-3efebf3566c1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 425ab566b5ddbfaad775d61609c0a4ccd98e96d0
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="prepare-for-unknown-computer-deployments-in-system-center-configuration-manager"></a>Preparar implementações de computadores desconhecidos no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize as informações neste tópico para implementar sistemas operativos em computadores desconhecidos no seu ambiente do System Center Configuration Manager. Um computador desconhecido é um computador que não seja gerido pelo Configuration Manager. Isto significa que não existe nenhum registo destes computadores na base de dados do Configuration Manager. Os computadores desconhecidos incluem o seguinte:  

-   Um computador em que o cliente do Configuration Manager não está instalado  

-   Um computador que não é importado para o Configuration Manager  

-   Um computador que não é detetado pelo Configuration Manager  

 Pode implementar sistemas operativos em computadores desconhecidos com os seguintes métodos de implementação:  

-   [Utilizar o PXE para implementar o Windows na rede](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)  

-   [Utilizar suportes de dados para implementar um sistema operativo](../deploy-use/create-bootable-media.md)  

-   [Utilizar suportes de dados pré-configurados para implementar um sistema operativo](../deploy-use/create-prestaged-media.md)  

## <a name="unknown-computer-deployment-workflow"></a>Fluxo de trabalho da implementação em computadores desconhecidos  
 É apresentado a seguir o fluxo de trabalho básico para implementar um sistema operativo num computador desconhecido:  

-   Selecione um objeto de computador desconhecido para utilizar na implementação. Pode implementar o sistema operativo num dos objetos de computador desconhecido na coleção **Todos os Computadores Desconhecidos** ou adicionar os objetos da coleção **Todos os Computadores Desconhecidos** a outra coleção. Configuration Manager fornece dois objetos de computador desconhecido no **todos os computadores desconhecidos** coleção. Um dos objetos destina-se a computadores x86 e outro a computadores x64.  

    > [!NOTE]  
    >  O objeto **Computador Desconhecido x86** destina-se a computadores que apenas são compatíveis com x86. O objeto **Computador Desconhecido x64** destina-se a computadores que apenas são compatíveis com x86 e x64. Por outras palavras, estes objetos descrevem a arquitetura do computador de destino. Não descrevem o sistema operativo que pretende implementar no computador de destino.  

-   Configure um suporte de dados ou um ponto de distribuição ativado para PXE ou crie um suporte de dados para suportar implementações em computadores desconhecidos.  

-   Implemente a sequência de tarefas para instalar o sistema operativo.  

## <a name="unknown-computer-installation-process"></a>Processo de Instalação de Computador Desconhecido  
 Quando um computador é iniciado pela primeira vez a partir de PXE ou de suportes de dados, o Configuration Manager verifica se existe um registo desse computador na base de dados do Configuration Manager. Se existir um registo, o Configuration Manager, em seguida, verifica se existem sequências de tarefas implementadas no registo. Se não existir um registo, o Configuration Manager verifica se existem sequências de tarefas implementadas num objeto de computador desconhecido. Em ambos os casos, o Configuration Manager, em seguida, executa uma das seguintes ações:  

-   Se existir uma sequência de tarefas disponível, o Configuration Manager pede ao utilizador a executar a sequência de tarefas.  

-   Se existir uma sequência de tarefas necessária, o Configuration Manager é executado automaticamente a sequência de tarefas.  

-   Se uma sequência de tarefas não for implementada para o registo, o Configuration Manager gera um erro que não existe nenhuma sequência de tarefas implementada para o computador de destino.  

 Quando um computador desconhecido é iniciado, o Configuration Manager reconhece o computador como um computador não aprovisionado em vez de um computador desconhecido. Isto significa que o computador pode agora receber as sequências de tarefas que foram implementadas no objeto de computador desconhecido. A sequência de tarefas implementada, em seguida, instala uma imagem do sistema operativo que tem de incluir o cliente do Configuration Manager.  

 Depois do cliente do Configuration Manager está instalado, é criado um registo para o computador e o computador é listado na coleção do Configuration Manager adequado. Se o computador falhar ao instalar a imagem do sistema operativo ou o cliente do Configuration Manager, é criado um registo "Desconhecido" para o computador e o computador é apresentado no **todos os sistemas** coleção.  

> [!NOTE]  
>  Durante a instalação da imagem do sistema operativo, a sequência de tarefas pode obter as variáveis de coleção mas não as variáveis de computador deste computador.  

##  <a name="BKMK_EnablingUnknown"></a> Ativar o Suporte para Computadores Desconhecidos  
 Utilize o seguinte para ativar o suporte para computadores desconhecidos quando implementar um sistema operativo através de PXE, suportes de dados de arranque e suportes de dados pré-configurados.  

-   **PXE**  

     Selecione a caixa de verificação **Ativar suporte para computadores desconhecidos** no separador **PXE** para um ponto de distribuição ativado para PXE. Para obter mais informações, veja [Configurar pontos de distribuição para aceitar pedidos PXE](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint).  

-   **Suporte de dados de arranque**  

     Selecione a caixa de verificação **Ativar suporte para computadores desconhecidos** na página **Segurança** do Assistente de Criação de Suporte de Dados da Sequência de Tarefas. Para obter mais informações, veja [Configurar pontos de distribuição para aceitar pedidos PXE](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint) e [Utilizar PXE para implementar o Windows através da rede com o System Center Configuration Manager](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

-   **Suportes de dados de pré-configuração**  

     Selecione a caixa de verificação **Ativar suporte para computadores desconhecidos** na página **Segurança** do Assistente de Criação de Suporte de Dados da Sequência de Tarefas. Para obter mais informações, veja [Criar suportes de dados pré-configurados com o System Center Configuration Manager](../deploy-use/create-prestaged-media.md).  
