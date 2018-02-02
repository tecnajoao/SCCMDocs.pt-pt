---
title: Preterido para funcionalidades do Configuration Manager
titleSuffix: Configuration Manager
description: "Saiba mais sobre as funcionalidades que já não suporta o System Center Configuration Manager."
ms.custom: na
ms.date: 01/25/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 287a6324-ae65-4d38-b2ef-198d47c91231
caps.latest.revision: 
caps.handback.revision: 
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: d49e0f839106af652f7b49227b6c4f8c957347d9
ms.sourcegitcommit: b13da5ad8ffd58e3b89fa6d7170e1dec3ff130a4
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 02/01/2018
---
# <a name="removed-and-deprecated-features-for-system-center-configuration-manager"></a>Funcionalidades removidas e preteridas do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo descreve as funcionalidades que são removidas do suporte para o System Center Configuration Manager ou serão removidas numa futura atualização (preterida). Este artigo fornece aviso antecipado sobre futuras alterações que podem afetar a utilização do Configuration Manager.  

Esta informação está sujeita a alterações em versões futuras e não pode incluir cada funcionalidade despromovida do Configuration Manager.

## <a name="deprecated-features"></a>Funcionalidades preteridas  

|**Funcionalidade**|**Preterição anunciada pela primeira vez**|**Suporte removido**|  
|-|-|-|  
|Com a chegada da nova experiência de centro de Software na versão 1511, as aplicações que eram apenas no catálogo de aplicações (aplicações disponíveis ao utilizador) agora apresentadas no Centro de Software. </br></br>Com esta funcionalidade principal do catálogo de aplicações agora incluída no Centro de Software, a experiência de catálogo de aplicações baseadas na web deixará de estar disponível nos próximos meses.|11 de Agosto de 2017| Suporte para as extremidades de experiência do utilizador do web site do catálogo de aplicações com a primeira atualização lançada após 1 de Junho de 2018|
|Centro de software tem um aspeto novo e moderno. Nos próximos meses, a versão anterior do Centro de Software já não estará disponível.<br><br>Pode configurar clientes para utilizar o novo Centro de Software, ativando o definição de cliente **agente do computador** > **utilizar o novo Centro de Software**.<br><br>Para obter mais informações acerca do Centro de Software, consulte [planear e configurar a gestão de aplicações no System Center Configuration Manager](https://docs.microsoft.com/sccm/apps/plan-design/plan-for-and-configure-application-management).|13 de Dezembro de 2016|Suporte para a versão anterior do Centro de Software extremidades com a primeira atualização lançada após 1 de Janeiro de 2018.|
|Gestão de discos rígidos virtuais (VHDs) com o Configuration Manager. </br></br>Isto inclui a remoção das opções para criar um novo VHD ou gerir um VHD através de uma sequência de tarefas e a remoção do nó de discos rígidos virtuais a partir da consola do Configuration Manager. </br></br>Quando este suporte é removido, VHDs existentes não serão eliminados, mas deixará de estar acessíveis a partir da consola do Configuration Manager.  |6 de Janeiro de 2017 |Versão 1710|
|As sequências de tarefas: <br /> -Converter disco em dinâmico <br /> -Instalar ferramentas de implementação |18 de Novembro de 2016|Versão 1710|
|Ferramenta de avaliação de atualização do Configuration Manager do System Center. </br></br>A ferramenta de avaliação de atualização depende do System Center Configuration Manager e do Application Compatibility Toolkit (ACT) 6. x. A versão final do ACT foi incluída no Windows 10 v1511 ADK. Como vai haver não existem atualizações adicionais para ACT, suporte para a ferramenta de avaliação da atualização serão descontinuadas. </br></br>A ferramenta de avaliação da atualização foi substituída pelo [atualizar preparação](/sccm/core/clients/manage/upgrade/upgrade-analytics) funcionalidade. Aviso de preterição foi adicionado para o [página de transferência de UAT](https://www.microsoft.com/download/details.aspx?id=37145) no dia 12 de Setembro de 2016. | 12 de Setembro de 2016  | 11 de Julho de 2017 |
|As sequências de tarefas: <br /> -OSDPreserveDriveLetter  <br /><br /> Durante a implementação do sistema operativo, por predefinição, a configuração do Windows agora determina a letra de unidade melhor a utilizar (normalmente c). Se pretender especificar uma unidade diferente a utilizar, pode alterar a localização no passo de sequência de tarefas Aplicar sistema operativo. Vá para o **selecionar a localização onde pretende aplicar este sistema operativo** definição. Selecione **letra de unidade lógica específica** e escolha a unidade que pretende utilizar. |20 de Junho de 2016 |Versão 1606 |
|Proteção de acesso de rede (NAP) - como encontrada no System Center 2012 Configuration Manager|10 de Julho de 2015|Versão 1511|  
|Gestão fora de banda - como encontrada no System Center 2012 Configuration Manager|16 de Outubro de 2015|Versão 1511|



<br></br>
Detalhes adicionais para funcionalidades removidas com a versão 1511 da versão do System Center Configuration Manager:

###  <a name="bkmk_amt"></a>Gestão fora de banda  
 Com o Configuration Manager, o suporte nativo para computadores baseados em AMT da consola do Configuration Manager foi removido.  

-   Computadores baseados em AMT continuam a ser completamente geridos quando utiliza o [suplemento Intel SCS para o Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html). O suplemento permite que aceder às funcionalidades mais recentes para gerir a AMT, ao remover as limitações introduzidas até que o Configuration Manager pudesse incorporar essas alterações.  

-   Gestão fora de banda no System Center 2012 Configuration Manager não é afetada por esta alteração.  

###  <a name="bkmk_nap"></a>Proteção de acesso à rede  
 System Center Configuration Manager removeu o suporte para proteção de acesso à rede. A funcionalidade foi preterida no Windows Server 2012 R2 e é removida do Windows 10.  

 Para alternativas de proteção de acesso da rede, veja a secção *Funcionalidade preterida* na [Política de Rede e Descrição Geral dos Serviços de Acesso](https://technet.microsoft.com/library/hh831683.aspx).

## <a name="more-information"></a>Obter mais informações
Para obter mais informações, consulte:
 - [Removidas e preteridas](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated)
 - O [ciclo de vida de suporte de Microsoft](https://support.microsoft.com/lifecycle) Web site.
 - [Suporte para versões de ramo atual do Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported).
