---
title: Ferramenta de limpeza da biblioteca de conteúdos
titleSuffix: Configuration Manager
description: Utilize a ferramenta de limpeza da biblioteca de conteúdos para remover o conteúdo órfão já não está associado a uma implementação do Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 226cbbb2-9afa-4e2e-a472-be989c0f0e11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7662ccba7b6f672888ab8d98954fb8cb70631fe4
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56134627"
---
# <a name="content-library-cleanup-tool"></a>Ferramenta de limpeza da biblioteca de conteúdos

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Utilize a ferramenta de linha de comandos de limpeza de biblioteca de conteúdos para remover o conteúdo já não está associado a nenhum pacote ou aplicação num ponto de distribuição. Este tipo de conteúdo é denominado *órfãos conteúdo*. Essa ferramenta substitui as versões mais antigas ferramentas semelhantes foram lançadas nos últimos produtos do Configuration Manager.  

A ferramenta só afeta o conteúdo no ponto de distribuição que especifica quando executar a ferramenta. A ferramenta não é possível remover o conteúdo da biblioteca de conteúdos no servidor do site.

Encontrar **ContentLibraryCleanup.exe** no `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` no servidor do site.



## <a name="requirements"></a>Requisitos  

- Apenas execute a ferramenta em relação a um único ponto de distribuição ao mesmo tempo.  

- Executá-lo diretamente no computador que aloja o ponto de distribuição para a limpeza, ou remotamente a partir de outro computador.  

- A conta de utilizador que executa a ferramenta tem de ter permissões igual a **administrador total** a função de segurança no Configuration Manager.  



## <a name="modes-of-operation"></a>Modos de funcionamento

Execute a ferramenta nos dois modos seguintes: [E se](#what-if-mode) e [eliminar](#delete-mode).

> [!Tip]  
> Começar com o *hipóteses* modo. Quando estiver satisfeito com os resultados, em seguida, execute a ferramenta no *eliminar* modo.  


### <a name="what-if-mode"></a>Modo de hipóteses   

Se não especificar o `/delete` parâmetro, a ferramenta é executada no modo de hipóteses. Este modo identifica os conteúdos que serão eliminados do ponto de distribuição.

- Ao serem executados neste modo, a ferramenta não elimina quaisquer dados.  

- A ferramenta escreve as informações de ficheiro de registo sobre o conteúdo que ele faria a excluir. Não lhe for pedido para confirmar a cada eliminação potencial.  


### <a name="delete-mode"></a>Eliminar modo   

Quando executa a ferramenta com o `/delete` parâmetro, a ferramenta é executada no modo de eliminação.

- Ao serem executados neste modo, o conteúdo órfão que encontrar no ponto de distribuição especificado pode ser eliminado da biblioteca de conteúdos do ponto de distribuição.  

- Antes de eliminar cada ficheiro, confirme que a ferramenta deverá eliminá-lo. Selecione **Y** para Sim, **N** para não, ou **Sim para todos os** para ignorar a outros prompts e eliminar conteúdo órfão tudo.  


### <a name="log-file"></a>Ficheiro de registo

Quando a ferramenta é executada no modo de ambos, este cria automaticamente um registo. Nomes de ficheiro de registo com as seguintes informações: 
- O modo da ferramenta é executada no  
- O nome do ponto de distribuição  
- A data e hora da operação  

Quando a ferramenta estiver concluída, ele abre automaticamente o ficheiro de registo no Windows. 

Por predefinição, a ferramenta escreve no ficheiro de registo para a pasta temporária da conta de utilizador que executa a ferramenta. Esta localização é no computador em que executou a ferramenta, que nem sempre é o destino da ferramenta. Utilize o `/log` parâmetro para redirecionar o ficheiro de registo para outro local, incluindo um compartilhamento de rede.



## <a name="run-the-tool"></a>Execute a ferramenta

Para executar a ferramenta: 

1. Abra uma linha de comandos como administrador. Altere o diretório para a pasta que contém **ContentLibraryCleanup.exe**.  

2. Introduza uma linha de comandos que inclui o necessários [parâmetros da linha de comandos](#bkmk_params)e quaisquer parâmetros opcionais que pretende utilizar.



## <a name="bkmk_params"></a> Parâmetros da linha de comandos  

Utilize estes parâmetros de linha de comando por qualquer ordem.   

### <a name="required-parameters"></a>Parâmetros necessários

|Parâmetro|Detalhes|
|---------|-------|
| `/dp <distribution point FQDN>`  | Especifique o nome de domínio completamente qualificado (FQDN) do ponto de distribuição para limpar. |
| `/ps <primary site FQDN>` | *Necessário* apenas quando a limpeza de conteúdo a partir de um ponto de distribuição num site secundário. A ferramenta se conectar ao site primário principal para executar consultas contra o fornecedor de SMS. Estas consultas permitem que a ferramenta de determinar o conteúdo que deve estar no ponto de distribuição. Em seguida, poderá identificar o conteúdo órfão para remover. Esta ligação para o site primário principal deve ser tomada para pontos de distribuição num site secundário porque os detalhes necessários não estão disponíveis diretamente a partir do site secundário.|
| `/sc <primary site code>`  | *Necessário* apenas quando a limpeza de conteúdo a partir de um ponto de distribuição num site secundário. Especifique o código do site do site primário principal. |

#### <a name="example-scan-and-log-what-content-it-would-delete-what-if"></a>Exemplo: Analisar e qual o conteúdo de registo excluísse (hipóteses)
`ContentLibraryCleanup.exe /dp server1.contoso.com`

#### <a name="example-scan-and-log-content-for-a-dp-at-a-secondary-site"></a>Exemplo: Analisar e conteúdo de registo para um ponto de distribuição num site secundário
`ContentLibraryCleanup.exe /dp server1.contoso.com /ps siteserver1.contoso.com /sc ABC` 


### <a name="optional-parameters"></a>Parâmetros opcionais

|Parâmetro|Detalhes|
|---------|-------|
|`/delete`| Utilize este parâmetro quando estiver pronto para eliminar o conteúdo do ponto de distribuição. Pede-lhe antes de que elimina o conteúdo. </br></br> Quando não utiliza este parâmetro, a ferramenta regista resultados sobre o conteúdo que ele faria a excluir. Sem este parâmetro, não elimina, na verdade, qualquer conteúdo do ponto de distribuição. |
| `/q` | Este parâmetro executa a ferramenta num modo silencioso, que suprime todas as instruções. Estas instruções incluem quando elimina o conteúdo. Ele também não abre automaticamente o ficheiro de registo. |
| `/ps <primary site FQDN>` | Opcional apenas quando o conteúdo de um ponto de distribuição num site primário de limpeza. Especifique o FQDN do site primário que pertence o ponto de distribuição. |
| `/sc <primary site code>` | Opcional apenas quando o conteúdo de um ponto de distribuição num site primário de limpeza. Especifique o código do site do site primário que pertence o ponto de distribuição. |
| `/log <log file directory>` | Especifique a localização onde a ferramenta grava o ficheiro de registo. Esta localização pode ser uma unidade local ou uma partilha de rede.</br></br> Quando não utiliza este parâmetro, a ferramenta coloca o ficheiro de registo no diretório temp do usuário no computador onde a ferramenta é executada.|

#### <a name="example-delete-content"></a>Exemplo: Eliminar conteúdo 
`ContentLibraryCleanup.exe /dp server1.contoso.com /delete`

#### <a name="example-delete-content-without-prompts"></a>Exemplo: Eliminar conteúdo sem pedidos
`ContentLibraryCleanup.exe /q /dp server1.contoso.com /delete` 

#### <a name="example-log-to-local-drive"></a>Exemplo: Inicie sessão para a unidade local
`ContentLibraryCleanup.exe /dp server1.contoso.com /log C:\Users\Administrator\Desktop` 

#### <a name="example-log-to-network-share"></a>Exemplo: Inicie sessão para partilha de rede
`ContentLibraryCleanup.exe /dp server1.contoso.com /log \\server\share`


### <a name="known-issue"></a>Problema conhecido

Quando nenhum pacote ou implementação falhou ou está em curso, a ferramenta pode devolver o erro seguinte: `System.InvalidOperationException: This content library cannot be cleaned up right now because package <packageID> is not fully installed.`

Não é uma solução para este problema. A ferramenta de forma fiável não consegue identificar arquivos órfãos quando o conteúdo está em curso ou falhou a implementação. A ferramenta não permite a limpeza dos conteúdos até resolver o problema.
