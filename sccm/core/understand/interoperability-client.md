---
title: Utilizar o cliente do Configuration Manager interoperabilidade expandida com o ramo atual | Microsoft Docs
description: "Saiba mais sobre como utilizar o cliente da longo prazo manutenção ramo do Configuration Manager com um site do ramo atual."
ms.custom: na
ms.date: 08/09/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 600086d5-bd9e-4ac1-8ace-c7a62de80dc2
caps.latest.revision: "0"
author: robstackmsft
ms.author: robstack
ms.openlocfilehash: 6487a7c0eb958c74ca4c6a7233747966110eceb9
ms.sourcegitcommit: b41d3e5c7f0c87f9af29e02de3e6cc9301eeafc4
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/11/2017
---
# <a name="use-the-configuration-manager-client-software-for-extended-interoperability-with-future-versions-of-a-current-branch-site"></a>Utilize o software de cliente do Configuration Manager para interoperabilidade expandida com versões futuras de um site do ramo atual

*Aplica-se a: O System Center Configuration Manager (ramo atual), (ramo de manutenção longo prazo)*  

Em alguns casos, as políticas da empresa podem não permitir-lhe atualizar regularmente o cliente do Configuration Manager em alguns computadores. Por exemplo, poderá ser necessário está em conformidade com políticas de gestão de alterações ou o dispositivo poderá ser fundamentais.

Embora deve continuar a utilizar a atualização automática de cliente quando possível para a maior parte dos clientes, começando com o Configuration Manager atualizar 1610, pode acomodar estas necessidades ao instalar um novo cliente para utilização de longa duração, denominado o cliente de interoperabilidade expandida (EIC).

O EIC é compatível com sites do Configuration Manager a executar a versão 1610 ou posterior. O EIC só deve ser utilizada para computadores específicos que não podem ser atualizadas com frequência, tal como de local público ou dispositivos de ponto de venda. Utilize o cliente mais recente do Configuration Manager para todos os outros PCs.

## <a name="how-this-scenario-works"></a>Como funciona este cenário

Normalmente, quando instala uma nova atualização na consola para o ramo atual, os clientes atualizar automaticamente os respetivos software de cliente para que possam utilizar as novas funcionalidades.

Com este cenário, utilize o ramo atual e receber as novas funcionalidades e atualizações. A maioria dos clientes executam o software de cliente do ramo atual e podem atualizar esse software de cliente com cada atualização de versão a que instalar. No entanto, num subconjunto de sistemas críticos que não pretende receber atualizações de software de cliente, instala o cliente de interoperabilidade expandida. Estes clientes não instalam o novo software de cliente até explicitamente implementar uma nova versão do software de cliente aos mesmos.

>[!IMPORTANT]
>O site de Current Branch tem de executar versão 1610 ou posterior.

## <a name="how-to-use-the-eic"></a>Como utilizar o EIC

1. Obter o EIC (versão de cliente 5.00.8412) da pasta de \SMSSETUP\Client do suporte de instalação de atualização do Configuration Manager 1606. Certifique-se de que copie todo o conteúdo da pasta.
2. Instale manualmente o EIC nesses dispositivos. [Leia mais detalhes sobre como instalar manualmente o cliente](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual).
3. Exclua nessa coleção de atualizações de cliente.

>[!TIP]
>Para localizar o System Center Configuration Manager versão 1606 no Volume Licensing Service Center (VLSC), vá para o **transfere e chaves** separador do [VLSC](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx), procure "configuração de centro de sistema" e, em seguida, selecione **System Center Config Mgr (ramo atual e LTSB)**.

## <a name="the-extended-interoperability-client-software"></a>O software de cliente de interoperabilidade expandida

Atual EIC continuará a ser suportada com versões atualizadas do Configuration Manager atual ramo até, pelo menos, 18 de Novembro de 2018. Após este tempo, verifique esta página para detalhes de um novo EIC ou uma extensão de suporte para o EIC existente.

>[!TIP]
>O EIC é suportada para, pelo menos, dois anos a partir da data da versão (consulte [suporte para versões do System Center Configuration Manager current branch](/sccm/core/servers/manage/current-branch-versions-supported)). Por exemplo, suporte para o atual EIC for dois anos após o lançamento de 1610, que é 18 de Novembro de 2018.

Planear atualizar o cliente de interoperabilidade expandidas em dispositivos que gere com o ramo atual antes do suporte para o cliente expira. Para tal, transfira uma nova versão do cliente da Microsoft e, em seguida, implementar esse software de cliente atualizado nos seus dispositivos que utilizam o cliente de interoperabilidade expandida atual.

## <a name="limitations-of-the-extended-interoperability-client"></a>Limitações do cliente interoperabilidade expandida

- Atualizações para o software de cliente de interoperabilidade expandida não estão disponíveis através da utilização de atualizações na consola. Detalhes adicionais para a implementação de um software de cliente atualizado são fornecidos quando um cliente atualizado for lançado.
- O EIC suporta apenas as atualizações de software, inventário e os pacotes e programas.

## <a name="next-steps"></a>Passos seguintes

Utilize as informações em [como monitorizar clientes](/sccm/core/clients/manage/monitor-clients) para se certificar de que os clientes estão corretamente instalados nos dispositivos que pretende.
