---
title: Como utilizar variáveis de sequência de tarefas
titleSuffix: Configuration Manager
description: Saiba mais sobre como utilizar as variáveis numa sequência de tarefas do Configuration Manager.
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: bc7de742-9e5c-4a70-945c-df4153a61cc3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3e8ebea21b735e6b93d73bf6ff5eb842243ef42d
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56121867"
---
# <a name="how-to-use-task-sequence-variables-in-configuration-manager"></a>Como utilizar variáveis de sequência de tarefas no Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

 O motor de sequência de tarefas na funcionalidade de implementação do sistema operacional do Configuration Manager usa muitas variáveis para controlar seus comportamentos. Utilize estas variáveis para: 
 - Conjunto de condições nos passos  
 - Alterar comportamentos para obter passos específicos  
 - Utilize scripts para medidas mais complexas  


 Para obter uma referência de todas as variáveis de sequência de tarefas disponíveis, consulte [variáveis de sequência de tarefas](/sccm/osd/understand/task-sequence-variables).



## <a name="bkmk_types"></a> Tipos de variáveis

 Existem vários tipos de variáveis:  
 - [Incorporado](#bkmk_built-in)  
 - [ação](#bkmk_action)  
 - [Personalizar](#bkmk_custom)  
 - [só de leitura](#bkmk_read-only)  
 - [Matriz](#bkmk_array)  


### <a name="bkmk_built-in"></a> Variáveis incorporadas

 As variáveis incorporadas fornecem informações sobre o ambiente em que a sequência de tarefas é executada. Os valores estão disponíveis em toda a sequência de tarefas de todo. Normalmente, o motor de sequência de tarefas inicializa as variáveis incorporadas antes da execução quaisquer passos. 

 Por exemplo,  **\_SMSTSLogPath** é uma variável de ambiente que especifica o caminho para o qual os componentes do Configuration Manager escrever ficheiros de registo. Qualquer passo de sequência de tarefas pode aceder a esta variável de ambiente. 

 A sequência de tarefas avalia algumas variáveis antes de cada passo. Por exemplo,  **\_SMSTSCurrentActionName** lista o nome do passo atual. 

### <a name="bkmk_action"></a> Variáveis de ação

 Variáveis de ação de sequência de tarefas, especificar definições de configuração que utiliza um passo de sequência de tarefas único. Por predefinição, o passo inicializa as respetivas definições antes da execução. Estas definições estão disponíveis apenas enquanto o passo de sequência de tarefas associado é executado. A sequência de tarefas adiciona o valor da variável de ação para o ambiente antes da execução do passo. Em seguida, remove o valor do ambiente após o passo ser executado.

 Por exemplo, adicione a **executar linha de comandos** passo para uma sequência de tarefas. Este passo inclui uma **iniciar em** propriedade. A sequência de tarefas armazena um valor predefinido para esta propriedade como o **WorkingDirectory** variável. A sequência de tarefas inicializa este valor antes da execução de **executar linha de comandos** passo. Enquanto estiver a executar este passo, aceder a **iniciar em** valor da propriedade da **WorkingDirectory** valor. Depois de concluir a etapa, a sequência de tarefas remove o valor do **WorkingDirectory** variável do ambiente. Se a sequência de tarefas inclui outro **executar linha de comandos** passo, ele inicializa um novo **WorkingDirectory** variável. Nessa altura, a sequência de tarefas define a variável como o valor inicial para o passo atual. Para obter mais informações, consulte [WorkingDirectory](using-task-sequence-variables.md#WorkingDirectory).  

 O *predefinição* valor para uma variável de ação é presente quando o passo for executado. Se definir um *novo* valor, está disponível para vários passos numa sequência de tarefas. Se substituir um valor predefinido, o novo valor permanece no ambiente. Este novo valor substitui o valor predefinido para outros passos da sequência de tarefas. Por exemplo, adicionar um **Set Task Sequence Variable** passo como o primeiro passo da sequência de tarefas. Este passo define a **WorkingDirectory** variável à `C:\`. Qualquer **executar linha de comandos** passo na sequência de tarefas utiliza o novo valor inicial do diretório.  

 Alguns passos de sequência de tarefas marcar determinados variáveis de ação como *saída*. Estas variáveis de saída de leitura de passos mais tarde na sequência de tarefas.

 > [!Note]  
 > Nem todos os passos de sequência de tarefas tem variáveis de ação. Por exemplo, apesar de existirem variáveis associadas com o **ativar BitLocker** ação, não há nenhuma variável associada a **desativar BitLocker** ação.  


### <a name="bkmk_custom"></a> Variáveis personalizadas

 Estas variáveis são os que não cria o Configuration Manager. Inicialize o seu próprio variáveis para utilizar como condições, nas linhas de comandos ou em scripts. 

 Quando especificar um nome para uma nova variável de sequência de tarefas, siga estas diretrizes:  

 - O nome de variável de sequência de tarefas pode incluir letras, números, o caráter de sublinhado (`_`) e um hífen (`-`).  

 - Nomes de variáveis de sequência de tarefas têm um comprimento mínimo de um caráter e um comprimento máximo de 256 carateres.  

 - As variáveis definidas pelo utilizador têm de começar com uma letra (`A-Z` ou `a-z`).  

 - Os nomes de variáveis definidas pelo utilizador não podem começar pelo caráter de sublinhado. Apenas variáveis de sequência de tarefas só de leitura são precedidas pelo caráter de sublinhado.  

 - Nomes de variáveis de sequência de tarefas não são maiúsculas e minúsculas. Por exemplo, `OSDVAR` e `osdvar` são a mesma variável de sequência de tarefas.  

 - Nomes de variáveis de sequência de tarefas não podem começar nem terminar com um espaço. Eles também não é possível ter incorporado espaços. A sequência de tarefas ignora os espaços no início ou fim de um nome de variável.  


 Não existe nenhum limite de conjunto para quantas variáveis de sequência de tarefas, pode criar. No entanto, o número de variáveis é limitado pelo tamanho do ambiente de sequência de tarefas. O limite de tamanho total para o ambiente da sequência de tarefas é de 32 MB.  


### <a name="bkmk_read-only"></a> Variáveis só de leitura

 Não é possível alterar o valor de algumas variáveis, que são só de leitura. Normalmente, o nome começa com um caráter de sublinhado (\_). A sequência de tarefas utiliza-os para suas operações. As variáveis só de leitura são visíveis no ambiente de sequência de tarefas. 

 Estas variáveis são úteis em scripts ou linhas de comando. Por exemplo, executar uma linha de comandos e encaminhando a saída para um registo de ficheiros  **\_SMSTSLogPath** com os outros ficheiros de registo.

 > [!NOTE]  
 >  Passos de sequência de tarefas só de leitura variáveis podem ser lidos por uma sequência de tarefas, mas não podem ser definidas. Por exemplo, usar uma variável só de leitura como parte da linha de comandos para um **executar linha de comandos** passo. Não é possível definir uma variável só de leitura com o **definir variável da sequência de tarefas** passo.  



### <a name="bkmk_array"></a> Variáveis de matriz

 A sequência de tarefas armazena algumas variáveis como uma matriz. Cada elemento da matriz representa as definições para um único objeto. Quando um dispositivo tiver mais do que um objeto para configurar, utilize estas variáveis. Os seguintes passos de sequência de tarefas utilizam variáveis de matriz:

 - [Aplicar definições de rede](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  

 - [Formatar e particionar disco](task-sequence-steps.md#BKMK_FormatandPartitionDisk)  



## <a name="bkmk_set"></a> Como definir as variáveis

 Para variáveis personalizadas ou variáveis que não são só de leitura, existem vários métodos para inicializar e definir o valor da variável:  

 - [Definir variável da sequência de tarefas](#bkmk_set-ts-step)  
 - [Definir variáveis dinâmicas](#bkmk_set-dyn-step)  
 - [Variáveis de coleção e dispositivo](#bkmk_set-coll-var)  
 - [Objeto TSEnvironment COM](#bkmk_set-com)  
 - [Comando de Pré-início](#bkmk_set-prestart)  
 - [Assistente de suporte de dados de sequência de tarefas](#bkmk_set-media)  


 Elimine uma variável do ambiente utilizando os mesmos métodos usados para criar uma variável. Para eliminar uma variável, defina o valor da variável como uma cadeia vazia.  

 Pode combinar métodos para definir uma variável de sequência de tarefas para diferentes valores para a mesma sequência. Por exemplo, defina os valores padrão usando o editor de sequência de tarefas e, em seguida, definir valores personalizados usando um script. 

 Se definir a mesma variável pelos métodos diferentes, o motor de sequência de tarefas utiliza pela seguinte ordem:  

 1. Avalia as variáveis de coleção em primeiro lugar.  

 2. Variáveis específicas de dispositivo substituem a mesma variável definida numa coleção.  

 3. As variáveis definidas por qualquer método durante a sequência de tarefas têm precedência sobre as variáveis de coleção ou dispositivo.  


#### <a name="general-limitations-for-task-sequence-variable-values"></a>Limitações gerais para valores de variáveis de sequência de tarefas  

 - Valores de variáveis de sequência de tarefas não podem ser mais de 4.000 caracteres.  

 - Não é possível alterar uma variável de sequência de tarefas só de leitura. As variáveis só de leitura têm nomes que começam com um caráter de sublinhado (`_`).  

 - Valores de variáveis de sequência de tarefas podem ser maiúsculas e minúsculas consoante a utilização do valor. Na maioria dos casos, os valores de variáveis de sequência de tarefas não diferencia maiúsculas de minúsculas. Uma variável que inclui uma palavra-passe diferencia maiúsculas de minúsculas.  


### <a name="bkmk_set-ts-step"></a> Definir variável da sequência de tarefas

 Utilize este passo na sequência de tarefas para definir uma única variável como um valor único. 

 Para obter mais informações, consulte [Set Task Sequence Variable](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable). 


### <a name="bkmk_set-dyn-step"></a> Definir variáveis dinâmicas

 Utilize este passo na sequência de tarefas para definir um ou mais variáveis de sequência de tarefas. Pode definir regras neste passo, determinar quais variáveis e valores a utilizar. 

 Para obter mais informações, consulte [definir variáveis dinâmicas](/sccm/osd/understand/task-sequence-steps#BKMK_SetDynamicVariables).


### <a name="bkmk_set-coll-var"></a> Variáveis de coleção e dispositivo

 Definir variáveis as propriedades de uma coleção ou um dispositivo específico. 

 Para obter mais informações, consulte [criar variáveis de sequência de tarefas para computadores e coleções](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_CreateTSVariables).


### <a name="bkmk_set-com"></a> Objeto TSEnvironment COM

 Para trabalhar com variáveis a partir de um script, utilize o **TSEnvironment** objeto. 

 Para obter mais informações, consulte [como utilizar variáveis numa sequência de tarefas em execução](/sccm/develop/osd/how-to-use-task-sequence-variables-in-a-running-task-sequence) no SDK do Configuration Manager.


### <a name="bkmk_set-prestart"></a> Comando de Pré-início

 O comando de Pré-início é um script ou executável que é executado no Windows PE antes do utilizador seleciona a sequência de tarefas. O comando de Pré-início pode consultar uma variável ou solicitar ao utilizador informações e, em seguida, guarde-o no ambiente. Utilize o [TSEnvironment](#bkmk_set-com) objeto de COM para ler e escrever as variáveis do comando de Pré-início. 

 Para obter mais informações, consulte [comandos para suporte de dados de sequência de tarefas de Pré-início](/sccm/osd/understand/prestart-commands-for-task-sequence-media).


### <a name="bkmk_set-media"></a> Assistente de suporte de dados de sequência de tarefas

 Especifica variáveis de sequências de tarefas que executam a partir de suportes de dados. Quando utilizar suportes de dados para implantar o sistema operacional, adicione as variáveis de sequência de tarefas e especifique os respetivos valores quando criar o suporte de dados. As variáveis e os respetivos valores são armazenadas no suporte de dados.  

 > [!NOTE]  
 >  Sequências de tarefas são armazenadas no suporte de dados autónomo. No entanto, todos os outros tipos de suportes de dados, tais como suportes de dados pré-configurados, obtêm a sequência de tarefas de um ponto de gestão.  

 Quando executa uma sequência de tarefas do suporte de dados, pode adicionar uma variável no **personalização** página do assistente. 

 Utilize as variáveis de suporte de dados em vez de variáveis por coleção ou por computador. Se a sequência de tarefas é executada a partir de suportes de dados, as variáveis por computador e por coleção não se aplicam e não são utilizadas.  

 > [!TIP]  
 >  A sequência de tarefas escreve o ID de pacote e a linha de comandos de Pré-início para o **Createtsmedia** ficheiro no computador que executa a consola do Configuration Manager. Este ficheiro de registo inclui o valor das eventuais variáveis de sequência de tarefas. Consulte este ficheiro de registo para verificar o valor das variáveis de sequência de tarefas.  

 Para obter mais informações, consulte [criar suporte de dados de sequência de tarefas](/sccm/osd/deploy-use/create-task-sequence-media).



## <a name="bkmk_access"></a> Como aceder a variáveis

 Depois de especificar a variável e o respetivo valor utilizando um dos métodos da secção anterior, utilizá-lo nas suas sequências de tarefas. Por exemplo, aceder a valores predefinidos para variáveis de sequência de tarefas incorporadas ou fazer uma etapa condicional no valor de uma variável.  

 Utilize os seguintes métodos para aceder a valores de variáveis no ambiente de sequência de tarefas:
 - [Utilizar um passo](#bkmk_access-step)  
 - [Condição do passo](#bkmk_access-condition)  
 - [Script personalizado](#bkmk_access-script)  
 - [Arquivo de resposta de configuração do Windows](#bkmk_access-answer)  
  

### <a name="bkmk_access-step"></a> Utilizar um passo

 Especifique um valor de uma definição de variável num passo de sequência de tarefas. No editor de sequência de tarefas, editar o passo e especificar o nome da variável como o valor do campo. Coloque o nome da variável de percentagem (`%`). 

 Por exemplo, utilize o nome da variável como parte do **linha de comandos** campo a **executar linha de comandos** passo. A seguinte linha de comando escreve o nome do computador para um arquivo de texto. 

 `cmd.exe /c %_SMSTSMachineName% > C:\File.txt`


### <a name="bkmk_access-condition"></a> Condição do passo

 Utilize variáveis de sequência de tarefas internas ou personalizadas como parte de uma condição num passo ou grupo. A sequência de tarefas avalia o valor da variável antes da execução do passo ou grupo.

 Para adicionar uma condição que avalia um valor de variável, efetue os seguintes passos:  

 1. No editor de sequência de tarefas, selecione o passo ou grupo ao qual pretende adicionar a condição.  

 2. Mude para o **opções** separador para o passo ou grupo. Clique em **adicionar condição**e selecione **Task Sequence Variable**.  

 3. Na **Task Sequence Variable** diálogo caixa, especifique as seguintes definições:  

    - **Variável**: O nome da variável. Por exemplo, `_SMSTSInWinPE`.  

    - **Condição**: A condição para avaliar o valor da variável. Por exemplo, **é igual a**.  

    - **Valor**: O valor da variável para verificar. Por exemplo, `false`.  


 Os três exemplos acima formam uma condição comum para testar se a sequência de tarefas for executada a partir de uma imagem de arranque no Windows PE: 

 > **Variável de sequência de tarefas** `_SMSTSInWinPE equals "false"`

 Consulte esta condição sobre o **capturar ficheiros e definições** grupo do modelo de sequência de tarefas padrão para instalar uma imagem de SO existente.


### <a name="bkmk_access-script"></a> Script personalizado

 Ler e escrever as variáveis com o **tsenvironment** objeto COM enquanto a sequência de tarefas está em execução.

 As seguintes consultas de exemplo do Windows PowerShell a **smstslogpath** variável para obter a localização do registo atual. O script também define uma variável personalizada.

 ```PowerShell
 # Create an object to access the task sequence environment
 $tsenv = New-Object -ComObject Microsoft.SMS.TSEnvironment
 
 # Query the environment to get an existing variable
 # Set a variable for the task sequence log path
 $LogPath = $tsenv.Value("_SMSTSLogPath")

 # Or, convert all of the variables currently in the environment to PowerShell variables
 $tsenv.GetVariables() | % { Set-Variable -Name "$_" -Value "$($tsenv.Value($_))" }

 # Write a message to a log file
 Write-Output "Hello world!" | Out-File -FilePath "$_SMSTSLogPath\mylog.log" -Encoding "Default" -Append
 
 # Set a custom variable "startTime" to the current time
 $tsenv.Value("startTime") = (Get-Date -Format HH:mm:ss) + ".000+000"
 ```


###  <a name="bkmk_access-answer"></a> Arquivo de resposta de configuração do Windows

O arquivo de resposta de configuração de Windows que fornecer pode ter incorporadas as variáveis de sequência de tarefas. Use o formulário `%varname%`, onde *varname* é o nome da variável. O **configuração do Windows e ConfigMgr** passo substitui a cadeia de caracteres do nome da variável para o valor da variável real. Estas variáveis de sequência de tarefas incorporadas não podem ser utilizados em campos apenas numéricos num ficheiro de resposta Unattend. XML.

Para mais informações, consulte [Setup Windows and ConfigMgr](/sccm/osd/understand/task-sequence-steps#BKMK_SetupWindowsandConfigMgr).



## <a name="see-also"></a>Consulte também

- [Passos de sequência de tarefas](/sccm/osd/understand/task-sequence-steps)
- [Variáveis de sequência de tarefas](/sccm/osd/understand/task-sequence-variables)
- [Considerações sobre planeamento para automatizar tarefas](/sccm/osd/plan-design/planning-considerations-for-automating-tasks)
