---
title: Criar e executar scripts
titleSuffix: Configuration Manager
description: Criar e executar scripts do Powershell nos dispositivos cliente.
ms.custom: na
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
caps.latest.revision: "14"
caps.handback.revision: "0"
author: BrucePerlerMS
ms.author: bruceper
manager: angrobe
ms.openlocfilehash: 964f6d39c4c1afc82ff4336821740923d27cd569
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 11/21/2017
---
# <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>Criar e executar scripts do PowerShell a partir da consola do Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

-Por agora integrado melhor a capacidade de executar Scripts do Powershell com o System Center Configuration Manager. PowerShell tem a vantagem de criar sofisticadas, scripts automatizados, compreendeu e partilhados com uma Comunidade maior. Os scripts de simplificam a criação de ferramentas personalizadas para administrar o software e permitem-lhe realizar tarefas criar rapidamente, permitindo-lhe obter tarefas grandes feitas de forma mais fácil e mais consistente.

Esta integração no System Center Configuration Manager, pode utilizar o *executar Scripts* funcionalidade fazer o seguinte:

- Criar e editar os scripts para utilização com o Configuration Manager.
- Gerir a utilização de script através de funções e âmbitos de segurança  
- Executar scripts em coleções ou individuais no local geridos Windows PCs.
- Obter resultados de script agregados rápida dos dispositivos cliente.
- Monitorizar a execução do script e ver relatórios de resultados da saída do script.

>[!IMPORTANT]
>Tendo em conta a potência de scripts, iremos relembrá-intencional e cuidado com a respetiva utilização. Criámos proteções adicionais para o ajudar a; segregated funções e âmbitos. Lembre-se de que validar a precisão dos scripts antes de executá-los e confirmar são de uma origem fidedigna, para impedir a execução do script indesejados. Ser mindful de caracteres expandidas ou outro obfuscation e informe-se sobre como proteger scripts.

>[!TIP]
>Introduzido com a versão 1706, Scripts do PowerShell é uma funcionalidade de pré-lançamento. Para ativar scripts, consulte [no System Center Configuration Manager de funcionalidades de pré-lançamento](/sccm/core/servers/manage/pre-release-features).

## <a name="prerequisites"></a>Pré-requisitos

- Para executar scripts do PowerShell, o cliente deve executar o PowerShell versão 3.0 ou posterior. No entanto, se um script executa contém funcionalidade de uma versão posterior do PowerShell, o cliente em que executa o script tem de executar essa versão do PowerShell.
- Clientes do Configuration Manager tem de executar o cliente a partir da versão 1706 ou posterior para executar scripts.
- Para utilizar scripts, tem de ser um membro da função de segurança adequado do Configuration Manager.
- Para importar e criar scripts - a conta tem de ter **criar** permissões para **SMS Scripts** no **administrador total** função de segurança.
- Para aprovar ou recusar scripts - a conta tem de ter **aprovar** permissões para **SMS Scripts** no **administrador total** função de segurança.
- Para executar scripts - a conta tem de ter **executar Script** permissões para **coleções** no **Gestor de definições de compatibilidade** função de segurança.

Para mais informações sobre funções de segurança do Configuration Manager, consulte [Noções básicas da administração baseada em funções](/sccm/core/understand/fundamentals-of-role-based-administration).

## <a name="limitations"></a>Limitações

Executadas Scripts atualmente suporta:

- Linguagens de scripts: PowerShell
- Tipos de parâmetro: número inteiro e cadeia

## <a name="run-script-authors-and-approvers"></a>Execução de Script de autores e aprovadores

Executar utiliza Scripts o conceito de *script autores* e *script aprovadores* como funções separadas para implementação e a execução de um script. Com as funções de autor e aprovador separadas permite uma verificação de processo importante para a ferramenta de elevado desempenho que está a executar Scripts.

### <a name="scripts-roles-control"></a>Controlo de funções de scripts

Por predefinição, os utilizadores não podem aprovar um script que tenham criado. Uma vez scripts são poderosa, versátil e podem ser implementados em vários dispositivos, pode dividir as funções entre a pessoa que cria o script e a pessoa que aprove o script. Estas funções dar um nível adicional de segurança contra a execução de um script sem supervisão. Pode desativar esta aprovação secundária, para facilitar a testar.

### <a name="approve-or-deny-a-script"></a>Aprovar ou recusar um script

Scripts devem ser aprovados, pelo *script aprovador* função, antes de estes serem executados. Para aprovar um script:

1. Na consola do Configuration Manager, clique em **Biblioteca de Software**.
2. No **biblioteca de Software** área de trabalho, clique em **Scripts**.
3. No **Script** lista, selecione o script que pretende aprovar ou recusar e, em seguida, no **home page** separador o **Script** , clique em **aprovar/negação**.
4. No **aprovar ou negar o script** caixa de diálogo, selecione **aprovar** ou **negar** para o script e, opcionalmente, introduza um comentário sobre a sua decisão.  Se negar um script, não pode ser executado nos dispositivos cliente. <br>
![Script - aprovação](./media/run-scripts/RS-approval.png)
5. Conclua o assistente. No **Script** lista, verá o **estado de aprovação** alteração de coluna consoante a ação que demorou.

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
1. Conclua o assistente. O novo script é apresentado no **Script** lista com um Estado de **aguardar aprovação**. Antes de poder executar este script nos dispositivos cliente, terá de o aprovar.

## <a name="script-parameters"></a>Parâmetros do script
*(Introduzida com a versão 1710)*  
Adicionar parâmetros a um script fornece uma maior flexibilidade para o seu trabalho. A seguir descreve a capacidade de atual a funcionalidade de executar Scripts com parâmetros do script para; *Cadeia*, *número inteiro* tipos de dados. Apresenta uma lista de valores predefinidas também está disponível. Se o script tem o tipos de dados não suportado, receberá um aviso.

No **criar Script** caixa de diálogo, clique em **parâmetros do Script** em **Script**.

Cada um dos parâmetros do script tem a suas próprias caixa de diálogo para adicionar mais detalhes e validação.

### <a name="parameter-validation"></a>Validação dos parâmetros

Cada parâmetro no script tem um **propriedades de parâmetro de Script** caixa de diálogo para adicionar a validação para este parâmetro. Depois de adicionar a validação, deve obter erros se está a introduzir um valor para um parâmetro que não cumprem a respectiva validação.

#### <a name="example-firstname"></a>Exemplo: Nome próprio

Neste exemplo, é possível definir as propriedades de parâmetro de cadeia, *FirstName*. Tenha em atenção o campo opcional para **personalizada erro**. Este campo é útil para adicionar orientações para o utilizador sobre o campo específico e as orientações para o utilizador sobre a sua interação com o parâmetro de cadeia, *FirstName* neste caso.

![Parâmetros do script - cadeia](./media/run-scripts/RS-parameters-string.png)

## <a name="script-examples"></a>Exemplos de script

Seguem-se alguns exemplos que ilustram scripts que pode querer utilizar com esta capacidade.

### <a name="create-a-folder"></a>Crie uma pasta

``` powershell
New-Item "c:\scripts" -type folder name
```

### <a name="create-a-file"></a>Criar um ficheiro

```powershell
New-Item "c:\scripts\new_file.txt" -type file name
```

### <a name="ping-a-given-computer"></a>Ping num computador especificado

Este script utiliza uma cadeia e utiliza-o como um parâmetro para um *ping* operação.

``` powershell
Param
(
 [String][Parameter(Mandatory=$True, Position=1)] $Computername
)

Ping $Computername
```

### <a name="get-battery-status"></a>Obter o estado de bateria

Este script utiliza o WMI para consultar a máquina para o estado da bateria.

``` powershell
Write-Output (Get-WmiObject -Class Win32_Battery).BatteryStatus

```

## <a name="run-a-script"></a>Executar um script

Depois de um script é aprovado, podem ser executada em relação a uma coleção que escolher. Depois de inicia a execução do script, é iniciada, rapidamente, através de um sistema de alta prioridade e é executado dentro de uma hora. São apresentados os resultados do script a utilizar um sistema de mensagens de estado, mais lento.

1. Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.
2. Nos ativos e compatibilidade área de trabalho, clique em **coleções de dispositivos**.
3. No **coleções de dispositivos** lista, clique na coleção de dispositivos nos quais pretende executar o script.
4. No **home page** separador o **todos os sistemas** , clique em **executar Script**.
5. No **Script** página do **executar Script** assistente, escolha um script da lista. Apenas aprovados scripts são apresentados.
6. Clique em **seguinte**e, em seguida, conclua o assistente.

>[!IMPORTANT]
>Se um script não é executado, por exemplo porque um cliente de destino estiver desligado, na hora de um período de tempo, deve executá-la novamente.

### <a name="target-machine-execution"></a>Execução da máquina de destino
O script é executado como o *sistema* ou *computador* conta nas clientes de destino. Esta conta tem acesso à rede limitado. Qualquer acesso à sistemas remotos e localizações pelo script tem de ser aprovisionado em conformidade.

## <a name="work-flow-and-monitoring"></a>Fluxo de trabalho e monitorização

Eis o aspeto executar Scripts como um fluxo de trabalho; criar, aprovar, executar e, monitorizar.

![Executar Scripts - fluxo de trabalho](./media/run-scripts/RS-run-scripts-work-flow.png)

### <a name="script-monitoring"></a>Script de monitorização

Depois de terem iniciado a executar um script numa coleção de dispositivos, utilize o procedimento seguinte para monitorizar a operação. A partir da versão 1710, é ambos poderá monitorizar um script em tempo real, ser executada e também pode regressar a um relatório para uma execução de executar o Script especificado.

1. Na consola do Configuration Manager, clique em **monitorização**.
2. No **monitorização** área de trabalho, clique em **Script estado**. ![Monitor de script - estado de execução do Script](./media/run-scripts/RS-monitoring-three-bar.png)
3. No **Script estado** lista, poderá ver os resultados para cada script executado nos dispositivos cliente. Um código de saída do script de **0** normalmente indica que o script é executado com êxito.

## <a name="see-also"></a>Consulte Também

- [Configurar a administração baseada em funções para o System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md)
- [Noções básicas sobre a administração baseada em funções](/sccm/core/understand/fundamentals-of-role-based-administration)
