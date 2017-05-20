---
title: "Introdução à implementação do sistema operativo | Documentos do Microsoft"
description: Compreenda os conceitos antes de implementar sistemas operativos no seu ambiente do Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d9a1c545-8301-492c-832f-2c108ff93c77
caps.latest.revision: 12
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 55a9f1caedcfa810e9a97e43626e4cf5fdbcfa0d
ms.openlocfilehash: 2baa6b7dbd66ab41bc9b67e8f43c313be233153c
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="introduction-to-operating-system-deployment-in-system-center-configuration-manager"></a>Introdução à implementação de sistemas operativos no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode utilizar o Configuration Manager para implementar sistemas operativos de várias formas diferentes. Utilize as informações nesta secção para compreender como implementar sistemas operativos e Automatize tarefas. 

##  <a name="BKMK_OSDeploymentProcess"></a> Processo de implementação do sistema operativo  
 O Configuration Manager oferece vários métodos que pode utilizar para implementar um sistema operativo. Existem várias ações que deverá efetuar, independentemente do método de implementação que utilizar:  

-   Identificar os controladores de dispositivo do Windows necessários para executar a imagem de arranque ou a imagem do sistema operativo que tem de implementar.  

-   Identificar a imagem de arranque que pretende utilizar para iniciar o computador de destino.  

-   Utilizar uma sequência de tarefas para capturar uma imagem do sistema operativo que pretende implementar. Em alternativa, pode utilizar uma imagem predefinida do sistema operativo.  

-   Distribuir a imagem de arranque, a imagem de sistema operativo e qualquer conteúdo relacionado a um ponto de distribuição.  

-   Criar uma sequência de tarefas com os passos para implementar a imagem de arranque e a imagem do sistema operativo.  

-   Implementar a sequência de tarefas numa coleção de computadores.  

-   Monitorizar a implementação.  

##  <a name="BKMK_OSDScenarios"></a> Cenários de implementação do sistema  
 Existem muitos cenários de implementação do sistema operativo no Configuration Manager que pode escolher entre dependendo do seu ambiente e o objetivo para a instalação de sistema operativo.  Por exemplo, pode particionar e formatar um computador existente com uma nova versão do Windows ou atualizar o Windows para a versão mais recente. Para ajudar a determinar o método de implementação que satisfaça as suas necessidades, reveja [cenários para implementar sistemas operativos enterprise](../deploy-use/scenarios-to-deploy-enterprise-operating-systems.md).  Pode escolher de entre os seguintes cenários de implementação do sistema operativo:  

-   [Atualizar o Windows para a versão mais recente](../deploy-use/upgrade-windows-to-the-latest-version.md)  

-   [Atualizar um computador existente com uma nova versão do Windows](../deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Instalar uma nova versão do Windows num novo computador (bare-metal)](../deploy-use/install-new-windows-version-new-computer-bare-metal.md)  

-   [Substituir um computador existente e definições de transferência](../deploy-use/replace-an-existing-computer-and-transfer-settings.md)  

##  <a name="BKMK_OSDMethods"></a> Métodos para implementar sistemas operativos  
 Existem vários métodos que pode utilizar para implementar sistemas operativos em computadores de cliente do Configuration Manager.  

-   **Implementações iniciadas por PXE**: Implementações iniciadas por PXE permitem aos computadores cliente pedir uma implementação através da rede. Neste método de implementação, a imagem de sistema operativo e uma imagem de arranque do Windows PE são enviadas para um ponto de distribuição configurado para aceitar pedidos de arranque PXE. Para obter mais informações, veja [Utilizar o PXE para implementar o Windows na rede com o System Center Configuration Manager](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

-   **Disponibilizar os sistemas operativos no Centro de Software**: Pode implementar um sistema operativo e disponibilizá-la no Centro de Software. Clientes do Configuration Manager podem iniciar a instalação de sistema operativo a partir do Centro de Software. Para obter mais informações, consulte o artigo [substituir um computador existente e transferir definições](../deploy-use/replace-an-existing-computer-and-transfer-settings.md).  

-   **As implementações multicast**: As implementações multicast conservam a largura de banda de rede ao enviarem dados simultaneamente para vários clientes em vez de enviarem uma cópia dos dados a cada cliente através de uma ligação individual. Neste método de implementação, a imagem de sistema operativo é enviada para um ponto de distribuição. Este, por sua vez, implementa a imagem quando os computadores cliente pedem a implementação. Para obter mais informações, consulte o artigo [utilize o multicast para implementar o Windows através da rede](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

-   **Implementações de suportes de dados**: Implementações de suportes de dados permitem-lhe implementar o sistema operativo quando iniciar o computador de destino. Quando o computador de destino é iniciado, obtém a sequência de tarefas, a imagem do sistema operativo e outro conteúdo necessário a partir da rede. Como esse conteúdo não está incluído no suporte de dados, pode atualizar o conteúdo sem ter de recriar o suporte de dados. Para obter mais informações, consulte o artigo [criar suportes de dados](../deploy-use/create-bootable-media.md).  

-   **Implementações de suportes de dados autónomos**: As implementações com suportes de dados autónomos permitem implementar sistemas operativos nas seguintes condições:  

    -   Em ambientes onde não é prático copiar uma imagem de sistema operativo ou outros pacotes grandes através da rede.  

    -   Em ambientes sem conectividade de rede ou uma conectividade de rede com largura de banda reduzida.  

     Para obter mais informações, consulte o artigo [criar suportes de dados autónomos](../deploy-use/create-stand-alone-media.md).  

-   **Implementações de suportes de dados pré-configurados**: As implementações de suportes de dados pré-configurados permitem implementar um sistema operativo num computador que não esteja totalmente aprovisionado. Suporte de dados pré-configurado é um ficheiro de formato WIM (Windows Imaging) que pode ser instalado num computador bare-metal pelo fabricante ou num centro de transição empresarial que não está ligado ao ambiente do Configuration Manager.  

     Mais tarde no ambiente do Configuration Manager, o computador inicia utilizando a imagem de arranque fornecida pelo suporte de dados e, em seguida, liga ao ponto de gestão do site para sequências de tarefas disponíveis que concluam o processo de transferência. Este método de implementação pode reduzir o tráfego de rede porque a imagem de arranque e a imagem do sistema operativo já estão no computador de destino. Pode especificar aplicações, pacotes e pacotes de controladores para incluir no suporte de dados pré-configurado. Para obter mais informações, consulte o artigo [criar suportes de dados pré-configurados](../deploy-use/create-prestaged-media.md).  

##  <a name="BKMK_BootImages"></a> Imagens de arranque  
 Uma imagem de arranque no Configuration Manager é uma imagem do Windows PE (WinPE) que é utilizada durante uma implementação do sistema operativo. As imagens de arranque são utilizadas para iniciar um computador no WinPE, que é um sistema operativo minimalista com componentes e serviços limitados que preparam o computador de destino para a instalação do Windows. O Configuration Manager oferece duas imagens de arranque: Uma para suportar x86 plataformas e outra para suportar x64 plataformas. Estas são consideradas imagens de arranque predefinidas. Imagens de arranque que pode criar e adicionar para o Configuration Manager são consideradas imagens personalizadas. Imagens de arranque predefinidas podem ser substituídas automaticamente quando atualizar do Configuration Manager. Para obter mais informações sobre imagens de arranque, veja [Gerir imagens de arranque](../get-started/manage-boot-images.md).  

##  <a name="BKMK_OSImages"></a> Imagens de sistema operativo  
 As imagens de sistema operativo no Configuration Manager são armazenadas no formato de ficheiro Windows Imaging (WIM) e representam uma coleção comprimida de ficheiros e pastas de referência que são necessários para instalar e configurar com êxito um sistema operativo num computador. Para todos os cenários de implementação do sistema operativo, tem de selecionar uma imagem do sistema operativo. Pode utilizar a imagem predefinida do sistema operativo ou compilar a imagem do sistema operativo a partir de um computador de referência que configurar. Para obter mais informações, consulte o artigo [gerir imagens do sistema operativo](../get-started/manage-operating-system-images.md).  

##  <a name="BKMK_OSUpgradePackages"></a> Pacotes de atualização do sistema operativo  
 Os pacotes de atualização do sistema operativo são utilizados para atualizar um sistema operativo e são implementações do sistema operativo iniciadas pela configuração. Importar pacotes de atualização do sistema operativo no Configuration Manager a partir de um DVD ou o ficheiro ISO montado. Para obter mais informações, consulte o artigo [gerir pacotes de atualização do sistema operativo](../get-started/manage-operating-system-upgrade-packages.md).  

##  <a name="BKMK_OSDMedia"></a> Métodos para implementar sistemas operativos  
 Pode criar vários tipos de suportes de dados que podem ser utilizados para implementar sistemas operativos. Isto inclui suportes de dados de captura, que são utilizados para capturar imagens de sistema operativo, e suportes de dados de arranque pré-configurados e autónomos, que são utilizados para implementar um sistema operativo. Utilizando suportes de dados, pode implementar sistemas operativos em computadores que não tenham uma ligação de rede ou que tenha uma ligação de largura de banda reduzida ao seu site do Configuration Manager. Para obter mais informações sobre como utilizar suportes de dados, consulte o artigo [criar suportes de dados de sequência de tarefas](../deploy-use/create-task-sequence-media.md).  

##  <a name="BKMK_DeviceDrivers"></a> Controladores de dispositivo  
 Pode instalar controladores de dispositivo em computadores de destino sem os incluir na imagem do sistema operativo que está a ser implementada. O Configuration Manager oferece um catálogo de controladores que contém referências a todos os controladores de dispositivo que importar para o Configuration Manager. O catálogo de controladores está localizado no **biblioteca de Software** área de trabalho e é composto por dois nós: **Controladores** e **pacotes de controladores**. O nó **Controladores** lista todos os controladores que importou para o catálogo de controladores. Pode utilizar este nó para saber os detalhes de cada controlador importado, para alterar o pacote de controladores ou a imagem de arranque a que um controlador pertence, para ativar ou desativar um controlador, etc. Para obter mais informações, consulte o artigo [gerir controladores](../get-started/manage-drivers.md).  

##  <a name="BKMK_OSDUserState"></a> Guardar e restaurar estado do utilizador  
 Quando implementa sistemas operativos, pode guardar o estado de utilizador do computador de destino, implementar o sistema operativo e, em seguida, restaurar o estado de utilizador, após a implementação do sistema operativo. Este processo é normalmente utilizado quando instalar o sistema operativo num computador cliente do Configuration Manager.  

 As informações de estado de utilizador são capturadas e restauradas utilizando sequências de tarefas. Quando as informações de estado de utilizador são capturadas, podem ser armazenadas de uma das seguintes formas:  

-   Pode armazenar os dados de estado de utilizador remotamente através da configuração de um ponto de migração de estado. A sequência de tarefas de captura envia os dados para o ponto de migração de estado. Em seguida, depois de o sistema operativo ser implementado, a sequência de tarefas de restauro obtém os dados e restaura o estado de utilizador no computador de destino.  

-   Pode armazenar os dados de estado de utilizador localmente numa localização específica. Neste cenário, a sequência de tarefas de captura copia os dados de utilizador para uma localização específica no computador de destino. Em seguida, depois de o sistema operativo ser implementado, a sequência de tarefas de restauro obtém os dados de utilizador dessa localização.  

-   Pode especificar ligações fixas que podem ser utilizadas para restaurar os dados de utilizador na localização original. Neste cenário, os dados de estado de utilizador permanecem na unidade quando o sistema operativo anterior é removido. Em seguida, depois de o sistema operativo ser implementado, a sequência de tarefas de restauro utiliza as ligações fixas para restaurar os dados de estado de utilizador na localização original.  

 Para obter mais informações [gerir o estado do utilizador](../get-started/manage-user-state.md).  

##  <a name="BKMK_UnknownComputer"></a> Implementar em computadores desconhecidos  
 Pode implementar um sistema operativo em computadores que não são geridos pelo Configuration Manager. Não existe nenhum registo desses computadores na base de dados do Configuration Manager. Estes computadores são designados por computadores desconhecidos. Os computadores desconhecidos incluem o seguinte:  

-   Um computador onde não está instalado o cliente do Configuration Manager  

-   Um computador que não é importado para o Configuration Manager  

-   Um computador que não é detetado pelo Configuration Manager  

 Para obter mais informações, consulte o artigo [preparar para implementações de computadores desconhecidos](../get-started/prepare-for-unknown-computer-deployments.md).  

##  <a name="BKMK_UDA"></a> Associar utilizadores a um computador  
 Quando implementa um sistema operativo, pode associar utilizadores ao computador de destino para suportar ações de afinidade dispositivo/utilizador. Quando associa um utilizador ao computador de destino, posteriormente, o utilizador administrativo poderá efetuar ações em qualquer computador que esteja associado a esse utilizador, como implementar uma aplicação no computador de um utilizador específico. No entanto, quando implementa um sistema operativo, não é possível implementar o sistema operativo no computador de um utilizador específico. Para obter mais informações, consulte o artigo [associar utilizadores um computador de destino](../get-started/associate-users-with-a-destination-computer.md).  

##  <a name="BKMK_TaskSequences"></a> Utilizar sequências de tarefas para automatizar passos  
 Pode criar sequências de tarefas para executar uma variedade de tarefas no ambiente do Configuration Manager. As ações da sequência de tarefas são definidas nos passos individuais da sequência. Quando a sequência de tarefas é executada, as ações de cada passo são efetuadas ao nível da linha de comandos, sem necessidade de intervenção do utilizador. Pode utilizar sequências de tarefas para o seguinte:  

-   [Criar uma sequência de tarefas para instalar um sistema operativo](../deploy-use/create-a-task-sequence-to-install-an-operating-system.md)  

-   [Criar uma sequência de tarefas para implementações do sistema de operativo](../deploy-use/create-a-task-sequence-for-non-operating-system-deployments.md)  

-   [Criar uma sequência de tarefas para capturar um sistema operativo](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md)  

-   [Criar uma sequência de tarefas para capturar e restaurar o estado do utilizador](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md)  

-   [Criar uma sequência de tarefas personalizada](../deploy-use/create-a-custom-task-sequence.md)  

