---
title: Gerir imagens de arranque
titleSuffix: Configuration Manager
description: No Configuration Manager, Aprenda a gerir as imagens de arranque do Windows PE que utilizou durante uma implementação do sistema operacional.
ms.date: 02/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 97f2d81a-2c58-442c-88bc-defd5a1cd48f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d4ed731b9b931e76e6d6b6d1399bf5a273bf561b
ms.sourcegitcommit: 56ec6933cf7bfc93842f55835ad336ee3a1c6ab5
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/01/2019
ms.locfileid: "57211657"
---
# <a name="manage-boot-images-with-configuration-manager"></a>Gerir imagens de arranque com o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Uma imagem de arranque no Configuration Manager é uma [Windows PE](https://docs.microsoft.com/windows-hardware/manufacture/desktop/winpe-intro) imagem (WinPE) utilizada durante uma implementação do sistema operacional. Imagens de arranque são utilizadas para iniciar um computador no WinPE. Esse SO mínimo contém componentes e serviços limitados. O Configuration Manager utiliza o WinPE para preparar o computador de destino para a instalação do Windows. 



## <a name="BKMK_BootImageDefault"></a> Imagens de arranque predefinidas

O Configuration Manager fornece duas imagens de arranque predefinidas: Uma para suportar plataformas x86 e outra para suportar x64 plataformas. Estas imagens são armazenadas no *x64* ou *i386* pastas na seguinte partilham no servidor do site: `\\<SiteServerName>\SMS_<sitecode>\osd\boot\`. Imagens de arranque predefinidas são atualizadas ou regeneradas dependendo da ação que efetuar.

Considere os seguintes comportamentos para qualquer uma das ações descritas para imagens de arranque predefinidas:

- Os objetos do controlador de origem tem de ser válidos. Estes objetos incluem os ficheiros de origem do driver. Se os objetos não são válidos, o site não adiciona os controladores a imagens de arranque.  

- Imagens de arranque que não são baseadas em imagens de arranque predefinidas, mesmo que utilizem a mesma versão do Windows PE, não são modificadas.  

- Redistribuir as imagens de arranque modificado para pontos de distribuição.  

- Recrie qualquer suporte de dados que utiliza as imagens de arranque modificado.  

- Se não pretender que as imagens de arranque personalizadas/predefinido atualizadas automaticamente, não armazená-las na localização predefinida.  

> [!NOTE]
> A ferramenta de registo do Configuration Manager (**CMTrace**) é adicionada a todas as imagens de arranque no **biblioteca de Software**. Quando estiver no Windows PE, inicie a ferramenta digitando `cmtrace` na linha de comandos. 
> 
> A partir da versão 1802, ao iniciar a ferramenta CMTrace no Windows PE, já não for pedido para escolher se pretende tornar este Visualizador padrão para ficheiros de registo do programa.


### <a name="use-updates-and-servicing-to-install-the-latest-version-of-configuration-manager"></a>Utilizar as atualizações e manutenção para instalar a versão mais recente do Configuration Manager

Quando atualizar a versão de avaliação do Windows e Deployment Kit (ADK) e, em seguida, utiliza as atualizações e manutenção para instalar a versão mais recente do Configuration Manager, o site volta a gerar as imagens de arranque predefinidas. Esta atualização inclui a nova versão do WinPE partir do ADK atualizado do Windows, a nova versão do cliente do Configuration Manager, drivers e personalizações. O site não modifica as imagens de arranque personalizadas.


### <a name="upgrade-from-configuration-manager-2012-to-current-branch"></a>Atualizar do Configuration Manager 2012 para o ramo atual

Ao atualizar o Configuration Manager 2012 para o ramo atual, o site volta a gerar as imagens de arranque predefinidas. Esta atualização inclui a nova versão do WinPE partir do ADK atualizado do Windows e a nova versão do cliente do Configuration Manager. Todas as personalizações de imagem de arranque permanecem inalteradas. O site não modifica as imagens de arranque personalizadas.


### <a name="update-distribution-points-with-the-boot-image"></a>Atualizar pontos de distribuição com a imagem de arranque

Quando utiliza a **atualizar pontos de distribuição** ação por parte da **imagens de arranque** nó na consola, o site atualiza a imagem de arranque de destino com os componentes do cliente, drivers e personalizações.    

Pode recarregar a imagem de arranque com a versão mais recente do WinPE do diretório de instalação Windows ADK. O **gerais** página do assistente atualizar pontos de distribuição fornece as seguintes informações: 
 - A versão atual do Windows ADK instalada no servidor do site
 - A versão atual do cliente de produção
 - A versão do Windows ADK do WinPE na imagem de arranque
 - A versão do cliente do Configuration Manager na imagem de arranque

Se as versões na imagem de arranque estão Desatualizadas, utilize a opção para **recarregar esta imagem de arranque com a versão atual do Windows PE partir do Windows ADK**. 

> [!Important]  
> Esta ação está disponível para o padrão e imagens de arranque personalizadas. Durante este processo para recarregar a imagem de arranque, o site não mantém qualquer manuais personalizações efetuadas fora do Configuration Manager. Estas personalizações incluem extensões de terceiros. Esta opção recria a imagem de arranque utilizando a versão mais recente do WinPE e a versão mais recente do cliente. Apenas as configurações que especificar nas propriedades da imagem de arranque são reaplicadas. <!--SCCMDocs issue #1283-->

O **imagens de arranque** nó também inclui uma nova coluna para (**versão de cliente**). Utilize esta coluna para ver rapidamente a versão de cliente do Configuration Manager em cada imagem de arranque.    



##  <a name="BKMK_BootImageCustom"></a> Personalizar uma imagem de arranque  

Quando uma imagem de arranque baseia-se a versão do WinPE da versão suportada do Windows ADK, pode personalizar ou [modificar uma imagem de arranque](#BKMK_ModifyBootImages) a partir da consola. Quando atualizar um site e instalar uma nova versão do Windows ADK, imagens de arranque personalizadas não são atualizadas com a nova versão do Windows ADK. Quando isso acontece, não é possível personalizar as imagens de arranque na consola do Configuration Manager. No entanto, eles continuar a funcionar como antes da atualização.  

Quando uma imagem de arranque se baseia numa versão diferente do Windows ADK instalado num site, tem de personalizar as imagens de arranque. Utilize outro método para personalizar estas imagens de arranque, como a ferramenta de linha de comandos Deployment Image Servicing and Management (DISM). O DISM é parte do Windows ADK. Para obter mais informações, consulte [personalizar imagens de arranque](customize-boot-images.md).  



##  <a name="BKMK_AddBootImages"></a> Adicionar uma imagem de arranque  

Durante a instalação de site, o Configuration Manager adiciona automaticamente imagens de arranque baseadas numa versão do WinPE da versão suportada do Windows ADK. Dependendo da versão do Configuration Manager, pode adicionar imagens de arranque baseadas numa versão do WinPE diferente da versão suportada do Windows ADK. Ocorre um erro quando tentar adicionar uma imagem de arranque que contém uma versão não suportada do WinPE. As versões atualmente suportadas do Windows ADK e o WinPE-se a lista seguinte: 


|  |  |
|---------|---------|
| Versão do Windows ADK | Windows ADK para Windows 10 |
| Versões do Windows PE para imagens de arranque podem ser personalizadas na consola do Configuration Manager | Windows PE 10 |
| Versões suportadas do Windows PE para imagens de arranque *não podem ser personalizadas* da consola do Configuration Manager | -Windows PE 3.1<sup>[observe 1](#bkmk_note1)</sup> <br> -Windows PE 5 |

Por exemplo, utilize a consola do Configuration Manager para personalizar imagens de arranque baseadas no Windows PE 10 a partir do Windows ADK para Windows 10. Para uma imagem de arranque baseada no Windows PE 5, personalizá-lo a partir de um computador diferente, utilizando a versão do DISM do Windows ADK para Windows 8. Em seguida, adicione a imagem de arranque personalizadas na consola do Configuration Manager. Para obter mais informações, veja os artigos seguintes:
- [Personalizar imagens de arranque](/sccm/osd/get-started/customize-boot-images)
- [Suporte para o Windows 10 ADK](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk)
- [Plataformas suportada do DISM](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms)

#### <a name="bkmk_note1"></a> Nota 1: Suporte para o Windows PE 3.1

Apenas adicionar uma imagem de arranque ao Configuration Manager com base no Windows PE *versão 3.1*. Atualize o Windows AIK para Windows 7 (baseado no Windows PE 3.0) com o Windows AIK suplemento para o Windows 7 SP1 (baseado no Windows PE 3.1). Transferir o suplemento do Windows AIK para Windows 7 SP1 a partir da [Centro de transferências da Microsoft](https://www.microsoft.com/download/details.aspx?id=5188).  


#### <a name="process-to-add-a-boot-image"></a>Processo para adicionar uma imagem de arranque  

1. Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho, expanda **sistemas operativos**e, em seguida, selecione o **imagens de arranque** nó.  

2. Sobre o **home page** separador do Friso, no **criar** grupo, selecione **adicionar imagem de arranque**. Esta ação inicia o Assistente para adicionar imagem de arranque.  

3. Sobre o **origem de dados** página, especifique as seguintes opções:  

    - Na caixa **Caminho**, especifique o caminho do ficheiro WIM da imagem de arranque. O caminho especificado tem de ser um caminho de rede válido no formato UNC. Por exemplo: `\\ServerName\ShareName\BootImageName.wim`

    - Selecione a imagem de arranque na lista pendente **Imagem de Arranque**. Se o ficheiro WIM contiver várias imagens de arranque, selecione a imagem adequada.  

4. Sobre o **gerais** página, especifique as seguintes opções:  

    - Na caixa **Nome**, especifique um nome exclusivo para a imagem de arranque.  

    - Na caixa **Versão**, especifique um número de versão para a imagem de arranque.  

    - Na **comentário** caixa, especifique uma breve descrição de como utilizar a imagem de arranque.  

5. Conclua o assistente.  

A imagem de arranque é agora listada no **imagem de arranque** nó. Antes de utilizar a imagem de arranque para implementar um sistema operacional, distribua a imagem de arranque para pontos de distribuição. 

> [!Tip]  
> Na **imagem de arranque** nó da consola, o **tamanho (KB)** coluna exibe o tamanho descomprimido de cada imagem de arranque. Quando o site envia uma imagem de arranque através da rede, envia uma cópia compactada. Esta cópia é normalmente menor do que o tamanho listado na **tamanho (KB)** coluna.  



##  <a name="BKMK_DistributeBootImages"></a> Distribuir imagens de arranque  

As imagens de arranque são distribuídas para pontos de distribuição da mesma forma que são distribuídos outros conteúdos. Antes de implementar um sistema operacional ou criar suportes de dados, distribua a imagem de arranque para, pelo menos, um ponto de distribuição.   

Para obter mais informações sobre como distribuir uma imagem de arranque, consulte [distribuir conteúdo](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute).  

Para utilizar o PXE para implementar um sistema operacional, considere os seguintes pontos antes de distribuir a imagem de arranque:  
- Configure o ponto de distribuição para aceitar pedidos PXE.  
- Distribuir um x86 e x64 imagem de arranque com PXE ativado para o ponto de distribuição com PXE ativado pelo menos um.  
- O Configuration Manager distribui as imagens de arranque para o **RemoteInstall** pasta no ponto de distribuição com PXE ativado.  
  
Para obter mais informações sobre como utilizar o PXE para implementar sistemas operativos, consulte [utilizar o PXE para implementar o Windows na rede](/sccm/osd/deploy-use/use-pxe-to-deploy-windows-over-the-network).  



##  <a name="BKMK_ModifyBootImages"></a> Modificar uma imagem de arranque  

Adicionar ou remover controladores de dispositivo para a imagem ou editar as propriedades da imagem de arranque. Os controladores que adicionar ou remover podem incluir controladores de armazenamento ou de rede. Ao modificar imagens de arranque, considere os seguintes fatores:  

- Antes de adicionar controladores à imagem de arranque, importar e ativá-los no catálogo de controladores de dispositivo.  

- Ao modificar uma imagem de arranque, a imagem de arranque não altera nenhum dos pacotes associados que referencia a imagem de arranque.  

- Depois de efetuar alterações a uma imagem de arranque **atualizar** a imagem de arranque no distribuição aponta que já o tiver. Este processo torna a versão mais atual da imagem de arranque disponíveis para clientes. Para obter mais informações, consulte [gerir conteúdo que foi distribuído](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_manage).  


### <a name="process-to-modify-the-properties-of-a-boot-image"></a>Processo para modificar as propriedades de uma imagem de arranque  

1. Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho, expanda **sistemas operativos**e, em seguida, selecione o **imagens de arranque** nó.  

2. Selecione a imagem de arranque que pretende modificar.  

3. Sobre o **home page** separador do Friso, no **propriedades** grupo, selecione **propriedades**.  

4. Defina qualquer uma das seguintes definições para alterar o comportamento da imagem de arranque:  

#### <a name="images"></a>Imagens
Sobre o **imagens** separador, se alterar as propriedades da imagem de arranque, utilizando uma ferramenta externa, clique em **recarregar**.  

#### <a name="drivers"></a>Controladores
No separador **Controladores**, adicione os controladores de dispositivo Windows que são precisos para iniciar o WinPE. Ao adicionar controladores de dispositivo, considere os seguintes pontos:  

- Certifique-se de que os controladores que adiciona à imagem de arranque correspondem à arquitetura da imagem de arranque.  

- Para apresentar apenas controladores para a arquitetura da imagem de arranque, selecione **Ocultar controladores que não correspondem à arquitetura da imagem de arranque**. A arquitetura do controlador baseia-se na arquitetura reportada no INF do fabricante.  

- WinPE é fornecido com muitos controladores incorporados. Adicione apenas controladores de rede e armazenamento que não estão incluídos no WinPE.  

- Adicione apenas controladores de rede e armazenamento para a imagem de arranque, a menos que haja outros controladores no WinPE.  

- Para apresentar apenas controladores de armazenamento e rede, selecione **Ocultar controladores que não estão numa classe de armazenamento ou de rede (para imagens de arranque)**. Esta opção também oculta a outros controladores que normalmente não são necessários para imagens de arranque, como drivers de vídeo ou de modem.  

- Para ocultar controladores que não tem uma assinatura digital válida, selecione **Ocultar controladores que não estejam assinados digitalmente**.  

> [!NOTE]  
> Importe controladores de dispositivo para o catálogo de controladores antes de adicioná-los para uma imagem de arranque. Para obter informações sobre como importar controladores de dispositivo, consulte [gerir controladores](manage-drivers.md).  

#### <a name="customization"></a>Personalização
No separador **Personalização**, selecione qualquer uma das seguintes definições:  

- Selecione o **ativar comando de Pré-início** opção para especificar um comando para executar antes da sequência de tarefas é executado. Quando ativa esta opção, especifique também a linha de comandos para executar e quaisquer ficheiros de suporte necessários pelo comando.  

    > [!WARNING]  
    > Adicione **cmd /c** no início da linha de comandos. Se não especificar **cmd /c**, o comando não fechado depois de ser executado. A implementação continua a aguardar que o comando seja concluído e não inicia quaisquer outros comandos ou ações configurados.  

    > [!TIP]  
    > Durante a criação de suportes de dados de sequência de tarefas, o assistente escreve o ID de pacote e a linha de comandos de Pré-início para o ficheiro de registo Createtsmedia. Estas informações incluem o valor das eventuais variáveis de sequência de tarefas. Este registo está no computador que executa a consola do Configuration Manager. Consulte este ficheiro de registo para verificar os valores para as variáveis de sequência de tarefas.  

- Configure as definições de **Fundo do Windows PE** para especificar se pretende utilizar o fundo predefinido do WinPE ou um fundo personalizado.  

- Selecione **Ativar suporte de comando (apenas teste)** para abrir uma linha de comandos com a tecla **F8** quando a imagem de arranque estiver a ser implementada. Esta opção é útil para resolução de problemas quando estiver a testar a implementação. Com esta definição numa implementação de produção não é aconselhado devido a questões de segurança.  

- Configure o espaço scratch do Windows PE, que é armazenamento temporário (unidade de RAM) utilizado pelo WinPE. Por exemplo, quando uma aplicação é executada no WinPE e tem de escrever ficheiros temporários, o WinPE redireciona os ficheiros para o espaço scratch na memória, para simular a presença de um disco rígido. Por predefinição, esta quantidade é 512 MB para dispositivos com mais de 1 GB de RAM, caso contrário, a predefinição é de 32 MB.  

#### <a name="optional-components"></a>Componentes opcionais
Sobre o **componentes opcionais** separador, especifique os componentes que são adicionados ao Windows PE para utilização com o Configuration Manager. Para obter mais informações sobre os componentes opcionais disponíveis, consulte [WinPE: Adicionar pacotes (referência de componentes opcionais)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/winpe-add-packages--optional-components-reference).  

Os seguintes componentes são necessários pelo Configuration Manager e sempre adicionados às imagens de arranque:
- Criação de scripts (WinPE-Scripting)
- Startup (WinPE-SecureStartup)
- Rede (WinPE-WDS-Tools)
- Scripting (WinPE-WMI)

O **componentes** lista mostra itens adicionais que são adicionados a esta imagem de arranque. Para adicionar mais componentes, selecione o asterisco gold. Para remover um componente, selecione-o na lista e, em seguida, selecione o X vermelho. 

Os seguintes componentes são comumente usados pelos clientes:
- Microsoft .NET (WinPE-NetFX): Este componente é um pré-requisito para o PowerShell. É um dos componentes opcionais maiores.  
- Windows PowerShell (WinPE-PowerShell): Este componente requer o .NET e adiciona suporte limitado do PowerShell. Se executar scripts personalizados do PowerShell durante a fase WinPE da sequência de tarefas, adicione este componente. Existem outros componentes que podem ser necessários para outros cmdlets do PowerShell.   
- HTML (WinPE-HTA): Se executar aplicações de HTML personalizadas durante a fase WinPE da sequência de tarefas, adicione este componente. 

Para obter mais informações sobre como adicionar idiomas, consulte [configurar vários idiomas](#BKMK_BootImageLanguage). 

#### <a name="data-source"></a>Origem de Dados
No separador **Origem de Dados**, atualize qualquer uma das seguintes definições:  

- Para alterar o ficheiro de origem da imagem de arranque, defina **caminho de imagem** e **índice de imagens**.  

- Para criar uma agenda para quando o site atualiza a imagem de arranque, selecione **atualizar pontos de distribuição com base numa agenda**.  

- Se não pretender que o conteúdo deste pacote seja por antiguidade para disponibilizar espaço para outro conteúdo a cache do cliente, selecione **manter conteúdo na cache do cliente**.  

- Para especificar que o site apenas distribui ficheiros alterados quando atualiza o pacote de imagem de arranque no ponto de distribuição, selecione **ativar a replicação diferencial de binários** (BDR). Esta definição minimiza o tráfego de rede entre sites. A BDR é especialmente útil quando o pacote de imagem de arranque for grande e as alterações forem relativamente pequenas.  

- Se utilizar a imagem de arranque numa implementação com PXE ativado, selecione **implementar esta imagem de arranque do ponto de distribuição com PXE ativado**. Para obter mais informações, consulte [utilizar o PXE para implementar o Windows na rede](/sccm/osd/deploy-use/use-pxe-to-deploy-windows-over-the-network).  

#### <a name="data-access"></a>Acesso a dados
Sobre o **acesso a dados** separador, pode configurar definições de partilha de pacote. Se for necessário no seu ambiente, definir a opção como **copiar o conteúdo deste pacote para uma partilha de pacote em pontos de distribuição**. Em seguida, tem a opção adicional para **utilizar um nome personalizado para a partilha de pacote** e especifique o personalizado **nome da partilha**. Espaço em disco adicional é necessária em pontos de distribuição quando ativa esta opção. Aplica-se a todos os pontos de distribuição que recebem esta imagem de arranque. 

#### <a name="distribution-settings"></a>Definições de distribuição
No separador **Definições de Distribuição**, selecione qualquer uma das seguintes definições:  

- Na **prioridade de distribuição** , especifique o nível de prioridade. O Configuration Manager utiliza esta lista de prioridade quando o site distribui vários pacotes para o mesmo ponto de distribuição.  

- Se pretender ativar a distribuição de conteúdo a pedido para pontos de distribuição preferenciais, selecione **ativar para distribuição a pedido**. Quando ativa esta definição, se um cliente solicita o conteúdo do pacote e o conteúdo não está disponível em quaisquer pontos de distribuição, o ponto de gestão distribui o conteúdo. Para obter mais informações, consulte [distribuição de conteúdo a pedido](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#on-demand-content-distribution).  

- Para especificar como pretende que o site para distribuir a imagem de arranque para pontos de distribuição que estão ativados para conteúdo pré-configurado, defina o **pré-configurado as definições do ponto de distribuição**. Para obter mais informações sobre conteúdo pré-configurado, veja [Pré-configurar conteúdo](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_prestage).  

#### <a name="content-locations"></a>Localizações de conteúdo
Sobre o **localizações de conteúdo** separador, selecione o ponto de distribuição ou grupo de pontos de distribuição e utilize as seguintes ações:  

- **Validar**: Verificar a integridade do pacote de imagem de arranque no ponto de distribuição selecionados ou grupo de pontos de distribuição.  

- **Redistribuir**: Distribua novamente a imagem de arranque para o ponto de distribuição selecionado ou o grupo de pontos de distribuição.  

- **Remover**: Elimine a imagem de arranque a partir do ponto de distribuição selecionado ou o grupo de pontos de distribuição.  

#### <a name="security"></a>Segurança
Sobre o **segurança** separador, ver os utilizadores administrativos que têm permissões para este objeto.



## <a name="BKMK_BootImagePXE"></a> Configurar uma imagem de arranque de PXE  

Antes de poder utilizar uma imagem de arranque para uma implantação baseada em PXE, configure a imagem de arranque para implementar a partir de um ponto de distribuição com PXE ativado.  

1. Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho, expanda **sistemas operativos**e, em seguida, selecione o **imagens de arranque** nó.  

2. Selecione a imagem de arranque que pretende modificar.  

3. Sobre o **home page** separador do Friso, no **propriedades** grupo, selecione **propriedades**.  

4. No separador **Origem de Dados**, selecione **Implementar esta imagem de arranque a partir do ponto de distribuição ativado por PXE**. Para obter mais informações, consulte [utilizar o PXE para implementar o Windows na rede](/sccm/osd/deploy-use/use-pxe-to-deploy-windows-over-the-network).  



## <a name="BKMK_BootImageLanguage"></a> Configurar vários idiomas

As imagens de arranque são independentes de idiomas. Esta funcionalidade permite-lhe utilizar uma imagem de arranque para apresentar o texto da sequência de tarefas em vários idiomas no WinPE. Incluir o suporte de idioma apropriado da imagem de arranque **componentes opcionais** separador. Em seguida, defina a variável de sequência de tarefas apropriada para indicar o idioma a apresentar. O idioma do sistema operativo implementado é independente do idioma no WinPE. O idioma que WinPE apresenta ao utilizador é determinado da seguinte forma:  

- Quando um utilizador executa a sequência de tarefas a partir de um sistema operacional existente, o Configuration Manager utiliza automaticamente o idioma configurado para o utilizador. Quando a sequência de tarefas é executado automaticamente como resultado de um prazo de implementação obrigatório, o Configuration Manager utiliza o idioma do sistema operacional.  

- Para Implantações de SO que utilizam o PXE ou suportes de dados, defina o valor de ID de idioma **SMSTSLanguageFolder** variável como parte de um comando de Pré-início. Quando o computador inicia o WinPE, as mensagens são apresentadas no idioma que especificou na variável. Se ocorrer um erro ao aceder ao ficheiro de recursos de idioma na pasta especificada ou não defina a variável, o WinPE apresenta as mensagens no idioma padrão.  

    > [!NOTE]  
    > Quando protege o suporte de dados com uma palavra-passe, o texto que solicita ao utilizador a palavra-passe é sempre apresentado no idioma do WinPE.  

Utilize o procedimento seguinte para definir o idioma do WinPE para implementações de sistema operacional iniciadas por suportes de dados ou de PXE.  

#### <a name="process-to-set-the-windows-pe-language-for-a-pxe-or-media-initiated-os-deployment"></a>Processo para definir o idioma do Windows PE para uma implantação de sistema operacional iniciadas por suportes de dados ou de PXE  

1. Antes de atualizar a imagem de arranque, certifique-se de que o arquivo de recurso de sequência de tarefas adequado (tsres) está na pasta do idioma correspondente no servidor do site. Por exemplo, o ficheiro de recursos em inglês está na seguinte localização: `<ConfigMgrInstallationFolder>\OSD\bin\x64\00000409\tsres.dll`  

2. Como parte do comando de Pré-início, defina o **SMSTSLanguageFolder** variável de ambiente para o ID de idioma apropriado. O ID de idioma deve ser especificado utilizando o formato decimal e não o hexadecimal. Por exemplo, para definir o ID de idioma para inglês, especifique o valor decimal **1033**, não o valor hexadecimal 00000409 do nome da pasta.  
