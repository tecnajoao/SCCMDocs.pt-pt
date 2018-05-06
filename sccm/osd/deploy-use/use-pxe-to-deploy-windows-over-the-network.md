---
title: Utilizar o PXE para OSD através da rede
titleSuffix: Configuration Manager
description: Utilize implementações iniciadas por PXE SO para atualizar o sistema operativo do computador ou para instalar uma nova versão do Windows num novo computador.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: da5f8b61-2386-4530-ad54-1a5c51911f07
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: deb8321400eac4085cefca8686f2703cea5f659a
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="use-pxe-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Utilizar o PXE para implementar o Windows na rede com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Ambiente de execução pré-arranque (PXE)-as implementações de SO iniciadas no Configuration Manager permitem aos clientes pedir e implementar sistemas operativos através da rede. Neste cenário de implementação, enviar a imagem do SO e as imagens de arranque para um ponto de distribuição com PXE ativado.

> [!NOTE]  
>  Quando cria uma implementação de SO que computadores de BIOS de destinos apenas x64, ambas as x64 arrancar a imagem e x86 imagem de arranque tem de estar disponível no ponto de distribuição.

Pode utilizar implementações iniciadas por PXE SO nos seguintes cenários:

-   [Atualizar um computador existente com uma nova versão do Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Instalar uma nova versão do Windows num novo computador (bare-metal)](install-new-windows-version-new-computer-bare-metal.md)  

Conclua os passos dos cenários de implementação do SO e, em seguida, utilize as secções neste artigo para se preparar para implementações iniciadas por PXE.



##  <a name="BKMK_Configure"></a> Configurar pelo menos um ponto de distribuição para aceitar pedidos PXE
Para implementar sistemas operativos em clientes do Configuration Manager que efetuam pedidos de arranque PXE, tem de configurar um ou mais pontos de distribuição para aceitar pedidos PXE. Depois de configurar o ponto de distribuição, responde a pedidos de arranque PXE e determina a ação de implementação adequada a tomar. Para obter mais informações, consulte [instalar ou modificar um ponto de distribuição](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#pxe).  



## <a name="prepare-a-pxe-enabled-boot-image"></a>Preparar uma imagem de arranque preparada para PXE
Para utilizar o PXE para implementar o sistema operativo, tem de ter x86 e x64 distribuídas as imagens de arranque preparada para PXE para um ou mais pontos de distribuição com PXE ativado. Utilize as informações para ativar o PXE numa imagem de arranque e distribuí-la por pontos de distribuição:

-   Para ativar o PXE numa imagem de arranque, selecione **implementar esta imagem de arranque a partir do ponto de distribuição com PXE ativado** do **origem de dados** separador nas propriedades da imagem de arranque.

-   Se alterar as propriedades da imagem de arranque, redistribuir a imagem de arranque para pontos de distribuição. Para obter mais informações, consulte [distribuir conteúdo](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).



##  <a name="BKMK_PXEExclusionList"></a> Criar uma lista de exclusões para implementações PXE
Quando implementar sistemas operativos com PXE, pode criar uma lista de exclusões em cada ponto de distribuição. Adicione os endereços MAC à lista de exclusão dos computadores que pretende que o ponto de distribuição para ignorar. Computadores listados não recebem as sequências de tarefas de implementação utilizadas pelo Configuration Manager para a implementação de PXE.

#### <a name="to-create-the-exclusion-list"></a>Para criar a lista de exclusão

1.  Crie um ficheiro de texto no ponto de distribuição que esteja preparado para PXE. Por exemplo, atribua a este ficheiro de texto o nome **pxeExceptions.txt**.

2.  Utilize um editor de texto simples, como o Notepad e adicione os endereços MAC dos computadores a ser ignorada pelo ponto de distribuição com PXE ativado. Separe os valores dos endereços MAC por dois pontos e introduza cada endereço numa linha separada. Por exemplo: `01:23:45:67:89:ab`

3.  Guarde o ficheiro de texto no servidor do sistema de sites do ponto de distribuição preparado para PXE. O ficheiro de texto pode ser guardado para qualquer localização no servidor.

4.  Editar o registo do ponto de distribuição com PXE ativado para criar um **MACIgnoreListFile** chave de registo. Adicione o valor de cadeia do caminho completo para o ficheiro de texto no servidor do sistema de sites de ponto de distribuição com PXE ativado. Utilize o caminho de registo seguinte:

     **HKLM\Software\Microsoft\SMS\DP**  

    > [!WARNING]  
    >  A utilização incorreta do Editor de registo poderá causar problemas graves que poderão exigir a reinstalação do sistema operativo. A Microsoft não garante que consiga resolver os problemas resultantes da utilização incorreta do Editor de Registo. A utilização do Editor de Registo é da exclusiva responsabilidade do utilizador.

     Não é necessário reiniciar o servidor depois de efetuar esta alteração ao registo.



## <a name="manage-duplicate-hardware-identifiers"></a>Gerir os identificadores de hardware duplicados
O Configuration Manager pode reconhecer vários computadores como o mesmo dispositivo se têm atributos SMBIOS duplicados ou utilizar um adaptador de rede partilhada. Pode mitigar estes problemas através da gestão de hardware duplicados identificadores nas definições de hierarquia. Para obter mais informações, consulte [identificadores de hardware duplicados gerir](/sccm/core/clients/manage/manage-clients#manage-duplicate-hardware-identifiers).



##  <a name="BKMK_RamDiskTFTP"></a>Tamanho do bloco TFTP do disco de RAM e o tamanho da janela
Pode personalizar os tamanhos de bloco e a janela de TFTP do disco de RAM para pontos de distribuição com PXE ativado. Se tiver personalizado a rede, um tamanho de bloco ou da janela grande causam a transferência da imagem de arranque falhe, com um erro de tempo limite. As personalizações de tamanho de bloco e a janela de TFTP do disco de RAM permitem-lhe otimizar o tráfego TFTP ao utilizar o PXE para satisfazer os requisitos de rede específicos. Para determinar que configuração é mais eficiente, teste as definições personalizadas no seu ambiente. Para obter mais informações, consulte [personalizar o tamanho do bloco TFTP do disco de RAM e o tamanho da janela em pontos de distribuição com PXE ativado](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP).



## <a name="configure-deployment-settings"></a>Configurar definições de implementação
Para utilizar uma implementação de SO iniciadas por PXE, configure a implementação para disponibilizar o SO para pedidos de arranque PXE. Configurar os sistemas operativos disponíveis no **definições de implementação** separador nas propriedades de implementação. Para o **tornar disponível para o seguinte** definição, selecione uma das seguintes opções:

-   Clientes do Configuration Manager, suportes de dados e PXE

-   Apenas suportes de dados e PXE

-   Apenas suportes de dados e PXE (oculto)



##  <a name="BKMK_Deploy"></a> Implementar a sequência de tarefas
Implemente o sistema operativo numa coleção de destino. Para obter mais informações, veja [Implementar uma sequência de tarefas](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS). Quando implementar sistemas operativos através de PXE, pode configurar se a implementação é necessária ou se está disponível.

-   **Implementação necessária**: Requer a utilização de implementações PXE sem qualquer intervenção do utilizador. O utilizador não é possível ignorar o arranque PXE. No entanto, se o utilizador cancela o arranque PXE antes do ponto de distribuição responde, SO não está implementado.

-   **Implementação disponível**: As implementações disponíveis exigem que o utilizador esteja presente no computador de destino. Um utilizador deve premir a tecla F12 para continuar o processo de arranque PXE. Se um utilizador não estiver presente para premir a tecla F12, o computador arranca no sistema operativo atual ou o dispositivo de arranque disponível seguinte.

Pode Reimplementar uma implementação de PXE necessária limpando o estado da última implementação PXE atribuída a uma colecção do Configuration Manager ou num computador. Para mais informações sobre o **limpar implementações de PXE necessária** ação, consulte [gerir clientes](/sccm/core/clients/manage/manage-clients#BKMK_ManagingClients_DevicesNode) ou [gerir coleções](/sccm/core/clients/manage/collections/manage-collections#how-to-manage-device-collections). Esta ação repõe o estado dessa implementação e reinstala as implementações necessárias mais recentes.

> [!IMPORTANT]
> O protocolo PXE não é seguro. Certifique-se de que o servidor PXE e o cliente PXE estão localizados numa rede fisicamente segura, como um centro de dados, para evitar o acesso não autorizado ao site.



##  <a name="how-is-the-boot-image-selected-for-clients-booting-with-pxe"></a>Como a imagem de arranque está selecionada para clientes de arranque com PXE?
Quando um cliente arranca com PXE, o Configuration Manager fornece o cliente com uma imagem de arranque para utilizar. O Configuration Manager utiliza uma imagem de arranque com uma correspondência exata arquitetura. Se uma imagem de arranque com a arquitetura de exata não estiver disponível, o Configuration Manager utiliza uma imagem de arranque com uma arquitetura compatível. A lista seguinte fornece detalhes sobre como uma imagem de arranque está selecionada para clientes de arranque com PXE.
1. O Configuration Manager procura na base de dados do site para o registo do sistema que corresponde ao endereço MAC ou o GUID do SMBIOS do cliente que está a tentar efetuar o arranque.  

    > [!NOTE]
    > Se um computador que está atribuído a um site arranca no PXE para um site diferente, as políticas não são visíveis para o computador. Por exemplo, se um cliente já estiver atribuído ao site um, o ponto de gestão e o ponto de distribuição para o local B não são capazes de aceder às políticas do site A. O cliente não com êxito o arranque PXE.

2. Procura do Configuration Manager para sequências de tarefas que são implementadas no registo de sistema foi encontrado no passo 1.

3. Na lista de sequências de tarefas foi encontrado no passo 2, o Configuration Manager procura uma imagem de arranque que corresponda à arquitetura do cliente que está a tentar efetuar o arranque. Se for encontrada uma imagem de arranque com a mesma arquitetura, essa imagem de arranque é utilizada.

4. Se uma imagem de arranque não for encontrada com a mesma arquitetura, procura do Configuration Manager para uma imagem de arranque que é compatível com a arquitetura do cliente. Procura na lista de sequências de tarefas foi encontrado no passo 2. Por exemplo, um cliente de 64 bits é compatível com as imagens de arranque de 32 bits e 64 bits. Um cliente de 32 bits é compatível com apenas imagens de arranque de 32 bits. Um cliente UEFI é compatível com apenas imagens de arranque de 64 bits.
