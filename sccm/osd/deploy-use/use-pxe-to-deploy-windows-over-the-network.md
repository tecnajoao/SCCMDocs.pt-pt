---
title: Utilizar o PXE para OSD através da rede
titleSuffix: Configuration Manager
description: Utilize implementações de sistema operacional iniciadas por PXE para atualizar o sistema operativo de um computador ou para instalar uma nova versão do Windows num novo computador.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: da5f8b61-2386-4530-ad54-1a5c51911f07
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 75e463d27475e82677e91b00bfba4c4287d463ee
ms.sourcegitcommit: f2a1fa59fb3870a6bebca61daf15c0c157e9fdd6
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/04/2019
ms.locfileid: "54030993"
---
# <a name="use-pxe-to-deploy-windows-over-the-network-with-configuration-manager"></a>Utilizar o PXE para implementar o Windows na rede com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Ambiente de execução pré-arranque (PXE)-iniciadas implementações de sistema operacional no Configuration Manager permitem que os clientes pedir e implementar sistemas operativos na rede. Neste cenário de implementação, envie a imagem do SO e as imagens de arranque para um ponto de distribuição com PXE ativado.

> [!NOTE]  
>  Quando cria uma implementação do SO que visam apenas x64 BIOS computadores, tanto o x64 arrancar a imagem e x86 imagem de arranque tem de estar disponível no ponto de distribuição.

Pode utilizar implementações do sistema operacional iniciadas por PXE nos seguintes cenários:

-   [Atualizar um computador existente com uma nova versão do Windows](/sccm/osd/deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows)  

-   [Instalar uma nova versão do Windows num novo computador (bare-metal)](/sccm/osd/deploy-use/install-new-windows-version-new-computer-bare-metal)  

Conclua os passos dos cenários de implementação do sistema operacional e, em seguida, utilize as secções neste artigo para se preparar para as implementações iniciadas por PXE.



##  <a name="BKMK_Configure"></a> Configurar pelo menos um ponto de distribuição para aceitar pedidos PXE

Para implementar sistemas operativos em clientes do Configuration Manager que efetuam pedidos de arranque PXE, tem de configurar um ou mais pontos de distribuição para aceitar pedidos PXE. Depois de configurar o ponto de distribuição, ele responde a pedidos de arranque PXE e determina a ação de implementação adequada a tomar. Para mais informações, consulte [Install or modify a distribution point](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  

> [!NOTE]  
>  Quando configurar um único PXE ativado o ponto de distribuição para suportar várias sub-redes não é suportado para utilizar as opções de DHCP. Configure programas auxiliares IP os routers para permitir pedidos PXE a reencaminhar para os pontos de distribuição PXE ativado.

> [!NOTE]  
>  Não é suportado para utilizar o dispositivo de resposta PXE sem o WDS em servidores que também estão a utilizar um servidor DHCP.

## <a name="prepare-a-pxe-enabled-boot-image"></a>Preparar uma imagem de arranque preparada para PXE

Para utilizar o PXE para implementar um sistema operacional, tem de ter o x86 e x64 distribuídas as imagens de arranque preparada para PXE para um ou mais pontos de distribuição com PXE ativado. Utilize as informações para ativar o PXE numa imagem de arranque e distribuí-la por pontos de distribuição:

-   Para ativar o PXE numa imagem de arranque, selecione **implementar esta imagem de arranque a partir do ponto de distribuição ativado por PXE** partir do **origem de dados** separador nas propriedades de imagem de arranque.

-   Se alterar as propriedades da imagem de arranque, atualizar e redistribuir a imagem de arranque para pontos de distribuição. Para mais informações, consulte [Distribute content](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute).



##  <a name="BKMK_PXEExclusionList"></a> Criar uma lista de exclusões para implementações PXE

Ao implementar sistemas operativos com PXE, pode criar uma lista de exclusões em cada ponto de distribuição. Adicione os endereços MAC à lista de exclusão, os computadores que pretende que o ponto de distribuição para ignorar. Computadores listados não recebem as sequências de tarefas de implementação utilizadas pelo Configuration Manager para a implementação de PXE.

#### <a name="to-create-the-exclusion-list"></a>Para criar a lista de exclusão

1.  Crie um ficheiro de texto no ponto de distribuição que esteja preparado para PXE. Por exemplo, atribua a este ficheiro de texto o nome **pxeExceptions.txt**.  

2.  Utilize um editor de texto sem formatação, como o bloco de notas e adicione os endereços MAC dos computadores a ser ignorados pelo ponto de distribuição com PXE ativado. Separe os valores dos endereços MAC por dois pontos e introduza cada endereço numa linha separada. Por exemplo: `01:23:45:67:89:ab`  

3.  Guarde o ficheiro de texto no servidor do sistema de sites do ponto de distribuição preparado para PXE. O arquivo de texto pode ser salvas em qualquer local no servidor.  

4.  Editar o registo do ponto de distribuição com PXE ativado para criar uma **MACIgnoreListFile** chave de registo. Adicione o valor da cadeia do caminho completo para o ficheiro de texto no servidor do sistema de sites de ponto de distribuição com PXE ativado. Utilize o caminho de registo seguinte:  

     `HKLM\Software\Microsoft\SMS\DP`  

    > [!WARNING]  
    >  A utilização incorreta do Editor de registo poderá causar problemas graves que podem exigir a reinstalação do sistema operativo. A Microsoft não garante que consiga resolver os problemas resultantes da utilização incorreta do Editor de Registo. A utilização do Editor de Registo é da exclusiva responsabilidade do utilizador.  

5. Reinicie o serviço WDS ou o serviço de resposta PXE depois de efetuar esta alteração ao registo. Não precisa de reiniciar o servidor.<!--512129-->  



## <a name="manage-duplicate-hardware-identifiers"></a>Gerir os identificadores de hardware duplicados

O Configuration Manager podem reconhecer vários computadores como o mesmo dispositivo, se têm duplicados SMBIOS atributos ou utilizar um adaptador de rede partilhada. Reduza esses problemas ao gerir os identificadores de hardware duplicado nas definições de hierarquia. Para obter mais informações, consulte [identificadores de hardware duplicados gerir](/sccm/core/clients/manage/manage-clients#manage-duplicate-hardware-identifiers).



##  <a name="BKMK_RamDiskTFTP"></a>Tamanho do bloco TFTP do disco e o tamanho da janela

Pode personalizar os tamanhos de bloco e a janela de TFTP de Ramdisk baseada em pontos de distribuição com PXE ativado. Se personalizou sua rede, um tamanho de bloco ou da janela grandes pode causar falha com um erro de tempo limite a transferência da imagem de arranque. As personalizações de tamanho de bloco e a janela de TFTP de RamDisk permitem-lhe otimizar o tráfego TFTP ao utilizar o PXE para satisfazer os seus requisitos de rede específicas. Para determinar que configuração é mais eficiente, teste as definições personalizadas no seu ambiente. Para obter mais informações, consulte [personalizar o tamanho do bloco TFTP do disco e o tamanho da janela em pontos de distribuição com PXE ativado](/sccm/osd/get-started/prepare-site-system-roles-for-operating-system-deployments#BKMK_RamDiskTFTP).



## <a name="configure-deployment-settings"></a>Configurar definições de implementação

Para utilizar uma implementação de sistema operacional iniciadas por PXE, configure a implementação para disponibilizar o sistema operacional para pedidos de arranque PXE. Configurar os sistemas operativos disponíveis no **definições de implementação** separador nas propriedades de implementação. Para o **tornar disponível para o seguinte** definição, selecione uma das seguintes opções:

-   Clientes do Configuration Manager, suportes de dados e PXE

-   Apenas suportes de dados e PXE

-   Apenas suportes de dados e PXE (oculto)



##  <a name="BKMK_Deploy"></a> Implementar a sequência de tarefas

Implantar o sistema operacional a uma coleção de destino. Para obter mais informações, veja [Deploy a task sequence (Implementar uma sequência de tarefas)](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS). Quando implementar sistemas operativos através de PXE, pode configurar se a implementação é necessária ou se está disponível.

-   **Implementação necessária**: É necessário o uso de implementações PXE sem qualquer intervenção do utilizador. O utilizador não é possível ignorar o arranque PXE. No entanto, se o utilizador cancelar o arranque PXE antes do ponto de distribuição responde, o sistema operacional não está implementado.

-   **Implementação disponível**: As implementações disponíveis exigem que o utilizador esteja presente no computador de destino. Um utilizador deve premir o **F12** tecla para continuar o processo de inicialização PXE. Se um utilizador não estiver presente para premir **F12**, o computador é inicializado no sistema operacional atual, ou a partir do dispositivo de arranque disponível seguinte.

Pode Reimplementar uma implementação de PXE necessária limpando o estado da última implementação PXE atribuída a uma coleção do Configuration Manager ou de um computador. Para obter mais informações sobre o **implementações de PXE necessária clara** ação, veja [gerir clientes](/sccm/core/clients/manage/manage-clients#BKMK_ManagingClients_DevicesNode) ou [gerir coleções](/sccm/core/clients/manage/collections/manage-collections#how-to-manage-device-collections). Esta ação repõe o estado dessa implementação e reinstala as implementações necessárias mais recentes.

> [!IMPORTANT]  
> O protocolo PXE não é seguro. Certifique-se de que o servidor PXE e o cliente PXE estão localizados numa rede fisicamente segura, tal como num centro de dados para impedir o acesso não autorizado ao seu site.



##  <a name="how-is-the-boot-image-selected-for-clients-booting-with-pxe"></a>Como é selecionada a imagem de arranque para inicialização com o PXE de clientes?

Quando um cliente efetua o arranque com PXE, o Configuration Manager fornece o cliente com uma imagem de arranque para utilizar. O Configuration Manager utiliza uma imagem de arranque com uma correspondência exata da arquitetura. Se uma imagem de arranque com a arquitetura exata não estiver disponível, o Configuration Manager utiliza uma imagem de arranque com uma arquitetura compatível. 

A lista seguinte fornece detalhes sobre como uma imagem de arranque é selecionada para inicialização com o PXE de clientes:  

1. O Configuration Manager examina o banco de dados do site para o registo do sistema que corresponde ao endereço MAC ou do SMBIOS do cliente que está a tentar efetuar o arranque.  

    > [!NOTE]  
    > Se um computador que está atribuído a um site efetua o arranque PXE para um site diferente, as políticas não são visíveis para o computador. Por exemplo, se um cliente já está atribuído ao local A, o ponto de gestão e o ponto de distribuição para o local B não são capazes de acessar as políticas do site A. O cliente com êxito não arranque PXE.  

2. Procura do Configuration Manager para sequências de tarefas que são implementadas para o registo de sistema encontrado no passo 1.  

3. Na lista de sequências de tarefas que localizou no passo 2, o Configuration Manager procura uma imagem de arranque que corresponda à arquitetura do cliente que está a tentar efetuar o arranque. Se uma imagem de arranque for encontrada com a mesma arquitetura, essa imagem de arranque é utilizada.  

4. Se uma imagem de arranque não for encontrada com a mesma arquitetura, o Configuration Manager procura uma imagem de arranque que é compatível com a arquitetura do cliente. Ele procura na lista de sequências de tarefas que localizou no passo 2. Por exemplo, um cliente de 64 bits é compatível com imagens de arranque de 32 bits e 64 bits. Um cliente de 32 bits é compatível com apenas as imagens de arranque de 32 bits. Um cliente UEFI é compatível com apenas as imagens de arranque de 64 bits.  
