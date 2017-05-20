---
title: "Tarefas comuns de gestão de conformidade de dispositivos geridos pelo cliente - Configuration Manager | Documentos do Microsoft"
description: "Saiba mais sobre as definições de compatibilidade do System Center Configuration Manager ao trabalhar através de alguns cenários comuns."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4e345791-74db-41ad-b472-024ce6521daf
caps.latest.revision: 8
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 991eff171dce95590a7f050e0d3b07f98c0224b3
ms.openlocfilehash: 2012ab5e55da8d707fd668e0163b42fe7d56c72f
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="common-tasks-for-managing-compliance-on-devices-with-the-system-center-configuration-manager-client"></a>Tarefas comuns para gerir a compatibilidade em dispositivos com o cliente do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Os cenários neste tópico dão-lhe uma introdução à utilização de definições de compatibilidade do System Center Configuration Manager ao trabalhar através de alguns cenários comuns que poderá encontrar.  

 Se já estiver familiarizado com as definições de compatibilidade, documentação detalhada sobre todas as funcionalidades que utiliza pode ser encontrada no [itens de configuração para dispositivos geridos com o cliente do System Center Configuration Manager](../../compliance/deploy-use/configuration-items-for-devices-managed-with-the-client.md) secção.  

 Antes de começar, leia [começar com as definições de compatibilidade](../../compliance/get-started/get-started-with-compliance-settings.md) para algumas noções básicas sobre as definições de conformidade e consulte também [planear e configurar as definições de compatibilidade](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) para implementar os pré-requisitos necessários.  

## <a name="general-information-for-each-scenario"></a>Informações gerais para cada cenário  
 Em cada cenário, irá criar um item de configuração que realiza uma tarefa específica. Para abrir o Assistente de Criação de Item de Configuração, utilize os seguintes passos:  

1.  Na consola do Configuration Manager, clique em **ativos e compatibilidade** > **definições de compatibilidade** > **itens de configuração**.  

3.  No separador **Início** , no grupo **Criar** , clique em **Criar Item de Configuração**.  

4.  No separador **Geral** do Assistente de Criação de Item de Configuração, conforme apresentado abaixo, especifique um nome e uma descrição para o item de configuração e escolha o tipo de item de configuração adequado para cada cenário deste tópico.  

     ![Mostra a página geral do Assistente de item de configuração de criar.](/sccm/compliance/plan-design/media/Compliance-Settings-Wizard---1.png)  

## <a name="scenarios-for-windows-10-devices-managed-with-the-configuration-manager-client"></a>Cenários para dispositivos Windows 10 geridos com o cliente do Configuration Manager  

### <a name="scenario-disable-the-use-of-bluetooth-on-windows-10-devices"></a>Cenário: Desativar a utilização de Bluetooth nos dispositivos Windows 10  
 Neste cenário, o departamento de segurança identificou a capacidade de Bluetooth nos dispositivos como um meio que poderia ser utilizado para transmitir informações empresariais confidenciais fora da empresa. Atualizou recentemente todos os PCs para o Windows 10 e optou por desativar a capacidade de Bluetooth nestes dispositivos.  

1.  Na página **Geral** do Assistente de Criação de Item de Configuração, selecione o tipo de item de configuração **Windows 10** e clique em **Seguinte**.  

2.  Na página **Plataformas Suportadas** do assistente, selecione todas as plataformas Windows 10.  

3.  Na página **Definições do Dispositivo** , selecione **Dispositivo**e clique em **Seguinte**.  

4.  Na página **Dispositivo** , selecione **Proibido** como o valor de **Bluetooth**.  

5.  Selecione **Remediar definições incompatíveis** para garantir que a alteração é aplicada a todos os dispositivos Windows 10.  

6.  Conclua o assistente para criar o item de configuração.  

 Agora pode utilizar as informações de [tarefas comuns para criar e implementar linhas de base de configuração com o System Center Configuration Manager](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) tópico para ajudar a implementar a configuração que criou para dispositivos.  

## <a name="scenarios-for-windows-desktop-and-server-computers-managed-with-the-configuration-manager-client"></a>Cenários para computadores de secretária e computadores servidores Windows geridos com o cliente do Configuration Manager  
 Em computadores de Mac com o cliente do Configuration Manager, tem duas opções para avaliar a compatibilidade:  

-   Avaliar um ficheiro de preferências (plist) do Mac OS X.  

-   Utilizar um script personalizado e avaliar os resultados devolvidos pelo script.  

 Para obter mais informações, consulte o artigo [como criar itens de configuração para Mac OS X dispositivos geridos com o cliente do System Center Configuration Manager](../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md).  

### <a name="scenario-remediate-an-incorrect-registry-value-on-windows-desktop-computers"></a>Cenário: Remediar um valor de registo incorreto em computadores de ambiente de trabalho do Windows  
 Neste cenário, descobre que uma aplicação de linha de negócio importante não está a funcionar corretamente em alguns computadores que gere que têm o Windows 8.1. Depois de investigar, descobre que isto acontece porque uma chave de registo com o nome **HKEY_LOCAL_MACHINE\SOFTWARE\Woodgrove\LOB App\Configuration\Configuration1** está definida com o valor **0** em alguns computadores. Para que a aplicação de linha de negócio funcione corretamente, este valor tem de ser definido como **1**.  

 Neste procedimento, irá criar um item de configuração que monitoriza e retifica automaticamente quaisquer valores de chave de registo incorretos encontrados.  

1.  Na página **Geral** do Assistente de Criação de Item de Configuração, selecione o tipo de item de configuração **Ambiente de trabalho ou servidor do Windows (personalizado)** e clique em **Seguinte**.  

2.  Na página **Plataformas Suportadas** do assistente, selecione **Windows 8.1** (para garantir que o item de configuração é aplicado apenas aos computadores afetados).  

3.  Na página **Definições** , clique em **Novo** para criar uma nova definição.  

4.  No separador **Geral** da caixa de diálogo **Criar Definição** , configure o seguinte:  

    -   **Nome** > **Definição de exemplo**  

    -   **Tipo de definição** > **Valor de registo**  

    -   **Tipo de dados** > **Número inteiro** (uma vez que o valor contém apenas um número)  

    -   **Ramo de registo** > **HKEY_LOCAL_MACHINE**  

    -   **Chave** > **SOFTWARE\Woodgrove\LOB App\Configuration\Configuration1**  

    -   **Valor** > **1** (o valor necessário)  

5.  No separador **Regras de Compatibilidade** da caixa de diálogo **Criar Definição** , clique em **Novo**e, em seguida, na caixa de diálogo **Criar Regra** , configure o seguinte:  

    -   **Nome** > **Regra de Exemplo**  

    -   **Definição selecionada** – verifique se a definição selecionada é **Definição de exemplo**.  

    -   **Tipo de regra** > **Valor**  

    -   **A definição deve cumprir a seguinte regra** – verifique se o nome da definição está correto e configure a opção para especificar que o valor da definição tem de ser igual a **1**.  

    -   **Remediar regras incompatíveis quando suportado** – Selecione esta caixa para se certificar de que o Configuration Manager será reposto o valor da chave de registo para o valor correto se está incorreto.  

6.  Conclua o assistente para criar o item de configuração.  

 Agora pode utilizar as informações de [tarefas comuns para criar e implementar linhas de base de configuração](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) tópico para ajudar a implementar a configuração que criou para dispositivos.  

