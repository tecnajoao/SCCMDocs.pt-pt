---
title: Introdução ao Long Term Servicing Branch
titleSuffix: Configuration Manager
description: Saiba mais sobre o Long term Servicing Branch do System Center Configuration Manager.
ms.date: 05/01/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 694bc29f-a7fd-4e06-815a-1a9c5e9ac563
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f714be298c244b86178780138f5a700c89ae2a76
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56128988"
---
# <a name="introduction-to-the-long-term-servicing-branch-of-system-center-configuration-manager"></a>Introdução ao Long term Servicing Branch do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (Long term Servicing Branch)*

O term Servicing Branch (LTSB) do System Center Configuration Manager é um ramo distinto do Configuration Manager que foi concebido como uma opção de instalação disponível para todos os clientes. No entanto, é a única opção para os clientes que permitem lapso seu Software Assurance (SA) ou direitos de subscrição equivalente para o Configuration Manager.


Com base no Configuration Manager versão 1606, a LTSB tem funcionalidades reduzidas em comparação com para o atual ramo do Configuration Manager.

 > [!TIP]   
 > Se estava procurando informações sobre as ramificações da **Windows Server**, consulte [Windows Server 2016 novo ramo atual para empresas que opção de manutenção]( https://blogs.technet.microsoft.com/windowsserver/2016/07/12/windows-server-2016-new-current-branch-for-business-servicing-option/).

## <a name="features-that-are-not-available-in-the-ltsb-of-configuration-manager"></a>Funcionalidades que não estão disponíveis no LTSB do Configuration Manager
Ramo atual do Configuration Manager suporta as seguintes funcionalidades que não estão disponível quando utiliza o LTSB:

-   Atualizações na consola que adicionam novos recursos e melhorias.
-   Suporte para sistemas de operativos recém-lançada utilizar como servidores de sites e clientes.
-   Utilização de uma subscrição do Microsoft Intune para suportar:
    -   Intune numa configuração de gestão (MDM) de dispositivos móveis híbrida
    -   MDM no local
-   O Dashboard de manutenção do Windows 10 e, em seguida, planos de manutenção, incluindo suportam para Windows 10 Current Branch (CB) e Current Branch recentes para versões Business (CBB).  
-   Suporte para versões futuras do Windows Server e Windows 10 LTSB
-   Asset Intelligence
-   Pontos de distribuição baseados na nuvem
-   Exchange Online como um conector do Exchange    

Embora o suporte para esses recursos não está disponível com o LTSB, algumas funcionalidades permanecem visíveis na consola do Configuration Manager, mas não podem ser selecionadas ou utilizadas.


## <a name="find-documentation-for-the-ltsb"></a>Encontre documentação para o LTSB
O LTSB baseia-se a versão do Current Branch 1606. Para obter a documentação do produto, utilize o [documentação do Current Branch](https://docs.microsoft.com/sccm/), com avisos e limitações que são específicas para o LTSB. Essas limitações e avisos são identificadas nos seguintes tópicos online:

- [Introdução ao Long term Servicing Branch](introduction-to-the-ltsb.md): (Neste tópico)
- [Instalar o Long term Servicing Branch](install-the-ltsb.md)
- [Atualizar o Long term Servicing Branch para o Current Branch](convert-to-current-branch.md)
- [Configurações suportadas do Long Term Servicing Branch](supported-configurations-for-ltsb.md)
- [Gerir o Long term Servicing Branch do Configuration Manager](manage-the-ltsb.md)

Quando referencia a documentação do ramo atual para o LTSB, detalhes que se aplicam à versão 1606 também se aplicam ao LTSB. Funcionalidades ou detalhes que são introduzidas com a versão 1610 ou posterior, não são suportadas pelo LTSB.


## <a name="licensing-overview-for-the-ltsb"></a>Descrição geral do licenciamento para o LTSB   
Os clientes com Software Assurance (SA) ativo em licenças do System Center Configuration Manager ou com direitos de subscrição equivalente a partir de 1 de Outubro de 2016, tem direitos para utilizar o lançamento da versão 1606 de Outubro de 2016 do System Center Configuration Manager. Os clientes com direitos para o System Center Configuration Manager em ou depois de 1 de Outubro de 2016, encontrará duas opções licenciadas após a instalação: Ramo atual e Long term Servicing Branch (LTSB).

Os clientes que têm direitos perpétuos para o System Center Configuration Manager ou permitir que a SA ou uma subscrição para lapso após 1 de Outubro, podem instalar a versão do System Center Configuration Manager LTSB actual no momento do intervalo.

[Completos termos e condições para os produtos que comprar através do licenciamento por Volume da Microsoft podem ser encontradas aqui](http://go.microsoft.com/fwlink/?LinkId=800052).

Ver [licenciamento do System Center Configuration Manager e ramificações](learn-more-editions.md) para obter mais informações sobre o licenciamento do Configuration Manager ramos.

## <a name="next-steps"></a>Passos Seguintes

Se decidir que LTSB o Configuration Manager é o ramo correto para o seu ambiente, [instalar um novo LTSB](/sccm/core/understand/install-the-ltsb#install-a-new-site) site como parte de uma nova hierarquia, ou [atualizar um site do System Center 2012 Configuration Manager](/sccm/core/understand/install-the-ltsb#upgrade-from-system-center-2012-configuration-manager)e a hierarquia.

Se não tiver o suporte de instalação, veja [documentação do System Center 2016](https://technet.microsoft.com/system-center-docs/system-center) para obter informações sobre como instalar o System Center 2016, que inclui o suporte de dados que pode utilizar para instalar o LTSB do System Center Configuration Manager.  
