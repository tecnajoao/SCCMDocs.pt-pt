---
title: Criar e executar scripts
titleSuffix: Configuration Manager
description: Criar e executar scripts do Powershell nos dispositivos cliente.
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6d9b65629e000814f80876747e1148d450c2080b
ms.sourcegitcommit: fd16fc2b681608fd6def5bad2cedffbcd1f2423a
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/18/2019
ms.locfileid: "56405663"
---
# <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>Criar e executar scripts do PowerShell a partir da consola do Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

<!--1236459--> System Center Configuration Manager tem uma capacidade integrada para executar scripts do Powershell. PowerShell tem a vantagem de criar sofisticadas, scripts automatizados que estão compreendidos e partilhados com uma maior Comunidade. Os scripts simplificam a criação de ferramentas personalizadas para administrar o software e permitem que realizar tarefas mundanas rapidamente, permitindo-lhe obter o grande trabalho mais fácil e mais consistente.  

> [!TIP]  
> Esse recurso foi introduzido pela primeira vez na versão 1706 como um [funcionalidade de pré-lançamento](/sccm/core/servers/manage/pre-release-features). A partir da versão 1802, esta funcionalidade já não é uma funcionalidade de pré-lançamento.  


> [!Note]  
> O Configuration Manager não permite esta funcionalidade opcional por predefinição. Tem de ativar esta funcionalidade antes de o utilizar. Para obter mais informações, consulte [ativar funcionalidades opcionais de atualizações](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


Com esta integração no System Center Configuration Manager, pode utilizar o *executar Scripts* funcionalidade para efetue os seguintes procedimentos:

- Criar e editar scripts para utilização com o System Center Configuration Manager.
- Gerir a utilização de script através de funções e âmbitos de segurança. 
- Executar scripts em coleções ou individual no local geridos Windows PCs.
- Obtenha os resultados do script de agregados rápida dos dispositivos cliente.
- Monitorizar a execução do script e ver relatórios de resultados da saída do script.

>[!WARNING]
>Tendo em conta o poder de scripts, podemos lembrá-lo de ser intencional e cuidado com a utilização das mesmas. Criámos salvaguardas adicionais para ajudá-lo; âmbitos e funções segregadas. Certifique-se de que validar a precisão dos scripts antes de executá-los e confirmar que sejam provenientes de uma origem fidedigna, para impedir a execução de scripts não-intencionais. Estar atento a caracteres estendidos ou outra ofuscação e informe-se sobre como proteger a scripts. [Saiba mais sobre a segurança de script do PowerShell](/sccm/apps/deploy-use/learn-script-security)

## <a name="prerequisites"></a>Pré-requisitos

- Para executar scripts do PowerShell, o cliente tem de executar o PowerShell versão 3.0 ou posterior. No entanto, se um script que execute contém a funcionalidade de uma versão posterior do PowerShell, o cliente no qual executa o script tem de executar essa versão do PowerShell.
- Clientes do Configuration Manager tem de executar o cliente da versão 1706 ou posterior para executar scripts.
- Uso de scripts, tem de ser membro da função de segurança adequado do Configuration Manager.
- Para importar e criar scripts - sua conta tem de ter **Create** permissões para **Scripts do SMS**.
- Para aprovar ou recusar scripts - sua conta tem de ter **aprovar** permissões para **Scripts do SMS**.
- A execução de scripts - sua conta tem de ter **executar Script** permissões para **coleções**.

Para obter mais informações sobre funções de segurança do Configuration Manager:</br>
[Âmbitos de segurança para executar scripts](#BKMK_Scopes)</br>
[Funções de segurança para executar scripts](#BKMK_ScriptRoles)</br>
[Noções básicas da administração baseada em funções](/sccm/core/understand/fundamentals-of-role-based-administration).

## <a name="limitations"></a>Limitações

Executar Scripts atualmente suporta:

- Linguagens de script: PowerShell
- Tipos de parâmetro: número inteiro, a cadeia de caracteres e a lista.


>[!WARNING]
>Lembre-se de que, ao utilizar parâmetros, ela abre uma área de superfície potencial risco de ataque de injeção de PowerShell. Existem várias formas de reduzir e a resolver o problema como o uso de expressões regulares para validar a entrada de parâmetro ou usando predefinidos de parâmetros. Uma melhor prática é não incluir a segredos em seus scripts do PowerShell (não palavras-passe, etc.). [Saiba mais sobre a segurança de script do PowerShell](/sccm/apps/deploy-use/learn-script-security) <!--There are external tools available to validate your PowerShell scripts such as the [PowerShell Injection Hunter](https://www.powershellgallery.com/packages/InjectionHunter/1.0.0) tool. -->


## <a name="run-script-authors-and-approvers"></a>Execução de Script de autores e aprovadores

Executar utiliza Scripts o conceito de *autores de script* e *script aprovadores* como funções separadas para implementação e execução de um script. Ter as funções de autor e aprovador separadas permite a uma verificação de processo importante para a ferramenta poderosa que está a executar Scripts. Existe um adicionais *concorrentes do script* função que permite a execução de scripts, mas não a criação ou a aprovação de scripts. Ver [criar funções de segurança para os scripts](#BKMK_ScriptRoles).

### <a name="scripts-roles-control"></a>Controlo de funções de scripts

Por predefinição, os utilizadores não podem aprovar um script que tenham criado. Como os scripts são poderosas, versátil e potencialmente ser implantado em vários dispositivos, pode separar as funções entre a pessoa que cria o script e a pessoa que aprova o script. Estas funções oferecem um nível adicional de segurança contra a execução de um script sem supervisão. É possível desativar a aprovação secundária, para facilitar o teste.

### <a name="approve-or-deny-a-script"></a>Aprovar ou recusar um script

Scripts devem ser aprovados, pelo *aprovador de scripts* função, antes de podem ser executadas. Para aprovar um script:

1. Na consola do Configuration Manager, clique em **Biblioteca de Software**.
2. Na **biblioteca de Software** área de trabalho, clique em **Scripts**.
3. Na **Script** lista, selecione o script que pretende aprovar ou negar e, em seguida, no **home page** separador o **Script** , clique em **aprovar/negar**.
4. Na **aprovar ou recusar scriipt** caixa de diálogo, selecione **aprovar**, ou **negar** para o script. Opcionalmente, introduza um comentário sobre sua decisão.  Se negar um script, não pode ser executado nos dispositivos cliente. <br>
![Script - aprovação](./media/run-scripts/RS-approval.png)
1. Conclua o assistente. Na **Script** listar, verá o **estado de aprovação** alteração de coluna consoante a ação que realizar.

### <a name="allow-users-to-approve-their-own-scripts"></a>Permitir que os usuários aprovar os próprios scripts

Esta aprovação é usada principalmente para a fase de teste de desenvolvimento do script.

1. Na consola do Configuration Manager, clique em **Administração**.
2. Na área de trabalho **Administração** , expanda **Configuração do Site**e clique em **Sites**.
3. Na lista de sites, escolha o seu site e, em seguida, no **home page** separador a **Sites** , clique em **definições de hierarquia**.
4. Na **gerais** separador da **propriedades de definições de hierarquia** caixa de diálogo caixa, desmarque a caixa de verificação **autores de scripts exigem aprovador de scripts adicionais**.

>[!IMPORTANT]
>Como melhor prática, não deve permitir que um autor de script aprovar os próprios scripts. Só deve ser permitido num ambiente de laboratório. Tenha em atenção o impacto potencial de alterar esta definição num ambiente de produção.

## <a name="security-scopes"></a>Âmbitos de segurança
*(Introduzido com a versão 1710)*  
Executar âmbitos de segurança de usos de Scripts, uma funcionalidade existente do Configuration Manager, para controlar os scripts de criação e execução através da atribuição de etiquetas que representam os grupos de utilizadores. Para obter mais informações sobre como utilizar âmbitos de segurança, consulte [configurar a administração baseada em funções para o System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).

## <a name="bkmk_ScriptRoles"></a> Criar funções de segurança para os scripts
As funções de três segurança utilizadas para executar scripts não são criadas por predefinição no Configuration Manager. Para criar o script concorrentes, autores de scripts e funções de aprovadores de script, siga os passos descritos.

1. Na consola do Configuration Manager, aceda a **Administration** >**segurança** >**funções de segurança**
2. Com o botão direito numa função e clique em **cópia**. A função de que copiar tem as permissões já atribuídas. Certifique-se de que realizar apenas as permissões que pretende. 
3. Atribua a função personalizada uma **Name** e uma **Descrição**. 
4. Atribua a função de segurança com as permissões descritas abaixo.  

### <a name="security-role-permissions"></a>Permissões de função de segurança  

**Nome da função**: Script concorrentes  
- **Descrição**: Estas permissões ativar esta função apenas executar scripts que foram anteriormente criadas e aprovadas por outras funções.  
- **Permissões:** Certifique-se de que o seguinte está definido como **Sim**.  

|Categoria|Permissão|Estado|
|---|---|---|
|Coleção|Executar Script|Sim|
|Site|Leitura|Sim|
|Scripts SMS|Leitura|Sim|


**Nome da função**: Autores de script  
- **Descrição**: Estas permissões ativar esta função para scripts de autor, mas não pode aprovar ou executá-los.  
- **Permissões**: Certifique-se de que as seguintes permissões são definidas.
 
|Categoria|Permissão|Estado|
|---|---|---|
|Coleção|Executar Script|Não|
|Site|Leitura|Sim|
|Scripts SMS|Criar|Sim|
|Scripts SMS|Leitura|Sim|
|Scripts SMS|Eliminar|Sim|
|Scripts SMS|Modificar|Sim|


**Nome da função**: Aprovadores de script  
- **Descrição**: Estas permissões ativar esta função aprovar scripts, mas não é possível criar ou executá-los.  
- **Permissões:** Certifique-se de que as seguintes permissões são definidas.  

|Categoria|Permissão|Estado|
|---|---|---|
|Coleção|Executar Script|Não|
|Site|Leitura|Sim|
|Scripts SMS|Leitura|Sim|
|Scripts SMS|Aprovar|Sim|
|Scripts SMS|Modificar|Sim|

     
**Exemplo de permissões de Scripts de SMS para a função de autores de script**  

 ![Exemplo de permissões de Scripts de SMS para a função de autores de script](./media/run-scripts/script_authors_permissions.png)

   

## <a name="create-a-script"></a>Criar um script

1. Na consola do Configuration Manager, clique em **Biblioteca de Software**.
2. Na **biblioteca de Software** área de trabalho, clique em **Scripts**.
3. Sobre o **home page** separador a **criar** , clique em **criar Script**.
4. Na **Script** página de Create **Script** assistente, configure as seguintes definições:
    - **Nome do script** -introduza um nome para o script. Embora possa criar vários scripts com o mesmo nome, utilizar nomes duplicados torna mais difícil localizar o script que precisa na consola do Configuration Manager.
    - **Linguagem de script** -atualmente, apenas os scripts do PowerShell são suportados.
    - **Importar** -importar um script do PowerShell para a consola. O script é apresentado na **Script** campo.
    - **Limpar** -remove o script atual a partir do campo de Script.
    - **Script** -apresenta o script atualmente importado. Pode editar o script neste campo, se necessário.
5. Conclua o assistente. O script novo é apresentado na **Script** lista com o estado **aguardar aprovação**. Antes de poder executar este script nos dispositivos cliente, terá de o aprovar. 

> [!IMPORTANT]
> Evite scripts um reinício do dispositivo ou um reinício do agente do Configuration Manager, quando utilizar a funcionalidade de executar Scripts. Se o fizer, poderia levar a um estado contínuo de ser reiniciado. Se for necessário, há aprimoramentos para a funcionalidade de notificação de cliente que permitem dispositivos reiniciar, a partir do Configuration Manager versão 1710. O [pendente da coluna de reinício](/sccm/core/clients/manage/manage-clients#Restart-clients) pode ajudar a identificar dispositivos que necessitam de um reinício. 
> <!--SMS503978  -->

## <a name="script-parameters"></a>Parâmetros do script
*(Introduzido com a versão 1710)*  
Adicionar parâmetros a um script fornece maior flexibilidade para o seu trabalho. A seguir descreve a capacidade atual do recurso de executar Scripts com parâmetros de script para; *Cadeia de caracteres*, *inteiro* tipos de dados. Listas de valores predefinidos também estão disponíveis. Se o script tem não suportados tipos de dados, receberá um aviso.

Na **criar Script** caixa de diálogo, clique em **parâmetros do Script** sob **Script**.

Cada um dos parâmetros do seu script tem sua própria caixa de diálogo para adicionar mais detalhes e a validação.

>[!IMPORTANT]
> Valores de parâmetro não podem conter um apóstrofe. </br></br>
> Há um problema conhecido no Configuration Manager versão 1802 onde parâmetros com os espaços não de forem transmitidos para o script corretamente. Se um espaço é utilizado no parâmetro, apenas o primeiro item no parâmetro é passado para o script e tudo o que, depois do espaço não é passado. Os administradores podem criar scripts contornar isso substituindo os caracteres alternativos para os espaços e convertê-los ou com outros métodos.


### <a name="parameter-validation"></a>Validação de parâmetro

Cada parâmetro no script tem um **propriedades do parâmetro de Script** caixa de diálogo para adicionar validação para esse parâmetro. Depois de adicionar validação, obterá erros se estiver participando um valor para um parâmetro que não possui a respectiva validação.

#### <a name="example-firstname"></a>Exemplo: *FirstName*

Neste exemplo, é possível definir as propriedades do parâmetro de cadeia de caracteres *FirstName*.

![Parâmetros do script - cadeia de caracteres](./media/run-scripts/RS-parameters-string.png)


A secção de validação do **propriedades do parâmetro de Script** caixa de diálogo contém os seguintes campos para a sua utilização:

- **Comprimento mínimo** – mínimo número de carateres da *FirstName* campo.
- **Comprimento máximo**- máximo número de carateres da *FirstName* campo
- **RegEx** - abreviação de *expressão Regular*. Para obter mais informações sobre como utilizar a expressão Regular, consulte a secção seguinte, *validação de expressão Regular utilizando*.
- **Erro personalizado** - útil para adicionar sua própria mensagem de erro personalizada que substitui quaisquer mensagens de erro de validação do sistema.

#### <a name="using-regular-expression-validation"></a>Utilizar validação de expressão Regular

Uma expressão regular é um formato compacto de programação para a verificação de uma cadeia de caracteres em relação a uma validação codificada. Por exemplo, será possível verificar a ausência de um caractere alfabético capital no *FirstName* campo colocando `[^A-Z]` no *RegEx* campo.

A expressão regular de processamento para esta caixa de diálogo é suportada pelo .NET Framework. Para obter orientações sobre como usar expressões regulares, veja [expressão Regular .NET](https://docs.microsoft.com/dotnet/standard/base-types/regular-expressions). 


## <a name="script-examples"></a>Exemplos de script

Aqui estão alguns exemplos que ilustram os scripts que pode querer utilizar com esta capacidade.

### <a name="create-a-new-folder-and-file"></a>Criar uma nova pasta e ficheiro

Este script cria uma nova pasta e um arquivo dentro da pasta, dada sua entrada de nomenclatura.

``` powershell
Param(
[Parameter(Mandatory=$True)]
[string]$FolderName,
[Parameter(Mandatory=$True)]
[string]$FileName
)

New-Item $FolderName -type directory
New-Item $FileName -type file
```

### <a name="get-os-version"></a>Obter a versão do SO

Este script utiliza o WMI para consultar a máquina para a sua versão de SO.

``` powershell
Write-Output (Get-WmiObject -Class Win32_operatingSystem).Caption
```

## <a name="run-a-script"></a>Executar um script

Depois de um script for aprovado, ele pode ser executado num único dispositivo ou uma coleção. Assim que começa a execução do seu script, ele é iniciado rapidamente através de um sistema de alta prioridade que vezes horizontalmente numa hora. Os resultados do script, em seguida, são devolvidos a utilizar um sistema de mensagem de estado.

Para selecionar uma coleção de destinos para o seu script:

1. Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.
2. Nos ativos e área de trabalho de conformidade, clique em **coleções de dispositivos**.
3. Na **coleções de dispositivos** lista, clique na coleção de dispositivos em que pretende executar o script.
4. Selecione uma coleção de sua escolha, clique em **executar Script**.
5. Sobre o **Script** página do **executar Script** assistente, escolher um script a partir da lista. Apenas os scripts aprovados são apresentados.
6. Clique em **seguinte**e, em seguida, conclua o assistente.

>[!IMPORTANT]
>Se um script não é executado, por exemplo, uma vez que um dispositivo de destino é desativado durante a período de tempo de uma hora, tem de executá-lo novamente.

### <a name="target-machine-execution"></a>Execução da máquina de destino

O script é executado como a *system* ou *computador* conta em clientes de destino. Esta conta tem acesso de rede limitado. Qualquer acesso a sistemas remotos e locais pelo script tem de ser aprovisionado em conformidade.

## <a name="script-monitoring"></a>Script de monitorização

Depois de ter iniciado a execução de um script numa coleção de dispositivos, utilize o procedimento seguinte para monitorar a operação. A partir da versão 1710, são ambos capaz de monitorar um script em tempo real à medida que ele seja executado e também podem retornar a um relatório para uma determinada execução de executar o Script. <br>

![Monitor de script - estado de execução do Script](./media/run-scripts/RS-monitoring-three-bar.png)

1. Na consola do Configuration Manager, clique em **monitorização**.
2. Na **monitorização** área de trabalho, clique em **estado do Script**.
3. Na **estado do Script** lista, exibir os resultados para cada script tiver executado nos dispositivos cliente. Um código de saída do script **0** normalmente indica que o script foi executado com êxito.
    - Saída do script a partir na versão 1802 do Gestor de configuração, será truncada para 4 KB para permitir a melhor experiência de apresentação.  <!--510013-->
      ![Monitor de script - Script truncada](./media/run-scripts/Script-monitoring-truncated.png) 

## <a name="script-output"></a>Saída do script

- A partir do Configuration Manager versão 1802, saída do script devolve usando a formatação do JSON. Este formato consistentemente devolve uma saída de script legível. 
- Scripts que obter um resultado desconhecido ou onde o cliente estava offline, não será mostrada no gráficos ou do conjunto de dados. <!--507179-->
- Evite a devolução de saída do script grandes, uma vez que será truncado para 4 KB. <!--508488-->
- Algumas funcionalidades com o script de saída de formatação não está disponível ao executar o Configuration Manager versão 1802 ou posterior com uma versão anterior do cliente. <!--508487-->
    - Quando tiver um cliente do Configuration Manager de pré-1802, obtém uma saída de cadeia de caracteres.
    -  Para o Configuration Manager versão 1802 do cliente e acima, obtenha a formatação do JSON.
        - Por exemplo, poderá obter resultados que dizem o texto numa versão de cliente e de "TEXT" (a saída fica entre aspas duplas) em outra versão, que será colocado num gráfico como duas categorias diferentes.
        - Se precisar de contornar este comportamento, considere executar script em relação a duas coleções diferentes. Uma com a pré-1802 os clientes e outro com 1802 e superior. Em alternativa, pode converter um objeto de enumeração para um valor de cadeia de caracteres em scripts para que eles corretamente são apresentados no JSON de formatação. 
- Converta um objeto de enumeração para um valor de cadeia de caracteres em scripts para que eles corretamente são apresentados no JSON de formatação. <!--508377--> ![Converter o objeto de enumeração para um valor de sting](./media/run-scripts/enum-tostring-JSON.png)



## <a name="see-also"></a>Consulte Também

- [Configurar a administração baseada em funções para o System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md)
- [Noções básicas sobre a administração baseada em funções](/sccm/core/understand/fundamentals-of-role-based-administration)
