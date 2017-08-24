---
title: "Introdução para o ramo de manutenção longo prazo | Microsoft Docs"
description: "Saiba mais sobre o ramo de manutenção do System Center Configuration Manager longo prazo."
ms.custom: na
ms.date: 05/01/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 694bc29f-a7fd-4e06-815a-1a9c5e9ac563
caps.latest.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 91c1ca860069c6ebe0d20230c4620bf3f68735a2
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 08/07/2017
---
# <a name="introduction-to-the-long-term-servicing-branch-of-system-center-configuration-manager"></a>Introdução ao longo prazo manutenção ramo do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo de manutenção longo prazo)*

A longo prazo Servicing Branch (LTSB) do System Center Configuration Manager é um ramo distinto do Configuration Manager que foi concebido como uma opção de instalação disponível para todos os clientes. No entanto, é a única opção para os clientes que permitem o intervalo seu Assurance de Software (SA) ou direitos equivalentes de subscrição para o Configuration Manager.


Com base no Configuration Manager versão 1606, o LTSB foi reduzido funcionalidade quando comparado com a atual filial do Configuration Manager.

 > [!TIP]   
 > Se estivessem à procura de informações sobre os ramos de **do Windows Server**, consulte [Windows Server 2016 novo Current Branch for Business manutenção opção]( https://blogs.technet.microsoft.com/windowsserver/2016/07/12/windows-server-2016-new-current-branch-for-business-servicing-option/).

## <a name="features-that-are-not-available-in-the-ltsb-of-configuration-manager"></a>Funcionalidades que não estão disponíveis no LTSB do Configuration Manager
Ramo atual do Configuration Manager suporta as seguintes funcionalidades que não estão disponível quando utiliza o LTSB:

-   Atualizações na consola que adicionar funcionalidades novas e melhoradas.
-   Suporte para sistemas de operativos lançados recentemente a utilizar como servidores de sites e clientes.
-   Utilização de uma subscrição do Microsoft Intune para suportar:
    -   Intune numa configuração de gestão (MDM) de dispositivos móveis híbridos
    -   MDM no local
-   O Dashboard de manutenção do Windows 10 e planos de manutenção, incluindo suportem para Windows 10 Current Branch (CB) de recentes e ramo atual para versões Business (CBB).  
-   Suporte para versões futuras do Windows Server e Windows 10 LTSB
-   Asset Intelligence
-   Pontos de distribuição baseados na nuvem
-   Exchange Online como um conector do Exchange    

Embora suporta estas funcionalidades não está disponível com o LTSB, algumas funcionalidades permanecem visíveis na consola do Configuration Manager, mas não podem ser selecionadas ou utilizadas.


## <a name="find-documentation-for-the-ltsb"></a>Encontrar documentação sobre o LTSB
O LTSB baseia-se numa versão 1606 de Current Branch. Para obter documentação de produto, utilize o [documentação Current Branch](https://docs.microsoft.com/sccm/), com avisos e limitações que são específicas para o LTSB. Os avisos e limitações são identificadas nos seguintes tópicos online:

-     [Introdução para o ramo de manutenção longo prazo](introduction-to-the-ltsb.md): (Este tópico)
-     [Instalar o ramo de manutenção longo prazo](install-the-ltsb.md)
-     [Atualizar o ramo de manutenção longo prazo para o ramo atual](convert-to-current-branch.md)
-     [Configurações suportadas do Long Term Servicing Branch](supported-configurations-for-ltsb.md)
-   [Gerir o longo prazo ramo de manutenção do Configuration Manager](manage-the-ltsb.md)

Quando referenciar documentação do ramo atual para o LTSB, detalhes que se aplicam à versão 1606 também aplicam-se a LTSB. Não são suportados pelo LTSB funcionalidades ou detalhes que são introduzidas com a versão 1610 ou posterior.


## <a name="licensing-overview-for-the-ltsb"></a>Descrição geral de licenciamento para o LTSB   
Os clientes com o Active Directory Software Assurance (SA) de licenças do System Center Configuration Manager, ou com direitos de subscrição equivalente a partir de 1 de Outubro de 2016, tem direitos para utilizar a versão de versão 1606 de Outubro de 2016 do System Center Configuration Manager. Os clientes com direitos para o System Center Configuration Manager nesta ou após 1 de Outubro de 2016, irão encontrar duas opções licenciadas após a instalação: O ramo atual e a longo prazo manutenção Branch (LTSB).

Os clientes que têm direitos perpétuos descritos para o System Center Configuration Manager, ou que permitem SA ou de subscrição para o intervalo após 1 de Outubro, podem instalar a versão do System Center Configuration Manager LTSB actual no momento do intervalo.

[Completos termos e condições para os produtos comprar através de programas de licenciamento em Volume da Microsoft podem ser encontradas aqui](http://go.microsoft.com/fwlink/?LinkId=800052).

Consulte [licenciamento do System Center Configuration Manager e ramos](learn-more-editions.md) para obter mais informações sobre o licenciamento do Configuration Manager ramos.

## <a name="next-steps"></a>Passos Seguintes

Se decidir que o Configuration Manager LTSB é o ramo correto para o seu ambiente, [instalar um novo LTSB](/sccm/core/understand/install-the-ltsb#install-a-new-site) site como parte de uma nova hierarquia ou [atualizar um site do System Center 2012 Configuration Manager](/sccm/core/understand/install-the-ltsb#upgrade-from-system-center-2012-configuration-manager) e da hierarquia.

Se não tiver suporte de instalação, consulte [documentação do System Center 2016](https://technet.microsoft.com/system-center-docs/system-center) para obter informações sobre como obter o System Center 2016, que inclui suporte de dados que pode utilizar para instalar o LTSB do System Center Configuration Manager.  
