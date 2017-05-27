---
title: Preterido funcionalidades | Documentos do Microsoft
description: "Saiba mais sobre as funcionalidades, produtos e sistemas operativos que já não suporta o System Center Configuration Manager."
ms.custom: na
ms.date: 3/27/2017
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
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 57b9ab13bda0bb5fa5139e52a4c55ef9524e4097
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="removed-and-deprecated-features-for-system-center-configuration-manager"></a>Funcionalidades removidas e preteridas do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Este tópico descreve as funcionalidades, produtos e sistemas operativos que são removidos do suporte para o System Center Configuration Manager ou serão removidos numa atualização futura (preterida). Isto fornece antecipado aviso sobre as alterações futuras que podem afetar a utilização do Configuration Manager.  

Esta informação está sujeito a alterações com versões futuras e não pode incluir cada funcionalidade despromovida, produto ou sistema operativo.  

## <a name="how-to-use-this-information"></a>Como utilizar estas informações  
Quando um sistema operativo ou funcionalidade primeiro estiver listado como preterido, suporte para utilizá-lo com o Configuration Manager é agendado para ser removido numa versão futura do Configuration Manager. Estas informações são fornecidas para o ajudar a planear alternativas para utilizar essa funcionalidade de ou sistema operativo. Quando a primeira versão do Configuration Manager disponibiliza em que o suporte é removido, este tópico é atualizado para indicar essa versão específica.  

Quando o suporte é removido de um sistema operativo ou funcionalidade, a funcionalidade de ou sistema operativo permanece suportado quando utiliza uma versão anterior do Configuration Manager, desde que versão do Configuration Manager mantém-se no suporte. No entanto, quando utiliza uma versão do Configuration Manager após a data de publicação ou versão indicado, essa versão do Configuration Manager não fornecer suporte.

Por exemplo, se uma funcionalidade foi agendada para ter o respetivo suporte removido com a atualização primeiro lançada depois Setembro de 2016, suporte para essa funcionalidade seria já não está incluída no update 1610, lançado em Outubro de 2016.
-  Com 1610 de atualização, a funcionalidade seria deixará de ser suportada.
-  Este tópico seria atualizado para indicar o suporte foi removido com a versão 1610.
No entanto, se continuar a utilizar uma versão anterior que suporta a funcionalidade, como versão 1602 ou 1606, pode continuar a utilizar essa funcionalidade até que a versão que utiliza mudarem fora do suporte.

Para obter mais informações, consulte:
 - O [ciclo de vida de suporte de Microsoft](https://support.microsoft.com/lifecycle) Web site.
 - [Suporte para versões de ramo atual do Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported).




## <a name="deprecated-operating-systems"></a>Sistemas operativos preteridos
### <a name="server-operating-systems"></a>Sistemas operativos de servidor  

|**Sistemas operativos**|**Preterição comunicada pela primeira vez**|**Suporte removido** |  
|-|-|-|  
|Windows Server 2008|10 de Julho de 2015|Versão 1511 </br></br>Suportam como um sistema de sites é removido. (Ver nota 1).|  
|Windows Server 2008 R2|10 de Julho de 2015| Versão 1702 (ver nota 2)|  

-   Tenha em atenção 1: Este sistema operativo não é suportado para servidores de site ou funções de sistema de sites com a exceção do ponto de distribuição e ponto de distribuição de solicitação. Pode continuar a utilizar este sistema operativo como um ponto de distribuição até preterição deste suporte é anunciada ou do período de suporte alargado este sistema operativo. Para obter mais informações, consulte o artigo [instalação do System Center Configuration Manager CB e LTSB falha no Windows Server 2008](https://support.microsoft.com/help/4015095).

-   Tenha em atenção 2:    A partir da versão 1702, este sistema operativo não é suportado para servidores de site ou a maioria das funções de sistema de sites, no entanto, continuam a versões anteriores ao 1702 para suportar a sua utilização. Este sistema operativo permanecem suportado para o ponto de migração de estado e pontos de distribuição função do sistema de sites (incluindo os pontos de distribuição de solicitação e para PXE e multicast) até preterição deste suporte é anunciada ou este sistema operativo expandido suporte período expira. A partir da versão 1602, pode atualizar o sistema operativo de um servidor de site a partir do Windows Server 2008 R2 para Windows Server 2012 R2 no local.  

     Para obter mais informações sobre a atualização no local de um sistema de operativo de servidores de site, consulte o [no local de atualizar o sistema operativo de servidores de sites que executam o Windows Server 2008 R2](../../../core/plan-design/changes/whats-new-in-version-1602.md#bkmk_UpgradeOS) secção [itens que são alterados no System Center Configuration Manager](../../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md).



### <a name="client-operating-systems"></a>Sistemas operativos cliente  

 A menos que anotou caso contrário, cada sistema operativo que é suportado como um cliente do Configuration Manager é suportado até que a data de fim de suporte expandido desse sistema operativo. Para obter detalhes sobre datas de fim de suporte expandido, consulte o [ciclo de vida de suporte de Microsoft](https://support.microsoft.com/lifecycle). Se o suporte do Configuration Manager para um sistema operativo vai terminar antes da data de fim de suporte expandido, uma data de preterição e a data de remoção do suporte para esse sistema operativo serão aqui apresentados.  

|**Sistemas operativos**|**Preterição comunicada pela primeira vez**|**Suporte removido**|  
|-|-|-|  
|Windows XP|10 de Julho de 2015|Versão 1511|  
|Windows XP Embedded|10 de Julho de 2015|Versão 1702|  
|Windows Server 2003|10 de Julho de 2015|Versão 1511|  
|Windows Server 2003 R2|10 de Julho de 2015|Versão 1511|  
|Windows Vista|10 de Julho de 2015|Versão 1511|  
|Mac OS X 10.6 10.8|10 de Julho de 2015|Versão 1511|  
|Windows Mobile 6.0 6.5|10 de Julho de 2015|Versão 1511|  
|Nokia Symbian Belle|10 de Julho de 2015|Versão 1511|  
|Windows CE 5.0 6.0|10 de Julho de 2015|Versão 1511|  


## <a name="deprecated-support-for-sql-server-versions-as-a-site-database"></a>Suporte preterido para versões do SQL Server como uma base de dados do site  

|**Versões do SQL Server**|**Preterição comunicada pela primeira vez**|**Suporte removido**|   
|-|-|-|  
|SQL Server 2008|10 de Julho de 2015|Versão 1511|  
|SQL Server 2008 R2|10 de Julho de 2015|Versão 1702|  

Se precisar de atualizar a sua versão do SQL Server, recomendamos que os seguintes métodos de fácil à mais complexa.
1. [Atualizar o SQL Server no local](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#a-namebkmksupconfigupgradedbsrva-upgrade-sql-server-on-the-site-database-server) (recomendado).
2. Instalar uma nova versão do SQL Server num computador novo e, em seguida, [utilizar a opção de movimentação datbase](/sccm/core/servers/manage/modify-your-infrastructure#a-namebkmkdbconfiga-modify-the-site-database-configuration) de configuração do Configuration Manager que aponte o servidor do site para o novo SQL Server.
3. Utilize [cópia de segurança e recuperação](/sccm/protect/understand/backup-and-recovery).


## <a name="deprecated-features"></a>Funcionalidades preteridas  

|**Funcionalidade**|**Preterição comunicada pela primeira vez**|**Suporte removido**|  
|-|-|-|  
|Proteção de acesso de rede (NAP) - conforme obtido no System Center 2012 Configuration Manager|10 de Julho de 2015|Versão 1511|  
|Gestão fora de banda - conforme obtido no System Center 2012 Configuration Manager|16 de Outubro de 2015|Versão 1511|
|As sequências de tarefas: <br /> -OSDPreserveDriveLetter  <br /><br /> Durante uma implementação do sistema operativo por predefinição, a configuração do Windows agora determina a letra de unidade melhor utilizar (normalmente c:). Se pretender especificar uma unidade diferente para utilizar, pode alterar a localização no passo de sequência de tarefas Aplicar sistema operativo. Aceda ao **selecionar a localização onde pretende aplicar este sistema operativo** definição, selecione **letra de unidade lógica específica**e selecione a unidade que pretende utilizar. |20 de Junho de 2016 |Versão 1606 |
|As sequências de tarefas: <br /> -Converter disco em dinâmico <br /> -Instalar ferramentas de implementação |18 de Novembro de 2016|Suporte para estas tarefas sequências termina com a atualização primeiro lançada depois de 1 de Junho de 2017.|
|O Centro de Software tem um aspeto moderno e novo. As aplicações que poderiam ter apareceu apenas no catálogo de aplicações de dependentes do Silverlight (aplicações disponíveis para o utilizador) agora são apresentados no Centro de Software, no **aplicações** separador. O catálogo de aplicações ainda podem ser acedido utilizando a ligação a **estado da instalação** separador do Centro de Software.<br><br>Nos próximos meses, a versão anterior do Centro de Software já não estará disponível.<br><br>Pode configurar clientes para utilizar o novo Centro de Software, ativando o definição de cliente, **agente do computador** > **utilizar o Centro de Software novo**.<br><br>Para mais informações sobre o Centro de Software, consulte o artigo [planear e configurar a gestão de aplicações no System Center Configuration Manager](https://docs.microsoft.com/sccm/apps/plan-design/plan-for-and-configure-application-management).|13 de Dezembro de 2016|Para ser comunicadas|
|Gestão de discos rígidos virtuais (VHDs) com o Configuration Manager. </br></br>Isto inclui a remoção das opções para criar um novo VHD ou gerir um VHD utilizando uma sequência de tarefas e a remoção do nó discos rígidos virtuais a partir da consola do Configuration Manager. </br></br>Quando este suporte é removida, VHDs existentes não serão eliminadas, mas deixarão de estar acessíveis a partir da consola do Configuration Manager.  |6 de Janeiro de 2017 |Suporte para VHDs termina com a atualização primeiro lançados depois de 1 de Junho de 2017.|
|Ferramenta de avaliação de atualização do Configuration Manager do System Center. </br></br>A ferramenta de avaliação da atualização depende do System Center Configuration Manager e do Application Compatibility Toolkit (ACT) 6. x. A versão final do ACT foi incluída no ADK v1511 do Windows 10. Conforme vai haver não existem atualizações adicionais para ACT, suporte para a ferramenta de avaliação da atualização serão descontinuadas. </br></br>A ferramenta de avaliação da atualização foi substituída pelo [atualizar preparação](/sccm/core/clients/manage/upgrade/upgrade-analytics) funcionalidade. Aviso de preterição foi adicionado à [página de transferência para UAT](https://www.microsoft.com/download/details.aspx?id=37145) no 9/12/2016. |9/12/2016  | 11 de Julho de 2017 |  


<br></br>
Os detalhes adicionais para funcionalidades removidos com a versão 1511 de lançamento do System Center Configuration Manager:

###  <a name="bkmk_amt"></a>Gestão fora de banda  
 Com o Configuration Manager, suporte nativo para computadores baseados em AMT a partir da consola do Configuration Manager foi removido.  

-   Computadores baseados em AMT continuam a ser completamente geridos quando utiliza o [Intel SCS suplemento para o Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html). O suplemento lhe fornece que acesso às funcionalidades mais recentes para gerir AMT, ao remover limitações introduzidas até que o Configuration Manager foi possível incorporar essas alterações.  

-   Gestão fora de banda no System Center 2012 Configuration Manager não é afetada por esta alteração.  

###  <a name="bkmk_nap"></a>Proteção de acesso à rede  
 System Center Configuration Manager removeu o suporte para proteção de acesso à rede. A funcionalidade foi preterida no Windows Server 2012 R2 e é removida do Windows 10.  

 Para alternativas de proteção de acesso da rede, veja a secção *Funcionalidade preterida* na [Política de Rede e Descrição Geral dos Serviços de Acesso](https://technet.microsoft.com/library/hh831683.aspx).

