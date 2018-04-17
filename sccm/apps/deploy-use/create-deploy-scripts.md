---
title: Criar e executar scripts
titleSuffix: Configuration Manager
description: Criar e executar scripts do Powershell nos dispositivos cliente.
ms.custom: na
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
caps.latest.revision: 14
caps.handback.revision: 0
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b9699b2f4bd1f18890d25582be9a8d20778b64be
ms.sourcegitcommit: fb84bcb31d825f454785e3d9d8be669e00fe2b27
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 04/16/2018
---
# <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>Criar e executar scripts do PowerShell a partir da consola do Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

<!--1236459-->
System Center Configuration Manager tem uma capacidade integrada para executar Powershell scripts. PowerShell tem a vantagem de criar sofisticadas, scripts automatizados, compreendeu e partilhados com uma Comunidade maior. Os scripts de simplificam a criação de ferramentas personalizadas para administrar o software e permitem a realizar tarefas criar rapidamente, permitindo-lhe obter tarefas grandes feitas de forma mais fácil e mais consistente.  

> [!TIP]  
> Esta funcionalidade foi introduzida pela primeira vez na versão 1706 como um [funcionalidade de pré-lançamento](/sccm/core/servers/manage/pre-release-features). A partir da versão 1802, esta funcionalidade já não é uma funcionalidade de pré-lançamento.  


> [!Note]  
> O Configuration Manager não ativar esta funcionalidade opcional por predefinição. Tem de ativar esta funcionalidade antes de o utilizar. Para obter mais informações, consulte [ativar funcionalidades opcionais de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


Esta integração no System Center Configuration Manager, pode utilizar o *executar Scripts* funcionalidade para efetue os seguintes procedimentos:

- Criar e editar os scripts para utilização com o System Center Configuration Manager.
- Gerir a utilização de script através de funções e âmbitos de segurança. 
- Executar scripts em coleções ou individuais no local geridos Windows PCs.
- Obter resultados de script agregados rápida dos dispositivos cliente.
- Monitorizar a execução do script e ver relatórios de resultados da saída do script.

>[!WARNING]
>Tendo em conta a potência de scripts, iremos relembrá-intencional e cuidado com a respetiva utilização. Criámos proteções adicionais para o ajudar a; segregated funções e âmbitos. Lembre-se de que validar a precisão dos scripts antes de executá-los e confirmar são de uma origem fidedigna, para impedir a execução do script indesejados. Ser mindful de caracteres expandidas ou outro obfuscation e informe-se sobre como proteger scripts. [Saiba mais sobre a segurança de script do PowerShell](/sccm/apps/deploy-use/learn-script-security)

## <a name="prerequisites"></a>Pré-requisitos

- Para executar scripts do PowerShell, o cliente deve executar o PowerShell versão 3.0 ou posterior. No entanto, se um script executa contém funcionalidade de uma versão posterior do PowerShell, o cliente em que executa o script tem de executar essa versão do PowerShell.
- Clientes do Configuration Manager tem de executar o cliente a partir da versão 1706 ou posterior para executar scripts.
- Para utilizar scripts, tem de ser um membro da função de segurança adequado do Configuration Manager.
- Para importar e criar scripts - a conta tem de ter **criar** permissões para **SMS Scripts**.
- Para aprovar ou recusar scripts - a conta tem de ter **aprovar** permissões para **SMS Scripts**.
- Para executar scripts - a conta tem de ter **executar Script** permissões para **coleções**.

Para obter mais informações sobre funções de segurança do Configuration Manager:</br>
[Âmbitos de segurança para executadas scripts](#BKMK_Scopes)</br>
[Funções de segurança para executadas scripts](#BKMK_ScriptRoles)</br>
[Noções básicas da administração baseada em funções](/sccm/core/understand/fundamentals-of-role-based-administration).

## <a name="limitations"></a>Limitações

Executadas Scripts atualmente suporta:

- Linguagens de scripts: PowerShell
- Tipos de parâmetro: número inteiro, cadeia e lista.


>[!WARNING]
>Tenha em atenção que, ao utilizar parâmetros,-abre uma área de superfície de potenciais riscos de ataque de injeção de PowerShell. Existem várias formas para mitigar e resolver o problema, tais como utilizar expressões regulares para validar o parâmetro de entrada ou utilizar predefinidos a parâmetros. Melhor prática comum é não incluir a segredos no seu scripts do PowerShell (sem palavras-passe, etc.). [Saiba mais sobre a segurança de script do PowerShell](/sccm/apps/deploy-use/learn-script-security) <!--There are external tools available to validate your PowerShell scripts such as the [PowerShell Injection Hunter](https://www.powershellgallery.com/packages/InjectionHunter/1.0.0) tool. -->


## <a name="run-script-authors-and-approvers"></a>Execução de Script de autores e aprovadores

Executar utiliza Scripts o conceito de *script autores* e *script aprovadores* como funções separadas para implementação e a execução de um script. Com as funções de autor e aprovador separadas permite uma verificação de processo importante para a ferramenta de elevado desempenho que está a executar Scripts. Não há mais *script runners* função que permite a execução de scripts, mas não a criação ou a aprovação de scripts. Consulte [criar funções de segurança para os scripts](#BKMK_ScriptRoles).

### <a name="scripts-roles-control"></a>Controlo de funções de scripts

Por predefinição, os utilizadores não podem aprovar um script que tenham criado. Uma vez scripts são poderosa, versátil e potencialmente implementado para vários dispositivos, pode dividir as funções entre a pessoa que cria o script e a pessoa que aprove o script. Estas funções dar um nível adicional de segurança contra a execução de um script sem supervisão. É possível desativar aprovação secundária, para facilitar a testar.

### <a name="approve-or-deny-a-script"></a>Aprovar ou recusar um script

Scripts devem ser aprovados, pelo *script aprovador* função, antes de estes serem executados. Para aprovar um script:

1. Na consola do Configuration Manager, clique em **Biblioteca de Software**.
2. No **biblioteca de Software** área de trabalho, clique em **Scripts**.
3. No **Script** lista, selecione o script que pretende aprovar ou recusar e, em seguida, no **home page** separador o **Script** , clique em **aprovar/negação**.
4. No **aprovar ou negar o script** caixa de diálogo, selecione **aprovar**, ou **negar** para o script. Opcionalmente, introduza um comentário sobre a sua decisão.  Se negar um script, não pode ser executado nos dispositivos cliente. <br>
![Script - aprovação](./media/run-scripts/RS-approval.png)
1. Conclua o assistente. No **Script** lista, verá o **estado de aprovação** alteração de coluna consoante a ação que demorou.

### <a name="allow-users-to-approve-their-own-scripts"></a>Permitir que os utilizadores aprovar os seus próprios scripts

Esta aprovação é principalmente utilizada para a fase de teste de desenvolvimento do script.

1. Na consola do Configuration Manager, clique em **Administração**.
2. Na área de trabalho **Administração** , expanda **Configuração do Site**e clique em **Sites**.
3. Na lista de sites, selecione o site e, em seguida, no **home page** separador o **Sites** , clique em **definições de hierarquia**.
4. No **geral** separador do **propriedades de definições de hierarquia** diálogo caixa, desmarque a caixa de verificação **não permitir autores de script aprovar os seus próprios scripts**.

>[!IMPORTANT]
>Como melhor prática, não deve permitir que um autor de script para aprovar os seus próprios scripts. Só deve ser permitido num cenário de laboratório. Pondere cuidadosamente o impacto potencial da alteração desta definição num ambiente de produção.

## <a name="security-scopes"></a>Âmbitos de segurança
*(Introduzida com a versão 1710)*  
Execute utiliza Scripts âmbitos de segurança, uma funcionalidade existente do Configuration Manager, a criação de scripts de controlo e execução através da atribuição de etiquetas que representam os grupos de utilizadores. Para obter mais informações sobre como utilizar âmbitos de segurança, consulte [configurar a administração baseada em funções para o System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).

## <a name="bkmk_ScriptRoles"></a> Criar funções de segurança para os scripts
As funções de três segurança utilizadas para executar scripts não estão criadas por predefinição no Configuration Manager. Para criar o script runners, autores de scripts e funções de aprovadores de script, siga os passos delineados.

1. Na consola do Configuration Manager, vá para **administração** >**segurança** >**funções de segurança**
2. Faça duplo clique numa função e clique em **cópia**. A função que copiar tem permissões já atribuídas. Certifique-se de que tomar apenas as permissões que pretende. 
3. Atribua a função personalizada um **nome** e um **Descrição**. 
4. Atribua a função de segurança as permissões descritas abaixo. 

    ### <a name="security-role-permissions"></a>**Permissões de função de segurança**

     **Nome da função**: Script Runners
    - **Descrição**: Estas permissões ativar esta função executar apenas scripts que foram anteriormente criadas e aprovadas pela outras funções. 
    - **Permissões:** Certifique-se de que está definidas como **Sim**.
         |**Categoria**|**Permissão**|**Estado**|
         |---|---|---|
         |Coleção|Executar Script|Sim|
         |Scripts SMS|Criar|Sim|
         |Scripts SMS|Leitura|Sim|

     **Nome da função**: Autores de script
    - **Descrição**: Estas permissões ativar desta função de autor scripts, mas não podem aprovar ou executá-los. 
    - **Permissões**: Certifique-se de que as seguintes permissões são definidas.
    - 
         |**Categoria**|**Permissão**|**Estado**|
         |---|---|---|
         |Coleção|Executar Script|Não|
         |Scripts SMS|Criar|Sim|
         |Scripts SMS|Leitura|Sim|
         |Scripts SMS|Eliminar|Sim|
         |Scripts SMS|Modificar|Sim|

    **Nome da função**: Autores de script
    - **Descrição**: Estas permissões ativar esta função aprovar scripts, mas não é possível criar ou executá-los. 
    - **Permissões:** Certifique-se de que as seguintes permissões são definidas.

         |**Categoria**|**Permissão**|**Estado**|
         |---|---|---|
         |Coleção|Executar Script|Não|
         |Scripts SMS|Leitura|Sim|
         |Scripts SMS|Aprovar|Sim|
         |Scripts SMS|Modificar|Sim|
     
**Exemplo de permissões de Scripts de SMS para a função de autores de script**

 ![Exemplo de permissões de Scripts de SMS para a função de autores de script](./media/run-scripts/script_authors_permissions.png)

   

## <a name="create-a-script"></a>Criar um script

1. Na consola do Configuration Manager, clique em **Biblioteca de Software**.
2. No **biblioteca de Software** área de trabalho, clique em **Scripts**.
3. No **home page** separador o **criar** , clique em **criar Script**.
4. No **Script** página do criar **Script** assistente, configure as seguintes definições:
    - **Nome do script** -introduza um nome para o script. Embora possa criar vários scripts com o mesmo nome, utilizar nomes duplicados torna mais difícil localizar o script que terá na consola do Configuration Manager.
    - **Idioma de script** -atualmente, os scripts do PowerShell só são suportados.
    - **Importar** -importar um script do PowerShell para a consola. O script é apresentado no **Script** campo.
    - **Limpar** -remove o script atual o campo de Script.
    - **Script** -apresenta o script atualmente importado. Pode editar o script neste campo, conforme necessário.
5. Conclua o assistente. O novo script é apresentado no **Script** lista com um Estado de **aguardar aprovação**. Antes de poder executar este script nos dispositivos cliente, terá de o aprovar. 

> [!IMPORTANT]
    >Evite um reinício de dispositivo ou reiniciar o agente do Configuration Manager de processamento de scripts ao utilizar a funcionalidade de executar Scripts. Se o fizer, poderão levar para um Estado rebooting contínuo. Se for necessário, existem melhoramentos para a funcionalidade de notificação de cliente que permitem dispositivos reiniciar, a partir do Configuration Manager versão 1710. O [pendente da coluna de reinício](/sccm/core/clients/manage/manage-clients#Restart-clients) pode ajudar a identificar dispositivos que necessitam de um reinício. 
<!--SMS503978  -->

## <a name="script-parameters"></a>Parâmetros do script
*(Introduzida com a versão 1710)*  
Adicionar parâmetros a um script fornece uma maior flexibilidade para o seu trabalho. A seguir descreve a capacidade de atual a funcionalidade de executar Scripts com parâmetros do script para; *Cadeia*, *número inteiro* tipos de dados. Apresenta uma lista de valores predefinidas também está disponível. Se o script tem o tipos de dados não suportado, receberá um aviso.

No **criar Script** caixa de diálogo, clique em **parâmetros do Script** em **Script**.

Cada um dos parâmetros do script tem a suas próprias caixa de diálogo para adicionar mais detalhes e validação.

>[!IMPORTANT]
> Os valores de parâmetros não podem conter um apóstrofo. 


### <a name="parameter-validation"></a>Validação dos parâmetros

Cada parâmetro no script tem um **propriedades de parâmetro de Script** caixa de diálogo para adicionar a validação para este parâmetro. Depois de adicionar a validação, deve obter erros se está a introduzir um valor para um parâmetro que não cumprem a respectiva validação.

#### <a name="example-firstname"></a>Exemplo: *FirstName*

Neste exemplo, é possível definir as propriedades de parâmetro de cadeia, *FirstName*.

![Parâmetros do script - cadeia](./media/run-scripts/RS-parameters-string.png)


A secção de validação do **propriedades de parâmetro de Script** diálogo contém os campos seguintes para utilização:

- **Comprimento mínimo** - mínimo número de carateres da *FirstName* campo.
- **Comprimento máximo**- máximo número de carateres da *FirstName* campo
- **RegEx** - curto para *expressão Regular*. Para obter mais informações sobre como utilizar a expressão Regular, consulte a secção seguinte, *validação de expressão Regular utilizando*.
- **Erro personalizado** - útil para adicionar a sua própria mensagem de erro personalizada que substitui quaisquer mensagens de erro de validação do sistema.

#### <a name="using-regular-expression-validation"></a>Utilizando a validação de expressão Regular

Uma expressão regular é um formato compacto de programação para a verificação de uma cadeia de carateres em relação a uma validação codificada. Por exemplo, pode procurar a ausência de um caráter alfabético capital no *FirstName* campo colocando `[^A-Z]` no *RegEx* campo.

A expressão regular de processamento para esta caixa de diálogo é suportada pelo .NET Framework. Para obter orientações sobre como utilizar expressões regulares, consulte [expressão Regular .NET](https://docs.microsoft.com/dotnet/standard/base-types/regular-expressions). 


## <a name="script-examples"></a>Exemplos de script

Seguem-se alguns exemplos que ilustram scripts que pode querer utilizar com esta capacidade.

### <a name="create-a-new-folder-and-file"></a>Criar uma nova pasta e ficheiro

Este script cria uma nova pasta e um ficheiro dentro da pasta, a entrada de nomenclatura especificada.

``` powershell
Param(
[Parameter(Mandatory=$True)]
[string]$FolderName,
[Parameter(Mandatory=$True)]
[string]$FileName,
)

New-Item $FolderName -type directory
New-Item $FileName -type file
```

### <a name="get-os-version"></a>Obter a versão do SO

Este script utiliza o WMI para consultar a máquina para a versão do SO.

``` powershell
Write-Output (Get-WmiObject -Class Win32_operatingSystem).Caption
```

## <a name="run-a-script"></a>Executar um script

Depois de um script é aprovado, podem ser executada em relação a uma coleção ou um único dispositivo. Depois de inicia a execução do script, é iniciado rapidamente através de um sistema de alta prioridade que Escalamento vezes dentro de uma hora. Em seguida, são apresentados os resultados do script a utilizar um sistema de mensagens de estado.

Para selecionar uma coleção de alvos de script:

1. Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.
2. Nos ativos e compatibilidade área de trabalho, clique em **coleções de dispositivos**.
3. No **coleções de dispositivos** lista, clique na coleção de dispositivos nos quais pretende executar o script.
4. Selecione uma coleção à sua escolha, clique em **executar Script**.
5. No **Script** página do **executar Script** assistente, escolha um script da lista. Apenas aprovados scripts são apresentados.
6. Clique em **seguinte**e, em seguida, conclua o assistente.

>[!IMPORTANT]
>Se um script não é executado, por exemplo porque um dispositivo de destino é desativado durante a período de tempo de uma hora, deve executá-la novamente.

### <a name="target-machine-execution"></a>Execução da máquina de destino

O script é executado como o *sistema* ou *computador* conta nas clientes de destino. Esta conta tem acesso à rede limitado. Qualquer acesso à sistemas remotos e localizações pelo script tem de ser aprovisionado em conformidade.

## <a name="script-monitoring"></a>Script de monitorização

Depois de terem iniciado a executar um script numa coleção de dispositivos, utilize o procedimento seguinte para monitorizar a operação. A partir da versão 1710, são ambos poderá monitorizar um script em tempo real, como a ser executada e também pode regressar a um relatório para uma execução de executar o Script especificado. <br>

![Monitor de script - estado de execução do Script](./media/run-scripts/RS-monitoring-three-bar.png)

1. Na consola do Configuration Manager, clique em **monitorização**.
2. No **monitorização** área de trabalho, clique em **Script estado**.
3. No **Script estado** lista, poderá ver os resultados para cada script executado nos dispositivos cliente. Um código de saída do script de **0** normalmente indica que o script é executado com êxito.
    - Saída de scripts a partir do Configuration Manager 1802, será truncada para 4 KB para permitir a melhor experiência de apresentação.  <!--510013-->
      ![Monitor de script - truncada de Script](./media/run-scripts/Script-monitoring-truncated.png) 

## <a name="script-output"></a>Resultado do script

- A partir do Configuration Manager versão 1802, o resultado do script devolve utilizando a formatação JSON. Este formato consistentemente devolve um resultado de script legível. 
- Scripts que obter um resultado desconhecido ou onde o cliente estiver offline, não irão mostrar no conjunto de dados ou de gráficos. <!--507179-->
- Evite a devolução de saída do script de grandes dimensões, uma vez que será truncado para 4 KB. <!--508488-->
- Algumas funcionalidades com script de saída de formatação não está disponível quando em execução 1802 de versão do Configuration Manager ou posterior com uma versão de nível inferior do cliente. <!--508487-->
    - Quando tiver um cliente de Configuration Manager de pre-1802, obter um resultado de cadeia.
    -  Para o Configuration Manager versão de cliente 1802 e acima, obter formatação JSON.
        - Por exemplo, poderá obter resultados que afirmam texto uma versão de cliente e "TEXT" (o resultado é rodeado entre aspas duplas) na outra versão, o que irá ser colocada no gráfico como duas categorias diferentes.
        - Se precisar de contornar este comportamento, considere executar script contra duas coleções diferentes. Uma com a pré-1802 os clientes e outra com 1802 e superior. Em alternativa, pode converter um objeto de enumeração para um valor de cadeia em scripts para que estes são apresentados corretamente no JSON de formatação. 
- Converter um objeto de enumeração para um valor de cadeia em scripts para que estes são apresentados corretamente no JSON de formatação. <!--508377--> ![Converter o objeto de enumeração para um valor de sting](./media/run-scripts/enum-tostring-JSON.png)



## <a name="see-also"></a>Consulte Também

- [Configurar a administração baseada em funções para o System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md)
- [Noções básicas sobre a administração baseada em funções](/sccm/core/understand/fundamentals-of-role-based-administration)
