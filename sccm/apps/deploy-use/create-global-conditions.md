---
title: Criar condições globais
titleSuffix: Configuration Manager
description: Crie condições globais para especificar como uma aplicação é fornecida e implementada em dispositivos cliente.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2d5f871a-19dc-4bd3-a3ad-4230c7a69f1b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: dac47f55a1ad0d287e789d555d2f0a93b40f9376
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-create-global-conditions-in-system-center-configuration-manager"></a>Como criar condições globais no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

No System Center Configuration Manager, as condições globais são regras que representam condições comerciais ou técnicas que pode utilizar para especificar como uma aplicação é fornecida e implementada em dispositivos cliente. O acesso às condições globais é efetuado na página **Requisitos** do Assistente para Criar Tipo de Implementação.  

> [!NOTE]  
>  Pode editar condições globais apenas a partir do site onde foram criados.  

 Utilize os procedimentos seguintes para criar condições globais do Configuration Manager.  

## <a name="provide-basic-information-about-the-global-condition"></a>Fornecer informações básicas sobre a condição global  
 Existem vários tipos diferentes de condições globais. Aos diferentes tipos de condições globais estão associadas opções diferentes. Quando seleciona um tipo de condição global específico, o Configuration Manager mostra as opções que se aplicam à seleção.  

1.  Na consola do Configuration Manager, escolha **biblioteca de Software** > **gestão de aplicações** > **condições globais**.  

3.  No **home page** separador o **criar** grupo, escolha **criar condição Global**.  

4.  Na caixa de diálogo **Criar Condição Global** , forneça um nome e uma descrição opcional para a condição global.  

5.  No **tipo de dispositivo** pendente lista, escolha se a condição global é de um **Windows** computador ou um **Windows Mobile** dispositivo.  

6.  Na lista pendente **Tipo de Condição** , escolha uma das seguintes opções:  

    -   **Definição** – esta opção verifica a existência de um ou mais itens em dispositivos cliente. Por exemplo, pode verificar se um valor de chave de ficheiro, pasta ou de registo existe num dispositivo cliente.  

    -   **Expressão** – esta opção permite-lhe configurar regras mais complexas para verificar se a condição é satisfeita em dispositivos cliente. Por exemplo, pode verificar se a memória física de um computador é entre 2 GB e 4 GB ou se um dispositivo móvel utiliza introdução por ecrã tátil.  

## <a name="set-up-rules-for-the-global-condition"></a>Configurar regras para a condição global  
 O procedimento para definir as regras da condição global é diferente consoante esteja a configurar uma definição ou uma expressão. Utilize o procedimento aplicável aqui para configurar uma definição ou uma expressão para a condição global.  

### <a name="to-set-up-a-setting-for-the-global-condition"></a>Para configurar uma definição para a condição global  

1.  Na lista pendente **Tipo de Condição** , escolha **Definição**.  

2.  Na lista pendente **Tipo de definição** , escolha o item a utilizar como a condição para a qual os requisitos serão verificados. Estão disponíveis os seguintes tipos de definição e configurações.  

    -   **Consulta do Active Directory**  

        -   **Prefixo LDAP** - especifique um prefixo LDAP válido para a consulta dos Serviços de Domínio do Active Directory para avaliar a compatibilidade em computadores cliente. Pode utilizar **LDAP://** ou **GC://**.  

        -   **Nome único (DN)** -especifique o nome único do objeto serviços de domínio do Active Directory que será avaliada relativamente à compatibilidade em computadores cliente.  

        -   **Filtro de procura** - especifique um filtro de LDAP opcional para refinar os resultados da consulta dos Serviços de Domínio do Active Directory para avaliar a compatibilidade em computadores cliente.  

        -   **Âmbito da procura** - especifique o âmbito da procura nos Serviços de Domínio do Active Directory:  

            -   **Base** -consulta apenas o objeto especificado.  

            -   **Um nível** -esta opção não está a ser utilizada nesta versão do Configuration Manager.  

            -   **Subárvore** -consulta o objeto especificado e a respetiva subárvore completa no diretório.  

        -   **Propriedade** - especifique a propriedade do objeto dos Serviços de Domínio do Active Directory que será utilizada para avaliar a compatibilidade em computadores cliente.  

        -   **Consulta** -mostra a consulta LDAP construída a partir das entradas em **prefixo LDAP**, **nome único (DN)**, **filtro de pesquisa** se for especificado e  **Propriedade**. Esta consulta será utilizada para avaliar a compatibilidade em computadores cliente.  

    -   **Assemblagem**  

        -   **Nome da assemblagem** - Especifica o nome do objeto de assemblagem a procurar. O nome não pode ser o mesmo que qualquer outro objeto de assemblagem do mesmo tipo e o nome tem de estar registado na Global Assembly Cache. O nome da assemblagem pode ter um máximo de 256 carateres.  

        > [!NOTE]  
        >  Uma assemblagem é um fragmento de código que pode ser partilhado entre aplicações. As assemblagens podem ter a extensão de nome de ficheiro. dll ou .exe. A Global Assembly Cache é uma pasta denominada *%systemroot%\assembly* em computadores cliente em que todas as assemblagens partilhadas são armazenados.  

    -   **Sistema de ficheiros**  

        -   **Tipo** – na lista pendente, escolha se pretende procurar um **ficheiro** ou um **pasta**.  

        -   **Caminho** – especifique o caminho da pasta ou do ficheiro especificado nos computadores cliente. Pode especificar variáveis de ambiente do sistema e a variável de ambiente *%USERPROFILE%* no caminho.  

            > [!NOTE]  
            >  Se utilizar a variável de ambiente *%USERPROFILE%* no campo **Caminho** ou **Nome da pasta ou ficheiro** , a procura será efetuada em todos os perfis de utilizador do computador cliente. Isto pode resultar na deteção de várias instâncias do ficheiro ou pasta.  

        -   **Nome da pasta ou ficheiro** – especifique o nome do objeto de ficheiro ou de pasta que será procurado. Pode especificar variáveis de ambiente do sistema e a variável de ambiente *%USERPROFILE%* no nome da pasta ou ficheiro. Também pode utilizar o * e? carateres universais no nome do ficheiro.  

            > [!NOTE]  
            >  Se especificar um nome de ficheiro ou de pasta e utilizar carateres universais, isto poderá produzir um elevado número de resultados. Isto pode resultar numa utilização intensiva de recursos no computador cliente e tráfego de rede elevado ao reportar os resultados para o Configuration Manager.  

        -   **Incluir subpastas** – ative esta opção se também pretender procurar em todas as subpastas do caminho especificado.  

        -   **Este ficheiro ou pasta está associada a uma aplicação de 64 bits** -escolher se o sistema de 64 bits localização de ficheiros (*% windir %* \system32) deve ser pesquisada, além da localização do ficheiro de sistema de 32 bits (*% windir %* \syswow64) em clientes do Configuration Manager com uma versão de 64 bits do Windows.  

            > [!NOTE]  
            >  Se o mesmo ficheiro ou pasta existir em ambas as localizações no mesmo computador de 64 bits, serão detetados múltiplos ficheiros pela condição global.  

         O tipo de definição **Sistema de ficheiros** não suporta a especificação de um caminho UNC de partilha de rede no campo **Caminho** .  

    -   **Metabase do IIS**  

        -   **Caminho da metabase** - especifique um caminho válido para a Metabase do IIS.  

        -   **ID da Propriedade** - especifique a propriedade numérica da definição da Metabase do IIS.  

    -   **Chave de registo**  

        -   **Ramo de registo** – na lista pendente, selecione o ramo de registo que pretende procurar.  

        -   **Chave** – especifique o nome da chave de registo que pretende procurar. O formato utilizado deve ser *chave\subchave*.  

        -   **Esta chave de registo está associada a uma aplicação de 64 bits** – especifica se a procura deve ser efetuada nas chaves de registo de 64 bits, além das chaves de registo de 32 bits, em clientes com uma versão de 64 bits do Windows.  

            > [!NOTE]  
            >  Se a mesma chave de registo existir nas localizações do registo de 64 bits e de 32 bits no mesmo computador de 64 bits, a condição global detetará ambas as chaves de registo.  

    -   **Valor de registo**  

        -   **Ramo** – na lista pendente, selecione o ramo do registo em que pretende procurar.  

        -   **Chave** – especifique o nome da chave de registo que pretende procurar. O formato utilizado deve ser *chave\subchave*.  

        -   **Valor** – especifique o valor que deve estar incluído na chave de registo especificada.  

        -   **Esta chave de registo está associada a uma aplicação de 64 bits** – especifica se a procura deve ser efetuada nas chaves de registo de 64 bits, além das chaves de registo de 32 bits, em clientes com uma versão de 64 bits do Windows.  

            > [!NOTE]  
            >  Se a mesma chave de registo existir nas localizações do registo de 64 bits e de 32 bits no mesmo computador de 64 bits, a condição global detetará ambas as chaves de registo.  

    -   **Script**  

        -   **Script de deteção** – escolha **adicionar** para introduzir ou navegue para o script a utilizar. Pode utilizar scripts do Windows PowerShell, VBScript ou JScript.  

        -   **Executar scripts ao utilizar o iniciada em credenciais de utilizador** – se ativar esta opção, o script será executado nos computadores cliente utilizando as credenciais do utilizador que tenha sessão iniciada.  

            > [!NOTE]  
            >  O valor devolvido pelo script será utilizado para avaliar a compatibilidade da condição global. Por exemplo, quando utilizar VBScript, poderá utilizar o **WScript resultado** comando para devolver o valor da variável resultado à condição global.  
            >   
            >  Se o script devolver vários valores, estes valores devem estar numa única linha e separadas por ponto e vírgula. Se cada valor estiver numa linha separada, a avaliação irá falhar.  

    -   **Consulta SQL**  

        -   **Instância do SQL Server** – escolha se pretende que a consulta SQL seja executada na instância predefinida, em todas as instâncias ou na instância de base de dados com o nome especificado.  

            > [!NOTE]  
            >  O nome da instância deve referir-se a uma instância local do SQL Server. Para fazer referência a uma instância do SQL Server em cluster, deverá utilizar uma definição de script.  

        -   **Base de dados** – especifique o nome da base de dados do Microsoft SQL Server relativamente à qual será executada a consulta SQL.  

        -   **Coluna** – especifique o nome da coluna devolvido pela instrução Transact-SQL a utilizar para avaliar a compatibilidade da condição global.  

        -   **Instrução Transact-SQL** – especifique a consulta SQL completa a utilizar para a condição global. Também pode optar por **abrir** para abrir uma consulta SQL existente.  

    -   **Consulta WQL**  

        -   **Espaço de nomes** - especifique o espaço de nomes WMI que será utilizado para criar uma consulta WQL que será avaliada relativamente à compatibilidade em computadores cliente. O valor predefinido é Root\cimv2.  

        -   **Classe** - especifica a classe WMI que será utilizada para criar uma consulta WQL que será avaliada relativamente à compatibilidade em computadores cliente.  

        -   **Propriedade** - especifica a propriedade WMI que será utilizada para criar uma consulta WQL que será avaliada relativamente à compatibilidade em computadores cliente.  

        -   **Cláusula WHERE da consulta WQL** - pode utilizar o item **Cláusula WHERE da consulta WQL** para especificar uma cláusula WHERE a aplicar ao espaço de nomes, à classe e à propriedade especificados nos computadores cliente.  

    -   **Consulta XPath**  

        -   **Caminho** - especifique o caminho para o ficheiro XML em computadores cliente que serão utilizados para avaliar a compatibilidade. O Configuration Manager suporta a utilização de todas as variáveis de ambiente de sistema do Windows e o *% USERPROFILE %* variável de utilizador no nome do caminho.  

        -   **Nome do ficheiro XML** -especifique o nome de ficheiro que contém a consulta XML a utilizar para avaliar a compatibilidade em computadores cliente.  

        -   **Incluir subpastas** - ative esta opção se também pretender procurar em todas as subpastas do caminho especificado.  

        -   **Este ficheiro está associado uma aplicação de 64 bits** -escolher se o sistema de 64 bits localização de ficheiros (*% windir %* \system32) deve ser pesquisada, além da localização do ficheiro de sistema de 32 bits (*% windir %* \syswow64) em clientes do Configuration Manager com uma versão de 64 bits do Windows.  

        -   **Consulta XPath** - especifique uma consulta da linguagem XPath completa e válida a utilizar para avaliar a compatibilidade em computadores cliente.  

        -   **Espaços de Nomes** - abre a caixa de diálogo **Espaços de Nomes XML** para identificar espaços de nomes e prefixos a utilizar durante a consulta XPath.  

3.  Na lista pendente **Tipo de dados** , escolha o formato em que os dados serão devolvidos pela condição, antes da sua utilização para verificar os requisitos.  

    > [!NOTE]  
    >  O **tipo de dados** na lista pendente não é apresentada para todos os tipos de definição.  

4.  Configurar detalhes adicionais sobre esta definição abaixo o **tipo de definição** na lista pendente. Os itens que pode configurar irão variar consoante o tipo de definição selecionado.  

5.  Escolha **OK** para guardar a regra e fechar o **criar condição Global** caixa de diálogo.  

### <a name="set-up-an-expression-for-the-global-condition"></a>Configurar uma expressão para a condição global  

1.  Na lista pendente **Tipo de Condição** , escolha **Expressão**.  

2.  Escolha **Adicionar cláusula** para abrir o **Adicionar cláusula** caixa de diálogo.  

3.  Na lista pendente **Selecionar categoria** , selecione se esta expressão se destina a um dispositivo ou um utilizador. Em alternativa, selecione **Personalizado** para utilizar uma condição global configurada anteriormente.  

4.  Na lista pendente **Selecione uma condição** , selecione a condição a utilizar para avaliar se o utilizador ou o dispositivo satisfaz os requisitos da regra. O conteúdo desta lista varia consoante a categoria selecionada.  

5.  Na lista pendente **Selecione operador** , escolha o operador que será utilizado para comparar a condição selecionada com o valor especificado para avaliar se o utilizador ou o dispositivo satisfaz os requisitos da regra. Os operadores disponíveis variam consoante a condição selecionada.  

6.  No campo **Valor** , especifique os valores que serão utilizados com a condição e o operador selecionados para avaliar se o utilizador ou o dispositivo satisfaz os requisitos da regra. Os valores disponíveis variam consoante a condição selecionada e o operador selecionado.  

7.  Escolha **OK** para guardar a expressão e fechar o **Adicionar cláusula** caixa de diálogo.  

8.  Quando acabar de adicionar cláusulas à condição global, escolha **OK** para fechar o **criar condição Global** caixa de diálogo e guardar a condição global.  
