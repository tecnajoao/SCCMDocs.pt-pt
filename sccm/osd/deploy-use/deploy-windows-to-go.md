---
title: Implementar o Windows to Go
titleSuffix: Configuration Manager
description: "Saiba como aprovisionar o Windows To Go no System Center Configuration Manager, para criar uma área de trabalho Windows To Go que iniciam a partir de uma unidade externa."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8eed50f5-80a4-422e-8aa6-a7ccb2171475
caps.latest.revision: "8"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 91e3fa4aba93dc3012fe1e702f50c4f9438a69e8
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="deploy-windows-to-go-with-system-center-configuration-manager"></a>Implementar o Windows to Go com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este tópico fornece os passos para aprovisionar o Windows To Go no System Center Configuration Manager. O Windows To Go é uma funcionalidade empresarial do Windows 8 que permite a criação de uma área de trabalho do Windows To Go que pode arrancar a partir de uma unidade externa ligada por USB em computadores que cumpram os requisitos de certificação do Windows 7 ou do Windows 8, independentemente do sistema operativo em execução no computador. As áreas de trabalho do Windows To Go podem utilizar a mesma imagem que as empresas utilizam nos seus computadores de secretária e portáteis e podem ser geridas da mesma forma.  

 Para obter mais informações sobre o Windows To Go, consulte [Windows To Go descrição geral da funcionalidade](http://go.microsoft.com/fwlink/p/?LinkId=263433).  

## <a name="provision-windows-to-go"></a>Aprovisionar o Windows To Go  
 O Windows To Go é um sistema operativo armazenado numa unidade externa ligada por USB. Pode aprovisionar a unidade do Windows To Go tal como aprovisiona outras implementações de sistema operativo. No entanto, uma vez que o Windows To Go foi concebido para ser uma solução centrada no utilizador e com elevada mobilidade, tem de adotar uma abordagem ligeiramente diferente ao aprovisionamento destas unidades.  

 A um nível elevado, o Windows To Go é uma implementação de duas fases que lhe permite configurar o dispositivo do Windows To Go e pré-configurar conteúdo para a implementação do sistema operativo. Pode conseguir isto com um impacto mínimo do utilizador e o período de indisponibilidade do limite para o computador do utilizador. Depois de pré-configurar o computador, tem de concluir o processo de aprovisionamento para garantir que o computador fica pronto para o utilizador. O processo de aprovisionamento é semelhante ao processo de implementação do sistema operativo atual. Segue-se o fluxo de trabalho geral para pré-configurar conteúdo e aprovisionar o Windows To Go:  

1.  [Pré-requisitos para aprovisionar o Windows To Go](#BKMK_Prereqs)  

2.  [Criar suportes de dados pré-configurados](#BKMK_CreatePrestagedMedia)  

3.  [Criar um pacote do Windows To Go Creator](#BKMK_CreatePackage)  

4.  [Atualizar a sequência de tarefas para ativar o BitLocker para o Windows To Go](#BKMK_UpdateTaskSequence)  

5.  [Implementar o pacote do Windows To Go Creator e a sequência de tarefas](#BKMK_Deployments)  

6.  [O utilizador executa o Windows To Go Creator](#BKMK_UserExperience)  

7.  [O Configuration Manager configura e prepara a unidade do Windows To Go](#BKMK_ConfigureStageDrive)  

8.  [O utilizador inicia sessão no Windows 8](#BKMK_UserLogsIn)  

###  <a name="BKMK_Prereqs"></a> Pré-requisitos para aprovisionar o Windows To Go  
 Antes de aprovisionar o Windows To Go, tem de concluir o seguinte no Configuration Manager:  

-   **Distribuir uma imagem de arranque para um ponto de distribuição**  

     antes de criar o suporte de dados pré-configurado, tem de distribuir a imagem de arranque a um ponto de distribuição.  

    > [!NOTE]  
    >  Imagens de arranque são utilizadas para instalar o sistema operativo dos computadores de destino no seu ambiente do Configuration Manager. Contêm uma versão do Windows PE que instala o sistema operativo, bem como os controladores de dispositivo adicionais que sejam necessários. Configuration Manager fornece duas imagens de arranque: Uma para suportar plataformas x86 e outra para suportar x64 plataformas. Também pode criar imagens de arranque próprias. Para obter mais informações, consulte [gerir imagens de arranque](../get-started/manage-boot-images.md).  

-   **Distribuir a imagem do sistema operativo Windows 8 para um ponto de distribuição**  

     antes de criar o suporte de dados pré-configurado, tem de distribuir a imagem do sistema operativo Windows 8 a um ponto de distribuição.  

    > [!NOTE]  
    >  As imagens de sistema operativo são ficheiros com o formato .WIM e representam uma coleção comprimida de ficheiros e pastas de referência que são necessários para instalar e configurar com êxito um sistema operativo num computador. Para obter mais informações, consulte [gerir imagens do sistema operativo](../get-started/manage-operating-system-images.md).  

-   **Criar uma Sequência de Tarefas para Implementar o Windows 8**  

     tem de criar uma sequência de tarefas para uma implementação do Windows 8 que será referenciar quando criar suportes de dados pré-configurados. Para obter mais informações, consulte [gerir sequências de tarefas para automatizar tarefas](manage-task-sequences-to-automate-tasks.md).  

###  <a name="BKMK_CreatePrestagedMedia"></a> Criar suportes de dados pré-configurados  
 O suporte de dados pré-configurado contém a imagem de arranque utilizada para iniciar o computador de destino e a imagem de sistema operativo aplicada no computador de destino. O computador que for aprovisionado com um suporte de dados pré-configurado pode ser iniciado utilizando a imagem de arranque. Em seguida, o computador pode executar uma sequência de tarefas existente de implementação de sistema operativo para instalar uma implementação completa do sistema operativo. A sequência de tarefas que implementa o sistema operativo não está incluída no suporte de dados.  

 Pode adicionar conteúdo, como aplicações e controladores de dispositivo, para além da imagem do sistema operativo e da imagem de arranque, durante a fase de pré-configuração. Isto reduz o tempo de implementação de um sistema operativo e reduz o tráfego de rede porque o conteúdo já está na unidade.  

 Utilize o procedimento seguinte para criar o suporte de dados pré-configurado.  

#### <a name="to-create-prestaged-media"></a>Para criar um suporte de dados pré-configurado  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**e clique em **Sequências de Tarefas**.  

3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Suportes de Dados da Sequência de Tarefas** para iniciar o Assistente de Criação de Suporte de Dados da Sequência de Tarefas.  

4.  Na página **Selecione o Tipo de Suporte de Dados** , especifique as informações seguintes e clique em **Seguinte**.  

    -   Selecione **Suporte de dados pré-configurado**.  

    -   Selecione **Permitir a implementação do sistema operativo autónoma** para arrancar a implementação do Windows To Go sem interação do utilizador.  

        > [!IMPORTANT]  
        >  Quando utiliza esta opção com a variável personalizada SMSTSPreferredAdvertID (definida mais adiante neste procedimento), não é necessária qualquer interação do utilizador e o computador arrancará automaticamente na implementação do Windows To Go quando detetar uma unidade do Windows To Go. Ainda assim, será solicitada uma palavra-passe ao utilizador se o suporte de dados estiver configurado com proteção por palavra-passe. Se utilizar a definição **Permitir a implementação do sistema operativo autónoma** sem configurar a variável SMSTSPreferredAdvertID, ocorrerá um erro quando implementar a sequência de tarefas.  

5.  Na página **Gestão de Suporte de Dados** , especifique as informações seguintes e clique em **Seguinte**.  

    -   Selecione **Suporte de dados dinâmico** se pretender permitir que um ponto de gestão redirecione o suporte de dados para outro ponto de gestão, com base na localização do cliente nos limites do site.  

    -   Selecione **Suporte de dados baseado no site** se pretender que o suporte de dados entre em contacto apenas com o ponto de gestão especificado.  

6.  Na página **Propriedades do Suporte de Dados**  , especifique as informações seguintes e, em seguida, clique em **Seguinte**.  

    -   **Criado pelo**: Especifique quem criou o suporte de dados.  

    -   **Versão**: Especifique o número de versão do suporte de dados.  

    -   **Comentário**: Especifique uma descrição exclusiva da que é utilizado o suporte de dados.  

    -   **Ficheiro de multimédia**: Especifique o nome e caminho dos ficheiros de saída. O assistente escreve os ficheiros de saída nesta localização. Por exemplo:  **\\\servername\folder\outputfile.wim**  

7.  Na página **Segurança** , especifique as seguintes informações e clique em **Seguinte**.  

    -   Selecione **ativar suporte para computadores desconhecidos** para permitir que o suporte de dados implementar um sistema operativo num computador que não seja gerido pelo Configuration Manager. Não há nenhum registo destes computadores na base de dados do Configuration Manager. Os computadores desconhecidos incluem o seguinte:  

        -   Um computador em que o cliente do Configuration Manager não está instalado  

        -   Um computador que não é importado para o Configuration Manager  

        -   Um computador que não é detetado pelo Configuration Manager  

    -   Selecione **Proteger suporte de dados com uma palavra-passe** e introduza uma palavra-passe segura para ajudar a proteger o suporte de dados contra acesso não autorizado. Quando especificar uma palavra-passe, o utilizador terá de fornecer essa palavra-passe para utilizar o suporte de dados pré-configurado.  

        > [!IMPORTANT]  
        >  Como procedimento de segurança recomendado, atribua sempre uma palavra-passe para ajudar a proteger o suporte de dados pré-configurado.  

        > [!NOTE]  
        >  Quando protege o suporte de dados pré-configurado com uma palavra-passe, esta é solicitada ao utilizador mesmo quando o suporte de dados está configurado com a definição **Permitir a implementação do sistema operativo autónoma** .  

    -   Para comunicações HTTP, selecione **Criar um certificado de suporte de dados autoassinado**e especifique as datas de início e de expiração do certificado.  

    -   Para comunicações HTTPS, selecione **Importar certificado PKI**e especifique o certificado a importar e a respetiva palavra-passe.  

         Para mais informações sobre este certificado de cliente que é utilizado para imagens de arranque, consulte [requisitos dos certificados PKI](../../core/plan-design/network/pki-certificate-requirements.md).  

    -   **Afinidade dispositivo / utilizador**: Para suportar a gestão centrada no utilizador no Configuration Manager, especifique como pretende que o suporte de dados associe utilizadores ao computador de destino. Para obter mais informações sobre como implementação de sistemas operativos suporta a afinidade dispositivo / utilizador, consulte [associar utilizadores um computador de destino](../get-started/associate-users-with-a-destination-computer.md).  

        -   Especifique **Permitir afinidade dispositivo/utilizador com aprovação automática** se pretender que o suporte de dados associe automaticamente utilizadores ao computador de destino. Esta funcionalidade baseia-se nas ações da sequência de tarefas que implementa o sistema operativo. Neste cenário, a sequência de tarefas cria uma relação entre os utilizadores especificados e o computador de destino quando implementa o sistema operativo no computador de destino.  

        -   Especifique **Permitir afinidade dispositivo/utilizador com aprovação pendente pelo administrador** se pretender que o suporte de dados associe utilizadores ao computador de destino após concessão da aprovação. Esta funcionalidade baseia-se no âmbito da sequência de tarefas que implementa o sistema operativo. Neste cenário, a sequência de tarefas cria uma relação entre os utilizadores especificados e o computador de destino, mas aguarda a aprovação de um utilizador administrativo antes da implementação do sistema operativo.  

        -   Especifique **Não permitir afinidade dispositivo/utilizador** se não pretender que o suporte de dados associe utilizadores ao computador de destino. Neste cenário, a sequência de tarefas não associa utilizadores ao computador de destino durante a implementação do sistema operativo.  

8.  Na página **Sequência de Tarefas** , especifique a sequência de tarefas do Windows 8 que criou na secção anterior.  

9. Na página **Imagem de arranque** , especifique as seguintes informações e clique em **Seguinte**.  

    > [!IMPORTANT]  
    >  A arquitetura da imagem de arranque que é distribuída deve ser adaptada à arquitetura do computador de destino. Por exemplo, um computador de destino x64 pode efetuar o arranque e a execução de uma imagem de arranque x86 ou x64. No entanto, um computador de destino x86 só pode efetuar o arranque e a execução de uma imagem de arranque x86. Para computadores com certificação do Windows 8 no modo EFI, tem de utilizar uma imagem de arranque x64.  

    -   **Imagem de arranque**: Especifique a imagem de arranque para iniciar o computador de destino.  

    -   **Ponto de distribuição**: Especifique o ponto de distribuição que aloja a imagem de arranque. O assistente obtém a imagem de arranque do ponto de distribuição e escreve-a no suporte de dados.  

        > [!NOTE]  
        >  O utilizador administrativo tem de ter direitos de acesso de **Leitura** para o conteúdo da imagem de arranque no ponto de distribuição. Para obter mais informações, consulte [gerir contas para aceder ao conteúdo](../../core/plan-design/hierarchy/manage-accounts-to-access-content.md).  

    -   Se tiver selecionado **Suporte de dados baseado no site** na página **Gestão de Suporte de Dados** deste assistente, na caixa **Ponto de gestão** , especifique um ponto de gestão de um site primário.  

    -   Se tiver selecionado **Suporte de dados dinâmico** na página **Gestão de Suporte de Dados** do assistente, na caixa **Pontos de gestão associados** , especifique os pontos de gestão do site primário a utilizar e uma ordem de prioridades para as comunicações iniciais.  

10. Na página **Imagens** , especifique as seguintes informações e clique em **Seguinte**.  

    -   **Pacote de imagem**: Especifique o pacote que contém a imagem do sistema operativo Windows 8.  

    -   **Índice de imagens**: Especifique a imagem a implementar se o pacote contiver várias imagens de sistema operativo.  

    -   **Ponto de distribuição**: Especifique o ponto de distribuição que aloja o pacote de imagem do sistema operativo. O assistente obtém a imagem do sistema operativo a partir do ponto de distribuição e escreve-a no suporte de dados.  

        > [!NOTE]  
        >  O utilizador administrativo tem de ter direitos de acesso de **Leitura** para o conteúdo da imagem de sistema operativo no ponto de distribuição. Para obter mais informações, consulte [gerir contas para aceder ao conteúdo](../../core/plan-design/hierarchy/manage-accounts-to-access-content.md).  

11. Na página **Selecionar Aplicação** , selecione conteúdo de aplicações a incluir no ficheiro do suporte de dados e clique em **Seguinte**.  

12. Na página **Selecionar Pacote** , selecione conteúdo de pacote adicional a incluir no ficheiro do suporte de dados e clique em **Seguinte**.  

13. Na página **Selecionar o Pacote do Controlador** , selecione conteúdo de pacote de controladores a incluir no ficheiro do suporte de dados e clique em **Seguinte**.  

14. Na página **Pontos de Distribuição** , selecione um ou vários pontos de distribuição que contenham o conteúdo exigido pela sequência de tarefas e clique em **Seguinte**.  

15. Na página **Personalização** , especifique as seguintes informações e clique em **Seguinte**.  

    -   **Variáveis**: Especifique as variáveis utilizadas pela sequência de tarefas para implementar o sistema operativo. Para o Windows To Go, utilize a variável SMSTSPreferredAdvertID para selecionar automaticamente a implementação do Windows To Go utilizando o seguinte formato:  

         SMSTSPreferredAdvertID = {*IDdaImplementação*}, em que IDdaImplementação é o ID da implementação associado à sequência de tarefas que irá utilizar para concluir o processo de aprovisionamento para a unidade do Windows To Go.  

        > [!TIP]  
        >  Quando utiliza esta variável com uma sequência de tarefas definida para execução automática (definida mais adiante neste procedimento), não é necessária qualquer interação do utilizador e o computador arranca automaticamente na implementação do Windows To Go quando detetar uma unidade do Windows To Go. Ainda assim, será solicitada uma palavra-passe ao utilizador se o suporte de dados estiver configurado com proteção por palavra-passe.  

    -   **Comandos de Pré-início**: Especifique os comandos de pré-início que pretende executar antes da execução da sequência de tarefas. Os comandos de pré-início podem ser um script ou um ficheiro executável que podem interagir com o utilizador no Windows PE antes da execução da sequência de tarefas para instalar o sistema operativo. Configure as seguintes variáveis para a implementação do Windows To Go:  

        -   **OSDBitLockerPIN**: O BitLocker para Windows To Go necessita de uma frase de acesso. Defina a variável **OSDBitLockerPIN** como parte de um comando de pré-início para definir a frase de acesso do BitLocker para a unidade do Windows To Go.  

            > [!WARNING]  
            >  Quando o BitLocker tiver a frase de acesso ativada, o utilizador terá de introduzir a frase de acesso sempre que o computador arrancar na unidade do Windows To Go.  

        -   **SMSTSUDAUsers**: Especifica o utilizador primário do computador de destino. Utilize esta variável para recolher o nome do utilizador, que pode então ser utilizado para associar o utilizador e o dispositivo. Para obter mais informações, consulte [associar utilizadores um computador de destino](../get-started/associate-users-with-a-destination-computer.md).  

            > [!TIP]  
            >  Para obter o nome de utilizador, pode criar uma caixa de introdução como parte do comando de pré-início, para o utilizador introduzir o respetivo nome de utilizador, e, em seguida, definir a variável com o valor. Por exemplo, pode adicionar as seguintes linhas ao ficheiro de script do comando de pré-início:  
            >   
            >  `UserID = inputbox("Enter Username" ,"Enter your username:","",400,0)`  
            >   
            >  `env("SMSTSUDAUsers") = UserID`  

         Para obter mais informações sobre como criar um ficheiro de script para utilizar como comando de Pré-início, consulte [comandos para suporte de dados de sequência de tarefas de Pré-início](../understand/prestart-commands-for-task-sequence-media.md).  

16. Conclua o assistente.  

    > [!NOTE]  
    >  A conclusão do ficheiro do suporte de dados pré-configurado pelo assistente poderá demorar bastante tempo.  

###  <a name="BKMK_CreatePackage"></a> Criar um pacote do Windows To Go Creator  
 Como parte da implementação do Windows To Go, tem de criar um pacote para implementar o ficheiro de suporte de dados pré-configurado. O pacote tem de incluir a ferramenta que configura a unidade do Windows To Go e extrai o suporte de dados pré-configurado para a unidade. Utilize o procedimento seguinte para criar o pacote do Windows To Go Creator.  

#### <a name="to-create-the-windows-to-go-creator-package"></a>Para criar o pacote do Windows To Go Creator  

1.  No servidor para alojar os ficheiros do pacote do Windows To Go Creator, crie uma pasta de origem para os ficheiros de origem do pacote.  

    > [!NOTE]  
    >  A conta de computador do servidor do site tem de ter direitos de acesso de **Leitura** para a pasta de origem.  

2.  Copie o ficheiro de suporte de dados pré-configurado criado na secção [Criar suportes de dados pré-configurados](#BKMK_CreatePrestagedMedia) para a pasta de origem do pacote.  

3.  Copie a ferramenta Windows To Go Creator (WTGCreator.exe) para a pasta de origem do pacote. A ferramenta de criação está disponível em qualquer servidor de site primário na seguinte localização: <*ConfigMgrInstallationFolder*> \OSD\Tools\WTG\Creator.  

4.  Crie um pacote e um programa utilizando o Assistente para Criar Pacote e Programa.  

5.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

6.  Na área de trabalho **Biblioteca de Software** , expanda **Gestão de Aplicações**e clique em **Pacotes**.  

7.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Pacote**.  

8.  Na página **Pacote** , especifique o nome e a descrição do pacote. Por exemplo, introduza **Windows To Go** para o nome do pacote e especifique **Package to configure a Windows To Go drive using System Center Configuration Manager** para a descrição do pacote.  

9. Selecione **Este pacote contém ficheiros de origem**, especifique o caminho da pasta de origem do pacote que criou no passo 1 e clique em **Seguinte**.  

10. Na página **Tipo de Programa** , selecione **Programa padrão**e clique em **Seguinte**.  

11. Na página **Programa Padrão** , especifique o seguinte:  

    -   **Nome**: Especifique o nome do programa. Por exemplo, escreva **Creator** para o nome do programa.  

    -   **Linha de comandos**: Tipo **WTGCreator.exe /wim: nomepré-Config.wim**, em que PrestageName é o nome do ficheiro pré-configurado que criou e copiou para a pasta de origem do pacote para o pacote Windows To Go Creator.  

         Opcionalmente, pode adicionar as seguintes opções:  

        -   **enableBootRedirect**: opção da linha de comandos para alterar as opções de arranque do Windows To Go para permitir o redirecionamento do arranque. Quando utilizar esta opção, o computador arrancará a partir do USB sem ter de alterar a ordem de arranque no firmware do computador ou o utilizador ter de selecionar a partir de uma lista de opções durante o arranque. Se for detetada uma unidade do Windows To Go, o computador arrancará nessa unidade.  

    -   **Executar**: Especifique **Normal** para executar o programa com base nas predefinições do sistema e do programa.  

    -   **Programa pode ser executado**: Especifique se o programa pode ser executado apenas quando um utilizador tiver sessão iniciado.  

    -   **Modo de execução**: Especifique se o programa será executado com o com sessão iniciada nas permissões de utilizadores ou com permissões administrativas. O Windows To Go Creator requer permissões elevadas para ser executado.  

    -   Selecione **Permitir que os utilizadores visualizem e interajam com a instalação do programa**e clique em **Seguinte**.  

12. Na página Requisitos, especifique o seguinte:  

    -   **Requisitos de plataforma**: Selecione as plataformas do Windows 8 aplicáveis para permitir o aprovisionamento.  

    -   **Espaço em disco estimado**: Especifica o tamanho da pasta de origem do pacote para o Windows To Go Creator.  

    -   **Máximo tempo de execução permitido (minutos)**: Especifica o tempo máximo que o programa poderá demorar a ser executado no computador cliente. Por predefinição, este valor é definido para 120 minutos.  

        > [!IMPORTANT]  
        >  Se estiver a utilizar janelas de manutenção para a coleção onde este programa é executado, pode ocorrer um conflito se o **Tempo máximo de execução permitido** for superior à janela de manutenção agendada. Se o tempo de execução máximo for definido para **Desconhecido**, começará durante a janela de manutenção, mas continuará a ser executado até concluir ou falhar depois de a janela de manutenção fechar. Se definir o tempo de execução máximo para um período específico (não definido para Desconhecido) que excede a duração de qualquer janela de manutenção, esse programa não será executado.  

        > [!NOTE]  
        >  Se o valor estiver definido como **desconhecido**, tempo de execução do Configuration Manager define o número máximo para 12 horas (720 minutos).  

        > [!NOTE]  
        >  Se o tempo máximo de execução (definido pelo utilizador ou como valor predefinido) for excedido, o Configuration Manager interrompe o programa se **executar com direitos administrativos** está selecionado e **permitir que os utilizadores visualizem e interajam com a instalação do programa** não estiver selecionada no **programa padrão** página.  

     Clique em **Seguinte** e conclua o assistente.  

###  <a name="BKMK_UpdateTaskSequence"></a> Atualizar a sequência de tarefas para ativar o BitLocker para o Windows To Go  
 O Windows To Go ativa o BitLocker numa unidade de arranque externa sem a utilização do TPM. Por conseguinte, terá de utilizar uma ferramenta separada para configurar o BitLocker na unidade do Windows To Go. Para ativar o BitLocker, terá de adicionar uma ação à sequência de tarefas após o passo **Configurar Windows e ConfigMgr** .  

> [!NOTE]  
>  O BitLocker para Windows To Go necessita de uma frase de acesso. No passo [Criar suportes de dados pré-configurados](#BKMK_CreatePrestagedMedia) , defina a frase de acesso enquanto parte de um comando pré-arranque utilizando a variável OSDBitLockerPIN.  

 Utilize o seguinte procedimento para atualizar a sequência de tarefas do Windows 8 para ativar o BitLocker para Windows To Go.  

#### <a name="to-update-the-windows-8-task-sequence-to-enable-bitlocker"></a>Para atualizar a sequência de tarefas do Windows 8 para ativar o BitLocker  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** , expanda **Gestão de Aplicações**e clique em **Pacotes**.  

3.  No separador **Home Page** , no grupo **Criar** , clique em **Criar Pacote**.  

4.  Na página **Pacote** , especifique o nome e a descrição do pacote. Por exemplo, escreva **BitLocker for Windows To Go** para o nome do pacote e especifique **Package to update BitLocker for Windows To Go** para a descrição do pacote.  

5.  Selecione **Este pacote contém ficheiros de origem**, especifique a localização para a ferramenta BitLocker para Windows To Go e clique em **Seguinte**. A ferramenta BitLocker está disponível em qualquer servidor de site primário do Configuration Manager na seguinte localização: <*ConfigMgrInstallationFolder*> \OSD\Tools\WTG\BitLocker\  

6.  Na página **Tipo de Programa** , selecione **Não criar um programa**.  

7.  Clique em **Seguinte** e conclua o assistente.  

8.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

9. Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**e clique em **Sequências de Tarefas**.  

10. Selecione a sequência de tarefas do Windows 8 que referencia nos suportes de dados pré-configurados.  

11. No separador **Home Page** , no grupo **Sequência de Tarefas** , clique em **Editar**.  

12. Clique no passo **Configurar Windows e ConfigMgr** , clique em **Adicionar**, clique em **Geral**e, em seguida, clique em **Executar Linha de Comandos**. O passo Executar Linha de Comandos é adicionado após o passo Configurar Windows e ConfigMgr.  

13. No separador **Propriedades** para o passo **Executar Linha de Comandos** , adicione o seguinte:  

    1.  **Nome**: Especifique um nome para a linha de comandos, tal como **ativar o BitLocker para Windows To Go**.  

    2.  **Linha de comandos**: i386\osdbitlocker_wtg.exe /Enable /pwd: < *None &#124; AD*>  

         Parâmetros:  

        -   /pwd: < none &#124; AD >-especificar o modo de recuperação de palavra-passe do BitLocker. Este parâmetro obriga que utilize o parâmetro /Enable na linha de comandos.  

             Selecione **AD** para configurar a Encriptação da Unidade do BitLocker para criar cópias de segurança das informações de recuperação para unidades protegidas pelo BitLocker para Serviços de Domínio do Active Directory (AD DS). Criar cópias de segurança de palavras-passe de recuperação para uma unidade protegida pelo BitLocker permite que os utilizadores administrativos recuperem a unidade se estiver bloqueada. Isto garante que os dados encriptados pertencentes à empresa podem ser sempre acedidos por utilizadores autorizados. Quando especificar **Nenhum**, o utilizador é responsável por manter uma cópia da palavra-passe de recuperação ou chave de recuperação. Se o utilizador perder essa informação ou negligenciar a desencriptação da unidade antes de abandonar a organização, os utilizadores administrativos não conseguem aceder facilmente à unidade.  

        -   /wait: < TRUE &#124; FALSE >-especificar se a sequência de tarefas aguarda que encriptação seja concluída antes da conclusão.  

    3.  Selecione **pacote**e, em seguida, especifique o pacote que criou no início deste procedimento.  

    4.  No separador **Opções** , adicione as seguintes condições:  

        -   Condição = Variável de Sequência de Tarefas  

        -   Variável = _SMSTSWTG  

        -   Condição = Igual a  

        -   Valor = Verdadeiro  

    > [!NOTE]  
    >  O passo **Ativar o BitLocker** , o mais provável depois do novo passo da linha de comandos, não é utilizado para ativar o BitLocker para Windows To Go. No entanto, pode manter este passo na sequência de tarefas a utilizar para implementações do Windows 8 que não utilizem uma unidade do Windows To Go.  

###  <a name="BKMK_Deployments"></a> Implementar o pacote do Windows To Go Creator e a sequência de tarefas  
 O Windows To Go é um processo de implementação híbrido. Por conseguinte, terá de implementar o pacote do Windows To Go Creator e a sequência de tarefas do Windows 8. Utilize os seguintes procedimentos para concluir o processo de implementação.  

#### <a name="to-deploy-the-windows-to-go-creator-package"></a>Para implementar o pacote do Windows To Go Creator  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** , expanda **Gestão de Aplicações**e clique em **Pacotes**.  

3.  Selecione o pacote Windows To Go que criou no Windows no passo [Criar um pacote do Windows To Go Creator](#BKMK_CreatePackage) .  

4.  No separador **Home Page** , no grupo **Implementação** , clique em **Implementar**.  

5.  Na página **Geral** , especifique as seguintes definições:  

    1.  **Software**: Certifique-se de que o pacote Windows To Go está selecionado.  

    2.  **Coleção**: Clique em **procurar** para selecionar a coleção à qual pretende implementar o pacote Windows To Go.  

    3.  **Utilizar grupos de pontos de distribuição predefinidos associados a esta coleção**: Selecione esta opção se pretender armazenar o conteúdo do pacote no grupo de ponto de distribuição da predefinição de coleções. Se não tiver associado a coleção selecionada a um grupo de pontos de distribuição, esta opção estará indisponível.  

6.  Na página **Conteúdo** , clique em **Adicionar** e, em seguida, selecione os pontos de distribuição ou os grupos de pontos de distribuição nos quais pretende implementar o conteúdo associado a este pacote e programa.  

7.  Na página **Definições de Implementação** , selecione **Disponível** para o tipo de implementação e, em seguida, clique em **Seguinte**.  

8.  No **Agendamento**, configure quando este pacote e programa serão implementados ou colocados à disposição dos dispositivos cliente.  

     As opções desta página serão diferentes consoante a ação de implementação esteja definida para **Disponível** ou **Necessária**.  

9. No **Agendamento**, confirme as seguintes definições e clique em **Seguinte**.  

    1.  **Agendar quando esta implementação ficará disponível**: Especifique a data e hora em que o pacote e programa está disponível para ser executada no computador de destino. Se selecionar **UTC**, esta definição garantirá que o pacote e programa ficarão disponíveis para vários computadores de destino ao mesmo tempo, em vez de em alturas diferentes, de acordo com a hora local dos computadores de destino.  

    2.  **Agendar quando esta implementação expirará**: Especifique a data e hora em que o pacote e programa expiram no computador de destino. Se selecionar **UTC**, esta definição garantirá que a sequência de tarefas expira em vários computadores de destino no mesmo tempo, em vez de tal acontecer em diferentes momentos, de acordo com a hora local dos computadores de destino.  

10. Na página **Experiência de Utilizador** do Assistente, especifique as seguintes informações:  

    -   **Instalação de software**: Permite que o software seja instalado fora de quaisquer janelas de manutenção configurada.  

    -   **Reinício do sistema (se for necessário para concluir a instalação)**: Permite que um dispositivo reinicie fora das janelas de manutenção configuradas quando exigido pela instalação do software.  

    -   **Dispositivos Embedded**: Quando implementa pacotes e programas em dispositivos Windows Embedded que tenham um filtro de escrita ativado, pode especificar a instalação de pacotes e programas na sobreposição temporária e confirmar as alterações mais tarde, ou confirmar as alterações no prazo de instalação ou durante uma janela de manutenção. Ao consolidar alterações no momento da instalação ou durante uma janela de manutenção, será necessário um reinício para que as alterações sejam mantidas no dispositivo.  

11. Na página **Pontos de Distribuição** , especifique as seguintes informações:  

    -   **Opções de implementação:** Especifique **transferir conteúdo do ponto de distribuição e executar localmente**.  

    -   **Permitir que os clientes partilhem conteúdos com outros clientes na mesma sub-rede**: Selecione esta opção para reduzir a carga na rede ao permitir que os clientes transfiram conteúdos a partir de outros clientes na rede que já tenham transferido e colocado o conteúdo na cache. Esta opção utiliza o Windows BranchCache e pode ser utilizada em computadores com o Windows Vista SP2 e posterior.  

    -   **Todos os clientes utilizem uma localização de origem de contingência para conteúdo**: Especifique se pretende permitir que os clientes revertam e utilizem um ponto de distribuição não preferencial como localização de origem de conteúdo quando o conteúdo não está disponível num ponto de distribuição preferencial.  

12. Conclua o assistente.  

#### <a name="to-deploy-the-windows-8-task-sequence"></a>Para implementar a sequência de tarefas do Windows 8  

1.  Na consola do Configuration Manager, clique em **Biblioteca de Software**.  

2.  Na área de trabalho **Biblioteca de Software** , expanda **Sistemas Operativos**e clique em **Sequências de Tarefas**.  

3.  Selecione a sequência de tarefas do Windows 8 que criou no passo [Prerequisites to provision Windows To Go](#BKMK_Prereqs) .  

4.  No separador **Home Page** , no grupo **Implementação** , clique em **Implementar**.  

5.  Na página **Geral** , especifique as seguintes definições:  

    1.  **Sequência de tarefas**: Certifique-se de que a sequência de tarefas do Windows 8 está selecionada.  

    2.  **Coleção**: Clique em **procurar** para selecionar a coleção que inclui todos os dispositivos para os quais um utilizador pode aprovisionar o Windows To Go.  

        > [!IMPORTANT]  
        >  Se os suportes de dados pré-configurados que criou na secção [Criar suportes de dados pré-configurados](#BKMK_CreatePrestagedMedia) utilizarem a variável SMSTSPreferredAdvertID, poderá implementar a sequência de tarefas na coleção **Todos os Sistemas** e especificar a definição **Apenas Windows PE (oculto)** na página **Conteúdo** . Porque a sequência de tarefas está oculta, só estará disponível para suportes de dados.  

    3.  **Utilizar grupos de pontos de distribuição predefinidos associados a esta coleção**: Selecione esta opção se pretender armazenar o conteúdo do pacote no grupo de ponto de distribuição da predefinição de coleções. Se não tiver associado a coleção selecionada a um grupo de pontos de distribuição, esta opção estará indisponível.  

6.  Na página **Definições de Implementação** , configure as seguintes definições e clique em **Seguinte**.  

    -   **Objetivo**: Selecione **disponíveis**. Quando implementar a sequência de tarefas num utilizador, este verá a sequência de tarefas publicada no Catálogo de Aplicações e poderá solicitá-la a pedido. Se implementar a sequência de tarefas num dispositivo, o utilizador irá ver a sequência de tarefas no Centro de Software e pode instalá-lo a pedido.  

    -   **Tornar disponível para o seguinte**: Especifique se a sequência de tarefas está disponível para clientes do Configuration Manager, suportes de dados ou PXE.  

        > [!IMPORTANT]  
        >  Utilize a definição **Apenas suportes de dados e PXE (oculto)** para implementações com sequências de tarefas automatizadas. Selecione **Permitir implementação de sistema operativo autónoma** e defina a variável SMSTSPreferredAdvertID como parte dos suporte de dados pré-configurados para que o computador arranque automaticamente para a implementação de Windows To Go, sem interação do utilizador quando deteta uma unidade do Windows To Go. Para mais informações sobre estas definições de suporte de dados pré-configurados, consulte a secção [Criar suportes de dados pré-configurados](#BKMK_CreatePrestagedMedia) .  

7.  Na página **Agendamento** , confirme as seguintes definições e clique em **Seguinte**.  

    1.  **Agendar quando esta implementação ficará disponível**: Especifique a data e hora em que a sequência de tarefas ficará disponível para ser executada no computador de destino. Se selecionar **UTC**, esta definição garantirá que a sequência de tarefa ficará disponível para vários computadores de destino ao mesmo tempo, em vez de em alturas diferentes, de acordo com a hora local dos computadores de destino.  

    2.  **Agendar quando esta implementação expirará**: Especifique a data e hora em que a sequência de tarefas expira no computador de destino. Se selecionar **UTC**, esta definição garantirá que a sequência de tarefas expira em vários computadores de destino no mesmo tempo, em vez de tal acontecer em diferentes momentos, de acordo com a hora local dos computadores de destino.  

8.  Na página **Experiência de Utilizador** , especifique as seguintes informações:  

    -   **Mostrar Progresso da sequência de tarefas**: Especifique se o cliente do Configuration Manager apresenta o progresso da sequência de tarefas.  

    -   **Instalação de software**: Especifique se o utilizador tem permissão para instalar o software fora das janelas de manutenção configuradas e depois da data agendada.  

    -   **Reinício do sistema (se for necessário para concluir a instalação)**: Permite que um dispositivo reinicie fora das janelas de manutenção configuradas quando exigido pela instalação do software.  

    -   **Dispositivos Embedded**: Quando implementa pacotes e programas em dispositivos Windows Embedded que tenham um filtro de escrita ativado, pode especificar a instalação de pacotes e programas na sobreposição temporária e confirmar as alterações mais tarde, ou confirmar as alterações no prazo de instalação ou durante uma janela de manutenção. Ao consolidar alterações no momento da instalação ou durante uma janela de manutenção, será necessário um reinício para que as alterações sejam mantidas no dispositivo.  

    -   **Os clientes baseados na Internet**: Especifique se a sequência de tarefas pode ser executada num cliente baseado na Internet. As operações que instalam software, por exemplo um sistema operativo, não são suportadas por esta definição. Só deve utilizar esta opção para sequências de tarefas genéricas, baseadas em scripts, que executem operações padrão do sistema operativo.  

9. Na página **Alertas** , especifique as definições de alerta pretendidas para esta implementação de sequências de tarefas e, em seguida, clique em **Seguinte**.  

10. Na página **Pontos de Distribuição** , especifique as seguintes informações e, em seguida, clique em **Seguinte**.  

    -   **Opções de implementação**: Selecione **transferir o conteúdo localmente quando necessário para executar a sequência de tarefas**.  

    -   **Se estiver disponível nenhum ponto de distribuição local, utilizar um ponto de distribuição remoto**: Especifique se os clientes podem utilizar pontos de distribuição localizados em redes lentas e pouco fiáveis para transferir o conteúdo necessário pela sequência de tarefas.  

    -   **Permitir que os clientes utilizem uma localização de origem de contingência para conteúdo**:
        - *Antes de versão 1610*, pode selecionar a permitir a localização de origem de contingência para conteúdo caixa de verificação para permitir que os clientes fora destes grupos de limites recorram à contingência e utilizem o ponto de distribuição como uma localização de origem de conteúdo quando não houver outros pontos de distribuição disponíveis.
        - *A partir da versão 1610*, já não pode configurar **permitir a localização de origem de contingência para conteúdo**.  Em vez disso, configure as relações entre grupos de limites que determinam quando um cliente pode começar a procurar grupos de limites adicionais para uma localização de origem de conteúdo válida. 

11. Conclua o assistente.  

###  <a name="BKMK_UserExperience"></a> O utilizador executa o Windows To Go Creator  
 Depois de implementar o pacote Windows To Go e a sequência de tarefas do Windows 8, o Windows To Go Creator fica disponível para o utilizador. O utilizador pode ir para o catálogo de software, ou o Centro de Software se o Windows To Go Creator foi implementado em dispositivos, e executar o programa Windows To Go Creator. Depois de o pacote de autor é transferido, será apresentado um ícone intermitente na barra de tarefas. Quando o utilizador clica no ícone, é apresentada uma caixa de diálogo para o utilizador selecionar a unidade do Windows To Go a aprovisionar (exceto se a /opção da linha de comandos da unidade for utilizada). Caso a unidade não satisfaça os requisitos para o Windows To Go ou caso a unidade não tenha espaço livre suficiente no disco para instalar a imagem, o programa de autor apresenta uma mensagem de erro. O utilizador pode verificar a unidade e a imagem que serão aplicadas a partir da página de confirmação. Enquanto o autor configura e prepara conteúdo para a unidade do Windows To Go, apresenta uma caixa de diálogo de progresso. Uma vez concluída a pré-configuração, o criador apresenta um aviso para reiniciar o computador para arrancar para a unidade do Windows To Go.  

> [!NOTE]  
>  Se não tiver ativado o redirecionamento do arranque enquanto parte da linha de comandos para o programa de autor na secção [Criar um pacote do Windows To Go Creator](#BKMK_CreatePackage) , é possível que o utilizador tenha de arrancar manualmente a unidade do Windows To Go em cada reinício do sistema.  

###  <a name="BKMK_ConfigureStageDrive"></a> O Configuration Manager configura e prepara a unidade do Windows To Go  
 Depois de o computador reiniciar a unidade do Windows To Go, a unidade arrancará no Windows PE e ligar-se-á ao ponto de gestão para obter a política para concluir a implementação do sistema operativo. O Configuration Manager configura e prepara a unidade. Depois do Gestor de configuração prepara a unidade, o utilizador pode reiniciar o computador para finalizar o processo de aprovisionamento (como juntar-se um domínio ou instalar aplicações). Este processo é o mesmo para qualquer suporte de dados pré-configurado.  

###  <a name="BKMK_UserLogsIn"></a> O utilizador inicia sessão no Windows 8  
 Depois do Configuration Manager concluir o processo de aprovisionamento e é apresentado o ecrã de bloqueio do Windows 8, o utilizador pode iniciar sessão no sistema operativo.  
