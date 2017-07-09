---
title: Use o PXE para implantar o Windows pela rede | Microsoft Docs
description: "Use implantações de sistema operacional iniciadas pelo PXE para atualizar o sistema operacional do computador ou para instalar uma nova versão do Windows em um novo computador."
ms.custom: na
ms.date: 06/15/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: da5f8b61-2386-4530-ad54-1a5c51911f07
caps.latest.revision: 19
caps.handback.revision: 0
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: f4c46bfab9b40b29654f4e883817a5508ab25b74
ms.openlocfilehash: b88ab3799027c78a8c605e934b247097b31e1d21
ms.contentlocale: pt-pt
ms.lasthandoff: 06/28/2017


---
# <a name="use-pxe-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Utilizar o PXE para implementar o Windows na rede com o System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

Ambiente Pre-Boot execution (PXE) iniciada implantações de sistema operacional no System Center Configuration Manager o cliente permitem que computadores solicitem e implantem sistemas operacionais pela rede. Nesse cenário de implantação, você envia a imagem do sistema operacional e as imagens de inicialização x86 e x64 do Windows PE para um ponto de distribuição configurado para aceitar solicitações de inicialização PXE.

> [!NOTE]  
>  Quando você criar uma implantação de sistema operacional que computadores com BIOS destinos apenas para x64, ambas as x64 x86 e imagem de inicialização imagem de inicialização deve estar disponível no ponto de distribuição.

Pode utilizar implementações do sistema operativo iniciadas por PXE nos seguintes cenários de implementação do sistema operativo:

-   [Atualizar um computador existente com uma nova versão do Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Instalar uma nova versão do Windows num novo computador (bare-metal)](install-new-windows-version-new-computer-bare-metal.md)  

Conclua as etapas em um dos cenários de implantação de sistema operacional e, em seguida, use as seções a seguir para preparar para implantações iniciadas pelo PXE.

##  <a name="BKMK_Configure"></a> Configurar pelo menos um ponto de distribuição para aceitar pedidos PXE
Para implantar sistemas operacionais em clientes que fazem solicitações de inicialização PXE, use um ou mais pontos de distribuição configurados para responder às solicitações de inicialização PXE. Para obter as etapas habilitar o PXE em um ponto de distribuição, consulte [Configurando pontos de distribuição para aceitar PXE solicitações](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint).

## <a name="prepare-a-pxe-enabled-boot-image"></a>Preparar uma imagem de arranque preparada para PXE
Para utilizar o PXE para implementar um sistema operativo, tem de ter imagens de arranque preparada para PXE x86 e x64 distribuídas por um ou mais pontos de distribuição preparados para PXE. Utilize as informações para ativar o PXE numa imagem de arranque e distribuí-la por pontos de distribuição:

-   Para habilitar o PXE em uma imagem de inicialização, selecione **implantar esta imagem de inicialização do ponto de distribuição habilitado para PXE** do **fonte de dados** guia nas propriedades da imagem de inicialização.

-   Se você alterar as propriedades da imagem de inicialização, redistribua a imagem de inicialização para pontos de distribuição. Para obter mais informações, consulte [distribuir conteúdo](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkdistributea-distribute-content).

##  <a name="BKMK_PXEExclusionList"></a> Criar uma lista de exclusões para implementações PXE
Quando você implanta sistemas operacionais com o PXE, você pode criar uma lista de exclusões em cada ponto de distribuição. Adicione os endereços MAC à lista de exclusão dos computadores que você deseja que o ponto de distribuição para ignorar. Computadores listados não recebem as sequências de tarefas de implantação do Configuration Manager usa para a implantação do PXE.

#### <a name="to-create-the-exclusion-list"></a>Para criar a lista de exclusão

1.  Crie um ficheiro de texto no ponto de distribuição que esteja preparado para PXE. Por exemplo, atribua a este ficheiro de texto o nome **pxeExceptions.txt**.

2.  Use um editor de texto sem formatação, como o bloco de notas e adicione os endereços MAC dos computadores sejam ignorados pelo ponto de distribuição habilitado para PXE. Separe os valores dos endereços MAC por dois pontos e introduza cada endereço numa linha separada. Por exemplo: `01:23:45:67:89:ab`

3.  Guarde o ficheiro de texto no servidor do sistema de sites do ponto de distribuição preparado para PXE. O arquivo de texto pode ser salvo em qualquer local no servidor.

4.  Editar o registro do ponto de distribuição habilitado para PXE para criar um **MACIgnoreListFile** chave do registro. Adicione o valor de cadeia de caracteres do caminho completo para o arquivo de texto no servidor de sistema de site do ponto de distribuição habilitado para PXE. Utilize o caminho de registo seguinte:

     **HKLM\Software\Microsoft\SMS\DP**  

    > [!WARNING]  
    >  Se você usar o Editor do Registro incorretamente, você poderá causar sérios problemas que talvez exijam a reinstalação do sistema operacional. A Microsoft não garante que consiga resolver os problemas resultantes da utilização incorreta do Editor de Registo. A utilização do Editor de Registo é da exclusiva responsabilidade do utilizador.

     Não é necessário reiniciar o servidor depois de efetuar esta alteração ao registo.

##  <a name="BKMK_RamDiskTFTP"></a>Tamanho de bloco do RamDisk TFTP e tamanho da janela
Você pode personalizar o tamanho de bloco do RamDisk TFTP e a partir do Configuration Manager versão 1606, o tamanho da janela de pontos de distribuição habilitados para PXE. Se tiver personalizado a rede, poderá fazer com que a transferência da imagem de arranque falhe, com um erro de tempo limite excedido, porque o tamanho do bloco ou da janela é demasiado grande. A personalização do tamanho do bloco TFTP do disco de RAM e do tamanho da janela permitem otimizar o tráfego TFTP ao utilizar o PXE para satisfazer requisitos de rede específicos. Teste as configurações personalizadas em seu ambiente para determinar o método mais eficiente. Para obter mais informações, consulte [personalizar o tamanho da janela pontos de distribuição habilitados para PXE e o tamanho de bloco do RamDisk TFTP](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP).

## <a name="configure-deployment-settings"></a>Configurar definições de implementação
Para utilizar uma implementação do sistema operativo iniciada por PXE, tem de configurar a implementação para disponibilizar o sistema operativo nos pedidos de arranque PXE. Você pode configurar os sistemas operacionais disponíveis no **configurações de implantação** página do Assistente de implantação de Software ou o **configurações de implantação** guia nas propriedades de implantação. Na definição **Tornar disponível para o seguinte** , configure um dos seguintes:

-   Clientes do Configuration Manager, mídia e PXE

-   Apenas suportes de dados e PXE

-   Apenas suportes de dados e PXE (oculto)

##  <a name="BKMK_Deploy"></a> Implementar a sequência de tarefas
Implemente o sistema operativo numa coleção de destino. Para obter mais informações, veja [Implementar uma sequência de tarefas](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS). Quando implementar sistemas operativos através de PXE, pode configurar se a implementação é necessária ou se está disponível.

-   **Implantação necessária**: Exigia o uso de implantações PXE sem qualquer intervenção do usuário. O usuário não será capaz de ignorar a inicialização PXE. No entanto, se o usuário cancelar a inicialização PXE antes do ponto de distribuição responde, o sistema operacional não será implantado.

-   **Implantação disponível**: As implantações disponíveis requerem que o usuário esteja presente no computador de destino para que eles podem pressionar a tecla F12 para continuar o processo de inicialização PXE. Se o utilizador não estiver presente para premir a tecla F12, o computador arrancará no sistema operativo atual ou do dispositivo de arranque disponível seguinte.

Você pode reimplantar uma implantação PXE necessária apagando o status da última implantação PXE atribuída a um computador ou uma coleção do Configuration Manager. Essa ação redefine o status dessa implantação e reinstala as implantações necessárias mais recentes.

> [!IMPORTANT]
> O protocolo PXE não é seguro. Certifique-se de que o servidor PXE e o cliente PXE estão localizados numa rede fisicamente segura, como um centro de dados, para evitar o acesso não autorizado ao site.

##  <a name="how-is-the-boot-image-selected-for-clients-booting-with-pxe"></a>Como a imagem de inicialização é selecionada para inicialização com o PXE de clientes?
Quando um cliente é inicializado com o PXE, o Configuration Manager fornece ao cliente com uma imagem de inicialização para usar. A partir da versão 1606 do Configuration Manager, Configuration Manager usa uma imagem de inicialização com uma correspondência exata de arquitetura. Se uma imagem de inicialização com a arquitetura exata não estiver disponível, o Configuration Manager usa uma imagem de inicialização com uma arquitetura compatível. A lista a seguir fornece detalhes sobre como uma imagem de inicialização é selecionada para clientes de inicialização com o PXE.
1. Gerenciador de configuração examina o banco de dados do site para o registro do sistema que corresponde ao endereço MAC ou SMBIOS do cliente que está tentando inicializar.  

    > [!NOTE]
    > Se um computador que é atribuído a um site inicializar o PXE para um site diferente, as políticas não são visíveis para o computador. Por exemplo, se um cliente já está atribuído a um local, o ponto de gerenciamento e ponto de distribuição para o site B não conseguirá acessar as políticas de site A. O cliente não se preocupe com êxito a inicialização PXE.

2. Gerenciador de configuração procura sequências de tarefas que são implantadas no registro do sistema encontrado na etapa 1.

3. Na lista de sequências de tarefas encontrado na etapa 2, o Configuration Manager procura uma imagem de inicialização que corresponda à arquitetura do cliente que está tentando inicializar. Se uma imagem de inicialização é encontrada com a mesma arquitetura, a imagem de inicialização é usada.

4. Se uma imagem de inicialização não foi encontrada com a mesma arquitetura, o Configuration Manager procura uma imagem de inicialização que é compatível com a arquitetura do cliente. Ele procura na lista de sequências de tarefas encontrado na etapa 2. Por exemplo, um cliente de 64 bits é compatível com imagens de inicialização de 32 bits e 64 bits. Um cliente de 32 bits é compatível com apenas as imagens de inicialização de 32 bits. Um cliente UEFI é compatível com apenas as imagens de inicialização de 64 bits.

