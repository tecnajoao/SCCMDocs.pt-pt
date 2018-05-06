---
title: Funcionalidades preteridas
titleSuffix: Configuration Manager
description: Saiba mais sobre as funcionalidades que já não suporta o System Center Configuration Manager.
ms.date: 05/01/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 287a6324-ae65-4d38-b2ef-198d47c91231
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 967c0ff71af5b3586568bf3f5d2fee7ed5b8bb06
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 05/03/2018
---
# <a name="removed-and-deprecated-features-for-system-center-configuration-manager"></a>Funcionalidades removidas e preteridas do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo apresenta as funcionalidades são preteridas ou removidas do suporte para o Configuration Manager. Funcionalidades preteridas serão removidas numa atualização futura. Estas alterações futuras podem afetar a utilização do Configuration Manager.  

Estas informações estão sujeitas a alterações em versões futuras. Poderá não incluir cada funcionalidade despromovida do Configuration Manager.



## <a name="deprecated-features"></a>Funcionalidades preteridas  

|Funcionalidade|Preterição anunciada pela primeira vez|Suporte&nbsp;removido|  
|-----------|---|--------------|  
|Aplicações disponíveis ao utilizador que anteriormente eram apenas no catálogo de aplicações agora apresentada no Centro de Software novo. </br></br>Por conseguinte, a experiência de catálogo de aplicações baseadas na web não estarão disponível nos próximos meses.|11 de Agosto de 2017| Suporte para as extremidades de experiência de utilizador de web site de catálogo do aplicações com a primeira atualização lançada após 1 de Junho de 2018|
|A versão anterior do Centro de Software.<br><br>Para mais informações sobre o novo Centro de Software, consulte [planear e configurar a gestão de aplicações](/sccm/apps/plan-design/plan-for-and-configure-application-management#configure-software-center-and-the-application-catalog-windows-pcs-only).|13 de Dezembro de 2016|Versão 1802|
|Gestão de discos rígidos virtuais (VHDs) com o Configuration Manager. </br></br>Este descontinuação inclui a remoção das opções para criar um novo VHD ou gerir um VHD através de uma sequência de tarefas e a remoção do nó de discos rígidos virtuais a partir da consola do Configuration Manager. </br></br>VHDs existentes não são eliminados, mas deixam de ser acessíveis a partir da consola do Configuration Manager.  |6 de Janeiro de 2017 |Versão 1710|
|As sequências de tarefas: <br /> -Converter disco em dinâmico <br /> -Instalar ferramentas de implementação |18 de Novembro de 2016|Versão 1710|
|Ferramenta de avaliação de atualização do Configuration Manager do System Center. </br></br>A ferramenta de avaliação de atualização depende do System Center Configuration Manager e do Application Compatibility Toolkit (ACT) 6. x. A versão final do ACT foi incluída no Windows 10 v1511 ADK. Como não são necessárias mais existam atualizações ao ATO, suporte para a ferramenta de avaliação da atualização foi descontinuada. </br></br>A ferramenta de avaliação da atualização foi substituída pelo [atualizar preparação](/sccm/core/clients/manage/upgrade/upgrade-analytics) funcionalidade. Aviso de preterição foi adicionado para o [página de transferência de UAT](https://www.microsoft.com/download/details.aspx?id=37145) no dia 12 de Setembro de 2016. | 12 de Setembro de 2016  | 11 de Julho de 2017 |
|As sequências de tarefas: <br /> -OSDPreserveDriveLetter  <br /><br /> Durante a implementação do sistema operativo, por predefinição, a configuração do Windows agora determina a letra de unidade melhor a utilizar (normalmente c). Se pretender especificar uma unidade diferente a utilizar, pode alterar a localização no passo de sequência de tarefas Aplicar sistema operativo. Vá para o **selecionar a localização onde pretende aplicar este sistema operativo** definição. Selecione **letra de unidade lógica específica** e escolha a unidade que pretende utilizar. |20 de Junho de 2016 |Versão 1606 |
|Proteção de acesso de rede (NAP) - como encontrada no System Center 2012 Configuration Manager|10 de Julho de 2015|Versão 1511|  
|Gestão fora de banda - como encontrada no System Center 2012 Configuration Manager|16 de Outubro de 2015|Versão 1511|



## <a name="features-removed-in-version-1511"></a>Funcionalidades removidas na versão 1511
As secções seguintes incluem detalhes adicionais para funcionalidades removidas com a versão 1511:

###  <a name="bkmk_amt"></a> Gestão fora de banda  
 Com o Configuration Manager, o suporte nativo para computadores baseados em AMT da consola do Configuration Manager foi removido.  

-   Computadores baseados em AMT continuam a ser completamente geridos quando utiliza o [suplemento Intel SCS para o Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html). O suplemento permite que aceder às funcionalidades mais recentes para gerir a AMT, ao remover as limitações introduzidas até que o Configuration Manager pudesse incorporar essas alterações.  

-   Gestão fora de banda no System Center 2012 Configuration Manager não é afetada por esta alteração.  

###  <a name="bkmk_nap"></a> Proteção de acesso à rede  
 System Center Configuration Manager removeu o suporte para proteção de acesso à rede. A funcionalidade foi preterida no Windows Server 2012 R2 e é removida do Windows 10.  

 Para alternativas de proteção de acesso da rede, veja a secção *Funcionalidade preterida* na [Política de Rede e Descrição Geral dos Serviços de Acesso](https://technet.microsoft.com/library/hh831683.aspx).



## <a name="more-information"></a>Mais informações
Para obter mais informações, consulte:
 - [Removidas e preteridas](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated)
 - [Ciclo de vida do suporte da Microsoft](https://support.microsoft.com/lifecycle)
 - [Suporte para versões de ramo atual do Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported).
