---
title: Criar aplicações
titleSuffix: Configuration Manager
description: Crie aplicações com requisitos para instalar software, métodos de deteção e tipos de implementação.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ae97c9017f084e69a0e3660339bbd2b326afd296
ms.sourcegitcommit: 2491fbe98915b7a30c2422a371c929d0d4ebf22f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53247548"
---
# <a name="create-applications-in-configuration-manager"></a>Criar aplicações no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Uma aplicação do Configuration Manager define os metadados sobre a aplicação. Um aplicativo tem um ou mais tipos de implementação. Estes tipos de implementação incluem os ficheiros de instalação e informações que são necessárias para instalar software nos dispositivos. Um tipo de implementação também possui regras, como os requisitos e métodos de deteção. Estas regras especificam quando e como o cliente instala o software.  

Crie aplicações com os seguintes métodos:  

-   Crie automaticamente uma tipos de aplicação e implementação lendo os ficheiros de instalação do aplicativo:  
    - [Criar um aplicativo](#bkmk_create) e [detetar automaticamente](#bkmk_auto-app) informações sobre a aplicação
    - [Criar um tipo de implementação](#bkmk_create-dt) e [identificar automaticamente](#bkmk_auto-dt) informações de tipo de implementação

-   Criar manualmente uma aplicação e, em seguida, adicionar tipos de implementação mais tarde:  
    - [Criar um aplicativo](#bkmk_create) e [especificar manualmente](#bkmk_manual-app) informações sobre a aplicação
    - [Criar um tipo de implementação](#bkmk_create-dt) e [especificar manualmente](#bkmk_manual-dt) informações de tipo de implementação

-   [Importar uma aplicação](#bkmk_import) de um ficheiro  

Este artigo também inclui as seguintes informações para configurar um tipo de implementação:  
- [Conteúdo](#bkmk_dt-content)
- [Método de deteção](#bkmk_dt-detect)
- [Experiência de utilizador](#bkmk_dt-ux)
- [Requirements](#bkmk_dt-require)
- [Códigos de retorno](#bkmk_dt-return)
- [Dependências](#bkmk_dt-depend)



## <a name="bkmk_create"></a> Criar uma aplicação  

1.  Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho, expanda **gestão de aplicações**e selecione o **aplicativos** nó.  

2.  Sobre o **home page** separador do Friso, no **criar** , clique em **Criar aplicação**.  

Em seguida, detetar automaticamente ou especificar manualmente informações sobre a aplicação:  

-   [Detetar automaticamente](#bkmk_auto-app) informações sobre a aplicação para criar uma aplicação básica com um tipo de implementação única. Por exemplo, um Windows Installer ficheiro que não existem dependências ou requisitos. Depois de criar uma aplicação ao utilizar este procedimento, editá-la conforme necessário. Pode adicionar ou alterar os tipos de implementação e adicionar métodos de deteção, dependências ou requisitos.  

-   [Especificar manualmente](#bkmk_manual-app) informações sobre a aplicação para criar aplicações mais complexas. Defina mais do que um tipo de implementação, dependências, métodos de deteção ou requisitos.  


### <a name="bkmk_auto-app"></a> Detetar automaticamente informações sobre a aplicação  

1.  Sobre o **gerais** página do Assistente para criar aplicação, selecione **detetar automaticamente informação sobre esta aplicação nos ficheiros de instalação**.  

2.  Na **tipo** na lista pendente, selecione tipo que pretende utilizar para detetar informações sobre a aplicação de ficheiro de instalação do aplicativo. Para obter mais informações sobre os tipos de instalação disponíveis, consulte [tipos de implementação suportados pelo Configuration Manager](/sccm/apps/deploy-use/create-applications#bkmk_deploy-types).  

3.  Na **localização** caixa, especifique o ficheiro de instalação de aplicação que pretende utilizar para detetar informações sobre a aplicação. Esta localização é um caminho de rede (`\\server\share\filename`) ou uma hiperligação do arquivo. Tem de ter acesso ao caminho de rede e eventuais subpastas que incluem o conteúdo da aplicação.  

    > [!IMPORTANT]  
    >  Quando seleciona **Windows Installer (\*arquivo. msi)** como tipo de aplicação, o site importa todos os ficheiros na pasta especificada. Em seguida, envia estes ficheiros para pontos de distribuição. Certifique-se de que a pasta especificada contém apenas os ficheiros que são necessários para instalar a aplicação. Microsoft testa o Configuration Manager para suportar até 20 000 ficheiros no pacote de aplicação. Se seu aplicativo tiver mais ficheiros, considere criar múltiplas aplicações com menos ficheiros.    

4.  Sobre o **importar informação** página do Assistente para criar aplicação, reveja as informações e clique em **próxima**. Se necessário, clique em **Previous** para voltar atrás e corrigir quaisquer erros.  

5.  Sobre o **informações gerais** página do Assistente para criar aplicação, especifique as seguintes informações:  

    > [!NOTE]  
    >  Se o Configuration Manager Deteta automaticamente estas informações dos arquivos de instalação de aplicativo, ele já está preenchido aqui. Além disso, as opções apresentadas poderão ser diferentes dependendo do tipo de aplicação que criou.  

    -   Informações gerais sobre a aplicação, como o aplicativo **Name**, **comentários do administrador**, **publicador**, e **deversãodoSoftware**. Para ajudar a encontrar a aplicação na consola do Configuration Manager, especifique um **referência opcionais**, ou selecione **categorias administrativas**.  

    -   **Programa de instalação**: Especifique o programa de instalação e eventuais propriedades que são necessários para instalar o tipo de implementação de aplicação.  

        > [!TIP]  
        >  Se o programa de instalação não aparecer, escolha **procurar** e navegue até à localização do programa de instalação.  

    -   **Comportamento de instalação**: Selecione uma das três opções para como o Configuration Manager instala este tipo de implementação. Para obter mais informações sobre estas opções, consulte [experiência de utilizador](#bkmk_dt-ux).  

    -   **Utilizar uma ligação VPN automática (se configurada)**: Se tiver implementado um perfil VPN para o dispositivo no qual o utilizador inicia a aplicação, ligue-se a VPN quando a aplicação for iniciada. Esta opção é apenas para Windows 8.1 e Windows Phone 8.1. Em dispositivos Windows Phone 8.1, se implementar mais do que um perfil VPN no dispositivo, as ligações VPN automáticas não são suportadas. Para obter mais informações, consulte [perfis VPN](/sccm/protect/deploy-use/vpn-profiles).  

    - **Aprovisionar esta aplicação para todos os utilizadores do dispositivo**<!--1358310-->: A partir da versão 1806, aprovisionar uma aplicação com um pacote de aplicação do Windows para todos os utilizadores no dispositivo. Para obter mais informações, consulte [aplicativos Windows criar](/sccm/apps/get-started/creating-windows-applications#bkmk_provision).  

       > [!Tip]  
       > Se estiver a modificar uma aplicação existente, esta definição é sobre o **experiência de utilizador** separador das propriedades de tipo de implementação do pacote de aplicação do Windows.  

6.  Escolher **próxima**, reveja as informações da aplicação na **resumo** página e, em seguida, concluir o Assistente para criar aplicação.  

Agora a nova aplicação aparece no **aplicativos** nó da consola do Configuration Manager. Concluir a criação de um aplicativo. 

Para adicionar mais tipos de implementação ou configurar outras definições, consulte [criar tipos de implementação para a aplicação](#bkmk_create-dt).  


### <a name="bkmk_manual-app"></a> Especificar manualmente informações sobre a aplicação  

1.  Sobre o **gerais** página do Assistente para criar aplicação, selecione **especificar manualmente as informações da aplicação**e, em seguida, escolha **seguinte**.  

2.  Especifique **informações gerais** sobre a aplicação:  

    - O aplicativo **nome** é necessário e tem de ter menos de 256 carateres.  

    - **Comentários do administrador**, **publicador**, e **versão do Software** são metadados adicionais para descrever ainda mais o aplicativo.  

    - Para ajudar a encontrar a aplicação na consola do Configuration Manager, especifique um **referência opcionais**, ou selecione **categorias administrativas**.  

    - **Data de publicação**  

    - Selecionar utilizadores ou grupos que são responsáveis por esta aplicação como **proprietários** e **contactos de suporte**. Por predefinição, estes valores são definidos para o seu nome de utilizador.  

3.  Sobre o **catálogo de aplicações** página do Assistente para criar aplicação, especifique as seguintes informações:  

    -   **Idioma selecionado**: Na lista pendente, selecione a versão de idioma da aplicação que pretende configurar. Escolher **Adicionar/remover** para configurar mais idiomas para esta aplicação.  

    -   **Nome da aplicação localizada**: Especifique o nome da aplicação no idioma selecionado.  

        > [!IMPORTANT]  
        > Um nome da aplicação localizada é necessário para cada versão de idioma que configurar.  

    -   **Categorias de utilizador**: Escolher **editar** para especificar categorias de aplicação no idioma selecionado. Os utilizadores do Centro de Software utilizam estas categorias para ajudar a filtrar e ordenar as aplicações disponíveis.  

    -   **Documentação do utilizador**: Especifique a localização de um ficheiro a partir do qual os utilizadores do Centro de Software podem obter mais informações sobre esta aplicação. Esta localização é um endereço de Web site ou um nome de ficheiro e caminho de rede. Certifique-se de que os utilizadores têm acesso a esta localização.  

    -   **Texto da hiperligação**: Especifique o texto que aparece em vez do URL da aplicação.  

    -   **URL de privacidade**: Especifique um endereço de Web site à declaração de privacidade para a aplicação.  

    -   **Descrição localizada**: Introduza uma descrição para esta aplicação no idioma selecionado.  

    -   **Palavras-chave**: Introduza uma lista de palavras-chave no idioma selecionado. Estas palavras-chave que ajudam a pesquisa de utilizadores do Centro de Software para a aplicação.  

    -   **Ícone**: Clique em **procurar** para selecionar um ícone para esta aplicação. Se não especificar um ícone, o Configuration Manager utiliza um ícone predefinido. Ícones podem ter dimensões de pixel de até 512 x 512.  

    -   **Apresentar como aplicação em destaque e destacá-la no portal da empresa**: Esta opção apresenta destaque a aplicação no portal da empresa em dispositivos móveis.  

4.  Sobre o **tipos de implementação** página do Assistente para criar aplicação, escolha **Add** para criar um novo tipo de implementação. Para obter mais informações, consulte [criar tipos de implementação para a aplicação](#bkmk_create-dt).  

5.  Escolher **próxima**, reveja as informações da aplicação na **resumo** página e, em seguida, concluir o Assistente para criar aplicação.  

Agora a nova aplicação aparece no **aplicativos** nó da consola do Configuration Manager.  



## <a name="bkmk_create-dt"></a> Criar tipos de implementação para a aplicação  

Se [detetar automaticamente informações sobre a aplicação](#bkmk_auto-app), não poderá ter de concluir alguns dos passos nesta secção.  

> [!Note]  
> Ao visualizar as propriedades de um tipo de implementação existente, as secções seguintes correspondem às guias da janela de propriedades do tipo de implementação:  
> - [Conteúdo](#bkmk_dt-content)
> - [Método de deteção](#bkmk_dt-detect)
> - [Experiência de utilizador](#bkmk_dt-ux)
> - [Requirements](#bkmk_dt-require)
> - [Códigos de retorno](#bkmk_dt-return)
> - [Dependências](#bkmk_dt-depend)
>  
> Para obter informações sobre o **comportamento de instalação** separador nas propriedades de um tipo de implementação, consulte [verificar para executar ficheiros executáveis](/sccm/apps/deploy-use/deploy-applications#bkmk_exe-check).  


### <a name="start-the-create-deployment-type-wizard"></a>Iniciar o Assistente para criar tipo de implementação  

Existem três formas de iniciar o Assistente para criar tipo de implementação:

- **No nó Applications**: Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho, expanda **gestão de aplicações**e selecione o **aplicativos** nó. Selecione uma aplicação e, em seguida, clique em **criar tipo de implementação** na faixa de opções.  

- **Ao criar um aplicativo**: Quando [especificar manualmente informações sobre a aplicação](#bkmk_manual-app) no Assistente para criar aplicação, clique em **Add** na página de tipos de implementação.  

- **A partir das propriedades da aplicação**: Selecione uma aplicação existente na **aplicativos** nó e clique em **propriedades**. Mude para o **tipos de implementação** separador e clique em **Add**.

Em seguida, utilize um dos seguintes procedimentos para [identificar automaticamente](#bkmk_auto-dt) ou [especificar manualmente](#bkmk_manual-dt) informações de tipo de implementação.  


### <a name="bkmk_auto-dt"></a> Identificar automaticamente informações de tipo de implementação  

1.  Sobre o **gerais** página do Assistente para criar tipo de implementação:  

    1. Selecione o ficheiro de instalação do aplicativo **tipo** para detetar as informações de tipo de implementação.  

    2. Selecione **identificar automaticamente informações sobre este tipo de implementação nos ficheiros de instalação**.  

    3.  Na **localização** caixa, especifique o ficheiro de instalação de aplicação que pretende utilizar para detetar as informações de tipo de implementação. Esta localização é um caminho de rede (`\\server\share\filename`) ou uma hiperligação do arquivo. Tem de ter acesso ao caminho de rede e eventuais subpastas que incluem o conteúdo da aplicação.  

2.  Sobre o **importar informação** página do Assistente para criar tipo de implementação, reveja as informações e clique em **próxima**. Se necessário, clique em **Previous** para voltar atrás e corrigir quaisquer erros.  

3.  Sobre o **informações gerais** página do Assistente para criar tipo de implementação, especifique as seguintes informações:  

    > [!NOTE]  
    >  Algumas das informações sobre o tipo de implementação podem já estar presentes se já foram lidas nos ficheiros de instalação da aplicação. Além disso, as opções apresentadas poderão diferir, dependendo do tipo de implementação que está a criar.  

    -   **Informações gerais** sobre o tipo de implementação:      
        - O **nome** é necessário  

        - **Comentários do administrador** para descrevem melhor  

        - **Idiomas** que estão disponíveis para o mesmo   

    -   **Programa de instalação**: Especifique o programa de instalação e eventuais propriedades de que necessita para instalar o tipo de implementação.  

    -   **Comportamento de instalação**: Selecione uma das três opções para como o Configuration Manager instala este tipo de implementação. Para obter mais informações sobre estas opções, consulte [experiência de utilizador](#bkmk_dt-ux).  

    -   **Utilizar uma ligação VPN automática (se configurada)**: Se tiver implementado um perfil VPN para o dispositivo no qual o utilizador inicia a aplicação, ligue-se a VPN quando a aplicação for iniciada. Esta opção é apenas para Windows 8.1 e Windows Phone 8.1. Em dispositivos Windows Phone 8.1, se implementar mais do que um perfil VPN no dispositivo, as ligações VPN automáticas não são suportadas. Para obter mais informações, consulte [perfis VPN](/sccm/protect/deploy-use/vpn-profiles).  

4.  Escolher **próxima**e, em seguida, continuar a [opções de conteúdo do tipo de implementação](#bkmk_dt-content).  


### <a name="bkmk_manual-dt"></a> Especificar manualmente as informações de tipo de implementação  

1.  Na **gerais** página do tipo de implementação criar assistente, no **tipo** pendente lista, escolha o tipo de ficheiro de instalação de aplicações para este tipo de implementação. 

2.  Selecione **especificar manualmente as informações de tipo de implementação**e, em seguida, clique em **próxima**.

3.  Sobre o **informações gerais** página do Assistente para criar tipo de implementação, especifique um **nome** para o tipo de implementação. Opcionalmente, especificar **comentários do administrador**, selecione a **idiomas** para este tipo de implementação e, em seguida, clique **seguinte**.  

4.  Continuar a [opções de conteúdo do tipo de implementação](#bkmk_dt-content).  

### <a name="bkmk_dt-content"></a> Tipo de implementação **conteúdo** opções  

Sobre o **conteúdo** , especifique as seguintes informações:  

> [!Note]  
> Ao visualizar as propriedades de um tipo de implementação existente, algumas dessas opções aparecem na **conteúdo** separador e outros na **programas** separador.  

- **Localização do conteúdo**: Especifique a localização do conteúdo para este tipo de implementação, ou selecione **procurar** para escolher a pasta de conteúdo de tipo de implementação.  

    > [!IMPORTANT]  
    >  A conta de sistema do computador do servidor do site tem de ter permissões para a localização de conteúdo especificada.  

    - **Manter conteúdo na cache do cliente**: O cliente do Configuration Manager mantém indefinidamente em seu cache o conteúdo do tipo de implementação. O cliente mantém o conteúdo, mesmo que a aplicação já está instalada. Esta opção é útil em algumas implementações, como software baseados no Windows Installer. Instalador do Windows precisa de uma cópia local do conteúdo de origem para aplicar atualizações. Esta opção reduz o espaço disponível na cache. Se selecionar esta opção, pode fazer com que uma implementação de grande dimensão falhar posteriormente caso a cache não tem espaço suficiente disponível.  

- **Programa de instalação**: Especifique o nome do programa de instalação e quaisquer parâmetros de instalação necessários.  

    - **Início da instalação em**: Opcionalmente, especifique a pasta que contém o programa de instalação para o tipo de implementação. Esta pasta pode ser um caminho absoluto no cliente ou um caminho para a pasta de ponto de distribuição que tenha os ficheiros de instalação.  

- **Desinstalar programa**: Opcionalmente, especifique o nome do programa de desinstalação e quaisquer parâmetros necessários.  

    - **Iniciar desinstalação em**: Opcionalmente, especifique a pasta que contém o programa de desinstalação para o tipo de implementação. Esta pasta pode ser um caminho absoluto no cliente. Também pode ser um caminho relativo de um ponto de distribuição da pasta com o pacote.  

- **Programa de reparação**: A partir da versão 1810, para o Windows Installer e tipos de implementação do instalador de Script, opcionalmente, especifique o nome do programa de reparação e quaisquer parâmetros necessários.<!--1357866-->  

    - **Início da reparação em**: Opcionalmente, especifique a pasta que contém o programa de reparo para o tipo de implementação. Esta pasta pode ser um caminho absoluto no cliente. Também pode ser um caminho relativo de um ponto de distribuição da pasta com o pacote.  

- **Executar a instalação e desinstalação programa como um processo de 32 bits em clientes de 64 bits**: Utilize as localizações de ficheiros e registo de 32 bits em computadores baseados em Windows para executar o programa de instalação para o tipo de implementação.  


#### <a name="deployment-type-properties-content-options"></a>Propriedades do tipo de implementação **conteúdo** opções
Ao visualizar as propriedades de um tipo de implementação, as opções seguintes são apresentadas apenas nos **conteúdo** separador:

- **Definições de conteúdo de desinstalação**:  

    - **Mesmo como instalar o conteúdo**: Se a instalação e conteúdo de desinstalação são os mesmos, selecione esta opção. Esta opção é a predefinição.  

    - **Não conteúdo de desinstalação**: Se seu aplicativo não precisa de conteúdo para a desinstalação, selecione esta opção.  

    - **Diferente do conteúdo de instalação**: Se o conteúdo de desinstalação é diferente do conteúdo de instalação, selecione esta opção.  

        - **Localização de conteúdo de desinstalação**: Especifique o caminho de rede para o conteúdo que é utilizado para desinstalar a aplicação.  

- **Permitir aos clientes utilizar pontos de distribuição do grupo de limite de site predefinido**: Especifique se os clientes devem transferir e instalar o software a partir de um ponto de distribuição no grupo de limite predefinido de site, quando o conteúdo não está disponível a partir de um ponto de distribuição no atual ou os grupos de limites de vizinho.  

- **Opções de implementação**: Especifique se os clientes devem transferir a aplicação quando estiverem a utilizar um ponto de distribuição de um vizinho ou os grupos de limites de site padrão.  

- **Permitir que os clientes partilhem conteúdos com outros clientes na mesma sub-rede**: Especifique se pretende ativar a utilização do BranchCache para transferências de conteúdos. Para obter mais informações, consulte [BranchCache](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#branchcache). A partir da versão 1802, BranchCache está sempre ativada nos clientes. Esta definição for removida, como os clientes utilizam o BranchCache, se o ponto de distribuição suportar.  


### <a name="bkmk_dt-detect"></a> Tipo de implementação **método de deteção** opções   

Este procedimento configura um método de deteção que indica a presença do tipo de implementação. Em outras palavras, se o dispositivo de Windows já tem a aplicação foi instalada. Utilize um dos dois métodos seguintes para criar um método de Deteção:  
- [Configurar regras para detetar a presença deste tipo de implementação](#bkmk_detect-rule)
- [Utilizar um script personalizado para detetar a presença deste tipo de implementação](#bkmk_detect-script)


#### <a name="bkmk_detect-rule"></a> Configurar regras para detetar a presença deste tipo de implementação

1.  Sobre o **método de deteção** página, a opção de **configurar regras para detetar a presença deste tipo de implementação** está selecionada por predefinição. Clique em **Adicionar cláusula**.  

2.  Na **regra de deteção** caixa de diálogo, clique nas **tipo de definição** na lista pendente. Selecione um dos seguintes métodos para detetar a presença do tipo de implementação:  

    - **Sistema de ficheiros**: Detete se uma pasta ou ficheiro específicos existe num dispositivo. Esta deteção indica que a aplicação é instalada. Especifique os seguintes detalhes adicionais:  

        - **Tipo de**: Selecione se é um ficheiro ou pasta.  

        - **Caminho** (obrigatório): Introduzir ou navegue para o caminho local no dispositivo que inclui o ficheiro ou pasta. Por exemplo, `C:\Program Files`. Não é possível especificar um caminho de rede partilhada. Se clicar **procurar**, procurar o sistema de arquivos local ou ligar a um cliente representativo para procurar.  

        - **Nome de ficheiro ou pasta** (obrigatório): Especifique o nome de ficheiro ou pasta específico para detetar no caminho acima. Se o cliente Deteta este ficheiro ou pasta no dispositivo, considera o aplicativo como instalada no dispositivo.  

        - **Este ficheiro ou pasta está associada a uma aplicação de 32 bits em sistemas de 64 bits**: Esta opção está selecionada por predefinição. O cliente verifica primeiro as localizações de ficheiros de 32 bits para a pasta ou ficheiro especificados. Se o ficheiro ou pasta não for encontrada, o cliente procura, em seguida, localizações de 64 bits.  

    - **Registo**: Detete se uma chave de registo especificada ou o valor de registo existe num dispositivo cliente. Esta deteção indica que a aplicação é instalada. Especifique os seguintes detalhes adicionais:  

        - **Hive** (obrigatório): Escolha um ramo de registo na lista pendente. Por exemplo, `HKEY_LOCAL_MACHINE`.  

        - **Chave** (obrigatório): Especifique a chave de registo para pesquisar na colmeia acima. Por exemplo, `SOFTWARE\Microsoft\Office`.  

        - **Valor** (opcional): Introduza um valor específico para detetar na chave acima. Se pretender que o cliente para detetar o valor (padrão), ative a opção para **valor de chave de registo de utilização (predefinição) para a deteção de**. Ao introduzir um valor ou ative esta opção, tem de selecionar uma **tipo de dados**.  

        - **Esta chave de registo está associada uma aplicação de 32 bits em sistemas de 64 bits**: Selecione esta opção para primeiro localizações de registo de 32 bits de verificação para a chave de registo especificada. Se a chave de registo não for encontrada, o cliente procura as localizações de 64 bits.  

    - **Windows Installer**: Detete a existência de um ficheiro do Windows Installer especificado num dispositivo cliente. Esta deteção indica que a aplicação é instalada. Especifique o MSI **código de produto** para detetar no cliente. Se clicar **procurar**, selecione o ficheiro MSI do qual é possível ler o código de produto. 

3.  Na parte inferior da janela de regra de deteção, especifique se o item tem de existir ou cumprir uma regra. Por exemplo, se detectar com um ficheiro, a seguinte opção está selecionada por predefinição: **A definição de sistema de ficheiros deve existir no sistema de destino para indicar a presença desta aplicação**. Selecione a outra opção para criar uma regra de deteção com base nas propriedades de ficheiro ou pasta. Essas propriedades incluem a data de modificação, data de criação, versão ou tamanho. Estes critérios de regra são diferentes para cada tipo de definição.  

4.  Clique em **OK** para fechar a **regra de deteção** caixa de diálogo.  

Ao criar mais do que um método de deteção para um tipo de implementação, crie uma lógica mais complexa através do agrupamento de cláusulas em conjunto. 

Continue para a próxima seção sobre como utilizar um script personalizado como um método de deteção. Ou avançar para o [experiência de utilizador](#bkmk_dt-ux) opções para o tipo de implementação.


#### <a name="bkmk_detect-script"></a> Utilize um script personalizado para verificar a presença de um tipo de implementação  

1.  Sobre o **método de deteção** página, selecione a **utilizar um script personalizado para detetar a presença deste tipo de implementação** caixa. Em seguida, clique em **editar**.  

2.  Na **Editor de scripts** caixa de diálogo, clique nas **tipo de Script** na lista pendente. Selecione uma das seguintes linguagens de script para detetar o tipo de implementação: PowerShell, VBScript ou JScript.  

3.  Na **conteúdo do Script** , introduza o script que pretende utilizar ou cole o conteúdo de um script existente. Escolher **aberto** para navegar para um script existente já guardado. Clique em **clara** para remover o texto no campo de conteúdo de Script. Se necessário, ative a opção para **executar o script como um processo de 32 bits em clientes de 64 bits**.  

    > [!NOTE]  
    >  O tamanho máximo para um script é 32 KB.  

4.  Clique em **OK** para guardar o script e fechar o **Editor de scripts** caixa de diálogo. Novamente no Assistente para criar tipo de implementação, o **tipo de Script** e **Script comprimento** campos atualizar com detalhes sobre o seu script.   


#### <a name="about-custom-script-detection-methods"></a>Sobre métodos de deteção de script personalizado  

O Configuration Manager verifica os resultados do script. Ele lê os valores escritos pelo script para o fluxo de saída padrão (STDOUT), o erro padrão (STDERR) e o código de saída. Se o script é encerrado com um valor diferente de zero, o script falha, e o estado de deteção de aplicação *desconhecido*. Se o código de saída for igual a zero e STDOUT tem dados, o estado de deteção de aplicação é *instalada*.

Utilize as tabelas seguintes para verificar se uma aplicação é instalada a partir da saída de um script:  

**Sem código de saída:**  
|STDOUT|STDERR|Resultado do script|Estado de deteção de aplicação|
|---------|---------|---------|---------|
|vazio|vazio|Êxito|Não instalado|
|vazio|Não pode estar vazio|Falha|Desconhecido|
|Não pode estar vazio|vazio|Êxito|Instalado|
|Não pode estar vazio|Não pode estar vazio|Êxito|Instalado|


**Código de saída de diferentes de zero:**  
|STDOUT|STDERR|Resultado do script|Estado de deteção de aplicação|
|---------|---------|---------|---------|
|vazio|vazio|Falha|Desconhecido|
|vazio|Não pode estar vazio|Falha|Desconhecido|
|Não pode estar vazio|vazio|Falha|Desconhecido|
|Não pode estar vazio|Não pode estar vazio|Falha|Desconhecido|


**Exemplos de VBScript**

Utilize os seguintes exemplos de VBScript para escrever seus próprios scripts de deteção de aplicação:  

Exemplo 1: O script devolve um código de saída diferente de zero. Este código indica que o script não foi executada com êxito. Neste caso, o estado de deteção de aplicação é desconhecido.  
``` VBScript
WScript.Quit(1)
```

Exemplo 2: O script devolve um código de saída igual a zero, mas o valor de STDERR não está vazio. Este resultado indica que o script não foi executada com êxito. Neste caso, o estado de deteção de aplicação é desconhecido.  
``` VBScript
WScript.StdErr.Write "Script failed"
WScript.Quit(0)
```

Exemplo 3: O script devolve um código de saída igual a zero, que indica que foi executada com êxito. No entanto, o valor de STDOUT está vazio, que indica que a aplicação não está instalada.  
``` VBScript
WScript.Quit(0)
```

Exemplo 4: O script devolve um código de saída igual a zero, que indica que foi executada com êxito. O valor de STDOUT não está vazio, que indica que a aplicação está instalada.  
``` VBScript
WScript.StdOut.Write "The application is installed"
WScript.Quit(0)
```

Exemplo 5: O script devolve um código de saída igual a zero, que indica que foi executada com êxito. Os valores de STDOUT e STDERR não estão vazios, que indica que a aplicação está instalada.  
``` VBScript
WScript.StdOut.Write "The application is installed"
WScript.StdErr.Write "Completed"
WScript.Quit(0)
```


### <a name="bkmk_dt-ux"></a> Tipo de implementação **experiência de utilizador** opções   

Estas definições especificam como o cliente instala a aplicação em dispositivos e o que o usuário vê.  

Na página **Experiência de Utilizador** , especifique as seguintes informações:  

- **Comportamento de instalação**: Na lista pendente, selecione uma das seguintes opções:  

    - **Instalar para utilizador**: O cliente instala apenas o aplicativo para o utilizador a quem implementou a aplicação.  

    - **Instalar para o sistema**: O cliente instala a aplicação apenas uma vez. Está disponível para todos os utilizadores.  

    - **Instalar para o sistema se o recurso for o dispositivo; caso contrário instalar para utilizador**: Se implementar a aplicação num dispositivo, o cliente instala-o para todos os utilizadores. Se implementar a aplicação a um utilizador, o cliente instala-apenas para esse utilizador.  

- **Requisito de início de sessão**: Selecione uma das seguintes opções:  

    - **Apenas quando um utilizador tem sessão iniciada**  

    - **Se pretende ou não um utilizador tem sessão iniciada**  

    - **Só quando nenhum utilizador tem sessão iniciada**  

    > [!NOTE]  
    >  Esta opção assume a predefinição **apenas quando um usuário está conectado no**. Se selecionou **instalar para utilizador** no **comportamento de instalação** na lista pendente, não é possível alterar esta opção.  

- **Visibilidade do programa de instalação**: Especifique o modo no qual o tipo de implementação é executado nos dispositivos cliente. Selecione uma das seguintes opções:  

    - **Maximizado**: O tipo de implementação é executado maximizado nos dispositivos cliente. Os utilizadores veem todas as atividades de instalação.  

    - **Normal**: O tipo de implementação é executado no modo normal, com base nas predefinições do sistema e do programa. Esse modo é a predefinição.  

    - **Minimizado**: O tipo de implementação é executado minimizado nos dispositivos cliente. Os utilizadores poderão ver a atividade de instalação na área de notificação ou na barra de tarefas.  

    - **Oculto**: O tipo de implementação é executado ocultado nos dispositivos cliente. Os utilizadores não veem nenhuma atividade de instalação.  

- **Permitir que os utilizadores visualizem e interajam com a instalação do programa**: Especifica se um utilizador pode interagir com a instalação do tipo de implementação para configurar as opções de instalação.  

    > [!NOTE]  
    >  Se selecionar a **instalar para utilizador** opção a **comportamento de instalação** na lista pendente, esta opção está ativada por predefinição.  

    > [!IMPORTANT]  
    > A partir da versão 1802, quando seleciona a **instalar para o sistema** comportamento, esta definição é opcional. Esta alteração é principalmente permitir que um utilizador final interagir com a instalação durante uma sequência de tarefas. Por exemplo, para executar um processo de configuração, que pede ao utilizador final para várias opções. Alguns instaladores de aplicativo não podem ter silenced avisos do utilizador ou o processo de instalação pode exigir valores de configuração específicas apenas conhecidas do usuário. <!--1356976-->  
    >  
    > Instalar no contexto do sistema e permitir que os utilizadores interajam com a instalação não é uma configuração segura. Para obter mais informações, consulte [segurança e privacidade para gestão de aplicações](/sccm/apps/plan-design/security-and-privacy-for-application-management#bkmk_interact).  

- **Máximo permitido (minutos) de tempo de execução**: Especifique o tempo máximo dentro de minutos que esperava o tipo de implementação para ser executado no computador cliente. Especifique esta definição como um número inteiro maior que zero. O valor predefinido é 120 minutos (duas horas).  

    Utilize este valor para as seguintes ações:  

    - Para monitorizar os resultados do tipo de implementação.  

    - Para verificar se um tipo de implementação está instalado ao definir janelas de manutenção nos dispositivos cliente. Quando uma janela de manutenção estiver em vigor, um tipo de implementação é iniciada apenas se houver tempo suficiente na janela de manutenção para acomodar os **máximo tempo de execução permitido** definição.  

    > [!IMPORTANT]  
    >  Pode ocorrer um conflito se o **máximo de tempo de execução permitido** é superior à janela de manutenção agendada. Se o utilizador definir o tempo de execução máximo para um período superior ao comprimento de qualquer janela de manutenção disponível, esse tipo de implementação não é executado.  

- **Tempo de instalação (minutos) estimado**: Especifique a hora de instalação estimado do tipo de implementação. Os utilizadores veem este tempo, no Centro de Software.  


#### <a name="deployment-type-properties-user-experience-options"></a>Propriedades do tipo de implementação **experiência de utilizador** opções
Ao visualizar as propriedades de um tipo de implementação, as opções seguintes são apresentadas apenas nos **experiência de utilizador** separador:

Impor um comportamento específico de pós-instalação. Selecione uma das seguintes opções:  

- **Determinar comportamento baseado em códigos de retorno**: Lidar com reinicializações com base nos códigos configurados no [códigos de retorno](#bkmk_dt-return) separador. O Centro de software apresenta **podem exigir um reinício**. Se um utilizador tem sessão iniciado durante a instalação, for pedidos consoante a *da implementação* configuração de experiência do usuário.  

- **Nenhuma ação específica**: Sem reinício é necessário após a instalação. Relatórios do Centro de software que não o reinício é necessário.  

- **O programa de instalação de software poderá forçar um reinício de dispositivo**: O Configuration Manager não controla nem iniciar um reinício, mas a instalação real pode ser feito sem aviso. Utilize esta definição para impedir que o Configuration Manager comunicar a falha de instalação quando o instalador inicia uma reinicialização. O Centro de software apresenta **podem exigir um reinício**.  

- **Cliente do Configuration Manager irá forçar um reinício de dispositivo obrigatório**: O Configuration Manager força um reinício do dispositivo após a instalação com êxito. Relatórios do Centro de software que é necessário um reinício. Se um utilizador tem sessão iniciado durante a instalação, for pedidos consoante a *da implementação* configuração de experiência do usuário.  


### <a name="bkmk_dt-require"></a> Tipo de implementação **requisitos**

Antes de instalar o tipo de implementação, o Gestor de configuração verifica estes requisitos em dispositivos. Utilize os requisitos para refinar e controlar os dispositivos ou utilizadores que recebem esta aplicação. Por exemplo, se implementar a aplicação numa coleção de utilizador, especifica aqui o requisitos de hardware da aplicação. 

1.  Na **requisitos** página, clique em **Add** para abrir o **criar requisito** caixa de diálogo.  

2.  Na **categoria** na lista pendente, selecione se este requisito corresponde a um **dispositivo** ou uma **utilizador**.  

    Selecione **personalizado** para utilizar uma condição global criada anteriormente. Quando seleciona **personalizada**, também é possível **criar** para criar uma nova condição global. Para obter mais informações sobre as condições globais, consulte [como criar condições globais](/sccm/apps/deploy-use/create-global-conditions).  

    > [!IMPORTANT]  
    >  Se implementar a aplicação para uma coleção de dispositivos, o cliente ignora qualquer requisito da categoria **usuário** e a condição **dispositivo primário**.  

3.  Na **condição** pendente, selecione a condição para avaliar se o utilizador ou dispositivo satisfaz os requisitos de instalação. O conteúdo desta lista variam consoante a categoria selecionada.  

4.  Na **operador** pendente, selecione o operador a utilizar. Este operador compara a condição selecionada com o valor especificado. Ele avalia se o utilizador ou dispositivo satisfaz o requisito de instalação. Os operadores disponíveis variam consoante a condição selecionada.  

    > [!Note]  
    >  Os requisitos disponíveis variam consoante o tipo de dispositivo que utiliza o tipo de implementação.  

5.  Na **valor** caixa, especifique os valores a utilizar para comparação. Estes valores, juntamente com a condição selecionada e o operador, avaliam se o utilizador ou dispositivo satisfaz os requisitos de instalação. Os valores disponíveis variam consoante a condição selecionada e o operador selecionado.  

6.  Escolher **OK** para guardar o requisito e fechar o **criar requisito** caixa de diálogo.  


### <a name="bkmk_dt-depend"></a> Tipo de implementação **dependências**  

As dependências definem um ou mais tipos de implementação de outra aplicação que o cliente tem de instalar antes que ele instala este tipo de implementação.   

> [!IMPORTANT]  
>  Em alguns casos, um tipo de implementação está dependente de um tipo de implementação que também tenha dependências. O número máximo de dependências suportadas na cadeia é cinco.  

1.  Sobre o **dependências** página, clique em **Add**.  

2.  Na janela Adicionar dependência, introduza o **nome do grupo de dependência**. Este nome refere-se a este grupo de dependências de aplicações.  

3.  Na janela Adicionar dependência, clique em **adicionar**.  

4.  Na **especificar aplicação necessária** janela, selecione uma aplicação disponível e, pelo menos, uma das sua implantação tipos a utilizar como uma dependência.  

    > [!TIP]  
    >  Clique em **vista** para apresentar as propriedades do tipo de aplicação ou implementação selecionado.  

5.  Clique em **OK** para fechar a **especificar aplicação necessária** janela.  

6.  Se pretender que o cliente para instalar automaticamente a aplicação dependente, selecione **instalação automática** junto a dependência.  

    > [!NOTE]  
    >  Não precisa de implementar uma aplicação dependente para o cliente instalar automaticamente.  

7.  Se adicionar mais do que uma dependência, utilize o **aumentar prioridade** e **diminuir prioridade** botões. Estas ações alteram a ordem em que o cliente avalia cada dependência.  

8.  Clique em **OK** para fechar a **adicionar dependência** janela.  


### <a name="bkmk_dt-return"></a> Tipo de implementação **códigos de retorno**

> [!Note]  
> Esta página não está no Assistente para criar tipo de implementação. É apenas uma guia nas propriedades de um tipo de implementação existente.  

Especifique códigos de retorno para controlar os comportamentos depois do tipo de implementação concluída. Por exemplo, sinalize que é necessário um reinício, a instalação estiver concluída. 

1. Sobre o **códigos de retorno** separador da janela de propriedades do tipo de implementação, clique em **Add**.  

2. Na janela de adicionar o código de retorno, especifique a **retornar o valor de código** que espera deste tipo de implementação. Este valor é qualquer número inteiro positivo ou negativo entre `-2147483648` e `2147483647`.  

3. Selecione um **tipo de código** na lista pendente. Esta definição define como o Configuration Manager interpreta o código de retorno especificado deste tipo de implementação. Os tipos disponíveis variam consoante a tecnologia de tipo de implementação.   

    - **Êxito (não reiniciado)**: O tipo de implementação foi instalado com êxito e a reinicialização não será necessária.  

    - **Falha (não reiniciado)**: Não foi possível instalar o tipo de implementação.  

    - **Reinício por hardware**: O tipo de implementação instalado com êxito, mas requer o dispositivo seja reiniciado. Nada mais pode ser instalado até que o dispositivo for reiniciado.  

    - **Reinício por software**: O tipo de implementação instalado com êxito, pedidos, mas o dispositivo seja reiniciado. Outras instalações podem ocorrer antes do dispositivo for reiniciado.    

    - **Repetição rápida**: Já existe outra instalação em curso no dispositivo. O cliente tenta novamente a cada duas horas, para um total de 10 vezes.  

4. Opcionalmente, introduza um **Name** e **Descrição** para este código de retorno.

5. Clique em **OK** para fechar a janela de adicionar o código de retorno.  


#### <a name="example-non-zero-success"></a>Exemplo: sucesso de diferente de zero
Estiver implantando um aplicativo que retorna um código de saída `1` quando ele instala com êxito. Por predefinição, o Configuration Manager detetar este código de retorno diferente de zero como uma falha. Especifique o valor de código de retorno de `1`e selecione o tipo de código de **êxito (não reiniciado)**. Agora, o Configuration Manager interpreta que retornam o código como um êxito para este tipo de implementação.


#### <a name="default-return-codes"></a>Códigos de retorno de predefinição
Quando criar alguns tipos de implementação, o Configuration Manager adiciona automaticamente que os seguintes códigos que são comuns a que a tecnologia de retorno:  

**Windows Installer (\*arquivo. msi)**  
|Valor    |Tipo de código|
|---------|---------|
|0        |Êxito (não reiniciado)|
|versão 1707     |Êxito (não reiniciado)|
|3010     |Reinício por software|
|1641     |Reinício por hardware|
|1618     |Repetição rápida|

**Instalador de script**  
|Valor    |Tipo de código|
|---------|---------|
|0        |Êxito (não reiniciado)|
|1641     |Reinício por hardware|
|3010     |Reinício por software|
|1618     |Repetição rápida|

**Pacote de aplicação do Windows (\*. AppX, \*. appxbundle, \*.msix, \*.msixbundle)**  
|Valor    |Tipo de código|
|---------|---------|
|15605    |Repetição rápida|
|15618    |Repetição rápida|



## <a name="bkmk_appv"></a> Opções adicionais para tipos de implementação de App-V  

Configure opções adicionais que são exclusivas para tipos de implementação para aplicações virtuais (App-V).  

### <a name="bkmk_appv-content"></a> Tipo de implementação de App-V **conteúdo** opções  

1.  Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho, expanda **gestão de aplicações**e selecione o **aplicativos** nó.  

2.  Selecione uma aplicação com um tipo de implementação de App-V e clique em **propriedades**.  

3.  Nas propriedades da aplicação, mude para o **tipos de implementação** separador. Selecione o tipo de implementação de App-V e clique em **editar**.  

4.  Nas propriedades do tipo de implementação, mude para o **conteúdo** separador. Configure as seguintes opções conforme necessário:  

    -   **Manter conteúdo na cache do cliente**: O cliente do Configuration Manager não elimine a partir da respetiva cache o conteúdo para este tipo de implementação.  

    -   **Carregar conteúdo para a cache de App-V antes de iniciar**: Antes do aplicativo é iniciado, o cliente do Configuration Manager carrega no cache do App-V todo o conteúdo para este tipo de implementação. O cliente não afixe conteúdo na cache. Elimina o conteúdo conforme necessário.  

5.  Clique em **OK** para fechar as propriedades de tipo de implementação. Em seguida, clique em **OK** para fechar as propriedades da aplicação.  


### <a name="bkmk_appv-pub"></a> Tipo de implementação de App-V **publicação** opções   

1.  Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho, expanda **gestão de aplicações**e selecione o **aplicativos** nó.  

2.  Selecione uma aplicação com um tipo de implementação de App-V e clique em **propriedades**.  

3.  Nas propriedades da aplicação, mude para o **tipos de implementação** separador. Selecione o tipo de implementação de App-V e clique em **editar**.  

4.  Nas propriedades do tipo de implementação, mude para o **publicação** separador. Selecione os itens na aplicação virtual que pretende publicar.  

5.  Clique em **OK** para fechar as propriedades de tipo de implementação. Em seguida, clique em **OK** para fechar as propriedades da aplicação.  



## <a name="bkmk_import"></a> Importar uma aplicação  

Utilize o procedimento seguinte para importar uma aplicação para o Configuration Manager: 

1.  Na consola do Configuration Manager, vá para o **biblioteca de Software** área de trabalho, expanda **gestão de aplicações**e selecione o **aplicativos** nó.   

2.  No Friso, no **home page** separador e o **Create** , clique em **importar aplicação**.  

3.  Sobre o **gerais** página do Assistente para importar aplicação, especifique o caminho de rede para o **ficheiro** para importar. Por exemplo, `\\server\share\file.zip`. Este ficheiro é um arquivo compactado válido (formato ZIP) de uma aplicação exportada do Configuration Manager.  

4.  Sobre o **conteúdo do ficheiro** , selecione a ação a tomar se esta aplicação é um duplicado de um aplicativo existente. Criar um novo aplicativo, ou ignorar o duplicado e adicionar uma nova revisão à aplicação existente.  

5.  Sobre o **resumo** página, reveja as ações e, em seguida, conclua o assistente.  

A nova aplicação aparece no nó **Aplicações**.  

> [!TIP]  
>  O cmdlet do Windows PowerShell **Import-CMApplication** tem a mesma função que este procedimento. Para obter mais informações, consulte [Import-CMApplication](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmapplication?view=sccm-ps).  

Para obter mais informações sobre como exportar uma aplicação, consulte [tarefas de gestão para aplicações](/sccm/apps/deploy-use/management-tasks-applications). 



## <a name="bkmk_deploy-types"></a> Tipos de implementação suportados  

O Configuration Manager suporta os seguintes tipos de implementação para aplicações:

| Nome do tipo de implementação | Descrição |   
|--------------------------|----------------------|  
| **Windows Installer (\*arquivo. msi)** | Um ficheiro de instalador do Windows. |  
| **Pacote de aplicação do Windows (\*. AppX, \*. appxbundle)** | Para o Windows 8 ou posterior. Selecione um ficheiro de pacote de aplicação do Windows ou um pacote de pacote de aplicação do Windows. |  
| **Pacote de aplicação do Windows (\*. AppX, \*. appxbundle, \*.msix, \*.msixbundle)** | A partir da versão 1806, para o novo pacote de aplicação do Windows 10 (.msix) e formatos de pacote (.msixbundle) da aplicação. Selecione um ficheiro de pacote de aplicação do Windows ou um pacote de pacote de aplicação do Windows.<!--1357427--> |  
| **Pacote de aplicação do Windows (na Store Windows)** | Para o Windows 8 ou posterior. Especifique uma ligação para a aplicação na Windows Store ou procurar loja para selecionar a aplicação.<sup>[Nota 1](#bkmk_note1)</sup> |  
| **Instalador de script** | Especifica um script ou programa que é executado nos clientes do Windows para instalar o conteúdo ou para efetuar uma ação. Utilize este tipo de implementação para instaladores setup.exe ou invólucros de script. |  
| **Microsoft Application Virtualization 4** | Um manifesto de v4 Microsoft App-V. |  
| **Microsoft Application Virtualization 5** | Um ficheiro de pacote do Microsoft App-V v5. |  
| **Pacote de aplicação do Windows Phone (\*arquivo. xap)** | Um ficheiro de pacote de aplicação do Windows Phone. |  
| **Pacote de aplicação do Windows Phone (na Store de telefone Windows)** | Especifique uma ligação para a aplicação na Windows Store. |  
| **Pacote de aplicação para iOS (\*ficheiro. IPA)** | Um ficheiro de pacote do Apple iOS aplicação. |  
| **Pacote de aplicação para iOS da App Store** | Especifique uma ligação para a aplicação iOS na Store da Apple. |  
| **Pacote de aplicação para Android (\*ficheiro. apk)** | Um ficheiro de pacote de aplicação Android. |  
| **Pacote de aplicação para Android no Google Play** | Especifique uma ligação para a aplicação na Google Play store. |  
| **Mac OS X** | Para computadores de macOS com o cliente do Configuration Manager. Crie um ficheiro. cmmac com o **CMAppUtil** ferramenta. |  
| **Aplicação Web** | Especifique uma ligação a uma aplicação web. Este tipo de implementação instala um atalho para a aplicação web no dispositivo do utilizador. <sup> [Observe 2](#bkmk_note2)</sup> |  
| **Windows Installer através de MDM (\*. msi)** | Criar e implementar aplicações baseadas no Windows Installer em dispositivos Windows 10. Para obter mais informações, consulte [aplicações de implementar o Windows Installer em dispositivos inscritos na MDM do Windows 10](/sccm/apps/get-started/creating-windows-applications#bkmk_mdm-msi). |  

#### <a name="bkmk_note1"></a> Nota 1: Pacote de aplicações do Windows (na Loja Windows)
Para implementar a aplicação como uma ligação para a Windows Store, configure a política de grupo **desativar a aplicação de Store**. Definir esta política como **desativada** ou **não configurada**. Se ativar esta definição, os clientes não é possível ligar para o Store do Windows para transferir e instalar aplicações.

Os clientes do Windows sempre avaliam os tipos de implementação que utilizam uma ligação para um arquivo antes de outros tipos de implementação. Em seguida, o cliente avalia os tipos de implementação por prioridade. 

#### <a name="bkmk_note2"></a> Nota 2: Aplicação Web  
Se tiver instalado o browser gerido do Microsoft Intune em dispositivos iOS ou Android, certifique-se de que os utilizadores só podem utilizar o browser gerido para abrir a aplicação. O endereço do Web site, substitua **http** com **http-intunemam**, ou **https** com **https-intunemam**. Por exemplo: 
- `http-intunemam://<path to web app>`
- `https-intunemam://<path to web app>`

Utilize o Gestor de configuração [requisitos de aplicação](#bkmk_dt-require) para se certificar de que esse web apps com o browser gerido só são instaladas em dispositivos iOS e Android. 

Para obter mais informações sobre o Intune managed browser, consulte [acesso à internet de gerir através de políticas de browser gerido](/sccm/apps/deploy-use/manage-internet-access-using-managed-browser-policies).



## <a name="next-steps"></a>Passos seguintes

Depois de criar uma aplicação no Configuration Manager, a próxima etapa é [implementar a aplicação](/sccm/apps/deploy-use/deploy-applications).

Para obter mais informações sobre a criação de aplicativos em diferentes plataformas de SO, consulte os artigos seguintes:  
- [Criar aplicações Windows](/sccm/apps/get-started/creating-windows-applications)
- [Criar aplicações para dispositivos móveis](/sccm/mdm/deploy-use/create-applications) (iOS, Windows Mobile e Android)  
- [Criar aplicações para Mac](/sccm/apps/get-started/creating-mac-computer-applications)
- [Criar aplicações de servidor Linux e UNIX](/sccm/apps/get-started/creating-linux-and-unix-server-applications)
- [Criar aplicações Windows Embedded](/sccm/apps/get-started/creating-windows-embedded-applications)

