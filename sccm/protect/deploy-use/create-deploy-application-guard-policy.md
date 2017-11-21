---
title: "Criar e implementar uma política de proteção de aplicações do Windows Defender"
titleSuffix: Configuration Manager
description: "Criar e implementar a política de proteção de aplicações do Windows Defender."
ms.custom: na
ms.date: 11/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 
caps.latest.revision: "5"
author: ErikjeMS
ms.author: erikje
manager: angrobe
ms.openlocfilehash: db2508e5bbd1435fce432b6ef98d7968e68ea5ab
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 11/21/2017
---
# <a name="create-and-deploy-windows-defender-application-guard-policy----1351960---"></a>Criar e implementar a política de proteção de aplicações do Windows Defender<!-- 1351960 -->

Pode criar e implementar [Guard de aplicação do Windows Defender](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview) políticas utilizando o endpoint protection do Configuration Manager. Estas políticas ajudam a proteger os seus utilizadores abrindo não fidedignos web sites num contentor isolado seguro que não pode ser acedido por outras partes do sistema operativo.

## <a name="prerequisites"></a>Pré-requisitos

Para criar e implementar uma política de proteção de aplicações do Windows Defender, tem de utilizar atualização do Windows 10, enquadram-se criador. Além disso, os dispositivos Windows 10 nos quais implementou a política tem de ser configurados com uma política de isolamento de rede. Para obter mais informações, consulte o [descrição geral da proteção de aplicações do Windows Defender](https://docs.microsoft.com/en-us/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview). Esta capacidade funciona apenas com atuais compilações do Windows 10 internas. Para testar, os clientes tem de executar um recente Windows 10 Insider criar.


## <a name="create-a-policy-and-to-browse-the-available-settings"></a>Crie uma política de e para procurar as definições disponíveis:

1. Na consola do Configuration Manager, escolha **ativos e compatibilidade**.
2. No **ativos e compatibilidade** área de trabalho, escolha **descrição geral** > **Endpoint Protection** > **Guard de aplicação do Windows Defender**.
3. No **home page** separador o **criar** , clique em **criar Windows Defender Guard política aplicações**.
4. Utilizar o [blogue](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97) como uma referência, pode procurar e configurar as definições disponíveis.
5. No **definição de rede** página, especifique a identidade empresarial e definir o limite da rede empresarial.

    > [!NOTE]
    > Windows 10 PCs armazenar apenas uma lista de isolamento de rede no cliente. Pode criar dois tipos diferentes de listas de isolamento de rede e implementá-las para o cliente:
    >
    >  - um Windows Information Protection
    >  - um da proteção de aplicações do Windows Defender
    >
    > Se implementar ambas as políticas, estas listas de isolamento de rede tem de corresponder. Se implementar listas não correspondem ao cliente mesmo, a implementação irá falhar. Para obter mais informações, consulte o [documentação de Windows Information Protection](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-sccm).
    > 
    > 

6. Quando tiver terminado, conclua o assistente e implementar a política para um ou mais dispositivos do Windows 10.

## <a name="next-steps"></a>Passos seguintes
Para ler mais informações sobre proteção de aplicações do Windows Defender, consulte [esta mensagem de blogue](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97). Além disso, para saber mais sobre o modo autónomo de proteção de aplicações do Windows Defender, consulte o artigo [esta mensagem de blogue](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903).
