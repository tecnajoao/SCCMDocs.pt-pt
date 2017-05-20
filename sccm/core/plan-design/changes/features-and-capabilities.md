---
title: Funcionalidades e capacidades | Documentos do Microsoft
description: "Saiba mais sobre as capacidades de gestão principal do System Center Configuration Manager."
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5d388399-07ca-431c-a9b2-56c69771aa87
caps.latest.revision: 18
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Machine Translation
ms.sourcegitcommit: 53b27dcb5c8bb670556fe4cee9e990619a9a63e9
ms.openlocfilehash: 4691f43dccdf73936107f4635321897b9779bead
ms.contentlocale: pt-pt
ms.lasthandoff: 05/17/2017


---
# <a name="features-and-capabilities-of-system-center-configuration-manager"></a>Funcionalidades e capacidades removidas do System Center Configuration Manager

*Aplica-se a: O System Center Configuration Manager (ramo atual)*

Seguem-se as principais capacidades de gestão do System Center Configuration Manager. Cada capacidade tem os seus pré-requisitos e as capacidades que pretender utilizar podem influenciar a estrutura e a implementação da hierarquia do Configuration Manager. Por exemplo, se pretender implementar software nos dispositivos na sua hierarquia, tem de instalar a função de sistema de sites de ponto de distribuição.  

 Para mais informações sobre como planear e instalar o Configuration Manager para suportar estas capacidades de gestão no seu ambiente, consulte o artigo [Prepare-se para o System Center Configuration Manager](../../../core/plan-design/get-ready.md).  

 **Gestão de aplicações**  

 Fornece um conjunto de ferramentas e recursos que o podem ajudar a criar, gerir, implementar e monitorizar aplicações numa gama de diferentes dispositivos que gere. Além disso, o Configuration Manager oferece com ferramentas que ajudam a proteger dados da sua empresa nas aplicações do utilizador. Consulte o artigo [introdução à gestão de aplicações](/sccm/apps/understand/introduction-to-application-management).

 **Acesso a recursos da empresa**  

 Fornece um conjunto de ferramentas e recursos que lhe permite conceder aos utilizadores da organização acesso a dados e aplicações de localizações remotas. Essas ferramentas incluem perfis Wi-Fi, perfis VPN, perfis de certificado e o acesso condicional para Exchange e SharePoint online. Consulte o artigo [proteger dados e o site de infraestrutura com o System Center Configuration Manager](../../../protect/understand/protect-data-and-site-infrastructure.md) e [gerir o acesso aos serviços no System Center Configuration Manager](../../../protect/deploy-use/manage-access-to-services.md).  

 **Definições de compatibilidade**  

 Fornece um conjunto de ferramentas e recursos que podem ajudar a avaliar, controlar e remediar a compatibilidade de configuração de dispositivos de cliente na empresa. Além disso, pode utilizar definições de compatibilidade para configurar uma variedade de funcionalidades e definições de segurança nos dispositivos que gere. Consulte o artigo [garantir a conformidade de dispositivos com o System Center Configuration Manager](../../../compliance/understand/ensure-device-compliance.md).  

 **Endpoint Protection**  

 Fornece segurança, proteção antimalware e gestão da Firewall do Windows para os computadores da empresa. Consulte o artigo [Endpoint Protection no System Center Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).  

 **Inventário**  

 Fornece um conjunto de ferramentas para ajudar a identificar e monitorizar ativos:  

-   **Inventário de hardware**: Recolhe informações detalhadas sobre o hardware dos dispositivos na sua empresa. Consulte o artigo [introdução ao inventário de hardware no System Center Configuration Manager](../../../core/clients/manage/inventory/introduction-to-hardware-inventory.md).  

-   **Inventário de software**: Recolhe e comunica informações sobre os ficheiros que estão armazenados nos computadores cliente na sua organização. Consulte o artigo [introdução ao inventário de software no System Center Configuration Manager](../../../core/clients/manage/inventory/introduction-to-software-inventory.md).  

-   **O Asset Intelligence**: Fornece ferramentas para recolher dados de inventário e monitorizar a utilização de licenças de software na sua empresa. Consulte o artigo [introdução Asset intelligence no System Center Configuration Manager](../../../core/clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

**Gestão de dispositivos móveis com o Microsoft Intune**  

 Pode utilizar o Configuration Manager para gerir dispositivos Windows, Windows Phone, Android (incluindo Samsung KNOX Standard) e iOS utilizando o serviço Microsoft Intune através da Internet.

 Apesar de utilizar o serviço Intune, tarefas de gestão são concluídas com a serviço ligação ponto função sistema de sites disponível através da consola do Configuration Manager. Consulte o artigo [gestão de dispositivos móveis (MDM) híbrida com o System Center Configuration Manager e o Microsoft Intune](../../../mdm/understand/hybrid-mobile-device-management.md).  

 **Gestão de dispositivos móveis no local**  

 Inscreve e gere os PCs e dispositivos móveis utilizando no local do Configuration Manager infraestrutura e gestão funcionalidade incorporada nas plataformas de dispositivos (em vez de depender de um cliente de Configuration Manager instalado em separado). Atualmente, suporta a gestão de dispositivos Windows 10 Enterprise e Windows 10 Mobile. Consulte o artigo [gerir dispositivos móveis com a infraestrutura no local no System Center Configuration Manager](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

 **Implementação do sistema operativo**  

 Fornece uma ferramenta para criar imagens do sistema operativo. Em seguida, pode utilizar estas imagens para implementar os sistemas operativos em computadores, utilizando o PXE de arranque ou suportes de dados, tais como um conjunto de CD, DVD ou USB unidades flash. Tenha em atenção que isto aplica-se a computadores que são geridos pelo Configuration Manager, bem como computadores não geridos. Consulte o artigo [introdução à implementação de sistemas operativos no System Center Configuration Manager](../../../osd/understand/introduction-to-operating-system-deployment.md).  

 **Gestão de energia**  

 Fornece um conjunto de ferramentas e recursos que pode utilizar para gerir e monitorizar o consumo de energia dos computadores cliente na empresa. Consulte o artigo [introdução à gestão de energia no System Center Configuration Manager](../../../core/clients/manage/power/introduction-to-power-management.md).  

 **Consultas**  

 Fornece uma ferramenta para obter informações sobre os recursos da hierarquia e informações sobre os dados do inventário e as mensagens de estado. Em seguida, pode utilizar estas informações para relatórios ou para definir coleções de dispositivos ou utilizadores para definições de configuração e implementação de software. Consulte o artigo [introdução às consultas no System Center Configuration Manager](../../../core/servers/manage/introduction-to-queries.md).  

 **Perfis de ligação remota**  

 Fornece um conjunto de ferramentas e recursos para ajudá-lo a criar, implementar e monitorizar as definições de ligação remota para dispositivos na sua organização. Ao implementar estas definições, estará a minimizar o esforço necessário por utilizadores para se ligar aos respetivos computadores na rede da empresa. Consulte o artigo [trabalhar com perfis de ligação remota no System Center Configuration Manager](/sccm/compliance/deploy-use/create-remote-connection-profiles).  

 **Itens de configuração de dados e perfis de utilizador**  

 Dados e perfis de itens de configuração utilizador no Configuration Manager contêm definições que podem gerir o redirecionamento de pastas, ficheiros offline e perfis itinerantes em computadores que executam o Windows 8 e posterior para utilizadores na hierarquia. Consulte o artigo [trabalhar com dados e perfis de itens de configuração utilizador no System Center Configuration Manager](/sccm/compliance/deploy-use/create-user-data-and-profiles-configuration-items).  

 **Controlo remoto**  

 Fornece ferramentas para administrar remotamente computadores cliente a partir da consola do Configuration Manager. Consulte o artigo [introdução ao controlo remoto no System Center Configuration Manager](../../../core/clients/manage/remote-control/introduction-to-remote-control.md).  

 **Relatórios**  

 Fornece um conjunto de ferramentas e recursos que ajudam a utilizam as capacidades avançadas de relatórios do SQL Server Reporting Services a partir da consola do Configuration Manager. Consulte o artigo [introdução aos relatórios no System Center Configuration Manager](../../../core/servers/manage/introduction-to-reporting.md).  

 **Medição de software**  

 Fornece ferramentas para monitorizar e recolher dados de utilização do software de clientes do Configuration Manager. Veja [Monitorizar a utilização da aplicação com a medição de software no System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

 **Atualizações de software**  

 Fornece um conjunto de ferramentas e recursos que podem ajudar a gerir, implementar e monitorizar atualizações de software na empresa. Consulte o artigo [introdução ao software atualizações no System Center Configuration Manager](/sccm/sum/understand/software-updates-introduction).  

