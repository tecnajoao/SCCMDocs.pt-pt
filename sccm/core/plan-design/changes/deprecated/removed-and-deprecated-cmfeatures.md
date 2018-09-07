---
title: Funcionalidades preteridas
titleSuffix: Configuration Manager
description: Saiba mais sobre as funcionalidades que já não suporta o Configuration Manager.
ms.date: 08/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 287a6324-ae65-4d38-b2ef-198d47c91231
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: dbebfa1ef5d4851cfd6bbc118c2d7bab30f0b01f
ms.sourcegitcommit: 0d7efd9e064f9d6a9efcfa6a36fd55d4bee20059
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 09/06/2018
ms.locfileid: "43893455"
---
# <a name="removed-and-deprecated-features-for-configuration-manager"></a>Funcionalidades removidas e preteridas para o Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este artigo lista as funcionalidades preteridas ou removidas do suporte do Configuration Manager. Funcionalidades preteridas serão removidas numa atualização futura. Estas alterações futuras podem afetar a utilização do Configuration Manager.  

Estas informações estão sujeitas a alterações em versões futuras. Não pode incluir cada funcionalidade despromovida do Configuration Manager.



## <a name="deprecated-features"></a>Funcionalidades preteridas  

|Funcionalidade|Preterição anunciada pela primeira vez|Suporte&nbsp;removido|  
|-----------|---|--------------|  
|Gestão de dispositivos móveis híbrida. Para obter mais informações, consulte [o que é a MDM híbrida](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->|14 de Agosto de 2018|1 de Setembro de 2019|
|O **experiência de usuário do Silverlight** para o site do catálogo de aplicativos ponto já não é suportado. Os utilizadores devem utilizar o novo Centro de Software. NOTA: Os catálogo site web e de ponto de serviço ponto funções da aplicação ainda são suportadas. Em alguns cenários, o novo Centro de Software se comunica com o ponto de Web site do catálogo de aplicações. Para obter mais informações, consulte [configurar o Centro de Software](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_userex).<!--1358309-->|11 de Agosto de 2017| Versão 1806|
|A versão anterior do Centro de Software.<br><br>Para obter mais informações sobre o novo Centro de Software, consulte [planear e configurar a gestão de aplicações](/sccm/apps/plan-design/plan-for-and-configure-application-management##bkmk_userex).|13 de Dezembro de 2016|Versão 1802|
|Gestão de discos rígidos virtuais (VHDs) com o Configuration Manager. </br></br>Essa depreciação inclui a remoção das opções para criar um novo VHD ou gerir um VHD com uma sequência de tarefas e a remoção do nó de discos rígidos virtuais a partir da consola do Configuration Manager. </br></br>VHDs existentes não são eliminados, mas já não são acessíveis a partir da consola do Configuration Manager.  |6 de Janeiro de 2017 |Versão 1710|
|Sequências de tarefas: <br /> -Converter disco em dinâmico <br /> -Instalar ferramentas de implantação |18 de Novembro de 2016|Versão 1710|
|Ferramenta de avaliação de atualização do Configuration Manager do System Center. </br></br>A ferramenta de avaliação da atualização depende do System Center Configuration Manager e o Application Compatibility Toolkit (ACT) 6.x. A versão final do ACT foi lançada no Windows 10 v1511 ADK. Como não são necessárias mais existam atualizações ao ACT, o suporte para a ferramenta de avaliação de atualização foi descontinuada. </br></br>A ferramenta de avaliação de atualização é substituída pelos [preparação](/sccm/core/clients/manage/upgrade/upgrade-analytics) funcionalidade. Aviso de preterição foi adicionado para o [página de transferência do UAT](https://www.microsoft.com/download/details.aspx?id=37145) 12 de Setembro de 2016. | 12 de Setembro de 2016  | 11 de Julho de 2017 |
|Pontos de atualização de software com um cluster de (NLB) de balanceamento de carga do rede | 27 de Fevereiro de 2016 | Versão 1702 | 
|Sequências de tarefas: <br /> -OSDPreserveDriveLetter  <br /><br /> Durante a implementação do sistema operativo, por predefinição, a configuração do Windows agora determina a melhor letra de unidade a utilizar (normalmente c). Se pretender especificar uma unidade diferente para utilizar, pode alterar o local no passo de sequência de tarefas Aplicar sistema operativo. Vá para o **selecione a localização onde pretende aplicar este sistema operativo** definição. Selecione **letra de unidade lógica específica** e escolha a unidade que pretende utilizar. |20 de Junho de 2016 |Versão 1606 |
|Proteção de acesso de rede (NAP) - como encontrada no System Center 2012 Configuration Manager|10 de Julho de 2015|Versão 1511|  
|Gestão fora de banda - como encontrada no System Center 2012 Configuration Manager|16 de Outubro de 2015|Versão 1511|



## <a name="features-removed-in-version-1511"></a>Funcionalidades removidas na versão 1511
As secções seguintes incluem detalhes adicionais para funcionalidades removidas com a versão 1511:

###  <a name="bkmk_amt"></a> Gestão fora de banda  
 Com o Configuration Manager, o suporte nativo para computadores baseados em AMT partir da consola do Configuration Manager foi removido.  

-   Computadores baseados em AMT continuam a ser completamente geridos quando utiliza a [suplemento Intel SCS para o Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html). O suplemento permite que aceder às funcionalidades mais recentes para gerir a AMT, ao mesmo tempo que elimina as limitações introduzidas até que o Configuration Manager pudesse incorporar essas alterações.  

-   Gestão fora de banda no System Center 2012 Configuration Manager não é afetada por esta alteração.  

###  <a name="bkmk_nap"></a> Proteção de acesso à rede  
 System Center Configuration Manager removeu o suporte para proteção de acesso de rede. A funcionalidade foi preterida no Windows Server 2012 R2 e é removida do Windows 10.  

 Para alternativas de proteção de acesso da rede, veja a secção *Funcionalidade preterida* na [Política de Rede e Descrição Geral dos Serviços de Acesso](https://technet.microsoft.com/library/hh831683.aspx).



## <a name="more-information"></a>Mais informações
Para obter mais informações, consulte:
 - [Removidas e preteridas](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated)
 - [Ciclo de vida do suporte da Microsoft](https://support.microsoft.com/lifecycle)
 - [Suporte para versões de ramo atual do Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported).
