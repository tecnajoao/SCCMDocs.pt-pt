---
title: Criar itens de configuração personalizada
titleSuffix: Configuration Manager
description: Gerir as definições para servidores e computadores do Windows com um item de configuração personalizada para servidores e áreas de trabalho do Windows
ms.date: 03/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 1eb2fcaf-acac-4388-9b31-6cccafacaabe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4253fdd94985a8a9adbc9e782f8397c2f76f5f2c
ms.sourcegitcommit: 4ab85212268e76d3fd22f00e6c74edaa5abde60c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 03/05/2019
ms.locfileid: "57426894"
---
# <a name="create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-configuration-manager-client"></a>Criar itens de configuração personalizada para os computadores de secretária e servidor do Windows geridos com o cliente do Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*


Utilize o Gestor de configuração **áreas de trabalho do Windows e de servidores personalizados** item de configuração para gerir as definições para computadores Windows e servidores que são geridos pelo cliente do Configuration Manager.  



## <a name="start-the-wizard"></a>Iniciar o Assistente

1. Na consola do Configuration Manager, vá para o **ativos e compatibilidade** área de trabalho, expanda **definições de compatibilidade**e selecione o **itens de configuração** nó.  

2. Sobre o **home page** separador do Friso, no **criar** grupo, selecione **Criar Item de configuração**.  

3. Na página **Geral** do **Assistente de Criação de Item de Configuração**, especifique um nome e uma descrição opcional para o item de configuração.  

4. Em **Especifique o tipo de item de configuração que pretende criar**, selecione **Servidores e Computadores de Secretária Windows (personalizado)**.  

    > [!TIP]  
    > Se pretender fornecer as definições do método de deteção que verificam a existência de uma aplicação, selecione **Este ficheiro de configuração contém as definições da aplicação**.  

5. Para ajudar a procurar e filtrar itens de configuração na consola do Configuration Manager, selecione **categorias** para criar e atribuir categorias.  



## <a name="detection-methods"></a>Métodos de deteção  

Utilize este procedimento para fornecer informações do método de deteção para o item de configuração.  

> [!NOTE]  
> Essas informações se aplicam apenas se selecionar **este item de configuração contém as definições da aplicação** sobre o **geral** página do assistente.  

Um método de deteção no Configuration Manager contém as regras que são utilizadas para detetar se uma aplicação é instalada num computador. Esta deteção ocorre antes do cliente avalia a conformidade do item de configuração. Para detetar se uma aplicação está instalada, pode detetar a presença de um ficheiro do Windows Installer para a aplicação, utilizar um script personalizado ou selecionar **Assumir sempre que a aplicação está instalada** para avaliar o item de configuração relativamente à compatibilidade, independentemente se a aplicação está instalada.  


### <a name="to-detect-an-application-installation-by-using-the-windows-installer-file"></a>Para detetar uma instalação de aplicações através do ficheiro de instalador do Windows  

1. Na **métodos de deteção** página do **criar Assistente de Item de configuração**, selecione a opção para **detecção do instalador do Windows de utilização**.  

2. Selecione **aberto**, procure o ficheiro do Windows Installer (MSI) que pretende detetar e, em seguida, selecione **aberto**.  

3. O **versão** campo é preenchido automaticamente com o número de versão de ficheiro do Windows Installer. Se o valor apresentado estiver incorreto, introduza um novo número de versão aqui.  

4. Se pretender detetar cada perfil de utilizador no computador, selecione **esta aplicação é instalada para um ou mais utilizadores**.  


### <a name="to-detect-a-specific-application-and-deployment-type"></a>Para detetar uma aplicação e um tipo de implementação específicos  

1. Na **métodos de deteção** página do **criar Assistente de Item de configuração**, selecione para **detetar um tipo específico de aplicação e implementação**. Escolha **Selecionar**.   

2. Na caixa de diálogo **Especificar Aplicação**, selecione a aplicação e um tipo de implementação associados que pretende detetar.  


### <a name="to-detect-an-application-installation-by-using-a-custom-script"></a>Para detetar uma instalação de aplicações utilizando um script personalizado  

1. Na **métodos de deteção** página do **criar Assistente de Item de configuração**, selecione a opção para **utilizar um script personalizado para detetar esta aplicação**.  

2. Na lista, selecione o idioma do script. Escolha entre os seguintes formatos:  

    - **VBScript**  

    - **JScript**  

    - **PowerShell**  

        > [!Note]  
        > A partir da versão 1810, quando um script do Windows PowerShell é executado como um método de deteção, o cliente do Configuration Manager que chama o PowerShell com o `-NoProfile` parâmetro. Esta opção inicia PowerShell sem perfis. Um perfil de PowerShell é um script que é executada quando o PowerShell é iniciado. <!--3607762-->  

3. Selecione **aberto**, navegue para o script que pretende utilizar e, em seguida, selecione **aberto**.  



##  <a name="specify-supported-platforms"></a>Especificar plataformas suportadas  

Sobre o **plataformas suportadas** página do **criar Assistente de Item de configuração**, selecione as versões do Windows nas quais pretende que a configuração ser avaliado relativamente à compatibilidade do item ou escolha  **Selecionar tudo**. 

Também pode **especificar a versão do Windows manualmente**. Selecione **adicionar** e especifique o número de compilação de cada parte do Windows. 



##  <a name="configure-settings"></a>Configurar definições  

Utilize este procedimento para configurar as definições no item de configuração.  

As definições representam as condições empresariais ou técnicas utilizadas para avaliar a compatibilidade nos dispositivos cliente. Pode configurar uma nova definição ou navegar para uma definição existente num computador de referência.  

1. Na **definições** página do **criar Assistente de Item de configuração**, selecione **New**.  

2. No separador **Geral** da caixa de diálogo **Criar Definição**, forneça as seguintes informações:  

    - **Nome**: Introduza um nome exclusivo para a definição. Pode utilizar até 256 carateres.  

    - **Descrição**: Introduza uma descrição para a definição. Pode utilizar até 256 carateres.  

    - **Tipo de definição**: Na lista, escolha e configure um dos seguintes tipos de definição a utilizar para esta definição:  
        - [Consulta do Active Directory](#bkmk_adquery)
        - [Assemblagem](#bkmk_assembly)
        - [Sistema de ficheiros](#bkmk_file)
        - [Metabase do IIS](#bkmk_iis)
        - [Chave de registo](#bkmk_regkey)
        - [Valor de registo](#bkmk_regval)
        - [Script](#bkmk_script)
        - [Consulta SQL](#bkmk_sql)
        - [Consulta WQL](#bkmk_wql)
        - [Consulta XPath](#bkmk_xpath)

    - **Tipo de dados**: Escolha o formato no qual a condição devolve os dados antes de ser utilizada para avaliar a definição. O **tipo de dados** não é apresentada uma lista de todos os tipos de definição.  

        > [!Tip]  
        > O **flutuante** tipo de dados suporta apenas três dígitos depois da casa decimal.  

3. Configure detalhes adicionais sobre esta definição na lista **Tipo de definição**. Os itens que pode configurar variam consoante o tipo de definição que selecionou.  

4. Selecione **OK** para guardar a definição e fechar o **Criar definição** caixa de diálogo.  


### <a name="bkmk_adquery"></a> Consulta do Active Directory

- **Prefixo LDAP**: Especifique um prefixo válido para a consulta de serviços de domínio do Active Directory para avaliar a compatibilidade em computadores cliente. Para fazer uma pesquisa de catálogo global, utilize `LDAP://` ou `GC://`.  

- **Nome único (DN)**: Especifique o nome único do objeto serviços de domínio do Active Directory que é avaliado relativamente à compatibilidade em computadores cliente.  

- **Filtro de pesquisa**: Especifique um filtro LDAP opcional para refinar os resultados da consulta do Active Directory Domain Services para avaliar a compatibilidade em computadores cliente. Para devolver todos os resultados da consulta, introduza `(objectclass=*)`.  

- **Âmbito da procura**: Especifique o âmbito da procura nos serviços de domínio do Active Directory  

    - **Base**: Consulta apenas o objeto especificado  

    - **Um nível**: Esta opção não é utilizada nesta versão do Configuration Manager  

    - **Subárvore**: Consulta o objeto especificado e a respetiva subárvore completa no diretório  

- **Propriedade**: Especifique a propriedade do objeto serviços de domínio do Active Directory que é utilizada para avaliar a compatibilidade em computadores cliente.  

    Por exemplo, se pretender consultar a propriedade do Active Directory que armazena o número de vezes que um utilizador introduz incorretamente uma palavra-passe, introduza `badPwdCount` neste campo.  

- **consulta**: Apresenta a consulta construída a partir das entradas em **prefixo LDAP**, **nome único (DN)**, **filtro de pesquisa** (se especificada), e **propriedade**.  


### <a name="bkmk_assembly"></a> Assemblagem

Uma assemblagem é um fragmento de código que pode ser partilhado entre aplicações. As assemblagens podem ter a extensão de nome de ficheiro .dll ou .exe. A global assembly cache é a pasta `%SystemRoot%\Assembly` nos computadores cliente. Esta cache é onde o Windows armazena todos os assemblies compartilhados.  

- **Nome da assemblagem:** Especifica o nome do objeto de assemblagem que pretende procurar. O nome não pode ser o mesmo que outros objetos de assemblagem do mesmo tipo. Em primeiro lugar registrá-la no cache de assemblies global. O nome da assemblagem pode ter até 256 carateres.  


### <a name="bkmk_file"></a> Sistema de ficheiros

- **Tipo de**: Na lista, selecione se pretende procurar um **arquivo** ou uma **pasta**.  

- **Caminho**: Especifique o caminho da pasta ou do ficheiro especificado nos computadores cliente. Pode especificar variáveis de ambiente de sistema e o `%USERPROFILE%` variável de ambiente no caminho.  

    > [!NOTE]  
    > Se utilizar o `%USERPROFILE%` variável de ambiente no **caminho** ou **nome da pasta ou ficheiro** caixas, o cliente do Configuration Manager procura todos os perfis de utilizador no computador cliente. Esse comportamento pode resultar na mesma localização de várias instâncias do ficheiro ou pasta.  
    >   
    > Se as definições de compatibilidade não tem acesso ao caminho especificado, é gerado um erro de deteção. Além disso, se o ficheiro que está a procurar estiver atualmente em utilização, é gerado um erro de deteção.  

    > [!Tip]  
    > Selecione **procurar** para configurar a definição de valores num computador de referência.   

- **Nome de ficheiro ou pasta**: Especifique o nome do objeto de ficheiro ou pasta para procurar. Pode especificar variáveis de ambiente de sistema e o `%USERPROFILE%` variável de ambiente no nome do ficheiro ou pasta. Também pode utilizar os carateres universais `*` e `?` no nome do ficheiro.  

    > [!NOTE]  
    > Se especifica um nome de ficheiro ou pasta e utiliza carateres universais, esta combinação poderá produzir um elevado número de resultados. Pode também resultar na utilização intensiva de recursos no computador cliente e tráfego de rede elevado quando reportar os resultados para o Configuration Manager.  

- **Incluir subpastas**: Também procure em todas as subpastas do caminho especificado.  

- **Este ficheiro ou pasta está associada a uma aplicação de 64 bits**: Se estiver ativada, apenas pesquisar localizações de ficheiros de 64 bits, tais como `%ProgramFiles%` nos computadores de 64 bits. Se esta opção não está ativada, pesquise localizações de 64 bits e localizações de 32 bits, como `%ProgramFiles(x86)%`.  

    > [!NOTE]  
    > Se o mesmo ficheiro ou pasta existir em ambas as localizações no mesmo computador de 64 bits, são detetados múltiplos ficheiros pela condição global.  

    O **sistema de ficheiros** tipo de definição não suporta a especificação de um caminho UNC para uma partilha de rede na **caminho** caixa.  


### <a name="bkmk_iis"></a> Metabase do IIS

- **Caminho da metabase**: Especifique um caminho válido para a metabase do serviços de informação Internet (IIS). Por exemplo, `/LM/W3SVC/`.  

- **ID de propriedade**: Especifique a propriedade numérica da definição de metabase do IIS.  


### <a name="bkmk_regkey"></a> Chave de registo

- **Hive**: Selecione o ramo de registo que pretende procurar

    > [!Tip]  
    > Selecione **procurar** para configurar a definição de valores num computador de referência. Para procurar uma chave de registo num computador remoto, ative o **registo remoto** serviço no computador remoto.  

- **chave**: Especifique o nome de chave de registo que pretende procurar. Utilize o formato `key\subkey`.  

- **Esta chave de registo está associada uma aplicação de 64 bits**: Pesquisar chaves de registo de 64 bits, além de chaves de registo de 32 bits em clientes que executem uma versão de 64 bits do Windows.  

    > [!NOTE]  
    > Se a mesma chave de registo existir nas localizações do registo de 64 bits e de 32 bits no mesmo computador de 64 bits, a condição global deteta ambas as chaves de registo.  


### <a name="bkmk_regval"></a> Valor de registo

- **Hive**: Selecione o ramo do registo para pesquisar.  

    > [!Tip]  
    > Selecione **procurar** para configurar a definição de valores num computador de referência. Para navegar para um valor de registo num computador remoto, ativar a **registo remoto** serviço no computador remoto. Também precisa de permissões de administrador para aceder ao computador remoto.  

- **chave**: Especifique o nome de chave de registo para procurar. Utilize o formato `key\subkey`.  

- **Valor**: Especifique o valor que deve ser incluído na chave de registo especificada.  

- **Esta chave de registo está associada uma aplicação de 64 bits**: Pesquise as chaves de registo de 64 bits, além de chaves de registo de 32 bits em clientes que executem uma versão de 64 bits do Windows.  

    > [!NOTE]  
    > Se a mesma chave de registo existir nas localizações do registo de 64 bits e de 32 bits no mesmo computador de 64 bits, a condição global deteta ambas as chaves de registo.  


### <a name="bkmk_script"></a> script

O valor devolvido pelo script é utilizado para avaliar a compatibilidade da condição global. Por exemplo, quando utilizar VBScript, poderá utilizar o comando **WScript.Echo Result** para devolver o valor da variável *Result* à condição global.  

- **Script de deteção**: Selecione **Adicionar Script**e introduzir ou navegue para um script. Este script é utilizado para encontrar o valor. Pode utilizar scripts do Windows PowerShell, VBScript ou Microsoft JScript.  

- **Script de remediação (opcional)**: Selecione **Adicionar Script**e introduzir ou navegue para um script. Este script é utilizado para remediar os valores de definição em não conformidade. Pode utilizar scripts do Windows PowerShell, VBScript ou Microsoft JScript.  

- **Executar scripts ao utilizar o com sessão iniciada nas credenciais de utilizador**: Se ativar esta opção, o script é executado em computadores cliente que utilizam as credenciais do utilizador com sessão iniciada.  

> [!Note]  
> A partir da versão 1810, quando utilizar o Windows PowerShell como um script de deteção ou a remediação, o cliente do Configuration Manager que chama PowerShell com o `-NoProfile` parâmetro. Esta opção inicia PowerShell sem perfis. Um perfil de PowerShell é um script que é executada quando o PowerShell é iniciado. <!--3607762-->  


### <a name="bkmk_sql"></a> Consulta SQL

- **Instância do SQL Server**: Escolha se pretende que a consulta SQL seja executada na instância predefinida, todas as instâncias ou um nome de instância de base de dados especificada.  

    > [!NOTE]  
    > O nome da instância deve referir-se a uma instância local do SQL Server. Para fazer referência a uma instância do SQL Server em cluster, deverá utilizar uma definição de script.  

- **Base de dados**: Especifique o nome da base de dados Microsoft SQL Server relativamente à qual pretende executar a consulta SQL.  

- **Coluna**: Especifique o nome da coluna devolvido pela instrução Transact-SQL que é utilizada para avaliar a compatibilidade da condição global.  

- **Instrução Transact-SQL**: Especifique a consulta SQL completa que pretende utilizar para a condição global. Para utilizar uma consulta SQL existente, selecione **aberto**.  

    > [!IMPORTANT]  
    > Definições da consulta de SQL não suportam os comandos SQL que modificam a base de dados. Apenas pode utilizar comandos SQL que leem as informações da base de dados.  


### <a name="bkmk_wql"></a> Consulta WQL

- **Namespace**: Especifique o espaço de nomes WMI que é avaliado relativamente à compatibilidade em computadores cliente. O valor predefinido é `root\cimv2`.  

- **classe**: Especifique o destino de classe do WMI no espaço de nomes acima.  

- **Propriedade**: Especifique o destino propriedade WMI na classe acima.  

- **Cláusula WHERE da consulta WQL**: Especifica uma cláusula Qualificável para reduzir os resultados. Por exemplo, para consultar apenas o serviço DHCP na classe Win32_Service, a cláusula WHERE pode ser `Name = 'DHCP' and StartMode = 'Auto'`.   


### <a name="bkmk_xpath"></a> Consulta XPath

- **Caminho**: Especifique o caminho do ficheiro. XML em computadores cliente que é utilizado para avaliar a compatibilidade. O Configuration Manager suporta a utilização de todas as variáveis de ambiente de sistema do Windows e o `%USERPROFILE%` variável de utilizador no nome do caminho.  

- **Nome do ficheiro XML**: Especifique o nome de ficheiro que contém a consulta XML no caminho acima.  

- **Incluir subpastas**: Ative esta opção Procurar todas as subpastas do caminho especificado.  

- **Este ficheiro está associado uma aplicação de 64 bits**: Procurar a localização do ficheiro de sistema de 64 bits `%Windir%\System32` , além da localização do ficheiro de sistema de 32 bits `%Windir%\Syswow64` nos clientes do Configuration Manager que executem uma versão de 64 bits do Windows.  

- **Consulta XPath**: Especifique uma consulta linguagem XPath completa válida.  

- **Namespaces**: Identifique os espaços de nomes e prefixos a utilizar durante a consulta XPath.  

Se tentou detetar um ficheiro. XML encriptado, as definições de compatibilidade encontrar o ficheiro, mas a consulta XPath não produz resultados. O cliente do Configuration Manager não gera um erro.  

Se a consulta XPath não é válida, a definição é avaliada como não compatível em computadores cliente.  



##  <a name="configure-compliance-rules"></a>Configurar regras de compatibilidade  

As regras de compatibilidade especificam as condições que definem a compatibilidade de um item de configuração. Antes de poder ser avaliada a compatibilidade de uma definição, tem de ter, pelo menos, uma regra de compatibilidade. O WMI, o registo e as definições de script permitem remediar os valores considerados não compatíveis. Pode criar novas regras ou navegar para uma definição existente em qualquer item de configuração para selecionar regras no mesmo.  


### <a name="to-create-a-compliance-rule"></a>Para criar uma regra de compatibilidade  

1. Na **regras de conformidade** página do **criar Assistente de Item de configuração**, selecione **New**.  

2. Na caixa de diálogo **Criar Regra**, forneça as seguintes informações:  

    - **Nome**: Introduza um nome para a regra de compatibilidade.  

    - **Descrição**: Introduza uma descrição para a regra de compatibilidade.  

    - **Definição selecionada**: Selecione **navegue** para abrir o **selecionar definição** caixa de diálogo. Selecione a definição que pretende definir uma regra ou selecione **nova definição**. Quando tiver terminado, escolha **selecione**.  

        > [!Tip]  
        > Para ver informações sobre a definição atualmente selecionada, selecione **propriedades**.  

    - **Tipo de regra**: Selecione o tipo de regra de compatibilidade que pretende utilizar:  

        - **Valor**: Crie uma regra que compara o valor devolvido pelo item de configuração em relação a um valor que especificar. Para obter mais informações sobre as definições adicionais, consulte [valor regras](#bkmk_value).  

        - **Existencial**: Crie uma regra que avalie a definição consoante se existe num dispositivo cliente ou o número de vezes que pode ser encontrada. Para obter mais informações sobre as definições adicionais, consulte [regras Existencial](#bkmk_exist).  

3. Selecione **OK** para fechar a **criar regra** caixa de diálogo.  




### <a name="bkmk_value"></a> Regras de valor  

- **Propriedade**: A propriedade do objeto a verificar varia consoante a definição selecionada. As propriedades disponíveis variam consoante o tipo de definição. 

- **A definição deve estar em conformidade com o seguinte...** : As permissões ou regras disponíveis variam consoante o tipo de definição.

- **Remediar regras incompatíveis quando suportado**: Selecione esta opção para o Configuration Manager retifique automaticamente as regras não conformes. O Configuration Manager suporta esta ação com os seguintes tipos de regra:  

    - **Valor de registo**: Se não for compatível, o cliente define o valor de registo. Se não existir, o cliente cria o valor.  

    - **script**: O cliente utiliza o script de remediação que especificou com a definição.  

    - **Consulta WQL**  

    > [!IMPORTANT]  
    > Só pode remediar regras incompatíveis quando o operador de regra estiver definido como **É igual a**.  

- **Reportar incompatibilidade se a instância desta definição não for encontrada**: Se esta definição não for encontrada nos computadores cliente, ative esta opção para o item de configuração comunicar não conformidade.  

- **Gravidade de incompatibilidade para relatórios**: Especifique o nível de gravidade reportado nos relatórios do Configuration Manager se esta regra de compatibilidade falhar. Os seguintes níveis de gravidade estão disponíveis:  
    - **Nenhum**  
    - **Informações**  
    - **Aviso**  
    - **Crítico**  
    - **Crítico com evento**: Computadores que não obedeçam a esta regra de compatibilidade reportam uma gravidade de falha **crítico**. Este nível de gravidade é também registado como um evento do Windows no registo de eventos de aplicações.  


### <a name="bkmk_exist"></a> Existencial regras 

> [!NOTE]  
> As opções apresentadas podem variar consoante o tipo de definição que estiver a configurar uma regra.  

- **A definição deve existir nos dispositivos cliente**  

- **A definição não deve existir nos dispositivos cliente**  

- **A definição ocorre o seguinte número de vezes:**  

- **Gravidade de incompatibilidade para relatórios**: Especifique o nível de gravidade reportado nos relatórios do Configuration Manager se esta regra de compatibilidade falhar. Os seguintes níveis de gravidade estão disponíveis:  
    - **Nenhum**  
    - **Informações**  
    - **Aviso**  
    - **Crítico**  
    - **Crítico com evento**: Computadores que não obedeçam a esta regra de compatibilidade reportam uma gravidade de falha **crítico**. Este nível de gravidade é também registado como um evento do Windows no registo de eventos de aplicações.  



## <a name="next-steps"></a>Passos seguintes

[Criar linhas de base de configuração](/sccm/compliance/deploy-use/create-configuration-baselines)
