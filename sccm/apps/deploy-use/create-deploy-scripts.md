---
title: Criar e executar scripts
titleSuffix: Configuration Manager
description: Criar e executar scripts nos dispositivos cliente com o Configuration Manager.
ms.custom: na
ms.date: 09/15/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
caps.latest.revision: "14"
caps.handback.revision: "0"
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.openlocfilehash: d1cbb760c6e40c21b97d0227ff93613066189d4b
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>Criar e executar scripts do PowerShell a partir da consola do Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

No Configuration Manager, além de utilizar pacotes e programas para implementar scripts, pode utilizar a seguinte funcionalidade para efetuar as seguintes ações:

- Importar Scripts do PowerShell para o Configuration Manager
- Editar os scripts a partir da consola do Configuration Manager (para apenas scripts não assinados)
- Scripts de marca como aprovado ou negado, para melhorar a segurança
- Executar scripts em coleções de computadores de cliente do Windows e no local geridos Windows PCs. Não implementa scripts, em vez disso, são executados quase imediatamente nos dispositivos cliente.
- Examine os resultados devolvidos pelo script na consola do Configuration Manager.

>[!TIP]
>Nesta versão do Configuration Manager, scripts são uma funcionalidade de pré-lançamento. Para ativar scripts, consulte [no System Center Configuration Manager de funcionalidades de pré-lançamento](/sccm/core/servers/manage/pre-release-features).

## <a name="prerequisites"></a>Pré-requisitos

Para executar scripts do PowerShell, o cliente deve executar o PowerShell versão 3.0 ou posterior. No entanto, se um script executa contém funcionalidade de uma versão posterior do PowerShell, o cliente em que executa o script tem de executar essa versão.

Clientes do Configuration Manager tem de executar o cliente a partir da versão 1706 ou posterior para executar scripts.

Para utilizar scripts, tem de ser um membro da função de segurança adequado do Configuration Manager.

- Para importar e criar scripts - a conta tem de ter **criar** permissões para **SMS Scripts** no **administrador total** função de segurança.
- Para aprovar ou negar scripts - a conta tem de ter **aprovar** permissões para **SMS Scripts** no **administrador total** função de segurança.
- Para executar scripts - a conta tem de ter **executar Script** permissões para **coleções** no **Gestor de definições de compatibilidade** função de segurança.

Para mais informações sobre funções de segurança do Configuration Manager, consulte [Noções básicas da administração baseada em funções](/sccm/core/understand/fundamentals-of-role-based-administration).

Por predefinição, os utilizadores não podem aprovar um script que tenham criado. Uma vez scripts são poderosa, versátil e podem ser implementados em vários dispositivos, pode dividir as funções entre a pessoa que cria o script e a pessoa que aprove o script. Estas funções dar um nível adicional de segurança contra a execução de um script sem supervisão. Pode desativar esta aprovação secundária, para facilitar a testar.

## <a name="allow-users-to-approve-their-own-scripts"></a>Permitir que os utilizadores aprovar os seus próprios scripts

1. Na consola do Configuration Manager, clique em **Administração**.
2. Na área de trabalho **Administração** , expanda **Configuração do Site**e clique em **Sites**.
3. Na lista de sites, selecione o site e, em seguida, no **home page** separador o **Sites** , clique em **definições de hierarquia**.
4. No **geral** separador do **propriedades de definições de hierarquia** diálogo caixa, desmarque a caixa de verificação **não permitir autores de script aprovar os seus próprios scripts**.

>[!IMPORTANT]
>Como melhor prática, não deve permitir que um autor de script para aprovar os seus próprios scripts. Só deve ser permitido num cenário de laboratório. . Considere cuidadosamente o impacto potencial da alteração desta definição num ambiente de produção.

## <a name="import-and-edit-a-script"></a>Importar e editar um script

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

### <a name="script-examples"></a>Exemplos de script

Seguem-se alguns exemplos que ilustram scripts que pode querer utilizar com esta capacidade.

#### <a name="create-a-folder"></a>Crie uma pasta

*Novo Item "c:\scripts"-nome de pasta do tipo*


#### <a name="create-a-file"></a>Criar um ficheiro

*Novo Item c:\scripts\new_file.txt-nome do tipo de ficheiro*


## <a name="approve-or-deny-a-script"></a>Aprovar ou recusar um script

Antes de poder executar um script, deve ser aprovado. Para aprovar um script:

1. Na consola do Configuration Manager, clique em **Biblioteca de Software**.
2. No **biblioteca de Software** área de trabalho, clique em **Scripts**.
3. No **Script** lista, selecione o script que pretende aprovar ou recusar e, em seguida, no **home page** separador o **Script** , clique em **aprovar/negação**.
4. No **aprovar ou negar** caixa de diálogo de script, **aprovar**, ou **negar** o script e, opcionalmente, introduza um comentário sobre a sua decisão. Se negar um script, não pode ser executado nos dispositivos cliente.
5. Conclua o assistente. No **Script** lista, verá o **estado de aprovação** alteração de coluna consoante a ação que demorou.

## <a name="run-a-script"></a>Executar um script
Depois de um script é aprovado, podem ser executada em relação a uma coleção que escolher.

1. Na consola do Configuration Manager, clique em **Ativos e Compatibilidade**.
2. Nos ativos e compatibilidade área de trabalho, clique em **coleções de dispositivos**.
3. No **coleções de dispositivos** lista, clique na coleção de dispositivos nos quais pretende executar o script.
4. No **home page** separador o **todos os sistemas** , clique em **executar Script**.
5. No **Script** página do **executar Script** assistente, escolha um script da lista. Apenas aprovados scripts são apresentados.
6. Clique em **seguinte**e, em seguida, conclua o assistente.

>[!IMPORTANT]
>O script é dado um período de tempo de uma hora para executar. Se não é executado (por exemplo, se o computador estiver desativado) neste período de tempo, deve executá-la novamente.

>[!IMPORTANT]
>O script é executado como conta de sistema ou o computador em que os clientes visados. Esta conta tem muito limitado de acesso à rede. Qualquer acesso à sistemas remotos e localizações pelo script têm de ser aprovisionado com isto em mente.

## <a name="next-steps"></a>Passos seguintes

Depois de executar um script em dispositivos cliente, utilize este procedimento para monitorizar o êxito da operação.

1. Na consola do Configuration Manager, clique em **monitorização**.
2. No **monitorização** área de trabalho, clique em **Script estado**.
3. No **Script estado** lista, poderá ver os resultados para cada script executado nos dispositivos cliente. Um código de saída do script de **0** normalmente indica que o script é executado com êxito.
