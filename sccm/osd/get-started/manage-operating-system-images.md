---
title: Gerir imagens de sistema operativo
titleSuffix: Configuration Manager
description: No Configuration Manager, saiba mais sobre os métodos que pode utilizar para gerir imagens de sistema operativo que estão armazenadas nos arquivos de Windows Imaging (WIM).
ms.date: 12/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: fab13949-371c-4a4c-978e-471db1e54966
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 82909cced6783f73608f155e64b7dd30b4087b06
ms.sourcegitcommit: a52255da16c9f8b0b60a6c299a369347c7e01bef
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/24/2018
ms.locfileid: "49989166"
---
# <a name="manage-operating-system-images-with-system-center-configuration-manager"></a>Gerir imagens de sistema operativo com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

As imagens de sistema operativo no Configuration Manager são armazenadas no formato de ficheiro Windows Imaging (WIM) e representam uma coleção comprimida de ficheiros e pastas de referência que são necessários para instalar e configurar com êxito um sistema operativo num computador. Para todos os cenários de implementação do sistema operativo, tem de selecionar uma imagem do sistema operativo.   Pode utilizar a imagem predefinida do sistema operativo ou compilar a imagem do sistema operativo a partir de um computador de referência que configurar. Quando criar o computador de referência, pode adicionar ficheiros do sistema operativo, controladores, ficheiros de suporte, atualizações de software, ferramentas e outras aplicações de software ao sistema operativo antes de capturá-la para criar o ficheiro de imagem. O seguinte fornece informações sobre cada método.  

 **Imagem predefinida**  

 A imagem predefinida do sistema operativo está incluída nos ficheiros de instalação do sistema operativo Windows. Esta imagem é uma imagem básica do sistema operativo que contém um conjunto padrão de controladores. Quando utiliza a imagem predefinida do sistema operativo, pode instalar aplicações e efetuar outras configurações após a instalação do sistema operativo utilizando os passos de sequência de tarefas.  A imagem predefinida do sistema operativo está localizada em <*caminho de origem do sistema operativo*>\Sources\install.wim.  

-   **Vantagens**  

    -   O tamanho de imagem é menor do que uma imagem capturada.  

    -   A instalação de aplicações e configurações com passos de sequência de tarefas é mais dinâmica. Por exemplo, pode alterar as aplicações que serão instaladas e as configurações na sequência de tarefas sem ter de recriar a imagem do sistema operativo.  

-   **Desvantagens**  

    -   A instalação do sistema operativo pode demorar mais tempo porque a instalação da aplicação e outras configurações ocorrem depois de concluída a instalação do sistema operativo.  

 **Imagem capturada**  

 Para criar uma imagem personalizada do sistema operativo, crie um computador de referência com o sistema operativo pretendido e instale aplicações, configure definições, etc. Em seguida, capture a imagem do sistema operativo a partir do computador de referência para criar o ficheiro WIM. Pode criar manualmente o computador de referência ou utilizar uma sequência de tarefas para automatizar alguns ou todos os passos da criação.   
Para obter os passos criar uma imagem personalizada do sistema operativo, consulte [personalizar imagens de sistema de operativo](customize-operating-system-images.md).  

-   **Vantagens**  

    -   A instalação pode ser mais rápida do que utilizando a imagem predefinida. Por exemplo, as aplicações podem ser pré-instaladas com a imagem do sistema operativo capturada, não sendo necessário instalar as aplicações mais tarde, utilizando os passos de sequência de tarefas.  

-   **Desvantagens**  

    -   A instalação do sistema operativo pode demorar mais tempo porque a instalação da aplicação e outras configurações ocorrem depois de concluída a instalação do sistema operativo.  


##  <a name="BKMK_AddOSImages"></a> Adicionar imagens do sistema operativo ao Configuration Manager  
 Antes de poder utilizar uma imagem do sistema operativo, tem de adicionar a imagem a um site do Configuration Manager. Utilize o procedimento seguinte para adicionar uma imagem do sistema operativo a um site.  

#### <a name="to-add-an-operating-system-image-to-a-site"></a>Para adicionar uma imagem do sistema operativo a um site  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software**, expanda **Sistemas Operativos** e clique em **Imagens de Sistema Operativo**.  

3.  No separador **Home page**, no grupo **Criar**, clique em **Adicionar Imagem de Sistema Operativo** para iniciar o Assistente para Adicionar Imagem de Sistema Operativo.  

4.  Na página **Origem de Dados**, especifique o caminho de rede para a imagem do sistema operativo. Por exemplo, especifique **\\\server\path\OS. WIM**.  

5.  Na página **Geral**, especifique as seguintes informações e clique em **Seguinte**. Estas informações são úteis para fins de identificação quando adiciona várias imagens do sistema operativo no mesmo site.  

    -   **Nome**: Especifique o nome da imagem. Por predefinição, o nome da imagem é retirado do ficheiro WIM.  

    -   **Versão**: Especifique a versão da imagem.  

    -   **Comentário**: Especifique uma breve descrição da imagem.  

6.  Conclua o assistente.  

 Pode agora distribuir a imagem do sistema operativo por pontos de distribuição.  

##  <a name="BKMK_DistributeBootImages"></a> Distribuir imagens do sistema operativo por pontos de distribuição  
 As imagens do sistema operativo são distribuídas por pontos de distribuição da mesma forma que são distribuídos outros conteúdos. Na maioria dos casos, terá de distribuir a imagem do sistema operativo por, pelo menos, um ponto de distribuição antes de implementar o sistema operativo. Para obter os passos para distribuir uma imagem do sistema operativo, veja [Distribuir conteúdo](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

##  <a name="BKMK_OSImagesApplyUpdates"></a> Aplicar atualizações de software numa imagem de sistema operativo  
 Periodicamente, são lançadas novas atualizações de software que são aplicáveis ao sistema operativo da imagem do sistema operativo. Antes de poder aplicar as atualizações de software numa imagem tem de ter as atualizações de software, infraestrutura na colocar, ter sincronizado com êxito as atualizações de software e transferidas as atualizações de softare para a biblioteca de conteúdos no servidor do site. Para obter mais informações, consulte [implementar atualizações de software](../../sum/deploy-use/deploy-software-updates.md).  

 Pode aplicar atualizações de software aplicáveis a uma imagem numa agenda especificada. Na agenda que especificar, o Configuration Manager aplica-se as atualizações de software que selecionar a imagem do sistema operativo e, em seguida, distribui opcionalmente a imagem atualizada para pontos de distribuição. As informações sobre a imagem do sistema operativo são armazenadas na base de dados do site, incluindo as atualizações de software que foram aplicadas no momento da importação. As atualizações de software aplicadas à imagem desde que esta foi inicialmente adicionada também são armazenadas na base de dados do site. Ao iniciar o assistente para aplicar as atualizações de software à imagem do sistema operativo, o assistente obtém uma lista de atualizações de software aplicáveis que ainda não foram aplicadas à imagem para que possa selecioná-las. Configuration Manager copia as atualizações de software da biblioteca de conteúdos no servidor do site e aplica as atualizações de software à imagem do sistema operativo.  

 Utilize o procedimento seguinte para aplicar atualizações de software numa imagem do sistema operativo.  

#### <a name="to-apply-software-updates-to-an-operating-system-image"></a>Para aplicar atualizações de software numa imagem do sistema operativo  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software**, expanda **Sistemas Operativos** e clique em **Imagens de Sistema Operativo**.  

3.  Selecione a imagem do sistema operativo em pretende aplicar atualizações de software.  

4.  No separador **Home page**, no grupo **Imagem do Sistema Operativo**, clique em **Agendar Atualizações** para iniciar o assistente.  

5.  Na página **Escolher as Atualizações** , selecione as atualizações de software para aplicar à imagem do sistema operativo e clique em **Seguinte**.  

6.  Na página **Definir Agendamento** , especifique as seguintes definições e clique em **Seguinte**.  

    1.  **Agenda**: Especifique a agenda para quando as atualizações de software são aplicadas à imagem do sistema operativo.  

    2.  **Continuar com o erro**:  Selecione esta opção para continuar a aplicar atualizações de software à imagem, mesmo se ocorrer um erro.  

    3.  **Distribuir a imagem por pontos de distribuição**: Selecione esta opção para atualizar a imagem de sistema operativo em pontos de distribuição depois de serem aplicadas as atualizações de software.  

7.  Na página **Resumo** , verifique as informações e clique em **Seguinte**.  

8.  Na página **Conclusão** , confirme que as atualizações de software foram aplicadas com êxito na imagem do sistema operativo.  

> [!NOTE]  
>  Para minimizar o tamanho da carga, a manutenção de pacotes de atualização do SO e imagens do sistema operacional remove a versão mais antiga.  

##  <a name="BKMK_OSImageMulticast"></a> Preparar a imagem de sistema operativo para implementações por multicast  
 Utilize implementações por multicast para permitir que vários computadores transfiram simultaneamente uma imagem do sistema operativo. A imagem é transferida por multicast aos clientes pelo ponto de distribuição, em vez de ser o ponto de distribuição a enviar uma cópia da imagem para cada cliente através de uma ligação separada. Quando escolhe o [utilizar multicast para implementar o Windows através da rede](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md) método de implementação do sistema de operativo, tem de configurar o pacote de imagem do sistema operativo para suportar multicast antes de distribuir a imagem do sistema operativo para um ponto de distribuição com capacidade multicast. Utilize o procedimento seguinte para definir as opções de multicast de um pacote de imagens do sistema operativo existente.  

#### <a name="to-modify-an-operating-system-image-package-to-use-multicast"></a>Para modificar um pacote de imagens do sistema operativo para utilizar o multicast  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software**, expanda **Sistemas Operativos** e clique em **Imagens de Sistema Operativo**.  

3.  Selecione a imagem do sistema operativo que pretende distribuir pelo ponto de distribuição preparado para multicast.  

4.  No separador **Home page** , no grupo **Propriedades** , clique em **Propriedades**.  

5.  Selecione o separador **Definições de Distribuição** e configure as seguintes opções:  

    -   **Permitir deste pacote a ser transferidos através de multicast (só WinPE)**: Tem de selecionar esta opção para o Configuration Manager implemente as imagens do sistema operativo em simultâneo.  

    -   **Encriptar pacotes multicast**: Especifique se a imagem é encriptada antes de ser enviada para o ponto de distribuição. Utilize esta opção se o pacote contiver informações confidenciais. Se a imagem não for encriptada, o conteúdo do pacote ficará visível na rede em texto simples e poderá ser lido por um utilizador não autorizado.  

    -   **Transferir este pacote apenas através de multicast**: Especifique se pretende que o ponto de distribuição implemente a imagem apenas durante uma sessão multicast.  

         Se selecionar a opção **Transferir este pacote apenas através de multicast**, também tem de especificar **Transferir o conteúdo localmente quando necessário para a sequência de tarefas em execução** como a opção de implementação da imagem do sistema operativo. Pode especificar as opções de implementação da imagem ao implementar a imagem do sistema operativo ou pode especificá-las mais tarde editando as propriedades da implementação. As opções de implementação estão no separador **Pontos de Distribuição** da página **Propriedades** do objeto de implementação.  

6.  Clique em **OK**.  
