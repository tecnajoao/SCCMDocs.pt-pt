---
title: "Atualizar o ramo de manutenção de longa duração para o ramo atual | Documentos do Microsoft"
description: "Aprenda a converter um site secundário de manutenção de longo prazo para um site secundário atual."
ms.custom: na
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ec5b54cf-62b7-4ed1-9bb3-e8c63b9641c8
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 60631bc0346bd78d704e7129bb755af504c59b1b
ms.openlocfilehash: 6e7edc85630d22c5bbba1ff66bd1199903db76db
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---


# <a name="upgrade-the-long-term-servicing-branch-to-the-current-branch"></a>Atualizar o ramo de manutenção de longa duração para o ramo atual

*Aplica-se a: System Center Configuration Manager (ramo longa duração de manutenção)*

Utilize este tópico para saber como (converter) de atualizar um site e hierarquia que executa a longo prazo manutenção ramo (LTSB) do Configuration Manager para o ramo atual.

Quando tiver um contrato de Software Assurance atual (ou direitos de licenciamento semelhantes) que lhe concede direitos de utilização no ramo atual, pode converter a instalação a partir de LTSB o ramo atual.  Esta é uma conversão unidirecional porque não existe suporte para a conversão de um site secundário atual para o LTSB.

Se tiver vários sites, só precisa de converter o site de nível superior da hierarquia. Depois do site de nível superior é convertido em:
- Os sites primários subordinados converter automaticamente.
-    Tem de atualizar manualmente os sites secundários a partir da consola do Configuration Manager.

## <a name="run-setup-to-convert-the-long-term-servicing-branch"></a>Execute a configuração para converter o ramo de manutenção de longo prazo
No site de nível superior da hierarquia, pode executar a configuração do Configuration Manager a partir do qualificados suportes de dados de linha de base e selecionar **manutenção do Site**.  Em seguida, quando-lhe apresentada a página de licenciamento, selecione a opção para o ramo atual e conclua o assistente.

Quando o site tiver convertido para o ramo atual, anteriormente indisponível funcionalidades e capacidades estarão disponíveis para utilização.

> [!NOTE]  
> Qualificar suportes de dados do plano base é um suporte de dados que tenha uma versão que é igual ou posterior à sua instalação LTSB.

Por exemplo, uma vez que o LTSB baseia-se na versão 1606, não é possível utilizar o suporte de dados do plano base 1511 para converter o ramo atual. Em vez disso, pode executa a configuração do mesmo versão 1606 plano base suporte de dados que utilizou para instalar o site LTSB e escolha a opção de licenciamento para o ramo atual.  Em alternativa, se foi lançada um plano base mais à frente do mesmo atual, pode executar a configuração do suporte de dados nessa linha de base.

Para obter uma lista das versões do plano base, consulte o artigo **versões de linha de base e atualização** no [atualizações para o Configuration Manager](/sccm/core/servers/manage/updates).

## <a name="use-the-configuration-manager-console-to-convert-the-long-term-servicing-branch"></a>Utilizar a consola do Configuration Manager para converter o ramo de manutenção de longa duração
Se o seu site é executada a LTSB, pode utilizar a seguinte opção na consola do Configuration Manager para converter o ramo atual:

 1. Na consola, vá para **administração** > **configuração do Site** > **Sites**e, em seguida, abra **definições de hierarquia**.  

 2. Selecione a opção para converter para o ramo atual e, em seguida, escolha **aplicar**.  

Quando o site tiver convertido para o ramo atual, anteriormente indisponível funcionalidades e capacidades estarão disponíveis para utilização.

