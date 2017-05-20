---
title: "Planear relatórios | Documentos do Microsoft"
description: "A partir de detalhes de instalação para segurança e de largura de banda de rede, é importante planear relatórios no Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: ff920c84-d5c8-458c-b67f-bc7219b05690
caps.latest.revision: 6
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 119f501057bf44e483be31db20b88326b3d05ebb
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="planning-for-reporting-in-system-center-configuration-manager"></a>Planeamento de relatórios no System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Relatórios no System Center Configuration Manager fornecem um conjunto de ferramentas e recursos que ajudam a utilizam as capacidades avançadas de relatórios do SQL Server Reporting Services. Utilize as secções seguintes para ajudar a planear relatórios no Configuration Manager.  

##  <a name="BKMK_InstallReportingServicesPoint"></a> Determinar onde instalar o Ponto do Reporting Services  
 Quando executa relatórios do Configuration Manager num site, os relatórios têm acessos às informações na base de dados de site que se ligam. Utilize as secções seguintes para o ajudar a determinar onde deve instalar o ponto do Reporting Services e qual a origem de dados a utilizar.  

> [!NOTE]  
>  Para obter mais informações sobre o planeamento de sistemas de sites no Configuration Manager, consulte o artigo [adicionar funções do sistema de sites](../deploy/configure/add-site-system-roles.md).  

###  <a name="BKMK_SupportedSiteServers"></a> Servidores do sistema de sites suportados  
 É possível instalar o ponto do Reporting Services num site de administração central, em sites primários, em vários sistemas de sites num site e noutros sites da hierarquia. O ponto do Reporting Services não é suportado em sites secundários. O primeiro ponto do Reporting Services num site é configurado como o servidor de relatórios predefinido. Pode adicionar mais pontos do reporting services num site, mas o servidor de relatórios predefinido em cada site é utilizado ativamente para relatórios do Configuration Manager. É possível instalar o ponto do Reporting Services no servidor do site ou num sistema de sites remoto. No entanto, como melhor prática por motivos de desempenho, utilize o Reporting Services num servidor do sistema de sites remoto.  

###  <a name="BKMK_DataReplication"></a> Considerações sobre replicação de dados  
 O Configuration Manager classifica os dados que replica como dados globais ou dados do site. Os dados globais referem-se a objetos criados por utilizadores administrativos e replicados em todos os sites ao longo da hierarquia, enquanto os sites secundários recebem apenas um subconjunto dos dados globais. São exemplos de dados globais as implementações de software, as atualizações de software, as coleções e os âmbitos de segurança da administração baseada em funções. Dados do site refere-se a informações operacionais que sites primários do Configuration Manager e os clientes que criar relatório para sites primários. Os dados do site replicam para o site de administração central, mas não para outros sites primários. São exemplos de dados do site os dados de inventário de hardware, as mensagens de estado, os alertas e os resultados de coleções baseadas em consulta. Os dados do site apenas são visíveis no site de administração central e no site primário de origem dos dados.  

 Considere os seguintes fatores para o ajudar a determinar onde instalar os pontos do Reporting Services:  

-   Um ponto do reporting services com a base de dados do site de administração central como origem de dados relatório tem acesso a todos os globais e os dados do site na hierarquia do Configuration Manager. Se forem necessários relatórios que contenham dados do site para vários sites numa hierarquia, considere a instalação do reporting services num sistema de sites no site de administração central de pontos e utilizar a base de dados do site de administração central como origem de dados do relatório.  

-   Um ponto do Reporting Services que tenha a base de dados de um site primário subordinado como origem de dados do relatório tem acesso a dados globais e a dados do site apenas no site primário local e em todos os sites secundários subordinados. Dados do site para outros sites primários na hierarquia do Configuration Manager não são replicados para o site primário e, por conseguinte, Reporting Services não é possível aceder ao mesmo. Se forem necessários relatórios que contenham dados do site para um site primário específico ou dados globais, mas não pretende que o utilizador do relatório tenha acesso aos dados do site de outros sites primários, instale um ponto do reporting services num sistema de sites no site primário e utilizar a base de dados do site primário como origem de dados do relatório.  

###  <a name="BKMK_NetworkBandwidth"></a> Considerações sobre largura de banda da rede  
 Os servidores do sistema de sites no mesmo site comunicam entre si através da utilização do bloco de mensagem de servidor (SMB), de HTTP ou de HTTPS, dependendo da forma como configurar o site. Uma vez que estas comunicações não são geridas e podem ocorrer em qualquer altura sem controlo da largura de banda da rede, reveja a largura de banda da rede disponível antes de instalar a função ponto do Reporting Services num sistema de sites.  

> [!NOTE]  
>  Para obter mais informações sobre o planeamento de sistemas de sites, consulte o artigo [adicionar funções do sistema de sites](../deploy/configure/add-site-system-roles.md).  

##  <a name="BKMK_RoleBaseAdministration"></a> Planeamento da administração baseada em funções para relatórios  
 Segurança para relatórios é idêntica de outros objetos no Configuration Manager onde pode atribuir funções de segurança e permissões a utilizadores administrativos. Os utilizadores administrativos só podem executar e modificar relatórios para os quais têm direitos de segurança adequados. Para executar relatórios na consola do Configuration Manager, tem de ter o **leitura** para a direita para a **Site** permissões e as permissões configuradas para objetos específicos.  

 No entanto, ao contrário de outros objetos no Configuration Manager, os direitos de segurança definidos para os utilizadores administradores na consola do Configuration Manager devem igualmente ser configurados no Reporting Services. Ao configurar direitos de segurança na consola do Configuration Manager, o ponto do reporting services liga ao Reporting Services e define as permissões adequadas para relatórios. Por exemplo, a função de segurança **Gestor de Atualizações de Software** possui as permissões **Executar Relatório** e **Ler Relatório** associadas à função. Os utilizadores administrativos que apenas têm atribuída a função **Gestor de Atualizações de Software** só podem executar e modificar relatórios para atualizações de software. Relatórios de outros objetos não são apresentados na consola do Configuration Manager. A exceção é que alguns relatórios não estão associados a objetos com capacidade de segurança específicos do Configuration Manager. Para esses relatórios, o utilizador administrativo deve possuir o direito **Ler** para a permissão do **Site** para executar os relatórios e o direito **Modificar** para a permissão do **Site** para modificar os relatórios.  

 Os relatórios têm o suporte de administração baseada em funções ativado. Os dados para todos os relatórios incluídos com o Configuration Manager são filtrados com base nas permissões do utilizador administrativo que executa o relatório. Os utilizadores administrativos com funções específicas apenas podem ver informações definidas para as respetivas funções.  

 Para obter mais informações sobre direitos de segurança para relatórios, consulte o artigo [configurar reporting](configuring-reporting.md).  

 Para obter mais informações sobre a administração baseada em funções no Configuration Manager, consulte o artigo [configurar a administração baseada em funções](../deploy/configure/configure-role-based-administration.md).  

## <a name="next-steps"></a>Passos seguintes  
 Utilize os tópicos adicionais seguintes para ajudar a planear relatórios no Configuration Manager:  

-   [Pré-requisitos para relatórios no System Center Configuration Manager](../../../core/servers/manage/prerequisites-for-reporting.md)  
-   [Melhores práticas para relatórios no System Center Configuration Manager](../../../core/servers/manage/best-practices-for-reporting.md)  

