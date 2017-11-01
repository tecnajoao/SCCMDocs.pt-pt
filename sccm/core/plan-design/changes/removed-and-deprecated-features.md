---
title: Funcionalidades preteridas
titleSuffix: Configuration Manager
description: "Saiba mais sobre as funcionalidades, produtos e sistemas operativos que já não suporta a System Center Configuration Manager."
ms.custom: na
ms.date: 08/16/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d8c8b44c-1e8a-42b6-bab4-23c72a0a6169
caps.latest.revision: "15"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 7a87e03cdade6339bc0ea0055edf8791e197e6f1
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/12/2017
---
# <a name="removed-and-deprecated-features-for-system-center-configuration-manager"></a>Funcionalidades removidas e preteridas do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este tópico descreve as funcionalidades, produtos e sistemas operativos que são removidos do suporte para o System Center Configuration Manager ou serão removidos numa futura atualização (preterida). Isto fornece o aviso antecipado sobre futuras alterações que podem afetar a utilização do Configuration Manager.  

Esta informação está sujeita a alterações em versões futuras e não pode incluir cada funcionalidades preteridas, produtos ou sistema operativo.  

## <a name="how-to-use-this-information"></a>Como utilizar estas informações  
Quando um sistema operativo ou de funcionalidade é primeiro listado como preteridos, suporte para utilizá-la com o Configuration Manager está agendado para ser removido numa versão futura do Configuration Manager. Esta informação é fornecida para o ajudar a planear para alternativas para essa funcionalidade ou o sistema operativo a utilizar. Quando a primeira versão do Configuration Manager disponibiliza em que o suporte é removido, este tópico foi atualizado para indicar que a versão específica.  

Quando o suporte é removido de um sistema operativo ou funcionalidade, a funcionalidade ou o sistema operativo continua a ser suportado quando utiliza uma versão anterior do Configuration Manager, desde que essa versão do Configuration Manager permanece no suporte. No entanto, quando utiliza uma versão do Configuration Manager lançada após a data ou versão indicado, essa versão do Configuration Manager não fornece suporte.

Por exemplo, se uma funcionalidade foi agendada com o respetivo suporte removido com a primeira atualização lançada após Setembro de 2016, suporte para essa funcionalidade já não seria ser incluída na atualização 1610, lançada em Outubro de 2016.
-  Com 1610 de atualização, a funcionalidade já não seria suportada.
-  Este tópico seria atualizado para indicar o suporte foi removido com a versão 1610.
No entanto, se continuar a utilizar uma versão anterior que suporta a funcionalidade, como a versão 1602 ou 1606, pode continuar a utilizar essa funcionalidade até a versão que utilizar ignora fora de suporte.

Para obter mais informações, consulte:
 - O [ciclo de vida de suporte de Microsoft](https://support.microsoft.com/lifecycle) Web site.
 - [Suporte para versões de ramo atual do Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported).




## <a name="deprecated-operating-systems"></a>Sistemas de operativos preteridos
### <a name="server-operating-systems"></a>Sistemas operativos de servidor  

|**Sistemas operativos**|**Preterição anunciada pela primeira vez**|**Suporte removido** |  
|-|-|-|  
|Windows Server 2008|10 de Julho de 2015|Versão 1511 </br></br>Suporta como um sistema de sites é removido. (Ver nota 1).|  
|Windows Server 2008 R2|10 de Julho de 2015| Versão 1702 (ver nota 2)|  

-   Nota 1: Este sistema operativo não é suportado para servidores de site ou funções de sistema de sites com a exceção do ponto de distribuição e ponto de distribuição de solicitação. Pode continuar a utilizar este sistema operativo como um ponto de distribuição, até que a desaprovação deste suporte é anunciada ou o período de suporte expandido deste sistema operativo expira. Para obter mais informações, consulte [instalação do System Center Configuration Manager CB e LTSB falha no Windows Server 2008](https://support.microsoft.com/help/4015095).

-   Nota 2:    A partir da versão 1702, este sistema operativo não é suportado para servidores de site ou a maioria das funções do sistema de sites, no entanto, as versões anteriores 1702 continuam a suportar a sua utilização. Este sistema operativo ser suportado para a função de sistema de sites de ponto de distribuição (incluindo pontos de distribuição de extração e para PXE e multicast), até que a desaprovação deste suporte é anunciada ou expandido deste sistema operativo período de suporte expira. A partir da versão 1602, pode atualizar no local o sistema operativo de um servidor de site do Windows Server 2008 R2 para o Windows Server 2012 R2.  

     Para obter mais informações sobre a atualização no local de um sistema de operativo de servidores de site, consulte o [direta atualizar o sistema operativo de servidores de sites que executam o Windows Server 2008 R2](../../../core/plan-design/changes/whats-new-in-version-1602.md#bkmk_UpgradeOS) secção [o que mudou no System Center Configuration Manager](../../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md).



### <a name="client-operating-systems"></a>Sistemas operativos cliente  

 A menos que indicado em contrário, cada sistema operativo que é suportado como um cliente do Configuration Manager é suportado até que a data de fim de suporte alargado desse sistema operativo. Para obter detalhes sobre as datas de fim de suporte expandido, consulte o [ciclo de vida de suporte de Microsoft](https://support.microsoft.com/lifecycle). Se o suporte do Configuration Manager para um sistema operativo termine a data de fim de suporte expandido, uma data de preterição e data de remoção de suporte para esse sistema operativo serão listadas aqui.  

|**Sistemas operativos**|**Preterição anunciada pela primeira vez**|**Suporte removido**|  
|-|-|-|  
|Windows XP|10 de Julho de 2015|Versão 1511|  
|Windows XP Embedded <br><br> Isto inclui todos os [sistemas de operativos incorporados baseados no XP](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices#windows-embedded-computers).|10 de Julho de 2015|Versão 1702|  
|Windows Server 2003|10 de Julho de 2015|Versão 1511|  
|Windows Server 2003 R2|10 de Julho de 2015|Versão 1511|  
|Windows Vista|10 de Julho de 2015|Versão 1511|  
|Mac OS X 10.6 10.8|10 de Julho de 2015|Versão 1511|  
|Windows Mobile 6.0 6.5|10 de Julho de 2015|Versão 1511|  
|Nokia Symbian Belle|10 de Julho de 2015|Versão 1511|  
|Windows CE 5.0 6.0|10 de Julho de 2015|Versão 1511|  


## <a name="deprecated-support-for-sql-server-versions-as-a-site-database"></a>Suporte preterido para versões do SQL Server como uma base de dados do site  

|**Versões do SQL Server**|**Preterição anunciada pela primeira vez**|**Suporte removido**|   
|-|-|-|  
|SQL Server 2008|10 de Julho de 2015|Versão 1511|  
|SQL Server 2008 R2|10 de Julho de 2015|Versão 1702|  

Se precisar de atualizar a sua versão do SQL Server, recomendamos os seguintes métodos, de fácil mais complexas.
1. [Atualizar o SQL Server no local](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#a-namebkmksupconfigupgradedbsrva-upgrade-sql-server-on-the-site-database-server) (recomendado).
2. Instalar uma nova versão do SQL Server num novo computador e, em seguida, [utilizar a opção de mover a base de dados](/sccm/core/servers/manage/modify-your-infrastructure#a-namebkmkdbconfiga-modify-the-site-database-configuration) de configuração do Configuration Manager para apontar o seu servidor do site para o novo SQL Server.
3. Utilize [cópia de segurança e recuperação](/sccm/protect/understand/backup-and-recovery).


## <a name="deprecated-features"></a>Funcionalidades preteridas  

|**Funcionalidade**|**Preterição anunciada pela primeira vez**|**Suporte removido**|  
|-|-|-|  
|Proteção de acesso de rede (NAP) - como encontrada no System Center 2012 Configuration Manager|10 de Julho de 2015|Versão 1511|  
|Gestão fora de banda - como encontrada no System Center 2012 Configuration Manager|16 de Outubro de 2015|Versão 1511|
|As sequências de tarefas: <br /> -OSDPreserveDriveLetter  <br /><br /> Durante a implementação do sistema operativo, por predefinição, a configuração do Windows agora determina a letra de unidade melhor a utilizar (normalmente c). Se pretender especificar uma unidade diferente a utilizar, pode alterar a localização no passo de sequência de tarefas Aplicar sistema operativo. Vá para o **selecionar a localização onde pretende aplicar este sistema operativo** definição, selecione **letra de unidade lógica específica**e escolha a unidade que pretende utilizar. |20 de Junho de 2016 |Versão 1606 |
|As sequências de tarefas: <br /> -Converter disco em dinâmico <br /> -Instalar ferramentas de implementação |18 de Novembro de 2016|Suporte para estas tarefas sequências extremidades com a primeira atualização lançada após 1 de Junho de 2017.|
|Centro de software tem um aspeto novo e moderno. Nos próximos meses, a versão anterior do Centro de Software já não estará disponível.<br><br>Pode configurar clientes para utilizar o novo Centro de Software, ativando o definição de cliente **agente do computador** > **utilizar o novo Centro de Software**.<br><br>Para obter mais informações acerca do Centro de Software, consulte [planear e configurar a gestão de aplicações no System Center Configuration Manager](https://docs.microsoft.com/sccm/apps/plan-design/plan-for-and-configure-application-management).|13 de Dezembro de 2016|Suporte para a versão anterior do Centro de Software extremidades com a primeira atualização lançada após 1 de Janeiro de 2018.|
|Com a chegada da nova experiência de centro de Software na versão 1511, as aplicações que eram apenas no catálogo de aplicações (aplicações disponíveis ao utilizador) agora apresentadas no Centro de Software. </br></br>Com esta funcionalidade principal do catálogo de aplicações agora incluída no Centro de Software, a experiência de catálogo de aplicações baseadas na web deixará de estar disponível nos próximos meses.|11 de Agosto de 2017| Suporte para as extremidades de experiência do utilizador do web site do catálogo de aplicações com a primeira atualização lançada após 1 de Junho de 2018|
|Gestão de discos rígidos virtuais (VHDs) com o Configuration Manager. </br></br>Isto inclui a remoção das opções para criar um novo VHD ou gerir um VHD através de uma sequência de tarefas e a remoção do nó de discos rígidos virtuais a partir da consola do Configuration Manager. </br></br>Quando este suporte é removido, VHDs existentes não serão eliminados, mas deixará de estar acessíveis a partir da consola do Configuration Manager.  |6 de Janeiro de 2017 |Suporte para os VHDs extremidades com a primeira atualização lançada após 1 de Junho de 2017.|
|Ferramenta de avaliação de atualização do Configuration Manager do System Center. </br></br>A ferramenta de avaliação de atualização depende do System Center Configuration Manager e do Application Compatibility Toolkit (ACT) 6. x. A versão final do ACT foi incluída no Windows 10 v1511 ADK. Como vai haver não existem atualizações adicionais para ACT, suporte para a ferramenta de avaliação da atualização serão descontinuadas. </br></br>A ferramenta de avaliação da atualização foi substituída pelo [atualizar preparação](/sccm/core/clients/manage/upgrade/upgrade-analytics) funcionalidade. Aviso de preterição foi adicionado para o [página de transferência de UAT](https://www.microsoft.com/download/details.aspx?id=37145) no 9/12/2016. |9/12/2016  | 11 de Julho de 2017 |


<br></br>
Detalhes adicionais para funcionalidades removidas com a versão 1511 da versão do System Center Configuration Manager:

###  <a name="bkmk_amt"></a>Gestão fora de banda  
 Com o Configuration Manager, o suporte nativo para computadores baseados em AMT da consola do Configuration Manager foi removido.  

-   Computadores baseados em AMT continuam a ser completamente geridos quando utiliza o [suplemento Intel SCS para o Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html). O suplemento permite que aceder às funcionalidades mais recentes para gerir a AMT, ao remover as limitações introduzidas até que o Configuration Manager pudesse incorporar essas alterações.  

-   Gestão fora de banda no System Center 2012 Configuration Manager não é afetada por esta alteração.  

###  <a name="bkmk_nap"></a>Proteção de acesso à rede  
 System Center Configuration Manager removeu o suporte para proteção de acesso à rede. A funcionalidade foi preterida no Windows Server 2012 R2 e é removida do Windows 10.  

 Para alternativas de proteção de acesso da rede, veja a secção *Funcionalidade preterida* na [Política de Rede e Descrição Geral dos Serviços de Acesso](https://technet.microsoft.com/library/hh831683.aspx).
