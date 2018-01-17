---
title: "Utilizador suscitada pelo departamento de instalação"
titleSuffix: Microsoft Deployment Toolkit
description: "Guia para programadores para utilizador suscitada pelo departamento de instalação do Microsoft implementação Toolkit 2013. "
ms.date: 09/09/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: article
ms.assetid: a2b3a3a0-7b81-4191-b1f9-c618e59347c3
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 434178f100c32a4188ecf5283066f9332035f761
ms.sourcegitcommit: 645cd5a324bdd299906efa27eaca5885eafc9e9c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/16/2018
---
# <a name="user-driven-installation---developers-guide"></a>Utilizador orientadas por instalação - guia para programadores
Instalação de orientadas por utilizador (UDI) ajuda a simplificar a implementação de Windows® sistemas operativos cliente, como o Windows 8.1, a computadores utilizando a funcionalidade de implementação (OSD) do sistema operativo no Microsoft® System Center 2012 R2 Configuration Manager. UDI faz parte do Microsoft Deployment Toolkit (MDT).  

## <a name="introduction"></a>Introdução  
 Normalmente, quando implementar sistemas operativos utilizando a funcionalidade OSD, tem de fornecer todas as informações necessárias para implementar o sistema operativo. As informações estão configuradas nos ficheiros de configuração ou nas bases de dados (por exemplo, o ficheiro CustomSettings.ini ou a base de dados do MDT [MDT DB]). Tem de fornecer todas as definições de configuração pode iniciar a implementação.  

 UDI fornece uma interface orientada por assistente que permite-lhe fornecer informações de configuração imediatamente antes de efetuar a implementação. Este comportamento permite-lhe criar sequências de tarefas OSD genéricas e, em seguida, fornecer informações específicas do computador no momento da implementação, que fornece uma maior flexibilidade no processo de implementação.  

### <a name="target-audience"></a>Público-alvo  
 Este guia foi escrito para os programadores que criam páginas do assistente personalizado para o Assistente de UDI e editores de página do assistente personalizado para o UDI Wizard Designer. Este guia pressupõe que está familiarizado com o desenvolvimento de aplicações do Windows a utilizar:  

-   C++, o que é utilizado para criar páginas de assistente personalizado  

-   Microsoft .NET Framework, que é utilizado para criar uma página do assistente personalizado editores  

-   Windows Presentation Foundation (WPF), que é utilizado para criar uma página do assistente personalizado editores  

-   Idiomas WPF suporta, como c#, C++ ou Visual Basic do Microsoft® .NET, que são utilizados para criar editores de página do assistente personalizado  

### <a name="about-this-guide"></a>Acerca deste guia  
 Este guia fornece as informações de referência necessários para o ajudar a personalizar UTI para a sua organização. Este guia aborda tópicos administrativos ou operacionais, tais como instalar o MDT (que inclui UDI), configurar UDI para implementar sistemas operativos e aplicações ou efetuar implementações que utilizam o Assistente de UDI. Para mais informações sobre estes tópicos, consulte os tópicos UDI *utilizar o Microsoft Deployment Toolkit*, que está incluída no MDT.  

## <a name="udi-development-overview"></a>Descrição geral do desenvolvimento de UDI  
 Desenvolvimento de UDI permite que expandir as funcionalidades que fornece UDI. Normalmente, desenvolvimento de UDI é necessário quando pretender recolher informações adicionais que o processo de implementação de UDI consome. Estas informações adicionais, normalmente, são guardadas como variáveis de sequência de tarefas que os passos de sequência de tarefas numa sequência de tarefas UDI no Configuration Manager de leitura.  

### <a name="udi-architecture"></a>Arquitetura UDI  
 O objetivo de nível superior de desenvolvimento de UDI consiste em criar páginas de assistente personalizadas que podem ser apresentadas no Assistente de UDI. Ao criar páginas do assistente personalizado, pode expandir as funcionalidades existentes de UDI para satisfazer os da empresa e requisitos técnicos da sua organização. Uma página do assistente personalizado recolhe informações para além ou em vez das páginas do assistente que UDI fornece.  

 Figura 1 ilustra a relação entre o UDI Wizard Designer e o Assistente de UDI.  

 ![UDIDevelopersGuide1](media/UDIDevelopersGuide1.jpg "UDIDevelopersGuide1")  
Figura 1. Relação entre o assistente UDI e UDI Wizard Designer  

 **Figura 1. Relação entre o assistente UDI e UDI Wizard Designer**  

 Um nível conceptual, desenvolvimento de UDI inclui a criação de:  

-   **Páginas do assistente personalizado**. Páginas do assistente são apresentadas no Assistente de UDI e recolhem as informações necessárias para concluir o processo de implementação. Criar páginas de assistente utilizar C++ Microsoft Visual Studio®. As páginas do assistente personalizados são implementadas como dll, que lê o Assistente de UDI. O UDI software development kit (SDK) inclui um exemplo de como criar páginas do assistente personalizado.  

-   **Editores de página do assistente personalizado**. Utilize editores de página do Assistente para configurar o comportamento da sua página de assistente personalizado. Os editores de página do assistente personalizados são implementados como dll, que lê o UDI Wizard Designer. Criar página do Assistente para editores utilizando:  

    -   [WPF](http://msdn.microsoft.com/library/ms754130.aspx) versão 4.0  

    -   [Microsoft prisma](http://compositewpf.codeplex.com/) versão 4.0  

    -   [Microsoft Unity Application Block](http://unity.codeplex.com/) (Unity) versão 2.1  

     MDT inclui todas as assemblagens necessárias para criar uma página do assistente personalizado editor para utilização no UDI Wizard Designer. O SDK de UDI inclui um exemplo de como criar editores de página do assistente personalizado.  

 Além disso, o UDI Wizard Designer consome suporte ficheiros de configuração do editor de página do assistente. Criar o editor de página do Assistente de ficheiros de configuração como parte do processo para criar as páginas do assistente personalizado e editores de página do assistente personalizado. O UDI Wizard Designer cria as informações necessárias do XML no ficheiro de configuração do Assistente de UDI e ficheiro. App correspondente.  

### <a name="preparing-the-udi-development-environment"></a>Preparar o ambiente de desenvolvimento de UDI  
 Antes de começar a criar os seus próprios páginas do assistente personalizados e a página do Assistente para editores, execute os seguintes passos para preparar o ambiente de desenvolvimento de UDI:  

1.  Prepare o desenvolvimento de UDI pré-requisitos de ambiente conforme descrito no [preparar os pré-requisitos de ambiente de desenvolvimento de UDI](#PrepareUDIDevelopmentEnvironmentPrerequisites).  

2.  Configurar o ambiente de desenvolvimento de UDI conforme descrito em [configurar o ambiente de desenvolvimento de UDI](#ConfigureUDIDevelopmentEnvironment).  

3.  Certifique-se de que o ambiente de desenvolvimento de UDI está configurado corretamente conforme descrito em [verificar o ambiente de desenvolvimento de UDI](#VerifyUDIDeploymentEnvironment).  

####  <a name="PrepareUDIDevelopmentEnvironmentPrerequisites"></a>Preparar os pré-requisitos de ambiente de desenvolvimento de UDI  
 Para preparar o desenvolvimento de UDI pré-requisitos de ambiente, execute os seguintes passos:  

1.  Prepare os pré-requisitos de hardware de ambiente de desenvolvimento UDI conforme descrito no [preparar os pré-requisitos de Hardware de ambiente de desenvolvimento de UDI](#PrepareUDIDevelopmentEnvironmentHardwarePrerequisites).  

2.  Preparar o ambiente de desenvolvimento de UDI os pré-requisitos de software, tal como descrito no [preparar os pré-requisitos de Software de ambiente de desenvolvimento de UDI](#PrepareUDIDevelopmentEnvironmentSoftwarePrerequisites).  

#####  <a name="PrepareUDIDevelopmentEnvironmentHardwarePrerequisites"></a>Preparar os pré-requisitos de Hardware de ambiente de desenvolvimento de UDI  
 Os pré-requisitos de hardware de ambiente de desenvolvimento de UDI são os mesmos requisitos de hardware para a edição do Microsoft Visual Studio 2010 estiver a utilizar. Para obter mais informações sobre estes requisitos, consulte os requisitos de sistema para cada edição em [produtos do Visual Studio 2010](http://www.microsoft.com/visualstudio/products/2010-editions).  

#####  <a name="PrepareUDIDevelopmentEnvironmentSoftwarePrerequisites"></a>Preparar os pré-requisitos de Software de ambiente de desenvolvimento de UDI  
 O ambiente de desenvolvimento de UDI tem os seguintes pré-requisitos de software:  

-   Janelas de sistema operativo que suporta do Visual Studio 2010 (Windows 7 ou Windows Server® 2008 R2 é recomendado.)  

     Precisa de um sistema operativo Windows que suporte a arquitetura de processador para o qual pretende desenvolver. Pode efetuar o desenvolvimento de UDI de 32 bits e 64 bits com um sistema operativo de 64 bits. Apenas efetuar o desenvolvimento de UDI de 32 bits em sistemas operativos de 32 bits. Por este motivo, deve utilizar um sistema operativo de 64 bits.  

    > [!NOTE]
    >  Versões de IntelItanium (IA-64) do sistema operativo Windows não são suportadas para ambientes de desenvolvimento de UDI.  

     Para mais informações sobre os sistemas operativos que suporta o Visual Studio 2010, consulte os requisitos de sistema para cada edição em [produtos do Visual Studio 2010](http://www.microsoft.com/visualstudio/products/2010-editions).  

-   Microsoft .NET Framework versão 4.0 (requerido pelo Visual Studio 2010)  

-   Linguagem C++ (o idioma utilizado em expandir as páginas do Assistente de UDI)  

-   Outros idiomas que WPF suporta, como c#, Visual Basic .NET ou C + + /Safari/Chrome idioma uma infraestrutura comum, que são utilizados para expandir editores de página do assistente UDI Wizard Designer  

    > [!NOTE]
    >  O código de origem de exemplo para os editores de página do Assistente de UDI Wizard Designer é escrito em c#. Instale a linguagem c#, se pretender utilizar o código de origem de exemplo.  

####  <a name="ConfigureUDIDevelopmentEnvironment"></a>Configurar o ambiente de desenvolvimento de UDI  
 Depois de UDI, em seguida, são cumpridos os pré-requisitos de ambiente de desenvolvimento, execute os seguintes passos para configurar o ambiente de desenvolvimento de UDI:  

1.  Instale Visual Studio 2010.  

     Certifique-se de que instala o idioma de C++ e qualquer idioma que suporta o WPF.  

    > [!NOTE]
    >  O código de origem de exemplo para as páginas do editor de UDI Wizard Designer é escrito em c#. Instale a linguagem c#, se pretender utilizar o código de origem de exemplo.  

     Para obter mais informações sobre a instalação do Visual Studio 2010, consulte [instalar o Visual Studio](http://msdn.microsoft.com/library/e2h7fzkw.aspx).  

2.  Instale o MDT.  

     Para obter mais informações sobre como instalar o MDT, consulte a secção "Instalar ou atualizar para o MDT", no MDT documentar *utilizar o Microsoft Deployment Toolkit*.  

3.  No Explorador do Windows, criar *local_folder* (onde *local_folder* é qualquer pasta localizada numa unidade local no computador de desenvolvimento).  

4.  Copiar o *installation_folder*\SDK pasta *local_folder* (onde *installation_folder* é a pasta na qual instalou o MDT e *local_ pasta* é qualquer pasta localizada numa unidade local no computador de desenvolvimento).  

     Copie a pasta SDK para outra localização porque o MDT é instalado na pasta de ficheiros de programa, não pode ser escrita sem permissões elevadas. Copiar a pasta SDK para outra localização permite-lhe modificar os ficheiros na pasta SDK sem necessidade de permissões elevadas.  

5.  Copiar o *installation_folder*\Templates\Distribution\Tools pasta *local_folder* (onde *installation_folder* é a pasta na qual instalou o MDT e *local_folder* é a pasta que criou anteriormente no processo).  

6.  Mudar o nome de *local_folder*\Tools pasta *local_folder*\OSDSetupWizard (onde *local_folder* é a pasta que criou anteriormente no processo).  

     Quando tiver terminado, a estrutura de pastas sob *local_folder* deverá ser semelhante a estrutura de pasta ilustrada na figura 2 (onde *local_folder* é a pasta que criou anteriormente no processo e é apresentada como *UDIDevelopment* na figura).  

     ![UDIDevelopersGuide2](media/UDIDevelopersGuide2.jpg "UDIDevelopersGuide2")  
Figura 2. Estrutura de pastas para o desenvolvimento de UDI  

     **Figura 2. Estrutura de pastas para o desenvolvimento de UDI**  

####  <a name="VerifyUDIDeploymentEnvironment"></a>Verifique se o ambiente de desenvolvimento de UDI  
 Quando o ambiente de desenvolvimento de UDI está configurado, certifique-se de que o ambiente de desenvolvimento de UDI está configurado corretamente, garantindo que os projetos de exemplo corretamente compilar no Visual Studio 2010.  

 Certifique-se de que o ambiente de desenvolvimento de UDI está corretamente configurado através da determinação de se:  

-   O projeto de SamplePage baseia-se corretamente conforme descrito em [Certifique-se de que o projeto de SamplePage baseia-se corretamente](#VerifySamplePageProjectBuildsCorrectly)  

-   O projeto de SampleEditor baseia-se corretamente conforme descrito em [Certifique-se de que o projeto de SampleEditor baseia-se corretamente](#VerifySampleEditorProjectBuildsCorrectly)  

#####  <a name="VerifySamplePageProjectBuildsCorrectly"></a>Certifique-se de que o projeto de SamplePage baseia-se corretamente  
 O projeto de SamplePage fornece um exemplo de como criar uma página do assistente personalizado para o Assistente de UDI. Para obter mais informações sobre o projeto de SamplePage, consulte [reveja o SamplePage solução do Visual Studio](#ReviewSamplePageVisualStudioSolution).  

 **Para verificar que o projeto de SamplePage baseia-se corretamente**  

1.  Inicie o Visual Studio 2010.  

2.  Abra o projeto de SamplePage.  

     O projeto de SamplePage reside no *local_folder*\SDK\UDI\SamplePage pasta (onde *local_folder* é a pasta que criou anteriormente no processo).  

3.  No Visual Studio 2010, no Explorador de soluções, clique com o botão direito no projeto SamplePage e, em seguida, clique em **propriedades**.  

     O **páginas de propriedades de SamplePage** é apresentada a caixa de diálogo.  

4.  No **páginas de propriedades de SamplePage** caixa de diálogo, aceda a propriedades/depuração de configuração.  

5.  Nas propriedades de depuração, sob **configuração**, selecione **todas as configurações**.  

6.  Nas propriedades de depuração, sob **comando**, tipo **$(TargetDir)\OSDSetupWizard.exe.**  

7.  Nas propriedades de depuração, sob **diretório de trabalho**, tipo **$(TargetDir)**.  

8.  No **páginas de propriedades de SamplePage** caixa de diálogo, aceda a propriedades de configuração/compilação eventos/Post-Build eventos.  

9. Nas propriedades do evento de pós-compilação, sob **linha de comandos**, escreva o seguinte:  

    ```  
    copy /y "$(ProjectDir)..\..\..\..\OSDSetupWizard\x86\*.*" "$(TargetDir)"  
    xcopy /y /i "$(ProjectDir)..\..\..\..\OSDSetupWizard\x86\en-us" "$(TargetDir)en-us"  
    copy /y "$(ProjectDir)..\..\..\..\OSDSetupWizard\OSDResults\Images\UDI_Wizard_Banner.bmp" "$(ProjectDir)header.bmp"  
    copy /y "$(ProjectDir)Config.xml" "$(TargetDir)”  
    copy /y "$(ProjectDir)header.bmp" "$(TargetDir)header.bmp"  
    ```  

10. No **páginas de propriedades de SamplePage** caixa de diálogo, clique em **OK**.  

11. Guarde o projeto.  

12. Do **depurar** menu, clique em **iniciar depuração**.  

     O **Microsoft Visual Studio**é apresentada a caixa de diálogo que indica que a origem de está desatualizada e pede-lhe se pretende criar o projeto.  

13. No **Microsoft Visual Studio** caixa de diálogo, clique em **Sim**.  

     O **informações de depuração não** é apresentada a caixa de diálogo informando-o de que não existem informações de depuração estão disponíveis para OSDSetupWizard.exe.  

14. No **informações de depuração não** caixa de diálogo, clique em **Sim**.  

     O Assistente de UDI abre-se com a página do assistente personalizado apresentada.  

15. Certifique-se de que pode selecionar um valor na **escolha a localização**.  

16. No **assistente com a página de exemplo** formulário, clique em **Cancelar**.  

     O **cancelar o assistente** é apresentada a caixa de diálogo.  

17. No **cancelar o assistente** caixa de diálogo, clique em **Sim**.  

18. Feche o Visual Studio 2010.  

#####  <a name="VerifySampleEditorProjectBuildsCorrectly"></a>Certifique-se de que o projeto de SampleEditor baseia-se corretamente  
 O projeto de SampleEditor fornece um exemplo de como criar um editor de página do assistente personalizado para o UDI Wizard Designer. Para obter mais informações sobre o projeto de SampleEditor, consulte [reveja o SamplePage solução do Visual Studio](#ReviewSamplePageVisualStudioSolution).  

 **Para verificar que o projeto de SampleEditor baseia-se corretamente**  

1.  Inicie o Visual Studio 2010.  

2.  Abra o projeto de SampleEditor.  

     O projeto de SampleEditor reside no *local_folder*\SDK\UDI\SampleEditor pasta (onde *local_folder* é a pasta que criou anteriormente no processo).  

3.  No Visual Studio 2010, no Explorador de soluções, selecione o projeto de SampleEditor.  

4.  Do **projeto** menu, clique em **Adicionar referência**.  

     O **Adicionar referência** é aberta a caixa de diálogo.  

5.  No **Adicionar referência** caixa de diálogo, clique em de **procurar** separador.  

6.  No **procurar** separador, aceda a *installation_folder*\Bin (onde *installation_folder* é a pasta na qual instalou o MDT). Selecione os seguintes ficheiros e, em seguida, clique em **OK**:  

    -   Microsoft.Enterprise.UDIDesigner.Common.dll  

    -   Microsoft.Enterprise.UDIDesigner.DataService.dll  

    -   Microsoft.Enterprise.UDIDesigner.Infrastructure.dll  

    -   Microsoft.Practices.Prism.dll  

    -   Microsoft.Practices.ServiceLocation.dll  

    -   Microsoft.Practices.Unity.dll  

    -   RibbonControlsLibrary.dll  

    > [!NOTE]
    >  Pode selecionar vários ficheiros no **procurar** separador ao premir a tecla CTRL enquanto clica os ficheiros.  

7.  No Explorador de soluções, aceda a SampleEditor/referências.  

8.  Certifique-se de que nenhuma das referências tem quaisquer avisos ou erros.  

9. No Explorador de soluções, clique com o botão direito no projeto SampleEditor e, em seguida, clique em **propriedades**.  

     O **páginas de propriedades de SampleEditor** é apresentada a caixa de diálogo.  

10. No **páginas de propriedades de SampleEditor** caixa de diálogo, clique no **depurar** separador.  

11. No **depurar** separador, clique em **programa externo início**.  

12. No **programa externo início**, tipo ***installation_folder\Bin\UDIDesigner.exe*** (onde *installation_folder* é a pasta na qual instalou o MDT) e, em seguida, clique em **OK**.  

    > [!TIP]
    >  Pode clicar no botão de reticências (…) para navegar para a pasta e selecione UDIDesigner.exe.  

13. Do **ficheiro** menu, clique em **Guardar tudo**.  

14. Copiar o *local_folder*\SDK\SamplePage\SamplePage.dll.config ficheiro para o *installation_folder*\Bin\Config pasta (onde *local_folder* é a pasta criado no computador de desenvolvimento anteriormente no processo de configuração e*installation_folder* é a pasta na qual instalou o MDT).  

15. No Visual Studio 2010, do **depurar** menu, clique em **iniciar depuração**.  

     Inicia o UDI Wizard Designer.  

16. No UDI Wizard Designer, no Friso, clique em **abra**.  

     O **abra** é apresentada a caixa de diálogo.  

17. No **abrir** caixa de diálogo, abra o *local_folder*\SDK\SamplePage\SamplePage\Config.xml ficheiro (onde *local_folder* é a pasta que criou no desenvolvimento computador anteriormente no processo de configuração).  

     Config.xml para abrir o ficheiro e personalizada [StageGroup](#StageGroup) é apresentado no painel de detalhes.  

18. No painel de detalhes, clique o **configurar** separador.  

19. Reveja as informações de configuração para o **localização** caixa, incluindo o seguinte:  

    -   **Desbloqueado** botão, com a qual ativar ou desativar o **localização** caixa  

    -   **Valor predefinido** caixa, na qual introduz um valor predefinido para ser apresentado no **localização** caixa  

    -   **Nome a apresentar amigável visível na página Resumo**, na qual introduz a legenda para as informações apresentadas no **resumo** página  

    -   **Localização** caixa de listagem que inclui uma lista de localizações possíveis  

20. Feche o UDI Wizard Designer.  

21. Feche o Visual Studio 2010.  

## <a name="reviewing-the-udi-sdk-examples"></a>Rever os exemplos de UDI SDK  
 Antes de iniciar o desenvolvimento, reveja os exemplos fornecidos no UDI SDK. Utilize as informações neste guia e o código de origem nos exemplos para ajudar a criar os seus próprios páginas do assistente personalizada de UDI e a página do Assistente para editores.  

 Avance os exemplos de UDI SDK revendo o:  

-   Conteúdo da pasta SDK que copiou anteriormente no processo de instalação, conforme descrito em [reveja o conteúdo da pasta SDK](#ReviewContentsofSDKFolder)  

-   Personalizado exemplo página do assistente UDI conforme descrito em [reveja o SamplePage solução do Visual Studio](#ReviewSamplePageVisualStudioSolution)  

-   Personalizado UDI assistente página editor exemplo conforme descrito em [reveja o SampleEditor solução do Visual Studio](#ReviewSampleEditorVisualStudioSolution)  

###  <a name="ReviewContentsofSDKFolder"></a>Reveja o conteúdo da pasta SDK  
 Durante a configuração do ambiente de desenvolvimento de UDI, copiados da pasta SDK a partir da pasta na qual instalou o MDT para outra pasta que criou. Tabela 1 apresenta uma lista de pastas imediatamente abaixo da pasta SDK e fornece uma breve descrição de cada.  

### <a name="table-1-folders-in-the-udi-sdk"></a>Tabela 1. Pastas no UDI SDK  

|**Pasta**|**Esta pasta contém**|  
|-|-|  
|Inclui|Os ficheiros de cabeçalho de C++ necessários para criar páginas do assistente personalizado para o Assistente de UDI|  
|Bibliotecas|Os ficheiros da biblioteca C++ que serão ligados à sua página personalizada; Existem versões de 32 bits e 64 bits das bibliotecas de ligação estático. **Nota:**  Versões de Itanium das bibliotecas (IA-64) não estão disponíveis.|  
|SampleEditor|Um projeto do Visual Studio para a criação de um editor de personalizado utilizado para Editar página de SamplePage de UDI Wizard Designer, é escrito em c#|  
|SamplePage|Um projeto do Visual Studio para criar uma página de assistente UDI personalizada, o que é escrita em Visual C++|  

###  <a name="ReviewSamplePageVisualStudioSolution"></a>Analise a solução do SamplePage Visual Studio  
 Antes de começar a criar as páginas do assistente personalizado e página do Assistente para editores, efetue as seguintes tarefas para preparar o ambiente de desenvolvimento de UDI:  

-   Reveja as fases no ciclo de vida de uma página do assistente UDI conforme descrito em [reveja o ciclo de vida de página do assistente](#ReviewWizardPageLifeCycle).  

-   Reveja a solução do Visual Studio para o exemplo de SamplePage no UDI SDK conforme descrito em [reveja o exemplo de SamplePage](#ReviewSamplePageExample).  

####  <a name="ReviewWizardPageLifeCycle"></a>Reveja o ciclo de vida de página do Assistente  
 Uma página do assistente UDI tem métodos que correspondem a cada fase (ou fase) do ciclo de vida da página. Como parte da criação da página do assistente personalizado, tem de substituir estes métodos com o seu código. Tabela 2 lista os métodos que terá de substituir e fornece uma breve descrição de cada método, incluindo quando utilizar o método no ciclo de vida da página do assistente.  

### <a name="table-2-methods-in-a-wizard-page-life-cycle"></a>Tabela 2. Métodos de um assistente página ciclo de vida  

|**Método**|**Descrição**|  
|-|-|  
|**OnWindowCreated**|Este método é chamado uma vez, depois de ter sido criada a janela da página.<br /><br /> Para que este método, escreva código que inicializa a página pela primeira vez e só tem de ser efetuada uma vez. Por exemplo, utilizar este método para inicializar campos ou ler informações de configuração a **Setter** elementos no ficheiro de configuração do Assistente de UDI.|  
|**OnWindowShown**|Este método é denominado sempre que a página é apresentada (mostrado) no Assistente de UDI. É denominado na primeira vez que a página é apresentada e sempre navegar para a página clicando **seguinte** ou **novamente** no assistente.<br /><br /> Para que este método, escrever código que prepara a página ser apresentada — por exemplo, ao ler as variáveis de memória, as variáveis de sequência de tarefas ou variáveis de ambiente e, em seguida, atualizar a página com base nas alterações para essas variáveis.|  
|**OnCommonControlEvent**|Este método pode ser chamado sempre que a página do assistente, é apresentada e recebe uma mensagem WM_NOTIFY a partir de um elemento subordinado (normalmente, controla comum).<br /><br /> Para que este método, escreva código que processa WM_NOTIFY com base na mensagem de notificação. Por exemplo, poderá responder a eventos a partir de um controlo comuns, tais como responder clique ou faça duplo clique em eventos para um **TreeView** controlo.|  
|**OnUnhandledEvent**|Este método é denominado sempre que ocorre uma mensagem de janela não processada para a página do assistente. Este método proporciona a oportunidade de intercetar e processar estas caso contrário, não processada mensagens de janela.<br /><br /> Para que este método, escreva código que processa as mensagens de janela que são relevantes para a página do assistente. Normalmente, não terá de substituir este método.|  
|**OnNextClicked**|Este método é denominado quando clicar em **seguinte** no assistente.<br /><br /> Para que este método, escrever código que efetua quaisquer ações necessárias antes de mover para a página seguinte do assistente — por exemplo, efetuar a validação pode demorar muito tempo. Se a validação falhar, pode cancelar o **seguinte** pedir e apresentar uma mensagem.|  
|**OnWindowHidden**|Este método é denominado sempre que a página se encontra oculto quando é apresentada a página de assistente anterior ou seguinte.<br /><br /> Para que este método, escreva código que efetua quaisquer ações antes da página está oculta, antes de outra página a ser mostrada. Normalmente, não terá de substituir este método.|  

####  <a name="ReviewSamplePageExample"></a>Reveja o exemplo de SamplePage  
 Reveja o exemplo de SamplePage utilizando a lista seguinte, que representa a sequência de eventos durante o ciclo de vida de página do Assistente do exemplo SamplePage:  

1.  O Assistente de UDI, OSDSetupWizard.exe, lê as informações de configuração do ficheiro de configuração do Assistente de UDI no exemplo (o ficheiro Config.xml), conforme descrito em [passo 1: O assistente UDI (OSDSetupWizard.exe) lê o ficheiro de Config.xml](#UDIWizardReadstheConfigFile).  

2.  O Assistente de UDI carrega a dll necessários para cada página do assistente listada no ficheiro de configuração do Assistente de UDI conforme descrito em [passo 2: O assistente UDI carrega a DLL para a página do assistente personalizado](#UDIWizardLoadstheDLLforCustomWizardPage).  

3.  O Assistente de UDI apresenta a página do assistente personalizado e permite a interação do controlo pretendido conforme descrito em [passo 3: O assistente UDI apresenta a página do assistente personalizado](#UDIWizardDisplaysCustomWizardPage).  

4.  Quando a página do assistente personalizado recolheu as informações, executar quaisquer tarefas de necessárias antes de clicar em **seguinte** prossiga para o assistente seguinte, conforme descrito em [passo 4: O botão seguinte é clicado na página do assistente personalizado](#TheNextButtonisClickedinCustomWizardPage).  

#####  <a name="UDIWizardReadstheConfigFile"></a>Passo 1: O assistente UDI (OSDSetupWizard.exe) lê o ficheiro de Config.xml  
 Quando é iniciado o Assistente de UDI (OSDSetupWizard.exe), por predefinição, lê o ficheiro de configuração do Assistente de UDI, que é o ficheiro UDIWizard_Config.xml — o ficheiro de configuração principal para o Assistente de UDI.  

> [!NOTE]
>  O exemplo utiliza o ficheiro Config.xml como o ficheiro de configuração. No MDT, o ficheiro de configuração predefinida é o ficheiro de UDIWizard_Config.xml, que reside na pasta de Scripts no pacote de ficheiros do MDT, para a configuração.  

 Pode substituir o ficheiro de configuração predefinida que o Assistente de UDI utiliza modificando o passo de sequência de tarefas do Assistente de UDI para utilizar o **/definition** parâmetro. Para obter mais informações sobre como substituir o ficheiro de configuração predefinidas que utiliza o Assistente de UDI, consulte "Substituir a configuração do ficheiro que o UDI assistente utiliza".  

 Os elementos de nível superior no ficheiro Config.xml são o  

-   [DLLs](#DLLs) elemento  

-   [Estilo](#Style) elemento  

-   [Páginas](#Pages) elemento  

-   [StageGroups](#StageGroups) elemento  

 Para obter mais informações sobre o esquema do ficheiro de configuração do Assistente de UDI e cada um destes elementos, consulte [referência de esquema de ficheiro de configuração de Assistente de UDI](#UDIWizardConfigurationFileSchemaReference).  

 O Assistente de UDI analisa o **DLLs** elemento à procura de ficheiros. dll carregar. No exemplo, dois ficheiros. dll estão listados: SamplePage.dll e SharedPages.dll. Estes ficheiros. dll tem de residir na mesma pasta que OSDSetupWizard.exe—the ferramentas\\*plataforma* pasta (onde *plataforma* x86 para a versão de 32 bits ou x64 para a versão de 64 bits).  

 O Assistente de UDI analisa o **páginas** elemento procura as páginas que estão definidas. No exemplo, são definidas duas páginas: **Personalizada** e **SummaryPage**. O **tipo** atributo o **página** elemento é definido no ficheiro PageClassIDs.h e exclusivamente define o tipo da sua página personalizado.  

 No exemplo, é o tipo definido **Microsoft.SamplePage.LocationPage**. Para a sua página personalizada, substitua o seguinte procedimento para evitar quaisquer potenciais conflitos com outras páginas, que pode criar no futuro:  

-   O nome da organização em vez de **Microsoft**.  

-   O nome do projeto em vez de **SamplePage**.  

-   O nome de página do assistente personalizado em vez de **LocationPage**.  

#####  <a name="UDIWizardLoadstheDLLforCustomWizardPage"></a>Passo 2: O assistente UDI carrega a DLL para a página do assistente personalizado  
 Quando o Assistente de UDI carrega a DLL, aquele invoca o **RegisterFactories** função, o que tem de ser implementada no seu ficheiro. dll. No exemplo, esta função é implementada no ficheiro dllmain.ccp. Cada página do assistente criar tem de implementar o **RegisterFactories** função.  

 O **RegisterFactories** função é utilizada para registar a classe de fábrica do seu página do assistente com o registo de fábrica de classe para o Assistente de UDI. *Classe fábricas* são as classes que podem criar uma instância de outra classe. O **RegisterFactories** função cria uma nova instância de uma classe de fábrica e transmite dessa classe para o registo de fábrica de classe para o Assistente de UDI, que disponibiliza dessa classe de fábrica para o assistente. O Assistente de UDI procura uma classe de fábrica registada com um ID que corresponda a **tipo** atributo do **página** elemento para a página do assistente personalizado.  

 No exemplo, o ID está definido como **ID_Location** no ficheiro PageClassIds.h como **Microsoft.SamplePage.LocationPage**, que corresponde a **tipo** atributo para o  **Página** elemento no ficheiro Config.xml. **ID_Location** é transmitida como um parâmetro no **RegisterFactories** função implementada no ficheiro dllmain.ccp.  

 Pode criar uma função utilizando o Register_*nome* modelo de função para simplificar a criação de uma nova instância de fábrica e registar a instância recentemente criada. O **nome** valor fornecido utilizando o modelo de função de registo tem de implementar o **iClassFactory** interface. O [ClassFactoryImpl classe](#ClassFactoryImplClass) processa a maioria dos detalhes para implementar uma fábrica de classe.  

 Também pode utilizar o **RegisterFactories** função registar tipos de tarefas e tipos de validação. Para obter mais informações, consulte o seguinte:  

-   [Criar tarefas UDI personalizado](#CreatingCustomUDITasks)  

-   [Criar validações UDI personalizado](#CreatingCustomUDIValidators)  

> [!NOTE]
>  O exemplo contém e regista apenas um personalizado página do assistente. O exemplo não inclui tarefas personalizadas ou validações e, por isso, não registou qualquer tarefas personalizadas ou validações.  

#####  <a name="UDIWizardDisplaysCustomWizardPage"></a>Passo 3: O assistente UDI apresenta a página do assistente personalizado  
 A página do assistente personalizado no exemplo é definida no ficheiro LocationPage.cpp. Páginas do assistente são derivadas de classes de modelo que fornecem que tem muito a uma página de funcionalidade. Todas as páginas de assistente devem derivar de [WizardPageImpl modelo classe](#WizardPageImplTemplateClass), que implementa o [IWizardPage Interface](#IWizardPageInterface). Pode implementar a cada página do Assistente de outras classes do modelo opcional e interfaces correspondentes com base nas necessidades da página.  

 O [WizardPageImpl modelo classe](#WizardPageImplTemplateClass) tem vários interfaces útil que podem ajudar a escrever páginas do assistente personalizado. Implementar o [WizardPageImpl modelo classe](#WizardPageImplTemplateClass) como a classe base para a página do assistente personalizado.  

 Para obter uma lista de disponíveis:  

-   Classes de modelo para páginas do assistente, consulte [Classes de programa auxiliar de página do Assistente](#WizardPageHelperClasses)  

-   Interfaces para as classes de modelo de página do assistente, consulte [Interfaces de página do Assistente](#WizardPageInterfaces)  

 A página do assistente personalizado no exemplo é derivada do [WizardPageImpl modelo classe](#WizardPageImplTemplateClass) e implementa o [IWizardPage Interface](#IWizardPageInterface). Além disso, a página do assistente personalizado implementa o **IFieldCallback** interface. Ambos são implementados no ficheiro LocationPage.cpp.  

 Página do assistente personalizada de exemplo substitui os seguintes métodos:  

-   **OnWindowCreated**. O **OnWindowCreated** método na página do Assistente de exemplo chama os métodos seguintes:  

    -   [AddField](#AddField). Este método relacionado com o **IDC_COMBO_LOCATION** caixa controlo a **IDD_LOCATION_PAGE** recurso com o [dados](#Data) elemento com o nome **localização**no ficheiro Config.xml.  

         Para além de **AddField** método, pode utilizar o [AddRadioGroup](#AddRadioGroup) e [AddToGroup](#AddToGroup) métodos para suportar outros controlos e comportamentos.  

        > [!NOTE]
        >  Certifique-se de que tem de chamar o [AddField](#AddField), [AddRadioGroup](#AddRadioGroup), ou [AddToGroup](#AddToGroup) método antes de chamar o [InitFields](#InitFields) método.  

    -   [InitFields](#InitFields). Utilize este método de inicialização de campos (controlos) que tenha adicionado ao formulário. O apontador da página é um parâmetro. No exemplo, o **isto** ponteiro é transmitido, que se refere a página atual.  

        > [!NOTE]
        >  Para suportar a utilização do **isto** ponteiro, tem de implementar o **IFieldCallback** interface para além das interfaces que o [WizardPageImpl modelo classe](#WizardPageImplTemplateClass) suporta.  

         O **IFieldCallback** interface chamadas a **SetFieldDefault** método, o que é utilizado para definir os valores predefinidos para controlos que não sejam de texto controlos caixa e a caixa de verificação. No exemplo, o **SetFieldDefault** método define o índice inicial do controlo de caixa de combinação com base no valor predefinido especificado no **predefinido** elemento para a [campo](#Field) elemento no ficheiro Config.xml.  

     O **OnWindowCreated** método configura o controlador de formulário utilizando o [IFormController interface](#IFormController-Interface). Para obter mais informações sobre como configurar o controlador do formulário, consulte [como configurar a forma](#SettingUptheForm).  

-   **InitLocations**. Este método preenche a caixa de combinação da lista de localizações no ficheiro Config.xml. O [dados](#Data) elemento e subordinados [DataItem](#DataItem) elementos o ficheiro Confg.xml fornecer a lista de valores possíveis.  

-   **OnNextClicked**. Este método efetua as seguintes tarefas:  

    -   Atualizações a **TSLocation** variável de sequência de tarefas com o valor selecionado a caixa de combinação utilizando o **SaveFields** método  

    -   Adiciona as informações que serão apresentadas no **resumo** página com o **SaveFields** método  

#####  <a name="TheNextButtonisClickedinCustomWizardPage"></a>Passo 4: O botão seguinte é clicado na página do assistente personalizado  
 Quando o utilizador concluir os campos na página do assistente personalizado, seja clica **seguinte**, que invoca o **OnNextClicked** método. O **OnNextClicked** método efetua quaisquer tarefas necessárias antes de avançar para a página seguinte do assistente, tais como a gravação de alterações de configuração efetuadas na página do assistente personalizado.  

 Para a página do assistente personalizado exemplo, a substituição para o **OnNextClicked** método é implementado no ficheiro LocationPage.ccp. No **OnNextClicked** são chamar do método na página do assistente personalizada de exemplo, os seguintes métodos:  

1.  [InitSection](#InitSection). Este método inicializa o cabeçalho (legenda etiqueta) para os dados de resumos apresentados no **resumo** página. Normalmente, pode definir este valor a utilizar o **DisplayName()** função. Os dados associados esta legenda estão guardados através de [SaveFields](#SaveFields) método.  

2.  [SaveFields](#SaveFields). Este método poupa valores de campo para variáveis de sequência de tarefas e os dados apresentados no **resumo** página.  

###  <a name="ReviewSampleEditorVisualStudioSolution"></a>Analise a solução do SampleEditor Visual Studio  
 Antes de começar a criar os seus próprios páginas do assistente personalizados e a página do Assistente para editores, execute os seguintes passos para preparar o ambiente de desenvolvimento de UDI:  

-   Reveja a arquitetura de UDI Wizard Designer, conforme descrito em [rever a arquitetura de estruturador do Assistente de UDI](#ReviewUDIWizardDesignerArchitecture).  

-   Reveja os componentes de uma página do Assistente de UDI que pode ser personalizada com o ficheiro de configuração do Assistente de UDI conforme descrito em [revisão componentes configurável de uma página do Assistente de UDI](#ReviewConfigurableComponentsofUDIWizardPage).  

-   Reveja o exemplo de EditorPage fornecido no UDI SDK conforme descrito em [reveja o exemplo de EditorPage](#ReviewEditorPageExample).  

####  <a name="ReviewUDIWizardDesignerArchitecture"></a>Reveja a arquitetura de estruturador de assistente UDI  
 O UDI Wizard Designer foi desenvolvido utilizando WPF, prisma e Unity. O estruturador de UDI é utilizado para editar o ficheiro de configuração do Assistente de UDI (UDIWizard_Config.xml), que lê o Assistente de UDI (OSDSetupWizard.exe) em tempo de execução. O [páginas](#Pages) elemento no ficheiro de configuração do Assistente de UDI contém uma lista das páginas que tenha um separado [página](#Page) elemento para cada página do assistente.  

 Ao editar as definições de configuração para uma página do assistente, o UDI Wizard Designer carrega o editor de página personalizada que corresponde ao tipo de página do assistente. Os editores de página do assistente personalizado são desenvolvidas como controlos de utilizador do WPF. O editor de página do assistente personalizado páginas utilize o [modelo – vista – ViewModel](http://msdn.microsoft.com/magazine/dd419663.aspx) padrão de conceção (MVVM) para WPF.  

 O padrão de conceção MVVM ajuda a separar a interface de utilizador (IU; apresentação) a partir dos dados que está a ser apresentados. Os dados são uma fachada através de [página](#Page) elemento no ficheiro de configuração de Assistente de UDI (o ficheiro de Config.xml no exemplo), que é acedido utilizando o [CurrentPage](#CurrentPage) propriedade do [ IDataService](#IDataService) interface.  

 O UDI Wizard Designer utiliza o **DependencyAttribute** para obter acesso ao **DataService** classe com base no framework de injeção de dependência na Unity. Para obter mais informações sobre a arquitetura de interjection de dependência na Unity, consulte [Injetar algumas vida nas suas aplicações — obter saber o bloco de aplicação Unity](http://msdn.microsoft.com/library/ff650806.aspx).  

####  <a name="ReviewConfigurableComponentsofUDIWizardPage"></a>Reveja configuráveis componentes de uma página do assistente UDI  
 Como criar a página do assistente personalizado, algumas das definições de configuração podem ser definidas no código e não podem ser alteradas após ter compilação da página. No entanto, para outras definições de configuração, será necessário permitir que as definições de configuração a ser alterado utilizando o UDI Wizard Designer.  

 Normalmente, as definições de configuração que pretende configurar com o UDI Wizard Designer são guardadas no ficheiro de configuração do Assistente de UDI (o ficheiro Config.xml no exemplo). No entanto, também pode criar os seus próprios ficheiros de configuração separadas, se necessário. Um exemplo de utilização de um ficheiro de configuração separadas é o UDIWizard_Config.xml.app de ficheiros, que o **deteção de aplicação** tarefas e o **ApplicationPage** utilização de tipo de página do assistente.  

 Segue-se uma lista das definições de configuração típica que possa gerir utilizando o UDI Wizard Designer:  

-   **Campo**. Campos de utilização permitem aos utilizadores fornecer comentários. Os campos são apresentados como [campo](#Field) elementos no ficheiro de configuração do Assistente de UDI (UDIWizard_Config.xml), que contém as definições de configuração para cada campo. O editor de página do assistente correspondente tem de fornecer um método para editar as definições de configuração de campo para o campo utilizando o [FieldElementControl](#FieldElementControl).  

-   **Propriedades**. Setters ajudam a criar propriedades de entidades na página, tais como páginas na [página](#Page) elemento, campos no [campo](#Field) elemento ou dados no [dados](#Data) ou [ DataItem](#DataItem) elementos. Configurar propriedades de [Setter]() elementos. Adicionar um separado [Setter]() elemento para cada propriedade que pretende definir. Editar as propriedades utilizando o [SetterControl](#SetterControl) e configurar outros [Setter]() elementos utilizando outros controlos.  

-   **Dados**. Dados são utilizados para armazenar informações de utilização por outros componentes e a página do assistente. Pode definir os dados para as páginas ou campos utilizando o [dados](#Data) ou [DataItem](#DataItem) elementos. Os dados podem ser definidos numa estrutura hierárquica ou simples através da utilização adequada do [dados](#Data) ou [DataItem](#DataItem) elementos. Config.xml no exemplo no SDK mostra como criar estruturas de dados simples.  

 O editor de página do assistente personalizados que criar tem de ser capaz de gerir estas definições de configuração.  

####  <a name="ReviewEditorPageExample"></a>Reveja o exemplo de EditorPage  
 O exemplo de EditorPage é utilizado para configurar as definições de configuração para o **SamplePage** página do assistente no ficheiro de configuração do Assistente de UDI. O exemplo de EditorPage tem os seguintes componentes principais:  

-   IU para configurar o **localização** definições da caixa de combinação  

-   IU para adicionar ou editar uma localização na lista de localizações possíveis, o que são apresentadas no **localização** caixa de combinação  

-   Definições de configuração lida e guardado o ficheiro de configuração do Assistente de UDI  

-   Código de suporte para os outros componentes  

 Reveja o exemplo de EditorPage no Visual Studio, efetuando os seguintes passos:  

1.  Reveja como as **SampleEditor** editor de página do assistente é carregado e inicializada no UDI Wizard Designer, conforme descrito em [revisão assistente página Editor carregar e inicialização](#ReviewWizardPageEditorLoadingInitialization).  

2.  Reveja a IU utilizada para editar o **localização** caixa de combinação nos ficheiros de LocationPageEditor.xaml e LocationPageEditor.xaml.cs conforme descrito em [rever a Interface de utilizador utilizada para configurar a caixa de combinação da localização](#ReviewUserInterfaceUsedtoConfigureLocationComboBox).  

3.  Reveja a IU utilizada para adicionar ou editar as localizações para a lista os ficheiros AddEditLocationView.xaml e AddEditLocationView.xaml.cs conforme descrito em [rever a Interface de utilizador utilizado para modificar a lista de localizações possíveis](#ReviewUserInterfaceUsedtoModifyListofPossibleLocations).  

4.  Rever o código utilizado para gerir as informações de configuração guardadas no ficheiro de configuração do Assistente de UDI conforme descrito em [rever o código utilizado para gerir as informações de configuração](#ReviewCodeUsedtoManageConfigurationInformation).  

#####  <a name="ReviewWizardPageEditorLoadingInitialization"></a>Reveja o carregamento da página Editor de assistente e inicialização  
 Editores de página do assistente personalizado são carregadas conforme exigido pelo UDI Wizard Designer. Os ficheiros de configuração de UDI Wizard Designer são carregados quando é iniciado o UDI Wizard Designer. O UDI Wizard Designer analisa o *install_folder*\Bin\Config pasta (onde *install_folder* é o nome da pasta onde está instalado o MDT) para os ficheiros que tenham uma extensão de ficheiro. config.  

 Durante a configuração do ambiente de desenvolvimento de UDI, copiou o ficheiro de SamplePage.dll.confg para o *install_folder*\Bin\Config pasta. Quando inicia o UDI Wizard Designer, o ficheiro de SamplePage.dll.confg é localizado e carregado.  

 O UDI Wizard Designer utiliza os seguintes atributos do [página](#Page) elemento no ficheiro SamplePage.dll.confg para carregar e inicializar o exemplo de EditorPage:  

-   **DesignerAssembly**. Este atributo determina o nome da DLL seja carregado. Esta DLL necessita de ser colocada na mesma pasta que o ficheiro de UDIDesigner.exe, que é o *install_folder*pasta \Bin (onde *install_folder* é o nome da pasta na qual está instalado o MDT).  

-   **DesignerType**. Este atributo é o nome do tipo Microsoft .NET da classe que contém o controlo de utilizador do WPF.  

-   **Tipo**. Utilize este atributo para configurar o tipo de página de página do assistente personalizado, o que o Assistente de UDI é carregado. O UDI Wizard Designer utiliza este atributo localizar apropriados [página](#Page) elemento no ficheiro de configuração do Assistente de UDI.  

-   **Dll**. Utilize este atributo para configurar o [DLL](#DLL) elemento no ficheiro de configuração do Assistente de UDI, que cria o UDI Wizard Designer.  

-   **Descrição**. Utilize este atributo para fornecer informações sobre o editor de página do assistente. O valor deste atributo é apresentado no **Adicionar nova página** caixa de diálogo no UDI Wizard Designer, que é utilizada para adicionar a página do assistente na "página biblioteca".  

-   **DisplayName**. Utilize este atributo para fornecer o nome da página do assistente personalizada que é apresentado no UDI Wizard Designer. O valor deste atributo é apresentado no **Adicionar nova página** caixa de diálogo no UDI Wizard Designer, que é utilizada para adicionar a página do assistente na "página biblioteca".  

     No exemplo, o tipo do **SamplePage** página do assistente personalizado é **Microsoft.SamplePage.LocationPage**, que é guardada no ficheiro Config.xml. O ficheiro Config.xml reside no *local_folder*\SDK\SamplePage\SamplePage pasta (onde *local_folder* é a pasta que criou no computador de desenvolvimento anteriormente na configuração processo).  

#####  <a name="ReviewUserInterfaceUsedtoConfigureLocationComboBox"></a>Reveja a Interface de utilizador utilizada para configurar a caixa de combinação da localização  
 Quando o editor de página do assistente é carregado e inicializado, o editor de página do Assistente de SampleEditor é carregado quando uma página com um tipo de **Microsoft.SamplePage.LocationPage** é editado. A IU para o editor de página é armazenada no ficheiro LocationPageEditor.xaml.  

 Se examinar a IU no **Design** separador e o código no **XAML** separador, pode ver a relação entre a IU do gráfica e os elementos e atributos no idioma de marcação de aplicação extensível ( XAML).  

 Por exemplo, se que reveja o **controlos: FieldElementControl** elemento no XAML, pode ver como que se relaciona com o esquema da IU correspondente. Utilize o **controlos: FieldElementControl** elemento para definir o [FieldElementControl](#FieldElementControl) controlo.  

 O **enlace** parâmetros no ficheiro XAML vincular os campos no editor de página de exemplo com as informações no ficheiro de configuração do Assistente de UDI. Por exemplo, o seguinte código ties o **valor predefinido** caixa de texto com o [predefinido](#Default) elemento no ficheiro de configuração do Assistente de UDI (Config.xml no exemplo):  

```  
<TextBox Text="{Binding FieldData.DefaultValue,  
 UpdateSourceTrigger=PropertyChanged,  
 Mode=TwoWay}"/>  
```  

 Para obter mais informações, consulte [como: Disponibilizar dados para o enlace em XAML](http://msdn.microsoft.com/library/ms748857.aspx).  

 Utilize o **Views:CollectionTControl.ColumnCollectionView** elemento no XAML para editar a lista de localizações disponíveis na vista de grelha. Utilizar o [CollectionTControl](#CollectionTControl) controlo para apresentar a vista de grelha e vincular a vista de grelha para o [dados](#Data) elemento com o nome **localização** no ficheiro de configuração de UDI.  

#####  <a name="ReviewUserInterfaceUsedtoModifyListofPossibleLocations"></a>Reveja a Interface de utilizador utilizada para modificar a lista de localizações possíveis  
 A IU para modificar a lista de localizações possíveis é composto por:  

-   Um menu sensível ao contexto e botões do friso que lhe permitem adicionar, editar, remover ou alterar a ordem dos itens na lista de localizações, conforme descrito em [revisão Context-sensitive Menu e botões do friso para modificar a lista de localizações](#ReviewContextSensitiveMenuandRibbonButtons)  

-   Uma caixa de diálogo que é iniciada ao selecionar a opção Adicionar ou editar um item na lista de localizações, conforme descrito em [rever a caixa de diálogo para adicionar ou editar localizações](#ReviewDialogBoxforAddingEditingLocations)  

######  <a name="ReviewContextSensitiveMenuandRibbonButtons"></a>Reveja o Menu sensível ao contexto e botões do friso para modificar a lista de localizações  
 Quando faça duplo clique na caixa de listagem que contém a lista de localizações, é apresentado um menu sensível ao contexto. O Friso tem correspondentes botões que permitem-lhe executar as mesmas tarefas. O **vistas: CollectionsTControl** elemento de controlo no ficheiro LocationPageEditor.xaml define os métodos chamados com base na ação tomada e as propriedades que definir da seguinte forma:  

-   **SelectedItem**. Esta propriedade vinculados a dados está ativada quando o utilizador selecciona um item da lista. Esta propriedade está associada à **CurrentLocation** propriedade no modelo de vista que está localizado no ficheiro LocationPageEditorViewModel.cs e utilizado pelo [CollectionTControl](#CollectionTControl) controlo para passar o item selecionado quando editar ou remover um item existente.  

-   **AddItemAction**. Esta ação é executada quando o utilizador clica o **Adicionar Item** opção do menu sensível ao contexto ou clicando nos botões correspondentes no Friso. Há um enlace de dados para uma propriedade no modelo de vista que devolve o **AddLocationAction** objeto. Este objeto é o **AddLocationCallback** método, localizada no ficheiro LocationPageEditorViewModel.cs e apresenta a caixa de diálogo no ficheiro AddEditLocationView.xaml.  

-   **EditItemAction**. Esta ação é executada quando o utilizador clica o **Editar Item** opção no menu sensível ao contexto. Há um enlace de dados para uma propriedade no modelo de vista que devolve o **EditLocationAction** objeto. Este objeto é o **EditLocationCallback** método, localizada no ficheiro LocationPageEditorViewModel.cs e apresenta a caixa de diálogo no ficheiro AddEditLocationView.xaml.  

-   **RemoveAction**. Esta ação é executada quando o utilizador clica o **Remover Item** opção no menu sensível ao contexto. Há um enlace de dados para uma propriedade no modelo de vista que devolve o **RemoveAction** objeto. Este objeto é o **EditLocationCallback** método, localizada no ficheiro LocationPageEditorViewModel.cs e mostra uma mensagem que confirma a eliminação da localização.  

######  <a name="ReviewDialogBoxforAddingEditingLocations"></a>Reveja a caixa de diálogo Adicionar ou editar localizações  
 Se adicionar uma nova localização para a lista de localizações ou editar uma localização existente, é apresentada uma mensagem que consta do ficheiro AddEditLocationView.xaml. É apresentada a mensagem com o [ShowDialogWindow](#ShowDialogWindow) método janela no ficheiro LocationPageEditorViewModel.cs.  

 A IU no ficheiro AddEditLocationView.xaml consiste em:  

-   Com o nome de um intervalo de caixa de diálogo **DialogFrame**, que inclui os seguintes elementos:  

    -   Um título, que configura através do **DialogTitle** atributos da moldura de caixa de diálogo  

    -   Um **OK** botão, que define o estado de retorno como para o **aprovado** propriedade **verdadeiro** (o estado devolvido é verificado **AddLocationCallback** método no ficheiro LocationPageEditorViewModel.cs para determinar se o utilizador clica no **OK**.)  

    -   A **Cancelar** botão, que define o estado de retorno como para o **aprovado** propriedade **falso** (o estado devolvido é verificado **AddLocationCallback**  método no ficheiro LocationPageEditorViewModel.cs para determinar se o utilizador clica no **Cancelar**.)  

-   Um elemento WPF contém:  

    -   Uma etiqueta, que configura através do **conteúdo** atributo  

    -   Uma caixa de texto, o que está vinculada ao [dados](#Data) elemento com o nome **localização** no ficheiro de configuração de UDI (o ficheiro Config.xml no exemplo)  

######  <a name="ReviewCodeUsedtoManageConfigurationInformation"></a>Rever o código utilizado para gerir as informações de configuração  
 As informações de configuração para a página do assistente personalizada são armazenadas no ficheiro de configuração do Assistente de UDI, que é o:  

-   Ficheiro Config.XML no exemplo fornecido com o SDK de UDI (este ficheiro contém apenas as definições de configuração para o exemplo.)  

-   O ficheiro UDIWizard_Config.xml fornecido com o MDT, armazenado no *installation_folder*\Templates\Distribution\Scripts pasta (onde *installation_folder* é a pasta na qual instalou o MDT); Este ficheiro contém as definições de configuração para todas as páginas do assistente incorporadas e fases  

 No exemplo SampleEditor, o **localizações** rotina ajuda a gerir as informações de configuração e está localizada no ficheiro LocationPageEditorViewModel.cs. O **localizações** rotina devolve uma lista das localizações no Assistente de UDI ficheiro de configuração. Especificamente, a lista devolvida contém um item para cada [DataItem](#DataItem) elemento no ficheiro de configuração do Assistente de UDI.  

## <a name="creating-custom-udi-wizard-pages"></a>Criar páginas de assistente UDI personalizado  
 O processo de alto nível para criar páginas de assistente UDI personalizadas é o seguinte:  

1.  Faça uma cópia da solução SamplePage como um ponto de partida.  

2.  Coloque os controlos pretendidos (campos) no formulário.  

3.  Escrever código para executar as tarefas adequadas quando carrega a página do assistente (substituições para o **OnWindowCreated** método), incluindo os seguintes passos:  

    1.  Inicializar o formulário.  

    2.  Memória de leitura variáveis, variáveis de sequência de tarefas, as variáveis de ambiente ou XML de informações de ficheiro (tal como **Setter** propriedades).  

4.  Escrever qualquer código para executar as tarefas adequadas quando é apresentada a página (substituições para o **OnWindowShown** método), incluindo os seguintes passos:  

    1.  Ativar ou desativar os controlos com base nas informações de leitura ao carregar a página no passo 3.  

    2.  Os controlos com base nas informações de leitura quando, em seguida, carregar página no passo 3, tais como o número de controlos de atualização com base nas informações de leitura.  

5.  Escreva qualquer código para executar as tarefas adequadas, enquanto o utilizador interage com a página do assistente.  

6.  Escrever qualquer código para executar as tarefas adequadas quando o utilizador clica **seguinte** no Assistente de UDI (substituições para o **OnNextClicked** método), incluindo os seguintes passos:  

    1.  Atualize quaisquer variáveis de memória, as variáveis de sequência de tarefas, as variáveis de ambiente ou informações de ficheiro XML.  

    2.  Atualize informações da página de resumo (se não for efetuado pelos campos da página).  

7.  Compilar a solução.  

     Certifique-se de que a versão da DLL de criar é a mesma plataforma do processador da instalação do MDT — especificamente, a plataforma de processador para o ambiente de pré-instalação do Windows (Windows PE). O Assistente de UDI pode executar no:  

    -   **O sistema operativo existente no computador de destino**. Pode executar as versões de 32 bits da sua página de assistente em sistemas operativos do Windows de 32 ou 64 bits. No entanto, apenas pode executar as versões de 64 bits da sua página de assistente em sistemas de operativos do Windows de 64 bits.  

    -   **Windows PE no computador de destino**. Windows PE não suporta a execução de aplicações de 32 bits numa versão de 64 bits do Windows PE. Por isso, tem de ter criado uma versão para a página do Assistente para cada arquitetura de processador do Windows PE que pretende utilizar.  

8.  Copie o ficheiro DLL para a página do assistente personalizado para *installation_folder*\Templates\Distribution\Tools\ pasta de plataforma (onde *installation_folder* é a pasta na qual instalou o MDT e *plataforma* é **x86** para a versão de 32 bits ou **x64** destina-se a versão de 64 bits).  

9. Conclua os passos para criação personalizada página editor.  

## <a name="creating-custom-wizard-page-editors"></a>Criar editores de página do assistente personalizado  
 O processo de alto nível para criar editores de página do assistente UDI personalizado é o seguinte:  

1.  Faça uma cópia da solução SampleEditor como um ponto de partida.  

2.  Crie a página principal da IU do editor num ficheiro primeiro.  

3.  Adicionar as instâncias do [FieldElementControl](#FieldElementControl) controlar conforme exigido pelo página do assistente, ser configurado (se necessário).  

4.  Adicionar as instâncias do [SetterControl](#SetterControl) controlar conforme exigido pelo página do assistente, ser configurado (se necessário).  

5.  Adicionar as instâncias do [CollectionTControl](#CollectionTControl) controlar conforme exigido pelo página do assistente, ser configurado (se necessário).  

6.  Adicionar o [IDataService](#IDataService) interface.  

7.  Escreva o código adequado para atualizar o ficheiro de configuração do Assistente de UDI com base nas definições de configuração para ser configurado utilizando o editor de página do assistente personalizado.  

8.  Criar subordinados caixas de diálogo num ficheiro primeiro e chamá-los a partir da página principal editor utilizando o [IMessageBoxService](#IMessageBoxService) interface conforme exigido pelo página do assistente, ser configurado.  

9. Adicione que as interfaces adequadas ao Friso de estruturador do Assistente de UDI com base nos requisitos de página do assistente, ser configurado.  

10. Compilar a solução.  

    > [!NOTE]
    >  Certifique-se de que a versão da DLL de criar é a mesma plataforma do processador da instalação do MDT. Por exemplo, se instalar a versão de 64 bits do MDT, em seguida, crie uma versão de 64 bits do seu editor de página personalizada.  

11. Crie um ficheiro de configuração ao carregar os dll necessários e mapear a página do Assistente de UDI Wizard Designer editor com a página do assistente correspondente (o ficheiro SamplePage.dll.config no exemplo).  

     Para obter mais informações sobre os elementos necessários para efetuar o mapeamento entre a página do assistente e o editor de página do assistente, consulte o [DesignerMappings](#DesignerMappings) elemento, elementos subordinados e atributos correspondentes.  

12. Copie o ficheiro de configuração de UDI Wizard Designer que criou no passo anterior para o *installation_folder*\Bin\Config pasta (onde *installation_folder* é a pasta onde instalou Versão do MDT).  

13. Copie o ficheiro DLL para o seu editor de página do assistente personalizado para o *installation_folder*pasta \Bin (onde *installation_folder* é a pasta na qual instalou o MDT).  

##  <a name="CreatingCustomUDITasks"></a>Criar tarefas UDI personalizado  
 *Tarefas UDI* são DLLs escritos em C++, que implementa o [ITask interface](#ITaskinterface). Registe a DLL com a biblioteca de tarefas de UDI Wizard Designer através da criação de um ficheiro de configuração de UDI Wizard Designer (ficheiro. config) e colocá-lo no *installation_folder*\Bin\Config pasta (onde *installation_ pasta* é a pasta na qual instalou o MDT).  

> [!NOTE]
>  Pode criar um DLL que contém as páginas do assistente, tarefas e validações dentro do mesmo ficheiro. dll. Também pode criar um único UDI Wizard Designer ficheiro de configuração (. config) que contém as definições de configuração para as páginas do assistente, tarefas e validações na DLL.  

 **Para criar tarefas UDI personalizadas**  

1.  Código de escrita que implementa o [ITask Interface](#ITaskinterface) e os métodos seguintes:  

    -   [Init](#Init). Este método é chamado para inicializar a tarefa.  

    -   [Executar](#Execute). Este método é denominado para executar a tarefa.  

2.  Escreva código que regista a fábrica de classe de tarefas personalizada com o registo de fábrica.  

3.  Compilar a solução para a sua tarefa personalizada.  

    > [!NOTE]
    >  Certifique-se de que a versão da DLL de criar é a mesma plataforma do processador da instalação do MDT. Por exemplo, se instalar a versão de 64 bits do MDT, em seguida, crie uma versão de 64 bits do seu tarefas UDI personalizada.  

4.  Criar um [tarefas](#Task) elemento sob o [TaskLibrary](#TaskLibrary) elemento no ficheiro de configuração de UDI Wizard Designer semelhante para o excerpt seguinte:  

    ```  
    <Task DLL="OSDRefreshWizard.dll" Description="Discovers supported applications for install." Type="Microsoft.OSDRefresh.AppDiscoveryTask" Name="Application Discovery">  
       <TaskItem Type="Setter" Name="Status Bitmap">  
          <Param Name="BitmapFilename"/>  
       </TaskItem>  
       <TaskItem Type="Setter" Name="Log File">  
          <Param Name="log"/>  
       </TaskItem>  
       <TaskItem Type="Setter" Name="Write Configuration File">  
          <Param Name="writecfg"/>  
       </TaskItem>  
       <TaskItem Type="Setter" Name="Read Configuration File">  
          <Param Name="readcfg"/>  
       </TaskItem>  
    </Task>  
    ```  

    > [!NOTE]
    >  Todos os [tarefas](#Task) elementos devem incluir o **BitmapFilename** parâmetro. Especifique todos os outros parâmetros como requer que a tarefa. Por exemplo, no excerpt anterior, o **registo** parâmetro é utilizado para especificar um parâmetro para a localização do ficheiro de registo.  

5.  Copie o ficheiro de configuração de UDI Wizard Designer criado no passo anterior para o *installation_folder*\Bin\Config pasta (onde *installation_folder* é a pasta na qual instalou o MDT).  

6.  Copie o ficheiro DLL para a sua tarefa personalizada para o *installation_folder*\Templates\Distribution\Tools\ pasta de plataforma (onde *installation_folder* é a pasta na qual instalou o MDT e *plataforma* é **x86** para a versão de 32 bits ou **x64** destina-se a versão de 64 bits).  

##  <a name="CreatingCustomUDIValidators"></a>Criar validações UDI personalizado  
 *Validações UDI* são DLLs escritos em C++, que implementa o **IValidator** interface. Registe a DLL com a biblioteca de validação de UDI Wizard Designer através da criação de um ficheiro de configuração de UDI Wizard Designer (ficheiro. config) e colocá-lo no *installation_folder*\Bin\Config pasta (onde  *installation_folder* é a pasta na qual instalou o MDT).  

 **Para criar validações UDI personalizadas**  

1.  Escrever código que cria uma subclasse do **BaseValidator** classe e implementa os seguintes métodos:  

    -   **Init (IControl \*pControl, IWizardPageContainer \*pContainer, IStringProperties \*pProperties)**. As chamadas de controlador de forma a **Init** membro ao inicializar o validador. Este método tem de chamar o **Init** método para o **BaseValidator** classe. Normalmente, é lida quaisquer propriedades a definir para o validador no Assistente de UDI ficheiro de configuração. Por exemplo, o **InvalidCharactersValidator** validador obtém o valor da **InvalidChars** propriedade através deste método.  

    -   **IsValid**. O controlador de formulário chama este método para ver se o controlo contém texto válido. Segue-se um exemplo do **IsValid** método para um validador que valida que o campo não está vazio:  

        ```  
        BOOL IsValid(LPBSTR pMessage)  
        {  
            __super::IsValid(pMessage);  

            _bstr_t text;  
            m_pText->GetText(text.GetAddress());  
            return (text.length() > 0);  
        }  
        ```  

    -   **Init (IControl \*pControl, mensagem LPCTSTR)**. O controlador de formulário chama este membro para cada batimento de tecla e outros eventos, para que a validação do pode validar o conteúdo do controlo e mensagens atualizadas na parte inferior da página do assistente (ou limpar estes).  

     Normalmente, estes são os métodos de apenas terá de substituir. No entanto, consoante o validador, poderá ter de substituição de outros métodos de subclasse do **BaseValidator** classe que cria. Para obter mais informações sobre estes outros métodos, consulte o **BaseValidator** classe.  

2.  Escreva código que regista a classe de tarefas personalizada com a fábrica de registo.  

3.  Compilar a solução para a sua tarefa personalizada.  

    > [!NOTE]
    >  Certifique-se de que a versão da DLL de criar é a mesma plataforma do processador da instalação do MDT. Por exemplo, se instalar a versão de 64 bits do MDT, em seguida, crie uma versão de 64 bits do seu tarefas UDI personalizada.  

4.  Criar um [validador](#Validator) elemento sob o **ValidatorLibrary** elemento no ficheiro de configuração de UDI Wizard Designer semelhante para o excerpt seguinte:  

    ```  
    <Validator   
    <Validator DLL="" Description="Must follow a pre-defined pattern" Type="Microsoft.Wizard.Validation.RegEx" Name="NamedPattern">  
       <Param Description="Enter the message you want displayed when the text in this field doesn't match the pattern:" Name="Message" DisplayName="Message"/>  
       <Param Description="The name of a pre-defined regular expression pattern. Must be Username, ComputerName, or Workgroup" Name="NamedPattern" DisplayName="Named Pattern"/>  
    </Validator>  
    ```  

    > [!WARNING]
    >  Todos os [validador](#Validator) elementos devem incluir o **mensagem** parâmetro. Especifique todos os outros parâmetros conforme necessário ao validador. Por exemplo, no excerpt anterior, o **NamedPattern** parâmetro é utilizado para especificar um parâmetro para o nome de um padrão de expressão regular predefinidas.  

5.  Copie o ficheiro de configuração de UDI Wizard Designer criado no passo anterior para o *installation_folder*\Bin\Config pasta (onde *installation_folder* é a pasta na qual instalou o MDT).  

6.  Copie o ficheiro DLL para a sua tarefa personalizada para o *installation_folder*\Templates\Distribution\Tools\ pasta de plataforma (onde *installation_folder* é a pasta na qual instalou o MDT e *plataforma* é **x86** para a versão de 32 bits ou **x64** destina-se a versão de 64 bits).  

## <a name="udi-wizard-reference"></a>Referência do Assistente de UDI  

### <a name="wizard-page-components"></a>Componentes de página do Assistente  
 Pode utilizar qualquer um dos vários componentes prebuilt para criar as suas páginas personalizadas.  

#### <a name="creating-component-instances"></a>Criar instâncias do componente  
 O Assistente de UDI utiliza fábricas de classe para criar novas instâncias de objetos para si. Estes factories estão registados com um registo de fábrica, a utilização de uma cadeia como a chave para a fábrica. Por exemplo, o **WmiRepository** componente é identificado pela cadeia de caracteres "Microsoft.Wizard.WmiRepository", que está disponível no ficheiro de cabeçalho IWmiRepository como **ID_WmiRepository**.  

 Partindo do princípio que tem a escrita na sua página como uma subclasse de **WizardPageImpl**, pode criar uma nova instância de um **WmiRepoistory** como esta:  

```  
PWmiRepository pWmi;  
CreateInstance(Container(), ID_WmiRepository, &pWmi);  
```  

 O **CreateInstance** função é uma função de modelo de tipo seguro para a criação de novas instâncias dos componentes. **PWmiRepository** . existe um ponteiro inteligente, pelo que processa a referência de contagem por si.  

#### <a name="creatable-components"></a>Componentes criados  
 Não há um conjunto de componentes pode registar no registo. O primeiro conjunto de componentes é registado sempre, porque o ficheiro executável principal do Assistente de UDI fornece-lo. Os outros dois conjuntos de componentes são fornecidos na DLLs "opcionais". Estes componentes estar disponível, a DLL tem de estar listada no **DLLs** secção do ficheiro XML. config. O código não precisa de saber qual executável contém um componente específico.  

 A lista de IDs de componente de componentes (o nome do componente é o mesmo que o ID, mas sem iniciais *ID_*) registado com a fábrica de registo (definido no OSDSetupWizard) é apresentado na tabela 3.  

### <a name="table-3-component-ids"></a>Tabela 3. IDs de componente  

|**ID**|**Descrição**|  
|-|-|  
|ID_ACPowerTask|(ITask, IWizardComponent) Uma tarefa de verificação prévia que assegura que o seu computador não está em execução com bateria individualmente|  
|ID_AppDiscoveryTask|(ITask, IWizardComponent) Uma tarefa especializada para detetar os itens de software instalou no seu computador|  
|**ID_BackgroundTask**|(**IBackgroundTask**, **IWizardComponent**) pode ser utilizada para executar uma tarefa noutro thread|  
|**ID_CopyFilesTask**|(**ITask**, **IWizardComponent**) uma tarefa ao copiar um ou mais ficheiros|  
|**ID_FormController**|(**IFormController**) será mais como não tem de criar uma instância de si próprio, como a página recebe a sua própria instância|  
|**ID_InvalidCharactersValidator**|(**IValidator**) assegura que nenhum campo de texto contém carateres de uma lista fornecida ao validador|  
|**ID_Logger**|(**ILogger**) será mais como não tem de criar uma instância de si próprio, como a página recebe um ponteiro para a instância partilhada|  
|**ID_NonEmptyValidator**|(**IValidator**) um validador que assegura que nenhum campo está vazio|  
|**ID_PasswordValidator**|(**IValidator**) um validador que assegura que não existem campos de dois texto têm os mesmos conteúdos|  
|**ID_Regex**|(**IRegEx**) avalia as expressões regulares, à procura de correspondências|  
|**ID_RegExValidator**|(**IValidator**) um validador que valida contra uma expressão regular ou um padrão conhecido|  
|**ID_SimpleStringProperties**|(**IStringProperties**, **ISimpleStringProperties**) fornece uma forma simples para enviar as propriedades para tarefas sem utilizar XML|  
|**ID_ShellExecuteTask**|(**ITask**, **IWizardComponent**) executar um programa externo|  
|**ID_SummaryBag**|(**ISummaryBag**) disponível indiretamente a partir da sua página através do método do formulário|  
|**ID_TaskManager**|(**ITaskManager**, **IBackgroundCallback**, **IWizardComponent**) gere a executar um conjunto de tarefas e a IU|  
|**ID_WmiRepository**|(**IWmiRepository**, **IWizardComponent**) permite-lhe executar consultas Windows Management Instrumentation (WMI)|  
|**ID_IXmlDocument**|(**IXmlDocument**) fornece uma fachada para ler e escrever documentos XML|  

 O OSDRefreshWizard.dll definido, páginas partilhadas e outros componentes de controlo são apresentados na tabela 4 e 5 de tabela.  

### <a name="table-4-directory-controls"></a>Tabela 4. Controlos de diretório  

|**ID**|**Descrição**|  
|-|-|  
|**ID_Directory**|(**IDirectory**) uma fachada para obter informações de diretório do sistema de ficheiros|  

### <a name="table-5-defined-sharedpagesdll"></a>Tabela 5. SharedPages.dll definido  

|**ID**|**Descrição**|  
|-|-|  
|**ID_ADHelper**|(**IADHelper**) fornece uma fachada de um conjunto limitado de funcionalidades nos serviços de domínio do Active Directory® (AD DS)|  
|**ID_CpuInfo**|(**ICpuInfo**) determina se a CPU é de 32 ou 64 bits|  
|**ID_DomainJoinValidator**|(**IDomainJoinValidator**) tem alguns métodos de a verificar se um conjunto de credenciais está autorizado a aderir a um domínio|  
|**ID_DriveList**|(**IDriveList**, **IBindableList**, **IWizardComponent**) utiliza o WMI para obter uma lista de unidades do computador|  
|**ID_WiredNetworkTask**|(**ITask**) que verifica se está ligado à rede com um hard-wired (em vez de sem fios) tarefas de um adaptador de rede|  

#### <a name="control-components"></a>Componentes de controlo  
 Interagir com os controlos na sua página através de **GetControlWrapper** função de modelo, que fornece acesso a um dos tipos de componentes listados na tabela 6.  

### <a name="table-6-components"></a>Tabela 6. Componentes  

|**Tipos de controlo de caixa de diálogo**|**Descrição**|  
|-|-|  
|**CONTROL_CHECK_BOX**|(**ICheckBox**) uma fachada para trabalhar com os controlos de caixa de verificação|  
|**CONTROL_COMBO_BOX**|(**IComboBox**) uma fachada para controlos de caixa de combinação|  
|**CONTROL_GENERIC**|(**IControl**) permite-lhe trabalhar com a maioria dos tipos de controlos para ativar de controlo e estado visível|  
|**CONTROL_LIST_VIEW**|(**IListView**) uma fachada fornecer acesso às funcionalidades de um controlo de vista de lista|  
|**CONTROL_PROGRESS_BAR**|(**IProgressBar**) uma fachada para trabalhar com a posição de um controlo de barra de progresso|  
|**CONTROL_RADIO_BUTTON**|(**IRadioButton**) uma fachada para trabalhar com os controlos de botão de opção|  
|**CONTROL_STATIC_TEXT**|(**IStaticText**) uma fachada que fornece a permissão de leitura/escrita para o texto de um controlo, tais como uma caixa de texto ou etiqueta|  
|**CONTROL_TREE_VIEW**|(**ItreeView**) uma fachada para trabalhar com um controlo de vista de árvore|  

#### <a name="image-list-component"></a>Componente da lista de imagem  
 Este componente é uma fachada para um **ImageList** controlo na página. Criar uma lista de imagem através do **IListView** ou **ITreeView** interface.  

#### <a name="formcontroller-component"></a>Componente de FormController  
 O assistente cria este componente para si e passa-a para a página. Aceder a partir da sua página utilizando a **formulário** método, que o **WizardPageImpl** base classe implementa.  

#### <a name="invalidcharactervalidator-component"></a>Componente de InvalidCharacterValidator  
 Este é um tipo de validação do que pode incluir numa página. O ID é **ID_InvalidCharactersValidator** (definido no IValidator.h), que tem um valor de texto de "Microsoft.Wizard.Validation.InvalidChars."  

 Este validador procura para uma propriedade de único (um **Setter** elemento no ficheiro. config) chamado **InvalidChars**, que é uma lista de carateres que não são permitidos. Verifica os carateres na caixa de texto; Se o texto contém caracteres desta lista, o componente de relatórios de falha.  

#### <a name="nonemptyvalidator-component"></a>Componente de NonEmptyValidator  
 Este é um tipo de validação do que pode incluir numa página. O ID é **ID_NonEmptyValidator** (definido no IValidator.h), que tem um valor de texto de "Microsoft.Wizard.Validation.NonEmpty."  

 Este validador relatórios falha se a caixa de texto (ou qualquer outro controlo que suporte **IStaticText**) tem um valor de cadeia vazia.  

#### <a name="passwordvalidator-component"></a>Componente de PasswordValidator  
 Este é um tipo de validação do que pode incluir numa página. O ID é **ID_PasswordValidator** (definido no IValidator.h), que tem um valor de texto de "Microsoft.Wizard.Validation.Password."  

 Este validador funciona com dois controlos de texto diferente (controla que suportam **IStaticText**) e relatórios falha se não contêm os mesmos valores. Por outras palavras, falhar se o **palavra-passe** e **Confirmar palavra-passe** não correspondem às caixas de texto.  

 Uma vez que este validador requer dois controlos, necessita de configuração mais do que outras validações. O programa de configuração poderá ter um aspeto semelhante ao seguinte:  

```  
Form()->AddToGroup(IDC_EDIT_PASSWORD, IDC_EDIT_PASSWORD2);  
PValidator pValidator;  
Form()->AddValidator(IDC_EDIT_PASSWORD, ID_PasswordValidator, pMessage, &pValidator);  
PStaticText pPassword2;  
GetControlWrapper(View(), IDC_EDIT_PASSWORD2, CONTROL_STATIC_TEXT, &pPassword2);  
pValidator->SetProperty(0, pPassword2);  
```  

 Em primeiro lugar, é possível definir o **Confirmar palavra-passe** controlo como "subordinado" do **palavra-passe** controlo. Dessa forma, se o controlador de formulário desativa o **palavra-passe** controlo, irá desativar também o **Confirmar palavra-passe** controlo. Em seguida, adicione uma validação de palavra-passe para o formulário. Por fim, forneça a validação da palavra-passe com a interface para o **Confirmar palavra-passe** controlo.  

 Devido ao requisito de dois controlos, tem de utilizar o código para configurar este validador em vez do ficheiro XML. config.  

#### <a name="regexvalidator-component"></a>Componente de RegExValidator  
 Este é um tipo de validação do que pode incluir numa página. O ID é **ID_RegExValidator** (definido no IValidator.h), que tem um valor de texto de "Microsoft.Wizard.Validation.RegEx."  

 Este validador compara o conteúdo de um controlo de texto (um que suporta **IStaticText**) para uma expressão regular e falha se o texto não corresponde à expressão regular.  

 Em alternativa, pode utilizar este validador com um padrão com o nome predefinido. Para utilizar uma expressão regular, o XML tem de conter uma propriedade setter denominada **padrão**. Se pretender utilizar um padrão com nome em vez disso, utilize um setter chamado **NamedPattern** definido como um dos valores existentes na tabela 7.  

### <a name="table-7-named-pattern-setters"></a>A tabela 7. Setters denominado padrão  

|**Padrão**|**Descrição**|  
|-|-|  
|Nome de Utilizador|Verifica se o texto é um do formato domínio \ utilizador ouuser@domain|  
|ComputerName|O nome tem de estar entre 1 e 15 carateres e não pode incluir um conjunto de carateres (tais como: e?)|  
|Grupo de trabalho|O nome tem de estar entre 1 e 15 carateres e não pode conter um conjunto de carateres (por exemplo, =, +, e?)|  

#### <a name="factoryregistry-component"></a>Componente de FactoryRegistry  
 Este componente mantém um registo dos todas as fábricas de classe e serviços. Implementa o **IFactoryRegistry** interface e está disponível indiretamente através da página **contentor** método. Além disso, o registo carrega DLLs de extensão. Depois de medida que é carregado um DLL, o registo de procura para uma função exportada chamada **RegisterFactories**. Tem de implementar esta função e na mesma registar as fábricas de classe para as páginas, tarefas, validações (e quaisquer fábricas de classe que pretende registar). Eis um exemplo do projeto de exemplo:  

```  
extern "C" __declspec(dllexport) void RegisterFactories(IFactoryRegistry *factories)  
{  
Register<LocationPageFactory>(ID_LocationPage, factories);  
}  
```  

#### <a name="logger-component"></a>Componente de registo  
 Este componente está disponível para a página através de **registador** método (implementado por **WizardPageImpl**). Utilize este método para escrever entradas de ficheiro de registo. O conteúdo do ficheiro de registo é úteis para diagnosticar problemas que os utilizadores poderão ter de executar o Assistente de UDI.  

#### <a name="propertybag-component"></a>Componente de PropertyBag  
 O *matriz de propriedades* é um contentor para variáveis de memória. Está disponível a partir da sua página utilizando **Container() -> Properties()**. Variáveis de memória são úteis para transmitir dados temporários entre páginas diferentes.  

#### <a name="tsvariablebag-and-tsrepository-components"></a>TSVariableBag e TSRepository componentes  
 O **TSVariableBag** componente permite-lhe ler e escrever as variáveis de sequência de tarefas. Mantém os valores na memória até a utilizador clica em **concluir** (por predefinição). Pode aceder a **TSVariable** matriz através da página **TSVariables** método (implementado pelo **WizardPageImpl** classe base). Estes componentes registar todas as leituras e escritas de variáveis de sequência de tarefas.  

#### <a name="wmirepository-component"></a>Componente de WmiRepository  
 Este componente fornece uma fachada para trabalhar com consultas do WMI. Pode chamar o **CreateInstance** função auxiliar com **ID_WmiRepository** para obter uma instância deste componente, que suporta o **IWmiRepository** interface. Este componente devolve registos de resultado através de **IWmiIterator** interface.  

###  <a name="WizardPageHelperClasses"></a>Classes de programa auxiliar de página do Assistente  
 Pode criar páginas do assistente UDI personalizadas a utilizar classes de programa auxiliar incorporada fornecidas com o SDK de UDI. Tabela 8 apresenta as classes de programa auxiliar que pode utilizar para criar páginas de assistente personalizado.  

### <a name="table-8-helper-classes"></a>Tabela 8. Classes de programa auxiliar  

|**Classe de programa auxiliar**|**Descrição**|  
|-|-|  
|[Classe de ClassFactoryImpl](#ClassFactoryImplClass)|Esta é uma classe base úteis para criar uma fábrica de classe, em seguida, pode registar com o registo de fábrica.|  
|[Modelo classe de interface](#InterfaceTemplateClass)|Utilize esta classe de modelo quando pretender criar um componente que implementa mais de uma interface.|  
|[Classe de programa auxiliar de caminho](#PathHelperClass)|Esta classe fornece operações comuns do diretório do ficheiro.|  
|[Classe de modelo do ponteiro](#PointerTemplateClass)|Esta classe fornece referência contando para a gestão de duração no componentes COM. É importante libertar interfaces quando tiver terminado com os mesmos. Esta classe de modelo processa a duração automaticamente.|  
|[Classe de PUnknown](#PUnkownClass)|Esta classe é um ponteiro inteligente especificamente para a interface IUnknown. Para todas as outras interfaces, utilize a classe de modelo do ponteiro.|  
|[Classe de programa auxiliar de StringUtil](#StringUtilHelperClass)|Esta classe fornece métodos de programa auxiliar que torna mais fácil trabalhar com cadeias.|  
|[Classe de modelo subInterface](#SubInterfaceTemplateClass)|Esta classe base torna mais fácil de implementar um componente que suporta uma interface que próprio herda de outra interface.|  
|[Classe de modelo UnknownImpl](#UnknownImplTemplateClass)|Esta classe processa a maioria dos detalhes da criação de um componente COM.|  
|[Classe de modelo WizardComponent](#WizardComponentTemplateClass)|Esta classe base é utilizada para criar os componentes que precisam de acesso para os serviços do assistente, tais como a criação do componente e registo.|  
|[Classe de modelo WizardPageImpl](#WizardPageImplTemplateClass)|Esta classe base deve ser utilizado como a classe base para todas as páginas de assistente personalizado|  

####  <a name="ClassFactoryImplClass"></a>Classe de ClassFactoryImpl  
 Esta é uma classe base úteis para criar uma fábrica de classe, em seguida, pode registar com o registo de fábrica.  

 Segue-se um excerpt do ficheiro LocationPage.h no projeto de exemplo para definir o **ClassFactoryImpl** classe.  

```  
#pragma once  

#include "ClassFactoryImpl.h"  

class LocationPageFactory :public ClassFactoryImpl  
{  
protected:  
    IUnknown *CreateNewInstance();  
};  
```  

 Segue-se um excerpt do ficheiro LocationPage.cpp na página do Assistente de exemplo utilizado para definir a fábrica de classe para a página.  

```  
IUnknown *LocationPageFactory::CreateNewInstance()  
{  
    return static_cast<IWizardPage *>(new LocationPage);  
}  
```  

####  <a name="InterfaceTemplateClass"></a>Modelo classe de interface  
 Utilizar esta classe de modelo quando pretender criar um componente que implementa mais de uma interface — por exemplo:  

```  
classLocationPage :public Interface<IFieldCallback, WizardPageImpl<IDD_LOCATION_PAGE>>  
```  

 Este código cria uma cadeia de classe base que suporta **IFieldCalback** e as interfaces que **WizardPageImpl** suporta (que acontece ser **IWizardPage**).  

####  <a name="PathHelperClass"></a>Classe de programa auxiliar de caminho  
 Esta classe fornece operações comuns do diretório do ficheiro:  

```  
static inline std::wstring GetModulePath(HINSTANCE hModule)  
```  

 Também devolve o caminho completo para o ficheiro .exe ou. dll com o identificador de instância que fornece a este método:  

```  
static inline std::wstring GetModuleFilename(HINSTANCE hModule)  
```  

 A classe devolve o nome de ficheiro e caminho completo do ficheiro. dll. .exe e com o identificador de instância que fornece a este método:  

```  
static inline std::wstring GetDirecotryName(LPCWSTR fullName)  
```  

 . . . apenas o caminho ou ao stripping o nome do ficheiro:  

```  
static inline std::wstring GetFileName(LPCWSTR fullName)  
```  

 Tendo em conta um caminho com um nome de ficheiro, a classe de programa auxiliar de caminho devolve apenas o nome do ficheiro:  

```  
static inline std::wstring Combine(LPCWSTR path, LPCWSTR name)  
```  

 Por fim, a classe devolve uma cadeia nova, que é o caminho combinado e ficheiro nome (ou outro caminho).  

####  <a name="PointerTemplateClass"></a>Classe de modelo do ponteiro  
 Esta classe está definida no Pointer.h. Porque é utilizado por componentes COM referência contando para gestão de duração, é importante que versão sempre interfaces quando tiver terminado com os mesmos. A Microsoft fornece uma classe de modelo que processa a duração automaticamente. Por exemplo, se pretender que um ponteiro inteligente para uma interface XML, pode escrever algo semelhante ao seguinte:  

```  
Pointer<IXMLDOMNode> pNewChild  
pXmlDom->CreateNode(NODE_ELEMENT, L"MyElement", L"", &pNewChild);  
```  

 A primeira linha define o ponteiro inteligente. A segunda linha mostra a obter um ponteiro inteligente através de outra chamada. O  **&**  operador sempre disponibiliza uma interface existente se contém um e devolve o endereço para o ponteiro interno. Depois de ter obtido um ponteiro como esta, o **ponteiro** instância chamadas **versão** para si quando a variável passa fora do âmbito. A Microsoft recomenda que utilize inteligentes ponteiros em vez de chamar **AddRef** e **versão** manualmente.  

 Além disso, o **ponteiro** smart chamadas de classe do ponteiro **QueryInterface** obter outras interfaces para si. Por exemplo, quando o registo de fábrica cria uma nova instância de um componente, tem o código seguinte:  

```  
PWizardComponent pComp = pUnknown;  
if (pComp != nullptr)  
    pComp->SetContainer(m_pContainer);  
```  

 As chamadas de linha primeiro **QueryInterface** bastidores para pedir a **IWizardComponent** interface. O apontador inteligente resultante será igual **nullptr** se o componente não suporta esse interface.  

####  <a name="PUnkownClass"></a>Classe de PUnknown  
 Esta classe é um ponteiro inteligente especificamente para o **IUnknown** interface. Para todas as outras interfaces, utilize o **ponteiro** classe de modelo.  

####  <a name="StringUtilHelperClass"></a>Classe de programa auxiliar de StringUtil  
 Esta classe está definida no Utilities.h e fornece métodos de programa auxiliar que torna mais fácil trabalhar com cadeias de:  

```  
static inline int CompareIgnore(LPCWSTR first, LPCWSTR second)  
```  

 Este método compara duas cadeias ao ignorando maiúsculas e minúsculas (consulte a tabela 9).  

### <a name="table-9-stringutil-helper-class"></a>Tabela 9. Classe de programa auxiliar de StringUtil  

|**Devolve**|**Descrição**|  
|-|-|  
|**0**|Corresponde a cadeias, ignorando maiúsculas e minúsculas|  
|**< 0**|Primeiro < segundo|  
|**> 0**|Primeiro > segundo|  

 Eis um exemplo:  

```  
static inline std::wstring Format(LPCWSTR input, int index, LPCWSTR value)  
static inline std::wstring Format(LPCWSTR input, int index, DWORD value)  
```  

 Estes métodos são um pouco, como o Microsoft .NET **formato** métodos na medida em que os parâmetros estão no formato **{0}**. No entanto, se não efetuar qualquer formatação da entrada — apenas substituição:  

```  
static inline std::wstring Printf(std::wstring format, I val)  
static inline std::wstring Printf(std::wstring format, I val1, J val2)  
static inline std::wstring Printf(std::wstring format, I val1, J val2, K val3)  
static inline std::wstring Printf(std::wstring format, I val1, J val2, K val3, L val4)  
```  

 Estes são wrappers à volta a **StringCchPrintf** esse devolver um **wstring** para que não tenha de alocar memória para cadeias ou memórias intermédias por si.  

####  <a name="SubInterfaceTemplateClass"></a>Classe de modelo subInterface  
 Esta classe base torna mais fácil de implementar um componente que suporta uma interface que próprio herda de outra interface. Por exemplo, o **ICheckBox** interface herda **IControl**. Eis como esta classe é utilizada para definir o **CheckBoxWrapper**:  

```  
classCheckBoxWrapper :public SubInterface<IControl, UnknownImpl<ICheckBox> >  
```  

 A interface de base é o primeiro parâmetro, enquanto a interface derivada é o segundo parâmetro.  

####  <a name="UnknownImplTemplateClass"></a>Classe de modelo UnknownImpl  
 Esta classe está definida no UnknownImpl.h e processa a maioria dos detalhes da criação de um componente COM. Eis um exemplo de como pretende utilizar esta classe base:  

```  
classDirectory :public UnknownImpl<IDirectory>  
```  

 Este código define uma classe que suporta o **IDirectory** interface.  

####  <a name="WizardComponentTemplateClass"></a>Classe de modelo WizardComponent  
 Esta classe está definida no IWizardComponent.h e é uma classe base útil para a criação de componentes que precisam de acesso para os serviços do assistente, tais como a criação do componente e registo.  

 Por exemplo, eis como o **CopyFilesTask** componente está definido:  

```  
classCopyFilesTask :public WizardComponent<ITask>  
{  
    ...  
```  

 O parâmetro para esta classe de modelo é o que pretende utilizar para o seu componente, que, no caso de tarefas, é a interface "principal" **ITask**. Utilizar **WizardComponent** significa que o seu componente suporta a interface de ambos os seu forneça (**ITask** neste exemplo) e **IWizardComponent**.  

 Sempre que utilizar o registo de fábrica de classe para criar um novo componente, o registo chama o componente **IWizardComponent -> SetContainer** método para fornecer o acesso do componente para os serviços do assistente.  

####  <a name="WizardPageImplTemplateClass"></a>Classe de modelo WizardPageImpl  
 Utilizar esta classe como a classe base para as suas páginas personalizadas — por exemplo:  

```  
class LocationPage :public WizardPageImpl<IDD_LOCATION_PAGE>  
```  

 O parâmetro é o ID de recurso para o modelo de caixa de diálogo.  

###  <a name="WizardPageInterfaces"></a>Interfaces de página do Assistente  
 O Assistente de UDI utiliza interfaces para controlos de diferentes na sua página de acesso. Na página, utilize o **GetControlWrapper** função para obter um wrapper do controlo. Eis um exemplo:  

```  
PStaticText pFormat;  
GetControlWrapper(View(), IDC_CHECK_PARTITION, CONTROL_STATIC_TEXT, &pFormat);  
```  

 Aqui, **PStaticText** um ponteiro inteligente para o **IStaticText** interface. Ponteiros inteligentes chamar automaticamente o COM **Release()** método quando avançam fora do âmbito ou transmita o endereço de uma variável (como **& pFormat**) para um método.  

#### <a name="iadhelper-interface"></a>IADHelper Interface  

```  
__interfaceIADHelper : IUnknown  
{  
    HRESULT Init(ILogger *pLogger);  
    HRESULT ValidLogon(LPCTSTR userName, LPCTSTR password, LPCTSTR domain);  
    HRESULT HasAccess(LPCTSTR username, LPCTSTR password, LPCTSTR domain, LPCTSTR computerName, LPCTSTR accountDomain);  
};  

```  

##### <a name="hresult-initilogger-plogger"></a>HRESULT Init(ILogger \*pLogger)  
 Inicializar este componente, passou-a para o registo para que possa registar informações.  

##### <a name="hresultvalidlogonlpctstr-username-lpctstr-password-lpctstr-domain"></a>HRESULTValidLogon (LPCTSTR nome de utilizador, palavra-passe LPCTSTR, domínio LPCTSTR)  
 Este método verifica se a um conjunto de credenciais é válido, conforme mostrado na tabela 10.  

### <a name="table-10-hresultvalidlogon"></a>Tabela 10. HResultValidLogon  

|**HResult**|**Descrição**|  
|-|-|  
|S_OK|As credenciais são válidas|  
|S_FALSE|As credenciais não são válidas|  
|E_FAIL|Não foi possível localizar o controlador de domínio; Verifique os registos para obter detalhes|  

##### <a name="hresult-hasaccesslpctstr-username-lpctstr-password-lpctstr-domain-lpctstr-computername-lpctstr-accountdomain"></a>HRESULT HasAccess(LPCTSTR username, LPCTSTR password, LPCTSTR domain, LPCTSTR computerName, LPCTSTR accountDomain)  
 Este método verifica se um conjunto de credenciais tem acesso de leitura/escrita para o objeto de computador no AD DS, conforme mostrado na tabela 11.  

### <a name="table-11-hresult-hasaccess"></a>Tabela 11. HResult HasAccess  

|**HRESULT**|**Descrição**|  
|-|-|  
|S_OK|O utilizador tem acesso|  
|E_FAIL|O utilizador não tem acesso. Verifique o ficheiro de registo para obter informações adicionais.|  

#### <a name="ibackgroundtask-interface"></a>IBackgroundTask Interface  

```  
__interface IBackgroundTask : IUnknown  
{  
    HRESULT Init(ITask *pTask, int id, IBackgroundCallback *pCallback);  
    void Start(void);  
    BOOL Running(void);  
    HRESULT Wait(DWORD waitMilliseconds);  
    HRESULT Terminate(DWORD exitCode);  
    HRESULT GetExitCode(LPDWORD pCode, HRESULT *pHresult);  
    HRESULT Close(void);  
};  
```  

##### <a name="overview"></a>Descrição Geral  
 O **progresso** página utiliza esta classe para executar tarefas num thread separado. Também pode utilizar esta classe sempre que pretender efetuar operações num thread separado. *Tarefas* são qualquer classe que suporte o **ITask** interface.  

 Esta interface é implementada pelo **ID_BackgroundTask** componente ("Microsoft.Wizard.BackgroundTask"), definido na interface de IBackgroundTask.h.  

##### <a name="hresult-inititask-ptask-int-id-ibackgroundcallback-pcallback"></a>HRESULT Init(ITask \*pTask, int id, IBackgroundCallback \*pCallback)  
 Esta interface inicializa o componente, conforme mostrado na tabela 12.  

### <a name="table-12-hresult-init"></a>A tabela 12. HRESULT Init  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**pTask**|Apontador para a classe que contém o código que pretende executar no outro thread|  
|**ID**|Um número que pode utilizar a chamada de retorno **concluído** método dizer que a tarefa foi concluída em execução; útil se iniciar várias tarefas com o mesmo método de chamada de retorno|  
|**pCallback**|Uma classe que implementa o **concluído** método, o que é chamado sempre que uma tarefa é concluída em execução; a chamada para o **concluído** método estará no thread em segundo plano, não o thread de IU|  

##### <a name="void-startvoid"></a>void Start(void)  
 Este método inicia a tarefa no thread de segundo plano e devolve os elementos mostrados na tabela 13.  

### <a name="table-13-return-background-thread"></a>Tabela 13. Devolver o Thread de segundo plano  

|**Devolve**|**Descrição**|  
|-|-|  
|**E_INVALIDARG**|A tarefa já está em execução, pelo que não é possível iniciar neste momento.|  
|**E_FAIL**|Ocorreu um problema ao iniciar o thread.|  
|**S_OK**|O thread foi iniciado.|  

##### <a name="bool-running"></a>BOOL Running()  
 Este método devolve TRUE se a tarefa em segundo plano está atualmente em execução e FALSE se não está em execução.  

##### <a name="hresult-waitdword-waitmilliseconds"></a>HRESULT Wait(DWORD waitMilliseconds)  
 Este método aguarda até que o thread deixa de ser executada ou o número de milissegundos tiver decorrido.  

##### <a name="hresult-terminatedword-exitcode"></a>HRESULT Terminate(DWORD exitCode)  
 Este método inutilizam o thread está em execução (consulte a tabela 14 e tabela 15). Este processo pode demorar um curto período de tempo para terminar depois deste método devolve.  

### <a name="table-14-hresult-terminate-exit-code"></a>Tabela 14. HRESULT terminar o código de saída  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**exitCode**|O código de saída que será enviado para o método de chamada de retorno de conclusão, o que também estará disponível a partir do **GetExitCode** método.|  

### <a name="table-15-termination-codes"></a>Tabela 15. Códigos de terminação  

|**Devolve**|**Descrição**|  
|-|-|  
|**E_FAIL**|Falha ao chamar terminar.|  
|**S_OK**|O pedido para terminar o thread foi concluída com êxito.|  

##### <a name="hresult-getexitcodelpdword-pcode-hresult-phresult"></a>HRESULT GetExitCode(LPDWORD pCode, HRESULT \*pHresult)  
 Utilize este método para obter os resultados da execução da tarefa no thread em segundo plano (consulte a tabela 16).  

### <a name="table-16-result-codes"></a>Tabela 16. Códigos de resultado  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**pCode**|Apontador para um **DWORD** que serão definidas no retorno ou **nullptr** se não for necessário o valor de retorno. Sair, este parâmetro estiver definido como **STILL_ACTIVE** se o thread está em execução, o código pela tarefa **executar** método ou o valor transmitido para o **terminar** método se chamar este método.|  
|**pHresult**|Apontador para um **HRESULT** que serão definidas no retorno ou **nullptr** se não tiver o **HRESULT** valor.|  

##### <a name="hresult-closevoid"></a>HRESULT Close(void)  
 Este método versões o thread de segundo plano. Devolve **E_INVALIDARG** se o thread está atualmente em execução e **S_OK** caso contrário.  

#### <a name="icheckbox-interface"></a>ICheckBox Interface  

```  
__interface ICheckBox : IControl  
{  
    void Check(BOOL check);  
    BOOL IsButtonChecked();  
};  
```  

##### <a name="void-checkbool-check"></a>Verificação de um valor nulo (verifique, BOOL)  
 Defina o estado verificado da caixa de verificação. Quando o método é verdadeiro, a caixa de verificação está selecionada; Quando o método é FALSE, a caixa de verificação está desmarcada.  

##### <a name="bool-isbuttonchecked"></a>BOOL IsButtonChecked()  
 Este método reporta o estado atual da verificação de uma caixa de verificação.  

#### <a name="icombobox-interface"></a>IComboBox Interface  

```  
__interface IComboBox : IControl  
{  
    HRESULT Bind([in] IBindableList *pList);  
    HRESULT Select(int index);  
    int Selected(void);  
    void Add([in] LPCTSTR caption);  
    HRESULT GetText([out, retval] LPBSTR pText);  
    void Clear();  
};  
```  

##### <a name="overview"></a>Descrição Geral  
 Esta interface é implementada pelo **CheckBoxWrapper** componente. Obter uma instância deste componente utilizando o **GetControlWrapper** função auxiliar com o tipo **CONTROL_COMBO_BOX**.  

##### <a name="hresult-bindin-ibindablelist-plist"></a>HRESULT Bind([in] IBindableList \*pList)  
 Utilize este método quando tem uma origem de dados que implementa o **IBindableList** interface. A caixa de listagem inicializa o conteúdo com legendas desta lista.  

##### <a name="hresult-selectint-index"></a>HRESULT Select(int index)  
 Selecione o item na caixa de combinação no índice.  

##### <a name="int-selectedvoid"></a>Int Selected(void)  
 Este método devolve o índice do item selecionado ou **-1** se nada estiver selecionado.  

##### <a name="void-addin-lpctstr-caption"></a>Adicionar um valor nulo ([in] legenda LPCTSTR)  
 Adicione manualmente um item a caixa de combinação.  

##### <a name="hresult-gettextout-retval-lpbstr-ptext"></a>HRESULT GetText([out, retval] LPBSTR pText)  
 Obter a cadeia do item atualmente selecionado na caixa de combinação.  

##### <a name="void-clear"></a>limpar um valor nulo  
 Remova todos os itens da caixa de combinação.  

#### <a name="icontrol-interface"></a>IControl Interface  

```  
__interface IControl : IUnknown  
{  
    HRESULT SetEnable(BOOL enable);  
    BOOL IsEnabled(void);  
    HRESULT SetVisible(BOOL visible);  
};  
```  

##### <a name="overview"></a>Descrição Geral  
 Esta interface é implementada pelo **ControlWrapper** componente. Obter uma instância deste componente utilizando o **GetControlWrapper** função auxiliar com o tipo **CONTROL_GENERIC**.  

##### <a name="hresult-setenablebool-enable"></a>HRESULT SetEnable(BOOL enable)  
 Ativar ou desativar o controlo.  

##### <a name="bool-isenabledvoid"></a>BOOL IsEnabled(void)  
 Devolve TRUE se o controlo está ativado, FALSE se não estiver.  

##### <a name="hresult-setvisiblebool-visible"></a>HRESULT SetVisible(BOOL visible)  
 Mostrar ou ocultar o controlo.  

#### <a name="icpuinfo-interface"></a>ICpuInfo Interface  

```  
__interface ICpuInfo : IUnknown  
{  
    BOOL Is64Bit(void);  
};  
```  

##### <a name="overview"></a>Descrição Geral  
 Obter esta interface criando uma nova **ID_CpuInfo** componente. O único método relatórios se a CPU é 32 ou 64 bits. Tenha em atenção que se tiver um sistema operativo de 32 bits num computador de 64 bits, este método devolve TRUE, porque está apenas a comunicar a largura da CPU (não o sistema operativo).  

##### <a name="idirectory-interface"></a>IDirectory Interface  

```  
__interface IDirectory : IUnknown  
{  
    BOOL FileExists(LPCWSTR name);  
    BOOL FindFirst([in] LPCWSTR name);  
    HRESULT FoundName([out, retval] LPBSTR name);  
    DWORD FoundAttributes(void);  
    BOOL FindNext(void);  
    void FinishFind(void);  
};  
```  

###### <a name="overview"></a>Descrição Geral  
 O **diretório** componente, que criar utilizando **ID_Directory**, fornece uma fachada para trabalhar com diretórios no sistema de ficheiros.  

###### <a name="bool-fileexistslpcwstr-name"></a>BOOL FileExists(LPCWSTR name)  
 Este método devolve TRUE se existir um ficheiro com o nome que fornecer.  

###### <a name="bool-findfirstin-lpcwstr-name"></a>BOOL FindFirst([in] LPCWSTR name)  
 Este método localiza uma correspondência primeiro para o nome que fornecer. É também suporta carateres universais e devolve os nomes de ficheiros e diretórios. O método devolve TRUE se um foi encontrada uma correspondência, FALSE caso contrário.  

###### <a name="hresult-foundnameout-retval-lpbstr-name"></a>HRESULT FoundName([out, retval] LPBSTR name)  
 Este método obtém o nome do ficheiro encontrado com uma chamada para **FindFirst** ou **FindNext**.  

###### <a name="dword-foundattributesvoid"></a>DWORD FoundAttributes(void)  
 Este método devolve o atributo para o ficheiro foi encontrado mais recente ou diretório. Pode utilizar o seguinte código para testar se se trata de um diretório:  

```  
pDirectory->FoundAttributes() & FILE_ATTRIBUTE_DIRECTORY  
```  

###### <a name="bool-findnextvoid"></a>BOOL FindNext(void)  
 Localize o seguinte. Este método devolve TRUE se o outra correspondência foi encontrado, FALSE caso contrário.  

###### <a name="void-finishfindvoid"></a>void FinishFind(void)  
 Este método versões recursos utilizados para a operação de localização.  

#### <a name="idomainjoinvalidator-interface"></a>IDomainJoinValidator Interface  

```  
__interface IDomainJoinValidator : IUnknown  
{  
    HRESULT Init(ILogger *pLogger, IWizardPageContainer *pContainer, IStaticText *pUsername, IStaticText *pPassword, IStaticText *pComputerName);  
    HRESULT IsUsernameValid(LPCWSTR domainName);  
    BOOL CanModifyComputerAdEntry(LPCWSTR domainName);  
};  
```  

##### <a name="overview"></a>Descrição Geral  
 Obter uma instância desta interface utilizando o **ID_DomainJoinValidator** valor para o **CreateInstance** da função de modelo.  

##### <a name="hresult-initilogger-plogger-iwizardpagecontainer-pcontainer-istatictext-pusername-istatictext-ppassword-istatictext-pcomputername"></a>HRESULT Init (ILogger \*pLogger, IWizardPageContainer \*pContainer, IStaticText \*pUsername, IStaticText \*pPassword, IStaticText \*pComputerName)  
 Inicializar a instância, conforme mostrado na tabela 17.  

### <a name="table-17-hresult-init---instance-initialization"></a>Tabela 17. HRESULT Init - inicialização de instância  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**pLogger**|A instância de registo, que está disponível para a página através da página **registador** método|  
|**pContainer**|Transmite os resultados da sua página **contentor** método|  
|**pUsername**|A caixa de texto que contém o nome de utilizador para ser validado|  
|**pPassword**|Caixa de texto que contém a palavra-passe para ser validado|  
|**PComputerName**|A caixa de texto que contém o nome do computador que eventualmente será associado ao domínio|  

##### <a name="hresult-isusernamevalidlpcwstr-domainname"></a>HRESULT IsUsernameValid(LPCWSTR domainName)  
 Este método utiliza o **IADHelper -> ValidLogon** método para realizar o trabalho. Consulte este método para obter mais detalhes.  

##### <a name="bool-canmodifycomputeradentrylpcwstr-domainname"></a>BOOL CanModifyComputerAdEntry(LPCWSTR domainName)  
 Certifique-se de que o se o utilizador tem direitos para modificar a entrada de computador. A maioria do trabalho é feita **IADHelper -> HasAccess**. Se este método devolve FALSE, verifique o ficheiro de registo para obter mais detalhes.  

#### <a name="idrivelist-interface"></a>IDriveList Interface  

```  
__interface IDriveList : IUnknown  
{  
    HRESULT Init(IWmiRepository *pWmi);  
    HRESULT SetWhereClause(LPCTSTR whereClause);  
    HRESULT SetMinimumDriveSize(__int64 size);  
    HRESULT Update(void);  
    HRESULT AddProperty(ENUM_DISK_QUERY_SECTION section, LPCTSTR propName, LPCTSTR propNameReturned);  

    size_t Count(void);  
    HRESULT GetProperty(size_t index, LPCTSTR propName,  LPVARIANT value);  
    HRESULT GetCaption(size_t index,  LPBSTR pCaption);  
}  
```  

##### <a name="hresult-initiwmirepository-pwmi"></a>HRESULT Init(IWmiRepository \*pWmi)  
 Chame este método antes de chamar qualquer outros componentes. Terá de criar um novo **WmiRepository** antes de chamar este método.  

##### <a name="hresult-setwhereclauselpctstr-whereclause"></a>HRESULT SetWhereClause(LPCTSTR whereClause)  
 Este método permite-lhe adicionar o texto que aparece como uma cláusula "where" na consulta. Por exemplo, a linha seguinte devolve apenas as unidades USB:  

```  
pDrives->SetWhereClause(L"WHERE InterfaceType='USB'");  
```  

##### <a name="hresult-setminimumdrivesizeint64-size"></a>HRESULT SetMinimumDriveSize (\__int64 tamanho)  
 Defina o tamanho de unidade de minimizar em bytes, para as unidades que serão devolvidas da consulta.  

##### <a name="hresult-updatevoid"></a>HRESULT Update(void)  
 Execute a consulta. A lista de unidade disponível depois de chamar este método é ordenada pela letra de unidade.  

##### <a name="hresult-addpropertyenumdiskquerysection-section-lpctstr-propname-lpctstr-propnamereturned"></a>HRESULT AddProperty(ENUM_DISK_QUERY_SECTION section, LPCTSTR propName, LPCTSTR propNameReturned)  
 Este método adiciona os nomes das propriedades adicionais que pretende disponibilizar nos resultados da consulta. Chamar este método antes de chamar **atualização**. Tabela 18 mostra três das propriedades de útil.  

### <a name="table-18-hresult-addproperty-useful-properties"></a>Tabela 18. HRESULT AddProperty: Propriedades útil  

|**Secção**|**Propriedade**|**Descrição**|  
|-|-|-|  
|**DISKQUERY_LOGICALDISK**|**Tamanho**|O tamanho, em bytes, representada como uma cadeia|  
|**DISKQUERY_DISKPARTITION**|**DiskIndex**|O número de disco como um número inteiro, a partir de 0|  
|**DISKQUERY_LOGICALDISK**|**VolumeName**|A etiqueta de volume|  

##### <a name="sizet-countvoid"></a>size_t Count(void)  
 O número de registos que a consulta devolve. Chamar **atualização** antes de chamar este método.  

##### <a name="hresult-getpropertysizet-index-lpctstr-propname--lpvariant-value"></a>HRESULT GetProperty(size_t index, LPCTSTR propName, LPVARIANT value)  
 Este método obtém o valor de uma propriedade de resultados da consulta, conforme mostrado na tabela 19.  

### <a name="table-19-hresult-getproperty"></a>Tabela 19. HRESULT GetProperty  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**Índice**|Índice baseado em zero para o registo de resultado|  
|**propName**|Nome da propriedade, por exemplo, "Tamanho"|  
|**Valor**|No retorno, este parâmetro contém um valor de variante da propriedade|  

##### <a name="hresult-getcaptionsizet-index--lpbstr-pcaption"></a>HRESULT GetCaption(size_t index, LPBSTR pCaption)  
 Este método obtém a legenda para mudar um registo é igual a **legenda** propriedade.  

#### <a name="iimagelist-interface"></a>IImageList Interface  

```  
__interface IImageList  
{  
    HRESULT CreateImageList(int width, int height, UINT flags);  
    HImageList GetImageList(void);  
    int AddImage(HInstance hInstance, int resourceId);  
};  
```  

##### <a name="overview"></a>Descrição Geral  
 Esta interface é implementada pelo **ImageList** componente. Obter uma instância deste componente o **IListView** interface.  

##### <a name="hresult-createimagelistint-width-int-height-uint-flags"></a>HRESULT CreateImageList(int width, int height, UINT flags)  
 Crie uma nova lista de imagem, que gere este componente. Chame este método apenas uma vez.  

##### <a name="himagelist-getimagelistvoid"></a>HImageList GetImageList(void)  
 Este método devolve o identificador para obter a lista de imagem no caso de necessitar de efetuar outras operações em lista de imagens.  

##### <a name="int-addimagehinstance-hinstance-int-resourceid"></a>Int AddImage (HInstance hInstance, int resourceId)  
 Adicione uma nova imagem para a lista de imagens de um recurso, conforme mostrado na tabela 20.  

### <a name="table-20-hresult-iimagelist-interface"></a>A tabela 20. HRESULT IImageList Interface  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**hInstance**|Identificador de instância do módulo que contém o recurso de mapa de bits|  
|**resourceId**|ID do recurso para carregar para a lista de imagens|  

#### <a name="ilistview-interface"></a>IListView Interface  

```  
__interface IListView : IControl  
{  
    int AddItem([in] LPCTSTR text);  
    int AddColumn(int width, [in] LPCTSTR text);  
    HRESULT SetSubItem(int index, int column, [in] LPCTSTR text);  
    int GetWidth(void);  
    void SetExtendedStyle(DWORD style);  
    int GetSelectedItem(void);  
    HRESULT SelectItem(int index);  
    BOOL IsItemChecked(int index);  
    int GetItemCount(void);  
    HRESULT CreateImageList(int width, int height, UINT flags);  
    int AddImage(HINSTANCE hInstance, int resourceId);  
    HRESULT SetImage(int index, int imageIndex);  
    HRESULT Clear(void);  
};  
```  

##### <a name="overview"></a>Descrição Geral  
 Esta interface é implementada pelo **ControlWrapper** componente. Obter uma instância deste componente utilizando o **GetControlWrapper** função auxiliar com o tipo **CONTROL_LIST_VIEW**.  

##### <a name="int-additemin-lpctstr-text"></a>Int AddItem ([in] texto LPCTSTR)  
 Adicione uma nova linha para a caixa de listagem. O devolve método acabou de adicionar o índice do item.  

##### <a name="int-addcolumnint-width-in-lpctstr-text"></a>Int AddColumn (int largura, texto LPCTSTR [in])  
 Adicione uma nova coluna para a vista de lista.  

##### <a name="hresult-setsubitemint-index-int-column-in-lpctstr-text"></a>HRESULT SetSubItem(int index, int column, [in] LPCTSTR text)  
 Defina o texto numa coluna que não seja a primeira coluna da caixa de listagem, conforme mostrado na tabela 21.  

### <a name="table-21-hresult-setsubitem"></a>Tabela 21. HRESULT SetSubItem  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**índice**|O índice do item da lista que pretende modificar|  
|**coluna**|O índice da coluna que pretende atualizar; a primeira coluna está definida com **AddItem**, colunas, dois e seguintes estão definidos com este método|  
|**texto**|A cadeia a mostrar na coluna|  

##### <a name="int-getwidthvoid"></a>Int GetWidth(void)  
 Este método devolve a largura da caixa de texto completo.  

##### <a name="void-setextendedstyledword-style"></a>void SetExtendedStyle(DWORD style)  
 Este método permite-lhe definir estilos expandidos na caixa de listagem — por exemplo:  

```  
m_pList->SetExtendedStyle(LVS_EX_FULLROWSELECT);  
```  

##### <a name="int-getselecteditemvoid"></a>Int GetSelectedItem(void)  
 Este método devolve o índice da vista de lista item atualmente selecionado.  

##### <a name="hresult-selectitemint-index"></a>HRESULT SelectItem(int index)  
 Defina o item selecionado na lista para este índice.  

##### <a name="bool-isitemcheckedint-index"></a>BOOL IsItemChecked(int index)  
 Este método devolve TRUE se um item na lista é selecionado. Este método requer que chamar **SetExtendedStyle** ao definir o estilo de caixa de verificação.  

##### <a name="int-getitemcountvoid"></a>Int GetItemCount(void)  
 Este método devolve o número de itens na vista de lista.  

##### <a name="hresult-createimagelistint-width-int-height-uint-flags"></a>HRESULT CreateImageList(int width, int height, UINT flags)  
 Criar uma nova lista de imagem e anexe-o para a vista de lista.  

##### <a name="int-addimagehinstance-hinstance-int-resourceid"></a>Int AddImage (HINSTANCE hInstance, int resourceId)  
 Adicione uma imagem a lista de imagens a vista de lista. Tem de chamar **CreateImageList**, primeiro.  

##### <a name="hresult-setimageint-index-int-imageindex"></a>HRESULT SetImage(int index, int imageIndex)  
 Defina a imagem que será apresentada no lado esquerdo para um item da vista de lista específica.  

##### <a name="hresult-clearvoid"></a>HRESULT Clear(void)  
 Remova todos os itens a partir da vista de lista.  

#### <a name="iprogressbar-interface"></a>IProgressBar Interface  

```  
__interface IProgressBar : IControl  
{  
    HRESULT SetPercentage(int position);  
    int GetPercentage(void);  
};  
```  

##### <a name="overview"></a>Descrição Geral  
 Esta interface é implementada pelo **ProgressBarWrapper** componente. Obter uma instância deste componente utilizando o **GetControlWrapper** função auxiliar com o tipo **CONTROL_PROGRESS_BAR**.  

##### <a name="hresult-setpercentageint-position"></a>HRESULT SetPercentage(int position)  
 Defina a posição do progresso de barra utilizando um número entre 0 e 100. Por predefinição, as barras de progresso do novo Win32® tem um intervalo máximo de 100.  

##### <a name="int-getpercentagevoid"></a>Int GetPercentage(void)  
 Este método devolve a posição actual da barra de progresso.  

#### <a name="iradiobutton-interface"></a>IRadioButton Interface  

```  
__interface IRadioButton : IControl  
{  
public:  
    void SetGroup(int firstId, int lastId);  
    void CheckRadio(int id);  
    BOOL IsButtonChecked(int id);  
    void EnableRadio(int id, BOOL enable);  
};  
```  

##### <a name="overview"></a>Descrição Geral  
 Esta interface é implementada pelo **RadioButtonWrapper** componente. Obter uma instância deste componente utilizando o **GetControlWrapper** função auxiliar com o tipo **CONTROL_RADIO_BUTTON**.  

##### <a name="void-setgroupint-firstid-int-lastid"></a>void SetGroup (int firstId, int lastId)  
 Forneça o wrapper de com o intervalo de botões de opção que devem ser tratados como um grupo. Chamar este método antes de chamar **CheckRadio**.  

##### <a name="void-checkradioint-id"></a>void CheckRadio(int id)  
 Defina o botão de opção específica para ser o único botão no grupo de botões de opção selecionados. Chamar **SetGroup** antes de chamar este método.  

##### <a name="bool-isbuttoncheckedint-id"></a>BOOL IsButtonChecked(int id)  
 Este método devolve TRUE se o botão de opção atualmente selecionado, FALSE caso contrário.  

##### <a name="void-enableradioint-id-bool-enable"></a>void EnableRadio (id de int, ativar BOOL)  
 Este método ativa ou desativa um botão de opção.  

#### <a name="istatictext-interface"></a>IStaticText Interface  

```  
__interface IStaticText : IControl  
{  
    HRESULT SetText([in] LPCTSTR pText);  
    HRESULT GetText([out, retval] LPBSTR pText);  
};  
```  

##### <a name="overview"></a>Descrição Geral  
 Esta interface é implementada pelo **StaticTextWrapper** componente. Obter uma instância deste componente utilizando o **GetControlWrapper** função auxiliar com o tipo **CONTROL_STATIC_TEXT**.  

##### <a name="hresult-settextin-lpctstr-ptext"></a>HRESULT SetText([in] LPCTSTR pText)  
 Defina o texto do controlo.  

##### <a name="hresult-gettextout-retval-lpbstr-ptext"></a>HRESULT GetText([out, retval] LPBSTR pText)  
 Este método devolve o valor atual do texto para o controlo.  

####  <a name="ITaskinterface"></a>ITask Interface  

```  
__interface IControl : IUnknown  
{  
    HRESULT Init(IStringProperties *pProperties, ISettingsProperties *pTaskSettings);  
    HRESULT Execute(LPDWORD pReturnCode);  
};  
```  

 Implemente esta interface se pretender que o componente esteja disponível como uma tarefa na página de verificação prévia ou se quiser utilizar o **BackgroundTask** componente para efetuar o trabalho no thread de segundo plano.  

 Seguem-se os componentes que implementam o **ITask** interface:  

-   ID_ShellExecuteTask, L"Microsoft.Wizard.ShellExecuteTask"  

-   ID_CopyFilesTask, L"Microsoft.Wizard.CopyFilesTask"  

-   ID_ACPowerTask, L"Microsoft.OSDRefresh.ACPowerTask"  

-   ID_WiredNetworkTask, L"Microsoft.SharedPages.WiredNetworkTask"  

##### <a name="init"></a>Init  

```  
HRESULT Init(IStringProperties *pProperties, ISettingsProperties *pTaskSettings)  
```  

 Se estiver a escrever uma tarefa de verificação prévia da página, chame este método para inicializar a tarefa. O ficheiro. config contém XML que pode ter um aspeto semelhante ao seguinte:  

```  
<Task DisplayName="Check Windows Scripting Host" Type="Microsoft.Wizard.ShellExecuteTask">  
  <Setter Property="filename">%windir%\system32\cscript.exe</Setter>  
  <Setter Property="parameters">Preflight\OSDCheckWSH.vbs</Setter>  
  <Setter Property="BitmapFilename">images\WinScriptHost.bmp</Setter>  
  <ExitCodes>  
    <ExitCode State="Success" Type="0" Value="0" Text="" />  
    <ExitCode State="Error" Type="-1" Value="*" Text="Windows Scripting Host not installed." />  
  </ExitCodes>  
</Task>  
```  

 O **pProperties** parâmetro fornece acesso para os valores de três setter, enquanto o **pTaskSettings** parâmetro fornece acesso ao **tarefas** elemento e subordinados. A maioria das tarefas só precisa de ler dados a partir de **pProperties** parâmetro.  

#####  <a name="Execute"></a>Executar  

```  
HRESULT Execute(LPDWORD pReturnCode)  
```  

 Aqui é onde pode escreve o código que executa a tarefa. Este método deverá devolver **S_OK** se ocorreram sem erros, e pode devolver outro **HRESULT** se Ocorreu um erro ao executa a tarefa. Os valores que **S_OK** que este método devolve são correspondidas até < erro\> elementos a < ExitCodes\> secção se estiver a utilizar a página de verificação prévia.  

 O **pReturnCode** parâmetro tem de ser atualizado com um número que reporta o estado da tarefa. Estes valores são correspondidos por página preflights para < ExitCode\> elementos.  

#### <a name="itreeview-interface"></a>ITreeView Interface  

```  
__interface ITreeView : IControl  
{  
    void EnableCheckboxes(void);  
    HRESULT CreateImageList(int width, int height, UINT flags);  
    int AddImage(HINSTANCE hInstance, int resourceId);  

    HTREEITEM AddItem(LPCTSTR text, HTREEITEM hParent = NULL);  
    void SetImage(HTREEITEM item, int image, int expandImage);  

    void Clear(void);  
    BOOL SetFirstVisible(HTREEITEM item);  
    BOOL SelectItem(HTREEITEM item);  
    void CheckItem(HTREEITEM item, UINT checkState);  
    HTREEITEM SelectedItem(void);  
    int SetItemHeight(SHORT height);  
    HRESULT EnableItem(HTREEITEM item, BOOL enable);  
    void Expand(HTREEITEM hItem, BOOL expand);  

    HTREEITEM GetChild(HTREEITEM hParent);  
    HTREEITEM GetParent(HTREEITEM hNode);  
    HTREEITEM GetNextItem(HTREEITEM hPrevious);  

    UINT IsChecked(HTREEITEM item);  
    BOOL IsEnabled(HTREEITEM item);  

    INT_PTR CommonControlEvent(WORD controlId, void* pInfo, BOOL *pCancel);  
    HRESULT SetEventHandler(ITreeViewEvent *pEventHandler);  

    void SetSelectedBackColor(COLORREF color);  
};  
```  

##### <a name="overview"></a>Descrição Geral  
 Esta interface é implementada pelo **TreeViewWrapper** componente. Obter uma instância deste componente utilizando o **GetControlWrapper** função auxiliar com o tipo **CONTROL_TREE_VIEW**.  

##### <a name="void-enablecheckboxesvoid"></a>void EnableCheckboxes(void)  
 Este método Ativa as caixas de verificação no controlo de vista de árvore, definindo o **TVS_CHECKBOXES** estilo.  

##### <a name="hresult-createimagelistint-width-int-height-uint-flags"></a>HRESULT CreateImageList(int width, int height, UINT flags)  
 Adicione uma nova lista de imagem para o controlo de vista de árvore. O **sinalizadores** parâmetro é transmitido na chamada para o **ImageList_Create** função Win32.  

##### <a name="int-addimagehinstance-hinstance-int-resourceid"></a>Int AddImage (HINSTANCE hInstance, int resourceId)  
 Adicionar uma imagem para a lista de imagens a partir de um recurso (**resourceId**) no módulo com o identificador de instância **hInstance**.  

##### <a name="htreeitem-additemlpctstr-text-htreeitem-hparent--null"></a>HTREEITEM AddItem(LPCTSTR text, HTREEITEM hParent = NULL)  
 Adicione um nó para a vista de árvore. O novo nó será adicionado no nível superior se **hParent** é NULL. Caso contrário, forneça o identificador do item principal de onde pretende que o novo item adicionado. Este método devolve o identificador para o novo item.  

##### <a name="void-setimagehtreeitem-item-int-image-int-expandimage"></a>void SetImage (HTREEITEM item, imagem de int, int propriedades-expandImage)  
 Defina a imagem a utilizar para um item da vista de árvore. Pode definir o normal e a imagem expandida.  

##### <a name="void-clearvoid"></a>void Clear(void)  
 Remova todos os itens a partir da vista de árvore.  

##### <a name="bool-setfirstvisiblehtreeitem-item"></a>BOOL SetFirstVisible(HTREEITEM item)  
 Certifique-se de que o item da vista de árvore está visível. A árvore deslocam se for necessário para tornar este item visível.  

##### <a name="bool-selectitemhtreeitem-item"></a>BOOL SelectItem(HTREEITEM item)  
 Defina o item atualmente selecionado para o item que fornecer. Pode chamar **SetFirstVisible** após esta opção para garantir que o item recentemente selecionado está visível.  

##### <a name="void-checkitemhtreeitem-item-uint-checkstate"></a>void CheckItem (HTREEITEM item, UINT checkState)  
 O método basicamente define a imagem que será mostrada para a caixa de verificação na vista de árvore. Estas imagens estão num separado **ImageList** controlo que gere a vista de árvore. Por predefinição, esta lista de imagens tem três imagens no mesmo, mostrado na tabela 22.  

### <a name="table-22void-checkitem-image-list-default"></a>22 de tabela. void CheckItem imagem lista predefinida  

|**checkState**|**Descrição**|  
|-|-|  
|**0**|Em branco|  
|**1**|Limpo|  
|**2**|Selecionado|  

##### <a name="htreeitem-selecteditemvoid"></a>HTREEITEM SelectedItem(void)  
 Este método devolve o identificador da vista de árvore item atualmente selecionado.  

##### <a name="int-setitemheightshort-height"></a>Int SetItemHeight (ABREVIADA altura)  
 Este método define a altura de todos os itens no controlo de vista de árvore em pixéis. Devolve a altura anterior em pixéis.  

##### <a name="hresult-enableitemhtreeitem-item-bool-enable"></a>HRESULT EnableItem(HTREEITEM item, BOOL enable)  
 Este método ativa ou desativa um único item na árvore. Desativar um item com elementos subordinados não desativará o subordinado.  

##### <a name="void-expandhtreeitem-hitem-bool-expand"></a>void expansão (HTREEITEM hItem, BOOL expand)  
 Este método expande ou fecha um nó na árvore.  

##### <a name="htreeitem-getchildhtreeitem-hparent"></a>HTREEITEM GetChild(HTREEITEM hParent)  
 Este método devolve o primeiro subordinado de um item da vista de árvore ou nulo se não existirem sem subordinados.  

##### <a name="htreeitem-getparenthtreeitem-hnode"></a>HTREEITEM GetParent(HTREEITEM hNode)  
 Este método devolve o identificador do elemento principal para um nó na vista de árvore ou nulo se o nó no nível superior.  

##### <a name="htreeitem-getnextitemhtreeitem-hprevious"></a>HTREEITEM GetNextItem(HTREEITEM hPrevious)  
 Pode chamar este método com um identificador que **GetChild** devolve para iterar através de todos os elementos subordinados de um nó. Este método devolve o seguinte colateral na árvore da partilha o mesmo elemento principal.  

##### <a name="uint-ischeckedhtreeitem-item"></a>UINT IsChecked(HTREEITEM item)  
 Este método devolve **0** se o nó de vista de árvore não estiver seleccionado e **1** se for.  

##### <a name="bool-isenabledhtreeitem-item"></a>BOOL IsEnabled(HTREEITEM item)  
 Este método devolve TRUE se o nó de vista de árvore estiver ativado, FALSE caso contrário.  

##### <a name="intptr-commoncontroleventword-controlid-void-pinfo-bool-pcancel"></a>INT_PTR CommonControlEvent(WORD controlId, void* pInfo, BOOL \*pCancel)  
 Este método é apenas para utilização interna.  

##### <a name="hresult-seteventhandleritreeviewevent-peventhandler"></a>HRESULT SetEventHandler(ITreeViewEvent \*pEventHandler)  
 Chame este método se pretender receber notificações quando as alterações do item selecionado ou o utilizador altera o estado de verificação de um item da vista de árvore. Tem de implementar o **ITreeViewEvent** no seu componente para receber estas chamadas de retorno.  

##### <a name="void-setselectedbackcolorcolorref-color"></a>void SetSelectedBackColor(COLORREF color)  
 Defina a cor de fundo utilizada para o item selecionado.  

#### <a name="iwmiiteration-interface"></a>IWmiIteration Interface  

```  
__interface IWmiIterator : IUnknown  
{  
    HRESULT Next(void);  
    HRESULT GetProperty(LPCTSTR propertyName, [out] LPVARIANT pValue);  
};  
```  

##### <a name="overview"></a>Descrição Geral  
 Normalmente utiliza esta interface, juntamente com **IWmiRepository**, ao trabalhar com as chamadas WMI. O **IWmiIteration** interface permite-lhe itere através de valores que devolva uma consulta.  

##### <a name="hresult-nextvoid"></a>HRESULT Next(void)  
 Mover para o item seguinte nos resultados da consulta, conforme mostrado na tabela 23.  

### <a name="table-23-hresult-nextvoid-query-returns"></a>Tabela 23. HRESULT Next(void) consulta devolve  

|**HRRESULT**|**Descrição**|  
|-|-|  
|**S_OK**|Mover para o seguinte resultado; Pode utilizar **GetProperty** obter as propriedades de que resultam.|  
|**S_FALSE**|Existem não existem mais itens na lista.|  
|**E_NOT_SET**|Existem não existem resultados de consulta|  

##### <a name="hresult-getpropertylpctstr-propertyname-out-lpvariant-pvalue"></a>HRESULT GetProperty(LPCTSTR propertyName, [out] LPVARIANT pValue)  
 Este método obtém o valor de uma propriedade do registo de resultados atual, conforme mostrado na tabela 24 e 25 em tabela.  

### <a name="table-24-hresult-getproperty"></a>Tabela 24. HRESULT GetProperty  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**propertyName**|Nome da propriedade que pretende obter|  
|**pValue**|Aponta para uma estrutura de variante que devolvida contém o valor da propriedade|  

### <a name="table-25-hresult-getproperty-result"></a>Tabela 25. HRESULT GetProperty resultado  

|**HRESULT**|**Descrição**|  
|-|-|  
|**S_OK**|O valor da propriedade foi obtido.|  
|**WBEM_E_NOT_FOUND**|Não há nenhuma propriedade com o nome.|  
|**E_NOT_VALID_STATE**|Há um registo atual.|  

> [!NOTE]
>  O **GetProperty** método pode devolver outros códigos de erro WMI que não se encontram listados na tabela 25. Os valores apresentados são os resultados comuns que são devolvidos.  

#### <a name="iwmirepository-interface"></a>IWmiRepository Interface  

```  
__interface IWmiRepository : IUnknown  
{  
    HRESULT SetNamespace(LPCWSTR namespaceName);  
    HRESULT ExecQuery(LPCWSTR query, [out] IWmiIterator **ppIterator);  
};  
```  

##### <a name="overview"></a>Descrição Geral  
 Esta interface é implementada pelo **WmiRepository** componente (**ID_WmiRepository**).  

##### <a name="hresult-setnamespacelpcwstr-namespacename"></a>HRESULT SetNamespace(LPCWSTR namespaceName)  
 Este método define o espaço de nomes WMI que será utilizado para a consulta. Chamar este método antes de chamar **em ExecQuery**. Se não chame este método, o espaço de nomes será root\cimv2. Este método devolve sempre **S_OK**.  

##### <a name="hresult-execquerylpcwstr-query-out-iwmiiterator-ppiterator"></a>HRESULT ExecQuery(LPCWSTR query, [out] IWmiIterator **ppIterator)  
 Executar uma consulta contra o espaço de nomes WMI definida com uma chamada para **SetNamespace**, conforme mostrado na tabela 26 e 27 de tabela.  

### <a name="table-26-hresult-execquery"></a>26 de tabela. Em ExecQuery HRESULT  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**Consulta**|A cadeia para a consulta WMI que pretende executar|  
|**ppIterator**|Transmita um ponteiro para um apontador de interface que devolvida será preenchido com uma interface, concedendo acesso para os resultados da consulta|  

### <a name="table-27-hresult-query-result"></a>27 de tabela. Resultado da consulta HRESULT  

|**HRESULT**|**Descrição**|  
|-|-|  
|**S_OK**|Consulta concluída com êxito|  
|**Outros**|Se a consulta não foi concluída com êxito, devolve uma WMI **HRESULT**|  

#### <a name="iformcontroller-interface"></a>IFormController Interface  

```  
__interface IFormController : IUnknown  
{  
    Init(IWizardPageView *pView, IWizardPageContainer *pContainer);  
    SetPageInfo(ISettingsProperties *pPageInfo);  

    Validate(void);  

    AddToGroup(int groupControlId, int controlId);  
    UpdateCheckGroup(int groupControlId);  
    AddValidator(int controlId, IValidator *pValidator, IControl *pCOntrol = 0);  

    AddValidator(int controlId, LPCWSTR validatorId, LPCWSTR message, IValidator **ppValidator = nullptr);  
    DisableValidation(int controlId, BOOL disable);  

    AddField(LPCWSTR fieldName, int controlId, BOOL suppressLog, DialogControlTypes type);  
    AddRadioGroup(LPCWSTR groupName, int radioControlId);  
    EnableRadioGroup(LPCWSTR groupName, BOOL enable);  
    InitFields(IFieldCallback *pFieldCallback = nullptr);  
    SaveFields(IFieldCallback *pFieldCallback = nullptr);  
    BOOL IsFieldDisabled(int controlId);  

    InitSection(LPCWSTR key, LPCWSTR sectionCaption);  
    AddSummaryItem(LPCWSTR first, LPCWSTR second);  
    SuppressLogValue(LPCWSTR tsVariableName);  
    SaveText(int controlId, LPCWSTR tsVariableName, LPCWSTR summaryCaption);  
    LoadText(int controlId, LPCWSTR tsVariableName);  

    void ControlEvent(WORD eventId, WORD controlId);  
    BOOL IsValid(void);  
 };  
```  

##### <a name="overview"></a>Descrição Geral  
 Todas as páginas no Assistente de UDI tem o seu próprio controlador de formulário que implemente esta interface. Utilize este controlador de ligar os dados de campo no ficheiro XML. config para os controlos da página. O controlador do formulário, em seguida, processa muitos dos detalhes por si.  

#####  <a name="SettingUptheForm"></a>Configurar o formulário  
 Geralmente, configurar o controlador de formulário da página **OnWindowCreated** método. Se o fizer, por isso, normalmente, envolve a chamar os métodos mostrados na tabela 28.  

### <a name="table-28-onwindowcreated-method"></a>28 de tabela. Método de OnWindowCreated  

|**Método**|**Descrição**|  
|-|-|  
|**Init**|Inicializa o controlador de formulário|  
|**AddField**|Fornece uma ligação entre um campo no ficheiro XML. config que é um nome de cadeia e um controlo na caixa de diálogo da página que é um ID|  
|**AddRadioGroup**|Utilizado para ligar um botão de opção para um grupo e um controlo na sua caixa de diálogo|  
|**AddToGroup**|Permite-lhe controlos de "subordinados" ativados ou desativados, juntamente com o respetivo principal ou com base na qual botão de opção está selecionado|  
|**InitFields**|Chamar depois de ter chamado todos os o **adicionar** métodos para configurar o formulário|  
|**Validar**|Efetua a validação inicial|  

##### <a name="processing-form-events"></a>Eventos de formulário de processamento  
 Adicione a seguinte chamada ao seu **OnControlEvent** método:  

```  
Form()->ControlEvent(eventId, controlId);  
```  

 Esta chamada transmite eventos sessão no controlador de formulário, pelo que pode processar eventos relacionados com o formulário.  

##### <a name="save-form-data"></a>Guardar dados do formulário  
 No **OnNextClicked** método, chamar os métodos de formulário mostrados na tabela 29.  

### <a name="table-29-onnextclicked-method"></a>29 de tabela. Método de OnNextClicked  

|**Método**|**Descrição**|  
|-|-|  
|**InitSection**|Fornece o nome da secção que será mostrada no **resumo** página para esta página|  
|**SaveFields**|Guardar valores de campo para variáveis de sequência de tarefas e o **resumo** página|  

#####  <a name="Init"></a>Init  

```  
HRESULT Init(IWizardPageView *pView, IWizardPageContainer *pContainer)  
```  

 Normalmente, chamar este método perto do início da sua página **OnWindowCreated** método. O comando deverá ter um aspeto semelhante ao seguinte:  

```  
Form()->Init(View(), Container());  
```  

##### <a name="setpageinfo"></a>SetPageInfo  

```  
HRESULT SetPageInfo(ISettingsProperties *pPageInfo)  
```  

 Este método é denominado internamente e deve não chamá-la. Fornece XML a página para o controlador de formulário.  

##### <a name="validate"></a>Validar  

```  
HRESULT Validate(void)  
```  

 Este método executa todas as validações ligadas para controlos. Se não obtiver uma validação, o controlador de formulários apresenta uma mensagem de aviso e desativa o **seguinte** botão, em seguida, pára processamento validações. Normalmente, apenas tem de chamar este método no final do seu **OnWindowCreated** método; -devolve sempre **S_OK**.  

##### <a name="addtogroup"></a>AddToGroup  

```  
AddToGroup(int groupControlId, int controlId)  
```  

 Este método adiciona um controlo como "subordinado" de uma caixa de verificação ou um botão de opção, conforme mostrado na tabela 30. Todos os esses controlos subordinados serão desativados quando o controlo de principal não estiver seleccionado. O método devolve sempre **S_OK**.  

### <a name="table-30-addtogroup"></a>30 de tabela. AddToGroup  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**groupControlId**|O ID da caixa de verificação ou do botão de opção que controlará o estado de ativação do controlo subordinado|  
|**Controlld**|O ID do controlo que pretende adicionar como um elemento subordinado|  

##### <a name="updatecheckgroup"></a>UpdateCheckGroup  

```  
HRESULT UpdateCheckGroup(int groupControlId)  
```  

 Este método atualiza a ativar ou desativar o estado de controlos subordinados de um grupo com base no estado do controlo principal. Geralmente, não terá de chamar este método por si, porque o controlador de formulário denomina-o por si.  

##### <a name="addvalidator"></a>AddValidator  

```  
HRESULT AddValidator(int controlId, IValidator *pValidator, IControl *pControl = 0)  
```  

 Chame este método apenas se tiver um validador que pretende criar no código em vez de com o XML. Este método devolve sempre **S_OK**.  

##### <a name="addvalidator"></a>AddValidator  

```  
HRESULT AddValidator(int controlId, LPCWSTR validatorId, LPCWSTR message, IValidator **ppValidator = nullptr)  
```  

 Chame este método apenas se tiver um validador que pretende criar no código em vez de com o XML.  

##### <a name="disablevalidation"></a>DisableValidation  

```  
HRESULT DisableValidation(int controlId, BOOL disable)  
```  

 Chame este método para explicitamente desativar a validação para um controlo ou restaurar validação normal, conforme mostrado na tabela 31. Este método é útil, por exemplo, se tiver regras de ativar/desativar para controlos que não são abrangidos com validação de formulário e terá de desativar a validação de um controlo. Por outras palavras, seria não normalmente chamar este método. Este método devolve sempre **S_OK**.  

### <a name="table-31-hresult-disablevalidation"></a>31 de tabela. HRESULT DisableValidation  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**controlId**|O controlo para o qual pretende ativar ou desativar a validação|  
|**Desativar**|Definido como TRUE para desativar validação e como falso para restaurar a validação normal|  

#####  <a name="AddField"></a>AddField  

```  
HRESULT AddField(LPCWSTR fieldName, int controlId, BOOL suppressLog, DialogControlTypes type)  
```  

 Adicionar um mapeamento de controlo entre o nome num **campo** elemento do ficheiro XML. config e o ID de controlo na caixa de diálogo da página, conforme mostrado na tabela 32. Tem de chamar este método antes da chamada para **InitFields**porque **InitFields** utiliza estas informações. Este método devolve sempre **S_OK**.  

### <a name="table-32-hresult-addfield"></a>Tabela 32. HRESULT AddField  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**FieldName**|Nome do campo conforme é apresentado no XML da página|  
|**controlId**|O ID de controlo no modelo de caixa de diálogo da página|  
|**suppressLog**|Defina como VERDADEIRO se não pretender que os valores deste campo escritas no ficheiro de registo; sempre defina este parâmetro como TRUE para palavra-passe ou campos PIN|  
|**Tipo**|O tipo de controlo, o que é um dos seguintes:<br /><br /> -   **CONTROL_STATIC_TEXT**<br />-   **CONTROL_COMBO_BOX**<br />-   **CONTROL_LIST_VIEW**<br />-   **CONTROL_PROGRESS_BAR**<br />-   **CONTROL_GENERIC**<br />-   **CONTROL_RADIO_BUTTON**<br />-   **CONTROL_CHECK_BOX**<br />-   **CONTROL_TREE_VIEW**|  

#####  <a name="AddRadioGroup"></a>AddRadioGroup  

```  
HRESULT AddRadioGroup(LPCWSTR groupName, int radioControlId)  
```  

 Este método adiciona um controlo a um grupo de botão de opção com nome, conforme mostrado na tabela 33. Tem de chamar este antes do **InitFields** método, porque este método utiliza a atributos no **RadioGroup** elemento para controlar as definições para todos os controlos de botão de opção no grupo. Grupos de botões de opção podem ser bloqueados, por exemplo, para que todos os botões de opção estiverem desativados, mas controlos subordinados estão ativados ou desativadas em apenas o botão de opção está selecionada. Este método devolve sempre **S_OK**.  

### <a name="table-33-hresult-addradiogroup"></a>33 de tabela. HRESULT AddRadioGroup  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**groupName**|Uma cadeia que define um grupo de botões de opção nesta página|  
|**radioControlId**|O ID de um botão de opção única para adicionar a este grupo|  

##### <a name="enableradiogroup"></a>EnableRadioGroup  

```  
HRESULT EnableRadioGroup(LPCWSTR groupName, BOOL enable)  
```  

 Este método permite-lhe ativar ou desativar a um grupo completo de botões de opção. A desativação de um grupo de botões de opção desativa todos os controla o botão de opção no grupo, bem como quaisquer elementos subordinados dos botões de opção que foram adicionados com **AddToGroup**. Consulte a tabela 34 e 35 de tabela.  

### <a name="table-34-enableradiogroup"></a>34 de tabela. EnableRadioGroup  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**groupName**|Nome de um grupo de botão de opção que já definiu com uma chamada para **AddRadioGroup**|  
|**Ativar**|Definido como verdadeiro para ativar o grupo de botões de opção e FALSE desativar o grupo|  

### <a name="table-35-hresult-enableradiogroup"></a>35 de tabela. HRESULT EnableRadioGroup  

|**HRESULT**|**Descrição**|  
|-|-|  
|**S_OK**|Grupo ativado ou desativado|  
|**E_INVALIDARG**|Não há nenhum grupo de botões de opção com o nome fornecido|  

#####  <a name="InitFields"></a>InitFields  

```  
HRESULT InitFields(IFieldCallback *pFieldCallback = nullptr)  
```  

 Antes de chamar este método, chamar **AddField** para cada campo que pode controlar o XML. Este método devolve sempre **S_OK**.  

 O **pFieldCallback** parâmetro é opcional. Se fornecê-lo, o controlador de formulário chama **SetFieldDefault** para controlos que não **CONTROL_STATIC_TEXT** ou **CONTROL_CHECK_BOX**. Este comportamento permite-lhe obter um valor predefinido de XML e defina-o no controlo por si.  

#####  <a name="SaveFields"></a>SaveFields  

```  
HRESULT SaveFields(IFieldCallback *pFieldCallback = nullptr)  
```  

 Este método poupa valores de campo para variáveis de sequência de tarefas e os dados de resumos que serão mostrados no **resumo** página. Fornecer um ponteiro no **pFieldCallback** permite-lhe processar guardar valores para os controlos que não suportam **CONTROL_STATIC_TEXT**.  

##### <a name="isfielddisabled"></a>IsFieldDisabled  

```  
BOOL IsFieldDisabled(int controlId)  
```  

 Este método permite-lhe determinar se um campo foi desativado no XML.  

#####  <a name="InitSection"></a>InitSection  

```  
HRESULT InitSection(LPCWSTR key, LPCWSTR sectionCaption)  
```  

 Este método inicializa os dados de resumos que serão mostrados no **resumo** página, conforme mostrado na tabela 36. Chamar este método seu **OnNextClicked** método antes de chamar **SaveFields**. Este método devolve sempre **S_OK**.  

### <a name="table-36-hresult-initsection"></a>Tabela 36. HRESULT InitSection  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**Chave**|Este parâmetro deve ser exclusivo para a página. É utilizado para garantir que todas as páginas tem as suas informações de resumidas.|  
|**sectionCaption**|O cabeçalho que será mostrado no **resumo** página de informações de resumo de nesta página. Normalmente, utiliza **DisplayName()** como o valor para este parâmetro.|  

##### <a name="addsummaryitem"></a>AddSummaryItem  

```  
HRESULT AddSummaryItem(LPCWSTR first, LPCWSTR second)  
```  

 Este método permite-lhe adicionar itens de resumos para a **resumo** página above and beyond esses itens definido com o XML. Consulte 37 de tabela.  

### <a name="table-37-hresult-addsummaryitem"></a>37 de tabela. HRESULT AddSummaryItem  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**Primeiro**|A legenda para o item de resumo, que é apresentado no lado esquerdo|  
|**Segundo**|O valor que será apresentado no lado direito|  

##### <a name="suppresslogvalue"></a>SuppressLogValue  

```  
HRESULT SuppressLogValue(LPCWSTR tsVariableName)  
```  

 Chame este método para variáveis de sequência de tarefas para os quais não pretende que os valores a serem escritos para o ficheiro de registo. Chame este método para a tarefa de variáveis de sequência que armazenam palavras-passe, PINs ou outros valores confidenciais que um utilizador pode introduzir.  

##### <a name="savetext"></a>SaveText  

```  
HRESULT SaveText(int controlId, LPCWSTR tsVariableName, LPCWSTR summaryCaption)  
```  

 Este método poupa o valor de um controlo de texto para uma variável de sequência de tarefas e a secção de resumo. Normalmente, não terá de chamar este método por si, porque o controlador de formulário efetua este procedimento para todos os campos. Consulte a tabela de 38.  

### <a name="table-38-hresult-savetext"></a>Tabela de 38. HRESULT SaveText  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**controlId**|O ID da caixa de texto que contém o valor que pretende guardar (ou qualquer outro controlo que pode devolver texto)|  
|**tsVariableName**|Nome da variável de sequência de tarefas que pretende modificar|  
|**summaryCaption**|A legenda no **resumo** página para este valor|  

##### <a name="loadtext"></a>LoadText  

```  
HRESULT LoadText(int controlId, LPCWSTR tsVariableName)  
```  

 Este método lê o valor da variável de sequência de tarefas e define a caixa de texto para este valor.  

##### <a name="controlevent"></a>ControlEvent  

```  
void ControlEvent(WORD eventId, WORD controlId)  
```  

 Chamar este método no seu **OnControlEvent** método para se certificar de que o controlador de formulário pode processar eventos de controlo, o que precisa de fazer para funcionar corretamente. Os valores que passa a este método são os mesmos valores transmitidos para o **OnControlEvent** método.  

##### <a name="isvalid"></a>IsValid  

```  
BOOL IsValid(void)  
```  

 Este método devolve o estado da validação do mais recente do formulário. Se qualquer um dos validadores controlo comunicou um erro, este método devolve FALSE. Por outras palavras, devolve TRUE apenas se os controlos na página são válidos.  

#### <a name="ivalidator-interface"></a>IValidator Interface  

```  
__interface IValidator : IUnknown  
{  
    HRESULT Init(IControl *pControl, LPCTSTR message);  
    HRESULT Init(IControl *pControl, IWizardPageContainer *pContainer, IStringProperties *pProperties);  
    BOOL, IsValid(LPBSTR pMessage);  
    HRESULT SetProperty(int propertyId, LPVARIANT pValue);  
    HRESULT SetProperty(int propertyId, IUnknown *pUnknown);  
    HRESULT SetProperty)(int propertyId, LPCTSTR pValue);  
};  
```  

##### <a name="overview"></a>Descrição Geral  
 *Validações* são componentes que podem validar um controlo único na página. A forma mais fácil de implementar um validador é uma subclasse do **BaseValidator** classe que está definida no ficheiro de cabeçalho BaseValidator.h.  

##### <a name="hresult-initicontrol-pcontrol-lpctstr-message"></a>HRESULT Init(IControl \*pControl, LPCTSTR message)  
 Se criar um validador no código, pode chamar este método para inicializar o validador. Consulte 39 de tabela.  

### <a name="table-39-hresult-init"></a>39 de tabela. HRESULT Init  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**pControl**|O controlo necessário validar a validação do|  
|**Mensagem**|A mensagem a apresentar na página, se o controlo não é válido|  

##### <a name="hresult-initicontrol-pcontrol-iwizardpagecontainer-pcontainer-istringproperties-pproperties"></a>HRESULT Init(IControl \*pControl, IWizardPageContainer \*pContainer, IStringProperties \*pProperties)  
 O controlador de formulário chama este método de inicialização validações criados com base em XML da página. Consulte a tabela 40.  

### <a name="table-40-hresult-init-method"></a>40 de tabela. Método Init HRESULT  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**pControl**|O controlo necessário validar a validação do|  
|**pContainer**|Caso o validador precisa de acesso para o registo ou tem de criar outros componentes|  
|**pProperties**|Fornece acesso às propriedades (elementos setter) para a validação do|  

##### <a name="bool-isvalidlpbstr-pmessage"></a>BOOLEANA, IsValid (LPBSTR pMessage)  
 Este método devolve TRUE se o controlo é válida ou FALSO se o controlo é inválido. No retorno, **pMessage** deve ser preenchida com um novo **BSTR** que contém a mensagem a apresentar quando o controlo não é válido.  

##### <a name="hresult-setpropertyint-propertyid-lpvariant-pvalue"></a>HRESULT SetProperty(int propertyId, LPVARIANT pValue)  
 Pode implementar este método se precisar de valores adicionais que não são fornecidos no XML.  

##### <a name="hresult-setpropertyint-propertyid-iunknown-punknown"></a>HRESULT SetProperty(int propertyId, IUnknown \*pUnknown)  
 Pode implementar este método se precisar de valores adicionais que não são fornecidos no XML.  

##### <a name="hresult-setpropertyint-propertyid-lpctstr-pvalue"></a>HRESULT SetProperty) (int propertyId, LPCTSTR pValue)  
 Pode implementar este método se precisar de valores adicionais que não são fornecidos no XML.  

#### <a name="iregex-interface"></a>IRegEx Interface  

```  
__interface IRegEx : IUnknown  
{  
    BOOL MatchesRegex(LPCTSTR input, LPCTSTR regex);  
    HRESULT GetMatch(size_t index, LPBSTR pValue);  
};  
```  

 Este método é implementado pelo **ID_Regex** componente (IRegex.h) e fornece suporte para processamento de expressão regular.  

##### <a name="bool-matchesregexlpctstr-input-lpctstr-regex"></a>BOOL MatchesRegex(LPCTSTR input, LPCTSTR regex)  
 Este método é executada a expressão regular contra o texto de entrada. Utiliza a C++ biblioteca padrão **regex_match** função para realizar o trabalho real. O método devolve TRUE se existir correspondências, FALSE caso contrário.  

##### <a name="hresult-getmatchsizet-index-lpbstr-pvalue"></a>HRESULT GetMatch(size_t index, LPBSTR pValue)  
 Este método permite-lhe obter correspondências da mais recente **MatchesRegex** chamada. Tenha em atenção que não há nenhum erro ao processar este método, e que devolva **S_OK** ou emite uma exceção.  

#### <a name="isummaryinfo-interface"></a>ISummaryInfo Interface  

```  
__interface ISummaryInfo : IUnknown  
{  
    size_t Count(void);  
    HRESULT Clear(void);  
    HRESULT AddInfo(LPCTSTR pFirst, LPCTSTR pSecond);  
    HRESULT GetInfo(size_t index, LPBSTR pFirst, LPBSTR pSecond);  
    HRESULT GetCaption(LPBSTR pCaption);  
    HRESULT SetCaption(LPCTSTR caption);  
};  
```  

 Deve não terá de utilizar esta interface diretamente. Em alternativa, utilize **IFormController**.  

#### <a name="isummarybag"></a>ISummaryBag  

```  
__interface ISummaryBag : IUnknown  
{  
    size_t Count(void);  
    HRESULT GetInfoByIndex(size_t index, [out] ISummaryInfo **ppSummary);  
    HRESULT GetInfoByKey(LPCTSTR key, [out] ISummaryInfo **ppSummary);  
};  
```  

 Deve não terá de utilizar esta interface diretamente. Em alternativa, utilize **IFormController**.  

#### <a name="itsvariablebag-interface"></a>ITSVariableBag Interface  

```  
__interface ITSVariableBag : IUnknown  
{  
    void GetValue([in] LPCTSTR variableName, [out] LPBSTR pValue);  
    void SetValue([in] LPCTSTR variableName, [in] LPCTSTR pValue);  
    void Clear(void);  
    HRESULT Remove([in] LPCTSTR variableName);  
    HRESULT SuppressLogValue([in] LPCTSTR variableName);  
    void Save(void);  
};  
```  

 Esta interface fornece acesso a variáveis de sequência de tarefas. Pode aceder a esta interface utilizando a sua página **TSVariables()** método.  

##### <a name="void-getvaluein-lpctstr-variablename-out-lpbstr-pvalue"></a>GetValue void ([in] variableName LPCTSTR, LPBSTR pValue [out])  
 Este método lê o valor da variável de sequência de tarefas.  

> [!NOTE]
>  Os valores são colocadas em cache após o primeiro de leitura.  

##### <a name="void-setvaluein-lpctstr-variablename-in-lpctstr-pvalue"></a>SetValue void ([in] variableName LPCTSTR, LPCTSTR pValue [in])  
 Este método define o valor da variável de sequência de tarefas. Este valor é guardado na memória. Os valores de sequência de tarefas são escritos assim que clicar em **concluir** no Assistente de UDI.  

##### <a name="void-clearvoid"></a>void Clear(void)  
 Este método Remove todos os valores de sequência de tarefas que foram guardados na memória.  

##### <a name="hresult-removein-lpctstr-variablename"></a>HRESULT Remove([in] LPCTSTR variableName)  
 Este método Remove um valor de sequência de tarefas específica de memória. Da próxima vez que tem de chamar **GetValue** com o mesmo nome de sequência de tarefas, o método tenta para obtê-lo a partir da sequência de tarefas.  

##### <a name="hresult-suppresslogvaluein-lpctstr-variablename"></a>HRESULT SuppressLogValue([in] LPCTSTR variableName)  
 Sempre que são escritas variáveis de sequência de tarefas, tais como quando clicar em **concluir** no Assistente de UDI, os nomes e valores são escritos para o ficheiro de registo. Chame este método para suprimir o registo de valores confidenciais, tais como palavras-passe ou PINs, para uma variável de sequência de tarefas específica.  

##### <a name="void-savevoid"></a>void Save(void)  
 Este método poupa todos os valores de sequência de tarefas que foram definidos com chamadas para **SetValue**.  

#### <a name="itsvariablerepository-interface"></a>ITSVariableRepository Interface  

```  
__interface ITSVariableRepository : IUnknown  
{  
    void GetValue([in] LPCTSTR variableName, BOOL logValue, [out] LPBSTR pValue);  
    void SetValue([in] LPCTSTR variableName, BOOL logValue, [in] LPCTSTR value);  
};  
```  

 Esta interface é para utilização interna pelo **TSVariableBag** para ler e escrever as variáveis de sequência de tarefas.  

#### <a name="iwizardfinish-interface"></a>IWizardFinish Interface  

```  
__interface IWizardFinish : IUnknown  
{  
    HRESULT Canceled(void);  
    HRESULT Finished(void);  
};  
```  

 Esta interface é útil em cenários avançados em que pretende efetuar o processamento adicional quando clicar em **concluir** ou **Cancelar** no Assistente de UDI. O Assistente de UDI contém um **concluir** tarefa que guarda as variáveis de sequência de tarefas ao clicar em **concluir**. Se cancelar o assistente, a tarefa apenas define o **OSDSetupWizCancelled** variáveis de sequência de variável de sequência de tarefas como TRUE e faz a gravação não é alterado para qualquer outra tarefa.  

 Se criar o seus próprios componente concluir, tem de registá-lo com o código seguinte:  

```  
Register<MyFinishTaskFactory>(ID_MyFinishTask, pRegistry);  

PWizardFinish pFinish;  
CreateInstance(pRegistry, ID_MyFinishTask, &pFinish);  

PWizardFinishService pService;  
GetService<IWizardFinishService>(pRegistry, &pService);  

pService->Register(pFinish);  
```  

#### <a name="ibindablelist-interface"></a>IBindableList Interface  

```  
__interface IBindableList : IUnknown  
{  
    size_t Count(void);  
    HRESULT GetCaption(size_t index, LPBSTR pCaption);  
};  
```  

 Implemente esta interface se tiver um componente de origem de dados que pretende vincular a caixa de combinação chamando respetivo **vincular** método.  

##### <a name="sizet-countvoid"></a>size_t Count(void)  
 Este método devolve o número de itens na lista.  

##### <a name="hresult-getcaptionsizet-index-lpbstr-pcaption"></a>HRESULT GetCaption(size_t index, LPBSTR pCaption)  
 Este método devolve a legenda do item num índice específico.  

#### <a name="idatanodes-interface"></a>IDataNodes Interface  

```  
__interface IDataNodes : IUnknown  
{  
    size_t Count();  
    HRESULT SetCaptionProperty(LPCTSTR captionProperty);  
    HRESULT GetProperty(size_t index, LPCTSTR propertyName, [out] LPBSTR propertyValue);  
    HRESULT GetNode(size_t index, [out] ISettingsProperties **ppNode);  
};  
```  

 Esta interface fornece acesso aos dados hierárquicos que podem ser guardados numa página. Obter esta interface através de métodos no **ISettingsProperties** interface, o que está disponível para a página através de **definições** método.  

 Os dados no XML de uma página podem algo semelhante ao seguinte  

```  
      <Data Name="Network">  
        <DataItem>  
          <Setter Property="DisplayName">Public</Setter>  
          <Setter Property="Share">\\servername\Share</Setter>  
        </DataItem>  
        <DataItem>  
          <Setter Property="DisplayName">Dev Team</Setter>  
          <Setter Property="Share">\\servername\DevShare</Setter>  
        </DataItem>  
      </Data>  
```  

 Chamar **Settings() -> GetDataNode (L "Rede" & pData)** dá-lhe um **IDataNodes** instância com itens de dados de dois (cada um dos quais por sua vez tem duas propriedades).  

##### <a name="sizet-count"></a>size_t existente  
 Este método devolve o número de **DataItem** elementos.  

##### <a name="hresult-setcaptionpropertylpctstr-captionproperty"></a>HRESULT SetCaptionProperty(LPCTSTR captionProperty)  
 O componente que suporte esta interface também suporta **IBindableList**, que torna mais fácil preencher a caixa de combinação com os dados a partir de XML da página. Este método controla cuja propriedade (setter) em cada **DataItem** elemento será utilizado para este enlace. Por exemplo, pode chamar este método com **DisplayName**, e de pretende utilizar essa propriedade setter para enlace de dados. A caixa de combinação, em seguida, iria conter **pública** e **equipa de desenvolvimento** como itens.  

##### <a name="hresult-getpropertysizet-index-lpctstr-propertyname-out-lpbstr-propertyvalue"></a>HRESULT GetProperty(size_t index, LPCTSTR propertyName, [out] LPBSTR propertyValue)  
 Este método obtém uma propriedade de um do **DataItem** elementos. Consulte a tabela 41 e 42 de tabela.  

### <a name="table-41-dataitem-getproperty"></a>Tabela 41. DataItem GetProperty  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**Índice**|O valor de índice (começando com 0) da **DataItem** para o qual pretende obter um valor de propriedade|  
|**propertyName**|Nome da propriedade para o qual pretende obter um valor de setter|  
|**propertyValue**|No retorno, contém o valor da cadeia de uma propriedade|  

### <a name="table-42-hresult-getproperty"></a>42 de tabela. HRESULT GetProperty  

|||  
|-|-|  
|**HRESULT**|**Descrição**|  
|**S_OK**|A propriedade foi obtida.|  
|**E_INVALIDARG**|O índice ultrapassa o fim da matriz.|  

##### <a name="hresult-getnodesizet-index-out-isettingsproperties-ppnode"></a>HRESULT GetNode(size_t index, [out] ISettingsProperties **ppNode)  
 Este método é semelhante à **GetProperty**, mas em vez de devolver um valor de um **DataItem**, devolve a toda a **DataItem** moldado num  **ISettingsProperties** interface. Consulte a tabela 43 e 44 de tabela.  

### <a name="table-43-hresult-getnode"></a>43 de tabela. HRESULT GetNode  

|**Parâmetro**|**Descrição**|  
|-|-|  
|Índice|O valor de índice (começando com 0) da **DataItem** para o qual pretende obter um valor de propriedade|  
|**ppNode**|Sair, a **ISettingsProperties** interface que encapsula num wrapper a **DataItem** nós|  

### <a name="table-44-hresult-getnode-results"></a>44 de tabela. HRESULT GetNode resultados  

|**HRESULT**|**Descrição**|  
|-|-|  
|**S_OK**|O nó foi obtido.|  
|**E_INVALIDARG**|O índice ultrapassa o fim da matriz.|  

#### <a name="ifactoryregistry-interface"></a>IFactoryRegistry Interface  

```  
__interface IFactoryRegistry : IUnknown  
{  
    void Register(LPCTSTR type,  IClassFactory *pFactory);  
    HRESULT LoadAndRegister(LPCTSTR dllName, ILogger *pLogger);  
    BOOL Contains(LPCTSTR type);  
    HRESULT GetFactory(LPCTSTR type,  IClassFactory **ppFactory);  
    HRESULT CreateInstance(LPCTSTR type,  IUnknown **ppInstance);  
    HRESULT SetContainer(IWizardPageContainer *pContainer);  
    HRESULT RegisterService(REFGUID iid, IUnknown *pService);  
    HRESULT GetService(REFGUID iid,  IUnknown **ppService);  
};  
```  

##### <a name="overview"></a>Descrição Geral  
 Quando cria uma nova página personalizada, no mínimo tem de criar um *fábrica página*— uma classe que implementa **IClassFactory**. (Pode utilizar **ClassFactoryImpl** como uma classe base para a fábrica.)  

##### <a name="void-registerlpctstr-type--iclassfactory-pfactory"></a>void registar (tipo LPCTSTR, IClassFactory \*pFactory)  
 Este método regista uma fábrica de classe com o registo. Consulte a tabela 45.  

### <a name="table-45-iclassfactory-void-register"></a>Tabela 45. Registar void IClassFactory  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**Tipo**|Uma cadeia que identifica a fábrica de que está a registar; Geralmente, este parâmetro deve ter o nome da empresa na cadeia para se certificar de que é exclusivo|  
|**pFactory**|Um apontador para a instância de fábrica de classe|  

##### <a name="hresult-loadandregisterlpctstr-dllname-ilogger-plogger"></a>HRESULT LoadAndRegister(LPCTSTR dllName, ILogger \*pLogger)  
 Este método é apenas para utilização interna.  

##### <a name="bool-containslpctstr-type"></a>BOOL Contains(LPCTSTR type)  
 Este método é, geralmente, para utilização interna. -Verifica se uma fábrica de classe tiver sido registada para um tipo.  

##### <a name="hresult-getfactorylpctstr-type--iclassfactory-ppfactory"></a>HRESULT GetFactory(LPCTSTR type, IClassFactory **ppFactory)  
 Este método permite-lhe obter a fábrica de classe. Normalmente, iria chamar **CreateInstance**. No entanto, se pretender criar um grande número de mesmo componente, é mais eficiente para obter a fábrica e, em seguida, peça ao criar as instâncias para si.  

##### <a name="hresult-createinstancelpctstr-type--iunknown-ppinstance"></a>HRESULT CreateInstance(LPCTSTR type, IUnknown **ppInstance)  
 Este método cria uma nova instância de um componente, o tipo indicado. Utilize o **CreateInstance** método de modelo em vez disso, que permite a criação do objeto de tipo seguro.  

##### <a name="hresult-setcontaineriwizardpagecontainer-pcontainer"></a>HRESULT SetContainer(IWizardPageContainer \*pContainer)  
 Este método é apenas para utilização interna.  

##### <a name="hresult-registerservicerefguid-iid-iunknown-pservice"></a>HRESULT RegisterService(REFGUID iid, IUnknown \*pService)  
 *Serviços* são instâncias único de um componente que podem ser utilizadas em vários locais. Pode utilizar este método para registar um serviço numa página e, em seguida, obter essa mesma instância de outra página.  

##### <a name="hresult-getservicerefguid-iid--iunknown-ppservice"></a>HRESULT GetService(REFGUID iid, IUnknown **ppService)  
 Este método obtém um serviço que foi registado com uma chamada para RegisterService.  

##### <a name="hresult-setlanguagelangid-languageid"></a>HRESULT SetLanguage(LANGID languageId)  
 Este método define o idioma do Assistente de UDI para o identificador de linguagem fornecida no **languageId** parâmetro.  

##### <a name="langid-getlanguage"></a>LANGID GetLanguage()  
 Este método devolve o valor do identificador de linguagem fornecido com o **/locale** parâmetro da linha de comandos para que o Assistente de UDI. O método devolve um dos seguintes valores:  

-   Valor do identificador de linguagem fornecido com o **/locale** parâmetro da linha de comandos  

-   0, se não forneceu o **/locale** parâmetro da linha de comandos  

#### <a name="ilogger-interface"></a>ILogger Interface  

```  
__interface ILogger : IUnknown  
{  
    HRESULT Init(LPCWSTR logFilename);  
    HRESULT MoveLog(LPCWSTR logFilename);  
    HRESULT LogBase(EMessageType messageType, LPCTSTR component, SYSTEMTIME eventTime, LPCTSTR message);  
    HRESULT Log(EMessageType messageType, LPCTSTR component, LPCTSTR message);  
    HRESULT Error(HRESULT error, LPCTSTR component, LPCTSTR message);  
    HRESULT Error2(HRESULT error, LPCTSTR component, LPCTSTR message, LPCTSTR message2);  
    HRESULT Normal(LPCTSTR component, LPCTSTR message);      
    HRESULT Normal2(LPCTSTR component, LPCTSTR message, LPCTSTR message2);  
    HRESULT Verbose(LPCTSTR component, LPCTSTR message);  
    HRESULT Verbose2(LPCTSTR component, LPCTSTR message, LPCTSTR message2);  
    HRESULT Debug(LPCWSTR component, LPCWSTR message);  
    HRESULT EnableDebug(BOOL debug);  
    HRESULT Close(void);  
    HRESULT GetLogFilename(LPBSTR pFilename);  
};  
```  

##### <a name="overview"></a>Descrição Geral  
 O Assistente de UDI regista as informações para um ficheiro de registo, que ajuda a resolver problemas encontrados no campo. É aconselhável para as suas páginas registar informações. Pode obter um ponteiro para esta interface a partir de dentro da sua página utilizando a página **Logger()** método. Linhas no ficheiro de registo contém um número de "nível" esse erro representa, normal, verboso ou mensagens de depuração.  

> [!NOTE]
>  Mensagens de depuração não são guardadas no ficheiro de registo, a menos que o suporte de depuração está ativado. Pode ativar o suporte de depuração, adicionando a seguinte linha para o **estilo** elemento no ficheiro. config:  

```  
<Setter Property="debug">true</Setter>  
```  

##### <a name="init"></a>Init  

```  
HRESULT Init(LPCWSTR logFilename)  
```  

 Este método é apenas para utilização interna.  

##### <a name="movelog"></a>MoveLog  

```  
HRESULT MoveLog(LPCWSTR logFilename)  
```  

 Este método é apenas para utilização interna.  

##### <a name="logbase"></a>LogBase  

```  
HRESULT LogBase(EMessageType messageType, LPCTSTR component, SYSTEMTIME eventTime, LPCTSTR message)  
```  

 Este método é apenas para utilização interna.  

##### <a name="log"></a>Registo  

```  
HRESULT Log(EMessageType messageType, LPCTSTR component, LPCTSTR message)  
```  

 Este método é apenas para utilização interna.  

##### <a name="error"></a>Erro  

```  
HRESULT Error(HRESULT error, LPCTSTR component, LPCTSTR message)  
```  

 Chame este método para registar informações sobre o erro. Consulte 46 de tabela.  

### <a name="table-46-hresult-error"></a>46 de tabela. Erro HRESULT  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**Erro**|O código de erro devolvido por uma chamada (este código será apresentado na entrada de registo como um número).|  
|**Componente**|Uma cadeia que identifica a origem do erro, o que é, geralmente, a página ou o componente que tenha escritas|  
|**Mensagem**|A mensagem que explica o que causou o erro|  

#####  <a name="Error2"></a>Error2  

```  
HRESULT Error2(HRESULT error, LPCTSTR component, LPCTSTR message, LPCTSTR message2)  
```  

 Este método é semelhante a **erro** método, mas permite-lhe fornecer uma mensagem de duas partes. A mensagem final terá "mensagem" e, em seguida, "message2" no ficheiro de saída. Este é simplesmente um método de conveniência.  

##### <a name="normal"></a>Normal  

```  
HRESULT Normal(LPCTSTR component, LPCTSTR message)  
```  

 Este método regista uma mensagem normal. Consulte a descrição do [erro](#Error) método para os parâmetros.  

##### <a name="normal2"></a>Normal2  

```  
HRESULT Normal2(LPCTSTR component, LPCTSTR message, LPCTSTR message2)  
```  

 Este método regista uma mensagem normal. Consulte a descrição do [Error2](#Error2) método para os parâmetros.  

##### <a name="verbose"></a>Verboso  

```  
HRESULT Verbose(LPCTSTR component, LPCTSTR message)  
```  

 Este método regista uma mensagem verbosa. Consulte a descrição do [erro](#Error) método para os parâmetros.  

##### <a name="verbose2"></a>Verbose2  

```  
HRESULT Verbose2(LPCTSTR component, LPCTSTR message, LPCTSTR message2)  
```  

 Este método regista uma mensagem verbosa. Consulte a descrição do [Error2](#Error2) método para os parâmetros.  

##### <a name="debug"></a>Depuração  

```  
HRESULT Debug(LPCWSTR component, LPCWSTR message)  
```  

 Este método regista uma mensagem de depuração. Consulte a descrição do [erro](#Error) método para os parâmetros. Depurar mensagens não são guardadas para o ficheiro, a menos que ativado. Consulte a secção de descrição geral para obter mais detalhes.  

##### <a name="enabledebug"></a>EnableDebug  

```  
HRESULT EnableDebug(BOOL debug)  
```  

 Este método é apenas para utilização interna.  

##### <a name="close"></a>Fechar  

```  
HRESULT Close(void)  
```  

 Este método é apenas para utilização interna.  

##### <a name="getlogfilename"></a>GetLogFilename  

```  
HRESULT GetLogFilename(LPBSTR pFilename)  
```  

 Este método obtém o nome do ficheiro de registo.  

#### <a name="iorientation-interface"></a>IOrientation Interface  

```  
__interface IOrientation : IUnknown  
{  
    void SetController(IWizardDialogController *pController);  
    int AddPage(LPCTSTR name);  
    void SelectPage(int index);  
};  
```  

 Esta interface é apenas para utilização interna.  

#### <a name="isettings-interface"></a>ISettings Interface  

```  
__interface ISettings : IUnknown  
{  
    int NumDlls();  
    int NumPages();  

    HRESULT SetStage(LPCWSTR stageName);  
    HRESULT GetDllName(long index, __out LPBSTR pDllName);  
    HRESULT GetPageInfo(long index, __out ISettingsProperties **ppPageInfo);  
    HRESULT GetStyle(__out ISettingsProperties **ppStyleInfo);  
};  
```  

 Esta interface é apenas para utilização interna.  

#### <a name="isettingsproperties-interface"></a>ISettingsProperties Interface  

```  
__interface ISettingsProperties : IUnknown  
{  
    HRESULT GetAttribute(LPCTSTR attributeName, __out LPBSTR attributeValue);  
    IStringProperties * Properties();  
   RESULT SelectNodes(LPCTSTR xPath, __out IXMLDOMNodeList **ppList);  
    HRESULT SelectSingleNode(LPCTSTR xPath, __out IXMLDOMNode **ppNode);  
    HRESULT GetDataNode(LPCTSTR name, __out ISettingsProperties **ppNode);  
    HRESULT GetDataNodes(__out IDataNodes **ppNodes);  
    HRESULT GetChildDataNodes(LPCTSTR childeName, __out IDataNodes **ppNodes);  
};  
```  

##### <a name="overview"></a>Descrição Geral  
 Esta interface fornece acesso aos dados de página. Para obter o nível superior dos dados de página, utilize a página **Settings()** método.  

##### <a name="hresult-getattributelpctstr-attributename--lpbstr-attributevalue"></a>HRESULT GetAttribute(LPCTSTR attributeName, LPBSTR attributeValue)  
 Este método permite-lhe obter os valores dos atributos no nó principal, que é o **página** nó quando estiver a utilizar o **Settings()** método da página.  

##### <a name="istringproperties--properties"></a>IStringProperties * Properties()  
 Este método proporciona acesso para os valores de propriedade setter sob o nó principal. Para uma página, estas são as propriedades de nível superior.  

##### <a name="hresult-selectnodeslpctstr-xpath--ixmldomnodelist-pplist"></a>HRESULT SelectNodes(LPCTSTR xPath, IXMLDOMNodeList **ppList)  
 Chame este método se pretender obter diretamente uma lista de nós XML a utilizar uma expressão de XPath. É melhor utilizar um dos outros métodos se puder. Utilize este método apenas se não é possível obter a nós de qualquer forma.  

##### <a name="hresult-selectsinglenodelpctstr-xpath--ixmldomnode-ppnode"></a>HRESULT SelectSingleNode(LPCTSTR xPath, IXMLDOMNode **ppNode)  
 Chame este método se pretender obter diretamente um único nó XML utilizando uma expressão de XPath. É melhor utilizar um dos outros métodos se puder. Utilize este método apenas se não é possível obter a um nó de qualquer forma.  

##### <a name="hresult-getdatanodelpctstr-name--isettingsproperties-ppnode"></a>HRESULT GetDataNode(LPCTSTR name, ISettingsProperties **ppNode)  
 Obter um **dados** elemento com base no elemento da **nome** atributo.  

##### <a name="hresult-getdatanodesidatanodes-ppnodes"></a>HRESULT GetDataNodes(IDataNodes **ppNodes)  
 Este método obtém uma lista de **DataItem** elementos sob o nó atual. Do nível da página, chamar **GetDataNode** para obter um **ISettingsProperty** interface para os dados. Em seguida, nessa instância, chame **GetDataNodes** para obter a lista de registos. Por exemplo, fornecido este XML:  

```  
    <Page …>  
      <Data Name="Network">  
        <DataItem>  
          <Setter Property="DisplayName">Public</Setter>  
          <Setter Property="Share">\\servername\Share</Setter>  
        </DataItem>  
        <DataItem>  
          <Setter Property="DisplayName">Dev Team</Setter>  
          <Setter Property="Share">\\servername\DevShare</Setter>  
        </DataItem>  
      </Data>  

PSettingsProperties pData;  
Settings()->GetDataNode(L"Network", &pData);  
PDataNodes pNodes;  
pData->GetDataNodes(&pNodes);  
```  

##### <a name="hresult-getchilddatanodeslpctstr-childename--idatanodes-ppnodes"></a>HRESULT GetChildDataNodes(LPCTSTR childeName, IDataNodes **ppNodes)  
 Este método proporciona uma forma rápida de obter ao conjunto de **DataItem** nós em específico **dados** nós. Utilizar o XML do **GetDataNodes** exemplo, o seguinte código exatamente a mesma coisa como as quatro linhas de código no exemplo em **GetDataNodes** mas com a verificação do erro:  

```  
ISimpleStringProperties Interface  
```  

#### <a name="isimplestringproperties-interface"></a>ISimpleStringProperties Interface  

```  
__interface ISimpleStringProperties : IStringProperties  
{  
void Add(LPCTSTR propertyName, LPCTSTR value);  
};  
```  

 Por si só, esta interface não pode ser útil. No entanto, é implementado pelo **ID_SimpleStringProperties** componente, que também implementa o **IStringProperties** interface. Pode utilizar este componente em casos em que tem de passar de um conjunto de propriedades para outro componente, tais como uma tarefa, mas que pretende adicionar valores programaticamente em vez de utilizar os valores a partir de XML. Eis um exemplo de como pretende utilizar esta interface:  

```  
PSimpleStringProperties *pProperties;  
CreateInstance(Container(), ID_SimpleStringProperties, &pProperties);  
pProperties->Add(L"filename", L"%windir%\\system32\\cscript.exe");  
pTask->Init(pProperties, nullptr);  
IStringProperties  
__interface IStringProperties : IUnknown  
{  
    HRESULT Get(LPCTSTR propertyName, [out] LPBSTR pPropValue);  
};  
```  

 Esta interface fornece acesso simple para um conjunto de elementos setter provenientes de XML. Esta interface está disponível para as propriedades de uma página utilizando **Settings() -> Properties()**.  

##### <a name="hresult-getlpctstr-propertyname-out-lpbstr-ppropvalue"></a>HRESULT Get(LPCTSTR propertyName, [out] LPBSTR pPropValue)  
 Este método obtém um valor de propriedade de único. Consulte a tabela 47 e 48 de tabela.  

### <a name="table-47-ihresult-get-property-value"></a>47 de tabela. Valor da propriedade Get IHRESULT  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**propertyName**|Nome da propriedade que pretende ler|  
|**pPropValue**|Sair, contém o valor da propriedade como uma cadeia (este valor será **nullptr** se não houver nenhuma essa propriedade.)|  

### <a name="table-48-ihresult-get-property-value-results"></a>Tabela 48. IHRESULT obter resultados de valor de propriedade  

|||  
|-|-|  
|**HRESULT**|**Descrição**|  
|**S_OK**|Obter o valor da propriedade.|  
|**E_INVALIDARG**|Não há nenhuma propriedade com o nome que forneceu.|  

#### <a name="itaskmanager-interface"></a>ITaskManager Interface  

```  
__interface ITaskManager : IUnknown  
{  
    HRESULT Init(IWizardPageView *pPageView, int idListView, int idMessage, int idRetryButton, ISettingsProperties *pPageInfo, ITaskManagerCallback *pCallback);  
    HRESULT SetFailMessage(LPCWSTR message);  

    HRESULT Start(void);  

    HRESULT GetTaskMessage(size_t index, LPBSTR message);  
    HRESULT GetResultType)(size_t index, LPBSTR type);  
    HRESULT GetProperty(size_t index, LPCTSTR propertyName, LPBSTR value);  
    int GetSelectedIndex(void);  
    HRESULT Wait(DWORD waitMilliseconds);  
    size_t FailedCount(void);  
    size_t WarningCount(void);  
    size_t SucceedCount(void);  
    size_t RunningCount(void);  

    void OnCommonControlEvent(WORD controlId, LPNMHDR pInfo);  
    void OnControlEvent(WORD eventId, WORD controlId);  
    void EnableButtons(BOOL enable);  
}  
```  

 Esta interface é implementada pelo **TaskManager** componente (**ID_TaskManager** no ITaskManager.h), que é o componente que executa tarefas na página de verificação prévia. Pode utilizar a página verificação prévia de uma só diretamente, o que é o que fazer a maioria das vezes, ou criar a seus próprios página, permitir que este componente efetuar a maioria do trabalho.  

##### <a name="hresult-initiwizardpageview-ppageview-int-idlistview-int-idmessage-int-idretrybutton-isettingsproperties-ppageinfo-itaskmanagercallback-pcallback"></a>HRESULT Init(IWizardPageView \*pPageView, int idListView, int idMessage, int idRetryButton, ISettingsProperties \*pPageInfo, ITaskManagerCallback \*pCallback)  
 Tem de chamar este método antes de chamar qualquer outro método. -Inicializa a **TaskManager** componente. Consulte 49 de tabela.  

### <a name="table-49-hresult-init"></a>49 de tabela. HRESULT Init  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**pPageView**|Fornece acesso para a página que irá ser tarefas em execução (esta página tem de ter um conjunto específico de controlos, que são descritas na seguintes alguns parâmetros.)|  
|**idListView**|O ID de controlo de um **ListView** controlo irá apresentar a lista de tarefas e o estado dessas tarefas|  
|**idMessage**|O ID de controlo de uma caixa de texto que será utilizado para apresentar uma mensagem para a tarefa que selecionou|  
|**idRetryButton**|O ID de controlo de um botão pode clicar em executar novamente as tarefas|  
|**pPageInfo**|Um wrapper em torno XML da página (**TaskManager** carrega o conjunto de tarefas para executar a partir deste XML.)|  
|**pCallback**|Pode ser nulo (se este parâmetro não for nulo, **TaskManager** chamadas a **iniciado** método quando inicia uma tarefa e o **concluído** método para cada tarefa que termina em execução.)|  

##### <a name="hresult-setfailmessagelpcwstr-message"></a>HRESULT SetFailMessage(LPCWSTR message)  
 Este método define a mensagem que será apresentada se um ou mais tarefas falharem.  

##### <a name="hresult-startvoid"></a>HRESULT Start(void)  
 Este método inicia todas as tarefas. Cada tarefa é iniciada num thread separado.  

##### <a name="hresult-gettaskmessagesizet-index-lpbstr-message"></a>HRESULT GetTaskMessage(size_t index, LPBSTR message)  
 Este método é apenas para utilização interna. Obtém a mensagem atual para uma tarefa com base no respetivo índice na lista de tarefas.  

##### <a name="hresult-getresulttypesizet-index-lpbstr-type"></a>HRESULT GetResultType) (índice de size_t, tipo LPBSTR)  
 Este método obtém atual "type" de uma tarefa. 50 tabela mostra os tipos disponíveis.  

### <a name="table-50-hresult-getresulttype"></a>50 de tabela. HRESULT GetResultType  

|**Tipo**|**Descrição**|  
|-|-|  
|**0**|Representa uma tarefa que foi concluída com êxito|  
|**1**|Representa um tarefas que devolveu um aviso|  
|**-1**|Representa uma tarefa falhada|  

 O tipo é obtido pelo observar o código de saída ou de erros da tarefa e encontrar uma correspondência da tarefa < ExitCodes\> elemento XML.  

##### <a name="hresult-getpropertysizet-index-lpctstr-propertyname-lpbstr-value"></a>HRESULT GetProperty(size_t index, LPCTSTR propertyName, LPBSTR value)  
 Este método é utilizado pelas páginas de progresso e verificação prévia para obter o **BitmapFilename** propriedade setter para poder apresentar uma imagem junto a mensagem para a tarefa que o utilizador realça. Por outras palavras, pode adicionar um setter personalizado para XML a tarefa e, em seguida, obtê-lo com este método.  

##### <a name="int-getselectedindexvoid"></a>Int GetSelectedIndex(void)  
 Este método obtém o índice da tarefa atualmente selecionado, o que é útil se pretender obter informações adicionais sobre a tarefa (consulte **GetProperty** método) a apresentar para a tarefa selecionada. O progresso e páginas prévias utilizam este método para apresentar uma imagem para a tarefa selecionada.  

##### <a name="hresult-waitdword-waitmilliseconds"></a>HRESULT Wait(DWORD waitMilliseconds)  
 Este método principalmente ajuda com os testes de unidade para que o teste pode Certifique-se de que o das tarefas esteja concluída antes da unidade sai de teste. Normalmente, não deverá chamar este método. Devolve quando concluir a todas as tarefas em execução ou o tempo de espera expirou.  

##### <a name="sizet-failedcountvoid"></a>size_t FailedCount(void)  
 Este método devolve o número de tarefas atualmente marcado como falhado.  

##### <a name="sizet-warningcountvoid"></a>size_t WarningCount(void)  
 Este método devolve o número de tarefas atualmente marcado como aviso.  

##### <a name="sizet-succeedcountvoid"></a>size_t SucceedCount(void)  
 Este método devolve o número de tarefas atualmente marcados como concluída com êxito.  

##### <a name="sizet-runningcountvoid"></a>size_t RunningCount(void)  
 Este método devolve o número de tarefas atualmente em execução.  

##### <a name="void-oncommoncontroleventword-controlid-lpnmhdr-pinfo"></a>void OnCommonControlEvent (WORD controlId, LPNMHDR pInfo)  
 Chamar este método a partir da página **OnCommonControlEvent** o **TaskManager** pode processar os eventos que necessita.  

##### <a name="void-oncontroleventword-eventid-word-controlid"></a>void OnControlEvent (WORD eventId, WORD controlId)  
 Chamar este método a partir da página **OnControlEvent** o **TaskManager** pode processar os eventos que necessita.  

##### <a name="void-enablebuttonsbool-enable"></a>void EnableButtons(BOOL enable)  
 Este método é apenas para utilização interna.  

#### <a name="iwizardcomponent-interface"></a>IWizardComponent Interface  

```  
__interface IWizardComponent : IUnknown  
{  
    HRESULT SetContainer(IWizardPageContainer *pContainer);  
};  
```  

##### <a name="overview"></a>Descrição Geral  
 Normalmente, que não implementará esta interface diretamente, mas em vez disso, através de **WizardComponent** classe de modelo. Se o componente implemente esta interface e que registou uma fábrica de classe com o registo, o seu componente recebe um ponteiro para o **IWizardPageContainer** instância quando é criado. Isto ajuda a que, por exemplo, o registo ou no registo para a criação de outros componentes que poderá ter o componente de acesso.  

#### <a name="iwizarddialogcontroller-interface"></a>IWizardDialogController Interface  

```  
__interface IWizardDialogController : IUnknown  
{  
    void Initialize(ISettings *pSettings);  
    void InitPages(void);  
    void Start();  
    void Next();  
    void Finish();  
    void Previous();  
    int NumPages();  
    void Cancel();  

    HRESULT Focus(WizardButtons button);  
    HRESULT SetEnable(WizardButtons button, BOOL enable);  
    void ShowWarningMessage(LPCTSTR message);  
    void HideWarningMessage();  

    void ChangePage(size_t newIndex);  
    IUnknown *CurrentPage(void);  
    HRESULT GetCurrentTitle([out, retval] LPBSTR pDisplayName);  
};  
```  

 Esta interface é apenas para utilização interna.  

#### <a name="iwizarddialogview-interface"></a>IWizardDialogView Interface  

```  
__interface IWizardDialogView : IUnknown  
{  
    HRESULT LoadBannerImage(LPCTSTR bannerFilename);  
    HRESULT LoadPage(LPCTSTR pageType, ISettingsProperties *pPageSettings, IWizardPageView **view);  
    HRESULT SetEnable(WizardButtons button, BOOL enable);  
    HRESULT Focus(WizardButtons button);  
    void EnableFinish(BOOL isFinish);  
    void Exit(int exitCode);  
    void ShowWarningMessage(LPCTSTR message);  
    void HideWarningMessage(void);  
    void SetTitle(LPCTSTR title);  
    void SetPageTitle(LPCTSTR title);  
    int ShowMessageBox(LPCTSTR message, LPCTSTR lpCaption, UINT uType);  
    HWND GetHwnd(void);  
    void UpdateFocus(void);  
};  
```  

 Esta interface é apenas para utilização interna.  

####  <a name="IWizardPageInterface"></a>IWizardPage Interface  

```  
__interface IWizardPage : IUnknown  
{  
    HRESULT SetPageSettings(ISettingsProperties *pPageSettings);  
    HINSTANCE GetInstanceHandle(void);  
    int GetDialogResourceId(void);  
    void WindowCreated(IWizardPageView *pView, IWizardPageContainer *pContainer);  
    void WindowShown(void);  
    void WindowHidden(void);  

    HRESULT NextClicked(void);  
    void ControlEvent(WORD eventId, WORD controlId);  
    void CommonControlEvent(WORD controlId, LPNMHDR pInfo, LPBOOL pCancel);  
    void UnhandledEvent(HWND hwnd, UINT message, WPARAM wParam, LPARAM lParam);  
};  
```  

##### <a name="overview"></a>Descrição Geral  
 Esta interface é implementada por **WizardPageImpl**, pelo que será, normalmente, tem de implementar este it por si. O assistente chama todos estes métodos para si quando interage com as suas páginas personalizadas.  

#### <a name="iwizardpagecontainer-interface"></a>IWizardPageContainer Interface  

```  
__interface IWizardPageContainer : IUnknown  
{  
    ILogger * Logger(void);  
    IPropertyBag * Properties(void);  
    HRESULT CreateInstance(LPCTSTR type, [out] IUnknown **ppInstance);  
    HRESULT GetService(REFIID iid, [out] IUnknown **ppInstance);  
    HRESULT ReplaceVariables(LPCTSTR source, [out] LPBSTR pDest);  
    HRESULT GotoPage(LPCTSTR pageName);  
    int ShowMessageBox(LPCTSTR message, LPCTSTR lpCaption, UINT uType);  
    BOOL InPreview(void);  
    HWND GetHwnd(void);  
};  
```  

##### <a name="overview"></a>Descrição Geral  
 Esta interface está disponível para a página através de **contentor** método (implementado por **WizardPageImpl**) e permite-lhe aceder a vários serviços do assistente.  

##### <a name="ilogger--loggervoid"></a>ILogger * Logger(void)  
 Utilize este método para escrever mensagens para o ficheiro de registo — por exemplo:  

```  
Logger()->Verbose(s_component, L"Message for log file");  
```  

##### <a name="ipropertybag--propertiesvoid"></a>IPropertyBag * Properties(void)  
 Este método fornece acesso a variáveis de "memória", que são as propriedades na memória apenas enquanto o Assistente de UDI está em execução. Estas propriedades estão disponíveis para outras páginas no código ou em XML utilizando o **$memoryVarName$** sintaxe.  

##### <a name="hresult-createinstancelpctstr-type-out-iunknown-ppinstance"></a>HRESULT CreateInstance(LPCTSTR type, [out] IUnknown **ppInstance)  
 Este método permite-lhe criar uma nova instância de qualquer componente que foi registado. No entanto, é melhor utilizar a função de modelo **CreateInstance**, uma vez que é do tipo seguro.  

##### <a name="hresult-getservicerefiid-iid-out-iunknown-ppinstance"></a>HRESULT GetService(REFIID iid, [out] IUnknown **ppInstance)  
 Este método permite-lhe obter um serviço que foi registado. No entanto, é melhor chamar o **GetService** função de modelo, que é do tipo seguro (em vez de utilizar **IUnknown**).  

##### <a name="hresult-replacevariableslpctstr-source-out-lpbstr-pdest"></a>HRESULT ReplaceVariables(LPCTSTR source, [out] LPBSTR pDest)  
 Este método processa a trabalhar com variáveis dentro de valores de cadeia. Suporta os formatos mostrados na tabela 51 e 52 de tabela.  

### <a name="table-51-hresult-replacevariables"></a>51 de tabela. HRESULT ReplaceVariables  

|**Formato**|**Descrição**|  
|-|-|  
|**$Name$**|Substitui o valor de uma variável de memória com este nome (se não houver nenhuma variável de memória com o nome, o "token" será removido.)|  
|**% Name %**|Uma variável de sequência de tarefas ou uma variável de ambiente. A ordem é o seguinte:<br /><br /> 1.  Utilize o valor da variável de sequência de tarefas, se estiver presente.<br />2.  Utilize o valor da variável de ambiente, se estiver presente.<br />3.  Caso contrário, remova este texto da cadeia.|  

### <a name="table-52-hresult-parameter"></a>52 de tabela. Parâmetro HRESULT  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**Origem**|Cadeia de entrada, o que pode conter qualquer combinação de  **$**  e  **%**  variáveis ou none de todo|  
|**pDest**|No retorno, contém uma cadeia nova que tenha todos os tokens substituídos, de acordo com 51 de tabela|  

##### <a name="hresult-gotopagelpctstr-pagename"></a>HRESULT GotoPage(LPCTSTR pageName)  
 Este método ainda não foi totalmente testado. A ideia é que pode alternar diretamente para uma página específica, com base no nome da página, tal como definido no ficheiro XML. config. Chamar este método ignora a **OnNextClicked** da página. Além disso, o comportamento deste método está sujeita a alterações, por isso, utilizá-lo a sua conta e risco.  

##### <a name="int-showmessageboxlpctstr-message-lpctstr-lpcaption-uint-utype"></a>Int ShowMessageBox (mensagem LPCTSTR LPCTSTR lpCaption, UINT uType)  
 Este método apresenta uma caixa de mensagem com o texto e a legenda que fornecer. O **uType** parâmetro é qualquer valor que pode fornecer para o **MessageBox** função Win32.  

##### <a name="bool-inpreviewvoid"></a>BOOL InPreview(void)  
 Este método devolve TRUE se foi iniciado o assistente em modo de "pré-visualização", fornecendo o **/pré-visualizar** mudar. No modo de pré-visualização, o **seguinte** botão nunca está desativado. Este método permite-lhe ignorar um código no modo de pré-visualização, por exemplo, que pode causar problemas quando não tem dados válidos na página.  

##### <a name="hwnd-gethwndvoid"></a>HWND GetHwnd(void)  
 Este método devolve o **HWND** para a caixa de diálogo principal. Utilize este método com cuidado. Geralmente, a interface de programação de aplicação de Assistente de UDI foi concebida para que nunca trabalhar diretamente com identificadores de janela.  

#### <a name="iwizardpageview-interface"></a>IWizardPageView Interface  

```  
__interface IWizardPageView : IUnknown  
{  
    HRESULT GetControlWrapper(int itemId, DialogControlTypes controlType, IUnknown **ppControl);  
    HWND GetHwnd(void);  
    HWND GetControl(int itemId);  
    HRESULT Show (void);  
    HRESULT Hide(void);  
    HRESULT Focus(int itemId);  
    IWizardPage * Page(void);  
    IFormController * Form(void);  

    HRESULT FocusWizardButton(WizardButtons button);  
    HRESULT SetEnable(WizardButtons button, BOOL enable);  
    void ShowWarningMessage(LPCTSTR message);  
    void HideWarningMessage(void);  
};  
```  

 Esta interface está disponível para o código na sua página através de **vista** método (implementado por **WizardPageImpl**).  

##### <a name="hresult-getcontrolwrapperint-itemid-dialogcontroltypes-controltype-iunknown-ppcontrol"></a>HRESULT GetControlWrapper(int itemId, DialogControlTypes controlType, IUnknown \*ppControl)  
 O Assistente de UDI utiliza *wrappers*, que são, de facto façades para interagir com os controlos da página. Utilizando estas façades em vez dos controlos reais torna muito mais fácil escrever testes para a sua página, porque pode fornecer mock façades dos testes.  

 Em vez de utilizar este método diretamente, é melhor utilizar o **GetControlWrapper** método de modelo, que é do tipo seguro — por exemplo:  

```  
PComboBox m_pLanguagePackCombo;  
GetControlWrapper(View(), IDC_MY_COMBO, CONTROL_COMBO_BOX, &m_pCombo);  
```  

##### <a name="hwnd-gethwndvoid"></a>HWND GetHwnd(void)  
 Este método devolve o identificador de janela para a página. Geralmente, não deverá necessitar de acesso para este identificador de janela.  

##### <a name="hwnd-getcontrolint-itemid"></a>HWND GetControl(int itemId)  
 Se necessário, pode chamar este método para obter o identificador de janela para um controlo na página. (É melhor chamar o **GetControlWrapper** da função de modelo).  

##### <a name="hresult-show-void"></a>HRESULT Mostrar (void)  
 Este método é apenas para utilização interna.  

##### <a name="hresult-hidevoid"></a>HRESULT Hide(void)  
 Este método é apenas para utilização interna.  

##### <a name="hresult-focusint-itemid"></a>HRESULT Focus(int itemId)  
 Defina o foco de entrada para um controlo específico.  

##### <a name="iwizardpage--pagevoid"></a>IWizardPage * Page(void)  
 Este método é apenas para utilização interna.  

##### <a name="iformcontroller--formvoid"></a>IFormController * Form(void)  
 Este método é apenas para utilização interna.  

##### <a name="hresult-focuswizardbuttonwizardbuttons-button"></a>HRESULT FocusWizardButton(WizardButtons button)  
 Define o foco para um dos botões do assistente. **WizardButtons** tem dois valores: **BackButton** e **NextButton**.  

##### <a name="hresult-setenablewizardbuttons-button-bool-enable"></a>HRESULT SetEnable(WizardButtons button, BOOL enable)  
 Pedido de um dos botões de assistente estar ativado ou desativado. O botão poderá não corresponder o estado que pedir. Por exemplo, se executar o Assistente de UDI com o **/pré-visualizar** mudar, os botões estará sempre ativados. **WizardButtons** tem dois valores: **BackButton** e **NextButton**.  

##### <a name="void-showwarningmessagelpctstr-message"></a>void ShowWarningMessage(LPCTSTR message)  
 Este método é apresentada uma mensagem de aviso na parte inferior da área de conteúdo de página. Esta mensagem pode ser qualquer texto que pretende.  

##### <a name="void-hidewarningmessagevoid"></a>void HideWarningMessage(void)  
 Ocultar uma mensagem de aviso é apresentado com uma chamada para **ShowWarningMessage**.  

#### <a name="ixmldocument-interface"></a>IXmlDocument Interface  

```  
__interface IXmlDocument : IUnknown  
    HRESULT Load(LPCTSTR filename);  
    HRESULT LoadXml(LPCTSTR xml);  
    HRESULT Save(LPCWSTR filename);  
    HRESULT GetParseErrorMessage(LPBSTR pMessage);  
    HRESULT SelectNodes(LPCTSTR xpath, IXMLDOMNodeList **ppNodes);  
    HRESULT SelectSingleNode(LPCTSTR xpath, IXMLDOMNode **ppNode);  
    HRESULT AddSchema(LPCTSTR filename, LPCTSTR ns);  
    HRESULT AddAttribute(IXMLDOMNode *pNode, LPCWSTR name, LPCWSTR value);  
    HRESULT CreateNode(DOMNodeType type, LPCWSTR name, LPCWSTR ns, IXMLDOMNode **ppNode);  
};  
```  

##### <a name="overview"></a>Descrição Geral  
 Esta interface é implementada pelo **ID_IXmlDocument** componente, que é uma fachada concebida para tornar mais fácil trabalhar com documentos XML em C++.  

##### <a name="hresult-loadlpctstr-filename"></a>HRESULT Load(LPCTSTR filename)  
 Este método carrega um documento XML a partir de um ficheiro externo. Devolve **S_OK** se o ficheiro foi carregado sem erros ou **S_FALSE** se Ocorreu um erro. Quando existe um erro, pode obter a mensagem de erro ao chamar **GetParseErrorMessage**.  

##### <a name="hresult-loadxmllpctstr-xml"></a>HRESULT LoadXml(LPCTSTR xml)  
 Este método carrega um documento XML de uma cadeia em vez de um ficheiro externo. Que não seja a origem para ler o XML, o comportamento é o mesmo que o **carga** método.  

##### <a name="hresult-savelpcwstr-filename"></a>HRESULT Save(LPCWSTR filename)  
 Este método poupa o documento XML que se encontra na memória para um ficheiro externo.  

##### <a name="hresult-getparseerrormessagelpbstr-pmessage"></a>HRESULT GetParseErrorMessage(LPBSTR pMessage)  
 Este método devolve uma cadeia nova com a mensagem de erro de carregar o documento XML, se aplicável. Devolve sempre **S_OK**.  

##### <a name="hresult-selectnodeslpctstr-xpath-ixmldomnodelist-ppnodes"></a>HRESULT SelectNodes(LPCTSTR xpath, IXMLDOMNodeList \**ppNodes)  
 Este método permite-lhe utilizar uma expressão de XPath para obter uma coleção de nós do documento. Devolve sempre **S_OK**.  

##### <a name="hresult-selectsinglenodelpctstr-xpath-ixmldomnode-ppnode"></a>HRESULT SelectSingleNode(LPCTSTR xpath, IXMLDOMNode \**ppNode)  
 Este método permite-lhe utilizar uma expressão de XPath para obter um nó do documento. Devolve sempre **S_OK**.  

##### <a name="hresult-addschemalpctstr-filename-lpctstr-ns"></a>HRESULT AddSchema(LPCTSTR filename, LPCTSTR ns)  
 Este método adiciona o nome de um ficheiro de esquema externo que será utilizado para validar o esquema do seu documento XML ao carregá-lo. O espaço de nomes que fornece é a cadeia pode utilizar consultas XPath, apesar de este ainda não foi testada.  

##### <a name="hresult-addattributeixmldomnode-pnode-lpcwstr-name-lpcwstr-value"></a>HRESULT AddAttribute(IXMLDOMNode \*pNode, LPCWSTR name, LPCWSTR value)  
 Este método adiciona um novo atributo para um nó existente no documento XML. Consulte 53 de tabela.  

### <a name="table-53-hresult-addattribute"></a>53 de tabela. HRESULT AddAttribute  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**pNode**|O nó para o qual pretende adicionar um atributo|  
|**Nome**|Nome do novo atributo|  
|**Valor**|O valor para o atributo novo|  

##### <a name="hresult-createnodedomnodetype-type-lpcwstr-name-lpcwstr-ns-ixmldomnode-ppnode"></a>HRESULT CreateNode(DOMNodeType type, LPCWSTR name, LPCWSTR ns, IXMLDOMNode \**ppNode)  
 Chame este método para criar um novo nó:  

```  
Pointer<IXMLDOMNode> pNewChild  
pXmlDom->CreateNode(NODE_ELEMENT, L"MyElement", L"", &pNewChild);  
```  

 Depois de criar um novo nó, pode adicioná-lo como elemento subordinado para outro nó, chamando o principal **appendChild** método.  

### <a name="helper-functions"></a>Funções de programa auxiliar  

#### <a name="createinstance-template-function"></a>Função de modelo de CreateInstance  

```  
HRESULT CreateInstance(IWizardPageContainer *pContainer, LPCTSTR type, I **ppObject)  
```  

 Esta função está definida no IWizardPageContainer.h e fornece um dispositivo de moldagem de tipo seguro relativamente a **IWizardPageContainer -> CreateInstance** método — por exemplo:  

```  
CreateInstance<IDirectory>(Container(), ID_Directory, &pDirectory);  
```  

 Este código cria um novo **ID_Directory** componente para obter o **IDirectory** interface desse componente.  

#### <a name="getservice-template-function"></a>Função de modelo GetService  

```  
void GetService(IWizardPageContainer *pContainer, I **ppService)  
```  

 Esta função está definida no IWizardPageContainer.h e fornece um dispositivo de moldagem de tipo seguro relativamente a **IWizardPageContainer -> GetService** método — por exemplo:  

```  
GetService<ITSVariableBag>(Container(), &pTsBag);  
```  

 Esta função obtém o componente de sequência de tarefas, que suporta o **ITSVariableBag** interface. (Para **ITSVariableBag**, pode utilizar o método TSVariables o **WizardPageImpl** classe, em vez disso.)  

### <a name="udi-wizard-designer-configuration-file-schema-reference"></a>Referência de esquema de ficheiro de configuração estruturador de assistente UDI  
 Este ficheiro é consumido pelo UDI Wizard Designer. É criado um ficheiro separado para cada ficheiro. dll personalizada, o que pode conter editores de página do assistente personalizado, tarefas personalizadas ou validações personalizadas. O ficheiro tem de terminar com *. config* e residem no *installation_folder*\Bin\Config pasta (onde *installation_folder* é a pasta na qual instalou o MDT).  

  54 em que tabela apresenta os elementos no ficheiro de configuração de UDI Wizard Designer e as respetivas descrições. O **DesignerConfig** elemento é o nó de raiz para esta referência.  

### <a name="table-54-elements-in-the-udi-wizard-designer-configuration-file-and-their-descriptions"></a>54 em tabela. Elementos do ficheiro de configuração estruturador do assistente UDI e as respetivas descrições  

|**Nome do elemento**|**Descrição**|  
|-|-|  
|[DesignerConfig](#DesignerConfig)|Especifica a raiz para todos os outros elementos|  
|[DesignerMappings](#DesignerMappings)|Grupos de um conjunto de [página](#Page)elementos|  
|[Página](#Page)|Especifica um editor de página do Assistente para ser carregado no UDI Wizard Designer, que é utilizada para editar as definições de configuração para uma página do Assistente|  
|[Param](#Param)|Especifica um parâmetro que é transferido para o elemento principal [tarefas](#Task) ou [validador](#Validator) elemento e corresponde a um [Setter]() elemento no ficheiro de configuração do Assistente de UDI **Nota:**  Os atributos para este elemento são diferentes, se o principal já se encontra o [tarefas](#Task) ou [validador](#Validator) elemento.|  
|[Tarefa](#Task)|Especifica uma tarefa na biblioteca de tarefas|  
|[TaskItem](#TaskItem)|Especifica um grupo de parâmetros que são transmitidos para a tarefa|  
|[TaskLibrary](#TaskLibrary)|Grupos de um conjunto de [tarefas](#Task) elementos|  
|[A validação do](#Validator)|Especifica a validação na biblioteca de validação|  
|[ValidatorLibrary](#ValidatorLibrary)|Grupos de um conjunto de [validador](#Validator) elementos|  

####  <a name="DesignerConfig"></a>DesignerConfig  
 Este elemento Especifica a raiz para todos os outros elementos.  

##### <a name="element-information"></a>Informação de elemento  
  Tabela 55 fornece informações sobre o [DesignerConfig](#DesignerConfig) elemento.  

### <a name="table-55-designerconfig-element-information"></a>55 de tabela. Informação de elemento DesignerConfig  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Um: Este elemento é necessário.|  
|Elementos principais|Nenhum|  
|Conteúdo|**DesignerMappings**, **TaskLibrary**, **ValidatorLibrary**|  

##### <a name="element-attributes"></a>Atributos de elemento  
 Este elemento tem sem atributos.  

##### <a name="remarks"></a>Observações  
 Nenhuma.  

##### <a name="example"></a>Exemplo  

```  
<DesignerConfig>  
   + <TaskLibrary>  
   + <ValidatorLibrary>  
   + <DesignerMappings>  
</DesignerConfig>  
```  

####  <a name="DesignerMappings"></a>DesignerMappings  
 Este elemento de um conjunto de grupos [página](#Page) elementos.  

##### <a name="element-information"></a>Informação de elemento  
  Tabela 56 fornece informações sobre o [DesignerMappings](#DesignerMappings) elemento.  

### <a name="table-56-designermappings-element-information"></a>56 de tabela. Informação de elemento DesignerMappings  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Zero ou um dentro de [DesignerConfig](#DesignerConfig) elemento (este elemento é opcional não se existirem nenhuma página do assistente personalizado na DLL que corresponde a este ficheiro de configuração de UDI Wizard Designer.)|  
|Elementos principais|**DesignerConfig**|  
|Conteúdo|**Página**|  

##### <a name="element-attributes"></a>Atributos de elemento  
 Este elemento tem sem atributos.  

##### <a name="remarks"></a>Observações  
 Nenhuma.  

##### <a name="example"></a>Exemplo  

```  
<DesignerConfig>  
   + <TaskLibrary>  
   + <ValidatorLibrary>  
   - <DesignerMappings>  
        <Page DLL="SharedPages.dll"  
           Description="Used to display text that describes the current stagegroup"  
           Type="Microsoft.SharedPages.WelcomePage"  
           DisplayName="Welcome"   
           Image="Welcome_188.png"  
           DesignerType="Microsoft.Enterprise.UDIDesigner.CoreModules.Views.WelcomePageView"  
           DesignerAssembly="Microsoft.Enterprise.UDIDesigner.CoreModules.dll"/>  
        <Page DLL="OSDRefreshWizard.dll"  
           Description="Captures or restores user state data"  
           Type="Microsoft.OSDRefresh.UserStatePage"  
           DisplayName="User Data"  
           Image="UserState_188.png"  
           DesignerType="Microsoft.Enterprise.UDIDesigner.CoreModules.Views.UserStatePageView"  
           DesignerAssembly="Microsoft.Enterprise.UDIDesigner.CoreModules.dll"/>  
        <Page DLL="OSDRefreshWizard.dll"  
           Description="Allows selecting the image to install, target drive, and whether to format"  
           Type="Microsoft.OSDRefresh.VolumePage"  
           DisplayName="Volume"  
           Image="Volume_188.png"  
           DesignerType="Microsoft.Enterprise.UDIDesigner.CoreModules.Views.VolumePageView"  
           DesignerAssembly="Microsoft.Enterprise.UDIDesigner.CoreModules.dll"/>  
     </DesignerMappings>  
</DesignerConfig>  
```  

####  <a name="Page"></a>Página  
 Este elemento Especifica um editor de página do Assistente para ser carregado no UDI Wizard Designer, que por sua vez é utilizada para editar as definições de configuração para uma página do assistente.  

##### <a name="element-information"></a>Informação de elemento  
Tabela 57 fornece informações sobre o [página](#Page) elemento.  

### <a name="table-57-page-element-information"></a>57 de tabela. Informação de elemento da página  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Um ou mais para cada página do assistente definido no [DesignerMappings](#DesignerMappings) elemento|  
|Elementos principais|**DesignerMappings**|  
|Conteúdo|Qualquer conteúdo XML corretamente formado|  

##### <a name="element-attributes"></a>Atributos de elemento  
58 tabela lista os atributos do [página](#Page) elemento e uma descrição para cada.  

### <a name="table-58-attributes-and-corresponding-values-for-the-page-element"></a>58 de tabela. Atributos e valores correspondentes para o elemento da página  

|**Atributo**|**Descrição**|  
|-|-|  
|**Descrição**|Especifica o texto que fornece informações sobre o parâmetro que é apresentado no UDI Wizard Designer|  
|**DesignerAssembly**|Especifica o nome do ficheiro. dll associado com o editor de página do assistente (o ficheiro. dll tem de existir o *installation_folder*pasta \Bin (onde *installation_folder* é a pasta na qual a MDT instalado.)|  
|**DesignerType**|Especifica o nome do editor de página do assistente no ficheiro. dll especificado no **DesignerAssembly** atributo (este é o tipo de Microsoft .NET para o editor de página do assistente, com o espaço de nomes do Microsoft .NET completamente qualificado.)|  
|**DisplayName**|Especifica o nome amigável de utilizador do editor de página, é apresentado no UDI Wizard Designer|  
|**DLL**|Especifica o nome do ficheiro. dll associado com a página do assistente (o ficheiro. dll tem de existir o *installation_folder*\Templates\Distribution\Tools\\*plataforma* pasta (onde *installation_folder* é a pasta na qual instalou o MDT e *plataforma* é **x86** para a versão de 32 bits ou **x64** é para a versão de 64 bits.) **Nota:**  Certifique-se de que a arquitetura de processador DLL corresponde à arquitetura do processador MDT instalada. Por exemplo, se tiver instalado uma versão de 32 bits do MDT, em seguida, certifique-se de que utiliza um DLL de 32 bits para a página do assistente.|  
|**Imagem**|Especifica o nome de uma imagem da página que está no formato Portable rede gráficos (PNG) (o ficheiro PNG tem de existir o *installation_folder*\Bin\Images pasta (onde *installation_folder* é o pasta na qual instalou o MDT.)|  
|**Tipo**|Especifica o editor de página do assistente e tem de corresponder ao nomeado utilizado quando a página personalizada foi registada|  

##### <a name="remarks"></a>Observações  
 O UDI Wizard Designer utiliza o [página](#Page) elemento como um modelo para criar o XML inicial de um Assistente de novo. O UDI Wizard Designer efetua a validação de esquema para se certificar de que o [página](#Page) e elementos subordinados têm um formato válido. Este elemento fornece um mapeamento entre o tipo de página do Assistente de UDI e as informações que o UDI Wizard Designer tem de editar e criar páginas deste tipo com um editor de página personalizada.  

##### <a name="example"></a>Exemplo  
 Nenhuma.  

####  <a name="Param"></a>Param  
 Este elemento Especifica um parâmetro que é transferido para o elemento principal [tarefas](#Task) ou [validador](#Validator) elemento e corresponde a um [Setter]() elemento no ficheiro de configuração do Assistente de UDI.  

> [!NOTE]
>  Os atributos para este elemento são diferentes, se o principal já se encontra o [tarefas](#Task) ou [validador](#Validator) elemento.  

##### <a name="element-information"></a>Informação de elemento  
 Tabela 59 fornece informações sobre o [Param](#Param) elemento.  

### <a name="table-59-param-element-information"></a>Tabela 59. Informação de elemento param  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Um ou mais para cada [TaskItem](#TaskItem) ou [validador](#Validator) elemento principal|  
|Elementos principais|**TaskItem**, **validador**|  
|Conteúdo|Qualquer conteúdo XML corretamente formado|  

##### <a name="element-attributes"></a>Atributos de elemento  
  60 tabela lista os atributos do [Param](#Param) elemento e fornece uma descrição de cada.  

### <a name="table-60-attributes-and-corresponding-values-for-the-param-element"></a>60 de tabela. Atributos e valores correspondentes para o elemento de Param  

|**Atributo**|**Descrição**|  
|-|-|  
|**Descrição**|Especifica o texto que fornece informações sobre o parâmetro que é apresentado no UDI Wizard Designer **Nota:**  Este atributo só é válido para o [validador](#Validator) elemento.|  
|**DisplayName**|Especifica o nome amigável de utilizador do parâmetro de validação, o que é apresentado para a página do Assistente de UDI adequada no UDI Wizard Designer (este nome é normalmente mais descritivo do que o **nome** atributos.) **Nota:**  Este atributo só é válido para o [validador](#Validator) elemento.|  
|**Nome**|Especifica o nome do parâmetro que é transmitido para a tarefa ou a validação do, consoante o elemento principal (este atributo irá tornar-se a **propriedade** atributo num [Setter]() elemento no Assistente de UDI ficheiro de configuração.) **Nota:**  Este parâmetro é utilizado para [TaskItem](#TaskItem) e [validador](#Validator) principais elementos.|  

##### <a name="remarks"></a>Observações  
 Nenhuma.  

##### <a name="example"></a>Exemplo  
 Nenhuma.  

####  <a name="Task"></a>Tarefa  
 Este elemento Especifica uma tarefa na biblioteca de tarefas.  

##### <a name="element-information"></a>Informação de elemento  
 Tabela 61 fornece informações sobre o [tarefas](#Task) elemento.  

### <a name="table-61-task-element-information"></a>61 de tabela. Informação de elemento de tarefa  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Um ou mais dentro de [TaskLibrary](#TaskLibrary) elemento (este elemento não é opcional se a **TaskLibrary** elemento é especificado.)|  
|Elementos principais|**TaskLibrary**|  
|Conteúdo|**TaskItem**|  

##### <a name="element-attributes"></a>Atributos de elemento  
  62 tabela lista os atributos do [tarefas](#Task) elemento e fornece uma descrição de cada.  

### <a name="table-62-attributes-and-corresponding-values-for-the-task-element"></a>62 de tabela. Atributos e valores correspondentes para o elemento de tarefa  

|**Atributo**|**Descrição**|  
|-|-|  
|**Descrição**|Especifica o texto que fornece informações sobre a tarefa, o que é apresentada no UDI Wizard Designer|  
|**DLL**|Especifica o nome do ficheiro. dll associado com a tarefa (o ficheiro. dll tem de existir o *installation_folder*\Templates\Distribution\Tools\\*plataforma* pasta (onde *installation_folder* é a pasta na qual instalou o MDT e *plataforma* é **x86** para a versão de 32 bits ou **x64** para a 64 -versão de bits.)|  
|**Nome**|Especifica o nome da tarefa, que é apresentado na página do Assistente de UDI adequada e o UDI Wizard Designer|  
|**Tipo**|Especifica o tipo de tarefa, o que é registado com o registo de fábrica e utilizado para chamar uma tarefa específica dentro de um ficheiro. dll|  

##### <a name="remarks"></a>Observações  
 Nenhuma.  

##### <a name="example"></a>Exemplo  
 Nenhuma.  

####  <a name="TaskItem"></a>TaskItem  
 Este elemento Especifica um grupo de parâmetros que são transmitidos para a tarefa.  

##### <a name="element-information"></a>Informação de elemento  
  Tabela 63 fornece informações sobre o [TaskItem](#TaskItem) elemento.  

### <a name="table-63-taskitem-element-information"></a>Tabela 63. Informação de elemento TaskItem  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Um ou mais para cada **tarefas** elemento|  
|Elementos principais|**Tarefa**|  
|Conteúdo|**Param**|  

##### <a name="element-attributes"></a>Atributos de elemento  
 64 tabela lista os atributos do [TaskItem](#TaskItem) elemento e fornece uma descrição de cada.  

### <a name="table-64-attribute-and-corresponding-values-for-the-taskitem-element"></a>Tabela 64. Atributos e valores correspondentes para o elemento de TaskItem  

|**Atributo**|**Descrição**|  
|-|-|  
|**Tipo**|Especifica o tipo de elemento que será criado no ficheiro de configuração do Assistente de UDI. Será possível criar um elemento XML que corresponde ao valor deste atributo. Por exemplo, se o valor para este atributo é [ficheiro](#File), em seguida, um **ficheiro** elemento será criado no ficheiro de configuração do Assistente de UDI.<br /><br /> Atualmente, os únicos valores suportados são:<br /><br /> -   **Ficheiro**, que requer dois [Param](#Param) elementos subordinados (um **Param** elemento subordinado com o **nome** atributo definido como **origem** e outro **Param** elemento subordinado com o **nome** atributo definido como **Dest**)<br />-   [Setter](), que requer um **Param** elemento subordinado|  

##### <a name="remarks"></a>Observações  
 Nenhuma.  

##### <a name="example"></a>Exemplo  
 Nenhuma.  

####  <a name="TaskLibrary"></a>TaskLibrary  
 Este elemento de um conjunto de grupos [tarefas](#Task) elementos.  

##### <a name="element-information"></a>Informação de elemento  
 Tabela 65 fornece informações sobre o [TaskLibrary](#TaskLibrary) elemento.  

### <a name="table-65-tasklibrary-element-information"></a>65 de tabela. Informação de elemento TaskLibrary  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Zero ou um dentro de [DesignerConfig](#DesignerConfig) elemento (este elemento é opcional se existem não existem tarefas personalizadas na DLL do que correspondem a este ficheiro de configuração de UDI Wizard Designer.)|  
|Elementos principais|**DesignerConfig**|  
|Conteúdo|**Tarefa**|  

##### <a name="element-attributes"></a>Atributos de elemento  
 Este elemento tem sem atributos.  

##### <a name="remarks"></a>Observações  
 Nenhuma.  

##### <a name="example"></a>Exemplo  

```  
<DesignerConfig>  
   - <TaskLibrary>  
        +<Task DLL="" Description="Executes a process with the given command line." Type="Microsoft.Wizard.ShellExecuteTask" Name="Shell Execute Task">  
        +<Task DLL="OSDRefreshWizard.dll" Description="Discovers supported applications for install." Type="Microsoft.OSDRefresh.AppDiscoveryTask" Name="Application Discovery">  
        +<Task DLL="SharedPages.dll" Description="Check to ensure a wired network connection is available." Type="Microsoft.SharedPages.WiredNetworkTask" Name="Wired Network Check">  
        +<Task DLL="OSDRefreshWizard.dll" Description="Check to ensure power source is AC (not battery)." Type="Microsoft.OSDRefresh.ACPowerTask" Name="AC Power Check">  
        +<Task DLL="" Description="Check to ensure power source is AC (not battery)." Type="Microsoft.Wizard.CopyFilesTask" Name="Copy Files Task">  
     </TaskLibrary>  
   + <ValidatorLibrary>  
   + <DesignerMappings>  
</DesignerConfig>  
```  

####  <a name="Validator"></a>A validação do  
 Este elemento Especifica um validador na biblioteca do validador.  

##### <a name="element-information"></a>Informação de elemento  
 Tabela 66 fornece informações sobre o [validador](#Validator) elemento.  

### <a name="table-66-validator-element-information"></a>66 de tabela. Informações de elemento do validador  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Zero ou mais dentro de [ValidatorLibrary](#ValidatorLibrary) elemento (este elemento é opcional.)|  
|Elementos principais|**ValidatorLibrary**|  
|Conteúdo|**Param**|  

##### <a name="element-attributes"></a>Atributos de elemento  
67 tabela lista os atributos do [validador](#Validator) elemento e fornece uma descrição de cada.  

### <a name="table-67-attributes-and-corresponding-values-for-the-validator-element"></a>Tabela 67. Atributos e valores correspondentes para o elemento de validação  

|**Atributo**|**Descrição**|  
|-|-|  
|**Descrição**|Especifica o texto que fornece informações sobre a validação, o que é apresentada no UDI Wizard Designer|  
|**DisplayName**|Especifica o nome amigável de utilizador do validador apresentado no UDI Wizard Designer (este nome é normalmente mais descritivo do que o **nome** atributos.)|  
|**DLL**|Especifica o nome do ficheiro. dll associado o validador (o ficheiro. dll tem de existir o *installation_folder*\Templates\Distribution\Tools\\*plataforma* pasta (onde *installation_folder* é a pasta na qual instalou o MDT e *plataforma* é **x86** para a versão de 32 bits ou **x64** para a versão de 64 bits.)|  
|**Nome**|Especifica o nome de validação, o que é apresentado na página do Assistente de UDI adequada e o UDI Wizard Designer|  
|**Tipo**|Especifica o tipo de validação, o que é registado com o fator de registo e utilizado para chamar um validador específico dentro de um ficheiro. dll|  

##### <a name="remarks"></a>Observações  
 Nenhuma.  

##### <a name="example"></a>Exemplo  
 Nenhuma.  

####  <a name="ValidatorLibrary"></a>ValidatorLibrary  
 Este elemento de um conjunto de grupos [validador](#Validator) elementos.  

##### <a name="element-information"></a>Informação de elemento  
 Tabela 68 fornece informações sobre o [ValidatorLibrary](#ValidatorLibrary) elemento.  

### <a name="table-68-validatorlibrary-element-information"></a>68 de tabela. Informação de elemento ValidatorLibrary  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Zero ou um dentro de [DesignerConfig](#DesignerConfig) elemento (este elemento é opcional se existirem não validações personalizadas na DLL do que correspondem a este ficheiro de configuração de UDI Wizard Designer.)|  
|Elementos principais|**DesignerConfig**|  
|Conteúdo|**A validação do**|  

##### <a name="element-attributes"></a>Atributos de elemento  
 Este elemento tem sem atributos.  

##### <a name="remarks"></a>Observações  
 Nenhuma.  

##### <a name="example"></a>Exemplo  
 < DesignerConfig\> + < TaskLibrary\> -< ValidatorLibrary\> + < DLL de validador = "" Descrição = "Necessita de texto num campo" Type="Microsoft.Wizard.Validation.NonEmpty" Name = "NonEmpty"\> + < a validação do DLL = "" Descrição = "Não permitir que determinados caracteres de ser um campo" Type="Microsoft.Wizard.Validation.InvalidChars" Name = "InvalidChars"\> + < DLL de validação do = "" Descrição = "Tem de seguir um padrão de pré-definido" tipo = " Microsoft.Wizard.Validation.RegEx"Name ="NamedPattern"\> + < DLL de validação do =" "Descrição ="Exigir o conteúdo corresponde a uma expressão regular"Type="Microsoft.Wizard.Validation.RegEx "Name ="RegEx"\> < / ValidatorLibrary\> + < DesignerMappings\>< / DesignerConfig\>  

## <a name="udi-wizard-designer-reference"></a>Referência de estruturador de assistente UDI  

### <a name="controls"></a>controlos  
 Os controlos utilizados para criar a página do assistente personalizado editores para utilização no UDI Wizard Designer são WPF **UserControl** instâncias. 69 tabela lista os controlos que pode utilizar para criar editores de página do assistente personalizado.  

### <a name="table-69-controls-that-can-be-used-to-create-custom-wizard-page-editors"></a>69 de tabela. Controlos que podem ser utilizados para criar editores de página do assistente personalizado  

|Controlo|Descrição|  
|-|-|  
|[CollectionTControl](#CollectionTControl)|Este controlo é utilizado para editar os dados armazenados no [dados](#Data) elemento dentro de um [página](#Page) elemento.|  
|[FieldElementControl](#FieldElementControl)|Este controlo é utilizado para editar um campo, o que normalmente está ligado a um controlo de caixa de texto na página primeiro.|  
|[SetterControl](#SetterControl)|Este controlo é utilizado para modificar o valor de um [setter]() elemento no ficheiro de configuração do Assistente de UDI.|  

####  <a name="CollectionTControl"></a>CollectionTControl  
 Este controlo oferece muitas funcionalidades de dados de edição. A melhor forma de aprender a utilizar este controlo está a observar o exemplo que mostra como editar dados de uma página **dados** elemento. Em particular, o exemplo mostra como adicionar, remover e editar itens neste controlo.  

####  <a name="FieldElementControl"></a>FieldElementControl  
 Utilize este controlo para editar um campo, o que normalmente está ligado a um **TextBox** controlo na página primeiro.  

##### <a name="example"></a>Exemplo  
 O excerpt seguinte a partir de um ficheiro de primeiro ilustra a utilização do **FieldElementControl** para configurar o valor predefinido para um campo numa página do assistente com um elemento subordinado **TextBox** controlo:  

```  
<Controls:FieldElementControl  
Width="450"  
Margin="0,5"  
FieldData="{Binding DataContext.Location, ElementName=ControlRoot}"  
HeaderText="Location Combo Box"  
InstructionText="Here you can configure the behavior of the location combo box."  
HideValidationTab="True">  

<TextBox Text="{Binding FieldData.DefaultValue,  
 UpdateSourceTrigger=PropertyChanged,  
 Mode=TwoWay}"/>  
</Controls:FieldElementControl>  
```  

##### <a name="properties"></a>Propriedades  

###### <a name="fielddata"></a>FieldData  
 Esta propriedade de cadeia contém informações para ligar o **FieldElementControl** ao XML subjacente para o campo. A ligação é efetuada para uma propriedade da interface do editor de página. O excerpt seguinte a partir de um ficheiro de primeiro ilustra a utilização do **FieldData** propriedade:  

```  
FieldData="{Binding DataContext.Location, ElementName=ControlRoot}"  
```  

 Este excerpt, a interface do editor de página é designada **ControlRoot** e está especificado no **ElementName** parâmetro. O enlace é efetuado para a **DataContext.Location** propriedade o **ControlRoot** interface do editor de página. **DataContext** é um modelo de vista que aponta para o [página](#Page) elemento no ficheiro de configuração de Assistente de UDI. **Localização** é uma propriedade da vista que devolve uma lista das localizações possíveis e é definida por um [dados](#Data) elemento no ficheiro de configuração de Assistente de UDI. Cada localização é definida por um [DataItem](#DataItem) elemento no ficheiro de configuração de Assistente de UDI.  

###### <a name="headertext"></a>HeaderText  
 Esta propriedade de cadeia permite-lhe especificar um cabeçalho para o [FieldElementControl](#FieldElementControl) controlo. O cabeçalho age como um título para o controlo e é formatado como texto negrito, laranja imediatamente apresentado acima do controlo.  

###### <a name="instructiontext"></a>InstructionText  
 Esta propriedade de cadeia permite-lhe especificar informativo texto para o [FieldElementControl](#FieldElementControl) controlo. Normalmente, o texto é utilizado para fornecer uma breve descrição do campo e explicam como configurar o campo afeta a página do assistente correspondente.  

###### <a name="hideenablebutton"></a>HideEnableButton  
 Esta propriedade booleana permite-lhe controlar a visibilidade do botão muda de estado entre **Unlocked** e **está bloqueado** (ativada ou desativada). Se definido como:  

-   **Verdadeiro**, o botão não está visível  

-   **FALSO**, o botão está visível (este é o valor predefinido.)  

###### <a name="hidedefaulttab"></a>HideDefaultTab  
 Esta propriedade booleana permite-lhe controlar a visibilidade da secção que contém o controlo utilizado para definir o valor predefinido. Embora a propriedade se refere a um separador, não há nenhum separador no [FieldElementControl](#FieldElementControl) , mas sim uma secção que pode ser ocultada. Se definido como:  

-   **Verdadeiro**, a secção não é visível  

-   **FALSO**, a secção está visível (este é o valor predefinido.)  

###### <a name="hideborder"></a>HideBorder  
 Esta propriedade booleana permite-lhe controlar a visibilidade do limite em redor do controlo de campo. Se definido como:  

-   **Verdadeiro**, limite não está visível  

-   **FALSO**, o limite é visível (este é o valor predefinido.)  

###### <a name="hideimage"></a>HideImage  
 Esta propriedade booleana permite controlar a visibilidade da imagem que o **FieldImageSource** configura a propriedade. Se definido como:  

-   **Verdadeiro**, a imagem não está visível  

-   **FALSO**, a imagem é visível (este é o valor predefinido.)  

###### <a name="hidevalidationtab"></a>HideValidationTab  
 Esta propriedade booleana permite-lhe controlar a visibilidade da secção em que é gerida a lista de validações. Embora a propriedade se refere a um separador, não há nenhum separador no [FieldElementControl](#FieldElementControl) , mas sim uma secção que pode ser ocultada. Se definido como:  

-   **Verdadeiro**, a secção não é visível  

-   **FALSO**, a secção está visível (este é o valor predefinido.)  

###### <a name="hidesummarytab"></a>HideSummaryTab  
 Esta propriedade booleana permite-lhe controlar a visibilidade da secção na qual pode configura a legenda de resumo de campo. O valor correspondente do campo e de legenda são apresentados num **SummaryPage** tipo de página do assistente no fluxo de fase. Embora a propriedade se refere a um separador, não há nenhum separador no [FieldElementControl](#FieldElementControl) , mas sim uma secção que pode ser ocultada. Se definido como:  

-   **Verdadeiro**, a secção não é visível  

-   **FALSO**, a secção está visível (este é o valor predefinido.)  

###### <a name="hidetasksequencetab"></a>HideTaskSequenceTab  
 Esta propriedade booleana permite-lhe controlar a visibilidade da secção na qual pode configura a variável de sequência de tarefas que corresponde ao campo. Embora a propriedade se refere a um separador, não há nenhum separador no [FieldElementControl](#FieldElementControl) , mas sim uma secção que pode ser ocultada. Se definido como:  

-   **Verdadeiro**, a secção não é visível  

-   **FALSO**, a secção está visível (este é o valor predefinido.)  


####  <a name="SetterControl"></a>SetterControl  
 Utilize este controlo para modificar o valor de um [Setter]() elemento no ficheiro de configuração do Assistente de UDI. Este controlo contém um controlo subordinado utilizado para modificar o valor da **setter** elemento.  

##### <a name="example"></a>Exemplo  
 O excerpt seguinte a partir de um ficheiro de primeiro ilustra a utilização do **SetterControl** para modificar um [Setter]() elemento com o nome **KeyLocationSetter** utilizando um subordinado **TextBox** controlo.  

```  
<Controls:SetterControl Margin="5"  
        Width="450"  
        HeaderText="Title text"  
        SetterData="{Binding KeyLocationSetter}"   
        InstructionText="What this means…"  
        HorizontalAlignment="Left">  

    <TextBox  
                   Margin="0,3"  
                   Text="{Binding SetterData.SetterValue, Mode=TwoWay, UpdateSourceTrigger=PropertyChanged}"  
    />  

</Controls:SetterControl>  
```  

##### <a name="properties"></a>Propriedades  

###### <a name="setterdata"></a>SetterData  
 Tem de vincular isto a uma propriedade da vista ou do modelo de vista que liga o setter. Se o fizer, é semelhante à forma como iria vincular a um campo, conforme descrito para o **FieldElementControl**.  

###### <a name="headertext"></a>HeaderText  
 Esta propriedade permite-lhe definir o texto que será apresentado no cabeçalho do controlo. Considerar desta propriedade como um título para o controlo; Por predefinição, é apresentada como texto negrito, laranja.  

###### <a name="instructiontext"></a>InstructionText  
 Defina esta propriedade como o texto que pretende ver apresentado abaixo o cabeçalho — normalmente, o texto de instrução que informa o utilizador do seu editor personalizado quando e por que motivo seja pretenda modificar o comportamento do campo.  

### <a name="interfaces"></a>Interfaces  
70 tabela lista as interfaces que pode utilizar para criar editores de página do assistente personalizado.  

### <a name="table-70-interfaces-that-can-be-used-to-create-custom-wizard-page-editors"></a>Tabela 70. Interfaces que podem ser utilizadas para criar editores de página do assistente personalizado  

|**Interface**|**Descrição**|  
|-|-|  
|[IDataService](#IDataService)|Utilize esta interface para ligar os campos para o **dados** elementos no ficheiro de configuração do Assistente de UDI.|  
|[IMessageBoxService](#IMessageBoxService)|Esta interface fornece acesso aos métodos que pode utilizar para apresentar as caixas de mensagem.|  

####  <a name="IDataService"></a>IDataService  
 Esta interface contém vários métodos e propriedades, mas não existe apenas uma propriedade que são como precisam. Se a propriedade é a única documentada aqui.  

 Pode utilizar a inserção de dependências para obter um ponteiro para esta interface com o código como esta na sua classe:  

```  
[Dependency]  
public IDataService DataService { get; set; }  
```  

##### <a name="properties"></a>Propriedades  
 71 tabela lista as propriedades do **IDataService** interface.  

### <a name="table-71-properties-for-the-idataservice-interface"></a>71 de tabela. Propriedades para a Interface IDataService  

|**Interface**|**Descrição**|  
|-|-|  
|[CurrentPage](#CurrentPage)|Esta propriedade fornece acesso aos elementos XML, atributos e valores sob o contexto da página atual a ser editado no ficheiro de configuração do Assistente de UDI|  

######  <a name="CurrentPage"></a>CurrentPage  

```  
XElement CurrentPage { get; set; }  
```  

 Esta propriedade fornece acesso ao XML para a página atual. Nunca deverá definir esta propriedade, mas está livres modificar o XML para a página. O editor da página de exemplo mostra exemplos de modificar o XML. Utilize esta propriedade principalmente quando tiver dados personalizados. Para os campos e propriedades (setters), pode utilizar os controlos de prebuilt asseguramos todos os detalhes.  

####  <a name="IMessageBoxService"></a>IMessageBoxService  
 Esta interface fornece acesso aos métodos que pode utilizar para apresentar as caixas de mensagem. -Pode estar a pensar por que motivo precisa de uma interface para apresentar uma caixa de mensagem. A realidade é que não o fizer: A Microsoft utiliza esta interface no código, porque esta ajuda na escrita testes automáticos para páginas estruturador.  

 No entanto, utilizar esses métodos benefício um úteis: As caixas de diálogo tem sempre o "proprietário" definido para o Assistente de UDI, que garante que a caixa de diálogo é agrupada corretamente com a janela principal.  

 Pode utilizar a inserção de dependências para obter um ponteiro para esta interface com o código como esta na sua classe:  

```  
[Dependency]  
public IMessageBoxService MessageBoxes { get; set; }  
```  

##### <a name="methods"></a>Métodos  
 72 tabela lista os métodos para a **IMessageBoxService** interface.  

### <a name="table-72-methods-for-the-imessageboxservice-interface"></a>72 de tabela. Métodos para a Interface IMessageBoxService  

|**Método**|**Descrição**|  
|-|-|  
|[ShowMessageBox](#ShowMessageBox)|Este método sobrecarregado é utilizado para apresentar uma caixa de mensagem com os seguintes membros:<br /><br /> -   [ShowMessageBox (String mensagem legenda de cadeia, MessageBoxImage ícone)](#ShowMessageBox_Stringmessage_Stringcaption_MessageBoxImage_icon)<br />-   [ShowMessageBox (string mensagem legenda de cadeia, MessageBoxButton botão, o ícone de MessageBoxImage)](#ShowMessageBox_stringmessage_stringcaption_MessageBoxButtonbutton_MessageBoxImage_icon)<br />-   [ShowMessageBox (exceção exceção)](#ShowMessageBox_Exception_exception)|  
|[ShowDialogWindow](#ShowDialogWindow)|Utilize este método para criar uma caixa de diálogo de novo.|  
|[ShowWizardWindow](#ShowWizardWindow)|Utilize este método para apresentar um editor de personalizado no interior de uma caixa de diálogo inclui **seguinte** e **novamente** botões de navegação.|  

######  <a name="ShowMessageBox"></a>ShowMessageBox  
 Este método apresenta uma caixa de mensagem que é um elemento subordinado do editor de página do assistente personalizado. Este membro está sobrecarregado: Tabela 73 contém uma lista de membros e uma descrição breve de cada. Para obter informações completas sobre cada membro (incluindo sintaxe, utilização e exemplos), consulte a secção que corresponde a cada membro.  

### <a name="table-73-overloaded-members-for-the-showmessagbox-method"></a>73 de tabela. Membros sobrecarregados para o método ShowMessagBox  

|Membro|Descrição|  
|-|-|  
|[ShowMessageBox (String mensagem legenda de cadeia, MessageBoxImage ícone)](#ShowMessageBox_Stringmessage_Stringcaption_MessageBoxImage_icon)|Apresenta uma caixa de mensagem com um ícone e uma **OK** botão|  
|[ShowMessageBox (string mensagem legenda de cadeia, MessageBoxButton botão, o ícone de MessageBoxImage)](#ShowMessageBox_stringmessage_stringcaption_MessageBoxButtonbutton_MessageBoxImage_icon)|Apresenta uma caixa de mensagem com um ícone e diferentes combinações possíveis dos botões|  
|[ShowMessageBox (exceção exceção)](#ShowMessageBox_Exception_exception)|Apresenta uma caixa de mensagem que fornece informações sobre uma exceção e tem um **OK** botão|  

######  <a name="ShowMessageBox_Stringmessage_Stringcaption_MessageBoxImage_icon"></a>ShowMessageBox (String mensagem legenda de cadeia, MessageBoxImage ícone)  

```  
void ShowMessageBox(String message, String caption, MessageBoxImage icon);  
```  

 Este método apresenta uma caixa de mensagem com um **OK** botão. Consulte 74 de tabela.  

### <a name="table-74-parameters-for-the-showmessageboxstring-message-string-caption-messageboximage-icon-method"></a>74 de tabela. Parâmetros para o método ShowMessageBox(String message, String caption, MessageBoxImage icon)  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**mensagem**|A mensagem a apresentar na área de conteúdo da caixa de mensagem|  
|**Legenda**|O texto a mostrar na barra de título da caixa de diálogo|  
|**ícone**|O tipo do ícone para mostrar na caixa de mensagem|  

######  <a name="ShowMessageBox_stringmessage_stringcaption_MessageBoxButtonbutton_MessageBoxImage_icon"></a>ShowMessageBox (string mensagem legenda de cadeia, MessageBoxButton botão, o ícone de MessageBoxImage)  

```  
MessageBoxResult ShowMessageBox(string message, string caption, MessageBoxButton button, MessageBoxImage icon);  
```  

 Este método apresenta uma caixa de mensagem com o conjunto de botões a apresentar e relatórios que botão é clicado. Consulte a tabela 75.  

### <a name="table-75-parameters-for-the-showmessageboxstring-message-string-caption-messageboxbutton-button-messageboximage-icon-method"></a>75 de tabela. Parâmetros para o método ShowMessageBox(string message, string caption, MessageBoxButton button, MessageBoxImage icon)  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**mensagem**|A mensagem a apresentar na área de conteúdo da caixa de mensagem|  
|**Legenda**|O texto a mostrar na barra de título da caixa de diálogo|  
|**botão**|Os botões para mostrar|  
|**ícone**|O tipo do ícone para mostrar na caixa de mensagem|  

######  <a name="ShowMessageBox_Exception_exception"></a>ShowMessageBox (exceção exceção)  

```  
void ShowMessageBox(Exception exception);  
```  

 Este método apresenta uma caixa de mensagem que comunica informações sobre uma exceção. Esta caixa de mensagem tem um único **OK** botão. Consulte a tabela 76.  

### <a name="table-76-parameters-for-the-showmessageboxexception-exception-method"></a>Tabela 76. Parâmetros para o método ShowMessageBox(Exception exception)  

|**Parâmetro**|**Descrição**|  
|-|-|  
|**exceção**|A exceção que pretende que o relatório (utiliza a caixa de diálogo **exceção. Mensagem** como o conteúdo.)|  

######  <a name="ShowDialogWindow"></a>ShowDialogWindow  

```  
void ShowDialogWindow(Type viewType, DialogInteraction dialogPayload);  
```  

 Este método cria uma caixa de diálogo novo, o conteúdo que é o texto fornecer no **viewType** parâmetro. O estruturador de UDI cria uma nova instância deste tipo e encapsula num wrappê-la numa caixa de diálogo que tenha **OK** e **Cancelar** botões.  

 Transmitir dados para o controlo utilizando o parâmetro dialogPayload. O **SampleEditor** solução no diretório do SDK tem um exemplo de como utilizar esta funcionalidade.  

######  <a name="ShowWizardWindow"></a>ShowWizardWindow  

```  
void ShowWizardWindow(Type viewType, DialogInteraction dialogPayload);  
```  

 Este método permite-lhe apresentar um editor de personalizado no interior de uma caixa de diálogo inclui **seguinte** e **novamente** botões de navegação. Microsoft não forneceu um exemplo de como utilizar este método.  

###  <a name="UDIWizardConfigurationFileSchemaReference"></a>Referência de esquema de ficheiro de configuração de assistente UDI  
 Este ficheiro é consumido pelo Assistente de UDI e configurado, o UDI Wizard Designer. Este ficheiro é utilizado para configurar o:  

-   Páginas de assistente apresentadas no Assistente de UDI  

-   A sequência de páginas do assistente no Assistente de UDI  

-   Definições para os campos em cada página do Assistente  

-   StageGroups disponíveis no UDI Wizard Designer  

-   Fases disponíveis dentro de cada assistente de implementação no UDI Wizard Designer  

  77 apresenta os elementos no ficheiro de configuração do Assistente de UDI e as respetivas descrições. O **assistente** elemento é o nó de raiz para esta referência.  

### <a name="table-77-elements-in-the-udi-wizard-configuration-file-and-their-descriptions"></a>77 de tabela. Elementos do ficheiro de configuração do assistente UDI e as respetivas descrições  

|**Nome do elemento**|**Descrição**|  
|-|-|  
|[Dados](#Data)|Grupos o indivíduo [DataItem](#DataItem) elementos dentro de um [página](#Page) elemento e o nome pelo **nome** atributo.|  
|[DataItem](#DataItem)|Grupos o indivíduo [Setter]() elementos dentro de um [página](#Page) elemento. Pode criar dados hierárquicos, incluindo um ou mais [dados](#Data) elementos dentro de um [DataItem](#DataItem) elemento. Cada **DataItem** elemento representa um item individuais. Por exemplo, poderá ter uma lista de unidades disponíveis um **DataItem** para o nome a apresentar e outra **DataItem** elemento para a letra de unidade correspondente.|  
|[Predefinição](#Default)|Especifica um valor predefinido para o campo especificado no principal [campo](#Field) ou [RadioGroup](#RadioGroup) elemento. A predefinição está definida para o valor entre parênteses por este elemento.|  
|[DLL](#DLL)|Especifica um DLL que está a ser carregado e referenciada pelo Assistente de UDI e o UDI Wizard Designer.|  
|[DLLs](#DLLs)|Grupos o indivíduo [DLL](#DLL) elementos.|  
|[Erro](#Error)|Especifica pode devolver um código de erro possíveis que podem uma tarefa. O valor do código de erro é devolvido pela tarefa de **HRESULT** e é trapped por este elemento para fornecer informações de erro mais específicas.|  
|[ExitCode](#ExitCode)|Especifica um código de saída possíveis para uma tarefa. Códigos de saída são códigos de retorno que a tarefa de espera. Criar um **ExitCode** elemento para cada código de saída possíveis. Caso contrário, pode especificar um asterisco (\*) no **valor** atributo para lidar com códigos de retorno não indicados noutras **ExitCode** elementos.|  
|[ExitCodes](#ExitCodes)|Grupos de um conjunto de [ExitCode](#ExitCode) e [erro](#Error) elementos para um [tarefas](#Task) elemento ou um **erro** elemento.|  
|[Campo](#Field)|Especifica uma instância de um controlo num [página](#Page) elemento que é utilizado para fornecer a personalização com XML. Nem todos os controlos permitem a personalização com XML — apenas controla que utilizam o [campo](#Field) elemento.|  
|[Campos](#Fields)|Grupos o indivíduo [campo](#Field) elementos dentro de um [página](#Page) elemento.|  
|[Ficheiro](#File)|Especifica a origem e destino para uma através de operação de cópia do ficheiro a **Microsoft.Wizard.CopyFilesTask** tipo de tarefas. Pode incluir um separado **ficheiro** elemento copiar mais de um ficheiro numa única tarefa.|  
|[Página](#Page)|Especifica uma instância de uma página e inclui todas as definições de configuração para a página.|  
|[PageRef](#PageRef)|Especifica uma referência a uma instância de uma página dentro de um [fase](#Stage) dentro de um [StageGroup](#StageGroup).|  
|[Páginas](#Pages)|Grupos o indivíduo [página](#Page) elementos.|  
|[RadioGroup](#RadioGroup)|Especifica um grupo de botões de opção dentro de um [campo](#Field) elemento.|  
|[StageGroup](#StageGroup)|Especifica um grupo de fases de um ou mais.|  
|[StageGroups](#StageGroups)|Grupos de um conjunto de grupos de fase dentro de um ficheiro de configuração do Assistente de UDI.|  
|[Setter]()|Especifica uma definição de propriedade de um valor para uma propriedade com o nome no **propriedade** propriedade.|  
|[Fase](#Stage)|Especifica uma fase dentro de um [StageGroup](#StageGroup) e contém um ou mais [PageRef](#PageRef) elementos.|  
|[Estilo](#Style)|Grupos o indivíduo [setter]() elementos que configurar o Assistente de UDI aspeto e funcionalidade, incluindo o título apresentado na parte superior do assistente e a imagem de faixa apresentado no Assistente de UDI.|  
|[Tarefa](#Task)|Especifica uma tarefa que está a ser executada na página especificada na principal [página](#Page) elemento.|  
|[Tarefas](#Tasks)|Grupos de um conjunto de tarefas para um [página](#Page) elemento.|  
|[A validação do](#Validator)|Especifica um validador para o controlo de campo especificado no principal [campo](#Field) elemento.|  
|[Assistente](#Wizard)|Especifica a raiz para todos os outros elementos.|  

####  <a name="Data"></a>Dados  
 Este elemento grupos o indivíduo [DataItem](#DataItem) elementos dentro de um [página](#Page) elemento e o nome pelo **nome** atributo.  

##### <a name="element-information"></a>Informação de elemento  
Tabela 78 fornece informações sobre o [dados](#Data) elemento.  

### <a name="table-78-data-element-information"></a>78 de tabela. Informação de elemento de dados  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Zero ou mais dentro de cada [página](#Page) elemento (este elemento é opcional.)|  
|Elementos principais|**Página**, **DataItem**|  
|Conteúdo|**DataItem**, **Setter**|  

##### <a name="element-attributes"></a>Atributos de elemento  
 79 tabela lista os atributos do [dados](#Data) elemento e fornece uma descrição de cada.  

### <a name="table-79-attributes-and-corresponding-values-for-the-data-element"></a>79 de tabela. Atributos e valores correspondentes para o elemento de dados  

|**Atributo**|**Descrição**|  
|-|-|  
|**Nome**|Especifica o nome do [dados](#Data) elemento|  

##### <a name="remarks"></a>Observações  
 O **nome** atributo permite código para obter um conjunto específico de dados.  

##### <a name="example"></a>Exemplo  
 Nenhuma.  

####  <a name="DataItem"></a>DataItem  
 Este elemento grupos o indivíduo [Setter]() elementos dentro de um [página](#Page) elemento. Pode criar dados hierárquicos, incluindo um ou mais [dados](#Data) elementos dentro de um [DataItem](#DataItem) elemento. Cada **DataItem** elemento representa um item individuais. Por exemplo, poderá ter uma lista de unidades disponíveis um **DataItem** para o nome a apresentar e outra **DataItem** elemento para a letra de unidade correspondente.  

##### <a name="element-information"></a>Informação de elemento  
 Tabela 80 fornece informações sobre o [DataItem](#DataItem) elemento.  

### <a name="table-80-dataitem-element-information"></a>80 de tabela. Informação de elemento DataItem  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Zero ou mais dentro de cada [dados](#Data) elemento (este elemento é opcional.)|  
|Elementos principais|**Dados**|  
|Conteúdo|**Dados**, **Setter**|  

##### <a name="element-attributes"></a>Atributos de elemento  
 Este elemento tem sem atributos.  

##### <a name="remarks"></a>Observações  
 Nenhuma.  

##### <a name="example"></a>Exemplo  
 Nenhuma.  

#### <a name="default"></a>Predefinição  
 Este elemento Especifica um valor predefinido para o campo especificado no principal [campo](#Field) ou [RadioGroup](#RadioGroup) elemento. A predefinição está definida para o valor que este Retos de elemento.  

##### <a name="element-information"></a>Informação de elemento  
Tabela 81 fornece informações sobre o [predefinido](#Default) elemento.  

### <a name="table-81-default-element-information"></a>81 de tabela. Informações de elemento predefinidas  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências |Zero ou mais dentro de um [campo](#Field) ou [RadioGroup](#RadioGroup) elemento (este elemento é opcional.)|  
|Elementos principais|**Campo**, **RadioGroup**|  
|Conteúdo|Pode ser qualquer XML bem formado conteúdo, mas é texto normalmente padrão|  

##### <a name="element-attributes"></a>Atributos de elemento  
 Este elemento tem sem atributos.  

##### <a name="remarks"></a>Observações  
 Nenhuma.  

##### <a name="example"></a>Exemplo  
 No exemplo seguinte, a predefinição para o **fuso horário** campo está definido como "Hora padrão do Pacífico":  

```  
<Field Name="TimeZone" Enabled="true" VarName="OSDTimeZone" Summary="Time Zone:">  
  <Default>Pacific Standard Time</Default>  
```  

####  <a name="DLL"></a>DLL  
 Este elemento Especifica um DLL para o Assistente de UDI e UDI Wizard Designer para carregar e de referência.  

##### <a name="element-information"></a>Informação de elemento  
Tabela 82 fornece informações sobre o [DLL](#DLL) elemento.  

### <a name="table-82-dll-element-information"></a>82 de tabela. Informação de elemento DLL  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Um ou mais dentro de [DLLs](#DLLs) elemento|  
|Elemento principal|**DLLs**|  
|Conteúdo|Nenhum conteúdo permitido para este elemento|  

##### <a name="element-attributes"></a>Atributos de elemento  
 83 tabela lista os atributos do [DLL](#DLL) elemento e fornece uma descrição de cada.  

### <a name="table-83-attributes-and-corresponding-values-for-the-dll-element"></a>83 de tabela. Atributos e valores correspondentes para o elemento DLL  

|**Atributo**|**Descrição**|  
|-|-|  
|Nome|Especifica o nome da DLL para o Assistente de UDI e UDI Wizard Designer para efeitos de referência|  

##### <a name="remarks"></a>Observações  
 Nenhuma.  

##### <a name="example"></a>Exemplo  

```  
<DLLs>  
  <DLL Name="OSDRefreshWizard.dll" />   
  <DLL Name="SharedPages.dll" />  
</DLLs>  
```  

####  <a name="DLLs"></a>DLLs  
 Este elemento grupos o indivíduo [DLL](#DLL) elementos.  

##### <a name="element-information"></a>Informação de elemento  
Tabela de 84 fornece informações sobre o [DLLs](#DLLs) elemento.  

### <a name="table-84-dlls-element-information"></a>84 de tabela. Informações dos elementos DLLs  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|um|  
|Elementos principais|**Assistente**|  
|Conteúdo|**DLL**|  

##### <a name="element-attributes"></a>Atributos de elemento  
 Este elemento tem sem atributos.  

##### <a name="remarks"></a>Observações  
 Nenhuma.  

##### <a name="example"></a>Exemplo  

```  
<DLLs>  
   <DLL Name="OSDRefreshWizard.dll" />  
   <DLL Name="SharedPages.dll" />   
</DLLs>  
```  

####  <a name="Error"></a>Erro  
 Este elemento Especifica um código de erro possíveis que pode devolver uma tarefa. O valor do código de erro é devolvido e trapped pela tarefa **HRESULT** para fornecer informações de erro mais específicas.  

##### <a name="element-information"></a>Informação de elemento  
 Tabela 85 fornece informações sobre o [erro](#Error) elemento.  

### <a name="table-85-error-element-information"></a>85 de tabela. Informação de elemento de erro  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Zero ou mais dentro de cada [ExitCode](#ExitCode) elemento (este elemento é opcional.)|  
|Elementos principais|**ExitCodes**|  
|Conteúdo|Qualquer conteúdo XML corretamente formado|  

##### <a name="element-attributes"></a>Atributos de elemento  
 86 tabela lista os atributos do [erro](#Error) elemento e fornece uma descrição de cada.  

###  

|**Atributo**|**Descrição**|  
|-|-|  
|**Estado**|Especifica o estado de retorno de uma tarefa que encontrou um erro. Normalmente, o valor para este atributo é definido como erro. Este valor é apresentado no **estado** coluna na página do assistente no Assistente de UDI.|  
|**Texto**|Especifica o texto descritivo sobre a condição de erro que a tarefa encontrado.|  
|**Tipo**|Especifica se este elemento representa um erro, aviso ou com êxito. O valor especificado no**tipo** têm de ser exclusivos dentro de um [ExitCodes](#ExitCodes) elemento. Seguem-se os valores válidos para este elemento:<br /><br /> -   **0.**o elemento de representar um êxito.<br />-   **1.** O elemento representa um aviso.<br />-   **-1.** O elemento representa um erro.|  
|**Valor**|Especifica o valor do código que a tarefa devolvida como um valor numérico. Especifica o valor de um asterisco (*) indica o elemento predefinido códigos de retorno que não estejam listadas noutras [erro](#Error) elementos.|  

##### <a name="remarks"></a>Observações  
 Nenhuma.  

##### <a name="example"></a>Exemplo  
 Nenhuma.  

####  <a name="ExitCode"></a>ExitCode  
 Este elemento Especifica um código de saída possíveis para uma tarefa. Códigos de saída são códigos de retorno que a tarefa de espera. Criar um **ExitCode** elemento para cada código de saída possíveis. Caso contrário, pode especificar um asterisco (\*) no **valor** atributo para lidar com códigos de retorno não indicados noutras **ExitCode** elementos.  

##### <a name="element-information"></a>Informação de elemento  
Tabela 87 fornece informações sobre o [ExitCode](#ExitCode) elemento.  

### <a name="table-87-exitcode-element-information"></a>87 de tabela. Informação de elemento ExitCode  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Zero ou mais dentro de cada [ExitCodes](#ExitCodes) elemento (este elemento é opcional.)|  
|Elementos principais|**ExitCodes**|  
|Conteúdo|Pelo menos um [ExitCode](#ExitCode) elemento e zero ou mais [erro](#Error) elementos|  

##### <a name="element-attributes"></a>Atributos de elemento  
88 tabela lista os atributos do [ExitCode](#ExitCode) elemento e fornece uma descrição de cada.  

### <a name="table-88-attributes-and-corresponding-values-for-the-exitcode-element"></a>88 de tabela. Atributos e valores correspondentes para o elemento de ExitCode  

|**Atributo**|Descrição|  
|-|-|  
|**Estado**|Especifica o estado de retorno de uma tarefa. O valor deste atributo é apresentado no **estado** coluna na página do assistente correspondente no Assistente de UDI. Pode utilizar quaisquer valores para este atributo descritivos para a tarefa. Seguem-se típico valores utilizados para este atributo:<br /><br /> -Êxito<br />-Aviso<br />-Erro|  
|**Texto**|Especifica o texto descritivo sobre o código de exist da tarefa.|  
|**Tipo**|Especifica se este elemento representa um erro, aviso ou com êxito. O valor especificado no tipo tem de ser exclusivo dentro de um [ExitCodes](#ExitCodes) elemento. Seguem-se os valores válidos para este elemento:<br /><br /> -   **0.** O elemento representa um êxito.<br />-   **1.** O elemento representa um aviso.<br />-   **-1.** O elemento representa um erro.|  
|**Valor**|Especifica o valor do código que a tarefa devolvida como um valor numérico. Especifica o valor de um asterisco (*) indica o elemento predefinido códigos de retorno que não estejam listadas noutras [ExitCode](#ExitCode) elementos.|  

##### <a name="remarks"></a>Observações  
 Nenhuma.  

##### <a name="example"></a>Exemplo  
 Nenhuma.  

####  <a name="ExitCodes"></a>ExitCodes  
 Este elemento de um conjunto de grupos [ExitCode](#ExitCode) e [erro](#Error) elementos para um [tarefas](#Task) ou um **erro** elemento.  

##### <a name="element-information"></a>Informação de elemento  
Tabela 89 fornece informações sobre o [ExitCodes](#ExitCodes) elemento.  

### <a name="table-89-exitcodes-element-information"></a>89 de tabela. Informação de elemento ExitCodes  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Um em cada [tarefas](#Task) elemento|  
|Elementos principais|**Tarefa**|  
|Conteúdo|**Erro**, **ExitCode**|  

##### <a name="element-attributes"></a>Atributos de elemento  
 Este elemento tem sem atributos.  

##### <a name="remarks"></a>Observações  
 Nenhuma.  

##### <a name="example"></a>Exemplo  
 Nenhuma.  

####  <a name="Field"></a>Campo  
 Este elemento Especifica uma instância de um controlo num [página](#Page) elemento utilizado para fornecer a personalização com XML. Nem todos os controlos permitem a personalização com XML — apenas controla que utilizam o [campo](#Field) elemento.  

##### <a name="element-information"></a>Informação de elemento  
 Tabela 90 fornece informações sobre o [campo](#Field) elemento.  

### <a name="table-90-field-element-information"></a>Tabela 90. Informação de elemento do campo  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Zero ou mais dentro de cada [campo](#Field) elemento (este elemento é opcional.)|  
|Elementos principais|**Campos**|  
|Conteúdo|**Predefinição**, **validador**|  

##### <a name="element-attributes"></a>Atributos de elemento  
91 tabela lista os atributos do [campo](#Field) elemento e fornece uma descrição de cada.  

### <a name="table-91-attributes-and-corresponding-values-for-the-field-element"></a>Tabela 91. Atributos e valores correspondentes para o elemento de campo  

|**Atributo**|**Descrição**|  
|-|-|  
|**Ativado**|Especifica se o campo está ativado para o utilizador entrada (o atributo pode ser definido como VERDADEIRO ou FALSO.)|  
|**Nome**|Especifica o nome do campo|  
|**Resumo**|Especifica o texto descritivo apresentado no **resumo** página do Assistente para o valor que define este campo|  
|**VarName**|Especifica o nome sequência de tarefas variáveis de leitura ou configurada utilizando o campo no principal [campo](#Field) elemento|  

##### <a name="remarks"></a>Observações  
 Este elemento pode conter zero ou mais [predefinido](#Default) elementos e zero ou mais [validador](#Validator) elementos.  

##### <a name="example"></a>Exemplo  
 Nenhuma.  

####  <a name="Fields"></a>Campos  
 Este elemento grupos o indivíduo [campo](#Field) elementos dentro de um [página](#Page) elemento.  

##### <a name="element-information"></a>Informação de elemento  
Tabela 92 fornece informações sobre o [campos](#Fields) elemento.  

### <a name="table-92-fields-element-information"></a>92 de tabela. Informação de elemento de campos  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Zero ou mais dentro de cada [página](#Page) elemento (este elemento é opcional.)|  
|Elementos principais|**Página**|  
|Conteúdo|**Campo**, **RadioGroup**|  

##### <a name="element-attributes"></a>Atributos de elemento  
 Este elemento tem sem atributos.  

##### <a name="remarks"></a>Observações  
 Nenhuma.  

##### <a name="example"></a>Exemplo  
 Nenhuma.  

####  <a name="File"></a>Ficheiro  
 Este elemento Especifica a origem e destino para uma através de operação de cópia do ficheiro a **Microsoft.Wizard.CopyFilesTask** tipo de tarefas. Pode incluir um separado [ficheiro](#File) elemento copiar mais de um ficheiro numa única tarefa.  

##### <a name="element-information"></a>Informação de elemento  
 Tabela 93 fornece informações sobre o [ficheiro](#File) elemento.  

### <a name="table-93-file-element-information"></a>93 de tabela. Informação de elemento do ficheiro  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Um ou mais para cada tarefa tem um tipo de tarefa de **Microsoft.Wizard.CopyFilesTask**|  
|Elementos principais|**Tarefa**|  
|Conteúdo|Nenhum|  

##### <a name="element-attributes"></a>Atributos de elemento  
 94 tabela lista os atributos do [ficheiro](#File) elemento e fornece uma descrição de cada.  

### <a name="table-94-attributes-and-corresponding-values-for-the-file-element"></a>94 de tabela. Atributos e valores correspondentes para o elemento do ficheiro  

|**Atributo**|**Descrição**|  
|-|-|  
|**Dest**|Especifica o caminho completamente qualificado ou relativo para a pasta de destino para o ficheiro especificado no **origem** atributo. As variáveis de ambiente são permitidas como parte do caminho.|  
|**Origem**|Especifica o caminho completamente qualificado ou relativo para a origem de ficheiros que o **Microsoft.Wizard.CopyFilesTask** cópias do tipo de tarefas. Este atributo suporta carateres universais, para que possam ser copiados vários ficheiros de utilização de uma única [ficheiro](#File) elemento. As variáveis de ambiente são permitidas como parte do caminho.|  

##### <a name="remarks"></a>Observações  
 Nenhuma.  

##### <a name="example"></a>Exemplo  
 Nenhuma.  

####  <a name="PageElement"></a>Página  
 Este elemento Especifica uma instância de uma página e inclui todas as definições de configuração para a página.  

##### <a name="element-information"></a>Informação de elemento  
Tabela 95 fornece informações sobre o [página](#Page) elemento.  

### <a name="table-95-page-element-information"></a>95 de tabela. Informação de elemento da página  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Um ou mais dentro de cada [páginas](#Pages) elemento|  
|Elementos principais|**Páginas**|  
|Conteúdo|**Dados**, **campos**, **Setter**, **tarefas**|  

##### <a name="element-attributes"></a>Atributos de elemento  
96 tabela lista os atributos do [página](#Page) elemento e fornece uma descrição de cada.  

### <a name="table-96-attributes-and-corresponding-values-for-the-page-element"></a>96 de tabela. Atributos e valores correspondentes para o elemento da página  

|**Atributo**|**Descrição**|  
|-|-|  
|**DisplayName**|Especifica o nome amigável de utilizador da página do assistente, apresentado no UDI Wizard Designer. Este nome é normalmente mais descritivo do que o **nome** atributo.|  
|**Nome**|Especifica o nome da página do assistente, apresentado no UDI Wizard Designer.|  
|**Tipo**|Especifica o tipo de página do assistente que está diretamente relacionada com a uma página do assistente específicos dentro de uma DLL.|  

##### <a name="remarks"></a>Observações  
 Nenhuma.  

##### <a name="example"></a>Exemplo  
 Nenhuma.  

####  <a name="PageRef"></a>PageRef  
 Este elemento Especifica uma referência a uma instância de uma página dentro de um [fase](#Stage) dentro de um [StageGroup](#StageGroup).  

##### <a name="element-information"></a>Informação de elemento  
Tabela 97 fornece informações sobre o [PageRef](#PageRef) elemento.  

### <a name="table-97-pageref-element-information"></a>97 de tabela. Informação de elemento PageRef  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Um ou mais dentro de um [fase](#Stage) elemento|  
|Elementos principais|**Fase**|  
|Conteúdo|Nenhum|  

##### <a name="element-attributes"></a>Atributos de elemento  
98 tabela lista o atributo do [PageRef](#PageRef) elemento e fornece uma descrição do mesmo.  

### <a name="table-98-attributes-and-corresponding-values-for-the-pageref-element"></a>Tabela 98. Atributos e valores correspondentes para o elemento de PageRef  

|**Atributo**|**Descrição**|  
|-|-|  
|**Página**|Especifica a instância de uma página dentro de um [fase](#Stage) dentro de um [StageGroup](#StageGroup). Definir este valor para o atributo de nome de um [página](#Page) elemento.|  

##### <a name="remarks"></a>Observações  
 Nenhuma.  

##### <a name="example"></a>Exemplo  
 Nenhuma.  

####  <a name="Pages"></a>Páginas  
 Este elemento grupos o indivíduo [página](#Page) elementos.  

##### <a name="element-information"></a>Informação de elemento  
Tabela 99 fornece informações sobre o [páginas](#Pages) elemento.  

### <a name="table-99-pages-element-information"></a>Tabela 99. Informação de elemento de páginas  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|um|  
|Elementos principais|**Assistente**|  
|Conteúdo|**Página**|  

##### <a name="element-attributes"></a>Atributos de elemento  
 Este elemento tem sem atributos.  

##### <a name="remarks"></a>Observações  
 Nenhuma.  

##### <a name="example"></a>Exemplo  

```  
<Pages>  
   + <Page Name="WelcomePage" DisplayName="Welcome" Type="Microsoft.SharedPages.WelcomePage">  
   + <Page Name="ConfigScanPage" DisplayName="Deployment Readiness" Type="Microsoft.OSDRefresh.ConfigScanPage">  
   + <Page Name="ConfigScanBareMetal" DisplayName="Deployment Readiness" Type="Microsoft.OSDRefresh.ConfigScanPage">  
   + <Page Name="RebootPage" DisplayName="Reboot" Type="Microsoft.OSDRefresh.RebootPage">  
   + <Page Name="WelcomePageReplace" DisplayName="Welcome" Type="Microsoft.SharedPages.WelcomePage">  
   + <Page Name="VolumePage" DisplayName="Volume" Type="Microsoft.OSDRefresh.VolumePage">  
   + <Page Name="UserRestorePage" DisplayName="Select Target" Type="Microsoft.OSDRefresh.UserStatePage">  
   + <Page Name="ComputerPage" DisplayName="New Computer Details" Type="Microsoft.OSDRefresh.ComputerPage">  
   + <Page Name="AdminAccounts" DisplayName="Administrator Password" Type="Microsoft.SharedPages.AdminAccountsPage">  
   + <Page Name="UDAPage" DisplayName="User Device Affinity" Type="Microsoft.OSDRefresh.UDAPage">  
   + <Page Name="LanguagePage" DisplayName="Language" Type="Microsoft.OSDRefresh.LanguagePage">  
   + <Page Name="ApplicationPage" DisplayName="Install Programs" Type="Microsoft.OSDRefresh.ApplicationPage">  
     <Page Name="SummaryPage" DisplayName="Summary" Type="Microsoft.Shared.SummaryPage" />   
   + <Page Name="UserCapturePageOldPC" DisplayName="Select Target" Type="Microsoft.OSDRefresh.UserStatePage">  
   + <Page Name="ProgressPage" DisplayName="Capture Data" Type="Microsoft.OSDRefresh.ProgressPage">  
   + <Page Name="RebootAfterCapture" DisplayName="Reboot" Type="Microsoft.OSDRefresh.RebootPage">  
</Pages>  
```  

####  <a name="RadioGroup"></a>RadioGroup  
 Este elemento Especifica um grupo de botões de opção num [campo](#Field) elemento.  

##### <a name="element-information"></a>Informação de elemento  
Tabela 100 fornece informações sobre o [RadioGroup](#RadioGroup) elemento.  

### <a name="table-100-radiogroup-element-information"></a>100 de tabela. Informação de elemento RadioGroup  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Zero ou mais dentro de um [campos](#Fields) elemento (este elemento é opcional.)|  
|Elementos principais|**Campos**|  
|Conteúdo|**Predefinição**|  

##### <a name="element-attributes"></a>Atributos de elemento  
 101 tabela lista os atributos do [RadioGroup](#RadioGroup) elemento e fornece uma descrição de cada.  

### <a name="table-101-attributes-and-corresponding-values-for-the-radiogroup-element"></a>101 de tabela. Atributos e valores correspondentes para o elemento de RadioGroup  

|**Atributo**|**Descrição**|  
|-|-|  
|**Bloqueado**|Especifica se o grupo de botões de opção está ativado para a entrada do utilizador. O atributo pode ser definido como:<br /><br /> -   **Verdadeiro**. Especifica que os botões de opção estão desativados e os utilizadores não é possível selecionar um botão de opção no grupo.<br />-   **FALSO**. Especifica que os botões de opção estão ativados e os utilizadores podem selecionar um botão de opção no grupo.|  
|**Nome**|Especifica o nome do grupo de opção de botões de opção.|  

##### <a name="remarks"></a>Observações  
 Nenhuma.  

##### <a name="example"></a>Exemplo  
 Nenhuma.  

####  <a name="StageGroup"></a>StageGroup  
 Este elemento Especifica um grupo de fase de implementação.  

##### <a name="element-information"></a>Informação de elemento  
Tabela 102 fornece informações sobre o [StageGroup](#StageGroup) elemento.  

### <a name="table-102-stagegroup-element-information"></a>102 de tabela. Informação de elemento StageGroup  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Um ou mais dentro de um [StageGroups](#StageGroups) elemento|  
|Elementos principais|**StageGroups**|  
|Conteúdo|**Fase**|  

##### <a name="element-attributes"></a>Atributos de elemento  
 103 tabela lista os atributos do [StageGroup](#StageGroup) elemento e uma descrição do atributo.  

### <a name="table-103-attributes-and-corresponding-values-for-the-stagegroup-element"></a>103 de tabela. Atributos e valores correspondentes para o elemento de StageGroup  

|**Atributo**|**Descrição**|  
|-|-|  
|**DisplayName**|Especifica o nome amigável de utilizador do grupo fase apresentado no UDI Wizard Designer. Este nome é normalmente mais descritivo do que o **nome** atributo.|  

##### <a name="remarks"></a>Observações  
 Nenhuma.  

##### <a name="example"></a>Exemplo  
 Nenhuma.  

####  <a name="StageGroups"></a>StageGroups  
 Este elemento grupos de um conjunto de grupos de fase dentro de um ficheiro de configuração do Assistente de UDI.  

##### <a name="element-information"></a>Informação de elemento  
Tabela 104 fornece informações sobre o [StageGroups](#StageGroups) elemento.  

### <a name="table-104-stagegroups-element-information"></a>104 de tabela. Informação de elemento StageGroups  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Zero ou um dentro de um [assistente](#Wizard) elemento|  
|Elementos principais|**Assistente**|  
|Conteúdo|**StageGroup**|  

##### <a name="element-attributes"></a>Atributos de elemento  
 Este elemento tem sem atributos.  

##### <a name="remarks"></a>Observações  
 Nenhuma.  

##### <a name="example"></a>Exemplo  
 Nenhuma.  

####  <a name="Setter"></a>Setter  
 Este elemento Especifica uma definição de propriedade para o valor para uma propriedade com o nome no **propriedade** propriedade.  

##### <a name="element-information"></a>Informação de elemento  
 Tabela 105 fornece informações sobre o [Setter]() elemento.  

### <a name="table-105-setter-element-information"></a>105 de tabela. Informações dos elementos setter  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Zero ou mais dentro de cada elemento principal (este elemento é opcional.)|  
|Elementos principais|**Dados**, **DataItem**, **página**, **estilo**, **tarefas**, **validador**|  
|Conteúdo|Contém um valor de cadeia no **propriedade** atributo|  

##### <a name="element-attributes"></a>Atributos de elemento  
106 tabela lista o atributo do [Setter]() elemento e fornece uma descrição do mesmo.  

### <a name="table-106-attributes-and-corresponding-values-for-the-setter-element"></a>106 de tabela. Atributos e valores correspondentes para o elemento de Setter  

|**Atributo**|**Descrição**|  
|-|-|  
|**Propriedade**|Especifica o nome de propriedade que está a ser definido. O nome da propriedade está definido como o valor que este atributo Parênteses Retos.|  

##### <a name="remarks"></a>Observações  
 Nenhuma.  

##### <a name="example"></a>Exemplo  
 Nenhuma.  

#### <a name="stage"></a>Fase  
 Este elemento Especifica um [fase](#Stage) dentro de um [StageGroup](#StageGroup) e contém um ou mais [PageRef](#PageRef) elementos.  

##### <a name="element-information"></a>Informação de elemento  
Tabela 107 fornece informações sobre o [fase](#Stage) elemento.  

### <a name="table-107-stage-element-information"></a>107 de tabela. Fase informações dos elementos  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Um ou mais dentro de um [StageGroup](#StageGroup) elemento|  
|Elementos principais|**StageGroup**|  
|Conteúdo|**PageRef**|  

##### <a name="element-attributes"></a>Atributos de elemento  
108 tabela lista os atributos do [fase](#Stage) elemento e fornece uma descrição de cada.  

### <a name="table-108-attributes-and-corresponding-values-for-the-stage-element"></a>108 de tabela. Atributos e valores correspondentes para o elemento de fase  

|**Atributo**|**Descrição**|  
|-|-|  
|**DisplayName**|Especifica o nome amigável de utilizador da página do assistente, apresentado no UDI Wizard Designer. Este nome é normalmente mais descritivo do que o **nome** atributo.|  
|**Nome**|Especifica o nome de fase. É utilizado o valor deste elemento ao iniciar o Assistente de UDI com o **/testar: nome** parâmetro de linha de comandos.|  

##### <a name="remarks"></a>Observações  
 Nenhuma.  

##### <a name="example"></a>Exemplo  
 Nenhuma.  

####  <a name="Style"></a>Estilo  
 Este elemento grupos o indivíduo [Setter]() elementos que configurar o Assistente de UDI aspeto e funcionalidade, incluindo o título apresentado na parte superior do assistente e a imagem de faixa apresentado no Assistente de UDI.  

##### <a name="element-information"></a>Informação de elemento  
109 tabela fornece informações sobre o elemento de estilo.  

### <a name="table-109-style-element-information"></a>109 de tabela. Informação de elemento de estilo  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|um|  
|Elementos principais|**Assistente**|  
|Conteúdo|**Setter**|  

##### <a name="element-attributes"></a>Atributos de elemento  
 Este elemento tem sem atributos.  

##### <a name="remarks"></a>Observações  
 Nenhuma.  

##### <a name="example"></a>Exemplo  

```  
<Style>  
  <Setter Property="bannerFilename">UDI_Wizard_Banner.bmp</Setter>   
  <Setter Property="title">Operating System Deployment (OSD) Refresh Wizard</Setter>   
</Style>  
```  

####  <a name="TaskElement"></a>Tarefa  
 Este elemento Especifica uma tarefa que está a ser executada na página especificada na principal [página](#Page) elemento.  

##### <a name="element-information"></a>Informação de elemento  
Tabela 110 fornece informações sobre o [tarefas](#Task) elemento.  

### <a name="table-110-task-element-information"></a>110 de tabela. Informação de elemento de tarefa  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Um ou mais dentro de um [tarefas](#Tasks) elemento|  
|Elementos principais|**Tarefas**|  
|Conteúdo|**ExitCodes**, **ficheiro**, **Setter**|  

##### <a name="element-attributes"></a>Atributos de elemento  
111 tabela lista os atributos do [tarefas](#Task) elemento e fornece uma descrição de cada.  

### <a name="table-111-attributes-and-corresponding-values-for-the-task-element"></a>111 de tabela. Atributos e valores correspondentes para o elemento de tarefa  

|**Atributo**|**Descrição**|  
|-|-|  
|**DependsOn**|Especifica se a tarefa é depende de outra tarefa. O valor deste atributo é definido como o **nome** atributo de outro [tarefas](#Task) elemento. **Nota:**  Este atributo não pode ser configurado com o UDI Wizard Designer. No entanto, pode adicionar manualmente este atributo como uma [tarefas](#Task) elemento modificando diretamente o ficheiro. XML.|  
|**DisplayName**|Especifica o nome amigável de utilizador da tarefa apresentado no UDI Wizard Designer. Este nome é normalmente mais descritivo do que o **nome** atributo.|  
|**Nome**|Especifica o nome da tarefa. Este nome tem de ser exclusivo.|  
|Type|Especifica o tipo de tarefa para a tarefa a ser executada, que está definido na DLL que contém a tarefa.|  

##### <a name="remarks"></a>Observações  
 Nenhuma.  

##### <a name="example"></a>Exemplo  
 Nenhuma.  

####  <a name="Tasks"></a>Tarefas  
 Este elemento grupos de um conjunto de tarefas para um [página](#Page) elemento.  

##### <a name="element-information"></a>Informação de elemento  
Tabela 112 fornece informações sobre o [tarefas](#Tasks) elemento.  

### <a name="table-112-tasks-element-information"></a>112 de tabela. Informação de elemento de tarefas  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Zero ou um em cada [página](#Page) elemento (este elemento é opcional.)|  
|Elementos principais|**Página**|  
|Conteúdo|**Tarefa**|  

##### <a name="element-attributes"></a>Atributos de elemento  
113 tabela lista os atributos do [tarefas](#Tasks) elemento e fornece uma descrição de cada.  

### <a name="table-113-attributes-and-corresponding-values-for-the-tasks-element"></a>113 de tabela. Atributos e valores correspondentes para o elemento de tarefas  

|**Atributo**|**Descrição**|  
|-|-|  
|**NameTitle**|Especifica a legenda que aparece na parte superior da coluna que contém o nome das tarefas na página do assistente adequado.|  
|**StatusTitle**|Especifica a legenda que aparece na parte superior da coluna que contém o estado das tarefas na página do assistente adequado.|  

##### <a name="remarks"></a>Observações  
 Nenhuma.  

##### <a name="example"></a>Exemplo  
 Nenhuma.  

####  <a name="ValidatorElement"></a>A validação do  
 Este elemento Especifica um validador para o controlo de campo especificado no principal [campo](#Field) elemento.  

##### <a name="element-information"></a>Informação de elemento  
Tabela 114 fornece informações sobre o [validador](#Validator) elemento.  

### <a name="table-114-validator-element-information"></a>114 de tabela. Informações de elemento do validador  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|Zero ou um dentro de um [campo](#Field) elemento|  
|Elementos principais|**Campo**|  
|Conteúdo|**Setter**|  

##### <a name="element-attributes"></a>Atributos de elemento  
115 tabela lista o atributo do [validador](#Validator) elemento e fornece uma descrição do mesmo.  

### <a name="table-115-attributes-and-corresponding-values-for-the-validator-element"></a>115 de tabela. Atributos e valores correspondentes para o elemento de validação  

|**Atributo**|**Descrição**|  
|-|-|  
|Type|Especifica o tipo para o validador, que está definido na DLL que contém o validador|  

##### <a name="remarks"></a>Observações  
 Nenhuma.  

##### <a name="example"></a>Exemplo  
 Nenhuma.  

####  <a name="Wizard"></a>Assistente  
 Este elemento Especifica a raiz para todos os outros elementos.  

##### <a name="element-information"></a>Informação de elemento  
Tabela 116 fornece informações sobre o [assistente](#Wizard) elemento.  

### <a name="table-116-wizard-element-information"></a>116 de tabela. Informação de elemento do Assistente  

|**Atributo**|**Valor**|  
|-|-|  
|Número de ocorrências|um|  
|Elementos principais|Nenhum|  
|Conteúdo|**DLLs**, **páginas**, **StageGroups**, **estilo**|  

##### <a name="element-attributes"></a>Atributos de elemento  
 Este elemento tem sem atributos.  

##### <a name="remarks"></a>Observações  
 Nenhuma.  

##### <a name="example"></a>Exemplo  

```  
<Wizard>  
   + <DLLs>  
   + <Style>  
   + <Pages>  
   + <StageGroups>  
</Wizard>  
```
