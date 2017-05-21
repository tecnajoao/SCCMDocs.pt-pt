---
title: "Criar e implementar uma aplicação | Documentos do Microsoft"
description: "Criar e implementar uma aplicação que contenha uma aplicação de linha de negócio e saiba como gerir aplicações de forma eficaz."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3bd1e487-ea18-43c1-b7c3-acbd9b86d429
caps.latest.revision: 15
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 6516db6f4c09fdd173b498c58ccc411847752c4e
ms.openlocfilehash: bbbf278f5d31c51bfe061dd44e170f7ab1ca70ad
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="create-and-deploy-an-application-with-system-center-configuration-manager"></a>Criar e implementar uma aplicação com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Neste tópico, terá de avançar diretamente e criar uma aplicação com o System Center Configuration Manager. Neste exemplo, terá de criar e implementar uma aplicação que contém uma aplicação de linha de negócio para PCs Windows denominado **Contoso.msi**, que tem de ser instalado em todos os computadores que executem o Windows 10 na sua empresa. Ao longo da forma, irá aprender sobre muitas das coisas que pode fazer para gerir aplicações de forma eficaz.  

 Este procedimento foi concebido para fornecer-lhe uma descrição geral de como criar e implementar aplicações do Configuration Manager. No entanto, não abrange a configuração de todas as opções, ou como criar e implementar aplicações para outras plataformas.  

 Para detalhes específicos que são relevantes para cada plataforma, consulte um dos seguintes tópicos:  

-   [Criar aplicações do Windows](../../apps/get-started/creating-windows-applications.md)  
-   [Criar aplicações iOS](../../apps/get-started/creating-ios-applications.md)  
-   [Criar aplicações Android](../../apps/get-started/creating-android-applications.md)  
-   [Criar aplicações do Windows Phone](../../apps/get-started/creating-windows-phone-applications.md)  
-   [Criar aplicações de computador Mac](../../apps/get-started/creating-mac-computer-applications.md)  
-   [Criar aplicações de servidor Linux e UNIX](../../apps/get-started/creating-linux-and-unix-server-applications.md)
-   [Criar aplicações Windows Embedded](../../apps/get-started/creating-windows-embedded-applications.md)


Se já estiver familiarizado com as aplicações do Configuration Manager, pode ignorar este tópico. No entanto, pode querer rever [criar aplicações](../../apps/deploy-use/create-applications.md) para saber mais sobre todas as opções que estão disponíveis quando criar e implementar aplicações.  

## <a name="before-you-start"></a>Antes de começar  

Certifique-se de que a reviu as informações na [introdução à gestão de aplicações](/sccm/apps/understand/introduction-to-application-management) para que se preparou o seu site para instalar aplicações e perceber a terminologia que é utilizada neste tópico.  

 Além disso, certifique-se de que a instalação de ficheiros para o **Contoso.msi** app estão numa localização acessível na sua rede.  

## <a name="create-the-configuration-manager-application"></a>Criar a aplicação do Configuration Manager  

### <a name="to-start-the-create-application-wizard-and-create-the-application"></a>Para iniciar o Assistente para criar aplicação e criar a aplicação  

1.  Na consola do Configuration Manager, escolha **biblioteca de Software** > **gestão de aplicações** > **aplicações**.  

3.  No **base** separador o **criar** grupo, selecione **Criar aplicação**.  

4.  No **geral** página do **Assistente para criar aplicação**, escolha **detetar automaticamente informação sobre esta aplicação nos ficheiros de instalação**. Isto preenche algumas das informações no assistente com as informações que são extraídas de ficheiro. msi de instalação. Em seguida, especifique as seguintes informações:  

    -   **Tipo de**: Escolher **do Windows Installer (\*ficheiro. msi)**.  

    -   **Localização**: Escreva a localização (ou escolha **procurar** para selecionar a localização) do ficheiro de instalação **Contoso.msi**. Tenha em atenção que a localização tem de ser especificada no formulário  *\\\Server\Share\File* para o Configuration Manager para localizar os ficheiros de instalação.  

    Acabará com algo que se pareça com a seguinte captura de ecrã:  

    ![Página geral do Assistente de gestão de aplicação](/sccm/apps/get-started/media/App-management-wizard-general-page.png)  

5.  Escolher **seguinte**. No **importar informação** página, verá algumas informações sobre a aplicação e todos os ficheiros associados que foram importados para o Configuration Manager. Quando tiver terminado, selecione **seguinte** novamente.  

6.  No **informações gerais** página, pode fornecer mais informações sobre a aplicação para o ajudar a ordenar e localizá-lo na consola do Configuration Manager.  

     Além disso, o **programa de instalação** campo permite-lhe especificar a linha de comandos completa que será utilizada para instalar a aplicação nos PCs. Pode editar esta opção para adicionar as propriedades do seu próprio (por exemplo **/q** para a instalação automática).  

    > [!TIP]  
    >  Alguns dos campos nesta página do assistente poderão ter sido preenchidos automaticamente quando importou os ficheiros de instalação da aplicação.  

     Acabará com um ecrã semelhante a seguinte captura de ecrã:  

     ![Página de informações gerais do Assistente de gestão de aplicações](/sccm/apps/get-started/media/App-management-wizard-general-information-page.png)  

7.  Escolher **seguinte**. Na página Resumo, pode confirmar as definições da aplicação e, em seguida, conclua o assistente.  

 Acabou de criar a aplicação. Para localizá-lo, além de **biblioteca de Software** área de trabalho, expanda **gestão de aplicações**e, em seguida, escolha **aplicações**. Para este exemplo, será apresentado:  

 ![Gráfico de aplicação final](/sccm/apps/get-started/media/Final-app-graphic.png)  

## <a name="examine-the-properties-of-the-application-and-its-deployment-type"></a>Examinar as propriedades da aplicação e o respetivo tipo de implementação  

Agora que criou uma aplicação, pode refinar as definições da aplicação se for necessário. Para ver as propriedades da aplicação, selecione a aplicação e, em seguida, no **base** separador o **propriedades** grupo, selecione **propriedades**.  

 No **< Contoso\> propriedades da aplicação** caixa de diálogo, verá que muitos dos itens que pode configurar para otimizar o comportamento da aplicação. Para obter detalhes sobre todas as definições que pode configurar, consulte o artigo [criar aplicações](../../apps/deploy-use/create-applications.md). Para efeitos deste exemplo, irá alterar apenas algumas propriedades do tipo de implementação da aplicação.  

 Escolha o **tipos de implementação** separador > **Contoso aplicação** tipo de implementação > **editar**.     

Será apresentada uma caixa de diálogo como a seguinte:  

![Página de propriedades da aplicação de gestão de aplicações](/sccm/apps/get-started/media/App-management-app-properties-page.png)  

## <a name="add-a-requirement-to-the-deployment-type"></a>Adicionar um requisito ao tipo de implementação  
 Os requisitos especificam condições que têm ser satisfeitas para que uma aplicação possa ser instalada num dispositivo.  Pode escolher a partir de requisitos incorporados, ou pode criar o seu próprio. Neste exemplo, adicione um requisito que a aplicação apenas irá obter instalada nos computadores que executem o Windows 10.  

1.  A página de propriedades de tipo de implementação que acabou de abrir, escolha o **requisitos** separador.  

2.  Escolher **adicionar** para abrir o **criar requisito** caixa de diálogo.  

3.  Na caixa de diálogo **Criar Requisito** , especifique as seguintes informações:  

    -   **Categoria**: **Dispositivo**  

    -   **Condição**: **Sistema operativo**  

    -   **Tipo de regra**: **Valor**  

    -   **Operador**: **Uma das**  

    -   Na lista de sistemas operativos, selecione **Windows 10**.  

    Será apresentada uma caixa de diálogo semelhante à seguinte:  

    ![Página de requisitos de gestão de aplicações](/sccm/apps/get-started/media/App-management-requirements-page.png)  

4.  Escolher **OK** para fechar cada página de propriedades que tenha aberto. Em seguida, regressar à **aplicações** lista na consola do Configuration Manager.  

> [!TIP]  
>  Requisitos de ajuda a reduzir o número de coleções do Configuration Manager que necessita. Uma vez que acabou de especificar que a aplicação apenas pode obter instalada nos computadores que executem o Windows 10, pode implementar este mais tarde para uma coleção que contenha PCs com muitos sistemas operativos diferentes. Mas a aplicação apenas irá obter instalada no Windows 10 PCs.  

## <a name="add-the-application-content-to-a-distribution-point"></a>Adicionar o conteúdo da aplicação a um ponto de distribuição  

Em seguida, implementar a aplicação em PCs, certifique-se de que o conteúdo da aplicação é copiado para um ponto de distribuição. PCs que acedem ao ponto de distribuição para instalar a aplicação.  

> [!TIP]  
>  Para obter mais informações sobre pontos de distribuição e gestão de conteúdo no Configuration Manager, consulte o artigo [gerir a infraestrutura do conteúdo e conteúda](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

1.  Na consola do Configuration Manager, escolha **biblioteca de Software**.  

2.  No **biblioteca de Software** área de trabalho, expanda **aplicações**. Em seguida, na lista de aplicações, selecione o **Contoso aplicação** que criou.  

3.  No **base** separador o **implementação** grupo, selecione **distribuir conteúdo**.  

4.  No **geral** página do **Assistente para distribuir conteúdo**, verifique se o nome da aplicação está correto e, em seguida, selecione **seguinte**.  

5.  No **conteúdo** página, reveja as informações que vai ser copiadas para o ponto de distribuição e, em seguida, escolha **seguinte**.  

6.  No **conteúdo destino** página, selecione **adicionar** para selecionar um ou mais pontos de distribuição ou grupos de pontos de distribuição em que pretende instalar o conteúdo da aplicação.  

7.  Conclua o assistente.  

Pode verificar que o conteúdo da aplicação foi copiado com êxito para o ponto de distribuição a partir de **monitorização** área de trabalho, em **estado da distribuição** > **estado do conteúdo**.  

## <a name="deploy-the-application"></a>Implementar a aplicação  

Em seguida, implemente a aplicação numa coleção de dispositivos na sua hierarquia. Neste exemplo, implementar a aplicação a **todos os sistemas** coleção de dispositivos.  

> [!TIP]  
>  Lembre-se de que apenas os computadores Windows 10 irão instalar a aplicação devido aos requisitos que selecionou anteriormente.  

1.  Na consola do Configuration Manager, escolha **biblioteca de Software** > **gestão de aplicações** > **aplicações**.  

3.  Na lista de aplicações, selecione a aplicação que criou anteriormente (**Contoso aplicação**) e, em seguida, no **base** separador o **implementação** grupo, selecione **implementar**.  

4.  No **geral** página do **Assistente de implementação de Software**, escolha **procurar** para selecionar o **todos os sistemas** coleção de dispositivos.  

5.  No **conteúdo** página, verifique que o ponto de distribuição a partir do qual pretende PCs para instalar a aplicação está selecionado.  

6.  No **definições de implementação** página, certifique-se de que a ação de implementação está definida para **instalar**, e o objetivo de implementação está definido para **necessário**.  

    > [!TIP]  
    >  Ao definir o objetivo de implementação para **necessário**, certificar-se de que a aplicação é instalada em computadores que cumprem os requisitos que definir. Se definir este valor como **Disponível**, os utilizadores poderão instalar a aplicação a pedido a partir do Centro de Software.  

7.  Na página **Agendamento** , pode configurar quando a aplicação será instalada. Para este exemplo, selecione **Logo que possível após o tempo disponível**.  

8.  No **experiência de utilizador** página, selecione **seguinte** para aceitar os valores predefinidos.  

9. Conclua o assistente.  

Utilize as informações nas seguintes **monitorizar a aplicação** secção para ver o estado da implementação da aplicação.  

## <a name="monitor-the-application"></a>Monitorizar a aplicação  
 Nesta secção, irá demorar um breve olhar o estado de implementação da aplicação que acabou de ser implementada.  

### <a name="to-review-the-deployment-status"></a>Para rever o estado de implementação  

1.  Na consola do Configuration Manager, escolha **monitorização** > **implementações**.  

3.  Na lista de implementações, selecione **Aplicação Contoso**.  

4.  No **base** separador o **implementação** grupo, selecione **Ver estado**.  

5.  Selecione uma das seguintes separadores para ver as atualizações de estado mais sobre a implementação da aplicação:  

    -   **Êxito**: A aplicação instalada com êxito nos PCs indicados.  

    -   **Em curso**: A aplicação não ainda concluiu a instalação.  

    -   **Erro**: Erro ao instalar a aplicação nos PCs indicados. São também apresentadas mais informações sobre o erro.  

    -   **Requisitos não cumpridos**: Não foi efetuada nenhuma tentativa de instalação nos dispositivos indicados porque não cumpria os requisitos que configurou (neste exemplo, uma vez que estes não são executadas no Windows 10).  

    -   **Desconhecido**: O Configuration Manager não conseguiu comunicar o estado da implementação. Verifique novamente mais tarde.  

> [!TIP]  
>  Existem algumas formas que pode monitorizar implementações de aplicações. Para mais informações, consulte o artigo [monitorizar aplicações](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

## <a name="end-user-experience"></a>Experiência do utilizador final  

Os utilizadores que têm PCs que são geridos pelo Configuration Manager e em execução Windows 10 veem uma mensagem a informar que o tem de instalar a aplicação de Contoso. Assim que aceitam a instalação, a aplicação é instalada.  

