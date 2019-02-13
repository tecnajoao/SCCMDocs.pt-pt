---
title: 'Gerir imagens de arranque '
titleSuffix: Configuration Manager
description: No Configuration Manager, Aprenda a gerir as imagens de arranque do Windows PE que utilizar durante a implementação do sistema operativo.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 97f2d81a-2c58-442c-88bc-defd5a1cd48f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2dfce18955f4cdfe62830eb3454520c904627117
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56122598"
---
# <a name="manage-boot-images-with-system-center-configuration-manager"></a>Gerir imagens de arranque com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Uma imagem de arranque no Configuration Manager é uma [Windows PE](https://docs.microsoft.com/windows-hardware/manufacture/desktop/winpe-intro) imagem (WinPE) utilizada durante a implementação do sistema operativo. Imagens de arranque são utilizadas para iniciar um computador no WinPE. Este sistema operativo mínimo contém componentes e serviços limitados. O Configuration Manager utiliza o WinPE para preparar o computador de destino para a instalação do Windows. Utilize as secções seguintes para gerir imagens de arranque.

## <a name="BKMK_BootImageDefault"></a> Imagens de arranque predefinidas
O Configuration Manager fornece duas imagens de arranque predefinidas: Uma para suportar plataformas x86 e outra para suportar x64 plataformas. Estas imagens são armazenadas em: \\ \\ *servername*> \SMS_ <*sitecode*> \osd\boot\\<*x64* > ou <*i386*>. Imagens de arranque predefinidas são atualizadas ou regeneradas dependendo da ação que efetuar.

Considere os seguintes comportamentos para qualquer uma das ações descritas para imagens de arranque predefinidas:
- Os objetos do controlador de origem tem de ser válidos. Estes objetos incluem os ficheiros de origem do driver. Se os objetos não são válidos, o site não adiciona os controladores a imagens de arranque.
- Imagens de arranque que não são baseadas em imagens de arranque predefinidas, mesmo que utilizem a mesma versão do Windows PE, não são modificadas.
- Redistribuir as imagens de arranque modificado para pontos de distribuição.
- Recrie qualquer suporte de dados que utiliza as imagens de arranque modificado.
- Se não pretender que as imagens de arranque personalizadas/predefinido atualizadas automaticamente, não armazene-os na localização predefinida.

> [!NOTE]
> A ferramenta de registo de rastreio (CMTrace) do Configuration Manager é adicionada a todas as imagens de arranque no **biblioteca de Software**. Quando estiver no Windows PE, inicie a ferramenta, escrevendo **CMTrace** na linha de comandos. A partir da versão 1802, ao iniciar cmtrace.exe no Windows PE, já não for pedido para escolher se pretende tornar este Visualizador padrão para ficheiros de registo do programa.

### <a name="use-updates-and-servicing-to-install-the-latest-version-of-configuration-manager"></a>Utilizar as atualizações e manutenção para instalar a versão mais recente do Configuration Manager
A partir da versão 1702, quando atualizar a versão de avaliação do Windows e Deployment Kit (ADK) e, em seguida, utilizar as atualizações e manutenção para instalar a versão mais recente do Configuration Manager, o site Regenera as imagens de arranque predefinidas. Esta atualização inclui a nova versão do WinPE partir do ADK atualizado do Windows, a nova versão do cliente do Configuration Manager, drivers e personalizações. O site não modifica as imagens de arranque personalizadas.

Antes da versão 1702, o Configuration Manager atualiza a imagem de arranque existentes com os componentes do cliente, drivers e personalizações, mas não utiliza a versão mais recente do WinPE partir do Windows ADK. Modificar manualmente a imagem de arranque para utilizar a nova versão do Windows ADK.

### <a name="upgrade-from-configuration-manager-2012-to-configuration-manager-current-branch-cb"></a>Atualizar do Configuration Manager 2012 para o Configuration Manager Current Branch (CB)
Quando atualizar do Configuration Manager 2012 para o Configuration Manager CB utilizando o processo de configuração, o site volta a gerar as imagens de arranque predefinidas. Esta atualização inclui a nova versão do WinPE partir do ADK atualizado do Windows e a nova versão do cliente do Configuration Manager. Todas as personalizações de imagem de arranque permanecem inalteradas. O site não modifica as imagens de arranque personalizadas.

### <a name="update-distribution-points-with-the-boot-image"></a>Atualizar pontos de distribuição com a imagem de arranque
Quando utiliza a **atualizar pontos de distribuição** ação por parte da **imagens de arranque** nó na consola, o site atualiza a imagem de arranque de destino com os componentes do cliente, drivers e personalizações.    

A partir do Configuration Manager versão 1706, recarregue a imagem de arranque com a versão mais recente do WinPE a partir do diretório de instalação Windows ADK. O **gerais** página do assistente atualizar pontos de distribuição fornece as seguintes informações: 
 - A versão do Windows ADK instalada no servidor do site
 - A versão do Windows ADK do WinPE na imagem de arranque
 - A versão do cliente do Configuration Manager utilizar estas informações para ajudar a decidir se pretende recarregar a imagem de arranque. O **imagens de arranque** nó também inclui uma nova coluna para (**versão de cliente**). Utilize esta coluna para ver rapidamente a versão de cliente do Configuration Manager em cada imagem de arranque.    


##  <a name="BKMK_BootImageCustom"></a> Personalizar uma imagem de arranque  
 Quando uma imagem de arranque baseia-se a versão do WinPE da versão suportada do Windows ADK, pode personalizar ou [modificar uma imagem de arranque](#BKMK_ModifyBootImages) a partir da consola. Quando um site é atualizado com uma nova versão e uma nova versão do Windows ADK está instalada, as imagens de arranque personalizadas (não na localização de imagem de arranque predefinida) não forem atualizadas com a nova versão do Windows ADK. Quando isso acontece, não é possível personalizar as imagens de arranque na consola do Configuration Manager. No entanto, eles continuar a funcionar como antes da atualização.  

 Quando uma imagem de arranque se baseia numa versão diferente do Windows ADK instalado num site, tem de personalizar as imagens de arranque. Utilize outro método para personalizar estas imagens de arranque, como a ferramenta de linha de comandos Deployment Image Servicing and Management (DISM). O DISM é parte do Windows ADK. Para obter mais informações, consulte [personalizar imagens de arranque](customize-boot-images.md).  

##  <a name="BKMK_AddBootImages"></a> Adicionar uma imagem de arranque  

 Durante a instalação de site, o Configuration Manager adiciona automaticamente imagens de arranque baseadas numa versão do WinPE da versão suportada do Windows ADK. Dependendo da versão do Configuration Manager, poderá conseguir adicionar imagens de arranque baseadas numa versão do WinPE diferente da versão suportada do Windows ADK. Ocorre um erro quando tentar adicionar uma imagem de arranque que contém uma versão não suportada do WinPE. As versões atualmente suportadas do Windows ADK e o WinPE-se a lista seguinte: 

- **Versão do Windows ADK**  

   Windows ADK para Windows 10  

- **Versões do Windows PE para imagens de arranque podem ser personalizadas na consola do Configuration Manager**  

   Windows PE 10  

- **Versões suportadas do Windows PE para imagens de arranque não podem ser personalizadas na consola do Configuration Manager**  

   Windows PE 3.1<sup>1</sup> e Windows PE 5  

   <sup>1</sup> só pode adicionar uma imagem de arranque para o Configuration Manager quando se baseia no Windows PE 3.1. Atualize o Windows AIK para Windows 7 (baseado no Windows PE 3.0) com o Windows AIK suplemento para o Windows 7 SP1 (baseado no Windows PE 3.1). Transferir o suplemento do Windows AIK para Windows 7 SP1 a partir da [Centro de transferências da Microsoft](https://www.microsoft.com/download/details.aspx?id=5188).  

   Por exemplo, utilize a consola do Configuration Manager para personalizar imagens de arranque baseadas no Windows PE 10 a partir do Windows ADK para Windows 10. Para uma imagem de arranque baseada no Windows PE 5, personalizá-lo a partir de um computador diferente, utilizando a versão do DISM do Windows ADK para Windows 8. Em seguida, adicione a imagem de arranque personalizadas na consola do Configuration Manager. Para obter mais informações, consulte [personalizar imagens de arranque](customize-boot-images.md).

  Utilize o procedimento seguinte para adicionar manualmente uma imagem de arranque.  

#### <a name="to-add-a-boot-image"></a>Para adicionar uma imagem de arranque  

1. Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2. Na área de trabalho **Biblioteca de Software**, expanda **Sistemas Operativos** e clique em **Imagens de Arranque**.  

3. No separador **Home Page**, no grupo **Criar**, clique em **Adicionar Imagem de Arranque** para iniciar o Assistente Adicionar Imagem de Arranque.  

4. Na página **Origem de Dados**, especifique as seguintes opções e clique em **Seguinte**.  

   -   Na caixa **Caminho**, especifique o caminho do ficheiro WIM da imagem de arranque.  

        O caminho especificado tem de ser um caminho de rede válido no formato UNC. Por exemplo: \\ \\ < *servername*\\<*sharename* > \\ < *bootimagename*>. wim.  

   -   Selecione a imagem de arranque na lista pendente **Imagem de Arranque**. Se o ficheiro WIM contiver várias imagens de arranque, selecione a imagem adequada.  

5. Na página **Geral**, especifique as seguintes opções e clique em **Seguinte**.  

   -   Na caixa **Nome**, especifique um nome exclusivo para a imagem de arranque.  

   -   Na caixa **Versão**, especifique um número de versão para a imagem de arranque.  

   -   Na caixa **Comentário**, insira uma breve descrição do modo como a imagem de arranque é utilizada.  

6. Conclua o assistente.  

   A imagem de arranque é agora listada no **imagem de arranque** nó da consola do Configuration Manager. Antes de utilizar a imagem de arranque para implementar um sistema operativo, distribua a imagem de arranque para pontos de distribuição. 

> [!NOTE]  
>  Na **imagem de arranque** nó da consola, o **tamanho (KB)** coluna exibe o tamanho descomprimido de cada imagem de arranque. Quando o site envia uma imagem de arranque através da rede, envia uma cópia compactada. Esta cópia é normalmente menor do que o tamanho listado na **tamanho (KB)** coluna.  

##  <a name="BKMK_DistributeBootImages"></a> Distribuir imagens de arranque para um ponto de distribuição  
 As imagens de arranque são distribuídas para pontos de distribuição da mesma forma que são distribuídos outros conteúdos. Na maioria dos casos, terá de distribuir a imagem de arranque para, pelo menos, um ponto de distribuição antes de implementar um sistema operativo e antes de criar suportes de dados.   

> [!NOTE]  
> Para utilizar o PXE para implementar um sistema operativo, considere os seguintes pontos antes de distribuir a imagem de arranque:  
> - Configure o ponto de distribuição para aceitar pedidos PXE.  
> - Distribuir um x86 e x64 imagem de arranque com PXE ativado para o ponto de distribuição com PXE ativado pelo menos um.  
> - O Configuration Manager distribui as imagens de arranque para o **RemoteInstall** pasta no ponto de distribuição com PXE ativado.  
>   
> Para obter mais informações sobre como utilizar o PXE para implementar sistemas operativos, consulte [utilizar o PXE para implementar o Windows na rede](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

 Para obter os passos para distribuir uma imagem de arranque, veja [Distribuir conteúdo](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute).  

##  <a name="BKMK_ModifyBootImages"></a> Modificar uma imagem de arranque  
 Pode adicionar ou remover controladores de dispositivo da imagem ou editar as propriedades associadas à imagem de arranque. Os controladores de dispositivo que adicionar ou remover podem incluir controladores de placas de rede ou de dispositivos de armazenamento de massa. Ao modificar imagens de arranque, considere os seguintes fatores:  

- Importar e ativar os controladores de dispositivo no catálogo de controladores de dispositivo antes de os adicionar à imagem de arranque.  

- Quando modifica uma imagem de arranque, esta não altera nenhum dos pacotes associados aos quais a imagem de arranque faz referência.  

- Depois de efetuar alterações a uma imagem de arranque **atualizar** a imagem de arranque no distribuição aponta que já o tiver. Este processo torna a versão mais atual da imagem de arranque disponíveis para clientes. Para obter mais informações, veja [Gerir conteúdo que distribuiu](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_manage).  

  Utilize o procedimento seguinte para modificar uma imagem de arranque.  

#### <a name="to-modify-the-properties-of-a-boot-image"></a>Para modificar as propriedades de uma imagem de arranque  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software**, expanda **Sistemas Operativos** e clique em **Imagens de Arranque**.  

3.  Selecione a imagem de arranque que pretende modificar.  

4.  No separador **Home Page**, no grupo **Propriedades**, clique em **Propriedades** para abrir a caixa de diálogo **Propriedades** da imagem de arranque.  

5.  Defina qualquer uma das seguintes definições para alterar o comportamento da imagem de arranque:  

    -   No separador **Imagens**, se tiver alterado as propriedades da imagem de arranque com uma ferramenta externa, clique em **Recarregar**.  

    -   No separador **Controladores**, adicione os controladores de dispositivo Windows que são precisos para iniciar o WinPE. Ao adicionar controladores de dispositivo, considere os seguintes pontos:  

        -   Selecione **Ocultar controladores que não correspondem à arquitetura da imagem de arranque** para apresentar apenas os controladores para a arquitetura da imagem de arranque. A arquitetura baseia-se na arquitetura reportada no INF do fabricante.  

        -   Selecione **Ocultar controladores que não estão numa classe de armazenamento ou de rede (para imagens de arranque)** para apresentar apenas controladores de armazenamento e rede. Esta opção também oculta a outros controladores que normalmente não são necessários para imagens de arranque, como drivers de vídeo ou de modem.  

        -   Selecione **Ocultar controladores que não estejam assinados digitalmente** para ocultar controladores que não tem uma assinatura digital válida.  

        -   Como melhor prática, adicione apenas rede e controladores de armazenamento em massa à imagem de arranque, a menos que haja outros controladores no WinPE.  

        -   Porque o WinPE é fornecido com muitos controladores incorporados, adicione apenas controladores armazenamento de rede e em massa que não sejam fornecidos pelo WinPE.  

        -   Certifique-se de que os controladores que adiciona à imagem de arranque correspondem à arquitetura da imagem de arranque.  

        > [!NOTE]  
        >  Tem de importar controladores de dispositivo para o catálogo de controladores antes de os adicionar a uma imagem de arranque. Para obter informações sobre como importar controladores de dispositivo, consulte [gerir controladores](manage-drivers.md).  

    -   No separador **Personalização**, selecione qualquer uma das seguintes definições:  

        -   Selecione a caixa de verificação **Ativar Comando de Pré-início** para especificar a execução de um comando antes da execução da sequência de tarefas. Quando ativa esta opção, especifique também a linha de comandos para executar e quaisquer ficheiros de suporte necessários pelo comando.  

            > [!WARNING]  
            >  Adicione **cmd /c** no início da linha de comandos. Se não especificar **cmd /c**, o comando não fechado depois de ser executado. A implementação continua a aguardar que o comando seja concluído e não inicia quaisquer outros comandos ou ações configurados.  

            > [!TIP]  
            >  Durante a criação de suportes de dados de sequência de tarefas, o assistente escreve o ID de pacote e a linha de comandos de Pré-início, incluindo o valor das eventuais variáveis de sequência de tarefas, para o ficheiro de registo Createtsmedia. Este registo está no computador que executa a consola do Configuration Manager. Consulte este ficheiro de registo para verificar o valor das variáveis de sequência de tarefas.  

        -   Configure as definições de **Fundo do Windows PE** para especificar se pretende utilizar o fundo predefinido do WinPE ou um fundo personalizado.  

        -   Selecione **Ativar suporte de comando (apenas teste)** para abrir uma linha de comandos com a tecla **F8** quando a imagem de arranque estiver a ser implementada. Esta opção é útil para resolução de problemas quando estiver a testar sua implantação. Não é aconselhada a utilização desta definição numa implementação de produção.  

        -   Configure o espaço scratch do Windows PE, que é armazenamento temporário (unidade de RAM) utilizado pelo WinPE. Por exemplo, quando uma aplicação é executada no WinPE e tem de escrever ficheiros temporários, o WinPE redireciona os ficheiros para o espaço scratch na memória, para simular a presença de um disco rígido. Por predefinição, o WinPE atribui 32 megabytes (MB) de memória gravável.  

    -   No separador **Origem de Dados**, atualize qualquer uma das seguintes definições:  

        -   Para alterar o ficheiro de origem da imagem de arranque, defina **caminho de imagem** e **índice de imagens**.  

        -   Para criar uma agenda para quando o site atualiza a imagem de arranque, selecione **atualizar pontos de distribuição com base numa agenda**.  

        -   Se não pretender que o conteúdo deste pacote seja por antiguidade para disponibilizar espaço para outro conteúdo a cache do cliente, selecione **manter conteúdo na cache do cliente**.  

        -   Para especificar que o site apenas distribui ficheiros alterados quando atualiza o pacote de imagem de arranque no ponto de distribuição, selecione **ativar a replicação diferencial de binários** (BDR). Esta definição minimiza o tráfego de rede entre sites. A BDR é especialmente útil quando o pacote de imagem de arranque for grande e as alterações forem relativamente pequenas.  

        -   Se utilizar a imagem de arranque numa implementação com PXE ativado, selecione **implementar esta imagem de arranque do ponto de distribuição com PXE ativado**.  

            > [!NOTE]  
            >  Para obter mais informações, consulte [utilizar o PXE para implementar o Windows na rede](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

    -   No separador **Acesso a Dados**, selecione qualquer uma das seguintes definições:  

        -   Configure as **Definições de partilha de pacote** se pretender que os clientes instalem o conteúdo deste pacote a partir da rede.  

        -   Definir o **definições de atualização do pacote** para especificar como pretende que o Configuration Manager, desligue os utilizadores do ponto de distribuição. O Configuration Manager poderão não é possível atualizar a imagem de arranque quando os utilizadores estão ligados ao ponto de distribuição.  

    -   No separador **Definições de Distribuição**, selecione qualquer uma das seguintes definições:  

        -   Na **prioridade de distribuição** , especifique o nível de prioridade. O Configuration Manager utiliza esta lista de prioridade quando o site distribui vários pacotes para o mesmo ponto de distribuição.  

        -   Se pretender ativar a distribuição de conteúdo a pedido para pontos de distribuição preferenciais, selecione **distribuir o conteúdo do pacote para pontos de distribuição preferenciais**. Quando ativa esta definição, se um cliente solicita o conteúdo do pacote e o conteúdo não está disponível em quaisquer pontos de distribuição preferenciais, em seguida, o ponto de gestão distribui o conteúdo por todos os pontos de distribuição preferenciais.  

        -   Para especificar como pretende que o site para distribuir a imagem de arranque para pontos de distribuição que estão ativados para conteúdo pré-configurado, defina o **pré-configurado as definições do ponto de distribuição**.  

            > [!NOTE]  
            >  Para obter mais informações sobre conteúdo pré-configurado, veja [Pré-configurar conteúdo](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_prestage).  

    -   No separador **Localizações de Conteúdo**, selecione o ponto de distribuição ou o grupo de pontos de distribuição e execute qualquer uma das seguintes ações:  

        -   Clique em **Redistribuir** para distribuir novamente a imagem de arranque para o ponto de distribuição ou grupo de pontos de distribuição selecionado.  

        -   Clique em **Validar** para verificar a integridade do pacote de imagem de arranque no ponto de distribuição ou grupo de pontos de distribuição selecionado.  

    -   Sobre o **componentes opcionais** separador, especifique os componentes que são adicionados ao Windows PE para utilização com o Configuration Manager. Para obter mais informações sobre os componentes opcionais disponíveis, consulte [WinPE: Adicionar pacotes (referência de componentes opcionais)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/winpe-add-packages--optional-components-reference).  

    -   No separador **Segurança**, selecione um utilizador administrativo e altere as operações que este pode realizar.  

6.  Depois de configurar as propriedades, clique em **OK**.  

##  <a name="BKMK_BootImagePXE"></a> Configurar uma imagem de arranque para implementar a partir de um ponto de distribuição com PXE ativado  
 Antes de poder utilizar uma imagem de arranque para uma implementação de sistema operativo PXE, tem de configurar a imagem de arranque para implementar a partir de um ponto de distribuição ativado por PXE.  

#### <a name="to-configure-a-boot-image-to-deploy-from-a-pxe-enabled-distribution-point"></a>Para configurar uma imagem de arranque para implementar a partir de um ponto de distribuição ativado por PXE  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software**, expanda **Sistemas Operativos** e clique em **Imagens de Arranque**.  

3.  Selecione a imagem de arranque que pretende modificar.  

4.  No separador **Home Page**, no grupo **Propriedades**, clique em **Propriedades** para abrir a caixa de diálogo **Propriedades** da imagem de arranque.  

5.  No separador **Origem de Dados**, selecione **Implementar esta imagem de arranque a partir do ponto de distribuição ativado por PXE**.  

    > [!NOTE]  
    >  Para obter mais informações, consulte [utilizar o PXE para implementar o Windows na rede](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

6.  Depois de configurar as propriedades, clique em **OK**.  

##  <a name="BKMK_BootImageLanguage"></a> Configurar vários idiomas para implementação de imagem de arranque  
 As imagens de arranque são independentes de idiomas. Esta funcionalidade permite-lhe utilizar uma imagem de arranque para apresentar o texto da sequência de tarefas em vários idiomas no WinPE. Incluir o suporte de idioma apropriado da imagem de arranque **componentes opcionais** separador. Em seguida, defina a variável de sequência de tarefas apropriada para indicar o idioma a apresentar. O idioma do sistema operativo implementado é independente do idioma no WinPE. O idioma que WinPE apresenta ao utilizador é determinado da seguinte forma:  

- Quando um utilizador executa a sequência de tarefas a partir de um sistema operativo existente, o Configuration Manager utiliza automaticamente o idioma configurado para o utilizador. Quando a sequência de tarefas é executado automaticamente como resultado de um prazo de implementação obrigatório, o Configuration Manager utiliza o idioma do sistema operativo.  

- Para implementações do sistema operativo que utilizam o PXE ou suportes de dados, defina o valor de ID de idioma **SMSTSLanguageFolder** variável como parte de um comando de Pré-início. Quando o computador inicia o WinPE, as mensagens são apresentadas no idioma que especificou na variável. Se ocorrer um erro ao aceder ao ficheiro de recursos de idioma na pasta especificada ou se não tiver definido a variável, o WinPE apresenta as mensagens no idioma padrão.  

  > [!NOTE]  
  >  Quando o suporte de dados estiver protegido por uma palavra-passe, o texto que solicita ao utilizador a palavra-passe é sempre apresentado no idioma do WinPE.  

  Utilize o procedimento seguinte para definir o idioma do WinPE para implementações do sistema operativo iniciadas por PXE ou suportes de dados.  

#### <a name="to-set-the-windows-pe-language-for-a-pxe-or-media-initiated-operating-system-deployment"></a>Para definir o idioma do Windows PE para uma implementação do sistema operativo iniciada por suportes de dados ou por PXE  

1.  Certifique-se de que o arquivo de recurso de sequência de tarefas adequado (tsres) está na pasta do idioma correspondente no servidor do site antes de atualizar a imagem de arranque. Por exemplo, o ficheiro de recursos em inglês está na seguinte localização: <*ConfigMgrInstallationFolder*> \OSD\bin\x64\00000409\tsres.dll.  

2.  Como parte do comando de pré-início, defina a variável de ambiente SMSTSLanguageFolder no ID de idioma apropriado. O ID de idioma deve ser especificado utilizando o formato decimal e não o hexadecimal. Por exemplo, para definir o ID de idioma para inglês, especifique o valor decimal 1033, não o valor hexadecimal 00000409 do nome da pasta.  
