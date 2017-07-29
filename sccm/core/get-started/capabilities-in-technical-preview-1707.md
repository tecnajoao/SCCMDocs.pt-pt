---
title: "Pré-visualização técnica 1707 | Microsoft Docs"
description: "Saiba mais sobre as funcionalidades disponíveis na versão de pré-visualização técnica 1707 para o System Center Configuration Manager."
ms.custom: na
ms.date: 06/30/2017
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cb405ba0-8792-4ab7-988b-2f835f3a9550
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: MT
ms.sourcegitcommit: 1f57c63ceeb13c7f7d760d7ecfb48df749da6770
ms.openlocfilehash: 118f20768ffc99364eb9e8cf2074d7a23f4dc572
ms.contentlocale: pt-pt
ms.lasthandoff: 07/28/2017

---
# <a name="capabilities-in-technical-preview-1707-for-system-center-configuration-manager"></a>Funcionalidades no Technical Preview 1707 do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (Technical Preview)*

Este artigo apresenta as funcionalidades que estão disponíveis no Technical Preview do System Center Configuration Manager, versão 1707. Pode instalar esta versão para atualizar e adicionar novas capacidades ao seu local de pré-visualização técnica do Configuration Manager. Antes de instalar esta versão do technical preview, reveja [pré-visualização técnica do System Center Configuration Manager](../../core/get-started/technical-preview.md) para se familiarizar com os requisitos gerais e limitações para utilizar como uma pré-visualização técnica, ao atualizar entre versões e como fornecer comentários sobre as funcionalidades de um technical preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->

**Seguem-se novas funcionalidades que pode experimentar com esta versão.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="client-peer-cache-support-for-express-installation-files-for-windows-10-and-office-365"></a>Suporte de Cache ponto a ponto do cliente para ficheiros de instalação rápida para Windows 10 e o Office 365
<!-- 1352486 -->
A partir desta versão, a Cache suporta a distribuição dos ficheiros de conteúdo de instalação rápida para o Windows 10 e dos ficheiros de atualização para o Office 365. Não existem configurações adicionais são necessárias.

## <a name="surface-device-dashboard"></a>Dashboard de dispositivo superfície
<!--1355788-->
O dashboard de dispositivo superfície fornece informações sobre os dispositivos superfície encontrado no seu ambiente. Na consola, aceda a **monitorização** > **dispositivos Surface**. Pode ver o seguinte:
- percentagem de analisa
- percentagem dos modelos superfície
- principais cinco versões de sistema operativo

Clique na secção do **superfície modelos** gráfico para uma lista completa dos dispositivos.  

## <a name="configure-and-deploy-windows-defender-application-guard-policies"></a>Configurar e implementar políticas de proteção de aplicações do Windows Defender
<!-- 1351960 -->

[Proteção de aplicações do Windows Defender](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) é uma nova funcionalidade do Windows que ajuda a proteger os seus utilizadores abrindo não fidedignos web sites num contentor isolado seguro que não pode ser acedido por outras partes do sistema operativo. Esta pré-visualização técnica, adicionámos suporte para configurar esta funcionalidade utilizando as definições de compatibilidade do Configuration Manager que configurar e, em seguida, implementar numa coleção. Esta funcionalidade será lançada em pré-visualização para a versão de 64 bits da atualização do Windows 10 Creator (nome: RS2). Para testar esta funcionalidade agora, tem de utilizar uma versão de pré-visualização desta atualização.

### <a name="before-you-start"></a>Antes de começar

Para criar e implementar políticas de proteção de aplicações do Windows Defender, os dispositivos Windows 10 nos quais implementou a política tem de ser configurados com uma política de isolamento de rede. Para obter mais detalhes, consulte [esta mensagem de blogue](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97). Esta capacidade funciona apenas com atuais compilações do Windows 10 internas. Para testar, os clientes tem de executar um recente Windows 10 Insider criar.

### <a name="try-it-out"></a>Experimente!

#### <a name="to-create-a-policy-and-to-browse-the-available-settings"></a>Para criar uma política e, para procurar as definições disponíveis:

1. Na consola do Configuration Manager, escolha **ativos e compatibilidade**.
2. No **ativos e compatibilidade** área de trabalho, escolha **descrição geral** > **Endpoint Protection** > **Guard de aplicação do Windows Defender**.
3. No **home page** separador o **criar** , clique em **criar Windows Defender Guard política aplicações**.
4. Utilizar a mensagem de blogue como uma referência, pode procurar e configurar as definições disponíveis para experimentar a funcionalidade.
5. Nesta versão, adicionámos as novas **definição de rede** página para o assistente. Nesta página, especifique a identidade empresarial e definir o limite da rede empresarial.<br>Windows 10 PCs armazenar apenas uma lista de isolamento de rede no cliente. Nesta versão, pode criar dois tipos diferentes de listas de isolamento de rede (uma da proteção de informações do Windows e outro da proteção de aplicações do Windows Defender) e implementá-las para o cliente. Se implementar ambas as políticas, estas listas de isolamento de rede tem de corresponder. Se implementar listas não correspondem ao cliente mesmo, a implementação irá falhar.
Pode encontrar mais informações sobre como especificar definições de rede no [documentação de Windows Information Protection](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-sccm).
6. Quando tiver terminado, conclua o assistente e implementar a política para um ou mais dispositivos do Windows 10.

### <a name="further-reading"></a>Ler mais
Para ler mais informações sobre proteção de aplicações do Windows Defender, consulte [esta mensagem de blogue](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97). Além disso, para saber mais sobre o modo autónomo de proteção de aplicações do Windows Defender, consulte o artigo [esta mensagem de blogue](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903).

## <a name="add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager"></a>Adicionar parâmetros ao implementar scripts do PowerShell do Configuration Manager

<!-- 1236459 --->

No último Technical Preview, introduzimos uma nova capacidade que permite-lhe [criar e executadas scripts do PowerShell da consola do Configuration Manager]( /core/get-started/capabilities-in-technical-preview-1706#create-and-run-powershell-scripts-from-the-configuration-manager-console).
Nesta pré-visualização técnica, iremos tiver expandido sobre esta capacidade. Configuration Manager agora lê o script do PowerShell e apresenta quaisquer parâmetros no Assistente de criação de scripts. Pode fornecer um valor para o parâmetro no assistente que será utilizado quando o script é executado. Em alternativa, pode deixar o parâmetro em branco. Se o fizer, terá de fornecer um valor para o parâmetro ao executar o script.

### <a name="try-it-out"></a>Experimente!

1. Siga as instruções para [criar e executadas scripts do PowerShell da consola do Configuration Manager]( /core/get-started/capabilities-in-technical-preview-1706#create-and-run-powershell-scripts-from-the-configuration-manager-console).
2. No novo **parâmetros do Script** página do **Assistente de criação de scripts**, escolha um parâmetro e, em seguida, clique em **editar**.
3. Forneça um valor de parâmetro para o parâmetro selecionado e, em seguida, clique em **OK**.
4. Conclua o assistente.

Quando o script é executado, irá utilizar os valores de parâmetros que configurou.
