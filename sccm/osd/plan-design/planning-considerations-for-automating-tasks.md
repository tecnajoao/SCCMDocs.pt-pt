---
title: "Considerações sobre planeamento para automatizar tarefas"
titleSuffix: Configuration Manager
description: Planear antes de automatizar tarefas no System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fc497a8a-3c54-4529-8403-6f6171a21c64
caps.latest.revision: "13"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: cfd3e33006f05b4270266b3c8b316764d29cdb0d
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="planning-considerations-for-automating-tasks-in-system-center-configuration-manager"></a>Considerações sobre planeamento para automatizar tarefas no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Pode criar sequências de tarefas para automatizar tarefas no seu ambiente do System Center Configuration Manager. Estas tarefas abrangem desde a captura de um sistema operativo num computador de referência até à implementação do sistema operativo num ou mais computadores de destino. As ações da sequência de tarefas são definidas nos passos individuais da sequência. Quando a sequência de tarefas é executada, as ações de cada passo são efetuadas ao nível da linha de comandos no contexto Sistema Local, sem necessidade de intervenção do utilizador. Utilize as secções seguintes para ajudar a planear automatizar tarefas no Configuration Manager.

##  <a name="BKMK_TSStepsActions"></a>Passos de sequência de tarefas e ações  
 Passos são os componentes básicos de uma sequência de tarefas. Podem conter comandos que configurem e capturem o sistema operativo num computador de referência ou conter comandos que instalem o sistema operativo, controladores, o cliente do Configuration Manager e o software no computador de destino. Os comandos de um passo de sequência de tarefas são definidos pelas ações do passo. Existem dois tipos de ações: As ações definidas utilizando uma cadeia de linha de comandos são referidas como ações personalizadas. Uma ação que está predefinida pelo Configuration Manager é referida como ações incorporadas. Uma sequência de tarefas pode executar qualquer combinação de ações personalizadas e incorporadas.  

 Passos de sequência de tarefas também poderão incluir condições que controlam o comportamento, tais como parar a sequência de tarefas ou continuar a sequência de tarefas, se ocorrer um erro. A inclusão de uma variável de sequência de tarefas no passo permite adicionar condições ao passo. Por exemplo, poderá utilizar a variável **SMSTSLastActionRetCode** para testar a condição do passo anterior. As variáveis podem ser adicionadas a um único passo ou um grupo de passos.  

 Passos de sequência de tarefas são processados sequencialmente, que inclui a ação do passo e quaisquer condições que estão atribuídas ao passo. Quando o Configuration Manager começa a processar um passo de sequência de tarefas, o passo seguinte não está iniciado até que a ação anterior tenha sido concluída. Uma sequência de tarefas é considerada concluída quando todos os seus passos foram concluídos ou quando uma falha de um passo faz com que o Configuration Manager para interromper a execução da sequência de tarefas antes de todos os passos são concluídos. Por exemplo, se o passo da sequência de tarefas não é possível localizar uma imagem ou pacote referenciados num ponto de distribuição, a sequência de tarefas contém uma referência quebrada e o Configuration Manager deixa de executar a sequência de tarefas nesse momento, a menos que o passo falhado possua uma condição para continuar quando ocorre um erro.  

> [!IMPORTANT]  
>  Por predefinição, uma sequência de tarefas falhará se falhar um passo ou ação. Se pretender que a sequência de tarefas continue mesmo quando um passo falhar, edite a sequência de tarefas, clique no separador **Opções** e, em seguida, selecione **Continuar com o erro**.  

 Para obter mais informações sobre os passos que podem ser adicionados a uma sequência de tarefas, consulte [passos de sequência de tarefas](../understand/task-sequence-steps.md).  

##  <a name="BKMK_TSGroups"></a> Grupos de sequências de tarefas  
 **Grupos** são conjuntos de passos numa sequência de tarefas. Um grupo de sequência de tarefas consiste num nome, descrição opcional e eventuais condições opcionais, avaliados como uma unidade antes de a sequência de tarefas prosseguir para o passo seguinte. Os grupos podem ser aninhados uns nos outros, e um grupo poderá conter uma mistura de passos e subgrupos. Os grupos são úteis para combinar diversos passos que partilhem uma condição comum.  

> [!IMPORTANT]  
>  Por predefinição, um grupo de sequência de tarefas falhará se falhar qualquer passo ou grupo incorporado no grupo. Se pretender que a sequência de tarefas continue após a falha de um passo ou grupo incorporado, edite a sequência de tarefas, clique no separador **Opções** e, em seguida, selecione **Continuar com o erro**.  

 A tabela seguinte mostra como as **continuar com o erro** opção funciona ao agrupar passos.  

 Neste exemplo, existem dois grupos de sequências de tarefas que contêm três passos de sequência tarefas cada.  

|Grupo ou passo de sequência de tarefas|Definição Continuar com o erro|  
|---------------------------------|-------------------------------|  
|**Grupo de Sequência de Tarefas 1**|**Continuar com o erro** selecionado.|  
|Sequência de Tarefas Passo 1|**Continuar com o erro** selecionado.|  
|Passo 2 da Sequência de Tarefas|Não definido.|  
|Passo 3 da Sequência de Tarefas|Não definido.|  
|**Grupo 2 da Sequência de Tarefas**|Não definido.|  
|Passo 4 da Sequência de Tarefas|Não definido.|  
|Passo 5 da Sequência de Tarefas|Não definido.|  
|Passo 6 da Sequência de Tarefas|Não definido.|  

-   Se o passo de sequência de tarefas 1 falhar, a sequência de tarefas continua com o passo de sequência de tarefas 2.  

-   Se o passo de sequência de tarefas 2 falhar, a sequência de tarefas não é executado o passo de sequência de tarefas 3, mas continua a executar os passos de sequência de tarefas 4 e 5, que estão num grupo de sequência de tarefas diferente.  

-   Se o passo de sequência de tarefas 4 falha, não existem mais passos são executados e a sequência de tarefas falhará, porque o **continuar com o erro** definição não foi configurada para o grupo de sequência de tarefas 2.  

 Tem de atribuir um nome de grupos de sequências de tarefas, embora o nome do grupo não tem de ser exclusivo. Também poderá fornecer uma descrição opcional para o grupo de sequência de tarefas.  

##  <a name="BKMK_TSVariables"></a> Variáveis de sequência de tarefas  
 Variáveis de sequência de tarefas são um conjunto de pares nome / valor que fornecem definições de implementação de configuração e o sistema operativo para o computador, o sistema operativo e o utilizador tarefas de configuração de estado num computador cliente do Configuration Manager. As variáveis de sequência de tarefas fornecem um mecanismo de configuração e personalização dos passos de uma sequência de tarefas.  

 Quando executa uma sequência de tarefas, muitas das respetivas definições são armazenadas como variáveis de ambiente. Pode aceder ou alterar os valores das variáveis de sequência de tarefas incorporadas e pode criar a nova tarefa de variáveis de sequência para personalizar a forma como uma sequência de tarefas é executada num computador de destino.  

 Pode utilizar variáveis de sequência de tarefas no ambiente de sequência de tarefas para executar as seguintes ações:  

-   Configurar definições para uma ação de sequência de tarefas  

-   Fornecer argumentos de linha de comandos para um passo de sequência de tarefas  

-   Avaliar uma condição que determina se um grupo ou passo de sequência de tarefas é executado  

-   Fornecer valores para scripts personalizados utilizados numa sequência de tarefas  

 Por exemplo, poderá ter uma sequência de tarefas que inclua um **associar domínio ou grupo de trabalho** passo de sequência de tarefas. A sequência de tarefas poderá ser implementada para diversas coleções, em que a associação à coleção é determinada pela associação ao domínio. Nesse caso, pode especificar uma variável de sequência de tarefas por coleção para o nome de domínio de cada coleção e, em seguida, utilizar essa variável de sequência de tarefas para fornecer o nome de domínio apropriado na sequência de tarefas.  

###  <a name="BKMK_TSCreateVariables"></a> Criar variáveis de sequência de tarefas  
 Pode adicionar novas variáveis de sequência de tarefas para personalizar e controlar os passos numa sequência de tarefas. Por exemplo, poderá criar uma variável de sequência de tarefas para substituir uma definição de um passo incorporado de sequência de tarefas. Também poderá criar uma variável personalizada de sequência de tarefas para utilizar com condições, linhas de comandos ou passos personalizados na sequência de tarefas. Ao criar uma variável de sequência de tarefas, a variável e o valor associado serão mantidos no ambiente de sequência de tarefas, mesmo se a sequência reiniciar o computador de destino. A variável e o respetivo valor podem ser utilizados na sequência de tarefas em diversos ambientes de sistema operativo. Por exemplo, pode ser utilizado no sistema operativo Windows completo e no ambiente Windows PE.  

 A tabela seguinte descreve os métodos para criar uma informações de utilização adicionais e variável de sequência de tarefas.  

|Método de criação|Utilização|  
|-------------------|-----------|  
|Definir campos em passos de sequência de tarefas utilizando o Editor de Sequência de Tarefas|Especifica os valores predefinidos do passo de sequência de tarefas. A variável e o valor só estarão acessíveis quando o passo for executado na sequência de tarefas. Não fazem parte do ambiente geral da sequência e que não estejam acessíveis por outros passos de sequência de tarefas na sequência de tarefas.<br /><br /> Para obter uma lista de variáveis incorporadas e respetivas ações associadas, consulte [variáveis de ação da sequência de tarefas](../understand/task-sequence-action-variables.md).|  
|Adicionar um passo de definição de variável de sequência de tarefas a uma sequência de tarefas|Especifica a variável e o valor de sequência de tarefas no ambiente de sequência de tarefas quando o passo de sequência de tarefas é executado como parte de uma sequência de tarefas. Todos os passos de sequência de tarefas subsequentes poderão aceder à variável de ambiente e ao respetivo valor.|  
|Definir uma variável por coleção|Especifica variáveis e valores de sequência de tarefas para uma coleção de computadores. Todas as sequências de tarefas direcionadas para a coleção poderão aceder às variáveis de sequência de tarefas e aos respetivos valores.|  
|Definir uma variável por computador|Especifica variáveis e valores de sequência de tarefas para um computador específico. Todas as sequências de tarefas direcionadas para o computador poderão aceder às variáveis de sequência de tarefas e aos respetivos valores.|  
|Adicionar uma variável de sequência de tarefas na página **Personalização** do Assistente de Criação de Suporte de Dados da Sequência de Tarefas|Especifica variáveis e valores de sequência de tarefas para a sequência de tarefas que é executada a partir do suporte de dados que consegue aceder à variável de sequência de tarefas e ao respetivo valor.|  

 Para substituir o valor predefinido de uma variável incorporada de sequência de tarefas, terá de definir uma variável de sequência de tarefas com o mesmo nome que a variável incorporada de sequência de tarefas. Para obter uma lista de variáveis de sequência de tarefas incorporadas com as ações associadas e utilização, consulte [variáveis incorporadas de sequência de tarefas](../understand/task-sequence-built-in-variables.md).  

 Pode eliminar uma variável de sequência de tarefas do ambiente de sequência de tarefas utilizando os mesmos métodos de como criar uma variável de sequência de tarefas. Neste caso, para eliminar uma variável do ambiente de sequência de tarefas, defina o valor de variável de sequência de tarefas para uma cadeia vazia.  

 Pode combinar diversos métodos para definir uma variável de sequência de tarefas do ambiente para valores diferentes para a mesma sequência. Num cenário avançado, poderá definir os valores predefinidos dos passos de uma sequência utilizando o Editor de Sequência de Tarefas e, em seguida, definir um valor personalizado para a variável utilizando os diversos métodos de criação. A lista seguinte descreve as regras que determinam que valor é utilizado quando uma variável de sequência de tarefas é criada utilizando mais de um método.  

1.  O **Set Task Sequence Variable** passo substitui todos os outros métodos de criação.  

2.  As variáveis por computador têm precedência sobre variáveis por coleção. Se especificar o mesmo nome sequência de tarefas variável para uma variável por computador e uma variável por coleção, o valor da variável por computador é utilizado quando o computador de destino executa a sequência de tarefas implementada.  

3.  Sequências de tarefas podem ser executadas a partir do suporte de dados. Utilize as variáveis de suporte de dados em vez de variáveis por coleção ou por computador. Se a sequência de tarefas for executada a partir de suportes de dados, as variáveis por computador e por coleção não se aplicarão, não sendo utilizadas. Em vez disso, as variáveis de sequência definidas de tarefas a **personalização** página do Assistente de suporte de dados de sequência de tarefas são utilizadas para definir valores específicos para uma sequência de tarefas executada a partir do suporte de dados  

4.  Se um valor de variável de sequência de tarefas não está definido no ambiente de sequência geral, as ações incorporadas utilizam o valor predefinido para o passo, conforme definido no Editor de sequência de tarefas.  

 Além de substituir os valores para definições de passo de sequência de tarefas incorporadas, também pode criar uma nova variável de ambiente para utilização num passo de sequência de tarefas, script, linha de comandos ou condição. Quando especificar um nome para uma nova variável de sequência de tarefas, siga estas diretrizes:  

-   O nome variável da sequência de tarefas que especificar pode conter letras, números, caráter de sublinhado (_) e um hífen (-).  

-   Nomes de variáveis de sequência de tarefas têm um comprimento mínimo de 1 caráter e um comprimento máximo de 256 carateres.  

-   Variáveis definidas pelo utilizador têm de começar com uma letra (A-Z ou a-z).  

-   Os nomes de variáveis definidas pelo utilizador não podem começar pelo caráter de sublinhado. Apenas variáveis de sequência de tarefas só de leitura são precedidas pelo caráter de sublinhado  

    > [!NOTE]  
    >  As variáveis de sequência de tarefas só de leitura podem ser lidos pelos passos de sequência de tarefas numa sequência de tarefas mas não podem ser definidas. Por exemplo, pode utilizar uma variável de sequência de tarefas só de leitura como parte da linha de comandos para um **executar linha de comandos** variável de ação de sequência de tarefas, mas não é possível definir uma variável só de leitura utilizando a **definir variável da sequência de tarefas** variável de ação.  

-   Nomes de variáveis de sequência de tarefas não são sensíveis a maiúsculas e minúsculas. Por exemplo, OSDVAR e osdvar representam a mesma variável de sequência de tarefas.  

-   Nomes de variáveis de sequência de tarefas não podem começar ou terminar com um espaço nem conter espaços incorporados. Os espaços no início ou fim de um nome de variável de sequência de tarefas são ignorados.  

 A tabela seguinte apresenta exemplos de variáveis de sequência de tarefa especificado de um utilizador válido e não válido.  

|Exemplos de nomes válidos de variáveis especificadas pelo utilizador|Exemplos de nomes não válidos de variáveis especificadas pelo utilizador|  
|-------------------------------------------------------|----------------------------------------------------------|  
|MyVariable|1Variable<br /><br /> As variáveis de sequência de tarefas especificadas de utilizador não podem começar com um número.|  
|My_Variable|MyV@riable<br /><br /> As variáveis de sequência de tarefas especificadas de utilizador não podem conter o símbolo @.|  
|My_Variable_2|_MyVariable<br /><br /> As variáveis de sequência de tarefas especificadas de utilizador não podem começar com um caráter de sublinhado.|  

 Limitações genéricas para variáveis de sequência de tarefas:  

-   Valores de variáveis de sequência de tarefas não podem exceder 4.000 carateres.  

-   Não é possível criar ou substituir uma variável de sequência de tarefas só de leitura. As variáveis só de leitura são designadas por nomes que começam com um caráter de sublinhado (_). Pode aceder ao valor das variáveis de sequência de tarefas só de leitura na sua sequência de tarefas; no entanto, é impossível alterar os respetivos valores associados.  

-   Os valores das variáveis de sequência de tarefas podem ser sensíveis a maiúsculas e minúsculas consoante a utilização do valor. Na maioria dos casos, os valores das variáveis de sequência de tarefas não são sensíveis a maiúsculas e minúsculas. No entanto, alguns valores podem ser maiúsculas confidenciais, tais como uma variável que contém uma palavra-passe.  

-   Não há nenhum limite para quantas variáveis de sequência de tarefas podem ser criadas. No entanto, o número de variáveis é limitado pelo tamanho do ambiente de sequência de tarefas. O limite de tamanho total para o ambiente da sequência de tarefas é de 32 MB.  

###  <a name="BKMK_TSEnvironmentVariables"></a> Aceder a variáveis de ambiente  
 Depois de especificar a variável de sequência de tarefas e o respetivo valor utilizando um dos métodos da secção anterior, pode utilizar o valor da variável de ambiente nas sequências de tarefas. Pode aceder aos valores predefinidos para variáveis de sequência de tarefas incorporadas, especifique um novo valor para uma variável incorporada ou utilizar uma variável de sequência de tarefas personalizada numa linha de comandos ou script.  

 A tabela seguinte descreve as operações de sequência de tarefas que podem ser executadas acedendo às variáveis de ambiente de sequência de tarefas.  

|Operação de sequência de tarefas|Utilização|  
|-----------------------------|-----------|  
|Configurar definições de ação|Pode especificar que um passo de sequência de tarefas a definição é fornecido por um valor variável quando a sequência de tarefas.<br /><br /> Para fornecer um passo de sequência de tarefas definir utilizando uma variável de ambiente de sequência de tarefas, utilize o Editor de sequência de tarefas para editar o passo e especificar o nome da variável como o valor do campo. O nome da variável tem de estar entre símbolos de percentagem (%) para indicar que é uma variável de ambiente.|  
|Fornecer argumentos da linha de comandos|Pode especificar parte ou a totalidade de uma linha de comandos personalizada utilizando um valor de variável de ambiente.<br /><br /> Para fornecer uma definição da linha de comandos utilizando uma variável de ambiente, utilize o nome da variável como parte do **linha de comandos** campo a **executar linha de comandos** passo de sequência de tarefas. O nome da variável deve estar entre sinais de percentagem (%).<br /><br /> Por exemplo, a linha de comandos utiliza uma variável de ambiente incorporada para escrever o nome do computador C:\File.txt.<br /><br /> <br /><br /> **Cmd /C % smstsmachinename % > C:\File.txt**|  
|Avaliar uma condição do passo|Pode utilizar variáveis de ambiente incorporadas ou personalizadas de sequência de tarefas como parte de uma condição do passo de sequência de tarefas ou grupo. O valor da variável de ambiente será avaliado antes do passo de sequência de tarefas ou grupo for executada.<br /><br /> Para adicionar uma condição que avalia um valor de variável, efetue o seguinte:<br /><br /> 1.  Selecione o passo ou grupo que pretende adicionar a condição.<br />2.  No **opções** separador para o passo ou grupo, selecione **Task Sequence Variable** do **adicionar condição** pendente.<br />3.  No **variável de sequência de tarefas** diálogo caixa, especifique o nome da variável, a condição que é testada e o valor da variável.|  
|Fornecer informações para um script personalizado|Variáveis de sequência de tarefas podem ser lidos e escritas utilizando o objeto Microsoft.SMS COM enquanto a sequência de tarefas está em execução.<br /><br /> O exemplo a seguir ilustra um ficheiro de script do Visual Basic que consulta o **smstslogpath** variável de sequência de tarefas para obter a localização do registo atual. O script também define uma variável personalizada.<br /><br /> <br /><br /> **dim osd: set env = CreateObject("Microsoft.SMS.TSEnvironment")**<br /><br /> <br /><br /> **dim logPath**<br /><br /> <br /><br /> **' Pode consultar o ambiente para obter uma variável existente.**<br /><br /> **logPath = env("_SMSTSLogPath")**<br /><br /> <br /><br /> **' Também pode definir uma variável no ambiente OSD.**<br /><br /> **env("MyCustomVariable") = "varname"**<br /><br /> <br /><br /> Para mais informações sobre como utilizar variáveis de sequência de tarefas em scripts, consulte a documentação do SDK|  

###  <a name="BKMK_ComputerCollectionVariables"></a> Variáveis de computador e coleção  
 Pode configurar sequências de tarefas para ser executada simultaneamente em vários computadores ou coleções. Pode especificar informações exclusivas por computador ou por coleção, tais como especificar uma chave de produto exclusiva do sistema operativo ou associe todos os membros de uma coleção a um domínio especificado.  

 Pode atribuir variáveis de sequência de tarefas para um único computador ou uma coleção. Quando a sequência de tarefas começa a ser executada no computador de destino ou coleção, os valores especificados são aplicados ao computador de destino ou coleções.  

 Pode especificar variáveis de sequência de tarefas para um único computador ou uma coleção. Quando a sequência de tarefas começa a ser executada no computador de destino ou coleção, as variáveis especificadas são adicionadas para o ambiente e os valores estão disponíveis para todos os passos de sequência de tarefas na sequência de tarefas.  

> [!WARNING]  
>  Se utilizar o mesmo nome de variável variável um por coleção e por computador, o valor da variável de computador tem precedência sobre a variável de coleção. Variáveis de sequência de tarefas que atribui às coleções têm precedência sobre as variáveis de sequência de tarefas incorporadas.  

 Para obter mais informações sobre como criar variáveis de sequência para computadores e coleções de tarefas, consulte [criar variáveis de sequência de tarefas para computadores e coleções](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_CreateTSVariables).  

###  <a name="BKMK_TSMediaVariables"></a> Variáveis de suporte de dados de sequência de tarefas  
 Pode especificar variáveis de sequência de tarefas para sequências de tarefas que são executadas a partir do suporte de dados. Quando utilizar suportes de dados para implementar o sistema operativo, adicione as variáveis de sequência de tarefas e especifique os respetivos valores quando criar o suporte de dados; as variáveis e os respetivos valores são armazenadas no suporte de dados.  

> [!NOTE]  
>  Sequências de tarefas são armazenadas no suporte de dados autónomo. No entanto, todos os outros tipos de suportes de dados, tais como suportes de dados pré-configurados, obtêm a sequência de tarefas de um ponto de gestão.  

 Pode especificar variáveis de sequência de tarefas no **personalização** página do Assistente de suporte de dados de sequência de tarefas. Para obter informações sobre como utilizar suportes de dados, veja [Criar um suporte de dados de sequência de tarefas](../deploy-use/create-task-sequence-media.md).  

> [!TIP]  
>  A sequência de tarefas escreve o ID de pacote e da linha de comandos, incluindo o valor das eventuais variáveis de sequência de tarefas, para o ficheiro de registo CreateTSMedia.log no computador que executa a consola do Configuration Manager de Pré-início. Poderá consultar este ficheiro de registo para verificar o valor das variáveis da sequência de tarefas.  

##  <a name="BKMK_TSCreate"></a> Criar uma sequência de tarefas  
 Criar sequências de tarefas utilizando o Assistente de criação de sequência de tarefas. O assistente pode criar sequências de tarefas incorporadas que efetuem tarefas específicas ou sequências de tarefas personalizadas que podem executar muitas tarefas diferentes.  

 Por exemplo, pode criar sequências de tarefas que compilam e capturam uma imagem do sistema operativo de um computador de referência, instalar uma imagem do sistema operativo existente num computador de destino ou criar uma sequência de tarefas personalizada que realiza uma tarefa personalizada. Pode utilizar sequências de tarefas personalizadas para efetuar implementações especializadas do sistema operativo.  

 Para obter mais informações sobre como criar sequências de tarefas, consulte [criar sequências de tarefas](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_CreateTaskSequence).  

##  <a name="BKMK_TSEdit"></a> Editar uma sequência de tarefas  
 Edita a sequência de tarefas, utilizando o **Editor de sequência de tarefas**. O editor pode efetuar as seguintes alterações à sequência de tarefas:  

-   Pode adicionar ou remover passos da sequência de tarefas.  

-   Pode alterar a ordem dos passos da sequência de tarefas.  

-   Pode adicionar ou remover grupos de passos.  

-   Pode especificar se a sequência de tarefas continua quando ocorre um erro.  

-   Pode adicionar condições aos passos e grupos de uma sequência de tarefas.  

> [!IMPORTANT]  
>  Se a sequência de tarefas tiver quaisquer referências não associadas a um pacote ou um programa em resultado da edição, tem de corrigir a referência, eliminar o programa sem da sequência de tarefas ou desativar temporariamente o passo de sequência de tarefas falhado até a referência quebrada é corrigida ou removida.  

 Para obter mais informações sobre como editar sequências de tarefas, consulte [editar uma sequência de tarefas](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_ModifyTaskSequence).  

##  <a name="BKMK_TSDeploy"></a> Implementar uma sequência de tarefas  
 Pode implementar uma sequência de tarefas para computadores de destino que estejam em qualquer coleção do Configuration Manager. Isto inclui a coleção **Todos os Computadores Desconhecidos** que é utilizada para implementar sistemas operativos em computadores desconhecidos. No entanto, não é possível implementar uma sequência de tarefas em coleções de utilizador.  

> [!IMPORTANT]  
>  Não implemente sequências de tarefas que instalem sistemas operativos em coleções inadequadas, por exemplo a coleção **Todos os Sistemas** . Certifique-se de que a coleção na qual implementa a sequência de tarefas contém apenas os computadores onde pretende que o sistema operativo seja instalado. Para ajudar a impedir uma implementação do sistema operativo indesejada, pode gerir definições de implementação. Para obter mais informações, consulte [definições para gerir implementações de alto risco](../../protect/understand/settings-to-manage-high-risk-deployments.md).  

 Cada computador de destino que recebe a sequência de tarefas executa a sequência de tarefas, de acordo com as definições especificadas na implementação. As sequências de tarefas propriamente ditas não contêm ficheiros ou programas associados. Quaisquer ficheiros que sejam referenciados por uma sequência de tarefas terão de já estar presentes no computador de destino ou residir num ponto de distribuição ao qual os clientes podem aceder. Além disso, a sequência de tarefas instala os pacotes que são referenciados por programas, mesmo que o programa ou o pacote já está instalado no computador de destino.  

> [!NOTE]  
>  Em comparação com pacotes e programas, se a sequência de tarefas instala uma aplicação, a aplicação é instalada apenas se as regras de requisitos para a aplicação são cumpridas e a aplicação não estiver já instalada, com base no método de deteção que é especificado para a aplicação.  

 O cliente do Configuration Manager executa uma implementação de sequência de tarefas quando transfere a política de cliente. Para iniciar esta ação em vez de aguardar até ao próximo ciclo de consulta, veja [Iniciar a Obtenção de Política para um Cliente do Configuration Manager](../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval).  

 Quando implementar sequências de tarefas em dispositivos Windows Embedded que tenham o filtro de escrita ativado, pode especificar se pretende desativar o filtro de escrita no dispositivo durante a implementação e reiniciar o dispositivo após a implementação. Se o filtro de escrita não estiver desativado, a sequência de tarefas é implementada numa sobreposição temporária e não estará disponível quando o dispositivo for reiniciado.  

> [!NOTE]  
>  Quando implementa uma sequência de tarefas num dispositivo Windows Embedded, certifique-se de que o dispositivo é membro de uma coleção que tenha uma janela de manutenção configurada. Isto permite-lhe gerir o filtro de escrita desativação e a ativação, bem como quando o dispositivo for reiniciado.  
>   
>  Se os clientes transferirem sequências de tarefas fora da janela de manutenção, a sequência de tarefas é transferida duas vezes. Neste cenário clientes irão transferir a sequência de tarefas, desativar os filtros de escrita, reiniciar o computador e, em seguida, transferir a sequência de tarefas novamente porque a sequência de tarefas foi transferida para a sobreposição temporária que será eliminada quando o dispositivo for reiniciado.  

 Para obter mais informações sobre como implementar sequências de tarefas, consulte o [implementar uma sequência de tarefas](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  

##  <a name="BKMK_TSExportImport"></a> Exportar e importar sequências de tarefas  
 O Configuration Manager permite-lhe exportar e importar sequências de tarefas. Quando exporta uma sequência de tarefas, pode incluir os objetos referenciados pela sequência de tarefas. Estes incluem uma imagem do sistema operativo, uma imagem de arranque, um pacote de agente do cliente, um pacote de controladores e aplicações que têm dependências.  

> [!NOTE]  
>  O processo de exportação e importação para sequências de tarefas é muito semelhante ao processo de exportação e importação para aplicações no Configuration Manager.  

 Para obter mais informações sobre como exportar e importar sequências de tarefas, consulte [exportar e importar sequências de tarefas](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_ExportImport).  

##  <a name="BKMK_TSRun"></a> Executar uma sequência de tarefas  
 Por predefinição, as sequências de tarefas são sempre executam utilizando a conta de sistema Local. O passo da linha de comandos da sequência de tarefas fornece a capacidade para executar a sequência de tarefas como uma conta diferente. Quando a sequência de tarefas é executada, o cliente do Configuration Manager começa por verifica quaisquer pacotes referenciados antes de iniciar os passos da sequência de tarefas. Se um pacote referenciado não for validado ou não estiver disponível num ponto de distribuição, a sequência de tarefas devolve um erro para o passo associado da sequência de tarefas.  

 Se uma sequência de tarefas distribuída estiver configurada para transferir e executar, todos os pacotes dependentes e aplicações são transferidas para a cache do cliente do Configuration Manager. Os pacotes e aplicações necessários são obtidas a partir de pontos de distribuição e, se o tamanho da cache do cliente do Configuration Manager é demasiado pequeno ou não é possível encontrar o pacote ou aplicação, a sequência de tarefas falha e é gerada uma mensagem de estado. Pode também especificar que o cliente transfere conteúdo apenas quando é necessário, quando seleciona **Transferir o conteúdo localmente quando necessário para a sequência de tarefas em execução**, ou pode utilizar a opção **Executar o programa a partir do ponto de distribuição** para especificar que o cliente instala os ficheiros diretamente a partir do ponto de distribuição sem transferi-los primeiro para a cache. O **programa de execução a partir do ponto de distribuição** opção só está disponível se os pacotes referenciados tiverem a definição **copiar o conteúdo deste pacote para uma partilha de pacote em pontos de distribuição** ativada no **acesso a dados** separador do **pacote** propriedades.  

 Se um pacote dependente ou uma aplicação não pode ser localizada pelo cliente que executa a sequência de tarefas, o cliente envia imediatamente um erro quando a implementação é configurada como **disponível**. No entanto, se a implementação for configurada como **necessário**, aguarda do cliente do Configuration Manager e do ponto de tentativas de transferência do conteúdo até ao prazo, no caso do conteúdo ainda não foi replicado uma distribuição que o cliente pode aceder.  

 Quando uma sequência de tarefas é concluída com êxito ou falha, o Configuration Manager regista o resultado no histórico de cliente do Configuration Manager. Não pode cancelar nem parar uma sequência de tarefas depois de iniciada num computador.  

> [!IMPORTANT]  
>  Se um passo de sequência de tarefas requer o reinício do computador cliente, o cliente tem de ser capaz de arrancar para uma partição de disco formatado. Caso contrário, a sequência de tarefas falha independentemente de qualquer tratamento de erros especificada pela mesma.  

 Quando um objeto dependente de uma sequência de tarefas, como um pacote de distribuição de software, é atualizado para uma versão mais recente, qualquer sequência de tarefas que referencia o pacote é atualizada automaticamente e referencia a versão mais recente, independentemente do número de atualizações implementadas.  

> [!NOTE]  
>  Antes de um cliente de Configuration Manager executa uma sequência de tarefas, o cliente verifica todas as sequências de tarefas para deteção de possíveis dependências e a disponibilidade dessas dependências num ponto de distribuição. Se o cliente localizar um objeto eliminado do qual depende a sequência de tarefas, o cliente gera um erro e não executa a sequência de tarefas.  

###  <a name="BKMK_RunProgram"></a> Executar um programa antes da execução da sequência de tarefas  
 Pode selecionar um programa que é executado antes de executar a sequência de tarefas. Para especificar um programa para ser executado primeiro, abra o **propriedades** caixa de diálogo para a sequência de tarefas e selecione o **avançadas** separador para definir as opções seguintes:  

> [!IMPORTANT]  
>  Para executar um programa antes da sequência de tarefas é executada, todo o conteúdo da tarefa de sequência e o programa tem de estar disponíveis numa partilha de pacote para o pacote. Configure a partilha de pacote no separador **Acesso a Dados** das propriedades do pacote.  

-   **Executar outro programa primeiro**: Especifique que pretende que outro programa para ser executada antes de executar a sequência de tarefas.  

    > [!IMPORTANT]  
    >  Esta definição só se aplica a sequências de tarefas que são executados no sistema operativo completo. Gestor de configuração ignora esta definição se a sequência de tarefas é iniciada através de suportes de dados de arranque ou PXE.  

-   **Pacote**: Especifique o pacote que contém o programa.  

-   **Programa**: Especifique o programa para ser executada.  

-   **Executar sempre este programa primeiro**: Especifique que pretende que o Configuration Manager para executar este programa sempre que executar a sequência de tarefas no mesmo cliente. Por predefinição, após a execução bem-sucedida de um programa, este não é executado novamente se a sequência de tarefas for executada novamente no mesmo cliente.  

 Se o programa selecionado não for executado num cliente, a sequência de tarefas não é executada.  

##  <a name="BKMK_TSMaintenanceWindow"></a> Utilizar uma janela de manutenção para especificar quando pode executar uma sequência de tarefas  
 Pode especificar quando a sequência de tarefas pode executar, definir uma janela de manutenção para a coleção que contém os computadores de destino. As janelas de manutenção são configuradas com uma data de início, uma hora de início e de fim e um padrão de periodicidade. Além disso, quando definir a agenda para a janela de manutenção, pode especificar que a janela de manutenção só se aplica a sequências de tarefas. Para obter mais informações, consulte [como utilizar janelas de manutenção](../../core/clients/manage/collections/use-maintenance-windows.md).  

> [!IMPORTANT]  
>  Quando configura uma janela de manutenção para executar uma sequência de tarefas, uma vez as sequências de tarefas iniciadas, continuam a ser executadas mesmo que a janela de manutenção se feche. A sequência de tarefas será concluída com sucesso ou falha.  

##  <a name="BKMK_TSNetworkAccessAccount"></a> Sequências de tarefas e Conta de Acesso à Rede  
 Embora as sequências de tarefas executadas apenas no contexto da conta do sistema Local, poderá ter de configurar a conta de acesso de rede nas seguintes circunstâncias:  

-   Tem de configurar a conta de acesso à rede corretamente ou a sequência de tarefas falhará se tentar aceder aos pacotes do Configuration Manager em pontos de distribuição para concluir a tarefa. Para obter mais informações sobre a conta de acesso à rede, consulte [conta de acesso à rede](../../core/plan-design/hierarchy/manage-accounts-to-access-content.md#bkmk_NAA).  

    > [!NOTE]  
    >  A conta de acesso à rede nunca é utilizada como o contexto de segurança para executar programas, instalar aplicações, instalação de atualizações ou executar sequências de tarefas No entanto, a conta de acesso à rede é utilizada para aceder aos recursos associados na rede.  

-   Quando utiliza uma imagem de arranque para iniciar a implementação do sistema operativo, Configuration Manager utiliza o ambiente do Windows PE, que não é um sistema operativo completo. O ambiente do Windows PE utiliza um nome aleatório gerado automaticamente que não é um membro de qualquer domínio. Se não configurar a conta de acesso à rede corretamente, o computador pode não ter as permissões necessárias para aceder os pacotes do Configuration Manager necessária para concluir a sequência de tarefas.  

##  <a name="BKMK_TSCreateMedia"></a> Criar suportes de dados para sequências de tarefas  
 É possível escrever sequências de tarefas e os respetivos ficheiros relacionados e as dependências para vários tipos de suportes de dados. Isto inclui a escrita em suportes de dados amovíveis, como um conjunto de DVD ou CD ou uma unidade flash USB para suportes de dados de captura, autónomos e de arranque, ou a escrita num ficheiro WIM (Windows Imaging Format) para suportes de dados pré-configurados.  

 Pode criar os seguintes tipos de suportes de dados:  

-   **Suporte de dados de captura**. Capturas de suporte de dados de captura uma imagem do sistema operativo configurada e criada fora da infraestrutura do Configuration Manager. O suporte de dados de captura pode conter programas personalizados que podem ser executados antes da execução de uma sequência de tarefas. O programa personalizado pode interagir com o ambiente de trabalho, solicitar ao utilizador para os valores de entrada ou criar variáveis para serem utilizadas pela sequência de tarefas.  

     Para obter mais informações, consulte [criar suportes de dados de captura](../deploy-use/create-capture-media.md).  

-   **Suporte de dados autónomo**. O suporte de dados autónomo contém a sequência de tarefas e todos os objetos associados necessários à execução da sequência de tarefas. Tarefas de suporte de dados autónomo sequências podem ser executadas quando o Configuration Manager possui limitada ou sem conectividade à rede. Suporte de dados autónomo pode ser executadas das seguintes formas:  

    -   Se o computador de destino não for inicializado, a imagem do Windows PE que está associada a sequência de tarefas é utilizada a partir do suporte de dados autónomo e começa a sequência de tarefas.  

    -   O suporte de dados autónomo pode ser iniciado manualmente se um utilizador com sessão iniciado rede e inicia a instalação.  

    > [!IMPORTANT]  
    >  Os passos da sequência de tarefas de suporte de dados autónomo tem de ser capazes de executar sem qualquer obter quaisquer dados a partir da rede; caso contrário, o passo de sequência de tarefas que tenta obter os dados de falha. Por exemplo, um passo de sequência de tarefas que necessita de um ponto de distribuição para obter um pacote falha; No entanto se o pacote necessário estiver contido no suporte de dados autónomo, o passo de sequência de tarefas é concluída com êxito.  

     Para obter mais informações, consulte [criar suportes de dados autónomos](../deploy-use/create-stand-alone-media.md).  

-   **Suportes de dados**. Suportes de dados contém os ficheiros necessários para iniciar um computador de destino para que possa estabelecer ligação à infraestrutura do Configuration Manager para determinar que sequências de tarefas executar com base na respetiva associação a uma coleção. A sequência de tarefas e os objetos dependentes não estão contidos no suporte de dados; em vez disso, são obtidos através da rede do cliente do Configuration Manager. Este método é útil para novos computadores ou implementações bare-metal ou quando nenhum cliente do Configuration Manager ou o sistema operativo está no computador de destino.  

     Para obter mais informações, consulte [criar suportes de dados](../deploy-use/create-bootable-media.md).  

-   **Suporte de dados pré-configurado**. O suporte de dados pré-configurado implementa uma imagem do sistema operativo num computador de destino que não está aprovisionado. O suporte de dados pré-configurado é armazenado como um ficheiro de formato WIM (Windows Imaging) que pode ser instalado num computador bare-metal pelo fabricante ou num centro de transição empresarial que não está ligado ao ambiente do Configuration Manager.  

     Para obter mais informações, consulte [criar suportes de dados pré-configurados](../deploy-use/create-prestaged-media.md).  

 Quando cria suportes de dados, especifique uma palavra-passe para o suporte de dados controlar o acesso aos ficheiros que estão contidos no suporte de dados. Se especificar uma palavra-passe, um utilizador tem de estar presente para introduzir a palavra-passe no computador de destino quando a sequência de tarefas é executada.  

 Quando executa uma sequência de tarefas utilizando suportes de dados, a arquitetura de chips do computador especificado contida no suporte de dados não será reconhecida e a sequência de tarefas tenta executar, mesmo se a arquitetura especificada não corresponde ao que está atualmente instalada no computador de destino. Se a arquitetura de chips contida no suporte de dados não corresponde a arquitetura de chips instalada no computador de destino, a instalação falha.  

 Para obter mais informações sobre como implementar sistemas operativos utilizando suportes de dados, consulte [criar suportes de dados de sequência de tarefas](../deploy-use/create-task-sequence-media.md).  
