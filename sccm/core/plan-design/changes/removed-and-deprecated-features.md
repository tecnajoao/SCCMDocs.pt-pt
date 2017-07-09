---
title: Recursos preteridos | Microsoft Docs
description: "Saiba mais sobre os recursos, produtos e sistemas operacionais que o System Center Configuration Manager não oferece mais suporte."
ms.custom: na
ms.date: 06/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d8c8b44c-1e8a-42b6-bab4-23c72a0a6169
caps.latest.revision: 15
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0ec241d07f51b80b84d65676ef1207b31a9a9983
ms.openlocfilehash: e23acf743d8f73afd213c44c3728d1b66d7e558f
ms.contentlocale: pt-pt
ms.lasthandoff: 06/28/2017


---
# <a name="removed-and-deprecated-features-for-system-center-configuration-manager"></a>Funcionalidades removidas e preteridas do System Center Configuration Manager

*Aplica-se a: System Center Configuration Manager (ramificação atual)*

Este tópico descreve os recursos, produtos e sistemas operacionais que foram removidos do suporte para o System Center Configuration Manager, ou que serão removidos em uma atualização futura (preterida). Isso fornece um aviso antecipado sobre futuras alterações que podem afetar o uso do Configuration Manager.  

Essas informações estão sujeitas a alterações em versões futuras e podem não incluir cada recurso preterido, produto ou sistema operacional.  

## <a name="how-to-use-this-information"></a>Como usar essas informações  
Quando um recurso ou o sistema operacional é primeiro listado como preteridos, suporte para usá-lo com o Configuration Manager está programado para ser removido em uma versão futura do Configuration Manager. Essas informações são fornecidas para ajudá-lo a planejar alternativas para usar esse recurso ou o sistema operacional. Quando a primeira versão do Configuration Manager versões no qual o suporte foi removido, este tópico foi atualizado para indicar que a versão específica.  

Quando o suporte foi removido para um recurso ou o sistema operacional, o sistema operacional ou o recurso permanece com suporte quando você usa uma versão anterior do Configuration Manager, desde que essa versão do Configuration Manager permaneça no suporte. No entanto, quando você usa uma versão do Configuration Manager lançados após a data ou indicado, essa versão do Configuration Manager não dá suporte.

Por exemplo, se um recurso foi agendado para ter seu suporte removida com a primeira atualização liberada após setembro de 2016, o suporte para esse recurso não mais ser incluída na atualização 1610, que lançado em outubro de 2016.
-  Com atualização 1610, o recurso seria não mais suporte.
-  Este tópico será atualizado para indicar o suporte foi removido com versão 1610.
No entanto, se você continuar a usar uma versão anterior que suporta o recurso, como a versão 1602 ou 1606, você pode continuar a usar esse recurso até que a versão que você use descarta sem suporte.

Para obter mais informações, consulte:
 - O [Microsoft Support Lifecycle](https://support.microsoft.com/lifecycle) site.
 - [Suporte para versões de ramificação atual do Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported).




## <a name="deprecated-operating-systems"></a>Sistemas operacionais preteridos
### <a name="server-operating-systems"></a>Sistemas operacionais de servidor  

|**Sistemas operacionais**|**Substituição anunciada pela primeira vez**|**Suporte removido** |  
|-|-|-|  
|Windows Server 2008|10 de julho de 2015|Versão 1511 </br></br>Suporte de um sistema de site é removido. (Consulte a Observação 1).|  
|Windows Server 2008 R2|10 de julho de 2015| Versão 1702 (veja a Observação 2)|  

-   Observação 1: Não há suporte para este sistema operacional para servidores do site ou funções de sistema de site com a exceção do ponto de distribuição e ponto de distribuição de recepção. Você pode continuar a usar este sistema operacional como um ponto de distribuição até que a desaprovação desse suporte seja anunciada ou o período de suporte estendido deste sistema operacional expire. Para obter mais informações, consulte [LTSB e instalação do System Center Configuration Manager CB falhar no Windows Server 2008](https://support.microsoft.com/help/4015095).

-   Observação 2:    A partir da versão 1702, este sistema operacional não há servidores do site ou a maioria das funções do sistema de site, no entanto, as versões anteriores à 1702 continuam dar suporte ao seu uso. Este sistema operacional permanecem com suporte para a função de sistema de site do ponto de distribuição (incluindo pontos de distribuição de recepção e para PXE e multicast) até que a desaprovação desse suporte seja anunciada ou estendido do sistema operacional suporte expirar. A partir da versão 1602, você pode atualizar o sistema operacional de um servidor de site do Windows Server 2008 R2 para o Windows Server 2012 R2 no local.  

     Para obter mais informações sobre a atualização in-loco de um sistema de operacional de servidores de site, consulte o [in-loco o sistema operacional de servidores de site que executam o Windows Server 2008 R2](../../../core/plan-design/changes/whats-new-in-version-1602.md#bkmk_UpgradeOS) seção [o que mudou no System Center Configuration Manager](../../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md).



### <a name="client-operating-systems"></a>Sistemas operacionais cliente  

 A menos que indicado de outra forma, cada sistema operacional com suporte como um cliente do Configuration Manager terá suporte até a data de término de suporte estendido do sistema operacional. Para obter detalhes sobre as datas de fim de suporte estendido, consulte o [Microsoft Support Lifecycle](https://support.microsoft.com/lifecycle). Se o suporte do Configuration Manager para um sistema operacional terminar antes da data de término suporte estendido, uma data de substituição e a data de remoção de suporte para o sistema operacional serão listadas aqui.  

|**Sistemas operacionais**|**Substituição anunciada pela primeira vez**|**Suporte removido**|  
|-|-|-|  
|Windows XP|10 de julho de 2015|Versão 1511|  
|Windows XP Embedded|10 de julho de 2015|Versão 1702|  
|Windows Server 2003|10 de julho de 2015|Versão 1511|  
|Windows Server 2003 R2|10 de julho de 2015|Versão 1511|  
|Windows Vista|10 de julho de 2015|Versão 1511|  
|Mac OS X 10.6 10.8|10 de julho de 2015|Versão 1511|  
|Windows Mobile 6.0 6.5|10 de julho de 2015|Versão 1511|  
|Nokia Symbian Belle|10 de julho de 2015|Versão 1511|  
|Windows CE 5.0 6.0|10 de julho de 2015|Versão 1511|  


## <a name="deprecated-support-for-sql-server-versions-as-a-site-database"></a>Suporte preterido para versões do SQL Server como um banco de dados do site  

|**Versões do SQL Server**|**Substituição anunciada pela primeira vez**|**Suporte removido**|   
|-|-|-|  
|SQL Server 2008|10 de julho de 2015|Versão 1511|  
|SQL Server 2008 R2|10 de julho de 2015|Versão 1702|  

Se você precisar atualizar a versão do SQL Server, recomendamos os seguintes métodos, de fácil mais complexas.
1. [Atualização do SQL Server no local](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#a-namebkmksupconfigupgradedbsrva-upgrade-sql-server-on-the-site-database-server) (recomendado).
2. Instalar uma nova versão do SQL Server em um novo computador e, em seguida, [usar a opção de mover banco](/sccm/core/servers/manage/modify-your-infrastructure#a-namebkmkdbconfiga-modify-the-site-database-configuration) de instalação do Configuration Manager para apontar o servidor do site para o novo SQL Server.
3. Use [backup e recuperação](/sccm/protect/understand/backup-and-recovery).


## <a name="deprecated-features"></a>Recursos preteridos  

|**Recurso**|**Substituição anunciada pela primeira vez**|**Suporte removido**|  
|-|-|-|  
|Proteção de acesso à rede (NAP) - como encontrado no System Center 2012 Configuration Manager|10 de julho de 2015|Versão 1511|  
|Gerenciamento fora da banda - como encontrado no System Center 2012 Configuration Manager|16 de outubro de 2015|Versão 1511|
|Sequências de tarefas: <br /> -OSDPreserveDriveLetter  <br /><br /> Durante uma implantação de sistema operacional, por padrão, a instalação do Windows agora determina a melhor letra da unidade a ser usado (geralmente, c). Se você deseja especificar uma unidade diferente para usar, você pode alterar o local na etapa da sequência de tarefas aplicar sistema operacional. Vá para o **selecione o local onde você deseja aplicar este sistema operacional** configuração, selecione **letra de unidade lógica específica**e escolher a unidade que você deseja usar. |20 de junho de 2016 |Versão 1606 |
|Sequências de tarefas: <br /> -Converter disco em dinâmico <br /> -Instalar ferramentas de implantação |18 de novembro de 2016|Suporte para essas tarefas sequências termina com a primeira atualização liberada após 1 de junho de 2017.|
|O Centro de Software tem uma aparência nova e moderna. Aplicativos que antes eram exibidos somente no catálogo de aplicativos dependente do Silverlight (aplicativos disponíveis para o usuário) agora aparecem no Centro de Software, no **aplicativos** guia. O catálogo de aplicativos ainda podem ser acessado usando o link no **Status da instalação** guia do Centro de Software.<br><br>Nos próximos meses, a versão anterior do Centro de Software não estarão disponível.<br><br>Você pode configurar clientes para usar o novo centro de Software habilitando o configuração do cliente, **computador agente** > **usar o novo centro de Software**.<br><br>Para obter mais informações sobre o Centro de Software, consulte [planejar e configurar o gerenciamento de aplicativos no System Center Configuration Manager](https://docs.microsoft.com/sccm/apps/plan-design/plan-for-and-configure-application-management).|13 de dezembro de 2016|Suporte para a versão anterior do Centro de Software termina com a primeira atualização liberada após 1 de janeiro de 2018.|
|Gerenciamento de discos de rígidos virtuais (VHDs) com o Configuration Manager. </br></br>Isso inclui a remoção de opções para criar um novo VHD ou gerenciar um VHD usando uma sequência de tarefas e a remoção do nó de discos rígidos virtuais do console do Configuration Manager. </br></br>Quando esse suporte é removido, VHDs existentes não serão excluídos, mas não poderá ser acessados de dentro do console do Configuration Manager.  |6 de janeiro de 2017 |Suporte para VHDs termina com a primeira atualização liberada após 1 de junho de 2017.|
|Ferramenta de avaliação de atualização do Configuration Manager do System Center. </br></br>A ferramenta de avaliação de atualização depende do System Center Configuration Manager e o Application Compatibility Toolkit (ACT) 6. x. A versão final do ACT foi fornecida no Windows 10 v1511 ADK. Como haverá nenhuma atualização adicional para ATUAR, suporte para a ferramenta de avaliação de atualização será descontinuada. </br></br>A ferramenta de avaliação de atualização é substituída pelo [preparação de atualização](/sccm/core/clients/manage/upgrade/upgrade-analytics) recurso. Aviso de substituição foi adicionado para o [página de download para UAT](https://www.microsoft.com/download/details.aspx?id=37145) em 12/9/2016. |9/12/2016  | 11 de julho de 2017 |  


<br></br>
Detalhes adicionais para recursos removidos com a versão 1511 da versão do System Center Configuration Manager:

###  <a name="bkmk_amt"></a>Gerenciamento fora da banda  
 Com o Configuration Manager, o suporte nativo para computadores baseados em AMT de dentro do console do Configuration Manager foi removido.  

-   Computadores baseados em AMT permanecem totalmente gerenciados, quando você usa o [complemento Intel SCS para o Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html). O complemento fornece que acesso aos recursos mais recentes para gerenciar o AMT, ao mesmo tempo que remove as limitações introduzidas até que o Configuration Manager possa incorporar essas alterações.  

-   Gerenciamento fora de banda no System Center 2012 Configuration Manager não é afetado por essa alteração.  

###  <a name="bkmk_nap"></a>Proteção de acesso à rede  
 System Center Configuration Manager removeu o suporte para proteção de acesso à rede. O recurso foi preterido no Windows Server 2012 R2 e removido do Windows 10.  

 Para alternativas de proteção de acesso da rede, veja a secção *Funcionalidade preterida* na [Política de Rede e Descrição Geral dos Serviços de Acesso](https://technet.microsoft.com/library/hh831683.aspx).

