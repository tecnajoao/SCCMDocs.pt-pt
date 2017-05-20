---
title: "Introdução para o ramo de manutenção de longa duração | Documentos do Microsoft"
description: "Saiba mais sobre a longo prazo ramificação de manutenção do System Center Configuration Manager."
ms.custom: na
ms.date: 05/01/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 694bc29f-a7fd-4e06-815a-1a9c5e9ac563
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: d940fd1bbf96767d44f8c55315e814be55a83897
ms.openlocfilehash: 91c1ca860069c6ebe0d20230c4620bf3f68735a2
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="introduction-to-the-long-term-servicing-branch-of-system-center-configuration-manager"></a>Introdução para o ramo manutenção longa duração do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramo longa duração de manutenção)*

A longo prazo manutenção ramo (LTSB) do System Center Configuration Manager é um ramo diferente do Configuration Manager que foi concebido como uma opção de instalação disponível a todos os clientes. No entanto, é a única opção para os clientes que lhe permitem intervalo o Software Assurance (SA) ou direitos de subscrição equivalente para o Configuration Manager.


Com base no Configuration Manager versão 1606, o LTSB tem funcionalidades reduzidas quando comparado com o atual ramo do Configuration Manager.

 > [!TIP]   
 > Se estiver a visualizar para obter informações sobre os ramos de **Windows Server**, consulte o artigo [ramo atual novo Windows Server 2016 para empresas manutenção opção]( https://blogs.technet.microsoft.com/windowsserver/2016/07/12/windows-server-2016-new-current-branch-for-business-servicing-option/).

## <a name="features-that-are-not-available-in-the-ltsb-of-configuration-manager"></a>Funcionalidades que não estão disponíveis no LTSB do Configuration Manager
Ramo atual do Configuration Manager suporta as seguintes funcionalidades que não está disponível quando utiliza o LTSB:

-   Na consola atualizações que adicionar novas funcionalidades e melhorias.
-   Suporte para sistemas de operativos recentemente publicados utilizar como servidores de sites e clientes.
-   Utilização de uma subscrição do Windows Intune para suportar:
    -   Intune numa configuração híbrida dispositivos móveis (MDM) de gestão
    -   MDM no local
-   O Dashboard de manutenção do Windows 10 e manutenção planos, incluindo suportem para recentes Windows 10 atual ramo (CB) e ramo atual para versões de negócio (CBB).  
-   Suporte para versões futuras do Windows Server e Windows 10 LTSB
-   Asset Intelligence
-   Pontos de distribuição baseados na nuvem
-   Exchange Online como um conector do Exchange    

Apesar de suporte para estas funcionalidades não está disponível com o LTSB, algumas funcionalidades permanecem visíveis na consola do Configuration Manager, mas não podem ser selecionadas ou utilizadas.


## <a name="find-documentation-for-the-ltsb"></a>Encontrar documentação sobre o LTSB
O LTSB baseia-se na versão atual ramo 1606. Para a documentação do produto, utilize o [documentação ramo atual](https://docs.microsoft.com/sccm/), com advertências e limitações que são específicas para o LTSB. Esses advertências e limitações são identificadas nos seguintes tópicos online:

-      [Introdução para o ramo de manutenção de longa duração](introduction-to-the-ltsb.md): (Neste tópico)
-      [Instalar o ramo de manutenção de longa duração](install-the-ltsb.md)
-      [Atualizar o ramo de manutenção de longa duração para o ramo atual](convert-to-current-branch.md)
-      [Configurações suportadas para o ramo de manutenção de longa duração](supported-configurations-for-ltsb.md)
-   [Gerir a longo prazo ramificação de manutenção do Configuration Manager](manage-the-ltsb.md)

Quando referenciar documentação de ramo atual para o LTSB, os detalhes que se aplicam à versão 1606 também se aplicam ao LTSB. Não são suportados pelo LTSB funcionalidades ou detalhes introduzido com a versão 1610 ou posterior.


## <a name="licensing-overview-for-the-ltsb"></a>Descrição geral do licenciamento para o LTSB   
Os clientes com o Active Directory Software Assurance (SA) no System Center Configuration Manager licenças, ou com direitos de subscrição equivalente a partir de 1 de Outubro de 2016, tem direitos para utilizar a versão de versão 1606 Outubro de 2016 do System Center Configuration Manager. Os clientes com direitos para o System Center Configuration Manager em ou depois de 1 de Outubro de 2016, irão encontrar duas opções licenciadas após a instalação: Ramo atual e ramo de manutenção de longa duração (LTSB).

Os clientes que possuem direitos descritos infra para o System Center Configuration Manager ou que permitem SA ou subscrição para o intervalo depois de 1 de Outubro, podem instalar a versão do System Center Configuration Manager LTSB que é atual no momento do intervalo.

[Concluída termos e condições para os produtos de compra através de programas de licenciamento em Volume da Microsoft podem ser encontradas aqui](http://go.microsoft.com/fwlink/?LinkId=800052).

Consulte o artigo [licenciamento do System Center Configuration Manager e ramos](learn-more-editions.md) para obter mais informações sobre o licenciamento do Configuration Manager ramificações.

## <a name="next-steps"></a>Passos Seguintes

Se decidir que o Configuration Manager LTSB é o ramo correto para o seu ambiente, [instalar um novo LTSB](/sccm/core/understand/install-the-ltsb#install-a-new-site) site como parte de uma nova hierarquia, ou [atualizar um site do System Center 2012 Configuration Manager](/sccm/core/understand/install-the-ltsb#upgrade-from-system-center-2012-configuration-manager) e da hierarquia.

Se não tem suporte de instalação, consulte o artigo [documentação do System Center 2016](https://technet.microsoft.com/system-center-docs/system-center) para obter informações sobre como obter o System Center 2016, que inclui suporte de dados que pode utilizar para instalar o System Center Configuration Manager LTSB.  

