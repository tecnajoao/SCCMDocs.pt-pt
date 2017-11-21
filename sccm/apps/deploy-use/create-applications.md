---
title: "Criar aplicações"
titleSuffix: Configuration Manager
description: "Criar e implementar aplicações e tipos de implementação com o System Center Configuration Manager."
ms.custom: na
ms.date: 11/07/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
caps.latest.revision: "14"
caps.handback.revision: "0"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: f680b692f3ae92fb8a5e8b6640ed053ceedba436
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 11/21/2017
---
# <a name="create-applications-with-system-center-configuration-manager"></a>Criar aplicações com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Uma aplicação do System Center Configuration Manager tem os ficheiros e informações necessários para implementar software num dispositivo. Uma aplicação tem um ou mais tipos de implementação que compõem os ficheiros de instalação e informações que são necessários para instalar o software. Um tipo de implementação tem também as regras que especificam quando e como o software é implementado.  

 Pode criar aplicações utilizando os seguintes métodos:  

-   Crie automaticamente os tipos de aplicação e implementação ao ler os ficheiros de instalação da aplicação.  

-   Criar manualmente a aplicação e adicionar posteriormente os tipos de implementação.  

-   Importe uma aplicação de um ficheiro.  

> [!NOTE]  
>  [Criar aplicações para dispositivos móveis](../../mdm/deploy-use/create-applications.md) fornece informações detalhadas sobre como criar aplicações Android, iOS e Windows Phone.  

Utilize os seguintes passos para criar aplicações do Configuration Manager e tipos de implementação.  

## <a name="start-the-create-application-wizard"></a>Iniciar o Assistente para criar aplicação  

1.  Na consola do Configuration Manager, escolha **biblioteca de Software** > **gestão de aplicações** > **aplicações**.  

3.  No **home page** separador o **criar** grupo, escolha **Criar aplicação**.  

## <a name="specify-whether-you-want-to-automatically-detect-application-information-or-manually-define-the-information"></a>Especifique se pretende detetar automaticamente informações sobre a aplicação ou definir manualmente as informações  

-   Deteta automaticamente informações sobre a aplicação quando pretender criar uma aplicação simples que tem um tipo de implementação única, como um ficheiro do Windows Installer sem dependências ou requisitos. Depois de criar uma aplicação utilizando este procedimento, pode editá-la conforme necessário para adicionar ou alterar tipos de implementação e adicionar métodos de deteção, dependências ou requisitos.  

-   Especificar manualmente informações sobre a aplicação para criar aplicações mais complexas que possuem vários tipos de implementação, dependências, métodos de deteção ou requisitos.  

### <a name="automatically-detect-application-information"></a>Detetar automaticamente informações sobre a aplicação  

1.  No **geral** página do Assistente Criar aplicação, selecione **detetar automaticamente informação sobre esta aplicação nos ficheiros de instalação**.  

2.  No **tipo** na lista pendente, selecione a instalação da aplicação tipo de ficheiro que pretende utilizar para detetar informações sobre a aplicação. Para obter informações sobre os tipos de instalação disponíveis, veja [Tipos de implementação suportados pelo Configuration Manager](/sccm/apps/deploy-use/create-applications#deployment-types-supported-by-configuration-manager) neste tópico.  

3.  No **localização** caixa, especifique o caminho UNC (no formato * \\ \\servidor\\partilhar\\\filename*) ou a hiperligação do arquivo para o ficheiro de instalação da aplicação que pretende utilizar para detetar informações sobre a aplicação. Em alternativa, clique em **Procurar** para procurar o ficheiro de instalação.  

    > [!IMPORTANT]  
    >  Quando seleciona **do Windows Installer (\*ficheiro. msi)** como um tipo de aplicação, todos os ficheiros na pasta que especificar serão importados com a aplicação e serão enviados para os pontos de distribuição. Certifique-se de que a pasta que especificou contém apenas os ficheiros que são necessários para instalar a aplicação. O Configuration Manager é testado para suportar até 20.000 ficheiros de aplicação no pacote de aplicação. Se a sua aplicação tiver mais ficheiros, considere criar múltiplas aplicações que têm um número mais pequeno de ficheiros.  

    >  Tem de ter acesso ao caminho UNC que tenha a aplicação e eventuais subpastas que contêm o conteúdo da aplicação.  

4.  No **importar informação** página do Assistente para criar aplicação, reveja as informações que foi importadas e, em seguida, escolha **seguinte**. Se necessário, pode escolher **anterior** para voltar atrás e corrigir os eventuais erros.  

5.  No **informações gerais** página do Assistente para criar aplicação, especifique as seguintes informações:  

    > [!NOTE]  
    >  Algumas dessas informações poderão já ter sido preenchidas se tiverem sido obtidas automaticamente a partir dos ficheiros de instalação da aplicação. Além disso, as opções apresentadas poderão ser diferentes dependendo do tipo de aplicação que criou.  

    -   Informações gerais acerca da aplicação, como o nome da aplicação, comentários, versão e uma referência opcional para ajudar a encontrar a aplicação na consola do Configuration Manager.  

    -   **Programa de instalação**– especifique o programa de instalação e quaisquer necessárias propriedades que são necessários para instalar o tipo de implementação de aplicação.  

        > [!TIP]  
        >  Se o programa de instalação não aparecer, escolha **procurar** e navegue até à localização do programa de instalação.  

    -   **Comportamento de instalação**-especificar se o tipo de implementação de aplicação será instalado para apenas o utilizador com sessão atualmente iniciada ou para todos os utilizadores. Também pode especificar que o tipo de implementação será instalado para todos os utilizadores se for implementado num dispositivo ou apenas a um utilizador específico se for implementado num utilizador.  

    -   **Utilizar uma ligação VPN automática (se configurada)**– se um perfil da VPN tiver sido implementado no dispositivo onde a aplicação foi lançada, lance a ligação VPN quando a aplicação for iniciada (Windows 8.1 e Windows Phone 8.1 apenas).  

         Em dispositivos Windows Phone 8.1, as ligações VPN automáticas não são suportadas se mais do que um perfil da VPN tiver sido implementado no dispositivo.  

         Para obter mais informações sobre perfis da VPN, consulte [perfis VPN](../../protect/deploy-use/vpn-profiles.md).  

6.  Escolha **seguinte**, reveja as informações da aplicação no **resumo** página e, em seguida, conclua o Assistente para criar aplicação.  

A nova aplicação aparece no **aplicações** nós da consola do Configuration Manager e concluir a criação de uma aplicação. Se pretender adicionar mais tipos de implementação à aplicação, veja [Criar tipos de implementação para a aplicação](/sccm/apps/deploy-use/create-applications#create-deployment-types-for-the-application) neste tópico.  

### <a name="manually-specify-application-information"></a>Especificar manualmente informações sobre a aplicação  

1.  No **geral** página do Assistente Criar aplicação, selecione **especificar manualmente as informações da aplicação**e, em seguida, escolha **seguinte**.  

2.  Especificar informações gerais acerca da aplicação, como o nome da aplicação, comentários, versão e uma referência opcional para ajudar a encontrar a aplicação na consola do Configuration Manager.  

3.  No **catálogo de aplicações** página do Assistente para criar aplicação, especifique as seguintes informações:  

    -   **Idioma selecionado**– na lista pendente, selecione a versão de idioma da aplicação que pretende configurar. Escolha **Adicionar/remover** para configurar mais idiomas para esta aplicação.  

    -   **Nome da aplicação localizada**– especifique o nome da aplicação no idioma que selecionou no **idioma selecionado** na lista pendente.  

        > [!IMPORTANT]  
        >  Tem de especificar um nome da aplicação localizada para cada versão de idioma que configurou.  

    -   **Categorias de utilizador**– escolha **editar** para especificar categorias de aplicação no idioma que selecionou no **idioma selecionado** na lista pendente. Os utilizadores do Centro de Software podem utilizar estas categorias selecionadas para ajudar a filtrar e ordenar as aplicações disponíveis.  

    -   **Documentação do utilizador**– escolha **procurar** para especificar o URL ou o nome de ficheiro e caminho UNC de um ficheiro que os utilizadores do Centro de Software podem ler para obter mais informações sobre esta aplicação.  

    -   **Texto da hiperligação**– especifique o texto que irá aparecer em vez do URL da aplicação.  

    -   **URL de privacidade da aplicação**– Especifique um URL que liga à declaração de privacidade para a aplicação.  

    -   **Descrição localizada**-introduza uma descrição para esta aplicação no idioma que selecionou no **idioma selecionado** na lista pendente.  

    -   **As palavras-chave**-introduza uma lista de palavras-chave no idioma que selecionou no **idioma selecionado** na lista pendente. Estas palavras-chave vai ajudar os utilizadores de pesquisa de centro de Software para a aplicação.  

    -   **Ícone**– escolha **procurar** para selecionar um ícone para esta aplicação a partir dos ícones disponíveis. Se não especificar um ícone, será utilizado um ícone predefinido para esta aplicação. Agora pode definir um ícone com um dimensões de pixel de até 512 x 512.

    -   **Apresentar esta aplicação como uma aplicação em destaque e destacá-la no portal da empresa**– Selecione esta opção para apresentar a aplicação de forma destacada no portal da empresa.  

4.  No **tipos de implementação** página do Assistente para criar aplicação, escolha **adicionar** para criar um novo tipo de implementação.  

 Para obter mais informações, consulte [criar tipos de implementação para a aplicação](/sccm/apps/deploy-use/create-applications#create-deployment-types-for-the-application).  

5.  Escolha **seguinte**, reveja as informações da aplicação no **resumo** página e, em seguida, conclua o Assistente para criar aplicação.  

A nova aplicação aparece no **aplicações** nós da consola do Configuration Manager.  

##  <a name="create-deployment-types-for-the-application"></a>Criar tipos de implementação para a aplicação  
 Se selecionar **identificar automaticamente informações sobre este tipo de implementação nos ficheiros de instalação** no **geral** página do Assistente para criar tipo de implementação, poderá não ser necessário concluir a alguns dos passos nos seguintes procedimentos.  

## <a name="start-the-create-deployment-type-wizard"></a>Iniciar o assistente para criar tipo de implementação  

1.  Na consola do Configuration Manager, escolha **biblioteca de Software** > **gestão de aplicações** > **aplicações**.  

3.  Selecione uma aplicação e, em seguida, no **home page** separador o **aplicação** grupo, escolha **criar tipo de implementação**.  

> [!TIP]  
>  Também pode iniciar o Assistente para criar tipo de implementação do Assistente para criar aplicação e do **tipos de implementação** separador do *< nome da aplicação\> * **propriedades** caixa de diálogo.  

## <a name="specify-whether-you-want-to-automatically-detect-deployment-type-information-or-manually-set-up-the-information"></a>Especifique se pretende detetar automaticamente informações de tipo de implementação ou configurar manualmente as informações  
 Utilize um dos seguintes procedimentos para detetar automaticamente ou definir manualmente informações de tipo de implementação.  

### <a name="automatically-detect-deployment-type-information"></a>Detetar automaticamente informações de tipo de implementação  

1.  No **geral** página do assistente criar tipo de implementação, selecione **identificar automaticamente informações sobre este tipo de implementação nos ficheiros de instalação**.  

2.  No **tipo** caixa, selecione o tipo de ficheiro de instalação de aplicações que pretende utilizar para detetar as informações de tipo de implementação.  

3.  No **localização** caixa, especifique o caminho UNC (no formato * \\ \\servidor\\partilhar\\filename*) ou especificar a hiperligação do arquivo para os ficheiros de instalação da aplicação e o conteúdo que pretende utilizar para detetar as informações de tipo de implementação. Também pode optar por **procurar** para localizar o ficheiro de instalação.  

    > [!NOTE]  
    >  Tem de ter acesso ao caminho UNC que tenha a aplicação e eventuais subpastas que contêm o conteúdo da aplicação.  

4.  No **importar informação** página do Assistente para criar tipo de implementação, reveja as informações que foi importadas e, em seguida, escolha **seguinte**. Também pode optar por **anterior** para voltar atrás e corrigir os eventuais erros.  

5.  No **informações gerais** página do Assistente para criar tipo de implementação, especifique as seguintes informações:  

    > [!NOTE]  
    >  Algumas das informações sobre o tipo de implementação podem já estar presentes se já foram lidas nos ficheiros de instalação da aplicação. Além disso, as opções apresentadas poderão diferir, consoante o tipo de implementação que está a criar.  

    -   Informações gerais sobre o tipo de implementação, como o nome, comentários de administrador e idiomas disponíveis.  

    -   **Programa de instalação**– especifique o programa de instalação e eventuais propriedades de que necessita para instalar o tipo de implementação.  

    -   **Comportamento de instalação**-especificar se pretende instalar o tipo de implementação para o utilizador atual, ou para todos os utilizadores. Também pode especificar se pretende instalar o tipo de implementação para todos os utilizadores se for implementado num dispositivo, ou se pretende instalar a implementação de tipo para um utilizador apenas se for implementado num utilizador.  

    -   **Utilizar uma ligação VPN automática (se configurada)**– se um perfil da VPN tiver sido implementado no dispositivo onde a aplicação foi lançada, lance a ligação VPN quando a aplicação for iniciada (Windows 8.1 e Windows Phone 8.1 apenas). Se múltiplos perfis da VPN tiverem sido implementados num dispositivo Windows 8.1, o primeiro perfil da VPN implementado é utilizado por predefinição.  

         Em dispositivos Windows Phone 8.1, as ligações VPN automáticas não são suportadas se mais do que um perfil da VPN tiver sido implementado no dispositivo.  

         Para obter mais informações sobre perfis da VPN, consulte [perfis VPN no System Center Configuration Manager](../../protect/deploy-use/vpn-profiles.md).  

6.  Escolha **seguinte**e, em seguida, continuar a [especificar opções de conteúdo para o tipo de implementação](/sccm/apps/deploy-use/create-applications#specify-content-options-for-the-deployment-type).  

### <a name="manually-set-up-the-deployment-type-information"></a>Configurar manualmente as informações de tipo de implementação  

1.  No **geral** página do assistente criar tipo de implementação, selecione **especificar manualmente as informações de tipo de implementação**.  

2.  No **tipo** caixa, escolha o tipo de ficheiro de instalação de aplicações que pretende utilizar para detetar as informações de tipo de implementação. Pode escolher os mesmos tipos de instalação que utilizaria quando detetar automaticamente as informações de tipo de implementação e também pode especificar um script para instalar o tipo de implementação.  

3.  No **informações gerais** página do Assistente para criar tipo de implementação, especifique um nome para o tipo de implementação, uma descrição opcional e os idiomas em que pretende disponibilizar este tipo de implementação e, em seguida, escolha **seguinte**.  

4.  Continue para [Especificar as opções de conteúdo do tipo de implementação](/sccm/apps/deploy-use/create-applications#specify-content-options-for-the-deployment-type).  

##  <a name="specify-content-options-for-the-deployment-type"></a>Especificar opções de conteúdo para o tipo de implementação  

1.  No **conteúdo** página do Assistente para criar tipo de implementação, especifique as seguintes informações:  

    -   **Localização de conteúdo**– especifique a localização do conteúdo para este tipo de implementação, ou selecione **procurar** para escolher a pasta de conteúdo de tipo de implementação.  

        > [!IMPORTANT]  
        >  A conta de sistema do computador do servidor do site tem de ter permissões para a localização de conteúdos que especificar.  

    -   **Definições de conteúdo de desinstalação**-especifique uma das seguintes opções:
        - **Igual à instalar conteúdo**– Selecione esta opção se a instalação e desinstalação de conteúdo são os mesmos. Este é o comportamento predefinido.
        - **Não desinstale conteúdo**– Selecione esta opção se a aplicação não precisa de conteúdo de desinstalação.
        - **Diferente do conteúdo de instalação**– Selecione esta opção se o conteúdo de desinstalação é diferente do conteúdo de instalação.

4. Se tiver selecionado **Different do conteúdo de instalação**, navegue para ou introduza a localização do conteúdo de aplicação que é utilizado para desinstalar a aplicação.
5. Clique em **OK** para fechar a caixa de diálogo de propriedades de tipo de implementação.

    -   **Manter conteúdo na cache do cliente**– Selecione esta opção para especificar se o conteúdo deve ser mantido na cache no computador cliente indefinidamente, mesmo que já tenha sido executado. Embora esta opção pode ser útil em algumas implementações, como software baseado no Windows Installer que necessita de uma cópia local da origem fique disponível para aplicar atualizações, reduzirá o espaço disponível na cache. Se selecionar esta opção, pode provocar uma implementação de grande dimensão falhar posteriormente caso a cache não tem espaço livre suficiente.  

    -   **Permitir que os clientes partilhem conteúdos com outros clientes na mesma sub-rede**– Selecione esta opção para reduzir a carga na rede ao permitir que os clientes transfiram conteúdos a partir de outros clientes na rede que já tenham transferido e colocado o conteúdo na cache locais. Esta opção utiliza a tecnologia BranchCache do Windows.  

    -   **Programa de instalação**– especifique o nome do programa de instalação e quaisquer parâmetros de instalação necessários ou escolha **procurar** para localizar o ficheiro de instalação.  

    -   **Início da instalação em**-opcionalmente, especifique a pasta que tem o programa de instalação para o tipo de implementação. Esta pasta pode ser um caminho absoluto no cliente ou um caminho para a pasta do ponto de distribuição que tenha os ficheiros de instalação.  

    -   **Desinstalar programa**-opcionalmente, especifique o nome do programa de desinstalação e quaisquer parâmetros necessários, ou escolha **procurar** a localizá-la.  

    -   **Iniciar desinstalação em**-opcionalmente, especifique a pasta que tem o programa de desinstalação para o tipo de implementação. Esta pasta pode ser um caminho absoluto no cliente ou um caminho relativo para a pasta do ponto de distribuição que tenha o pacote.  

    -   **Execute a instalação e desinstalação como um processo de 32 bits em clientes de 64 bits**-utilize as localizações de ficheiros e registo de 32 bits em computadores baseados em Windows para executar o programa de instalação para o tipo de implementação.  

2.  Escolha **seguinte**.  

## <a name="set-up-detection-methods-to-indicate-the-presence-of-the-deployment-type-windows-pcs-only"></a>Configurar métodos de deteção para indicar a presença do tipo de implementação (apenas PCs Windows)  
 Este procedimento configura um método de deteção que indica se o tipo de implementação já está instalado.  

1.  No **método de deteção** página do assistente criar tipo de implementação, selecione **configurar regras para detetar a presença deste tipo de implementação**e, em seguida, escolha **Adicionar cláusula**.  

    > [!NOTE]  
    >  Também pode selecionar **Utilizar um script personalizado para detetar a presença deste tipo de implementação**. Para obter mais informações, consulte [utilizar um script personalizado para verificar a presença de um tipo de implementação](/sccm/apps/deploy-use/create-applications#Use-a-custom-script-to-check-for-the-presence-of-a-deployment-type).  

2.  Na caixa de diálogo **Regra de Deteção**, na lista pendente **Tipo de definição**, selecione o método que pretende utilizar para detetar a presença do tipo de implementação. Pode optar por um dos seguintes métodos disponíveis:  

    -   **Sistema de ficheiros**-Utilize este método para detetar se uma pasta ou ficheiro específicos existe num dispositivo cliente, indicará que a aplicação está instalada.  

        > [!NOTE]  
        >  O **sistema de ficheiros** tipo de definição não suporta a especificação de um caminho UNC para uma partilha de rede no campo do caminho. Apenas pode especificar um caminho local no dispositivo cliente.  
        >   
        >  Para verificar as localizações de ficheiros de 32 bits para a pasta ou ficheiro especificados, selecione a opção **este ficheiro ou pasta está associada a uma aplicação de 32 bits em sistemas de 64 bits** primeiro. Se ficheiro ou pasta não forem encontrados, serão procurados nas localizações de 64 bits.  

    -   **Registo**-utilizar este método para detetar se uma chave de registo ou valor de registo existe num dispositivo cliente, indicará que a aplicação está instalada.  

        > [!NOTE]  
        >  Para verificar as localizações de registo de 32 bits para a chave de registo, selecione a opção **esta chave de registo está associada uma aplicação de 32 bits em sistemas de 64 bits** primeiro. Se a chave de registo não for encontrada, será procurada nas localizações de 64 bits.  

    -   **Windows Installer**-Utilize este método para detetar a existência de um ficheiro do Windows Installer especificado num dispositivo cliente, indicará que a aplicação está instalada.  

3.  Especifique os detalhes sobre o item que pretende utilizar para detetar se este tipo de implementação está instalado. Por exemplo, pode utilizar um ficheiro, pasta, chave do registo, valor do registo ou um código de produto do Windows Installer.  

4.  Especifique detalhes sobre o valor que pretende avaliar em comparação com o item que utilizar para detetar se o tipo de implementação está instalado. Por exemplo, se utilizar um ficheiro para verificar se o tipo de implementação está instalado, pode selecionar **a definição de sistema de ficheiros deve existir no sistema de destino para indicar a presença desta aplicação**.  

5.  Escolha **seguinte** para fechar o **regra de deteção** caixa de diálogo.  

###  <a name="use-a-custom-script-to-check-for-the-presence-of-a-deployment-type"></a>Utilizar um script personalizado para verificar a presença de um tipo de implementação  

1.  No **método de deteção** página do assistente criar tipo de implementação, selecione o **utilizar um script personalizado para detetar a presença deste tipo de implementação** caixa e, em seguida, escolha **editar**.  

2.  Na caixa de diálogo **Editor de Scripts**, na lista pendente **Tipo de Script**, selecione o idioma de script que pretende utilizar para detetar o tipo de implementação.  

3.  No **conteúdo do Script** box, introduza o script que pretende utilizar. Também pode colar o conteúdo de um script existente neste campo, ou escolha **abra** para procurar um script existente já guardado. O Configuration Manager verifica os resultados do script ao ler os valores que são escritos no fluxo de saída Standard Out (STDOUT), o fluxo de saída Standard Error (STDERR) e o código de saída do script. Se o código de saída for um valor diferente de zero, o script falhou e o estado de deteção de aplicação é desconhecido. Se o código de saída for zero e STDOUT tem dados, o estado de deteção de aplicação é instalado.  

 Utilize a tabela seguinte para ver como utilizar a saída de um script para verificar se uma aplicação é instalada.  

|Código de saída do script|Detalhes|
|--------------------------------|-----------------|
|0|**Dados lidos em STDOUT**-vazio<br /><br /> **Dados lidos em STDERR**-vazio<br /><br /> **Resultado do script**-êxito<br /><br /> **Estado de deteção de aplicação**-não instalado|  
|0|**Dados lidos em STDOUT**-vazio<br /><br /> **Dados lidos em STDERR**-não vazio<br /><br /> **Resultado do script**-falha<br /><br /> **Estado de deteção de aplicação**-desconhecido|  
|0|**Dados lidos em STDOUT**-não vazio<br /><br /> **Dados lidos em STDERR**-vazio<br /><br /> **Resultado do script**-êxito<br /><br /> **Estado de deteção de aplicação**-instalado|  
|0|**Dados lidos em STDOUT**-não vazio<br /><br /> **Dados lidos em STDERR**-não vazio<br /><br /> **Resultado do script**-êxito<br /><br /> **Estado de deteção de aplicação**-instalado|  
|Valor diferente de zero|**Dados lidos em STDOUT**-vazio<br /><br /> **Dados lidos em STDERR**-vazio<br /><br /> **Resultado do script**-falha<br /><br /> **Estado de deteção de aplicação**-desconhecido|  
|Valor diferente de zero|**Dados lidos em STDOUT**-vazio<br /><br /> **Dados lidos em STDERR**-não vazio<br /><br /> **Resultado do script**-falha<br /><br /> **Estado de deteção de aplicação**-desconhecido|  
|Valor diferente de zero|**Dados lidos em STDOUT**-não vazio<br /><br /> **Dados lidos em STDERR**-vazio<br /><br /> **Resultado do script**-falha<br /><br /> **Estado de deteção de aplicação**-desconhecido|  
|Valor diferente de zero|**Dados lidos em STDOUT**-não vazio<br /><br /> **Dados lidos em STDERR**-não vazio<br /><br /> **Resultado do script**-falha<br /><br /> **Estado de deteção de aplicação**-desconhecido|  

A tabela seguinte tem scripts de exemplo do Microsoft Visual Basic (VB) que pode utilizar para escrever os seus próprios scripts de deteção de aplicação.  

|Script de exemplo do Visual Basic|Descrição|  
|--------------------------------|-----------------|  
|**WScript.Quit(1)**|O script devolve um código de saída diferente de zero, o que significa que não foi executado com êxito. Neste caso, o estado de deteção de aplicação é desconhecido.|  
|**WScript.StdErr.Write "O Script falhou"**<br /><br /> **WScript.Quit(0)**|O script devolve um código de saída zero, mas o valor de STDERR não está vazio, o que significa que o script não foi executado com êxito. Neste caso, o estado de deteção de aplicação é desconhecido.|  
|**WScript.Quit(0)**|O script devolve um código de saída de zero, o que indica que foi executado com êxito. No entanto, o valor de STDOUT está vazio, o que significa que a aplicação não está instalada.|  
|**WScript.StdOut.Write "a aplicação está instalada"**<br /><br /> **WScript.Quit(0)**|O script devolve um código de saída de zero, o que indica que foi executado com êxito. O valor de STDOUT não está vazio, o que significa que a aplicação está instalada.|  
|**WScript.StdOut.Write "a aplicação está instalada"**<br /><br /> **WScript.StdErr.Write "Concluída"**<br /><br /> **WScript.Quit(0)**|O script devolve um código de saída de zero, o que indica que foi executado com êxito. Os valores de STDOUT e STDERR não estão vazios, o que significa que a aplicação está instalada.|  

 > [!NOTE]  
 >  O tamanho máximo que pode utilizar para um script é 32 kilobytes (KB).  

4.  Escolha **OK** para fechar o **Editor de scripts** caixa de diálogo.  

## <a name="specify-user-experience-options-for-the-deployment-type"></a>Especificar opções de experiência de utilizador para o tipo de implementação  
 Estas definições especificam como a aplicação será instalada nos dispositivos e que o utilizador irá ver.  

1.  No **experiência de utilizador** página do Assistente para criar tipo de implementação, especifique as seguintes informações:  

    -   **Comportamento de instalação**– na lista pendente, selecione uma das seguintes opções:  

        -   **Instalar para utilizador**– a aplicação é instalada apenas para o utilizador a quem a aplicação é implementada.  

        -   **Instalar para o sistema**– a aplicação é instalada apenas uma vez e fica disponível para todos os utilizadores.  

        -   **Instalar para o sistema se o recurso for o dispositivo; caso contrário instalar como utilizador**-se a aplicação é implementada num dispositivo, será instalada para todos os utilizadores. Se a aplicação for implementada para um utilizador, será instalada apenas para esse utilizador.  

    -   **Requisito de início de sessão**– especificar os requisitos de início de sessão para este tipo de implementação das seguintes opções:  

        -   **Apenas quando um utilizador com sessão iniciada**  

        -   **Se pretende ou não um utilizador tenha iniciado sessão**  

        -   **Só quando nenhum utilizador com sessão iniciada**  

        > [!NOTE]  
        >  Esta opção, será assumida a **apenas quando um utilizador é iniciado**, e não pode ser alterada se tiver selecionado **instalar para utilizador** no **comportamento de instalação** na lista pendente.  

    -   **Visibilidade do programa de instalação**– especifique o modo no qual o tipo de implementação será executado nos dispositivos cliente. Estão disponíveis as seguintes opções:  

        -   **Maximizado**– o tipo de implementação é executado maximizado nos dispositivos cliente. Os utilizadores verão todas as atividades de instalação.  

        -   **Normal**– o tipo de implementação é executado no modo normal, com base nas predefinições do sistema e do programa. Este é o modo predefinido.  

        -   **Minimizado**– o tipo de implementação é executado minimizado nos dispositivos cliente. Os utilizadores poderão ver a atividade de instalação na área de notificação ou na barra de tarefas.  

        -   **Oculto**– o tipo de implementação é executado ocultado nos dispositivos cliente e os utilizadores verão qualquer atividade de instalação.  

    -   **Permitir que os utilizadores visualizem e interajam com a instalação do programa**-especificar se um utilizador pode interagir com a instalação do tipo de implementação para configurar as opções de instalação.  

        > [!NOTE]  
        >  Esta opção está ativada por predefinição, se tiver selecionado o **instalar para utilizador** opção o **comportamento de instalação** na lista pendente.  

    -   **Máximo tempo de execução permitido (minutos)**– especifique o tempo máximo que o programa poderá demorar a ser executado no computador cliente. Pode especificar esta definição no formato de número inteiro maior que zero. A predefinição é 120 minutos.  

         Este valor é utilizado para:  

        -   Monitorize os resultados do tipo de implementação.  

        -   Verifique se um tipo de implementação será instalado quando janelas de manutenção são definidas nos dispositivos cliente. Quando uma janela de manutenção no local, um programa apenas será iniciado se houver tempo suficiente está disponível na janela de manutenção para contemplar a **máximo tempo de execução permitido** definição.  

        > [!IMPORTANT]  
        >  Poderá ocorrer um conflito se o **máximo tempo de execução permitido** é superior à janela de manutenção agendada. Se o utilizador definir o tempo máximo de execução para um período que exceda a duração de qualquer janela de manutenção disponível, esse tipo de implementação não será executado.  

2.  **Instalação tempo estimado (minutos)**– especifique o tempo estimado que a instalação do tipo de implementação irá demorar. Esta informação é apresentada aos utilizadores do Centro de Software.  

## <a name="specify-requirements-for-the-deployment-type"></a>Especificar requisitos para o tipo de implementação  

1.  No **requisitos** página do Assistente para criar tipo de implementação, escolha **adicionar** para abrir o **criar requisito** diálogo caixa e adicionar um novo requisito.  

    > [!NOTE]  
    >  Também pode adicionar novos requisitos no **requisitos** separador do *< nome do tipo de implementação\> * **propriedades** caixa de diálogo.  

2.  Na lista pendente **Categoria**, indique se este requisito corresponde a um dispositivo ou utilizador, ou selecione **Personalizada** para utilizar uma condição global criada anteriormente. Quando seleciona **personalizada**, também pode optar por **criar** para criar uma nova condição global. Para obter mais informações sobre as condições globais, consulte [como criar condições globais](../../apps/deploy-use/create-global-conditions.md).  

    > [!IMPORTANT]  
    >  Qualquer requisito da categoria **utilizador** e a condição **dispositivo primário** será ignorado se implementar a aplicação a uma coleção de dispositivos.  
    >   
    >  Se tiver criado um pacote do Windows e uma sequência de programas ou tarefas com o Windows 10 como requisito utilizando o System Center 2012 R2 Configuration Manager SP1 e, em seguida, atualizar para o System Center Configuration Manager, os requisitos para o Windows 10 poderão ser removidos. Para corrigir este problema, especifique os requisitos novamente. Tenha em atenção que apesar do requisito de foi removido a apresentação de requisitos, é ainda processado corretamente nos dispositivos.  

3.  No **condição** pendente lista, selecione a condição que pretende utilizar para avaliar se o utilizador ou dispositivo satisfaz os requisitos de instalação. O conteúdo desta lista varia consoante a categoria selecionada.  

4.  No **operador** pendente lista, selecione o operador que será utilizado para comparar a condição selecionada com o valor especificado para avaliar se o utilizador ou dispositivo satisfaz os requisitos de instalação. Os operadores disponíveis variam consoante a condição selecionada.  

    > [!IMPORTANT]  
    >  Os requisitos disponíveis irão variar consoante o tipo de dispositivo que utiliza o tipo de implementação.  

5.  No **valor** caixa, especifique os valores que serão utilizados com a condição e operador selecionados para avaliar se o utilizador ou dispositivo cumpre os requisitos de instalação. Os valores disponíveis variam consoante a condição selecionada e o operador selecionado.  

6.  Escolha **OK** para guardar o requisito e fechar o **criar requisito** caixa de diálogo.  

## <a name="specify-dependencies-for-the-deployment-type"></a>Especificar dependências para o tipo de implementação  
 As dependências definem um ou mais tipos de implementação a partir de outra aplicação que tem de ser instalada antes de um tipo de implementação ser instalado. Pode configurar os tipos de implementação dependentes para serem automaticamente instalados antes de um tipo de implementação está instalado.  

> [!IMPORTANT]  
>  Em alguns casos, um tipo de implementação está dependente de um tipo de implementação que também tenha dependências. O número máximo de dependências suportadas na cadeia é cinco.  

1.  No **dependências** página do Assistente para criar tipo de implementação, escolha **adicionar** se pretender especificar os tipos de implementação que devem ser instalados antes de instalar este tipo de implementação.  

    > [!IMPORTANT]  
    >  Também pode adicionar novas dependências no **dependências** separador do *< nome do tipo de implementação\> * **propriedades** caixa de diálogo.  

2.  No **adicionar dependência** diálogo caixa, escolha **adicionar**.  

3.  No **especificar aplicação necessária** caixa de diálogo, selecione os tipos de uma aplicação existente e um da implementação da aplicação a utilizar como uma dependência.  

    > [!TIP]  
    >  Pode escolher **vista** para apresentar as propriedades do tipo de aplicação ou implementação selecionado.  

4.  Escolha **OK** para fechar o **especificar aplicação necessária** caixa de diálogo.  

5.  Se pretender que uma aplicação dependente seja instalada automaticamente, selecione **instalação automática** junto da aplicação dependente.  

    > [!NOTE]  
    >  Uma aplicação dependente não necessita de ser implementada para ser instalada automaticamente.  

6.  No **adicionar dependência** caixa de diálogo em **nome do grupo de dependência**, introduza um nome para fazer referência a este grupo de dependências de aplicações.  

7.  Opcionalmente, utilize o **aumentar prioridade** e **diminuir prioridade** botões para alterar a ordem de avaliação de cada dependência.  

8.  Escolha **OK** para fechar o **adicionar dependência** caixa de diálogo.  

## <a name="confirm-the-deployment-type-settings-and-finish-the-wizard"></a>Confirme as definições de tipo de implementação e concluir o Assistente  

1.  No **resumo** página do Assistente para criar tipo de implementação, reveja as ações que o assistente executará. Escolha **seguinte** para criar o tipo de implementação, ou escolha **anterior** para voltar atrás e alterar as definições para o tipo de implementação.  

2.  Depois do **progresso** página depois de concluída, reveja as ações efetuadas pelo assistente e, em seguida, escolha **fechar** para concluir o assistente.  

3.  Se tiver iniciado o Assistente para criar tipo de implementação a partir do Assistente para criar aplicação, regressará ao **tipos de implementação** página do Assistente para criar aplicação.  

## <a name="set-up-additional-options-for-deployment-types-that-contain-virtual-applications"></a>Configurar opções adicionais para tipos de implementação que contêm aplicações virtuais  
 Utilize os procedimentos seguintes para configurar opções adicionais para tipos de implementação que contêm aplicações virtuais.  

### <a name="set-up-content-options-for-application-virtualization-app-v-deployment-types"></a>Configurar opções de conteúdo para os tipos de implementação de Application Virtualization (App-V)  

1.  Na consola do Configuration Manager, escolha **biblioteca de Software** > **aplicações**.  

2.  No **aplicações** lista, selecione uma aplicação que tenha um tipo de implementação de App-V. Em seguida, no **home page** separador o **propriedades** grupo, escolha **propriedades**.  

3.  No *< nome da aplicação\> * **propriedades** caixa de diálogo a **tipos de implementação** separador, selecione um tipo de implementação de App-V e, em seguida, escolha **editar**.  

4.  No *< nome do tipo de implementação\> * **propriedades** caixa de diálogo a **conteúdo** separador, configure as seguintes opções, se necessário:  

    -   **Manter conteúdo na cache do cliente**– Selecione esta opção para garantir que o conteúdo para este tipo de implementação não é eliminado da cache do cliente do Configuration Manager.  

    -   **Carregar conteúdo para a cache de App-V antes de iniciar**– Selecione esta opção para garantir que todo o conteúdo da aplicação virtual é carregado para a cache de App-V antes de iniciar a aplicação. A seleção desta opção também garante que o conteúdo da aplicação não seja fixado na cache e pode ser eliminado conforme necessário.  

5.  Escolha **OK** para fechar o *< nome do tipo de implementação\> * **propriedades** caixa de diálogo.  

6.  Escolha **OK** para fechar o *< nome da aplicação\> * **propriedades** caixa de diálogo.  

### <a name="set-up-publishing-options-for-app-v-deployment-types"></a>Configurar as opções para tipos de implementação de App-V de publicação  

1.  Na consola do Configuration Manager, escolha **biblioteca de Software** > **aplicações**.  

3.  No **aplicações** lista, selecione uma aplicação que tenha um tipo de implementação de App-V. Em seguida, no **home page** separador o **propriedades** grupo, escolha **propriedades**.  

4.  No *< nome da aplicação\> * **propriedades** caixa de diálogo a **tipos de implementação** separador, selecione um tipo de implementação de App-V e, em seguida, escolha **editar**.  

5.  No *< nome do tipo de implementação\> * **propriedades** caixa de diálogo a **publicação** separador, selecione os itens na aplicação virtual que pretende publicar.  

6.  Escolha **OK** para fechar o *< nome do tipo de implementação\> * **propriedades** caixa de diálogo.  

7.  Escolha **OK** para fechar o *< nome da aplicação\> * **propriedades** caixa de diálogo.  

## <a name="import-an-application"></a>Importar uma aplicação  
 Utilize o procedimento seguinte para importar uma aplicação para o Configuration Manager. Para obter informações sobre como exportar uma aplicação, consulte [tarefas de gestão do System Center Configuration Manager aplicações](../../apps/deploy-use/management-tasks-applications.md).  

1.  Na consola do Configuration Manager, escolha **biblioteca de Software** > **gestão de aplicações** > **aplicações**.   

3.  No **home page** separador o **criar** grupo, escolha **importar aplicação**.  

4.  No **geral** página do **Assistente para importar aplicação**, escolha **procurar**e, em seguida, especifique um caminho UNC para o ficheiro. zip que tenha a aplicação que pretende importar.  

5.  No **conteúdo do ficheiro** página, selecione a ação que irá ser executada se a aplicação que está a tentar importar for um duplicado da aplicação existente. Pode criar uma nova aplicação ou ignorar o duplicado e adicionar uma nova revisão à aplicação existente.  

6.  No **resumo** página, reveja as ações a executar e, em seguida, conclua o assistente.  

 A nova aplicação aparece no nó **Aplicações**.  

> [!TIP]  
>  O cmdlet Windows PowerShell **Import-CMApplication** tem a mesma função que este procedimento. Para obter mais informações, consulte [Import-CMApplication](https://technet.microsoft.com/library/jj821738.aspx) no Microsoft System Center 2012 Configuration Manager SP1 referência de cmdlets.  

##  <a name="deployment-types-supported-by-configuration-manager"></a>Tipos de implementação suportados pelo Gestor de Configuração  

|Nome do tipo de implementação|Mais informações|  
|--------------------------|----------------------|  
|**Windows Installer (\*ficheiro. msi)**|Cria um tipo de implementação a partir de um ficheiro do Windows Installer.|  
|**Pacote de aplicação do Windows (\*. AppX, \*. appxbundle)**|Cria um tipo de implementação para o Windows 8, Windows RT a partir de um ficheiro de pacote de aplicações do Windows ou de um pacote de grupos de aplicações.|  
|**Pacote de aplicação do Windows (na loja Windows)**|Cria um tipo de implementação para o Windows 8, Windows RT, ou posterior, especificando uma ligação para a aplicação na loja Windows ou navegando na loja para selecionar a aplicação pretendida.<br /><br /> Se pretender implementar a aplicação como uma hiperligação para a loja Windows, certifique-se de que a definição de política de grupo **desativar a aplicação de arquivo** está definido como **desativado** ou **não configurado**. Se esta definição estiver ativada, os clientes não conseguirão estabelecer ligação com a Loja Windows para transferir e instalar aplicações.<br /><br /> Os tipos de implementação do Windows 8 que utilizam uma ligação para um arquivo são sempre avaliados antes de outros tipos de implementação, independentemente da sua prioridade.|  
|**Instalador de script**|Cria um tipo de implementação que especifica um script que é executado nos dispositivos cliente para instalar o conteúdo ou para efetuar uma ação.|  
|**Microsoft Application Virtualization 4**|Cria um tipo de implementação a partir de um manifesto do Microsoft Application Virtualization 4|  
|**Microsoft Application Virtualization 5**|Cria um tipo de implementação a partir de um ficheiro de pacote do Microsoft Application Virtualization 5.|  
|**Pacote de aplicação do Windows Phone (\*ficheiro. xap)**|Cria um tipo de implementação a partir de um ficheiro de pacote de aplicação do Windows Phone.|  
|**Pacote de aplicação do Windows Phone (na loja Windows Phone)**|Cria um tipo de implementação, ao especificar uma ligação para a aplicação na loja do Windows Phone.|  
|**Ficheiro CAB móveis do Windows**|Cria um tipo de implementação para dispositivos do Windows Mobile a partir de um ficheiro CAB (Windows Mobile Cabinet).|  
|**Pacote de aplicação para iOS (\*ficheiro. IPA)**|Cria um tipo de implementação a partir de um ficheiro de pacote de aplicação do iOS.|  
|**Pacote de aplicação para iOS da App Store**|Cria um tipo de implementação, especificando uma ligação para a aplicação do iOS na App Store.|  
|**Pacote de aplicação para Android (\*ficheiro. apk)**|Cria um tipo de implementação a partir de um ficheiro de pacote de aplicação do Android.|  
|**Pacote de aplicação para Android no Google Play**|Cria um tipo de implementação, especificando uma ligação para a aplicação no Google Play.|  
|**Mac OS X**|Cria um tipo de implementação para computadores Mac a partir de um ficheiro .cmmac que tenha criado com a ferramenta CMAppUtil.<br /><br /> Aplica-se apenas a computadores Mac que executem o cliente do Configuration Manager.|  
|**Aplicação Web**|Cria um tipo de implementação que especifica uma ligação para uma aplicação Web. O tipo de implementação instala um atalho para a aplicação web no dispositivo do utilizador.<br /><br /> Se tiver instalado o browser gerido do Intune no iOS ou Android dispositivos que gere, pode certificar-se de que os utilizadores só podem utilizar o browser gerido para abrir a aplicação. Para tal, utilize um dos seguintes formatos quando especificar uma ligação para a aplicação, substituindo **http:** com **http-intunemam:** ou **https:** com **https-intunemam:**<br /><br /> - **http-intunemam: / / < caminho para a aplicação web\>**<br /><br /> - **https-intunemam: / / < caminho para a aplicação web\>**<br /><br /> Pode utilizar os requisitos da aplicação do Configuration Manager para se certificar de que as aplicações que pretende associar o browser gerido só são instaladas em dispositivos iOS e Android.<br /><br /> Para obter mais informações sobre o Intune managed browser, consulte [Internet gerir o acesso através de políticas de browser gerido](../../apps/deploy-use/manage-internet-access-using-managed-browser-policies.md).|  
|**Windows Installer através de MDM (\*. msi)**|Este tipo de instalador permite-lhe criar e implementar aplicações baseadas no Windows Installer em PCs com Windows 10.<br /><br /> As considerações seguintes são aplicáveis quando utiliza este tipo de instalador:<br><br>-Só pode carregar um único ficheiro com a extensão. msi.<br /><br /> -Código de produto o ficheiro e a versão do produto são utilizados para deteção da aplicação.<br /><br /> -O comportamento de reinício predefinido da aplicação será utilizado. O Configuration Manager não controla este procedimento.<br /><br /> -Serão instalados pacotes MSI de por utilizador para um único utilizador.<br /><br /> -Serão instalados pacotes MSI de por máquina para todos os utilizadores no dispositivo.<br /><br /> -Pacotes MSI de modo duplo atualmente instalados apenas para todos os utilizadores do dispositivo.<br /><br /> -As atualizações de aplicações são suportadas quando o código de produto MSI de cada versão for igual.|  
