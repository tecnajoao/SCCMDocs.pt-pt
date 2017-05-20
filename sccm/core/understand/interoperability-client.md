---
title: Utilize o cliente de interoperabilidade expandida com o atual ramo | Documentos do Microsoft
description: "Saiba como utilizar o cliente a partir de longo prazo manutenção secundário do Configuration Manager com um site secundário atual."
ms.custom: na
ms.date: 01/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 600086d5-bd9e-4ac1-8ace-c7a62de80dc2
caps.latest.revision: 0
author: robstackmsft
ms.author: robstack
Robots: NOINDEX,NOFOLLOW
ms.translationtype: Machine Translation
ms.sourcegitcommit: 4eee9731a4a27328c47c0d15931cab28cf520a18
ms.openlocfilehash: 4cc339e28110a3097c318b61224ae7692c47a31a
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="use-the-client-software-from-the-version-1606-baseline-media-for-extended-interoperability-with-future-versions-of-a-current-branch-site"></a>Utilizar o software de cliente a partir do suporte de dados de linha de base de 1606 de versão para interoperabilidade expandida com versões futuras de um site secundário atual

*Aplica-se a: System Center Configuration Manager (ramo atual), (ramo longa duração de manutenção)*  

Pode utilizar o software de cliente do Configuration Manager para computadores Windows (Client. msi) a partir do suporte de linha de base de versão 1606 DVD que obtém com o System Center 2016 ou a partir de um ou uma versão do System Center Configuration Manager (ramo atual e longo prazo manutenção ramo 1606) para gerir dispositivos que pertencem a um site secundário atual. Este cliente chama-se o cliente de interoperabilidade expandida.

## <a name="how-this-scenario-works"></a>Como funciona este cenário:
Normalmente, quando instala uma atualização na consola novo para o ramo atual, os clientes são atualizados automaticamente o software de cliente para que possam utilizar as novas funcionalidades.

Com este cenário, utilize o ramo atual e receber as novas funcionalidades e atualizações. A maioria dos clientes executam o software de cliente a partir do ramo atual e podem atualizar esse software de cliente com cada atualização de versão a que instalar. No entanto, num subconjunto de críticos sistemas que não pretende receber as atualizações de software de cliente, instala o cliente de interoperabilidade expandida. Estes clientes não instalará o novo software de cliente até explicitamente implementar uma nova versão do software de cliente aos mesmos.

Obter mais informações sobre como impedir que os clientes de ramo atual atualizar automaticamente quando instala uma nova versão do Configuration Manager irão estar disponíveis com a versão atual ramo 1610.

O site secundário atual tem de executar versão 1606 ou posterior.

## <a name="the-extended-interoperability-client-software"></a>O software de cliente de interoperabilidade expandida
Quando utiliza o cliente de interoperabilidade expandida a 2016 do Centro de sistema ou uma versão do System Center Configuration Manager (ramo atual e longo prazo manutenção ramo 1606) com um site secundário atual, o cliente é suportado para dois anos após a disponibilidade geral da versão que corresponde ao 12º de Outubro de 2016.

Planeie a atualização do cliente de interoperabilidade expandida em dispositivos que gere com o ramo atual antes de suporte para o cliente expira. Para fazê-lo transferir uma nova versão do cliente da Microsoft e, em seguida, implementar esse software de cliente atualizado nos seus dispositivos que utilizam atual expandido cliente de interoperabilidade.

**Limitações do cliente interoperabilidade expandida:**
-     Atualizações para o software de cliente de interoperabilidade expandida não estão disponíveis através da utilização de atualizações na consola. Os detalhes adicionais para implementação de um software de cliente atualizado, serão fornecidos quando for lançado um cliente atualizado.

## <a name="identify-the-client-version-you-use"></a>Identificar a versão do cliente que utiliza
Seguem-se as versões principais cliente disponíveis para o ramo atual e LTSB:

|Versão do cliente|Ramo e versão |  
|----------------|---------------------|
|5.00.8325.xxxx |    -Ramo atual 1511|
|5.00.8355.xxxx    |-Ramo atual 1602|
|5.00.8412.1307    |-Ramo atual 1606 </br> -Ramo atual 1606 com o rollup de correção 1606 (KB3186654)</br>-cliente de interoperabilidade expandida do suporte de dados de linha de base da versão 1606|  

No cliente pode ver o versão do cliente no **geral** separador da miniaplicação de painel de controlo do Configuration Manager.

No **componentes** separador da miniaplicação, alguns componentes mostram valores diferentes. Por exemplo, para uma versão do cliente 8412.1307, alguns componentes poderão ser listadas como 5.00.8412. **1000** ou 5.00.8412. **1006**.  Neste diferente os últimos quatro dígitos de alguns componentes é normais e não indicam uma falha do componente para atualizar para a versão atual do cliente.

