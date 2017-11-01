---
title: "Criar aplicações para computadores Mac"
titleSuffix: Configuration Manager
description: "Consulte as considerações deve ter em conta quando criar e implementar aplicações para computadores Mac."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ab1aecdd-d943-44f5-b0a9-e8fe7439e5d6
caps.latest.revision: "9"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: 912632c672c49deefc946e089dad6a82454c4b67
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="create-mac-computer-applications-with-system-center-configuration-manager"></a>Criar aplicações para computadores Mac com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Manter as seguintes considerações em mente quando criar e implementar aplicações para computadores Mac.  

> [!IMPORTANT]  
>  Os procedimentos deste tópico abrangem informações sobre como implementar aplicações em computadores de Mac em que instalou o cliente do Configuration Manager. Os computadores Mac que inscreveu no Microsoft Intune não suportam a implementação de aplicação.  

## <a name="general-considerations"></a>Considerações gerais  
 Pode utilizar o System Center Configuration Manager para implementar aplicações em computadores Mac que executem o cliente do Configuration Manager Mac. Os passos para implementar software em computadores Mac são semelhantes aos passos para implementar software em computadores Windows. No entanto, antes de criar e implementar aplicações para computadores Mac que sejam geridos pelo Configuration Manager, considere o seguinte:  

-   Antes de poder implementar pacotes de aplicações para computadores Mac, tem de utilizar o **CMAppUtil** ferramenta num computador Mac para converter estas aplicações num formato que possa ser lido pelo Configuration Manager.  

-   O Configuration Manager não suporta a implementação de aplicações Mac para os utilizadores. Em vez disso, estas implementações têm de ser efetuadas num dispositivo. Da mesma forma, para implementações de aplicações Mac, o Configuration Manager não suporta o **pré-implementar software no dispositivo primário do utilizador** opção o **definições de implementação** página do **Assistente de implementação de Software**.  

-   As aplicações MAC suportam implementações simuladas.  

-   Não é possível implementar aplicações em computadores Mac que tenham um objetivo de **Disponível**.  

-   A opção de enviar pacotes de reativação ao implementar software não é suportada para computadores Mac.  

-   Computadores Mac não suportam a serviço de transferência inteligente em segundo plano (BITS) para transferir o conteúdo da aplicação. Se uma transferência de aplicação falhar, é reiniciado desde o início.  

-   O Configuration Manager não suporta condições globais ao criar tipos de implementação para computadores Mac.  

## <a name="steps-to-create-and-deploy-an-application"></a>Passos para criar e implementar uma aplicação  
 A tabela seguinte fornece os passos, detalhes e informações para criar e implementar aplicações para computadores Mac.  

|Passo|Detalhes|  
|----------|-------------|  
|**Passo 1**: Preparar aplicações Mac para o Configuration Manager|Antes de poder criar aplicações do Configuration Manager a partir de pacotes de software Mac, tem de utilizar o **CMAppUtil** ferramenta num computador Mac para converter o software Mac para o Configuration Manager**. cmmac** ficheiro.|  
|**Passo 2**: Criar uma aplicação do Configuration Manager que contenha o software Mac|Utilize o **Assistente para criar aplicação** para criar uma aplicação para o software Mac.|  
|**Passo 3**: Criar um tipo de implementação para a aplicação Mac|Este passo só será necessário se não tiver importado automaticamente estas informações a partir da aplicação.|  
|**Passo 4**: Implementar a aplicação Mac|Utilize o **Assistente de implementação de Software** para implementar a aplicação em computadores Mac.|  
|**Passo 5**: Monitorize a implementação da aplicação Mac|Monitorize o êxito das implementações de aplicações para computadores Mac.|  

## <a name="supplemental-procedures-to-create-and-deploy-applications-for-mac-computers"></a>Procedimentos suplementares para criar e implementar aplicações para computadores Mac  
 Utilize os procedimentos seguintes para criar e implementar aplicações para computadores Mac que sejam geridos pelo Configuration Manager.  

###  <a name="step-1-prepare-mac-applications-for-configuration-manager"></a>Passo 1: Preparar aplicações Mac para o Configuration Manager  
 O processo para criar e implementar aplicações do Configuration Manager em computadores Mac é semelhante ao processo de implementação para computadores Windows. No entanto, antes de criar aplicações do Configuration Manager que contenham tipos de implementação Mac, tem de preparar as aplicações utilizando o **CMAppUtil** ferramenta. Esta ferramenta é transferida com os ficheiros de instalação do cliente Mac. A ferramenta **CMAppUtil** reúne informações sobre a aplicação, incluindo os dados de deteção dos seguintes pacotes Mac:  

-   Imagem de Disco Apple (.dmg)  

-   Ficheiro de Pacote Meta (.mpkg)  

-   Pacote Instalador do Mac OS X (.pkg)  

-   Aplicação do Mac OS X (.app)  

Após recolher as informações, a ferramenta **CMAppUtil** cria um ficheiro com a extensão **.cmmac**. Este ficheiro contém os ficheiros de instalação do software Mac e informações sobre métodos de deteção que podem ser utilizados para avaliar se a aplicação já está instalada. A ferramenta**CMAppUtil** também pode processar ficheiros **.dmg** que contenham várias aplicações Mac e criar tipos de implementação diferentes para cada aplicação.  

1.  Copie o pacote de instalação do software Mac para a pasta do computador Mac onde extraiu os conteúdos do ficheiro **macclient.dmg** que transferiu a partir do Centro de Transferências da Microsoft.  

2.  No mesmo computador Mac, abra uma janela de terminal e navegue para a pasta onde extraiu os conteúdos do ficheiro **macclient.dmg** .  

3.  Navegue para o **ferramentas** pasta e escreva o seguinte comando da linha de comandos:  

     **./CMAppUtil** *<properties\>*  

     Por exemplo, imagine que pretende converter os conteúdos de um ficheiro de imagem de disco Apple com o nome **MySoftware.dmg** que é armazenado na pasta de ambiente de trabalho do utilizador para um **cmmac** ficheiro na mesma pasta. Pretende também criar **cmmac** ficheiros para todas as aplicações que se encontram no ficheiro de imagem de disco. Para tal, utilize a seguinte linha de comandos:  

     **./CMApputil –c /Users/** *<User Name\>* **/Desktop/MySoftware.dmg -o /Users/** *<User Name\>* **/Desktop -a**  

    > [!NOTE]  
    >  O nome da aplicação não é possível ter mais de 128 carateres.  

     Para configurar as opções da ferramenta **CMAppUtil**, utilize as propriedades da linha de comandos da seguinte tabela:  

  	|Propriedade|Mais informações|  
  	|--------------|----------------------|  
  	|**-h**|Apresenta as propriedades da linha de comandos disponíveis.|  
  	|**-r**|Produz o **detection.xml** do ficheiro **.cmmac** fornecido para **stdout**. A saída contém os parâmetros de deteção e a versão da ferramenta **CMAppUtil** que foi utilizada para criar o ficheiro **.cmmac** .|  
  	|**-c**|Especifica o ficheiro de origem a converter.|  
  	|**-o**|Especifica o caminho de saída em conjunto com a propriedade-c.|  
  	|**-a**|Cria automaticamente os ficheiros. cmmac em conjunto com a propriedade-c para todas as aplicações e pacotes no ficheiro de imagem de disco.|  
  	|**-s**|Ignora a geração de **detection.xml** se não forem encontrados parâmetros de deteção e força a criação do ficheiro **.cmmac** sem o ficheiro **detection.xml** .|  
  	|**-v**|Apresenta uma saída mais detalhada da ferramenta **CMAppUtil** , juntamente com informações de diagnóstico.|  

4.  Certifique-se de que o ficheiro **.cmmac** foi criado na pasta de saída que especificou.  

###  <a name="create-a-configuration-manager-application-that-contains-the-mac-software"></a>Criar uma aplicação do Configuration Manager que contenha o software Mac  

Utilize o procedimento seguinte para ajudar a criar uma aplicação para computadores Mac que sejam geridos pelo Configuration Manager.  

1.  Na consola do Configuration Manager, escolha **biblioteca de Software** > **gestão de aplicações** > **aplicações**.  

3.  No **home page** separador o **criar** grupo, escolha **Criar aplicação**.  

4.  No **geral** página do **Assistente para criar aplicação**, selecione **detetar automaticamente informação sobre esta aplicação nos ficheiros de instalação**.  

    > [!NOTE]  
    >  Se pretender especificar informações acerca da aplicação por si, selecione **especificar manualmente as informações da aplicação**. Para obter mais informações sobre como especificar manualmente as informações, veja [Como criar aplicações com o System Center Configuration Manager](../../apps/deploy-use/create-applications.md).  

5.  Na lista pendente **Tipo** , selecione **Mac OS X**.  

6.  No **localização** campo, especifique o caminho UNC no formato  *\\ \\< servidor\>\\< partilhar\>\\< filename\>*  para o ficheiro de instalação de aplicação Mac (**. cmmac** ficheiro) que detetará as informações da aplicação. Em alternativa, optar **procurar** procurar e especificar a localização do ficheiro de instalação.  

    > [!NOTE]  
    >  Terá de ter acesso ao caminho UNC que contém a aplicação.  

7.  Escolha **seguinte**.  

8.  No **importar informação** página do **Assistente para criar aplicação**, reveja as informações que foram importadas. Se necessário, pode escolher **anterior** para voltar atrás e corrigir os eventuais erros. Escolha **seguinte** para continuar.  

9. No **informações gerais** página do **Assistente para criar aplicação**, especifique as informações sobre a aplicação, tais como o nome da aplicação, comentários, versão e uma referência opcional para o ajudar a referir a aplicação na consola do Configuration Manager.  

    > [!NOTE]  
    >  Algumas das informações da aplicação poderão já estar nesta página, se tiverem sido obtidas anteriormente a aplicação nos ficheiros de instalação.  

10. Escolha **seguinte**, reveja as informações da aplicação no **resumo** página e, em seguida, conclua o **Assistente para criar aplicação**.  

11. A nova aplicação é apresentada no **aplicações** nós da consola do Configuration Manager.  

###  <a name="step-3-create-a-deployment-type-for-the-mac-application"></a>Passo 3: Criar um tipo de implementação para a aplicação Mac  
 Utilize o procedimento seguinte para ajudar a criar um tipo de implementação para computadores Mac que sejam geridos pelo Configuration Manager.  

> [!NOTE]  
>  Se tiver importado automaticamente informações sobre a aplicação no **Assistente para criar aplicação**, um tipo de implementação para a aplicação poderá já ter sido criado.  

1.  Na consola do Configuration Manager, escolha **biblioteca de Software** > **gestão de aplicações** > **aplicações**.  

3.  Selecione uma aplicação. Em seguida, no **home page** separador o **aplicação** grupo, escolha **criar tipo de implementação** para criar um novo tipo de implementação para esta aplicação.  

    > [!NOTE]  
    >  Também pode iniciar o **implementação Assistente para criar tipo** do **Assistente para criar aplicação** e para o **tipos de implementação** separador do *< nome da aplicação\>*  **propriedades** caixa de diálogo.  

4.  No **geral** página do **implementação Assistente para criar tipo**, no **tipo** na lista pendente, selecione **Mac OS X**.  

5.  No **localização** campo, especifique o caminho UNC no formato \\ \\< servidor\>\\< partilhar\>\\< filename\> para o ficheiro de instalação da aplicação (**. cmmac** ficheiro). Em alternativa, optar **procurar** procurar e especificar a localização do ficheiro de instalação.  

    > [!NOTE]  
    >  Terá de ter acesso ao caminho UNC que contém a aplicação.  

6.  Escolha **seguinte**.  

7.  Na página **Importar Informação** do **Assistente para Criar Tipo de Implementação**, reveja as informações que foram importadas. Se necessário, escolha **anterior** para voltar atrás e corrigir os eventuais erros. Escolha **seguinte** para continuar.  

8.  Na página **Informações Gerais** do **Assistente para Criar Tipo de Implementação**, especifique informações sobre a aplicação, tais como o respetivo nome, comentários e os idiomas em que o tipo de implementação está disponível.  

    > [!NOTE]  
    >  Algumas das informações de tipo de implementação podem já estar nesta página, se tiverem sido obtidas anteriormente a aplicação nos ficheiros de instalação.  

9. Escolha **seguinte**.  

10. No **requisitos** página do **implementação Assistente para criar tipo**, pode especificar as condições que devem ser satisfeitas para que o tipo de implementação possa ser instalado em computadores Mac.  

11. Escolha **adicionar** para abrir o **criar requisito** diálogo caixa e adicionar um novo requisito.  

    > [!NOTE]  
    >  Também pode adicionar novos requisitos no **requisitos** separador do *< nome do tipo de implementação\>*  **propriedades** caixa de diálogo.  

12. Na lista pendente **Categoria** , selecione que este requisito se aplica a um dispositivo.  

13. Do **condição** pendente lista, selecione a condição que pretende utilizar para avaliar se o computador Mac cumpre os requisitos de instalação. O conteúdo desta lista varia consoante a categoria que selecionar.  

14. Do **operador** pendente lista, escolha o operador a utilizar para comparar a condição selecionada com o valor especificado para avaliar se o utilizador ou dispositivo satisfaz os requisitos de instalação. Os operadores disponíveis variam consoante a condição selecionada.  

15. No **valor** campo, especifique os valores a utilizar com a condição e operador selecionados para avaliar se o utilizador ou dispositivo satisfaz o requisito de instalação. Os valores disponíveis variam consoante a condição e operador que selecionar.

16. Escolha **OK** para guardar a regra de requisito e sair do **criar requisito** caixa de diálogo.  

17. No **requisitos** página do **implementação Assistente para criar tipo**, escolha **seguinte**.  

18. Na página **Resumo** do **Assistente para Criar Tipo de Implementação**, reveja as ações que o assistente deverá executar.  Se necessário, escolha **anterior** para voltar atrás e alterar as definições de tipo de implementação. Escolha **seguinte** para criar o tipo de implementação.  

19. Depois do **progresso** página depois de concluída, reveja as ações que foram executadas e, em seguida, escolha **fechar** para concluir a **implementação Assistente para criar tipo**.  

20. Se tiver iniciado o Assistente do **Assistente para criar aplicação**, regressará ao **tipos de implementação** página.  

###  <a name="deploy-the-mac-application"></a>Implementar a aplicação Mac  
 Os passos para implementar uma aplicação em computadores Mac são os mesmos que os passos para implementar uma aplicação em computadores Windows, exceto as seguintes diferenças:  

-   A implementação de aplicações para utilizadores não é suportada.  

-   Não são suportadas implementações que tenham um objetivo de **Disponível** .  

-   O **pré-implementar software no dispositivo primário do utilizador** opção o **definições de implementação** página do **Assistente de implementação de Software** não é suportada.  

-   Porque os computadores Mac não suportam o Centro de Software, a definição **notificações do utilizador** no **experiência de utilizador** página do **Assistente de implementação de Software** é ignorada.  

-   A opção de enviar pacotes de reativação ao implementar software não é suportada para computadores Mac.  

> [!NOTE]  
>  Pode criar uma coleção que contenha apenas computadores Mac. Para tal, crie uma coleção que utilize uma regra de consulta e utilize a consulta de exemplo WQL no [como criar consultas](../../core/servers/manage/create-queries.md) tópico.  

 Para obter mais informações, consulte [implementar aplicações](../../apps/deploy-use/deploy-applications.md).  

###  <a name="step-5-monitor-the-deployment-of-the-mac-application"></a>Passo 5: Monitorize a implementação da aplicação Mac  
 Pode utilizar o mesmo processo para monitorizar implementações de aplicações para computadores Mac, tal como faria para monitorizar implementações de aplicações para computadores Windows.  

 Para obter mais informações, consulte [monitorizar aplicações](/sccm/apps/deploy-use/monitor-applications-from-the-console).  
