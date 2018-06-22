---
title: 'Criar itens de configuração para a computadores geridos pelo cliente do Windows '
titleSuffix: Configuration Manager
description: Gerir as definições para servidores com um item de configuração personalizado do Windows computadores de secretária e servidores e computadores Windows.
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 1eb2fcaf-acac-4388-9b31-6cccafacaabe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b2b2af6c022d854a6c6d623e3901abac70d42c7a
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32342788"
---
# <a name="how-to-create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-system-center-configuration-manager-client"></a>Como criar itens de configuração personalizados para computadores de secretária e de servidor do Windows geridos com o cliente do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Utilizar o System Center Configuration Manager **personalizado Windows Desktops and Servers** item de configuração para gerir as definições para computadores com o Windows e servidores que são geridos pelo cliente do Configuration Manager.  

## <a name="start-the-create-configuration-item-wizard"></a>Iniciar o Assistente de item de configuração criar

1.  Na consola do Configuration Manager, clique em **ativos e compatibilidade** > **as definições de compatibilidade** > **itens de configuração**.  

3.  No separador **Início** , no grupo **Criar** , clique em **Criar Item de Configuração**.  

4.  Na página **Geral** do **Assistente de Criação de Item de Configuração**, especifique um nome e uma descrição opcional para o item de configuração.  

5.  Em **Especifique o tipo de item de configuração que pretende criar**, selecione **Servidores e Computadores de Secretária Windows (personalizado)**.  

    > [!TIP]  
    >  Se pretender fornecer as definições do método de deteção que verificam a existência de uma aplicação, selecione **Este ficheiro de configuração contém as definições da aplicação**.  

6.  Clique em **categorias** se criar e atribuir categorias para o ajudar a procurar e filtrar itens de configuração na consola do Configuration Manager.  

## <a name="provide-detection-method-information"></a>Fornecer informações do método de deteção  
 Utilize este procedimento para fornecer informações do método de deteção para o item de configuração.  

> [!NOTE]  
>  Aplica-se apenas se tiver selecionado **Este item de configuração contém as definições da aplicação** na página **Geral** do assistente.  

 Um método de deteção no Configuration Manager contém regras que são utilizadas para detetar se uma aplicação é instalada num computador. Esta deteção ocorre antes de o item de configuração ser avaliado relativamente à compatibilidade. Para detetar se uma aplicação está instalada, pode detetar a presença de um ficheiro do Windows Installer para a aplicação, utilizar um script personalizado ou selecionar **Assumir sempre que a aplicação está instalada** para avaliar o item de configuração relativamente à compatibilidade, independentemente se a aplicação está instalada.  

 Utilize estes procedimentos para configurar os métodos de deteção no System Center Configuration Manager.  

### <a name="to-detect-an-application-installation-by-using-the-windows-installer-file"></a>Para detetar uma instalação de aplicações utilizando o ficheiro do Windows Installer  

1.  Na página **Métodos de Deteção** do **Assistente de Criação de Item de Configuração**, selecione a caixa de verificação **Utilizar deteção do Windows Installer**.  

2.  Clique em **Abrir**, navegue até ao ficheiro do Windows Installer (.msi) que pretende detetar e, em seguida, clique em **Abrir**.  

3.  A caixa **Versão** é preenchida automaticamente com o número de versão do ficheiro do Windows Installer que selecionou. Pode introduzir um novo número de versão nesta caixa, se o valor apresentado estiver incorreto.  

4.  Selecione a caixa de verificação **Esta aplicação está instalada para um ou mais utilizadores** se pretender detetar cada perfil de utilizador no computador.  

### <a name="to-detect-a-specific-application-and-deployment-type"></a>Para detetar uma aplicação e um tipo de implementação específicos  

1.  Na página **Métodos de Deteção** do **Assistente de Criação de Item de Configuração**, selecione a caixa de verificação **Detetar uma aplicação e um tipo de implementação específicos** e, em seguida, clique em **Selecionar**.  

2.  Na caixa de diálogo **Especificar Aplicação**, selecione a aplicação e um tipo de implementação associados que pretende detetar.  

### <a name="to-detect-an-application-installation-by-using-a-custom-script"></a>Para detetar uma instalação de aplicações utilizando um script personalizado  

1.  Na página **Métodos de Deteção** do **Assistente de Criação de Item de Configuração**, selecione a caixa de verificação **Utilize um script personalizado para detetar esta aplicação**.  

2.  Na lista, selecione a linguagem do script que pretende abrir. Pode escolher um dos seguintes scripts:  

    -   **VBScript**  

    -   **JScript**  

    -   **PowerShell**  

3.  Clique em **Abrir**, navegue até ao script que pretende utilizar e, em seguida, clique em **Abrir**.  

##  <a name="configure-settings"></a>Configurar definições  
 Utilize este procedimento para configurar as definições no item de configuração.  

 As definições representam as condições empresariais ou técnicas utilizadas para avaliar a compatibilidade nos dispositivos cliente. Pode configurar uma nova definição ou navegar para uma definição existente num computador de referência.  

1.  Na página **Definições** do **Assistente de Criação de Item de Configuração**, clique em **Novo**.  

2.  No separador **Geral** da caixa de diálogo **Criar Definição**, forneça as seguintes informações:  

    -   **Nome:** Introduza um nome exclusivo para a definição. Pode utilizar até 256 carateres.  

    -   **Descrição:** Introduza uma descrição para a definição. Pode utilizar até 256 carateres.  

    -   **Tipo de definição:** Na lista, escolha e configure um dos seguintes tipos de definição a utilizar para esta definição:  

        -   **Consulta do Active Directory**  

             **Prefixo LDAP** - Especifique um prefixo válido para a consulta dos Serviços de Domínio do Active Directory para avaliar a compatibilidade em computadores cliente. Pode utilizar **LDAP://** ou **GC://** para fazer uma pesquisa de catálogo global.  

             **Nome Único (DN)** - Especifique o nome único do objeto dos Serviços de Domínio do Active Directory avaliado relativamente à compatibilidade em computadores cliente.  

             Por exemplo, se pretender avaliar um valor relacionado com um utilizador com o nome João Silva no domínio corp.contoso.com, introduza o seguinte:  

            -   **Filtro de pesquisa** - Especifique um filtro de LDAP opcional para refinar os resultados da consulta dos Serviços de Domínio do Active Directory para avaliar a compatibilidade em computadores cliente.  

                 Para devolver todos os resultados da consulta, introduza **(objectclass=\*)**.  

            -   **Âmbito da procura** - Especifique o âmbito da procura nos Serviços de Domínio do Active Directory. Pode escolher entre:  

                -   **Base** - Consulta apenas o objeto especificado.  

                -   **Um nível** -esta opção não está a ser utilizada nesta versão do Configuration Manager.  

                -   **Subárvore** - Consulta o objeto especificado e a respetiva subárvore completa no diretório.  

            -   **Propriedade** - Especifique a propriedade do objeto dos Serviços de Domínio do Active Directory utilizada para avaliar a compatibilidade em computadores cliente.  

                 Por exemplo, se pretender consultar a propriedade do Active Directory **badPwdCount**, a qual armazena o número de vezes que um utilizador introduz incorretamente uma palavra-passe, introduza **badPwdCount** neste campo.  

            -   **Consulta** - Apresenta a consulta construída a partir das entradas em **Prefixo LDAP**, **Nome único (DN)**, **Filtro de pesquisa** (se especificado) e **Propriedade**, utilizados para avaliar a compatibilidade em computadores cliente.  

             Para mais informações sobre a construção de consultas LDAP, consulte a documentação do Windows Server.  

        -   **Assemblagem**  

             Configure as seguintes opções para este tipo de definição:  

            -   **Nome da assemblagem:** Especifica o nome do objeto de assemblagem que pretende procurar. O nome não pode ser igual ao de outros objetos de assemblagem do mesmo tipo e tem de estar registado na Global Assembly Cache. O nome da assemblagem pode ter até 256 carateres.  

             Uma assemblagem é um fragmento de código que pode ser partilhado entre aplicações. As assemblagens podem ter a extensão de nome de ficheiro .dll ou .exe. A Global Assembly Cache é uma pasta denominada *%systemroot%\Assembly* nos computadores cliente onde são armazenadas todas as assemblagens partilhadas.  

        -   **Sistema de ficheiros**  

            -   **Tipo** – Na lista, selecione se pretende procurar um **Ficheiro** ou uma **Pasta**.  

            -   **Caminho** – Especifique o caminho da pasta ou do ficheiro especificado nos computadores cliente. Pode especificar variáveis de ambiente do sistema e a variável de ambiente *%USERPROFILE%* no caminho.  

                > [!NOTE]  
                >  Se utilizar a variável de ambiente *%USERPROFILE%* nas caixas **Caminho** ou **Nome de ficheiro ou pasta**, são procurados todos os perfis de utilizador no computador cliente, o que pode resultar em várias instâncias do ficheiro ou pasta encontradas.  
                >   
                >  Se as definições de compatibilidade não tiverem acesso ao caminho especificado, é gerado um erro de deteção. Além disso, se o ficheiro que está a procurar estiver atualmente em utilização, é gerado um erro de deteção.  

            -   **Nome do ficheiro ou da pasta** – Especifique o nome do objeto de ficheiro ou pasta a procurar. Pode especificar variáveis de ambiente do sistema e a variável de ambiente *%USERPROFILE%* no nome da pasta ou ficheiro. Também pode utilizar os carateres universais * e ? no nome de ficheiro.  

                > [!NOTE]  
                >  Se especificar um nome de ficheiro ou pasta e utilizar carateres universais, esta combinação poderá produzir um elevado número de resultados e pode resultar numa utilização intensiva de recursos no computador cliente e tráfego de rede elevado ao reportar os resultados para o Configuration Manager.  

            -   **Incluir subpastas** – ative esta opção se também pretender procurar em todas as subpastas do caminho especificado.  

            -   **Este ficheiro ou pasta está associado a uma aplicação de 64 bits** - Se estiver ativada, apenas as localizações de ficheiros de 64 bits (como *%ProgramFiles%*) serão verificadas nos computadores de 64 bits. Se esta opção não estiver ativada, ambas as localizações de 32 bits (como *%ProgramFiles(x86)%*) e 64 bits serão verificadas.  

                > [!NOTE]  
                >  Se o mesmo ficheiro ou pasta existir em ambas as localizações no mesmo computador de 64 bits, são detetados múltiplos ficheiros pela condição global.  

             O tipo de definição **Sistema de ficheiros** não suporta a especificação de um caminho UNC de partilha de rede na caixa **Caminho**.  

        -   **Metabase do IIS**  

            -   **Caminho da metabase** - Especifique um caminho válido para a Metabase dos Serviços de Informação Internet (IIS).  

            -   **ID da Propriedade** - especifique a propriedade numérica da definição da Metabase do IIS.  

        -   **Chave de registo**  

            -   **Hive** – Na lista, selecione o ramo de registo onde pretende procurar.  

            -   **Chave** – Especifique o nome da chave de registo que pretende procurar. Utilize o formato *key\subkey*.  

            -   **Esta chave de registo está associada a uma aplicação de 64 bits** – Especifica se a procura deve ser feita nas chaves de registo de 64 bits, além das chaves de registo de 32 bits, em clientes com uma versão de 64 bits do Windows.  

                > [!NOTE]  
                >  Se a mesma chave de registo existir nas localizações do registo de 64 bits e de 32 bits no mesmo computador de 64 bits, a condição global deteta ambas as chaves de registo.  

        -   **Valor de registo**  

            -   **Hive** – Na lista, selecione o ramo de registo onde pretende procurar.  

            -   **Chave** – especifique o nome da chave de registo que pretende procurar. Utilize o formato *key\subkey*.  

            -   **Valor** – Especifique o valor que deve estar incluído na chave de registo especificada.  

            -   **Esta chave de registo está associada a uma aplicação de 64 bits** – Especifica se a procura deve ser feita nas chaves de registo de 64 bits, além das chaves de registo de 32 bits, em clientes com uma versão de 64 bits do Windows.  

                > [!NOTE]  
                >  Se a mesma chave de registo existir nas localizações do registo de 64 bits e de 32 bits no mesmo computador de 64 bits, a condição global deteta ambas as chaves de registo.  

             Também pode clicar em **Procurar** para navegar para uma localização de registo no computador ou num computador remoto. Para procurar um computador remoto, tem de ter direitos de administrador no computador remoto e o computador remoto tem de executar o serviço de registo remoto.  

        -   **Script**  

            -   **Script de deteção** – Clique em **Adicionar** para introduzir ou navegue para o script que pretende utilizar. Pode utilizar scripts do Windows PowerShell, VBScript ou Microsoft JScript.  

            -   **Executar scripts ao utilizar as credenciais do utilizador com sessão iniciada** – Se ativar esta opção, o script é executado nos computadores cliente que utilizam as credenciais dos utilizadores com sessão iniciada.  

                > [!NOTE]  
                >  O valor devolvido pelo script é utilizado para avaliar a compatibilidade da condição global. Por exemplo, quando utilizar VBScript, poderá utilizar o comando **WScript.Echo Result** para devolver o valor da variável *Result* à condição global.  

        -   **Consulta SQL**  

            -   **Instância do SQL Server** – escolha se pretende que a consulta SQL seja executada na instância predefinida, em todas as instâncias ou na instância de base de dados com o nome especificado.  

                > [!NOTE]  
                >  O nome da instância deve referir-se a uma instância local do SQL Server. Para fazer referência a uma instância do SQL Server em cluster, deverá utilizar uma definição de script.  

            -   **Base de dados** – Especifique o nome da base de dados do Microsoft SQL Server relativamente à qual pretende executar a consulta SQL.  

            -   **Coluna** – Especifique o nome da coluna devolvido pela instrução Transact-SQL utilizada para avaliar a compatibilidade da condição global.  

            -   **Instrução Transact-SQL** – Especifique a consulta SQL completa que pretende utilizar para a condição global. Também pode clicar em **Abrir** para abrir uma consulta SQL existente.  

                > [!IMPORTANT]  
                >  As definições da Consulta SQL não suportam os comandos SQL que modificam a base de dados. Apenas pode utilizar comandos SQL que leem as informações da base de dados.  

        -   **Consulta WQL**  

            -   **Espaço de nomes** - Especifique o espaço de nomes Windows Management Instrumentation (WMI) utilizado para criar uma consulta WQL avaliada relativamente à compatibilidade em computadores cliente. O valor predefinido é Root\cimv2.  

            -   **Classe** - Especifica a classe WMI utilizada para criar uma consulta WQL avaliada relativamente à compatibilidade em computadores cliente.  

            -   **Propriedade** - Especifica a propriedade WMI utilizada para criar uma consulta WQL avaliada relativamente à compatibilidade em computadores cliente.  

            -   **Cláusula WHERE da consulta WQL** - pode utilizar o item **Cláusula WHERE da consulta WQL** para especificar uma cláusula WHERE a aplicar ao espaço de nomes, à classe e à propriedade especificados nos computadores cliente.  

        -   **Consulta XPath**  

            -   **Caminho** - Especifique o caminho para o ficheiro .xml em computadores cliente utilizado para avaliar a compatibilidade. O Configuration Manager suporta a utilização de todas as variáveis de ambiente de sistema do Windows e o *% USERPROFILE %* variável de utilizador no nome do caminho.  

            -   **Nome do ficheiro XML** - Especifique o nome de ficheiro que contém a consulta XML utilizada para avaliar a compatibilidade em computadores cliente.  

            -   **Incluir subpastas** - ative esta opção se também pretender procurar em todas as subpastas do caminho especificado.  

            -   **Este ficheiro está associado uma aplicação de 64 bits** -escolher se o sistema de 64 bits localização de ficheiros (*% windir %* \System32) deve ser pesquisada, além da localização do ficheiro de sistema de 32 bits (*% windir %* \Syswow64) em clientes do Configuration Manager que executam uma versão de 64 bits do Windows.  

            -   **Consulta XPath** - Especifique uma consulta da linguagem XPath completa e válida utilizada para avaliar a compatibilidade em computadores cliente.  

            -   **Espaços de Nomes** - Abre a caixa de diálogo **Espaços de Nomes XML** para identificar espaços de nomes e prefixos a utilizar durante a consulta XPath.  

             Se tentou detetar um ficheiro .xml encriptado, as definições de compatibilidade localizam o ficheiro, mas a consulta XPath não produz resultados e não é gerado nenhum erro.  

             Se a consulta XPath não for válida, a definição é avaliada como não compatível em computadores cliente.  

    -   **Tipo de dados:** Na lista, escolha o formato no qual a condição devolve os dados antes de ser utilizado para avaliar a definição. A lista **Tipo de dados** não é apresentada para todos os tipos de definição.  

        > [!NOTE]  
        >  O tipo de dados **Vírgula flutuante** suporta apenas três dígitos depois da casa decimal.  

3.  Configure detalhes adicionais sobre esta definição na lista **Tipo de definição**. Os itens que pode configurar variam consoante o tipo de definição selecionado.  

    > [!NOTE]  
    >  Quando criar definições do tipo **Sistema de ficheiros**, **Chave de registo** e **Valor de registo**, pode clicar em **Procurar** para configurar a definição a partir de valores num computador de referência. Para procurar uma chave ou valor de registo num computador remoto, o computador remoto tem de ter o serviço Registo Remoto ativado.  

4.  Clique em **OK** para guardar a definição e fechar a caixa de diálogo **Criar Definição**.  

##  <a name="configure-compliance-rules"></a>Configurar regras de compatibilidade  
 Utilize o procedimento seguinte para configurar regras de compatibilidade para o item de configuração.  

 As regras de compatibilidade especificam as condições que definem a compatibilidade de um item de configuração. Antes de poder ser avaliada a compatibilidade de uma definição, tem de ter, pelo menos, uma regra de compatibilidade. O WMI, o registo e as definições de script permitem remediar os valores considerados não compatíveis. Pode criar novas regras ou navegar para uma definição existente em qualquer item de configuração para selecionar regras no mesmo.  

### <a name="to-create-a-compliance-rule"></a>Para criar uma regra de compatibilidade  

1.  Na página **Regras de Compatibilidade** do **Assistente de Criação de Item de configuração**, clique em **Novo**.  

2.  Na caixa de diálogo **Criar Regra**, forneça as seguintes informações:  

    -   **Nome:** Introduza um nome para a regra de compatibilidade.  

    -   **Descrição:** Introduza uma descrição para a regra de compatibilidade.  

    -   **Definição selecionada:** Clique em **procurar** para abrir o **selecionar definição** caixa de diálogo. Selecione a definição na qual pretende definir uma regra ou clique em **Nova Definição**. Quando terminar, clique em **Selecionar**.  

        > [!NOTE]  
        >  Também pode clicar em **Propriedades** para ver informações sobre a definição atualmente selecionada.  

    -   **Tipo de regra:** Selecione o tipo de regra de compatibilidade que pretende utilizar:  

        -   **Valor** Crie uma regra que compara o valor devolvido pelo item de configuração com um valor que especificar.  

        -   **Existencial** Crie uma regra que avalie a definição consoante se existe num dispositivo cliente ou o número de vezes que pode ser encontrada.  

    -   Num tipo de regra de **Valor**, especifique as seguintes informações:  

        -   **A definição deve cumprir a seguinte regra** – Selecione um operador e um valor que é avaliado quanto à compatibilidade com a definição selecionada. Pode utilizar os seguintes operadores:  

            |Operador|Mais informações|  
            |--------------|----------------------|  
            |É igual a|Não existem informações adicionais|  
            |Não é igual a|Não existem informações adicionais|  
            |Maior que|Não existem informações adicionais|  
            |Menor que|Não existem informações adicionais|  
            |Entre|Não existem informações adicionais|  
            |Maior que ou igual a|Não existem informações adicionais|  
            |Menor que ou igual a|Não existem informações adicionais|  
            |Um de|Na caixa de texto, especifique uma entrada em cada linha.|  
            |Nenhum de|Na caixa de texto, especifique uma entrada em cada linha.|  

        -   **Remediar regras incompatíveis quando suportado** – selecione esta opção se pretender que o Configuration Manager retifique automaticamente as regras incompatíveis. O Configuration Manager pode remediar automaticamente os seguintes tipos de regra:  

            -   **Valor de registo** – O valor de registo é remediado se não for compatível e criado se não existir.  

            -   **Script** (executando automaticamente um script de remediação).  

            -   **Consulta WQL**  

            > [!IMPORTANT]  
            >  Só pode remediar regras incompatíveis quando o operador de regra estiver definido como **É igual a**.  

        -   **Reportar incompatibilidade se a instância desta definição não for encontrada** – O item de configuração reporta a incompatibilidade se esta definição não for encontrada em computadores cliente.  

        -   **Gravidade de incompatibilidade para relatórios:** Especifique o nível de gravidade reportado (em relatórios do Configuration Manager) se esta regra de compatibilidade falhar. Os níveis de gravidade disponíveis são os seguintes:  

            -   **Nenhum** computadores que não cumpram esta regra de compatibilidade não reportam uma gravidade de falha.  

            -   **Informações** os computadores que não cumpram esta regra de compatibilidade reportam uma gravidade de falha de **informações**.  

            -   **Aviso** os computadores que não cumpram esta regra de compatibilidade reportam uma gravidade de falha de **aviso**.  

            -   **Crítico** os computadores que não cumpram esta regra de compatibilidade reportam uma gravidade de falha de **críticos**.  

            -   **Crítico com evento** os computadores que não cumpram esta regra de compatibilidade reportam uma gravidade de falha de **críticos**. Este nível de gravidade é também registado como um evento do Windows no registo de eventos de aplicações.  

        -   Para um tipo de regra **Existencial**, especifique as seguintes informações:  

            > [!NOTE]  
            >  As opções apresentadas podem variar consoante o tipo de definição para o qual está a configurar uma regra.  

            -   **A definição deve existir nos dispositivos cliente**  

            -   **A definição não deve existir nos dispositivos cliente**  

            -   **A definição ocorre o seguinte número de vezes:**  

        -   **Gravidade de incompatibilidade para relatórios:** Especifique o nível de gravidade reportado (em relatórios do Configuration Manager) se esta regra de compatibilidade falhar. Os níveis de gravidade disponíveis são os seguintes:  

            -   **Nenhum** computadores que não cumpram esta regra de compatibilidade não reportam uma gravidade de falha.  

            -   **Informações** os computadores que não cumpram esta regra de compatibilidade reportam uma gravidade de falha de **informações**.  

            -   **Aviso** os computadores que não cumpram esta regra de compatibilidade reportam uma gravidade de falha de **aviso**.  

            -   **Crítico** os computadores que não cumpram esta regra de compatibilidade reportam uma gravidade de falha de **críticos**.  

            -   **Crítico com evento** os computadores que não cumpram esta regra de compatibilidade reportam uma gravidade de falha de **críticos**. Este nível de gravidade é também registado como um evento do Windows no registo de eventos de aplicações.  

3.  Clique em **OK** para fechar a caixa de diálogo **Criar Regra**.  

##  <a name="specify-supported-platforms"></a>Especificar plataformas suportadas  
 As plataformas suportadas são os sistemas operativos em que um item de configuração é avaliado relativamente à compatibilidade.  

Na página **Plataformas Suportadas** do **Assistente de Criação de Item de configuração**, na lista, selecione as versões do Windows nas quais pretende que o item de configuração seja avaliado relativamente à compatibilidade ou clique em **Selecionar tudo**.  

## <a name="complete-the-wizard"></a>Concluir o assistente  
 Na página **Resumo** do assistente, reveja as ações que serão executadas e conclua o assistente. O novo item de configuração é apresentado no nó **Itens de Configuração** da área de trabalho **Ativos e Compatibilidade**.  
