---
title: Criar e implementar uma aplicação
titleSuffix: Configuration Manager
description: Criar e implementar uma aplicação que contenha uma aplicação de linha de negócio e saiba como gerir aplicações com eficiência.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 3bd1e487-ea18-43c1-b7c3-acbd9b86d429
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 18f51e43e223b13c01d0c6bde5a30fe08af64f61
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53415461"
---
# <a name="create-and-deploy-an-application-with-system-center-configuration-manager"></a>Criar e implementar uma aplicação com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Neste tópico, irá avançar diretamente e criar uma aplicação com o System Center Configuration Manager. Neste exemplo, irá criar e implementar uma aplicação que contém uma aplicação de linha de negócio para PCs com Windows denominada **contoso. msi**, que deve ser instalada em todos os PCs que estejam a executar o Windows 10 na sua empresa. Ao longo do processo, irá aprender várias coisas que pode fazer para gerir aplicações com eficiência.  

 Este procedimento foi concebido para lhe dar uma visão geral de como criar e implementar aplicações do Configuration Manager. No entanto, não abrange toda a configuração opções ou como criar e implementar aplicações em outras plataformas.  

 Para obter detalhes específicos que são relevantes para cada plataforma, consulte um dos seguintes tópicos:  

-   [Criar aplicações Windows](../../apps/get-started/creating-windows-applications.md)  
-   [Criar aplicações iOS](../../apps/get-started/creating-ios-applications.md)  
-   [Criar aplicações Android](../../apps/get-started/creating-android-applications.md)  
-   [Criar aplicações Windows Phone](../../apps/get-started/creating-windows-phone-applications.md)  
-   [Criar aplicações para computadores Mac](../../apps/get-started/creating-mac-computer-applications.md)  
-   [Criar aplicações de servidor Linux e UNIX](../../apps/get-started/creating-linux-and-unix-server-applications.md)
-   [Criar aplicações Windows Embedded](../../apps/get-started/creating-windows-embedded-applications.md)


Se já estiver familiarizado com aplicações do Configuration Manager, pode ignorar este tópico. No entanto, pode querer rever [criem aplicativos](../../apps/deploy-use/create-applications.md) para saber mais sobre todas as opções que estão disponíveis quando criar e implementar aplicações.  

## <a name="before-you-start"></a>Antes de começar  

Certifique-se de que reviu as informações em [introdução à gestão de aplicações](/sccm/apps/understand/introduction-to-application-management) para que tem o site preparado para instalar aplicações e perceber a terminologia utilizada neste tópico.  

 Além disso, certifique-se de que os ficheiros de instalação do **contoso. msi** aplicação estão numa localização acessível na sua rede.  

## <a name="create-the-configuration-manager-application"></a>Criar a aplicação do Configuration Manager  

### <a name="to-start-the-create-application-wizard-and-create-the-application"></a>Para iniciar o Assistente para criar aplicação e criar a aplicação  

1. Na consola do Configuration Manager, escolha **biblioteca de Software** > **gestão de aplicações** > **aplicativos**.  

2. Sobre o **home page** separador a **criar** de grupo, escolha **Criar aplicação**.  

3. Na **gerais** página do **Assistente para criar aplicação**, escolha **detetar automaticamente informação sobre esta aplicação nos ficheiros de instalação**. Isto preenche antecipadamente algumas das informações no assistente com informações que são extraídas do ficheiro de instalação do. msi. Em seguida, especifique as seguintes informações:  

   -   **Tipo de**: Escolher **Windows Installer (\*arquivo. msi)**.  

   -   **Localização**: Escreva a localização (ou escolha **navegue** para selecionar a localização) do ficheiro de instalação **contoso. msi**. Tenha em atenção que a localização tem de ser especificada no formato  *\\\Server\Share\File* para o Configuration Manager para localizar os ficheiros de instalação.  

   Será apresentado algo semelhante à seguinte captura de ecrã:  

   ![Página geral do Assistente de gestão de aplicações](/sccm/apps/get-started/media/App-management-wizard-general-page.png)  

4. Selecione **Next**. Sobre o **importar informação** página, verá algumas informações sobre a aplicação e todos os ficheiros associados que foram importados para o Configuration Manager. Quando tiver terminado, escolha **seguinte** novamente.  

5. Sobre o **informações gerais** página, pode fornecer mais informações sobre a aplicação para ajudá-lo a ordená-la e localizá-la na consola do Configuration Manager.  

    Além disso, o **programa de instalação** campo permite-lhe especificar a linha de comandos completa que será utilizada para instalar a aplicação nos PCs. Pode editá-lo para adicionar as suas propriedades (por exemplo **/q** para uma instalação autónoma).  

   > [!TIP]  
   >  Alguns dos campos nesta página do assistente poderão ter sido preenchidos automaticamente quando importou os ficheiros de instalação da aplicação.  

    Será apresentado um ecrã semelhante à captura de ecrã seguinte:  

    ![Página de informações gerais do Assistente de gestão de aplicações](/sccm/apps/get-started/media/App-management-wizard-general-information-page.png)  

6. Selecione **Next**. Na página Resumo, pode confirmar as definições da aplicação e, em seguida, conclua o assistente.  

   Acabou de criar a aplicação. Para localizar, na **biblioteca de Software** área de trabalho, expanda **gestão de aplicações**e, em seguida, escolha **aplicativos**. Para este exemplo, será apresentado:  

   ![Gráfico de final do aplicativo](/sccm/apps/get-started/media/Final-app-graphic.png)  

## <a name="examine-the-properties-of-the-application-and-its-deployment-type"></a>Examinar as propriedades da aplicação e o respetivo tipo de implementação  

Agora que criou uma aplicação, pode refinar as definições da aplicação se precisar. Para ver as propriedades da aplicação, selecione a aplicação e, em seguida, no **home page** separador a **propriedades** de grupo, escolha **propriedades**.  

 Na **< Contoso\> propriedades da aplicação** caixa de diálogo, verá muitos itens que pode configurar para refinar o comportamento do aplicativo. Para obter detalhes sobre todas as definições que pode configurar, consulte [criem aplicativos](../../apps/deploy-use/create-applications.md). Para efeitos deste exemplo, irá alterar apenas algumas propriedades do tipo de implementação da aplicação.  

 Escolha o **tipos de implementação** separador > **aplicação Contoso** tipo de implementação > **editar**.  

Será apresentada uma caixa de diálogo como a seguinte:  

![Página de propriedades da aplicação de gestão de aplicações](/sccm/apps/get-started/media/App-management-app-properties-page.png)  

## <a name="add-a-requirement-to-the-deployment-type"></a>Adicionar um requisito ao tipo de implementação  
 Os requisitos especificam condições que têm ser satisfeitas para que uma aplicação possa ser instalada num dispositivo.  Pode escolher a partir de requisitos incorporados ou criar os seus próprios. Neste exemplo, adicionar um requisito que a aplicação só irá obter instalada em PCs que estão a executar o Windows 10.  

1.  A partir da página de propriedades de tipo de implementação acabou de abrir, selecione o **requisitos** separador.  

2.  Escolher **Add** para abrir o **criar requisito** caixa de diálogo.  

3.  Na caixa de diálogo **Criar Requisito** , especifique as seguintes informações:  

    -   **Categoria**: **Dispositivo**  

    -   **Condição**: **Sistema operativo**  

    -   **Tipo de regra**: **Valor**  

    -   **Operador**: **Um dos**  

    -   Na lista de sistemas operativos, selecione **Windows 10**.  

    Será apresentada uma caixa de diálogo semelhante à seguinte:  

    ![Página de requisitos de gestão de aplicações](/sccm/apps/get-started/media/App-management-requirements-page.png)  

4.  Escolher **OK** para fechar a cada página de propriedades que abriu. Em seguida, retorno para o **aplicativos** lista na consola do Configuration Manager.  

> [!TIP]  
>  Os requisitos podem ajudar a reduzir o número de coleções do Configuration Manager, que precisa. Uma vez que acabou de especificar que a aplicação apenas pode obter instalada em PCs que estão a executar o Windows 10, posteriormente, pode implementá-la numa coleção que contenha PCs com muitos sistemas operativos diferentes. Mas o aplicativo será apenas é instalado em Windows 10 PCs.  

## <a name="add-the-application-content-to-a-distribution-point"></a>Adicionar o conteúdo da aplicação a um ponto de distribuição  

Em seguida, para implementar a aplicação em PCs, certifique-se de que o conteúdo da aplicação foi copiado para um ponto de distribuição. O ponto de distribuição para instalar a aplicação de acesso de PCs.  

> [!TIP]  
>  Para obter mais informações sobre pontos de distribuição e gestão de conteúdos no Configuration Manager, veja [gerir a infraestrutura de conteúdo e conteúda](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

1.  Na consola do Configuration Manager, escolha **biblioteca de Software**.  

2.  Na **biblioteca de Software** área de trabalho, expanda **aplicativos**. Em seguida, na lista de aplicações, selecione o **aplicação Contoso** que criou.  

3.  Sobre o **home page** separador o **implementação** de grupo, escolha **distribuir conteúdo**.  

4.  Na **gerais** página do **Assistente para distribuir conteúdo**, verifique se o nome da aplicação está correto e, em seguida, escolha **seguinte**.  

5.  Sobre o **conteúdo** , reveja as informações que serão copiadas para o ponto de distribuição e, em seguida, escolha **próxima**.  

6.  Sobre o **destino do conteúdo** página, selecione **Add** para selecionar um ou mais pontos de distribuição ou grupos de pontos de distribuição em que pretende instalar o conteúdo da aplicação.  

7.  Conclua o assistente.  

Pode verificar se o conteúdo da aplicação foi copiado com êxito para o ponto de distribuição a partir da **monitorização** área de trabalho, em **estado de distribuição** > **conteúdo Estado**.  

## <a name="deploy-the-application"></a>Implementar a aplicação  

Em seguida, implemente a aplicação numa coleção de dispositivos na sua hierarquia. Neste exemplo, vai implementar a aplicação para o **todos os sistemas** coleção de dispositivos.  

> [!TIP]  
>  Lembre-se de que apenas os computadores Windows 10 irão instalar a aplicação devido aos requisitos que selecionou anteriormente.  

1.  Na consola do Configuration Manager, escolha **biblioteca de Software** > **gestão de aplicações** > **aplicativos**.  

3.  Na lista de aplicações, selecione a aplicação que criou anteriormente (**aplicação Contoso**) e, em seguida, no **home page** separador o **implementação** de grupo, selecione **Implementar**.  

4.  Na **gerais** página do **Assistente de implementação de Software**, escolha **procurar** para selecionar o **todos os sistemas** coleção de dispositivos.  

5.  Sobre o **conteúdo** página, verifique se o ponto de distribuição a partir do qual pretende que os PCs instalem a aplicação está selecionado.  

6.  Na **definições de implementação** página, certifique-se de que a ação de implementação está definida como **instalar**, e o objetivo da implementação está definido como **necessário**.  

    > [!TIP]  
    >  Ao definir o objetivo de implementação **necessário**, certifique-se de que a aplicação é instalada em PCs que cumprem os requisitos que definir. Se definir este valor como **Disponível**, os utilizadores poderão instalar a aplicação a pedido a partir do Centro de Software.  

7.  Na página **Agendamento** , pode configurar quando a aplicação será instalada. Para este exemplo, selecione **Logo que possível após o tempo disponível**.  

8.  Sobre o **experiência de utilizador** página, selecione **próxima** para aceitar os valores predefinidos.  

9. Conclua o assistente.  

Utilize as informações a seguir **monitorizar a aplicação** secção para ver o estado da implementação da aplicação.  

## <a name="monitor-the-application"></a>Monitorizar a aplicação  
 Nesta secção, irá dar uma olhada rápida o estado de implementação da aplicação que acabou de implementar.  

### <a name="to-review-the-deployment-status"></a>Para rever o estado de implementação  

1.  Na consola do Configuration Manager, escolha **monitorização** > **implementações**.  

3.  Na lista de implementações, selecione **Aplicação Contoso**.  

4.  Na **home page** separador a **implantação** de grupo, escolha **ver o estado**.  

5.  Selecione um dos seguintes separadores para ver mais atualizações de estado sobre a implementação da aplicação:  

    -   **Êxito**: A aplicação foi instalada com êxito nos PCs indicados.  

    -   **Em curso**: A aplicação não ainda acabou de instalar.  

    -   **Erro**: Ocorreu um erro ao instalar a aplicação nos PCs indicados. São também apresentadas mais informações sobre o erro.  

    -   **Requisitos não cumpridos**: Não foi efetuada nenhuma tentativa de instalação nos dispositivos indicados porque estes não cumpriam os requisitos que configurou (neste exemplo, uma vez que eles não são executados no Windows 10).  

    -   **Desconhecido**: O Configuration Manager não conseguiu comunicar o estado da implementação. Verifique novamente mais tarde.  

> [!TIP]  
>  Existem algumas maneiras, pode monitorizar implementações de aplicações. Para obter detalhes completos, veja [monitorizar aplicações](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

## <a name="end-user-experience"></a>Experiência do utilizador final  

Os utilizadores que têm PCs geridos pelo Configuration Manager e em execução com o Windows 10 veem uma mensagem que indica que têm de instalar a aplicação Contoso. Assim que aceitarem a instalação, a aplicação é instalada.  
