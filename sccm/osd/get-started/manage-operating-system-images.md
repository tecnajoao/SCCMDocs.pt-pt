---
title: Gerir imagens do SO
titleSuffix: Configuration Manager
description: Saiba os métodos para gerir imagens de sistema operacional armazenadas nos arquivos de imagem (WIM) do Windows.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: fab13949-371c-4a4c-978e-471db1e54966
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ea320b42bfb08ec0023598d010375042d143c220
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56124075"
---
# <a name="manage-os-images-with-configuration-manager"></a>Gerir imagens do sistema operacional com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Imagens do sistema operacional no Configuration Manager são armazenadas no formato de ficheiro de imagem (WIM) do Windows. Estas imagens são uma coleção comprimida de ficheiros de referência e nas pastas usadas para instalar e configurar um novo sistema operacional num computador. Muitos cenários de implementação de SO requerem uma imagem de SO. 

Pode utilizar um [imagem predefinida do SO](#default-image), ou compilar a imagem de SO de um [computador de referência](#bkmk_capture) que configurar. Ao criar o computador de referência, adicione OS ficheiros, controladores, ficheiros de suporte, atualizações de software, ferramentas e aplicativos para o sistema operacional. Em seguida, capturá-la para criar o ficheiro de imagem. 

### <a name="default-image"></a>Imagem predefinida

Os ficheiros de instalação do Windows incluem a imagem predefinida do sistema operacional. Esta imagem é uma imagem de sistema operacional básica que contém um conjunto padrão de controladores. Quando utiliza a imagem predefinida do sistema operacional, utilize os passos de sequência de tarefas para instalar aplicações e efetuar outras configurações após o sistema operacional é instalado num dispositivo. Localize a imagem do SO predefinido nos ficheiros de origem do Windows: `\Sources\install.wim`.  

#### <a name="default-image-advantages"></a>Vantagens de imagem padrão

- O tamanho de imagem é menor do que uma imagem capturada.  

- Instalar aplicações e configurações com passos de sequência de tarefas é mais dinâmica. Por exemplo, altere as configurações e aplicações que instalar na sequência de tarefas, sem ter de recriar a imagem do dispositivo.  

#### <a name="default-image-disadvantages"></a>Desvantagens de imagem padrão

- A instalação do sistema operacional pode demorar mais tempo. A instalação da aplicação e outras configurações ocorrem depois de concluída a instalação de sistema operacional.  


### <a name="bkmk_capture"></a> Imagem capturada de um computador de referência

Para criar uma imagem personalizada do sistema operacional, crie um computador de referência com o SO desejado. Em seguida, instalar aplicações e configurar as definições. Capture a imagem do SO do computador de referência para criar o ficheiro WIM. Manualmente compilar computador de referência ou utilizar uma sequência de tarefas para automatizar alguns ou todos os passos de compilação. Para obter mais informações, consulte [imagens do sistema operacional personalizar](/sccm/osd/get-started/customize-operating-system-images).  

#### <a name="captured-image-advantages"></a>Vantagens da imagem capturada

- A instalação pode ser mais rápida do que utilizando a imagem predefinida. Por exemplo, os aplicativos podem ser pré-instalados com a imagem capturada do sistema operacional. Em seguida, não precisa de instalar esses aplicativos mesmo mais tarde, utilizando os passos de sequência de tarefas.  

#### <a name="captured-image-disadvantages"></a>Desvantagens da imagem capturada

- O tamanho da imagem é potencialmente maior do que a imagem predefinida.  

- Tem de criar uma nova imagem quando necessitar de atualizações para aplicações e ferramentas.  



##  <a name="BKMK_AddOSImages"></a> Adicionar uma imagem de SO  

Antes de poder utilizar uma imagem de SO, adicione-o para o seu site do Configuration Manager. 

1.  Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho, expanda **sistemas operativos**e, em seguida, selecione o **imagens do sistema operativo** nó.  

2.  No **home page** separador do Friso, no **Create** grupo, selecione **adicionar a imagem do sistema operativo**. Esta ação inicia o Assistente para adicionar imagem de sistema operativo.  

3.  Sobre o **origem de dados** , especifique a rede **caminho** para o ficheiro de imagem do sistema operacional. Por exemplo, `\\server\share\path\image.wim`.  

4.  Sobre o **gerais** , especifique as seguintes informações. Estas informações são úteis para fins de identificação quando tem mais do que uma imagem do SO.  

    -   **Nome**: Um nome exclusivo para a imagem. Por predefinição, o nome tem origem o nome do ficheiro WIM.  

    -   **Versão**: Um identificador de versão opcional. Esta propriedade não precisa ser a versão do SO da imagem. É, muitas vezes, versão da sua organização para o pacote.   

    -   **Comentário**: Uma breve descrição opcional.  

5.  Conclua o assistente.  


Em seguida, distribua a imagem do SO para pontos de distribuição.  



##  <a name="BKMK_DistributeBootImages"></a> Distribuir conteúdo para pontos de distribuição  

Distribua imagens do sistema operacional para pontos de distribuição, o mesmo que outro conteúdo. Antes de implementar a sequência de tarefas, distribua a imagem do SO para, pelo menos, um ponto de distribuição. Para mais informações, consulte [Distribute content](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute).  



[!INCLUDE [Apply software updates to an image](includes/wim-apply-updates.md)]



##  <a name="BKMK_OSImageMulticast"></a> Preparar a imagem do SO para implementações por multicast  

Utilize implementações por multicast para permitir que mais de um computador transfiram simultaneamente uma imagem de SO. A imagem é transferida por multicast aos clientes pelo ponto de distribuição, em vez de cada cliente baixar uma cópia da imagem do ponto de distribuição através de uma ligação separada. Ao escolher o método de implementação do sistema operacional para [utilizar multicast para implementar o Windows através da rede](/sccm/osd/deploy-use/use-multicast-to-deploy-windows-over-the-network), configurar a imagem do SO para suportar multicast. Em seguida, distribua a imagem para um ponto de distribuição com capacidade multicast. 

1.  Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho, expanda **sistemas operativos**e, em seguida, selecione o **imagens do sistema operativo** nó.  

2.  Selecione a imagem do SO que deseja distribuir para um ponto de distribuição com capacidade multicast.  

3.  Sobre o **home page** separador do Friso, no **propriedades** grupo, selecione **propriedades**.  

4.  Mude para o **definições de distribuição** separador e configure as seguintes opções:  

    -   **Permitir deste pacote a ser transferidos através de multicast (só WinPE)**: Selecione esta opção para o Configuration Manager para implementar em simultâneo a utilização de multicast de imagens do sistema operacional.  

    -   **Encriptar pacotes multicast**: Especifique se o site encripta a imagem antes de ser enviada para o ponto de distribuição. Se a imagem contém informações confidenciais, utilize esta opção. Se a imagem não está encriptada, seu conteúdo é visível em texto não encriptado na rede. Em seguida, um utilizador não autorizado poderia interceptar e exibir o conteúdo de imagem.  

    -   **Transferir este pacote apenas através de multicast**: Especifique se pretende que o ponto de distribuição implemente a imagem apenas durante uma sessão multicast.  

         Se selecionou **transferir este pacote apenas através de multicast**, também tem de especificar a opção de implementação de sequência de tarefas para **transferir o conteúdo localmente quando necessário para a sequência de tarefas em execução**. Para obter mais informações, veja [Deploy a task sequence (Implementar uma sequência de tarefas)](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS).   

5.  Selecione **OK** para guardar as definições e fechar as propriedades de imagem.  
