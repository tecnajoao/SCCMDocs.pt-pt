---
title: "Utilizar o PXE para implementar o Windows através da rede | Documentos do Microsoft"
description: "Utilize implementações de sistema operativo iniciadas por PXE para atualizar o sistema operativo do computador ou para instalar uma nova versão do Windows num novo computador."
ms.custom: na
ms.date: 12/07/2016
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
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 3f44505c977b511223a083a960f871371c0ff133
ms.openlocfilehash: b22cdbd42693078caa47f41182ce73ea881c3515
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="use-pxe-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Utilizar o PXE para implementar o Windows na rede com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Implementações de sistema operativo iniciadas por PXE no System Center Configuration Manager permitem aos computadores cliente pedir e implementar sistemas operativos através da rede. Neste cenário de implementação do sistema operativo, a imagem do sistema operativo e as imagens de arranque do Windows PE x86 e x64 são enviadas para um ponto de distribuição configurado para aceitar pedidos de arranque PXE.  

> [!NOTE]  
>  Quando cria uma implementação do sistema operativo apenas com computadores BIOS de x64 como destino, ambas as imagens de arranque de x64 e de x86 têm de estar disponíveis no ponto de distribuição.  

 Pode utilizar implementações do sistema operativo iniciadas por PXE nos seguintes cenários de implementação do sistema operativo:  

-   [Atualizar um computador existente com uma nova versão do Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Instalar uma nova versão do Windows num novo computador (bare-metal)](install-new-windows-version-new-computer-bare-metal.md)  

 Conclua os passos num dos cenários de implementação do sistema operativo e utilize as secções seguintes para se preparar para as implementações iniciadas por PXE.  

##  <a name="BKMK_Configure"></a> Configurar pelo menos um ponto de distribuição para aceitar pedidos PXE  
 Para implementar sistemas operativos em clientes do Configuration Manager que efetuam pedidos de arranque PXE, tem de utilizar um ou mais pontos de distribuição que estão configurados para responder a pedidos de arranque PXE.  Para obter os passos ativar a opção PXE num ponto de distribuição, consulte o artigo [configurar pontos de distribuição para aceitar PXE pedidos](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint).  

## <a name="prepare-a-pxe-enabled-boot-image"></a>Preparar uma imagem de arranque preparada para PXE  
 Para utilizar o PXE para implementar um sistema operativo, tem de ter imagens de arranque preparada para PXE x86 e x64 distribuídas por um ou mais pontos de distribuição preparados para PXE. Utilize as informações para ativar o PXE numa imagem de arranque e distribuí-la por pontos de distribuição:  

-   Para ativar o PXE numa imagem de arranque, selecione  **Implementar esta imagem de arranque a partir do ponto de distribuição ativado por PXE** no separador **Origem de Dados** nas propriedades da imagem de arranque.  

-   Se alterar as propriedades da imagem de arranque, distribua novamente a imagem de arranque por pontos de distribuição. Para obter mais informações, consulte o artigo [distribuir conteúdo](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkdistributea-distribute-content).  

##  <a name="BKMK_PXEExclusionList"></a> Criar uma lista de exclusões para implementações PXE  
 Quando utiliza o PXE para implementar sistemas operativos, pode criar uma lista de exclusões em cada ponto de distribuição para ignorar pedidos de arranque PXE de computadores que estão na lista de exclusões. A lista de exclusões contém os endereços MAC dos computadores que pretende que o ponto de distribuição ignore. Estes computadores não recebem as sequências de tarefas de implementação utilizadas pelo Configuration Manager para a implementação de PXE.  

 Utilize os passos seguintes para criar a lista de exclusão do PXE.  

#### <a name="to-create-the-exclusion-list"></a>Para criar a lista de exclusão  

1.  Crie um ficheiro de texto no ponto de distribuição que esteja preparado para PXE. Por exemplo, atribua a este ficheiro de texto o nome **pxeExceptions.txt**.  

2.  Utilize um editor de texto padrão, como o Bloco de Notas, e adicione os endereços MAC dos computadores que deverão ser ignorados pelo ponto de distribuição preparado para PXE. Separe os valores dos endereços MAC por dois pontos e introduza cada endereço numa linha separada. Por exemplo: `01:23:45:67:89:ab`  

3.  Guarde o ficheiro de texto no servidor do sistema de sites do ponto de distribuição preparado para PXE. O ficheiro de texto pode ser guardado em qualquer localização do servidor.  

4.  Edite o registo do ponto de distribuição preparado para PXE para criar uma chave de registo do **MACIgnoreListFile** que contém o valor da cadeia do caminho completo para a localização do ficheiro de texto no servidor do sistema de sites do ponto de distribuição preparado para PXE. Utilize o caminho de registo seguinte:  

     **HKLM\Software\Microsoft\SMS\DP**  

    > [!WARNING]  
    >  A utilização incorreta do Editor de Registo poderá causar problemas graves que exijam a reinstalação do sistema operativo. A Microsoft não garante que consiga resolver os problemas resultantes da utilização incorreta do Editor de Registo. A utilização do Editor de Registo é da exclusiva responsabilidade do utilizador.  

     Não é necessário reiniciar o servidor depois de efetuar esta alteração ao registo.  

##  <a name="BKMK_RamDiskTFTP"></a>Tamanho de bloco de TFTP de disco de RAM e tamanho da janela  
Pode personalizar o tamanho de bloco de TFTP de disco de RAM e, a partir do Configuration Manager versão 1606, o tamanho da janela de pontos de distribuição com PXE ativado. Se tiver personalizado a rede, poderá fazer com que a transferência da imagem de arranque falhe, com um erro de tempo limite excedido, porque o tamanho do bloco ou da janela é demasiado grande. A personalização do tamanho do bloco TFTP do disco de RAM e do tamanho da janela permitem otimizar o tráfego TFTP ao utilizar o PXE para satisfazer requisitos de rede específicos. Terá de testar as definições personalizadas no seu ambiente para determinar o que é mais eficiente. Para obter mais informações, consulte o artigo [personalizar o tamanho de bloco de TFTP de disco de RAM e o tamanho da janela em pontos de distribuição com PXE ativado](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP).

## <a name="configure-deployment-settings"></a>Configurar definições de implementação  
 Para utilizar uma implementação do sistema operativo iniciada por PXE, tem de configurar a implementação para disponibilizar o sistema operativo nos pedidos de arranque PXE. Pode configurar esta opção na página **Definições de Implementação** do Assistente de Implementação de Software ou no separador **Definições de Implementação** , nas propriedades da implementação.  Na definição **Tornar disponível para o seguinte** , configure um dos seguintes:  

-   Clientes do Configuration Manager, suportes de dados e PXE  

-   Apenas suportes de dados e PXE  

-   Apenas suportes de dados e PXE (oculto)  

##  <a name="BKMK_Deploy"></a> Implementar a sequência de tarefas  
 Implemente o sistema operativo numa coleção de destino. Para obter mais informações, veja [Implementar uma sequência de tarefas](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS). Quando implementar sistemas operativos através de PXE, pode configurar se a implementação é necessária ou se está disponível.  

-   **Implementação necessária**: As implementações necessárias utilizarão o PXE sem qualquer intervenção do utilizador. O utilizador não poderá ignorar o arranque PXE. No entanto, se o utilizador cancelar o arranque PXE antes da resposta do ponto de distribuição, o sistema operativo não será implementado.  

-   **Implementação disponível**: As implementações disponíveis exigem que o utilizador esteja presente no computador de destino para poder premir a tecla F12 para continuar o processo de arranque PXE. Se o utilizador não estiver presente para premir a tecla F12, o computador arrancará no sistema operativo atual ou do dispositivo de arranque disponível seguinte.  

 É possível Reimplementar uma implementação de PXE necessária limpando o estado da última implementação de PXE atribuída a uma coleção do Configuration Manager ou num computador. Esta ação repõe o estado dessa implementação e reimplementa as implementações necessárias mais recentes.  

> [!IMPORTANT]  
>  O protocolo PXE não é seguro. Certifique-se de que o servidor PXE e o cliente PXE estão localizados numa rede fisicamente segura, como um centro de dados, para evitar o acesso não autorizado ao site.  

##  <a name="how-is-the-boot-image-selected-for-clients-booting-with-pxe"></a>Como a imagem de arranque está selecionada para clientes de arranque com PXE?
Quando um cliente inicia com PXE, o Configuration Manager oferece o cliente com uma imagem de arranque para utilizar. A partir do Configuration Manager versão 1606, o Configuration Manager utiliza uma imagem de arranque com uma correspondência exata arquitetura estiver disponível. Se uma imagem de arranque com a arquitetura exata não estiver disponível, o Configuration Manager utiliza uma imagem de arranque com uma arquitetura compatível. A lista seguinte fornece detalhes sobre como uma imagem de arranque está selecionada para clientes de arranque com PXE.
1. Procura do Configuration Manager na base de dados do site para o registo do sistema que corresponde ao endereço MAC ou SMBIOS do cliente que está a tentar efetuar o arranque.
    > [!NOTE]
    > Se um computador que está atribuído a um site arranca no PXE para um site de differenet, as políticas não estão visíveis para o computador. Por exemplo, se um cliente já é atribuído ao site A, o ponto de gestão e ponto de distribuição no site B não conseguirá aceder políticas a partir do site e o cliente irá não com êxito o arranque PXE.
2. Procura do Configuration Manager de sequências de tarefas que são implementadas no registo de sistema encontrado no passo 1.
3. Na lista de sequências de tarefas encontrada no passo 2, o Configuration Manager procura de uma imagem de arranque que corresponda à arquitetura do cliente que está a tentar efetuar o arranque. Se for encontrada uma imagem de arranque com a mesma arquitetura, essa imagem de arranque é utilizada.

4. Se não for encontrada uma imagem de arranque com o mesmo architecuture, o Configuration Manager procura de uma imagem de arranque (a partir da lista de sequências de tarefas encontrada no passo 2) que é compatível com a arquitetura do cliente que está a tentar efetuar o arranque. Por exemplo, um cliente de 64 bits é compatível com imagens de arranque de 32 bits e 64 bits. Um cliente de 32 bits é compatível com apenas as imagens de arranque de 32 bits. Um cliente UEFI é compatível com apenas as imagens de arranque de 64 bits.

