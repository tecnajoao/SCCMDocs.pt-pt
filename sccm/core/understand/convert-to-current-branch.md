---
title: 'Atualizar o Long term servicing branch para o current branch '
titleSuffix: Configuration Manager
description: Saiba como converter um site de term Servicing Branch para um site do ramo atual.
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ec5b54cf-62b7-4ed1-9bb3-e8c63b9641c8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f1683f69ae065d0523719edd3d24da52d499341b
ms.sourcegitcommit: 1439817f1309658b31008d7bafaab32fc5ef8789
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52820004"
---
# <a name="upgrade-the-long-term-servicing-branch-to-the-current-branch"></a>Atualizar o Long term servicing branch para o current branch

*Aplica-se a: O System Center Configuration Manager (Long term Servicing Branch)*

Utilize este tópico para saber como atualizar (converter), um site e hierarquia que executa o term Servicing Branch (LTSB) do Configuration Manager para o Current Branch.

Quando tiver um contrato atual do Software Assurance (ou semelhante direitos de licenciamento) que lhe concede direitos para utilizar o ramo atual, pode converter a instalação do LTSB para o Current Branch.  Esta é uma conversão unidirecional porque não há suporte para a conversão de um site do ramo atual para o LTSB.

Se tiver vários sites, apenas terá de converter o site de nível superior da sua hierarquia. Depois do site de nível superior é convertido:
- Os sites primários subordinados converter automaticamente.
-   Tem de atualizar manualmente sites secundários a partir da consola do Configuration Manager.

## <a name="run-setup-to-convert-the-long-term-servicing-branch"></a>Executar a configuração para converter o term Servicing Branch
No site de nível superior da hierarquia, pode executar a configuração do Configuration Manager de qualificar o suporte de dados de linha de base e selecionar **manutenção do Site**.  Em seguida, quando apresentado com a página de licenciamento, selecione a opção para o ramo atual e conclua o assistente.

Quando o site tiver convertido para o Current Branch, anteriormente disponíveis funcionalidades e capacidades estarão disponíveis para utilização.

> [!NOTE]  
> Elegíveis do suporte de dados de linha de base é um suporte de dados que tem uma versão que é igual ou posterior à sua instalação LTSB.

Por exemplo, uma vez que o LTSB baseia-se a versão 1606, não é possível utilizar o suporte de dados de linha de base 1511 para converter para o Current Branch. Em vez disso, pode executar a configuração da mesma versão 1606 da linha de base mídia que utilizou para instalar o site LTSB e escolha a opção de licenciamento para o ramo atual.  Em alternativa, se tiver sido lançada uma linha de base do Current Branch posterior, pode executar a configuração desse suporte de dados de linha de base.

Para obter uma lista das versões de linha de base, consulte **versões de linha de base e de atualização** na [atualiza para o Configuration Manager](/sccm/core/servers/manage/updates).

## <a name="use-the-configuration-manager-console-to-convert-the-long-term-servicing-branch"></a>Utilizar a consola do Configuration Manager para converter o Long term servicing branch
Se o seu site executa o LTSB, pode utilizar a seguinte opção na consola do Configuration Manager para converter para o ramo atual:

 1. Na consola, aceda a **Administration** > **configuração do Site** > **Sites**e, em seguida, abra **dedefiniçõesdehierarquia**.  

 2. Na **definições de hierarquia**, mude para o **licenciamento** separador. Selecione a opção para **converter para Current Branch**e, em seguida, escolha **aplicar**.  

Quando o site tiver convertido para o Current Branch, anteriormente disponíveis funcionalidades e capacidades estarão disponíveis para utilização.
