---
title: "Utilizar o PXE para implementar o Windows através da rede"
titleSuffix: Configuration Manager
description: "Utilize implementações de sistema operativo iniciadas por PXE para atualizar o sistema operativo do computador ou para instalar uma nova versão do Windows num novo computador."
ms.custom: na
ms.date: 06/15/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: da5f8b61-2386-4530-ad54-1a5c51911f07
caps.latest.revision: "19"
caps.handback.revision: "0"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: 017a8f0d5b38145f6708e61ff5d7b2c3614b62a0
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="use-pxe-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Utilizar o PXE para implementar o Windows na rede com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Ambiente de execução pré-arranque (PXE) iniciada implementações do sistema operativo no System Center Configuration Manager cliente permitem computadores pedem e implementar sistemas operativos através da rede. Neste cenário de implementação, enviar a imagem do sistema operativo e imagens de arranque x86 e x64 com o Windows PE para um ponto de distribuição configurado para aceitar pedidos de arranque PXE.

> [!NOTE]  
>  Quando cria uma implementação do sistema operativo que computadores de BIOS de destinos apenas x64, ambas as x64 arrancar a imagem e x86 imagem de arranque tem de estar disponível no ponto de distribuição.

Pode utilizar implementações do sistema operativo iniciadas por PXE nos seguintes cenários de implementação do sistema operativo:

-   [Atualizar um computador existente com uma nova versão do Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Instalar uma nova versão do Windows num novo computador (bare-metal)](install-new-windows-version-new-computer-bare-metal.md)  

Conclua os passos dos cenários de implementação do sistema operativo e, em seguida, utilize as secções seguintes para se preparar para implementações iniciadas por PXE.

##  <a name="BKMK_Configure"></a> Configurar pelo menos um ponto de distribuição para aceitar pedidos PXE
Para implementar sistemas operativos em clientes que efetuam pedidos de arranque PXE, utilize um ou mais pontos de distribuição configurados para responder aos pedidos de arranque PXE. Para obter os passos ativar o PXE num ponto de distribuição, consulte [configurar pontos de distribuição para aceitar PXE pedidos](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint).

## <a name="prepare-a-pxe-enabled-boot-image"></a>Preparar uma imagem de arranque preparada para PXE
Para utilizar o PXE para implementar um sistema operativo, tem de ter imagens de arranque preparada para PXE x86 e x64 distribuídas por um ou mais pontos de distribuição preparados para PXE. Utilize as informações para ativar o PXE numa imagem de arranque e distribuí-la por pontos de distribuição:

-   Para ativar o PXE numa imagem de arranque, selecione **implementar esta imagem de arranque a partir do ponto de distribuição com PXE ativado** do **origem de dados** separador nas propriedades da imagem de arranque.

-   Se alterar as propriedades da imagem de arranque, redistribuir a imagem de arranque para pontos de distribuição. Para obter mais informações, consulte [distribuir conteúdo](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).

##  <a name="BKMK_PXEExclusionList"></a> Criar uma lista de exclusões para implementações PXE
Quando implementar sistemas operativos com PXE, pode criar uma lista de exclusões em cada ponto de distribuição. Adicione os endereços MAC à lista de exclusão dos computadores que pretende que o ponto de distribuição para ignorar. Os computadores listados não irão receber as sequências de tarefas de implementação utilizadas pelo Configuration Manager para a implementação de PXE.

#### <a name="to-create-the-exclusion-list"></a>Para criar a lista de exclusão

1.  Crie um ficheiro de texto no ponto de distribuição que esteja preparado para PXE. Por exemplo, atribua a este ficheiro de texto o nome **pxeExceptions.txt**.

2.  Utilize um editor de texto simples, como o Notepad e adicione os endereços MAC dos computadores a ser ignorada pelo ponto de distribuição com PXE ativado. Separe os valores dos endereços MAC por dois pontos e introduza cada endereço numa linha separada. Por exemplo: `01:23:45:67:89:ab`

3.  Guarde o ficheiro de texto no servidor do sistema de sites do ponto de distribuição preparado para PXE. O ficheiro de texto pode ser guardado para qualquer localização no servidor.

4.  Editar o registo do ponto de distribuição com PXE ativado para criar um **MACIgnoreListFile** chave de registo. Adicione o valor de cadeia do caminho completo para o ficheiro de texto no servidor do sistema de sites de ponto de distribuição com PXE ativado. Utilize o caminho de registo seguinte:

     **HKLM\Software\Microsoft\SMS\DP**  

    > [!WARNING]  
    >  A utilização incorreta do Editor de registo poderá causar problemas graves que poderão exigir a reinstalação do sistema operativo. A Microsoft não garante que consiga resolver os problemas resultantes da utilização incorreta do Editor de Registo. A utilização do Editor de Registo é da exclusiva responsabilidade do utilizador.

     Não é necessário reiniciar o servidor depois de efetuar esta alteração ao registo.

##  <a name="BKMK_RamDiskTFTP"></a>Tamanho do bloco TFTP do disco de RAM e o tamanho da janela
Pode personalizar o tamanho do bloco TFTP do disco de RAM e a partir do Configuration Manager versão 1606, o tamanho da janela de pontos de distribuição com PXE ativado. Se tiver personalizado a rede, poderá fazer com que a transferência da imagem de arranque falhe, com um erro de tempo limite excedido, porque o tamanho do bloco ou da janela é demasiado grande. A personalização do tamanho do bloco TFTP do disco de RAM e do tamanho da janela permitem otimizar o tráfego TFTP ao utilizar o PXE para satisfazer requisitos de rede específicos. Teste as definições personalizadas no seu ambiente para determinar o método mais eficaz. Para obter mais informações, consulte [personalizar o tamanho do bloco TFTP do disco de RAM e o tamanho da janela em pontos de distribuição com PXE ativado](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP).

## <a name="configure-deployment-settings"></a>Configurar definições de implementação
Para utilizar uma implementação do sistema operativo iniciada por PXE, tem de configurar a implementação para disponibilizar o sistema operativo nos pedidos de arranque PXE. Pode configurar os sistemas operativos disponíveis no **definições de implementação** página do Assistente de implementação de Software ou o **definições de implementação** separador nas propriedades para a implementação. Na definição **Tornar disponível para o seguinte** , configure um dos seguintes:

-   Clientes do Configuration Manager, suportes de dados e PXE

-   Apenas suportes de dados e PXE

-   Apenas suportes de dados e PXE (oculto)

##  <a name="BKMK_Deploy"></a> Implementar a sequência de tarefas
Implemente o sistema operativo numa coleção de destino. Para obter mais informações, veja [Implementar uma sequência de tarefas](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS). Quando implementar sistemas operativos através de PXE, pode configurar se a implementação é necessária ou se está disponível.

-   **Implementação necessária**: Requer a utilização de implementações PXE sem qualquer intervenção do utilizador. O utilizador não poderá ignorar o arranque PXE. No entanto, se o utilizador cancela o arranque PXE antes do ponto de distribuição responde, o sistema operativo não será implementado.

-   **Implementação disponível**: As implementações disponíveis exigem que o utilizador esteja presente no computador de destino para poder premir a tecla F12 para continuar o processo de arranque PXE. Se o utilizador não estiver presente para premir a tecla F12, o computador arrancará no sistema operativo atual ou do dispositivo de arranque disponível seguinte.

Pode Reimplementar uma implementação de PXE necessária limpando o estado da última implementação PXE atribuída a uma colecção do Configuration Manager ou num computador. Esta ação repõe o estado dessa implementação e reinstala as implementações necessárias mais recentes.

> [!IMPORTANT]
> O protocolo PXE não é seguro. Certifique-se de que o servidor PXE e o cliente PXE estão localizados numa rede fisicamente segura, como um centro de dados, para evitar o acesso não autorizado ao site.

##  <a name="how-is-the-boot-image-selected-for-clients-booting-with-pxe"></a>Como a imagem de arranque está selecionada para clientes de arranque com PXE?
Quando um cliente arranca com PXE, o Configuration Manager fornece o cliente com uma imagem de arranque para utilizar. A partir do Configuration Manager versão 1606, o Configuration Manager utiliza uma imagem de arranque com uma correspondência exata arquitetura. Se uma imagem de arranque com a arquitetura de exata não estiver disponível, o Configuration Manager utiliza uma imagem de arranque com uma arquitetura compatível. A lista seguinte fornece detalhes sobre como uma imagem de arranque está selecionada para clientes de arranque com PXE.
1. O Configuration Manager procura na base de dados do site para o registo do sistema que corresponde ao endereço MAC ou o GUID do SMBIOS do cliente que está a tentar efetuar o arranque.  

    > [!NOTE]
    > Se um computador que está atribuído a um site arranca no PXE para um site diferente, as políticas não são visíveis para o computador. Por exemplo, se um cliente já estiver atribuído ao site um, o ponto de gestão e o ponto de distribuição para o local B não será capazes de políticas de acesso do site A. O cliente não será com êxito o arranque PXE.

2. Procura do Configuration Manager para sequências de tarefas que são implementadas no registo de sistema foi encontrado no passo 1.

3. Na lista de sequências de tarefas foi encontrado no passo 2, o Configuration Manager procura uma imagem de arranque que corresponda à arquitetura do cliente que está a tentar efetuar o arranque. Se for encontrada uma imagem de arranque com a mesma arquitetura, essa imagem de arranque é utilizada.

4. Se uma imagem de arranque não for encontrada com a mesma arquitetura, procura do Configuration Manager para uma imagem de arranque que é compatível com a arquitetura do cliente. Procura na lista de sequências de tarefas foi encontrado no passo 2. Por exemplo, um cliente de 64 bits é compatível com as imagens de arranque de 32 bits e 64 bits. Um cliente de 32 bits é compatível com apenas imagens de arranque de 32 bits. Um cliente UEFI é compatível com apenas imagens de arranque de 64 bits.
