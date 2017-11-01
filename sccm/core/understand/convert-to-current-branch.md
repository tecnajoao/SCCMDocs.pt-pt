---
title: "Atualizar o ramo de manutenção longo prazo para o ramo atual "
titleSuffix: Configuration Manager
description: "Saiba como converter um site de sucursal de manutenção de longo prazo para um site do ramo atual."
ms.custom: na
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ec5b54cf-62b7-4ed1-9bb3-e8c63b9641c8
caps.latest.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 6a1726b4f23ce0022a3ed5c69c2735cf4d10500d
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="upgrade-the-long-term-servicing-branch-to-the-current-branch"></a>Atualizar o ramo de manutenção longo prazo para o ramo atual

*Aplica-se a: O System Center Configuration Manager (ramo de manutenção longo prazo)*

Utilize este tópico para saber como atualizar (converter), um site e hierarquia que executa a longo prazo Servicing Branch (LTSB) do Configuration Manager para o ramo atual.

Quando tiver um contrato de Software Assurance atual (ou semelhantes direitos licenciamento) que lhe concede direitos para utilizar o ramo atual, pode converter a instalação do LTSB para o ramo atual.  Esta é uma conversão unidirecional porque não há nenhum suporte para a conversão de um site do ramo atual para o LTSB.

Se tiver vários sites, apenas terá de converter o site de nível superior da hierarquia. Depois do site de nível superior é convertido:
- Os sites primários subordinados converter automaticamente.
-   Tem de atualizar manualmente sites secundários a partir da consola do Configuration Manager.

## <a name="run-setup-to-convert-the-long-term-servicing-branch"></a>Execute a configuração para converter o ramo de manutenção de longo prazo
No site de nível superior da hierarquia, pode executar a configuração do Configuration Manager de elegíveis suporte de dados de linha de base e selecionar **manutenção do Site**.  Em seguida, quando apresentado com a página de licenciamento, selecione a opção para o ramo atual e conclua o assistente.

Quando o site foi convertido para o ramo atual, anteriormente disponíveis funcionalidades e capacidades estará disponíveis para utilização.

> [!NOTE]  
> Elegíveis suporte de dados de linha de base é um suporte de dados que tenha uma versão igual ou posterior à sua instalação LTSB.

Por exemplo, porque o LTSB baseiam-se a versão 1606, não é possível utilizar o suporte de dados de linha de base 1511 converter para o ramo atual. Em vez disso, pode executar a configuração do mesmo versão 1606 da linha de base suporte de dados que utilizou para instalar o site LTSB e escolha a opção de licenciamento para o ramo atual.  Em alternativa, se uma linha de base posterior da filial atual foi lançada, pode executar a configuração do suporte de dados nessa linha de base.

Para obter uma lista das versões de linha de base, consulte **versões de linha de base e atualização** no [atualizações para o Configuration Manager](/sccm/core/servers/manage/updates).

## <a name="use-the-configuration-manager-console-to-convert-the-long-term-servicing-branch"></a>Utilize a consola do Configuration Manager para converter o ramo de manutenção longo prazo
Se o seu site executa o LTSB, pode utilizar a seguinte opção na consola do Configuration Manager para converter para o ramo atual:

 1. Na consola, aceda a **administração** > **configuração do Site** > **Sites**e, em seguida, abra **definições de hierarquia**.  

 2. Selecione a opção para converter para o ramo atual e, em seguida, escolha **aplicar**.  

Quando o site foi convertido para o ramo atual, anteriormente disponíveis funcionalidades e capacidades estará disponíveis para utilização.
