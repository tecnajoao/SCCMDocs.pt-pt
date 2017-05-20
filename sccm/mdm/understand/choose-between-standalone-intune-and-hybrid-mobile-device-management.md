---
title: "Escolher Intune autónomo ou híbrida MDM | Documentos do Microsoft"
description: "Escolha se pretende implementar a gestão de dispositivos móveis híbrida com o Intune e Configuration Manager ou executar Intune autónomo."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 73ff9bb9-e605-4b68-92a1-487684fed42d
caps.latest.revision: 10
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: cbdcf686b9565c56c7a6fca6086d94d9e45f641a
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017

---
# <a name="choose-between-microsoft-intune-standalone-and-hybrid-mobile-device-management-with-system-center-configuration-manager"></a>Escolher entre o Microsoft Intune de autónomas e híbrida de gestão de dispositivos móveis com o System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Um dos mais frequentemente mais frequentes questões sobre a gestão de dispositivos móveis (MDM) com o Microsoft Intune é "Deve posso integrar o Intune com o Configuration Manager (híbrido MDM) ou executar Intune autónomo na configuração apenas da nuvem?" Para responder a essa questão, deve cuidadosamente comparar as duas opções e considere atualizações futuras na 2017 antecipada ao Intune autónomo.

## <a name="what-is-intune-standalone"></a>O que é autónomo do Intune?

Intune autónomo é uma solução MDM apenas na nuvem que envolve sem recursos no local e seja gerida utilizando uma consola web que pode ser acedida a partir de qualquer parte do mundo. Intune centros de dados estão alojados na América do Norte, Europa e Ásia. Porque o Intune é um serviço em nuvem, pode implementar a gestão do Intune nos seus dispositivos num curto período de tempo. Também pode optar Intune autónomo se a organização está a mover para a nuvem.

## <a name="what-is-hybrid-mdm-with-configuration-manager"></a>O que é híbrida MDM com o Configuration Manager?

Híbrida MDM é uma solução que utiliza o Intune como o canal de entrega para as políticas, perfis e aplicações em dispositivos, mas utiliza a infraestrutura do Configuration Manager no local para armazenar e administrar o conteúdo e gerir os dispositivos. Pode optar híbrida MDM se já tiver um investimento significativo no Configuration Manager e pretender expandi-lo para gerir dispositivos móveis. Uma implementação híbrida dá-lhe o controlo de "único painel da Lupa", o que significa que pode utilizar a mesma infraestrutura no local e a consola de administração para gerir dispositivos móveis com o Intune, bem como PCs e os servidores com o cliente do Configuration Manager tradicional.

## <a name="whats-coming-to-intune-standalone-in-early-2017"></a>Novidades futuras ao Intune autónomo no 2017 iniciais

Se escolher entre autónomas e híbrida, deve efetuar para as funcionalidades em consideração que vêm ao Intune autónomo no 2017 antecipada. Hoje em dia, híbrida MDM tem várias funcionalidades avançadas que tenham sido historically por que motivo alguns clientes optar por gerir os respetivos dispositivos com híbrida MDM em vez do Intune autónomo:

-   Acesso programático (API) – as opções de gestão SDK e PowerShell.

-   Relatórios personalizados – criar relatórios personalizados.

-   Controlo de acesso baseado em funções – restringir o acesso às funções administrativas, com base em funções atribuídas.

-   Dimensionar – implementar e gerir mais de 100000 dispositivos móveis.

-   Painel único da Lupa – gerir os clientes de PC tradicionais e os dispositivos geridos pelo Intune utilizando a consola do mesma.

Se estiver a começar a planear a implementação do Intune hoje e ter uma janela de vários meses para piloting, testar a aceitação e implementação, poderá considerar escolher Intune autónomo agora com a noções básicas sobre que atualizações futuras para o serviço em nuvem irão incluir mais funcionalidade. Em toda a metade do ano de calendário 2017 primeiro, o Intune autónomo irá receber atualizações que fornecem grande parte das funcionalidades avançadas de uma implementação híbrida com o Configuration Manager. Intune autónomo logo que irá mover para a plataforma de nuvem do Microsoft Azure e com irá ter avançada escalabilidade, acesso baseado em funções através do Portal do Azure, relatórios personalizados e acesso programático através da API de gráfico do Azure.

Pode mudar de híbrida ao Intune autónomo ou de autónomo para híbrida, mas é necessário que o ajuda a partir do suporte da Microsoft e de operações. Também requer a anular a inscrição e reinscrição todos os dispositivos depois da autoridade de gestão é alterada.  Microsoft está a trabalhar em melhorar a experiência de configurações mudança de uma atualização de serviço futuras.

